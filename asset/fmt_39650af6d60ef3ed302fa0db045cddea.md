
```ruby
module Mod
def hello
  "Hello from Mod.\n"
end

class Klass
def hello
  "Hello from Class.\n"
end
```
```ruby
k = Klass.new
k.hello => "Hello from Class.\n"
k.extend(Mod) => <Klass:0x0000000146539d8>
k.hello => "Hello from Mod.\n"
```

写入 `obj.extend(Mod)` 基本等同于以下内容：

```ruby
class <<obj
include Mod
end
```

## freeze

防止对 `obj` 的修改。如果尝试修改，将抛出 `RuntimeError`。你无法取消冻结对象。另见 `Object#frozen?`

```ruby
a = [ "a", "b", "c" ]
a.freeze
a << "z"
```

产生：

```
prog.rb:3:in=`main>` can't modify frozen array (RuntimeError)
```

## 是否冻结?

返回 `obj` 的冻结状态。

```ruby
a = [ "a", "b", "c" ]
a.freeze #=> "a", "b", "c"
a.frozen? #=> true
```

## hash

为此对象生成 `Hash` 值。此函数必须具有属性 `a.eq?(b)` 意味着 `a.hash==b.hash`。`Hash` 值被 `Hash` 类使用。任何超过 `Fixnum` 容量的 hash 值在使用前会被截断。对于 `Object` 实例，`hash` 也是 `object_id`。对于子类来说并不总是如此。

## _id

`Object#object_id` 的同义词。

## initialize_copy

`Object#dup` 和 `Object#clone` 使用的协议的一部分，`initialize_copy` 作为回调被调用，应该拷贝任何 `dup` 和 `clone` 无法拷贝的状态信息。例如，在下面的代码中，`a` 和 `b` du 了容器类的实例，每个共享同一个对象：

```ruby
class Container
  attr_accessor :content
end
a = Container.new
a.content = "cat"
b = a.dup
b.content[1..-1] = "anary"
a.content #=> "canary"
b.content #=> "canary"
```

下一个示例使用 `initialize_copy` 在复制的 `Hash` 中创建一个新字符串。

# class Container

```ruby
class Container
  attr_accessor :content
  def initialize_copy(other)
    @content = String.new(other.content)
  end
  end
  a = Container.new
  a.content = "cat"
  b = a.dup
  a.content[1.-1] = "canary"
  a.content # => "canary"
  b.content # => "cat"
```

```ruby
obj.inspect -> string
```

# inspect

返回一个包含 `obj` 人类读表示的字符串。对于用 Ruby 编写的对象，如果存在实例变量，则会在类名后显示实例变量的值。在其他情况下，使用 `to_s` 方法生成字符串。通常在子类中重写此方法，以提供特定于类的信息。

```ruby
[1, 2, 3, 'four'].inspect => [1, 2, 3..4, 'five']
Time.new.inspect # => 2009-04-13 12:36:31 -0500
```

# class Demo

```ruby
def initialize
  @a, @b = 1, 2
end
```

```ruby
Demo.new.inspect # => <Demo:0x0a33a4 @a=1, @b=2>
```

# instance_of?

```ruby
obj.instance_of?(class) -> true or false
```

如果 `obj` 是给定类的实例，则返回 `true`。参见 `Object#kind_of`。

# instance_variable_defined?

```ruby
obj.instance_variable_defined?(name) -> true or false
```

如果名称已定义，则返回 `true`。注意，一种常见的惯用法使用 `@variable` 进行测试是错误的，因为第一个变量可能已定义但设置为 `nil`，且如果绑定未定义，第二个将触发警告。

# class Fred

```ruby
def initialize(p1, p2)
  @a, @b = p1, p2
end
```

```ruby
fred = Fred.new('cat', :a)
fred.instance_variable_defined?(:@a) # => true
fred.instance_variable_defined?(:@b) # => true
fred.instance_variable_defined?(:@c) # => false
```

# instance_variable_get

```ruby
obj.instance_variable_get(symbol) -> other_obj
```

返回给定实例变量的值（或抛出 `NameError` 异常）。对于普通实例变量，应包含变量名的部分。

