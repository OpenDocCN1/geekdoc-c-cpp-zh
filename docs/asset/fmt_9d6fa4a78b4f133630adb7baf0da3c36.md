
```xml
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="Default" %>
<!DOCTYPE html>
<!-- [W3C//DTD HTML 4.0 Transitional//EN] -->
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
  <title>EntityDataSource Application</title>
</head>
<body>
  <form id="form1" runat="server">
  <div>
    <asp:EntityDataSource ID="EntityDataSource" runat="server"
        ConnectionString="Data Source=NorthwindEntities"
        EnableFlattening="False"
        SelectName="NorthwindEntities" />
    </asp:EntityDataSource>
    <asp:Grid ID="GridView1" runat="server" AutoGenerateColumns="False"
        DataSourceID="EntityDataSource">
    <Columns>
      <asp:BoundField DataField="ProductID" HeaderText="ProductID" ReadOnly="True" />
      <asp:BoundField DataField="ProductName" HeaderText="ProductName" SortExpression="ProductName" />
      <asp:BoundField DataField="SupplierID" HeaderText="SupplierID" SortExpression="SupplierID" />
      <asp:BoundField DataField="Category" HeaderText="Category" SortExpression="Category" />
      <asp:BoundField DataField="QuantityPerUnit" HeaderText="QuantityPerUnit" />
      <asp:BoundField DataField="UnitPrice" HeaderText="UnitPrice" SortExpression="UnitPrice" />
      <asp:BoundField DataField="UnitsStock" HeaderText="UnitsStock" SortExpression="UnitsStock" />
      <asp:BoundField DataField="UnitOrder" HeaderText="UnitOrder" SortExpression="UnitOrder" />
      <asp:BoundField DataField="ReorderLevel" HeaderText="ReorderLevel" SortExpression="ReorderLevel" />
      <asp:BoundField DataField="Discontinued" HeaderText="Discontinued" />
    </Columns>
    </asp:Grid>
  </div>
  </form>
</body>
</html>
```

11. 按 `F5` 键运行应用程序。输出如图 22.40 所示：

![](img/17af790174c480761404624aeed9b30b_1089_0.png)

图 22.40：EntityDataSource 的输出

## 使用 GridView

现在让我们通过以下步骤在 GridView 中显示数据：

- 1. 创建一个 Web 应用程序并保存为 EntityDataSource。
- 2. 将 GridView 拖到 `Default.aspx` 的设计视图，并在“选择数据源”下拉列表中选择 `EntityDataSource`，如图 22.41 所示：

![](img/17af790174c480761404624aeed9b30b_1089_1.png)

图 22.41：选择数据源
- 3. 在数据源配置的“从从何获取数据”面板中选择 SQL 数据库选项并点击“确定”按钮，如图 22.42 所示：

![](img/17af790174c480761404624aeed9b30b_1090_0.png)

图 22.42：选择数据库
- 4. 点击“新建连接”按钮与数据库连接。
- 5. 在“添加连接”对话框中提供服务器名称和数据库名称以创建连接。
- 6. 在配置数据源向导的“选择您的数据连接”页面点击“下一步”按钮，如图 22.43 所示：

![](img/17af790174c480761404624aeed9b30b_1090_1.png)

图 22.43：选择连接字符串
- 7. 点击“下一步”按钮保存连接字符串，如图 22.44 所示：

![](img/17af790174c480761404624aeed9b30b_1091_0.png)

图 22.44：选择连接字符串
- 8. 点击“从表或视图指定列”按钮并在“列”面板中选择显示在 GridView 控件中的列。在此应用程序中，我们从 `products` 表选择了 `ProductID`、`ProductName`、`QuantityPerUnit`、`UnitPrice` 和 `UnitsInStock`（图 22.45）。
![](img/17af790174c480761404624aeed9b30b_1091_1.png)

图 22.45：选择列
- 9. 点击“下一步”按钮保存选择，如图 22.46 所示。
- 10. 点击“测试查询”按钮测试查询，然后点击“完成”按钮保存 `Select` 语句。

