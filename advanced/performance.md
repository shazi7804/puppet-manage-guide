# 效能調教

因為 Puppet 會面對非常大量的環境挑戰，所以 Puppet 的 performance 相對重要，在這個篇幅中會持續不斷的探討 Puppet 效能上的調教

## 版本建議

目前 Puppet 效能比較穩定的版本在於 `Puppet 5`，不管你是新/舊使用者，我都建議你直接使用 Puppet 5 的版本。

## Puppet 參數調整

以下參數可以有效的提昇效能，但是並非所有項目都能符合各種情境，請酌量斟酌使用。

### 停用 report 中的 i18n 翻譯功能提昇效率

利用 `puppet.conf` 中的 `disable_i18n` (Boolean) 參數來降低效能上的開銷 (This setting is false by default in open source Puppet.) [PUP-8009][PUP-8009]

> 此功能於 `puppet 5.3.1` 加入 `disable_i18n`.

### 讓 JRuby 有 Queue 的功能

當大量 Puppet agent 超出 Server 可承受資源時，可利用 `max-queued-requests` 讓 `JRuby` 有 `queue` 的功能，當達到 `queue` 達到上限時 return 503 並且加入 `Retry-After` header 返回給 `agent`。 

> 此功能於 `puppetserver 5.1.0` 和 `puppet 5.3.1` 加入 `max-queued-requests` and `max-retry-delay`.



[PUP-8009]: https://tickets.puppetlabs.com/browse/PUP-8009
