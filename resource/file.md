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

