

接下来，我们使用一种称为“块（block）”的 Ruby 技术来创建超文本传输协议（HTTP）对象的新实例。缩进定义了块的开始和结束。我们在这里不需要使用循环，但通过使用这个块，我们将值赋值给 `http` 变量。当块结束时，`Net::HTTP` 类将关闭套接字并处理清理工作。我们的 `http` 变量持有 HTTP 对象，允许我们向 Web 服务器发送 HTTP 命令。我们使用 `head` 方法在 Web 服务器上作为上下文中发送 HTTP Head 请求。这会返回相关信息，包括日期、Web 服务器类型、请求参数，以及常见的 `last-modified` 头部（该头部指示了页面更改的时间）。我们试图从服务器提取的两个数据是正在使用的软件和最后修改日期，我们将它们以数组的形式返回。

最后，我们关闭循环，让 HTTP 对象为我们进行清理。如果由于某种原因我们的请求失败，我们添加了一个回退机制，返回一个包含 `nil` 值的数组。这确保了函数返回信息的一致性。让我们让函数解析从命令行传递的选项，并使用这些变量来调用我们的函数。

```
if ARGV.size <= 0 || ARGV.size > 2
print "Usage: #{$0} Host [Port]\n"
exit
end
server, modified = getHeader(ARGV[0], ARGV[1])
print "Server #{ARGV[0]}:#{ARGV[1] || 80}(#{server}) last-modified #{modified}"
```

# 提示

注意 `ARGV` 处理上的区别。在许多语言中，`ARGV` 的第一个数组元素是程序本身。在 Ruby 中，`ARGV` 的第一个元素是第一个选项。要引用程序本身，我们使用 `$0`。

如果我们提供的 `ARGV` 参数数量无效，我们将显示错误消息并退出。我们在错误字符串中使用的符号允许我们有效地将代码或变量嵌入到字符串中。通过将代码或变量封装在 `#{}` 符号中，我们是在告诉 Ruby 符号内部的代码并将该值插入到我们的字符串中。在这种情况下，我们通过插入 `$0` 来包含所调用的脚本名称。

接下来，我们使用函数 `getHeader` 连接到远程服务器，获取头部，并将服务器类型和最后修改信息返回到我们的两个变量 `server` 和 `modified` 中。然后我们将它们打印到屏幕上。我们将脚本保存为 `head.rb`，并将脚本权限设置为 755。图 4.3 显示了我们的脚本针对 `syncgress.com` 运行的输出。在这里可以看到服务器是 Apache，并且服务器具有运行 Ruby on Rails 的潜力。

![](img/42f332b2adf7dab7e681e5d6cdd2074c_173_0.png)

# 图 4.3 针对 syncgress.com 运行 head.rb。

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

# 使用 Ruby 构建类

类允许我们将数据与方法分组，这些方法可以帮助处理、增强和报告这些数据。在 Ruby 中，类可以相互构建；它们被设计用于扩展和增强，以创建用于特定目的自定义类。这允许我们构建一个基础的套接字服务器类并扩展它以支持不同的协议。我们可以利用套接字服务器的基础代码，为每个协议编写较少的代码。通过这样做，当我们在基类中发现 bug 时，不需要复制粘贴来传播代码以定义协议。

让我们把创建的 `header` 函数并封装在一个类中。

### 构建类

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

