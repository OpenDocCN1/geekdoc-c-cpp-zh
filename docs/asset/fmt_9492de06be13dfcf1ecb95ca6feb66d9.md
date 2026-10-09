
## 第 26 章：用户与服务器控件

现在来测试页面并检查带有新增标签属性的 HTML 源代码。图 26-8 显示了控件渲染的 HTML 源代码。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1260_0.png)

你可以看到，你在服务器控件中添加的标签属性现在作为控件渲染的 HTML 标签的一部分包含了。

| 关于控件 ID 的说明 | 注意，在列表 26-11 中，将 `ClientID` 属性作为 `Id Name` 属性的值是非常重要的。派自 `WebControl` 类的控件暴露了三种不同类型的 ID 属性：`ID`、`UniqueID` 和 `ClientID`。这些属性每个都暴露了控件 ID 的略微修改版本，用于特定的场景。 |
`ID` 属性是最直观的。开发者使用它来获取和设置控件的 ID。它在页面设计中必须是唯一的。

`UniqueID` 属性是一个运行时生成的只读属性，它返回一个带有容器控件 ID 前缀的 ID。这非常重要，使得 ASP.NET 可以唯一标识页面树控件中的每个控件，即使该控件被 `Repeater` 或 `GridView` 等容器控件多次使用。例如，如果你将此控件添加到重复器中，`Repeater` 渲染的每个自定义控件的 `UniqueID` 都会修改为包含 `Repeater` 的 ID。

`MyRepeater:Ctrl10:MyCustomControl`

`ClientID` 属性本质与 `UniqueID` 属性相同，但有一个重要的例外。`ClientID` 属性使用下划线 `_` 来分隔 ID 值，而不是使用 `Idseparator` 属性的值。因为 ECMAScript 标准不允许在 ID 属性中使用冒号，而冒号是 `Idseparator` 属性的默认值。使用下划线确保了控件可以被客户端 JavaScript 创建。

此外，为了确保控件能够创建唯一的 ID，它们应该实现 `INamingContainer` 接口。这只是一个标记接口，意味着它不需要实现任何额外的方法；然而，它确保了 ASP.NET 运行时保证无论其容器如何，控件在页面的树层次结构中始终有一个唯一的名称。

## HTML 样式设置

到为止，你已经看到了如何构建一个简单的 HTML 控件并输出包含属性的属性。在本节中，我们将讨论如何控制你的渲染样式信息。正如在本节开头提到的，你正在创建继承自 `WebControl` 类的控件。由于原因，这些控件已经具有用于输出大多数标准 CSS 样式属性的基础设施。在相应的属性生成器中，你应该看到已经列出的许多样式属性，例如背景颜色、边框宽度和字体。你还可以启动样式生成器来创建 CSS 样式。这些基本属性由 `Web-Control` 类提供，但让你的控件在设计时渲染这些值取决于你。要做到这一点，你只需执行 `AddAttributeToRender` 方法。列表 26-16 向你展示了如何操作。

### 26-16：渲染样式属性

```VB
Protected Overrides Sub RenderContents(ByVal output as HtmlTextWriter)
output.RenderBeginTag(HtmlTextWriter.Div)
output.AddAttribute(HtmlTextWriterAttribute.Type, "text")
output.AddAttribute(HtmlTextWriterAttribute.Id, Me.ClientID & "_")
output.AddAttribute(HtmlTextWriterAttribute.Name, Me.ClientID & "_")
output.AddAttribute(HtmlTextWriterAttribute.Value, Me.Text)
output.AddAttributeToRender(output)
output.RenderBeginTag(HtmlTextWriterTag.Input)
output.RenderEndTag()
output.RenderEndTag()
End Sub
```

```csharp
protected override void RenderContents(HtmlTextWriter output)
{
output.RenderBeginTag(HtmlTextWriterTag.Div);
output.AddAttribute(HtmlTextWriterAttribute.Type, "text")
output.AddAttribute(HtmlTextWriterAttribute.Id, this.ClientID + "_id");
output.AddAttribute(HtmlTextWriterAttribute.Name, this.ClientID + "_name");
out.AddAttribute(HtmlTextWriterAttribute.Value, this.Text);
this.AddAttributesToRenderer(output);
output.RenderBeginTag(HtmlTextWriter.Input);
output.RenderEndTag();
output.RenderEndTag();
}
```

