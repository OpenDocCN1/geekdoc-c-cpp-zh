
# 演示内连接（Merge）

```
title "Demonstrating an Inner Join (Merge)"
proc sql;
 select H.Subj as Subj_Health,
         D.Subj as Subj_Demog,
         Height,
         Weight,
         Name,
         Gender
from Learn.Health as H inner join
Learn.Demographic as D
on H.Subj eq D.Subj;
quit;
```

SQL 的规则之一是，当你使用 `JOIN` 关键字连接两个表时，你使用 `ON` 子句而不是 `WHERE` 子句。`WHERE` 子句可用于对结果进行进一步筛选。

如果你编写这个内连接，可以很容易地将 `INNER JOIN` 替换为以下之一：`LEFT JOIN`、`RIGHT JOIN` 或 `FULL JOIN`。

左连接包含第一个表（左表）的所有行，以及第二个表中在第一个表中有对应值的行。右连接包含第二个表（右表）的所有行，以及第一个表中匹配的行。全连接包含两个表的所有行（等同于数据步中的 `merge`）。

## 第 26 章：介绍结构化查询语言 445

## 程序 26.9：演示左连接、右连接和全连接

```sas
proc sql;
title "Left Join"
select H.Subj as Subj_Health,
D.Subj as Subj_Demog,
Height,
Gender
from Learn.Health as H left join
Learn.demographic as D
on H.Subj eq D.Subj;
ntitle "Right Join"
select H.Subj as Subj_Health,
D.Subj as Subj_Demog,
Height,
Gender
from Learn.Health as H right join
Learn.demographic as D
on H.Subj eq D.Subj;

title "Full Join"
select H.Subj as Subj_Health,
D.Subj as Subj_Demog,
Height,
Gender
from Learn.Health as H full join
Learn.demographic as D
on H.Subj eq D.Subj;
quit;
```

结果如下：

446 实例 SAS 学习：程序员指南，第二版

图 26.8：程序 26.9 的输出

| Subj_Health | Subj_Demog | Height | Gender |
|---|---|---|---|
| 001 | 001 | 68 | M |
| 003 | 003 | 74 | F |
| 004 |  | 63 |  |
| 005 | 005 | 60 | F |

左连接

| Subj_Health | Subj_Demog | Height | Gender |
|---|---|---|---|
| 001 | 001 | 68 | M |
| 002 |  |  | M |
| 003 | 003 | 74 | F |
| 005 | 005 | 60 | F |

右连接

| Subj_Health | Subj_Demog | Height | Gender |
|---|---|---|---|
| 001 | 001 | 68 | M |
| 002 |  |  | M |
| 003 | 003 | 74 | F |
| 004 |  | 63 |  |
| 005 | 005 | 60 | F |

全连接

检查此输出应该有助于理清不同连接类型之间的区别。

## 26.5 合并数据集

在 `DATA` 步中，通过在单个 `SET` 语句中命名两个数据集来合并它们。在 `PROC SQL` 中，你使用 `UNION` 算符来合并来自两个表的查询结果。与 `DATA` 步不同，`UNION` 运算符有不同的“类型”。以下是总结。

第 26 章：介绍结构化查询语言 447

| 算符 | 描述 |
| --- | --- |
| Union | 按列位置匹配（不按列名）并删除重复行 |
| Union All | 按列位置匹配但不删除重复行 |
| Union Corresponding | 按列名匹配并删除重复行 |
| Union All Corresponding | 按列名匹配但不删除重复行 |
| Except | 按列名匹配并删除在两个表中都存在的行 |
| Intersection | 按列名匹配并保留两个表中的唯一行 |

`UNION ALL CORRESPONDING` 运算符等于在 `DATA` 步的 `SET` 语句中命名两个数据集。

非常重要的一点是不带 `CORRESPONDING` 关键字的 `UNION` 运算符将导致两个数据集按列位置合并，而不是按列名合并。这里的示例说明了这一点。

创建数据集 `New_Members` 是为了说明各种类型的合并。以下是列表：

**图 26.9：数据集 New_Members 的列表**

| 数据集 New_Members 的列表 | | |
| Subj | Gender | Name | DOB |
| --- | --- | --- | --- |
| 010 | F | Ostermeister | 03/05/1977 |
| 013 | M | Brown | 06/07/1999 |

作为参考，这里是数据集 `Demographic` 的列表：

**图 26.10：数据集 Demographic 的列表**

| 数据集 Demographic 的列表 | | |
| Subj | DOB | Gender | Name |
| --- | --- | --- | --- |
| 001 | 10/15/1960 | M | Friedman |
| 002 | 08/01/1955 | M | Stern |
| 003 | 12/25/1988 | F | McGoldrick |
| 005 | 05/28/1949 | F | Chien |

