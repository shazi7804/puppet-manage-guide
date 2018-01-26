# 實作 Facter 取得 OpenSSL 版本

`Facter` 可以讓你任意取得在 `Node` 環境的任何資訊，藉由練習來取得 OpenSSL 版本。

## 學習項目

- Facter
  - Facter.add
  - Facter.value
  - Facter::Core::Execution.exec

## 實作目標

- 取得 OpenSSL 版本，若有自行 build 的 OpenSSL 版本優先取得。

## Dependencies

NA
  
## LAB Start

這個 LAB 只有一個 `openssl_version.rb` 檔案，我把它放在 Profile 這個 module 使用。

- /etc/puppetlabs/code/modules/profile/lib/facter/openssl_version.rb

```ruby
# Make openssl version available as a fact

Facter.add(:openssl_version) do
  confine { Facter.value(:kernel) != 'windows' }
  confine { Facter.value(:operatingsystem) != 'nexus' }
  setcode do
    if File.exist? '/opt/openssl/bin/openssl'
      Facter::Core::Execution.exec('/opt/openssl/bin/openssl version 2>&1').match(/^OpenSSL (\d+\.\d+\.\d+([a-z]|\-[a-z]+)).*$/)[1]
    else Facter::Util::Resolution.which('openssl')
      Facter::Core::Execution.exec('openssl version 2>&1').match(/^OpenSSL (\d+\.\d+\.\d+([a-z]|\-[a-z]+)).*$/)[1]
    end
  end
end
```

1. 先用 Facter.add 宣告要加入的 facter name `openssl_version`

1. 用 confine 來限制不在 `kernel = windows` 和 `operatingsystem = nexus` 的環境下運行。

1. setcode 內就寫你怎麼抓取 OpenSSL 的版本。

1. 用 if / else 先判斷 `/opt/openssl/bin/openssl` 存在時用 `openssl version` 取得 match 的版本。

當 Agent sync 後可以在 Node 用 facter 來取得 OpenSSL version。

```bash
$ facter --custom-dir=/opt/puppetlabs/puppet/cache/lib/facter openssl_version
1.0.2g
```

或是在 Puppetdb 取得所有 Node 的 OpenSSL 版本。
