# service

service 用來管理 daemon，舉 Ubuntu / CentOS 來說就是 `service` / `systemd` 一樣支援不同的 [provider][service-provider] 

- 啟動 Apache2

```puppet
service { 'apache2':
  ensure => running,
  enable => true,
}
```

eunsure 定義這個服務的狀態，enable 則是定義在 on boot 的時候的狀態。

[service-provider]: https://puppet.com/docs/puppet/5.3/types/service.html#service-attribute-provider
