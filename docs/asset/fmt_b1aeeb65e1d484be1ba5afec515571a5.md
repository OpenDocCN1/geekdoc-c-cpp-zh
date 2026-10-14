
| fog01 | Fog Machine | 600W Fog mac... | The perfect fog... | fx | fog1.jpg | 34.9900 | 100 |
| fogj01 | Fog Juice (1qt) | 1 qt Bottle of fo... | The drink your ... | fx | fogjuice1.jpg | 9.9900 | 500 |
| frankc01 | Frankenstein | Frankenstein co... | It's alive! | costumes | frank1.jpg | 39.9900 | 100 |
| fred01 | Freddie | Freddie Krueger... | The ultimate in ... | masks | freddy1.jpg | 29.9900 | 50 |
| head01 | Michael Head | Mini Michael M... | For classic horro... | props | head1.jpg | 29.9900 | 100 |
| head02 | Saw Head | Jigsaw head sca... | Perfect for getti... | props | head2.jpg | 29.9900 | 100 |
| hippie01 | Hippie | Women's hippi... | Share the peace... | costumes | hippie01.jpg | 79.9900 | 40 |
| jar01 | Jarlar | Jar Jar Binks | Meesa happy t... | costumes | jarjar1.jpg | 59.9900 | 25 |
| martian01 | Martian | Martian costume | Now includes a... | costumes | martian1.jpg | 69.9900 | 100 |
| mum01 | Mummy | Mummy mask | All wrapped up ... | masks | mummy1.jpg | 39.9900 | 30 |
| pow01 | Austin Powers | Austin Powers ... | Be the most sh... | costumes | powers1.jpg | 79.9900 | 25 |
| rat01 | Ugly Rat | 16" Rat | This guy is sure... | props | rat1.jpg | 14.9900 | 75 |
| rat02 | Uglier Rat | 20" Rat | Yuch! This one ... | props | rat2.jpg | 19.9900 | 50 |
| skel01 | Life-size Skeleton | Life-size plastic ... | This blown plas... | props | skell.jpg | 14.9500 | 10 |
| skullfog01 | Skull Fogger | 2,800 cubic foo... | This fogger put... | fx | skullfog1.jpg | 39.9500 | 50 |
| stro01 | Mini-strobe | Black mini stro... | Perfect for crea... | fx | strobe1.jpg | 13.9900 | 200 |
| super01 | Superman | Superman cost... | Look, up in the ... | costumes | superman1.jpg | 39.9900 | 100 |
| tim01 | T&L Machine | Thunder & Lig... | Flash! Boom! Cr... | fx | tim1.jpg | 99.9900 | 10 |
| vader01 | Darth Vader Ma... | The legendary ... | OB1 has taught... | masks | vader1.jpg | 19.9900 | 100 |

## Concepts

- 关系数据库中的表通过其键列相互关联。例如，`CategoryID` 列用于关联上面的 `Categories` 和 `Products` 表。`Products` 表中的 `CategoryID` 列称为外键，因为它标识 `Categories` 表中的相关行。
- 通常，外键对应于相关表中的主键。但是在 SQL Server 中，外键也可以对应于相关表中的唯一键。
- 当两个表通过外键关联时，具有外键的表称为外键表，具有主键的表称为主键表。
- 数据库中表之间的关系对应于它们所代表的实体之间的关系。最常见的关系类型是图示的 `Categories` 和 `Products` 表所示的一对多关系。一个表也可以与另一个表具有一对一关系或多对多关系。

Figure 12-2 How the tables in a database are related

## How the columns in a table are defined

当你在表中定义一列时，你会像图 12-3 中 `Products` 表的设计所示那样为其分配属性。列的两个最重要的属性是 `Column Name`，它为列提供标识名称，以及 `Data Type`，它指定可以存储在列中的信息类型。使用 SQL Server 时，你可以从此图中的系统数据类型中选择，也可以定义基于系统数据类型的自己的数据类型。当你在表中定义每一列时，你通常会尝试分配将最大限度地减少磁盘存储使用的数据类型，因为这将提高以后查询的性能。

除了数据类型之外，你还必须指出列是否可以存储空值。空值表示未知、不可用或不适用的值。例如，`Products` 表允许其 `ImageFile` 列为空。

你还可以为每个列分配默认值。然后，如果未提供其他值，该值将被分配给该列。如果列不允许空值并且没有默认值，则在向表中添加新行时必须为该列提供值。否则，将发生错误。

每个表还可以包含一个数值列，其值由 DBMS 自动生成。在 SQL Server 中，这样的列称为 `identity column`，并且使用 `Identity`、`Identity Seed` 和 `Identity Increment` 属性来建立。标识列通常用作表的主键。

