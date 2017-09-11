# 處理 resource 的先後順序

開始寫 Puppet code 之後總是會遇到有些命令要先執行、後執行等相依性的東西，例如：要先安裝 nginx 後才能處理 service 的啟動，如果先執行 service，就會出現找不到 nginx package 的問題。

## before

`before` 這個可以用來對指定的資源執行之前應用，例如：要設定 `sshd_config` 之前，必須先安裝好 `openssh-server` 這個 package。

```puppet
package { 'openssh-server':
  ensure => present,
  before => File['/etc/ssh/sshd_config'],
}
```

## require

`require` 顧名思義就是一定要指定的資源有執行過，才會應用。

`require` 和 `before` 可以相呼應來做到防呆機制。

```puppet
file { '/etc/ssh/sshd_config':
  ensure  => file,
  mode    => '0600',
  source  => 'puppet:///modules/sshd/sshd_config',
  require => Package['openssh-server'],
}
```

## notify

`notify` 通常用來應用當 `設定檔` 被修改時，要觸發 service restart 的情境。

```puppet
file { '/etc/ssh/sshd_config':
  ensure => file,
  mode   => '0600',
  source => 'puppet:///modules/sshd/sshd_config',
  notify => Service['sshd'],
}
```

## subscribe

`subscribe` 也是拿來用於指定目標的觸發，和 `notify` 相反。

```puppet
service { 'sshd':
  ensure    => running,
  enable    => true,
  subscribe => File['/etc/ssh/sshd_config'],
}
```

`subscribe` 和 `notify` 可以相呼應避免設定檔沒有生效。



## 箭頭符號

如果是在寫 module，通常在 init.pp 會用 `->` 和 `~>` 來處理 class 的順序

```puppet
class nginx (){
  contain nginx::install
  contain nginx::config
  contain nginx::service

  Class['::nginx::install']
  -> Class['::nginx::config']
  ~> Class['::nginx::service']
}
```
`->` 代表左邊的資源會先應用後，再執行右邊資源。
`~>` 代表當左邊資源有異動的時候，觸發右邊資源更新。




