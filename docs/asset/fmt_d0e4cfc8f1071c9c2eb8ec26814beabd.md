
SQL 过程支持多种复杂查询结构（有时称为连接类型）。从内连接到左、右和全外连接，本章全面介绍了可用于操作和转换多个表的各种形式的 `SELECT` 语句。SQL 过程支持四类数据关系：一对一、一对多、多对一和多对多，其中每个类别由各表中行的相互关系进行分类。

一对一关系代表最简单的连接操作。其特征是表具有 `BY` 组列，且在任何表中 `BY` 值均无重复（唯一的 `BY` 列）。它假设每个表中的数据行具有完全相同的相对顺序，其中组合结果将包含表一中的第 1 行与表二中的第 1 行，表一中的第 2 行与表二中的第 2 行，表一中的第 3 行与表二中的第 3 行，依此类推。

一对多和多对一关系与一对一关系没有更复杂，并且可由 SQL 过程轻松表示。这类关系的特征是一个表没有 `BY` 值的重复，而另一个表有一个或多个 `BY` 值的重复。

多对多关系可能比一对一、一对多和多对一关系稍微复杂一些。多对多关系的特征是所有表都有一或多个 `BY` 值的重复。使用 SQL 过程执行这类连接具有显著优势。首先，源表中的列名不必完全相同。其次，无需预先对表进行排序，因为 SQL 优化器将确定是否有可用的索引（参见第 6 章“修改和更新表和索引”）或是否需要使用隐含的 `ORDER BY` 子句对数据进行排序。

其他主题和示例包括子查询和集合操作，如 `UNION`、`INTERSECT` 和 `EXCEPT` 运算符。表 7.2 介绍了 SQL 过程中可用的各种复杂查询类型。

## 表 7.2：复杂查询的类型

| 查询类型 | 描述 |
|---|---|
| 笛卡尔积或交叉连接 | 一个创建表示两个或多个表中的行和列所有组合的表的连接。它由 `WHERE` 子句的缺失表示。 |
| 内连接 | 一个仅检索两个或多个表中具有匹配值的行的连接（最多 256 个表）。这种类型的连接被称为常规类型的连接。 |
| 等值连接 | 在两个或多个表中的列之间指定相等条件（例如等号“`=`”）的连接。 |
| 非等值连接 | 在两个或多个表中的列之间指定不等条件（例如 `NE`、`>`、`<`）的连接。 |
| 自连接或 reflexive 连接 | 一个将表与其自身组合的连接。 |
| 外连接 | 一个检索具有匹配值的行同时保留一个或两个表中部分或全部未匹配行的连接（最多 2 个表）。 |
| 左外连接 | 一个保留左表中未匹配行的连接。 |
| 右外连接 | 一个保留右表中未匹配行的连接。 |
| 全外连接 | 一个保留左表和右表中未匹配行的连接。 |
| 子查询 | 一个在另一个查询内的查询，有时称为嵌套查询，用于基于另一表中的值从一个表检索行。 |
| 简单子查询 | 一个在另一个查询内的自包含且独立的查询，可从内部查询返回单个或多个值。 |
| 相关子查询 | 一个将值传递给内部查询的外层查询，执行后将结果传回外层查询。 |
| 集合操作 | 这些运算符垂直组合或连接查询结果。 |
| `UNION` | 组合两个查询中的所有唯一（非重复）行。 |
| `INTERSECT` | 组合第一个查询中的所有匹配行与第二个查询中的行。 |
| `EXCEPT` | 生成第一个查询中未出现在第二个查询中的行。 |
| `OUTER UNION` | 连接（追加）两个查询的结果。 |

## 揭秘连接算法

SQL 过程包含一个优化器，其目的是使用最佳计划执行查询。连接算法会为每个连接属性的每个不同值定位每个关系中显示该值的有序元素列表。SQL 优化器使用标准来确定使用哪种连接算法来优化查询。连接结构、数据的结构、索引的定义、可用实际内存以及其他因素都可能影响优化器选择的连接算法。下面描述了每种连接算法的具体细节。

### 嵌套循环

当处理小型数据表且一个表明显小于另一个表、连接条件不包含相等条件、优先匹配第一行，或已排除使用排序合并或哈希连接时，SQL 优化器可能会选择嵌套循环连接算法。该算法通过遍历较小的表来查找较大表中的匹配键。嵌套循环连接算法对右表的内容极其敏感，因为它为左表的每一行处理右表。因此，随着表大小的增加，这种连接算法往往比其他选择更耗 CPU。

### 排序合并

当表为小到中等大小时，SQL 优化器可能会选择排序合并连接算法。该算法首先使用一个或多个键列对数据表进行排序（如果需要），然后对于左表中的每一行，算法读取右表中所有匹配的行。当使用索引或哈希连接算法的条件被排除在考虑之外时，SQL 优化器会考虑使用排序合并连接算法。