执行此方法告诉控件渲染任何已设置的样式属性。

注意，此方法不仅导致样式相关的属性被渲染，还有其他属性，包括 `ID`、`tabindex` 和 `tooltip`。如果你在控件中手动渲染这些属性，可能会导致渲染重复的属性。此外，注意你使用 `AddAttributesToRenderer` 方法的地方。在列表 26-6 中，它在 `Input` 标签渲染之前立即执行，这意味着属性同时在 `Input` 元素和围绕 `Input` 的 `Span` 控件上被渲染。

尝试将调用放在 `DIV` 标签渲染之前，或者在 `DIV` 结束标签渲染之后。你会发现，对于前者，属性被应用到 `DIV` 及其周围的 span；对于后者，`SPAN` 拥有该属性。

使用属性生成器，你可以将背景颜色设置为红色，并将字体设置为粗体。当你设置这些属性时，它们会被自动添加到 ASP.NET 页面上的控件中。添加样式后，控件看起来如下：

```html
<ccl:ServerControl BackColor="Red" Font-Bold=true ID="ServerControl1" runat="server" />
```

样式更改已作为属性持久化到控件中。当你在浏览器中执行此页面时，样式信息会被渲染到 HTML 中，使文本框背景变为红色且字体加粗。图 26-9 显示了浏览器中的页面。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1260_0.png)

## 主题与皮肤

在 ASP.NET 2.0 中添加的一个伟大功能且在第 6 章中介绍过你的是主题和皮肤。此功能允许你为 Web 应用程序创建样式。在本节中，你将在创建服务器控件时了解主题和皮肤。

正如你在第 6 章所看到的，皮肤是设置应用程序中 UI 元素默认值的简单方法。你只需要在 `.skin` 文件中定义控件及其属性，这些值就会应用到控件上。

```vb
Set(ByVal Value As String)
ViewState("Text") = Value
End Set
```

现在，如果开发者尝试在他的皮肤文件定定义此属性，在执行页面时他将收到编译错误。

## 添加客户端功能

渲染和样式 HTML 的能力本身已经非常强大，其他资源也可以发送到客户端，例如客户端脚本、图像和资源。ASP.NET 3.5 了一了一些强大的工具，用于在你的服务器控件中使用客户端脚本，并随着你的控件生成的 HTML 一起将资源检索到客户端。此外，ASP.NET 10 现在包含了一个完整的模型，允许你从你的 Web 页面向服务器发出异步回调。

## 输出客户端脚本

将客户端脚本编写为 VBScript 或 JavaScript 可以让你能够为控件添加强大的客户端功能。客户端脚本语言利用客户端的浏览器进行控制。ASP.NET 1.0 提供了一些简单的方法向浏览器输出客户端脚本，ASP.NET 增强了这些功能，并且现在提供了多种方法来输出客户端脚本，你可以使用这些方法来控制脚本的渲染方式。

如果你已经使用过 ASP.NET 1.0 中的 `Page.RegisterClientScriptBlock` 和 `Page.RegisterStartupScript` 方法来渲染客户端脚本，这些类已经被废弃了。相反，ASP.NET 2.0 现在使用 `ClientManager` 类，你可以通过 `Page.ClientScript` 访问该类。该类暴露了各种静态脚本渲染方法，你可以使用这些方法来渲染客户端脚本。

列表-20 展示了你如何使用 `RegisterStartupScriptMethod` 向客户端渲染 JavaScript。此列表将代码添加到 `OnRender` 方法中，而不是之前示例中使用的 `Render` 方法。此方法允许每个控件通知页面它需要渲染的客户端脚本。在 `Render` 方法被调用后，页面能够渲染它在 `OnPreRender` 方法期间收集的所有客户端脚本。如果你在 `Render` 方法中调用客户端脚本注册方法，在你的客户端脚本渲染之前，页面已经完成了部分渲染。

### 列表 26-20：向浏览器输出客户端脚本

```vb
Protected Overrides Sub OnPreRender(ByVal e As System.EventArgs)
Page.ClientScript.RegisterStartupScript(GetType(), \
"ControlFocus", "document.getElementById("" + Me.ClientID & \
"_i" + "").focus();",", True)
End Sub
```

