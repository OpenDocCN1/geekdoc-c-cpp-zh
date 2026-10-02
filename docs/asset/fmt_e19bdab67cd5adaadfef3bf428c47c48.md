
<asp:ListItem Value="NET 4.5"/></asp:ListItem>

<asp:ListItem Value="ASP.NET MVC 4"/></asp:ListItem>

<asp:ListItem Value="jQuery 1.8.x"/></asp:ListItem>

<asp:ListItem Value="Visual Studio 2012"/></asp:ListItem>

</asp:ListBox>

<br />

<asp:Button ID="Button2" runat="server" Text="Submit" OnClick="Button2_Click" /> <br />

<asp:Label ID="Label1" runat="server"></asp:Label>

</div>

</form>

</body>

</html>

# C#

这是一个有趣的示例。首先，`ListBox` 控件中已经放置了一些默认项目（四种 ASP.NET 开发中常用的产品）。然而，表单顶部的文本框和按钮允许用户向列表添加产品。用户随后对 `ListBox` 进行一次或多次选择，包括对动态添加的项目进行选择。当用户做出选择并点击按钮后，`Button2_Click` 事件将遍历集合中的 `ListItem` 实例，并仅显示被选中的项目。

该控件通过创建 `ListItem` 对象的实例，并在集合中的特定项目被选中时使用其 `Selected` 属性来工作。`ListItem` 对象的使用不仅限于 `ListBox`。

![](img/67a6707ff505c052edb96c0128fb3096_192_0.png)

图 5-13

# 如何确定复选框是否被选中

你可能不想使用复选框的 `AutoPostBack` 功能，而是希望在回传到服务器后确定复选框是否被勾选。你可以通过 `If Then` 语句进行此检查，如下例所示：

```VB
If (Checkbox1.Checked = True) Then
    Response.Write("Thanks for your donation!")
End If
```

```csharp
if (Checkbox1.Checked == true)
{
    Response.Write("Thanks for your donation!");
}
```

此检查是通过控件的 `Checked` 属性对 `CheckBox` 值执行的。该属性的值是一个布尔值，因此是 `True`（已选中）或 `False`（未选中）。

> 注意：在 Visual Basic 和 C# 中，你可以省略对真值的显式检查，直接调用以下代码即可（此处用 C# 所示）：`if (Checkbox1.Checked) ...`

# 给复选框赋值

你也可以使用 `Checked` 属性，根据其他动态值来确保复选框被勾选：

```VB
If (Member = True) Then
    Checkbox1.Checked = True
End If
```

```csharp
if (Member == true)
{
    Checkbox1.Checked = true;
}
```

# 在复选框周围对齐文本

在之前的复选框示例中，文本出现在实际复选框的右侧，如图 5-14 所示。

使用 `CheckBox` 的 `TextAlign` 属性，你可以对齐文本，使其显示在复选框的另一侧：

```xml
<asp:CheckBox ID="Checkbox1" runat="server" Text="Donate $10 to my cause!" CheckedChanged="CheckBox1_CheckedChanged" AutoPostBack="true" TextAlign="Left" />
```

`TextAlign` 的可能值为 `Right`（默认设置）和 `Left`（左侧）。此属性也适用于 `CheckListBox`、`RadioButton` 和 `RadioButtonList` 控件。分配该值将产生图 5-15 所示的结果。

![](img/67a6707ff505c052edb96c0128fb3096_193_0.png)
![](img/67a6707ff505c052edb96c0128fb3096_193_1.png)

# CHECKBOXLIST 服务器控件

`CheckListBox` 服务器控件与 `CheckBox` 控件类似，区别在于前者允许你处理项目集合而不是单个项目。其设计思想是 `CheckListBox` 实例是相关项的集合，每个项本身都是一个复选框。

要查看 `CheckListBox` 控件的操作，你可以构建一个示例，使用 Microsoft 的 SQL Server 从 `AdventureWorks` 数据库的 `Customer` 表中提取信息。列表 5-14 提供了一个示例。

