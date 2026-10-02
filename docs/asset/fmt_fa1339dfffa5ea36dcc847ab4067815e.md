
每个帧都有一个操作码（`opcode`），用于指示帧的类型以及有效负载（`payload`）的大小。负载包含客户端和服务器想要相互发送的实际数据。WebSocket 协议支持帧的分段。这意味着没有长度的数据包可以被拆分成不同长度的帧。如果发送者/接收者不知道正在发送或接收的数据长度，WebSocket 将消息分段为帧。然后，每个帧都可以指示传输了多少数据，以及它是否是消息的最后一个帧。图 26-6 显示了典型的 WebSocket 数据帧格式。

| | | | | |
|---|---|---|---|---|
| 4 字节 | 2 字节 | 数据 | n 字节 |
| 图 26-6 | | | | |

（注：原文后续部分存在大量重复的描述性，已根据“不要重复输出原文”的原则在翻译中进行了精简，保留核心逻辑。）

数据帧的一个关键方面是掩码（`masking`）。掩码是一种简单的算法，将负载与一个不可预测的密钥进行异或运算，以防止恶意应用程序。

# WebSockets API

WebSocket 协议由 IETF（互联网工程任务组）标准组织进行了标准化。这意味着任何人都可以遵循此标准并在自己的客户端或服务器中实现它。所有常用的浏览器（如 Internet Explorer、Chrome、Firefox、Safari、Opera 等）都增加了对 WebSockets API 的支持。

表 26-1 显示了用于在 WebSocket 连接上执行操作的一些常用事件监听器。

| 事件监听器 | 说明 |
|---|---|
| `onopen` | WebSocket 连接打开时触发此事件。 |
| `onClose` | WebSocket 连接关闭时触发此事件。 |
| `onmessage` | 接收到服务器发送的数据时触发此事件。 |
| `Send` | 此方法用于从客户端发送数据到服务器。 |
| `close` | 此方法关闭 WebSocket 连接。 |

# ASP.NET 4.5 中的 WebSockets

现在你已经看到了 WebSocket 协议的运行，在这一节中你将查看如何在 ASP.NET 中使用 WebSockets 构建应用程序。

由于 WebSocket 协议需要客户端和服务器共同实现，你将查看所有情况。在 Web 服务器上，有一个名为 WebSocket 模块的新模块。它是 Windows Server 2012 IIS 8 中引入的。该模块实现了 WebSocket 协议并负责处理数据传输。

图 26-7 显示了如何在 IIS 8 中启用 WebSocket 协议（在 Windows 中启用 Web 服务器角色）。一旦启用此项，你需要在 IIS 应用开发功能中选择 WebSocket 协议选项。

![](img/67a6707ff505c052edb96c0128fb3096_1041_0.png)

图 26-7

## 检查服务器端 WebSockets 回显处理程序

列表 26-3 显示了一个简单的 WebSockets 回显处理程序。它接收一个 WebSockets 请求，接收来自客户端的消息，并将相同的消息发回给客户端。

### 列表 26-3：ASP.NET 中典型的 WebSockets 回显处理程序

#### VB

```vb
Public Class Handler
    Implements IHttpHandler

    Public Async Function WebSocket(context As AspWebSocketContext) As Task
        Dim socket As WebSocket = context.WebSocket
        While True
            Dim buffer As ArraySegment(Of Byte) (New Byte(1023) {})
            ' 异步等待从客户端接收消息
            Dim result As WebSocketResult = Await socket.ReceiveAsync(buffer, CancellationToken.None)

            ' 如果套接字状态仍然开启，则将消息回显给客户端
            If socket.State = WebSocketState.Open Then
                Dim userMessage As String = Encoding.UTF8.GetString(buffer.Array, 0, result.Count)
                userMessage = "You sent: " & userMessage & " at " & DateTime.Now.ToLongTimeString()
                buffer = New ArraySegment(Of Byte) (Encoding.UTF8.GetBytes(userMessage))

                ' 异步向客户端发送消息
                Await socket.SendAsync(buffer, WebSocketMessageType.Text, True, CancellationToken.None)
            Else
                Exit While
            End If
        End While
    End Function

    Public ReadOnly Property IsReusable() As Boolean Implements IMessageHandler.IsReusable
        Get
            Throw New NotImplementedException()
        End Get
    End Property

    Public Sub ProcessRequest(request As HttpContext) Implements IMessageHandler.ProcessRequest
        if context.IsWebSocketRequest Then
            context.AcceptWebSocketRequest(AddressOf MyWebSocket)
        End If
    End Sub
End Class
```

