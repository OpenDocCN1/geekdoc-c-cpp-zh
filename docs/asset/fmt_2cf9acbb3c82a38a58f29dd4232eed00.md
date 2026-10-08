
列表 11.29：显示 `Default.aspx` 的代码

```
<% Page Language="C#" AutoEventWireBack="true" CodeFile="Default.aspx.cs" Inherits="Default" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<server id="server">
<title>ImageButton control</title>
</head>
<body>
<form id="form">
<div>
<asp:Label Id="Label11" runat="server" Font-Bold="True" Font-Underline="True"
Text="ImageButton control" /></asp:Label>
<br />
<asp:Label Id="Label12" runat="server" Borderwidth="2px" Font-Italic="True"
ForeColor="#FF0066" Text="Click Anywhere on the ImageButton
control" /></asp:Label>
<br />
<asp:ImageButton Id="ImageButton1" runat="server" Height="300px"
ImageUrl="Hydranges.jpg" OnClick="ImageButton1_Click" />
<br />
<asp:Label Id="Label13" runat="server"
Text="You clicked on the ImageButton at following coordinates:"</asp:Label>
<asp:Label Id="Label14" runat="server" BackColor="#00CCFF" /></asp:Label>
</div>
</form>
</body>
</html>
```

现在，如列表 11.30 所示，在 `Default.aspx` 的后代码文件中添加代码：

列表 11.30：显示 `Default.aspx` 页面后代码文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.Controls;
public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs args)
{ }
    protected void ImageButton1_Click(object sender, EventArgs args)
{
    Label4.Text = e.X.ToString() + " , " + e.Y.ToString();
}
}
```

现在，按下键盘上的 `F5` 键运行应用程序。点击 `ImageButton` 控件后，输出结果如图 11.24 所示：

![](img/17af790174c480761404624aeed9b30b_550_0.png)

图 11.24：点击位置的坐标

## 使用 ImageMap 控件

当你在 Web 页面 (`Default.aspx`) 上添加 `ImageMap` 控件时，它向 Web 页面的源代码中添加代码：

```asp
<asp:ImageMap id="imagemap1" runat="server" />
```

让我们创建一个应用程序 `ImageMapControl`。向 Web 页面添加一个 `ImageMap` 控件。现在，让我们通过执行以下步骤查看它是如何工作的：

- 1. 首先，我们将图像放在项目文件夹中，然后通过 `Select Image`（选择图像）对话框将图像添加到 `ImageMap` 控件中（正如我们在处理 `Image Control` 时所做的）。
- 2. 在设计视图中选择 `ImageMap` 控件，点击属性窗口中 `HotSpots` 属性前面的省略号 (...) 按钮。打开 `HotSpot Editor` 对话框。
- 3. 右键点击 `Add`（添加）按钮并选择 `RectangleHotSpot`，我们将示例中的图像设为矩形。图 11.25 显示了已添加热点的 `HotSpot Collection Editor`（热点集合编辑器）对话框：

![](img/17af790174c480761404624aeed9b30b_550_1.png)

图 11.25：显示热点集合编辑器

在应用程序中添加另一个名为 `Default2.aspx` 的 Web 表单。当用户点击热点时，将显示该 Web 表单。设计时的 `ImageMap` 应用程序如图 11.26 所示：

![](img/17af790174c480761404624aeed9b30b_551_0.png)

图 11.26：设计时期的 `ImageMap` 控件

列表 11.31 显示了 `ImageMap` 控件的 `Default.aspx` 页面代码：

列表 11.31：显示 `Default.aspx` 页面代码

```
<@Page Language="C#" AutoEventWire="true" CodeFile="Default.aspx.cs">
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head id="head1" runat="server">
<title>ImageMap Example</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:label Id="Label1" runat="server" Font-Bold="True" Font-Underline="True" Text="ImageMap Example"></asp:label>
<br />
<br />
<asp:ImageMap Id="ImageMap1" runat="server" ImageUrl="~/ImageMap.png">
<asp:HotSpot AlternateText="HOTSPOT 1" Bottom="10" Mode="Navigate" NavigateUrl="~/Default2.aspx" Right="50" Top="100" />
</asp:ImageMap>
</form>
</body>
</html>
```

现在，如列表 11.32 所示，为 `ImageMap` 控件添加 `Default2.aspx` 页面代码：

列表 11.32：显示 `Default2.aspx` 页面

```
<@Page Language="C#" AutoEventWire="true" CodeFile="Default2.aspx.cs">
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head id="head1" runat="server">
<title>Image Map Example</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label Id="Label1" runat="server" Text="welcome to the Home Page"
Font-Bold="True" Font-Size="Larger" ForeColor="Red"
Height="104px" width="388px"></asp:Label>
</div>
</form>
</body>
</html>
```

在资源管理器中右键点击 `Default.aspx` 并选择 `Set Start Page`（设置起始页）作为起始。现在，按 `F5` 键运行应用程序，输出如图 11.27 所示：

![](img/17af790174c480761404624aeed9b30b_552_0.png)

点击 `HOTSPOT 1` `ImageMap` 控件。`Default2.aspx` 打开，如图 11.28 所示：

![](img/17af790174c480761404624aeed9b30b_552_1.png)

## 使用 Table 控件

当你在 Web 页面 (`Default2.aspx`) 上添加 `Table` 控件时，会将以下代码添加到源代码：

```
<asp:Table Id="Table1" runat="server"></asp:Table>
```

让我们创建一个名为 `TableSample` 的应用程序。在这个示例中，我们在 Web 页面上放置了一个 `Table` 控件，用于显示按钮点击事件详细信息。执行以下步骤操作 `Table` 控件：

- 1. 在设计模式下选择 `Table` 控件，点击属性窗口中 `Rows` 属性前面的省略号 (...) 按钮，通过 `Row Editor` 向 `Table` 控件添加行。
- 2. 为 `Table` 控件添加新行，点击 `Row Collection` 对话框中的 `Add`（添加）按钮。图 11.29 显示了已添加四行的 `Row Collection` 对话框：

![](img/17af790174c480761404624aeed9b30b_553_0.png)

图 11.29：显示 `Row Collection` 对话框
- 3. 向行添加单元格，点击 `Row` 属性中 `Cell` 属性前面的省略号 (...) 按钮。这将打开 `Cell Editor` 对话框（图 11.30）。
- 4. 向行添加单元格，点击 `Add`（添加）按钮。你可以通过 `Cell` 属性中的 `Text` 属性来设置在单元格中显示的文本，如图 11.30 所示：

![](img/17af790174c480761404624aeed9b30b_553_1.png)

图 11.30：显示 `Cell Collection` 对话框

列表 11.33 显示了 `Table` 控件的 `Default.aspx` 页面代码：

列表 11.33：显示 `Default.aspx` 页面代码

```
<% Page Language="C#" AutoEventWireup="True" CodeFile="Default.aspx.cs" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/html">
<head>
  <meta runat="server">
  <title>Table Control Example</title>
