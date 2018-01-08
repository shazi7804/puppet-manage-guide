# [puppet-lint][puppet-lint]

`puppet-lint` 是用來測試 puppet code 的 coding style 套件，內建許多 puppet **應該**要遵守的 `style guide`。

除了檢測以外，`puppet-lint` 還可以直接替你 fix 有格式不正確的部份，自動調整格式或是補上該有的字元。

`puppet-lint` 可以直接用 `gem` 安裝

```
$ gem install puppet-lint
```

拿去餵 module 的路徑就可以測。

```
$ puppet-lint /etc/puppet/modules
```
