# [beaker-rspec][beaker-rspec]

是 `rspec` 跟 [`beaker`][beaker] 的橋樑，同時也集成 [`serverspec`][serverspec]

## [beaker][beaker]

`acceptance test` 驗收測試是所有測試中的最後一環，對於 Puppet 中非常重要，因為 Puppet 提供多種不同 OS 環境的支援，但 Unit Test 僅能測試 function，但不同的環境上仍有疑慮，`beaker` 可以讓你在多個虛擬環境>中執行命令來進行 `puppet` 實際的佈署。

`gem` 安裝 `beaker`

```
$ gem install beaker
```

## [serverspec][serverspec]

`serverspec` 則是用來啟動虛擬環境，支援 `Docker` 和 `Vagrant` 來處理虛擬環境。

`gem` 安裝 `serverspec`

```
$ gem install serverspec
```

[beaker]: https://github.com/puppetlabs/beaker/
[serverspec]: http://serverspec.org/
[beaker-rspec]: https://github.com/puppetlabs/beaker-rspec/
