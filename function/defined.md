# defined 判斷資源是否存在

用到 defined 最常遇到的應該是 Class 重複宣告，Resource 只要有正確的命名比較不會遇到衝突，簡單寫幾個範例 defined 的用法：

判斷 elastic_sack 不存在才宣告 Class['elastic_stack']

```puppet
if ! defined(Class['elastic_stack::repo']) {
  class { 'elastic_stack::repo':
    version => 6,
  }
}
```

拿來判斷 Resource 也可以

```puppet
if ! defined(Package['apache2']) {
    package { 'apache2':
        ensure => present,
    }
}
```

拿來判斷變數也很容易

```puppet
defined('$name')
```

用 defined 來回應 true / false

```puppet
# Assign values to $is_defined_before and $is_defined_after using identical `defined`
# functions.

$is_defined_before = defined(File['/tmp/file'])

file { "/tmp/file":
  ensure => present,
}

$is_defined_after = defined(File['/tmp/file'])

# $is_defined_before returns false, but $is_defined_after returns true.
```

如果用來判斷多個 Resource ... 全部符合才會 true。

```puppet
file { "/tmp/file1": ensure => file, }

defined(File['/tmp/file1'],File['/tmp/file2'],File['/tmp/file3'])
# ... but this returns `false`.
```

或是更詳細的比對 Type 和 Resource

```puppet
defined(Type[Resource['file','/tmp/file2']])
defined(Resource['file','/tmp/file2'])
```



