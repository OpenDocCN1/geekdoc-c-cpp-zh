
来自 McAfee、Symantec、IBM、腾讯等许多供应商那里，存在着许多专业工具和技术。然而，要深入理解它们的作用、工作原理，以及其调查价值是否完整，在某种程度上仍然是一个谜团。还有像 `Wireshark` 这样的免费工具可以执行网络数据包的捕获和分析。

为了开启这些技术的一些理解，我将检查现代网络调查方法的基础。我将利用 Python 库以及几个第三方库来熟悉这些食谱中的示例。我将详细地介绍这些示例，所以如果这是你第一次接触网络编程，你将获得足够的细节。

## 什么是套字（sockets）？

## 网络调查基础 207

`192.168.0.1` 网络地址 本地主机

在此示例中，本地的网络设备、路由器、防火墙等将具有相同的网络部分（`192.168.0`），但每个都有从 0 到 255 的唯一范围。然而，只有 254 个地址是可用的，因为 `192.168.0.0` 是网络地址，不能分配给本地主机，而 `192.168.0.255` 专用广播地址。

基于此，可以使用简单的 Python 内置功能创建 IP 地址列表。这些语言功能包括字符串、`range` 函数和“for 循环”。

```python
# 指定基础网络地址（前三个字节节）
ipBase = '192.168.0.'

# 接下来是一个用于存储完整 IP 地址列表的空列表
ipList = []
# 最后，使用 range 函数遍历 0-255 的可能本地主机地址
# 然后将每个完整地址添加到 ipList 中
# 注意我使用了 str(ip) 函数将 ipBase 与 0-255 的数字连接
```

```python
for ip in range(0,256):
    ipList.append(ipBase+str(ip))
    print ipList.pop()
```

程序输出摘要

`192.168.0.0`

`192.168.0.1`

`192.168.0.2`

`192.168.0.3`

......跳过的项目

`192.168.0.252`

`192.168.0.253`

`192.168.0.254`

`192.168.0.255`

图 8.1

最简单的局域网。

![](img/7795602d6b06352c7ac43216_0.png)

# 208 第 8 章 网络取证：第一部分

![](img/77956026d6b06352c72ae6ac437ce8ab_218_0.png)

图 8.2

隔离的 *localhost* 环回。

## 使用 sockets 进行简单的网络客户端服务器连接

为了介绍 Python 提供的 sockets API，我将创建一个简单的网络服务器和客户端。为了实现这一点，我将使用同一个主机（也就是说，客户端和服务器将使用同一台机器上的相同 IP 地址），特别是特殊用途且保留的 *localhost* 环回 IP 地址 `127.0.0.1`。这个标准环回 IP 在几乎所有系统中都是相同的，发送到 `127.0.0.1` 的消息永远不会到达外部，而是自动返回给 *localhost*。当你开始尝试网络编程时，请使用 `127.0.0.1` 作为你的首选地址，直到你完善代码并准备好在真实网络上操作（图 8.2）。

为了完成任务，我将创建两个 Python 程序：(1) 服务器和 (2) 客户端。为了让其工作，两个应用程序必须就用于支持通信通道的端口达成一致。（我们已经决定使用 *localhost* 环回 IP 地址 `127.0.0.1`。）端口号范围在 0 到 65535 之间（基本上是任何无符号 16 位整数值）。你应该避开小于1024的低端口，因为它们被分配给了标准网络服务（实际上，现在的注册端口范围高达 49,500，但我们当前的系统中没有这些）。对于此应用程序，我将使用端口 `5555`，因为它很容易记忆。现在我已经定义了 IP 地址和端口号，拥有建立连接所需的所有信息。

IP 地址和端口：可以从更物理的角度来思考。将 IP 地址视为邮局的街道地址，将端口视为邮局内我想要投递的特定信箱。

### server.py 代码

```python
#
# 服务器目标
# 1) 设置一个简单的监听 Socket
# 2) 等待连接请求
# 3) 在端口 5555 上接受连接
# 4) 连接成功后向客户端发送消息
#
```

