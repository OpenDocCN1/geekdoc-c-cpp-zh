
你可以将主页中 `ThemeList_SelectedIndexIndexChanged` 中的代码简化为：

## VB.NET

```vbnet
Protected Sub ThemeList_SelectedIndexIndexChanged(sender As Object, e As EventArgs) Handles ThemeList.SelectedIndexIndexChanged
    Profile.FavoriteTheme = ThemeList.SelectedValue
    Response.Redirect(Request.Url.ToString())
End Sub
```

## C#

```csharp
protected void ThemeList_SelectedIndexIndexChanged(object sender, EventArgs e)
{
    Profile.FavoriteTheme = ThemeList.SelectedValue;
    Response.Redirect(Request.Url.ToString());
}
```

## 第 18 章

## 练习 1 答案

调试是在开发环境中观察代码执行的过程——通过调查变量和查看对象来理解代码的执行路径——旨在寻找并修复错误（bugs）。调试通常在你的 Visual Studio IDE 中开发阶段进行。

另一方面，追踪（Tracing）可以为你提供关于代码在运行时执行的信息。正如本章讨论的，你可以使用追踪来获取有关触发事件及其触发顺序的信息。此外，你还可以向跟踪中添加自己的信息。由于禁用追踪配置会极大地减少性能开销，你可以将追踪调用保留在代码中，以便在需要时轻松禁用或启用。

## 练习 2 答案

阻止异常导致用户界面崩溃的最佳方法是将代码封装在 `Try/Catch` 块中。这样，当出现问题时，你可以向用户显示错误消息。你的代码可能如下：

## VB.NET

```vbnet
Try
  //在此处执行代码以发送电子邮件。
Catch As SmtpException
  ErrorMessage.Text = "发送消息时发生错误。"
End Try
```

## C#

```csharp
try
{
  //在此处执行代码以发送电子邮件。
} catch (SmtpException ex) 
{ 
    ErrorMessage.Text = "发送消息时发生错误..."; 
}
```

## 练习 3 答案

为了理解网站中发生了哪些异常并找到它们发生的位置（即是哪些页面或代码文件导致了异常），你可以在 `Application_Error` 事件处理程序中使用一些代码记录所有异常。你可以在此方法中截获的异常详情应该帮助你理解异常产生，反之也应该帮助找到解决方案。

为了防止用户看到“死亡黄屏”错误消息，你需要使用自定义错误页面。你应该创建一个简单的 Web Form，告诉用户发生了问题。

要让 ASP.NET 运行时显示该文件的内容而不是错误消息，你需要在 `Web.config` 中包含以下元素：

```xml
<customErrors mode="On" defaultRedirect="~/Errors/AllOtherErrors.aspx">
  <error statusCode="500" redirect="~/Errors/Error500.aspx" />
</customErrors>
```

该元素为代码意外崩溃时发生的 500 错误代码设置了一个特殊页面。

当发生其他异常（例如“未找到页面”错误）时，用户将被重定向到更通用的 AllOtherErrors.aspx 页面。

## B 配置 SQL Server 2012

到目前为止，书中的练习假设你使用 Microsoft SQL 2012 LocalDB 版 11.0 作为 Planet Wrox 项目的数据库。SQL Express LocalDB 版 11.0 非常适合开发，因为它是免费、轻量且易于使用的。然而，它并非设计用于生产环境，在处理能力、内存使用和数据库大小方面存在限制。在 LocalDB 版本不足的情况下，你需要查看更大的版本：SQL Server 2012 Express 版或商业版的 Management Studio Express，以及 SQL Server 2012 的版本（如标准版或企业版）。在本附录中，你将学习更多关于 SQL Server 2012、其安全模型、如何让你的 SQL Server 2012 数据库与 ASP.NET 4.5.1 网站协同工作，以及如何使用 SQL Server Management Studio Express（微软提供的用于管理数据库的免费工具）。

尽管本附录没有讨论 SQL Server 的早期版本，但你会发现大多数概念也适用于这些旧版本。事实上，你也可以使用 SQL Server 2012 Management Studio 管理旧的 SQL Server 2005 和 2008 数据库。本附录使用 SQL Server Express 版是因为它是免费下载的，但相同的原理适用于 SQL Server 的商业版本。

## 配置 SQL SERVER 2012

在配置数据库之前，你需要了解与数据库和 Web 应用程序不可避免相关的各种安全概念。在第 19 章中，你学习了 Web 服务器使用的帐户在配置文件系统安全设置时起着重要作用，连接到 SQL Server 时也是如此。在接下来的章节中，你将快速入门连接 SQL Server 的不同方法。在随后的部分中，你将看到如何将 .ndf 数据库文件附加到 SQL Server，然后讨论如何配置你的应用程序和数据库以便它们相互通信。

## 术语和概念

当你连接到 SQL Server 数据库时，SQL Server 需要知道你的身份，以便对对象（如数据库中的表）执行正确的访问策略。SQL Server 支持两种身份验证机制：SQL Server 身份验证和 Windows 身份验证（通常称为集成安全）。两者都有各自的优势，并要求你编写不同的连接字符串来连接 SQL Server。

## SQL Server 身份验证

使用 SQL Server 身份验证时，SQL Server 负责用户管理。你使用 Management Studio 管理 SQL 数据库，可以是附录稍后介绍的 Express 版，也可以是商业版的完整版本。SQL Server 使用登录（login）来处理身份验证。你通过提供登录名和密码在服务器级别定义此登录。可以将登录映射到数据库用户以访问特定数据库。

要将 Web应用程序连接到需要 SQL Server 身份验证的 SQL 安装，你需要在应用程序连接字符串中传递用户名和密码。典型的连接字符串如下：

```text
Data Source=ServerName;Initial Catalog=DatabaseName;
User Id=UserName;Password=Password;
```

在这种情况下，Data Source 指向未命名的 SQL 实例：通过机器名即可访问。也可以将 SQL Server 安装为命名实例。对于命名实例，服务器名后跟着反斜杠（\）和特定的 SQL 实例名称。例如：

```text
Data Source=ServerName\InstanceName;Initial Catalog=DatabaseName;
User Id=UserName;Password=Password;
```

当你需要通过互联网连接远程 SQL Server 时，通常使用 SQL Server 身份验证，因为下文的 Windows 身份验证不支持这种场景。

## Windows 身份验证

使用 Windows 身份验证时，Windows 操作系统负责用户管理。与数据库的所有交互都在调用者的上下文中，因此数据库知道是谁在访问系统。你需要将 Windows 登录映射到 SQL Server 数据库用户，以便 SQL Server 确定该账户是否有足够的权限。我将在文中演示方法：

使用 Windows 身份验证的典型连接字符串如下：

```text
Data Source=ServerName;Initial Catalog=DatabaseName;Trusted_Connection=True
```

你不需要指定用户名和密码，而是添加 `Trusted_Connection=True` 以以调用者的上下文连接到服务器。你可能会遇到 `Integrated Security=True` 设置，其效果相同。
