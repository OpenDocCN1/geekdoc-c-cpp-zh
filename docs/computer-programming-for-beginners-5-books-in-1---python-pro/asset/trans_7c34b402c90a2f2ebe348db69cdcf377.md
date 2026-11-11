
在列中输入。这个表定义会生成一个 CHECK 约束和三列：

```sql
CREATE TABLE BOOK_TITLES
( BOOK_ID     INT,
  BOOK_TITLE  CHARACTER (50) NOT NULL,
  STOCK_AVAILABILITY  INT,
  CONSTRAINT TS_STOCK_AVAILABILITY ( STOCK_AVAILABILITY < 50
  AND STOCK_AVAILABILITY > 1 ) ); ²¹
```

生成的表将拒绝超出 1-50 范围的值。下面是编写该表的另一种方式：

```sql
CREATE TABLE BOOK_TITLES
( BOOK_ID     INT,
  BOOK_TITLE  CHARACTER (50) NOT NULL,
  STOCK_AVAILABILITY  INT CHECK ( STOCK_AVAILABILITY < 50
  AND STOCK_AVAILABILITY > 1 ) );
```

现在，让我们分析这些语句的条件子句。该子句告诉 SQL，添加到 STOCK_AVAILABILITY 列的所有值都必须小于 50。关键字 AND 告知 SQL，还有另一个必须应用的条件。最后，该子句告诉 SQL，添加到上述列的每个值都应大于 1。简而言之，每个值都应小于 50 且大于 1。

这个约束还允许你简单地列出你的“可接受的值”。对于不会经常更改的值，SQL 用户认为这是一个强大的选项。在下一个示例中，你将使用 CHECK 约束来定义图书的体裁：

```sql
CREATE TABLE BOOK_TITLES
( BOOK_ID     INT,
  BOOK_TITLE  CHARACTER (50) ,
  GENRE       CHAR (10) ,
  CONSTRAINT TS_GENRE CHECK ( GENRE IN ( 'DRAMA', 'HORROR',
  'SELF HELP', 'ACTION', 'MYSTERY', 'ROMANCE' ) ) ); ²²
```

GENRE 列中的每个值都应包含在条件所列出的体裁中。如你所见，这条语句使用了 IN（即一个 SQL 运算符）。基本上，IN 确保 GENRE 中的值都包含在所列出的条目中。

这个约束可能会极其令人困惑，因为它涉及大量括号。你可以通过将 SQL 代码分成多行来简化它们。作为示例，让我们重写上面给出的代码：

```sql
CREATE TABLE BOOK_TITLES
(
BOOK_ID      INT,
BOOK_TITLE   CHAR (50) ,
GENRE        CHAR (10) ,
CONSTRAINT TS_GENRE CHECK
(
GENRE IN
( 'DRAMA', 'HORROR', 'SELF HELP', 'ACTION', 'MYSTERY', 'ROMANCE'
)
)
) ;
```

这种编写 SQL 命令的风格可确保代码可读性。在这里，你需要缩进括号及其内容，以便它们清楚地显示其在 SQL 语句不同层级中的位置。通过使用这种风格，你可以快速识别每一对括号中的子句。此外，这条语句的作用与前一条相同。这种风格唯一的缺点是你需要使用大量空格。

让我们分析另一个示例：

```sql
CREATE TABLE BOOK_TITLES
( BOOK_ID      INT,
  BOOK_TITLE   CHAR (50) ,
  STOCK_AVAILABILITY  INT,
  CONSTRAINT TS_STOCK_AVAILABILITY_CHECK ( ( STOCK_AVAILABILITY BETWEEN 1 AND 50 ) OR ( STOCK_AVAILABILITY BETWEEN 79 AND 90 ) ) );
```

这段代码使用 BETWEEN（即另一个 SQL 运算符）来设置一个包含最低点和最高点的范围。由于它有两个范围，因此使用括号分隔范围规范。关键字 OR 连接这些范围规范。基本上，OR 告诉 SQL 需要满足其中一个条件。因此，你在名为 STOCK_AVAILABILITY 的列中输入的值应来自 1 到 50 或 79 到 90。

## 如何定义断言

断言是可以应用于多个表的 CHECK 约束。因此，你不能在定义表时创建断言。下面是创建断言时必须使用的语法：

