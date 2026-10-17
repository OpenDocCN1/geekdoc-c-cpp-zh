
```
options fmtsearch=(orion.MyFmts);
```

# 10-24 第10章 创建和维护永久格式

## 10.01 多选题调查 – 正确答案

哪个程序的效率更高？

+   a. 方案 1
b. 方案 2
c. 它们的效率应该相等。

+   - `RETAIN` 语句在编译时分配一个初始值。
- `RENAME=` 选项在编译时重命名新数据集中的变量。

## 使用 NOFMTERR 系统选项

默认情况下，`FMTERR` 系统选项生效。如果你使用了 SAS 无法加载的格式，SAS 会发出错误消息并停止处理该步骤。

要防止默认操作，将系统选项 `FMTERR` 改为 `NOFMTERR`。

```
OPTIONS FMTERR | NOFMTERR;
```

## 10.02 简答调查 – 正确答案

提交程序 `p210a01`。

你在 SAS 日志中看到了哪些错误消息？

```
477 data customers:
478 set orion_customer;
479 Country_format(Country,State);

 479 ERROR-48: The format CUSTOMER was not found or could not be loaded.
480 run;
NOTE: The SAS System stopped processing this step because of errors.
WARNING: The data set WORK_CUSTOMER may be incomplete. When this step was stopped.
NOTE: The data set WORK_CUSTOMER was not replaced this step was stopped.
NOTE: real time 0.10 seconds
NOTE: CPU time 0.00 seconds

481 proc freq_selection(employee_addresses);
482 tables Country;
483 Country=Sastra.;
484 ERROR: The format SEXTRA was not found or could not be loaded.
485 run;

NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE FREQ was used (full)
```

## 10.03 简答 – 正确答案

将当前语句替换为以下内容并重新提交 `p210a01`。结果是什么？

```
options fmtlib;
```

## 10.04 简答 – 正确答案

将当前语句替换为以下内容并重新提交 `p210a01`。结果是什么？

```
options fmtsearch=(orion.MyFmts);
```

# 11.01 多选题调查

以下哪项最能描述你对 SQL 过程的经验水平？

- 一年以上以上
- 六个月到一年
- 少于六个月
- 我看过 SQL 代码但没有写过任何代码。
- 没有 SQL 经验

## SQL 过程：语法概述

`PROC SQL` 语句表示一个 SQL 过程的开始。

`QUIT` 语句结束一个 SQL 过程。不需要 `RUN` 语句，因为查询在遇到分号时就会被执行。

```sas
options ls=80; PROC SQL;
proc sql;
select *
from orion.sales_mgmt;
quit;
QUIT;
```

如果省略了 `QUIT` 语句，SQL 过程将保留在内存中以处理后续查询。一个 `QUIT` 语句或另一个步骤的开始将终止 SQL 过程并将其从内存中移除。

## SQL 过程：语法概述

一个 SQL `SELECT` 语句（也称为*查询*）被提交到 SAS 表。查询包含名为*子句*的较小构建块。

```sas
SELECT *
options ls=80;
proc sql;
select *
from orion.sales_mgmt;
quit;
```

`SELECT` 子句识别要包含在查询结果中的列。要选择所有列，请使用星号代替列名。

## 查询结果

输出包含了 `orion.sales_mgmt` 中的所有行和所有列。

| 员工 | 性别 | ID | 开始日期 | 出生日期 | 结束日期 | 员工终止日期 | 员工职位 | 员工的经理 | 年薪 |
|---|---|---|---|---|---|---|---|---|---|
| | M | 121143 | 01JUL1901 | 31DEC1999 | | | 销售经理 | 121142 | $95,090 |
| | F | 121144 | 01NOV1995 | 31DEC1999 | | | 销售经理 | 121142 | $83,505 |
| | M | 121145 | 01APR1980 | 31DEC1999 | | | 销售经理 | 121142 | $84,260 |
| | F | 121147 | 01SEP1931 | 01SEP1991 | | | 秘书 II | 121142 | $29,145 |

## FROM 子句

`SELECT` 语句中列出的列用逗号分隔。列表中的最后一列之后没有逗号。

```sas
SELECT object-item <object-item>
proc sql;
select job_title, salary
from orion.sales_mgmt;
quit;
FROM from-list ...
```

`FROM` 子句识别要从中读取的 SAS 表或多个表。

## 11.02 简答调查

打开并提交 `p211a01`。查询显示 `orion.sales_mgmt` 表中的所有变量。修改 `SELECT` 语句以仅显示 `Employee_ID`、`Job_Title` 和 `Salary` 列。

```sas
proc sql;
select *
from orion.sales_mgmt;
quit;
```

## 输出：简单的 SQL 查询

