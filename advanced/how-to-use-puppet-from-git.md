# 讓 Puppet 進 Git 版控

## 為什麼要用 Git

Puppet 有個很大的特點是 Infrastructure as code




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

從這個 Puppet skeleton 