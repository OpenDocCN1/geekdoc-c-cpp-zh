
大于、小于某个值。

编写语法时，务必记住 WHERE 条件位于 FROM 语句之后。可使用的运算符类型因你筛选的数据类型而异。

-   **等于（EQUALS）** — 这用于查找精确匹配项。下面的语法对包含精确字符串“Value”的列使用 WHERE 子句。请注意，字符串两侧需要单引号，而数值不需要。

```sql
SELECT Column_Name1, Column_Name2
FROM Table_Name
WHERE Column_Name3 = 'Value'
```

-   **介于（BETWEEN）** — 通常用于查找某个数字范围或日期范围之间的值。需要注意的是，BETWEEN 比较运算符中的第一个值应小于右侧的值。请注意下面在 10 和 100 之间进行比较的示例。

```sql
SELECT Column_Name1, Column_Name2
FROM Table_Name
WHERE Column_Name3 BETWEEN 10 AND 100
```

-   **大于、小于、小于或等于、大于或等于** — SQL Server 提供了可用于比较特定值的比较运算符。

```sql
SELECT Column_Name1, Column_Name2
FROM Table_Name
WHERE Column_Name3 <= 1000 --Note that you can also use <, >, >= or even <> for not equal to
```

-   **LIKE（模糊匹配）** — 这会搜索列中包含的值或字符串。你仍然要使用单引号，但需包含百分号，以指示字符串位于开头、末尾还是字符串范围之间的任意位置。

```sql
SELECT Column_Name1, Column_Name2
FROM Table_Name
WHERE Column_Name3 LIKE '%Value%' --Searches for the word 'value' in any field
```

```sql
SELECT Column_Name1, Column_Name2
FROM Table_Name
WHERE Column_Name3 LIKE 'Value%' --Searches for the word 'value' at the beginning of the field
```

```sql
SELECT Column_Name1, Column_Name2
FROM Table_Name
WHERE Column_Name3 LIKE '%Value' --Searches for the word 'value' at the end of the field
```

-   **IS NULL 和 IS NOT NULL（为空和不为空）** — 如前所述，NULL 是包含无数据的空单元格。在数据库中，你将使用确实包含 NULL 值的表，可以通过几种方式处理这些值。

```sql
SELECT Column_Name1, Column_Name2
FROM Table_Name
WHERE Column_Name3 IS NULL --Filters any value that is NULL in that column, but don't put NULL in single quotes since it's not considered a string.
```

```sql
SELECT Column_Name1, Column_Name2
FROM Table_Name
WHERE Column_Name3 IS NOT NULL --Filters any value that is not NULL in that column.
```

再次使用 Production.Product 表，选择 Product ID、Name、Product Number 和 Color。筛选颜色为银色的产品。

## 使用 ORDER BY

ORDER BY 子句仅用于按升序或降序对数据排序，并通过你要排序的列来指定。此命令默认也按升序排序，因此如果要按降序排序，请在命令中使用 DESC。

```sql
SELECT Column_Name1, Column_Name2
FROM Table_Name
WHERE Column_Name3 = 'Value'
ORDER BY Column_Name1, Column_Name2 --Sorts in ascending order, but you can also include ASC to sort in ascending order.
```

```sql
SELECT Column_Name1, Column_Name2
FROM Table_Name
WHERE Column_Name3 = 'Value'
ORDER BY Column_Name1, Column_Name2 DESC --This sorts the data in descending order by specifying DESC after the column list.
```

从 Production.Product 表中选择 Product ID、Name、Product Number 和 List Price，其中 List Price 介于 $100.00 和 $400.00 之间。然后，按 List Price 从小到大对结果排序。

（提示：查询中不会使用 $；如有需要，可以回顾你刚刚复习过的排序选项。）

## 数据定义语言（DDL）

> “没有什么比咄咄逼人的愚蠢更糟糕的了。”——约翰·沃尔夫冈·冯·歌德