```sql
CREATE ASSERTION (name of constraint) CHECK (the search conditions)
```

定义断言类似于定义表级 CHECK 约束。输入 CHECK 后，你需要指定搜索条件。

让我们分析一个新示例。假设 BOOK_TITLES 表有一列保存库存图书数量。该表的总计应始终低于你期望的库存量。这个示例使用断言来检查 STOCK_AVAILABILITY 列的总和是否低于 3000。

```sql
CREATE ASSERTION LIMIT_STOCK_AVAILABILITY CHECK ( ( SELECT SUM (STOCK_AVAILABILITY) FROM BOOK_TITLES ) < 3000 ) ;
```

这条语句使用子查询（即“SELECT SUM (STOCK_AVAILABILITY) FROM BOOK_TITLES”）并将其与 3000 进行比较。子查询以 SQL 关键字 SELECT 开头，它从任意表中查询信息。名为 SUM 的 SQL 函数会将 STOCK_AVAILABILITY 中的所有值相加。另一方面，关键字 FROM 指定包含该列的表。然后系统会将子查询的结果与 3000 进行比较。如果你向 STOCK_AVAILABILITY 列添加一个使总和超过 3000 的条目，就会收到错误消息。

## 如何创建域和域约束

如前所述，你也可以将 CHECK 约束插入到域定义中。这种约束与你之前见过的约束类似。唯一的区别是，你不会将域约束附加到特定的表或列。实际上，域约束在引用为该域指定的列中的值时，会使用另一个 SQL 关键字 VALUE。现在，让我们讨论生成新域所需的语法：

```sql
CREATE DOMAIN (name of domain) {AS} (type of data)
{ DEFAULT (the default value) }
{ CONSTRAINT (name of constraint) } CHECK < (the search condition) >
```

这种语法包含你之前见过的元素，因为你在第三章中已经见过默认子句和数据类型。另一方面，约束的定义与最近几节中讨论的约束有一些相似之处。

在下面的示例中，你将生成一个 INT 类型的域。这个域只能接受 1 到 50 之间的值：

```sql
CREATE DOMAIN BOOK_QUANTITY AS INT CONSTRAINT TS_BOOK_QUANTITY CHECK (VALUE BETWEEN 1 AND 50);
```

这个示例涉及一个新项目，即 VALUE 关键字。如前所述，该关键字使用 BOOK_QUANTITY 域来引用列的指定值。因此，如果你输入不满足指定条件的值（即每个值必须在 1 到 50 之间），就会收到错误消息。

格式。你将在后面学习第三行。

你需要在定义的第一部分设置视图的名称。此外，如果你遇到以下任一情况，应命名视图的列：

- 如果你需要执行操作来获取列的值，而不是仅从表中复制这些值。
- 如果你要处理重复的列名。这种情况在组合表时会发生。

即使你不需要，也可以为列设置名称。例如，你可以为列分配逻辑名称，以便即使是没有经验的用户也能理解它们。

格式的第二部分有一个必需的关键字（即 AS）和一个查询占位符。尽管它看起来很简单，但查询占位符可能涉及执行不同操作的复杂 SQL 语句结构。

让我们分析一个基本示例：

```sql
CREATE VIEW BOOKS_IN_STOCK
( BOOK_TITLE, AUTHOR, STOCK_AVAILABILITY ) AS
SELECT BOOK_TITLE, AUTHOR, STOCK_AVAILABILITY

FROM BOOK_INVENTORY¹²
```

这个示例是你可以创建的最简单的视图之一。它从表中获取三列。请记住，SQL 在换行和空格方面并不严格。例如，在创建视图时，你可以将列名（如果适用）列在单独的一行上。数据库管理系统不会在意你使用哪种编码技术。但是，你可以通过采用一种编码风格来确保代码的可读性。

现在，让我们剖析上面给出的示例代码。第一部分将 BOOKS_IN_STOCK 设置为视图的名称。第二部分设置列的名称，并包含 SQL 关键字 AS。

如果你不指定要使用的名称，视图的列将直接复制表的列名。最后两行包含搜索表达式，它是一个 SELECT 语句。如下所示：

```sql
SELECT BOOK_TITLE, AUTHOR, STOCK_AVAILABILITY
```