假设你想将这些新成员添加到 `Demographic` 数据集中，并将新数据集命名为 `Complete_List`。以下是使用 `PROC SQL` 实现的方法（注意列顺序并不相同）。

## 程序 26.10：合并两个表

```sas
proc sql;
create table Complete_List as
select *
from Learn.Demographic union all
select *
from Learn.New_Members
quit;
```

生成的表包含 `Demographic` 的所有行，随后是 `New_Members` 的所有行。

## 程序 26.11：数据集 Complete_List 的输出

| Subj | DOB | Gender | Name |
|---|---|---|---|
| 001 | 10/15/1960 | M | Friedman |
| 002 | 08/01/1955 | M | Stern |
| 003 | 12/25/1988 | F | McGoldrick |
| 005 | 05/28/1949 | F | Chien |
| 010 | 03/05/1977 | F | Ostermeister |
| 013 | 06/07/1999 | M | Brown |

如果你漏掉了 `CORRESPOND` 关键字，结果如下（SAS 日志）：

```sas
proc sql;
create table Complete_List as
select *
from Learn.Demographic union all
select *
from Learn.New_Members
quit;
ERROR: UNION ALL 的第一个部分第 2 列与第二个部分的类型不匹配。
ERROR: UNION ALL 的第一个部分第 4 列与第二个部分的类型不匹配。
```

如果运气好，数据集中的列类型匹配，SQL 将执行合并。为了理解这一点，这里有一个数据集 `New_Members_Order`，其列顺序发生了变化：

第 26 章：介绍结构化查询语言 449

图 26.13：New_Members_Order 的列表

| 数据集 New_Members_Order 的列表 | | | |
| Name | DOB | Gender | Subj |
|---|---|---|---|
| Ostermeister | 03/05/1977 | F | 010 |
| Brown | 06/07/1999 | M | 013 |

`New_Members_Order` 的四个列与 `Demographic` 的四个列具有相同类型（字符或数值）。因此，如果在合并两个数据集时省略 `CORRESPONDING` 关键字，你会得到以下结果：

图 26.14：省略 CORRESPONDING 的结果

| 省略 CORRESPONDING 的数据集 Complete_List 列表 | | | |
| Subj | DOB | Gender | Name |
|---|---|---|---|
| 001 | 10/15/1960 | M | Friedman |
| 002 | 08/01/1955 | M | Stern |
| 003 | 12/25/1988 | F | McGoldrick |
| 005 | 05/28/1949 | F | Chien |
| 010 | 03/05/1977 | F | Ostermeister |
| 013 | 06/07/1999 | M | Brown |

现在你可以看到为什么在合并两个数据集时需要选择正确的 `UNION` 运算符了。

## 26.6 使用函数

你可以使用 `MEAN` 和 `SUM` 等函数来创建代表其他变量平均值或和的新变量。你也可以在查询中创建。以下程序了 `PROC SQL` 的优点之一：向现有表添加摘要变量。

假设你想将 `Health` 数据集中每个人的身高表示为所有受试者平均身高的百分比。你会首先使用 `PROC MEANS` 创建包含平均高度的数据集，然后将其与原始数据集合并并进行计算（参见第 10 章中关于合并详细数据的章节）。`PROC SQL` 使此任务变得简单得多。让我们来看看。

450 实例 SAS 学习：程序员指南，第二版

## 程序 26.11：在 PROC SQL 中使用摘要函数

```sas
proc sql;
select Subj,
  Height,
  Weight,
  mean(Height) as Ave_Height,
  100*Height/Calculated Ave_Height as
  Percent_Height
from Learn.Height;
```

平均值使用 `MEAN` 函数计算。该值也被名为 `Ave_Height`。当你在计算中使用此变量时，需要在前面加上 `CALCULATED` 关键字，以便 `PROC SQL` 在输入数据集中查找该变量。结果如下：

图 26.15：程序 26.11 的输出

| Subj | Height | Weight | Ave_Height | Percent_Height |
|---|---|---|---|---|
| 001 | 68 | 155 | 66.25 | 102.6415 |
| 003 | 74 | 250 | 66.25 | 111.6981 |
| 004 | 63 | 110 | 66.25 | 95.0932 |
| 005 | 60 | 95 | 26.25 | 90.5604 |

注意使用 `PROC SQL` 比使用 `DATA` 步容易得多。

## 26.7 演示 ORDER 子句

如果你使用 `ORDER` 子句，`PROC SQL` 也可以对你的表进行排序。例如，如果你想顺序排列 `Health` 表中的受试者，请使用：

## 程序 26.12：演示 ORDER 子句

```sas
proc sql;
select Subj,
  Height,
  Weight
from Learn.Health
order by Height;
quit;
```