## 立即解决方案

![](img/17af790174c480761404624aeed9b30b_1092_0.png)

要通过此数据源返回数据，请点击“测试查询”。要完成此向导，请点击“完成”。

| 产品ID | 产品名称 | 单元数量（单位） | 价格 | 库存数量 |
|---|---|---|---|---|
| 1 | Chai | 10 盒 | 18.000 | 39 |
| 2 | Chang | 20 罐 | 19.000 | 60 |
| 3 | Anjou Pear | 125 瓶 | 12.000 | 13 |
| 4 | Chef's Cousin | 10 kg | 17.000 | 20 |
| 5 | Chef's Gumbo Mi | 30 盒 | 21.250 | |
| 6 | Carnobary | 12 盎司 | 15.000 | 65 |
| 7 | Uncle Root Beef | 12 盎司罐 | 30.000 | 15 |
| 8 | North Carolina Blackberry | 12 盎司罐 | 40.000 | 6 |
| 9 | Moko Kula Na | 18 包 | 7.950 | 78 |

`SELECT` 语句：

`SELECT [ProductID],[ProductName],[QuantityPerUnit],[UnitPrice],[UnitsInStock] FROM [Products]`

![](img/17af790174c480761404624aeed9b30b_1092_1.png)

*图 22-4：完成向导*

在配置好 GridView 控件的数据后，GridViewControl 应用程序的 `Default.aspx` 如列表 22:7 所示。

### 列表 22:7：Default.aspx 页面的代码

```asp
@Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs"
<html xmlns="http://www.w3.org/1999/html">
<head>
<title>GridView Control Application</title>
</head>
<<body>
<form id="form" runat="server">
<div>
<asp:GridView id="GridView" runat="server" AutoGenerateColumns="False" DataKeyNames="ProductID" DataSource="<%= SqlDataSource %>">
<Columns>
<asp:BoundField DataField="ProductID" HeaderText="ProductID" SortExpression="ProductID" />
<asp:BoundField DataField="ProductName" HeaderText="ProductName" SortExpression="ProductName" />
<asp:BoundField DataField="QuantityPerUnit" HeaderText="QuantityPerUnit" SortExpression="QuantityPerUnit" />
<asp:BoundField DataField="UnitsInStock" HeaderText="UnitsInStock" SortExpression="UnitsInStock" />
</Columns>
</asp:GridView>
<asp:SqlDataSource ID="SqlDataSource" runat="server" ConnectionString="<%= ConnectionStrings.NorthwindconnectionString %>" SelectCommand="SELECT [ProductID],[ProductName],[QuantityPerUnit],[UnitsInStock] FROM [Products]" />
</div>
</form>
</body>
</html>
```

## 第 22 章：ASP.NET 中的数据绑定

11. 按键盘上的 `F5` 键运行应用程序。应用程序的输出如图 22:47 所示：

![](img/17af790174c480761404624aeed9b30b_1093_0.png)

图 22:47。GridViewControl 应用程序的输出

## 使用 DataList 控件

让我们通过以下步骤使用 DataList 控件显示数据库中的数据：

- 1. 创建一个应用程序并将其保存为 `DataListControl`。
- 2. 在 `Default.aspx` 的设计视图中拖放 `DataList` 控件。
- 3. 从“选择数据源”下拉列表中选择新的数据源选项以创建与数据库的连接，如图 22:48 所示：

![](img/17af790174c480761404624aeed9b30b_1093_1.png)

图 22:48。与数据源创建连接

出现数据源配置向导。
- 4. 创建 `DataListControl` 与数据库的连接。在这种情况下，我们正在创建与 `Northwind` 数据库中 `Products` 表的连接。

注意

你可以参考 `GridViewControl` 创建与数据库连接的步骤。

## 立即解决方案

- 5. 点击 `DataList` 控件的智能标记并选择“自动格式”链接。会出现“自动格式”对话框，你可以在其中对 `DataList` 控件应用彩色格式（见图 22.49）。
- 6. 从“选择方案”中选择“彩色”选项并点击“确定”按钮，如图 22:49 所示：

