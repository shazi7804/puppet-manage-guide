# Visual Studio Code plugin for Puppet

這邊先說沒有廣告的嫌疑，單純是因為作者用的是 Visual Studio Code 作為 Puppet 的編輯器，所以介紹一下在 Visual Studio Code 上怎麼更快速的開發 Puppet。


![puppet-and-vscode](/assets/images/puppet-and-vscode.png)

我主推在 VSCode 上就有的 Puppet 官方 [extension][puppet-vscode-extension-official]，雖然目前還在 preview 階段 (正式版本為 1.0)，但已經有許多功能支援，包含：

- 自動完成
- puppet-lint 測試
- node graph

在 0.x 的 preview 版本中，必須要安裝 `puppet agent`，正式版本則為 [`Puppet Development Kit` (PDK)][pdk]


在 MacOS 的環境下按 command + shift + P 可以看到所有 plugin 支援的功能

![vscode-ext-feature-overview](/assets/images/vscode-ext-feature-overview.png)


自動完成的功能讓開發速度大幅提昇 !! 但目前針對 `highlight` 的部份沒有太多顏色

如果你覺得 `highlight` 遠比上述功能還要重要的話，那麼建議可以安裝 [puppet/marcus][puppet-vscode-extension-marcus]，若是與官方 extension 共用則其中一個會無法使用。


[puppet-vscode-extension-marcus]: https://marketplace.visualstudio.com/items?itemName=bitzl.vscode-puppet
[pdk]: https://puppet.com/blog/develop-modules-faster-new-puppet-development-kit
[puppet-node-graph]: https://puppet.com/blog/visualize-your-infrastructure-models
[puppet-vscode-extension-official]: https://puppet.com/blog/announcing-puppet-visual-studio-code