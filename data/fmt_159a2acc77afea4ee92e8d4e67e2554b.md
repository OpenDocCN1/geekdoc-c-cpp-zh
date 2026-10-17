
关闭换行可能会导致水平滚动条开启（取决于面板区域中包含的内容）。

如果你不希望 ASP 引擎选择，你可以通过使用 `ScrollBars` 属性来实现这一点。除了 `Auto`，它的值还包括 `None` 和 `Vertical`。另一个属性是 `HorizontalAlign`。

如图 30 所示，单一的垂直滚动条已添加到 300 x 300 像素的设定区域。`Panel` 控件默认根据需要封装文本。要更改此行为，请使用 `Wrap` 属性，它具有布尔值：

```asp
<asp:Panel ID="Panel" runat="server"
Height="300" Width="300" ScrollBars="Auto"
Wrap="False" />
```

关闭换行可能会导致水平滚动条开启（取决于面板区域中包含的内容）。

如果你不希望 ASP 引擎选择，你可以通过使用 `ScrollBars` 属性来实现这一点。除了 `Auto`，它的值还包括 `None` 和 `Vertical`。另一个属性是 `HorizontalAlign`。

如图 30 所示，单一的垂直滚动条已添加到 300 x 300 像素的设定区域。`Panel` 控件默认根据需要封装文本。要更改此行为，请使用 `Wrap` 属性，它具有布尔值：

```asp
<asp:Panel ID="Panel" runat="server"
Height="300" Width="300" ScrollBars="Auto"
Wrap="False" />
```

dictum egestas, felis nulla ligura, ut bibendum peende eu auge. Sed vel risus nec uha phareet interdiet. Aenean semper. Sed ullamcorper auctor sapien. Suspendisse. Luct et ac nibh. Namam lorem. dictum aliquus purus.

```html
</form>
<body>
</html>
```

该示例展示了 XML 广告中指定的广告，它显示为页面顶部的横幅。

你不需要将所有的广告管理内容都放在 XML 广告中。相反，你可以使用另一个数据源并在该源上绑定 `AdRelator`。例如，你可以将 `AdRelator` 绑定到 `SqlDataSource` 对象，以便按照如下方式从 SQL Server 获取广告：

```asp
<AdRelator ID="AdRelator" runat="server"
DataSource="SqlDataSource" AlternateTextField="AlternateTF"
ImageUrlField="NavigateUrl" NavigateUrlFields=" />
```

`AlternateTextField`、`ImageUrlField` 和 `NavigateUrlFields` 指向 SQL Server 中用于这些内容的列名。

# XML 服务器控件

`XML` 服务器控件提供了一种获取 XML 并将其转换为 XSL 表格的方法。`XML` 控件可以通过两种方式与你的 XML 配合。最简单的方法是使用列表 3-25 中的结构。这将在第 10 章中详细介绍。

# 列表 3-25：显示 XML 文档

```asp
<Xml ID="Xml" runat="server" DocumentSource="~/MyXMLFile.xml"
TransformSource="MyXSLFile.xslt" /></asp:Xml>
```

该方法使用了几个属性来实现功能：`DocumentSource` 指 XML 文件的路径，`TransformSource` 提供在转换 XML 文档时使用的 XSL 文件。

使用 XML 服务器控件的另一种方法是将 XML 加载到对象并将对象传递给 XML 控件，如列表 3-26 所示。

# 列表 3-26：在提供给 XML 控件之前将 XML 加载到对象

| VB | C# |
| :--- | :--- |
| `Dim MyXmlDoc As XmlDocument = New XmlDocument()`<br>`MyXmlDoc.Load(Server.MapPath("Customers.xml"))`<br>`Dim MyXmlDoc As XslCompiledTransform = New XslCompiledTransform()`<br>`MyXmlDoc.Load(Server.MapPath("CustomersSchema.xslt"))`<br>`Xml.Document = MyXmlDoc`<br>`Xml.Transform = MyXmlDoc;` | `XmlDocument MyXmlDoc = new XmlDocument();`<br>`MyXmlDoc.Load(Server.MapPath("Customers.xml"));`<br>`XslCompiledTransform MyXmlDoc = new XslCompiledTransform();`<br>`MyXmlDoc.Load(Server.MapPath("CustomersSchema.xslt"));`<br>`Xml.Document = MyXmlDoc;`<br>`Xml.Transform = MyXmlDoc;` |

为了使此项生效，你必须确保在页面中导入了 `System.Xml` 和 `System.Xml.Xsl` 命名空间。示例同时加载了 XML 和 XSL 文件，并将这些文件赋值为 `Document` 和 `Transform` 属性的值。

