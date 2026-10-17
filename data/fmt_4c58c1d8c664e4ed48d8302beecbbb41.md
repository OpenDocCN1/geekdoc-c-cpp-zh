
```python
#!/usr/bin/python
### 以写入模式打开文件
f = open("test.txt", "w")
f.write("Hello world\n")
f.close()
### 以追加模式打开文件
f = open("test.txt", "a")
f.write("This is the end\n")
f.close()
### 以读写模式打开文件
f = open("test.txt", "r+")
### 文件内容
print("Current contents are:\n" + f.read())
### 跳转到文件末尾追加
f.seek(0,2)
print("Starting file length is %d" % f.tell())
f.write("This is the new end!\n")
print("End file length is %d" % f.tell())
### 回到文件开头读取
f.seek(0,0)
print("\nNew contents are:\n" + f.read())
f.close()
```

### 异常处理

有时候，良好的脚本也会出现问题。异常处理允许我们处理这些问题，并在发生意料错误时，从显示的堆栈跟踪中恢复执行或呈现出更友好的错误信息。异常处理的核心元素是 `try` 和 `except` 关键字。`try` 代码块是我们想要尝试执行的代码。如果我们的 `try` 块中发生错误，我们有一个 `except` 语句来处理它。异常处理块中可能出现的另外两个元素是 `else` 和 `finally`。`else` 关键字用于在没有抛出异常时运行的代码，而 `finally` 关键字用于无论是否发生错误都应该运行的代码。

让我们来看一个实际的例子。当我们打开文件时，文件可能不存在。我们可以通过多种方式解决这个问题，但由于这是异常处理章节，我们可能应该尝试这种方法。

```python
try:
    f = open("/tmp/nessus.nbe")
    print(f.read())
    f.close()
except IOError:
    print("Error occurred opening file")
except:
    print("Unknown error occurred")
else:
    print("File contents successfully read")
finally:
    print("Thanks for playing!")
```

这段示例代码包含了我们所有的条件。在 `try` 块中，我们尝试打开文件并打印内容。如果文件打开失败，代码将抛出 `IOError` 异常，我们通过 `except` 捕获它。如果发生了与我们预期的不同类型的错误，第二个 `except` 语句将捕获并打印不同的错误消息。如果没有错误，将打印成功消息。无论 `try` 块中发生了其他什么，最后的语句都会执行。

尝试创建文件然后删除文件，并查看差异：

- # 测试我们的异常处理代码

`$ touch /tmp/nessus.nbe`

`$ python exception.py`

File contents successfully read

Thanks for playing!

### 如果没有文件，我们应该得到一个异常

`$ rm /tmp/nessus.nbe`

`$ python exception.py`

Error occurred opening file

Thanks for playing!

### 没有异常处理的情况下

`$ python withoutexception.py`

```python
Traceback (most recent call last):
File "a.py", line 3, in <module>
  f = open("/tmp/nessus.nbe")
IOError: [Errno 2] No such file or directory: '/tmp/nessus.nbe'
```

### 网络通信

当我们进行网络渗透测试并需要自定义脚本时，Python 是一个常见的解决方案。网络库非常丰富，可以用于构建漏洞的 Basic socket 操作路由也非常易于使用。在这里，我们将分两个独立的部分探索网络概念：客户端通信和服务器通信。

#### 客户端通信

客户端通信将涵盖我们使用 sockets 的大部分部分工作。我们最初将关注使用基础 sockets。它们在构建网络漏洞、执行原始 socket（raw sockets）或当我们需要一些快速网络技巧来完成任务时将非常有用。对于更广泛的网络协议，使用能够处理协议中复杂部分的 Python 模块将是有意义的。

连接到主机涉及两个操作：创建一个 socket 并将该 socket 连接到远程主机。让我们来看代码，然后检查每个操作的功能：

```python
### 构建一个 socket 并连接到 google.com
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("www.google.com", 80))
```

