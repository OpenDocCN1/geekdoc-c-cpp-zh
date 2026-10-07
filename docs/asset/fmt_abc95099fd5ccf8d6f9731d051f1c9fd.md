
# :DEBUG_LEVEL / `conf.debug_level`

将内部级别设置为 `n`。如果你正在调试 `irb` 的词法器，这非常有用。[0]

# :IGNORE_EOF / `conf.ignore_eof`

指定在输入时接收到文件结束符（EOF）的行为。如果为 `true`，将忽略它；否则 `irb` 将退出。[false]

# :IGNORE_SIGINT / `conf.sigint`

如果为 `false`，*C (Ctrl+C) 将退出 `irb`*。如果为 `true`，输入期间按下 *C* 将取消输入并返回到顶层；在执行期间按下 *C* 将中止当前操作。[true]

# :INSPECT_MODE / `conf.inspect_mode`

指定值的显示方式：`true` 表示使用 `inspect`，`false` 使用 `to_s`，`nil` 在非数学模式下使用 `inspect`，在数学模式下使用 `to_s`。[nil]

# :RB_RC

可以是一个项目对象，当 `irb` 会话（或子会话）启动时会调用该对象。[nil]

# `conf.last_value`

`irb` 输出的最后一个值。[... ]

# :LOAD_MODULES / `conf.load_modules`

通过 `-r` 命令行选项加载的模块列表。[[]]

# :MATH_MODE / `conf.math_mode`

如果为 `true`，`irb` 将带有数学库运行（见第 767 页），并且不使用 `inspect` 显示值。[false]

# `conf.prompt_c`

延续语句的提示符（例如，紧跟在其之后）。[depends]

# `conf.prompt_i`

标准的顶层提示符。[depends]

# :PROMPT_MODE / `conf.prompt_mode`

提示符显示的样式。[:DEFAULT]

# `conf.prompt_s`

延续字符串的提示符。[depends]

# :PROMPT

请见第 287 页的“配置提示符”。[{ ... }]

# :RC / `conf.rc`

如果为 `false`，则不加载初始化文件。[true]

# `conf.return_format`

用于显示交互式输入的表达式结果的格式。[depends]

# :SAVE_HISTORY / `conf.save_history`

在 `irb` 会话之间保存的命令数量。[nil]

# :SINGLE_IRB

如果为 `true`，嵌套的 `irb` 会话将全部共享同一个绑定（binding）；否则，将根据 `.CONTEXT_MODE` 的值创建一个新的绑定。[nil]

# `conf.thread`

指向当前执行的 `Thread` 对象的只读引用。[current thread]

# :USE_LOADER / `conf.use_loader`

指定在 `load`/`require` 时是否使用 `irb` 自己的文件读取方法。[false]

# :USE_READLINE / `conf.use_readline`

如果可用，`irb` 将使用 `readline` 库（见第 797 页），除非此选项被设置为 `false`（在这种情况下将不使用 `readline`），或设置为 `nil`（在这种情况下在 `irb-ruby-mode` 中不使用 `readline`）。[depends]

# :USE_TRACER / `conf.use_tracer`

如果为 `true`，则跟踪语句的执行情况。[false]

# :VERBOSE / `conf.verbose`

理论上，当为 `true` 时会开启额外的跟踪；在实践中，几乎没有额外的跟踪结果。[true]

## 命令

在提示符处，你可以输入任何有效的 Ruby 表达式并查看结果。你可以使用以下任何一个命令来控制 `irb` 会话：¹

`help ClassName, string, or symbol`

显示给定内容的 `ripl` 帮助信息。要获取方法名的帮助，你可能需要传递一个字符串，如下：

```
irb(main):001=> help "String.encoding"  String#encoding
```

```
obj.encoding                          => encoding
```

返回表示 `obj` 编码的 `Encoding` 对象。

# `exit`, `quit`, `irb_exit`, `irb_quit`

退出此 `irb` 会话或子会话。如果你使用 `cb` 修改了绑定（见下文），将退出此绑定模式。

# `conf`, `context`, `irb_context`

显示当前配置。通过调用 `conf` 方法来修改配置。从 284 页开始的列表显示了可用设置。-1. 出于不明的原因，这些命令有多达九种不同的别名。我们没有显示所有这些命令。287

例如，要将默认提示符设置为某些内容，你可以使用：
`irb(main):001: conf.prompt_i = "Yes, Master? "`
=> "Yes, Master?"
`1 + 2`

`cb`, `change_binding ( )`

创建一个新的绑定（有时称为工作空间），它有自己的局部作用域。如果给了 `obj`，将作为新绑定使用。

`push obj`, `pop`

推入并弹出当前绑定。

`bindings`

列出当前绑定。

`irb ( )`

启动一个 `irb` 会话。如果给了 `obj`，将作为该会话使用。

`jobs`

列出 `irb` 会话。

`fg n`

切换到指定的 `irb` 会话。`n` 可以是以下值之一：`irb` 会话数量、线程 ID、一个 `irb` 对象，或启动会话时的 `self` 对象。

`kill n`

杀死 `irb` 会话。`n` 可以是为 `fg` 描述的任何值。