```python
import socket            # 标准库 Socket 模块

# 创建 Socket

myServerSocket = socket.socket()

# 获取本地主机地址

localHost = socket.gethostname()

# 指定接受连接的本地端口

localPort = 5555

# 将 myServerSocket 绑定到 localhost 和指定的端口

# 注意 bind 调用需要一个参数，但该

# 参数是一个元组（注意括号的使用）

myServerSocket.bind(localHost, localPort)

# 开始监听连接

myServerSocket.listen(1)

# 等待连接请求

# 注意这是一个同步调用

# 意味着程序将停止直到

# 收到连接

# 一旦收到连接

# 我们将接受连接并获取连接者的

# ip 地址

print('Python-Forensics .... 等待连接请求')

conn, clientInfo = myServerSocket.accept()

# 打印一条消息表示我们已收到连接

print('收到来自的连接:', clientInfo)

# 使用从 myServerSocket.accept() 调用返回的连接对象 'conn'

# 向连接者发送消息

# 在响应中包含客户端的 IP 地址和端口

conn.send('Connection Confirmed: ' + clientInfo[0] + ':Port ' + str(clientInfo[1]))
```

## client.py 代码

接下来是用于与服务器建立连接的客户端代码。

```python
# 客户端目标

### 1) 设置一个客户端 Socket

# 2) 尝试连接到端口 5555 服务器

# 3) 等待回复

### 4) 打印从服务器接收的消息
```

```python
import socket # 标准库 Socket 模块

MAX_BUFFER = 1024 # 设置最大接收大小

# 创建 Socket
myClientSocket = socket.socket()

# 获取本地主机地址
localHost = socket.gethostname()
# 指定接受连接的本地端口
localPort = 5555

# 尝试连接到服务器
myClientSocket.connect((localHost, localPort))

# 等待回复
msg = myClientSocket.recv(MAX_BUFFER)
# 打印从服务器接收的消息
print('收到服务器的消息:', msg)

### 关闭连接
myClientSocket.close()
```

# 拉米斯船长：重新验证我们的目标范围... 仅一次 Ping 213

### ping.py

`ping-py` 模块可在 `http://www.g-loaded.eu/2009/10/30/Python-ping/` 获取，这是一个完全用 Python 编写的用于处理 ICMP 操作细节的开源模块。由于这是一个开源模块，我将源代码包含在此处以供你查阅，并包含了所有相关的属性和修订版本。

[PYTHON PING]

```
#!/usr/bin/env Python
***
```

一个使用原始套字（raw socket）的纯 Python ping 实现。

请注意，ICMP 消息只能从以 root 权限运行的进程发送。

源自 Linux netkit 分发的 `ping.c`。该代码版权所有 (c) 1989 加加州大学董事会。该代码反转源自美国陆军弹道研究实验室的 Mike Muuss 在 1983 年 12 月编写的代码，并已置于公共领域。向他们表示感谢。

Bug 自然是我的。我很乐意听到它们的反馈。这里确实存在字大小（word-size）依赖性。

版权 (c) Dixon Cowles, <http://www.visi.com/~mdc/>。根据 GNU 通用公共许可证第 2 版分发。不提供任何形式的保证。

来自 Dixon Cowles 的原始版本：

-> `ftp://ftp.visi.com/users/mdc/ping.py`

由 Jens Demier 重写：

-> `http://www.Python-forum.de/post-6912.html@69122`

由 George Notaras 重写：

-> `http://www.g-loaded.eu/2009/10/30/Python-ping/`

修订历史

~~~~~~~~~~~~~~~~~~~~~

2009 年 11 月 8 日

~~~~~~~~~~~~~~~~~~~~~

提高了与 GNU/Linux 系统的兼容性。

+   修复者：

* George Notaras -- http://www.g-loaded.eu

报告者：

* Chris Hallman -- http://cdhallman.blogspot.com

# 第 8 章 网络取证：第一部分

此版本的更改：

- 复用 `time.time()` 代替 `time.clock()`。2007 年的实现仅在 Microsoft Windows 下运行。在 GNU/Linux 上运行失败。

`time.clock()` 在两个操作系统下的行为不同[1]。

[1] http://docs.python.org/library/time.html@time.clock

2007 年 5 月 30 日

+   - Jens Diemer 的简要重写：

- 将星号导入更改为普通导入

- 将 `time.time()` 替换为 `time.clock()`

- 删除 "return None"（或仅改为 "return"）

- 在 `checksum()` 中将 "str" 重命名为 "source_string"

1997 年 11 月 22 日

初步草案。没太大作用，更多是尝试猜测我（或其他人）未来可能需要的功能，我只放了目前现在需要的。

1997 年 12 月 16 日

由于某些原因，当在 Solaris 2.X for SPARC 下运行时，`checksumbytes` 的顺序是错误的，但在 Linux x86 上运行正常。由于我不知道哪里错了，我交换了字节然后在 `htons()` 上进行操作。

