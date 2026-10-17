
```asp
@Page Language="C#" AutoEventWireup="true" CodeFile="TreeViewData.aspx.cs" Inherits="TreeViewData">
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <meta name="server">
    <title></title>
  </head>
  <body>
    <form id="form" runat="server">
      <div>
        <asp:XmlDataSource ID="XMLDataSource" runat="server" DataFile="Navigation.xml" />
        <asp:Label ID="Label" runat="server" Text="来自 XMLDataSource 的 TreeView" />
        <br />
        <asp:TreeView ID="TreeView11" runat="server" DataSourceID="XMLDataSource">
          <DataBindings>
            <asp:NodeBinding DataMember="homepage" NavigateUrl="TreeViewDatabase.aspx" TextField="title" Tooltip="title" />
            <asp:NodeBinding DataMember="subpage" NavigateUrl="TreeViewData.aspx" TextField="title" Tooltip="title" />
            <asp:NodeBinding DataMember="subpage" NavigateUrl="SiteMapDataSource.aspx" TextField="title" Tooltip="title" />
          </DataBindings>
        </asp:TreeView>
      </div>
    </form>
  </body>
</html>
```

# 立即解决方案

![](img/17af790174c480761404624aeed9b30b_588_0.png)

图 12.13：为站点添加映射

点击“添加新项”对话框上的“添加”（Add）按钮。这将打开 `web.sitemap` 文件；然后将文件内容替换为以下内容：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<sitemap xmlns="http://schemas.microsoft.com/ASNET/Sitemap-File-1.0">
  <sitemode type="TreeView" content="Default.aspx" />
  <sitemode type="TreeView" content from database url="/Default.aspx" />
  <sitemode type="TreeView" with XMLDataSource url="/TreeViewDataBase.aspx" />
  <sitemode type="TreeView" with XMLDataSource url="/TreeViewXMLDataSource.aspx" />
</sitemode>
</sitemap>
```

现在，向 `TreeViewMapDataSource.aspx` 页面添加以下行代码以添加参数：

```asp
<asp:SiteDataSource ID="SiteDataSource" runat="server" />
```

`SiteDataSource` 控件会自动链接到我们在此应用程序中添加的 `web.sitemap` 文件。让我们添加一个根据此 SiteMapData 控件填充的 TreeView 控件。您可以在 TreeViewControl 应用程序的 `TreeViewMapDataSource.aspx` 页面第 124 行找到它：

## 列表 12.4：TreeViewMapDataSource.aspx 页面的代码

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
  <head runat="server">
  <title>TreeView Control Example</title>
</head>
<body>
  <form id="form1" runat="server">
  <asp:Label ID="Label" runat="server" Text="TreeView generated from SiteDataSource"/></asp:Label><br />
  <asp:SiteDataSource ID="SiteMapSource1" runat="server" />
  <asp:TreeView ID="TreeView2" DataSourceID="SiteMapSource1" runat="server">
  
  <DataBindings>
  <asp:TreeViewNode TextField="Title" NavigateUrlField="url" />
```

```html
<DataBindings>
  <asp:TreeView>
</asp:TreeView>
</form>
</body>
</html>
```

您可以在图 12.14 中看到上述列表的输出：

![](img/17af790174c480761404624aeed9b30b_589_0.png)

# 从数据库生成 TreeView

如果您想在数据库（例如 SQL Server）上生成 TreeView 控件，您需要使用 `TreeView` 类通过编程方式来生成 TreeView 控件，因为没有可用的向导可以实现此操作。我们将为当前示例扩展 TreeViewControl。只需向应用程序中添加一个名为 `TreeDatabase.aspx` 的新表。我们将显示来自 Northwind 数据库中 Categories 表的。。您可以在列表 12.5 中找到 `TreeDatabase.aspx` 页面的代码：

## 列表 12.5：TreeDatabase.aspx 的代码

```asp
<%@Page Language="C#" AutoEventWireup="true" CodeFile="TreeDatabase.aspx.cs" Inherits="TreeDatabase" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
  <title>TreeView Control Example</title>
</head>
<body>
  <form id="form" runat="server">
    <div>
      <asp:Label id="Label1" runat="server" Text="TreeView control bind to SQL Server Northwind database" Font-Bold="true"></asp:Label><br />
      <asp:TreeView id="TreeView1" runat="server" MaxDataDepth="2" width="260px">
        <Nodes>
          <asp:TreeViewNode OnNodePopulate="true" Text="Categories and their products" Value="Customer" />
        </Nodes>
      </asp:TreeView>
    </div>
  </form>
</body>
</html>
```

# 立即解决方案

现在，将代码添加到 `TreeDatabase.aspx` 页面的后台代码文件中，如列表 12.6 所示：