DDL 是用于在实例或数据库本身中创建、修改或删除对象的 SQL 语法。以下是一些示例，可帮助你入门。DDL 分为三类命令：

-   **创建（CREATE）** — 这将在数据库或实例中创建对象，例如其他数据库、表、视图等。

```sql
--Creates a Database
CREATE DATABASE DatabaseName
--Creates a schema (or container) for tables in the current database
CREATE SCHEMA SchemaName
--Creates a table within the specified schema
CREATE TABLE SchemaName.TableName
(
Column1 datatype PRIMARY KEY,
Column2 datatype(n),
Column3 datatype
)
--Creates a View
CREATE VIEW ViewName
AS
SELECT
Column1,
Column2
FROM TableName
```

-   **修改（ALTER）** — 此命令允许你修改现有对象，例如向表中添加额外的列或更改数据库名称。

```sql
--Alters the name of the database
ALTER DATABASE DatabaseName MODIFY NAME = NewDatabaseName
```

```sql
--Alters a table by adding a column
ALTER TABLE TableName

ADD ColumnName datatype(n)
```

-   **删除（DROP）** — 此命令允许你删除数据库中的对象或数据库本身。它可用于删除表、触发器、视图、存储过程等。请注意，这些项将不再存在于你的数据库中——或者，如果你删除数据库，该数据库将不复存在。

```sql
--Drops a Database - use the master db first
USE master
GO
```

```sql
--Then drop the desired database
DROP DATABASE DatabaseName
GO
```

```sql
--Drops a table; should be performed in the database where the specified table exists
DROP TABLE Table_Name
```

```sql
--Drops a view from the current database
DROP VIEW ViewName
```

### 应用 DDL 语句

在你的计算机上单击“New Query”按钮打开一个新的查询窗口，并确保你使用的是“master”数据库。

你可以通过查看下方并使用下拉菜单来确认当前使用的数据库，并在数据库之间切换。

![](img/239ff1e8a63502805c86c4dfbd71509a_162_0.png)

回到[编写 T-SQL 语法指南](#)部分，你学习了“USE”语句以及使用“GO”拆分代码批次。

你将在下一个练习中使用这些内容。因此，在练习之前或练习期间，请随时回顾该部分。

创建一个名为 Company 的数据库。别忘了在使用 master 数据库和创建新数据库之间使用 GO 语句！

执行此操作后，你现在将拥有一个可以开始向其添加表的数据库。下面是一系列练习，你将在其中开始在此数据库中创建第一个架构和表。

创建一个名为 Dept 的架构。你将在下一个练习中创建的表将与此架构关联。

创建一个名为 Department 的表。该表应有两列：Department_Id，应为整数数据类型并作为主键。另一列应为 Department_Name，其数据类型应为 30 字节的 VARCHAR。

将你的数据库名称从 Company 更改为 Company_Db。

### 运行 DDL 脚本

现在，该下载以下 DDL 脚本，以创建你将使用的其余表了。别担心，我已编写好该脚本，单击“Execute”按钮即可成功运行。只需确保你已正确完成练习，否则它不会工作。

完成此操作后，你将开始运用 DML 知识来添加和检索数据。

## 数据操纵语言（DML）

DML 或数据操纵语言正如其名；它操纵数据。作为 DML 一部分的语句允许你修改现有数据、创建新数据，甚至删除数据。

请注意，DML 并不专门针对修改表结构或数据库设置之类的对象，而是处理这些对象中的数据。

-   **选择（SELECT）** — 这条语句是最常见的 SQL 语句，它允许你检索数据。它也用于许多报表场景。

```sql
--Selects two columns from a table
SELECT

Column_Name1,

Column_Name2

FROM Table_Name
```

-   **插入（INSERT）** — 这条语句允许你将数据插入特定数据库的表中。

```sql
--Inserts three rows into the table
INSERT INTO Table_Name

(Column_Name1, Column_Name2) --These two items are the columns

VALUES
```
