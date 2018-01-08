# [rspec-puppet][rspec-puppet]

`Unit test` 最推薦的測試工具，這算是單機測試中最重要的一環，

`gem` 安裝 `rspec-puppet`

```
$ gem install rspec-puppet
```

範例 rspec-puppet 的作法

```
# role_spec.rb
require 'spec_helper'

describe 'role::base' do
  context 'with defaults for all parameters' do
    let(:facts) { global_facts }
    it do
      should contain_class('profile::base')
      should contain_class('profile::users')
    end
  end
end
```

這個範例會測試有 include 以下 class

- include profile::base
- include profile::user