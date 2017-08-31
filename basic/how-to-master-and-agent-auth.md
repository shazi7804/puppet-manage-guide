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

這個 CA 憑證可以是由外部頒發，或是自簽 CA，但通常會直接讓 Puppet 自簽 Internal CA，如果你用的是 Internet CA 則必須停用 Internal CA。