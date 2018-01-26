# Bolt 介紹

Bolt 是 Puppet 在 [PuppetConf 2017][PuppetConf-2017] 上發表的其中一個 tool，稱為 Puppet Tasks 的功能，而 Bolt 是 Puppet Tasks 在 open source 的版本。

一直以來 Puppet 都是以 Pull-based 的方式來架構整個 infrastructure，但是每次更新總要等待所有 node 更新完畢，如果要高效率的更新，那你就必須要增加 Node 更新的頻率，那麼你的 Puppet Master 的 Loading 就相對變重。

如果要臨時或一次性的更新，Puppet 在這點就真的做的不好，在 Chef 有 Push Jobs 可以實現，而 Ansible 本身就是 Push-based 所以沒這個問題，這次 Puppet 終於意識到單單 Pull-based 的方式是無法滿足全部的需求。

目前 Bolt 還在 0.x 版本，官方特別聲明在 1.0 之前都是開發階段的版本，不過已經陸陸續續有許多 module 開始支援 task 的功能。


[PuppetConf-2017]: https://puppet.com/community/events/puppetconf/puppetconf-2017 