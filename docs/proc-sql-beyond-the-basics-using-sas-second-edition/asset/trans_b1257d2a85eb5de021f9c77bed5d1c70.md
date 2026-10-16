

视图在应用程序中多次重复使用查询或子查询时也很有益。在这些情况下，添加视图只需更改一次，从而通过减少时间和资源来提高生产率。应考虑创建视图库，以便组织中的用户能够像使用宏一样轻松访问一系列生产率例程。

## 视图不是什么

视图不是表，但它们是包含访问一个或多个底层表的已编译代码的文件构造。因为视图不物理存储数据，所以它们被称为“虚拟”表。与表不同，视图不物理包含或存储数据行。然而，视图确实具有物理存在并占用空间。视图的存储需求很小，因为唯一保存的部分是 SELECT 语句或查询本身。另一方面，表在其结构中存储一个或多个数据行及其属性。

视图使用 CREATE VIEW 语句创建，而表使用 CREATE TABLE 语句创建。因为你使用一个或多个底层表来创建一个虚拟（派生）表，所以视图为你提供了访问数据源的强大方法。

尽管视图具有许多独特而强大的功能，但它们也存在陷阱。首先，视图通常比表处理时间更长。每次引用视图时，都会访问并处理当前的底层表或表。因为视图在被访问之前不会被物理物化，所以可以预期更高的利用成本，特别是对于较大的视图。此外，因为视图不是数据文件（表）并且不包含数据，所以无法为视图创建索引。但是，如果视图是从具有定义索引的数据文件创建的，那么 SQL 优化器可能会尝试在处理其关联的 WHERE 子句表达式时使用该索引。最后，如果在同一程序中多次使用视图的结果，将结果保存并在表中重用可能更有效，从而避免多次重新执行（物化）视图。

## 视图类型

视图可以设计来实现多个目标：

- 引用单个表
- 在一行上生成汇总数据
- 隐藏敏感信息
- 创建可更新视图
- 基于汇总函数或 HAVING 子句的分组数据
- 使用集合运算符
- 在连接操作中组合两个或多个表
- 在另一个视图中嵌套一个视图

为了区分各种类型的视图，Joe Celko 引入了一种基于所用 SELECT 语句类型的分类系统。参见《SQL for Smarties: Advanced SQL Programming》（Morgan Kaufman, 1999）。

为了帮助你理解不同的视图类型，本章描述并说明了视图的构造以及它们如何被使用。视图也可以具有一种或多种视图类型的特征，从而被归类为混合类型。例如，混合视图可以设计为引用两个或多个表、执行更新并包含复杂计算。表 8.1 介绍了不同的视图类型及其目的的简要描述。

## 表 8.1：各种视图类型的描述

| 视图类型 | 描述 |
|---|---|
| 单表视图 | 单表视图引用单个底层（基）表。它是最常见的视图类型。可以根据需要显示或隐藏选定的列和行。 |
| 计算列视图 | 计算列视图提供跨行的汇总数据。 |
| 只读视图 | 只读视图防止数据被更新（与可更新视图相反）并且仅用于显示数据。这也用于隐藏敏感信息的保护目的。 |
| 可更新视图 | 可更新视图添加（插入）、修改或删除数据行。 |
| 分组视图 | 分组视图使用基于包含 GROUP BY 子句的查询的查询表达式。 |
| 集合操作视图 | 集合操作视图包括两个表的并集、删除重复行、结果的连接以及查询结果的比较。 |
| 连接视图 | 连接视图基于两个或多个基表的连接。这种类型的视图通常用于表查找操作，以将编码数据扩展（或翻译）为文本。 |
| 嵌套视图 | 嵌套视图基于一个视图依赖于另一个视图，例如使用子查询。 |
| 混合视图 | 一种或多种视图类型的集成，用于处理更复杂的任务。 |

## 创建视图

你使用 SQL 过程中的 CREATE VIEW 语句来创建视图。当 SQL 处理器读取 CREATE VIEW 关键字时，它期望找到分配给新创建视图的名称。SELECT 语句定义分配给视图列的名称及其顺序。