默认情况下，查询会生成一份报告。它不会创建表。

## PROC SQL 输出

| 员工 ID | 员工职位 | 员工年薪 |
|---|---|---|
| 121143 | 高级销售经理 | $95,090 |
| 121144 | 销售经理 | $83,505 |
| 121145 | 销售经理 | $84,265 |
| 121147 | 秘书 II | $29,145 |

如果你想使用结果来创建一个数据集怎么办？

## CREATE TABLE 语句

`CREATE TABLE` 语句创建一个输出数据集或 SAS 表。结果不会显示在输出窗口中。

## 部分 SAS Log

```sas
38 proc sql;
39 create table direct_reports as
40 select employee_id, job_title, salary
41 from orion.sales_mgmt;
NOTE: Table WORK.DIRECT_REPORTS created, with 4 rows and 3 columns.
42 quit;
```

## 使用 SQL 查询显示 SAS 表

使用 SQL 查询显示新表。注意 `PROC SQL` 输出不按编号识别行。

```sas
proc sql;
select *
from direct_reports;
quit;
```

PROC SQL 输出

| 员工 ID | 员工职位 | 员工年薪 |
|---|---|---|
| 121143 | 高级销售经理 | $95,090 |
| 121144 | 销售经理 | $83,505 |
| 121145 | 销售经理 | $84,260 |
| 121147 | 秘书 II | $29,145 |

## 使用 SQL 查询显示 SAS 表

使用 SQL 查询显示表。`NUMBER` 选项包含一列行号，类似于 `PRINT` 过程生成的 Obs 列。

```sas
proc sql number;
select *
from direct_reports;
quit;
```

PROC SQL 输出

| 行 | 员工 ID | 员工职位 | 员工年薪 |
|---|---|---|---|
| 1 | 121143 | 高级销售经理 | $95,090 |
| 2 | 121144 | 销售经理 | $83,505 |
| 3 | 121145 | 销售经理 | $84,260 |
| 4 | 121147 | 秘书 II | $29,145 |

## 使用 PROC 显示 SAS 表

可以使用 `PRINT` 过程来显示新表，因为它是一个数据集。

```sas
proc print data=direct_reports;
run;
```

# PROC 输出

| Obs | Employee_ID | Job_Title | Salary |
|---|---|---|---|
| 1 | 121143 | 高级销售经理 | $95,090 |
| 2 | 121144 | 销售经理 | $83,505 |
| 3 | 121145 | 销售经理 | $84,260 |
| 4 | 121147 | 秘书 II | $29,145 |

## 笛卡尔积

`orion.sales_mgmt` 中的每一行都与 `orion.employee_addresses` 中的每一行组合。

| 部分 orion.sales_mgmt | | orion.employee_addresses |
|---|---|---|
| 121143 | 高级销售经理 | $95,090 | 201044 Abbott, Ray |
| 121144 | 销售经理 | $83,505 | 201045 Alisbitt, Sandy |
| 121145 | 销售经理 | $84,260 | 207061 Akinfolarin, Tameaka |
| 121147 | 秘书 II | $29,145 | 202056 Amos, Salley |

## 笛卡尔积

概念上，当在连接中指定两个表时，第一个表的每一行都与第二个表的每一行进行匹配，产生笛卡尔积，并存储在内部或中间表中。中间表的行数等于每个表行数的乘积。中间表成为查询其余部分的输入，尽管某些行可能会被 `WHERE` 子句消除。

## 根据共同变量进行连接

获取所需的输出需要匹配两个表中的 `Employee_ID` 值。这被称为内连接。

## 使用 SQL 连接

```sas
proc sql;
select sales_mgmt.Employee_ID,
  Employee_Name,
  Salary
from orion.sales_mgmt,
  orion.employee_addresses;
quit;
```

## 连接

要连接多个 SAS 表，请在 `FROM` 子句中用逗号列出它们。

## 使用 SQL 连接

在引用列时，使用表名作为前缀来限定该列。

```sas
proc sql;
select sales_mgmt.Employee_ID,
  Employee_Name,
  Salary
from orion.sales_mgmt,
  orion.employee_addresses;
quit;
```

## 11.03 简答调查

打开 `p211a02`，提交程序并查看输出。它连接 `orion.sales_mgmt`（共 4 行）和 `orion.employee_addresses`（共 24 行）以获得直属部门的名字。输出显示了预期的四个直属部门吗？

```sas
proc sql number;
select sales_mgmt.Employee_ID,
  Employee_Name,
  Salary
from orion.sales_mgmt,
  orion.employee_addresses
where orion.sales_mgmt.Employee_ID = orion.employee_addresses.Employee_ID;
quit;
```
