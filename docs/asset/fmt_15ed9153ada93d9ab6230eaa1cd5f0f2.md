
```asp
<asp:TreeView ID="server" DataSourceID="SiteMapDataSource"
ImageSet="Msdn" NodeIndex="0">
  <ParentNodeStyle BackColor-Bold="False" />
  <HoverNodeStyle BackColor="CCCCCC" BorderColor="#888888" BorderStyle="Solid"
  Font-Underline="True" />
  <SelectedNodeStyle BackColor="White" BorderColor="#888888" BorderStyle="Solid"
BorderWidth="1px" Font-Underline="False" HorizontalPadding="3px"
  VerticalPadding="1px" />
  <NodeStyle Font-Names="Verdana" Font-Size="8pt" ForeColor="Black"
  HorizontalPadding="5px" NodeSpacing="2px" VerticalPadding="2px" />
</asp:TreeView>
```

如你所见，如果这些内置样式，完全改变 `TreeView` 控件的外观和感觉并不困难。运行这段代码时，你将得到 14-10 所示的结果。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_713_0.png)

图 14-10

## TreeView 控件的组成

要掌握 `TreeView` 控件，你必须理解控件创建的层级树每个部分部分使用的术语。

首先，`TreeView` 控件中的每个元素都称为节点（node）。节点层级结构中最顶部的节点是根节点（root node）。`TreeView` 控件可以有多个根节点。任何节点（包括根节点）如果在其节点层级结构中直接下方有任何节点，它也被视为父节点（parent node）。直接位于此父节点下方的节点被称为子节点（child nodes）。每个父节点可以有一个或多个子节点。如果一个节点没有子节点，则它被称为叶子节点（leaf node）。

以下基于之前显示的站点地图，详细说明了这些术语的使用：

- 根节点，父节点
- 父节点，子节点
- 美国 (U.S.) - 子节点，叶子节点
- 世界 (World) - 子节点，叶子节点
- 技术 (Technology) - 子节点，叶子节点
- 体育 (Sports) - 子节点，叶子节点
- 金融 (Finance) - 父节点，子节点
- 引言 (Quotes) - 子节点，叶子节点
- 市场 (Markets) - 父节点，子节点
- 美国市场报告 (U.S. Market Report) - 子节点，叶子节点
- 纽约证券交易所 (NYSE) - 子节点，叶子节点
- 资金 (Funds) - 子节点，叶子节点
- 天气 (Weather) - 子节点，叶子节点

从此列表中，你可以看到每个节点及其在节点层级中的称呼。例如，美国市场报告节点是一个叶子节点——意味着它没有关联的子节点。但是，它是市场节点的子节点，而市场节点又是美国市场报告节点的父节点。如果你在处理市场节点，它也是金融节点的子节点，这一切都是站点地图与其他节点的关系。你必须理解这些关系，因为你可以通过编程方式处理这些节点，使用的方法包括 `RootNode`、`CurrentNode` 和 `ParentNode`。

## 将 TextView 控件绑定到 XML 文件

你不限于使用 sitemap 文件来填充 TextView 控件的节点。你有许多方法可以这一点。一种方法是使用 `XMLDataSource` 控件（而不是 `SiteMap` 控件）从你的 XML 文件填充 TextView 控件。此示例是在名为 `Hardware.xml` 的 XML 文件创建一个层级列表。此示例见列表 14-8。

### 列表 14-8：Hardware.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<Hardware>
  <Item Category="Motherboards">
    <Choice>Asus</Choice>
    <Choice>Abit</Choice>
  </Item>
  <Item Category="Memory">
    <Choice>128mb</Choice>
    <Choice>256mb</Choice>
    <Choice>512mb</Choice>
  </Item>
  <Item Category="HardDrives">
    <Choice>40GB</Choice>
    <Choice>80GB</Choice>
    <Choice>100GB</Choice>
  </Item>
  <Item Category="Drives">
    <Choice>CD</Choice>
    <Choice>DVD</Choice>
    <Choice>DVD Burner</Choice>
  </Item>
