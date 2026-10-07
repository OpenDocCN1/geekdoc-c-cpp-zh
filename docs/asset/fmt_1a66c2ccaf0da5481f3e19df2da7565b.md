
像 `Checkbox` 一样，`RadioButton` 控件有一个 `Changed` 事件，它在控件中放置了一个 `OnCheckedChanged` 属性。该属性的值指向当使用表单上的两个单选按钮之一进行选择时触发的服务器端事件。记住，需要将 `AutoPostBack` 属性设置为 `True` 才能生效。

图 3-19 显示了结果。

![](img/7040c21013b8e6c23c612d6da3599ff8_167_0.png)

图 3-19

`RadioButton` 控件相比 `RadioButtonList`（接下来将讨论）具有的一个优势是，它允许你在 `RadioButton` 控件本身之间放置其他项（文本、控件或图像）。然而，`RadioButtonList` 是你 Web 页面上单一的单选按钮列表。

## RADIOBUTTONLIST 服务器控件

`RadioButtonList` 控件在 Web 页面上显示一组单选按钮。`RadioButtonList` 与 `CheckBox` 以及其他控件非常相似，它允许你遍历用户选择的内容、进行计数或执行其他操作。典型的 `RadioButtonList` 控件以以下方式写入页面：

```xml
<asp:RadioButtonList ID="RadioButtonList" runat="server">
  <ListItem Selected="True">English</ListItem>
  <ListItem>Russian</ListItem>
  <ListItem>Finnish</ListItem>
</asp:RadioButtonList>
```

与其他控件一样，它为集合中的每个项使用 `ListItem` 对象的实例。从示例可以看出，当页面首次生成时，其中一个 `ListItem` 对象被设置为 `True`。这产生了图 3-20 的结果。`Selected` 属性不是必须的，如果你希望用户从集合中进行某些选择，这是一个好主意。你可以使用 `RadioButton` 控件来检查用户在页面任何部分选择的值。列表 3-16 显示了在 `RadioButtonList` 中选择值的 `Button_Click` 事件。

| English |
| Russian |
| Finnish |
| Swedish |

## IMAGE 服务器控件

服务器控件允许你从服务器显示 Web 页面上的图像。这是一个服务器控件，但它可以控制图像在浏览器上的显示。`Image` 控件按以下方式构造：

```xml
<asp:Image ID="Image1" runat="server" Url="~/MyImage.gif" />
```

重要的属性是 `ImageUrl`。它指向图像的文件。在这种情况下，位置由 `ImageUrl` 指定。列表 3-17 显示了动态更改 `ImageUrl` 的示例。

### 3-17：更改 ImageUrl

```vb
<%@ Page Language="VB" %>
<script runat="server">
    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
        Image1.ImageUrl = "~/MyImage.gif"
    End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Image control</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:Image ID="Image1" runat="server" Url="~/MyImage.gif" /><br />
            <asp:Button ID="Button1" runat="server" Text="Change Image" OnClick="Button1_Click" />
        </div>
    </form>
</body>
</html>
```

在此示例中，当页面首次加载时，浏览器会显示图像 (`MyImage1.gif`)。当最终用户点击按钮时，在回回过程中加载了新图像 (`MyImage2.gif`)。

特殊情况可能会防止用户查看其 Web 页面的一部分的图像。他们可能是物理上无法或使用纯文本浏览器。在这些情况下，浏览器会寻找 `<img>` 元素的 `longdesc` 属性，指向显示图像的详细描述。

对于这些情况，`Image` 控件包含了 `DescriptionUrl` 属性。分配给它的值是一个包含关联图像描述的文件。使用方法如下：

```xml
<asp:Image ID="Image" runat="server" DescriptionUrl="/Image01.txt" />
```

此代码产生如下结果：

```html
<img id="image" src="IMAGE.jpg" longdesc="Image01.txt" alt="" />
```

记住图像不支持点击。如果要根据点击编写事件，请使用本节之前讨论的 `Button` 服务器控件。

## TABLE 服务器

表格是 Web 页面常用的元素之一，因为 HTML `<table>` 元素是控制 Web 页面布局的可能格式之一（另一种是 CSS）。`Table` 控件的典型结构如下：

