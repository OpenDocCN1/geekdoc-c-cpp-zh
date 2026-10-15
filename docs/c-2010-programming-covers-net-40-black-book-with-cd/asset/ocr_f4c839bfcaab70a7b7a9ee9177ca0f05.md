```
```aspx
<asp:Label ID="Label12" runat="server" Text="TreeView generated from SiteMapDataSource"></asp:Label><br />
<br />
<asp:SiteMapDataSource ID="SiteMapSource1" runat="server" />
<asp:TreeView ID="TreeView2" DataSourceID="SiteMapSource1" runat="server">
  <DataBindings>
    <asp:TreeNodeBinding TextField="Title" NavigateUrlField="Url" />
  </DataBindings>
</asp:TreeView>
</div>
</form>
</body>
</html>
```
```

You can see the output of the preceding listing in Figure 15.14:

![](bbox=[0.227, 0.28, 0.762, 0.557])

# Generating TreeView from a Database

In case you want to generate TreeView control based on the database, such as SQL Server, you need to generate the TreeView control programmatically by using the TreeView class, since no wizard is available for this.

We will extend our TreeViewControl application for the current example. Just add a new Web form named TreeViewDataBase.aspx to the application. We are using Northwind database of the SQL Server. In this application, we will display the categories from the Categories table and their respective products from the Products table of the Northwind database in the TreeView control. You can find the code for the TreeViewDataBase.aspx page of the TreeViewControl application in Listing 15.5:

**Listing 15.5: Showing the Code for TreeViewDataBase.aspx Page**

```
```aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="TreeViewDataBase.aspx.cs" Inherits="TreeViewDataBase" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
  <title>TreeView Control Example</title>
</head>
<body>
  <form id="form1" runat="server">
    <div>
```
```