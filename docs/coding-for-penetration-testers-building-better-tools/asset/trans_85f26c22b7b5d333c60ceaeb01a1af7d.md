

```python
page = page + data
# close our socket and print the results
s.close()
print page
```

## 服务器通信

服务器通信比客户端通信更复杂。为了接受传入的连接，我们必须创建一个套字（socket），将其绑定到主机，然后监听连接。让我们来看一个例子。

```python
import socket
# Create a socket and then bind the socket to all addresses on
port 8080
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.bind(('', 8080))
# Listen for incoming connections
s.listen(1)
# Accept new connections, print "RANDOM DATA" and then close
# the socket
while True:
    conn, addr = s.accept()
    print('New connection from ', addr)
    conn.send("RANDOM DATA\n")
    conn.close()
s.close()
```

我们创建了一个将用于 TCP 连接的 socket。然后，我们使用 socket 的 `bind` 方法将 socket 绑定到所有接口上的 8080 端口。如果我们只想在本地回环 IP 上监听，可以在 `bind` 的第一个参数中使用 `127.0.0.1`，而不是示例代码中的空字符串。接下来，我们创建一个无限运行并接受传入连接的循环。`accept` 方法返回两个值：连接到我们服务器的 socket 以及远程主机的地址。我们打印一条消息表示我们有了新连接，然后向 socket 发送消息并将其关闭。

虽然我们现在有了一个基础服务器，但可能还有其他我们想做的事情。我们要与客户端交互，输入可能会有暂停。此外，我们可能想同时处理多个传入的连接。为了做到这一点并使脚本更加健壮，我们可以构建一个网络 shell（network shell）添加到我们的工具箱中。这个 shell可以通过 Netcat 访问。我们可以发送命令，输出将返回给我们。通常有更简单的方法来实现这一点，但当我们的传统工具被杀病毒软件或基于主机的入侵防御系统（HIPS）拦截时，这是一个很好的选择。因此让我们来看看更健壮的代码。

```python
# Create and bind socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.bind(('', 8080))
# Listen for up to 10 connections
s.listen(10)
```

input = [s]
最初，我们的代码看起来相似。但我们更改了 `listen` 方法，通过传递参数 10 让它接受 10 个 socket。我们还创建了一个名为 `input` 的新变量，并将我们的监听 socket 放入列表中。

```python
while True:
    # Check for sockets waiting read
    reader, exceptions = select.select(input, [], [])
```

我们的下一组代码利用了 `select` 模块中的 `select` 方法。该模块由冗余部门提供。`select` 方法接受三个参数：用于检查读取的 socket 列表、用于检查写入的 socket 列表以及用于检查错误的 socket 列表。由于在这个练习中我们只检查读取的 socket，因此我们提供了 `input` socket 列表，并对其他选项留空列表。`select` 方法返回三个列表：分别等待读取、写入和错误的列表。

```python
for sock in reader:
    # If the socket is our listener, accept a new connection
    if sock == s:
        c, addr = s.accept()
        print("New connection from", addr)
        input.append(c)
```

我们查看 `reader` 数组中的每个 socket。如果该 socket 是我们的监听器，我们就知道有了新连接。我们接受该连接，打印一条消息确认我们有了新连接，然后将其添加到我们的 `input` 列表中，这样我们就可以在 `select` 语句中检查它。这将允许我们知道客户端何时输入了新数据。

```python
# otherwise, it's a command to execute
else:
    command = sock.recv(1024)
    if command:
        shell = command.rstrip().split(" ")
        try:
            out = subprocess.Popen(shell, stdout=subprocess.PIPE).communicate()[0]
        except:
            out = "Command failed\n"
            sock.send(out)
    else:
        sock.close()
    input.remove(sock)
```

如果 socket 不等于我们的监听 socket，说明有一个客户端向我们发送了信息。我们可以将该信息读取到一个名为 `command` 的字符串中。如果没有数据在等待，说明 socket 已经关闭，我们需要关闭它。如果有数据在等待，我们需要对其进行清理以准备执行。首先，我们删除末尾的任何空格，然后将其拆分成单独参数传递给 shell。我们的网络 shell 只对命令有效，因此像 `cd`（更改目录）等操作可能无法工作。由于我们知道某些命令可能会失败，我们将进程创建命令封装在错误处理中，以防程序崩溃。

接下来，我们执行命令。使用 `Popen`（进程打开），我们使用从客户端传递的参数创建一个进程，并将输出重定向到管道。`communicate` 函数将与程序交互并返回输出列表。我们希望将该列表的第一个元素发送回客户端，因此我们使用 `communicate` 方法输出的第一个元素。接下来，我们将输出发送给客户端并回到循环，等待更多输入。

我们现在应该有一个可以工作的网络 shell 了。

```python
#!/usr/bin/python
import socket, select, os, subprocess
# Create and bind socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.bind(('', 8080))
# Listen for up to 10 connections
s.listen(10)
input = [s]
while 1:
    # Check for sockets waiting read
    reader, output, exceptions = select.select(input, [], [])
    for sock in reader:
        # If the socket is our listener, accept a new connection
        if sock == s:
            c, addr = s.accept()
            print("New connection from", addr)
            input.append(c)
        # otherwise, it's a command to execute
        else:
            command = sock.recv(1024)
            if command:
                shell = command.rstrip().split(" ")
                try:
                    out = subprocess.Popen(shell, stdout=subprocess.PIPE).communicate()[0]
                except:
                    out = "Command failed\n"
                    sock.send(out)
            else:
                sock.close()
            input.remove(sock)
```

## Scapy

Scapy 模块提供了高级数据包操作。它允许我们在开放系统互接栈的每一层操作数据包。Scapy 非常棒，但有一个学习曲线。首先，我们将查看 Scapy 交互式 shell 以帮助在编写脚本时熟悉。我们将构建包来处理两个测试问题：传输数据控制协议（ICMP）和处理嗅探数据。

### 注意

我们只是接触了 Scapy 的皮毛。Scapy 的主页位于 secdev.org/projects/scapy/。在这里你可以找到相关信息、文档并下载最新版本。

要执行交互式 shell，请在你的 Kali 窗口中输入 `scapy`。可能会出现警告消息。最后，我们会看到 Welcome to Scapy 以及熟悉的提示符。我们开始工作了。从哪里开始？要查看 Scapy 可以创建的数据包类型，输入 `ls()` 并按**回车**。

```
Can't import PyX. Won't be able to use psdump() or pdfdump().
WARNING: No route found for IPv6 destination :: (no default route?)
Welcome to Scapy (2.1.0)
>>> myip = IP()
>>> myip
<IP>
>>> myip.default_fields
{'frag': 0, 'src': None, 'proto': '0', 'tos': '0', 'dst': '127.0.0.1', 'chksum': None, 'len': 'None', 'Options': [], 'version': 4, 'flags': 0, 'ihl': None, 'ttl': 64, 'id': 1}
```

正如本节提到的，有两个错误。一个说我们无法创建 PDF 或 PostScript 文件，另一个说明我们没有 IPv6 地址。在这些例子中我们都不关心这些。我们使用 `IP()` 构造函数创建一个 IP 包并将该包赋值给 `myip` 变量。通过输入你的变量名，我们可以显示包中的内容。它是空的，这意味着包中包含默认值。现在我们要创建并发送一个基础 ping 包。我们需要填充

