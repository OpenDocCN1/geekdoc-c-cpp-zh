

```
Text='<%# Eval("ProductID") %>' />
<br />
ProductName:
<asp:TextBox ID="ProductNameTextBox" runat="server" Text='<%# Bind("ProductName") %>' />
<br />
QuantityPerUnit:
<asp:TextBox ID="QuantityPerUnitTextBox" runat="server" Text='<%# Bind("QuantityPerUnit") %>' />
<br />
UnitPrice:
<asp:TextBox ID="UnitPriceTextBox" runat="server" Text='<%# Bind("UnitPrice") %>' />
<br />
UnitsInStock:
<asp:TextBox ID="UnitsInStockTextBox" runat="server" Text='<%# Bind("UnitsInStock") %>' />
<br />
<asp:Button ID="UpdateButton" runat="server" CommandName="Update" Text="Update" />
<asp:Button ID="CancelButton" runat="server" CommandName="Cancel" Text="Cancel" />
</li>
</EditItemTemplate>
<EmptyDataTemplate>
No data was returned.
</EmptyDataTemplate>
<InsertItemTemplate>
<li style="">
ProductName:
<asp:TextBox ID="ProductNameTextBox" runat="server" Text='<%# Bind("ProductName") %>' />
<br />
QuantityPerUnit:
<asp:TextBox ID="QuantityPerUnitTextBox" runat="server" Text='<%# Bind("QuantityPerUnit") %>' />
<br />
UnitPrice:
<asp:TextBox ID="UnitPriceTextBox" runat="server" Text='<%# Bind("UnitPrice") %>' />
<br />
UnitsInStock:
<asp:TextBox ID="UnitsInStockTextBox" runat="server" Text='<%# Bind("UnitsInStock") %>' />
<br />
<asp:Button ID="InsertButton" runat="server" CommandName="Insert" Text="Insert" />
<asp:Button ID="CancelButton" runat="server" CommandName="Cancel" Text="Clear" />
</li>
</InsertItemTemplate>
<ItemSeparatorTemplate>
</ItemSeparatorTemplate>
<ItemTemplate>
<li style="background-color: #E0FFFF;color: #333333;">ProductID:
<asp:Label ID="ProductIDLabel" runat="server" Text='<%# Eval("ProductID") %>' />
<br />
ProductName:
<asp:Label ID="ProductNameLabel" runat="server" Text='<%# Eval("ProductName") %>' />
<br />
QuantityPerUnit:
<asp:Label ID="QuantityPerUnitLabel" runat="server" Text='<%# Eval("QuantityPerUnit") %>' />
<br />
UnitPrice:
<asp:Label ID="UnitPriceLabel" runat="server" Text='<%# Eval("UnitPrice") %>' />
<br />
UnitsInStock:
<asp:Label ID="UnitsInStockLabel" runat="server" Text='<%# Eval("UnitsInStock") %>' />
<br />
</li>
</ItemTemplate>
<LayoutTemplate>
<ul ID="itemPlaceholderContainer" runat="server" style="font-family: Verdana, Arial, Helvetica, sans-serif;">
<li runat="server" id="itemPlaceholder" />
</ul>
<div style="text-align: center;background-color: #5D7B9D;font-family: Verdana, Arial, Helvetica, sans-serif;color: #FFFFFF;">
</div>
</LayoutTemplate>
<SelectedItemTemplate>
<li style="background-color: #E2DED6;font-weight: bold;color: #333333;">ProductID:
<asp:Label ID="ProductIDLabel" runat="server" Text='<%# Eval("ProductID") %>' />
<br />
ProductName:
<asp:Label ID="ProductNameLabel" runat="server" Text='<%# Eval("ProductName") %>' />
<br />
QuantityPerUnit:
<asp:Label ID="QuantityPerUnitLabel" runat="server" Text='<%# Eval("QuantityPerUnit") %>' />
<br />
UnitPrice:
<asp:Label ID="UnitPriceLabel" runat="server" Text='<%# Eval("UnitPrice") %>' />
<br />
UnitsInStock:
<asp:Label ID="UnitsInStockLabel" runat="server" Text='<%# Eval("UnitsInStock") %>' />
<br />
</li>
</SelectedItemTemplate>
</asp:ListView>
<asp:SqlDataSource ID="SqlDataSource1" runat="server" ConnectionString="<%$ ConnectionStrings:northwindConnectionString %>" SelectCommand="SELECT [ProductID], [ProductName], [QuantityPerUnit], [UnitPrice], [UnitsInStock] FROM [Alphabetical list of products]">
</div>
<asp:DataPager ID="DataPager1" runat="server" PagedControlID="ListView1">
<Fields>
<asp:NextPreviousPagerField ButtonType="Button" ShowFirstPageButton="True" ShowNextPageButton="False" ShowPreviousPageButton="False" />
<asp:NumericPagerField />
<asp:NextPreviousPagerField ButtonType="Button" ShowLastPageButton="True" ShowNextPageButton="False" ShowPreviousPageButton="False" />
</Fields>
</asp:DataPager>
</form>
</body>
</html>

7. 在 Default.aspx 页面的源视图中添加代码后，Web 页面出现，如图 26.72 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1345_0.png)

# 图 26.72：添加代码后显示的 Web 页面

8. 按键盘上的 F5 键执行应用程序。输出显示，如图 26.73 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1345_1.png)

# 图 26.73：显示 ListViewControl 应用程序的输出

# 使用 Chart 控件

让我们通过执行以下步骤学习如何使用 Chart 控件显示记录：

+   1. 创建一个应用程序并将其保存为 ChartControl（可在 CD 上获得）。

+   2. 从工具箱拖放 Chart 控件并从“选择数据源”下拉列表中选择“新建数据源”选项，如图 26.74 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1346_0.png)

# 图 26.74：选择数据源

3. 创建 Chart 控件与数据库的连接。在此情况下，我们将与 northwnd 数据库的 Products 表创建连接。

> 注意
> 您可参考 GridViewControl 应用程序中创建与数据库连接的步骤。

4. 选择要在 x 轴和 y 轴上显示的成员。在此应用程序中，我们在 X Value Member 下拉列表中选择了 UnitsOnOrder 列，并在 Y Value Members 下拉列表中选择了 UnitsInStock 列，如图 26.75 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1346_1.png)

# 图 26.75：选择要在轴上显示的成员

设置 Chart 控件的属性后，Default.aspx 的源视图显示如下，见清单 26.14：

# 清单 26.14：显示 Default.aspx 页面的代码

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<%@ Register assembly="System.Web.DataVisualization, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" namespace="System.Web.UI.DataVisualization.Charting" tagprefix="asp" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
</div>
<asp:Chart ID="Chart1" runat="server" DataSourceID="SqlDataSource1" width="550px">
<series>
<asp:Series Name="Series1" XValueMember="UnitsOnOrder" YValueMembers="UnitsInStock">
</asp:Series>
</series>
<chartareas>
<asp:ChartArea Name="ChartArea1">
</asp:ChartArea>
</chartareas>
</asp:Chart>
<asp:SqlDataSource ID="SqlDataSource1" runat="server" ConnectionString="<%$ ConnectionStrings:northwndConnectionString %>" SelectCommand="SELECT [UnitPrice], [UnitsInStock], [UnitsOnOrder] FROM [Alphabetical list of products]">
</asp:SqlDataSource>
</form>
</body>
</html>
```

