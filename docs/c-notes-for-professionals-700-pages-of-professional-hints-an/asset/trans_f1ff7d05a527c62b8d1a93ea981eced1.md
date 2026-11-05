
## 第97章：文件和流 I/O

| 参数 | 详情 |
|---|---|
| path | 文件的位置。 |
| append | 如果文件存在，true 会将数据添加到文件末尾（追加），false 会覆盖文件。 |
| text | 要写入或存储的文本。 |
| contents | 要写入的字符串集合。 |
| source | 你想要使用的文件的位置。 |
| dest | 你希望文件去到的位置。 |

管理文件。

### 第97.1节：使用 System.IO.File 类从文件读取

你可以使用 System.IO.File.ReadAllText 函数将文件的全部内容读入一个字符串。

```
string text = System.IO.File.ReadAllText(@"C:\MyFolder\MyTextFile.txt");
```

你也可以使用 System.IO.File.ReadAllLines 函数将文件作为行数组读取：

```
string[] lines = System.IO.File.ReadAllLines(@"C:\MyFolder\MyTextFile.txt");
```

### 第97.2节：通过 IEnumerable 惰性逐行读取文件

处理大文件时，你可以使用 System.IO.File.ReadLines 方法将文件的所有行读入 IEnumerable<string>。这与 System.IO.File.ReadAllLines 类似，不同之处在于它不会一次性将整个文件加载到内存中，从而在处理大文件时更高效。

```
IEnumerable<string> AllLines = File.ReadLines("file_name.txt", Encoding.Default);
```

*File.ReadLines 的第二个参数是可选的。当需要指定编码时，你可以使用它。*

需要注意的是，调用 ToArray、ToList 或其他类似函数会强制一次性加载所有行，这意味着使用 ReadLines 的好处将被抵消。如果使用此方法，最好使用 foreach 循环或 LINQ 对 IEnumerable 进行枚举。

### 第97.3节：使用 StreamWriter 异步写入文件文本

```
// filename is a string with the full path
// true is to append
using (System.IO.StreamWriter file = new System.IO.StreamWriter(filename, true))
{
    // Can write either a string or char array
    await file.WriteAsync(text);
}
```

### 第97.4节：复制文件

### File 静态类

File 静态类可以轻松用于此目的。

```
~~~csharp
File.Copy(@"sourcePath\abc.txt", @"destinationPath\abc.txt");
File.Copy(@"sourcePath\abc.txt", @"destinationPath\xyz.txt");
~~~
```

**备注：** 通过此方法，文件将被复制，这意味着它将从源读取然后写入目标路径。这是一个资源消耗的过程，其耗时与文件大小相关，如果不使用线程，可能会导致你的程序冻结。

### 第97.5节：使用 System.IO.StreamWriter 类向文件写入行

The `System.IO.StreamWriter` class:

> 用于以特定编码向流写入字符的 TextWriter 的实现。

使用 `WriteLine` 方法，你可以逐行向文件写入内容。

注意 `using` 关键字的用法，它确保 StreamWriter 对象在超出作用域后立即被释放，从而关闭文件。

```
~~~csharp
string[] lines = { "My first string", "My second string", "and even a third string" };
using (System.IO.StreamWriter sw = new System.IO.StreamWriter(@"C:\MyFolder\OutputText.txt"))
{
    foreach (string line in lines)
    {
        sw.WriteLine(line);
    }
}
~~~
```

请注意，StreamWriter 的构造函数可以接收第二个 `bool` 参数，允许追加到文件而不是覆盖文件：

```
~~~csharp
bool appendExistingFile = true;
using (System.IO.StreamWriter sw = new System.IO.StreamWriter(@"C:\MyFolder\OutputText.txt", appendExistingFile))
{
    sw.WriteLine("This line will be appended to the existing file");
}
~~~
```

### 第97.6节：使用 System.IO.File 类写入文件

你可以使用 `System.IO.File.WriteAllText` 函数将字符串写入文件。

```
~~~csharp
string text = "String that will be stored in the file";
System.IO.File.WriteAllText(@"C:\MyFolder\OutputFile.txt", text);
~~~
```

