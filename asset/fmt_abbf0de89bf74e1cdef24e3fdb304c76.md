
`hsh.has_value?(999)` => false

```
# include?
```

`hsh.include?(key)` -> true or false

`Hash#hash_key` 的同义词。

```
# index
1.9
```

`hsh.index?(key)` -> key

已弃——请用 `Hash#key` 代替。

```
# invert
```

`hsh.invert` -> other_hash

返回一个使用 `hsh` 的值作为键、键作为值创建的新哈希。如果 `hsh` 有重复的值，结果将仅包含其中一个——其结果是不可预测的。

```
h = "n" => 100, "m" => 200, "y" => 300, "d" => 200, "a" => 0
```

`hsh.invert` => `{"100"=>"n", 300=>"y", 200=>"d", 0=>"a"}`

```
# key
1.9
```

`hsh.key?(key)` -> key or nil

返回第一个值为 value 的哈希的键。

```
h = { a: 100, b: 200, c: 100 }
```

`h.key(100)` => `:a`

`h.key(200)` => `:b`

`h.key(300)` => nil

```
# key?
```

`hsh.key?(key)` -> true or false

`Hash#hash_key` 的同义词。

```
# keys
```

`hsh.keys` -> array

返回一个包含此哈希中所有键的新数组。类似于 `Hash#values`。

```
h = { "a" => 100, "b" => 200, "c" => 300, "d" => 200 => 400 }
```

`h.keys` => `["a", "b", "c", "d"]`

```
# length
```

`hsh.length` -> fixnum

返回哈希中键/值对的数量。

```
h = { "d" => 100, "a" => 200, "v" => 300, "e" => 400 }
```

`h.length` => 4

`h.delete("a")` => 200

`h.length` => 3

```
# member?
```

`hsh.member?(key)` -> true or false

`Hash#hash_key` 的同义词。

```
# merge
```

```
hsh.merge(other_hash) -> result_hash
```

`hsh.merge(other_hash) -> {key, old_val, new_val | block} -> result_hash`

返回一个包含 `other_hash` 内容和 `hsh` 内容的新哈希。在没有块管理程序的情况下，将用 `other_hash` 中的重复键覆盖 `hsh` 中的条目。如果指定了块，则会使用每个重复键以及两个哈希的值来调用该块。返回的值是存储在新哈希中的块的结果。

```
h1 = {"a" => 100
```

```
# merge!
```

```
hsh.merge(other_hash) -> hsh
```

`hsh.merge(other_hash) {|key, old_val, new_val | block} -> hsh`

类似于 `Hash` 但会改变 `hsh` 的内容。

```
h1 = {"a" => 100
```

```
# rassoc
1.9
```

在哈希中搜索第一个值等于 key 的元素，并将键和值作为元素数组返回。如果值未在哈希中出现，则返回 nil。

```
h = {"a" => 100, "b" => 200, "c" => 100} => {"a"=>100, "b"=>200, "c"=>100}
```

`h.rassoc(100)` => `{"a", 100}`

`h.rassoc(200)` => `{"b", 200}`

```
# rehash
```

根据每个键的当前值重新哈希哈希。如果对象的值自插入以来发生了变化，遍历哈希的迭代器将通过此方法进行重新哈希。如果在遍历迭代器时调用 `Hash#rehash`，将在迭代器上抛出 `IndexError`。

```
a = ["a", "b"]
```

```
c = ["c", "d"]
```

`h = {a => 100, c => 300}`

`h[a]` => nil

`a[0]` => "z"

`h[a]` => nil

`h.rehash` => `{"z", "b"]=>100, ["c", "d"]=>300}`

`h[a]` => 100

```
# reject
```

`hsh.reject {|key, value| block}` → hash

类似于 `Hash#delete_if`，但作用于 `hsh` 的副本并返回该副本。这等于 `hsh.dup.delete_if`。

```
# reject!
```

`hsh.reject! ({key, value| block})` → hsh enumerator

等于 `Hash#delete_if`，但如果没有进行任何更改则返回 nil。如果提供了块，则返回一个 `Enumerator` 对象。

```
# replace
```

`hsh.replace(other_hash)` → hsh

用 `other_hash` 的内容替换 `hsh` 的内容。

```
h = {"a" => 100, "b" => 200}
```

`h.replace({"c" => 300, "d" => 400})` => `{"c" => 300, "d" => 400}`

```
# select
```

`hsh.select {|key, value| block}` → array

#1.9

返回块为 true 的新哈希对。这与 1.8 版本不同，1.8 返回的是数组。

```
h = {"a" => 100, "b" => 200, "c" => 300}
```

`hsh.select {|k,v| v > 200}` => `{"b" => 200, "c" => 300}`

`hsh.select {|k,v| v < 200}` => `{"a" => 100}`

```
# shift
```

`hsh.shift` → array or nil

从 `hsh` 中移除键/值对并以元素数组 `[key, value]` 返回它。如果哈希为空，则返回 nil。