#### C#

```csharp
public class Handler : IMessageHandler {
    public async Task Async(MyWebSocketContext AspNetWebSocketContext context)
    {
        WebSocket socket = context.WebSocket;
        while (true)
        {
            ArraySegment<byte> buffer = new ArraySegment<byte>(new byte[1024]);

            // 异步等待从客户端接收消息
            WebSocketReceiveResult result =
                await socket.ReceiveAsync(buffer, CancellationToken.None);

            // 如果套接字状态仍然开启，则将消息回显给客户端
            if (socket.State == WebSocketState.Open) {
                string userMessage = Encoding.UTF8.GetString(buffer.Array, 0,
                    result.Count);
                userMessage = "You sent: " + userMessage + " at " + 
                    DateTime.Now.LongTimeString();
                buffer = new ArraySegment<byte>(Encoding.UTF8.GetBytes(userMessage));

                // 异步向客户端发送消息
                await socket.SendAsync(buffer, WebSocketMessageType.Text,
                    true, CancellationToken.None);
            }
            else { break; }
        }
    }
    
    public bool IsReusable()
    {
        get { throw new NotImplementedException(); }
    }

    public void ProcessRequest(HttpContext context)
    {
        if (context.IsWebSocketRequest)
        {
            context.AcceptWebSocketRequest(MyWebSocket);
        }
    }
}
```

当请求到达此回显处理程序时，处理程序首先在 `ProcessRequest` 函数中检查请求是否为 WebSockets 请求。如果是，回显处理程序将在 `ProcessRequest` 中调用的 `MyWebSocket` 任务中读取通过 WebSockets 连接发送的消息。回显处理程序使用 WebSockets API 来接收和发送消息。

## 检查客户端 WebSockets 代码

现在你已经在 ASP.NET 处理程序中加载了 WebSockets 的服务器端实现，现在是时候查看如何从网页创建 WebSocket 连接了。

要连接到端点，只需创建一个新的 WebSocket 实例，为新对象提供一个代表你想要连接的端点的 URL 即可。

> 注意：`ws://` 和 `wss://` 前缀通常分别表示 WebSocket 连接和安全的 WebSocket 连接。

一旦建立连接，你就可以使用 `send` 和 `onmessage` 事件监听器在连接上发送消息。你可以使用表 26-1 所示的其他事件监听器来关闭连接并执行 WebSocket API 支持的任何其他功能。

列表 26–4 显示了一个典型的网页，该网页使用 JavaScript 中的 WebSockets API 实现来连接到 WebSocket 回显处理程序。

### 列表 26-4：典型的 WebSockets JavaScript 客户端

```html
<!@Page AutoEventWire="true %>
<!doctype html>
<html>
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type">
<title>WebSocket Test</title>
<script type="text/javascript">
var socket;
function initializeWebSocket() {
var host = "ws://localhost:33610/CS/Handler.ashx";
try {
    socket = new WebSocket(host);

    socket.onopen = function (msg) {
        var s = 'Socket open';
        document.getElementById("serverStatus").innerHTML = s;
    }
    socket.onmessage = function (msg) {
        var serverData = document.getElementById("serverData");
        var newElem = document.createElement("p");
        newElem.appendChild(document.createTextNode(msg.data));
        serverData.appendChild(newElem);
    }
    socket.onclose = function (msg) {
        var s = 'Socket closed';
        document.getElementById("serverStatus").innerHTML = s;
    }
} catch (ex) {
    alert(ex);
}

function send() {
    var e = document.getElementById("msgText");
    socket.send(e.value);
}
initializeWebSocket();
</script>
</head>
<body>
<h1>WebSocket Echo</h1>
<p id="serverStatus"></p>
<div id="serverData"></div>
<p>Send message: <input type="text" id="msgText" /><input type="button" value="Send" onclick="send()" /></p>
</body>
</html>
```

