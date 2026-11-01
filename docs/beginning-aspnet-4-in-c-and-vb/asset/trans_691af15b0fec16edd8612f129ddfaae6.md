
```
mm.To.Add(new MailAddress("editor@wrox.com", "Paul Reese"));
mm.To.Add(new MailAddress("marketing@wrox.com", "Wrox Marketing"));
mm.CC.Add(new MailAddress("publisher@wrox.com", "Barry Pruett"));
mm.Subject = "The latest chapter";
mm.Body = "<b>Here you can put a long message</b>";
mm.IsBodyHtml = true;
mm.Priority = MailPriority.High;
Attachment att = new Attachment("myExcelResults.zip",
    MediaTypeNames.Application.Zip);
mm.Attachments.Add(att);
sc.Send(mm);
```

在这种情况下，Attachment 对象是在调用 Send() 方法之前使用 Add() 方法创建并添加到 MailMessage 对象中的。

## 使用 TCP 类

传输控制协议（TCP）类提供了在两个端点之间连接和发送数据的简单方法。端点是 IP 地址和端口号的组合。现有协议具有明确定义的端口号，例如，HTTP 使用端口 80，而 SMTP 使用端口 25。互联网号码分配机构 IANA（www.iana.org）为这些众所周知的服务分配端口号。除非您正在实现一个众所周知的服务，否则您希望选择大于 1,024 的端口号。

TCP 流量目前构成了互联网上大部分流量。TCP 通常是首选协议，因为它提供保证交付、错误校正和缓冲。TcpClient 类封装了 TCP 连接，并提供了一系列用于调节连接的属性，包括缓冲、缓冲区大小和超时。读取和写入是通过 GetStream() 方法请求 NetworkStream 对象来完成的。

TcpListener 类使用 Start() 方法侦听传入的 TCP 连接。当连接请求到达时，您可以使用 AcceptSocket() 方法返回用于与远程机器通信的套接字，或使用 AcceptTcpClient() 方法使用更高级别的 TcpClient 对象进行通信。了解 TcpListener 和 TcpClient 类如何协同工作的最简单方法是通过一个示例来操作。

## TcpSend 和 TcpReceive 示例

为了演示这些类的工作方式，您需要构建两个应用程序。图 24-11 显示了第一个应用程序 TcpSend。该应用程序打开到服务器的 TCP 连接并发送其自身的 C# 源代码。

![](img/d7d2ffa0a76feaab821930e95daace93_719_0.png)

再次，您创建一个 C# Windows 应用程序。窗体包含两个文本框（txtHost 和 txtPort）分别用于主机名和端口，以及一个按钮（btnSend）用于单击并开始连接。首先，您确保包含相关的命名空间：

```
using System;
using System.IO;
using System.Net.Sockets;
using System.Windows.Forms;
```

以下代码显示了按钮 Click 事件的事件处理程序：

```
private void btnSend_Click(object sender, System.EventArgs e)
{
    TcpClient tcpClient = new TcpClient(txtHost.Text, Int32.Parse(txtPort.Text));
    NetworkStream ns = tcpClient.GetStream();
    FileStream fs = File.Open("form1.cs", FileMode.Open);

    int data = fs.ReadByte();

    while(data != -1)
    {
        ns.WriteByte((byte)data);
        data = fs.ReadByte();
    }

    fs.Close();
    ns.Close();
    tcpClient.Close();
}
```

此示例使用主机名和端口号创建 TcpClient。或者，如果您有 IPEndPoint 类的实例，则可以将该实例传递给 TcpClient 构造函数。在获取 NetworkStream 类的实例后，您打开源代码文件并开始读取字节。与许多二进制流一样，您需要通过将 ReadByte() 方法的返回值与 -1 进行比较来检查流的末尾。在循环读取所有字节并将其发送到网络流后，您必须关闭所有打开的文件、连接和流。

在连接的另一端，TcpReceive 应用程序在传输完成后显示接收到的文件（参见图 24-12）。

![](img/d7d2ffa0a76feaab821930e95daace93_720_0.png)

## 图 24-12

窗体包含一个名为 txtDisplay 的单个 TextBox 控件。TcpReceive 应用程序使用 TcpListener 等待传入连接。为了防止应用程序界面冻结，您使用后台线程等待然后从连接中读取。因此，您需要包含 System.Threading 命名空间以及以下其他命名空间：

```
using System;
using System.IO;
```

## UDP 类

