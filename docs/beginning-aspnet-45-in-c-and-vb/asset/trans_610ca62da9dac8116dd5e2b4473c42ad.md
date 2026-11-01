
![](img/eadab2ccd79b253c01a3fdff2321202d_498_0.png)

## 显示和更新数据

### 本章你将学习的内容：

- 如何使用 GridView、DetailsView 和 SqlDataSource 等控件显示、插入、编辑和删除数据
- 如何创建丰富的界面，使用户能够在保持数据完整性的同时，利用 ASP.NET 验证控件插入和编辑数据
- 在应用程序中存储连接字符串的最佳方式，以便轻松更新

### WROX.COM 本章代码下载

你可以在 www.wrox.com/remtitle.cgi?isbn=1118311809 的 Download Code 标签下找到本章的 wrox.com 代码下载。代码位于第 13 章下载中。

在本章中，你将学习如何使用随 ASP.NET 一起提供的流行数据控件来显示、插入、更新和删除数据。除了使用用于在网页上显示和编辑数据的视觉控件外，你还将学习如何使用 SqlDataSource 控件，该控件充当数据库与 ASPX 页面之间的桥梁。

你需要首先查看的是可用的数据控件，下一节将讨论这些控件。

## 数据控件

为了让你能够高效地处理系统中的数据，ASP.NET 提供了两组数据感知控件：数据绑定控件和数据源控件。

第一组包含用于显示和编辑数据的控件，例如用户界面中的 GridView、Repeater 和 ListView 控件。数据源控件用于从数据源（如数据库或 XML 文件）检索数据，然后将此数据提供给数据绑定控件。图 13-1 显示了工具箱数据类别中所有可用的数据控件的完整列表。

以下三个部分提供了数据类别中所有控件的快速概述。在本章的剩余部分，你将更详细地了解其中一些控件以及如何使用它们。

![](img/eadab2ccd79b253c01a3fdff2321202d_499_0.png)

图 13-1

### 数据绑定控件

图 13-1 中描绘的工具箱中的七个控件是所谓的数据绑定控件。你使用它们在网页上显示和编辑数据。GridView、DataList、ListView 和 Repeater 都能够同时显示多行。因此它们通常被称为列表控件。DetailsView 和 FormView 设计为一次显示一行。DataPager 是一个帮助程序控件，用于为 ListView 控件提供分页功能。

### 列表控件

由于 ASP.NET 提供了多个用于显示行列表的控件，你可能会想知道何时选择哪个控件。GridView 是一个非常通用的控件，支持自动分页（行分布在多个“页面”上）、排序、编辑、删除和选择。它像电子表格一样以行和列呈现数据。虽然存在许多为这些行和控件设置样式的可能性（你在第 15 章中会了解更多），但你无法从根本上改变数据的呈现方式。此外，GridView 不允许你直接在底层数据源中插入行。

图 13-2 显示了一个典型的 GridView。

![](img/eadab2ccd79b253c01a3fdff2321202d_499_1.png)

图 13-2

DataList 控件使你能够不仅像 GridView 一样以行呈现数据，还可以以列呈现，从而能够创建类似矩阵的数据呈现方式。该控件可以被认为已弃用，并被功能更强大的 ListView 取代。因此，本书不再进一步讨论 DataList。

Repeater 在输出到浏览器的 HTML 方面为你提供了最大的灵活性，因为该控件本身不会向页面输出添加任何 HTML。因此，它通常用于 HTML 有序或无序列表（<ol> 和 <ul>）以及其他列表，在这些列表中你无法容忍自己的 HTML 中混入不需要的 HTML。你通过控件公开的众多模板定义整个客户端标记。然而，这种灵活性是有代价的：该控件没有内置分页、排序或修改数据的功能。你将在下一章看到更多关于 Repeater 控件的内容。

ListView 在 ASP.NET 3.5 中引入，是 GridView、DataList 和 Repeater 的集大成者组合。它在 ASP.NET 4 和 4.5 中经过了一些更改，使其更容易使用。该控件支持编辑、删除和分页数据，与 GridView 类似。它支持 DataList 提供的多列和多行布局，并且让你能够完全控制控件生成的标记，就像 Repeater 一样。它还支持像 DetailsView 或 FormView 控件那样的插入和更新数据。在下一章中，你将看到更多关于 ListView 控件的内容。

