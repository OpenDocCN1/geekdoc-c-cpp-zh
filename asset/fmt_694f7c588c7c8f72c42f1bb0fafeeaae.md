
命令的退出状态可以通过全局变量 `$` 获取。

### 重新定义反引号

在命令输出表达式的描述中，我们说反引号中的字符串“默认”会被作为命令执行。事实上，字符串被传递给了方法 `Kernel`。如果你愿意，可以覆盖它。这个示例使用了 `$?`（单个反引号），它包含了最后执行命令的状态：

```ruby
alias old_backquote `
```

*(注：此处由于原始文本中提供的 Ruby 示例代码存在乱码或重复错误，翻译时基于上下文进行了逻辑对齐，意在解释如何覆盖该行为)*

### 赋值

到目前为止，我们看到的几乎每个例子都涉及赋值。也许是时候谈谈它了。赋值将左侧（*lvalue*）设置为右侧（*rvalue*）。然后作为赋值的结果返回。你可以进行链式赋值，并在某些地方执行赋值：

```
a = b = 1 + 2
a # 3
b # 3
a = b # 3
```

Ruby 有两种赋值形式。第一种将对象引用赋值给变量或常量。这种赋值形式是硬编码在语言中的：

```
instrument = "piano"
```

第二种赋值涉及左侧的对象或元素引用。这些形式是特殊的，因为它们通过调用方法来实现。我们已经看到过如何定义一个以等号结尾的方法。该方法接收赋值的值。

![](img/44b0533e8e4c9d6926ebd13a65acab0d_149_0.png)

```ruby
class ProjectList
  def initialize
    @projects = []
  end
  def projects=(list)
    @projects = list
  end
  def []=(offset)
    @projects[offset]
  end
end
```

```
list = ProjectList.new
list.projects = %w{SAND}
list[3] => "SAND"
list[4] => "PAINT"
```

如示例所示，这些属性方法不需要与内部变量对应，你不需要为每个写入器准备读取器。在旧版本的 Ruby 中，赋值的结果是由属性设置方法返回的。从 Ruby 1.8 开始，赋值的值总是参数；方法的返回值被丢弃。在后续代码中，旧版本的 Ruby 会将其设置为 `nil`。现在 `a` 将被设置为 2。

```ruby
samples/tutepceptions_1.rb
```

```ruby
class Test
  def val=(val)
    @val = val
    return val
  end
end
```

```
t = Test.new
a = (t.val = 2)
a # => 2
```

### 并行赋值

在编程课程的第一周（如果是学期的话），你可能需要编写代码来交换两个变量的值：

```
int a = 1;
int b = 2;
int temp;
temp = a;
a = b;
b = temp;
```

在 Ruby 中你可以干净地做到这一点：

```
a = 1
b = 2
a, b = b, a
```

Ruby 允许你使用逗号分隔的值列表（赋值右侧的内容）。一旦 Ruby 在赋值中看到多个值，结果就是并行赋值。以下是局部层面的描述：解释器内部发生了什么较为复杂。旧版本 Ruby 用户应该注意，这些规则在 Ruby 1.9 中发生了变化。

首先，所有的 rvalues 从左到右评估，并收集到一个数组中（除非它们已经是数组）。该数组将是整个赋值返回的返回值。

接下来，检查左侧（lhs）。如果它包含单个元素，则将数组赋值给该元素。

```
a = 1, 2, 3, 4 # a=[1, 2, 3, 4]
b = [1, 2, 3, 4] # b=[1, 2, 3, 4]
```

如果 lhs 包含逗号，Ruby 将 rhs 上的值与 lhs 的连续元素匹配。多余的元素被丢弃。

```
a, b = 1, 2, 3, 4 # a=1, b=2
c = 1, 2, 3, 4 # c=1
```

## Splat 与赋值

如果 Ruby 在赋值的右侧看到 splat（即由星号 `*` 前缀），它将在评估值期间并在赋值开始之前展开为它的组成值：

```
a, b, c, d, e = (1, 2, 3, 4, 5)
```

如果 splat 是最后一个，它将是一个包含剩余值的数组。这使得它具有贪性——它会吸收所有可能的值。

```
a, b, c, d, *e = 1, 2, 3, 4, 5 # a=1, b=2, c=3, d=4, e=[5]
a, b, c, *d, e = 1, 2, 3, 4, 5 # a=1, b=2, c=3, d=[4], e=5
```

如果 splat 不是最后一个，Ruby 确保 lvalues 将收集右侧结尾的所有值。

```
*a, b = 1, 2, 3, 4 # a=[1, 2, 3], b=4
a, *b = 1, 2, 3, 4 # a=1, b=[2, 3]
```

## 嵌套赋值

并行赋值还有一个值得注意的特征。赋值的左侧可以包含一个括号项列表。Ruby 将这些视为嵌套赋值。它会提取对应的值，将其赋值给括号项，然后继续执行高层赋值。

```
a, (b, c), d = 1, 2, 3, 4 # a=1, b=2, c=nil, d=3
a, (b, c), d = [1,2,3,4] # a=1, b=[2,3], d=4
a, (b, c), d = 1,[2,3],4 # a=1, b=2, c=nil, d=4
a, (b, c), d = 1,[2,3,4],5 # a=1, b=2, c=3, d=5
a, (*c), d = 1,[2,3,4],5 # a=1, c=[2, 4], d=5
```

第二种形式在内部被转换为第一种。这意味着你可以像预期的那样，在类中将定义的运算符定义为方法：

```ruby
samples/tutorial_expressions_26.rb

