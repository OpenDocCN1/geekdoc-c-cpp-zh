
虽然这个选择很好，但 VS 做的事情更有用；当你按 `Tab` 时，它还在 Code Behind 中为你添加了处理程序代码。要查看该代码，请按 `F7` 切换到 Code。

## 第4章 使用 ASP.NET 服务器控件

> 注意 使用此功能后，无需切换到设计视图并通过双击控件（像你在之前的练习中所做的那样）或使用属性网格的事件选项卡（稍后会看到）来设置处理程序的需求已大大减少。它非常适合喜欢手工编码设计视图的人，并且在设计视图根本不实用的更复杂页面中尤其有用。

请注意，如果你使用的是 `VB.NET`，通过标记视图和设计视图添加处理程序之间存在细微差别。如果你使用标记处理程序，处理程序会添加到标记中（`OnChange="Checkbox1_CheckedChanged"`），代码会添加到代码后置中。当你使用设计视图时，标记中的代码不受影响，后置中的代码会用 `Handles` 关键字进行注释，以指示代码响应的事件（例如按钮的单击、复选框的更改事件等）。但是在运行时，两者没有区别。

- 7. 接下来，在 VS 为你添加的处理程序代码内添加以下行：

### VB.NET

```
Protected Sub Checkbox1_CheckedChanged(sender As Object, e As EventArgs)
    Panel.Visible = Checkbox1.Checked
End Sub
```

### C#

```
protected void Checkbox1_CheckedChanged(object sender, EventArgs e)
{
    Panel.Visible = Checkbox1.Checked;
}
```

- 8. 保存所有更改并通过按 `Ctrl+F5` 在浏览器中请求页面。

- 9. 当页面首次加载时，你会看到复选框及其旁边的文本。当你在浏览器中查看页面的 HTML 时（右键单击页面并根据浏览器选择查看源代码或查看页面源代码），你只能看到复选框；此时面板控件的代码尚未发送到浏览器。当你单击复选框在其上放置复选标记时，页面会重新加载并显示你在步骤 5 中输入的文本。

> 警告 如果出现任何问题，请返回 VS 中的页面源代码并确保 `CheckBox` 控件上的 `AutoPostBack` 为 `True`。

如果你查看浏览器中的 HTML，你会看到你在步骤 5 中输入的文本被包裹在一个 id 为 `Panel1` 的 `<div>` 中：

```
<div id="Panel1">
    I am visible now
</div>
```

## 其工作原理

在本练习的步骤 4 中，你将面板控件的 `Visible` 属性设置为 `False`。这意味着当页面加载时，控件在服务器上不可见，因此其 HTML 永远不会到达浏览器。当你然后选中复选框时，会发生回发，将表单中包含的信息发送到服务器。在服务器上，会运行一段代码，该代码会在复选框的状态从选中变为未选中或相反时触发。在该代码块内部，会执行以下代码（以 C# 显示）：

```
Panel.Visible = CheckBox1.Checked;
```

这意味着面板只有在复选框被选中时才可见。如果未选中，面板会自动隐藏。

正如你所见，在 VS 中向面板控件添加文本和其他标记很容易。现在，你只添加了一些纯文本，但在下一节中你将看到如何添加向导控件以及如何使用它。

## 使用向导控件的魔力

向导控件是分解大型 Web 窗体并将其作为信息的小块呈现的绝佳工具。与用一个包含许多控件的页面让用户感到困惑相比，你可以分解页面并在单独的页面上呈现每个部分。向导控件然后通过自动创建下一步、上一步和完成按钮来处理导航问题。在本练习中，你使用向导为她创建一个用户及其最喜欢的编程语言。虽然示例本身很简单，你本可以将两个问题放在同一页面上而不会让用户感到困惑，但示例展示了向导的工作原理以及其有用性。你可以轻松地将相同的技术应用于你自己的、可能更大的 Web 窗体。

## 试用 使用向导创建易于使用的窗体

在本试用中，你将在上一练习中创建的面板内放置一个向导，使用户能够填写跨越几个页面的窗体。向导将有两个步骤供用户输入详细信息，以及一个显示用户提供的数据的结果页面。

- 1. 确保 `Containers.aspx` 页面仍在设计视图中打开。删除你在上一个试用中输入的“我现在可见”，并从工具箱中将向导控件拖到面板内。将其右边缘向右拖动更多，使控件的总宽度增加到 `500px`。你的页面现在看起来类似于图 4-11。

