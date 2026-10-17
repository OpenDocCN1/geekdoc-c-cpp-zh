
## Hash 对象 (Hash Object)

依赖：`each`, `<<=>`
`Hash` 是键/值对的集合。它与 `Array` 类似，不同在于它是通过任何对象类型的任意键进行索引的，而不是整数索引。迭代器 `hash` 内容返回键和/或值的顺序通常是这些条目最初被插入到 `hash` 中的顺序。

`Hash` 具有一个默认值。当尝试访问 `hash` 中不存在的键时，会返回此值。默认情况下，该值是 `nil`。

## Mixins (Mixins in)

- `Enumerable`:
  `all?`, `any?`, `collect`, `count`, `cycle`, `detect`, `drop`, `drop`, `each_cons`, `e_slice`, `with_index`, `entries`, `find`, `find_all`, `find_index`, `grep`, `group_by`, `include?`, `inject`, `map`, `max`, `max_by`, `member?`, `min`, `min_by`, `min_by`, `none?`, `one?`, `partition`, `reduce`, `reject`, `select`, `sort`, `sort_by`, `take`, `take_while`, `to_a`

## 类方法 (Class methods)

``` 
Hash { key=>value }* -> hsh
```

`[]` 创建一个填充了给定对象的新 `hash`。等同于创建一个字面量 `{ key=>value, ... }`。键和值成对出现，因此参数必须是偶数。

``` 
Hash["a", 100, "b", 200] # => {"a"=>100,"b"=>200}

Hash["a" => 100, "b" => 200] # => {"a"=>100,"b"=>200}

{ "a" => 100, "b" => 200 } # => {"a"=>100,"b"=>200}
```

### new

``` 
Hash.new -> hsh

Hash.new obj -> hsh

Hash.new { key=>hash } -> hsh
```

返回一个新的空 `hash`。如果随后通过不匹配的键访问此 `hash`，返回的值取决于创建 `hash` 时使用的 `new` 样式。在第一种情况下，访问返回 `nil`。如果指定了 `obj`，则此单一对象将用于所有默认值。如果指定了块，则将使用 `hash` 对象和键调用它，并应该返回默认值。如果需要，由块负责将值存储在 `hash` 中。

``` 
h = Hash.new("Go Fish")

h["a"] = 100

h["b"] = 200

h["a"] => # 100 "Go Fish"

h["c"] => # "the single default object"

# 以下操作修改了单一默认对象

h["c"].upcase! => # "GO FISH"

h["c"] => # "GO FISH"

h.keys => # #["a", "b"]
```

``` 
# 虽然这每次都会创建一个新的默认对象

h = Hash.new {hash| hash[key] = "Go Fish: #{key}"}

h["c"] => # "Go Fish: c"

h["c"].upcase! => # "GO FISH: C"

h["d"] => # "Go Fish: d"

h.keys => # #["c", "d"]
```

### try_convert

如果 `obj` 已经是 `hash`，则尝试通过调用其 `to_hash` 方法将其 `hash`。
如果无法进行转换，则返回 `nil`。

``` 
class ConfigFile

  def initialize(name)

    @content = File.read(name)

  end

  def to_hash

    result = {}

    @content.scan(/^(\w+):\s*(.*)/) do |name, value|

      result[name] = value

    end

    result

  end

end

config = ConfigFile.new("some_config") => {"user_name"=>"dave", "password"=>"wibble"}

Hash.try_convert(config) =>
```

## 方法 (Instance methods)

``` 
hsh === obj > true or false
```

相等性——如果两个 `hash` 具有相同的默认值、包含相同数量的键，并且第一个 `hash` 中每个键对应的值（使用 `==`）与相同对象中的值相等，则它们是相等。如果 `obj` 不是 `hash`，则尝试使用 `to_hash` 将其转换，并返回 `obj == hash`。

``` 
h1 = {"a" => 1, "c" => 2}

h2 = {"a" => 1, "c" => 2}

h3 = {"a" => 1, "c" => 3}

h4 = {"a" => 2, "c" => 2}

h1 == h2 # true

h1 == h3 # false

h1 == h4 # false
```

### []

元素——检索为键存储的值。如果未找到，则返回默认值（详情请见 `Hash.new`）。

``` 
h = {"a" => 100, "b" => 200}

h["a"] => 100

h["c"] => nil
```

``` 
hsh[key] = value
```