2000 年 12 月 4 日

更改了 `struct.pack()` 调用，将校验和和 ID 打包为无符号。感谢 Jerome Pincheval 的修复。

最后提交信息：

~~~~~~~~~~~~~~~~~~~~~

$LastChangedDate: $$

$Rev: $$

$Author: $$

""

```
import os, sys, socket, struct, select, time

# 源自 /usr/include/linux/icmp.h; 你的情况可能有所不同。
ICMP_ECHO_REQUEST = 8 # 在 Solaris 上似乎相同。

def checksum(source_string):
    """
```

我不确定这是否是正确的，但测试表明***

它与 `ping.c` 提供了相同的答案。

```
sum = 0
countTo = (len(source_string)/2)*2
count = 0
while count<countTo:
    thisVal = ord(source_string[count + 1])*256 or
    (source_string[count])
    sum = sum + thisVal
    sum = sum + 0ffff # Necessary
    count = count + 2
```

```
if countLen(source_string):
    sum = sum + ord(source_string[len(source_string) - 1])
    sum = sum + 0ffff # Necessary
```

```
sum = (sum >> 16) + (sum & 0xffff)
sum = sum + (sum >> 16)
answer = ~sum
answer = answer & 0xffff
```

@ 交换字节。该死我不知道为什么。

answer = answer >> 8 | (answer << 8 & 0ffff)

```
return answer
```

```
receive_one_ping(my_socket, ID, timeout):
***从 socket 接收 ping。
***
timeLeft = True
while True:
    startedSelect = time.time()
    whatReady = select.select([my_socket], [], [], timeLeft)
    longInSelect = (time.time() - startedSelect)
    if whatReady[0] == []: # Timeout
    return
```

```
timeReceived = time.time()
recPacket, addr = my_socket.recvfrom(1024)
icmpHeader = recPacket[20:28]
type, code, checksum, packetID, sequence = struct.unpack(
    "BBHHI", icmpHeader)
if packetID == ID:
    bytesDouble = struct.calcsize("d")
```

```
timeSent = struct.pack("d", recPacket[28:28 + bytesDouble])[0]
return timeReceived - timeSent
timeLeft = timeLeft - longInSelect
if timeLeft <= 0:
return
```

```
def send_one_ping(my_socket, dest_addr, ID):
向 dest_addr 发送一个 ping。
socket.gethostbyname(dest_addr)

# Header 为 type (8), code (8), checksum (16), sequence (16)
my_checksum = 0

# 用 0 创建一个伪头部。
header = struct.pack(
    "bbHHh", ICMP_ECHO_REQUEST, 0, socket.htons(my_checksum),
ID, 1)
bytesDouble = struct.calcsize("d")
data = (192 - bytesDouble) * "Q"
data = struct.pack("d", time.time()) + data
```

```
# 计算数据和伪头部的校验和。
my_checksum = checksum(header + data)

# 现在我们有了正确的校验和，把它放进去。构造一个新头部放入伪头部要容易。
header = struct.pack(
    "bbHHh", ICMP_ECHO_REQUEST, 0, socket.htons(my_checksum), ID, 1)
packet = header + data
my_socket.sendto(packet, (dest_addr, 1)) # 我不知道关于
```

```
def do_one(dest_addr, timeout):
    ***返回延迟（秒）或在超时时返回空。
***
icmp = socket.getprotobyname("icmp")
try:
    my_socket = socket.socket(socket.AF_INET, socket.SOCK_RAW,
    icmp)
except socket.error(errno, msg):
    if errno == 1: # 操作不允许
注意 ICMP 消息从从 root 权限运行的进程发送。
raise socket.error(msg) # 抛出原始错误
```

```
my_ID = os.getpid() & 0xFFFF
```

```
send_one_ping(my_socket, dest_addr, my_ID)
delay = receive_one_ping(my_socket, my_ID, timeout)
```

```
my_socket.close()
return delay
def verbose_ping(dest_addr, timeout=2, count=4):

"""
向 dest_addr 发送带有给定超时时间的 ping 并显示结果。
"""
```

```
for i in xrange(count):
    print "%s..." % dest_addr,
    try:
        delay = do_one(dest_addr, timeout)
    except socket.gaierror, e:
        print("failed. socket error: %s" % e[1])
        break
```

```
if delay == None:
    print("failed. timeout within sec" % timeout)
else:
    delay = delay * 1000
    print("ping get in %0.4fms" % delay)
```
