

Test Query 页面出现在 Configure Data Source 向导中（图 26.54）。

- 10. 单击 Test Query 按钮测试 Query，然后单击 Finish 按钮保存 Select 语句，如图 26.54 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1329_0.png)

## 图 26.54：完成向导

配置 GridView 控件的数据源后，GridViewControl 应用程序的 Default.aspx 页面显示如下，见清单 26.8：

## 清单 26.8：显示 Default.aspx 页面的代码

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
</div>
<asp:GridView ID="GridView1" runat="server" AutoGenerateColumns="False" DataKeyNames="ProductID" DataSourceID="SqlDataSource1">
<Columns>
<asp:BoundField DataField="ProductID" HeaderText="ProductID" InsertVisible="False" ReadOnly="True" SortExpression="ProductID" />
<asp:BoundField DataField="ProductName" HeaderText="ProductName" SortExpression="ProductName" />
<asp:BoundField DataField="QuantityPerUnit" HeaderText="QuantityPerUnit" SortExpression="QuantityPerUnit" />
<asp:BoundField DataField="UnitPrice" HeaderText="UnitPrice" SortExpression="UnitPrice" />
<asp:BoundField DataField="UnitsInStock" HeaderText="UnitsInStock" SortExpression="UnitsInStock" />
</Columns>
</asp:GridView>
<asp:SqlDataSource ID="SqlDataSource1" runat="server" ConnectionString="<%$ ConnectionStrings:northwindConnectionString %>"
```
```
SelectCommand="SELECT [ProductID], [ProductName], [QuantityPerUnit], [UnitPrice], [UnitsInStock] FROM [Alphabetical list of products]"
</asp:SqlDataSource>
</form>
</body>
</html>
```

11. 按键盘上的 F5 键运行应用程序。应用程序的输出显示在图 26.55 中：

![](img/e073a4882197be4ab61103cbe0bcb394_1330_0.png)

## 图 26.55：显示 GridViewControl 应用程序的输出

## 使用 DataList 控件

现在，让我们使用 DataList 控件通过执行以下步骤从数据库中显示数据：

- 1. 创建一个应用程序并将其保存为 DataListControl（可在 CD 上获得）。
- 2. 将 DataList 控件拖放到 Default.aspx 页面的设计视图中。
- 3. 从 Choose Data Source 下拉列表中选择 New data Source 选项以创建与数据库的连接，如图 26.56 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1330_1.png)

## 图 26.56：创建与数据源的连接

Configure Data Source Wizard 出现。

- 4. 创建 DataList 控件与数据库的连接。在本例中，我们正在创建与 northwind 数据库的 Products 表的连接。

### NOTE

您可以参考 GridViewControl 应用程序中创建与数据库连接的步骤。

- 5. 单击 DataList 控件的 Smart Tag 并选择 Auto Format 链接。AutoFormat 对话框出现，您可以在其中对 DataList 控件应用彩色格式（图 26.57）。

- 6. 从 Select a scheme 窗格中选择 Colorful 选项并单击 OK 按钮，如图 26.57 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1331_0.png)

## 图 26.57：选择格式

创建连接并应用格式化后的 DataList 控件显示如下，如图 26.58 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1331_1.png)

## 图 26.58：格式化后显示的网页

配置 DataList 控件的数据源后，DataListControl 应用程序的 Default.aspx 页面显示如下，见清单 26.9：

## 清单 26.9：显示 Default.aspx 页面的代码

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>

</div>
<asp:DataList ID="DataList1" runat="server" CellPadding="4" DataKeyField="ProductID" DataSourceID="SqlDataSource1" ForeColor="#333333">
<AlternatingItemStyle BackColor="White" />
<FooterStyle BackColor="#990000" Font-Bold="True" ForeColor="White" />
<HeaderStyle BackColor="#990000" Font-Bold="True" ForeColor="White" />
<ItemStyle BackColor="#FFFBDF" ForeColor="#333333" />
<ItemTemplate>
ProductID:
<asp:Label ID="ProductIDLabel" runat="server" Text='<%# Eval("ProductID") %>' />
<br />
ProductName:
<asp:Label ID="ProductNameLabel" runat="server" Text='<%# Eval("ProductName") %>' />
<br />
QuantityPerUnit:
<asp:Label ID="QuantityPerUnitLabel" runat="server" Text='<%# Eval("QuantityPerUnit") %>' />
<br />
UnitsInStock:
<asp:Label ID="UnitsInStockLabel" runat="server" Text='<%# Eval("UnitsInStock") %>' />
<br />
UnitPrice:
<asp:Label ID="UnitPriceLabel" runat="server" Text='<%# Eval("UnitPrice") %>' />
<br />
<br />
</ItemTemplate>
<SelectedItemStyle BackColor="#FFCC66" Font-Bold="True" ForeColor="Navy" />
</asp:DataList>
<asp:SqlDataSource ID="SqlDataSource1" runat="server" ConnectionString="<%$ ConnectionStrings:northwindConnectionString %>" SelectCommand="SELECT [ProductID], [ProductName], [QuantityPerUnit], [UnitsInStock], [UnitPrice] FROM [Alphabetical list of products]">
</asp:SqlDataSource>
</form>
</body>
</html>
```

