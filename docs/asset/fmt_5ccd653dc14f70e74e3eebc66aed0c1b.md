
```ruby
def prompt_and_get(prompt)
  print prompt
  res = readline.chomp
  throw :quit_requested if res == ""
  res
end
catch :quit_requested do
  name = prompt_and_get("Name: ")
  age = prompt_and_get("Age: ")
  sex = prompt_and_get("Sex: ")
  #
  #..
  # process information
end
```

正如此示例所示，`throw` 不需要出现在 `catch` 的静态作用域内。

# 第11 章

## 基础输入与输出

Ruby 乍看之下提供了两套独立的 I/O 例程。第一种是简单的接口——到为止我们几乎完全在使用它：

```ruby

print "Enter your name:"

name = gets

```

许多与 I/O 相关的方法实现在 `Kernel` 模块中——`gets`、`open`、`print`、`printf`、`put`、`puts`、`readline` 等——这使得编写简单的 Ruby 程序变得容易且方便。这些方法通常对标准输入和标准输出进行 I/O 操作，因此对于编写过滤器非常有用。它们从第 564 页开始记录。

第二种提供更多控制的方法是使用 `IO` 对象。

### 什么是 IO 对象？

Ruby 定义了一个基类 `IO` 来处理输入和输出。该基类被 `File` 和 `Socket` 等类派生以提供更专门的行为，但原理是相同的。`IO` 对象是程序和外部资源之间的双向通道。一个 IO 对象可能比你想象的要复杂，但它仍然简单地进行写入并从中读取。在本章中，我们将集中在 `IO` 及其最常用的派生类上。关于使用 `Socket` 类的更多细节，请参阅第 878 页。这意味着单个 IO 对象有时可以管理多个操作系统文件描述符。例如，如果你打开一对管道，单个 IO 对象包含了读管道和写管道。

### 打开和关闭文件

正如你预期的，可以使用 `File.new` 创建一个新的文件对象：

```ruby

file = File.new("testfile", "r")

```

第一个参数是文件名。第二个是模式，它允许你打开文件进行读取、写入或两者兼顾。（在这里我们使用 `"r"` 打开 testfile 进行读取）。我们也可以使用 `"w"` 用于写入或 `"a"` 用于追加。允许的模式列表出现在第 547 页。在创建文件时你还可以指定权限；详见第 512 页 `File.new` 的描述。打开文件后，我们可以根据需要对其进行写入/读取。最后，作为负责者，我们关闭文件以确保所有缓冲区数据已写入且所有资源被释放。

但 Ruby 可以让你的生活变得简单一点。`File.open` 方法也会打开文件。通常情况下，它的行为就像 `File.new` 一样。然而，如果你将块与调用关联，那么当块退出时，文件会自动关闭。

```ruby

File.open("testfile", "r") do |file|

  # process文件

end # 文件在这里自动关闭

```

这种方法有一个额外的好处。在之前的情况下，如果在处理文件时抛出异常，`file.close` 调用可能不会发生。如果 `file` 变量超出作用域，垃圾回收最终会关闭它，但这可能不会立即发生。在此期间，资源保持打开状态。这种情况在 `File.open` 的块形式中不会发生。如果在块内部抛出异常，文件在异常传播到调用者之前就会关闭。`open` 方法看起来如下所示：

```ruby

class File

  def open(*args)

    result = f = File.new(*args)

    if block_given?

      begin

        result = yield f

      ensure

        f.close

      end

    return result

  end

end

```

### 读取和写入文件

我们用于“简单”I/O 的相同方法适用于所有文件对象。因此，`gets` 从标准输入（或脚本调用时命令行指定的任何文件）读取一行，而 `file.gets` 从文件对象读取一行。

例如，我们创建一个名为 `copy.rb` 的程序：

```ruby

while line = gets

  puts line

end

```

如果我们不带参数运行此程序，它将从控制台读取行并将其复制回控制台。注意，每按下回车键，行就会回显一次。（在随后的示例中，我们用**粗体**显示用户输入。）

```text

% copy.rb

These are lines

These are lines

that I am typing

that I am typing

p

```

我们也可以在命令行传递零或多个文件名，在这种情况下，`gets` 会轮流读取：

```text

% copy.rb testfile

This is line one

This is line two

This is line three

And so on...

```

最后，我们可以显式地打开文件并从中读取：

```ruby

File.open("testfile") do |file|

  while line = file.gets

    puts line

  end

end

```

输出：

```text

This is line one

This is line two

This is line three

And so on...

```

除了 `gets`，I/O 对象还拥一组额外的访问方法，旨在让我们的生活更轻松。

### 读取的迭代器

除了使用通常循环从 IO 流读取数据外，还可以使用各种 Ruby 迭代器。`IO#each_byte` 调用一个块并传入 IO 对象的下一个 8 位字节（在本例中，一个 `File` 类型的对象）。`chr` 方法将整数转换为相应的 ASCII 字符。

