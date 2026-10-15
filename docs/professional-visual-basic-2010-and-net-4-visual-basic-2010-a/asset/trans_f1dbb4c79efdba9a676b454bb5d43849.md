

## 启动连接

ConnectForm 需要能够同时发起连接和接收入站连接——该应用程序既是客户端也是服务器。你已经通过创建 Listener 创建了一些服务器部分；现在你将查看客户端部分。

在使用套接字时通用的规则是，只要你通过网络发送任何内容，就必须在单独的线程中执行实际通信。几乎所有发送和接收的调用都是阻塞式的；也就是说，它们会阻塞直到接收到数据，阻塞直到所有数据发送完毕，等等。

如果线程使用得当，则 UI 将照常运行，而与传输和接收过程中可能出现的问题无关。这就是为什么在 ConnectForm 的 InitiateConnection 方法中，你将处理延迟到另一个名为 InitiateConnectionThreadEntryPoint 的方法中，该方法从新线程调用。向 ConnectForm 的代码中添加此方法：

```
Private Sub InitiateConnectionThreadEntryPoint(ByVal state As Object)
    Try
        ' Get the host name...
        Dim hostName As String = CStr(state)
        ' Resolve...
        Dim hostEntry As IPHostEntry = Dns.GetHostEntry(hostName)
        If Not hostEntry Is Nothing Then
            ' Create an end point for the first address.
            Dim endPoint As New IPEndPoint(hostEntry.AddressList(0), ServicePort)
            ' Create a TCP client...
            Dim client As New TcpClient()
            client.Connect(endPoint)
            ' Create the connection window...
            ProcessOutboundConnection(client)
        Else
            Throw New ApplicationException("Host " & hostName & _
                " could not be resolved.")
        End If
        Catch ex As Exception
            HandleInitiateConnectionException(ex)
        End Try
End Sub
```

来自 WroxMessenger 的代码片段

在线程内部，你尝试将给定的主机名转换为 IP 地址（演示中使用 localhost 作为主机名，但它也可以是本地网络上的机器名称或 Internet 上的主机名）。这是通过 System.Net.Dns 上的共享 GetHostEntry 方法完成的，并返回一个 System.Net.IPHostEntry 对象。因为主机名可以指向多个 IP 地址，所以你只使用给定的第一个地址。你将此作为 IP 表达的地址（例如，192.168.0.4）与端口号结合起来得到一个新的 System.Net.IPEndPoint。然后你从此 IPEndPoint 创建一个新的 TcpClient 并尝试连接。

如果在任何时候抛出异常（这可能发生在名称无法解析或连接无法建立时），你将异常传递给 HandleInitiateConnectionException。如果成功，则将其传递给 ProcessOutboundConnection。这两种方法将很快实现：

```
Private Sub InitiateConnectionThreadEntryPoint(ByVal state As Object)
    Try
        ' Get the host name...
        Dim hostName As String = CStr(state)
        ' Resolve...
        Dim hostEntry As IPHostEntry = Dns.GetHostEntry(hostName)
        If Not hostEntry Is Nothing Then
            ' Create an end point for the first address.
```

```
Dim endPoint As New IPEndPoint(hostEntry.AddressList(0), ServicePort)
' Create a TCP client...
Dim client As New TcpClient()
client.Connect(endPoint)
' Create the connection window...
ProcessOutboundConnection(client)
Else
Throw New ApplicationException("Host " & hostName & _
" could not be resolved.")
End If
Catch ex As Exception
HandleInitiateConnectionException(ex)
End Try
End Sub
```

来自 WroxMessenger 的代码片段

当涉及到 HandleInitiateConnectionException 时，你开始看到前面提到的跨线程 UI 问题。当异常出现问题时，你需要通知用户，这意味着你需要将异常从线程池管理的线程移动到主应用程序线程。其原理相同；你需要创建一个委托并通过表单的 Invoke 方法调用该委托。此方法在跨线程调度调用方面做了所有繁重的工作。

