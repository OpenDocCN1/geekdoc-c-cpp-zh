
```csharp
client.DropMulticastGroup(IPAddress.Parse(groupAddress));
```

当你使用以下选项同时启动接收方和发送方时，

```
-p 9400 -g 230.0.0.1
```

它们都属于同一组，多播即生效。与广播一样，你可以启动多个接收方和多个发送方。接收方将收到来自每个接收方的几乎所有消息。

### 使用套接字

HTTP 协议基于 TCP，因此 `Httpxx` 类提供了对 `TcpXX` 类的抽象层。不过，`TcpXX` 类给了你更多控制。使用套接字，你甚至可以比 `TcpXX` 或 `UdpXX` 类获得更多控制。使用套接字，你可以使用不同的协议，不仅仅是基于 TCP 或 UDP 的协议，还可以创建自己的协议。更重要的是，你可以对基于 TCP 或 UDP 的协议进行更多控制。

`SocketServerSender` 和 `SocketClient` 项目被实现为控制台应用程序（包），并使用以下依赖项和命名空间：

#### 依赖项

- `NETStandard.Library`
- `System.Net.NameResolution`

#### 命名空间

- `System`
- `System.Linq`
- `System.IO`
- `System.Net`
- `System.Net.Sockets`
- `System.Text`
- `System.Threading`
- `System.Threading.Tasks`
- `static System.Console`

### 使用套接字创建监听器

让我们从一个监听传入请求的服务器开始。服务器需要一个端口号，该端口号通过程序参数提供。然后，它调用 `Listener` 方法（代码文件 `SocketServer/Program.cs`）：

```
static void Main(string[] args)
{
    if (args.Length != 1)
    {
        ShowUsage();
        return;
    }

    int port;
    if (!int.TryParse(args[0], out port))
    {
        ShowUsage();
        return;
    }

    Listener(port);
    ReadLine();
}

private void ShowUsage()
{
    WriteLine("SocketServer port");
}
```

关于套接字最重要的代码在下面的代码片段中。监听器创建一个新的 `Socket` 对象。通过构造函数，提供了 `AddressFamily`、`SocketType` 和 `ProtocolType`。`AddressFamily` 是一个大型枚举，提供了许多不同的网络。例如，`DECnet`（1975 年由 Digital Equipment 发布，用作 PDP-11 系统之间的主要网络通信）、`Banyan VINES`（用于连接客户端机器），当然还有用于 IPv4 的 `InterNetwork` 和用于 IPv6 的 `InternetWorkV6`。如前所述，你可以将套接字用于大量网络协议。第二个参数 `SocketType` 指定套接字的类型。例如，`Stream` 用于 TCP，`Dgram` 用于 UDP，或者 `Raw` 用于原始套接字。第三个参数是 `ProtocolType` 的枚举。例如，`IP`、`Ucmp`、`Udp`、`IPv6` 和 `Raw`。你选择的设置需要匹配。例如，在 IPv4 上使用 TCP，地址族必须是 `InterNetwork`，套接字类型必须是 `Stream`，协议类型必须是 `Tcp`。要使用 IPv4 创建 UDP 通信，地址族需要设置为 `InterNetwork`，套接字类型设置为 `Dgram`，协议类型设置为 `Udp`。

```
public static void Listener(int port)
{
    var listener = new Socket(AddressFamily.InterNetwork,
        SocketType.Stream,
        ProtocolType.Tcp);
    listener.ReceiveTimeout = 5000; // receive timout 5 seconds
    listener.SendTimeout = 5000; // send timeout 5 seconds
    // etc.
```

```csharp
WriteLine($"{((IPEndPoint) client.RemoteEndpoint).Port}");
Task t = CommunicateWithClientUsingSocketAsync(client);
listener.Dispose();
WriteLine("Listener task closing");
}, cts.Token);
```

对于与客户端的通信，会创建一个新的任务。这使得监听任务可以立即进行下一次迭代，等待下一个客户端连接。`Socket` 类的 `Receive` 方法接受一个可以读取数据的缓冲区以及套接字的标志。该字节数组被转换为字符串，并使用 `Send` 方法带少量修改后发回客户端：

```csharp
private static Task CommunicateWithClientUsingSocketAsync(Socket socket)
{
	return Task.Run(() =>
	{
		try
		{
			using (socket)
			{
				bool completed = false;
				do
				{
					byte[] readBuffer = new byte[1024];
					int read = socket.Receive(readBuffer, 0, 1024,
						SocketFlags.None);
					string fromClient = Encoding.UTF8.GetString(readBuffer, 0, read);
					WriteLine($"read {read} bytes: {fromClient}");
					if (string.Compare(fromClient, "shutdown", ignoreCase: true) == 0)
					{
						completed = true;
					}
					byte[] writeBuffer = Encoding.UTF8.GetBytes($"echo {fromClient}");
					int send = socket.Send(writeBuffer);
					WriteLine($"sent {send} bytes");
				}
				while (!completed);
				WriteLine("closed stream and client socket");
			}
		}
		catch (Exception ex)
		{
			WriteLine(ex.Message);
		}
	});
}
```

服务器就绪状态保持不变。然而，让我们通过扩展抽象级别来查看不同的读写通信方式。

### 使用 Sockets 的 NetworkStream