</Hardware>
```

如你所见，此列表并非用于站点导航，而是为了让用户从层级列表中进行选择。此 XML 文件被分为四个类别：Motherboards、Memory、HardDrives 和 Drives。要将你的 TextView 控件绑定到 XML 文件，使用指定 XML 文件位置的 `XMLDataSource` 控件。然后在 TextView 控件内部，使用 `asp:TreeNodeBinding` 元素指定绑定 XML 文件中的哪些元素来填充 TextView 控件。这在 14-9 中所示。

### 列表 14-9：将 TreeView 控件绑定到 Hardware.xml

```asp
@Page Language="VB" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
  <title>Latest Hardware</title>
</head>
<body>
  <form id="form" runat="server">
    <asp:TreeView id="TreeView1" runat="server" DataSourceID="XmlDataSource">
      <DataBindings>
        <asp:TreeNodeBinding DataMember="Hardware" Text="Computer Hardware" />
        <asp:TreeNodeBinding DataMember="Item" TextField="Category" />
        <asp:TreeNodeBinding DataMember="Option" TextField="Choice" />
      </DataBindings>
    </asp:TreeView>
    <asp:XmlDataSource id="XmlDataSource" runat="server" DataFile="Hardware.xml" />
  </form>
</body>
</html>
```

要查看的第一项是 `<XmlDataSource>` 控件。它和 `<SiteMap>` 控件一样简单，但它使用 `DataFile` 属性指向 `Hardware.xml` 文件。

下一步是创建一个绑定此特定 XML 文件的 TreeView 控件。你可以直接为 XmlDataSource 控件创建一个默认 TreeView 控件，如下：

```asp
<asp:TreeView ID="TreeView1" runat="server" DataSourceID="XmlDataSource" />
```

通过这样做，图 14-11 显示了错误的结果。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_715_0.png)

图 14-11

如你所见，`TreeView` 控件正常绑定到 `Hardware.xml` 文件，但观察 Tree 控件内的节点，你可以发现它仅仅是在显示文件本身的 XML 元素名称。因为这不是你想要的，所以你通过 TreeView 控件内的 `<Bindings>` 元素指定如何绑定到 XML 文件。

`<Bindings>` 元素封装了一个或多个 `TreeNodeBinding` 对象。`TreeNodeBinding` 对象最重要的两个属性是 `DataMember` 和 `TextField` 属性。`DataMember` 属性指向 TreeView 控件应该查找的 XML 元素名称。`TextField` 属性指定 TreeView 在 XML 元素中查找的 XML 属性。如果你使用 `<Bindings>` 结构正确操作，你将得到图 14-12 所示的结果。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_716_0.png)

图 14-12

你也可以从列表 19-4 看到你可以覆盖 XML 文件根节点 `<Hardware>` 的类型，它将在 TreeView 控件中显示为 Computer Hardware，如下：

```asp
<asp:TreeNodeBinding DataMember="Hardware" Text="Computer Hardware" />
```

## 在 TreeView 中选择多个选项

如前所述，`TreeView` 控件并非旨在专门用于导航目的。你可以用它做各种事情。在许多情况下，你可能展示一个层级列表，并从中选择一个或多个项目。

`TreeView` 控件的一个很棒内置功能是在层级列表中的节点旁放置复选框。这些框允许用户进行多次选择。`TreeView` 控件包含一个名为 `ShowCheckBoxes` 的属性，用于在列表中的不同类型节点旁创建复选框。

# 第 14 章：站点导航

下表讨论了 `ShowCheckBoxes` 属性的可用值。

| 值 | 描述 |
| --- | --- |
| All | 对 `TreeView` 控件中的每一个节点应用复选框。 |
| Leaf | 仅对没有额外子元素的节点应用复选框。 |
| None | 对 `TreeView` 控件中的任何节点应用复选框。 |
| Parent | 仅对 `TreeView` 控件中视为父节点的节点应用复选框。父节点至少关联有一个子节点。 |
| Root | 对 `TreeView` 控件包含的任何根节点应用复选框。 |

在使用 `ShowCheckBoxes` 属性时，您可以像如下所示在控件本身中进行声明式设置：

```asp
<asp:TreeView ID="TreeView1" runat="server" Font-Underline="false"
    DataSource="XmlDataSource" ShowCheckBoxes="Leaf">
    ...
</asp:TreeView>
```

或者，您可以使用以下代码进行程序化设置：

```VB
TreeView1.ShowCheckBoxes = TreeNodeTypes.Leaf

