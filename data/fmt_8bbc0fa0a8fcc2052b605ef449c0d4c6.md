
8. 按 `F5` 键运行 `WCFDataServiceSite` 应用程序。运行应用程序时，您会发现一个带有文本 `HELLO WORLD` 的 Web 页面。您可以通过在 Internet Explorer 的地址栏中添加以下 Web 地址来检索 `Products` 表的第一条目：
`http://localhost:5461/WCFDataServiceSite/MyDataService.svc/Products(1)`
图 25.32 显示了 `WCFDataServiceSite` 应用程序的输出：

## 图 25.32：在网页上显示数据

#### 注意

如果你的 Web 浏览器未显示输出，即图 25.32 所示的输出，请执行以下步骤：

- 1. 选择 Tools→Internet Options。Internet 选项对话框打开。
- 2. 选择 Content 选项卡。
- 3. 在 Feeds and Slices 组框中单击 Settings 按钮。Feed and Web Slice Settings 对话框出现。
- 4. 清除 Turn on feed reading view 复选框并单击 OK 按钮，如图 25.33 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1253_0.png)

## 图 25.33：显示 Feed and Web Slice Settings 对话框

现在，让我们总结本章讨论的主要主题。

## 摘要

在本章中，你学习了如何将数据绑定到 Windows 和 WPF 应用程序。你还学习了 Windows Forms 应用程序中的基本数据绑定概念。接下来，你学习了 Windows Forms 应用程序中的数据绑定类型。此外，你还学习了如何将数据绑定到 Windows Forms 应用程序中的不同控件。本章还解释了 WPF 的数据绑定概念。接下来，你学习了数据绑定的不同数据源、数据绑定的声明以及将数据绑定到集合。最后，你学习了如何使用 WCF 数据服务绑定 SQL 数据。

这些概念的实际实现在本章的 Immediate Solutions 部分中介绍。

在下一章中，你将学习如何在 ASP.NET 应用程序中绑定数据。

## 26

## ASP.NET 应用程序中的数据绑定

| 如果你需要 Immediate Solution 来： | 请参见页码： |
|---|---|
| 使用 SqlDataSource 控件 | 1258 |
| 使用 AccessDataSource 控件 | 1264 |
| 使用 LinqDataSource 控件 | 1268 |
| 使用 ObjectDataSource 控件 | 1273 |
| 使用 XmlDataSource 控件 | 1276 |
| EntityDataSource 控件 | 1280 |
| 使用 GridView 控件 | 1285 |
| 使用 DataList 控件 | 1289 |
| 使用 DetailsView 控件 | 1292 |
| 使用 FormView 控件 | 1294 |
| 使用 Repeater 控件 | 1297 |
| 使用 ListView 和 DataPager 控件 | 1300 |
| 使用 Chart 控件 | 1304 |
| 使用 QueryExtender 控件 | 1307 |

## 深入探讨

什么是数据库？为什么我们需要数据库？.NET 应用程序如何与数据库协作？在学习 ASP.NET 中使用数据库控件之前，我们需要知道这些问题的答案。

数据库是以表格形式系统存储的记录或信息的集合，以便计算机程序在需要时可以轻松访问信息。结构化查询语言（SQL）用于检索、存储、删除和更新数据库中存储的记录。应用程序可能需要使用数据库来执行各种功能，例如：

- 通过从数据库检索记录以表格格式显示数据
- 在处理从数据库检索的记录后显示数据，例如计算每位员工的服务年限然后显示记录
- 处理检索到的数据并将其更新到数据库中
- 根据应用程序用户指定的选择或条件从数据库中删除记录

在本章中，你将学习 ASP.NET 4.0 支持的各种数据源和数据绑定控件的使用。数据绑定控件是复合控件，与数据源控件一起使用以在基于 Web 的应用程序中显示和修改数据。以下是数据绑定控件的列表：

- GridView 控件
- DataList 控件
- DetailsView 控件
- FormView 控件
- ListView 控件
- Repeater 控件
- DataPager 控件
- Chart 控件
- QueryExtender 控件

同样，数据源控件允许你使用不同类型的数据源，例如 SQL Server 或可扩展标记语言（XML）文件。以下是数据源控件的列表：

- SqlDataSource 控件
- AccessDataSource 控件
- LinqDataSource 控件
- ObjectDataSource 控件
- XmlDataSource 控件
- SiteMapDataSource 控件
- EntityDataSource 控件

现在，让我们从 GridView 控件开始详细讨论。

## GridView 控件

GridView 控件是一个数据绑定控件，以表格形式显示数据源的值。在此表中，每列代表一个字段，每行代表一条记录。GridView 控件存在于 `System.Web.UI.WebControls` 命名空间中。GridView 控件的继承层次结构如下：

```
System.Object

  System.Web.UI.Control

    System.Web.UI.WebControls.WebControl

      System.Web.UI.WebControls.BaseDataBoundControl

        System.Web.UI.WebControls.DataBoundControl
```

`System.Web.UI.WebControls.CompositeDataBoundControl`
`System.Web.UI.WebControls.GridView`

当你将 GridView 控件拖放到设计器页面上时，以下语法将添加到页面的源视图中：

```
<asp:GridView ID="GridView1" runat="server"> </asp:GridView>
```
