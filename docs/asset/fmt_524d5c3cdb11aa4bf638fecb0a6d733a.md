
| Dynamic | 0.471000 | 0.110000 | 0.581000 | ( 1.522000 ) |

| Via proxy | 0.470000 | 0.130000 | 0.600000 | ( 0.952000 ) |

代理版本比执行动态查找的代码快了 40% 以上。

### 更多帮助

如果您需要将 Ruby 与 Windows NT、2000 或 XP 建立接口，您可能想查看 Daniel Berger 的 Win32Utils 项目（http://rubyforge.org/projects/win32utils/）。您将可以在那里找到与 Windows 剪贴板、事件日志、调度程序等交互的模块。

此外，`DL` 接口（在第 746 页简要描述）允许 Ruby 程序调用动态加载的对象中的方法。在 Windows 上，这意味着您的 Ruby 代码可以加载。

### 表 22.1. 通用定界输入

| 类型 | 含义 | 页码 |

| --- | --- | --- |

| `%q` | 单引号字符串 | 328 |

| `%Q`, `%` | 双引号字符串 | 328 |

| `%w`, `%W` | 字符串数组 | 330 |

| `%f` | 正则表达式模式 | 332 |

| `%s` | 符号 | 331 |

| `%x` | Shell 命令 | 344 |

`%q/this is a string/`

`%q-string-`

`%q(a nested) string`

定界字符串可以跨行；行结束符和延续行开头的所有空格都将包含在字符串中：

```
meth = %q(def fred(a)
  a.each {|i| puts i }
end)
```

### 基本类型

Ruby 的基本类型包括数字、字符串、数组、哈希表、范围、符号和正则表达式。

### 整数和浮点数

Ruby 整数是 `Fixnum` 或 `Bignum` 类的对象。`Fixnum` 对象存储能够在原生机器减去 1 位范围内的整数。每当 `Fixnum` 超过此范围时，它会自动转换为 `Bignum`，其范围实际上受限于可用内存。对 `Bignum` 进行的操作得到的最终值如果可以放入 `Fixnum`，则结果将作为 `Fixnum` 返回。

整数的写法使用可选的前导符号和可选的基数指示符（`0` 或 `00` 表示八进制，`0d` 表示十进制，`0x` 表示十六进制），后跟相应基数的数字字符串。数字字符串中的下划线字符会被忽略。

```
123456 => 123456 # Fixnum
0123456 => 123456 # Fixnum
123_456 => 123456 # Fixnum - 忽略下划线
-543 => -543 # Fixnum - 负数
0aabb => 43707 # Fixnum - 十进制
0377 => 255 # Fixnum - 八进制
0037 => 255 # Fixnum
0b1_1010 => -42 # Fixnum - 二进制（取反）
123_456_789_123_456_789 => 123456789123456789 # Bignum
```

带有小数点和/或指数的数值字面量会被转换为 `Float` 对象，对应于原生架构的双精度数据类型。你必须在小数点后紧跟一个数字：如果你写 `1.e3`，Ruby 会尝试在 `Fixum` 对象 `1` 上调用 `e3` 方法。你必须在小数点之前至少放置一个数字。

```
12.34 # => 12.34
-0.1234e2 => -12.34
1234e-2 # => 12.34
```

### 有理数和复数

Ruby 解释器内置了支持有理数（整数比例）和复数的类。然而，Ruby 并没有对这些数值类型提供语言级别的支持。例如，并没有有理数或复数的字面量。更多信息请参见第 473 页和 660 页上 `Complex` 和 `Rational` 的描述。

### 字符串

Ruby 提供了多种创建字符串字面量的机制。每个都会生成一个 `String` 类型。不同机制的区别取决于字符串的定界方式以及字面量内容的划分程度。字符串字面量使用其包含的文件源编码进行编码。