C#
TreeView1.ShowCheckBoxes = TreeNodeTypes.Leaf;
```

关于在 `TreeView` 控件中使用复选框的示例，让我们继续扩展列表 14-9 中的计算机硬件示例。创建一个层次结构列表，允许人们从列表中选择多个项目以接收有关它们的更多信息。列表 14-10 显示了此类示例。

### 列表 14-10：在层次结构节点列表中叶子节点上应用复选框

```VB
<% Page Language="VB" %>

<script runat="server">
    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
        If TreeView1.CheckedNodes.Count > 0 Then
            Label1.Text = "We are sending you information on:<p>"
            For Each node As TreeNode In TreeView1.CheckedNodes
                Label1.Text += node.Text & " & " & node.Parent.Text & "<br>"
            Next
        Else
            Label1.Text = "You didn't select anything. Sorry!"
        End If
</script>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Latest Hardware</title>
</head>
<body>
<form runat="server">
Please select the items you are interested in:
<p>
<asp:TreeView ID="TreeView1" runat="server" Font-Underline="False"
DataSourceID="XmlDataSource" ShowCheckboxes="Leaf">
<DataBindings>
<asp:TreeNodeNode DataMember="Hardware"
Text="Computer Hardware" />
<asp:TreeNodeNode DataMember="Item" TextField="Category" />
<asp:TreeNodeNode DataMember="Option" TextField="Choice" />
</DataBindings>
</asp:TreeView>
<p>
<asp:Button ID="Button1" runat="server" Text="Submit Choices"
OnClick="Button1_Click" />
<asp:XmlDataSource ID="XmlDataSource" runat="server"
DataFile="Hardware.xml">
<asp:Label ID="Label" runat="Server" />
</form>
</body>
</html>
```

```csharp
@ Page Language="C#" %>

<script runat="server">
protected void Button1_Click(object sender, System.EventArgs e)
{
    if (TreeView1.CheckedNodes.Count > 0)
    {
        Label1.Text = "We are sending you information on:<p>";
        foreach (TreeNode node in TreeView1.CheckedNodes)
        {
            Label1.Text += node.Text + " " + node.Parent.Text + "<br>";
        }
    }
    else
    {
        Label1.Text = "You didn't select anything. Sorry!";
    }
}
</script>
```

在此示例中，您将 `ShowCheckBoxes` 属性 设置为 `Leaf`，这意味着您感兴趣为 `TreeView` 控件中不包含任何子节点的项目显示复选框。带有复选框的节点应该是层次结构列表中可以展开的最后一个项目。在设置此属性后，您在 `Button1_Click` 事件中处理用户选择的项。您首先应该检查的是是否进行了任何选择：

```csharp
if (TreeView1.CheckedNodes.Count > 0)
{
    ...
}
```

在这种情况下，回传时的选中节点数需要大于零，意味着至少选择了一个。如果是这样，您就可以执行 `If` 语句中的代码。为了从选中的节点填充 `Label` 控件的数据，您使用此处所示的 `For Each` 语句：

```VB
For Each node As TreeNode In TreeView1.CheckedNodes
    ...
Next
```

这适用于 `TreeNode` 对象的实例，并检查已选节点集合中的每个 `TreeNode`。对于每个被选中的节点，您获取此节点父节点的 `Text` 值来填充 `Label` 控件，如下所示：

```VB
Label1.Text += node.Text & " " & node.Parent.Text & "<br>"
```

在此处，您将获得图 14-13 所示的结果。

## 在 TreeView 控件中指定自定义图标

`TreeView` 控件允许高度自定义。您在章的早些部分已经看到，可以通过指定内置样式来轻松地自定义 `TreeView` 控件的外观和感受。应用这些样式之一可以极大地改变控件的样式。带有复选框的节点应该是层次结构列表中可以展开的最后一个项目。在设置此属性后，您在 `Button1_Click` 事件中处理用户选择的项。`TreeView` 包含了下表所示的属性，您可以指定自定义图标来用于节点。

![](img/54f286ad47e89bbf83ee2d279e6dd_720.png)

图 14-13

| 属性 | 描述 |
| --- | --- |
| CollapseImageUrl | 对已展开的节点应用自定义图标以显示其子节点。 |
| ExpandImageUrl | 对可以展开的节点应用自定义图标。 |
