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
    
  ```bash
  $ cat /etc/hosts
  192.168.10.10 master.puppet.com
  192.168.10.11 agent.puppet.com
  ```

1. Puppet Master 必須準確校時。

  ```bash
  $ sudo ntpdate time.stdtime.gov.tw
  $ sudo timedatectl set-timezone Asia/Taipei
  ```

1. 安裝 Puppet Master

  從官方 [repository][^1] 取得 Puppet package。

  ```bash
  $ wget https://apt.puppetlabs.com/puppet5-release-xenial.deb
  $ sudo dpkg -i puppet5-release-xenial.deb
  $ sudo apt-get update
  $ sudo apt-get install puppetserver
  ```
  

[^1]: https://docs.puppet.com/puppet/5.1/puppet_platform.html "About Puppet Platform and its packages"














