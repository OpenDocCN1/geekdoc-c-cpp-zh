
```
require 'thread'

group = ThreadsWait.new

# 创建等待 1 秒、0.9 秒等的线程
9.times do |i|
  thread = Thread.new(i) { sleep 1.0 }
  group.add(thread)
end

# 线程是否完成？
group.finished? => false

# 等待一个完成
group.next_wait.value => 8

# 等待另外 5 个完成
5.times { group.next_wait } => 5

# 等待下一个完成
group.next_wait.value => 2

# 然后等待所有线程完成
group.all_wait => nil
```

# Time

`time` 库为内置的 `Time` 类增加了功能，支持 RFC2822 (邮件)、RFC2816 (HTTP) 和 ISO8601 (XML schema) 使用的格式。

```ruby
require 'time'
Time.rfc2822("Thu, 1 Apr 2008 16:32:45 CST") => 2008-04-01 17:32:45 -0500
Time.rfc2822("Thu 1 Apr 2008 16:32:45") => 2008-04-01 17:32:45 -0600
Time.now.rfc2822 => Mon, 13 Apr 2009 13:27:18 -0500
Time.iso8601("2008-04-01T16:32:45") => 2008-04-01 16:32:45 -0500
Time.iso8601("2008-04-01T16:32:45.123Z") => 2008-04-01 22:32:45 UTC
```

# Timeout

`Timeout.timeout` 方法接收一个表示超时时间的秒参数、一个可选异常和一个块。执行该块并运行一个计时器。如果块在超时之前结束，`timeout` 返回块的值。否则，抛出异常（默认是 `Timeout::Error`）。

```ruby
require 'timeout'
for snooze in 1..2
  puts "About to sleep for #{snooze}"
  begin
    Timeout::timeout(1.5) do |timeout_length|
      puts "Timeout period is #{timeout_length}"
      sleep(snooze)
    end
    puts "That was refreshing"
  rescue Timeout::Error
    puts "Woken up!!"
  end
end
# samples/timeout_rb
```

产生：

- About to sleep for 1

  Timeout period is 1.5

  That was refreshing

- About to sleep for 2

  Timeout period is 1.5

  Woken up!!

使用超时时要小心——你可能会发现它们中断无法可靠重启的系统调用，导致数据丢失。

# Tk

Tcl/Tk 的封装器。

在所有创建 GUI 的 Ruby 中，`Tk` 库的使用最广泛，运行在 Windows、Linux、Mac OS 和其他类 Unix 平台上。虽然它生成的界面不是最美的，但 Tk 功能完备且编写相对简单。

```ruby
require 'tk'
include Math
root = TkRoot.new
root.title "Curves"
root.geometry "400x400"
canvas = TkCanvas.new(root)
canvas.width 400
height 400
canvas.pack(side='top', fill='both', expand='yes')
points = []
10.step(0.1) do |i|
  new_x = 5*scale*sin(i) + 200
  new_y = 5*scale*cos(i) + 200
  points << [new_x, new_y]
end
f = 2.0
r = (Math.sin(3*f))+127.0
g = (Math.cos(2*f))+127.0
b = (Math.sin(3*f))+127.0
col = sprintf("#%02x%02x%02x", r.to_i, g.to_i, b.to_i)
if points.size == 3
  Tkline.new(canvas,
    points[0][0], points[0][1],
    points[1][0], points[1][1],
    points[2][0], points[2][1],
    'smooth'=>'on',
    'width'=> 7,
    'fill' => col,
    'capstyle'=>'round')
end
points.shift(3)
end
Tk.mainloop
```

![](img/44b0533e8e4c9d26ebd13a65ab0d_820_0.png)

5. 所有这些环境要求在使用 Ruby Tk 扩展之前，必须安装 Tcl/Tk 库。

# 系统无关的临时目录

`tmpdir` 库为 `Dir` 类增加了 `tmpdir` 方法。该方法返回一个临时目录的路径，该目录应该是对当前进程可写的（如果所有常用的临时目录都不可写，且当前工作目录也不可写，则不成立）。候选目录包括环境变量 `TMPDIR`、`TMP`、`TEMP` 和 `USERPROFILE` 引用的目录、`/tmp` 目录以及（在 Windows 上）Windows 或系统目录下的 `tmp` 子目录。