![](img/9e033e3b9560597824f8b22941d6d8bb_154_0.png)

图 4-11

## 118 | 第4章 使用 ASP.NET 服务器控件

- 2. 打开向导的智能任务面板（单击其右上角的箭头）并选择添加/删除向导步骤。在随后出现的对话框中，单击添加按钮插入第三个向导步骤，如图 4-12 所示。

![](img/9e033e3b9560597824f8b22941d6d8bb_155_0.png)

图 4-12

- 3. 在左侧的成员列表中单击第一个标记为步骤 1 的 `WizardStep`，并将其标题从步骤 1 改为关于你。将另外两个步骤的标题分别设置为最喜欢的语言和准备就绪。

- 4. 将第二个步骤（现标记为最喜欢的语言）的 `StepType` 改为 `Finish`，最后一个步骤改为 `Complete`。你可以让第一个步骤的 `StepType` 保持为 `Auto`。单击确定关闭向导步骤集合编辑器。

- 5. 在设计中，单击左侧列表中的关于你使其处于活动状态，并将标签和文本框拖到向导的右侧。你需要将它们拖到向导右上角的灰色矩形内，否则控件不会最终位于向导内。将标签的文本属性设置为输入你的姓名并将文本框的 ID 更改为 `YourName`。完成后，你的向导看起来像图 4-13。

![](img/9e033e3b9560597824f8b22941d6d8bb_155_1.png)

图 4-13

- 6. 在左侧的列表中单击最喜欢的语言项使其处于活动状态。将 `DropDownList` 添加到向导步骤右侧带灰色边框的矩形中。通过将其 ID 设置为 `FavoriteLanguage` 重命名 `DropDownList`。打开 `DropDownList` 控件的智能任务面板并选择编辑项目。添加你在之前的试用中添加的三个项目，分别为 C#、Visual Basic 和 CSS。如果你愿意，可以从页面 `ListControls.aspx` 复制这三个项目并粘贴在第二个步骤内部的 `<asp:DropDownList>` 标签之间。你应该最终得到以下第二个步骤的代码：

```
</asp:WizardStep>
<asp:WizardStep runat="server" Title="Favorite Language" StepType="Finish">
<asp:DropDownList ID="FavoriteLanguage" runat="server">
<asp:ListItem Text="C#" </asp:ListItem>
<asp:ListItem Text="Visual Basic" </asp:ListItem>
<asp:ListItem Text="CSS" </asp:ListItem>
</asp:DropDownList>
</asp:WizardStep>
<asp:WizardStep runat="server" StepType="Complete" Title="Ready">
```

## 控件类型 | 19

- 7. 对于最后一步，使用标记视图。如果你想在设计中切换到该步骤，你可能会注意到向导消失了。如果发生这种情况，请切换到标记视图并将向导控件的 `ActiveStepIndex` 设置为 `0`。

在标记为结果的 `WizardStep` 内部，从工具箱拖动一个标签并通过设置其 ID 为 `Result` 重命名它。或者，使用最后一步的代码，键入标签和标签。然后按 `F4` 编辑插入的代码片段

- 8. 在设计视图中双击向导并添加以下代码，该代码将在用户单击向导最后一步的完成按钮时执行。如果遇到问题，VS 可以为你创建正确的代码，如下一个代码片段所示，选择向导，按 `F4` 打开控件的属性网格，并单击属性网格工具栏中带闪电图标的按钮（从左数第四个按钮），并参见图 4-14。

![](img/9e033e3b9560597824f8b22941d6d8bb_156_0.png)

属性网格的这一部分通常被称为属性网格的事件选项卡。在操作类别中定位并双击 `FinishButtonClick`。通过哪种方法，你应该最终得到一些 `Wizard1_FinishButtonClick` 的代码，你需要用以下代码扩展它：

### VB.NET

```
Protected Sub Wizard1_FinishButtonClick(sender As Object,
e As EventArgs) Handles Wizard1.FinishButtonClick
Result.Text = "Your name is " & YourName.Text
Result.Text &= "<br>Your favorite language is " & FavoriteLanguage.SelectedValue
End Sub
```

### C#

```
protected void Wizard1_FinishButtonClick(object sender,
NavigationEventArgs args)
{
Result.Text = "Your name is " + YourName.Text;
Result.Text += "<br>Your favorite language is " + FavoriteLanguage.SelectedValue;
}
```