![](img/17af790174c480761404624aeed9b30b_1094_0.png)

图 22.49：选择格式

创建连接并应用格式后，会出现 `DataList` 控件，如图 22:50 所示。

![](img/17af790174c480761404624aeed9b30b_1094_1.png)

图 22.50：格式化后的页面

## 第 22 章：ASP.NET 中的数据绑定

配置好 `DataList` 控件的数据后，`DataListControl` 应用程序的 `Default.aspx` 页如列表 22:8 所示。

### 列表 22:8：Default.aspx 的代码

```asp
@Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs"
@ Inherits="Default" %>
<html xmlns="http://www.w3.org/1999/html">
<head>
<title>DataList Application</title>
</head>
<body>
<form id="form1" runat="server">
<asp:DataList id="DataList" runat="server" CellPadding="4" DataKeyNames="ProductID" DataSource="SqlDataSource" AlternatingBackgroundColor="White" Width="100%">
<HeaderStyle BackColor="#333333" Font="Bold" />
<FooterStyle BackColor="#333333" />
<ItemStyle BackColor="#333333" />
<AlternatingItemStyle BackColor="#666666" />
<SelectedItemStyle BackColor="#9999FF" />
<Fields>
<asp:BoundField DataField="ProductID" HeaderText="ProductID" SortExpression="ProductID" />
<asp:BoundField DataField="ProductName" HeaderText="ProductName" SortExpression="ProductName" />
<asp:BoundField DataField="QuantityPerUnit" HeaderText="QuantityPerUnit" SortExpression="QuantityPerUnit" />
<asp:BoundField DataField="UnitsInStock" HeaderText="UnitsInStock" SortExpression="UnitsInStock" />
</Fields>
</asp:DataList>
<asp:SqlDataSource ID="SqlDataSource" runat="server" ConnectionString="<%= ConnectionStrings.NorthwindconnectionString %>" SelectCommand="SELECT [ProductID],[ProductName],[QuantityPerUnit],[UnitsInStock] FROM [Products]" />
</form>
</body>
</html>
```

## 立即解决方案

7. 按键盘上的 `F5` 键运行应用程序。应用程序的输出如图 22:47 所示：

![](img/17af790174c480761404624aeed9b30b_1096_0.png)

图 22:47。GridViewControl 应用程序的输出

## 使用 DataList 控件

让我们通过以下步骤使用 DataList 控件显示数据库中的数据：

- 1. 创建一个应用程序并将其保存为 `DataListControl`。
- 2. 在 `Default.aspx` 的设计视图中拖放 `DataList` 控件。
- 3. 从“选择数据源”下拉列表中选择新的数据源选项以创建与数据库的连接，如图 22:48 所示：

![](img/17af790174c480761404624aeed9b30b_1096_1.png)

图 22:48。与数据源创建连接

出现数据源配置向导。
- 4. 创建 `DataListControl` 与数据库的连接。在这种情况下，我们正在创建与 `Northwind` 数据库中 `Products` 表的连接。

注意

你可以参考 `GridViewControl` 创建与数据库连接的步骤。

## 立即解决方案

- 5. 点击 `DataList` 控件的智能标记并选择“自动格式”链接。会出现“自动格式”对话框，你可以在其中对 `DataList` 控件应用彩色格式（见图 22.49）。
- 6. 从“选择方案”中选择“彩色”选项并点击“确定”按钮，如图 22:49 所示：

![](img/17af790174c480761404624aeed9b30b_1097_0.png)

图 22.49：选择格式

创建连接并应用格式后，会出现 `DataList` 控件，如图 22:50 所示。

![](img/17af790174c480761404624aeed9b30b_1097_1.png)

图 22.50：格式化后的页面

## 第 22 章：ASP.NET 中的数据绑定

配置好 `DataList` 控件的数据后，`DataListControl` 应用程序的 `Default.aspx` 页如列表 22:9 所示。

### 列表 22:9：Default.aspx 页面的代码
