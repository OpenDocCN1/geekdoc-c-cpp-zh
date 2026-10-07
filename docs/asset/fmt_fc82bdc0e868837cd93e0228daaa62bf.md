
`<asp:TreeView id="TreeView1" runat="server" DataSourceID="XmlDataSource" />`

当你这样做时，你将在图 13-11 中得到正确的结果。

![](img/7040c21013b8e6c23c612d6da3599ff8_592_0.png)

图 13-11

如你所见，`TreeView`控件仅绑定到`Hardware.xml`文件，但对于`TreeView`控件内部的节点，你可以看到它仅仅显示了文件本身的`XML`元素名称。除非使用`TreeView`控件内的`<DataBindings>`元素指定如何绑定到`XML`文件。

`<DataBindings>`封装了一个或多个`TreeNodeBinding`对象。`TreeNodeBinding`对象两个重要的值是`DataMember`和`TextField`属性。`DataMember`属性指向`TreeView`控件应该查找的`XML`元素名称。`TextField`属性指定`TextView`在特定`XML`元素中查找的`XML`属性。如果你正确使用`<DataBindings>`元素和`<DataBindings>`构建，将得到图 13-12 所示的结果。

![](img/7040c21013b8e6c23c612d6da3599ff8_593_0.png)

图 13-12

你也可以从列表 13-9 中看到你可以覆盖`XML`文件`<Hardware>`根节点的文本值，并使其在`TreeView`控件中显示为`Computer Hardware`，如下：

```
<asp:TreeNodeBinding DataMember="Hardware" Text="Computer Hardware" />
```

# 在 TreeView 中选择多个选项

如前，`TreeView`控件并非专门用于导航目的。你可以用它处理各种事情。在许多情况下，你可以展示一个层级列表，让最终用户从中选择一个或多个元素。

`TreeView`控件的一个非常棒内置功能是在层级列表中的节点旁放置复选框。这些框允许用户进行多项选择。`TreeView`控件包含一个名为`ShowCheckBoxes`的属性，你可以用它在元素列表中的许多类型节点旁创建复选框。

表 13-3 列出了`ShowCheckBoxes`属性的可用值。

## 表 13-3

| 数值 | 描述 |
|---|---|
| All | 对`TreeView`控件中的每一个节点应用复选框。 |
| Leaf | 仅对没有子元素的节点应用复选框。 |
| None | 对`TreeView`控件中的任何节点不应用复选框。 |
| Parent | 对`TreeView`控件中被视为父节点的节点应用复选框。父节点至少关联一个子节点。 |
| Root | 对`TreeView`控件包含的任何根节点应用复选框。 |

在使用`ShowCheckBoxes`属性时，你可以在控件本身中声明式地设置它，如下所示：

```
<asp:TreeView ID="TreeView1" runat="server" Font-Underline="false"
    DataSourceID="XmlDataSource" ShowCheckBoxes="Leaf">
    ----
</asp:TreeView>
```

或者你也可以通过以下代码对其对其进行设置：

| VB | C# |
| :--- | :--- |
| TreeView.ShowCheckBoxes = NodeTypes.Leaf | TreeView.ShowCheckBoxes = System.Web.UI.WebControls.NodeTypes.Leaf; |

关于在`TreeView`控件上使用复选框的示例，让我们继续扩展列表 1 中的计算机硬件。分级列表允许人们从列表中选择多个项目，以接收有关这些项目的额外信息。列表 13-10 显示了此类列表的一个示例：

# 列表 13-10：在节点分级列表的叶子节点旁应用复选框

```vb
@ Page Language="VB" %>
<script runat="server">
Protected Sub Button_Click(ByVal sender As Object, ByVal e As System.EventArgs)
    If TreeView.CheckedNodes.Count > 0 Then
        Label.Text = "We are sending you information on:"<br>
        For Each node In TreeView.CheckedNodes
            Label.Text += " * " & node.Parent.Text & "<br>"
        Next
    Else
        Label.Text = "You didn't select anything. Sorry!"
    End If
End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>Latest Hardware</title>
</head>
<body>
<form runat="server">
Please select the items you are interested in:
<p>
<asp:TreeView ID="TreeView1" runat="server" Font-Underline="False"
    DataSourceID="XmlDataSource" ShowCheckBoxes="Leaf">
<DataBindings>
<asp:NodeBinding DataMember="Hardware" />
<asp:NodeBinding DataMember="Item" TextField="Category" />
<asp:NodeBinding DataMember="Option" TextField="Choice" />
</DataBindings>
</asp:TreeView>
<p>
<asp:Button ID="Button1" runat="server" Text="Submit Choices"
OnClick="Button1_Click" />
</p>
<asp:XmlDataSource ID="XmlDataSource" runat="server" DataFile="Hardware.xml">
</asp:XmlDataSource>
</p>
<asp:Label ID="Label" runat="Server" />
</form>
</body>
</html>
```

