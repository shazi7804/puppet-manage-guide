# Ubuntu 16.04 安裝 Puppet agent

## 環境

先定義好 Puppet master 和 agent 的環境：

  - Operating system: Ubuntu 16.04

  - Master
  
    - IP Address: 192.168.10.10

    - Domain : master.puppet.com
  
  - Agent
    
    - IP Address: 192.168.10.11

    - Domain : ubuntu.puppet.com


## 安裝

1. Puppet agent 一樣要定義 Domain，測試可以先寫在 hosts

  ```shell
  $ cat /etc/hosts
  192.168.10.10 master.puppet.com
  192.168.10.11 ubuntu.puppet.com
  ```

1. Puppet agent 必須準確校時。

  ```shell
  $ sudo ntpdate time.stdtime.gov.tw
  $ sudo timedatectl set-timezone Asia/Taipei
  ```

1. 安裝 Puppet agent

  從官方 repository([apt][apt-repository]/[yum][yum-repository]) 取得 Puppet package。

  ```shell
  $ wget https://apt.puppetlabs.com/puppet5-release-xenial.deb
  $ sudo dpkg -i puppet5-release-xenial.deb
  $ sudo apt-get update
  $ sudo apt-get install puppet-agent
  ```

1. 修改 Puppet 的主要設定檔 [puppet.conf][puppet-conf]

  ```shell
  sudo vim /etc/puppetlabs/puppet/puppet.conf
  
  [main]
    certname = ubuntu.puppet.com
    server = master.puppet.com
    environment = dev
    runinterval = 2h  
  ```

  這邊和 master 不同之處在於：
  
    - environment: 這台 node 是屬於哪個環境，所以 Puppet master 可以同時管理 dev/staging/production/pre-production 等環境。

    - runinterval: 當啟動 puppet daemon 時，會按照設定的時間定時和 master 更新 config，預設為 30m。
    
1. 在 Puppet master 先 signin ubuntu.puppet.com 這個 node，否則會無法取得 catalog。

  ```shell
  $ /opt/puppetlabs/bin/puppet cert sign agent.puppet.com
  ```
    
1. 再回到 Agent 使用 `puppet agent -t` 來測試和 master 的溝通

  ```shell
  $ /opt/puppetlabs/bin/puppet agent -t
  ...
  ...
  Info: Applying configuration version '1503680249'
  ```
  出現 Applying configuration version 代表能成功要到 catalog。

1. 啟動 puppet agent daemon 常駐。

  ```shell
  $ sudo systemctl start puppet
  $ sudo systemctl enable puppet
  ```    

當 Puppet master / agent 搞定之後就可以開始寫 manifests(倉儲) 啦 !!


[yum-repository]: https://yum.puppetlabs.com/
[apt-repository]: https://apt.puppetlabs.com/
[puppet-conf]: https://docs.puppet.com/puppet/5.0/configuration.html



