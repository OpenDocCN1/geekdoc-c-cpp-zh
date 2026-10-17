
接下来，我们使用函数 `getHeader` 连接到远程服务器，获取头部，并将服务器类型和最后修改信息返回到我们的两个变量 `server` 和 `modified` 中。然后我们将它们打印到屏幕上。我们将脚本保存为 `head.rb`，并将脚本权限设置为 755。图 4.3 显示了我们的脚本针对 `syncgress.com` 运行的输出。在这里可以看到服务器是 Apache，并且服务器具有运行 Ruby on Rails 的潜力。

![](img/42f332b2adf7dab7e681e5d6cdd2074c_173_0.png)

## 图 4.3 针对 syncgress.com 运行 head.rb。

以下是完整代码：

```ruby
#!/usr/bin/ruby
require 'net/http'
def getHeader(host,port = nil)
  port = port || 80
  Net::HTTP.start(host.to_s,port) do |http|
    resp = http.head('/')
    return [resp['server'].to_s,resp['Last-Modified'].to_s]
  end
  return [nil,nil]
end
if ARGV.size <= 0 || ARGV.size > 2
  print "Usage: #{$0} Host [Port]\n"
  exit
end
server, modified = getHeader(ARGV[0],ARGV[1])
print "Server #{ARGV[0]}:#{ARGV[1] || 80}(#{server}) last-modified #{modified}"
```

### 使用 Ruby 构建类

类允许我们将数据与方法分组，这些方法可以帮助处理、增强和报告这些数据。在 Ruby 中，类可以相互构建；它们被设计用于扩展和增强，以创建用于特定目的自定义类。这允许我们构建一个基础的套接字服务器类并扩展它以支持不同的协议。我们可以利用套接字服务器的基础代码，为每个协议编写较少的代码。通过这样做，当我们在基类中发现 bug 时，不需要复制粘贴来传播代码以定义协议。

让我们把创建的 `header` 函数并封装在一个类中。

#### 构建类

我们将创建一个名为 `Header` 的类。`initialize` 方法将用于设置主机和端口。然后我们定义 `getHeader` 方法来执行请求。

```ruby
#!/usr/bin/ruby
require 'net/http'

class Header
  def initialize(host, port = nil)
    @host = host
    @port = port || 80
  end

  def getHeader
    Net::HTTP.start(@host.to_s,@port) do |http|
      resp = http.head('/')
      return [resp['server'].to_s,resp['Last-Modified'].to_s]
    end
    return [nil,nil]
  end
end

if ARGV.size <= 0 || ARGV.size > 2
  print "Usage: #{$0} Host [Port]\n"
  exit
end

header = Header.new(ARGV[0], ARGV[1])
server, modified = header.getHeader
print "Server #{ARGV[0]}:#{ARGV[1] || 80}(#{server}) last-modified #{modified}"
```

通过将逻辑封装在类中，我们使得代码更有组织性且可重用。现在，我们可以根据需要创建不同主机和端口的多个 `Header` 实例。

```ruby
class MyHexMaker < HexMaker
def h_to_s(hex)
    i = 0
    return [hex].pack("H")
end
tst = HexMaker.new.str_to_h("AAAA")
print("Converted string: #{tst}\n")
tst = MyHexMaker.new.str_to_h("AAAA")
print("Original String: #{MyHexMaker.new.h_to_s(tst)}")
```

我们创建了 `MyHexMaker` 的新实例，将 `str_to_h` 的输出赋值给变量 `t` 并将其打印。为了证明我们在 `MyHexMaker` 类中具有相同的功能，我们将执行相同的操作。现在我们在 `tst` 中有了十六进制值，并将使用 `h_to_s` 将其转换回来。在图 4.4 中，我们看到该脚本将同时打印我们的十六进制值和原始字符串值，这表明我们已成功转换为十六进制，然后再转换回来。这个示例展示了我们如何获取一个类、扩展它并保持其原始功能。

![](img/42f332b2adf7dab7e681e5d6cdd2074c_177_0.png)

