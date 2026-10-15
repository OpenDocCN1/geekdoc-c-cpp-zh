
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

7. The Web page appears after adding the code in the Source view of the Default.aspx page, as shown in Figure 26.72:

![](img/e073a4882197be4ab61103cbe0bcb394_1345_0.png)

# Figure 26.72: Showing the Web Page after Adding the Code

8. Press the F5 key on the keyboard to execute the application. The output appears, as shown in Figure 26.73:

![](img/e073a4882197be4ab61103cbe0bcb394_1345_1.png)

# Figure 26.73: Displaying the Output of the ListViewControl Application

# Using the Chart Control

Let’s learn how to use the Chart control to display the records, by performing the following steps:

+   1. Create an application and save it as ChartControl (available on the CD).

+   2. Drag and drop the Chart control from the Toolbox and select the New data source option from the Choose Data Source drop-down list, as shown in Figure 26.74:

![](img/e073a4882197be4ab61103cbe0bcb394_1346_0.png)

# Figure 26.74: Selecting the Data Source

3. Create a connection of the Chart control with the database. In this case, we are creating the connection with the Products table of the northwnd database.

> NOTE
> You can refer to the GridViewControl application for the steps of creating connection with the database.

4. Select the members to display on the x-axis and y-axis. In this application, we have selected the UnitsOnOrder column in the X Value Member drop-down list and the UnitsInStock column in the Y Value Members drop-down list, as shown in Figure 26.75:

![](img/e073a4882197be4ab61103cbe0bcb394_1346_1.png)

# Figure 26.75: Selecting the Members to Display on the Axis

After setting the properties of the Chart control, the Source view of the Default.aspx is shown in Listing 26.14:

# Listing 26.14: Showing the Code for the Default.aspx page

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

5. Press the F5 key on the keyboard to execute the application.The output is as shown in Figure 26.76:

![](img/e073a4882197be4ab61103cbe0bcb394_1347_0.png)

# Figure 26.76: Displaying the Output of the Chart Control

# Using the QueryExtender Control

Let's learn how to use the QueryExtender control to display a set of records, by performing the following steps:

+   1. Create an application and save it as QueryExtenderControl (available on the CD).
+   2. Drag and drop a TextBox and a Button control on the Design view of the Default.aspx page.
+   3. Set the text property of the Button control to Search.
+   4. Drag and drop the LinqDataSource control on the Design view and connect it with the database as done in the LinqDataSource application.
+   5. Drag and drop the GridView control on the Design view of the page and select the data source name as LinqDataSource1 in the Choose Data Source drop-down list.
+   6. Drag and drop a QueryExtender control on the Design view of the Default.aspx and add the highlighted code in the Source view of the Default.aspx page, as shown in Listing 26.15:

# Listing 26.15: Showing the Code of the Default.aspx Page

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

+   7. Press the F5 key on the keyboard to view the output of the QueryExtenderControl application (Figure 26.77).
+   8. Enter the product name in the text box and click the Search button, as shown in Figure 26.77:
