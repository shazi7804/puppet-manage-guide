# 第一個 module 設定

Module 是 Puppet 管理中非常重要的一環，利用已經編寫好的 module 在 manifests 就不需要在打上落落長的設定檔。

## 從哪裡找 Module

### 從 Puppetforge 獲取 module

[Puppetforge][puppetforge] 是 Puppet 提供的一個 module 管理平台，你可以透過這個平台來找到各種你想要的 Puppet module。

### 從 Github 獲取 module

除了 Puppetforge 以外，最多資源的就是在 [Github][github]，就因為資源太多更需要慎選。

## 如何挑選 Module

由於 Puppet 已經算是很成熟的組態管理工具，所以 module 也是琳琅滿目，但是要怎麼去篩選適合的 module 就是一個很重要的課題。

### 從維護者挑選

- Puppet 官方維護的 Puppetlabs

[Puppetlabs][puppetlabs] 是官方提供的模組，不見得會是最新，但是會是最穩定的 module，基本上沒有太多問題，而且也沒有 EOL 的問題，而且 Test case 也算是最完整的。

- Github 維護的 voxpupuli

[voxpupuli][voxpupuli] 是由 Github 內部維護的 module，也算是穩定中可選的 module，有許多由 Puppetlabs 官方維護的 module 會直接移轉給 voxpupuli 進行維護，例如 [puppet-nginx][puppet-nginx]，算是除了 Puppetlabs 的第三方授權。

- 由套件本身官方維護的 module

各種套件本身會維護自己的 Puppet module，例如 [Elastic][elastic] 就維護 puppet-elasticsearch、puppet-kibana、puppet-logstash

### 適用自己環境

 - OS platform
 - Features
 - Puppet version

除了以上建議的 module 來源以外，除非這個 module 你有能力做後續的維護，否則都不建議使用。


## 動手寫 Module

如果覺得線上的所有 module 都不符合你的需求，可以自己動手寫，在這篇會以基礎的 module 方向去寫。

你可以把 module 放在以下位置：

 - /etc/puppetlabs/code/environments/production/modules
 - /etc/puppetlabs/code/modules
 - /opt/puppetlabs/puppet/modules

### 基礎 module 檔案結構

以一個 apache module 為例，我會需要產生以下這些檔案結構

```
$ tree /etc/puppetlabs/code/modules/apache
├── files
|   └── default.conf
└── manifests
    ├── init.pp
    ├── install.pp
    ├── config.pp
    ├── service.pp
```

### module 的 manifests

init.pp 是預設被讀取的檔案，通常用來定義變數、引用 class。

```puppet
# apache/manifests/init.pp
class apache (
  String $package_name      = 'apache2',
  String $package_ensure    = 'installed',
  String $service_name      = 'apache2',
  String $service_ensure    = 'running',
  String $default_site_conf = '/etc/apache2/sitesenabled/default.conf',
  String $run_user          = 'www-data',
){
  contain apache::install
  contain apache::config
  contain apache::service

  Class['::apache::install']
  -> Class['::apache::config']
  ~> Class['::apache::service']
}
```

install.pp 用來定義如何安裝 package。

```puppet
class apache::install inherits apache {
  package { $apache::package_name:
    ensure => $apache::package_ensure
  }
}
```

service.pp 用來處理服務

```puppet
class apache::service inherits apache {
  service { $apache::service_name:
    ensure    => $apache::service_ensure,
    subscribe => Package['apache'],
    require   => Class['apache::install']
  }
}
```

config.pp 用來處理設定檔

```puppet
class apache::config inherits apache {
  file { $apache::default_site_conf:
    ensure => file,
    owner  => $apache::run_user,
    source => "puppet:///modules/${module_name}/default.conf"
  }
}
```

## 怎麼引用 module

要引用 module 只需要使用 include 就可以把已經寫好的 apache module 引用近來

```puppet
node default {
  include ::apache
}
```
只要三行、三行、三行 !! 就完成佈署安裝 apache 了

這樣 Puppet code 就簡潔許多了，恭喜你已經學會了基本的 module 寫法，可以再往進階 module 前進。

[github]: https://github.com
[puppetforge]: https://forge.puppet.com/
[puppetlabs]: https://github.com/puppetlabs/
[voxpupuli]: https://github.com/voxpupuli
[puppet-nginx]: https://github.com/voxpupuli/puppet-nginx
[elastic]: https://github.com/elastic