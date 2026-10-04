

# 异常处理

上面的配置使用了关闭 SmtpClient 保存的更改，以尝试在 `DoesNotExist` 处发送电子邮件，这显然会失败。为了保存这些更改，请保持文件打开，这样你可以在稍后的步骤中轻松撤销此操作。

- 6. 回到 ExceptionHandling.aspx 并按 Ctrl+F5 在浏览器中打开该页面。你应该能看到带有错误信息的“死亡黄屏”。向下滚动页面查看堆栈跟踪（Stack Trace），如图 18-2 所示。

![](img/9e033e3b9560597824f8b22941d6d8bb_708_0.png)

```
[Exception: The name could not be resolved: "DoesNotExist"]
System.Net.Mail.PooledStream.GetConnection(PooledStream, Object object, Boolean object, IPAddress&address, So
System.Net.Mail.PooledStream.Activate(object object, GeneralAsyncdelegate async_callback) +300
System.Net.Mail.PooledStream.Activate(object object, GeneralAsyncdelegate async_callback) +19
System.Net.Mail.PooledStream.GetConnection(ServicePoint servicePoint, Int32 creationTime) +65
System.Net.Mail.PooledStream.GetConnection(ServicePoint servicePoint) +170
System.Net.Mail.PooledStream.Send(MailMessage) +1554
[Exception: The name could not be resolved: "DoesNotExist"]
System.Net.Mail.SmtpClient.Send(MailMessage) +1960
Demo.Page_Load(Object sender, EventArgs e) in c:\DefaultSite\ExceptionHandling.aspx.cs:2
System.Web.UI.Control.OnLoad(object sender, EventArgs e) +51
System.Web.UI.Page.ProcessRequest(Boolean includeStagesBeforeAsync, Boolean includeStagesAfterAsyncPoint) + -
```

注意列出了两个异常：一个 WebException（表示无法解析名称 DoesNotExist）和一个 SmtpException。在 SmtpClient 遇到并捕获 WebException 后，它将其封装在一个新的 SmtpException 中并抛出异常，以指示错误的类型。

- 7. 回到 VS，并在 Try 块中捕获分配地址和发送消息的代码：

## VB.NET

```vb
Try
    message.From = New MailAddress("*@*example.com")
    message.To.Add(New MailAddress("*@*example.com"))
    Dim SmtpClient As New SmtpClient("DoesNotExist")
    SmtpClient.Send(message)
    message.Text = "Message sent"
Catch ex As SmtpException
    message.Text = "发送您的电子邮件时发生错误。请重试。"
End Try
```

## C#

```csharp
try
{
    message.From = new MailAddress("*@*example.com");
    myMessage.To.Add(new MailAddress("you@example.com"));
    smtpClient mySmtpClient = new SmtpClient("DoesNotExist");
    mySmtpClient.Send(myMessage);
    Message.Text = "Message sent";
}
catch (SmtpException)
{
    Message.Text = "发送您的电子邮件时发生错误。请重试。
}
```

注意代码中仍然包含一个无效的邮件服务器。

- 8. 保存你的更改并在浏览器中再次请求该页面。你现在应该看到一个友好的错误消息，如图 18-3 所示。

![](img/9e033e3b9560597824f8b22941d6d8bb_709_0.png)

图 18-3

抛出的异常现在被 Catch 块捕获了。用户现在看到的不再替换了异常的所有技术细节，而是收到了一条友好的消息，说明出了某些问题。

- 9. 回到 ExceptionHandling.aspx，通过从构造函数调用中删除服务器名称来修复 SmtpClient 的代码：

```vb
Dim mySmtpClient As New SmtpClient()
```

```csharp
smtpClient mySmtpClient = new SmtpClient();
```

此外，在 Web.config 中恢复你之前对 <system.net> 元素所做的更改。

- 10. 保存所有更改并在浏览器中再次刷新 ExceptionHandling.aspx。你现在将收到一条指示电子邮件发送成功的消息。

- 11. 从控件中打开 ContactForm.ascx，切换到它的代码代码（Code Behind），并将创建和发送消息的代码封装以下 Try Catch 块中。此外，将设置 Message 控件可见性的行移动到 Finally 块：

```vb
Dim myMessage As New MailMessage()
...
System.Threading.Thread.Sleep(5000)
Catch ex As SmtpException
    Message.Text = "发送您的电子邮件时发生错误。请重试。"
Finally
    Message.Visible = True
End Try
```

## C#

```csharp
try {
    MailMessage myMessage = new MailMessage();
    ...
    System.Threading.Thread.Sleep(5000);
} catch (SmtpException) {
    Message.Text = "发送您的电子邮件时发生错误。请重试";
} finally {
    Message.Visible = true;
}
```

注意设置 Message 控件 Visible 属性为 True 的行现在位于 Finally 块中。这样，无论是否发生错误，标签都会变为可见。

从以后，每当发送电子邮件期间发生错误时，用户将获得一个正常的错误，而不是 .NET 默认显示的完整错误页面。

## 工作原理

当运行时发生异常时，NET 会检查它是否被封装在 Try Catch 块中。如果是，它会扫描 Catch 块列表以寻找与抛出的异常匹配的 Exception。第一个匹配的 Catch 块会被调用；其余 Catch 块将被忽略。Try 块中引起异常的行之后的代码将不再执行。

在此练习中，代码有一个针对 SmtpException 类型的 Catch 块，当遇到该类型或其子类型的异常时，会被执行。正如你之前学到的，你可以有多个 Catch 块，每个处理特定的异常类型。所有其他异常都不会被此代码处理。你将在后面的章节学习如何处理这些异常。

通过这些 Try Catch 块，你可以编写处理可能错误的代码。将可能抛异常的代码封装在 Try Catch 块中是一种良好的习惯，以便进行处理。可能抛异常的代码示例包括：

- 发送电子邮件——服务器可能宕，或者你可能没有访问它的权限。
- 访问数据库——服务器可能宕，你可能没有访问它的权限，可能会像第 15 章所示的那样由于外键约束违反而遇到错误等。
- 尝试将上传的文件写入磁盘——磁盘可能满，你可能没有写入磁盘的必要权限，或者你提供了无效的文件名。

虽然 Try 块非常有助于避免异常传递到用户界面，但你应该谨慎使用它们，因为它们是有成本的。Try Catch 块通常比没有块的代码慢，所以你不应该使用 Try Catch 来处理错误。

