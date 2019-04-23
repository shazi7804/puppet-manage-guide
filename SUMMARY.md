# Summary

- [前言](intro/README.md)
    - [什麼是 Puppet](intro/what-is-puppet.md)
    - [為什麼要用 Puppet](intro/why-use-puppet.md)
    
- [基礎概念](basic/README.md)
    - [架構](basic/architecture.md)
    - [版本大事紀](basic/release-history.md)
    - [安裝 Master Server](basic/install-master-server.md)
    - 安裝 Puppet Agent
        - [Ubuntu 16.04](basic/install-puppet-agent/ubuntu-install-puppet-agent.md)
        - [CentOS 6/7](basic/install-puppet-agent/centos-install-puppet-agent.md)

    - [Master 和 Agent 的認證關係](basic/how-to-master-and-agent-auth.md)
        - [實作 policy-based autosigning](basic/auth/how-to-policy-based-autoscaling.md)
    - [第一個 manifests 設定](basic/how-to-write-manifests.md)
    - [第一個 module 設定](basic/how-to-write-module.md)
    - [處理 Resource 之間的順序](basic/how-to-use-resource-older.md)
    - [Puppet 內建的檔案系統](basic/puppet-file-system.md)
    - [怎麼使用 Hiera data](basic/how-to-use-hiera-data.md)

- [Resource 特別介紹篇](resource/README.md)
    - [file 檔案與目錄](resource/file.md)
    - [package 安裝套件](resource/package.md)
    - [service 服務控制](resource/service.md)

- [Function 特別介紹篇](function/README.md)
    - [defined 判斷資源是否存在](function/defined.md)

- [Facter](facter/README.md)
    - [使用 Facter 取得 Server 資訊](facter/how-to-use-facter.md)
    - [自定義 facter](facter/write-custom-facter.md)

- [進階管理](advanced/README.md)
    - [效能調教](advanced/performance.md)
    - [VSCode plugin for Puppet](advanced/vscode-puppet-plugin.md)
    - [Role and Profile pattern 的管理方式](advanced/role-and-profile-pattern.md)
    - [怎麼加密 Hiera data](advanced/how-to-encrypt-hiera-data.md)
    - [用 templates 來處理檔案內容](advanced/how-to-use-templates.md)
    - [讓 Puppet 進 git 版控](advanced/how-to-use-puppet-from-git.md)
    - [備份與還原](advanced/backup-and-restore.md)

- [Bolt](bolt/README.md)
    - [介紹 Bolt](bolt/intro.md)

- [WorkShop](workshop/README.md)
    - [實作 Linux 基礎環境設定](workshop/build-linux-base.md)
    - [實作 LAMP](workshop/build-lamp.md)
    - [實作 Nginx 和 Nodejs](workshop/build-nginx-and-nodejs.md)
    - [實作 Facter 取得 OpenSSL 版本](workshop/facter-openssl.md)

- [測試](test/README.md)
    - [puppet-lint](test/puppet-lint.md)
    - [rspec-puppet](test/rspec-puppet.md)
    - [beaker-rspec](test/beaker-rspec.md)

- [佈署到其他平台](deploy/README.md)
    - [如何使用 Puppet 佈署 Docker](deploy/how-to-build-docker-container.md)
    - [如何使用 Puppet + Packer 佈署 AWS AMI](deploy/how-to-build-aws-ami.md)
    - [如何使用 Puppet Apply 佈署 Vagrant](deploy/how-use-puppet-apply-to-build-vagrant.md)
    - [如何使用 Puppet Master 佈署 Vagrant](deploy/how-use-puppet-master-to-build-vagrant.md)

- [疑難雜症Q&A](qa/README.md)
