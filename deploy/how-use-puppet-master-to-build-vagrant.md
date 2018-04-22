# 如何使用 Puppet Master 佈署 Vagrant

## 什麼是 Vagrant ?

[`HashiCorp`][hashicorp] 出品的 ~~HashiCorp 產品必屬佳作~~ `Vagrant`，簡單介紹一下 `Vagrant` 是一款用於構建及配置虛擬開發環境的軟體，基於 `Ruby` 開發，主要使用 `Oracle` 的開源 `VirtualBox` 虛擬化系統。

`Vagrant` 支援 Chef、Puppet、Ansible .. 等快速的方式構建環境。

---

## Requires

在開始之前，要先安裝 `Vagrant` 和 `Virtualbox`。

---

### Virtualbox 安裝

`Virtualbox` 的官方 [Download](https://www.virtualbox.org/wiki/Downloads) 找到適合自己的環境安裝。

### Vagrent 安裝

`Vagrant` 的安裝也很簡單，以 `Ubuntu` 為例

```bash
$ wget https://releases.hashicorp.com/vagrant/2.0.4/vagrant_2.0.4_x86_64.deb
$ dpkg -i vagrant_2.0.4_x86_64.deb
$ vagrant version
Installed Version: 2.0.4
Latest Version: 2.0.4
```

## 用 Puppet Master 來 build Vagrant

使用 `Puppet Master` 的話就單純許多，你只要有 `puppet agent` 就可以搞定

```
├── Vagrantfile
└── scripts
    └── puppet_install.sh
```

- `Vagrantfile` 用來定義這個 `Vagrent box` 要做的主要設定檔

假設環境：
  - Puppet Server：puppet.master.com
  - Puppet Node：puppet.node.com

```
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.provision "shell", path: 'scripts/puppet_install.sh'

  config.vm.provision "puppet_server" do |puppet|
    puppet.puppet_server = 'puppet.master.com'
    puppet.puppet_node = 'puppet.node.com'
    puppet.options = "--verbose --debug"
  end

  config.vm.network "forwarded_port", guest: 80, host: 8080, protocol: "tcp"
  config.vm.network "forwarded_port", guest: 443, host: 8443, protocol: "tcp"
end
```

然後 puppet_install.sh 裡面寫 puppet-agent 的安裝方式

```bash
#!/bin/bash
wget https://apt.puppetlabs.com/puppet5-release-xenial.deb
sudo dpkg -i puppet5-release-xenial.deb
sudo apt update && sudo apt install puppet-agent -y
sudo tee /etc/puppetlabs/puppet/puppet.conf <<EOF
[main]
  environment = production
EOF
```

如果該 node 已經有授權過的話則可以用 `client_cert_path` 和 `client_private_key_path` 來指定 cert / key。

---

## Build

```bash
$ vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'ubuntu/xenial64'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'ubuntu/xenial64' is up to date...
...
...
==> default: Notice: Applied catalog in 168.25 seconds
```

完成後就用 `vagrant ssh` 來登入虛擬機吧！

[hashicorp]: https://hashicorp.com
[librarian-puppet]: http://librarian-puppet.com
[composer]: https://getcomposer.org/
[r10k]: https://github.com/puppetlabs/r10k