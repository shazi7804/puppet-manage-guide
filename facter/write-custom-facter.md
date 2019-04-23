# 自己寫 facter 來收集資料

除了內建的 facter 以外，還可以自己寫 facter 來抓資料，你可以寫在 [module plugin][puppet-module-plugins] 內。

- `/etc/puppetlabs/code/modules/<module_name>/lib/facter/*.rb`

### 範例

簡單用個範例來取 resolv.conf 裡的 name server。

```
#!/usr/bin/env ruby
# /etc/puppetlabs/code/modules/profile/lib/facter/name_server.rb
Facter.add(:nameserver) do
  setcode do
    # Find all the nameserver values in /etc/resolv.conf
    nameserver_data = Facter::Core::Execution.exec('/bin/cat /etc/resolv.conf | grep nameserver | awk \'{print $2}\'')
    nameserver = nameserver_data.split(" ")
  end
end
```

利用 `Facter.add` 的方式加入新的 facter，這邊是直接用 exec 來跑 shell 取參數，很方便。[更多範例][facter-example]

## 寫了 facter 然後呢 ?

當 facter 成功被 deploy 到 Node 之後，在每次的 deploy，Agent 都會回穿 facter 給 Puppet Server，這時如果你有建立 Puppetdb 就會存入 Puppetdb 裡面。

透過 Dashboard 你可以看到被拋回來的資料

![puppet-facter-dashboard](/assets/images/puppet-facter-dashboard.png)

或是直接透過 [Puppet API][puppet-api] 來取得。

[puppet-module-plugins]: https://puppet.com/docs/puppet/5.3/plugins_in_modules.html
[facter-example]: https://puppet.com/docs/facter/3.6/fact_overview.html
[puppet-api]: https://puppet.com/docs/puppet/5.3/http_api/http_api_index.html
