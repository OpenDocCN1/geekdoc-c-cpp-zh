
```ruby
def marshal_load(marshal_data)

  @when_dumped = marshal_data[0].strftime("%Y-%m-%d")

  @other_data = marshal_data[1]

end

end
```

```ruby

t = TimedDump.new

t.other_data = "wobble"

t.when_dumped => nil

str = Marshal.dump(t)

newt = Marshal.load(str)

```

# Module 常量

`MAJOR_VERSION` `marshal` 格式号的主部分。
`MINOR_VERSION` `marshal` 格式号的次部分。

# Module 方法

```ruby

dump(obj {, :io}, limit=-1) -> io

```

序列化 `obj` 和所有后代。如果指定了 `io`，序列化数据将被写入；如果指定了 `limit`，子对象的遍历将被限制在该深度。如果 `limit` 为负，则不进行深度检查。

```ruby

load({from, :proc}) -> obj

```

将 `from` 中的序列化数据转换为 Ruby 对象（可能带有关联子对象）。`from` 可能是 IO 实例或响应 `to_str` 的对象。如果指定了 `proc`，则会在反序列化时传递每个对象。

# restore

```ruby

restore({from, :proc}) -> obj

```

`Marshal.load` 的同义词。

# MatchData < Object

所有模式匹配会将特殊变量 `$-` 转换为包含方法信息的 `MatchData`。`Regexp#match` 和 `Regexp.last_match` 也返回一个 `MatchData` 对象。该对象封装了模式匹配的所有结果，通常通过特殊变量 `$,$1,$2` 等访问（见第 240 页列表）。

# 实例方法

`[]`

匹配引用——`MatchData` 相当于数组或哈希，可以使用标准的索引技术。数字索引返回正则表达式中对应位置的捕获（从 1 开始）。符号索引返回对应的名称。`match[0]` 等于变量 `$$` 并返回整个匹配字符串。另见 `MatchData#select` 和 `MatchData#values_at`。

```ruby

m = /(.+)(\d+)/.match("THX138")

m[0] => "THX138"

m[1] => ["H", "X"

m[1..] => ["H", "X", "113"]

m[-2] => "113"

m = /.+/(?<digit_prefix>=\d+)/.match("THX138")

m[:digit_prefix] => "113"

```

# begin

```ruby

match.begin(n) => int

match.begin(name) => int

```

### 1.9

```ruby

m = /(.+)(\d+)/.match("THX138")

m.begin(0) => 1

m.begin(2) => 2

m = /.+/(?<digit_prefix>=\d+)/.match("THX138")

m.begin(:digit_prefix) => 3

```

# captures

返回所有匹配组的数组。对比 `MatchData#lo_a`，后者同时返回完整的匹配字符串和所有匹配组。

```ruby

m = /(.+)(\d+)/.match("THX138")

m.captures => [["H", "X", "113", "8"]]

```

`captures` 用于在赋值中提取匹配的部分。

```ruby

f1, f2, f3 = /(.+)(\d+)/.match("THX138").captures

f1 => "H"

f2 => "X"

f3 => "113"

```

`match.end(n ) -> int`
`match.end(name ) -> int`

### 1.9

返回第 `n` 个捕获或命名捕获在原始字符串中的偏移量。

```ruby
m = /(.)(\.)(\d+)(\d+)/match("THX1138.")
m.end(0) # => 7
m.end(2) # => 3
m = /(?<digit_prefix>\d+)/d/.match("THX1138.")
m.end(digit_prefix) # => 6
```

# length

`match.length -> int`

返回匹配数组中的元素个数。

```ruby
m = /(.)(\.)(\d+)(\d+)/match("THX1138.")
m.length # => 5
m.size # => 5
```

# names

`match.names -> array`

### 1.9

返回创建 `match` 的正则表达式中的名称列表。

```ruby
m = /(?<prefix>[A-Z])?<hyphen>)?(?<digits>\d+)/match("THX1138.")
m.names # => ["prefix", "hyphen", "digits"]
m.captures # => ["THX", "", "1138"]
m.prefix # => "THX",
```

