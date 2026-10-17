
Then the name is SomeClass

```

我们可以使用这些动态构造的类以有趣的方式扩展 Ruby。例如，这是一个简单的 `Struct` 实现：

```ruby

def MyStruct(*keys)

  Class.new do

    attr_accessor *keys

    def initialize(hash)

      hash.each do |key, value|

        instance_variable_set("@#{key}", value)

      end

    end

  end

end

Person = MyStruct(:name, :address, :likes)

dave = Person.new(name: "davo", address: "TX", likes: "some")

chad = Person.new(name: "chad", likes: "Jazz")

chad.address = "CO"

```

产生：
Dave's name is dave
Chad lives in CO

# instance_eval 和 class_eval

`Object#instance_eval`、`Object#class_eval` 和 `Object#module_eval` 允许 `self` 为任意对象，评估块中的代码，然后重置 `self`：

```ruby

"cat".instance_eval do

  puts "Upper case = #{upcase}"

  puts "Length is #{self.length}"

end

```

产生：
Upper case = CAT
Length is 3

两种形式都接受字符串（但关于评估的危险请见下一页）：

```ruby

"cat".instance_eval("Upper case=#{upcase}, length=#{self.length}")

```

产生：
Upper=CAT, length=3

`class_eval` 和 `instance_eval` 在块的执行期间都会设置 `self`。然而，它们设置环境的方式不同。`class_eval` 像你在类定义中一样设置，因此方法定义的是实例方法：

```ruby

class MyClass

end

MyClass.class_eval do

  def instance_method

    puts "In instance method"

  end

end

```

```ruby

obj = MyClass.new

obj.instance_method

```

产生：
In instance method

相比之下，`instance_eval` 像你在单例类中。因此，你定义的任何方法都成为类方法：

```ruby

class MyClass

end

MyClass.instance_eval do

  def class_method

    puts "In class method"

  end

end

```

```ruby

MyClass.class_method

```

产生：
In class method

# eval 过时了

你可能注意到我们一直在进行大量的元编程——访问实例变量、定义方法和创建类——而我们没有使用 `eval`。这是故意的。在 Ruby 的早期时代，语言缺乏许多这些设施，`eval` 是实现这些效果的唯一方法。但 `eval` 有几个缺点。

首先，它很慢——调用 `eval` 实际上是在执行之前编译字符串中的代码。但甚至，`eval` 也是危险的。如果外部数据（来自应用程序外部的内容）有可能会进入 `eval` 的参数，你就会有一个安全漏洞，外部数据可能包含你的应用程序执行的任意代码。

`eval` 现在被认为是最后的手段。

记住这一点可能有所帮助：在定义方法时，`class_eval` 和 `instance_eval` 的名字完全反了：`class_eval` 定义方法，而 `instance_eval` 定义类方法。你自己想吧。

Ruby 1.9 引入了这些方法的变体。`Object#instance_exec`、`Module#class_exec` 和 `Module#module_exec` 的行为与它们的 `_eval` 对应物相同，但只接受一个块（如果没有接收任何参数的话）。传递给方法的参数作为块参数传递。这是一个重要功能。以前无法将局部变量或实例变量传递到某个 `_eval` 的块中，因为 `self` 会随调用而改变，这些变量超出了作用范围。使用 `_exec` 形式，你现在可以将它们传递进去：

```ruby

animal = "cat"

"".instance_exec(animal) do |other|

  puts "#{other} and #{self}"

end

```

产生：
cat and dog

# instance_eval 和常量

Ruby 1.9 改变了 Ruby 在使用 `instance_eval` 和 `class_eval` 执行块时查找常量的方式。以前，常量是在引用的词法作用域中查找的。在 Ruby 1.9 中，它们现在是在调用 `instance_eval` 的作用域中查找的。这个（人工）示例展示了 Ruby 1.9 的输出：

# INSTANCE_EVAL 和 CLASS_EVAL 408

下载 `samples/classes_45.rb`

```ruby

module One

CONST = "Defined in One"

def self.eval_block(&block)

  instance_eval(&block)

end

module Two

CONST = "Defined in Two"

def self.call_eval_block

  One.eval_block do

    puts CONST

  end

end

Two.call_eval_block

```

