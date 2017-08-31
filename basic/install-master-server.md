# 安裝 Master Server

## 環境

先定義好 Puppet master 和 agent 的環境：

  - Operating system: Ubuntu 16.04

  - Master
  
    - IP Address: 192.168.10.10

    - Domain : master.puppet.com
  
  - Agent
    
    - IP Address: 192.168.10.11

    - Domain : agent.puppet.com


## 安裝    
    
1. Puppet 針對所有的主機皆須定義為 Domain。

  在 Puppet 官方有提到：
    
  > Name resolution: Every node must have a unique hostname. Forward and reverse DNS must both be configured correctly. (Instructions for configuring DNS are beyond the scope of this guide. If your site lacks DNS, you must write an /etc/hosts file on each node.)
    
  > Note: The default Puppet master hostname is puppet. Your agent nodes can be ready sooner if this hostname resolves to your Puppet master.
    
  如果你還沒有定義好 Puppet Master / Agent 的 Domain，可以先設定在 hosts。
    
  ```shell
  $ cat /etc/hosts
  192.168.10.10 master.puppet.com
  192.168.10.11 agent.puppet.com
  ```

1. Puppet Master 必須準確校時。

  ```shell
  $ sudo ntpdate time.stdtime.gov.tw
  $ sudo timedatectl set-timezone Asia/Taipei
  ```

1. 安裝 Puppet Master

  從官方 [repository][puppet-platform] 取得 Puppet package。

  ```shell
  $ wget https://apt.puppetlabs.com/puppet5-release-xenial.deb
  $ sudo dpkg -i puppet5-release-xenial.deb
  $ sudo apt-get update
  $ sudo apt-get install puppetserver
  ```
  
1. Puppet master Memory 調整，預設為 2G

  ```shell
  $ sudo vim /etc/default/puppetserver
  JAVA_ARGS="-Xms2g -Xmx2g"
  ```

1. 修改 Puppet 的主要設定檔 [puppet.conf][puppet-conf]

  ```shell
  sudo vim /etc/puppetlabs/puppet/puppet.conf
  
  [main]
    certname = master.puppet.com
  ```

  certname 是用來生成這台 node 憑證使用，Puppet 之間的溝通是使用 SSL 交握。
  

1. 嘗試啟動 Puppet master

  ```shell
  $ sudo service puppetserver start
  $ sudo systemctl enable puppetserver
  ```

1. 應該要 listen 8140 port，可以看到是由 Java 啟動，因為 Puppet master 是用 Java 開發。

  ```shell
  $ ss -tunlp | grep 8140
  tcp  LISTEN  0  50  :::8140  :::*  users  (("java",pid=27866,fd=32))
  ```

1. 初始化 Puppet server 的 ca 憑證，如果沒有執行 Agent 會無法透過 ca 來產生 Agent 的 certname。

  ```shell
  $ sudo puppet cert list
  ```

1. 如果你有開啟 Firewall 記得 allow 8140

  ```shell
  $ sudo ufw allow 8140
  ```

[puppet-platform]: https://docs.puppet.com/puppet/5.1/puppet_platform.html

[puppet-conf]: https://docs.puppet.com/puppet/5.0/configuration.html













