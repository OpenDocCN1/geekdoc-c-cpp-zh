

# 第 9 章 验证用户输入

（续）

| 类 | 描述 |
|---|---|
| Attachment | 此类表示一个可以附加到 MailMessage 的文件。当你构造一个 Attachment 实例时，可以传递你想要发送的文件名。然后，使用其 Attachments 集合的 Add 方法将附件添加到 MailMessage 中。 |
| SmtpClient | 此类用于发送实际的消息。默认情况下，该类的一个实例会检查 Web.config 文件中的设置，例如用于发送邮件的 SMTP 服务器（全称为简单邮件传输协议，Simple Mail Transfer Protocol）以及用于发送电子邮件的可选用户名和密码。 |

# 配置你的网站发送电子邮件

虽然发送电子邮件的代码非常简单，但配置你的应用程序和网络可能会有点复杂。你用于发送电子邮件的机器必须能够访问 SMTP 服务器，该服务器可能位于你的本地网络上，也可能在互联网上。在许多情况下，你应该使用与你的电子邮件客户端（例如 Microsoft Outlook）中相同的 SMTP 服务器。如果你使用外部托管服务托管你的网站，则应该使用该服务提供的 SMTP 服务器。如果不确定你的 SMTP 服务器，请联系你的网络管理员或互联网服务提供商（ISP）。

当你获得 SMTP 服务器地址后，可以在 Web.config 文件的 `<system.net>` 元素中进行全局配置。当你使用 ISP 的 SMTP 服务器时，配置看起来如下：

```
<system.net>
  <mailSettings>
    <smtp method="Network" from="Your Name&lt;example.com&gt;">
      <network host="smtp.example.com" />
    </smtp>
  </mailSettings>
</system.net>
```

你必须将 `<system.net>` 元素作为 Web.config 文件根元素 `<configuration>` 的子元素。在 `<system.net>` 内部添加 `<mailSettings>` 元素，其中包含一个 `<smtp>` 元素。最后，`<network>` 元素有一个 host 属性，指向你的 SMTP 服务器。

`<smtp>` 元素接受一个可选的 `from` 属性，允许你以“电子邮件地址”的格式发送服务器的名称和电子邮件地址。由于 XML 中的括号 `< >` 具有特殊含义，你必须使用 `&lt;` 和 `&gt;` 对它们进行转义。当你通过程序发送电子邮件时，可以像下一个“尝试”练习中所示那样覆盖此 From 设置。

如果你的 ISP 要求在发送电子邮件之前进行身份验证，或者你想使用不同的端口号，请使用 `<network />` 元素：

```
<smtp method="Network" from="Your Name&lt;example.com&gt;">
  <network host="smtp.example.com" username="UserName" password="Password"
    port="587" />
</smtp>
```

# 在服务器处理数据 | 323

端口号随服务器而异。在某些情况下，你可以留空输出端口，让 SmtpClient 使用默认端口号（即 25）。其他频繁使用的端口号包括 465 和 587。

某些层——例如 Gmail 提供的层——要求你使用安全套接层（SSL），这是一种加密发往邮件服务器的数据以提高安全性的技术。在版本 4 之前的 ASP.NET 中，你必须在自己的代码中通过程序地启用 SSL。坦率地说，有了 `<network>` 元素上的 `enabledsl` 属性，情况已不再如此。对于 Gmail 用户或任何需要 SSL 的邮件服务器，你可以使用如下所示的 `<network>` 元素：

```
<network enabledsl="true" host="smtp.gmail.com" password="Password" userName="YourAccount@gmail.com" port="587" />
```

不要忘记输入你的密码和用户名——对于 Gmail 来说就是你的电子邮件地址。根据你的设置，你可能需要生成一个应用程序特定的密码，你可以在这里生成：http://bit.ly/N9Wv35。

对于 Outlook.com（原 Hotmail），你可以使用以下设置：

```
<network host="smtp.mail.com" password="Password" enabledsl="true" userName="yourdomain.com" port="587" />
```