```ruby
class Fred
  def initialize(p1, p2)
    @a, @b = p1, p2
  end
fred = Fred.new('cat', 99)
fred.instance_variable_get(:@a) => "cat"
fred.instance_variable_get(:@b) => 99
```

# instance_variable_set

`obj.instance_variable_set(symbol, other_obj)` → `other_obj`

通过符号将实例变量名设置为 `other_obj`，从而破坏了该类作者尝试提供良好封装的努力。

```ruby
class Fred
  def initialize(p1, p2)
    @a, @b = p1, p2
  end
fred = Fred.new('cat', 99)
fred.instance_variable_set(:@a, 'dog') => "dog"
#<Fred:0x0a3c64
  @a="dog", @b=99>
nfred.inspect
```

# instance_variables

`obj.instance_variables` → `array`

返回接收者的实例变量名称数组。注意，仅仅定义访问器（`accessor`）并不会创建相应的实例变量。

```ruby
class Fred
  attr_accessor :al
  def initialize
    @iv = 3
  end
fred.new.instance_variables => [:@iv]
```

# is_a?

`obj.is_a?(class)` → `true or false`

`Object#kind_of` 的同义方法。

# kind_of?

`obj.kind_of?(class)` → `true or false`

如果 `class` 是 `obj` 的类，或者是 `obj` 的子类或包含的模块，则返回 `true`。

```ruby
module M;
  class A
    include M
  end
  class B < A; end
class C < B; end
```

```ruby
b = B.new
b.instance_of? A # => false
b.instance_of? B # => true
b.instance_of? C # => false
b.kind_of? M # => false
b.kind_of? A # => true
b.kind_of? B # => true
b.kind_of? C # => false
b.kind_of? M # => true
```

# method

在 `obj` 中查找命名方法，返回 `Method` 对象（或抛出 `NameError`）。`Method` 对象作为 `obj` 的闭包，因此实例变量和 `self` 的值仍然可用。

```ruby
class Demo
  def initialize(n)
    @iv = n
  end
  def hello()
    "Hello, #{@iv}"
  end
end
```

```ruby
k = Demo.new(99)
m = k.method(:hello)
m.call # => "Hello, 99"
```

```ruby
l = Demo.new('Fred')
m = l.method("hello")
m.call # => "Hello, Fred"
```

# methods

如果 `regular` 参数为 `true`，则返回 `obj` 及其祖类中公开访问的方法列表。否则，返回 `obj` 的单例方法。

```ruby
class Klass
  def my_method()
  end
end
k = Klass.new
k.methods() => [:single, :my_method, :nil?, :eql?, :clone, :dup]
k.methods.length => 5
k.methods(false) => [:single]
```

# nil?

除 `nil` 外的对象都返回 `false`。

# object_id

返回 `obj` 的整数标识符。所有调用都返回相同的数字，且没有两个对象共享它。`Object#id` 与 `Object#name` 是不同的概念。

# private_methods

返回 `obj` 内部的私有方法。这将包含 `obj` 祖类中的混合模块。

# protected_methods

返回 `obj` 的保护方法列表。

# public_method

在 `obj` 中查找命名方法，返回 `Method` 对象（如果方法未找到或找到但不是公共）。

```ruby
class Demo
  def initialize(n)
    @iv = n
  end
  def hello()
    puts "Hello, #{@iv}"
  end
end
k = Demo.new(99)
m = k.public_method(:hello)
m.call

produces:
Hello, 99
prog.rb:15: undefined method `initialize' for 'Demo' (NameError)
from /tmp/prog.rb:15:in `<name>`
```

# public_methods

`Object#methods` 的同义方法。

# public_send

调用 `obj` 的公共方法，传入任何参数。返回方法返回的值。参见 `send`，它会调用私有和保护方法。

# respond_to?

`obj.respond_to?(symbol, include=false)` → `true or false`

如果 `obj` 响应给定方法，则返回 `true`。如果第二个参数为 `true`，则搜索包含私有方法。

# send

`obj.send(symbol, *args, &block)` -> `other_obj`

调用 `symbol` 指定的方法，传入任何参数和块。如果名称与 `obj` 中存在的方法冲突，可以使用 `BasicObject#send`。

```ruby
class Klass
  def hello(*args)
    "Hello " + args.join(' ')
  end
end
k = Klass.new
k.send :hello, :readers # => "Hello readers"
```