## 列表 12.6：TreeDatabase.aspx 页面后台文件的代码

```csharp
using System;
using System.Collections;
using System.Data;
using System.Data.SqlClient;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.Controls;

public class TreeDatabase : System.Web.UI.Page
{
    public void GetCategoryNodes(TreeNode node)
    {
        SqlCommand sqlCommand = new SqlCommand("Select CategoryName, CategoryID FROM Categories");
        DataSet Result = null;
        Result = populateDataFunction(sqlCommand);
        if (Result.Tables.count > 0)
        {
            foreach (DataRow row in Result.Tables[0].Rows)
            {
                TreeNode TreeNode = new TreeNode(row["CategoryName"].ToString());
                TreeNode.Value = row["CategoryID"].ToString();
                TreeNode.PopulateOnDemand = true;
                TreeNode.Selection = TreeNodeSelectAction.Expand;
                node.Children.Add(TreeNode);
            }
        }
    }

    public void GetTreePopulate(TreeNode node)
    {
        SqlCommand sqlQuery = new SqlCommand("Select ProductName From Products WHERE CategoryID = @category");
        sqlQuery.Parameters.Add("@category", SqlDbType.Int).Value = node.Value;
        DataSet DataSet = populateDataFunction(sqlQuery);
        if (DataSet.Tables.count > 0)
        {
            foreach (DataRow row in DataSet.Tables[0].Rows)
            {
                TreeNode TreeNode = new TreeNode(row["ProductName"].ToString());
                TreeNode.PopulateOnDemand = false;
                TreeNode.Selection = TreeNodeSelectAction.None;
                node.Children.Add(TreeNode);
            }
        }
    }

    public DataSet populateDataFunction(SqlCommand sqlCommand)
    {
        SqlConnection dbConnection = new SqlConnection("Data Source=.; Catalog=Northwind;Integrated Security=true;");
        SqlDataAdapter dbAdapter = new SqlDataAdapter(sqlCommand);
        DataSet resultsDataSet = new DataSet();
        try
        {
            sqlCommand.Connection = dbConnection;
            dbAdapter.Fill(resultsDataSet);
        }
        catch (Exception ex)
        {
            // Handle exception
        }
        return resultsDataSet;
    }

    protected void TreeView1_NodePopulate(object sender, TreeNodeEventArgs e)
    {
        if (e.Node.Children.Count == 0)
        {
            switch (e.Node.Depth)
            {
                case 0:
                    GetCategoryNodes(e.Node);
                    break;
                case 1:
                    GetTreePopulate(e.Node);
                    break;
            }
        }
    }

    protected void Page_Load(object sender, EventArgs e)
    {
        TreeView1.ExpandDepth = 1;
    }
}
```

# 第 12 章：ASP.NET 4.5 中的导航控件

## 创建静态菜单

ASP.NET 4.5 中的菜单可以通过简单地将工具箱中的 Menu 控件拖放到设计器中来轻松创建。你可以通过双击工具箱中的 Menu 控件来添加静态菜单。Menu 控件会自动添加到设计器中。点击智能标记（smart tag），并在列表中选择“编辑菜单项”（Edit Menu Items）。将出一个 Menu Item 对话框。根据你的要求注意不同层级的项目。你也可以通过设置属性面板中的 `Text` 属性来设置菜单的文本，如图 12:16 所示。

![](img/17af790174c480761404624aeed9b30b_593_0.png)

插入节点后，点击 OK 按钮。将 `Default.aspx` 页面的代码替换为列表 12:10 所示的 MenuControl 应用程序。

```
Listing 12.10: Default.aspx 页面代码
<@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx"
Inherits="Default">
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Menu Example</title>
</head>
<body>
<form id="form1" runat="server">
<asp:Label Id="label1" runat="server" Text="Static Menu with vertical orientation="vertical"></asp:Label><br />
<br />
<asp:Menu Id="Menu1" runat="server" BackColor="#B5C7D7"
DynamicHorizontalOffset="False" Font-Name="Font" Size="Medium" ForeColor="#E4E4E4"
StaticMenuItems="true">
<StaticMenuTypeStyle HorizontalPadding="5px" VerticalPadding="2px" />
<DynamicMenuStyle BackColor="#E4E4E4" ForeColor="White" />
<StaticSelectedItem BackColor="#50D7C1" />
<DynamicSelectedStyle BackColor="#50D7C1" VerticalPadding="2px" />
<Items>
<asp:MenuItem Text="MenuItem1" Value="MenuItem1">
<asp:MenuItem Text="MenuItem1Leaf" Value="MenuItem1Leaf" />
<asp:MenuItem Text="MenuItem1Leaf2" Value="MenuItem1Leaf2" />
</asp:MenuItem>
</Items>
</asp:Menu>
</form>
</body>
</html>
```
