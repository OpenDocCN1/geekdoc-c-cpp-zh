

7. 再次切换到设计视图，点击 GridView 并按 F4 打开其属性网。切换到事件（Events）选项卡并双击以下事件，在后台代码（Code Behind）中为它们设置处理器。在每个处理器设置之后，按 Ctrl+Tab 回到设计视图，以便添加下一个事件。

- Sorted（排序）
- Sorting（排序）
- RowCreated（行创建）
- DataBinding（数据绑定）
- DataBound（数据已绑定）
- RowDataBound（行数据绑定）

8. 重复上述步骤，但现在为 SqlDataSource 控件的 Selecting（选择）事件设置处理器。

9. 确保你处于后台代码中，并在文件顶部添加以下 Imports/using 语句：

# VB.NET
```vb
Imports System.Runtime.CompilerServices
```

# C#
```csharp
using System.Runtime.CompilerServices;
```

然后在最后一个事件下方（但仍要在类定义内部），添加以下方法，该方法将向两个标签之一之一写入内容，取决于当前页面请求是否为回传（postback）：

# VB.NET
```vb
Private Sub WriteMessage(<CallerMemberName> Optional handlerName As String = "*")
    If Page.IsPostBack Then
        PostBack.Text &= handlerName & "<br />"
    Else
        NoPostBack.Text &= handlerName & "<br />"
    End If
End Sub
```

# C#
```csharp
private void WriteMessage([CallerMemberName] string handlerName = "*")
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

10. 为你设置的每个事件处理器添加以下调用你自定义方法的代码。由于你没有为可选参数 handlerName 传递值，.NET 会自动将调用者方法的名称作为 `CallerMemberName` 特性应用到 WriteMessage 方法的该参数上。你稍后将看到它是如何工作的。

# VB.NET
```vb
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    WriteMessage()
End Sub
```

# C#
```csharp
protected void Page_Load(object sender, EventArgs e)
{
    WriteMessage();
}
```

11. 最后，在后台代码中手动添加以下事件处理器：

# VB.NET
```vb
Protected Sub Page_PreRenderComplete(sender As Object,
    e As EventArgs) Handles Me.PreRenderComplete
    WriteMessage("Page_PreRenderComplete<br />-------")
End Sub
```

# C#
```csharp
protected void Page_PreRenderComplete(object sender, EventArgs e)
{
    WriteMessage("Page_PreRenderComplete<br />-------");
}
```

PreRenderComplete 事件在 Page 控件生命周期的非常后期才触发，这使其成为在列表底部放置代码的理想位置。这样，你就可以清楚地看到哪些事件是相互关联的，这反过来也有助于你弄清楚页面加载或回传期间触发了哪些事件。

12. 保存所有更改并在浏览器中打开该页面。除了带有可用生成器的 GridView 之外，你还应该在 No PostBack 标题下看到事件列表：

```
Page_Load
SqlDataSource_DataBinding
GridView1_DataBinding
GridView1_RowCreated
GridView1_RowDataBound
GridView1_RowCreated
GridView1_RowDataBound
...
GridView1_DataBound
Page_PreRenderComplete
```

注意，RowCreated 和 RowDataBound 事件重复了多次——对应数据库中的每种类型一次，外加另外两个。你稍后会看到为什么。点击 GridView 下方的按钮以触发回传。No PostBack 标签不会改变，但 PostBack 现在会显示以下事件名称列表：

# 处理事件 | 553

```
GridView1_RowCreated
GridView1_RowCreated
...
GridView1_RowCreated
GridView1_RowCreated
Page_Load
Button_Click
Page_PreRenderComplete
```

点击 GridView 的其中一个列头以对其显示的数据进行排序。注意，第二个标签的文本扩展了一组事件名称。每组事件之间由一条破折线隔开，该折线是由 Page_PreRenderComplete 事件处理器生成的。

# 工作原理

从技术上讲，这个练习并不复杂。你为页面中的各种控件设置了一系列事件处理器。在事件处理器内部，你调用了一个方法来检查页面当前是首次加载还是由于回传引起的。为了方便将调用者方法的名称添加到 Label 控件中，方法的 `handlerName` 参数具有一个特殊的 `CallerMemberName` 特性，如下：

# VB.NET
```vb
Private Sub WriteMessage(<CallerMemberName> Optional handlerName As String = "*")
```

# C#
```csharp
private void WriteMessage([CallerMemberName] string handlerName = "*")
```

该特性是在 .NET 中引入的。

