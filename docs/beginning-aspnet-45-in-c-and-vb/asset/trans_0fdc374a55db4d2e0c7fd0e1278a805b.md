

4. 确保你处于“标记视图”（Markup View），然后在开头的 Content 标记正下方、GridView 之前，添加以下标记，创建一个包含一行两列的表格，每个单元格分别有一个大标题（h1）和一个名为 `NoPostBack` 和 `PostBack` 的 Label 控件。

```html
<table>
<tr>
<td><h1>No PostBack</h1><asp:Label ID="NoPostBack" runat="server" /></td>
<td><h1>PostBack</h1><asp:Label ID="PostBack" runat="server" /></td>
</tr>
</table>
```

5. 切换到“设计视图”（Design View），在 GridView 下方放置一个 Button 控件，并在设计视图中双击该按钮，以便在代码隐藏文件中为其 Click 事件设置事件处理程序。

6. 切换回设计视图，双击页面的灰色只读区域，为 Page 控件的 Load 事件设置处理程序。

7. 再次切换到设计视图，单击 GridView，然后按 F4 打开其“属性”窗口。切换到“事件”选项卡，并双击以下事件，以便在代码隐藏文件中为它们设置处理程序。每处理完一个事件后，按 Ctrl+Tab 切换回设计视图，以便添加下一个事件。

   - Sorted
   - Sorting
   - RowCreated
   - DataBinding
   - DataBound
   - RowDataBound

8. 重复上一步骤，但现在为 EntityDataSource 控件设置以下事件：

   - ContextCreating
   - Selecting

9. 确保你处于代码隐藏文件，并在文件顶部添加以下 Imports/using 语句：

### VB.NET

```vbnet
Imports System.Runtime.CompilerServices
```

### C#

```csharp
using System.Runtime.CompilerServices;
```

然后在最后一个事件处理程序的下方（但仍在类定义内），添加以下方法，该方法根据当前页面请求是否为回发的结果，向两个标签之一写入一些文本：

### VB.NET

```vbnet
Private Sub WriteMessage(<CallerMemberName> Optional handlerName As String = "")
    If Page.IsPostBack Then
        PostBack.Text &= handlerName & "<br />"
    Else
        NoPostBack.Text &= handlerName & "<br />"
    End If
End Sub
```

### C#

```csharp
private void WriteMessage([CallerMemberName] string handlerName = "")
{
    if (Page.IsPostBack)
    {
        PostBack.Text += handlerName + "<br />";
    }
    else
    {
        NoPostBack.Text += handlerName + "<br />";
    }
}
```

10. 为你设置的每个事件处理程序添加以下代码，以调用你的自定义方法。由于你没有为可选的 `handlerName` 参数传递值，.NET 会因 `WriteMessage` 方法中该参数上应用了 `CallerMemberName` 特性而自动插入调用方法的名称。稍后你会看到这是如何工作的。

### VB.NET

```vbnet
Private Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    WriteMessage()
End Sub
```

### C#

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    WriteMessage();
}
```

11. 最后，手动向代码隐藏文件添加以下事件处理程序：

### VB.NET

```vbnet
Protected Sub Page_PreRenderComplete(sender As Object, e As EventArgs) Handles Me.PreRenderComplete
    WriteMessage("Page_PreRenderComplete<br />------")
End Sub
```

### C#

```csharp
protected void Page_PreRenderComplete(object sender, EventArgs e)
{
    WriteMessage("Page_PreRenderComplete<br />------");
}
```

`PreRenderComplete` 事件在 Page 控件的生命周期中触发得非常晚，因此它是将一行内容放在事件列表底部的理想位置。这样你就可以清楚地看到哪些事件属于同一组，进而帮助你弄清在页面加载或回发期间会触发哪些事件。

12. 保存所有更改并在浏览器中打开页面。除了带有可用流派的 GridView 之外，你还应在“无回发”（No PostBack）标题下看到一个事件名称列表：

```
Page_Load
EntityDataSource1_ContextCreating
EntityDataSource1_Selecting
GridView1_DataBinding
GridView1_RowCreated
GridView1_RowDataBound
GridView1_RowCreated
GridView1_RowDataBound
...
GridView1_DataBound
Page_PreRenderComplete
----------
```

请注意，`RowCreated` 和 `RowDataBound` 事件重复了多次——数据库中的每个流派一次，另外还有两次。稍后你将了解这是为什么。单击 GridView 下方的按钮以触发回发。“无回发”（NoPostBack）标签不会改变，但“回发”（PostBack）标签现在显示以下事件名称列表：

```
GridView1_RowCreated
GridView1_RowCreated

