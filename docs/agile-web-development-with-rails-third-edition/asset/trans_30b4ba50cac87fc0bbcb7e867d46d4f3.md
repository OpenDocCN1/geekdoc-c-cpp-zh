

通过在我们自己的控制器中重写 `local_request?` 方法，可以将其视为本地请求。

与其编写我们自己的自定义恢复机制，我们可能希望查看异常通知插件，以便在应用程序中抛出异常时设置向支持人员发送电子邮件的方式。使用以下命令安装：

```
depot> ruby script/plugin install git://github.com/rails/exception_notification.git
```

然后我们在应用程序控制器中添加以下内容：

```
class ApplicationController < ActionController::Base
  include ExceptionNotifiable
  # ...
```

然后在我们的 `environment.rb` 文件中设置接收通知电子邮件的人员列表：

```
ExceptionNotifier.exception_recipients =
%w(support@my-org.com dave@cell-phone.company)
```

我们需要确保 Action Mailer 已配置为发送电子邮件，如第 609 页开始所述。

## 28.7 迈向发布及以后

一旦我们设置了初始部署，我们就可以完成应用程序的开发并将其发布到生产环境。我们可能会设置额外的部署服务器，而从第一次部署中学到的经验将告诉我们如何构建后续部署。例如，我们可能会发现 Rails 是我们系统中最慢的组件之一——请求时间中大部分花费在 Rails 上，而非等待数据库或文件系统。这表明扩展的方法是添加机器来分摊 Rails 的负载。

然而，我们可能会发现请求花费的大部分时间在数据库上。如果是这种情况，我们需要查看如何优化数据库活动。也许我们需要改变访问数据的方式。或者也许我们需要自定义制作一些 SQL 来替换默认的 Active Record 行为。

有一点是肯定的：每个应用程序在其生命周期中都需要不同的调整。最重要的活动是随着时间的推移倾听它并发现需要做什么。我们的工作在发布应用程序时并没有结束。它实际上才刚刚开始。

如果您最终想要探索替代部署选项，您可以在《Deploying Rails Applications: A Step-by-Step Guide [ZT08]》中找到大量好的建议。

最后，我们可以简化此方法。Ruby 方法返回的值是最后一个求值的表达式的值，因此我们可以完全去掉临时变量和 return 语句：

```
def say_goodnight(name)
"Good night, #{name.capitalize}"
end
puts say_goodnight('ma')
```

## A.4 类

这是一个 Ruby 类定义：

```
class Order < ActiveRecord::Base
  has_many :line_items
  def self.find_all_unpaid
    find(:all, 'paid = 0')
  end
  def total
    sum = 0
    line_items.each {|li| sum += li.total}
  end
end
```

类定义以关键字 class 开头，后跟类名（必须以大写字母开头）。此 Order 类被定义为 ActiveRecord 模块中 Base 类的子类。

Rails 大量使用类级声明。这里的 has_many 是 Active Record 定义的方法。它在 Order 类被定义时被调用。通常这类方法对类做出断言，因此在本书中我们称它们为声明。

在类体内部，您可以定义类方法和实例方法。用 self. 前缀方法名（如第 5 行所示）使其成为类方法；它可以在类上调用。在这种情况下，我们可以在应用程序中的任何位置进行以下调用：

```
to_collect = Order.find_all_unpaid
```

常规方法定义创建实例方法（如第 9 行的 total 定义）。这些方法在类的对象上调用。在以下示例中，变量 order 引用一个 Order 对象。我们在前面的类定义中定义了 total 方法。

```
puts "The total is #{order.total}"
```

注意 find_all_unpaid 和 total 方法之间的区别。第一个不特定于某个订单，因此我们在类级别定义它并通过类本身调用它。第二个适用于一个订单，因此我们将其定义为实例方法并在特定的订单对象上调用它。

类的对象在其 *实例变量* 中保存状态。这些变量名都以 @ 开头，可供类的所有实例方法使用。每个对象都有自己的一组实例变量。

```
class Greeter
  def initialize(name)
    @name = name
  end
  def say(phrase)
    puts "#{phrase}, #{@name}"
  end
end

g1 = Greeter.new("Fred")
g2 = Greeter.new("Wilma")

g1.say("Hello")     #=> Hello, Fred
g2.say("Hi")        #=> Hi, Wilma
```

