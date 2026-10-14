

## 如何从两个或多个表中联接数据

图 12-6 展示了用于从两个表中检索数据的 Select 语句的语法。这种操作称为联接，因为来自两个表的数据被联接成一个单一的结果集。例如，本图中的 Select 语句将 Categories 和 Products 表中的数据联接成一个单一的结果集。

内联接是最常见的联接类型。当你使用内联接时，只有当联接中两个表的相关列匹配时，这些行才会被包含在结果集中。这些匹配的列在 Select 语句的 From 子句中指定。例如，在本图中的 Select 语句中，只有当 Categories 表中的 CategoryID 列的值与 Products 表中一个或多个行中的 CategoryID 列的值匹配时，Categories 和 Products 表中的行才会被包含。如果某个类别没有产品，则该类别不会被包含在结果集中。

请注意，本语句中的 Select 子句并未指明每个列包含在哪个表中。那是因为每个列只存在于其中一个表中。然而，如果某个列同时存在于两个表中，你就需要指明你想要检索该列的表。例如，如果你想从 Categories 表中检索 CategoryID 列，你需要像这样编码该列：

```
Categories.CategoryID
```

尽管本图展示了如何从两个表中联接数据，但你应该知道，你可以扩展此语法以联接来自更多表的数据。例如，如果你想在本图显示的结果中包含 LineItems 表的数据，你可以像这样编码 Select 语句的 From 子句：

```
From Categories
    Inner Join Products
        On Categories.CategoryID = Products.CategoryID
    Inner Join LineItems
        On Products.ProductID = LineItems.ProductID
```

然后，在 Select 语句的列列表中，你可以包含 LineItems 表中的任何列。

## 联接两个表的 Select 语句的语法

```
Select column-list
From table-1
    [Inner] Join table-2
    On table-1.column-1 {=|<|>|<=|>=|< >} table-2.column-2
[Where selection-criteria]
[Order By column-list]
```

## 一个联接 Products 和 Categories 表数据的 Select 语句

```
Select ShortName, ProductID, Name, UnitPrice
From Categories Inner Join Products
    On Categories.CategoryID = Products.CategoryID
Order By Categories.CategoryID
```

## Select 语句定义的结果集

