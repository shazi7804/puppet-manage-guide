# 安裝 Master Server

## 環境

先定義好 Puppet Master 的環境：

  - Operating system : Ubuntu 16.04

  - IP Address : 192.168.10.10

  - HostName/Domain : master.puppet.com

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

  從官方 [repository][^1] 取得 Puppet package。

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

1. 修改 Puppet master 的主要設定檔 puppet.conf

  ```shell
  sudo vim /etc/puppetlabs/puppet/puppet.conf
  
  [main]
    vardir = /opt/puppetlabs/server/data/puppetserver
    logdir = /var/log/puppetlabs/puppetserver
    rundir = /var/run/puppetlabs/puppetserver
    pidfile = /var/run/puppetlabs/puppetserver/puppetserver.pid
    codedir = /etc/puppetlabs/code
    certname = master.puppet.com
    server = master.puppet.com
    environment = production
    runinterval = 1h
    strict_variables = true
   
  [master]
    dns_alt_names = master.puppet.com
    ssl_client_header = SSL_CLIENT_S_DN
    ssl_client_verify_header = SSL_CLIENT_VERIFY
  ```






[^1]: https://docs.puppet.com/puppet/5.1/puppet_platform.html "About Puppet Platform and its packages"














