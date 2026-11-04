
- **1. 在“设计视图”中向默认窗体添加一个文本框，然后切换到“代码视图”。** 在“代码视图”顶部，确保已引用 `System.Net.Mail` 命名空间。

- **2. 创建一个名为 SendEmail 的新子例程。** 它应接受发件人电子邮件地址、收件人电子邮件地址、电子邮件主题和电子邮件正文。

- **3. 声明一个新的 MailMessage，并传入 fromAddress、toAddress、subject 和 body 参数，如下所示：** `MailMessage message = new MailMessage(fromAddress, toAddress, subject, body);`

- **4. 声明一个新的 SmtpClient，并传入邮件服务器的地址。** 该地址可以是 IP 地址、计算机名或 URL。

- **5. 使用你创建的 SmtpClient 对象的 Send 方法发送作为参数传入的 MailMessage。**

- **6. 完成后，请确保将 MailMessage 和 SmtpClient 的值设置为 Nothing，因为它们确实会占用资源。**

清单 4-2 显示了完整的子例程。

### 清单 4-2：SendEmail 子例程

```csharp
private void SendEmail(string fromAddress, string toAddress, string subject,
    string body)
{
    MailMessage message = new MailMessage(fromAddress, toAddress, subject, body);
    SmtpClient mailClient = new SmtpClient("localhost");
    mailClient.Send(message);
    message = null;
    mailClient = null;
}
```

请注意，我使用 localhost 作为电子邮件服务器名称。如果你在本地安装了电子邮件服务器软件，即使是带有 SMTP 的 IIS 6.0，这也会奏效。大多数时候，你会希望在 SmtpClient 构造函数中放入另一个电子邮件服务器名称。电子邮件服务器名称通常可以在 Outlook 首选项中找到。

编写完方法后，需要在 Button1_Click 事件处理程序中下载文件后调用它。将该子例程的代码更改为以下内容以调用该方法：

```csharp
private void button1_Click(object sender, EventArgs e)
{
    DownloadFile(@"ftp://ftp.server.net/sampleFile.bmp", @"c:\sampleFile.bmp");
    SendEmail(textBox1.Text, textBox1.Text,
        "FTP Successful", "FTP Successfully downloaded");
}
```

请注意，我两次传入了文本框的值：一次用于收件人地址，一次用于发件人地址。这并不总是必要的，因为你可能会遇到希望电子邮件仅来自网站管理员地址或仅发送到你的地址的情况。

现在你应该已经有足够的代码来运行应用程序了。按 F5 以调试模式启动应用程序并试一试。

单击按钮时，应用程序应将文件下载到本地驱动器，然后向你发送电子邮件，通知你下载已完成。不过，网络应用程序可能会出现很多问题，你应该了解它们。以下是几个问题：

- 对于大多数网络活动，运行软件的计算机必须连接到网络。作为开发人员，这对你来说不是问题，但你需要考虑到最终用户，他们可能需要连接才能访问他们想要使用的功能。使用网络状态代码可以帮助告知用户这些功能的可用性。

- 防火墙和其他网络设备有时会阻止来自合法应用程序的网络流量。其中的一些示例包括
  - FTP 经常被企业网络阻止。
  - .NET 的网络分析功能经常在公司服务器上被阻止。如果服务器对公众开放，这些开口可能会造成可供黑客钻入的漏洞。
  - 说到黑客，请确保如果你在应用程序中使用入站网络功能，你已经充分保护了应用程序。更多相关内容可在 Michael Howard 和 David C. LeBlanc 所著的优秀书籍《Writing Secure Code, Second Edition》（Microsoft Press 出版）中找到。
  - 电子邮件尤其脆弱。互联网服务提供商经常会阻止来自未在邮件服务器上注册的地址的电子邮件。这意味着，如果你使用的是 localhost 服务器（如清单 4-2 中的示例），你的 ISP 可能会阻止该电子邮件。

- 网络流量出了名地难以调试。例如，如果示例应用程序可以运行，但你从未收到来自你编写的 SmtpServer 的电子邮件，那么出了什么问题？你可能永远都不会知道。XML Web 服务（在第 VII 卷中介绍）也有类似的问题——要查看 SOAP 信封（围绕 Web 服务请求添加的标记）中的实际代码以判断出了什么问题，是极其困难的。