# offset

`match.offset(n ) -> array`
`match.offset(name ) -> array`

### 1.9

返回一个包含第 `n` 个或命名捕获的起始和结束偏移量的双元素数组。

```ruby
m = /(.)(\.)(\d+)(\d+)/match("THX1138.")
m.offset(0) # => [1, 7]
m.offset(4) # => [6, 7]
m = /(?<digit_prefix>\d+)/d/.match("THX1138.")
m.offset(digit_prefix) # => [3, 6]
```

# post_match

`match.post_match -> string`

返回原始字符串中当前匹配之后的位置。等同于特殊变量 `$`.

```ruby
m = /(.)(\.)(\d+)(\d+)/match("THX1138: The Movie")
m.post_match # => "The Movie"
```

# pre_match

`match.pre_match -> string`

返回原始字符串中当前匹配之前的位置。等同于特殊变量 `$`.

```ruby
m = /(.)(\.)(\d+)(\d+)/match("THX1138.")
m.pre_match # => "THX"
```

# match.regexp → a_regex

1.9 返回创建 `match` 的正则表达式的 `.regexp` 对象。

```ruby

m = /(.)\(\d+)(\d)/.match("THX1138: The Movie")

m.regexp => /(.)\(\d+)(\d)/

```

# size match.size → int

`MatchData#.length` 的同义词。

# string match.string → string

返回传递给 `match` 的字符串的冻副本。

```ruby

m = /(.)\(\d+)(\d)/.match("THX1138")

m.string => "THX1138",

```

# to_a match.to_a → array

返回匹配数组。与 `MatchData#captures` 不同，它返回匹配的完整字符串。

```ruby

m = /(.)\(\d+)(\d)/.match("THX1138")

m.to_a => ["THX1138", "H", "X", "113", "8"]

```

# to_s match.to_s → string

返回整个字符串。

```ruby

m = /(.)\(\d+)(\d)/.match("THX1138")

m.to_s => "THX1138",

```

# values_at match.values_at({ index }*) → array

`MatchData#.select` 的同义词。

# Math

`Math` 模块包含用于基本三角函数和超越函数的模块方法。请参见第 528 页的 `Float` 以获取定义 Ruby 浮点精度的常量列表。

# 模块常量

- * `E` $e$ 的近似值（自然对数的底数）
- `Pi` $\pi$ 的近似值

# 模块方法

```ruby

Math.acos(x) -> float

```

计算 $x$ 的反余弦。返回 $0..\pi$。

```ruby

Math.acosh(x) -> float

```

计算 $x$ 的反双曲余弦。

```ruby

Math.asin(x) -> float

```

计算 $x$ 的反正正弦。返回 $-\frac{\pi}{2}..\frac{\pi}{2}$。

```ruby

Math.asinh(x) -> float

```

计算 $x$ 的反双曲正弦。

```ruby

Math.atan(x) -> float

```

计算 $x$ 的反正正切。返回 $-\frac{\pi}{2}..\frac{\pi}{2}$。

```ruby

Math.atan2(y, x) -> float

```

计算由 $y$ 和 $x$ 给出的反正正切。返回 $-\pi..$.

```ruby

Math.cbrt(numeric) -> float

```

返回 *numeric* 的立方根。

```ruby

Math.cos(x) -> float

```

计算 $x$ 的余弦（以弧度表示）。返回 $-1..1$。

```ruby

Math.cosh(x) -> float

```

计算 $x$ 的双曲余弦（以弧度表示）。

# Math.erf(x) -> float

返回 $x$ 的误差函数。

```ruby

erf(x) = \frac{2}{\sqrt{\pi}} \int_{0}^{x} e^{-t^{2}} dt

```

# Math.erfc(x) -> float

返回 $x$ 的互补误差函数。

```ruby

erfc(x) = 1 - \frac{2}{\sqrt{\pi}} \int_{0}^{x} e^{-t^{2}} dt

```

# Math.exp(x) -> float

返回 $e^{x}$。

# Math.frexp(numeric) -> [fraction, exponent]

