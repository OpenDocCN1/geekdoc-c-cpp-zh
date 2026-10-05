

# 第 17 章 数据库编程简介 521

##构成 MMBooks 数据库的表

| Customers（客户） | Invoices（发票） |
| :--- | :--- |
| CustomerID | InvoiceID |
| Name | CustomerID |
| Address | InvoiceDate |
| City | ProductTotal |
| State | SalesTax |
| ZipCode | Shipping |
| | InvoiceTotal |
| States（州） | InvoiceLineItems（发票行项目） |
| StateCode | InvoiceID |
| StateName | ProductCode |
| | UnitPrice |
| | Quantity |
| OrderOptions（订单选项） | ItemTotal |
| SalesTax | |
| FirstBookShipCharge | ProductCode |
| AdditionalBookShipC | Description（描述） |
| UnitPrice | |
| OnHandQuantity（现库存量） | |

### 描述

Customers 表包含每个客户的一行数据。其主键是 CustomerID，这是一个标识列，在创建新客户时自动生成。State 是一个外键，将每个客户与 States 表中的行关联起来。
- Invoices 表包含每个发票的一行数据。其主键是 InvoiceID，这是一个标识列，在创建新发票时自动生成。CustomerID 是一个外键，将每张发票与一个客户关联。
- InvoiceLineItems 表包含发票中每个行项目的一行。其主键是 InvoiceID 和 ProductCode 的组合。InvoiceID 是一个外键，将每个行项目与一个发票关联，ProductCode 是一个外键，将每一行与一个产品关联。
- Products 表包含每个产品的一行数据。其主键是 ProductCode，这是一个 10 字符，用于标识每个产品。
- States 表包含每个州的一行数据。其主键是 StateCode。
- OrderOptions 表包含一个州的单行数据，用于存储应用程序使用的销售税和运费。
- 图中表之间的关系显示为连线，端点表示关系的类型。键表示关系的“一”的一侧，而无穷大符号（∞）表示“多”的一侧。

图 17-6 MMBooks 数据库的设计

## 如何使用 SQL 操作关系型数据库

在接下来的主题中，你将学习用于操作数据库数据的四种 SQL 语句：Select、Insert、Update 和 Delete。要掌握书中的材料，你需要理解这些语句的作用以及它们是如何重新编码的。

尽管你将在接下来的主题中学习编写这些语句的基础知识，但你可能想了解比这里展示的更多。在这种情况下，我们推荐我们的书籍《Murach's SQL Server 2008 for Developers》。除了 Select、Insert、Update 和 Delete 语句外，这本书还教你如何编写用于定义数据库中数据的语句，并教你如何使用专业人士使用的 SQL Server 的其他功能。

尽管 SQL 是一种标准语言，但每个数据库管理系统（DBMS）可能都有其自己的 SQL 方言，其中包含了对标准语言的扩展。因此，当你使用 SQL 时，需要确保你使用的是你的 DBMS 支持的方言。在本章和整本书中，所有的 SQL 示例都是针对 Microsoft SQL Server 方言，称为 Transact-SQL。

## 如何查询单表

图 17-7 显示了如何使用 Select 语句查询数据库中的单表。在图顶部的语法摘要中，你可以看到 Select 子句指定了要检索的列名，而 From 子句指定了包含这些列的表名。你还可以编写一个 Where 子句，为被选定的行提供标准。你可以编写一个 Order By 子句，指定结果应按一个或多个列进行排序，并指示每个列应按升序还是降序排序。

如果你学习语法摘要下方的 Select 语句，就可以看到它是如何工作的。在这里，Select 语句从住在华盛顿州的所有客户的表中检索了两列。它通过 Name 列对返回的行进行排序。

此图还显示了 Select 语句返回的结果表或结果集。结果集是在数据库内部临时的逻辑表。当应用程序从数据库请求数据时，它会接收结果集。

# 第 17 章 数据库编程简介 523

## Select 语句的简化语法

```
Select column-1 [, column-2]...
From table-1
[Where selection-criteria]
[Order By column-1 [Asc] [Desc], column-2 [Asc] [Desc]]...]
```

## Select 语句从 Customers 表中检索并排序选定的列

```
Select Name, City
From Customers
Where State = 'WA'
Order By Name
```

## Select 语句定义的结果集

| Name | City |
| :--- | :--- |
| Allen, Craig | Pullman |
| Antalocy, S. | Seattle |
| Cassara, Glenn | Van |
| Giraka, Eric | Kennewickrick |
| Hester, Maurice | Seattle |
| Howell, Kim | Renton |
| Mcmillen, G | Kirkland |
| Millard, Dwayne | Seattle |
| Oneil, Ri | Olympia |
| Seaver, Glenda | Mountlake Terr... |
| Smith, Lloyd | Pullman |
| Sundaram, Kelly | Oregon |

## 概念

- Select 语句的结果是一个结果表或结果集，如所示。
- 结果集是一个逻辑行集，包含了所有请求的列和行。
- Select 子句列出了包含在结果集中列。
- From 子句指定了从哪个表检索数据。
- Where 子句提供了一个条件，指定应该检索哪些行。
- Order By 子句列出了结果排序的列，并指示每个列是升序还是降序序列。
- 要选择表中的所有列，可以使用星号（*）来代替列名。例如：`Select * From Customers`

图 17-7 如何查询单表

## 如何从两个或多个表连接数据

图 17-8 展示了从两个表检索数据的 Select 语句语法。这种操作被称为“连接（join）”，因为来自两个表的数据连接成了一个单一的结果集。例如，图中的 Select 语句将来自 InvoiceLineItems 和 Products 表的数据连接成单个结果集。

内连接（inner join）是最常见的连接类型。当你使用内连接时，只有当两个表中的相关列匹配时，这两个表中的行才会被包含在结果集中。这些匹配的列在 Select 语句的 From 子句中指定。例如，在图中 Select 语句中，只有当 Products 表中的 ProductCode 值匹配 InvoiceLineItems 表中某几行的 ProductCode 值时，才会包含 InvoiceLineItems 和 Products 表的行。

注意 Select 子句中的每个列都指示了从哪个表检索。例如，InvoiceID、ProductCode、UnitPrice 和 Quantity 列来自 InvoiceLineItems 表，但 description 列来自 Products 表。只有存在于两个表中的列才需要限定限定（qualification）。在这种情况下，只有 ProductCode 列需要限定，因为 InvoiceLineItems 和 Products 表都有名为 ProductCode 的列。然而，我建议对所有列进行限定，以明确每个列是从哪个表检索的。

尽管此图显示了如何从两个表连接数据，但你应该知道可以扩展此语法来连接更多表的数据。例如，如果你想在包含 InvoiceLineItems 和 Products 数据的同时包含 Invoices 表的数据，你可以像这样编写 From 子句：

```
From Invoices
  Join InvoiceLineItems
    On Invoices.InvoiceID = InvoiceLineItems.InvoiceID
  Join Products
    On InvoiceLineItems.ProductCode =
    Products.ProductCode
```

那么，在 Select 语句的列列表中，你可以包含 Invoices、InvoiceLineItems 和 Products 表中的任何列。

