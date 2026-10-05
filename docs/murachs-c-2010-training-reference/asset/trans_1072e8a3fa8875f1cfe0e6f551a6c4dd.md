

## 用于连接两个表的 Select 语句的语法

```
Select column-list
From table-1
[Inner] Join table-2
On table-1.column-1 (=|<|>|>=|=|) table-2.column-2
[Where selection-criteria]
[Order By column-list]
```

一个连接 InvoiceLineItems 和 Products 表中数据的 Select 语句

```
Select InvoiceLineItems.InvoiceID, InvoiceLineItems.ProductCode,
Products.Description, InvoiceLineItems.UnitPrice,
InvoiceLineItems.Quantity
From InvoiceLineItems
Inner Join Products
On Products.ProductCode = InvoiceLineItems.ProductCode
Where InvoiceID = 46
```

## Select 语句定义的 Result集

| InvoiceID | ProductCode | Description | UnitPrice | Quantity |
|---|---|---|---|---|
| 46 | AJ3B | Murach's ASP... | 54.000 | 1 |
| 46 | DB2R | DB2 for the CO... | | 1 |
| 46 | SQL8 | Murach's SQL S... | 52.500 | 1 |
| 46 | VB08 | Murach's Visual... | 54.000 | 1 |

## 概念

- 连接（join）允许你将两个或多个表的数据合并到单个结果集中。
- 最常见的连接类型是内连接（inner join）。这种类型的连接仅当相关列匹配时才返回表中的行。

![](img/3148667e42d4db35b3d08576aaa1fa01_544_0.png)

## 如何在表中添加、更新和删除数据

图 17-9 显示了 SQL Insert、Update 和 Delete 语句的基本语法。你使用这些语句向表中添加新行、更新现有行中的数据以及删除现有行。

要向表中添加单行，你需要指定要添加该行的表名，以及你为哪些列提供数据的列名（例如，这些列的值）。例如，图中的语句向 Products 表添加了此行。如果你将为表中的所有列提供值，可以省略列名。如果你这样做，必须确保指定的值的顺序与列在表中出现的顺序一致。为了避免错误，我建议你始终编写列列表。

注意，如果表包含标识列（identity column），则你不应在 Insert 语句中为该列提供值。相反，SQL Server 在插入行时会为标识列生成一个值。

同样注意，可以使用单引号来标识字符串。例如，ProductCode 列的字符串被包含在单引号中。然而，如果字符串值包含单引号，你可以编写两个单引号。例如，Description 列的字符串使用两个单引号来标识 *Murach's* 中的单引号。

要更改表中一个或多个列的值，你将使用 Update 语句。在该条语句中，你指定要更新的表名、你想要更改的列以及一个标识你想要更改的行的条件。在图中的示例中，Update 语句将产品代码为 MCCP 的产品的 UnitPrice（单）列改为 54.00。

要从表中删除行，你使用 Delete 语句。在该条语句中，你指定要从其删除行的表，以及一个指示你想要删除的行的条件。图中的 Delete 语句删除了 Customers 表中客户 ID 558 的所有行。

## 如何添加单行

添加单行的 Insert 语句语法

```
Insert [Into] table-name ([column-list])
Values (value-list)
```

## 向 Products 表添加一行的语句

```
Insert Into Products (ProductCode, Description, UnitPrice, OnHandQuantity)
Values ('CS10', 'Murach''s C# 2010', 54.50, 3000)
```

## 如何更新行

Update 语句的语法

```
Update table-name
Set expression-1 = [, expression-2]...
[Where selection-criteria]
```

## 更新指定产品 UnitPrice 列的语句

``````
Update Products
Set UnitPrice = 54.00
Where ProductCode = 'MCCP'
```

## 如何删除行

Delete 语句的语法

```
Delete [From] table-name
[Where selection-criteria]
```

## 删除指定客户的语句

```
Delete From Customers
Where CustomerID = 558
```

## 描述

- 你使用 Insert、Update 和 Delete 语句来维护数据库表中的数据。
Insert 语句可用于向表中添加一个或多行。虽然上面显示的语法仅用于添加一行，但还有另一种用于添加多行的语法。
Update 和 Delete 语句可以使用上述语法来更新或删除表中的一个或多行。

![](img/3148667e42d4db35b3d08576aaa1fa01_546_0.png)

## ADO.NET 简介

ADO.NET（ActiveX Data Objects）是访问数据的主要 API。它分为两类：提供数据库访问的数据提供程序（data providers）和用于存储的数据集（datasets）。

数据提供程序

.NET 数据提供程序是一组提供数据库访问的类。它们被分为两类：提供数据库访问的数据提供程序和用于存储的数据集。

（注：原文中第 547 页的 OCR 文本存在严重重复和损坏，已根据标准 ADO.NET 上下进行逻辑处理。）