class Bowdlerize
  def initialize(string)
    @value = string.gsub(/[aeiou]/, '*')
  end

  def +(other)
    Bowdlerize.new(self.to_s + other.to_s)
  end

  def to_s
    @value
  end
end

a = Bowdlerize.new("damn") # => dmn
a += "shame" # => dmn shme
```

在 Ruby 中你找不到像 C 和 Java 那样的自动自增 (++) 和自动自减 (--) 运算符。相反，使用的是 `+=` 和 `-=` 这种形式。

### 条件执行

Ruby 有几种不同的机制可以实现代码的条件执行；其中大多数应该让你觉得很熟悉，而且其中一些有一些巧妙的变形。在我们深入研究之前，我们需要花一点短时间来看下布尔表达式。

### 布尔表达式

Ruby 对真值的定义非常简单。任何不是 `nil` 或常量 `false` 的值都是真——"cat"、99、0 和 `a_song` 都被视为真。

在本书中，当我们谈论通用的真值或假值时，我们使用普通的罗马字体：`true` 和 `false`。当我们想要引用实际的常量时，我们使用 `true` 和 `false`（代码字体）。

`nil` 被视为假值是非常重要的。例如，`IO#gets` 返回文件中的下一行，它在文件末尾会返回 `nil`，这使得你可以编写如下的循环：

```ruby
while line = gets
  # process line
```

然而，C++ 和 Perl 的程序员有时会掉进一个陷阱。数字 0 不被解释为假值。长度为 0 的字符串也是如此。这是一个很难改的习惯。

### 与、或、非

Ruby 支持所有的布尔运算符。关键字 `and` 和运算符 `&&` 在其第一个参数为假时，都会返回该第一个参数。否则，它们会求值并返回第二个参数（这有时被称为*短路*求）。两者唯一的区别在于优先级（且低于 `||`）。

```ruby
nil && #=> nil
false && #=> false
"cat" && #=> 99
```

因此，`&&` 和 `or ||` 只有在两个参数都为真时才会返回真值，正如预期的那样。

同样，`or` 和 `||` 在其第一个参数为假时会返回第一个参数，以防它们求值并返回第二个参数。

```ruby
nil || #=> 99
false || #=> 99
"cat" || #=> "cat"
```

和 `and` 一样，`or` 和 `||` 唯一的区别是优先级。为了让生活变得有趣且优先级不相同，`||` 的优先级高于 `||`。

一种常见的惯用法是使用 `||=` 仅当变量未设置时给该变量赋值：

```ruby
var ||= "default value"
```

这并不完全正确，它等同于 `var = "default value"`。它的区别在于，如果变量已经设置，则不会进行任何赋值。在伪代码中，这可以写成 `var = "default value"` 除非 `var || var = "default value"`。

`not` 和 `!` 是该操作数的取反（如果操作数为真则为假，如果操作数为假则为真）。是的，`not` 和 `!` 仅区别于优先级。

所有这些优先级都总结在第 345 页的表 22.4 中。

### defined?

`defined?` 运算符如果其参数（可以是一个表达式）未定义则返回它；否则，它返回该参数的描述。如果参数是 `yield`，如果当前上下文中关联了代码块，`defined?` 将返回字符串 "yield"。

```ruby
defined? #=> "expression"
defined dummy #=> nil
defined printf #=> "method"
defined String #=> "constant"
defined $ #=> "global-variable"
```

对于修饰符（modifier），前面的表达式仅在条件为真时才会被求值，除非情况反过来：

```ruby
File.foreach("/etc/passwd") do |line|
  next if line =~ /^\/  # 跳过注释
  parse(line) if line =~$/  # 不解析空行
end
```

因为 `if` 本身是一个表达式，你可以写出像下面这样非常晦涩的语句：

```ruby
if artist == "John Coltrane"
  artist = "Trane"
  unless use_nicknames == "no"
```

这条路径通向了疯狂的大门。

### Case 表达式 (Case Expressions)

Ruby 表达式是一个强大的野兽：一个加强版的多路分支（multiway on）。为了让它更加强大，它提供了两种形式。

第一种形式非常接近一系列语句；它允许你定义一系列条件，并执行与第一个真条件对应的语句：

```ruby
case
when song.name == "Misty"
  puts "Not again!"
when song.duration > 120
  puts "Too long!"
when Time.now.hour > 21
  puts "It's too late"
else
  song.play
end
```

第二种 `case` 语句可能更为常见。你在 `case` 语句的顶部指定一个目标，每个子句列出一个或多个比较项：