```
h = {"1" => "a", "2" => "b", "3" => "c"}
```

`h.shift` => `["1", "a"]`

`h = {"2" => "b", "3" => "c"}`

```
# size
```

`Hash#length` 的同义词。

```
# sort
```

`hsh.sort {|a,b|}` → array

将 h 转换为嵌套的 `[key, value]` 数组并使用 `Array#sort` 进行排序。

```
h = {"a" => 20, "b" => 10, "c" => 30}
```

`h.sort` => `[["b", 10], ["a", 20], ["c", 30]]`

```
# store
```

`hsh.store(key, value)` → value

赋值 (`=`) 的同义词。

```
# to_a
```

`hsh.to_a` → array

将 h 转换为嵌套的 `[key, value]` 数组。

```
h = {"c" => 300, "a" => 100, "d" => 400, "b" => 200}
```

`hsh.to_a` => `["c", 300], ["a", 100], ["d", 400], ["b", 200]`

```
# to_hash
```

`hsh.to_hash` → hsh

见第 376 页。

```
# to_s
```

`hsh.to_s` → string

通过将哈希转换为 `[key, value]` 数组，然后使用 `Array#join` 默认分隔符将 `hsh` 转换为字符串。

```
h = {"c" => 300, "a" => 100, "d" => 400, "b" => 200}
```

`hsh.to_s` => `"c=300,a=100,d=400,b=200"`

```
# update
```

`hsh.update(other_hash) { key, old_val, new_val }` → hsh

`Hash#merge!` 的同义词。

```
# value?
```

`hsh.value?` → true or false

`Hash#has_value` 的同义词。

```
# values
```

`hsh.values` → array

返回包含 `hsh` 中值的数组。参见 `Hash#keys`。

```
h = {"a" => 100, "b" => 200, "c" => 300}
```

`h.values` => `[100, 200, 300]`

```
# values_at
```

`hsh.values_at(key)+` → array

返回由给定键的值组成的数组。对于未找到的键，插入默认值。

```
h = {"a" => 100, "b" => 200, "c" => 300}
```

`h.values_at("a", "c")` => `[100, 300]`

`h.values_at("a", "c", "z")` => `[100, 300, nil]`

`h.default = "cat"`

`h.values_at("a", "c", "z")` => `[100, 300, "cat"]`

```
# Integer < Numeric
```

子类：`Bignum`, `Fixnum`

`Integer` 是存储整数的两个类 `Bignum` 和 `Fixnum` 的基础（如果你是为了寻找迭代器步长，请见 621 页）。

```
# 实例方法
```

+ `ceil`
`int.ceil` -> integer

`Integer#to_i` 的同义词。

+ `chr`
`int.chr` -> string

返回包含接收者值所代表的 ASCII 字符的字符串。

```
65.chr => "A"
```

```
97.chr => "a"
```

```
230.chr => "\uE6"
```

+ `denominator`
`int.denominator` -> integer

转换为 int 有理表示的分母。

```
1.denominator => 1
```

```
1.5.denominator => 2
```

```
# downto
```

`int.downto` -> integer

返回小于等于 int 的最大整数。

```
1.downto => 1
```

```
2.downto => 1
```

```
# even?
```

`int.even?` → true or false

如果 int 是偶数，则返回 true。

```
1.even? => false
```

```
2.even? => true
```

```
# floor
```

`int.floor` -> integer

返回小于等于 int 的最大整数。

```
1.floor => 1
```

```
1.5.floor => 1
```

```
# numerator
```

`int.numerator` -> integer

返回 int 有理表示的分子。

```
1.numerator => 1
```

```
1.5.numerator => 1
```

```
# denominator
```

`int.denominator` -> integer

返回 int 有理表示的分母。

```
1.denominator => 1
```

```
1.5.denominator => 2
```

```
# pred
```

`int.pred` -> integer

返回 `int - 1`。

```
1.pred => 0
```

```
2.pred => 1
```

```
# succ
```

`int.succ` -> integer

返回 `int + 1`。

```
1.succ => 2
```

```
2.succ => 3
```

```
# times
```

`int.times{i| block} -> int`

迭代 `block` 次，传入从零到 `int-1` 的值。

```
5.times {i|
```

```
print i, " "
```

```
end
```

产出：

```
0 1 2 3 4
```

```
# to_i
```

`int.to_i` -> int

返回 int。

```
1.5.to_i => 1
```

```
# to_r
```

`int.to_r` -> number

将 int 转换为有理数。

```
1.to_r => 1/1
```

```
-1.to_r => -1/1
```

```
# truncate
```

`int.truncate` -> integer

`Integer#to_i` 的同义词。

```
# upto
```

`int.upto(integer) {i| block} -> int`

迭代 `block`，传入从 int 直到包含 integer 的整数值。

```
5.upto(10) {i| print i, " " }
```

产出：

```
5 6 7 8 9 10
```

```
# IO < Object
```

子类：`File`

