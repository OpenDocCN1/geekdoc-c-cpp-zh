
# `name` `method.name` → `string`

1.9
返回方法 `meth` 的名称。
`method = "cat".method(:upcase)`
`method.name` # => `:upcase`

# `owner` `method.owner` → `module`

1.9
返回定义 `meth` 的类或模块。
`method = "cat".method(:upcase)`
`method.owner` # => `String`

# `receiver`

返回定义 `meth` 的对象。
`method = "cat".method(:upcase)`
`meth.receiver` # => `"cat"`

# `source_location`

返回定义 `meth` 的源代码文件名和行号；如果 `self` 未在 Ruby 源码中定义，则返回 `nil`。
`internal_method = "cat".method(:upcase)`
`internal_method.source_location` # => `nil`
`require 'set'`
`set = Set.new`
`ruby_method = set.method(:clear)`
`ruby_method.source_location` # => `["/usr/lib/ruby/1.9.1/set.rb", 114]`

# `to_proc`

返回与此方法对应的 `Proc` 对象。解释器在传递块参数时会调用 `.to_proc`，可以使用取符号符 `&` 后跟方法对象，以便将块传递给另一个方法调用。请参本节开头的示例。

# `unbind`

将 `meth` 从其当前的接收者中解除。生成的 `UnboundMethod` 随后可以绑定到相同类的新对象上（见第 724 页的 `UnboundMethod`）。

# `Module` Object

子类：`Class`

`Module` 是方法和常量的集合。模块中的方法可以是实例方法也可以是模块方法。当模块被包含（`include`）时，实例方法会作为类的方法出现；而模块方法不会。相反，可以在不创建封装对象的情况下调用模块方法，而实例方法则不行。另见第 609 页的 `Module#function`。

在随后的描述中，参数符号（parameter symbol）指的是符号，它可以是一个引号的字符串或 `Symbol`（例如 `:name`）。

```ruby
module Mod

  include Math

  CONST = 1

  def meth

    #

  end

end
```

```
Mod.class => Module

Mod.constants => [:CONST,:PI,:E]

Mod.instance_methods => [:meth]
```

# Class methods

`Module.constants` -> `array`
`Module.constants(include_parents)` -> `array`

`constants`

+ 1.9 不带参数时，返回解释器中顶层常量的列表。带一个参数时，返回在 `Module` 类中定义的常量（如果参数为 `true`，则包含其父类）。这种接口有些晦涩是因为 `Module` 是一种 `Class`，同时也是 `Module` 的子类。所有方法的第一次调用都是对类方法的真实调用，而第二种形式实际上是代理到实例方法（见本节稍后的 `Module#constants`）。

```ruby
module Mixin

  CONST_MIXIN = 1

end

class Class

  include Mixin

  SPURIOUS_CONSTANT = 2

end
```

```
Module.constants[1..S] => [:ARGV,:ArgumentError,:Array,:BasicObject,:Bignum]

Module.constants.include?(:CONST_MIXIN) => false

Module.constants(false) => [:SPURIOUS_CONSTANT]

Module.constants(true) => [:SPURIOUS_CONSTANT,:CONST_MIXIN]
```

# `nesting`

返回调用点嵌套的 `Modules` 列表。

```ruby
module M1

module M2

nest = Module.nesting

p nest

np nest[0].name

end
```

产生：

+ `[M1:M2, M1]`
`"M1:M2"`

# `new`

创建一个新的匿名模块。如果提供了块，则会将模块对象传递给块，并使用 `module_eval` 在该模块的上下文中该块。

```ruby
Fred = Module.new

  def meth1

    "hello"

  end

  def meth2

    "bye"

  end

a = "my string" => "my string"

a.extend(Fred)

a.meth1 => "hello"

a.meth2 => "bye"
```

# Instance methods

`<`, `<=`, `>=`, `>>`

层级查询——如果一个模块被包含（或是另一个模块的父类），则认为该模块比另一个模块大。其他运算符同样定义。如果模块之间没有关系，则返回 `false`。

```ruby
module Mixin

end

module Parent

  include Mixin

end

module Unrelated
```