```xml
<asp:Table ID="Table" runat="server">
    <asp:TableRow runat="server" Font-Bold="True" ForeColor="Black" BackColor="Silver">
        <asp:TableHeaderCell>First</asp:TableHeaderCell>
        <asp:TableHeaderCell>Last</asp:TableHeaderCell>
    </asp:TableRow>
    <asp:TableRow>
        <asp:TableCellCell>Bill</asp:TableCellCell>
        <asp:TableCellCell>Evjen</asp:TableCellCell>
    </asp:TableRow>
    <asp:TableRow>
        <asp:TableCellCell>Devin</asp:TableCellCell>
        <asp:TableCellCell>Rader</asp:TableCellCell>
    </asp:TableRow>
</asp:Table>
```

这产生了图 3-21 所示的三行表格。你可以使用 `Table` 服务器控件来实现。例如，你可以动态向表格中添加行，如列表 3-18 所示。

### 3-18：动态向表格添加行

```vb
<%@ Page Language="VB" %>
<script runat="server">
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.Events)
    Dim tr As New TableRow
</script>
```

```vb
Dim fname As New TableCell()
fname.Text = 'Scott'
tr.Cells.Add(fname)
Dim lname As New TableCell()
lname.Text = 'Hanselmen'
tr.Cells.Add(lname)
Table.Rows.Add(tr)
```

# 表格服务器控件

结束

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    TableRow tr = new TableRow();
    TableCell fname = new TableCell();
    fname.Text = "Scott";
    tr.Cells.Add(fname);
    TableCell lname = new TableCell();
    lname.Text = "Hanseman";
    tr.Cells.Add(lname);
    TableRow.Rows.Add(tr);
}
```

要向表格控件添加行，你必须创建 `TableRow` 和 `TableCell` 对象的新实例。先创建 `TableCell` 对象，然后将它们放置在添加到 `Table` 对象的 `TableRow` 对象中。

该服务器控件包含了一些超出介绍之外的功能。其中一个较简单的功能是在网页上添加标题（captions）。图 3-22 显示了一个带有标题的表格。

![](img/7040c21013b8e6c23c612d6da3599ff8_170_0.png)

图 3-22

要为表格添加标题，只需在 `Table` 控件中使用 `Caption` 属性，如代码列表 3-19 所示。

> 代码列表 3-19：使用 Caption 属性

```asp
<@ Page Language="VB" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Table Server Control</title>
</head>
<body>
<form id="form" runat="server">
  <asp:Table Id="Table" runat="server">
    <Caption Caption="Table 1: 这是一个表格上方标题的示例.*"></Caption>
    BackColor="Gainsboro"
    <asp:TableRow Id="TableRow1" Runat="server">
      <asp:TableCell Id="TableCell1" Runat="server">Lorem ipsum dolor sit
      amet, consectetur adipiscing elit. Duis well jest place. Aliquam
```

# 代码列表 3-19（续）

```
adipiscing. In mattis volutpat urna. Donec nisel eget dictum egestas, felis nulla ornare ligula, ut bibendum neque augue semper. Sed risus nec urna pharetra imperdiet. Aenean nec nibh. Sed vel ullamcorper auctor a sapien. Suspendisse luctus. Ut ac nibh. Lorem aliquam dictum aliquus mauris.</</asp:TableCell>
</asp:TableRow>
</asp:Table>
</form>
</body>
</html>
```

默认情况下，日历位于表格的顶部中央，但你可以使用另一个属性——`Caption` 来控制它的位置。可能的设置包括 `Bottom`（底部）、`Left`（左侧）、`NotSet`（未设置）、`Right`（右侧）和 `Top`（顶部）。

在 ASP.NET 的早期阶段，`<asp:Table>` 元素包含任意数量的 `<asp:TableRow>` 元素。在 ASP.NET 4 中，你可以在 `<asp:Table>` 元素内嵌套一些额外的元素。这些元素包括 `<asp:TableHeaderRow>` 和 `<asp:TableFooterRow>`。它们为你的表格添加表头或页脚，使能够使用服务器控件解析数据日志，同时仍保留文本以指示正在处理的日期类型。当你处理移动应用程序时，这是一个非常强大的功能，因为用户有时一次只能浏览几条记录。

# 日历服务器控件

日历服务器控件是一个功能丰富的控件，它允许你直接在 Web 页面上放置一个功能齐全的日历。它支持高度自定义，以确保其外观和行为具有独特性。日历控件在在最简单形式下的代码如下：

```asp
<asp:Calendar ID="Calendar1" runat="server" />
```

此代码会在你的 Web 页面上生成一个日历，不添加任何样式，如图 3-23 所示。

![](img/7040c21013b8e6c23c612d6da3599ff8_171_0.png)

# 从日历控件中选择

日历允许你浏览全年的月份，并在显示的月份中选择特定日期。代码列表 3-20 显示了一个允许用户选择月份中某一天日期的简单应用程序。

# 代码列表 3-20：在日历控件中选择单日

```vb
<@ Page Language="VB" %>
<script runat="server">
Protected Sub Calendar1_SelectionChanged(ByVal sender As Object, ByVal EventArgs As System.EventArgs)
    Response.Write("Selected: " & 
    Calendar1.SelectedDate.ToString())