> 你可以从 www.wgra.com/SQLServer2012DataSets 下载我们为本书使用的 `AdventureWorks` 数据库版本。

列表 5-14：动态填充 `CheckListBox`

```vb
<%@ Page Language="VB" %>
<!DOCTYPE html>
<script runat="server">
Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
    Label1.Text = "You selected:<br>"
    For Each i1 As ListItem In CheckListBox.Items
        If i1.Selected Then
            Label1.Text &= i1.Text & "<br>"
        End If
    Next
End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head" runat="server">
<title>CheckListBox control</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Button ID="Button1" runat="server" Text="Choices" OnClick="Button1_Click" /><br />
<br />
<asp:Label ID="Label1" runat="server"></asp:Label>
<br />
<asp:CheckBoxList ID="CheckBoxList1" runat="server" DataSource="SqlDataSource" DataField="CompanyName" RepeatColumns="3" BorderColor="Black" BorderStyle="Solid" BorderWidth="1px">
</asp:CheckBoxList>
<asp:SqlDataSource ID="SqlDataSource" runat="server" SelectCommand="SELECT DISTINCT TOP 12 [CompanyName] FROM [SalesLT].[Customer] ORDER BY [CompanyName]" ConnectionStrings="<%# ConnectionStrings:AdventureWorksConnectionString %>">
</asp:SqlDataSource>
</div>
</form>
</body>
</html>
```

# CheckBoxList 控件

```xml
<asp:Button ID="Button1" runat="server" Text="Choices" OnClick="Button1_Click" /><br />
<br />
<asp:Label ID="Label1" runat="server"></asp:Label>
<br />
<asp:CheckBoxList ID="CheckBoxList1" runat="server" DataSource="SqlDataSource" DataField="CompanyName" RepeatColumns="3" BorderColor="Black" BorderStyle="Solid" BorderWidth="1px">
</asp:CheckBoxList>
<asp:SqlDataSource ID="SqlDataSource" runat="server" SelectCommand="SELECT DISTINCT TOP 12 [CompanyName] FROM [SalesLT].[Customer] ORDER BY [CompanyName]" ConnectionStrings="<%# ConnectionStrings:AdventureWorksConnectionString %>">
</asp:SqlDataSource>
```

# C#

```csharp
<%@ Page Language="C#" %>
<!DOCTYPE html>
<script runat="server">
protected void Button1_Click(object sender, EventArgs e)
{
    Label.Text = "Selected:<br />";
    foreach (ListItem li in CheckBoxList.Items)
    {
        if (li.Selected == true)
        {
            Label.Text += li.Text + "<br />";
        }
    }
}
</script>
```

此 ASP.NET 页面上有一个 `SqlDataSource` 控件，用于从 `AdventureWorks` 中提取你所需的信息。

## 第 5 章 ASP.NET 服务器控件

![](img/67a6707ff505c052edb96c0128fb3096_197_0.png)

图 5-18

`RadioButton` 控件相比于 `RadioButtonList` 控件（将在下文中讨论）的优势在于，它允许你在各个 `RadioButton` 控件之间放置其他项目（文本、控件或图像）。然而，`RadioButtonList` 在 Web 页面上始终是一个直排的单选按钮列表。

## RADIOBUTTONLIST 服务器控件

`RadioButtonList` 控件允许你在 Web 页面上显示一组单选按钮。`RadioButtonList` 控件与 `CheckBoxList` 以及其他控件非常相似，它们允许你遍历用户选择的内容、进行计数或执行其他操作。

一个典型的 `RadioButtonList` 控件以如下方式被编写到页面中：

```xml
<asp:RadioButtonList Id="RadioButtonList" runat="server">
    <asp:ListItem Selected="True">English</asp:ListItem>
    <asp:ListItem>Russian</asp:ListItem>
    <asp:ListItem>Finnish</asp:ListItem>
    <asp:ListItem>Swedish</asp:ListItem>
</asp:RadioButtonList>
```

与其他控件一样，它为集合中的每个项目都使用 `ListItem` 对象的实例。从示例中，可以看到 `Selected` 属性被设置为 `True`，当页面首次生成时，其中一个 `ListItem` 被默认选中。这产生了图 5-19 所示的结果。