## 什么是 SignalR？

SignalR 是一个构建在 ASP.NET 之上的库。它让为 Web 应用程序添加实时功能变得极其简单。SignalR 在可用时底层使用 WebSockets，在不可用时会优雅地降级到其他技术和方案。在整个过程中，你的应用程序代码保持不变。

SignalR 还为编写实时应用程序提供了一个非常简单、高级的 API，并为连接管理增加了实用的钩子（`hooks`）。它实现了需要服务器高频率更新的新类型应用程序（例如实时游戏）。图 26-9 显示了 SignalR 的高级特性。

![](img/67a6707ff505c052edb96c0128fb3096_1046_0.png)

图 26-9

SignalR 还支持不同的环境和设备。它会确定客户端和服务器支持的内容，并选择最佳方法建立实时连接。如果客户端和服务器都支持 WebSockets，它将使用 WebSockets，否则将使用次优方案。这意味着你的应用程序可以在不同 Windows 版本的各种浏览器上无缝运行，而无需更改应用程序代码。SignalR 的另一个妙处在于它暴露了 API，因此你可以使用相同的服务器端代码为来自不同设备的客户端连接为移动设备和平板电脑构建实时应用程序。

## ASP.NET 中的服务器端 SignalR

在 ASP.NET 应用程序中使用 SignalR 与 WebSockets 类似。有一个服务器端部分负责接收客户端的连接并在所有客户端之间传输数据。SignalR 与 WebSockets API 的区别在于 SignalR 提供了管理连接的额外功能，并确保所有客户端都能无缝交换数据。正如你在列表 26-3 中看到的处理 WebSocket 连接的 HTTP 处理器，`hub`（枢纽）是客户端可以调用的服务器端节点。它管理所有连接，并从各种客户端发送或接收数据。列表 26-5 显示了一个用于聊天应用程序的 hub 示例。

与 WebSockets 不同，hub 不需要任何代码来接受连接。协商连接和选择最佳协议的底层细节对开发者隐藏了，这样他们就可以专注于应用程序代码，而不是协议协商。

# 第 26 章 实时通信

### 列表 26-5：典型的 ASP.NET SignalR 聊天 hub

#### VB

```vb
Public Class VChat
    Inherits Hub
    Public Sub Send(message As String)
        ' 调用所有客户端上的 addmessage 方法
        Clients.All.addMessage(message)
    End Sub
End Class
```

#### C#

```csharp
public class CSChat : Hub
{
    public async void Send(string message)
    {
        // 调用所有客户端上的 addmessage 方法
        Clients.All.addMessage(message);
    }
}
```

SignalR 支持服务器到客户端的 RPC（从服务器端 .NET 代码调用客户端中的函数）。例如，在列表 26-5 中，`addMessage` 是网页上的一个 JavaScript 函数（如列表 26-6 所示），它从服务器端 hub 被调用。

Hub 在服务器端提供了许多高级功能，包括某种级别的安全性。它们可以检查客户端是否经过身份验证并授权与服务器通信。Hub 可以多种方式向所有已连接的客户端广播消息，或仅向发送消息的客户端，或特定的客户端。Hub 还提供了在客户端连接、断开或重新连接时触发的事件。这些功能使得跟踪客户端和传输消息变得简单。

## ASP.NET 中的客户端端 SignalR

在应用程序中使用 SignalR 的另一个方面是客户端。SignalR 可以与不同类型的客户端一起使用。本节介绍了如何在可以通过浏览器访问的网页中使用它。体验将与列表 26-4 类似，该列表显示了如何在 JavaScript 中使用 WebSockets API 对列表 26-3 中的回显处理器建立 WebSockets 连接。
