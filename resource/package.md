# package

package 是用來管理套件的 resource，像是 apt / yum，也支援 rpm / dpkg 這類型的工具，針對不同的平台有各自的 [provider][package-provider]。

## 基本範例

最簡單的安裝 apache2 方式：

```puppet
package { 'apache2':
  ensure => installed,
}
```






[package-provider]: https://puppet.com/docs/puppet/5.3/types/package.html#package-attribute-provider