`check constraint` 定义了列的可接受值。例如，你可以为此图中的 `Products` 表定义一个 `check constraint`，以确保 `UnitPrice` 列大于零。这种 `check constraint` 可以在列级别定义，因为它仅涉及它所约束的列。但是，如果列的 `check constraint` 需要引用表中的其他列，则可以在表级别定义。

在你定义数据库的约束之后，它们由 DBMS 管理。例如，如果用户尝试添加违反约束的数据行，DBMS 会向应用程序发送适当的错误代码，而不会将该行添加到数据库中。然后应用程序可以响应错误代码。

另一种选择是在程序尝试将其添加到数据库之前验证将要添加到数据库的数据。这样，约束可能就不需要了，程序应该运行得更高效。在许多情况下，同时使用数据验证和约束。这样，如果数据验证例程有效，程序运行得更高效，但如果数据验证例程无效或未编码，约束仍然存在。

## Products 表的 Server Explorer 设计视图窗口

![](img/c024ccf88e28c30c07dd410d4342288f_402_0.png)

## Common SQL Server data types

| Type | Description |
|------|-------------|
| bit | A value of 1 or 0 that represents a True or False value. |
| char, varchar, text | Any combination of letters, symbols, and numbers. |
| date, time, datetime, smalldatetime | Alphanumeric data that represents a date, a time, or both a date and time. Various formats are acceptable. |
| decimal, numeric | Numeric data that is accurate to the least significant digit. The data can contain an integer and a fractional portion. |
| float, real | Floating-point values that contain an approximation of a decimal value. |
| bigint, int, smallint, tinyint | Numeric data that contains only an integer portion. |
| money, smallmoney | Monetary values that are accurate to four decimal places. |

## Description

- 分配给列的 *data type* 决定了可以存储在列中的信息类型。根据数据类型，列定义还可以包括其长度、精度和比例。
- 每个列定义还指示列是否可以包含 *null values*。空值表示列的值未知。
- 可以为列定义 *default value*。然后，如果在向表中添加行时未提供其他值，则使用该值。
- 列也可以定义为 *identity column*。标识列是数值列，其值在向表中添加行时自动生成。
- 为了限制列可以保存的值，你定义 *check constraints*。`Check constraints` 可以在列级别或表级别定义。

## 万圣节数据库的设计

现在你已经了解了关系数据库的基本元素的工作原理，图 12-4 显示了本书记述的编程示例中使用的万圣节数据库的设计。尽管这个数据库看起来可能很复杂，但它的设计实际上比你在实际数据库应用程序工作中遇到的大多数数据库要简单得多。

万圣节数据库的目的是跟踪在线万圣节产品商店中下的订单。为此，数据库必须跟踪的不仅是发票，还包括产品和客户。

该数据库的核心表是 `Invoices` 表，其中包含公司客户下的每个订单的一行。该表的 `primary key` 是 `InvoiceNumber` 列，它是一个 `identity` 列。因此，发票号码会在创建新发票时由 SQL Server 自动生成。

`LineItems` 表包含每个发票的明细行。该表的 `primary key` 是 `InvoiceNumber` 和 `ProductID` 列的组合。`InvoiceNumber` 列将每个明细行与发票关联，`ProductID` 列将每个明细行与产品关联。因此，每个发票对于给定产品只能有一个明细行。

`Products` 和 `Categories` 表协同工作以存储万圣节商店提供的产品信息。`Category` 表只有三列：`CategoryID`、`ShortName` 和 `LongName`。`CategoryID` 列是一个 10 字符的代码，用于唯一标识每个类别。`ShortName` 和 `LongName` 列提供了类别的两种不同描述，应用程序可以根据显示类别信息时可用的空间来使用。

`Products` 表包含每个产品的一行。其 `primary key` 是 `ProductID` 列。`Name`、`ShortDescription` 和 `LongDescription` 列提供了有关产品的描述性信息。`ImageFile` 列提供了描绘产品的单独图像文件的文件名（如果存在）。该列仅指定每个图像文件的文件名，而不是完整路径。本书中的应用程序将图像文件存储在应用程序主目录下名为 `Images` 的目录中，因此应用程序知道在哪里找到它们。如果产品没有图像，则该列包含 `null` 值。

`Customers` 表包含每个曾在万圣节商店购买过的客户的一行。该表的 `primary key` 是客户的电子邮件地址。该表中的其他列包含客户的姓名、地址和电话号码。`State` 列将每个客户与 `States` 表中的一个州关联。`States` 表的 `primary key` 是 2 字符的 `StateCode` 列。

## 构成万圣节数据库的表

![](img/c024ccf88e28c30c07dd410d4342288f_404_0.png)

## 描述

