
# 无论 obj 是 Fixnum 还是罗马数字，转换仍然成功

`num = obj.to_int`

### Symbol.to_proc 技巧

Ruby 1.9 在每个元素上调用 `to_proc` 来创建一个 Proc。如果你想将字符串数组转换为大写，你可以这样写：

```
names = [...]
result = names.map {|name| name.to_s}
```

这很疯狂对吧？但从 Ruby 1.9 开始，你可以这样写：

```
names = [...]
result = names.map(&:to_s)
```

## 标准协议与强制转换

现在很简洁了：`to_s` 方法处理 `names` 的每个元素。它是如何工作的？它依赖于 Ruby 的强制转换。让我们从顶部开始。当你说 `names.map(&xxx)` 时，你是在告诉 Ruby 在 `map` 方法中传递一个块。如果 `xxx` 已经是一个 Proc 对象，Ruby 会尝试通过调用 `to_proc` 将其转换为一个。如果用 Ruby 编写，它看起来是这样：

```
def to_upcase
  proc { |obj, *args| obj.send(self, *args) }
end
```

此方法创建一个 Proc，在对象上调用它时会发送。所以，当 `names.map(&upcase)` 开始迭代 `names` 中的字符串时，它将调用该块并调用它的 `upcase`。这是一种非常优雅的强制转换用法。然而，这也是代价的。动态方法调用意味着除非在性能关键区域，否则我们的 `upcase` 版本速度只有一半。

## 数字强制转换

回到第376页，我们说解释器执行了三种转换。我们涵盖了宽松转换和严格转换。第三种是数字转换。问题在这里：当你写 `1+2` 时，Ruby 会在对象 `1` (`Fixnum`) 上调用 `+`，并将 `Fixnum 2` 作为参数。然而，当你写 `1+2.3` 时，相同的方法返回了一个 `Float` 对象。它如何知道该做什么（特别是根据鸭子类型检查参数的类）？

答案在于 Ruby 的强制转换协议，基于 `coerce` 方法。强制转换的基本操作是简单的：它接收两个数字（一个作为接收者，另一个作为参数）。它返回一个包含这两个数字表示的数组（参数在前），然后是接收者。`coerce` 方法保证这两个对象具有相同的类，因此可以相加（或相乘、除法或减法）。

```
1.coerce(2)      => [2, 1]
1.coerce(2.3)    => [2.3, 1.0]
(4.5).coerce(2.3) => [2.3, 4.5]
(4.5).coerce(2)   => [2.0, 4.5]
```

技巧在于接收者调用其参数的 `coerce` 方法来生成这个数组。这种技术被称为双重调度（double dispatch），允许方法不仅根据其类，还根据参数的类来改变行为。在这种情况下，我们让参数来决定具体哪些对象被相加（或相乘、除法等）。

假设我们正在编写一个旨在参与算术的类。为了参与强制转换，我们需要实现一个 `coerce` 方法。它接收其他类型的数字作为参数，并返回两个相同类的对象，其值等于它的参数和自身。

对于我们的罗马数字类，这相当容易。内部，每个罗马数字对象在实例 `@value` 中以 `Fixnum` 存储真实值。`coerce` 方法检查参数的类是否为 `Integer`。如果是，它返回参数和它的内部值。如果不是，它将两者都转换为浮点数。

`img/44b0533e8e4c9d926ebd13a65acab0d_380_0.png`

```
class Roman
  def initialize(value)
    @value = value
  end
  def coerce(other)
    if Integer == other
      [ other,@value ]
    else
      [ Float(other), Float(@value) ]
    end
  end
end
```

```
# .. 其他内容
end
iv = Roman.new(4)
xi = Roman.new(11)
3 * iv => 12
1.1 + xi => 12.1
```

当然，实现的罗马数字不知道如何做加法。你无法在上一个例子中写 `xi+3`，因为罗马数字没有 `+` 方法。而它可能应该有的。但让我们疯狂一下，为罗马数字实现它：

`img/44b0533e8e4c9d6926ebd13a65acab0d_380_1.png`

```ruby
class Roman
MAX_ROMAN = 4999
  attr_reader :value
  protected :value
  def initialize(value)
    if value <= 0 || value > MAX_ROMAN
      fail "罗马值必须大于 0 且小于 #{MAX_ROMAN}"
    end
    @value = value
  end
end
```

```ruby
def coerce(other)
  if Integer === other
    [ other, @value]
  else
    [ Float(other), Float(@value) ]
  end
end
def nd +(other)
  if Roman === other
    other = other.value
  end
  if Fixnum === other && (@ + @value) < MAX_ROMAN
    Roman.new(@value) + other
  else
    x, y = other.coerce(@value)
    x + y
  end
end
```