在 ASP.NET 4 中，列表控件扩展了 ClientIDRowSuffix 属性，使你能够指定用于根据数据库中的数据创建唯一客户端 ID 的列的值。为了使它工作，你需要将你在前面章节中看到的 ClientIDMode 属性设置为 Predictable。

在 ASP.NET 4.5 中，控件再次扩展，新增了一个属性：ItemType。你将在下一章看到该属性的使用。

### 单项控件

DetailsView 和 FormView 控件在某些方面相似，因为两者都能够一次显示一条记录。DetailsView 使用内置的表格格式来显示数据，而 FormView 使用模板让你定义数据的外观。一个简单的基于模板的 DetailsView 可能看起来像图 13-3 所示的那样。

![](img/eadab2ccd79b253c01a3fdff2321202d_500_0.png)

FormView 控件和你在第 16 章中看到的一些 Login 控件具有 RenderOuterTable 属性。当你将此属性设置为 False 时（它默认为 True，因此你需要显式设置），控件不会生成包装的 HTML <table> 元素。这反过来会导致更少的代码和更干净的 HTML。两个控件都允许你为不同情况定义模板，例如数据的只读显示，以及数据的插入和更新。你将在本章的后半部分看到如何自定义这些模板：

### 分页控件

另一个有用的控件是 DataPager，它能够为其他控件提供分页。目前，你只能使用它来扩展 ListView 控件，但随着 .NET Framework 的未来版本，这可能会改变。ListView 和 DataPager 控件将在第 14 章中讨论。

为了让数据绑定控件显示有用的内容，你需要为它们分配数据源。要将此数据源绑定到控件，有两种主要方法：你可以将数据分配给控件的 DataSource 属性，或者使用单独的数据源控件。在后面的章节中，你将看到如何使用 DataSource 属性；不同的数据源控件是下一节的主题。

## 数据源控件

工具箱的数据类别包含六个不同的数据源控件，可用于将数据绑定到你的数据绑定控件。XmlDataSource 和 SiteMapDataSource 控件用于将分层、基于 XML 的数据绑定到这些控件。你在第 7 章创建站点地图时看到了 SiteMapDataSource 的使用。

ObjectDataSource 控件使你能够将数据绑定控件连接到应用程序中的单独对象。不是将数据感知控件直接绑定到数据库，而是将来自具有自定义对象的单独层的数据绑定到它们。如果你想了解更多关于 ObjectDataSource 控件的信息，请获取 Wrox 的 Professional ASP.NET 4.5（ISBN 978-1-118-31182-0）的一份副本。

最后三个数据源控件是 SqlDataSource、EntityDataSource 和 LinqDataSource 控件。前两个分别在本章和第 14 章中讨论。LinqDataSource 作为 LINQ to SQL 的数据源，LINQ to SQL 是一种类似于你在第 14 章中了解更多内容的 ADO.NET Entity Framework 的技术。由于微软现在推广 Entity Framework 而不是 LINQ to SQL，我不会在本书中讨论 LinqDataSource 控件。

QueryExtender 控件就像 LinqDataSource 和 EntityDataSource 控件的附加组件，它使你能够在不手动编写大量代码的情况下为搜索特定数据创建丰富的过滤界面。你可以在本文中了解更多关于 QueryExtender 的信息：http://bit.ly/92kMPQ.

## 其他数据控件

工具箱中的最后一个控件是 Chart 控件。它最初作为 Visual Studio 2008 的附加组件发布，但现在已完全集成到 VS 2012 中。它旨在呈现从简单条形图到 3D 饼图和花哨的线图等图表图形。我不会进一步讨论此控件，但你可以在这里找到一系列详细讨论它的文章：http://tinyurl.com/nsnbvv.

在下一节中，你将看到如何使用 SqlDataSource 和 GridView 从数据库检索和显示数据。后面的章节和章节将更深入地探讨其他数据控件。

## 数据源控件和数据绑定控件协同工作

SqlDataSource 控件使你能够快速创建功能性、基于数据库的网页。在不编写大量代码的情况下，你可以创建网页，使你能够执行 CRUD 缩写中的全部四个操作：创建、读取、更新和删除数据。虽然其名称可能意味着该控件只能访问 Microsoft 的 SQL Server，但事实并非如此。该控件还可以访问其他数据库，例如 Oracle 或 MySQL。

### 使用 GridView 显示和编辑数据

为了让你了解 SqlDataSource 控件如何与数据绑定控件协同工作，下一个 Try It Out 将向你展示如何创建一个非常简单的基于数据的网页，该网页
