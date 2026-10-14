

## 使用 OnClick 属性处理单击事件的代码

## 按钮控件的 asp 标签

```
<asp:Button id="btnCancel" runat="server" Text="Cancel Order"
    OnClick="btnCancel_Click" />
```

## 控件单击事件的事件处理程序

```
protected void btnCancel_Click(object sender, EventArgs e)
{
    Session.Remove("Cart");
    Response.Redirect("Order.aspx");
}
```

## 使用相同事件处理程序的两个按钮控件的 asp 标签

```
<asp:Button id="btnPrevious" runat="server" Text="Previous"
    OnClick="NavigationButtons_Click" />
<asp:Button id="btnNext" runat="server" Text="Next"
    OnClick="NavigationButtons_Click" />
```

## 常用控件事件

| 事件 | 属性 | 控件 |
|---|---|---|
| Click | OnClick | Button, image button, link button, image map |
| Command | OnCommand | Button, image button, link button |
| TextChanged | OnTextChanged | Text box |
| SelectedIndexChanged | OnSelectedIndexChanged | Drop-down list, list box, radio button list, check box list |
| CheckedChanged | OnCheckedChanged | Check box, radio button |

## 描述

- *事件处理程序* 是在指定事件发生时被调用的方法。事件处理程序必须声明为 public 或 protected 范围。
- 要将事件绑定到事件处理程序，您需要在控件的相应事件属性中命名该处理程序。例如，您可以使用 OnClick 属性来命名在用户单击控件时执行的事件处理程序。
- 一个事件处理程序可以处理多个事件。要做到这一点，您需要在每个想要其处理的控件的每个事件属性上命名该处理程序。

## 如何使用访问键与 Web 服务器控件

访问键允许用户使用键盘快捷键选择控件。例如，如果您将 F 指定为接受客户名字输入字段的访问键，用户可以通过按 Alt+F 直接将焦点移动到该字段。图 6-4 显示了如何使用访问键与 ASP.NET。

要创建访问键，您只需将 AccessKey 属性添加到要创建键盘快捷键的控件。由于此属性由 System.Web.UI.WebControls.WebControl 类定义，因此您可以使用它与任何 Web 控件。需要注意的是，您为表单定义的访问键可能会与浏览器定义的访问键冲突。因此，您需要确保使用所有现代浏览器对其进行测试。

当您使用访问键与文本框和其他由文字标识的控件时，通常会在文字中下划线标出访问键。要做到这一点，您可以使用带有 class 属性的 Span 元素。这在图中的文本中有所说明，该文本标识了两个文本框。在这里，class 属性的值为“accesskey”。然后，您可以为此类编写样式规则，将 text-decoration 属性设置为 underline。

如果您使用标签而不是文字来标识控件，您可以将访问键分配给标签，然后下划线标出标签的相应字母。在这种情况下，您还应编码 AssociatedControlID 属性，以指定当用户使用访问键时应接收焦点的控件。

您也可以为按钮控件指定访问键，如本图中的 aspx 代码所示。但是，您不能在按钮控件中下划线标出访问键。这是因为按钮使用 <input type="submit"> HTML 元素呈现，而该元素不提供格式化按钮上显示的文本的方法。

## 如何将焦点设置到 Web 服务器控件上

ASP.NET 提供了两个功能，让您可以将焦点设置到表单上的特定控件。首先，您可以使用表单的 DefaultFocus 属性来确定页面首次显示时哪个控件接收焦点。例如，在图 6-4 中，此属性设置为 txtName 控件。

其次，您可以在运行时将焦点移动到控件。要做到这一点，您使用控件的 Focus 方法。例如，本图中显示的语句将焦点移动到 txtEmail 控件。

## 如何设置默认按钮控件

ASP.NET 还允许您设置按 Enter 键时默认激活的按钮。要做到这一点，您设置表单的 DefaultButton 属性。在本图中的示例中，此属性设置为 btnNext 按钮。因此，当按下 Enter 键时，表单会发布回服务器，并执行下一个按钮的 Click 事件的方法。

## 使用访问键以及默认焦点和按钮属性的表单

![](img/c024ccf88e28c30c07dd410d4342288f_234_0.png)

## 表单的 aspx 代码