```ruby

File.open("testfile") do |file|

  file.each_byte {|ch| print "#{ch.chr}" ""}

end

```

输出：

```text

T: 84 h104 i105 s115 :32 i102 s115 :32 i108 i105 ...

T: 84 h104 i105 s115 :32 i102 s115 :32 i108 i105 ...

T: 84 h104 i105 s115 :32 i102 s115 :32 i108 i105 ...

```

## 但我怀念我的 C++ iostream

有时候，品味是无法计量的。然而，就像你可以使用 `<<` 运算符将对象追加到数组中一样，你也可以将对象追加到输出 IO 流中：

```
endl = "\n"
stdout << 99 << " red balloons" << endl
```

产生输出：

- 99 red balloons

再次，`<<` 方法在将参数发送到目的地之前，使用 `to_s` 将其转换为字符串。

尽管我们开始时贬低糟糕的 `<<` 运算符，但使用它实际上有一些好的理由。因为其他类（如 `String` 和 `Array`）也实现了具有相似语义的 `<<` 运算符，你通常可以编写 `<<` 追加某些内容的代码，而无需关心它是被添加到数组、文件还是字符串中。这种灵活性使得单元测试变得简单。我们将在第 370 页开始的鸭子类型（duck typing）章节中详细讨论这一观点。

### 字符串的 I/O

有时，你需要处理那些假设从文件读取到写入一个或多个文件的代码。但你遇到了一个问题：数据不在文件中。可能数据是通过 SOAP 服务提供的，或者它是作为命令行参数传递的。又你正在运行单元测试，不想修改真实的文件系统。

这时 `StringIO` 对象登场了。它们的行为与其他 I/O 对象一样，但它们读写的是字符串而不是文件。如果你打开一个 `StringIO` 对象进行读取，只需为它提供一个字符串。`StringIO` 对象上的所有读取操作都是从该字符串读取。同样，如果你想向 `StringIO` 对象写入内容，只需传递一个字符串使其进行填充。

```
require 'string'
ip = StringIO.new("now isnnthe\ntime learn\Ruby!")
op = StringIO.new("", "")
ip.each_line do |line|
  puts line.reverse
end
op.string = "\n won\,nemit eht\nnnrael on!nybuR\n"
```

### 与网络通信

Ruby 熟通大多数互联网协议，包括低层和高层协议。

对于喜欢在网络层面反复钻研的人，Ruby 在 `socket` 库中提供了一组类（从第 878 页开始记录）。这些类让你能够访问 TCP、UDP、SOCKS 和 Unix 套接字，以及你架构支持的任何额外套接字类型。该库还提供了辅助类来简化服务器的编写。这里有一个简单的程序，使用 `finger` 协议获取本地机器上 "mysql" 用户的信息：

```
require 'socket'
client = TCSocket.open('127.0.0.1', 'finger')
client.send("mysql", 0) # 0 意味着标准包
puts client.readlines()
client.close
```

产生输出：

- Login: _mysql Name: MySQL Server
Directory: /var/empty Shell: /usr/bin/false
Never logged in.
No Mail.
No Plan.

在更高层上，`lib/net` 模块集为一组应用协议（目前包括 FTP、HTTP、SMTP 和 telnet）提供了处理程序。这些内容从第 73 页开始记录。例如，以下程序列出了本书首页上的图片：

![](img/44b0533e8e4c9d6926ebd13a65acab0d_181_0.png)

```
require '/http'
h = Net::HTTP.new("www.pragprog.com", 80)
response = h.get('/titles/ruby3/programming-ruby-3')
if response.message == "OK"
  puts response.body.scan(/<img alt="(.*?)" src="(.*?)">/m).uniq
```

产生输出：

```
http://asset1.pragprog.com/images/logo.gif71239424264
http://asset1.pragprog.com/images/login-button.gif12239424264
http://asset1.pragprog.com/images/covers/190x28/betas/ruby3.jpg712362053616
http://asset1.pragprog.com/images/covers/40x48/fr_rr.jpg711841841447
```

尽管这个示例看起来简单，但它可以显著改进。特别是，它在错误处理方面进展不足。它真的应该报告“未找到”错误（臭名昭著的 404）并处理重定向（当网络服务器为客户端提供请求页面的替代地址时发生）。

我们可以将其提升到更高的水平。通过将程序引入 `open-uri` 库，`Kernel.open` 突然能够识别文件名中的 `http://` 和 `ftp://` URL。不仅如此——它还会自动处理重定向。

下载 samples/tution_19.rb

```
require 'open-uri'
open('http://pragprog.com/<img alt=".+?\>') do |f|
  puts f.read.scan(/<img alt=".+? src="(.+?)"/m).uniq
end
```

产生输出：