`source filename`

加载并执行给定文件，显示源行。

## 配置提示符

对于 `irb` 使用的提示符，你有很大的灵活性。提示符存储在 `conf:PROMPT` 中。例如，要建立像 `MY_PROMPT` 的新提示符，你可以输入以下内容（直接在 `irb` 中或 `.irrc` 文件中）：

```
IRB.conf[:PROMPT] = { # 提示符模式
:PROMPT_I => '--',
# 普通提示符
:PROMPT_S => '>',
# 延续字符串
:PROMPT_C => '+',
# 延续语句
:RETURN => "=>%%%n"
# 返回值的格式
}
```

一旦你定义了提示符，就必须告诉 `irb` 使用它。从命令行，可以使用 `-prompt` 选项。（注意提示符模式名称会自动转换为大写，连字符将变为下划线）。

```
--prompt
```

如果你想在 `.irrc` 中设置提示符，可以使用：

```
IRB.conf[:PROMPT_MODE] = :MY_PROMPT
```

提示符显示的样式由 `PROMPT_MODE` 决定。可用模式有：

- `:DEFAULT`：默认提示符。
- `:SIMPLE`：最小提示符。
- `:CUSTOM`：用户定义的自定义提示符。

一旦你定义了自定义提示符，可以通过设置激活它：

```
IRB.conf[:PROMPT_MODE] = :CUSTOM
```

符号 `PROMPT_I`、`PROMPT_S` 和 `PROMPT_C` 指定每个字符串的格式。在这种情况下，Ruby 通过赋值来判断是否为变量：

```
irb(main):001=> help "String.encoding"  String#encoding
```

```
obj.encoding                          => encoding
```

返回表示 `obj` 编码的 `Encoding` 对象。

## 限制

在 `irb` 中，赋值在遇到第二行之前执行了：

```
irb(main):001=> begin
irb(main):002=> var = 0
irb(main):003=> end
```

如果你需要匹配 `begin`/`end` 对内的 Ruby 语句：

```
irb(main):001=> begin
irb(main):002=> var = 0
irb(main):003=> end
```

在 `irb` 中，赋值在遇到第二行之前执行了：

```
irb(main):001=> begin
irb(main):002=> var = 0
irb(main):003=> end
```

在这种情况下，Ruby 通过赋值来判断是否为变量：

```
irb(main):001=> var = 0
```

## 限制

在 `irb` 中，赋值在遇到第二行之前执行了：

```
irb(main):001=> begin
irb(main):002=> var = 0
irb(main):003=> end
```

## 保存你的历史记录

如果 `irb` 中有 `readline` 支持（即你可以按方向键，`irb` 会回之前的命令），那么你就可以配置 `irb` 记住你在会话之间输入的命令。只需在你的 `.irrc` 中添加以下内容：

```
IRB.conf[:SAVE_HISTORY] = 50 # 保存最后 50 条命令
```

- 1. `RDoc` 也可以为 Fortran 77 程序编写文档。

## RDoc 文档

| 文件 | 类 | 方法 |
| --- | --- | --- |
| `exil.rb` | `Counter` | `inc (Counter)`<br>`new (Counter)` |

# `Counter` (类)

位于：`exil.rb`
父类：`Object`

## 方法

`inc` `new`

## 属性

`counter` [`Integer`]

```
class Counter
attr_reader :counter
def initialize(initial_value=0)
  @counter = initial_value
end
def inc
  @counter += 1
end
```

## 公共类方法

`new(initial_value=0)`

## 公共实例方法

`inc()`

此图显示了浏览器窗口中的某些 RDoc 输出。覆盖框显示了生成此输出的源程序。尽管源码没有包含内部文档，RDoc 仍然能够从中提取出有趣的信息。屏幕顶部有三个窗格显示了我们拥有文档的文件、类和方法。对于 `Counter` 类，RDoc 为我们显示属性和方法（包括方法签名）。如果我们点击一个方法签名，RDoc 将弹出一个包含相应方法源代码的窗口。

图 19.1. 浏览 `Counter` 类的 RDoc 输出

## RDoc 文档

| 文件 | 类 | 方法 |
| --- | --- | --- |
| `x2.rb` | `Counter` | `inc (Counter)`<br>`new (Counter)` |

| `Counter` (类) |
| 所在: `x2.rb` |
| 父类: `Object` |

实现了一个简单的累加器，通过方法 `Counter#inc` 访问其值，该方法会增加此值。

```
# 实现了一个简单的累加器，
# 数值通过属性进行访问
# 调用方法 Counter#inc
# 将会增加此值。
```

### 方法
`inc`
`new`

```ruby
class Counter
# 计数的当前值
attr_reader :counter
# 使用给定的初始值创建一个新的 Counter
def initialize(initial_value=0)
  @counter = initial_value
end
# 增加计数的当前值
def inc
  @counter += 1
end
```

### 属性
`counter` (R) 计数的当前值

## 公共类方法

`new(initial_value=0)`
使用给定的初始值创建一个新的 Counter

| 公共实例方法 |
| --- |
| `inc()` |
| 增加计数的当前值 |

[验证]

