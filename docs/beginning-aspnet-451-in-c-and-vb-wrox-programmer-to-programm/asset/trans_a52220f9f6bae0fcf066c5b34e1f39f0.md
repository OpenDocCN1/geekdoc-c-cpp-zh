
如果你无法从本地机器成功发送邮件，始终可以使用 `SpecifiedPickupDirectory` 交付选项将文件存储在本地机器上。这样一来，你只需要在部署网站时配置邮件服务器，这在开发期间为你提供了一个快速、方便的解决方案。

## 工作原理

你在后置代码（Code behind）中添加了以下 `Imports` 或 `using` 语句：

```
VB.NET
Imports System.Net.Mail
```

```C#
using System.Net.Mail;
```

该语句用于使此命名空间中的类在代码可用，而无需带有完整的命名空间前缀。这让你能够创建如下的 `MailMessage` 实例：

```
VB.NET
myMessage As MailMessage = New MailMessage()
```

```C#
MailMessage myMessage = new MailMessage();
```

如果没有 `Imports` 或 `using` 语句，你将需要以下代码：

```
VB.NET
myMessage As System.Net.Mail.MailMessage = New System.Net.Mail.MailMessage()
```

```C#
System.Net.Mail.MailMessage myMessage = new System.Net.Mail.MailMessage();
```

`Page_Load` 中的代码创建了一个新的 `MailMessage` 对象并设置了 `Subject`（主题）和 `Body`（正文）属性。随后代码处理电子邮件的发送者和接收者：

```
VB.NET
myMessage.From = New MailAddress("*@example.com", "Sender Name")
myMessage.To.Add(new MailAddress("*@example.com", "Receiver Name"));
```

```C#
myMessage.From = new MailAddress("*@example.com", "Sender Name")
myMessage.To.Add(new MailAddress("*@example.com", "Receiver Name"));
```

`MailMessage` 的 `From` 属性类型为 `MailAddress`，因此你可以直接分配一个新的 `MailAddress`。`MailAddress` 类的构造函数接受字符串格式的电子邮件地址和友好名称，因此你可以用一行代码创建创建并分配 `From` 地址。

## 在服务器端处理数据 | 327

`MailMessage` 类的属性是一个集合，因此你不能直接分配 `MailAddress` 实例。相反，你需要使用 `Add` 方法来分配地址。这允许你通过多次调用 `Add` 来添加多个接收者，每次传递一个不同的 `MailAddress` 实例。你可以类似地使用 `CC` 和 `Bcc` 属性将电子邮件地址分配给邮件的抄送和密抄字段。

代码的最后几行发送了实际消息：

```
VB.NET
Dim mySmtpClient As SmtpClient = New SmtpClient()
mySmtpClient.Send(myMessage)
```

```C#
smtpClient mySmtpClient = new SmtpClient();
mySmtpClient.Send(myMessage);
```

当调用 `Send` 方法时，`SmtpClient` 会扫描 `Web.config` 文件以查找配置好的 SMTP 服务器或本地投放文件夹。然后它联系该服务器并交付消息或将其保存到本地。

> 在之前的尝试中，邮件的正文内容是硬编码的。这并不总是最佳解决方案，因为这意味着每你想更改文本都需要扫描并修改代码。最好使用基于文本的模板。你将在下一节中看到如何这样做。

## 从文本文件中读取

.NET Framework 提供了一些实用的类和方法，使得处理文件变得非常简单。例如，位于 `System.IO` 命名空间中的 `File` 类允许你读取和写入文件、创建和删除文件以及在磁盘上移动文件。该类仅包含静态方法，这意味着你不需要创建类的实例。相反，你可以直接在 `File` 类上调用方法。例如，要读取文本文件的内容，可以使用以下代码：

```
VB.NET
Dim myContents As String = System.IO.File.ReadAllText("C:\MyFile.txt")
```

```C#
string myContents = System.IO.File.ReadAllText(@"C:\MyFile.txt");
```

在此示例中，C# 中的文件名带有 `@` 前缀，以避免对每个反斜杠 `\` 都进行转义。在 C# 中，反斜杠有特殊含义（用于“转义”其他具有特殊含义的字符），因此要在字符串中使用它，通常需要在它前面加另一个反斜杠。使用 `@` 符号告诉编译器应将每个反斜杠视为字面量，忽略字符的特殊含义。它还保留了字符串内部任何换行符。

下表列出了 `File` 类中最常用的、允许你处理文件的方法。

| METHOD | VALUE |
|---|---|
| AppendAllText | 将指定的字符串追加到文本文件。如果文件不存在，则先创建它。 |
| Copy | 将文件从一个位置复制到另一个位置。 |
| Delete | 从磁盘上删除指定的文件。 |
| Exists | 检查磁盘上是否存在指定的文件。 |
| Move | 将指定的文件移动到不同的位置。 |
| ReadAllText | 读取文本文件的内容。 |
| WriteAllText | 将字符串的内容写入新文件，如果目标文件已存在则覆盖它。 |