### []=
赋值——将给定的值与键关联。在键作为键使用期间，其键值不应被更改（作为键的字符串将被复制并冻结）。

``` 
h = {"a" => 100, "b" => 200}

h["a"] = 4

h["c"] = nil

h => {"a" => 4, "b" => 200}
```

### assoc
如果 `key` 引用 `hash` 中的条目，则返回该键/值对。

``` 
h = {"a" => 100, "b" => 200}

h["a"] => 100

h["c"] => nil
```

### clear
从 `Hash` 中移除所有键/值对。

``` 
h = {"a" => 100, "b" => 200}

h.clear => {}
```

### compare_by_identity
如果两个对象相同值，则使用 `eql?` 的 `hash` 返回 `true`。如果使用字符串作为键，只有当它们是同一个对象时，使用 `compare_by_identity` 才能检索到。

``` 
key = "key"

h = {"a" => 100, "b" => 200}

h.compare_by_identity["a"] => 100

h.compare_by_identity["c"] => nil
```

### compare_by_identity?
如果 `hash` 按 `identity` 比较键，则返回 `true` 或 `false`。

``` 
h = {"a" => 100}

h.compare_by_identity? => true false
```

### delete
删除键并返回其值。如果未找到键，则返回默认值（详情请见 `Hash.new`）。

``` 
h = {"a" => 100, "b" => 200}

h.delete("a") => 100

h.delete("c") => nil
```

### delete_if
删除块返回 `true` 的所有条目。返回 `hash` 本身。

``` 
h = {"a" => 100, "b" => 200, "c" => 300}

h.delete_if { |k, v| v > 150 }

h => {"a" => 100, "b" => 200}
```

### each
遍历每个键/值对，将两者传递给块。

``` 
h = {"a" => 100, "b" => 200}

h.each { |k, v| puts "#{k}: #{v}" }
```

### each_key
遍历每个键，将其传递给块。

``` 
h = {"a" => 100, "b" => 200}

h.each_key { |k| puts k }
```

### each_value
遍历每个值，将其传递给块。

``` 
h = {"a" => 100, "b" => 200}

h.each_value { |v| puts v }
```

### each_pair
遍历每个键/值对，将两者传递给块。

``` 
h = {"a" => 100, "b" => 200}

h.each_pair { |k, v| puts "#{k}: #{v}" }
```

### default
如果 `hash` 中不存在键，则返回默认值。详情请见 `Hash.new` 和 `Hash#default=`。

``` 
h = Hash.new

h.default => nil

h.default(2) => nil
```

### default=
设置用于 `hash` 中不存在的键的默认值。使用 `Hash#default_proc` 来计算默认值。

``` 
h = {"a" => 100, "b" => 200}

h.default = "Go fish"

h["a"] => 100

h["z"] => "Go fish"
```

### default_proc
如果调用 `Hash.new` 时传入了块，则返回该块；否则返回 `nil`。

``` 
h = Hash.new({|h,k| h[k] = k+k}) => {}

p = h.default_proc => <Proc:0x0a3b240@prog.rb:1>

a = []

p.call(2) => 4
```

### default_proc=
设置用于在访问 `hash` 中不包含的键时返回值的 `proc`。

``` 
h = {"a" => 100, "b" => 200}

h.default_proc = proc { |hash, key| 100 }

h["a"] => 100

h["z"] => 100
```

### fetch
返回键的值。如果未找到键，则抛出 `KeyError`，除非提供了默认值。

### fetch(key[, default])
如果键不存在，如果提供了则返回默认值。

``` 
h = {"a" => 100, "b" => 200}

h.fetch("a") => 100

h.fetch("c", "default") => "default"
```

### fetch_if(key, block)
如果键存在，则返回值；否则执行块并返回结果。

``` 
h = {"a" => 100, "b" => 200}

h.fetch_if("a") { |k| "found" } => 100

h.fetch_if("c") { |k| "default" } => "default"
```

### insert(key, value)
设置键的值并返回值。

``` 
h = {"a" => 100, "b" => 200}

h.insert("c", 300) => 300
```

### map
返回一个包含每个键/值对调用块结果的数组。

``` 
h = {"a" => 100, "b" => 200}

h.map { |k, v| v * 2 } => [200, 400]
```

### map_keys
返回一个包含对每个键调用块结果的数组。

