
文件名 `CallbackNorthwind.aspx.vb` 和 `CallbackNorthwind.aspx.cs`

此代码大部分与上一个示例中使用回调功能的文档相似。主要的区别在于 `RaiseCallbackEvent()` 方法。该方法首先使用通过 `eventArgument` 传递的 `CustomerID` 对 Customers 数据库执行 SELECT 语句。从该 SELECT 语句中检索到的值被作为字符串数组的一部分，最后使用 `String.Join()` 方法进行连接，然后作为 `_callbackresult` 对象的值传递。

有了这些代码，你现在可以使用回调功能填充整个数据表。这意味着无需刷新页面即可填充表格。执行结果如图 2-15 所示。

![](img/7040c21013b8e6c23c612d6da3599ff8_142_0.png)

### 总结

本章向你介绍了 ASP.NET 的核心构建模块之一——服务器控件。服务器控件是一种面向对象的开发方法，将页面元素封装为可修改和扩展的组件。

本章还介绍了如何使用层叠样式表（CSS）来定制服务器控件的外观。在 ASP.NET 中处理 CSS 是简单且快速的，特别是你有 Visual Studio 2010 帮助时。最后，本章查看了使用 HTML 控件以及向页面添加 JavaScript 来修改控件的行为。

## 3 ASP.NET 服务器控件

### 本章内容

- 回顾关键服务器控件
- 区分服务器控件功能
- 从集合中移除项

在两种类型的服务器控件（HTML 控件和服务器控件）中，后者被认为更强大、更灵活。本章查看了在应用程序中使用 HTML 控件。HTML 控件允许你从服务器端代码操作 HTML 元素。另一方面，服务器控件之所以强大是因为它们没有显式绑定到特定的 HTML 元素；而是对应你想要生成的特定功能。正如你在本章中所看到的，取决于你使用的设备，服务器控件可以非常简单，也可以非常复杂。

大量控件的目的是让你工作更高效。在过去，某些高级功能是难以实现的。例如，在早期的 ASP.NET 时代，网站上使用的控件很少。随着 ASP.NET 1.0 引入日历服务器控件，在站点上创建日历变成了一项易举的任务；在 ASP.NET 1.x 中创建图像是另一项困难的任务，但在 ASP.NET 2.0 中作为新的服务器控件引入。随着 ASP.NET 版本的演进，不断添加新控件来帮助开发者。

本章介绍了了一些可用的服务器控件。本章的第一部分关注 ASP.NET 诞生以来存在的服务器控件。然后探讨了 ASP.NET 最初发布后引入的服务器控件。本章没有讨论所有可能的控件，因为某些服务器控件在其他章节中介绍过，它们与特定主题更相关。

## 服务器控件概述

服务器控件是 ASP.NET 中最常用的组件。虽然你可能在上一章中看到了 HTML 控件的许多用途，但服务器控件在能力上更高。当你使用它们时，更高层次的功能变得更加明显。

### 第 3 章 ASP.NET 服务器控件

ASP.NET 提供的 HTML 控件的工作方式是映射到特定的 HTML 元素。你通过 HTML 元素提供的属性来控制输出。这些属性在最终输出到客户端之前可以在服务器端进行更改。这其中包含很大的力量，当你使用服务器控件时，拥有许多简单没有的能力。

服务器控件的工作方式不同。它们不映射到特定的 HTML 元素，而是通过 HTML 元素集合为你定义功能、能力和外观。当你构建由服务器控件组成的 Web 页面时，你是在描述页面的功能、外观和行为。ASP.NET 如何输出这种结构。当然，输出取决于客户端请求的能力。由于每个请求可能需要不同的 HTML 输出，ASP.NET 负责浏览器控件及其相关工作。

与 HTML 不同，服务器控件不仅用于常见的 Web 表单元素（如文本和按钮），还可以为你的页面带来高级功能。例如，Web 应用程序的一个常见功能是日历。没有任何 HTML 元素可以在你的表单上放置日历，但 ASP.NET 的服务器控件可以为你的应用程序提供完整的日历。在 Web 页面上添加日历并不是一项简单的任务。在过去的 ASP.NET 中非常简单，只需一行代码即可实现！

记住，当你构建服务器控件时，你实际上是在构建一个用于服务器（而不是客户端）的指令集。ASP.NET 提供的所有服务器控件都使用控件声明。以下是一个典型的服务器控件：

```
<asp:Label ID="Label1" runat="server" Text="Hello World"/></asp:Label>
```

