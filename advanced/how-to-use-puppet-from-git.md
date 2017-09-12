# 讓 Puppet 進 Git 版控

## 為什麼要用 Git

Puppet 有個很大的特點是 Infrastructure as code




## 怎麼用 Git 管理 Puppet

阿不是就把 Puppet 設定檔都丟上 Git 嗎 ?

事實是這樣沒錯 .. XDD

會寫 Puppet 是一個重點，另一個重點是怎麼讓你的 Project 讓人看的懂，通常一間好的公司 Infrastructure 的管理者至少會 N+1 人，這時候你就會面臨到多人管理的議題，一個好的 skeleton 和 flow 都會增加維護者的工作效率。

在現行的 Puppet 版本(5)中，最好的入口點是 `/etc/puppetlabs/code`，這一層位置包含了 environments、modules 和 hiera-data，當然你也可以規劃好自己的架構，然後 CD 才把檔案丟到相對的位置。


如果還是對怎麼用 Git 管理 Puppet 沒有頭緒的話，可以參考我正在使用的 Puppet skeleton。

```
puppet
├── .fixtures.yml     # Test case dependencies module.
├── .librarian        # librarian config.
├── Gemfile           # Puppet dependencies packages.
├── Makefile          # Build automating ci, install, module .. etc.
├── Puppetfile        # Puppet dependencies modules.
├── README.md         # readme file.
├── Rakefile          # Build automating tasks.
├── appspec.yml       # Codedeploy deploy manage.
├── autosign.conf     # Puppet trust domain.
├── data              # Global Hiera data dir.
├── environments      # dev/staging/production node manage.
├── hiera.yaml        # Global Hiera root file.
├── packer            # Packer manage.
├── private           # Private module.
├── profile           # Profile moudle.
├── role              # Role module (include multiple profile)
├── scripts           # Codedeploy script
└── spec              # Test case.
```

從這個 Puppet skeleton 下