</head>
<body>
  <form id="form" runat="server">
  <div>
    <asp:Label ID="Label" runat="server" Font-Bold="True" Font-Size="Medium" Font-Underline="True" Text="Table Control Example"></asp:Label>
    <br />
    <br />
    <asp:Button Id="Button1" runat="server" Font-Bold="True" Height="60px"
Text="Click Me to See the Details!"
Width="316px" OnClick="Button1_Click" />
    <br />
    <asp:Table Id="Table1" runat="server" Color="Black" BorderStyle="Solid"
BorderWidth="20px" Caption="Students Detail" Font-Size="Small" ForeColor="Red"
GridLines="Both" Height="HorizontalAlignment="Center" Visible="false"
Width="340px">
<asp:TableCell Id="TableCell0" runat="server" Color="Black" BorderStyle="Solid">
<asp:TableCell Id="TableCell1" runat="server"></asp:TableCell>
<asp:TableCell Id="TableCell2" runat="server" Color="Black" BorderStyle="Solid">Name</asp:TableCell>
<asp:TableCell Id="TableCell3" runat="server" Color="Black" BorderStyle="Solid">No</asp:TableCell>
<asp:TableCell Id="TableCell4" runat="server" Color="Black" BorderStyle="Solid">
<asp:TableCell Id="TableCell5" runat="server" Color="Black" BorderStyle="Solid">
<asp:TableCell Id="TableCell6" runat="server" Color="Black" BorderStyle="Solid">
<asp:TableCell Id="TableCell7" runat="server" Color="Black" BorderStyle="Solid"></asp:TableCell>
<asp:TableCell Id="TableCell8" runat="server" Color="Black" BorderStyle="Solid"Width="16px"></asp:TableCell>
</asp:Row>
<asp:Row Id="TableRow2" runat="server" Color="Black" BorderStyle="Solid">
<asp:TableCell Id="TableCell10" runat="server" Color="Black" BorderStyle="Solid"Width="400px"></asp:TableCell>
<asp:TableCell Id="TableCell11" runat="server" Color="Black" BorderStyle="Solid"></asp:TableCell>
<asp:TableCell Id="TableCell12" runat="server" Color="Black" BorderStyle="Solid"Width="20px"></asp:TableCell>
</asp:Row>
<asp:Row Id="TableRow3" runat="server" Color="Black" BorderStyle="Solid">
<asp:TableCell Id="TableCell13" runat="server" Color="Black" BorderStyle="Solid"Width="400px"></asp:TableCell>
<asp:TableCell Id="TableCell14" runat="server" Color="Black" BorderStyle="Solid"Width="17"></asp:TableCell>
<asp:TableCell Id="TableCell15" runat="server" Color="Black" BorderStyle="Solid"></asp:TableCell>
</asp:Row>
<asp:Row Id="TableRow4" runat="server" Color="Black" BorderStyle="Solid">
<asp:TableCell Id="TableCell16" runat="server" Color="Black" BorderStyle="Solid"Width="400px"></asp:TableCell>
<asp:TableCell Id="TableCell17" runat="server" Color="Black" BorderStyle="Solid"Width="20px"></asp:TableCell>
<asp:TableCell Id="TableCell18" runat="server" Color="Black" BorderStyle="Solid"></asp:TableCell>
</asp:Row>
</asp:Table>
/>
</form>
</body>
</html>
```

# 第 11 章：标准 Web 控件

```cs
protected void Button1_Click(object sender, EventArgs e)
{
Table1.visible = true;
}
```

按下键盘上的 `F5` 键运行应用程序。点击“Click Me to See the Student Detail!”输出如图 11.31 所示。

![](img/17af790174c480761404624aeed9b30b_555_0.png)

图 11.31：在按钮事件上显示表格控件及记录

## 使用向导控件 (Wizard Control)

当你在 Web 页面 (`Default.aspx`) 上添加 `Wizard` 控制时，它会在页面的源代码中添加以下代码：