# singleton_methods

`obj.singleton_methods(all=true)` -> `array`

返回 `obj` 的单例方法名称数组。如果可选参数为 `true`，列表将包含 `obj` 包含的模块中的方法。（2004 之前的版本中，该参数默认为 `false`。）

```ruby
module Other
  def three() end
end

class Single
  def four(four) end
end

a = Single.new
def a.one(one) end

```

```ruby
class << a
  include Other
  def two(two) end
end
```

```ruby
Single.singleton_methods => [:four]
a.singleton_methods(false) => [:one, :two]
a.singleton_methods(true) => [:one, :two, :three]
a.singleton_methods => [:one, :two, :three]
```

# taint

`obj.taint` → `obj`

将 `obj` 标记为污染。如果 `$SAFE` 级别大于零，某些对象将在创建时被污染。参见第 436 页的第 26 章。

# tainted?

如果对象被污染，则返回 `true`。

```ruby
a = "cat"
a.tainted? => false
a.taint => "cat"
a.tainted? => true
a.untaint => "cat"
a.tainted? => false
```

`obj.tainted?` → `true or false`

# tap

调用块，并将 `obj` 作为参数。返回 `obj`。允许你编写不影响链中值的代码。

```ruby
puts "dog"
.reverse
.tap {|obj| puts "Reversed: #{obj}"}
capitalize
```

produces:
Reversed: god
God

# obj.to_enum(using=:each, (args)+ → enumerator

# to_enum

返回一个遍历 `obj` 内容的 `Enumerator` 对象。`owner` 将调用 `self` 的每个方法，但默认情况下可以通过第一个参数传递不同的方法名来覆盖。传递给 `to_enum` 的任何额外参数将传递给 `enumerator` 方法。

```ruby
by_bytes = "cat".to_enum(:each_byte)
by_bytes.next => 99
by_bytes.next => 97
by_chars = "cat".to_enum(:each_char)
by_chars.next => "c"
by_chars.next # "a"
```

> `obj.to_s` → `string`

# to_s

返回对象 ID 的字符串。作为特殊情况，顶层打印对象的类和对象 ID 的编码。Ruby 程序的初始执行上下文返回 `"main"`。

# trust

`obj.trust` → `obj`

将 `obj` 标记为信任。（参见从第 438 页开始的 `trust` 章节。）

# untaint

`obj.untaint` → `obj`

移除 `obj` 的污染。

## untrust

1.9 将 `obj` 标记为不可信的。（参见从第 438 页开始的关于 `trust` 的章节。）

## untrusted?

1.9 如果 `obj` 是不可信的，则返回 `true`，否则返回 `false`。

## 私有实例方法

### initialize

`initialize` 作为对象构造过程的第三步也是最后一步被调用，负责设置新对象的初始状态。你使用 `initialize` 方法的方法与其它语言中使用构造函数的方法相同。如果你继承除了 `Object` 以外的，你可能希望调用 `super` 来执行父类的初始化器。

```ruby
class A
  def initialize(p1)
    puts "Initializing A: p1 = #{p1}"
    @var1 = p1
  end
end

class B < A
  attr_reader :pl, :var2
  def initialize(p1, p2)
    super(p1)
    puts "Initializing B: p2 = #{p2}"
    @var2 = p2
  end
end

b = B.new("cat", "dog")
puts b.inspect
```

输出：
Initializing A: p1 = cat
Initializing B: p2 = dog
#<B:0x0a0a2ea4 @var1="cat", @var2="dog">

## remove_instance_variable

从 `obj` 中移除命名的实例，并返回该变量的值。

```ruby
class Dummy
  def initialize
    @var = 99
  end
  def remove
    remove_instance_variable(:var)
  end
  def var_defined?
    defined? @var
  end
end

d = Dummy.new
d.var_defined? # => "instance-variable"
d.remove
d.var_defined? # => nil
```

## singleton_method_added singleton_method_added(symbol)

当单例方法被到接收者时，作为回调调用。

```ruby
module Chatty
  def Chatty.singleton_method_added(id)
    puts "Adding ##{id.id2name} to ##{self.name}"
  end
  def self.one()
  end
  def two()
```
