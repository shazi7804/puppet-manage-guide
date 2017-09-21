# 備份與還原

建置完 Puppet 之後最重要的議題就是 maintian，其中一項最基本也最重要的就是災難復原，雖然現在都會架構在 High Availability 的情況下，但還是要有一個備份機制以防萬一。

- 憑證

    - /etc/puppetlabs/puppet/ssl

> 這是 Puppet 最重要的項目，如果沒有憑證所有的 node 都必須重新 trust。

- Configuration
    - /etc/puppetlabs
    - /opt/puppetlabs

> 如果你所有的 Configuration 都在 Git 統一控管的話就不需要備份。

- PuppetDB

> 如果你有使用 report，那存在 DB 的 report 記錄也會是稽核的項目之一。

- Hiera-eyaml Key

> 和憑證列為重要項目之一，所有的 hiera-eyaml 加密字串都必須依靠這把 Key 來做加解密。

上述是使用 Puppet 的重點備份項目，如果你需要重建只要把上述的檔案放回原本相關位置，重啟 Puppet Server 就可以完成還原。