构建一个 socket，我们需要指定两个选项：socket 族（family）和 socket 类型（type）。在这种情况下，socket 族是 `AF_INET`，它是一个 IPv4 socket。其他族包括用于 IPv6 的 `AF_INET6`、用于本地 socket 的 `AF_UNIX` 以及用于原始 socket 的 `AF_RAW`。第二个选项是 socket 类型，在这种情况下，它是 `SOCK_STREAM` socket。`SOCK_STREAM` socket 是传输控制协议（TCP）风格的 socket，但我们也有选择使用 `SOCK_DGRAM` 用于用户数据报协议（UDP）风格的 socket 或使用 `SOCK_RAW` 用于原始 socket 的选项。

接下来，我们将 socket 连接到远程主机。我们必须给出一个主机名或 IP 地址以及我们想要连接的端口。`connect` 语句打开到远程主机的连接。现在我们有了对该 socket 进行读写的能力。让我们来看一些基础代码，从远程主机获取 Web 页面。

```python
### 发送一个基础 http 请求
s.send("GET / HTTP/1.0\nHost: www.google.com\n\n")
page = ""
### 当数据仍在返回时，追加到我们的 page 变量
while 1:
    data = s.recv(1024)
    if data == "":
        break
    page = page + data
```

socket 方法接收一个参数：你想要发送的字符串。在这里，我们正在向 Google 发送 Web 请求。我们将 `page` 变量初始化为空字符串。最后，我们创建并使用循环接收数据。我们想要循环是因为 `recv` 将读取多达参数指定的数据量——在这种情况下，是 1024 字节。我们希望继续读取直到获取所有数据。`recv` 方法在没有更多数据可读时将返回空字符串，因此我们检查该条件以跳出 while 循环。一旦有了数据，我们就关闭 socket 并打印数据。让我们来看完成的脚本：

```python
#!/usr/bin/python
import socket
### 构建一个 socket 并连接到 google.com
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("www.google.com", 80))
### 发送一个基础 http 请求
s.send("GET / HTTP/1.0\nHost: www.google.com\n\n")
page = ""
### 当数据仍在返回时，追加到我们的 page 变量
while 1:
    data = s.recv(1024)
    if data == "":
        break
    page = page + data
### 关闭 socket 并打印数据
s.close()
print(page)
```

此脚本将处理 IPv4 sockets。但如果我们想使用 IPv6，或者我们预先不知道将拥有哪个 IP 地址 呢？我们可以利用一些其他的 socket 功能来搜索可用的 IP 地址，它会解决这个问题。

```python
### 构建一个 socket 并连接到 google.com
af, type, proto, name, conn = socket.getaddrinfo("www.google.com", 80, 0, socket.SOCK_STREAM)
s = socket.socket(af, type)
s.connect(conn)
```

通过使用 `getaddrinfo` 函数，我们可以指定主机名、端口、族、socket 类型和协议，它将返回我们所需的信息。在这种情况下，我们向它传递了主机、服务器端口 80、TCP 协议以及用于族 类型的 0。这将允许它为我们解决问题。该函数返回一个可能的 IP 地址数组，这些地址可以很好地配合 socket 和族类型。在这种情况下，我们想要列表中的第一个。我们将返回的信息赋值给 `af`, `type`, `proto`, `name` 和 `conn` 变量，其中 `conn` 是包含 ip 和端口的元组，我们可以将其用于 `connect` 语句。

```python
page = page + data
# close our socket and print the results
s.close()
print page
```

#### 服务器通信

服务器通信比客户端通信更复杂。为了接受传入的连接，我们必须创建一个套字（socket），将其绑定到主机，然后监听连接。让我们来看一个例子。

```python
import socket
#### Create a socket and then bind the socket to all addresses on
port 8080
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.bind(('', 8080))
#### Listen for incoming connections
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
#### Create and bind socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.bind(('', 8080))
# Listen for up to 10 connections
s.listen(10)
```

`input = [s]`

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
#### otherwise, it's a command to execute
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
