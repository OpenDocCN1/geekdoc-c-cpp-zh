
### DefinePad 代码片段

8. 现在有了该类，您就可以创建客户端来使用它。在此情况下，您将创建一个简单的文本编辑器，增加检索单词定义的 capability。返回到为应用程序创建的窗体并添加如图 29-2 所示的控件。

![](img/d99870e80390742f93963da7be0b2e61_958_0.png)

#### 图 29-2

9. `DefinePad` 的用户界面很简单：一个 `TextBox` 和一个 `ContextMenuStrip`。按以下表格所示设置属性：

| 控件 | 属性 | 值 |
|---|---|---|
| TextBox | Name | TextField |
|  | Multiline | True |
|  | Dock | Fill |
|  | ContextMenuStrip | DefinitionMenu |
| ContextMenuStrip | Name | DefinitionMenu |

10. 窗体中唯一的代码是 `ContextMenuStrip` 的 `Opening` 事件的处理程序。在这里，您将定义添加到菜单。将以下代码添加到 `Opening` 事件的处理程序中：

```vbnet
Private Sub DefinitionMenu_Opening(ByVal sender As Object,
    ByVal e As System.ComponentModel.CancelEventArgs) _
    Handles DefinitionMenu.Opening
    Dim svc As New GoogleClient
    Dim definitions() As String
    Dim definitionCount As Integer
    DefinitionMenu.Items.Clear()
    Try
        'define the currently selected word
        If TextField.SelectionLength > 0 Then
            definitions = svc.Define(TextField.SelectedText)
            'build context menu of returned definitions
            definitionCount = definitions.Length
            If definitionCount > 6 Then
                definitionCount = 6
            ElseIf definitionCount = 0 Then
                'we can't do any more, so exit
                Dim item As New ToolStripButton
                item.Text = "Sorry, no definitions available"
                DefinitionMenu.Items.Add(item)
                Exit Sub
            End If
        End If
        For i As Integer = 1 To definitionCount
            Dim item As New ToolStripButton
```
```vbnet
item.Text = definitions(i-1)
DefinitionMenu.Items.Add(item)
Next
End If
Catch ex As Exception
    MessageBox.Show(ex.Message, "Error getting definitions", MessageBoxButtons.OK, MessageBoxIcon.Error)
End Try
End Sub
```

DefinePad 代码片段

此事件中代码的大部分用于限制菜单中显示的项目数。该例程的实际功能部分是对 `GoogleClient` 的 `Define` 方法的调用。如果您跟踪代码的运行情况，您会看到生成的 `WebRequest`、发出的调用以及由此产生的响应流被解析为所需的各个项目。最后，您可以使用返回的列表创建一组菜单项（实际上什么也不做），并显示“菜单”。单击任何定义都会关闭菜单。

11. 要测试应用程序，请运行它。在文本框中输入或复制一些文本，选择一个单词，然后右键单击它。稍作停顿后，您应该会看到该单词的定义（图 29-3 显示了“protocol”的定义）。

![](img/d99870e80390742f93963da7be0b2e61_959_0.png)

图 29-3

虽然它没有 Web 服务那么性感，但使用这种技术（`WebRequest`、屏幕抓取生成的 HTML）可以为您的应用程序提供访问互联网大量功能的能力。

### 使用 WebClient 简化常见的 Web 请求

我第一次在 2000 年初看到 `WebRequest` 类的演示时，我很高兴。这里有轻松访问互联网资源的能力。然而，演示的另一位与会者问道：“为什么这么困难？你需要做这么多才能让它工作。”下一次我看到同样的 `WebRequest` 演示时，主讲人以“对于那些执行常见场景的人，我们有更简单的方法”作为结尾。然后他继续向我们展示如何使用 `System.Net.WebClient`。

对于那些只想发送 GET 或 POST 请求并下载文件或结果数据的情况，您可以忘记 `WebRequest/WebResponse`。`WebClient` 抽象掉了进行 Web 请求的所有细节，使得从网络抓取数据变得异常简单。它通过抽象出人们使用 `WebRequest/WebResponse` 执行的最常用任务来实现这一点。`WebClient` 类包括用于上传和下载数据、字符串和文件的方法。