### 索引

当在参与连接关系的每个列上创建的索引会提高性能时，SQL 优化器可能会选择索引连接算法。该算法通过访问较大表的索引来查找较小表的每一行。SQL 优化器在较大表具有包含所有连接键的关联索引、表以相等条件相关、和/或连接条件在多个表达式之间使用 `AND` 运算符时，会考虑使用索引连接算法。

### 哈希

当系统有足够的内存可用，并且 `BUFFERSIZE` 选项足够大以将较小表存储到内存中时，SQL 优化器可能会选择哈希连接算法。该算法通过顺序扫描较大表并对较小表执行逐行查找来操作。SQL 优化器在索引连接算法被排除在考虑之外时，会考虑使用哈希连接算法。

## 用一点魔法影响连接

SQL 过程支持各种选项来影响特定连接算法的执行。以下 SQL 过程选项可用：

### 表 7.3：SQL 过程选项

| `Option` | `Description` |
|---|---|
| `MAGIC=101` | 影响 SQL 优化器选择嵌套循环连接算法。 |
| `MAGIC=102` | 影响 SQL 优化器选择排序-合并连接算法。 |
| `MAGIC=103` | 影响 SQL 优化器选择哈希连接算法。 |

在下一个示例中，指定了 `PROC SQL` 选项 `MAGIC=101` 以影响优化器为查询执行选择嵌套循环连接算法。

### SQL 代码

```
proc sql magic=101;
    select c.custname,
        p1.prodnum, p1.prodname, p2.units, p2.unitcost,
        p2.units * p2.unitcost as Total_Cost format=dollar12.2
    from products  p1,
        purchases  p2,
        customers  c
    where p1.prodnum = p2.prodnum  AND
        p2.custnum = c.custnum
    order by c.custname, p1.prodname;
quit;
```

以下日志结果显示，当指定 `MAGIC=101` 选项时，SQL 优化器（或规划器）选择了嵌套循环（顺序循环）连接算法。

### SAS 日志结果

```
proc sql magic=101;
    select c.custname,
        p1.prodnum, p1.prodname, p2.units, p2.unitcost,
        p2.units * p2.unitcost as Total_Cost format=dollar12.2
    from products  p1,
        purchases  p2,
        customers  c
    where p1.prodnum = p2.prodnum  AND
        p2.custnum = c.custnum
    order by c.custname, p1.prodname;
NOTE: PROC SQL planner chooses sequential loop join.
NOTE: PROC SQL planner chooses sequential loop join.
quit;
NOTE: PROCEDURE SQL used (Total process time):
      real time          0.08 seconds
      cpu time           0.07 seconds
```

在下一个示例中，指定了 `PROC SQL` 选项 `MAGIC=102` 以影响优化器为查询执行选择排序-合并连接算法。

### SQL 代码

```
proc sql magic=102;
    select c.custname,
        p1.prodnum, p1.prodname, p2.units, p2.unitcost,
        p2.units * p2.unitcost as Total_Cost format=dollar12.2
    from products  p1,
        purchases  p2,
        customers  c
    where p1.prodnum = p2.prodnum  AND
        p2.custnum = c.custnum
    order by c.custname, p1.prodname;
quit;
```

以下日志结果显示，当指定 `MAGIC=102` 选项时，SQL 优化器（或规划器）选择了排序-合并（合并）连接算法。

### SAS 日志结果

```
proc sql magic=102;
    select c.custname,
        p1.prodnum, p1.prodname, p2.units, p2.unitcost,
        p2.units * p2.unitcost as Total_Cost format=dollar12.2
    from products  p1,
        purchases  p2,
        customers  c
    where p1.prodnum = p2.prodnum  AND
        p2.custnum = c.custnum
    order by c.custname, p1.prodname;
NOTE: PROC SQL planner chooses merge join.
NOTE: PROC SQL planner chooses merge join.
quit;
NOTE: PROCEDURE SQL used (Total process time):
      real time          0.14 seconds
      cpu time           0.09 seconds
```

在下一个示例中，指定了 `PROC SQL` 选项 `MAGIC=103` 以影响优化器为查询执行选择哈希连接算法。

### SQL 代码

```
proc sql magic=103;
    select c.custname,
        p1.prodnum, p1.prodname, p2.units, p2.unitcost,
        p2.units * p2.unitcost as Total_Cost format=dollar12.2
    from products  p1,
        purchases  p2,
        customers  c
    where p1.prodnum = p2.prodnum  AND
        p2.custnum = c.custnum
    order by c.custname, p1.prodname;
quit;
```

日志显示，SQL 优化器（或规划器）最初选择了合并连接算法，但在指定 `MAGIC=103` 选项时，将合并连接转换为了哈希连接算法。