## 记录网络活动

这将引出下一个主题，即网络日志记录。由于网络活动问题非常难以调试和重现，Microsoft 内置了多种用于管理网络活动跟踪的工具。

此外，与可用的 ASP.NET 跟踪一样，`System.Net` 命名空间跟踪完全通过配置文件进行管理。因此，为了能够使用这些功能，你无需更改并重新编译代码。事实上，只需稍作管理，你甚至可以通过管理应用程序使用的配置文件来向用户显示调试信息。

每种应用程序都有不同类型的配置文件。对于你在这里使用的 Windows Forms 应用程序，该文件名为 `app.config`，存储在开发项目目录中。编译时，文件名会更改为应用程序的名称，并复制到 bin 目录中以供运行。

如果你现在打开 app.config 文件，你会看到其中几乎没有任何内容。这对 .NET 来说相当新，因为 .NET 过去有非常复杂的配置。你将向配置中添加一些内容以开启跟踪。

### 清单 4-3：默认 app.config 文件

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
</configuration>
```

首先，你需要为 System.Net 命名空间添加一个新源。接下来，在 Switches 部分为你添加的源添加一个开关。最后，你向该部分添加一个 SharedListener，并将文件设置为自动刷新跟踪信息。

完成后的 app.config 文件如清单 4-4 所示，其中新增内容以粗体显示。它也位于本书配套网站的示例代码中。

### 清单 4-4：完成后的 app.config 文件

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    <system.diagnostics>
        <sources>
            <source name="System.Net">
                <listeners>
                    <add name="System.Net" />
                </listeners>
            </source>
        </sources>
        <switches>
            <add name="System.Net" value="Verbose" />
        </switches>
        <sharedListeners>
            <add name="System.Net"
                 type="System.Diagnostics.TextWriterTraceListener"
                 initializeData="my.log" />
        </sharedListeners>
        <trace autoflush="true" />
    </system.diagnostics>

</configuration>
```

![](img/80ff26f06fc9ab951e1cd4257b867366_492_0.png)

再次运行应用程序并查看“输出”窗口。由于你对配置文件所做的更改，那里会显示高级日志记录信息。此外，还写入了一个日志文件。在开发环境中，该文件位于项目的 bin/debug 目录中。你可能需要单击“解决方案资源管理器”顶部的“显示所有文件”按钮才能看到它。

在该文件夹中，你应该会看到名为 my.log 的文件，你添加到 app.config 文件中的共享侦听器将日志记录信息定向到该文件。我的该文件副本如清单 4-5 所示——你的结果可能会有所不同。

### 清单 4-5：日志信息

```text
System.Net Information: 0 : WebRequest::Create(ftp://ftp.csharpfordummies.net/sample.bmp)
System.Net Information: 0 : Exiting WebRequest::Create() ->
    FtpWebRequest#37460558
System.Net Information: 0 : FtpWebRequest#37460558::GetResponse()
System.Net Information: 0 : Exiting FtpWebRequest#37460558::GetResponse()
System.Net Information: 0 : Associating Message#59487907 with
    HeaderCollection#23085090
System.Net Information: 0 : HeaderCollection#23085090::Set(mime-version=1.0)
System.Net Information: 0 : Associating MailMessage#964596 with Message#59487907
System.Net Information: 0 : SmtpClient::ctor(host=24.123.157.3)
System.Net Information: 0 : Associating SmtpClient#17113003 with
    SmtpTransport#3544512
System.Net Information: 0 : Exiting SmtpClient::ctor() -> SmtpClient#17113003
System.Net Information: 0 : SmtpClient#17113003::Send(MailMessage#964596)
System.Net Information: 0 : SmtpClient#17113003::Send(DeliveryMethod=Network)
System.Net Information: 0 : Associating SmtpClient#17113003 with
    MailMessage#964596
System.Net Information: 0 : Associating SmtpTransport#3544512 with
    SmtpConnection#44365459
System.Net Information: 0 : Associating SmtpConnection#44365459 with
    ServicePoint#7044526
System.Net Information: 0 : Associating SmtpConnection#44365459 with
    SmtpPooledStream#20001460
System.Net Information: 0 : HeaderCollection#30689639::Set(content-transfer-encoding=base64)
```

