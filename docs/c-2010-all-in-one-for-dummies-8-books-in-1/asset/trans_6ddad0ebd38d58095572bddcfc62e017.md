

## 462 使用 System.Net 命名空间

这段代码看起来与 FTP 示例非常相似，如下面的代码所示。恢复的是相同的流，只是格式有所不同。

```csharp
private void DownloadWebFile(string remoteFile, string localFile)
{
    FileStream localFileStream = new FileStream(localFile, FileMode.OpenCreate);
    WebRequest webRequest = WebRequest.Create(remoteFile);
    webRequest.Method = WebRequestMethods.Http;
    WebResponse webResponse = WebRequest.GetResponse();
    Stream webResponseStream = webResponse.GetResponseStream();
    byte[] buffer = new byte[1024];
    int bytes = webResponseStream.Read(buffer, 0, 1024);
    while (bytes > 0)
    {
        localFileStream.Write(buffer, 0, bytes);
        bytes = webResponseStream.Read(buffer, 0, 1024);
    }
    localFileStream.Close();
    webResponse.Close();
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_487_0.png)

你需要传递一个 Web 地址，或者像这样调用子程序：
`DownloadWebFile("http://www.csharpdummies.net/sampleFile.bmp", @"c:\sampleFile.bmp");`

加粗标记的注释：WebRequest 现在是 WebRequest 而不是 FtpWebRequest。此外，webRequest 的 Method 属性已更改为 WebRequestMethods.Http。最后，Credentials 属性已被移除，因为不再需要凭据了。

## 发送状态报告

电子邮件是网络化系统的常见需求。如果你在企业环境中工作，你将编写一个规模较大的应用程序来处理所有的电子邮件需求，而不是为每个单独的应用程序编写。

然而，如果你正在编写一个独立产品，它可能需要电子邮件支持。由于我恰好正在写独立应用程序，所以我打算这样做。

电子邮件是基于服务器的操作；如果没有位于电子邮件服务器，可能会很难。许多 ISP 不再允许中继（relaying），即在没有先拥有账户并登录的情况下发送出站消息。因此，你运行示例的这部分可能会遇到问题。

## 使用 System.Net 命名空间

但是，如果你处于企业环境中，你通常可以联系你的电子邮件管理员并获得使用电子邮件服务器的权限。由于出站请求通常在防火墙内部处理，中继通常是可用的。构建你的电子邮件功能，请遵循以下步骤：

- 1. 在设计视图的默认表中添加文本框，然后切换到代码视图。在代码视图顶部，确保你已引用了 System.Net 命名空间。
- 2. 创建一个新的子程序 SendEmail。它应该接收发件地址、收件地址、邮件主题和正文。
- 3. 创建一个新的 MailMessage 并传递 fromAddress、toAddress、subject 和 body 参数，如下所示：
```csharp
MailMessage message = New MailMessage(fromAddress, toAddress, subject, body);
```
- 4. 声明一个新的 smtpClient 并传入你的邮件服务器地址。这可以是一个 IP 地址、名称或 URL。
- 5. 使用你创建的 SmtpClient 对象的方法发送作为参数传递的 MailMessage。
- 6. 完成后，确保将 MailMessage 和 SmtpClient 的值设置为 Nothing，因为它们会占用资源。

列表 4-2 显示了完整的子程序。

### 列表 4-2：SendEmail 子程序

```csharp
private void SendEmail(string fromAddress, string toAddress, string subject, string body)
{
    MailMessage message = new MailMessage(fromAddress, toAddress, subject, body);
    mailClient = new SmtpClient("localhost");
    client.Send(message);
}
```

注意我们使用 localhost 作为电子邮件服务器名称。如果你本地安装了电子邮件服务器（即使是带有 SMTP 的 IIS 6.0），这也可以。大多数情况下，你需要在 SmtpClient 构造函数中放入另一个电子邮件服务器名称。可以在你的 Outlook 偏选项中找到电子邮件服务器。

| 第三卷 | |
| :--- | :--- |
| 第4 章 | |

## 464 使用 System.Net 命名空间

在你编写方法后，需要在 Button1_Click 事件处理程序中文件下载后调用它。将该子程序的代码更改如下方法：

```csharp
private void button1_Click(object sender, EventArgs e)
{
    DownloadFile("http://sharpfordies.net/sampleFile.bmp", @"c:\sampleFile.bmp");
    SendMail(textBox1.Text, textBox.Text, "FTP Successful", "FTP Successfully downloaded:");
}
```

注意我选择了两次文本框的值：一次用于地址，一次用于发件地址。这并不总是必要的，因为你可能会遇到一种情况：邮件仅来自 Web 管理员地址或仅发送到你的地址。

现在你应该有足够的代码来运行应用程序了。按 F5 调试模式启动应用程序并尝试一下。

当你点击按钮时，应用程序将把文件下载到本地驱动器，然后通过电子邮件发送。

