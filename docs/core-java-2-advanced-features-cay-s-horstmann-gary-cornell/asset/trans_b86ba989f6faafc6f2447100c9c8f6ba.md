
```java
catch (InterruptedIOException exception)
{
    react to timeout
}
```

还有一个需要解决的超时问题。构造函数

```
Socket(String host, int port)
```

可能会无限期阻塞，直到建立与主机的初始连接。

你可以先构造一个未连接的套接字，然后使用超时来连接它，从而克服这个问题：

```
Socket s = new Socket();
s.connect(new InetSocketAddress(host, port), timeout);
```

关于如何允许用户随时中断套接字连接，请参见第 250 页的 4.3 节“可中断套接字”。

| 成员 | 描述 |
|---|---|
| `java.net.Socket` 1.0 |  |
| `Socket()` 1.1 | 创建一个尚未连接的套接字。 |
| `void connect(SocketAddress address)` 1.4 | 将此套接字连接到给定地址。 |
| `void connect(SocketAddress address, int timeoutInMilliseconds)` 1.4 | 将此套接字连接到给定地址；如果时间间隔已过，则返回。 |
| `void setSoTimeout(int timeoutInMilliseconds)` 1.1 | 设置此套接字上读取请求的阻塞时间。如果达到超时时间，则会引发 InterruptedIOException。 |
| `boolean isConnected()` 1.4 | 如果套接字已连接，则返回 true。 |
| `boolean isClosed()` 1.4 | 如果套接字已关闭，则返回 true。 |

### 4.1.4 Internet 地址

通常，你不必过于担心 Internet 地址——即由 4 个字节（对于 IPv6，则为 16 个字节）组成的数字主机地址，例如 129.6.15.28。不过，如果需要在主机名和 Internet 地址之间进行转换，可以使用 `InetAddress` 类。

```java
public static void main(String[] args) throws IOException
{
    if (args.length > 0)
    {
        String host = args[0];
        InetAddress[] addresses = InetAddress.getAllByName(host);
        for (InetAddress a : addresses)
            System.out.println(a);
    }
    else
    {
        InetAddress localHostAddress = InetAddress.getLocalHost();
        System.out.println(localHostAddress);
    }
}
```

**java.net.InetAddress 1.0**

- `static InetAddress getByName(String host)` 为给定主机名构造一个 InetAddress，或构造一个包含所有 Internet 地址的数组。
- `static InetAddress[] getAllByName(String host)`
- `static InetAddress getLocalHost()` 为本地主机构造一个 InetAddress。
- `byte[] getAddress()` 返回一个包含数字地址的字节数组。
- `String getHostAddress()` 返回一个用句点分隔的十进制数字表示的 IP 地址，例如 "129.6.15.28"。
- `String getHostName()` 返回主机名。

## 4.2 实现服务器

现在我们已经实现了一个从 Internet 接收数据的基本网络客户端，接下来让我们编写一个可以向客户端发送信息的简单服务器。在上一节中，我们已经实现了一个从 Internet 接收数据的基本网络客户端。在接下来的几节中，我们将编写一个可以向客户端发送信息的简单服务器。

### 4.2.1 服务器套接字

服务器程序在启动时会等待客户端连接到其端口。对于我们的示例程序，我们选择了端口号 8189，该端口未被任何标准服务使用。ServerSocket 类会建立一个套接字。在我们的示例中，以下命令

```
ServerSocket s = new ServerSocket(8189);
```

建立一个监视端口 8189 的服务器。以下命令

```
Socket incoming = s.accept();
```

告诉程序无限期等待，直到有客户端连接到该端口。一旦有人通过网络发送正确的请求连接到该端口，此方法就会返回一个表示所建立连接的 Socket 对象。你可以使用该对象获取输入流和输出流，如下代码所示：

```
InputStream inStream = incoming.getInputStream();
OutputStream outStream = incoming.getOutputStream();
```

服务器发送到服务器输出流的所有内容都会成为客户端程序的输入，而客户端程序的所有输出最终都会进入服务器输入流。

在本章的所有示例中，我们都通过套接字传输文本。因此，我们将这些流转换为扫描器和写入器。

```
Scanner in = new Scanner(inStream, "UTF-8");
PrintWriter out = new PrintWriter(new OutputStreamWriter(outStream, "UTF-8"),
    true /* autoFlush */);
```