```csharp
@ Page Language="C#" runat="server"
<script>
protected void Button1_Click(object sender, System.EventArgs e)
{
    if (TreeView.CheckedNodes.Count > 0)
    {
        Label1.Text = "We are sending you on:<br>";
        foreach (TreeNode node in TreeView.CheckedNodes)
        {
            Label1.Text += node.Text + " " + node.Parent.Text + " <br>";
        }
    } else {
        Label1.Text = "You didn't select anything. Sorry!";
    }
}
</script>
```

在此示例中，你将`ShowCheckBoxes`设置为`Leaf`，使得你感兴趣的节点仅在`TreeView`控件中不包含子节点的项目旁显示复选框。带有复选框的项目应该是分级列表中可以可以展开的最后一个项目。

设置此项后，你可以在`Button1_Click`事件中处理终端用户选择的项目。你应该执行的第一件事是检查是否真的进行了任何选择：

```csharp
If TreeView.CheckedNodes.Count > 0
End If
```

在这种情况下，页面上选中的节点数将大于零，意味着至少有一个被选中。随后`If`语句将继续执行`If`语句内的代码，以填充页面上的`Label`控件。要用所选节点的数据填充`Label`控件，你使用`For Each`语句，如下所示：

```csharp
For Each node as TreeNode In TreeView.CheckedNodes
Next
```

这适用于`TreeNode`对象的实例，并检查`TreeView`集合中选中的节点中的每个`TreeNode`对象。对于每个被选中的节点，获取节点的`Text`值以及该节点父节点的`Text`值，以进一步填充`Label`控件，如下：

```csharp
Label1.Text += node.Text + " & " + node.Parent.Text + " <br>";
```

最后，你将得到一个产生图 13-13 所示结果的页面。

![](img/7040c21013b8e6c23c612d6da3599ff8_596_0.png)

图 13-13

# 在 TreeView 控件中指定自定义图标

`TreeView`控件允许高度自定义。你在本章前面的部分已经看到，可以通过指定这些样式之一来自定义`TreeView`控件的外观和感受，这极大地改变了控件的外观。最明显的变化涉及你用于`TreeView`控件内节点的图标。虽然这不像直接选择`TreeView`内置的某种样式那么简单，但你可以将自己的图标应用到节点上。

表 13-4

| 属性 | 描述 |
| :--- | :--- |
| CollapseImageUrl | 应用到折叠节点的自定义图像。 |
| ExpandImageUrl | 应用到展开节点的自定义图像。 |
| LeafImageUrl | 应用到叶子节点的自定义图像。 |
| NoImageUrl | 应用到没有子节点的节点的自定义图像。 |
| ParentNodeStyle | 应用到父节点的自定义样式。 |
| RootNodeStyle | 应用到根节点的自定义样式。 |

# 540 | 第 13 章 站点导航

从此对话框中，你可以为需要展开（Expand）、折叠（Collapse）或不折叠（NoCollapse）的节点选择图像。你还可以指定连接节点的颜色和样式。当你创建样式时，对话框将根据你样式的应用情况直接显示`TreeView`控件输出。完成后，点击确定。这将在你在详细信息中指定的文件夹中生成长的新文件列表。`ASP.NET TreeView`线生成器允许你将输出文件夹命名为`Images`，你可以随意命名。如果项目项目中不存在该文件夹，系统会提示你使用`Visual Studio`为你创建文件夹。如果此文件夹已到位，当你按照以下方式启动节点的展开和折叠时，`TreeView`控件就可以使用你的新图像和样式：

```
<asp:TreeView ID="TreeView" runat="server" ShowLines="True" LineImagesFolder="Images" />
```

