

按控件添加到页面的顺序。设置每个控件的 TabIndex 属性，从第一个开始为 1；零表示 TabIndex 未设置。如果多个控件具有相同的 TabIndex，则选项卡会按控件添加到页面的顺序移动。

## 将焦点设置到控件

你可以使用控件的 Focus 方法或页面的 SetFocus 方法将焦点设置到 ASP Web 控件。例如，要将初始焦点设置到 QuantityTextBox，请在 Page_Load 事件处理程序中使用以下两个语句之一：

```
QuantityTextBox.Focus()
```

或

```
SetFocus(QuantityTextBox)
```

## 反馈 7.2

+   1. 主页是如何创建的？如何将 Web 页面分配给主页？
+   2. 如果你未设置任何控件的 TabIndex 属性，按 Tab 键时焦点按什么顺序移动？
+   3. 创建级联样式表并将其应用于 Web 页面的一部分需要哪些步骤？

## 使用验证控件

ASP.NET 提供了几个控件，可自动验证输入数据。你添加一个验证控件，将其附加到文本框等输入控件，并设置错误消息。运行时，如果用户输入了错误数据，则会显示错误消息。表 7.2 显示了 ASP.NET 验证控件。

## 显示星号

你可以将验证控件的行为设置为许多网站上使用的常见技术。如果用户输入了无效数据或遗漏了必填项，你可以在错误字段旁边显示一个星号，并使实际消息出现在其他位置，例如页面底部。

按上述描述精确设置验证控件的 ErrorMessage 属性，但将其 Text 属性设置为星号（或你想要显示的任何其他字符）。运行时，除非关联控件验证失败，否则控件不会显示任何内容；但当验证失败时，星号会显示在错误字段旁边。ValidationSummary 控件将显示在验证控件的 ErrorMessage 属性中定义的整个消息。

如果使用此技术，请确保你的错误消息具有描述性并标识错误字段。图 7.36 显示了先前的验证示例，已修改为仅在 ValidationSummary 控件中显示错误消息。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_337_0.png)

## 测试有效性

使用验证控件检查有效性不需要任何代码。但有时你可能需要检查单个控件或页面上的所有控件是否已通过验证。每个验证控件都有一个 IsValid 属性，如果分配给验证器的控件通过，则返回 true。此外，Page 对象也有一个 IsValid 属性，当页面上的所有控件都通过验证时，该属性设置为 true。

```
If RequiredFieldValidator1.IsValid Then
    Perform some action.
End If

If Page.IsValid Then
    NavigateHyperlink.Enabled = True
End If
```

## 反馈 7.3

描述如何使用验证控件验证名为 QuantityTextBox 的文本框。需要输入数字，范围为 1 到 100。该字段不能为空。

## Web 应用程序对象

你的 Web 应用程序可以访问服务器对象：Request、Response、Session、Application 和 Server。这些是内在对象，你可以在不创建实例的情况下使用它们。Request 从客户端传递到服务器；Response 从服务器到客户端。

Request 对象保存有关当前用户、用户输入的数据以及 HTTP 请求的参数的信息。你使用 Response 对象创建 cookie 并使用 Request 对象检索它们。你将在本章后面的“Cookies”部分学习如何处理 cookie。

Response 对象将用于呈现页面的 HTML 发送到浏览器。此示例直接将文本插入 HTML 流中：

```
Private Sub Page_Load(ByVal sender As System.Object, _
ByVal e As System.EventArgs Handles MyBase.Load
    Print Hello World on the page.

    Response.Write("Hello World")
End Sub
```

Session 和 Application 对象用于在 ASP.NET 应用程序中存储状态信息。这些对象在后面的“状态管理”部分中介绍。你可以使用 Server 对象的 Transfer 方法导航到另一个 Web 页面。

> TIP
> 链接到目录时包含尾部斜杠 ["http://www.mysite.com/mydirectory/"]；它可节省一次额外的服务器往返。

## 状态管理

正如你所知，传统的 HTML 页面是无状态的，这意味着它们不会保留值。每次在浏览器中呈现 Web 页面时，所有控件都会重新创建。用户输入的任何值，即页面的状态，除非采取措施保留值，否则会丢失。你可能希望在单个页面内保留状态或将信息从一个页面传递到另一个页面。

ASP.NET 通过在往返服务器或导航到另一个页面并返回时维护控件中的值，解决了状态管理的一个问题。所有 EnableViewState 属性设置为 true 的控件中的值都会被加密并存储在隐藏控件的属性中。当页面重新显示时，ViewState 数据会被解密并用于填充控件。如果你查看浏览器中页面的源代码，可以看到隐藏控件的标签，该控件称为 __VIEWSTATE。以下是表单提交到服务器并重新显示的 ViewState 示例。控件名称及其值被压缩并加密为单个字符串，并分配给 Value 属性。

```
<input type="hidden" name="__VIEWSTATE" value="dW5MTQ4nEwM7E7Oz4tUQ/8e/xC31fa3oWMe7CXP+ EAq==" />
```

如果你想维护其他数据，例如保留用户 ID、数据集、对象或属性的值，或在多个表单之间共享的变量，

你将需要实现状态管理。以下各节讨论了一些维护状态的技术，包括在服务器上存储值和在客户端保留值。

## 状态管理技术概述

ASP.NET 有多种用于存储状态信息的工具。维护 .NET Web 应用程序状态的选择包括：

**服务器端**

- *Session 和 Application 对象。* 你可以为这些对象分配值，这些对象在服务器上维护，并在整个应用程序中使用。要使用 Session 对象，用户必须接受 cookie 或你必须修改 Web.config 文件以指定无 cookie 操作。
- *数据库字段。* 你可以将数据写入数据库字段，并在适当时读回。

**客户端**

- *Cookies。* 你可以在内存中创建 cookie 以进行临时存储，或在用户硬盘上创建 cookie 以进行更永久的存储。此技术仅在用户的浏览器设置为接受 cookie 时才有效。
  *注意：* 恶意用户可以查看 cookie。存储可用于查找用户的信息；不要存储敏感用户信息。
- *隐藏字段。* 你可以创建一个隐藏字段并为其分配值；该值在页面提交时传递到服务器，并在页面重新创建时替换到该字段中。
  *注意：* 恶意用户可以查看和修改隐藏字段。不要使用它们来存储敏感信息。
- *附加到 URL 的字符串。* 状态信息可以附加到要导航到的页面的 URL，并由新页面检索。示例：`http://localhost/Ch07Controls/Form1.aspx?user=Robert`。
  *注意：* 恶意用户可以访问查询字符串。不要使用它们来存储敏感信息。
  要在代码中使用查询字符串，请将查询附加到 URL。

```
Server.Transfer("Page2.aspx?answer=" & AnswerTextBox.Text)
```

在第二个页面上，使用 Request 对象的 QueryString 方法和查询字符串的名称。

```
ATextBox.Text = Request.QueryString("answer")
```

- *Web 表单的 ViewState 属性。* 你可以声明键/值对并将其分配给表单的 ViewState；该值可用于后续的页面发布，但不可用于其他页面。
- *控件状态。* 允许你保留控件的属性信息，例如 Tab 控件的当前选项卡。

有关每种方法的优点和缺点的更多详细信息，请参阅 MSDN 中的“ASP.NET State Management Recommendations”。