让我们向客户端发送一条问候语：

```
out.println("Hello! Enter BYE to exit.");
```

当你使用 telnet 连接到端口 8189 上的这个服务器程序时，你会在终端屏幕上看到这条问候语。

在这个简单服务器中，我们只是逐行读取客户端的输入并将其回显。这演示了程序接收输入。实际服务器显然会根据输入计算并返回答案。

```
String line = in.nextLine();
out.println("Echo: " + line);
if (line.trim().equals("BYE")) done = true;
```

最后，我们关闭传入套接字。

```
incoming.close();
```

这就是全部内容。每个服务器程序（例如 HTTP Web 服务器）都会持续执行以下循环：

- 1. 它通过传入数据流从客户端接收命令（“给我这个信息”）。
- 2. 它解码客户端命令。
- 3. 它收集客户端请求的信息。
- 4. 它通过传出数据流将信息发送给客户端。

程序清单 4.3 是完整的程序。

**程序清单 4.3  `server/EchoServer.java`**

```java
package server;

import java.io.*;
import java.net.*;
import java.util.*;

/**
 * This program implements a simple server that listens to port 8189 and echoes back all client
 * input.
 * @version 1.21 2012-05-19
 * @author Cay Horstmann
 */
public class EchoServer
{
    public static void main(String[] args) throws IOException
    {
        // establish server socket
        try (ServerSocket s = new ServerSocket(8189))
        {
            // wait for client connection
            try (Socket incoming = s.accept())
            {
                InputStream inStream = incoming.getInputStream();
                OutputStream outStream = incoming.getOutputStream();

                try (Scanner in = new Scanner(inStream, "UTF-8"))
                {
                    PrintWriter out = new PrintWriter(
                        new OutputStreamWriter(outStream, "UTF-8"),
                        true /* autoFlush */);

                    out.println("Hello! Enter BYE to exit.");

                    // echo client input
                    boolean done = false;
                    while (!done && in.hasNextLine())
                    {
                        String line = in.nextLine();
                        out.println("Echo: " + line);
                        if (line.trim().equals("BYE")) done = true;
                    }
                }
            }
        }
    }
}
```

要试用它，请编译并运行该程序。然后使用 telnet 连接到服务器 localhost（或 IP 地址 127.0.0.1）和端口 8189。

如果你直接连接到 Internet，那么世界上任何人都可以访问你的回显服务器，只要他们知道你的 IP 地址和这个神奇的端口号。

当你连接到该端口时，将看到图 4.4 所示的消息：

```
Hello! Enter BYE to exit.
```

![](img/7dd923a566750151a3aab0dacd0cdaa5_264_0.png)

**图 4.4** 访问回显服务器

输入任意内容，并观察屏幕上回显的输入。输入 **BYE**（全部大写字母）以断开连接。服务器程序也将终止。

| 成员 | 描述 |
|---|---|
| `java.net.ServerSocket` 1.0 |  |
| `ServerSocket(int port)` | 创建一个监视某个端口的服务器套接字。 |
| `Socket accept()` | 等待连接。此方法会阻塞（即空闲）当前线程，直到建立连接。该方法返回一个 `Socket` 对象，程序可通过该对象与正在连接的客户端通信。 |
| `void close()` | 关闭服务器套接字。 |

### 4.2.2 为多个客户端提供服务

前一个示例中的简单服务器存在一个问题。假设我们希望允许多个客户端同时连接到我们的服务器。通常，服务器会持续运行在一台服务器计算机上，而来自 Internet 各处的客户端可能希望同时使用它。拒绝多个连接会让任何一个客户端都能通过长时间连接来独占服务。借助线程的魔力，我们可以做得更好。

每当程序建立了一个新的套接字连接——也就是说，每当对 `accept()` 的调用返回一个套接字——我们就启动一个新线程来处理服务器与该客户端之间的连接。主程序只会返回并等待下一个连接。为此，服务器的主循环应如下所示：

```
while (true)
{
    Socket incoming = s.accept();
    Runnable r = new ThreadedEchoHandler(incoming);

    Thread t = new Thread(r);
    t.start();
}
```

`ThreadedEchoHandler` 类实现了 `Runnable`，并在其 run 方法中包含与客户端通信的循环。

```
class ThreadedEchoHandler implements Runnable
{
    . . .
}
```

