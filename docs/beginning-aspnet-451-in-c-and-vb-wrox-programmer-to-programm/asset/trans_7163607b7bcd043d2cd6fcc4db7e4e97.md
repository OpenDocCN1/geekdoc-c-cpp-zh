

myMessage.To.Add(New MailAddress("you@example.com", "Receiver Name"))
myMessage.ReplyToList.Add(New MailAddress(EmailAddress.Text))

```vb
Dim SmtpClient = New SmtpClient
mymtpClient.Send(myMessage)
```

```vb
Message.Visible = True
FormTable.Visible = False
End If
```

## C#

```csharp
protected void SendButton_Click(object sender, EventArgs e)
{
    if (Page.IsValid)
    {
        string fileName = Server.MapPath("~/App_Data/ContactForm.txt");
        string mailBody = File.ReadAllText(fileName);

        mailBody = mailBody.Replace("##Name##", Name.Text);
        mailBody = mailBody.Replace("##EmailAddress##", EmailAddress.Text);
        mailBody = mailBody.Replace("##Phone##", PhoneHome.Text);
        mailBody = mailBody.Replace("##BusinessPhone##", PhoneBusiness.Text);
        mailBody = mailBody.Replace("##Comments##", Comments.Text);

        myMessage = new MailMessage();
        myMessage.Subject = "Response from web site";
        myMessage.Body = mailBody;

        myMessage.From = new MailAddress("you@example.com", "Sender Name");
        myMessage.To.Add(new MailAddress("you@example.com", "Receiver Name"));
        myMessage.ReplyToList.Add(new MailAddress(EmailAddress.Text));

        smtpClient = new SmtpClient();
        mySmtpClient.Send(myMessage);

        Message.Visible = true;
        FormTable.Visible = false;
    }
}
```

再次，请确保你将 Message 的 From 和 To 属性中的电子邮件地址替换为你自己的地址。此外，`replace` 方法是区分大小写的，因此请确保你输入的占位符与你在文中编写的完全一致。

- 7. 保存所有更改，并再次在浏览器中请求 Contact.aspx 页面。输入你的详情并点击 Send 按钮。你会看到文本 Message 出现。

- 8. 检查你发送给自己的电子邮件（如果将邮件存到磁盘上的 C:\TempMail 文件夹中），你将看到一封与图 9-11 类似的电子邮件。

## 在服务器处理数据 | 331

![](img/9e033e3b9560597824f8b22941d6d8bb_368_0.png)

## 工作原理

本次练习中发送邮件的部分与你之前创建的演示页面非常相似。不同之处在于邮件消息正文的来源。你没有在 FormControl 控件的后台代码中硬编码正文，而是将文本移动到了单独的文件。该文件包含几个占位符，它们在运行时会被用户的详情所替换。要一次性读取整个文件，请使用以下代码：

## VBNET

```vb
Dim fileName As String = Server.MapPath("/App_Data/ContactForm.txt")
Dim mailBody As String = File.ReadAllText(fileName)
```

## C#

```csharp
string fileName = Server.MapPath("/App_Data/ContactForm.txt")
string mailBody = File.ReadAllText(fileName);
```

第一行使用 `Server.MapPath` 将虚拟路径转换为其物理对应路径，因为它不依赖于任何硬编码的路径。通过使用虚拟路径更容易可以将你的网站移动到不同的位置，因为 `Server.MapPath("/App_Data/ContactForm.txt")` 返回的是类似 C:\BegASPNET\Site\App_Data\ContactForm.txt 的物理路径。然后，该路径被传递给 `File` 类的 `ReadAllText` 方法，该方法打开文件并返回其内容，然后将其赋值给 `mailBody` 变量。

## 第 9 章验证用户输入

> 注意：每次需要时都读取此文件并不高效。在第 15 章中，你将看到如何缓存文件内容，这样你就不需要每次请求时都读取它。

代码使用了多次调用 `String` 类的 `Replace` 方法，将邮件主体中的静态占位符替换为用户在联系表单中输入的内容。`Replace` 方法的返回值（替换字符串后的新文本）被重新赋值给 `mailBody` 变量。在最后一次调用 `Replace` 之后，`mailBody` 不再包含占位符，而是包含了详情：

```vb
VB.NET
mailBody = mailBody.Replace("##Name##", Name.Text)
mailBody = mailBody.Replace("##Comments##", Comments.Text)

// C#
mailBody = mailBody.Replace("##Name##", Name.Text);
mailBody = mailBody.Replace("##Comments##", Comments.Text);
```

`Replace` 方法区分大小写，如果你发现占位符没有被正确替换，请确保在代码和消息正文中使用相同的大小写。

占位符被在一对双井符号（##）包围。井符号是任意选择的，有助于识别占位符，并最大限度地减少意外替换实际消息中文本的风险。

一旦设置好消息正文，它会被赋值给 `MailMessage` 对象的 `Body` 属性，然后使用 `SmtpClient` 发送，这与你在之前的练习中看到的完全相同。

你可能注意到了对 `MailMessage` 实例 `ReplyTo` 集合的调用。这段代码将用户在 `EmailAddress` 框中输入的电子邮件添加到邮件正文回复列表中。这意味着当你收到消息并想要回复时，回复将发送到用户的地址，而不是你分配给消息的 `From` 地址。这在联系表单中特别有用，因为用户输入电子邮件地址以便你可以直接回复他们。你可能想直接将用户输入的地址赋值给 `From` 属性，但建议不要这样做。某些邮件服务器要求该地址必须是你自己的，因此发送邮件可能会失败。当用户输入无效地址时，你的消息可能会被拒绝。通过将 `From` 地址设置为你自己的并将地址添加到 `ReplyToList`，当你在表单中填写详情并点击 Send 按钮时，可能会注意到页面刷新。这种页面刷新可以通过下一节讨论的 Ajax 技术轻松减少或消除。

## 验证数据的实用技巧

以下列表提供了关于验证数据的实用提示：

- 始终验证用户输入。每当你拥有互联网网站时，为了防止用户向系统输入错误数据，始终使用 ASP.NET 验证控件。

- 始终在验证控件中提供有用的错误信息。将错误分配给 `ValidationSummary` 控件以显示列表，或者让文本属性为空。

- 考虑使用验证控件的 `CssClass` 属性将错误信息的样式移动到单独的 CSS 文件中，而不是直接设置在控件上。

- 当你编写发送邮件的代码时，将邮件主体移动到存储在 `App_Data` 文件夹中的单独文件中，因为这使得你的应用程序更容易维护。

- 在 XML 文件中存储数据时，将其存储在专门为此目的设计的 `App_Data` 文件夹中。这样你的数据文件就集中在一起。此外，默认情况下 Web 服务器连接这些文件，因此访问者无法直接请求它们。

- 测试电子邮件时，始终发送到存在且有效的地址。即使像 `asdf@test.com` 这样的地址看起来无效，该账户很有可能存在并受到监控，这可能会丢失通过电子邮件发送的敏感数据。

- 在开发期间，考虑使用 `SpecifiedPickupDirectory` 作为 SMTP 的 `DeliveryMethod`。它避免了在网络上发送消息，从而获得更快的响应并保持收件箱整洁。

## 总结

用户输入是大多数交互式网站的重要部分。输入来自网站的不同来源：本章创建的联系表单、查询字符串以及其他来源。为了防止用户向系统输入无效甚至危险的内容，在处理输入之前对其进行验证是非常重要的。

