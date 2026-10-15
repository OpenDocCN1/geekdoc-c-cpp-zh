

## 使用 SiteMapPath 控件进行数据检索

SiteMapPath 控件使用 SiteMapProvider 获取数据并在 Web 表单上显示。如您之前所见，Menu 和 TreeView 控件都依赖于 SiteMapDataSource 控件。SiteMapPath 控件仅显示在指定的 SiteMapProvider 中存在其 URL 的数据。您应始终检查 Web.sitemap 文件中没有输入错误；否则，SiteMapProvider 将无法显示所需输出。

## SiteMapPath 行为

SiteMapPath 控件显示各种常用属性以更改显示行为。表 15.10 列出了 SiteMapPath 类的值得注意的属性，用于更改显示行为：

| Table 15.10: Noteworthy Properties of the SiteMapPath Class |
| Property | Description |
| ParentLevelsDisplayed | 默认设置为 -1，表示显示 XML 文件中的所有父级。您可以将其设置为任意整数值，例如 1、2 或 3，以指示沿当前页面的 N 级层次结构。 |
| PathDirection | 指定导航路径节点的渲染顺序。默认设置是从当前 XML 文件中的最高节点开始，直到当前页面。通过设置此属性，链接将以相反方向显示，这意味着节点将从当前页面开始显示，结束于根页面或第一页。 |
| PathSeparator | 将此属性设置为 :（分号）作为路径分隔符。其默认值是 >。 |
| RenderCurrentNodeAsLink | 将此属性设置为 true，以便 Web 页面上的当前节点文本将显示为超链接而不是纯文本。 |
| ShowToolTips | 将此属性设置为 false，以便 SiteMapProvider 控件中的描述文本不会自动显示。 |

## SiteMapPath 样式

您可以设置 SiteMapPath 控件可用的不同样式属性。以下是可用于设置 SiteMapPath 控件样式的属性列表：

- NodeStyle – 用于控制 SiteMapPath 控件显示的所有节点的文本外观。默认显示文本为 SiteMapNode 的 Title 属性中指定的文本。
- CurrentNodeStyle – 用于设置对应于当前显示 Web 页面的节点的属性。CurrentNodeStyle 属性通常与标准 Web 控件样式属性和 NodeStyle 属性合并。
- RootNodeStyle – 用于设置 SiteMapProvider 控件层次结构中绝对根的样式。根据当前页面上存在的层次结构级别，RootNodeStyle 可能不会显示在您网站的每个页面上。它与 NodeStyle 属性和标准 Web 控件样式属性合并。
- PathSeparatorStyle – 用于控制出现在导航路径节点之间的路径分隔符的外观。PathSeparatorStyle 与标准 Web 控件样式属性合并。

> NOTE
> 您可以通过其样式属性设置 SiteMapPath 控件的外观。您也可以使用皮肤和主题文件来设置外观。

## SiteMapPath 模板

除了前面讨论的样式属性外，SiteMapPath 控件还提供模板，可用于更灵活地设置控件的视图。模板控制控件特定部分的 HTML 渲染。请注意，如果您为特定节点定义了模板，它将覆盖为该节点之前定义的样式设置。要设置 SiteMapPath 控件的外观，您可以使用以下模板：

- NodeTemplate—应用于层次结构中的所有节点，无论其节点类型如何。
- CurrentNodeTemplate—设置对应于当前显示页面的节点的外观。CurrentNodeTemplate 优先于 NodeTemplate。
- RootNodeTemplate—设置站点层次结构根节点的外观。RootNodeTemplate 优先于 NodeTemplate 和 CurrentNodeTemplate。这意味着如果当前页面根据站点层次结构是根页面，则仅对根节点使用 RootNodeTemplate。
- PathSeparatorTemplate—用于在当前在 Web 页面上渲染的节点之间用分隔符分隔节点。它替换应用程序中 PathSeparator 文本值。

## 立即可用的解决方案

## 创建 TreeView 控件

TreeView 控件可以在 Visual Studio 2010（VS 2010）中轻松创建。为此，只需将控件拖放到 Web 页面上即可。TreeView 控件在 VS 2010 的工具箱中的导航选项卡下可用。

> NOTE
> 本章中的应用程序使用“新建网站”对话框中的 ASP.NET 空 Web 站点模板创建。创建应用程序后，您需要向应用程序添加 Default.aspx 页面。

我们在本章 In Depth 部分讨论的 CD-ROM 上的 TreeViewControlCS 示例中使用了 TreeView 控件。您可以在列表 15.1 中找到 Default.aspx 页面的代码：

### Listing 15.1: Showing the Code for the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Treeview Control Example</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="Label1" runat="server" Text="Static TreeView" Font-Bold="true" Font-Size="Medium"></asp:Label>
<asp:TreeView ID="TreeView1" runat="server">
<Nodes>
<asp:TreeNode Text="Navigate" Value="Navigate">
<asp:TreeNode Text="Simple TreeView" Value="Simple TreeView" NavigateUrl="~/SimpleTreeView.aspx"></asp:TreeNode>
<asp:TreeNode Text="Treeview from Database" Value="Treeview from Database" NavigateUrl="~/TreeviewDatabase.aspx">
</asp:TreeNode>
<asp:TreeNode Text="TreeView with XmlDataSource" Value="TreeView with XmlDataSource" NavigateUrl="~/TreeviewXMLData.aspx"></asp:TreeNode>
<asp:TreeNode Text="TreeView with SiteMapDataSource" Value="TreeView with SiteMapDataSource" NavigateUrl="~/TreeviewSiteMapDataSource.aspx"></asp:TreeNode>
</asp:TreeNode>
</Nodes>
</asp:TreeView>
</div>
</form>
</body>
</html>
```

在前面的列表中可以看到，我们在 Web 页面上放置了一个 TreeView 控件。它包含此应用程序的导航结构。前一个列表的输出如图所示 15.6：

## Chapter 15: Navigation Controls in ASP.NET 4.0

![](img/e073a4882197be4ab61103cbe0bcb394_761_0.png)

要在设计时添加 TreeView 控件的节点，请从 TreeView 控件的智能标记中选择 Edit Nodes 选项。一旦您单击 Edit Node 选项，TreeView Node Editor 对话框就会出现（之前在图 15.3 中显示）。

您现在可以通过单击 TreeView Node Editor 对话框工具栏上的 Add a root node 按钮来添加节点，如图 15.7 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_761_1.png)

您现在可以通过单击第一个按钮（Add a root node）添加根或父节点，并通过单击第二个按钮（Add a child node）添加子节点。在属性面板下为节点设置 Text 属性。创建应用程序的导航结构后，我们创建了六个不同的 TreeView 控件，每个控件都有不同的格式样式。为此，我们添加了一个新页面，即应用程序的 SimpleTreeView.aspx 页面。您可以在列表 15.2 中找到 TreeViewControl 应用程序的 SimpleTreeView.aspx 页面的代码。

### Listing 15.2: Showing the Code for the SimpleTreeView.aspx Page

```
```aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="SimpleTreeView.aspx.cs" Inherits="SimpleTreeView" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```

