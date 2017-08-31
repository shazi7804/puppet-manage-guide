# MASTER 和 AGENT 的認證關係

Puppet Master 和 Agent 是使用 CA 憑證來產生 SSL Cert 進行溝通

```
               +------------------------+
               |                        |
               |  Root self-signed CA   |
               |                        |
               +------+----------+------+
                      |          |
           +----------+          +------------+
           |                                  |
           v                                  v
  +-----------------+                +----------------+
  |                 |                |                |
  | Server SSL Cert |                | Agent SSL Cert |
  |                 |                |                |
  +-----------------+                +----------------+
```

[CA 憑證][^1]可以是由外部頒發，或是自簽 CA，但通常會直接讓 Puppet 自簽 Internal CA，如果你用的是 Internet CA 則必須停用 Internal CA。

整個認證的交易就和我們一般 HTTP 的 SSL 申請狀況相同，Agent 就像是一般企業客戶端，而 Master 就是 CA 憑證中心。

![](/assets/puppet-master-slave-communication.jpg)

1. 由 Agent 向 Master 發起憑證簽署需求 (CSR)
1. 由 Master 依照 Agent 提供的 CSR 簽署一份 SSL 憑證提交給 Agent
1. 由 Master 起的 CA 憑證底下皆信任所有簽署過的 CSR
1. Master 的 CA 憑證並不需要外部憑證信任，使用 local CA 信任
1. 整個的 SSL 的交易過程就像是我們向憑證中心交易的過程，只不過 HTTPS 是 trust internet，而 Puppet 是 trust local。





[^1]: https://docs.puppet.com/puppet/5.1/config_ssl_external_ca.html