| ShortName | ProductID | Name | UnitPrice |
|---|---|---|---|
| Costumes | frankc01 | Frankenstein | 39.9900 |
| Costumes | hippie01 | Hippie | 79.9900 |
| Costumes | jar01 | JarJar | 59.9900 |
| Costumes | martian01 | Martian | 69.9900 |
| Costumes | pow01 | Austin Powers | 79.9900 |
| Costumes | super01 | Superman | 39.9900 |
| FX | tlm01 | T&L Machine | 99.9900 |
| FX | fog01 | Fog Machine | 34.9900 |
| FX | fogj01 | Fog Juice (1qt) | 9.9900 |
| FX | skullfog01 | Skull Fogger | 39.9500 |
| FX | str01 | Mini-strobe | 13.9900 |
| FX | bl01 | Black Light (24") | 24.9900 |
| Masks | fred01 | Freddie | 29.9900 |
| Masks | mum01 | Mummy | 39.9900 |
| Masks | vader01 | Darth Vader Ma... | 19.9900 |
| Props | rat01 | Ugly Rat | 14.9900 |
| Props | rat02 | Uglier Rat | 19.9900 |
| Props | ske01 | Life-size Skeleton | 14.9500 |
| Props | head01 | Michael Head | 29.9900 |
| Props | head02 | Saw Head | 29.9900 |
| Props | cat01 | Deranged Cat | 19.9900 |
| Props | arm01 | Freddie Arm | 19.9500 |
| Props | bats01 | Flying Bats | 69.9900 |

## 概念

- 联接让你可以将来自两个或多个表的数据组合成一个单一的结果集。
- 最常见的联接类型是内联接。这种联接类型仅在相关列匹配时才返回来自两个表的行。

## 如何在表中添加、更新和删除数据

图 12-7 展示了 SQL Insert、Update 和 Delete 语句的基本语法。你使用这些语句向表中添加新行、更新现有行中的数据以及删除现有行。

要向表中添加单行，你使用本图所示语法的 Insert 语句。使用此语法，你指定要添加行的表名、你提供数据的列名以及这些列的值。在示例中，Insert 语句向 Categories 表添加一行并为该表中的三个列中的每一个提供值。如果表允许空值或为某些列提供默认值，则 Insert 语句不必为这些列提供值。此外，Insert 语句永远不会为标识列提供值，因为该值由 DBMS 生成。

要更改一个或多个行中一个或多个列的值，你使用 Update 语句。在此语句中，你指定要更新的表名、指示要更改的列以及如何更改它们的表达式，以及标识要更改的行条件的条件。在示例中，Update 语句仅更改 Categories 表中 CategoryID 值为“food”的那一行中的 ShortName 值。

要从表中删除一个或多个行，你使用 Delete 语句。在此语句中，你指定要从中删除行的表以及指示要删除的行的条件。在示例中，Delete 语句仅删除 Categories 表中 CategoryID 列为“food”的那一行。

## 如何添加单行

### 添加单行的 Insert 语句语法

```
Insert [Into] table-name [(column-list)]
Values (value-list)
```

### 添加单行到表的语句

```
Insert Into Categories (CategoryID, ShortName, LongName)
Values ('food', 'Spooky Food', 'The very best in Halloween cuisine')
```

## 如何更新行

### Update 语句的语法

```
Update table-name
    Set expression-1 [, expression-2]...
    [Where selection-criteria]
```

### 更改所选行的 ShortName 列值的语句

```
Update Categories
    Set ShortName = 'Halloween cuisine'
    Where CategoryID = 'food'
```

## 如何删除行

### Delete 语句的语法

```
Delete [From] table-name
    [Where selection-criteria]
```

### 删除指定类别的语句

```
Delete From Categories
    Where CategoryID = 'food'
```

## 描述

- 你使用 Insert、Update 和 Delete 语句来维护数据库表中的数据。
- Insert 语句可用于向表中添加一个或多个行。虽然上面显示的语法是用于添加单行，但还有另一种语法用于添加多行。
- Update 和 Delete 语句可用于使用上面显示的语法更新或删除表中的一个或多个行。

## ADO.NET 4 简介

*ADO.NET 4 (ActiveX Data Objects)* 是 .NET Framework 的主要数据访问 API。它提供了在开发数据库应用程序时使用的类。以下主题将介绍重要的 ADO.NET 概念。

## 基本 ADO.NET 组件如何工作

图 12-8 展示了在开发数据库应用程序时使用的主要 ADO.NET 对象。首先，应用程序使用的数据存储在 *dataset* 中，*dataset* 包含一个或多个 *data tables*。要将数据加载到数据表中，你使用 *data adapter*。

数据适配器的主要功能是管理数据集与数据库之间的数据流。为此，它使用 *commands* 来定义要发布的 SQL 语句。例如，用于检索数据的命令通常定义一个 Select 语句。然后，命令使用 *connection* 连接到数据库并将 Select 语句传递给数据库。Select 语句执行后，它产生的结果集被发送回数据适配器，数据适配器将结果存储在数据表中。

要更新数据库中的数据，数据适配器使用定义数据表 Insert、Update 或 Delete 语句的命令。然后，命令使用连接连接到数据库并执行请求的操作。

尽管在本图中并不明显，但数据集中的数据独立于数据被检索的数据库。事实上，连接通常在数据从数据库检索后关闭。然后，在需要时再次打开连接。正因为如此，应用程序必须使用存储在数据集中的数据的副本。这种用于实现此类数据处理的类型架构被称为 *disconnected data architecture*。尽管这比连接架构更复杂，但其优势抵消了复杂性。

使用断开连接数据架构的一个优势是由于使用更少的系统资源来维护连接而提高系统性能。另一个优势是它与 ASP.NET Web 应用程序配合良好，后者本质上是断开连接的。

负责直接与数据库工作的 ADO.NET 类由 *.NET data providers* 提供。这些数据提供程序包括用于创建数据适配器、命令和连接的类。 .NET Framework 目前包含针对 SQL Server、Oracle、OLE DB 和 ODBC 的数据提供程序，尽管 Oracle 数据提供程序已被弃用。还有其他第三方提供程序可用。

