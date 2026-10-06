
我们使用 `module` 关键字来创建我们的 DFTP 模块。我们的第一个类将包含客户端和服务器的基础代码。这将允许我们减少代码重复。我们将这些代码包含在客户端和服务器类中，如果其中任何部分需要更改，我们只需要在一个地方修改代码即可。我们的 `FTPBase` 类将处理包含 UDP 通信所需的 socket 模块。我们之前没有见过 `@@`，但在这种情况下该符号用于类变量。这些变量是按类设置的，而不是按实例设置的。在这种情况下，`read` 和 `write` 将始终具有二进制值 1 和二进制 2，以识别我们正在使用的请求类型，因此我们不需要按实例逐地更改它们。基类的最后部分是用于对象创建的 `initialize` 方法。我们将设置主机（host）、端口（port）和通信密钥（key）的实例变量。然后，我们将创建客户端和服务器通信所需的 UDP socket。

```ruby
class DFTPClient < FTPBase
  def send_file(fn,contents)
    contents = contents.split('')
    req = ""
    req << @@Write.to_s + @key + "\u000" + fn + "\u000"
    @sock.send(req,0,@host,@port)
    optstr,client = @sock.recv(1024)
    ses = optstr[1..].split("\u000").first if optstr[0] == "\u001"
    i = 1
    while contents.size > 0
      msg = ""
      msg << "##{ses}###\u000\u000"
      msg << "##{contents.shift(1022 - msg.size).join("")}\u000"
      @sock.send(msg.to_s,0,@port)
      i = i + 1
    end
  end
end
```

我们的下一步是创建客户端代码。我们创建一个新类并整合基类的代码。我们创建了一个名为 `send_file` 的方法，它接收两个参数：文件名和数据。为了能将字符串视为数组，我们获取文件内容并按每个字符对其进行拆分。这允许我们轻松地移动数组（shift）并提取字符。接下来，我们创建请求字符串。该字符串由我们的写入值和密钥组成，以空字符（`\000`）结束；然后是文件名，同样以空字符结束。我们使用在初始化部分创建的 socket 将请求发送到主机和端口。`0` 值是 `send` 方法的标志位（flags）。我们不需要在数据包中设置任何特殊标志位，因此将值保持为 `0`。

接下来，我们从服务器接收数据包。`recv` 方法返回两个内容：收到的数据以及关于数据来源的信息。我们忽略这些信息并解析我们的二进制字符串。我们知道第一个字符应该是 ASCII 1。因此，我们验证该位是否已设置，获取直到空字符为止的剩余信息，并将其赋值给 `ses` 变量。现在我们已经协商好了会话（session），将开始向服务器发送数据。

# 注意

如果客户端和服务器之间的通信出现问题，两个组件都可能会挂起，等待可能永远不会到达的输出。如果失败，我们可以重启这两个部分并重试。如果我们要在现实世界中使用它，额外的错误处理将帮助我们克服这些挑战。

我们将 `while` 循环的计数器初始化为 1。只要 `contents` 数组中仍有数据，就会创建一个新消息。我们使用空字符分隔符将会话和数据包计数值添加到消息中。最后，我们添加下一段内容和另一个空终止符。我们进行一些计算以确保数据包限制在 1024 个字符以内，以便数据包能够通过。我们发送每个分块直到完成。我们已经有了使用 DFTP 模块发送文件的方法。让我们看看如何接收它们。

```ruby
class DFTPServer < DFTPBase
  def initialize(host,port,key)
    super(host,port,key)
    @sock.bind(@host, @port)
    @sessions = {}
  end
end
```

我们创建 `DFTPServer` 类，但比客户端类需要更多的设置。我们使用 `super` 方法创建一个新的 `initialize` 类来调用 `DFTPBase` 类的初始化方法。接下来，我们使用实例 `sock` 变量的 `bind` 方法创建监听器。我们还为会话创建了一个存储哈希（hash）。这将帮助我们支持多个并发文件传输。只有当我们获取每个会话的最后一个数据包时，我们才会写入会话的文件。

```ruby
def run
  loop {
    rkey,rfile,type,data,pkt,ses,last = nil
    text, sender = @sock.recvfrom(1024)
```

我们的下一步是创建一个方法，使服务器开始处理传入的连接。我们希望服务器一直运行，直到我们发出断开控制序列（Ctrl+C）。我们创建一个循环并初始化变量。`rkey` 将是客户端传递给服务器的密钥，`rfile` 是客户端想要执行的命令类型。在这种情况下，我们只处理写入操作。`data`、`pkt` 和 `ses` 在客户端代码中也用过，`last` 将用于指示我们获取了会话的最后一个数据包。我们从客户端接收代码并将数据存储在 `text` 变量中，将发送者信息存储在 `sender` 变量中。现在我们有了消息，必须弄清楚如何处理它。

```ruby
if text.start_with? ?@Read or text.start_with? ?@Write
  type = text[0]
  rkey,rfile = text[1..-1].split("\000", 0, 2)
else
  ses = text[0..text.index("\000")-1]
  pkt = text[ses.size+1..ses.index("\000",ses.size+1)-1]
  data = text[(ses.size + pkt.size + 2)..-2]
  ses = ses.to_i
  pkt = pkt.to_i
  last = 1 if text.size < 1024
end
```

如果我们的数据包内容以 `read` 或 `write` 字符开头，我们就知道这是一个读或写请求。我们将 `type` 变量设置为该字符，并根据预期的空分隔符值设置 `rkey` 和 `filename` 变量。如果第一个字符是其他内容（我们的会话应该始终如此），我们尝试像解析数据包一样解析它。我们获取从第一个字符到第二个空字符为止的会话信息，数据包号是剩余部分。我们将 `ses` 和 `pkt` 转换回整数，并检查信息是否小于 1024 个字符。如果是，则应该是我们的最后一个数据包。
