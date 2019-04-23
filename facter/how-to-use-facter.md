# 使用 Facter 取得 Server 資訊

## facter command line

先講簡單的 cli 工具，只要你有裝 Puppet agent，那麼你已經有 `facter` 可以用，沒意外會在 `/opt/puppetlabs/bin/facter` 這邊找到 softlink 的 facter。

直接跑 facter 會出現內建的 variable

```shell
$ facter
aio_agent_version => 1.10.1
augeas => {
  version => "1.4.0"
}
dmi => {
  product => {
    name => "MacBookPro13,2"
    ...
```

會看到一堆系統參數，但是要怎樣取得有用的參數 ?，以 IP 為例

```shell
$ facter networking.ip
10.0.0.101
```

或是目前的 OS 訊息。

```shell
$ facter os
{
  architecture => "x86_64",
  family => "Darwin",
  hardware => "x86_64",
  macosx => {
    build => "17C88",
    product => "Mac OS X",
    version => {
      full => "10.13.2",
      major => "10.13",
      minor => "2"
    }
  },
  name => "Darwin",
  release => {
    full => "17.3.0",
    major => "17",
    minor => "3"
  }
}
```

除了這些以外可以直接看 [Core Facts][core-facts] 更多內建 facter

如果你有 `custom facter` 也可以 include dir 用 `--custom-dir` 指定位置，一般會在 `/opt/puppetlabs/puppet/cache/lib/facter/*.rb` 這邊。

或是直接利用 `FACTERLIB` 這個變數來 include custom-dir

```shell
$ export FACTERLIB=/opt/puppetlabs/puppet/cache/lib/facter
```

[core-facts]: https://puppet.com/docs/facter/3.6/core_facts.html