# PANEL 服务器控件

`Panel` 控件封装了一组的控件，你可以使用这些控件来操作或布局你的 ASP.NET 页面。它本质上是其他控件的包装器，允许你与其他元素（如 HTML 和图像）一起管理一组控件，然后将它们转换为单个单元。

使用 `Panel` 控件封装一组其他元素的优势在于，你可以通过使用 `Panel` 控件本身的一个属性将这些元素作为一个单元进行操作。将 `Font-Bold` 属性设置为 `True` 会导致 `Panel` 控件内的每个项目都采用此属性。

`Panel` 控件还具有带有滚动条滚动的能力，滚动条会根据 `Panel` 包含的信息量自动出现。你甚至可以指定滚动条如何显示。

关于滚动条的示例，请查看 Lorem 文本（位于 `www.lipsum.com`）并将该文本放置在 `Panel` 控件中，如列表 3-27 所示。

# 列表 3-27：在 Panel 服务器控件中使用滚动条功能

```asp
<@ Page Language="VB" %>
<html>
<head>
runat="server">
<title>Panel Server Control Page</title>
</head>
<body>
<form id="form" runat="server">
<asp:Panel ID="Panel" runat="server" Height="300" Width="300"
ScrollBars="auto">
<p>Lorem ipsum dolor sit amet...</p>
</asp:Panel>
</form>
</body>
</html>
```

通过为 `Panel` 服务器控件分配 `Height` 和 `Width` 属性并使用 `ScrollBars` 属性（在此情况下设置为 `Auto`），你可以使用滚动条显示定义区域内包含的信息（图 3-29）。

![](img/7040c21013b8e6c23c612d6da3599ff8_181_0.png)

图 3-29

如你所见，单一的垂直滚动条已添加到 300 x 300 像素的设定区域。`Panel` 控件默认根据需要封装文本。要更改此行为，请使用 `Wrap` 属性，它具有布尔值：

```asp
<asp:Panel ID="Panel" runat="server"
Height="300" Width="300" ScrollBars="Auto"
Wrap="False" />
```

关闭换行可能会导致水平滚动条开启（取决于面板区域中包含的内容）。

如果你不希望 ASP 引擎选择，你可以通过使用 `ScrollBars` 属性来实现这一点。除了 `Auto`，它的值还包括 `None` 和 `Vertical`。另一个属性是 `HorizontalAlign`。

如图 30 所示，单一的垂直滚动条已添加到 300 x 300 像素的设定区域。`Panel` 控件默认根据需要封装文本。要更改此行为，请使用 `Wrap` 属性，它具有布尔值：

# PLACEHOLDER 服务器控件

`Placeholder` 控件的工作正如其名称所示——它是你向页面注入对象的占位符。

要查看它如何工作，在页面中插入 `Placeholder` 控件，并从服务器端代码向其添加控件，如列表 3-28 所示。

```
LISTING 3-28: 使用 Placeholder 向页面添加控件
VB
Dim NewLabelControl As NewLabel()
NewLabelControl.Text = "Hello there"
Placeholder.Add(NewLabelControl)

C#
Label NewLabelControl = new Label();
NewLabelControl.Text = "Hello there";
Placeholder.Add(NewLabelControl);
```

此示例创建了一个新的标签实例，并在添加到 `Placeholder` 之前对其填充值。你可以为单个 `Placeholder` 实例添加多个控件。

# BULLETEDLIST 服务器控件

常见的 HTML 页面是列表项目的集合。`BulletedList` 服务器控件用于以以序（HTML `<ol>`）或无序（HTML `<ul>`）的方式显示列表。此外，控件可以决定你用于列表的样式。

`BulletedList` 可以由任意数量的 `<asp:ListItem>` 控件组成，也可以绑定到某种数据源并根据检索的内容进行填充。列表 3-29 显示了最简单形式的项目符号列表。

# 列表 3-29：简单的 BulletedList 控件

```asp
<@ xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>BulletedList Server Control</title>
</head>
<body>
<form id="form" runat="server">
<asp:BulletedList id="ListItem1">
<asp:ListItem Text="United States"/></asp:ListItem>
<asp:ListItem Text="United Kingdom"/></asp:ListItem>
<asp:ListItem Text="Finland"/></asp:ListItem>
<asp:ListItem Text="Russia"/></asp:ListItem>
<asp:ListItem Text="Sweden"/></asp:ListItem>
<asp:ListItem Text="Estonia"/></asp:ListItem>
</asp:BulletedList>
</form>
</body>
</html>
```