产生输出：
Defined in One
在 Ruby 1.8 中，这段代码将打印 Defined in Two。

# instance_eval 与领域特定语言（DSL）

事实证明，`instance_eval` 在某类特定类型的领域特定语言 (DSL) 中起着关键作用。例如，我们可能为绘图编写一个简单的 DSL。为了绘制一组 5x5 的正方形，我们可能会这样写：

```ruby

3.times do

  forward(8)

  pen_down

  4.times do

    forward(4)

    left

  end

  pen_up

end

```

显然，`pen_down`、`forward` 和 `pen_up` 可以实现为方法。为了像这样在没有接收者的情况下调用它们，我们必须位于定义这些方法的类内部（或该类的子类），或者使用 `instance_eval`。我们将定义一个定义这些方法的 `Turtle` 类，还会定义一个 `walk` 方法，它将执行我们的 DSL，以及一个 `draw` 方法来绘制图片：

2. 在绘图系统中，你有一个可以 `forward` n 个正方形、`left` 和 `right` 的 turtle。下了笔，就会画一条线。世界中很少有这些 turtle，所以我们倾向于在内部模拟它们。
3. 是的，`forward(4)` 在代码中是正确的。初始点总是被绘制。

# INSTANCE_EVAL 和 CLASS_EVAL 409

```ruby

class Turtle

  def left; end

  def right; end

  def forward(n); end

  def pen_up; end

  def pen_down; end

  def walk(...); end

  def draw; end

end

```

如果我们正确地实现了 `walk`，那么可以这样写：

```ruby

turtle = Turtle.new

turtle.walk do

  3.times do

    forward(8)

    pen_down

    4.times do

      forward(4)

      left

    end

    pen_up

  end

end

turtle.draw

```

那么，`walk` 的正确实现是什么？我们必须使用 `instance_eval`，因为 DSL 命令需要调用 turtle 对象中的方法。我们还需要将块传递给 `walk` 方法以便由 `instance_eval` 执行。我们的实现如下：

```ruby

def walk(&block)

  instance_eval(&block)

end

```

注意我们将块捕获到一个变量，并在 `instance_eval` 的调用将其展开回块。

turtle 程序的完整列表从 418 页开始。这是 `instance_eval` 的良好用法吗？取决于情况。好处是块内部的代码看起来很简单——你不需要显式指定接收者：

```ruby

4.times do

  forward(4)

  left

end

```

但也有缺点。在块内部，作用域并不是你想象的那样，所以这段代码不起：

```ruby

@size = 4

turtle.walk do

  4.times do

    forward(@size)

    left

  end

end

```

实例变量在 `self` 中查找，而块中的 `self` 与设置实例变量 `@size` 代码中的 `self` 不同。由于这一点，大多数人不再使用这种风格的 instance eval块。

# 回调方法（Hook Methods）

在 400 页的起始部分，我们在 Logger 模块中定义了一个名为 `included` 的方法。当这个模块被包含在一个类时，Ruby 会自动调用它，允许我们向宿类添加方法。

`included` 是回调方法的一个示例（有时称为回调）。回调方法是你编写的、当特定事件发生时由 Ruby 从解释器内部调的方法。解释器通过名称寻找这些方法——如果在正确的上下文中定义了适当的方法，Ruby 将相应事件发生时调用它。

从解释器可以调用的方法在下一页的表 24.1 中。我们在这个章节中不会讨论所有的方法——而是展示几个用法示例。本书的参考部分描述了各个方法，370 页的鸭子类型章节详细讨论了强制转换方法。

## inherited 回调

如果一个类定义了类方法 `inherited`，每当类被子类化时（即当类继承自原始类时），Ruby 都会调用它。

这种回调用于基类需要跟踪其子类的情况。例如，在线商店可能提供多种运输选项。每个选项可以用一个单独的类表示，这些类中的每一个都是 `Shipping` 类的子类。这个父类可以通过记录每个子类的类来跟踪所有各种运输选项。当向用户显示运输选项时，应用程序可以调用基类，请求它的列表：