- http://assets1.pragprog.com/images/logo.gif?1239424264
- http://assets0.pragprog.com/images/login-button.gif?1239424264
- http://assets1.pragprog.com/images/front_page.png?123942464
- http://assets0.pragprog.com/images/covers/75x90/ltp.jpg?23620526
- http://assets0.pragprog.com/images/covers/75x90/jrport.jpg?23620529

# 第 12 章：Fibers、线程和进程

Ruby 提供了两种基本方式来组织程序，以便“同时”运行不同的部分。Fibers 允许你暂停部分的执行并运行其他部分。为了解耦执行，你可以使用线程在程序内部划分任务，也可以使用多个进程在程序之间划分任务。让我们逐一查看。

Fibers 的引入带来了这种机制。尽管这个名称暗示了某种轻量级线程，但实际上 Ruby 的 fibers 只是一个简单的协程机制。它们允许你编写看起来像是在没有线程复杂性的情况下手动调度的程序。就像解析文本文件并统计每个单词的出现次数。我们可以在不使用 fibers 的情况下这样做：

```
下载 samples/threads_1.rb
counts = Hash.new(0)
File.foreach("test") do |line|
  line.scan(/\w+/) do |word|
    word = word.downcase
    counts[word] += 1
  end
end
counts.keys.sort { |k| print "#{k}:#{counts[k]} }
```

产生输出：

- and:1 line:3 on:1 so:1 three:3

然而，这段代码很乱，因为它混淆了查找单词和统计单词的概念。但 fibers 为我们提供了一个更简单的解决方案：

```
下载 samples/threads_2.rb
```

产生输出：

- and:1 line:3 on:1 one:1 this:3

`Fiber` 类的构造函数接收块并返回一个 fiber 对象。此时块的代码还没有执行。随后，我们可以对 fiber 对象调用 `resume`。这会导致块开始执行。文件被打开，`scan` 方法提取初始单词。然而，在此处，`Fiber.yield` 被调用。它挂了块的执行——即返回给 `Fiber.yield` 的任何值。我们的主程序进入循环并增加第一个单词的计数。然后它回到循环顶部，再次调用 `resume`。`resume` 调用持续到停止的地方（在 `Fiber.yield` 调用之后）。当 fiber 运行完文件中的单词时，块退出。下次调用 `resume` 时，它返回 `nil`（块已退出）。如果你之后尝试调用 `resume`，将得到 `FiberError`。

Fibers 通常用于按需从无限序列中生成值。这里有一个按顺序返回整数的 fiber：

```
下载 samples/threads_2.rb
```

```
twos = Fiber.new do
  num = 2
  loop do
    Fiber.yield(num) unless num % 3 == 0
    num += 2
  end
end
10.times { print twos.resume, " " }
```

产生输出：
2 4 8 10 14 16 20 22 26

由于 fibers 只是对象，你可以传递它们、将它们存储在变量中等。Fiber 只能在创建它们的线程中恢复。

### Fiber、协程和延续

Ruby 对 fiber 的基本支持是有限的——fiber 只能将控制交还给恢复它们的代码。Ruby 提供了两个标准库来扩展这种行为。`fiber` 库（见第 754 页）增加了完整的协程支持。一旦加载，fibers 就提供了一个 `transfer` 方法，允许它们将控制权转移到其他 fibers。

一个相关的更通用的机制是*continuation*（延续）。一种记录运行中的程序状态（所在位置、当前绑定等）然后从未来的某个点恢复的方法。可以使用延续（以及其他新结构）。延续也被用于在请求之间存储运行 Web 应用程序的状态——当应用程序向浏览器发送响应时，会创建一个延续；随后来自浏览器的下一个请求到达，延续被调用，应用程序从它停止的地方继续。你通过引入第 738 页描述的 `continuation` 库在 Ruby 中启用延续。

### 多线程

同时做两件事最简单的方法是使用 Ruby 线程。在 Ruby 1.9 之前，这些被实现为所谓的绿色线程——线程在解释器内部完全切换。在 Ruby 1.9 中，读取现在由操作系统执行。这是一个改进，但并不如你可能希望的大。尽管线程利用了多个处理器（以及单个进程中的多个核心），但有一个巨大的陷阱。许多 Ruby 扩展库不是线程安全的（因为它们是为旧线程模型编写的）。因此，Ruby 做了折中：它使用原生操作系统线程，但一次只操作一个线程。你永远不会在同一个应用程序中看到两个线程并发运行 Ruby 代码。（然而，你会看到线程忙于执行（例如）I/O，而另一个线程在执行 Ruby 代码。那是部分……）

### 创建线程

创建一个新线程是简单易当的。以下代码是一个简单的示例。它并行下载一组网页。对于要求下载的每个 URL，代码都会创建一个独立的线程来处理 HTTP 事务。

```
samples/threads_4.rb
require 'net/http'
```