## 图 4.4 使用 hex.rb 进行十六进制转换及反转。

### 访问类数据

当我们创建类时，有时限制暴露给用户的类变量是有意义的。在处理类变量时，我们有三种导出变量的基本方法：读取器 `readers`、写入器 `writers` 和访问器 `accessors`。正如我们可能猜到的，读取器用于读取变量，而写入器用于写入变量。访问器最初并不那么明确，但它们是被设计为既可读又可写的变量。如果我们在这三种类型范围之外创建了实例变量，它们被认为是私有的，直到我们创建一个允许它们被访问的函数。为了实现这一点，让我们创建一个新文件并添加以下代码。

为了尝试这些概念，让我们创建一个类并将其命名为 `Test`。我们创建了三种不同的变量类型：一个名为 `error` 的读取器，一个名为 `request` 的写入器，以及一个名为 `other` 的访问器。我们还为 `Test` 类创建了一个测试方法，用于设置 `error` 实例变量，并打印我们的 `request` 和 `other` 实例变量。我们需要这样做，因为我们无法在类外写入 `error` 或读取 `request`。接下来，我们需要创建一些代码来让我们练习这些概念。

```ruby
mytest = Test.new
print "Trying to set error to 'change me'"
begin
  mytest.error = "change me"
rescue
  print "....changing error failed\n"
end
```

我们创建了一个新的 `Test` 实例并将其赋值给变量 `mytest`。然后我们打印一条消息，说明我们将尝试更改 `error` 变量。这将从我们的屏幕输出中直观地看出发生了什么。但我们需要进行一些错误处理。

Ruby 的错误处理允许我们将代码段放在块 `blocks` 中，当该代码块失败时，我们能够对该操作进行清理，而不是让应用程序崩溃。我们用 `begin` 关键字开始代码块。在 `rescue` 语句之前的所有内容都将被视为执行的代码。如果代码失败，将调用 `rescue` 关键字处的代码块；否则，将忽略它。我们用 `end` 关键字结束代码块。现在，我们的程序将准备好捕获尝试更改 `error` 变量时发生的错误，并允许我们的应用程序继续后续测试。

> 提示
>
> Ruby 有根据特定类型错误进行 rescue 的能力。它可以处理多个 `rescue` 行，每行处理不同的错误。这种错误处理在调用使用其他类的类方法时非常有用。例如，如果我们有一个协议类 `protocol class`，我们希望能够处理协议所使用的套接字类 `socket class` 中的特定错误。关于 Ruby 错误处理的更多信息，请访问 http://www.ruby-doc.org/docs/ProgrammingRuby/html/tut_exceptions.html。

```ruby
print "Setting request to 'pretty please' and other to 'we change this at will!'\n"
mytest.request = "pretty please"
mytest.other = "we can change this at will"
print "Calling test function...\n"
mytest.test
print "\n"
print "Directly querying data...\n"
print "Error is #{mytest.error}\n"
print "Other is #{mytest.other}\n"
begin
  print "Request is #{mytest.request}\n"
rescue
  print "Failed to query mytest.request, it is write only\n"
end
```

为了完成代码测试，我们设置了 `request` 和 `other` 变量并执行测试方法。这将打印 `error` 和 `request`。接下来，我们直接查询变量。我们将打印 `error` 和 `other` 的内容，因为它们都在我们的方法之外。最后，我们将尝试打印 `request` 变量，但我们知道它会失败。我们将其封装在错误处理中。这应该在屏幕上打印错误。这应该显示错误到屏幕上。我们显示了 `testClass.rb` 的输出（见 4.5）。

```text
File Edit Search
root:~ ruby testClass.rb
Trying to set error to 'change me'
....changing error failed
Setting request to 'pretty please' and other to 'we change this at will!'
Calling test function...
Request is pretty please
Directly querying data...
Error is change me
Other is we can change this at will
Failed to query mytest.request, it is write only
```

## 4.5 输出。

### 文件操作