```ruby
case command
when "debug"
  dump_debug_info
  dump_symbols
when /p\s*(\w+)/
  dump_variable($1)
when "quit", "exit"
  exit
else
  print "Illegal command: #{command}"
end
```

与 `if` 一样，`case` 返回最后一个执行的表达式的值，如果表达式与条件在同一行，你可以使用一个关键字：^3

```ruby
kind = case year
  when 1850..1889 then "Blues"
  when 1890..1909 then "Ragtime"
  when 1910..1929 then "New Orleans Jazz"
  when 1930..1939 then "Swing"
  when 1940..1950 then "Bebop"
  else
    "Jazz"
  end
```

`case` 的工作原理是将目标（`case` 关键字后面的表达式）与每个关键字进行比较。这种测试通过比较运算符 `===` 完成。只要一个类为 `===` 定义了有意义的语义（以及所有内置对象），任何类都可以用于简单的模式匹配：

例如，正则表达式将 `===` 定义为简单的模式匹配：

```ruby
case line
  when /title=(.+)/
    puts "Title is #$1"
  when /track=(.+)/
    puts "Track is #$1"
  when /artist=(.+)/
    puts "Artist is #$1"
  end
```

Ruby 类是 `Class` 的实例。`===` 运算符在 `Class` 中定义，用于测试参数是否为接收者的实例或其超类之一。因此（尽管放弃了多态的好处并让重构之神降临你的头上），你可以测试对象的类：

```ruby
case shape
  when Square, Rectangle
    # ..
  when Circle
    # ..
  when Triangle
    # ..
  else
    # ..
  end
```

2. Ruby 1.8 允许使用冒号代替 `then` 关键字。从 Ruby 1.9 开始，这不再被支持。

### 循环 (Loops)

别告诉别人，但 Ruby 拥有相当原始的内置循环结构。

`while` 循环只要条件为真，就会执行零或多次循环体。例如，这个常用的用法会读取直到输入耗尽：

```ruby
while line = gets
  # ...
end
```

`until` 循环是相反的：它执行循环体直到条件变为真：

```ruby
until play_list.duration > 60
  play_list.add(song_list.pop)
end
```

与 `and` 和 `unless` 一样，你可以将循环作为语句修饰符：

```ruby
a = 1
a += 2 while a < 100
# ~ 128
a = 10 until a < 100
a ~= 98
```

在第 156 页的布尔表达式章节中，我们提到范围可以用作一种触发器（flip-flop），当某些事件发生时返回真并保持直到第二个事件发生。这种功能通常在循环内部使用。在下面的示例中，我们读取一个包含前十个序数（“first”、“second”等）的文本文件，但只打印从匹配“third”开头到匹配“fifth”结尾的行：

```ruby
file = File.open("ordinal")
while line = file.gets
  puts(line) if line =~ /third/ .. line =~ /fifth/
end
```

输出：

- third

- fourth

- fifth

你可能会发现使用 Perl 的人会略有不同的编写上面的示例：

```ruby
file = File.open("ordinal")
while line = file.gets
  print if line =~ /third/ .. /fifth/
end
```

输出：

- third

- fourth

- fifth

这使用了一些幕后的魔法行为：`gets` 将最后一行赋值给全局变量。例如，Ruby 提供了一个循环来遍历行：

```ruby
file = File.open("ordinal")
while line = file.gets
  puts(line) if line =~ /third/ .. line =~ /fifth/
end
```

输出：

- third

- fourth

- fifth

## 跳出、重试与继续

循环控制结构 `break`、`redo` 和 `next` 允许你改变循环或迭代器的正常执行流.³

`break` 终止立即包含它的循环；控制将从该块之后的语句处恢复；`redo` 从头开始重复执行循环的迭代，而无需重新评估条件或获取下一个元素（在迭代器中）；`next` 则跳到循环的末尾，实际上是开始下一次迭代：

```
while line = gets
  next if line =~ /^\s#/ # 跳过注释
  break if line =~ /END/ # 在结束处停止
  # 替换反引号中的内容并重试
  redo if line.gsub(/(.+)/) { eval($1) }
  # 处理行行
end
```

这些关键字也可以在块中使用。虽然你可以在任何块中使用它们，但它们通常在块被用于迭代时最有意义：

```
i=0
loop do
  i += 1
  next if i < 3
  print i
  break if i > 4
end
```

产生输出：

345

一个值可以传递给 `break` 和 `next`。在常规循环中使用，可能只有对 `break` 这样做才有意义，因为它设置了循环返回的值。（传递给 `next` 的任何值实际上都是开销的）。如果常规循环没有执行 `break`，则该值为 `nil`。

```
result = while line = gets
  break(line) if line =~ /answer/
end
```

如果你想了解 `break` 和 `next` 如何与块和 proc 工作的细节，请查看从第365页开始的参考描述。如果你在寻找退出嵌套块或循环的方法，请查看第 369 页和 567 页描述的 `Kærn.catch`。