End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
```

![](img/7040c21013b8e6c23c612d6da3599ff8_171_1.png)

```html
<head id="Head1" runat="server">
<title>Using the Calendar Control</title>
</head>
<body>
  <form id="form1" runat="server">
    <div>
      <asp:Calendar ID="Calendar1" runat="server"
      OnSelectionChanged="Calendar1_SelectionChanged">
      </asp:Calendar>
    </div>
  </form>
</body>
</html>
```

```csharp
<@ Page Language="C#" %>
<script runat="server">
    protected void Calendar1_SelectionChanged(object sender, EventArgs e)
    {
        Response.Write("Selected: " +
        Calendar1.SelectedDate.ToString());
    }
</script>
```

# 选择日、周或月份

默认情况下，日历控件允许用户选择日期，但你可以通过 `SelectionMode` 属性更改选择行为。可选值包括 `Day`（日）、`Week`（周）和 `Month`（月）。

# 116 | 第 3 章 ASP.NET Web 服务器控件

![](img/7040c21013b8e6c23c612d6da3599ff8_175_0.png)

图 3-26

你可以使用以下代码获取选择中的第一天：

```VB
Calendar.SelectedDates.Item(0).ToShortDateString()
```

你可以使用以下代码获取选择中的最后一个日期：

```VB
Calendar.SelectedDates.Item(Calendar.SelectedDates.Count-1).ToShortDateString();
```

如你所见，通过使用 `SelectedDates` 对象的 `Count` 属性可以实现这一点。

# 修改日历控件的样式和行为

日历控件有很多功能——超出了本章的涵盖范围。日历控件的一个很棒的特性是它提供的扩展性。我们可以通过查看更改它最简单的方法之一——为控件应用样式，来探索进一步自定义它的新方法。

使用 Visual Studio，你可以从正在处理的页面的设计视图（Design view）中为控件赋予全新的外观。高亮日历控件并打开控件的智能标签（smart tag），查看“自动格式”（Auto Format）链接。这将为你提供一个可以应用到日历控件的样式列表。

> 日历控件在这一功能上并非孤例。许多其他富控件也提供了样式列表。你始终可以在控件的智能标签中找到此功能。

图 3-27 显示了其中一些样式。

# 日历服务器控件

![](img/7040c21013b8e6c23c612d6da3599ff8_176_0.png)

图 3-27

除了更改日历控件的样式外，你还可以在其渲染过程中与控件进行交互。日历控件包含一个 `DayRender` 事件，它允许你控制单个日期或日历中所有日期的渲染方式。列表 3-22 显示了如何更改日历中渲染的其中一个日期的示例。

# 列表 3-22：控制日历中天的渲染方式

```vb
<% Page Language="VB" %>
<script runat="server">
Protected Sub Calendar_DayRender(ByVal sender As Object,
ByVal e As System.Web.Controls.DayRenderEventArgs)
e.Cell.VerticalAlignment = VerticalTop
```