![](img/44b0533e8e4c9d6926ebd13a65acab0d_409_0.png)

```ruby

class Shipping # 基类

  @children = [] # 该变量在类中而不是实例中

  def self.inherited(child)

    @children << child

  end

  def self.shipping_options(weight, international)

    @children.select { |child| child.can_ship(weight, international)}

  end

end

```

# 表 24.1. Ruby 回调方法

| 类别 | 回调方法 |
| :--- | :--- |
| 方法相关的回调 | method_added, method_missing, method_removed, method_undefined, singleton_method_added, singleton_method_removed, singleton_method_undefined |
| 类和模块相关的回调 | append_features, const_missing, extend_object, included, inherited |
| 对象序列化回调 | marshal_dump, marshal_load |
| 强制转换回调 | coerce, induced_from, to_xxx |

## method_missing 回调

早些我们看到 Ruby 首先在对象的类中调用方法，然后在它的超类中，依此类推。如果在用完所有超类后仍未找到（BasicObject 没有超类），搜索就会停止。内置的 `method_missing` 基本上会抛出一个异常（取决于情况是 NoMethodError 或 NameError）。

在于 `method_missing` 只是一个方法。我们可以在类中重写它以以特定的方式处理未定义的方法。

`method_missing` 签名简单，但许多人用错了：

```ruby

def method_missing(name, *args, &block)

```

`name` 接收未找到的方法。它以符号（symbol）形式传递。`args` 是传递给原始方法的参数数组。经常被忘记的 `block` 参数接收传递给原始方法的任何块。

![](img/44b0533e8e4c9d6926ebd13a65acab0d_411_0.png)

```ruby

def method_missing(name, *args, &block)

  puts "Called #{name} with #{args.inspect} and #{block}"

end

```

执行：
wigble 1, 2
wobble(3, 4) { stuff }

产生输出：
Called with [] and
Called with [1, 2] and
Called with [3, 4] and <Proc:0x03d6d8/tmp/prog.rb:7>

在深入细节之前，有一个提示。人们有两种方法使用每个未定义方法并处理它。第一种更微妙；它拦截所有调用但处理其中一些。在后的情况下，如果你决定不在你的 `method_missing` 实现中处理它，那么将调用转发给子类是重要的：

![](img/44b0533e8e4c9d6926ebd13a65acab0d_411_1.png)

```ruby

class MyClass < OtherClass

  def method_missing(name, *args, &block)

    if <some condition>

      # 处理调用

    else

      super # 否则传递

    end

  end

end

```

如果你没有传递（pass on）你不处理的调用，你的应用程序将静地忽略对类中未知方法的调用。

让我们来看看 `method_missing` 的几种用法。

### 使用 method_missing 模拟访问器（Accessors）

`OpenStruct` 类在 Ruby 中分分发。它允许你编写通过赋值动态创建属性的类。（我们在第 787 页中详细描述了它。）例如，你可以这样写：

```ruby

samples/classes_56.rb

require 'ostruct'

obj = OpenStruct.new(name: "Dave")

obj.address = "Texas"

obj.likes = "Programming"

puts "#{obj.name} lives in #{obj.likes}"

```

产生输出：
Dave likes Texas and Programming

让我们使用 `method_missing` 来编写自己版本的 `OpenStruct`：

```ruby

samples/classes_57.rb

class MyOpenStruct < BasicObject

  def initialize(initial_values = {})

    @values = initial_values

  end

  def singleton_class << self

    class

      self

    end

  end

  def method_missing(name, *args, &block)

    if name == ""

      base_name = name[0..-2].intern

      singleton_class.instance_exec(name) do |name|

        define_method(name) do |value|

        @values[base_name] = value

      end

      @values[base_name] = args[0]

    else

      singleton_class.instance_exec(name) do |name|

        define_method(name) do

        @values[name]

      end

      @values[name]

    end

  end

end

```

产生输出：
Dave Lives in likes and Programming

1.9 注意我们是如何基于 `BasicObject` 构建类的类的，这是 Ruby 1.9 引入的类。`BasicObject` 是 Ruby 对象层次结构的根节点，只包含最少的方法：

```ruby

p BasicObject.instance_methods

```
