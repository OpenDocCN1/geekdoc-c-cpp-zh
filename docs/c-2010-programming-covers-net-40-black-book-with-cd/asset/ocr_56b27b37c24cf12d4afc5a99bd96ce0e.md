![](bbox=[0.15, 0.06, 0.76, 0.39])

# Figure 26.10: Selecting the Data Source

After configuring the data source, the Default.aspx page for the SqlDataSource application is shown in Listing 26.1:

# Listing 26.1: Showing the Code of the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" codeFile="default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
</div>
<asp:SqlDataSource ID="SqlDataSource1" runat="server" ConnectionString="<%$ ConnectionStrings:northwindConnectionString %>" SelectCommand="SELECT [ProductID], [ProductName], [QuantityPerUnit], [UnitPrice], [UnitsInStock] FROM [Alphabetical list of products]">
</asp:SqlDataSource>
<asp:GridView ID="Gridview1" runat="server" AutoGenerateColumns="False" DataKeyNames="ProductID" DataSourceID="SqlDataSource1">
<Columns>
<asp:BoundField DataField="ProductID" HeaderText="ProductID" InsertVisible="False" ReadOnly="True" SortExpression="ProductID" />
<asp:BoundField DataField="ProductName" HeaderText="ProductName" SortExpression="ProductName" />
<asp:BoundField DataField="QuantityPerUnit" HeaderText="QuantityPerUnit" SortExpression="QuantityPerUnit" />
<asp:BoundField DataField="UnitPrice" HeaderText="UnitPrice" SortExpression="UnitPrice" />
<asp:BoundField DataField="UnitsInStock" HeaderText="UnitsInStock" SortExpression="UnitsInStock" />
</Columns>
</asp:GridView>
</form>
</body>
</html>
```