```ruby
require 'tmpdir'

Dir.tmpdir # == "/var/folders/a4-daQQQG4anp1m9DAY+TE+++/-tmp-"

ENV['TMPDIR'] = "wibble" # 不存在
ENV['TMP'] = "/sbin" # 不可写
ENV['TEMP'] = "/Users/ave/tmp" # 正确

Dir.tmpdir # == "/Users/ave/tmp"
```

`mktmpdir` 方法用于创建一个新的临时目录：

```ruby
require 'tmpdir'
name = Dir.mktmpdir
# .. process, process, ..
Dir.rmdir(name)
```

# 追踪器

## 追踪程序执行

`tracer` 库使用 `Kernel.set_trace_func` 来追踪整个 Ruby 程序的执行。被追踪的行会显示线程、文件、行号、类、事件和源行。显示的事件包括：`-` 表示更改，`>` 表示调用，`C` 表示返回，`E` 表示定义结束。

- 你可以通过从命令行使用 tracer 库来跟踪入口：

```ruby
class Account
# % r - tracer account.rb
  def initialize(balance)
#account.rb:2:class Account
    @balance = balance
#account.rb:3:class Account
  end
#account.rb:4:class Account
  def debit(amount)
#account.rb:5:def initialize(balance)
    if @balance < amount
#account.rb:6:Module::
      fail "insufficient funds"
#account.rb:7:Module::
    else
#account.rb:8:Module::
      @balance -= amount
#account.rb:9:Module::
    end
  end
end
acc = Account.new(100)
acct.debit(40)
```

- 你还可以使用 tracer 对象仅追踪部分代码，并使用过滤器来选择追踪的内容：

```ruby
require 'tracer'
class Account
  def initialize(balance)
    @balance = balance
  end
  def debit(amount)
    if @balance < amount
      fail "insufficient funds"
    else
      @balance -= amount
    end
  end
end
tr = Tracer.new
tr.add_filter lambda { |event, rest| event == "line" }
acct = Account.new(100)
tr.on :do
  acct.debit(40)
end
```

# TSort 拓扑排序

给定一组节点之间的依赖关系（每个节点依赖于零或多个节点，且依赖图中没有环），拓扑排序将返回一个节点列表，使得没有任何节点排在依赖它的节点之后。可以使用这些依赖关系进行任务调度，顺序意味着你将在启动任何依赖于这些项的任务之前完成这些依赖项。`make` 程序使用拓扑排序来安排其执行顺序。

在该库的实现中，你混入 `TSort` 模块并定义两个方法：`tsort_each_node`（它产生每个节点）和 `tsort_each_child`（它给定一个节点，产生它的每个依赖项）。

- 给定制作 piña colada 步骤之间的依赖关系，执行这些步骤的最优顺序是什么？

下载 `samples/tsort.rb`

```ruby
require 'tsort'
class TSort
  def initialize
    @dependencies = {}
  end

  def add_dependency(task, +rel_on)
    @dependencies[task] ||= rel_on
  end

  def tsort_each_node(&block)
    @dependencies.each_key { |node| block.call(node) }
  end

  def tsort_each_child(node, &block)
    @dependencies[node].each { |dep| block.call(dep) }
  end
end

tasks = TSort.new
tasks.add_dependency(:add_rum, :open_blender)
tasks.add_dependency(:add_pc_mix, :open_blender)
tasks.add_dependency(:add_ice, :open_blender)
tasks.add_dependency(:close_blender, :add_rum, :add_pc_mix, :add_ice)
tasks.add_dependency(:blend_mix, :close_blender)
tasks.add_dependency(:pour_drink, :blend_mix)
tasks.add_dependency(:pour_drink, :open_blender)
puts tasks.tsort
```

```
输出:
  open_blender
add_rum
add_pc_mix
add_ice
close_blender
blend_mix
pour_drink
```

# un FileUtils 的命令行界面

为什么要运行？当你从命令行通过 Ruby 的 `-r` 选项调用它时，它的拼写是 `-run`。这个双关语暗示了该库的意图：让你能够从命令行运行命令（在这种情况下，是 FileUtils 中的方法的子集）。理论上，这为你提供了一组与操作系统无关的文件操作命令，在编写可移植的 Makefile 时可能有用。

另请参：`FileUtils` (755)

- 可用命令如下：

- % ruby -run cp <options> source dest

