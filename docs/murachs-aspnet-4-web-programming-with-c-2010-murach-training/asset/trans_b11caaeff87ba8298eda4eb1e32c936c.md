

## 电子邮件客户端中 HTML 消息的显示方式

![](img/c024ccf88e28c30c07dd410d4342288f_696_0.png)

### 创建并发送简单 HTML 消息的方法

```csharp
private void SendConfirmation()
{
    MailMessage msg = new MailMessage("halloween@murach.com", toAddress);
    msg.Subject = "Order Confirmation";
    msg.Body = this.GetConfirmationMessage();
    msg.IsBodyHtml = true;
    string file = "C:\\aspnet4_cs\\Ch20HalloweenStore\\Images\\banner.jpg";
    msg.Attachments.Add(new Attachment(file));
    SmtpClient client = new SmtpClient("localhost");
    client.Send(msg);
}
```

```csharp
private string GetConfirmationMessage()
{
    string message = "<html><head><title>Order confirmation</title></head>"
                   + "<body><img src='banner.jpg' alt='Halloween Store' />"
                   + "<br /><br /><h3>Thanks for your order, "
                   + dvCustomer[0]["FirstName"].ToString() + " "
                   + dvCustomer[0]["LastName"].ToString() + "!</h3>"
                   + "<p>Your order total is " + total.ToString("c")
                   + ".</p></body></HTML>";
    return message;
}
```

### 描述

- 要以 HTML 格式创建电子邮件消息，请将 IsBodyHtml 属性设置为 True。然后，您可以在分配给 Body 属性的消息中使用 HTML。
- HTML 电子邮件消息可以包含指向您网站的链接。但是，您应避免发送包含脚本或 Web 表单控件的 HTML。许多邮件服务器会拒绝它们，因为它们可能是恶意的。
- 如果 HTML 包含 `<img>` 标签，您应将图像文件作为附件包含在内。否则，收件人将无法在电子邮件中看到图像。

Figure 20-6   如何创建 HTML 消息

## 如何使用自定义错误处理

当 ASP.NET 应用程序中发生错误时，会抛出异常。然后，如果应用程序未处理该异常，就会显示 ASP.NET 服务器错误页面。此页面包含错误消息、引发未处理异常的源代码部分以及其他调试信息。由于这种类型的错误页面通常不适合应用程序的用户，因此在完成网站测试但在正式上线之前，您通常会用自己的自定义错误页面替换通用错误页面。

### 自定义错误处理的介绍

Figure 20-7 描述了可用于显示自己的自定义错误页面的四种技术。根据您的应用程序，您可能需要使用其中一种或多种技术。

第一种技术是将可能生成异常的代码放在 try-catch 语句的 try 块中。然后，如果确实发生异常，您可以重定向到自定义错误页面。

第二种技术是在页面的代码隐藏文件中编写 Page_Error 方法。每当页面上发生未处理的异常时，就会调用此方法。然后，在 Page_Error 方法中，您将用户重定向到自定义错误页面。

第三种技术是在 global.asax 文件中编写 Application_Error 方法。每当在没有 Page_Error 方法的页面上发生未处理的异常时，就会调用此方法。然后，Application_Error 方法可以将用户重定向到自定义错误页面。

第四种技术是使用 web.config 文件中的 customErrors 元素指定自定义错误页面。此技术用于在发生常见的 HTTP 错误例如 404 – 未找到错误时显示自定义错误页面。

### 浏览器中的自定义错误页面

![](img/c024ccf88e28c30c07dd410d4342288f_698_0.png)

### 发生异常时显示自定义错误页面的四种方法

- 使用 try-catch 语句捕获发生的异常，然后重定向或转移到自定义错误页面。
- 使用代码隐藏文件中的 Page_Error 方法在页面级别捕获未处理的异常，然后重定向或转移到自定义错误页面。
- 使用 global.asax 文件中的 Application_Error 方法在应用程序级别捕获未处理的异常，然后重定向或转移到自定义错误页面。
- 使用 web.config 文件的 customErrors 元素指定在特定类型的 HTTP 错误时显示的自定义错误页面。

### 描述