重要的属性所示。你必须将`ShowLines`属性设置为`True`。设置后，该属性将使用较早显示的默认设置，除非你使用`LineImagesFolder`属性指定了可以检索自定义图像和样式的位置。如你所见，这只是指向了新文件夹`TreeViewLineImages`，其中包含了你创建的所有新图像和样式。查看该文件夹——查看工具的输出将大有益处。

## 以编程方式操作 TreeView 控件

到目前为止，通过`TreeView`控件，你已经学习了如何以声明的方式操作该控件。`ASP.NET`的强大之处在于，你不仅限于以声明的方式处理其组件，而是可以通过编程方式管理这些组件。

`TreeView`控件有一个可访问的`TreeView`类，它允许你从代码中完全管理`TreeView`控件及其功能方式。下一节将介绍如何使用一些常用方法通过编程控制`TreeView`。

## 以编程方式展开和折叠节点

你可以对`TreeView`控件执行的操作之一是以编程方式展开或折叠层级结构中的节点。你可以使用`TreeView`类中的`ExpandAll`或`CollapseAll`方法来实现。列表 13-12 显示了你在代码 13-6 中使用的早期`TreeView`之一，但其上方有两个按钮，你可以使用这些按钮来启动节点的展开和折叠。

列表 13-12：编程编程展开和折叠`TreeView`控件的节点

```asp
<%@ Language="VB" %>
<script runat="server">
Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
    TreeView.Expand()
End Sub

Protected Sub Button2_Click(ByVal sender As Object, ByVal e As System.EventArgs)
    TreeView.Collapse()
End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>TreeView Control</title>
</head>
<body>
<form id="Form1" runat="server">
<p>
<asp:Button ID="Button1" runat="server" Text="Expand Nodes" OnClick="Button1_Click" />
```

```
<asp:Button ID="Button2" runat="server" Text="Collapse Nodes" OnClick="Button2_Click" />
<br />
<br />
<asp:TreeView Id="TreeView1" runat="server" DataSourceID="SiteMapDataSource">
</asp:TreeView>
<asp:SiteMapDataSource ID="SiteMapDataSource" runat="server" /></p>
</form>
</body>
</html>
```

```csharp
// C#
<%@ Page Language="C#" %>
<script runat="server">
protected void Button1_Click(object sender, System.EventArgs e)
{
    TreeView1.ExpandAll();
}
protected void Button2_Click(object sender, System.EventArgs e)
{
    TreeView1.CollapseAll(); // 注意：原文此处可能漏了代码，已根据逻辑补全
}
</script>
```

# 列表 13-15（继续）

```html
<p>
  <strong>新节点的目标 URL：</strong>
  <asp:TextBox ID="TextBox2" runat="server">
  </asp:TextBox>
  <br />
  <br />
  <asp:Button ID="Button3" runat="server" Text="Add New Node" OnClick="Button3_Click" />
</p>
<p>
  <asp:TreeView ID="TreeView1" runat="server" DataSourceID="SiteMapDataSource">
  </asp:TreeView>
</p>
<p>
  <asp:SiteMapDataSource ID="SiteMapDataSource" runat="server" />
</p>
</form>
<html>
```

```csharp
protected void Button3_Click(object sender, System.EventArgs e)
{
  TreeNode node = new TreeNode();
  node.Text = TextBox1.Text;
  node.NavigateUrl = TextBox2.Text;
  TreeView.FindNode("Home/Finance/Markets").ChildNodes.Add(node);
}
```

此页面包含两个文本框和一个新按钮。第一个文本框用于填充所创建的新节点的`Text`属性。第二个文本框用于填充新节点的`NavigateUrl`属性。

如果你运行该页面，可以通过点击“展开节点”按钮来展开层级结构。然后，你可以向该节点添加额外的子节点。要通过程序方式添加新节点，请像你查找`Markets`节点那样样使用`FindNode`方法。当你找到它时，可以使用`ChildNodes.Add()`方法添加额外的子节点，并传入一个`TreeNode`对象。在文本框中输入`NASDAQ`并在第二个文本框输入，将显示`TreeView`控件，如图 13-18 所示。

![](img/7040c21013b8e6c23c612d6da3599ff8_603_0.png)

图 13-18

# 菜单服务器控件 | 545