7. 按键盘上的 F5 键执行应用程序。网页上的输出如图所示，见图 26.59：

## 使用 DetailsView 控件

现在，让我们使用 DetailsView 控件通过执行以下步骤从数据库中显示数据：

- 1. 创建一个应用程序并将其保存为 DetailsViewControl（可在 CD 上获得）。
- 2. 将 DetailsViewControl 拖放到 Default.aspx 页面的设计视图中，并从 Choose Data Source 下拉列表中选择 New data source 选项，如图 26.60 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1333_0.png)

## 图 26.59：显示 DataListControl 应用程序的输出

![](img/e073a4882197be4ab61103cbe0bcb394_1333_1.png)

## 图 26.60：选择数据源

Configure Data Source Wizard 出现。

- 3. 创建 DetailsView 控件与数据库的连接。在本例中，我们正在创建与 northwind 数据库的 Products 表的连接。

### NOTE

> 您可以参考 GridViewControl 应用程序中创建与数据库连接的步骤。

- 4. 单击 DetailsView 控件的 Smart Tag 并选择 Auto Format 链接。AutoFormat 对话框出现，可用于对 DetailsView 控件应用彩色布局。
- 5. 从 Select a scheme 窗格中选择 Slate 选项并单击 OK 按钮。
- 6. 选择 Enable Paging 复选框以在控件中提供分页。

创建连接并应用格式化后的 DetailsView 控件显示如下，如图 26.61 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1334_0.png)

## 图 26.61：显示网页

配置 DetailsView 控件的数据源后，DetailsView Control 应用程序的 Default.aspx 页面显示如下，见清单 26.10：

## 清单 26.10：显示 Default.aspx 页面的代码

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
</div>
<asp:DetailsView ID="DetailsView1" runat="server" AllowPaging="True" AutoGenerateRows="False" BackColor="White" BorderColor="#E7E7FF" BorderStyle="None" BorderWidth="1px" CellPadding="3" DataKeyNames="ProductID" DataSourceID="SqlDataSource1" GridLines="Horizontal" Height="50px" Width="272px">
<AlternatingRowStyle BackColor="#F7F7F7" />
<EditRowStyle BackColor="#738A9C" Font-Bold="True" ForeColor="#F7F7F7" />
<Fields>
<asp:BoundField DataField="ProductID" HeaderText="ProductID" InsertVisible="False" ReadOnly="True" SortExpression="ProductID" />
<asp:BoundField DataField="ProductName" HeaderText="ProductName" SortExpression="ProductName" />
<asp:BoundField DataField="QuantityPerUnit" HeaderText="QuantityPerUnit" SortExpression="QuantityPerUnit" />
<asp:BoundField DataField="UnitPrice" HeaderText="UnitPrice" SortExpression="UnitPrice" />
<asp:BoundField DataField="UnitsInStock" HeaderText="UnitsInStock" SortExpression="UnitsInStock" />
</Fields>
<FooterStyle BackColor="#5C7DC" ForeColor="#4A3C8C" />
<HeaderStyle BackColor="#4A3C8C" Font-Bold="True" ForeColor="#F7F7F7" />
<PagerStyle BackColor="#E7E7FF" ForeColor="#4A3C8C" HorizontalAlign="Right" />
<RowStyle BackColor="#E7E7FF" ForeColor="#4A3C8C" />
</asp:DetailsView>
<asp:SqlDataSource ID="SqlDataSource1" runat="server" ConnectionString="<%$ ConnectionStrings:northwindConnectionString %>" SelectCommand="SELECT [ProductID], [ProductName], [QuantityPerUnit], [UnitPrice], [UnitsInStock] FROM [Alphabetical list of products]">
</asp:SqlDataSource>
```
