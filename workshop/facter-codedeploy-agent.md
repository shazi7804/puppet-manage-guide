# 實作 Facter 取得 CodeDeploy Agent 版本

`Facter` 可以讓你任意取得在 `Node` 環境的任何資訊，藉由練習來取得 CodeDeploy Agent 版本。

## 學習項目

- Facter
  - Facter.add
  - Facter.value
  - Facter::Core::Execution.exec
  - File.exists

## 實作目標

- 取得 CodeDeploy Agent 版本。

## Dependencies

NA
  
## LAB Start

判斷 `/opt/codedeploy-agent/.version` 檔案存在時，擷取內容作為版本依據。

- lib/facter/codedeploy_agent_version.rb

```ruby
# Make codedeploy-agent version available as a fact

Facter.add(:codedeploy_agent_version) do
  confine { Facter.value(:kernel) != 'windows' }
  confine { Facter.value(:operatingsystem) != 'nexus' }
  setcode do
    if File.exists?('/opt/codedeploy-agent/.version')
      Facter::Core::Execution.exec('cat /opt/codedeploy-agent/.version 2>&1').match(/^agent_version:\ OFFICIAL_(\d+\.\d+\-\d+\.\d+).*$/)[1]
    end
  end
end
```

1. 先用 Facter.add 宣告要加入的 facter name `codedeploy_agent_version`

1. 用 confine 來限制不在 `kernel = windows` 和 `operatingsystem = nexus` 的環境下運行。

1. setcode 內就寫你怎麼抓取 OpenSSL 的版本。

1. 用 if 加上 File 判斷 `/opt/codedeploy-agent/.version` 存在後用 exec 擷取內容作為版本資訊。

當 Agent sync 後可以在 Node 用 facter 來取得 CodeDeploy Agent version。

```bash
$ facter --custom-dir=/opt/puppetlabs/puppet/cache/lib/facter codedeploy_agent_version
1.0-1.1518
```

或是在 Puppetdb 取得所有 Node 的 CodeDeploy Agent 版本。