- `Categories` 表包含每个产品类别的一行。其 `primary key` 是 `CategoryID`，一个标识每个类别的 10 字符代码。
- `Products` 表包含每个产品的一行。其 `primary key` 是 `ProductID`，一个标识每个产品的 10 字符代码。`CategoryID` 是外键，将每个产品与 `Categories` 表中的一行关联。
- `States` 表包含每个州的一行。其 `primary key` 是 `StateCode`，一个标识每个州的 2 字符代码。
- `Customers` 表包含每个客户的一行。其 `primary key` 是 `Email`，通过其电子邮件地址标识每个客户。`State` 是外键，将每个客户与 `States` 表中的一行关联。
- `Invoices` 表包含每个发票的一行。其 `primary key` 是 `InvoiceNumber`，一个在创建新发票时自动生成的 `identity` 列。`CustEmail` 是外键，将每个发票与 `Customers` 表中的一行关联。
- `LineItems` 表包含每个发票的每个明细项的一行。其 `primary key` 是 `InvoiceNumber` 和 `ProductID` 的组合。`InvoiceNumber` 是外键，将每个明细项与发票关联，`ProductID` 是外键，将每个明细项与产品关联。
- 该图中表之间的关系显示为链接，其中端点指示关系的类型。键表示关系的“一方”，无穷大符号（∞）表示关系的“多方”。

## 如何使用 SQL 在关系数据库中操作数据

在接下来的主题中，你将学习可用于操作数据库中数据的四条 SQL 语句：`Select`、`Insert`、`Update` 和 `Delete`。虽然你在接下来的主题中将学习编写这些语句的基础知识，但你可能希望了解的比这里介绍的更多。在这种情况下，我们推荐我们的书籍《Murach’s SQL Server 2008 for Developers》。除了 `Select`、`Insert`、`Update`、`Delete` 语句外，该书还教你如何编写用于定义数据库中数据的语句，并教你如何使用顶级专业人士使用的 SQL Server 的其他功能。

尽管 SQL 是一种标准语言，但每个 DBMS 很可能都有自己的 SQL 方言，其中包括对标准语言的扩展。因此，当你使用 SQL 时，你需要确保你使用的是 DBMS 支持的方言。在本章和整本书中，所有 SQL 示例都是针对 Microsoft SQL Server 的方言，即 `Transact-SQL`。

## 如何查询单个表

图 12-5 显示了如何使用 `Select` 语句查询数据库中的单个表。在该图顶部的语法摘要中，你可以看到 `Select` 子句命名要检索的列，`From` 子句命名包含这些列的表。你还可以编写 `Where` 子句，为要选择的行的条件提供标准。并且你可以编写 `Order By` 子句，命名结果应按其排序的一个或多个列，并指示每个列应按升序还是降序排序。

如果你研究语法摘要下方的 `Select` 语句，你可以看到其工作原理。这里，`Select` 语句从 `Products` 表检索三列。它仅在行的 `CategoryID` 列的值为“Props”时选择该行。并且它按 `UnitPrice` 对返回的行进行排序，因此最便宜的产品首先列出。

该图还显示了由 `Select` 语句返回的结果表，或结果集。结果集是在数据库内临时创建的逻辑表。当应用程序从数据库请求数据时，它会收到一个结果集。

尽管这里没有显示，但你应该意识到，结果集可以包含从表中其他列计算得出的列。例如，你可以通过将 `Products` 表中的 `OnHand` 列乘以 `UnitPrice` 列来为 `Products` 表中的每个产品创建总价值列。此类列称为计算列，它仅存在于查询的结果中。

### Select 语句的简化语法

```
Select column-1 [, column-2]...
From table-1
[Where selection-criteria]
[Order By column-1 [Asc|Desc] [, column-2 [Asc|Desc]]...]
```

### 一个从 Products 表检索并排序所选列和行的 Select 语句

```
Select ProductID, Name, UnitPrice
From Products
Where CategoryID = 'props'
Order By UnitPrice
```

### Select 语句定义的结果集

|  | ProductID | Name | UnitPrice |
|---|---|---|---|
| ▶ | skel01 | Life-size Skeleton | 14.9500 |
|  | rat01 | Ugly Rat | 14.9900 |
|  | arm01 | Freddie Arm | 19.9500 |
|  | cat01 | Deranged Cat | 19.9900 |
|  | rat02 | Uglier Rat | 19.9900 |
|  | head01 | Michael Head | 29.9900 |
|  | head02 | Saw Head | 29.9900 |
|  | bats01 | Flying Bats | 69.9900 |

## 概念

- `Select` 语句的结果是一个 *结果表*，或 *结果集*，如上所示。结果集是由 `Select` 语句请求的所有列和行组成的逻辑行集。
- 结果集可以包含从表中其他列计算的 *计算列*。