像 HTML 服务器控件一样，服务器控件需要一个 `ID` 属性在服务器端代码中引用控件，并且对于基于 XML 的元素，需要使用 XML 语法正确打开和关闭服务器控件。在前面的示例中，你可以使用`<asp:Label>` 控件，它关联有一个`</asp:Label>` 元素。你也可以使用以下语法关闭该元素：

```
<asp:Label ID="Label1" runat="server" Text="Hello World" />
```

本章其余部分将检查为你提供的所有服务器控件。

### Label 服务器控件

Label 控件用于在浏览器中显示文本。因为这是服务器控件，你可以从服务器端代码动态更改文本。正如你从前面的`<asp:Label>` 控件示例中所看到的，控件使用 `Text` 属性来分配控件的内容，如下所示：

与其使用 `Text` 属性，你可以将显示的内容放置 `<asp:Label>` 元素之间，如下：

```
<asp:Label ID="Label1" runat="server">Hello World</asp:Label>
```

你还可以通过程序化手段为控件提供内容。

#### Label 服务器控件

Label 服务器控件一直是一个仅显示文本的控件。自 ASP.NET 2.0 以来，它获得了一些额外功能。该框架版本的一个重大变化是，你现在可以在热键功能（也称为加速键）中使用项。这使得页面可以聚焦到你通过声明式分配给特定热键的控件上（例如，使用 Alt+N 聚焦到页面上的第一个框）。

热键是用户在页面上启动操作的快速方式。例如，如果你使用 Microsoft Internet Explorer，可以按 Ctrl+N 打开一个新的 IE 实例。热键在胖客户端应用程序（Windows Forms）中一直很常见，现在可以在 ASP.NET 中使用它们。列表 3-2 显示了如何将热键功能用于表单上的两个框的示例。

列表 3-2：使用 Label 服务器控件提供热键功能

```xml
<%@ Language="VB" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Label Server Control</title>
</head>
<body>
<form id="form" runat="server">
<asp:Label ID="Label1" runat="server" AccessKey="N"><u>Username</u></asp:Label>
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
<br>
<asp:Label ID="Label2" runat="server" AccessKey="P"><u>Password</u></asp:Label>
<asp:TextBox ID="TextBox2" runat="server"></asp:TextBox>
<br>
<asp:Button ID="Button1" runat="server" Text="Submit" />
</form>
</body>
</html>
```

热键通过 `AccessKey` 属性分配。在这种情况下，Label1 使用 N，Label2 使用 P。Label 的第二个属性是 `AssociatedControlID`。放置于此处的字符串（String）值将 Label 控件与页面上的另一个服务器控件关联起来。该值必须是其他控件之一。如果不是，页面在调用时将向你返回错误。

设置这些控件后，当在浏览器中调用页面时，你可以按 Alt+N 或 Alt+P 自动聚焦到表单中的特定文本框。在图 3-1 中，HTML 声明的下划线表示需要配合 Alt 键按下的字母，以便聚焦到相邻的控件。这不是强制要求的，但我们强烈建议这样做，因为这是用户在使用热键时的预期行为。在这个示例中，Username 中的字母 n 和 Password 中的字母 P 加了下划线。

![](img/7040c21013b8e6c23c612d6da3599ff8_146_0.png)

图 3-1

### 第 3 章 ASP.NET Web 服务器控件

在处理键时，请注意所有字母都可配合 Alt 键使用，Microsoft Internet Explorer 使用 Alt+F, E, V, I, O, T, A, W 和 H。如果你使用了这些任何字母，IE 的操作将优于你在页面上放置的任何操作。

### Literal 服务器控件

Literal 控件的工作方式与 Label 服务器控件非常相似。该控件在过去一直用于你想要输出到浏览器但在（字面状态）下保持不变的文本。Label 控件通过在文本周围放置 `<span>` 元素来控制输出，如下：

```html
<span id="Label">Here is some text</span>
```

Literal 控件输出不带 `<span>` 元素的文本。该服务器控件的一个功能是属性模式（Attribute Mode）。此属性允许你指定分配给控件的文本如何被 ASP.NET 引擎解释。

如果你在输出的字符串中放置一些 HTML（例如，`<b>Here is some text</b>`），Literal 控件将仅输出内容，消费者将以粗体显示文本：

Here is some text

尝试使用此处所示的 `Mode` 属性：