你已经使用 `NetworkStream` 类与 `TcpClient` 和 `TcpListener` 类一起使用。`NetworkStream` 构造函数允许传递一个 `Socket`，因此你可以使用 `Stream` 方法 `Read` 和 `Write` 而不是套接字的 `Send` 和 `Receive` 方法。使用 `NetworkStream` 的构造函数你可以定义流是否应该拥有套接字。如果——像本代码片段中一样——流拥有套接字，则在关闭流时套接字将被关闭（代码文件 `SocketServer/Program.cs`）：

```
private static async Task
CommunicateWithClientUsingNetworkStreamAsync(
    Socket socket)
{
    try
    {
        using (var stream = new NetworkStream(socket, ownsSocket: true))
        {
            bool completed = false;
            do
            {
                byte[] readBuffer = new byte[1024];
                int read = await stream.ReadAsync(readBuffer, 0, 1024);
                string fromClient = Encoding.UTF8.GetString(readBuffer, 0, read);
                WriteLine($"read {read} bytes: {fromClient}");
                if (string.Compare(fromClient,"shutdown", ignoreCase: true) == 0)
                {
                    completed = true;
                }
                byte[] writeBuffer = Encoding.UTF8.GetBytes($"echo {fromClient}");
                await stream.WriteAsync(writeBuffer, 0, writeBuffer.Length);
            } while (!completed);
        }
        WriteLine("closed stream and client socket");
    }
    catch (Exception ex)
    {
        WriteLine(ex.Message);
    }
}
```

要在代码示例中使用此方法，你需要更改 `Listener` 方法以调用方法 `CommunicateWithClientUsingNetworkStreamAsync` 而不是方法 `CommunicateWithClientUsingSocketAsync`。

### 使用 Sockets 的 Readers 和 Writers

让我们再添加一层抽象层。因为 `NetworkStream` 派生自 `Stream` 类，所以你也可以使用读取器和写入器来访问套接字。你需要注意的是读取器和写入器的生命周期。调用读取器或写入器的 `Dispose` 方法也会释放底层流。这就是为什么选择了 `StreamReader` 和 `StreamWriter` 的构造函数，其中 `leaveOption` 参数可以设置为 `true`。这样，在释放读取器和写入器时，底层流不会被释放。`NetworkStream` 在外部 `using` 语句结束时被释放，这反过来会关闭套接字，因为这里套接字是被拥有的。使用套接字时使用写入器时需要注意的另一个方面是：默认情况下写入器不会刷新数据，因此它们会保留在缓存中，直到缓存填满。使用网络流时，你可能需要更快地获得答案。这里你可以将 `AutoFlush` 属性设置为 `true`（另一种选择是调用 `FlushAsync` 方法）：

```
public static async Task
CommunicateWithClientUsingReadersAndWritersAsync(
    Socket socket)
{
    try
    {
        using (var stream = new NetworkStream(socket, ownsSocket: true))
        using (var reader = new StreamReader(stream, Encoding.UTF8, false, 8192, leaveOpen: true))
        using (var writer = new StreamWriter(stream, Encoding.UTF8, 8192, leaveOpen: true))
        {
            writer.AutoFlush = true;
            bool completed = false;
            do
            {
                string fromClient = await reader.ReadLineAsync();
                WriteLine($"read {fromClient}");
                if (string.Compare(fromClient,"shutdown", ignoreCase: true) == 0)
                {
                    completed = true;
                }
                await writer.WriteLineAsync($"echo {fromClient}");
            } while (!completed);
        }
        WriteLine("closed stream and client socket");
    }
    catch (Exception ex)
    {
        WriteLine(ex.Message);
    }
}
```

要在代码示例中使用此方法，你需要更改 `Listener` 方法以调用方法 `CommunicateWithClientUsingReadersAndWritersAsync` 而不是方法 `CommunicateWithClientUsingSocketAsync`。

```csharp
{
    WriteLine("no IPv4 address");
    return;
}

using (var client = new Socket(AddressFamily.InterNetwork,
    SocketType.Stream, ProtocolType.Tcp))
{
    client.Connect(ipAddress, port);
    WriteLine("client successfully connected");
    var stream = new NetworkStream(client);
    var cts = new CancellationTokenSource();
    Task tSender = Sender(stream, cts);
    Task tReceiver = Receiver(stream, cts.Token);
    await Task.WhenAll(tSender, tReceiver);
}

}
catch (SocketException ex)
{
    WriteLine(ex.Message);
}
}
```

> **NOTE** *如果将地址列表的过滤更改为获取 IPv6 地址而不是 IPv4 地址，你还需要更改 `Socket` 调用以创建用于 IPv6 地址族的套接字。*

`Sender` 方法提示用户输入并使用 `WriteAsync` 方法将此数据发送到网络流。`Receiver` 方法使用 `ReadAsync` 方法从流接收数据。在用户输入终止字符串后，取消会通过 `CancellationToken` 从 `Sender` 任务发送：

```csharp
public static async Task Sender(NetworkStream stream,
    CancellationTokenSource cts)
{
    WriteLine("Sender task");
    while (true)
    {
        WriteLine("enter a string to send, shutdown to exit");
        string line = ReadLine();
        byte[] buffer = Encoding.UTF8.GetBytes($"{line}\r\n");
        await stream.WriteAsync(buffer, 0, buffer.Length);
        await stream.FlushAsync();
        if (string.Compare(line,"Shutdown", ignoreCase: true) == 0)
        {
            cts.Cancel();
            WriteLine("sender task closes");
            break;
        }
    }
}
```

```csharp
private const int ReadBufferSize = 1024;

public static async Task Receiver(NetworkStream stream,
    CancellationToken token)
{
    try
    {
        stream.ReadTimeout = 5000;
        WriteLine("Receiver task");
```