```ruby
FACTORS = [["cm", 1000], ["cm", 900], ["d", ["cd", 400], ["c", 100], ["xc", 90], ["l", 50], ["xl", 40], ["x", 10], ["ix", 9], ["v", 5], ["iv", 4], ["i", 11]]]
```

```ruby
def to_s
  value = @value
  roman = ""
  for code, factor in FACTORS
    count, value = value.divmod(factor)
    roman << (code * count)
  end
  roman
end
```

![](img/44b0533e8e4c9d6926ebd13a65acab0d_381_0.png)

```ruby
iv = Roman.new(4)
xi = Roman.new(11)
iv + 3 # => vii
iv + 4 # => xi
iv + 3.14159 # => 7.14159
xi + 4900 # => mmmcmxi
xi + 4990 # => 5001
```

最后，请注意类型转换——始终尝试向更通用的类型转换。这是一种 A 尝试转换为 B，而 B 又尝试转换回 A 的情况。

# 知行合一 (Walk the Walk)

鸭子类型（Duck typing）可能会引发争议。邮件列表上偶尔会爆发激烈争论，或者有人会写支持或反对该概念的博客。这些讨论的许多参与者其实都持有着相当极端的立场。

但归结底来，鸭子类型并不是一套规则；它仅仅是一种编程风格。设计你的程序以在多疑和灵活性之间取得平衡。如果你觉得需要限制方法用户传入的对象类型，问问自己为什么。尝试确定如果你期望得到一个 String 却得到一个 Array，会发生什么错误。有时候，这种差异至关重要。但通常情况下，并非如此。尝试在一段时间内采取更宽松的立场，看看是否会发生坏事。如果没有，也许鸭子类型并不仅仅是给鸟类（玩笑）准备的。

# 第 24 章

## 元编程 (Metaprogramming)

雅quard 织机发明于 200 多年前，它是第一个使用打孔片控制的设备——每张卡片上的孔列用于控制织入织物的图案。但想象一下，如果织织机不仅能织布料，还能打出更多的卡片，而且这些卡片可以反馈回机制中。机器可以决定创建它可以执行的新程序。这就是元编程——编写编写代码的代码。

编程的核心在于构建抽象层。当你解决问题时，你正在构建从冷酷机械的硅片世界通往我们所处的模糊且流动的世界的桥梁。某些编程语言——如 C——非常接近机器。C 到应用领域之间的距离可能很大。其他语言——也许是 Ruby——提供了更高层次的抽象，让你从更接近目标领域的地方开始。正因如此，大多数人认为高层语言是应用开发的更好起点（尽管他们会为语言的选择争论不休）。

但当你进行元编程时，你不再受限于编程语言中构建的抽象集。实际上，你正在创建一种新的、领域特定的编程语言——一种能让你表达解决特定问题时所需的概念的语言。

Ruby 让元编程变得简单。结果，大多数高级 Ruby 程序员都会使用元编程技术来简化代码。本章将展示他们是如何做到的。它的目的并不是对元编程技术的详尽调查。相反，我们将观察使元编程可能的 Ruby 底层原理。从那里，你将能够发明自己的元编程范式。

### 对象与类

类和对象显然是 Ruby 的核心，但乍看之下可能会让人困惑。似乎有很多概念：类、对象、类对象、实例方法，

1. 如果在耗尽对象的类层次结构后仍找不到方法，Ruby 会在原始接收者上查找调用的 `method_missing`，从 `self` 的类开始，然后向上查找超链。

```ruby
def two
  puts @var
end
t = Test.new
t.one
```

产生：
99

倒数第二行的 `Test.new` 调用创建了一个新的 `Test` 对象，并将该对象赋值给变量 `t`。在下一行，我们调用了方法 `t.one`。为了执行此调用，Ruby 将 `self` 设置为 `t`，然后在 `t` 的类中查找该方法。Ruby 找到了在第 2 行定义的方法并调用它。

在方法内部，我们将实例变量 `@var` 设置为 99。这个实例变量将与当前对象关联。那个对象是什么？嗯，`t.one` 的调用将 `self` 设置为 `t`，因此在方法内部，`self` 将是……

（注：后部分提供的 OCR 文本在 384-386 页存在严重的乱码/重复。我已经根据提供的片段处理了连贯部分并清理了逻辑流。）

![](img/44b0533e8e4c9d6926ebd13a65acab0d_388_0.png)

### 单例与类