你可以将这些方法用于各种用途。例如，当你上传了一个文件时，可以使用 `Move` 方法将其移动到不同的文件夹。此外，当你想要移除不需要的上传文件时，请使用 `Delete` 方法。

`ReadAllText` 方法用于读取文本文件的完整内容。例如，在通过电子邮件发送文本时，你可以将邮件的正文存储在文本文件中。当你准备发送邮件时，调用 `ReadAllText` 并将该方法返回的内容分配给邮件的正文。你将在接下来的尝试中看到它是如何运作的。

## 尝试从联系表单用户控件发送邮件

此练习演示了如何使用电子邮件将数据从联系表单发送到自己的收件箱。作为邮件正文，代码读取了一个包含占位符的文本文件。这些占位符用源自实际用户数据填充。

- 1. 在网站的 `App_Data` 文件夹中添加一个新的文本文件。如果你还没有 `App_Data` 文件夹，右键点击网站并选择“添加 ASP.NET 文件夹 -> 添加 App_Data”。右键点击 `App_Data` 文件夹并选择“新建项”。选择“文本文件”，将文件命名为 `ContactForm.txt` 并点击“添加”。
- 2. 在文件中输入以下文本，包括用双符号包裹的占位符：
Hi there,
用户在站点留下了以下反馈：
##Name##
##Email##
##HomePhone##
##BusinessPhone##
##Comments##
- 3. 打开 `ContactForm.ascx` 的后置代码，并在文件顶部导入以下命名空间（无需输入）：

```
VB.NET
Imports System.IO
Imports System.Net.Mail
```

```C#
using System.IO;
using System.Net.Mail;
```

- 4. 切换到标记视图（Markup View），并为带有服务器属性的表格添加 `server` 和 `id="FormTable"` 属性。这样当表单提交时，你就可以程序地包含整个表格。要执行此操作，找到起始 `<table>` 标签并修改如下：
```
<table class="auto-style" runat="server" id="FormTable">
<asp:Label ID="Message" runat="server" Text="Message Sent" Visible="false" />
</table>
```
- 5. 滚动到文件末尾，在关闭 `</table>` 标签之后，添加一个标记为 `Message` 的标签。将其属性设置为 `Message Sent`。通过将 `Visible` 设置为 `false` 来隐藏该标签。
- 6. 切换到设计视图（Design View），将 `ValidationSummary` 的 `Summary` 设置回 `true`，并将 `ShowMessageBox` 设置为 `false`。由于这些是默认值，VS 会从标记中移除这些属性。接下来，双击发送按钮。在 VS 添加的事件处理器内部，添加以下代码：

```
VB.NET
Protected Sub SendButton_Click(Sender As Object, e As EventArgs)
Handles SendButton.Click
If If.IsPostBack Then
Dim fileName As String = "../App_Data/ContactForm.txt"
Dim mailBody As String = File.ReadAllText(fileName)
mailBody = mailBody.Replace("##Name##", Message.Text)
mailBody = mailBody.Replace("##Email##", EmailAddress.Text)
mailBody = mailBody.Replace("##HomePhone##", PhoneHome.Text)
mailBody = mailBody.Replace("##BusinessPhone##", PhoneBusiness.Text)
mailBody = mailBody.Replace("##Comments##", Comments.Text)

Dim myMessage As MailMessage = New MailMessage()
myMessage.Subject = "Response from web"
myMessage.Body = mailBody

myMessage.From = New MailAddress("*@example.com", "Sender Name")
Dim mySmtpClient As SmtpClient = New SmtpClient()
mySmtpClient.Send(myMessage)
End Sub
```

```C#
protected void SendButton_Click(object sender, EventArgs e)
{
    if (!Page.IsPostBack)
    {
        string fileName = "../App_Data/ContactForm.txt";
        string mailBody = File.ReadAllText(fileName);
        mailBody = mailBody.Replace("##Name##", Message.Text);
        mailBody = mailBody.Replace("##Email##", EmailAddress.Text);
        mailBody = mailBody.Replace("##HomePhone##", PhoneHome.Text);
        mailBody = mailBody.Replace("##BusinessPhone##", PhoneBusiness.Text);
        mailBody = mailBody.Replace("##Comments##", Comments.Text);

        MailMessage myMessage = new MailMessage();
        myMessage.Subject = "Response from web";
        myMessage.Body = mailBody;

        myMessage.From = new MailAddress("you@example.com", "Sender Name");
        SmtpClient mySmtpClient = new SmtpClient();
        mySmtpClient.Send(myMessage);
    }
}
```

partial class ContactForm : System.Web.UI.UserControl
{
}