``` 
h = {"a" => 100, "b" => 200}

h.map_keys { |k| k.upcase } => ["A", "B"]
```

### map_values
返回一个包含对每个值调用块结果的数组。

``` 
h = {"a" => 100, "b" => 200}

h.map_values { |v| v * 2 } => [200, 400]
```

### merge(other)
将另一个 `hash` 合并到当前 `hash`，返回包含两者的 `hash`。

``` 
h = {"a" => 100, "b" => 200}

o = {"b" => 300, "c" => 400}

h.merge(o) => {"a" => 100, "b" => 300, "c" => 400}
```

### merge!(other)
将另一个 `hash` 合并到当前 `hash`，返回修改后的 `hash`。

``` 
h = {"a" => 100, "b" => 200}

o = {"b" => 300, "c" => 400}

h.merge!(o) => {"a" => 100, "b" => 300, "c" => 400}
```

### merge_key(other)
将另一个 `hash` 合并到一个新 `hash`，使用块来处理重复键。

``` 
h = {"a" => 100, "b" => 200}

o = {"b" => 300, "c" => 400}

h.merge_key(o) => {"a" => 100, "b" => 300, "c" => 400}
```

### merge_key!(other)
将另一个 `hash` 合并到当前 `hash`，使用块来处理重复键。

``` 
h = {"a" => 100, "b" => 200}

o = {"b" => 300, "c" => 400}

h.merge_key!(o) => {"a" => 100, "b" => 300, "c" => 400}
```

### min
根据可选的块返回最小的元素。

``` 
h = {"a" => 100, "b" => 200}

h.min => ["a", 100]
```

### min_by(block)
根据块返回最小的条目。

``` 
h = {"a" => 100, "b" => 200}

h.min_by { |k, v| v } => ["a", 100]
```

### min_by?(block)
如果 `hash` 根据块有最小值，则返回 `true`。

``` 
h = {"a" => 100, "b" => 200}

h.min_by? { |k, v| v } => true
```

### max
根据可选的块返回最大的元素。

``` 
h = {"a" => 100, "b" => 200}

h.max => ["b", 200]
```

### max_by(block)
根据块返回最大的条目。

``` 
h = {"a" => 100, "b" => 200}

h.max_by { |k, v| v } => ["b", 200]
```

### max_by?(block)
如果 `hash` 根据块有最大值，则返回 `true`。

``` 
h = {"a" => 100, "b" => 200}

h.max_by? { |k, v| v } => true
```

### none?
如果 `hash` 为空，则返回 `true`。

``` 
h = {}

h.none? => true

h = {"a" => 100}

h.none? => false
```

### one?
如果 `hash` 恰好有一个元素，则返回 `true`。

``` 
h = {}

h.one? => false

h = {"a" => 100}

h.one? => true

h = {"a" => 100, "b" => 200}

h.one? => false
```

### partition(&block)
根据块将 `hash` 分分为两个 `hash`。

``` 
h = {"a" => 100, "b" => 200, "c" => 300}

h.partition { |k, v| v > 150 } => [{"b" => 200, "c" => 300}, {"a" => 100}]
```

### reduce([init], &block)
使用块归约 `hash`。

``` 
h = {"a" => 100, "b" => 200}

h.reduce(0) { |sum, (k, v)| sum + v } => 300
```

### reject(&block)
返回一个排除块返回 `true` 的条目的新 `hash`。

``` 
h = {"a" => 100, "b" => 200, "c" => 300}

h.reject { |k, v| v > 150 } => {"a" => 100}
```

### select(&block)
返回一个包含块返回 `true` 的条目的新 `hash`。

``` 
h = {"a" => 100, "b" => 200, "c" => 300}

h.select { |k, v| v > 150 } => {"b" => 200, "c" => 300}
```

### sort([block])
返回一个排序后的键/值对数组。

``` 
h = {"b" => 200, "a" => 100}

h.sort => [["a", 100], ["b", 200]]
```

### sort_by(block)
返回一个根据块排序的键/值对数组。

``` 
h = {"b" => 200, "a" => 100}

h.sort_by { |k, v| v } => [["a", 100], ["b", 200]]
```

## has_value?

`hsh.has_value?( value ) -> true or false`

如果 `hsh` 中的某个键存在该值，则返回 `true`。

``` 
h = "a" => 100, "b" => 200

hsh.has_value?(100) => true
```