除非我们正在处理二进制格式，否则 Ruby 的文件处理可能不是我们的首选。对于纯文本解析，Ruby 的正则能力使其成为领先者。Ruby 拥有丰富的类，允许我们执行基本的文件系统操作、链接查询以及读写。为了研究这些功能，我们将构建一个通过 proc 系统收集进程信息的脚本。我们有时想知道进程在哪里运行以及使用了什么选项，以便我们轻松地重建或修改符号文件。

```ruby
#!/usr/bin/ruby
require 'etc'
pid = ARGV[0].to_i
cwd = File.readlink("/proc/#{pid}/cmdline")
owner = File.stat("/proc/#{pid}/cmdline").uid
```

对于我们的程序，我们需要收集进程所有者、工作目录以及完整的命令行。我们将从命令行获取进程 ID 并将其存储在 `pid` 中。接下来，我们将查看 `/proc` 以检查链接。进程类的 `readlink` 方法将获取符号链接的目标并返回字符串。我们将该字符串存储在变量 `cwd` 中。然后我们将使用 `stat` 命令，它将返回关于文件的大量信息，包括修改、创建和访问时间。对我们更重要的是它会返回文件的所有者。我们将使用 `stat` 返回的 `uid` 变量来获取文件所有者的数字 ID 并将其赋值给 `owner`。

```ruby
file = File.new("/proc/#{pid}/cmdline")
cmdline = file.read.split("\000")
file.close
filename = cmdline.shift
```

进程 `cmdline` 包含了命令行传递的选项列表，以空字符分隔。我们读取这些信息，按空字符分割，并将数组存储在 `cmdline` 中。`cmdline` 的第一个元素是执行的命令。为了移除第一个元素并返回字符串，我们可以使用数组的 `shift` 方法。我们使用 `shift` 是因为我们 `cmdline` 只包含传递给正在调查的进程的选项。

```ruby
print "Process #{pid} is owned by #{etc.getpwuid(owner).name}\n"
print "Process #{pid} CWD: #{cwd}\n"
print "Process #{pid} Command: #{filename} #{cmdline.join(' ')}\n"
```

现在我们拥有了所需的信息，并构建打印语句。通常情况下，数字 ID 对我们没有任何意义。所以我们

我们将使用 `Etc` 模块的 `getpwuid` 方法将我们的 uid 转换为用户名。`getpwuid` 返回来自密码文件中关于该 uid 的信息。我们需要的唯一字段是 `name`，因此我们引用返回的密码结构中的 `name` 变量。为了能够读取其他用户拥有的进程并测试此程序，我们需要 root 权限。作为 root，我们运行脚本 `proc.rb`，其进程 ID 为 `i`，我们应该会在图 4.6 中看到输出。

```
File Edit View Search Terminal Help
root@kali:~ ruby proc.rb 1
Process 1 is owned by root
Process 1 CWD: /
Process 1 Command: /sbin/init
root@kali:~# 
```

## 图 4.6 使用 proc.rb 确定进程信息。

### 数据库基础

在 Ruby 中，即使是数据库记录也可以视为对象。`Active Record` 是一个为 Rails 框架设计的 Ruby 模块。它旨在抽象数据库内部细节。使用 Active Record 构建程序时，在某些情况下我们甚至不需要知道数据库的结构。与其处理复杂的 SQL 查询，`Active Record` 让我们像对待类一样对待数据库信息。我们可以使用这些 Active Record 模型连接到数据库服务器并查询记录，而没有大量的开销。如果在渗透测试期间遇到凭据，我们可以很容易使用 Ruby 将数据从数据库获取到可以轻松传输回系统的格式中。

为了演示，我们需要一个数据库服务器和一个用户。Kali 安装了 PostgreSQL 以供 Metasploit 使用。利用这一点来完成这些示例。开始之前，我们必须验证数据库服务器正在运行。要做到这一点，我们需要检查服务器状态，如果它没有运行，则启动它。我们需要变成 `postgres` 用户并为我们的使用创建一个用户和数据库。
