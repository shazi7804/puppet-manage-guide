# 架構

一開始我們先了解 Puppet 在整個運行中是如何架構出整個 configure system。

## Catalogs

catalog 是記錄每個受管 Node 的資料，在 Puppet 中又分為兩種：

- Compile a catalog
- Apply the catalog

前者被編譯過，在 Puppet Master / Agent 時傳遞資料時出現，後者則是明碼在 Puppet Master / Agent 各自的目錄內。

## Master / Agent

![puppetmaster-agent](/assets/images/puppetmaster-agent.png)

基於 `pull-based` 的架構

Puppet 的 Master / Agent 架構通常適用於有規模的環境佈署，由 Puppet Master 提供 configuration，在每台要被佈署的 Node 安裝 Puppet agent 向 Master 獲取 configuration。

Puppet Master 通常由 N + 1 台 Puppet Server 構成，必須要能夠承受所有的 Puppet agent 訪問，而 Puppet agent 通常透過 service 運行或是 cron 來定期向 Puppet Master 更新 catalog。

Agent 透過 catalog 更新完畢後，將 report 回傳給 Puppet Master。

## Masterless

基於 `push-based` 的架構

無 Master 又稱獨立佈署的架構，透過 `Puppet apply` 進行單機佈署的方式達成。

通常適用於數量少的環境，或是建立 image 時使用。


一般狀況來說會採用 Master / Agent 的架構使用，但你也可以兩者並用適用不同狀況。

## Tasks and Plans

Puppet tasks and plans 是 puppet 推出基於 `push-based` 的一次性的臨時佈署，與 Ansible 的方式相似，彌補 Puppet 長期以來使用 `pull-based` 必須等待 deploy time 的缺點。

可以使用 [Bolt](https://github.com/puppetlabs/bolt) 開源專案或是企業版的 Puppet Enterprise Task Management (available in Puppet Enterprise 2017.3) 來實現 Tasks and Plans。

[puppet-tasks-and-plans]: https://puppet.com/blog/easily-automate-ad-hoc-work-new-puppet-tasks