| English |
| Russian |
| Finnish |
| Swedish |

图 5-19

`Selected` 属性不是必须的，但如果你希望让最终用户从集合中某些选择，那么这是一个好主意。使用它可以防止集合为空。

你可以使用 `RadioButtonList` 控件在页面方法中检查最终用户选择的值。列表 5-16 显示了一个 `Button_Click` 事件，它会将 `RadioButtonList` 集合中选中的值输出。

## 列表 5-16: 检查从 RadioButtonList 选择的项的值

### VB

```vb
<%@ Page Language="VB" %>
<!DOCTYPE html>
<script runat="server">
    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
        Label1.Text = "You selected: " & RadioButtonList1.SelectedItem.ToString()
    End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
    <head id="Head1" runat="server">
    <title>RadioButtonControl</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:Label ID="Label1" runat="server" />
            <asp:RadioButtonList ID="RadioButton1" runat="server">
                <asp:ListItem Selected="True">English</asp:ListItem>
                <asp:ListItem Value="Russian"></asp:ListItem>
                <asp:ListItem Value="Finnish"></asp:ListItem>
                <asp:ListItem Value="Swedish"></asp:ListItem>
            </asp:RadioButtonList>
            <asp:Button ID="Button1" runat="server" Text="Submit" OnClick="Button1_Click" />
        </div>
    </form>
</body>
</html>
```

### C#

```csharp
<%@ Page Language="C#" %>
<script runat="server">
    protected void Button1_Click(object sender, EventArgs e)
    {
        Label1.Text = "You selected: " + RadioButtonList1.SelectedItem.ToString();
    }
</script>
```

这段代码从 `ListItem` 项的 `RadioList` 集合中获取选中的项。这就是你处理 ASP.NET 提供的其他列表控件的方式。`RadioButtonList` 还允许你访问 `Repeats` 和 `RepeatDirection` 属性（这些在 `CheckListBox` 部分中已解释过）。你可以将此控件绑定到来自任何数据源的项，以便在你的 Web 页面上动态创建单选按钮列表。

## IMAGE 服务器控件

`Image` 服务器控件允许你从服务器端代码处理 Web 页面上的图像。它是一个简单的服务器控件，但它可以让你拥有决定图像在浏览器屏幕上显示方式的能力。一个典型的图像控件按如下方式构造：

```xml
<asp:Image ID="Image1" runat="server" ImageUrl="~/Images/Windows.jpg" />
```

重要的属性是 `ImageUrl`。它指向图像的文件位置。在这种情况下，位置指定为 `Windows.jpg` 文件。

## 列表 5-17: 动态更改 ImageUrl 属性

列表 5-17 显示了动态更改 `ImageUrl` 属性的示例。

### VB

```vb
<%@ Page Language="VB" %>
<!DOCTYPE html>
<script runat="server">
    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
        ' 动态更改逻辑
    End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
    <head id="Head1" runat="server">
    <title>ImageControl</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:Image ID="Image1" runat="server" />
        </div>
    </form>
</body>
</html>
```

### C#

```csharp
<%@ Page Language="C#" %>
<script runat="server">
    protected void Button1_Click(object sender, EventArgs e)
    {
        // 动态更改逻辑
    }
</script>
```

## TABLE 控件

`Table` 是最常用的元素之一，因为 HTML `<table>` 元素是显示记录常用格式。`Table` 控件的典型构造如下：

```xml
<asp:Table ID="Table1" runat="server">
    <asp:TableRow Font="True" ForeColor="White" BackColor="DarkGray">
        <asp:TableHeaderCell>First</asp:TableHeaderCell>
        <asp:TableHeaderCell>Last</asp:TableHeaderCell>
    </asp:TableRow>
    <asp:TableRow>
        <asp:TableCell>Jason</asp:TableCell>
        <asp:TableCell>Gaylord</asp:TableCell>
    </asp:TableRow>
    <asp:TableRow>
```