- % ruby -run ln <options> target linkname

- % ruby -run mv <options> source dest

- % ruby -run rm <options> file

- % ruby -run mkdir <options> dirs

- % ruby -run rmdir <options> dirs

- % ruby -run install <options> source dest

- % ruby -run chmod <options> octal_mode file

- % ruby -run touch <options> file

注意使用 `--` 来告诉 Ruby 解释器选项是传给程序的。

你可以通过此命令获取所有可用命令列表：

```
下载 samples/slun_1.rb
```

% ruby -run -e help

要获取特定命令的帮助，请附加该命令名称：

```
下载 samples/slun_2.rb
```

% ruby -run -e help mkdir

# RFC 2396 统一资源标识符 (URI) 支持

`URI` 封装了统一资源标识符 (URI）概念，这是一种指定某种类型资源的方法。URI 是 URL 的超集（例如网页页面地址），并通过位置来标识资源。URI 由方案（例如 http、mailto、ftp 等）、结构数据以及名称组成。URI 具有工厂方法，接收一个 URI 字符串并返回一个特定于该方案的 URI 的子类。该库显式支持 ftp、http 和 mail 方案；其他将被视为通用 URI。URI 还有转义和反转义 URI 方法。

另请参见：`open-uri` (782), `Net::HTTP` (774)

```ruby
require 'uri'
```

```ruby
uri = URI.parse("pragprog.com:1234/mypage.cgi?q=ruby")
uri.class     => URI::HTTP
uri.scheme    => "http"
uri.host       => "pragprog.com"
uri.port       => 1234
uri.path       => "/mypage.cgi"
uri.query     => "q=ruby"
```

# WeakRef

在 Ruby 中，当对象不再被引用时，就会被垃圾回收。然而，有时你只想在对象当前被其他地方使用时才保持它。`WeakRef` 类允许你对对象创建一个“弱引用”，这种引用阻止对象被垃圾回收。

当你使用 `WeakRef` 时，必须在对象可能被垃圾回收之前检查它仍然存在。如果对象已被回收，`WeakRef` 将返回 `nil`。

```ruby
require 'weakref'
obj = "I am a string"
ref = WeakRef.new(obj)
puts ref # => "I am a string"

obj = nil
GC.start
puts ref # => nil
```

## WIN32OLE

仅限 Windows

Windows 自动化的接口，允许 Ruby 代码与 Windows 应用程序交互。Ruby 的 Windows 接口详细说明请参阅第 21 章（第 316 页）。

- 打开资源管理器并并在我们的主页上显示它：

```ruby
samples/swin32ole_1.rb
ie = WIN32OLE.new('InternetExplorer.Application')
ie.visible = true
is.navigate("http://www.progprog.com")
```

- 在 Microsoft Excel 中创建一个新图表并对其进行旋转：

```ruby
samples/swin32ole_2.rb
require 'win32ole'
# -4100 是 Excel 常量 xl3DColumn 的值
ChartTempVal = -4100
excel = WIN32OLE.new('excel.application')
# 创建并旋转图表
excel['Visible'] = TRUE
excel.Range('a1')['Value'] = 3
excel.Range('a2')['Value'] = 2
excel.Range('a3')['Value'] = 1
excel.Range('a1:a3').Select()
excelchart = excel.Charts.Add()
excelchart['Type'] = ChartTempVal
30.step(180) do |rot|
  excelchart.rotation = rot
  sleep(0.1)
end
excel.ActiveWorkbook.Close(0)
excel.Quit()
```

## XML-RPC

`XMLRPC` 客户端允许使用 XML-RPC 协议调用网络服务器上的方法。通信通过 HTTP 进行。服务器可能运行在 Web 服务器的上下文中，这通常会使用 80 或 443 (SSL) 端口。服务器也可以独立运行。Ruby 的 XML-RPC 服务器实现支持作为 CGI 脚本、mod ruby 脚本、Webber 句处理器以及独立服务器运行。它支持身份验证，客户端可以与各种服务器通信。服务器可能会抛出 `FaultException` 错误——这些错误会在客户端产生异常（或可能被标记为返回给客户端的状态）。

另请：`dRuby` (747), `WeeBrick` (828)

- 下面示例接受摄氏温度并将其转换为华氏度。它在 Webber 句处理器的上下文中运行。
