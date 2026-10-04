

# 本章你学到的内容

| | |
|---||-|
| CRUD | 用于数据库中处理数据的四种基本 SQL 操作：创建（Create）、读取（Read）、更新（Update）和删除（Delete） |
| 外键 | 指定表中中的某一列，它引用另一个表的主键，以实施引用完整性 |
| 标识 (Identity) | 分配给新行的自动顺序数字 |
| JOIN | 允许你在查询中表示两个或多个表之间的关系，以查找相关数据 |
| 主键 | 由表中的一个或多个列组成，用于唯一标识表中的某行 |
| 关系型数据库 | 一种数据库，数据存储在单独的、类似电子表格的表中，这些表可以相互引用 |
| 关系 | 定义一个或多个表之间的关系，并帮助你实施引用完整性 |
| 表 | 数据库中的一种对象，允许你存储数据 |

# 13

## 显示和更新数据

在本章你将学习到：

- 如何使用 GridView、DetailsView 和 DataSource 等控件显示、插入、编辑和删除数据
- 如何使用 ASP.NET 验证控件创建一个丰富的界面，使用户在插入和编辑数据的同时维护数据完整性
- 在应用程序中存储连接字符串的最佳方法，以便于后续更新

本章的 WROX.COM 代码下载

你可以在 www.wrox.com/go/beaspnet451 的 Download Code 标签上找到本章的 wrox.com 代码下载。代码位于第 13 文件夹中。

在本章中，你将学习如何使用 ASP.NET 自带的热门数据控件显示、插入、更新和删除数据。除了用于在网页中显示和编辑数据的视觉控件，你还将学习如何使用 SqlDataSource 控件，它是数据库与 ASPX 页面之间的桥梁。

你首先需要查看的是可用的数据控件，将在下一节中讨论。

## 数据控件

为了让你能够高效地处理系统中的数据，ASP.NET 提供了两组数据感知控件：数据绑定控件和数据源控件。

第一组包含你用于显示和编辑数据的控件，例如用户界界面中的 GridView、Repeater 和 ListView 控件。数据源控件用于从数据源（如数据库或 XML 文件）检索数据，然后为数据绑定控件提供数据。图 13-1 显示了工具箱中 Data 类别下可用数据控件的完整列表。

接下来的三个章节提供了 Data 类别所有控件的快速概述。在本章的剩余部分，你将更详细地了解这些控件的工作原理以及如何使用它们。

### 数据绑定控件

图 13-1 所示工具箱中的七个控件是所谓的数据绑定控件。你使用它们在你的网页上显示和编辑数据。GridView、DataList、ListView 和 Repeater 都用于同时显示多行，它们也被称为列表控件。DetailsView 和 FormView 设计用于一次显示单行。DataPager 是一个辅助控件，用于为 ListView 控件提供分页功能。

### 列表控件

由于 ASP.NET 提供了多个控件来显示列表

图 13-2 显示了一个典型的 GridView。

| Id | Title | CreateDateTime |
|---|---|---|
| 编辑 编辑 选择 | 17 | Renato Cohen 写的 Sixteen Drum Bricks | 6/12/2009 12:52:53 PM |
| 编辑 编辑 选择 | 18 | Depeche Mode 的 Sounds Of The Universe - 翻车还是杰作* | 6/12/2009 10:10:12 PM |
| 编辑 编辑 选择 | 19 | Miss Kitty & The Hacker 的 First Album | 6/6/2009 08:50:38 PM |
| 编辑 编辑 选择 | 20 | Dinosaur Jr 的 Farm | 6/23/2009 10:36:01 PM |
| 1 2 3 4 5 6 | | |

图 13-2

DataList 控件允许你不仅像 GridView 那样以行形式呈现数据，还可以以列的形式，使你能够创建类似矩阵的数据呈现方式。该控件可以被认为是过时的，并被更强大的 ListView 取代。因此，本书将不再进一步讨论 DataList。

![](img/9e033e3b9560597824f8b22941d6d8bb_477_0.png)

Repeater 在输出到浏览器的 HTML 方面提供了最大的灵活性，因为该控件本身不会向页面输出中添加任何 HTML，因为它经常用于 HTML 有序列表 `<ol>` 和无序列表 `<ul>` 以及其他你无法承受不必要的 HTML 与你自己的代码混杂的列表。通过该控件暴露的许多模板来定义整个标记。然而，这种灵活性是有代价的：该控件没有内置的排序、分页或修改数据的功能。你将在下一章中看到更多 Repeater 控件。

ListView 是 ASP.NET 3.5 中引入的，它是 GridView、DataList 和 Repeater 的完美结合。它在 ASP.NET 4 和 4.5 中经过了一些变化，使其更更容易操作。该控件支持数据的编辑、删除和分页。在 ASP.NET 4 和 4.5 中发生的一些变化使得它更更容易工作。在 ASP.NET 4 中，某些变化使得它更更容易工作。在 ASP.NET 4.5 中，某些变化使得它更更容易工作。

### 单行控件

DetailsView 和 FormView 设计用于一次显示单行。

| Id | Title | CreateDateTime |
|---|---|---|
| 编辑 编辑 选择 | 17 | 6/12/2009 12:52:53 PM |
| 编辑 编辑 选择 | 18 | 6/12/2009 10:10:12 PM |
| 编辑 编辑 选择 | 19 | 6/6/2009 08:50:38 PM |
| 编辑 编辑 选择 | 20 | 6/23/2009 10:36:01 PM |

由于 ASP.NET 提供了多个控件来显示列表

另一个有用的控件是 DataPager，它为 ListView 提供分页功能。

### 数据源控件

工具箱中的 Data 类别包含六种不同的数据源控件，你可以用它们绑定数据绑定控件。XmlDataSource 和 SiteMapDataSource 用于绑定分级数据，你将在第 7 章创建站点地图时看到 MapDataSource。ObjectDataSource 控件允许你将数据绑定控件连接到单独的对象。与其直接将数据绑定到数据库，不如从单独的对象层绑定数据。如果你想了解更多关于 ObjectDataSource 控件的信息，请购买《Professional ASP.NET 4.5》(978-1-118-31821-0）。最后三个数据源控件是 SqlDataSource、EntityDataSource 和 LinDataSource。第一个将在本章中讨论。LinDataSource 作为 LINQ to SQL 的源，这种技术类似于你学过的 ADO.NET Framework。

由于 Microsoft 现在推广 Entity Framework 而不是 LINQ to SQL，我不再在本章中讨论 LinDataSource 控件。EntityDataSource 用于旧版本的 Entity Framework，并且没有针对最新版本进行更新。与其使用该控件，Microsoft 建议使用在下一章详细讨论的 Model Binding 概念。

QueryExtender 控件类似于 LinDataSource 和 EntityDataSource 控件的扩展，它允许你创建一个丰富的过滤界面来搜索特定数据，而无需编写大量代码。你可以在这里了解更多关于 QueryExtender 的信息：http://bit.ly/92kMPQ。

工具箱中的最后一个控件是 Chart 控件。它最初作为 VS 2008 的插件发布，但它设计用于从简单的条形图到 3D 饼图和折线图渲染图表。你将不会进一步讨论该控件，但你可以在这里找到系列详细讨论它的文章：http://tinyurl.com/nsnbvv。

在下一节中，你将看到如何使用 SqlDataSource 和 GridView 从数据库中检索并显示数据。