以下是委托的示例。它们具有与调用本身相同的参数。作为命名约定，最好使用与方法相同的名称并在末尾加上“Delegate”一词：

```
Public Class ConnectForm
Private Shared _mainThreadId As Integer
' delegates...
Protected Delegate Sub HandleInitiateConnectionExceptionDelegate(_
ByVal ex As Exception)
```

来自 WroxMessenger 的代码片段

在 ConnectForm 的构造函数中，你捕获调用线程的线程 ID 并将其存储在 _mainThreadId 中。以下是比较捕获的 ID 与当前线程 ID 的方法：

```
Public Shared Function IsMainThread() As Boolean
If Thread.CurrentThread.GetHashCode() = _mainThreadId Then
Return True
Else
Return False
End If
End Function
```

来自 WroxMessenger 的代码片段

你在 HandleInitiateConnectionException 顶部做的第一件事是检查线程 ID。如果不匹配，则创建委托并调用它。请注意，你设置委托回调到同一方法，因为第二次调用时你将已移动到主线程；因此，IsMainThread 返回 True，你可以正确处理异常：

```
Protected Sub HandleInitiateConnectionException(ByVal ex As Exception)
' main thread?
If IsMainThread() = False Then
' Create and call...
Dim args(0) As Object
args(0) = ex
Invoke(New HandleInitiateConnectionExceptionDelegate(AddressOf _
HandleInitiateConnectionException), args)
' return
```

```
Return
End If
' Show it.
MessageBox.Show(ex.GetType().ToString() & ":" & ex.Message)
End Sub
```

来自 WroxMessenger 的代码片段

结果是，当调用来自线程池管理的线程时，IsMainThread 返回 False，并创建并调用委托。当方法因委托调用而再次进入时，IsMainThread 返回 True，你会看到消息框。

当涉及到 ProcessOutboundConnection 时，你必须再次跳转到主 UI 线程。然而，此方法的魔力是在一个名为 ProcessConnection 的单独方法中实现的，该方法可以处理入站或出站连接。以下是委托：

```
Public Class ConnectForm
    Private Shared _mainThreadId As Integer
    Private _listener As Listener
    Protected Delegate Sub ProcessConnectionDelegate(ByVal client As _
        TcpClient, ByVal direction As ConversationForm.ConversationDirection)
    Protected Delegate Sub HandleInitiateConnectionExceptionDelegate(ByVal _
        ex As Exception)
```

来自 WroxMessenger 的代码片段

以下是该方法本身，它创建新的会话表单并调用 ConfigureClient 方法：

```
Protected Sub ProcessConnection(ByVal client As TcpClient, _
    ByVal direction As ConversationForm.ConversationDirection)
    ' Do you have to move to another thread?
    If IsMainThread() = False Then
        ' Create and call...
        Dim args(1) As Object
        args(0) = client
        args(1) = direction
        Invoke(New ProcessConnectionDelegate(AddressOf ProcessConnection), args)
        Return
    End If

    ' Create the conversation window...
    Dim conversation As New ConversationForm()
    conversation.Show()
    conversation.ConfigureClient(client, direction)
End Sub
```

来自 WroxMessenger 的代码片段

当然，ProcessOutboundConnection 需要委派给 ProcessConnection：

```
Public Sub ProcessOutboundConnection(ByVal client As TcpClient)
    ProcessConnection(client, ConversationForm.ConversationDirection.Outbound)
End Sub
```

来自 WroxMessenger 的代码片段

现在你可以在客户端发起连接，让我们看看如何接收连接（在服务器端）。

## 接收入站连接

你已经构建了 Listener，但你尚未创建它的实例或启动其线程以等待传入连接。为此，你需要在 ConnectForm 中有一个字段来保存该对象的实例。你还需要调整构造函数。以下是该字段：
