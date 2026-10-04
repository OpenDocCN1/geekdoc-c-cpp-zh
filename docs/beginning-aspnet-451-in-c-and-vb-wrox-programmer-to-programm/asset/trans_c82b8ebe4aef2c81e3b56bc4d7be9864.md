

最后，单击 OK 以在页面中插入这些项目。你应该在 Markup 视图中得到以下代码：

<asp:DropDownList ID="DropDownList1" runat="server">
<asp:ListItem Text="C#"></asp:ListItem>
<asp:ListItem Text="Visual Basic"></asp:ListItem>
<asp:ListItem Text="CSS"></asp:ListItem>
</asp:DropDownList>

- 6. 在 Markup 视图中，从工具箱将 CheckList 控件拖动到代码窗口中，直接放在 DropDownList 之后。

- 7. 复制你在步骤 4 和 5 中创建的 DropDownList 中的 <asp:ListItem> 元素，并将它们粘贴在 CheckBoxList 的开始和结束标签之间。你应该得到以下代码：

<asp:ListItem Text="CSS"></asp:ListItem>
<asp:CheckList ID="CheckBox1" runat="server">
<asp:ListItem Text="C#"></asp:ListItem>
<asp:ListItem Text="Visual Basic"></asp:ListItem>
<asp:ListItem Text="CSS"></asp:ListItem>
</asp:CheckList>

- 8. 切换到 Design 视图，并在 Design 视图中从工具箱拖动一个 Button 放置在 CheckList 控件的右侧。Button 将被放置在 CheckBoxList 下方。接下来，拖动一个 Label 控件并将其放置在 Button 的右侧。通过将光标定位在控件之前并按两次 Enter 来在 Button 和 Label 之间创建一些空间。双击按钮以打开头页的 Code Behind。

- 9. 在 VS 为你添加的代码块中，添加以下加粗代码，该代码将在用户单击按钮时执行：

```
VB.NET
Protected Sub Button1_Click(sender As Object, e As EventArgs)
    Handles Button1.Click
    Label1.Text = "In the DDL you selected " & _
    DropDownList1.SelectedValue & "<br />"_

    For Each item As ListItem In CheckList1.Items
        If item.Selected = True Then
            Label1.Text &= "In the CBL you selected " & item.Value & "<br />"_
        End If
    Next
End Sub
```

```
C#
protected void Button1_Click(object sender, EventArgs e)
{
    Label1.Text = "In the DDL you selected " + _
    DropDownList1.SelectedValue + "<br />";

    foreach (ListItem item in CheckList1.Items)
{
```

## Types of Controls

```
if (item.Selected == true)
{
  Label1.Text += "In the CBL you selected " + item.Value + "<br />";
}
```

注意在 VB.NET 代码中，下划线是用来将代码拆分到两行的。VB.NET 要求在将 Handles 关键字移至

- 10. 保存页面并在浏览器中请求它。从 DropDownList 中选择一个项目，在 CheckBoxList 中勾选或一个项目，然后单击按钮。你会看到类似于图 4-8 的内容，该图显示了 Firefox 中的页面。

![](img/9e033e3b9560597824f8b22941d6d8bb_150_0.png)

FIGURE 4-8

## How it Works

各种列表控件都使用 <asp:ListItem> 元素。这使得通过从一个复制到另一个来创建它们变得很容易。DropDownList 一次只支持一个项目，获取其值非常容易。只需在 C# 中写一行代码即可)：

```
Label1.Text = "In the CBL you selected " + DropList1.SelectedValue + "<br />";
```

CheckBox 控件允许用户一次选择多个项目。因此，你需要编写更多代码来遍历项目集合，检查每个项目的 Selected 属性（再次以 C# 显示）：

```
foreach (ListItem item in CheckBoxList1.Items)
{
  if (item.Selected == true)
  {
    Label1.Text += "In the CBL you selected " + item.Value + "<br />";
  }
}
```

CheckList 和其他列表控件具有 Items，其中包含你在代码中定义的所有项目。因此，Try It Out、CheckBoxList 的代码包含三个项目，分别为 C#、Visual Basic 和 CSS。每个 ListItem 反过来包含一个属性，用于确定用户是否在列表中选中了该项目

使用 foreach 循环（VB.NET 中的 For Each），你可以遍历 ListItems 元素的集合，一一测试 Selected 属性。如果项目被选中，其 Selected 属性为 true（VB 中为 True），其 Value 会被追加到 Label 的文本中。注意在最后一个示例中使用 +=（VB.NET 中为 &=）将项目的 Value 与文本一起分配给 Label 的 Text 属性。+= 和 &= 语法是以下内容的简写：

Label1.Text = Label1.Text + "In the CBL you selected " + item.Value + "<br />";

这段代码从 Label 控件中获取当前文本，将文字 "In the CBL you selected" 追加到它后面，使用 item.Value 追加项目的值，最后追加文字 <br />。它将整个字符串重新分配回标签的 Text 属性。使用 += 语法通常更容易编写和理解，但较长的版本也很常见。

VB.NET 和 C# 都支持 each 循环，尽管两种语言使用略有不同的语法。在下一章中，你将学习更多关于循环和语言构造的知识。