返回一个包含 `numeric` 的标准化分数 (`Float`) 和指数 (`Fixnum`) 的双元素数组。

```ruby

fraction = Math.frexp(1234) # [0.60259025, 10]

exponent *= 2

```

# Math.gamma(x) -> float

返回 Gamma 函数 $\Gamma$。对于整数 $x$，近似 `factorial(x-1)`。

```ruby

gamma(2) => 1.0

gamma(3) => 2.0

gamma(4) => 6.0

```

# Math.hypot(x, y) -> float

返回边长 $x$ 和 $y$ 的直角三角形的斜边。

```ruby

hypot(3, 4) => 5.0

```

# Math.ldexp(float, integer) -> float

返回 $float \times 2^{integer}$。

```ruby

fraction, exponent = Math.ldexp(1234) # => 3.0

```

# Math.lgamma(x) -> [float, sign]

返回 Gamma 函数绝对值的自然对数。如果 Gamma 函数返回负数，`sign` 为 -1，否则为 +1。

# Math.log(numeric) -> float

返回 $numeric$ 的自然对数。

# Math.log10(numeric) -> float

返回 $numeric$ 的以 10 为底的对数。

# Math.log2(numeric) -> float

返回 $numeric$ 的以 2 为底的对数。（注：此处原文应为log2）

# Math.sin(numeric) -> float

计算 $numeric$ 的正弦（以弧度表示）。返回 $-1..1$。

# Math.sinh(numeric) -> float

计算 $numeric$ 的双曲正弦（以弧度表示）。

# Math.sqrt(numeric) -> float

返回 $numeric$ 的非负平方根。如果 $numeric$ 小于零，则抛出 `ArgError`。

# Math.tan(numeric) -> float

返回 $numeric$ 的正切（以弧度表示）。

# Math.tanh(numeric) -> float

计算 $numeric$ 的双曲正切（以弧度表示）。

# Method < Object

`Method` 对象由 `Object#method` 创建。它们与特定的对象关联（而不是类）。它们用于调用对象内部的方法或作为迭代器。它们也可以从一个对象取消（创建 `UnboundMethod`）并绑定到另一个对象。

```ruby

def square(n)

  n

end

meth = self.method(:square)

```

```ruby

meth.call(9) # => 9

[1, 2, 3].collect(&meth) # => [1, 4, 9]

```

# Instance methods

`call` 的同义词。

# == other -> true or false

如果 `meth` 和 `other` 是同一个方法，则返回 true。

```ruby

def fred()

  puts "Hello"

end

alias bert fred # => nil

```

```ruby

m1 = method(:fred)

m2 = method(:bert)

m1 == m2 # true

```

# arity

`meth.arity -> fixnum`

返回方法接受的参数个数。请参见下一页的图 27.2。另见 `Method#parameters`。

# call

`meth.call { args } -> object`

使用参数调用 `meth`，返回方法的返回值。

```ruby

m = 12.method("+")

m.call(3) # => 15

m.call(20) # => 32

```

# eq?

`meth.eq?(other) -> true or false`

如果 `meth` 和 `other` 是同一个方法，则返回 true。

# 图 27.2. Method#arity 的应用

`Method#arity` 为固定参数的方法返回非负整数。对于接受数量参数的 Ruby 方法，返回 -n，其中 n 是必需参数的个数。用 C 编写的方法如果调用接受数量参数，则返回 -1。

```ruby

class C

  def one; end

  def two(a); end

  def three(*); end

  def four(a, b); end

  def five(a, b, *c); end

  def six(a, b, *c, &d); end

end

c = C.new

c.method(:one).arity => 0

c.method(:two).arity => 1

c.method(:three).arity => -1

c.method(:four).arity => 2

c.method(:five).arity => -3

c.method(:six).arity => -3

"cat".method(:size).arity => 0

"cat".method(:replace).arity => 1

"cat".method(:squeeze).arity => -1

"cat".method(:count).arity => -1

```

```ruby

def fred(n)

  puts "Hello"

end

alias bert fred # = => nil

m1 = method(:fred)

m2 = method(:bert)

m1.eq?(m2) # = => true
```