```xml
<asp:Literal ID="Literal" runat="server" Mode="Encode">
  <b>Here is some text</b>
</asp:Literal>
```

添加 `Mode="Encode"` 会在输出被应用程序接收之前对其进行编码：

现在，文本不再被转换为粗体字体，而是显示 `<b>` 元素：

<b>Here is some text</b>

如果你想在应用程序中显示代码，这种处理方式是理想的。`Mode` 属性的其他值 `PassThrough` 和 `Transform` 取决于消费者并包含或移除元素。例如，并非所有设备都接受 HTML 元素，如果 `Mode` 属性的值设置为 `Transform`，则这些元素在发送给消费者之前会从字符串中移除。

`Mode` 属性的值为 `PassThrough` 意味着文本发送给消费者时未对字符串进行任何更改。

### TextBox 服务器控件

Web 页面的主要功能之一是提供用户可以使用其提交信息进行收集的表单。TextBox 服务器控件是空间中最常用的控件之一。正如名称所示，该控件在表单上提供了一个文本框，使用户输入文本。你可以将 TextBox 映射到表单中三个不同的 HTML 元素。

首先，TextBox 可以用作标准的 HTML 文本框，如下所示所示：

```xml
<asp:TextBox ID="TextBox" runat="server"></asp:TextBox>
```

此代码在表单上创建一个文本框，看起来类似于图 3-2 所示的。

![](img/7040c21013b8e6c23c612d6da3599ff8_147_0.png)

其次，TextBox 可以用作标准的 HTML 文本框，如下所示所示：

```xml
<asp:TextBox ID="TextBox" runat="server"></asp:TextBox>
```

此代码在表单上创建一个文本框，看起来类似于图 3-2 所示的。

第三次，TextBox 可以用作标准的 HTML 文本框，如下所示所示：

```xml
<asp:TextBox ID="TextBox" runat="server"></asp:TextBox>
```

此代码在表单上创建一个文本框，看起来类似于图 3-2 所示的。

#### 使用 Focus() 方法

由于 TextBox 服务器控件派自 WebControl 的基类，它可用的方法之一是 `Focus()`。`Focus()` 方法允许你动态将用户的光标放在适当的元素中（不是所有的，而是派自 WebControl 的服务器控件）。通过它，可以正确地配合 TextBox 控件使用，如 3-3 所示。

3-3：与 TextBox 控件配合 Focus()

```vb
Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    TextBox.Focus()
End Sub
```

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    TextBox.Focus();
}
```

#### 使用 AutoPostBack

ASP.NET 以事件驱动的方式工作。当 Web 页上的操作触发事件时，会启动服务器端代码。最常见的事件之一是最终用户点击表单上的按钮。如果你在 Visual Studio 2010 的设计视图中双击按钮，你可以看到带有 `Button_Click` 事件结构的代码。这是 TextBox 控件的事件。双击 TextBox 会构造 `OnTextChanged` 事件。当最终用户将焦点移到文本框之外，或者在文本框中输入内容后点击页面上的其他元素时，或者只需通过 Tab 键离开文本框时，就会触发此事件。该事件的使用见列表 3-4。

```xml
<% Page Language="VB" %>
```

```xml
<script runat="server">
```

![](img/7040c21013b8e6c23c612d6da3599ff8_148_0.png)

图 3-4

### 第 3 章 ASP.NET WEB 服务器控件

列表 3-4（续）

```vb
Protected Sub TextBox1_TextChanged(ByVal sender As Object,
ByVal e As System.EventArgs)
    Response.Write("OnTextChanged event triggered")
End Sub
```

```vb
Protected Sub Button1_Click(ByVal sender As Object,
ByVal e As System.EventArgs)
    Response.Write("OnClick event triggered")
End Sub
```

```html
</script>
```

```html
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>OnTextChanged 页面</title>
</head>
<body>
    <form id="form" runat="server">
        <div>
            <asp:TextBox id="TextBox1" runat="server" AutoPostBack="True"
OnTextChanged="TextBox1_TextChanged"></asp:TextBox>
            <asp:Button id="Button1" runat="server" Text="Button"
OnClick="Button1_Click" />
        </div>
    </form>
</body>
</html>
```

```csharp
<%@ Page Language="C#">
<script runat="server">
protected void TextBox1_TextChanged(object sender, EventArgs e)
{
    Response.Write("OnTextChanged event triggered");
}
protected void Button1_Click(object sender, EventArgs e)
{
    Response.Write("OnClick event triggered")
}
</script>
```
