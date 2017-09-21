# 測試

既然 Puppet 手握整個 infrastructure 的生殺大權，那麼 Puppet 的設定會是一整間公司的命脈，萬一寫錯某個設定可能就會造成專案無法運作，嚴重甚至整間公司都發生問題。

事前的測試將會是預防發生錯誤最好的方法，由於是 Code，所以我們可以用測試工具來寫 Test case，目前應用到的主流工具：

- [puppet-lint][puppet-lint]：測試 manifests 最好的自動化工具，內建 Puppet 的規則和 Coding style 項目。
- [rspec-puppet][rspec-puppet]：Unit test 最推薦的測試工具。
- [beaker][beaker]：用於驗收測試，你可以藉由 Docker/Vagrant 來測試你對於多平台的相容性。
- [beaker-rspec][beaker-rspec]：是 rspec 跟 beaker 的橋樑，同時也集成 [serverspec][serverspec]

[puppet-lint]: http://puppet-lint.com/
[rspec-puppet]: http://rspec-puppet.com/
[beaker]: https://github.com/puppetlabs/beaker/
[beaker-rspec]: https://github.com/puppetlabs/beaker-rspec/
[serverspec]: http://serverspec.org/