注意观察关于每个元素的注释如何在 RDoc 输出中显示，它们被重新格式化成了 HTML。不那么明显的是，RDoc 检测到了我们注释中的超链接机会：在类级别的注释中，对 `Counter#inc` 的引用是一个指向方法描述的超链接；而在该方法的注释中，对类 `Counter` 的引用则链接回类文档。这是 RDoc 的一个关键特性：它的设计初衷是在 Ruby 源文件中保持不干扰，并通过在生成输出时尝试智能来弥补这一点。

图 19.2. 当源码包含注释时浏览 RDoc 输出

# 图 19.3. 使用 `ri` 读取文档

| `ri Counter` | 类: `Counter` |
| 实现了一个简单的累加器，通过属性 `counter` 访问其值。调用方法 `Counter#inc` 将会增加此值。 |

类方法：
`new`

实例方法：
`inc`

属性：
`counter`

| `ri Counter.inc` | `Counter#inc` |
| `inc()`
| 增加计数的当前值 |

## 将 RDoc 添加到 Ruby 代码中

`RDoc` 解析 Ruby 源代码文件以提取主要元素（类、模块、方法、属性等）。你可以通过在文件元素之前添加注释块，选择与这些元素关联额外的文档。

注释块可以写得相当自然，可以通过在注释的连续行上使用 `#`，或者将注释包含在 `%begin...end` 块中。如果你使用后者，`=begin` 行必须标记一个 RDoc 标签，以将该块与其他风格的文档区分开。

```ruby
=begin rdoc
使用 Behninski 算法计算图中的最小成本路径，
并对孤立叶节点进行优化的反向剪枝。
end
def calculate_path
  ..
```

在文档注释中，段落是共享左对齐边界的行。超出此边界的缩进文本将按原样格式化。

# 图 19.4. 由 RDoc/ri 生成的 Proc 类文档

% `ri Proc` 类: `Proc`

`Proc` 对象是绑定到一组局部变量的代码块。一旦绑定，代码可以在不同的上下文中被调用，并且仍然访问那些变量。

```ruby
def gen_times(factor)
  return Proc.new{n| n+factor }
end
```

```ruby
times3 = gen_times(3)
times5 = gen_times(5)
```

```ruby
times3.call(12)      => 36
times5.call(5)      => 25
times3.call(times5.call(4)) => 60
```

类方法：
`new`

实例方法：
`==`, `[]`, `arity`, `binding`, `call`, `clone`, `eql?`, `hash`, `topro_proc`, `to_s`

非正文本可以进行标记。要将单个单词设置为斜体、粗体或打字机字体，你可以分别使用 `_word_`、`**word**` 和 `+word+`。如果你想对多个单词或包含非标准字符的文本进行操作，可以使用 `<em>multiple words</em>`、`<b>more words</b>` 和 `&lt;yet more words&gt;`。在内联标记前加上反斜杠可以停止其被解析。

如果文件包含以 `#-.` 开头的注释，RDoc 将停止处理。这可以用于区分外部注释和内部注释。

`:main name`
这等同于 `--main` 命令行参数，用于设置此文档的初始页面显示。

`:stopdoc:` / `:startdoc:`
这会停止或开始向容器中添加新的文档元素。例如，如果一个类有若干个你不想记录的常量，可以在第一个常量之前使用 `:stopdoc:`，在最后一个常量之后使用 `:startdoc:`。如果你在容器末尾之后没有指定 `:startdoc:`，则会禁用整个类或模块的文档生成。

`:enddoc:`
这表示当前词法层级上不再记录任何内容。

关于使用 RDoc 文档文件的更大示例，请参见第 302 页的第 19.5 节。

## 为 C 扩展添加 RDoc

在用 C 编写 Ruby 扩展时，RDoc 能够理解许多函数。

如果 RDoc 看到一个名为 `Init_ClassName` 的 C 函数，它会将其视为类定义——`Init_function` 之前的任何 C 注释将作为该类的文档。

`Init_function` 通常用于将 C 函数与 Ruby 方法名关联。例如，一个 C 扩展可能会定义一个 Ruby 方法 `salt=`，它通过 C 函数 `salt_set` 使用如下调用来实现：

```c
rb_define_method(Cipher, "salt=", salt_set, 1);
```

RDoc 解析此调用，并将 `salt=` 添加到类文档中。随后，RDoc 在源码中搜索 C 函数调用 `salt_set`。如果该调用之前有一个注释块，RDoc 将使用它作为该方法的文档。

这种基础方案除了你需要在注释中编写常规文档外，无需付出任何额外努力。然而，RDoc 无法辨别对应 Ruby 方法的调用序列。在这个示例中，RDoc 将输出一个名为（某种毫无意义的）"arg1" 的单个参数。你可以使用函数注释中的 `call-seq` 指令来覆盖这一点。`call-seq` 之后的行（直到遇到空行）将用于记录该方法的调用序列：

```c
/*
 * call-seq:
 * cipher.salt = number
 * cipher.salt = "string"
 * 将此加密器的盐值设置为二进制 +number 或
 * +string+ 中的位。
 */
```

```c
static VALUE
salt_set(cipher, salt)
...
```