还值得注意的是，ListItems 出现是因为你在第一个示例中看到了 ListItem，因为在 Try It Out 中，你看到了具有值和文本的 ListItem 项目：

```
<asp:ListItem Value="C#">C#</asp:ListItem>
<asp:ListItem Value="Visual Basic">Visual Basic</asp:ListItem>
<asp:ListItem Value="CSS">CSS</asp:ListItem>
```

当你使用 ListItem Collection Editor 添加项目到列表时，你可以获取 Value 属性

```
<asp:ListItem Value="C#">C#</asp:ListItem>
<asp:ListItem Value="Visual Basic">Visual Basic</asp:ListItem>
<asp:ListItem Value="CSS">CSS</asp:ListItem>
```

你没有得到 Value 属性，因为你在 ListItem Collection Editor 中没有为项目提供显式值。如果你省略值，则 ListItem 的开始和结束标签之间的文本会被隐式用作值，在许多情况下这是可以的。然而，拥有列表中不同的 Value 和 Text 属性也很常见。例如，当你有一个国家列表时，你可以使用国家的全名作为 Text（如 The Netherlands），并使用官方国家代码 [nl] 作为下拉列表的 Value。你可以在本书的其他章节中看到列表控件的工作情况。

## Container Controls

通常希望对相关内容和控件进行分组。你可以通过将控件（或其他标记）放在容器控件之一中来实现这一点，例如 Panel、PlaceHolder、MultiView 或 Wizard。例如，你可以一次显示多个控件。无需分别隐藏每个控件，只需隐藏包含所有单个控件和标记的整个容器即可。这两种控件各有优缺点。PlaceHolder 控件的好处是它本身没有 HTML 页面，因此你可以用它作为容器而不会在最终页面中产生任何副作用。然而，它缺乏设计支持，使得在设计时管理 PlaceHolder 内部的控件变得困难。相比之下，MultiView 允许你启用它包含的所有控件和其他内容，但它本身会渲染为 <div>。在许多情况下这不是问题，甚至可能有用，因为你可以使用 CSS 在控件上使用该 div，因此通常你最好使用 Panel 控件，因为它具有设计时支持。

MultiView（可以包含一个或多个 <asp:View> 元素）和 Wizard 在它们能够将长页面拆分为多个区域方面相似，使得填写长表单变得容易。例如。Wizard 具有内置支持，可使用 Previous、Next 和 Finish 按钮在页面之间移动，而 MultiView 必须以编程方式控制。

## A Closer Look at the Panel Control

在以下练习中，你使用 Panel 控件为其他控件和标记创建一个容器。你现在只添加一些文本，但在随后的 Try Out 练习中，你将向面板添加 ASP.NET 控件。

## TRY IT Using the Panel Control

在这个练习中，你将看到如何使用 Panel 控件作为一些简单文本的容器。此外，你还使用 CheckBox 在服务器上控制 Panel 的可见性。

- 首先在 Demos 项目中创建一个名为 Containers.aspx 的新 Web Form with Code Behind。

- 切换页面到 Design 视图并从工具箱拖动一个 CheckBox 和一个 Panel 控件到设计表面下方的虚线 `<div>` 元素下。

- 通过设置其 Text 属性为 Show Panel 并使用属性网格将其 PostBack 属性设置为 True 来为 CheckBox 控件提供有意义的描述。选择面板的下拉列表时，你也可以双击 PostBack 属性或其值在 False 和 True 之间切换。

- 使用属性网格将 Panel 的 Visible 属性设置为 False。这会在页面首次加载时隐藏面板。

- 在 Panel 控件内部，输入一些文本（例如，I am visible now）。请注意，面板的行为类似于 VS 设计表面的其余部分。你可以向其中添加文本、选择和格式化它，并通过从工具箱拖动来添加新控件。面板在 Markup 中应如下所示：

```
<asp:Panel ID="Panel" runat="server" Visible="False">
I am visible now
</asp:Panel>
```

```
<asp:CheckBox ID="CheckBox" runat="server" PostBack="True" Text="Show Panel" />
<asp:Panel ID="Panel" runat="server">
I am visible now
</asp:Panel>
```

FIGURE 4-9

- 在 Markup 中，找到 CheckBox 的代码。将光标定位在关闭斜杠（/）之前的正前方，然后按 Enter，后跟 Ctrl+Space。这会调出 IntelliSense，如图 4-9 所示。

选择 OnChanged 通过按 Tab 或 Enter。键入等号（=），这会调出 IntelliSense，如图 4-10 所示。请注意，如果你使用的是 C#，你可能还会看到事件处理程序列表中的 PostBack 项目。

```
<asp:CheckBox ID="CheckBox" runat="server" PostBack="True" 
Text="Show Panel" OnChanged="#CheckedChanged-" 
<asp:Panel ID="Panel" runat="server" # CreateNewEvent-">
I am visible now
</asp:Panel>
```

FIGURE 4-10

选择 <New Event> 项目并按 Tab。VS 会按如下方式完成代码：

```
OnChange="CheckBox1_CheckedChanged"
```

虽然这个选择很好，但 VS 做的事情更有用；当你按 Tab 时，它还在 Code Behind 中为你添加了处理程序代码。要查看该代码，请按 F7 切换到 Code

