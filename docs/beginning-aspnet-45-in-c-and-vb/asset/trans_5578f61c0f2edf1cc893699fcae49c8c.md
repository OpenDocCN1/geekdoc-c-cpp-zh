
## 容器控件

经常希望将相关内容和控件分组。你可以通过将控件（和其他标记）放在其中一个容器控件中来实现这一点，例如 Panel、PlaceHolder、MultiView 或 Wizard。例如，你可以使用 PlaceHolder 或 Panel 控件一次隐藏或显示多个控件。不是分别隐藏每个控件，你只需隐藏包含所有单个控件和标记的整个容器。这两个控件各有优缺点。PlaceHolder 控件的好处是它不会向页面输出自己的 HTML，因此你可以在最终页面中没有任何副作用的情况下将其用作容器。然而，它缺乏设计时支持，使得在 VS 中设计时难以管理 PlaceHolder 内部的控件。相比之下，Panel 使你能够轻松访问其包含的所有控件和其他内容，但它本身会渲染为一个 <div> 元素。在许多情况下这不是问题，甚至可能很有用，因为你可以在客户端使用 CSS 定位该 <div>，因此通常最好使用 Panel 控件，因为它具有设计时支持。

MultiView（可以包含一个或多个 <asp:View> 元素）和 Wizard 在能够将长页面拆分为多个区域方面类似，例如使填写长表单变得容易。Wizard 内置了使用 Previous、Next 和 Finish 按钮在页面之间移动的支持，而 MultiView 必须通过编程控制。

## 更深入地了解 Panel 控件

在下面的练习中，你使用 Panel 控件为其他控件和标记创建容器。现在你只添加一些文本，但在随后的 Try It Out 练习中你会向面板添加 ASP.NET 控件。

## 试一试 使用 Panel 控件

在本练习中，你将了解如何使用 Panel 控件作为一些简单文本的容器。此外，你使用 CheckBox 在服务器上控制 Panel 的可见性。

- 1. 首先在 Demos 文件夹中创建一个名为 Containers.aspx 的带代码隐藏的新 Web 窗体。
- 2. 将页面切换到设计视图，并从工具箱将 CheckBox 和 Panel 控件拖到设计表面中的虚线 <div> 元素上。
- 3. 通过将 Text 属性设置为 Show Panel 为 CheckBox 控件提供有意义的描述，并使用属性网格将 AutoPostBack 属性设置为 True。不要从属性的下拉列表中选择 True，你也可以双击 AutoPostBack 属性或其值在 False 和 True 之间切换。
- 4. 使用属性网格将 Panel 控件的 Visible 属性设置为 False。这会在页面首次加载时隐藏 Panel 控件。
- 5. 在 Panel 控件内部，键入一些文本（例如，I am visible now）。请注意，面板的行为与 VS 设计表面的其余部分相同。你可以简单地向其中添加文本、选择和格式化它，并通过从工具箱拖动来向其中添加新控件。面板的代码在标记视图中应如下所示：

```
<asp:Panel ID="Panel1" runat="server" Visible="False">
    I am visible now
</asp:Panel>
```

请注意，如果你使用 VB.NET，使用标记视图和设计视图添加处理程序之间存在细微差别。如果你使用标记视图，处理程序会添加到标记中（OnCheckedChanged="CheckBox1_CheckedChanged"），并且代码会添加到代码隐藏中。当你使用设计视图时，标记视图中的代码不受影响，而代码隐藏中的代码会用 Handles 关键字进行注释，以指示代码响应的事件（例如按钮的单击、复选框的检查更改事件等）。但是在运行时，两者没有区别。

7. 接下来，在 VS 为你添加的处理程序代码中添加以下加粗的行：

```
VB.NET
Protected Sub CheckBox1_CheckedChanged(sender As Object, e As EventArgs)
    Panel1.Visible = CheckBox1.Checked
End Sub
```

```
C#
protected void CheckBox1_CheckedChanged(object sender, EventArgs e)
{
    Panel1.Visible = CheckBox1.Checked;
}
```

8. 保存所有更改，然后按 Ctrl+F5 在浏览器中请求页面。

9. 页面首次加载时，你只能看到复选框及其旁边的文本。当你在浏览器中查看页面的 HTML 时（右键单击页面并根据浏览器选择查看源代码或查看页面源），你只能看到复选框；在此时没有 Panel 控件的代码发送到浏览器。当你单击复选框在其上放置复选标记时，页面会重新加载，现在会显示你在步骤 5 中输入的文本。

> **警告** *如果没有任何反应，请返回 VS 中的页面源并确保 CheckBox 控件的 AutoPostBack 设置为 True。*

