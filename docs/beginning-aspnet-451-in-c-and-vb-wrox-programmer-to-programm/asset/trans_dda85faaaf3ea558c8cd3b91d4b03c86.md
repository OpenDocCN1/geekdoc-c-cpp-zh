
对于所有你未显式定义的 HTTP 状态码，将使用 `defaultRedirect` 属性来确定自定义错误页。

`redirectMode` 属性决定了向用户显示新页的方式，将在本章稍后部分讨论。

虽然自定义错误页可以保护用户免受异常详情的影响，但它们并不能帮助你发现发生了异常。这些页面都会隐藏真实的错误，并显示一个包含自定义错误消息的页面。为了接收这些异常的通知，你可以编写代码检查异常并向你发送一封包含详细信息的电子邮件。或者，你可以编写代码将错误详情插入数据库，或将其写入文本文件。

ASP.NET 为你提供了一个中心位置来编写在异常发生时触发的代码。你可以在 `Global.asax` 文件中一个名为 `Application_Error` 的特殊处理程序中编写这些代码，该文件你在第 11 章中见过。在该事件内部，你可以收集有关异常的相关数据，将其放入电子邮件并发送到自己的收件箱。这让你获得有关网站上发生异常的详细信息，有助于你尽快解决问题。你可以在下一个练习中查看如何编写这些代码。

## 尝试一下 全站范围异常处理

在本次“尝试一下”中，你将学习如何在 `Global.asax` 文件中编写代码通过电子邮件发送异常消息。此外，你将学习如何创建全局错误页，以便在发生错误时向用户显示。

- 1. 从网站根目录打开 `Global.asax` 文件。

- 2. 在文件顶部、`Application` 指令之后，添加以下 `Import` 语句。注意，在标记视图（Markup View）中添加 `Import` 语句时，VB.NET 和 C# 使用关键字 `Import`，而不是你在代码后台（Code Behind）中通常使用的 `Imports`：

```vb
VB.NET
<@ Language="VB" *>
@ Import Namespace="System.Net.Mail" *>
```

```csharp
C#
<@ Language="C#" *>
@ Import Namespace="System.Net.Mail" *>
```

- 3. 在 `Global.asax` 文件应存在的 `Application_Error` 处理程序内部，添加以下代码，每当网站发生任何未处理的异常时，这些代码就会被触发。如果没有该处理程序，请确保你输入以下片段中的所有代码，包括未边界的部分：

```vb
VB.NET
Sub Application_Error(ByVal sender As Object, ByVal e As EventArgs)
 If HttpContext.Current.Server.GetLastError() IsNot Nothing Then
 Dim Exception As Exception = 
 HttpContext.Current.Server.GetLastError().BaseException()
 Dim mailSubject As String = "Error in page " & Request.Url.ToString()
```

```vb
VB.NET
Dim message As String = String.Empty
message &= "<strong>Message</strong><br />" * myException.Message & "<br />"
message &= "<strong>StackTrace</strong><br />" * myException.StackTrace & "<br />"
message &= "<strong>Query</strong><br />" * Request.Query.String.ToString() & "<br />"
Dim myMessage As MailMessage = New MailMessage("@example.com", "@example.com", mailSubject, message)
myMessage.IsBodyHtml = true
Dim SmtpClient As SmtpClient = New SmtpClient()
mySmtpClient.Send(myMessage)
End If
```

```csharp
C#
void Application_Error(object sender, EventArgs e)
{
    if (HttpContext.Server.GetLastError() != null)
    {
        Exception myException = HttpContext.Server.GetLastError().GetBaseException();
        string mailSubject = "Error in page " + Request.Url.ToString();
        string message = String.Empty;
        message += "<strong>Message</strong><br />" + myException.Message + "<br />";
        message += "<strong>StackTrace</strong><br />" + myException.StackTrace + "<br />";
        message += "<strong>Query</strong><br />" + Request.Query.String.ToString() + "<br />";
        MailMessage myMessage = new MailMessage("@example.com", "@example.com", mailSubject, message);
        myMessage.IsBodyHtml = true;
        SmtpClient mySmtpClient = new SmtpClient();
        mySmtpClient.Send(myMessage);
    }
}
```

不要忘记更改传递 `MailMessage` 构造函数的两个电子邮件地址。第一个地址代表发送者地址，第二个地址持有接收者地址。

- 4. 保存对 `Global.asax` 文件的所有更改。

- 5. 接下来，打开 `Web.config` 文件，作为 `<system.web>` 的直接子元素添加以下 `customErrors` 元素：

```xml
<system.web>
  <customErrors mode="On" defaultRedirect="~/Errors/OtherErrors.aspx"
                 redirectMode="ResponseWrite" />
    <error statusCode="404" redirect="~/Errors/Error404.aspx" />
  </customErrors>
```

保存并关闭配置文件。

- 6. 在网站根目录下创建一个文件夹并命名为 `Errors`。

- 7. 在此文件夹内创建新的 Web Forms，分别命名为 `Error404.aspx` 和 `OtherErrors.aspx`。确保它们都基于你的自定义模板，这样你就可以使用主页并继承自 `BasePage`。如果你遵循了上一章的练习并使用 `Profile` 来存储用户的喜好主题，请参考“常见错误”。

- 8. 将 `Error404.aspx` 的标题设置为 `File Found`。在主页中添加以下内容：

```xml
<asp:Content ID="Content2" ContentHolderID="MainContent" runat="Server">
<h1>File Not Found</h1>
<p>The page you requested could not be found. Please <a href="/">choose a different page</a>.</p>
</asp:Content>
```

- 9. 切换到设计视图，双击页面设置 `Page_Load` 并添加以下代码：

```vb
VB.NET
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
Response.Status = "404 Not Found"
Response.TryCustomErrors = True
```

```csharp
C#
protected void Page_Load(object sender, EventArgs e)
{
    Response.Status = "404 Not Found";
    Response.TryCustomErrors = true;
}
```

- 10. 打开通用的 `Errors.aspx` 页面，将其标题设置为 `An Error Occurred` 并创建以下内容：

```xml
<asp:Content ID="Content2" ContentHolderID="MainContent" runat="Server">
<h1>An unknown error</h1>
<p>An error occurred in the page you requested. We'll fix it.</p>
</asp:Content>
```

## Exception Handling | 67

```csharp
C#
protected void Page_Load(object sender, EventArgs e)
{
    Response.TryCustomErrors = true;
}
```

由于此页面将用于所有可能的 404 错误，因此没有必要设置显式的 `Status` 或 `StatusCode`。

![FIGURE 18-4](img9e033e3b9560597824f8b22941d6dbb_716_0.png)