- 如果发生不可恢复的错误，大多数应用程序会显示自定义错误页面以告知用户发生了问题。
- 在幕后，自定义错误页面还可能将错误记录在日志中或向应用程序的支持人员发送电子邮件以通知他们错误。
- 自定义错误页面通常使用 Exception 对象来显示描述错误的详细消息。

## 如何获取和使用错误的 Exception 对象

Figure 20-8 显示了如何使用 Exception 类和 HttpServerUtility 类的属性和方法来获取和使用错误的 Exception 对象。这是包含已发生异常信息的对象。此图中的示例展示了其工作原理。

第一个示例展示了如何使用 try-catch 语句获取 Exception 对象。正如您所知，如果 try 块中的任何语句抛出异常，catch 块就会捕获 Exception 对象。您可以在代码隐藏文件的任何方法中使用此技术。

第二个示例展示了如何在 Page_Error 方法内获取 Exception 对象。如果异常未被代码隐藏文件的其他方法处理，此方法会自动执行。在这里，您使用页面 Server 属性访问的 Server 对象的 GetLastError 方法。

第三个示例展示了如何在 global.asax 文件的 Application_Error 方法内获取 Exception 对象。如果异常未被代码隐藏文件中的任何方法包括 Page_Error 方法处理，此方法会自动执行。但是，在 Application_Error 方法中，GetLastError 方法不会返回正确的 Exception 对象。那是因为如果发生异常并且异常未被 try-catch 语句或 Page_Error 方法处理，就会抛出第二个名为 HttpUnhandledException 的异常。因此，GetLastError 方法返回 HttpUnhandledException 异常，而不是最初导致错误的异常。要访问原始异常，您必须使用 GetLastError 方法返回的 Exception 对象的 InnerException 属性。

尽管您可能认为可以使用 ClearError 方法清除 HttpUnhandledException 异常，然后使用 GetLastError 获取原始异常，但这行不通。那是因为您只能使用 GetLastError 获取最近发生的异常的 Exception 对象。在这种情况下，就是 HttpUnhandledException 异常。

第四个示例展示了在测试应用程序时如何使用 Exception 对象的属性。在这里，HttpResponse 对象的 Write 方法用于在页面上显示 Message 和 Source 属性。请注意，在执行此方法之前，使用 Server 对象的 ClearError 方法清除错误。这样，ASP.NET 服务器错误页面就不会显示。

### Exception 类的常见属性

| 属性 | 描述 |
|---|---|
| Message | 描述错误的<|message|> |
| Source | 导致错误的应用程序或对象的名称。 |
| InnerException | 在应用程序级别导致异常的 Exception 对象。 |

### 用于处理异常的 HttpServerUtility 类的方法

| 方法 | 描述 |
|---|---|
| GetLastError() | 获取最近的异常。 |
| ClearError() | 清除最近的异常。 |

### 在方法级别获取 Exception 对象的代码

```csharp
try
{
    statements that could throw an exception
}
catch (Exception ex)
{
    statements that use the Exception object named ex
}
```

### 在页面级别获取 Exception 对象的代码

```csharp
Exception ex = Server.GetLastError();
```

### 在应用程序级别获取 Exception 对象的代码

```csharp
Exception ex = Server.GetLastError().InnerException;
```

### 显示 Exception 对象的错误消息和来源的代码

```csharp
Server.ClearError();
Response.Write(ex.Message + "<br />" + ex.Source);
```

### 描述

- 您可以在代码隐藏文件的任何方法中使用 try-catch 语句来获取错误的 Exception 对象。
- 当发生未处理的异常时，会执行 Page_Error 方法。在此方法内，您使用 Server 对象的 GetLastError 方法获取错误的 Exception 对象。
- 如果您未使用 try-catch 语句或 Page_Error 方法处理异常，就会抛出 HttpUnhandledException。然后，您可以使用 global.asax 文件中的 Application_Error 方法处理异常。为此，您使用 Server 对象的 GetLastError 方法获取 HttpUnhandledException 的 Exception 对象，并使用该异常的 InnerException 属性获取导致错误的 Exception 对象。
- 在测试期间，您可能希望使用 HttpResponse 对象的 Write 方法将有关异常的信息写入页面。在执行此操作之前，您需要从 Server 对象清除错误，以便不会显示 ASP.NET 服务器错误页面。