# Ruby 3.1 文档

```
Parent > Mixin # => false

Parent < Mixin # => true

Parent <= Parent # => true

Parent < Unrelated # => nil

Parent > Unrelated # => nil
```

```
mod <=> other_mod -> -1,0,1

比较——如果 `mod` 包含 `other_mod`，返回 `-1`；如果 `mod` 和 `other_mod` 是同一个模块，返回 `0`；如果 `mod` 被 `other_mod` 包含，返回 `1`。
```
=== obj -> true or false
```

Case 等等——如果 `obj` 是 `mod` 的实例或其后代，返回 `true`。有限地用于 `case` 语句来测试对象。

# `ancestors`

```
mod.ancestors -> array

返回 `mod` 包含的模块列表（包括 `mod` 自身）。
```

```ruby
module Mod

include Math

include Comparable

end
```

```
Mod.ancestors => [Comparable, Math]

Math.ancestors => [Math]
```

```
mod.autoload(name, file_name) -> nil
```

# `autoload`

当在 `mod` 的命名空间访问 `name`（可能是字符串或符号）时，注册 `file_name` 进行加载（使用 `Kernel.require(name)`）。自动加载的文件在顶层上下文中执行。在此示例中，`module_b.rb` 包含：

```ruby
module A::B # in module_b.rb

def doit

  puts "In Module A::B"

end

module_function :doit
```

其他代码可以自动包含此模块。

```ruby
module A

autoload(:B, "module_b")

end

A::B # autoloads "module_b"
```

产生：

In Module A::B

# `autoload?`

`mod.autoload?(name)` -> `file_name` or `nil`

返回当字符串或符号 `name` 在 `mod` 中引用时将自动加载的文件名。如果没有关联的 `autoload`。

```ruby
module A

  autoload(:B, :module_b)

  A.autoload?(:B) => "module_b"

  A.autoload?(:C) => nil
```

# `class_eval`

`mod.class_eval(string, :file_name, (:line_number))` -> `obj`
`mod.class_eval(block)` -> `obj`

`Module.module_eval` 的别名。

# `class_exec`

`mod.class_exec(args)` -> `|block|` -> `obj`

`Module.module_eval` 的别名。

# `class_variable_defined?`

`mod.class_variable_defined?(name)` -> `true` or `false`

如果类变量在 `mod` 中定义，则返回 `true`。

```ruby
class One

  @var1 = "wibble"

end

One.class_variable_defined?(:var1) => true

One.class_variable_defined?(:var2) => false
```

# `class_variable_get`

`mod.class_variable_get(name)` -> `obj`

返回类变量的值。

```ruby
class One

  @var1 = "wibble"

end

One.class_variable_get(:var1) => "wibble"
```

# `class_variable_set`

`mod.class_variable_set(name, value)` -> `value`

将名称赋给给对象，创建该对象。如果之前不存在该命名的常量，则创建一个新常量。

```ruby
class One

  @var1 = "wibble"

end

One.class_variable_set(:var1, 99) => 99
```

# `class_variables`

`mod.class_variables` -> `array`

+ 1.9 返回 `mod` 中类变量名称数组。（从 Ruby 1.9 开始，类变量不再与子类共享，此列表仅限于在 `mod` 中定义的变量。）

```ruby
class One

  @var1 = 1

end

class Two < One

  @var2 = 2

end

One.class_variables => [:var1]

Two.class_variables => [:var2]
```

# `const_defined?`

`mod.const_defined?(name (search_parents=true))` -> `true` or `false`

如果给定命名的常量由 `mod` 或其父类定义（如果第二个参数为 `true`），则返回 `true`。

```
Math.const_defined?("PI") => true
```

# `const_get`

`mod.const_get(symbol)` -> `obj`

返回 `mod` 中具名常量的值。

```
Math.const_get(:PI) => 3.14159265358979
```

# `const_missing`

```
const_missing(symbol) -> obj
```

当在 `mod` 中引用未定义的常量时调用。它将符号传递给未定义的常量，并返回一个用于该常量的值。以下代码非常纯粹。如果引用了常量的某个版本，它尝试加载一个名为与常量小写版本相同的文件，因此 `class Fred` 被添加到 `file.rb` 中。如果找到，则返回加载的类的值。它实现了一种自动加载机制。

```ruby
def Object.const_missing(name)

  @looked_for ||= {}

  str_name = name.to_s

  raise "Class not found: #{name}" if @looked_for[str_name]

  @looked_for[str_name] = 1

  file = str_name.downcase

  require file

  klass = const_get(name)

  return klass if klass

  raise "Class not found: #{name}"