所有 `DownloadX` 和 `UploadX` 方法也都支持该方法的异步版本，称为 `DownloadXAsync`，例如 `DownloadFileAsync` 或 `UploadValuesAsync`。这些方法在后台线程上执行实际请求，并在任务完成后触发事件。如果你的应用程序具有某种形式的 пользователь界面，例如窗体，那么你通常应该使用这些方法来保持应用程序响应。

由于 `WebClient` 类使用 `WebRequest` 类来实际执行其功能，因此它可以大大简化网络编码。例如，只需替换之前创建的 `WebRequest` 示例中使用的代码。

**Before:**

```vbnet
Public Function Define(ByVal word As String) As String()
    Dim req As HttpWebRequest = Nothing
    Dim resp As HttpWebResponse
    Dim query As String
    Dim result As New List(Of String)
    query = "http://www.google.com/search?q=define%3A" & _
    HttpUtility.UrlEncode(word)
    Try
        req = DirectCast(WebRequest.Create(query), HttpWebRequest)
        With req
            .Method = "GET"
            resp = req.GetResponse
            If resp.StatusCode = HttpStatusCode.OK Then
                ParseResponse(resp.GetResponseStream, result)
            Else
                MessageBox.Show("Error calling definition service")
            End If
        End With
    Catch ex As Exception
    End Try
    Return result.ToArray()
End Function
```

*Code snippet from DefinePad*

**After:**

```vbnet
Public Function Define(ByVal word As String) As String()
    Dim client As New WebClient
    Dim query As String
    Dim result As New List(Of String)
    query = "http://www.google.com/search?q=define%3A" & _
    HttpUtility.UrlEncode(word)
    Try
        result = ParseResponse(client.DownloadString(query))
    Catch ex As Exception
    End Try
    Return result.ToArray()
End Function

Private Function ParseResponse(ByVal data As String) As List(Of String)
    Dim result As New List(Of String)
    Dim blockStart As String = "<p>Definitions of"
    Dim pos As Integer = data.IndexOf(blockStart)
    Dim posEnd As Integer
    Dim temp As String
    Do
        pos = data.IndexOf("<li>", pos + 1)
        If pos > 0 Then
            posEnd = data.IndexOf("<br>", pos)
            temp = data.Substring(pos + 4, posEnd - pos - 4)
            result.Add(ParseDefinition(temp))
            pos = posEnd + 1
        End If
    Loop While pos > 0
    Return result
End Function
```

*Code snippet from DefinePad*

`WebClient` 避免了 `WebRequest` 所需的所有流处理。然而，你仍然应该了解 `WebRequest` 的工作原理，因为这种知识与 `WebClient` 直接相关。

### SOCKETS

有时你可能需要在网络上传输数据（无论是私有网络还是互联网），但现有的技术和协议并不完全符合你的需求。例如，你不能使用本章前面讨论的技术下载资源，也不能使用 Windows Communication Foundation、Web 服务或远程处理。在这些情况下，最好的做法是使用套接字自行构建协议。

TCP/IP 以及因此的互联网本身都是基于套接字的。原理很简单：在一端建立一个端口，允许客户端从另一端“插入”到该端口。一旦连接建立，应用程序就可以通过流发送和接收数据。例如，HTTP 几乎总是运行在端口 80 上，因此 Web 服务器在端口 80 上打开一个套接字并等待传入连接（除非另有说明，Web 浏览器会尝试连接到端口 80 以向该 Web 服务器发出请求）。

在 .NET 中，套接字在 `System.Net.Sockets` 命名空间中实现，并使用 `System.Net` 和 `System.IO` 中的类来获取流类。虽然在 .NET 之外使用套接字可能有点棘手，但框架包含类使你能够为传入连接打开套接字（`System.Net.TcpListener`）和在两个打开的套接字之间进行通信（`System.Net.TcpClient`）。这两个类，结合一些线程技巧，使你能够构建自己的协议，通过该协议你可以发送任何你喜欢的数据。有了自己的协议，你对通信拥有最终控制权。