GridView1_RowCreated
GridView1_RowCreated
Page_Load
Button1_Click
Page_PreRenderComplete
----------
```

单击 GridView 的某个列标题以对其显示的数据进行排序。请注意，第二个标签的文本会扩展出第二组事件名称。每组之间由一行破折号分隔，这是由 `Page_PreRenderComplete` 事件处理程序生成的。

## 工作原理

从技术上讲，这个练习并不复杂。你为页面中的各种控件设置了一组事件处理程序。在事件处理程序内部，你调用一个方法，该方法检查页面当前是首次加载还是因回发而加载。为了方便将调用方法的名称添加到 Label 控件中，该方法的 `handlerName` 参数应用了一个特殊的 `CallerMemberName` 特性，如下所示：

### VB.NET

```vbnet
Private Sub WriteMessage(<CallerMemberName> Optional handlerName As String = "")
```

### C#

```csharp
private void WriteMessage([CallerMemberName] string handlerName = "")
```

此特性是 .NET 4.5 中的新功能，可应用于可选参数（在 VB.NET 中通过 `Optional` 关键字和默认值标识，在 C# 中只需为其分配默认值即可）。当未向 `WriteMessage` 方法的此参数传递任何值（大多数处理程序都是如此，除了你添加的最后一个处理程序），.NET 会自动用调用方法的名称填充该参数。这对于调试非常方便，因为它使你能够轻松地确定哪个方法调用了 `WriteMessage`。在 .NET 的早期版本中，你必须在每次调用 `WriteMessage` 时手动传递调用方法的名称，这使得代码编写起来更加繁琐。此外，由于该特性仅在未传入值时才会生效，你仍然可以自己提供一个值，就像 `Page_PreRenderComplete` 处理程序的情况一样。除了方法名之外，此代码还传递换行符和虚线，因此你需要自己提供该值。

然后，`WriteMessage` 方法会用触发事件处理程序的事件名称来更新两个 Label 控件之一。

这个练习另一个有趣的地方是事件的触发顺序。看一下页面首次加载时显示的第一个列表：

```
Page_Load
EntityDataSource1_ContextCreating
EntityDataSource1_Selecting
GridView1_DataBinding
GridView1_RowCreated
GridView1_RowDataBound
GridView1_RowCreated
GridView1_RowDataBound
...
GridView1_DataBound
Page_PreRenderComplete
------------------
```

首先触发 `Page_Load`。然后 GridView 发现它连接到了 EntityDataSource，并向该控件请求其数据。这会导致触发 `ContextCreating` 和 `Selecting` 事件。当 GridView 从 EntityDataSource 接收到数据后，它会触发其 `DataBinding` 事件，以表示即将将数据绑定到控件。然后 GridView 开始创建其行。对于数据源中的每一项，它都会创建一行，触发 `RowCreated`，将该行的数据绑定到该项，最后调用 `RowDataBound`。如果你仔细数一下 `RowCreated` 和 `RowDataBound` 被调用的次数，你会发现总调用次数是数据源中的实际项目数加二。这是因为当控件创建其页眉和页脚行时，也会引发相同的事件。你将在后续练习中了解如何在事件处理程序内区分这些行。

最后，当 GridView 完成创建并绑定数据源中的所有行后，它会触发其 `DataBound` 事件。

在回发时，情况则完全不同。当你单击按钮触发回发时，会引发以下事件：

```
...
GridView1_RowCreated
GridView1_RowCreated
GridView1_RowCreated
GridView1_RowCreated
Page_Load
```