单引号字符串字面量（`'...'`）和 `"..."` 的替换最少。两者都会将序列 `\` 转换为单个反斜杠，而单引号形式会将单引号转换为单引号。所有的反斜杠都会原样出现在字符串中。

```
"hello" # => hello
'\\ backslash\'' # => 反斜杠 '\'
%q/simple # => 一个简单的字符串
%q/nesting (really) works # 嵌套
%q/no_blanks_here # => 这里没有空格
```

双引号字符串（`"..."`）、`%Q` 和 `%{}` 会进行额外的替换，见下页的表 22.2。

```
a = 123
"123abc"
"Greek pi: \u03c0" # => π
"Greek pi: \pi" # => π
"Greek pi: %{70 69 3a 30}" # => π
"Say \Hello\" # => "Hello"
%Q!(I said 'nuts',), I said! => "nuts'"
%Q(Try #{a + 1}, #{a - 1}) # => 124, 22
%<(Try #{a + 1}, #{a - 1}> # => 124, 22
"#{#{a + 1}, #{a - 1}}" # => 124, 22
```

### 表 22.2. 双引号字符串中的替换

| \a Bell (0x07) | \n Octal |

| \b Backspace (0x08) | \x Hex |

| \c Escape (0x1b) | \cx Control |

| \f Formfeed (0x0c) | \C-x Control |

| \n Newline (0x0a) | \M-x Meta |

| \r Return (0x0d) | \M-\C-x Control |

| \s Space (0x20) | x |

| \t Tab (0x09) | #code Value |

| \v Vertical (0x0b) | \uxxx Unicode character |

（注：OCR 文本重复）

如果你保留了作为键的对象的外部引用并修改了它的哈希值，哈希查找可能无法工作。你可以通过调用 `rehash` 方法强制哈希重新索引。

```
arr = [1, 2]
hash = { arr => 'value' }
hash[arr] # => 99
arr[1] # => {[1, 3]->"value"
hash[arr] # => nil
hash.rehash
hash[arr] # => "value"
```

`:Object`

`:my_variable`

`:Ruby rules`

a = "cat"

```
':catsup # => :catsup
:#{a}sup => :catsup
:#{a}sup => \#{a}sup
$%symbol => :symbol
$% symbol with spaces
```

其他语言将此称为接口和符号（symbols）。

### 正则表达式

本节包含了 Ruby 使用的 Onigimura Ruby 表达式引擎的摘要。有关正则表达式的描述，请参阅第117页的第七章。

正则表达式是 `RegExp` 类型的对象。它们可以通过调用 `Regexp.new` 显式创建，也可以通过字面量形式 `/pattern/` 和 `%(pattern)` 隐式创建。`%t` 结构是一种通用界符的形式（见第326–327页）。

```
/pattern/
/pattern/options
%r(pattern)
%r(pattern)options
Regexp.new('pattern', [ ])
```

options 是一个或多个（忽略大小写，o 替换，m（匹配换行符），以及 x（允许空格和注释）。你还可以通过 n（无编码-ASCII）、e（EUC）、s（Shift_JIS）或 u（UTF-8）覆盖模式的默认编码。

# 正则表达式模式

- 1.9（本节包含与本书之前的版本的许多不同之处。Ruby 1.9 使用的是 Onigimura Ruby 表达式引擎。）^

```
characters All except, \ , ( ) [ [ \ ] ^ +, *, & . 要匹配所有这些字符，请在它们前面加一个反斜杠。
\a \c \e \f \t \n \u \v \CN \V-M \X-x
```

```
匹配根据第329页表22.2推导出的字符。
匹配字符串的开头/结尾。\Z 忽略末尾的 \。
匹配任何十数字（或 Unicode Decimal_Number），十六进制数字 [0-9a-A-F]
```

```
\s 匹配任何空白字符：制表符、换行符、垂直制表符、分页符、返回和空格。对于 Unicode，匹配 Line_Separator 代码点。
```

- 2 此处的某些信息基于 http://www.geocities.jp/kosako3/onigimura/doc/RE.txt。

- `\w` 匹配单词字符：字母、数字和下划线。对于 Unicode，将其添加到 Connector_Punctuation、Letter、Mark 和 Number 的代码点中。

- `\d`, `\h`, `\s`, 和 `\w` 的否定形式，匹配非十六进制数字、空白字符或单词字符的字符。

- 匹配单词/非单词边界。

- `\G \p(property)|\P(property)` 之前重复的序列完成的位置。

- 匹配不在给定组组中的字符（见第126页第7.3节）。

- (period) 出现在括号外时，匹配除换行符的任何字符。（带有 m 选项时，它也会匹配换行符）。

- [characters] 匹配指定集合中的单个字符。见第123页。

- re+ 匹配 re 的零次或多次。

- re(m,n) 匹配 re 至少 "m" 次且最多 "n" 次。

- re(m) 匹配 re 至少 "m" 次。

- re(n) 匹配 re 最多 "n" 次。

- re{m} 匹配 re 正好 "m" 次。

- ? 匹配 re 的零次或一次。

- ?, *, +, 和 [m] 修饰符默认是贪婪的。在后面加上问号使其变为最小的，并添加加号使其变为独占的（即它们是贪婪的且不会回溯）。

- re1|re2 匹配 re1 或 re2。

- (...) 分组表达式并引入扩展。

- #(...) 模式中的字符串替换。默认情况下，在每次评估正则表达式时都会执行替换。使用 /o 选项时，在第一次时执行。

- `\0`, `\1`, `\2`, ... `\n`, `\N`, `\v+` 通过第 n 个分组子表达式或整个匹配（匹配前或后匹配）或最高组来替换值。

- (?) 向模式中插入。

- (:re) 将 re 变为一个组但不生成反向引用。

- (=re)|(?<re) 如果 re 不在此处则进行匹配，但不消耗它。

- (?=re) 如果 re 在在此点之前则进行匹配，但不消耗它。

- (?>re) 匹配 re，但抑制后续的回溯。

- (?ix)(?:ix) 关闭 i, m 或 x 选项。如果在组内部使用，效果限于该组。

- (?ix:re) 关闭 re 的 i, m 或 x 选项。

- 3. 此类名称将无法从具有不同编码的其他文件使用。

# 表 22.3  留字

| | | | |

| :--- | :--- | :--- | :--- |

| __FILE_ and def end in or self unless | | | |

| __LINE_ begin defined? ensure module redo super until | | | |

| BEGIN break do false next rescue then when | | | |

| END case else for nil retry true while | | | |

| alias class elsif if not return undef yield | | |

按照惯例，常量对象引用通常使用全大写字母和下划线书写，而类和方法使用 MixedCase：

```
module Math
  ALMOST_PI = 22.0/7.0
end
class BigBlob
end
```

**全局变量**以及某些系统变量以美元符号 ($) 开头，后跟名称字符。此外，Ruby 定义了一组第二个字符为标点符号的双字符全局变量。这些预定义的变量从第339页开始列出。最后，一个...

# 变量与常量

```ruby
Holder.var = 123
a.var #> 123
```

```ruby
# 这引用顶层对象
def a.get_var
  @var
end
a.get_var #= "top level variable"
```

类变量会被子类继承，但在不同的子类之间是相互唯一的：

```ruby
class Top
  @@A = 1
  @@B = 1
  def dump
    puts values
    dump values
    "#{self.class.name}: @@A = #{@@A}, @@B = #{@@B}"
  end
end
```

```ruby
class MiddleOne < Top
  @@B = 2
  @@C = 2
  def dump
    super + ", C = #{@@C}"
  end
end
```

```ruby
class MiddleTwo < Top
  @@B = 3
  @@C = 3
  def dump
    super + "", C = #{@@C}"
  end
end
```

```ruby
class BottomOne < MiddleOne; end
class BottomTwo < MiddleTwo; end
```

```ruby
Top.new.dump
MiddleOne.new.dump
MiddleTwo.new.dump
BottomOne.new.dump
BottomTwo.new.dump
```

产生：

```
Top: @@A = 1, @@B = 3
MiddleOne: @@A = 1, @@B = 3, C = 2
MiddleTwo: @@A = 1, @@B = 3, C = 3
BottomOne: @@A = 1, @@B = 3, C = 2
BottomTwo: @@A = 1, @@B = 3, C = 3
```

出于这个原因，我不建议使用类变量。

块（block）捕获其创建时存在的局部变量集合。这构成了其绑定（binding）的一部分。注意变量的绑定在这一点就已经固定了，块在执行时将访问这些变量的*当前值*。即使原始的闭包被销毁，绑定也会保留这些变量。

`while`、`until` 和 `for` 循环的体处于它们所在的作用域；之前存在的局部变量可以在循环中使用，而任何新创建的局部变量在循环结束后位于外部。

## 定义变量

以下变量在 Ruby 解释器中是预定义的。在这些描述中，符号 [f/o] 表示这些变量是只读的；如果程序尝试修改只读变量，将抛出错误。毕竟，你可能不想在程序运行中途改变 `true` 的含义（除非你是个政治家）。

标记为 [thread] 的项目是线程局的。

# 变量与常量

许多全局变量看起来像 Snoopy 在咒脏：`$$`、`$` 等。由于“历史”原因，这些变量名大部分源自 Perl。如果你发现记忆这些标点很困难，可能想查看第 748 页记录的 `English` 库文件，它为常用的全局变量提供了更具描述性的名称。

在接下来的变量和常量表中，我们展示了变量、所引用对象的类型以及描述。

## 异常信息

- `$!` Exception 传递给 `raise` 的异常对象。[thread]

- `$@` Array 由上一个异常生成的堆栈回溯。详情参阅第 567 页的 `Kernel#caller`。[thread]

## 模式匹配变量

这些变量（除 `=` 外）在模式匹配失败后会被设置为 `nil`。

- `$` String 匹配到成功模式的字符串。该变量是当前作用域的局部的：[], [thread]

- `$+` String 匹配到成功模式中编号最高的组的内容。在 `"cat"=$=(i)/(z)` 中，`$+` 将被设置为 `"t"`。该变量是当前作用域的局部的：[], [thread]

- `$'` String 成功模式匹配中匹配项之前的字符串。该变量是当前作用域的局部的：[], [thread]

- `$`` String 成功模式匹配中匹配项之后的字符串。该变量是当前作用域的局部的：[], [thread]

- `$1..n` String 成功模式匹配中匹配到的各组的内容。在 `"cat"~=(i)/(z)` 中，`$1` 将设置为 `"a"`，`$2` 将设置为 `"t"`。该变量是当前作用域的局部的：[]

- `~` MatchData 一个封装成功模式匹配结果的对象。变量 `$`、`$$` 和 `$1` 均源自 `$-`。赋值给 `-=` 会改变这些变量的值。该变量是当前作用域的局部的：[thread]

此前控制大小不敏感匹配的变量 `=` 已在 Ruby 1.9 中移除。

## 输入/输出变量

- `$` String 输入记录分隔符（默认认为换行符）。这是 `Kernel#gets` 等例方法用于确定记录边界的值。如果设置为 `nil`，`gets` 将读取整个文件。

- `$0` `$` 的别名

- `$$` 附加到每次调用 `Kernel#print` 和 `IO#print` 等方法输出后的字符串。默认值为 `nil`。

- `,` 从 `Kernel#print` 和 `Array#Join` 等方法的参数输出的隔符字符串。默认值为 `nil`，不添加任何文本。

- `$.` Fixnum 当前输入文件的最后一行行号。

- `;` String `String#split` 使用的默认分隔符。可以通过命令行从 `-F` 标志设置。