你也可以使用 `System.IO.File.WriteAllLines` 函数，它接收 `IEnumerable<String>` 作为第二个参数（与前一个示例中的单个字符串相反）。这让你可以从行数组写入内容。

```
~~~csharp
string[] lines = { "My first string", "My second string", "and even a third string" };
System.IO.File.WriteAllLines(@"C:\MyFolder\OutputFile.txt", lines);
~~~
```

## 第98章：网络

### 第98.1节：基本 TCP 通信客户端

此代码示例创建一个 TCP 客户端，通过套接字连接发送 "Hello World"，然后在关闭连接之前将服务器响应写入控制台。

```csharp
// Declare Variables
string host = "stackoverflow.com";
int port = 9999;
int timeout = 5000;

// Create TCP client and connect
using (var _client = new TcpClient(host, port))
using (var _netStream = _client.GetStream())
{
    _netStream.ReadTimeout = timeout;

    // Write a message over the socket
    string message = "Hello World!";
    byte[] dataToSend = System.Text.Encoding.ASCII.GetBytes(message);
    _netStream.Write(dataToSend, 0, dataToSend.Length);

    // Read server response
    byte[] recvData = new byte[256];
    int bytes = _netStream.Read(recvData, 0, recvData.Length);
    message = System.Text.Encoding.ASCII.GetString(recvData, 0, bytes);
    Console.WriteLine(string.Format("Server: {0}", message));
}// The client and stream will close as control exits the using block (Equivalent but safer than calling Close());
```

### 第98.2节：从 Web 服务器下载文件

从互联网下载文件是几乎每个你可能构建的应用程序都需要的非常常见的任务。

要实现此目的，你可以使用 "System.Net.WebClient" 类。

使用 "using" 模式的最简单用法如下所示：

```csharp
using (var webClient = new WebClient())
{
    webClient.DownloadFile("http://www.server.com/file.txt", "C:\\file.txt");
}
```

此示例的作用是使用 "using" 确保在完成时你的 Web 客户端被正确清理，并简单地将第一个参数中 URL 的命名资源传输到第二个参数中本地硬盘上的命名文件。

第一个参数的类型为 "System.Uri"，第二个参数的类型为 "System.String"

你也可以将此函数用作异步形式，以便它在后台执行下载，而你的应用程序可以继续做其他事情，在现代应用程序中以这种方式调用非常重要，因为它有助于保持用户界面的响应性。

当你使用 Async 方法时，你可以挂钩事件处理程序以允许你监控进度，以便

### 第98.4节：基本 UDP 客户端

此代码示例创建一个 UDP 客户端然后向预期接收者跨网络发送 "Hello World"。监听器不必处于活动状态，因为 UDP 是无连接的并且无论如何都会广播消息。一旦消息发送，客户端的工作就完成了。

```
byte[] data = Encoding.ASCII.GetBytes("Hello World");
string ipAddress = "192.168.1.141";
string sendPort = 55600;
try
{
    using (var client = new UdpClient())
    {
        IPEndPoint ep = new IPEndPoint(IPAddress.Parse(ipAddress), sendPort);
        client.Connect(ep);
        client.Send(data, data.Length);
    }
}
catch (Exception ex)
{
    Console.WriteLine(ex.ToString());
}
```

下面是一个 UDP 监听器的示例，可补充上述客户端。它将不断坐在给定端口上监听流量并简单地将数据写入控制台。此示例包含一个控制标志 'done'，该标志在内部未设置并依赖于某些东西来设置它以允许结束监听器并退出。

```
bool done = false;
int listenPort = 55600;
using(UdpClient listener = new UdpClient(listenPort))
{
    IPEndPoint listenEndPoint = new IPEndPoint(IPAddress.Any, listenPort);
    while(!done)
    {
        byte[] receivedData = listener.Receive(ref listenPort);

        Console.WriteLine("Received broadcast message from client {0}", listenEndPoint.ToString());

        Console.WriteLine("Decoded data is:");
        Console.WriteLine(Encoding.ASCII.GetString(receivedData)); //should be "Hello World" sent from above client
    }
}
```