正如您所期望的，UdpClient 类的接口比 TcpClient 更小更简单。这反映了该协议相对更简单的性质。尽管 TCP 和 UDP 类在底层都使用套接字，但 UdpClient 类不包含用于读取和写入的返回网络流的方法。相反，成员函数 Send() 接受字节数组作为参数，而 Receive() 函数返回字节数组。此外，由于 UDP 是无连接协议，您可以等待将通信的端点指定为 Send() 和 Receive() 方法的参数，而不是在构造函数或 Connect() 方法中更早指定。您还可以在每次后续发送或接收时更改端点。

以下代码片段使用 UdpClient 类向回显服务发送消息。运行回显服务的服务器在端口 7 上接受 TCP 或 UDP 连接。回显服务只是将发送到服务器的任何数据回显给客户端。此服务对于诊断和测试很有用，尽管许多系统管理员出于安全原因禁用回显服务：

```csharp
using System;
using System.Text;
using System.Net;
using System.Net.Sockets;
namespace Wrox.ProCSharp.InternetAccess.UdpExample
{
    class Class1
    {
        [STAThread]
        static void Main(string[] args)
        {
            UdpClient udpClient = new UdpClient();
            string sendMsg = "Hello Echo Server";
            byte[] sendBytes = Encoding.ASCII.GetBytes(sendMsg);
            udpClient.Send(sendBytes, sendBytes.Length, "SomeEchoServer.net", 7);
            IPEndPoint endPoint = new IPEndPoint(0, 0);
            byte[] recvBytes = udpClient.Receive(ref endPoint);
            string rcvMessage = Encoding.ASCII.GetString(recvBytes,
                                                        0,
                                                        recvBytes.Length);
            // should print out "Hello Echo Server"
            Console.WriteLine(rcvMessage);
        }
    }
}
```

您大量使用 Encoding.ASCII 类将字符串转换为字节数组，反之亦然。另请注意，您按引用将 IPEndPoint 传递给 Receive() 方法。由于 UDP 不是面向连接的协议，每次对 Receive() 的调用可能从不同的端点获取数据，因此 Receive() 使用发送主机的 IP 地址和端口填充此参数。

UdpClient 和 TcpClient 都继承自对最低级类的抽象层：Socket。

## Socket 类

Socket 类在网络编程中提供了最高级别的控制。演示该类的最简单方法之一是用 Socket 类重写 TcpReceive 应用程序。更新后的 Listen() 方法在此示例中列出：

```csharp
public void Listen()
{
    Socket listener = new Socket(AddressFamily.InterNetwork,
        SocketType.Stream,
        ProtocolType.Tcp);
    listener.Bind(new IPEndPoint(IPAddress.Any, 2112));
    listener.Listen(0);
    Socket socket = listener.Accept();
    Stream netStream = new NetworkStream(socket);
    StreamReader reader = new StreamReader(netStream);
    string result = reader.ReadToEnd();
    Invoke(new UpdateDisplayDelegate(UpdateDisplay),
        new object[] { result });
    socket.Close();
    listener.Close();
}
```

Socket 类需要几行额外的代码来完成相同的任务。首先，构造函数参数需要指定用于 TCP 协议的流套接字的 IP 地址方案。这些参数只是 Socket 类可用的众多组合之一。TcpClient 类可以为您配置这些设置。然后您将侦听套接字绑定到端口并开始侦听传入连接。当传入请求到达时，您可以使用 Accept() 方法创建一个新套接字来处理连接。最终，您将 StreamReader 实例附加到套接字以读取传入数据，与之前的方式基本相同。

Socket 类还包含用于异步接受、连接、发送和接收的多种方法。您可以使用回调委托以与使用 WebRequest 类的异步页面请求相同的方式使用这些方法。如果您确实需要深入研究套接字的内部结构，则可以使用 GetSocketOption() 和 SetSocketOption() 方法。这些方法允许您查看和配置选项，包括超时、生存时间和其他低级选项。接下来，本章将介绍使用套接字的另一个示例。

## 构建服务器控制台应用程序

进一步研究 Socket 类，下一个示例创建了一个充当传入套接字请求服务器的控制台应用程序。从那里，将并行创建第二个示例（另一个控制台应用程序），它向服务器控制台应用程序发送消息。

您将构建的第一个应用程序是充当服务器的控制台应用程序。该应用程序将在特定的 TCP 端口上打开一个套接字并侦听任何传入消息。此控制台应用程序的代码在此完整呈现：

```csharp
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;

namespace SocketConsole
{
    class Program
    {
        static void Main()
        {
            Console.WriteLine("Starting: Creating Socket object");
            Socket listener = new Socket(AddressFamily.InterNetwork,
                SocketType.Stream,
                ProtocolType.Tcp);
            listener.Bind(new IPEndPoint(IPAddress.Any, 2112));
            listener.Listen(10);
            while (true)
            {
                Console.WriteLine("Waiting for connection on port 2112");
```
