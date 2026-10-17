
客户端连接到服务器并调用方法，该方法使用 `inject` 的魔力来对其参数求和。它返回结果，客户端打印出：

Sum is 6

`DRbObject` 的初始 `narg` 指明我们想要连接到一个新的分布式对象。我们也可以使用现有的对象。

噢，你可能会说。这听起来像 Java 的 RMI、CORBA 或类似的东西。这是一种函数对象机制——但它只用几行 Ruby 代码编写。没有 C 语言，没有花哨，只有纯粹的 Ruby 代码。当然，它没有命名服务或交易服务，或者其他你在 CORBA 中喜欢的任何功能，但它简单且足够快。在我的 2.5GHz Power Mac 系统上，这段示例代码每秒大约运行约 1,300 条远程消息。如果你需要命名服务，DRB 有一个可能符合要求的环形服务器。

而且，如果你喜欢 Sun 的 JavaSpaces（JINI 架构的基础）的外，你会感兴趣地知道，drb 也分发了一个短模块，可以执行相同的功能。JavaSpaces 基于一种名为 Linda 的技术。为了证明其日本作者很有幽默感，Ruby 版本的 Linda 被称为 Rinda。

## 编译时？运行时？随时？

关于 Ruby 需要记住的重要点是，“编译时”和“运行时”之间没有太大区别。它们是一样的。你可以向运行中的进程添加代码。你可以即时重新定义方法，将它们的作用域从公共改为私有，等等。你甚至可以修改基本类型，例如 `Class` 和 `Object`。

一旦你使用了这种灵活性，很难回到像 C++ 这样的静态语言，甚至是像 Java 这样的半静态语言。

但是，你为什么要那样做呢？

## 第 26 章

## 将 Ruby 锁在保险

Walter Webcoder 对门户网站有一个很棒的主意：算术网页。在各种酷炫的数学链接和横幅广告包围下，这只有一个包含一个文本字段和一个按钮的简单网页表单。用户在字段中输入算术表达式，点击按钮，答案就会显示。世界的计算器一夜之间诞生；Walter 赚了钱并退休，毕生投入他的汽车车牌收藏。

Walter 认为实现计算器很容易。他使用 Ruby 的 CGI 库访问表单内容，并使用 `eval` 方法将字符串评估为表达式：

```ruby
samples/taint.rb
require 'cgi'
cgi = CGI.new("html4")
# 获取表单字段 "expression" 的值
expr = cgi["expression"].to_s
begin
  result = eval(expr)
rescue Exception => detail
  # 处理错误的表达式
end
# 将结果显示回用户...
```

在 Walter 将应用程序上线大约七秒后，一个来自 Waxahahiye 的十二岁少年解决了全球问题，并在表单中输入了 `system("rm")`，他的计算机文件、Walter 的梦想随之崩塌了。

Walter 学到了一个重要的教训：外部数据是危险的。

## 安全级别 (Safe Levels)

变量 `$SAFE` 决定了内容。表 26 位于第 436 页。

| SAFE | 限制 |
| :--- | :--- |
| 0 | 无检查 |
| 1 | 禁止加载文件 |
| 2 | 禁止使用污染数据 |
| 3 | 不可传递污染对象 |
| 4 | 允许修改不可信对象 |

让我们更具体化。使用安全级别（safe level）小于 3 创建的对象是受信任的。然而，安全级别为 3 或 4 创建的对象将被视为不可信的。运行在安全级别 3 和 4 级的代码也被认为认为是不可信的。因为不可信的代码只能修改不可信的对象，所以在安全级别 3 和 4 下创建的代码将无法修改在较低安全级别创建的对象。

```
samples/taint.rb
```

```
produces:
dog.untrusted? = false
cat.untrusted? = true
DOG IS TRUSTED
CAT IS UNTRUSTED
cat is now 'cat is untrusted'
prog.rb:17:in `'downcase'`: Insecure: can't modify string (SecurityError)
from /tmp/prog.rb:17:in `'block in <main>'' 
from /tmp/prog.rb:17:in `'call'' 
from /tmp/prog.rb:17:in `'<main>'`
```

你可以设置并取消对象的不可信状态，即使用 `Object#untrust` 和 `Object#trust`（但你必须在安全级别 4 以下调用 `unrust`，并在安全级别 3 以下调用 `trust`）。
方法 `Object#untrusted?` 在对象为不可信的时返回 `true`。

## `$SAFE >= 1`

- 环境变量 `RUBYILOP` 和 `RUBYOPT` 不会被处理，当前目录不会被添加到路径中。
- 不允许命令行选项 `-i`, `-j`, `-r`, `-s` 和 `-x`。
- 如果 `$PATH` 中的任何目录是世界可写的，则无法从其启动。
- 不能对名为污染字符串（tainted string）的目录进行操作或 chroot。
- 不能评估污染字符串。
- 不能加载或要求名为污染字符串的文件（除非它被包裹）。
- 不能从污染字符串监控或查询文件或管道的状态。
- 不能从污染字符串执行系统命令或 `exec`。
- 不能对污染字符串传递 `trap`。

1.9

## `$SAFE >= 2`

- 不能更改、创建或删除目录，或进行 `chroot`。
- 不能从世界可写的目录加载文件。
- 不能使用 `Flag.chmod`, `File#chown`, `File#stat`, `File::stat`, `File::truncate`, `File::mask`, `File::flock`, `IO#ioctl`, `IO#stat`, `Kernel::stat`, `Kernel::syscall`, `Kernel#trap`, `Process.setpgid`, `Process.setsid`, `Process.setsctnl`, 或 `Process#exec`。
- 不能使用 `trap` 处理信号。

## `$SAFE >= 3`

- 所有对象在创建时都是被污染的。
- 不能取消对象的污染。
- 不能对一个对象赋予信任。
- 对象是不可信的。

## `$SAFE >= 4`

- 不能修改污染的数组、哈希或字符串。
- 不能修改全局变量。
- 不能访问污染对象的实例变量。
- 不能更改环境变量。
- 不能关闭或重新打开污染的文件。
- 不能冻结污染对象。
- 不能更改方法的可见性（公有/私有/保护）。
- 不能在污染的类或模块中创建别名（alias）。
- 不能获取元数据（例如方法变量列表）。
- 不能在污染的类或模块中定义、重定义或取消定义（undef）方法。
- 不能修改 `Object`。
- 不能从污染对象中移除实例变量或常量。
- 不能操作线程、终止当前线程以外的线程或设置 `abort_on_exception`。
- 不能拥有线程本地变量。
- 不能在 `$SAFE` 有值的线程中抛出异常。
- 不能在 `ThreadGroups` 之间移动线程。
- 不能调用 `fork`, `exec!` 或 `abort`。
- 只能加载被包裹的文件，并且可以在未污染的类和模块中包含模块。
- 不能将符号标识符转换为对象引用。
- 不能写入文件或管道。
- 不能使用 `autoload`。
- 不能使用污染对象。
- 不能取消对象的不可信状态。

## 第四部分

## Ruby 库参考指南

## 第 27 章

## 内置类和模块

本章记录了 Ruby 语言中内置的类和模块。它们在每个 Ruby 程序中都可用；无需 `require`。本节不包含各种变量和常量；这些列在第 339 页。

以下显示了每个方法的调用方式：

```
String.new(some_string) -> new_string
```

斜体表示传入了一个单个字符串，箭头表示从方法返回了另一个字符串。由于此值与参数的名称不同，我们在说明实例方法时，展示了带有接收者的调用：

```
each(str) -> record
```
