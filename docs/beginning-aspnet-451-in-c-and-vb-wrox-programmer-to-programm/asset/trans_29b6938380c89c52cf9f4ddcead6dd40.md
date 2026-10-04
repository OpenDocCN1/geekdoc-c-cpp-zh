
因此，拥有一个良好的错误处理策略非常重要。这种策略应该让你尽可能避免错误，并优雅地处理错误，并在错误发生时可选地记录相关信息。

下一节将介绍检测和处理错误（在 .NET 术语中称为异常）；在本章的后续部分，你将学习如何记录错误并保护用户免受带有详细异常信息的丑陋页面。

## 捕获和处理异常

通常，当发生严重异常时，用户会看到一条错误消息。例如，如果你尝试向一个未运行或不允许你连接的邮件服务器发送消息，你将获得一个提供错误详情的异常。你获得的异常是继承自 `System.Exception` 类的实例，该类是所有异常的基类。存在许多异常，每个异常都有独特的用途。

默认情况下，此异常会一直传播到用户界面，并在那里以所谓的“黄屏”（Yellow Screen of Death）的形式呈现，这引用了 Windows 崩溃时看到的“蓝屏”。你将在下一个练习中看到此错误的真实示例。

显然，如果你能预判异常并编写代码来防止其在用户界面中显示，情况会好得多。例如，你可以向用户显示一个格式良好的消息，告知他们目前无法发送消息。

幸运的是，这些场景已深度集成在 C# 和 Visual Basic 等 .NET 语言中。在这些语言中，你可以使用 `Try Finally` 块（C# 中为 `try finally`），将可能抛出异常的代码封装在 `Try` 块中。注意，VB.NET 和 C# 版本的这些关键字仅在于大小写；在本文的后续代码块中，我指的是大写版本。

当发生异常时，`Try` 块中的剩余代码将被跳过，并运行 `Catch` 块中的代码来处理错误。你可以拥有多个 `Catch` 块来处理特定的异常，但只有第一个捕获到异常类型的块会触发。因此，将各个 `Catch` 块按通用到具体的顺序排序非常重要，以便在特定的 `Catch` 块中处理异常。你将在稍后看到更多内容。

`Try` 或 `catch` 块后面可以跟一个 `Finally` 块。`Finally` 块中的代码无论是否发生异常都会执行，因此它是某些清理代码的理想位置。

`Catch` 和 `Finally` 块都是可选的，尽管你至少需要其中一个。

以下示例中的代码尝试发送电子邮件，然后将 Label 的 `Property` 设置为 `userMessage` 的值。注意：`myMessage` 和 `mySmtClient` 由此示例未显示的代码创建的。`userMessage` 在 `Try` 块中（代码执行成功时）或 `Catch` 块中（发生错误时）被赋值。无论如何，此 `userMessage` 都会在 `Finally` 块中赋值给 `Label`：

### VB.NET

```vb
Dim userMessage As String = String.Empty
Try
  mySmtpClient.Send(myMessage)
  Message = "Message sent"
Catch ex As Exception
  Message = "An unknown error occurred."
Finally
  Message.Text = userMessage
End Try
```

### C#

```csharp
string userMessage = string.Empty;
try{
  mySmtpClient.Send(myMessage);
  userMessage = "Message sent";
} catch (Exception ex){
  userMessage = "An unknown error occurred.";
} finally {
  Message.Text = userMessage;
}
```

在此代码示例中，`Catch` 块被设置为处理 `System.Exception` 类型的异常，它是 .NET Framework 中所有异常的基类。此异常是由...发送的。在 C# 中，如果你在代码中未使用 `ex` 变量，可以省略它：

### C#

```csharp
catch (Exception)
{
  userMessage = "An unknown error occurred.";
}
```

当你认为代码可能会遇到多个异常时，指定异常类型是非常有用的。在这种情况下，你可以为不同的异常类型拥有多个 `Catch` 块。以下代码能够处理邮件发送过程中可能发生的特定 `SmtpException`，并且通过其通用的 `Catch` 块捕获所有其他异常：

### VB.NET

```vb
Try
  mySmtpClient.Send(myMessage)
Catch smtpException As SmtpException
  userMessage = "Sorry, an error occurred while sending your message."
Catch ex As Exception
  ' Something went wrong
End Try
```

### C#

```csharp
try {
  mySmtpClient.Send(myMessage);
} catch (SmtpException) {
  userMessage = "Sorry, an error occurred while sending your message.";
} catch (Exception) {
  // Something went wrong
}
```

`Catch` 块的顺序非常重要。.NET 从上到下扫描 `Catch` 块列表并触发第一个匹配的异常。

## 尝试处理异常

在此尝试中，你看到如何编写异常处理代码来捕获发送电子邮件的问题。这些问题可能在邮件服务器宕机时发生。为了模拟损坏的邮件服务器，你将使用一个不存在的邮件服务器导致崩溃。

你会将 `Catch Finally` 代码放在单独的页面中，以便密切观察其行为。当你理解了它的原理后，将修改 `Form.ascx` 页面以使用控件并整合异常处理代码。你在演示页面中使用它的原因是，用户控件 `UpdatePanel` 默认会显示异常的脏细节，这使得很难看到内容。

- 在 Demos 文件夹中创建一个新文件并命名为 `ExceptionHandling.aspx`。基于你的自定义模板创建页面，并将标题设置为 `Exception Demo`。
- 在内容区域添加一个 Label 控件，并将其 ID 设置为 `Message`。
- 切到设计视图，通过双击页面的只读区域为页面 Load 事件设置事件处理程序。然后在文件顶部，为 `System.Net.Mail` 命名空间添加 `Imports` 或 `using` 语句：

### VB.NET

```vb
Imports System.Net.Mail
```

### C#

```csharp
using System.Net.Mail
```

添加以下代码来处理 VS 创建的事件。注意这段代码与 Form.ascx 用户控件中添加的代码几乎相同，因此你可以从该文件中复制部分代码来节省打字时间。注意代码如何将 "DoesNotExist" 作为邮件主机参数传递给 `SmtpClient` 的构造函数。这样做是为了故意触发异常。

### VB.NET

```vb
Protected Sub Page_Load(sender As Object, e As EventArgs)
```

### C#

```csharp
protected void Page_Load(object sender, EventArgs e)
```

不要忘记将两个电子邮件地址更改为你自己的。

打开 Web.config 并注释掉 `<system.net>` 元素（选择整个元素然后按 Ctrl+K 再按 Ctrl+C）。你在第 9 章中添加了此元素以配置站点发送电子邮件。通过临时禁用它，可以确保没有来自