`IO` 类是所有输入和输出的基础。I/O 流可以是全双工的（即双向的），并且可以使用多个一个操作系统的流。

本节中的许多示例使用了 `File`，它是 `IO` 唯一的标准子类。这两个类之间紧密相关。

在本节中，`portname` 可以取以下任何一种形式：

- 一个普通的字符串，表示适用于操作系统的文件名。
- 以 `|` 开头的字符串表示一个子进程。`|` 之后的剩余字符串将作为一个进程调用，并与其连接了输入/输出通道。
- 等于 `|` 的字符串可以将另一个 Ruby 实例作为子进程耦合。

`IO` 类使用了 Unix 文件描述符（fds）的抽象，这些是表示已打开文件的短整数。按照惯例，标准输入的 fd 为 0，标准输出的 fd 为 1，标准错误的 fd 为 2。

Ruby 会在不同的操作系统约定之间转换路径。例如，在 Windows 系统上，文件名 `/gumbry/ruby/test.rb` 将被打开为 `\gumbry\ruby\test.rb`。在双引号字符串中指定 Windows 风格的文件名时，请记住转义斜杠。

```
"c:\\gumbry\\ruby\\test.rb"
```

我们的示例使用 Unix 风格的正斜杠；可以使用 `File::SEPARATOR` 来获取特定平台的字符分隔符。

I/O 端口可以在几种不同模式中的任意一种打开，这些模式在 mode 节中显示。此模式必须是下一页表 27.7 中列出的值之一。从 Ruby 1.9 开始，模式还可以包含有关正在处理的数据外部和内部编码的信息。如果指定了外部编码，Ruby 假设它从操作系统接收到的数据使用该编码。如果没有给出内部编码，则从端口读取的字符串将具有此编码。数据将从外部编码转码为内部编码，且写入的字符串将具有该编码。输出时发生相反的操作。

文件模式可以可选地由 `Fixnum` 或或运算类型指定，该类型紧跟在第 514 页表 27.5 描述的标志之后。（是的，IO 使用子类中定义的常量是一种糟糕的耦合。）

```
# Mixins（混入）
```

`Enumerable`:
`all?`, `collect`, `count`, `cycle`, `detect`, `drop`, `drop_while`, `each_cons`, `each_slice`, `each_with_index`, `entries`, `find`, `find_all`, `find_index`, `grep`, `group_by`, `include?`, `inject`, `map`, `max`, `max_by`, `member?`, `min`, `min_by`, `minmax`, `minmax_by`, `none?`, `one?`, `partition`, `reduce`, `reject`, `select`, `sort`, `sort_by`, `take`, `take_while`, `to_a`, `zip`

```
# 表 27.7. 模式字符串
```

模式可以用由表 27.7 中的值通过或运算形成的整数来表示。它们更常见的表示形式是字符串。模式字符串的形式为 `"filemode[external-encoding][internal-encoding]"`。file-mode 部分是下表列出的选项之一。两个编码是你的解释器支持的编码名称（或别名）。更多信息请见第 264 页的第 17 章。

| Mode | 含义 |
|---|---|
| r | 只读，从文件开头开始（默认模式）。 |
| r+ | 读/写，从文件开头开始。 |
| w | 只写，将现有文件截断为零长度或创建一个新文件用于写入。 |
| w+ | 读/写，将现有文件截断为零长度或创建一个新文件用于读写。 |
| a | 只写，如果文件存在，则从文件末尾开始；否则创建一个新文件用于写入。 |
| a+ | 读/写，如果文件存在，则从文件末尾开始；否则创建一个新文件用于读写。 |
| b | 二进制模式（可能与之前列出的任何关键字一起出现）。从 Ruby 1.9 开始，所有以二进制模式打开的端口（无论 Unix 还是 DOS/Windows）都应提供此修饰符。要以二进制模式读取文件并将数据作为流，请使用修饰符 "ascii-8bit"。

```
# 类方法
```

`IO.binread(name, length, offset)` -> string

以模式：`ASCII-8BIT` 打开 `name`，从 `offset` 开始读取 `length` 个字节，并关闭文件。返回的字节将以具有 `ASCII-8BIT` 编码的字符串形式给出。`Offset` 默认为 0，`length` 默认为 `offset` 到文件末尾之间的字节数。

```
IO.binread("testfile", 20) => "This is line one\nThis"
```

```
IO.binread("testfile", 20) => "is line two\nThis"
```

```
IO.binread("testfile") => <Encoding:ASCII-8>
```

```
IO.binread("testfile") => <Encoding:UTF-8>
```

`IO.copy_stream(from, to, max_length, offset)` -> integer

将 `from` 复制到 `to`。这些可以指定为文件名或 `IO` 流。你可以可选地指定复制的最大长度和起始偏移量。返回复制的字节数。

```
IO.copy_stream("testfile", File.open("/etc/passwd", "w"), 10, 10)
```

```
op = File.open("extract", "w")
```