如果你在浏览器中查看 HTML，你会看到你在步骤 5 中键入的文本被包裹在一个 id 为 Panel1 的 <div> 元素中：

```
<div id="Panel1">
    I am visible now
</div>
```

## 其工作原理

在本练习的步骤 4 中，你将 Panel 控件的 Visible 属性设置为 False。这意味着当页面加载时，控件在服务器上不可见，因此其 HTML 永远不会到达浏览器。

当你然后选中复选框时，会发生回发，将表单中包含的信息发送到服务器。在服务器上，会运行一些代码，每当复选框从选中更改为未选中或反之时就会触发。在该代码块内部，会执行以下代码（以 C# 显示）：

```
Panel1.Visible = CheckBox1.Checked;
```

这意味着 Panel 仅在复选框被选中时可见。当未选中时，Panel 会自动隐藏。

如你所见，在 VS 中向 Panel 控件添加文本和其他标记很容易。现在你只添加了一些纯文本，但在下一节中你将了解如何添加 Wizard 控件以及如何使用它。

## 使用 Wizard 控件的魔力

Wizard 控件是拆分大型 Web 窗体并以小块信息形式向用户呈现的绝佳工具。不是用一个包含许多控件和文本的页面让用户感到困惑，你可以拆分页面并在单独的向导页面上呈现每个部分。然后 Wizard 控件通过自动创建 Next、Previous 和 Finish 按钮来处理所有导航问题。在下面的练习中，你使用向导询问用户她的姓名和最喜欢的编程语言。虽然示例本身相当简单，你本可以在同一页面上放置两个问题而不会让用户感到困惑，但示例展示了向导的工作原理以及其有用性。你可以轻松地将相同的技术应用于你自己的、可能更大的 Web 窗体。

## 试一试 使用向导创建易于使用的表单

在本 Try It Out 中，你将一个 Wizard 放置在上一练习中创建的面板内，使用户能够填写跨越几个页面的表单。向导将有两个步骤供用户输入详细信息，以及一个显示用户提供的数据的结果页面。

- 1. 确保 Containers.aspx 页面仍在设计视图中打开。删除你在上一个 Try It Out 中输入的文本 "I am visible now"，然后从工具箱将 Wizard 控件拖到 Panel 内部。将其右边缘向右拖动，进一步增加控件的总宽度至 500px。现在你的页面看起来类似于图 4-11。
- 2. 打开 Wizard 的 Smart Tasks 面板（单击其右上角的箭头）并选择 Add/Remove WizardSteps。在随后的对话框中，单击 Add 按钮插入第三个向导步骤，如图 4-12 所示。

![](img/eadab2ccd79b253c01a3fdff2321202d_171_0.png)

FinishButtonClick 在 Action 类别中。使用这两种方法，你应该得到一些 Wizard1_FinishButtonClick 的代码，你需要用以下代码扩展它：

### VB.NET

```vbnet
Protected Sub Wizard1_FinishButtonClick(sender As Object,
    e As WizardNavigationEventArgs) Handles Wizard1.FinishButtonClick
    Result.Text = "Your name is " & YourName.Text
    Result.Text &= "<br />Your favorite language is " &
        FavoriteLanguage.SelectedValue
End Sub
```

### C#

```csharp
protected void Wizard1_FinishButtonClick(object sender,
    WizardNavigationEventArgs e)
{
    Result.Text = "Your name is " + YourName.Text;
    Result.Text += "<br />Your favorite language is " +
        FavoriteLanguage.SelectedValue;
}
```

9. 切回设计视图并打开 Wizard 的属性网格，确保其 ActiveStepIndex 设置为 0。设计器会记住你设计的最后一步，并在标记视图中将该值存储在 Wizard 的 ActiveStepIndex 中。为了确保 Wizard 从第一页开始，你在保存更改并运行页面之前应始终将 ActiveStepIndex 重新设置为 0（或在设计视图中单击 Wizard 控件中的第一步）。

10. 保存所有更改，关闭所有打开的浏览器窗口，然后按 Ctrl+F5 在浏览器中打开页面。选择复选框使 Panel 可见，并在第一个向导页面上输入你的姓名。单击 Next 并选择你最喜欢的编程语言。注意现在有一个 Previous 按钮可用，可让你返回向导的第一步以更改姓名。除了单击 Next 和 Previous 按钮外，你也可以单击浏览器中向导左侧的链接。当你单击 Finish 按钮时，你将看到你在向导中输入的信息结果（见图 4-15）。

![](img/eadab2ccd79b253c01a3fdff2321202d_174_0.png)

图 4-15