```
<form id="form1" runat="server" defaultfocus="txtName" defaultbutton="btnNext">
<div id="page">
<p>Please enter your contact information:</p>
<p class="text"><span class="accesskey">N</span>ame:</p>
<p class="entry"><asp:TextBox ID="txtName" runat="server" AccessKey="N"></asp:TextBox></p>
<p class="text"><span class="accesskey">E</span>mail:</p>
<p class="entry"><asp:TextBox ID="txtEmail" runat="server" AccessKey="E"></asp:TextBox></p>
<p id="buttons">
<asp:Button ID="btnPrevious" runat="server" AccessKey="P" Text="Previous" />&nbsp;
<asp:Button ID="btnNext" runat="server" AccessKey="N" Text="Next" />
</p>
</div>
</form>
```

## accesskey 类的 CSS

```
.accesskey
{
    text-decoration: underline;
}
```

## 将焦点移动到控件的语句

```
txtEmail.Focus;
```

## 描述

- 您可以在 Web 服务器控件上使用 AccessKey 属性为控件指定键盘快捷键。要使用键盘快捷键，用户按住 Alt 键并按下访问键以将焦点移动到控件。
- 如果您使用文字来标识另一个控件，您可以通过在文字中下划线标出该控件使用的访问键的相应字母来标识它，如上所示。
- 如果您使用标签来标识另一个控件，您可以为标签设置 AccessKey 属性，然后将 AssociatedControlID 属性设置为另一个控件。当用户按下标签的访问键时，焦点将被移动到关联的控件。
- 您可以使用表单的 DefaultFocus 属性设置表单首次显示时接收焦点的控件。要在运行时将焦点移动到控件，请使用控件的 Focus 方法。
- 您可以使用表单的 DefaultButton 属性设置按 Enter 键时导致表单发布回的按钮。

## 如何使用按钮控件

大多数 Web 表单至少有一个用户可以单击以将表单提交到服务器进行处理的按钮控件，通常称为提交按钮。在接下来的主题中，您将学习如何使用 ASP.NET 提供的三种按钮控件：按钮、链接按钮和图像按钮。

## 如何使用按钮、链接按钮和图像按钮

图 6-5 展示了三种按钮控件。这些控件仅在向用户显示的方式上有所不同。这由本图顶部显示的三个按钮所说明。如您所见，按钮在矩形区域内显示文本。链接按钮显示看起来像超链接的文本。而图像按钮显示图像。

本图还展示了所说明的三个按钮的 asp 标签。对于按钮和链接按钮，Text 属性提供控件显示的文本。对于图像按钮，ImageUrl 属性提供按钮上显示的图像的 URL 地址。在某些情况下，浏览器可能无法显示图像。因此，您还应编码 AlternateText 属性，以便在浏览器无法显示图像时提供显示的文本。

当用户单击其中一个按钮控件时，ASP.NET 会引发两个事件：Click 和 Command。您可以在本图中看到按钮控件 Click 事件的事件处理程序。请注意，此事件处理程序接收两个参数。sender 参数表示被单击的控件。由于此参数的类型为 object，如果您想访问控件的属性和方法，则需要将其转换为按钮控件。例如，如果您编写一个处理多个按钮的处理方法，您可能希望这样做。然后，您可以使用控件的 ID 属性来确定单击了哪个按钮。然而，更简单的方法是使用 Command 事件。您将在图 6-7 中了解如何使用此事件。

传递给 Click 事件的事件处理程序的第二个参数 e 包含特定于事件的信息。您最有可能使用此参数与图像按钮控件，以确定用户在图像上单击的位置。您将在下一图中了解更多相关信息。

当然，Click 和 Command 事件处理程序仅在页面发布回自身时执行。但是，如果为 PostBackUrl 属性指定了值，则会执行并显示指定 URL 处的页面。这是您在第 3 章中了解的跨页发布功能。

顺便说一下，从本章及本书的这一点开始，图表通常会展示所使用的控件的 asp 元素。通过研究这些控件的代码，您可以快速了解其属性是如何设置的。请记住，通常您通过使用设计器将控件添加到表单，并通过使用属性窗口设置控件的属性。然后，aspx 文件中 asp 元素的代码会自动生成。

