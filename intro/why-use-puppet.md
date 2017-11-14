# 為什麼要用 Puppet

減少你的工作時間。

![puppet-speed](/assets/images/puppet-speed.png)

自動化的可靠性、重複性並且可以輕鬆的複製設定到多台機器。

![puppet-file-checkmark](/assets/images/puppet-file-checkmark.png)

你可以用 Git 來管理 Puppet 來做到版本控管及透明化。

![puppet-audtability](/assets/images/puppet-audtability.png)


你可以將所有的 Configuration 都放在 Puppet Server 上，若是遇到相同的設定可以直接分配設定檔給所有的 Server，只要修改對應的參數就好了。

![puppet-capabilities](/assets/images/capabilities.png)

按照 Puppet 官方說法：全球有 37,000 家企業使用 Puppet 開源專案，其中財星 Top 100 的企業中有 75% 使用 Puppet，由此可以 Puppet 能適用於規模夠大的環境下佈署。 

![puppet-fortune-100-use-puppet](/assets/images/fortune-100-use-puppet.png)


## Puppet vs. Ansible

"ssh in a for loop is not a solution" – Luke Kanies, Puppet developer

最明顯的差別就是 Ansible 採用的是 ssh 的方式來 `push`，而 Puppet 是依靠 agent 來 `pull`。

而官方強調 Ansible 是 by task 類型的工具，適合完成單一性任務，Puppet 則強調在於 `持續管理` 的概念並且能有效的 scale 架構，比起 Ansible，Puppet 針對大型架構也能有效的管理。

## Puppet vs. Chef

Puppet 和 Chef 彼此相似，在選擇上開發者多數喜愛 Chef，而系統人員偏愛 Puppet / Ansible，這是由於使用 Chef 需要比較多的 Ruby 經驗，開發者容易上手，系統人員反之。

Puppet 和 Chef 之間存在著微妙的關係，有許多企業會同時使用 Puppet 和 Chef 彌補彼此的缺點。 