结果（未显示）是按顺序排列的变量 `Subj`、`Height` 和 `Weight`。

第 26 章：介绍结构化查询语言 451

## 26.8 模糊匹配示例

`PROC SQL` 的优点之一是可以创建笛卡尔积。正如本章前面提到的，笛卡尔积是一个表中的每一行与另一个表的每一行的配对。这里有两个表：`Demographic`（在本章的许多其他示例中使用）和 `Insurance`。

图 26.16：数据集 Demographic 和 Insurance 的列表

| 数据集 Demographic 的列表 | | 数据集 Insurance 的列表 | | |
|---|---|---|---|---|
| Subj | DOB | Gender | Name | Name | Type |
| 001 | 10/15/1960 | M | Friedman | Friedman | F |
| 002 | 08/01/1955 | M | Stern | Goldman | P |
| 003 | 12/25/1988 | F | McGoldrick | Chein | F |
| 005 | 05/28/1949 | F | Chien | Stern | |

你想通过 `Name` 连接（合并）这些表，允许名字出现轻微拼写错误。以下是实现此操作的 SQL 查询：

## 程序 26.13：使用 PROC SQL 执行模糊匹配

```sas
title "Example of a Fuzzy Match";proc sql;
 select Subj,
  Demographic.Name,
  Insurance.Name
 from Learn.Demographic,
  Learn.Insurance
 where spedis(Demographic.Name,Insurance.Name) le 25;
quit;
```

`SPEDIS`（编辑距离）函数允许拼写错误（参见第 12 章）。`WHERE` 子句对两个表的每种行组合进行操作，并选择距离小于 25 的行。在实践中，你会希望比较两个文件的其他变量（如性别和生日），以增加建立有效匹配的可能性。查看下面的列表，看看此程序匹配了哪些名称：

图 26.17：程序 26.13 的输出

模糊匹配示例

| Subj | Name | Name |
|---|---|---|
| 001 | Friedman | Friedman |
| 005 | Chien | Chein |
| 002 | Stern | Stern |

452 实例实例学习 SAS：程序员指南，第二版

你可以轻松地修改此程序，使输出不包含完全匹配的名称。

我们仅仅触及了 SQL 能够实现功能的皮毛。希望这段关于 SQL 的介绍能鼓励你学习更多。

## 26.9 练习

奇数题的解答位于书末。所有题目的解答均供教授参考。如果您是教授，请访问书籍的配套网站 `support.sas.com/cody` 获取有关获取所有题目解答的信息。

- 1. 使用 `PROC SQL` 列出数据集 `Inventory` 中所有 `Price` 大于 20 的观测值。
- 2. 重复练习 1，但使用 `PROC SQL` 创建一个新的临时 SAS 数据集 (`Price20`)，包含 `Inventory` 中所有 `Price` 大于 20 的观测值。
- 3. 使用 `PROC SQL` 创建一个新的临时 SAS 数据集 (`N_Sales`)，包含 `Sales` 中 `Region` 值为 `North` 的观测值。在新数据集中仅包含 `Name` 和 `TotalSales` 两个变量。
- 4. 此处显示数据集 `Inventory` 和 `Purchase`：

| 数据集 `Inventory` 列表 | | | 数据集 `Purchase` 列表 | | |
| :--- | :--- | :--- | :--- | :--- |
| Model | Price | CustNumber | Model | Quantity |
| M567 | $23.50 | 101 | L776 | 1 |
| S888 | $12.99 | 102 | M123 | 10 |
| L776 | $159.98 | 103 | X999 | 2 |
| X999 | $29.95 | 103 | M567 | 1 |
| M123 | $4.59 | | | |
| S776 | $1.99 | | | |

使用 `PROC SQL` 列出所有购买的项目，显示 `Cust Number`、`Model`、`Quantity`、`Price` 以及一个新变量 `Cost`，其中 `Cost` 等于 `Price` 乘以 `Quantity`。
- 5. 此处显示数据集 `Left` 和 `Right`。使用 `PROC SQL` 创建一个新的临时 SAS 数据集 (`Both`)，包含 `Subj`、`Weight` 和 `Salary`。通过三种方式实现：首先，仅包含两个数据中的受试者；其次，包含两个数据集中的所有受试者；第三，仅包含数据集 `Left` 中的受试者。

| 数据集 `Left` 数据 | | | 数据集 `Right` 数据 | | |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Subj | Height | Weight | Subj | Salary |
| 001 | 68 | 155 | 001 | $46,000 |
| 002 | 75 | 220 | 003 | $67,900 |
| 003 | 65 | 99 | 005 | $228,200 |
| 005 | 79 | 266 | 006 | $98,200 |
