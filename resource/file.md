# file

file 可以用來管理檔案、目錄、檔案內容、以及權限，還有 symlink。

在 Puppet 裡使用 file 就跟吃飯一樣常常接觸，畢竟這是一套 Configuration 組態管理系統嘛！

## 基本範例

- 建立一個 Hello world !!

```puppet
file { '/tmp/bar':
  ensure  => file,
  mode    => '0644',
  owner   => 'root',
  group   => 'root',
  content => 'hello world!!'
}
```

實際上在 instances 會產生一個 /tmp/bar 的檔案，並且：

```shell
$ cat /tmp/bar
hello world!!
```

檔案權限的部份會變成這樣：

```shell
$ ll /tmp/bar
-rw-r--r-- 1 root root 13 Oct 24 11:45 bar
```

- 建立樹狀結構目錄

在 Linux 你可以用 `mkdir -p` 搞定，但是 Puppet 你要一層一層建立，就像這樣：

```puppet
file { ['/tmp/bar', '/tmp/bar/foo']:
  ensure => directory,
}
```

或是用變數：

```puppet
$sample_dirs = ['/tmp/bar', '/tmp/bar/foo']
file { $sample_dirs:
  ensure => directory,
}
```

- 處理檔案符號連結 (symlink)

```puppet
file { '/tmp/link-to-motd':
  ensure => link,
  target => '/etc/motd', 
}
```


## 情境範例：

- 用 default 來處理差不多的 resource

在實際管理的時候一定會遇到要同時處理很多 file，但是彼此又很像，只有一點點差異，那麼就可以利用 `default` 一次處理多個差不多的 resoure。

```puppet
file {
  default:
    ensure => file,
    mode   => '0644',
    owner  => 'root',
    group  => 'root',
  ;
  '/etc/hosts.allow':
    content => 'sshd:192.168.1.10',
  ;
  '/etc/hosts.deny':
    content => 'sshd:all:deny',
}
```

這樣就一次搞定 hosts.allow 和 hosts.deny 這兩個檔案。

file 多數用在你想 `完全掌控` 檔案或目錄的情況下使用，如果你只想針對內容的某一段修改，則應該使用 augeas 或是 file_line



