视图通常构造为列顺序与基表不同。在下一个示例中，视图的列出现的顺序与原始 MANUFACTURERS 基表不同。视图的 SELECT 语句在此步骤中不会执行，因为其唯一目的是在 CREATE VIEW 语句中定义视图。

### SQL 代码

```
PROC SQL;
    CREATE VIEW MANUFACTURERS_VIEW AS
        SELECT manuname, manunum, manucity, manustat
            FROM MANUFACTURERS;
QUIT;
```

### SAS 日志结果

```
PROC SQL;
    CREATE VIEW MANUFACTURERS_VIEW AS
        SELECT manuname, manunum, manucity, manustat
            FROM MANUFACTURERS;
NOTE: SQL view WORK.MANUFACTURERS_VIEW has been defined.
    QUIT;
NOTE: PROCEDURE SQL used:
    real time            0.44 seconds
```

当你创建视图时，可以创建在构建视图的基表中不存在的列。也就是说，你可以创建由一个或多个基表中一个或多个列的操作（加法、减法、乘法等）的结果组成的列。你也可以使用一个或多个基表的一个或多个未修改的列构建视图。以这种方式创建的列称为派生列或计算列。在下一个示例中，假设你想创建一个视图，该视图由 INVENTORY 基表的产品名称、库存数量和库存成本组成，以及库存中存储的平均产品成本的派生列。

### SQL 代码

```
PROC SQL;
    CREATE VIEW INVENTORY_VIEW AS
        SELECT prodnum, invenqty, invencst,
            invencst/invenqty AS AverageAmount
            FROM INVENTORY;
QUIT;
```

## SAS 日志结果

```
PROC SQL;
    CREATE VIEW INVENTORY_VIEW AS
        SELECT prodnum, invenqty, invencst,
               invencst/invenqty AS AverageAmount
        FROM INVENTORY;
NOTE: SQL view WORK.INVENTORY_VIEW has been defined.
QUIT;
NOTE: PROCEDURE SQL used:
      real time          0.00 seconds
```

## 显示视图的内容

你会期望 CONTENTS 过程显示 SAS 数据库及其表的物理特征信息。但你可能不知道的是，CONTENTS 过程也可以用于显示视图的信息。从 CONTENTS 过程生成的输出显示视图不包含行（观测值），通过在 Observations 字段中显示缺失值以及成员类型为 VIEW 来表示。使用的引擎是 SQLVIEW。以下示例说明了在 Windows 环境中使用 CONTENTS 过程显示 INVENTORY_VIEW 视图内容的方法。

### SQL 代码

```
PROC CONTENTS DATA=INVENTORY_VIEW;
RUN;
```

## SAS 输出结果

### CONTENTS 过程

| 数据集名称 | WORK.INVENTORY_VIEW | 观测值 | . |
| 成员类型 | VIEW | 变量 | 4 |
| 引擎 | SQLVIEW | 索引 | 0 |
| 创建 | Wed, Sep 04, 2013 02:15:38 AM | 观测长度 | 32 |
| 最后修改 | Wed, Sep 04, 2013 02:15:38 AM | 已删除观测值 | 0 |
| 保护 |  | 压缩 | NO |
| 数据集类型 |  | 已排序 | NO |
| 标签 |  |  |  |
| 数据表示 | Default |  |  |
| 编码 | Default |  |  |

### 变量和属性的字母顺序列表

| # | 变量 | 类型 | Len | 标志 | 格式 | 标签 |
| 4 | AverageAmount | Num | 8 | P- |  |  |
| 3 | invencst | Num | 6 | -C- | DOLLAR10.2 | 库存成本 |
| 2 | invenqty | Num | 3 | -C- |  | 库存数量 |
| 1 | prodnum | Num | 3 | -- |  | 产品编号 |

## 描述视图定义

因为视图由部分编译的可执行语句组成，通常你将无法读取视图定义中的代码。然而，SQL 过程提供了一条语句来检查包含在视图定义中的可执行指令（存储查询表达式）的内容。没有这种能力，视图的底层指令（PROC SQL 代码）将永远是个谜，并且使修改或自定义查询表达式的能力几乎不可能。无论你的工作是维护还是自定义视图，DESCRIBE VIEW 语句都是你查看构成视图的语句的方式。让我们看看如何描述视图定义。