早些时候提到，在类定义内部，`self` 被设置为正在定义的类对象。事实证明，这是 Ruby 对象模型中最优雅的特性之一的基础。

回想一下在 Ruby 中，我们可以使用 `def self.xxx` 或 `def ClassName.xxx` 两种形式来定义类方法：

`samples/classes_6.rb`

```ruby
class Dave
  def self.class_method_one
    puts "Class method one"
  end
  def Dave.class_method_two
    puts "Class method two"
  end
  Dave.class_method_one
  Dave.class_method_two
end
```

产生：

Class method one
Class method two

现在我们知道为什么两种形式是等等的：在类定义内部，`self` 被设置为 Dave。

但既然我们已经看了单例方法，我们也知道，实际上在 Ruby 中并没有所谓的“类方法”。之前的两种定义都是在类对象上定义单例方法。与所有其他单例方法一样，我们可以通过对象（在这种情况下是类 Dave）来调用它们。

在 `Dave` 类中创建单例方法之前，类对象中的指针指向 `Class`。（这句话听起来很困惑。另一种说法是“Dave 是一个类，所以 Dave 是类”，但这也很困惑。）情况如下一页的图 24.3 所示。

定义方法后 Dave 类的对象图如图 24.4 所示。你看到单例类是如何创建的了吗，就像动物示例中一样？该类被插入为 Dave 的类，而 Dave 的原始类变成了这个新类的父。

我们现在可以将 `self` 的两种用法（即当前对象）联系起来。我们讨论过如何在 `self` 中查找实例变量，也讨论过在 `self` 上定义的单例方法是如何变成类方法的。让我们利用这些来访问类对象的实例变量：

```ruby
samples/classes_7.rb
class Test
  @var = 99
  def self.var
    @var
  end
  def self.var=(value)
    @var = value
  end
  puts "Original value = #{Test.var}"
  Test.var = "cat"
  puts "New value = #{Test.var}"
end
```

产生：

Original value = 99
New value = cat

Ruby 初学者经常犯在类定义中内联设置实例的错误（正如我们在之前的代码中对 `@var` 所做的），并尝试从实例方法访问这些变量。正如代码所示，这是不通的，因为在类体中定义的实例变量与类对象相关，而不是与类的实例。

## 访问单例类的另一种方法

我们已经看到通过在方法定义中使用类似 `def animal.speak` 的方式添加对象引用，你可以在对象的单例类中创建方法。

你可以使用 Ruby 的 `class << an_object` 语法来实现同样的操作：

### 图 24.3. 基本类定义

![](img/44b0533e8e4c9d6926ebd13a65acab0d_390_0.png)

下载 `samples/classes_8.rb`

```ruby
animal = "dog"
class << animal
  def speak
    puts "The #{self} says WOOF!"
  end
end
animal.speak
```

产生：

The dog says WOOF!

在这种类的类定义内部，`self` 被设置为给定对象的单例类（在本例中为 `animal`）。因为类定义返回执行体中最后执行的语句的值，我们可以利用这一事实获取单例类对象：

```ruby
samples/classes_9.rb
animal = "dog"
def animal.speak
  puts "The #{self} says WOOF!"
end
singleton = class << animal
  def lie
    puts "The #{self} lies down"
  end
  self # 返回单例类对象
end
```

### 图 24.4. 带有类方法的类

![](img/44b0533e8e4c9d6926ebd13a65acab0d_391_0.png)

产生：
The dog says WOOF!
The dog lies down

单例类对象是 #<Class:String:0x0a36d8>
它定义了方法 [:speak, :lie]

注意 Ruby 用于表示单例类的符号表示：#<Class:#<String...>>。Ruby 会阻止你在其原始对象的语境之外使用单例类。例如，你不能创建一个单例类的新实例：

```ruby
### samples/classes_10.rb
singleton = class << "cat"; self; end
singleton.new
```

产生：

```
prog.rb:2in 'new': can't create instance of singleton class (TypeError)
from /tmp/prog.rb:2in <main>
```

让我们把关于实例变量、`self` 和单例类的知识联系起来。回到第 390 页，我们编写了类级方法以便让我们能够获取和设置实例变量。通常情况下，实例变量与实例相关，但当我们在类体中定义它们时，它们就与类对象本身相关。让我们利用这些来访问类对象的实例变量：

```ruby
samples/classes_7.rb
class Test
  @var = 99
  def self.var
    @var
  end
  def self.var=(value)
    @var = value
  end
  puts "Original value = #{Test.var}"
  Test.var = "cat"
  puts "New value = #{Test.var}"
end
```