end
```

# `const_set`

```
mod.const_set(symbol, obj) -> obj
```

将名称赋给给对象，创建该对象。如果之前不存在该命名的常量，则创建一个新常量。

```ruby
Math.const_set("HIGH_SCHOOL_PI", 22.0/7.0) => 3.1428571428571

Math::HIGH_SCHOOL_PI - Math::PI => 0.00126488926734
```

# `mod.constants( include_parents = true )` → `array`

1.9 返回一个包含 `mod` 中可访问的常量名称数组。如果参数为 `true`，则包含任何包含的模块中的常量。

```
IO.constants(false) # => [:SEEK_SET, :SEEK_CUR, :SEEK_END]

# 现在包含在模块 File::Constants 中定义的内容

IO.constants(true)[1,6] # => [:SEEK_CUR, :SEEK_END, :LOCK_SH, :LOCK_EX, :LOCK_UN, :LOCK_NB]
```

# `included?` `mod.include?(other_mod)` → `true` or `false`

如果 `other_mod` 被 `mod` 或其某个祖先类包含，则返回 `true`。

```ruby
module A

end

class B

include A

end

class C < B

end

B.include?(A) # => true

C.include?(A) # => true

A.include?(A) # => false
```

# `included_modules` `mod.included_modules` → `array`

返回在 `mod` 中包含的模块列表。

```ruby
module Mixin

end

module Outer

include Mixin

end

Mixin.included_modules # => []

Outer.included_modules # => [Mixin]
```

# `instance_method` `mod.instance_method( symbol )` → `unbound_method`

返回一个代表 `mod` 中实例方法的 `UnboundMethod`（未绑定方法）。

```ruby
class Interpreter

def do_a() print "there"; end

def do_d() print "Hello"; end

def do_e() print "!\n"; end

def do_v() print "Dave"; end

end

Dispatcher =

  'a' => instance_method(:do_a),

  'd' => instance_method(:do_d),

  'e' => instance_method(:do_e),

  'v' => instance_method(:do_v)

}

def interpret(string)

  string.each_char{|ch| Dispatcher[ch].bind(self).call

end

terpreter = Interpreter.new

terpreter.interpret('dave')
```

# `instance_methods`

返回一个包含接收者中公共和保护实例方法名称的数组。对于模块，这些是公共方法；对于类，这些是实例方法（而非单例方法）。如果不带参数或参数为 `true`，则返回 `mod` 及其超父类中的实例方法。当以模块作为接收者调用或参数为 `false` 时，返回 `mod` 自身的的实例方法。（在 2004 年 1 月之前的 Ruby 版本中，参数默认为 `false`。）

```ruby
module A

  def method1()

end

class B

  def method2()

end

class C < B

  def method3()

end

A.instance_methods #=> [:method1]

B.instance_methods(false) #=> [:method2]

C.instance_methods(false) #=> [:method3]

C.instance_methods(true).length #=> 54
```

# `method_defined?` `mod.method_defined?(symbol)` -> `true` or `false`

如果方法是由 `mod`（或其包含的模块，如果 `mod` 是类，则包括其祖先）定义的，则返回 `true`。匹配公共和保护方法。

```ruby
module A

def method1() end

end

class B

  def method2() end

end

class C < B

  include A

  def method3() end

end

A.method_defined? :method1 # => true

C.method_defined? "method1" # => true

C.method_defined? "method2" # => true

C.method_defined? "method3" # => true

C.method_defined? "method4" # => false
```