### SAS 日志结果

```
proc sql magic=103;
    select c.custname,
        p1.prodnum, p1.prodname, p2.units, p2.unitcost,
        p2.units * p2.unitcost as Total_Cost format=dollar12.2
    from products p1,
        purchases p2,
        customers c
    where p1.prodnum = p2.prodnum  AND
        p2.custnum = c.custnum
    order by c.custname, p1.prodname;
NOTE: PROC SQL planner chooses merge join.
NOTE: PROC SQL planner chooses merge join.
NOTE: A merge join has been transformed to a hash join.
NOTE: A merge join has been transformed to a hash join.
quit;
NOTE: PROCEDURE SQL used (Total process time):
    real time        0.08 seconds
    cpu time         0.07 seconds
```

## 笛卡尔积连接

如前所述，笛卡尔积（或交叉连接）表示连接表中行和列的所有可能组合。准确地说，它表示输入表的列数之和加上输入表的行数之积。换句话说，它表示第一个表中的每一行与第二个表中的每一行相匹配，以此类推。例如，如果你对一个包含 100,000 行的表和一个包含 10,000 行的第二个表执行连接操作，你将得到一个包含 10 百万行的笛卡尔积。

尽管笛卡尔积在关系模型中具有非常有用的目的，但对于用户来说，有意将其作为最终表产生几乎毫无意义。除了体积庞大之外，笛卡尔积包含的信息过多，使得从业者难以甚至不可能选择出重点。只有当你使用 `WHERE` 子句对笛卡尔积进行子集化时，你的数据才变得可量化且可管理。有关笛卡尔积连接的更多信息以及说明这些连接结果的示例，请访问本书的作者页面 `support.sas.com/lafler`。

## 内连接

如前所述，内连接一次最多可处理 256 个表，并且是最被认可和最广泛使用的连接类型。它们主要用于限制行，其中

### 结果

| `Product Name` | `Product Cost` | `Manufacturer Number` | `Manufacturer Name` |
|---|---|---|---|
| Dream Machine | $3,200.00 | 111 | Cupid Computer |
| Business Machine | $3,300.00 | 120 | Storage Devices Inc |
| Analog Cell Phone | $35.00 | 210 | Global Comm Corp |
| Digital Cell Phone | $175.00 | 210 | Global Comm Corp |
| Spreadsheet Software | $299.00 | 500 | KPL Enterprises |
| Database Software | $399.00 | 500 | KPL Enterprises |
| Wordprocessor Software | $299.00 | 500 | KPL Enterprises |
| Graphics Software | $299.00 | 500 | KPL Enterprises |

上一个示例可以通过在 `WHERE` 子句中添加另一个条件来进一步限定。例如，假设你只想显示由制造商 KPL Enterprises 生产的产品。以下连接标识了由 `WHERE` 子句中指定的 KPL Enterprises 制造的所有产品（所有不符合 `WHERE` 子句条件的行都会自动从连接结果中排除）。

注意：此连接假设你知道 KPL Enterprises 的唯一制造商编号。

### SQL 代码

```
PROC SQL;
    SELECT prodname, prodcost,
        manufacturers.manunum, manuname
    FROM PRODUCTS, MANUFACTURERS
    WHERE products.manunum =
        manufacturers.manunum AND
        products.manunum = 500;
QUIT;
```

① `WHERE` 子句中 `AND` 逻辑运算符的指定表示必须两个条件都为真才能从两个表中检索行。

### 结果

| `Product Name` | `Product Cost` | `Manufacturer Number` | `Manufacturer Name` |
|---|---|---|---|
| Spreadsheet Software | $299.00 | 500 | KPL Enterprises |
| Graphics Software | $299.00 | 500 | KPL Enterprises |
| Wordprocessor Software | $299.00 | 500 | KPL Enterprises |
| Database Software | $399.00 | 500 | KPL Enterprises |

让我们通过确定由 KPL Enterprises 制造的产品所占用的资金来扩展我们对等值连接的了解。为了实现这一点，你需要做两件事。首先，你需要在匹配 `WHERE` 子句条件的每一行上对产品成本（`PRODCOST`）列求和。因为等值连接的目标是计算由 KPL Enterprises 制造的产品总额，所以你需要防止结果中出现重复行。为了防止重复行，你需要指定 `DISTINCT` 关键字。

### SQL 代码

```
PROC SQL;
    SELECT DISTINCT SUM(prodcost) AS Total_Cost
        FORMAT=DOLLAR10.2,
        manufacturers.manunum
    FROM PRODUCTS, MANUFACTURERS
    WHERE products.manunum =
        manufacturers.manunum AND
        manufacturers.manuname = 'KPL Enterprises';
QUIT;
```
