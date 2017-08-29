# Puppet 管理者指南

Puppet 是一個基於實現 infrastructure as a code 的組態管理工具，與其相同性質的有 Ansible、SaltStack、Chef 等工具，Puppet 的特性是幾乎涵蓋所有的 OS System，並且適合在大量佈署的環境下使用。

## Summary
- [前言](intro.md)
    - [為什麼要用 Puppet](intro/why-use-puppet.md)
- [基礎](basic.md)
    - [安裝 Master Server](basic/install-master-server.md)
    - [安裝 Puppet Agent ](basic/install-puppet-agent.md)
    - [Master 和 Agent 的認證關係](basic/how-to-master-and-agent-auth.md)
        - [實作 policy-based autosigning](basic/auth/how-to-policy-based-autoscaling.md)
    - [第一個 manifests 設定檔](basic/how-to-write-manifests.md)
    - [利用 module 簡化 manifests 的設定檔](basic/how-to-write-module.md)
    - [對於 node 的管理](basic/how-to-manage-node.md)
- [進階](advanced.md)
    - [Role and Profile pattern 的管理方式](advanced/how-to-use-role-and-profile-pattern-manage.md)
    

## 勘誤

請來信 _shazi7804 (at) gmail.com_ 或至 [Github][shazi7804/puppet-manage-guide] 推送 Pull Request 和 Issues。


[shazi7804/puppet-manage-guide]: https://github.com/shazi7804/puppet-manage-guide