使用 `<asp:BulletedList>` 元素结合 `<asp:ListItem>` 元素会产生像图 3-32 所示的简单项目符号列表。

## BulletedList 服务器控件

![](img/7040c21013b8e6c23c612d6da3599ff8_184_0.png)

图 3-32

`BulletedList` 控制还允许你轻松更改列表每行之前的项目符号样式。它的可能值包括：`Numbered`（数字）、`LowerAlpha`（小写字母）、`UpperAlpha`（大写字母）、`LowerRoman`（小写罗马数字）、`UpperRoman`（大写罗马数字）、`Disc`（实圆）、`Circle`（圆）、`Square`（正方形）、`Not`（无）和 `CustomImage`（自定义图像）。图 3-33 显示这些样式的示例（不包含可以使用任意图像的 `CustomImage` 设置）。

![](img/7040c21013b8e6c23c612d6da3599ff8_184_1.png)

图 3-33

你可以通过 `FirstBulletNumber` 属性更改任何编号样式（`Numbered`, `LowerAlpha`, `UpperAlpha`, `LowerRoman`, `UpperRoman`）中第一个项目的起始值。例如，当你使用 `UpperRoman` 设置并将该属性的值设置为 5 时，你将得到图 3-34 所示的格式。

![](img/7040c21013b8e6c23c612d6da3599ff8_185_0.png)

图 3-34

要使用图像作为项目符号，请使用 `BulletedList` 控制中的 `CustomImage` 设置。你还必须以下方式使用 `BulletImageUrl` 属性：

```asp
<asp:BulletedList ID="Bulletedlist" runat="server"
    BulletStyle="Custom" BulletImageUrl="~/myImage.gif">
```

图 3-35 显示了图像符号的示例。

![](img/7040c21013b8e6c23c612d6da3599ff8_185_1.png)

图 3-35

`BulletedList` 控制有一个 `DisplayMode` 属性，它三个可能的值：`Text`（文本）、`HyperLink`（超链接）和 `LinkButton`（链接按钮）。默认值是 `Text`，并在之前的示例中一直使用它。使用 `Text` 意味着项目列表中的项目以项目符号的形式列出。`HyperLink` 意味着每个项目都转换为超链接——用户点击任何项都会被重定向到另一个页面，该页面由 `<asp:bulletedlist>` 的 `Value` 属性指定。`LinkButton` 值则将每个项目列表项转换为指向相同页面的超链接。它允许你检索用户所做的选择，如代码列表 3-30 所示。

### 代码列表 3-30：为 DisplayMode 属性使用 LinkButton 值

```vb
<%@ Page Language="server" %>
<script runat="server">
    Protected Sub BulletedList_Click(ByVal sender As Object,
        ByVal e As System.Web.UI.Controls.BulletedListEventArgs)
        Label1.Text = "所选项目的索引为: * " & e.Index & _
            "<br>所选项目的值: " & _
            BulletedList.Items(e.Index).Text
    End Sub
</script>
```

## BulletedList 服务器控件

```html
</script>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
  <title>BulletedList 服务器控件</title>
</head>
<body>
  <form id="form" runat="server">
    <asp:BulletedList Id="BulletedList1" runat="server"
      OnClick="BulletedList_Click" DisplayMode="LinkButton">
      <asp:ListItem Text="美国"</asp:ListItem>
      <asp:ListItem Text="英国"</asp:ListItem>
      <asp:ListItem Text="芬兰"</asp:ListItem>
      <asp:ListItem Text="俄罗斯"</asp:ListItem>
      <asp:ListItem Text="瑞典"</asp:ListItem>
      <asp:ListItem Text="爱斯陶尼亚"</asp:ListItem>
    </asp:BulletedList>
    <asp:Label ID="Label1" runat="server"></asp:Label>
  </form>
</body>
</html>
```

```csharp
// Page Language:"C#"
<script runat="server">
  protected void BulletedList_Click(object sender, System.Web.UI.Controls.BulletedListEventArgs e)
  {
    Label.Text = "所选项目的索引: " + e.Index +
    "<br>所选项目的值: " +
    BulletedList.Items[e.Index].Text;
  }
</script>
```

在此示例中，`DisplayMode` 属性设置为 `LinkButton`，`OnClick` 属性指向 `BulletedList_Click`。`BulletedList_Click` 使用 `BulletedListEventArgs` 对象，它仅暴露 `Index` 属性。通过它你可以确定所选项目的索引。

你可以通过 `Items` 属性直接获取选中项目的值，或者可以使用该属性获取 `ListItem` 对象，如下：
