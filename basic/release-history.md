# 版本大事紀

作者也沒有接觸 Puppet 很久，但是在使用 Puppet 的過程中經歷了幾個大版本更新，針對目前還有在 repository 存在的版本進行介紹，也避免安裝錯版本。

主要的版本分為 3、4、5 這幾個大版本來介紹。

## Puppet 3

這個版本是我剛接觸 Puppet 時的起手式，在 Puppet 3 的資源應該算是最多的，在許多官方 module 都還是以 Puppet 3 的形式在寫，該有的功能都有，算是入門版本。

- repository：
  - puppetlabs-release-el-6.noarch.rpm (RedHat)
  - puppet-release-xenial.deb (Debian)

## Puppet 4

Puppet 4 在「[Welcome to Puppet Collections][welcome-to-puppet-collections]」有不錯的介紹，這個版本為 Puppet Collections (又名 PC1)，在這個版本中強調 Hiera、Facter、Augeas 的使用，也優化在 Puppet 3 使用的 params.pp 儲存參數的方法，非常建議至少要使用 Puppet 4 以上的版本。

- repository：
  - puppetlabs-release-pc1-el-6.noarch.rpm (RedHat)
  - puppetlabs-release-pc1-xenial.deb (Debian)
  
## Puppet 5 (stable)

在 5 這個版本有點像是重新整理 Puppet 的感覺，把該升級的都升上來，本來在 Puppet 4 準備被棄用的功能正式移除，大多數的 Release 強調在於優化效能與功能，如果你對於效能有瓶頸，可以嘗試升級到 5 提供的 `retry` 這類型的參數。

- repository：
  - puppet5-release-el-6.noarch.rpm (RedHat)
  - puppet5-release-xenial.deb (Debian)

[welcome-to-puppet-collections]:https://puppet.com/blog/welcome-to-puppet-collections