为了演示这些技术，你将构建 Wrox Messenger，这是一个非常基本的即时通讯应用程序，类似于 MSN Messenger。

#### Building the Application

你将把应用程序的所有功能封装到一个单一的 Windows 应用程序中，该应用程序既充当等待传入连接的服务器，又充当建立传出连接的客户端。

创建一个名为“WroxMessenger”的新 Windows 窗体应用程序项目。将 `Form1` 的标题更改为 Wrox Messenger 并添加一个名为 `ConnectToField` 的 `TextBox` 控件和一个名为 `ConnectButton` 的 `Button` 控件。将窗体的名称设置为 `ConnectForm`。窗体应如下图 29-4 所示。

![](img/d99870e80390742f93963da7be0b2e61_961_0.png)

FIGURE 29-4

你将在后面更详细地学习这一点，但现在非常重要的一点是，所有 UI 代码都在同一个线程中运行，并且该线程实际上是创建并运行窗体的主应用程序。

为了跟踪正在发生的事情，你将在窗体中添加一个字段，使你能够存储启动线程的 ID 并在标题上报告该 ID。这有助于为后面讨论的线程/UI 问题提供上下文。你还需要一些命名空间导入和一个指定默认端口 ID 的常量。将以下代码添加到你的窗体中：

```vbnet
Imports System.Net
Imports System.Net.Sockets
Imports System.Threading
Public Class ConnectForm
    Private Shared _mainThreadId As Integer
    Public Const ServicePort As Integer = 10101
```

接下来，为窗体创建一个 New 方法，并在构造函数中添加此代码以填充字段并更改标题：

```vbnet
Public Sub New()
    ' This call is required by the Windows Form Designer.
    InitializeComponent()
    ' Add any initialization after the InitializeComponent() call.
    _mainThreadId = System.Threading.Thread.CurrentThread.GetHashCode()
    Text &= "-" & _mainThreadId.ToString()
End Sub
```

为了监听传入连接，你将创建一个名为 `Listener` 的单独类。该类使用 `System.Net.Sockets.TcpListener` 的实例来等待传入连接。具体来说，它打开一个 TCP 端口，任何客户端都可以连接到该端口——套接字不是平台特定的。虽然连接始终在特定的已知端口上建立，但实际通信发生在 TCP/IP 子系统选择的端口上，这意味着你可以同时支持许多传入连接，尽管它们都连接到同一个端口。套接字是一种开放标准，几乎可在任何平台上使用。例如，如果你发布协议的规范，那么在 Linux 上工作的开发人员就可以连接到你的 Wrox Messenger 服务。

当你检测到传入连接时，你会得到一个 `System.Net.Sockets.TcpClient` 对象。这是通往远程客户端的网关。要发送和接收数据，你需要获取一个 `System.Net.NetworkStream` 对象（通过对 `TcpClient` 的 `GetStream` 调用返回），它返回一个可用于此目的的流。

创建一个名为 `Listener` 的新类。此线程需要成员来保存 `System.Threading.Thread` 对象的实例，以及对应用程序中作为主窗体的 `ConnectForm` 类的引用。这里没有涉及如何启动和停止线程或同步。（如果需要更多信息，请参阅第 33 章。）

以下是 `Listener` 类的基本代码：

```vbnet
Imports System.Net.Sockets
Imports System.Threading
Imports System.Net
Public Class Listener
    Implements IDisposable
    Private main As ConnectForm
    Private listener As TcpListener
    Private thread As Thread
    Public Sub New(ByVal main As ConnectForm)
        Me.main = main
    End Sub
    Public Sub SpinUp()
        ' create and start the new thread...
        thread = New Thread(AddressOf ThreadEntryPoint)
        thread.Start()
    End Sub
End Class
```
