# Puppet 管理者指南

Puppet 是一個基於實現 infrastructure as a code 的組態管理工具，與其相同性質的有 Ansible、SaltStack、Chef 等工具，Puppet 的特性是幾乎涵蓋所有的 OS System，並且適合在大量佈署的環境下使用。

## Summary
1. [前言](01.intro.md)
    1. [為什麼要用 Puppet](01-1.why-use-puppet.md)
1. [基礎](02.basic.md)
    1. [安裝 Master Server](02-1.install-master-server.md)
    1. [安裝 Puppet Agent ](02-2.install-puppet-agent.md)
    1. [Master 和 Agent 的認證關係](02-3.how-to-master-and-agent-trust.md)
        1. [實作 policy-based autosigning](02-4.how-to-policy-based-autoscaling.md)
    1. [第一個 manifests 設定檔](02-5.how-to-write-manifests.md)
    1. [利用 module 簡化 manifests 的設定檔](02-6.how-to-write-module.md)
    1. [對於 node 的管理](02-7.how-to-manage-node.md)
1. [進階](03.advanced.md)
    1. [Role and Profile pattern 的管理方式](03-1.how-to-use-role-and-profile-pattern-manage.md)

## 勘誤

請來信 _shazi7804 (at) gmail.com_ 或至 [Github][shazi7804/puppet-manage-guide] 推送 Pull Request 和 Issues。


[shazi7804/puppet-manage-guide]: https://github.com/shazi7804/puppet-manage-guide