对于 Yahoo，你可以使用以下设置：

```
<network host="smtp.yahoo.com" password="Password" userName="YourAccount@yahoo.com" />
```

在开发期间，有一种更简单的方法发送邮件，就是将它丢到本地硬盘上的一个文件夹中。要实现这一点，创建一个类似 `C:\Mailbox` 的文件夹。你需要手动创建该文件夹，因为它不会自动创建。然后如下如下配置 `<smtp>` 元素：

```
<smtp deliveryMethod="SpecifiedPickupDirectory" from="PlanWrox&lt;planwatroxexample.com&gt;">
<specifiedPickupDirectory pickupDirectoryLocation="C:\Mail" />
</smtp>
```

使用 Web.config 中的设置后，你的消息不会以物理文件（带有 .eml 扩展名）的形式放入 `PickupDirectoryLocation` 配置的文件夹中。你可以使用 Outlook 或 Windows Live（可以从互联网下载）等客户端读取这些内容。在开发期间，我更倾向于这种设置而不是网络版本，因为邮件即时到达，且不会占用你的邮箱或收件箱。另一个替代方案是使用如 `smtpdev` 之类的伪 SMTP 服务器。你可以在他们的网站 http://smtp4dev.codeplex.com 上找到更多信息。

参考 MSDN 文档 http://tinyurl.com/bu79nkm 了解更多关于 `<mailSettings>` 元素接受的不同设置的信息。

# 创建电子邮件

要发送电子邮件，你需要创建一个 MailMessage 实例。首先，通过 MailMessage 类创建发送者信息。最后，使用 SmtpClient 类来发送邮件。

# 尝试：发送电子邮件

在这个练习中，我们将通过代码来发送电子邮件。接下来的步骤将展示如何配置发送邮件。

- 1. 在 Demos 文件夹下创建一个名为 Email.aspx 的新文件。确保它继承 BasePage。
- 2. 按 F7 到代码。在文件顶部添加以下内容：
```vb
Imports System.Net
```
- 3. 在 Page_Load 程序中，添加以下内容：
```vb
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    Dim myMessage As New MailMessage
    myMessage.Subject = "Test Message"
    myMessage.Body = "Hello world"
    myMessage.From = New MailAddress("you@example.com")
    myMessage.To.Add(New MailAddress("Receiver"))

    Dim SmtpClient As New SmtpClient
    SmtpClient.Send(myMessage)
End Sub
```
- 4. 在 `</configuration>` 标签之前，添加以下内容：
```xml
<system.net>
  <mailSettings>
    <smtp method="Network" from="Your Name&lt;example.com&gt;">
      <network host="smtp.example.com" />
    </smtp>
  </mailSettings>
</system.net>
```
- 5. 保存所有更改，返回 Email.aspx，并在浏览器中请求它。一段时间后，你应该会在练习第 3 步指定的地址或你的本地拾取文件夹中收到一封电子邮件。

# 常见错误

首先，确保你在 Web.config 中输入了正确的 SMTP 服务器。你可能需要联系你的互联网提供商或网络管理员获取正确的地址以及可选的用户名和密码。此外，确保你使用的邮件服务器允许你发送消息。如果你收到如“服务器需要安全连接或客户端连接未验证”之类的错误，你的提供商可能要求你登录或使用 SSL 安全连接。如果是这样，请检查 Web.config 中的用户名、密码和端口号，或者尝试像之前所示设置 `<network>` 元素的 `enabledsl` 属性。在某些情况下，如果你的开发机器名称包含下划线，可能会出错。在这种情况下，你需要重命名帐户或使用不同的 SMTP 服务器。

另一个问题可能是账户名称与代码中 From 属性中指定的地址不匹配。某些邮件服务器要求这些值完全一致。

最后，如果你收到“指定的字符串不是电子邮件地址所需的格式”错误，请检查是否在 Web.config 文件的 `from` 属性中输入了有效的电子邮件地址。如果你漏掉了 @ 符号或犯了其他语法错误，就会收到此错误。