```csharp
protected override void OnPreRender(EventArgs e)
{
Page.ClientScript.RegisterStartupScript(GetType(),
"ControlFocus", document.getElementById("" + this.ClientID +
"_i" + "").focus();",
true);
}
```

在此列表中，代码输出客户端脚本以便在 Web 页面加载时自动将焦点移动到 `TextBox` 控件。当你使用 `RegisterStartupScript` 方法时，注意它包含一个重载，允许你指定该方法是否渲染脚本标签。如果你正在向页面渲染多个脚本，这会非常有用。

另外请注意，该方法需要一个 `key` 参数。该参数用于唯一标识脚本块；如果你在 Web 页面上注册了多个脚本块，请确保为每个块提供唯一的 `key`。你可以使用 `IsScriptRegistered` 方法和 `key` 来确定特定脚本是否已使用 `RegisterStartupScript` 方法注册到客户端。

当你在浏览器中执行代码时，焦点会自动放置在文本框中。如果你查看 Web 页面的源代码，你会发现 JavaScript 被写在了页面底部，如图 26-11 所示。

如果你想让脚本渲染到页面顶部，请使用 `RegisterClientScriptBlock` 方法，它会在 `<form>` 元素之后立即输出脚本块。

请记住，如果浏览器从上到下解析 Web 页面，如果你在页面顶部输出未包含在函数中的客户端脚本，任何对页面后续 HTML 元素的引用都将失败。因为浏览器尚未解析页面的该部分。

能够渲染页面加载时自动执行的脚本是很棒的，但你可能更根据页面上 HTML 元素的事件来执行代码，例如 `Click`、`Focus` 或 `Blur` 事件。为了实现这一点，你必须在你想要获取事件的 HTML 元素上添加属性。列表 26-21 显示了你如何修改控件的 `Render` 方法来添加此属性。

```html
<!DOCTYPE html PUBLIC "//W3C//DTD HTML 1.0 Transitional//EN"
"http://www.w3.org/TR/html10-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>Hello World</title>
</head>
<body>
<form name="form1" method="post" action="Default.aspx" id="form1">
<div>
<input type="hidden" name="__VIEWSTATE" id="__VIEWSTATE" value="EVPAW3QULTEMv8bZMjNjR85En0cbWDA/ep0d6/qAo/Arp" />
<div>
<input type="text" name="__VIEWSTATE" id="__VIEWSTATE" value="EVPAW3QULTEMv8bZMjNjR85En0cbWDA/ep0d6/qAo/Arp" />
</div>
</div>
</form>
</body>
</html>
```

### 列表 26-21：使用客户端脚本和事件属性

```vb
Protected Overrides Sub OnPreRender(ByVal e as System.EventArgs)
Page.ClientScript.RegisterStartupScript(GetType(), \
"ControlFocus", "document.getElementById("" + Me.ClientID & \
"_i" + "").focus();",", True)
End Sub
```

```csharp
protected override void OnPreRender(EventArgs e)
{
Page.ClientScript.RegisterStartupScript(GetType(),
"ControlFocus", document.getElementById("" + this.ClientID +
"_i" + "").focus();",
true);
}
```

```html
<!DOCTYPE html
//W3C//DTD HTML 4.0 Transitional//EN"
"http://www.w3.org/TR/html4/html4-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>Hello World</title>
</head>
<body>
<form name="form1" method="post" action="Default.aspx" id="form1">
<input type="hidden" name="____VIEWSTATE" id="__VIEWSTATE" value="/EwFAAAAAAAAITXN6QEZgWEoE33AgQ5tS15GbD8/NgQ==" />
</form>
<br />
<span id="ctl02_i">
<input type="text" name="ctl02_i" id="ctl02_i" value="Hello World" />
</span>
<input type="submit" value="Submit" />
</form>
<script type="text/javascript">
window.onload=function() {document.getElementById('ctl02_i').focus();};
</script>
</body>
</html>
```

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1269_0.png)

列表 26-22 显示了你如何修改列表 26-20 中为 TextBox 控件添加的验证；但这次，JavaScript 验证函数存储在外部文件中。