实例变量在类外部不能直接访问。要使其可用，请编写返回其值的方法：

```
class Greeter
  def initialize(name)
    @name = name
  end

  def name
    @name
  end

  def name=(new_name)
    @name = new_name
  end
end

g = Greeter.new("Barney")
puts g.name   #=> Barney
g.name = "Betty"
puts g.name   #=> Betty
```

Ruby 提供了便捷方法为您编写这些访问器方法（这对厌倦编写所有那些 getter 和 setter 的人来说是个好消息）：

```
class Greeter
  attr_accessor :name      # create reader and writer methods
  attr_reader   :greeting  # create reader only
  attr_writer   :age       # create writer only
```

### 私有和受保护

类的实例方法默认是公开的；任何人都可以调用它们。您可能希望对此进行覆盖，以用于仅打算由其他类实例方法使用的情况：

```
class MyClass
  def m1      # this method is public
  end

  protected

  def m2      # this method is protected
  end

  private

  def m3      # this method is private
  end
end
```

private 指令是最严格的；私有方法只能从同一实例内部调用。受保护方法既可以在同一实例中调用，也可由同一类的其他实例及其子类调用。

## A.5 模块

模块与类相似，因为它们包含一组方法、常量以及其他模块和类定义。与类不同，您不能基于模块创建对象。

模块有两个用途。首先，它们充当命名空间，让您可以定义方法名不会与其他地方定义的方法冲突。其次，它们允许您在类之间共享功能——如果一个类混入一个模块，该模块的实例方法就变得可用，就好像它们是在类中定义的一样。多个类可以混入同一个模块，共享模块的功能而无需使用继承。您还可以将多个模块混入单个类。

Rails 大量使用模块。例如，辅助方法是在模块中编写的。Rails 会自动将这些辅助模块混入适当的视图模板中。例如，如果您想编写一个可在 store 控制器调用的视图中调用的辅助方法，您可以在 app/helpers 目录中的 store_helper.rb 文件中定义以下模块：

```
module StoreHelper
  def capitalize_words(string)
    string.gsub(/\b\w/) { $&.upcase }
  end
end
```

## A.6 数组和哈希

Ruby 的数组和哈希都是索引集合。两者都存储可通过键访问的对象集合。对于数组，键是整数，而哈希支持任何对象作为键。数组和哈希在需要容纳新元素时会按需增长。访问数组元素更高效，但哈希提供更大的灵活性。任何特定的数组或哈希都可以保存不同类型的对象；例如，您可以有一个包含整数、字符串和浮点数的数组。

您可以使用数组字面量——方括号之间的一组元素——创建并初始化新的数组对象。给定一个数组对象，您可以通过在方括号之间提供索引来访问单个元素，如下一个示例所示。Ruby 数组索引从零开始。

```
a = [ 1, 'cat', 3.14 ]    # array with three elements
a[0]                    # access the first element (1)
a[2] = nil              # set the third element
                        # array now [ 1, 'cat', nil ]
```

您可能已经注意到我们在本示例中使用了特殊值 nil。在许多语言中，nil（或 null）的概念意味着“无对象”。在 Ruby 中并非如此；nil 是一个对象，就像其他对象一样，只是恰好代表 nothing。

方法 << 通常与数组一起使用。它将值附加到其接收者。

```
ages = []
for person in @people
  ages << person.age
end
```

Ruby 有一个创建单词数组的快捷方式：

```
a = [ 'ant', 'bee', 'cat', 'dog', 'elk' ]
# this is the same:
a = %w{ ant bee cat dog elk }
```

Ruby 哈希与数组类似。哈希字面量使用大括号而不是方括号。字面量必须为每个条目提供两个对象：一个作为键，另一个作为值。例如，您可能想将乐器映射到其管弦乐队声部：

```
inst_section = {
  :cello    => 'string',
  :clarinet => 'woodwind',
  :drum     => 'percussion',
  :oboe     => 'woodwind',
  :trumpet  => 'brass',
  :violin   => 'string'
}
```