5. 按键盘上的 F5 键执行应用程序。输出如下所示，如图 26.76 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1347_0.png)

# 图 26.76：显示 Chart 控件的输出

# 使用 QueryExtender 控件

让我们通过执行以下步骤学习如何使用 QueryExtender 控件显示一组记录：

+   1. 创建一个应用程序并将其保存为 QueryExtenderControl（可在 CD 上获得）。
+   2. 在 Default.aspx 页面的设计视图上拖放一个 TextBox 和一个 Button 控件。
+   3. 将 Button 控件的文本属性设置为 Search。
+   4. 在设计视图上拖放 LinqDataSource 控件并像在 LinqDataSource 应用程序中一样将其与数据库连接。
+   5. 在页面设计视图上拖放 GridView 控件并在“选择数据源”下拉列表中选择数据源名称为 LinqDataSource1。
+   6. 在 Default.aspx 的设计视图上拖放一个 QueryExtender 控件，并在 Default.aspx 页面的源视图中添加突出显示的代码，如清单 26.15 所示：

# 清单 26.15：显示 Default.aspx 页面的代码

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
</div>
Enter Product Name:<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
<asp:Button ID="Button1" runat="server" Text="Search" />
<asp:LinqDataSource ID="LinqDataSource1" runat="server" ContextTypeName="DataClassesDataContext" EntityTypeName="" Select="new (ProductID, ProductName)" TableName="Products">
</asp:LinqDataSource>
<asp:GridView ID="GridView1" runat="server" AutoGenerateColumns="False" DataSourceID="LinqDataSource1">
<Columns>
<asp:BoundField DataField="ProductID" HeaderText="ProductID" ReadOnly="True" SortExpression="ProductID" />
<asp:BoundField DataField="ProductName" HeaderText="ProductName" ReadOnly="True" SortExpression="ProductName" />
</Columns>
</asp:GridView>
<asp:QueryExtender ID="QueryExtender1" runat="server" TargetControlID="LinqDataSource1">
<asp:SearchExpression SearchType="StartsWith" DataFields="ProductName">
<asp:ControlParameter ControlID="TextBox1" />
</asp:SearchExpression>
</asp:QueryExtender>
</form>
</body>
</html>
```

+   7. 按键盘上的 F5 键查看 QueryExtenderControl 应用程序的输出（图 26.77）。
+   8. 在文本框中输入产品名称并单击 Search 按钮，如图 26.77 所示：

