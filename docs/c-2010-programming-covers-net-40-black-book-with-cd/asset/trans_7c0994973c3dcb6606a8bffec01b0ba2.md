

# 第 15 章：ASP.NET 4.0 中的导航控件

通过右键单击解决方案名称并在解决方案资源管理器中的上下文菜单中选择 Add New Item 选项来添加我们的解决方案。在 Add New Item 对话框中，从可用模板列表中选择 Site Map Template 并将其命名为 Web.sitemap，如图 15.13 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_767_0.png)

图 15.13：向解决方案添加站点地图

单击 Add New Item 对话框的 Add 按钮。这将打开 Web.sitemap 文件；然后用以下代码替换文件的内容：

```
<?xml version="1.0" encoding="utf-8" ?>
<siteMap xmlns="http://schemas.microsoft.com/AspNet/SiteMap-File-1.0" >
  <siteMapNode title="Treeview Control Example" url="~/default.aspx" >
    <siteMapNode title="Treeview from database" url="~/treeviewdatabase.aspx"/>
    <siteMapNode title="Treeview with XMLDataSource" url="~/treeviewxmldat.aspx"/>
    <siteMapNode title="Treeview with SiteMapDataSource" url="~/TreeViewSiteMapDataSource.aspx"/>
  </siteMapNode>
</siteMap>
```

现在在 TreeViewSiteMapDataSource.aspx 页面中添加以下代码行以添加 SiteMapDataSource 控件：

```
<asp:SiteMapDataSource ID="SiteMapSource1" runat="server" />
```

SiteMapDataSource 控件会自动链接到我们在本应用程序中添加的 Web.sitemap 文件。让我们添加一个 TreeView 控件，它将基于此 SiteMapDataSource 控件进行填充。您可以在清单 15.4 中找到 TreeViewControl 应用程序的 TreeViewSiteMapDataSource.aspx 页面的代码：

# 清单 15.4：显示 TreeViewSiteMapDataSource.aspx 页面的代码

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="TreeViewSiteMapDataSource.aspx.cs" Inherits="TreeViewSiteMapDataSource" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Treeview Control Example</title>
</head>
<body>
<form id="form1" runat="server">
<div>
```

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

您可以在图 15.14 中看到前面清单的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_768_0.png)

# 从数据库生成 TreeView

如果您想基于数据库，例如 SQL Server 生成 TreeView 控件，则需要使用 TreeView 类以编程方式生成 TreeView 控件，因为没有可用的向导。

我们将为当前示例扩展我们的 TreeViewControl 应用程序。只需向应用程序添加一个名为 TreeViewDataBase.aspx 的新 Web 表单。我们使用 SQL Server 的 Northwind 数据库。在此应用程序中，我们将在 TreeView 控件中显示来自 Northwind 数据库的 Categories 表中的类别及其各自来自 Products 表中的产品。您可以在清单 15.5 中找到 TreeViewControl 应用程序的 TreeViewDataBase.aspx 页面的代码：

**清单 15.5：显示 TreeViewDataBase.aspx 页面的代码**

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
```csharp
{
    foreach (DataRow row in ResultSet.Tables[0].Rows)
    {
        TreeNode NewNode = new TreeNode(row["productName"].ToString());
        NewNode.PopulateOnDemand = false;
        NewNode.SelectAction = TreeNodeSelectAction.None;
        node.ChildNodes.Add(NewNode);
    }
}

public dataset PopulateDataFunction(SqlCommand sqlQuery)
{
    SqlConnection dbConnection = new SqlConnection("Data Source=AVANTIKA-PC\\SQLEXPRESS;Initial Catalog=Northwind;Integrated Security=True");
    SqlDataAdapter dbAdapter = new SqlDataAdapter();
    dbAdapter.SelectCommand = sqlQuery;
    sqlQuery.Connection = dbConnection;
    DataSet resultsDataSet = new DataSet();
    try
    {
        dbAdapter.Fill(resultsDataSet);
    }
    catch (Exception ex)
    {
    }
    return resultsDataSet;
}

protected void Treeview2_TreeNodePopulate(object sender,
    System.Web.UI.WebControls.TreeNodeEventArgs e)
{
    if (e.Node.ChildNodes.Count == 0)
    {
        switch (e.Node.Depth)
        {
            case 0:
                GetCategories(e.Node);
                break;
            case 1:
                GetProducts(e.Node);
                break;
        }
    }
}

protected void Page_Load(object sender, EventArgs e)
{
    Treeview2.ExpandDepth = 1;
}
```
```

为了理解前面的代码，我们现在将逐步讨论代码。在第一步中，我们将添加 TreeView2_TreeNodePopulate 方法的代码，如清单 15.7 所示：

# 清单 15.7：显示 TreeView2_TreeNodePopulate 方法的代码

```
```csharp
protected void Treeview2_TreeNodePopulate(object sender,
    System.Web.UI.WebControls.TreeNodeEventArgs e)
{
    if (e.Node.ChildNodes.Count == 0)
    {
        switch (e.Node.Depth)
```

```
case 0:
    GetCategories(e.Node);
    break;
case 1:
    GetProducts(e.Node);
    break;
}
```

前面的清单检查 TreeView2 控件是否存在。如果发现 TreeView2 控件中不存在任何节点，则调用 GetCategories 函数以生成包含类别名称的第一级节点。在 GetCategories 函数中，我们查询数据库以检索记录并使用 node.ChildNodes.Add 方法生成第一级树节点，如清单 15.8 所示：

# 清单 15.8：显示生成第一级树节点的代码

```
public void GetCategories(TreeNode node)
{
    SqlCommand sqlQuery = new SqlCommand("Select CategoryName, CategoryID From Categories");
    DataSet ResultSet = null;
    ResultSet = PopulateDataFunction(sqlQuery);
    if (ResultSet.Tables.Count > 0)
    {
        foreach (DataRow row in ResultSet.Tables[0].Rows)
        {
            TreeNode NewNode = new TreeNode(row["CategoryName"].ToString(), row["CategoryID"].ToString());
            NewNode.PopulateOnDemand = true;
            NewNode.SelectAction = TreeNodeSelectAction.Expand;
            node.ChildNodes.Add(NewNode);
        }
    }
}
```

生成作者名称后，代码再次检查 TreeView2_TreeNodePopulate 事件，这次调用 GetProducts 函数以生成第二级节点，其中包含相应类别中的产品，其名称已通过 GetCategories 函数从数据库中检索，如清单 15.9 所示：

# 清单 15.9：显示从数据库检索产品名称的代码

```
public void GetProducts(TreeNode node)
{
    SqlCommand sqlQuery = new SqlCommand();
    sqlQuery.CommandText = "Select ProductName From Products where CategoryID = @categoryid";
    sqlQuery.Parameters.Add("@categoryid", SqlDbType.Int).Value = node.Value;
    DataSet ResultSet = PopulateDataFunction(sqlQuery);
    if (ResultSet.Tables.Count > 0)
    {
        foreach (DataRow row in ResultSet.Tables[0].Rows)
        {
            TreeNode NewNode = new TreeNode(row["ProductName"].ToString());
            NewNode.PopulateOnDemand = false;
            NewNode.SelectAction = TreeNodeSelectAction.None;
            node.ChildNodes.Add(NewNode);
        }
    }
}
```

