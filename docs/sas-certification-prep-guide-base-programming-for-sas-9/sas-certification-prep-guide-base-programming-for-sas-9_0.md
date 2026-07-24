# SAS 认证备考指南：SAS 9 基础编程











# 关于本书

## 读者群

《SAS Certification Prep Guide: Advanced Programming for SAS^®9, Fourth Edition》适用于准备参加 SAS Advanced Programming for SAS 9 考试的新手或资深 SAS 程序员。

### 要求与详述

### 目的与内容
本指南帮助你准备参加 SAS Advanced Programming for SAS 9 考试。新手或资深 SAS 用户将发现本指南是一份非常有价值的资源，涵盖了考试中测试的目标。主要主题包括使用 SAS 进行 SQL 处理、使用 SAS 宏语言、高级 SAS 编程技术以及优化 SAS 程序。你还将熟悉 SAS^®9 中提供的增强和新功能。
书中包含了测验，用于测试你对每章内容的理解情况。书末附有测验答案。
欲查找本指南的更新，请访问 SAS 培训与书籍网站 [`support.sas.com/publishing/cert`](http://support.sas.com/publishing/cert "opens in a new browser tab")。
注意：考试目标可能会发生。请在 [`support.sas.com/certify`](http://support.sas.com/certify "opens in a new browser tab") 查看当前的考试目标。

### 前提条件
在参加 SAS Advanced Programming for SAS 9 考试之前，必须获得 SAS Certified Base Programmer for SAS 9 认证。《SAS Certification Prep Guide: Base Programming for SAS^®9》涵盖了 SAS Base Programming for SAS 9 考试测试的目标，包括导入导出原始数据文件；创建和修改 SAS 数据集；以及识别并修正数据、语法和编程逻辑错误。
要查看你是否具备必要的 Base SAS 编程知识，请访问 [`support.sas.com/basepractice`](http://support.sas.com/basepractice "opens in a new browser tab")。

### 如何创建练习数据

## SAS 环境

在 SAS 中设置练习数据，请从 SAS 主菜单选择 Help>Learning SAS Programming。当出现 SAS Online Training Sample Data 窗口时，点击 OK 创建示例数据。

## SAS Studio 和 SAS University Edition

如果你在使用 SAS Studio 或 SAS University Edition，你可能没有存储示例数据的 Sasuser 目录的写入权限。
要确定 Sasuser 文件夹是否只读，请提交以下代码：

```
proc options option=rsasuser;
run;
```

如果 `PROC OPTIONS` 代码的结果为 `NORSASUSER`，则 Sasuser 文件夹是可写的，你可以按照以下步骤在 SAS Studio 中设置练习数据：

1. 将示例数据程序复制到 SAS Studio 中的新 Code 窗口中。你可以在 [`support.sas.com/publishing/cert/sampdata.txt`](http://support.sas.com/publishing/cert/sampdata.txt "opens in a new browser tab") 获取示例数据。
2. 点击运行。

如果 `PROC OPTIONS` 代码的结果为 `RSASUSER`，则 Sasuser 文件夹是只读的，你需要使用 `LIBNAME` 语句重定向 Sasuser 文件夹。要设置练习数据：

1. 在 Folders 格中选择 My Folders。然后右键点击并选择 New>Folder。
2. 在 Name 框中输入文件夹名称。在我们的示例中，我们使用 `certprep`。点击 Save。

```
libname sasuser "/folders/certprep";
```

注意：必须使用目录名称。在我们的示例中，我们使用 `certprep`。如果你使用了其他文件名，请将 `certprep` 替换为你创建的。如果你使用的是 SAS Studio，请执行：

1. 右键点击你创建的文件夹并选择 Properties。
2. 复制 Location 字段中的路径。
3. 输入以下代码，将 `location field` 替换为你复制的路径：

```
libname sasuser "location field";
```

4. 点击运行。
5. 将程序保存为 `libname_cert.sas`。每次处理示例数据都要重新提交此 `LIBNAME` 程序。
6. 将示例数据程序复制到 SAS Studio 中的新 Code 窗口中。你可以在 [`support.sas.com/publishing/cert/sampdata.txt`](http://support.sas.com/publishing/cert/sampdata.txt "opens in a new browser tab") 获取示例数据。
7. 点击运行。

现在你已经将示例数据存储在永久目录中，每次需要使用数据时重新执行 `LIBNAME` 语句。

## SAS Enterprise Guide

下载示例数据：

1. 启动 SAS Enterprise Guide。
2. 在 Welcome to SAS Enterprise 窗口中选择 New Project。
3. 选择 File>New>Program。
4. 根据你的网络配置，你可能没有存储示例数据的 Sasuser 目录的写入权限。要确定 Sasuser 文件夹的状态，提交以下代码：

```
proc options option=rsasuser;
run;
```




5. 如果 `PROC OPTIONS` 代码的结果为 `RSASUSER`，你必须通过创建一个新文件夹来重定向 `Sasuser` 文件夹。从你的服务器区域，打开 `Files` 文件夹，右键点击驱动器或文件夹，并选择 `New Folder`。输入新文件夹名称。注意：如果 `PROC OPTIONS` 代码的结果为 `NORSASUSER`，则 `Sasuser` 文件夹是可写的，你不需要重定向 `Sasuser` 文件夹。因此，你可以跳过此步和下一步。

6. 在 Code 窗口中提交以下代码：

```sas
libname sasuser "/folders/myfolders/certprep";
```

注意：你必须使用新文件夹的。在我们的示例中，我们使用 `certprep` 名称。如果你使用其他文件名，请用你创建的文件夹名称替换 `certprep`。

7. 将示例数据程序复制到 `Program` 窗口中然后运行程序。你可以在 [`support.sas.com/publishing/cert/sampdata.txt`](http://support.sas.com/publishing/cert/sampdata.txt "在新浏览器标签页中打开") 访问示例数据。

8. 因为你不需要使用这些快捷方式，可以从项目中删除 `Program` 项和所有快捷方式。此操作不会删除你创建的数据。要从项目中删除该项，右键点击 `Program` 并选择 `Delete`。

9. 在 `Confirmation` 窗口中，点击 `Yes`。

### 考试

SAS 认证练习考试：SAS 9 高级编程可以帮助你准备 SAS 9 高级编程考试。这门练习考试测试的是与官方认证考试相同的知识和技能。你可以在 SAS 认证类别下访问此考试：[`support.sas.com/edu/schedules.html?id=449`](https://support.sas.com/edu/schedules.html?id=449 "在新浏览器标签页中打开")。此练习考试需要付费。要注册官方 SAS 9 高级编程考试，请访问 SAS 全球认证网站：[`support.sas.com/certify`](http://support.sas.com/certify "在新浏览器标签页中打开")。

### 额外资源

在学习 SAS 编程时，以下资源可以帮助你。

| 来自 SAS 软件 |
| --- |
| 帮助 | 对于 SAS^®9，选择 `Help>SAS Help and Documentation`；SAS Enterprise Guide，选择 `Help>SAS Enterprise Guide Help` |
| 文档 | 对于 SAS^®9，选择 `Help>SAS Help and Documentation`；SAS Studio，选择 ![SAS Studio 帮助图标](img/question_circle.png) |

| 网上 |
| --- |
| 书店 | [`support.sas.com/publishing/`](http://support.sas.com/publishing/ "在新浏览器标签页中打开") |
| 培训 | [`support.sas.com/training/`](http://support.sas.com/training/ "在新浏览器标签页中打开") |
| 文档（包括 SAS Enterprise Guide） | [`support.sas.com/documentation/`](http://support.sas.com/documentation/ "在新浏览器标签页中打开") |
| 认证 | [`support.sas.com/certify/`](http://support.sas.com/certify/ "在新浏览器标签页中打开") |
| SAS 全球学术计划 | [`support.sas.com/learn/ap`](http://support.sas.com/learn/ap "在新浏览器标签页中打开") |
| SAS OnDemand | [`support.sas.com/ondemand/`](http://support.sas.com/ondemand/ "在新浏览器标签页中打开") |
| 知识库 | [`support.sas.com/resources/`](http://support.sas.com/resources/ "在新浏览器标签页中打开") |
| 支持 | [`support.sas.com/techsup/`](http://support.sas.com/techsup/ "在新浏览器标签页中打开") |
| 学习中心 | [`support.sas.com/learn/`](http://support.sas.com/learn/ "在新浏览器标签页中打开") |
| 社区 | [`support.sas.com/community/`](http://support.sas.com/community/ "在新浏览器标签页中打开") |

### 语法规范

以下示例显示了书中所示 SAS 代码的一般形式。

| `PROC SQL;SELECT column-1<,...column-n>FROM table-1|view-1<,...table-n|view-n><WHERE expression><GROUP BY column-1<, ... column-n>><ORDER BY column-1<,... column-n>>;` |
| --- |
| `PROC SQL` 调用 SQL 过程。 |
| `SELECT` 指定要选择的列。 |
| `FROM` 指定要查询的表。 |
| `WHERE` 根据条件对数据进行子集划分。 |
| `GROUP BY` 根据指定的列将数据分类。 |
| `ORDER BY` 根据指定列的值对查询返回的行进行排序。 |

以下是详细信息。`SELECT`、`FROM`、`WHERE`、`GROUP BY` 和 `ORDER BY` 使用大写，因为它们必须按所示拼写。`column-1`、`table-1`、`view-1` 和 `expression` 使用斜体，因为它们每个都代表你提供的值。`<,...column-n>` 包在角括号中，因为它是可选语法。`table-1` 和 `view-1` 之间用竖线（ `|` ）隔开，表示它们是互斥的。本书涵盖了你准备认证考试所需的所需的基础语法。

# 第 1 章：使用 PROC SQL 执行查询

## 概述

## 引言

有时你需要关于数据的快速答案。你可能想对单个数据集或数据集组合进行查询（检索数据），以实现以下操作：

- 检查数据值之间的关系
- 查看数据的子集
- 快速计算值

SQL 过程 (`PROC SQL`) 提供了一种简单灵活的方法来合并你的数据。本章将你如何使用一个或多个表创建基础查询![SAS 表和输出](img/m10f1g1.png)

## PROC 基础




```
proc sql;
   select empid,jobcode,salary,
          salary*.06 as bonus
      from sasuser.payrollmaster
      where salary<32000
      order by jobcode;
```

*   `PROC SQL` 步骤不需要 `RUN` 语句。`PROC SQL` 会自动执行每个查询。如果你在 `PROC SQL` 步骤中使用 `RUN` 语句，SAS 会忽略该 `RUN` 语句，照常执行语句，并在 SAS 日志中生成如下所示的注释。

表 1.1 SAS 日志

```
1884 proc sql; 
1885    select empid,jobcode,salary, 
1886           salary*.06 as bonus
1887       from sasuser.payrollmaster 
1888       where salary<32000 
1889       order by jobcode;
1890 run;
NOTE: PROC SQL statements are executed immediately;
      The RUN statement has no effect.
```

*   与许多其他 SAS 过程不同，在提交一个步骤后，`PROC SQL` 会继续运行。要结束该过程，你必须提交另一个 `PROC` 步骤、`DATA` 步骤或 `QUIT` 语句，如下：

```
proc sql;
   select empid,jobcode,salary,
          salary*.06 as bonus
      from sasuser.payrollmaster
      where salary<32000
      order by jobcode;
quit;
```

当你提交一个没有结束的 `PROC SQL` 步骤时，状态栏会显示消息：

```
PROC SQL running
```

注意：作为预防措施，SAS Enterprise Guide 在你将代码提交到 SAS 时会自动向你的代码中添加 `QUIT` 语句。然而，你应该养成在代码中添加 `QUIT` 语句的习惯。

### 编写 PROC SQL 步骤

## 概述

在创建查询之前，你必须先引用存储表所在的库。然后，你编写一个 `PROC SQL` 步骤来查询你的表。

| 通用形式，执行查询的 Basic PROC SQL 步骤：`PROC SQL;SELECT column-1<,...column-n>FROM table-1|view-1<,...table-n|view-n><WHERE expression><GROUP BY column-1<, ... column-n>><ORDER BY column-1<,... column-n>>;` | 此处是该语法的解释： | `PROC SQL` 调用 SQL 过程 | `SELECT` 指定要选择的列 | `FROM` 指定要查询的表 | `WHERE` 根据一个或多个条件对数据进行子集划分 | `GROUP BY` 根据指定的列将数据分类为组 | `ORDER BY` 根据指定列的值对查询返回的行进行排序。 | |

**注意**：与其他 SAS 过程不同，`PROC SQL` 中 `SELECT` 语句的子句顺序是重要的。子句必须按照上述所示的顺序出现。
**注**：查询也可以包含 `HAVING` 子句，该子句将在本章末尾介绍。要了解更多关于 `HAVING` 子句的信息，请参阅 使用 PROC SQL 执行高级查询。

## SELECT 语句

跟在 `PROC SQL` 语句之后的 `SELECT` 语句用于检索和显示数据。它由以关键字开头的子句组成，后面跟着一个或多个组件。以下示例代码中的 `SELECT` 语句包含四个子句：必需子句 `SELECT` 和 `FROM`，以及可选子句 `WHERE` 和 `ORDER BY`。语句的结束由分号指示。

```
proc sql;
 |-select empid,jobcode,salary,
 |        salary*.06 as bonus
 |----from sasuser.payrollmaster
 |----where salary<32000
 |----order by jobcode;
```

**注**：包含一个或多个 `SELECT` 语句的 `PROC SQL` 步骤被称为 `PROC SQL` 查询。`SELECT` 语句只是可与 `PROC SQL` 使用的多个语句之一。下面的 `PROC SQL` 查询创建了所示输出报告：

```
proc sql;
   select empid,jobcode,salary,
          salary*.06 as bonus
      from sasuser.payrollmaster
      where salary<32000
      order by jobcode;
```

![显示 EmpID, JobCode, Salary 和 bonus 的输出报告](img/m10-6-g1.png)

`PROC SQL` 查询产生结果集，该结果可以输出为报告、表或 `PROC SQL` 视图。

| 输出类型 | PROC SQL 语句 |
| --- | --- |
| 报告 | `SELECT` |
| 表 | `CREATE TABLE` |
| PROC SQL 视图 | `CREATE VIEW` |

**注**：`CREATE TABLE` 语句在本章稍后部分介绍。你可以在 使用 PROC SQL 创建和管理表 中学习创建表。你可以在 使用 PROC SQL 创建和管理视图 中了解更多关于 `PROC SQL` 视图的信息。将在后续章节中学习更多 `SELECT` 语句。

### 选择列

## 概述

要指定在查询中显示哪些列，你需要编写 `SELECT` 子句。在 `SELECT` 关键字之后列出一个或多个列，并用逗号分隔列名。在 `SELECT` 子句中，你可以同时指定现有列（存储在表中）和新列。下面的 `SELECT` 子句指定了 `EmpID`、`JobCode` 和 `Salary`。名为 `bonus` 的列是一个新列。

```
proc sql;
   select empid,jobcode,salary,
          salary*.06 as bonus
      from sasuser.payrollmaster
      where salary<32000
      order by jobcode;
```

## 创建新列

你可以创建包含或计算的新列。除非创建了表或视图，否则新列仅在查询期间存在。要创建新列，请 `SELECT` 子句中包含任何有效的 SAS 表达式。通过使用关键字 `AS` 后跟名称为新列分配别名。
**注**：别名必须 SAS 名称规则。在示例 `PROC SQL` 查询中，使用表达式来计算新列：`Salary` 的值乘以 `.06`。使用 `AS` 关键字为新列分配别名 `bonus`。

```
proc sql;
   select empid,jobcode,salary,
          salary*.06 as bonus
      from sasuser.payrollmaster
      where salary<32000
      order by jobcode;
```

列别名非常有用，因为它允许你在查询的其他地方引用该列。
**注**：此外，列别名作为列标题。下面的输出显示了计算列显示。注意列别名 `bonus` 以小写显示，与你在 `SELECT` 子句中指定的相同。

![带有计算 Bonus 的输出](img/m10-7-g1.png)

在 `SELECT` 子句中，你可以为现有列或新列指定标签。如果为新列同时指定标签别名和列别名，则标签将作为输出中的列标题。如果只指定列别名，则确保按照你希望在输出中显示的格式来指定列别名。
**注**：你可以在 使用 PROC SQL 执行高级查询 中学习创建文本的新列以及指定标签。

### 指定表

在编写 `SELECT` 子句之后，在 `FROM` 子句中指定要查询的表。输入关键字 `FROM`，后接表名，如下所示：

```
proc sql;
   select empid,jobcode,salary,
          salary*.06 as bonus
      from sasuser.payrollmaster
      where salary<32000
      order by jobcode;
```

上述 `PROC SQL` 步骤查询了存储在分配了 libref `Sasuser` 的 SAS 库中的永久 SAS 表 `Payrollmaster`。

# 指定子集条件




要根据条件对数据进行子集划分，请在 `SELECT` 语句中使用 `WHERE` 子句。与其他 SAS 过程中使用的 `WHERE` 语句和 `WHERE` 命令一样，`WHERE` 子句中的表达式可以是任何有效的 SQL 表达式。在 `WHERE` 子句中，你可以指定底层表中的任何列。`WHERE` 子句中指定的列并不一定必须在 `SELECT` 子句中指定。在接下来的 `PROC SQL` 查询中，`WHERE` 子句选择了 `Salary` 列值小于 `32,000` 的行。输出结果也如下所示。

| | ```
proc sql;
   select empid,jobcode,salary,
          salary*.06 as bonus
      from sasuser.payrollmaster
      where salary<32000
      order by jobcode;
``` | ![工资小于 32,000 的工资子集](img/m10-12-g1.png) |

# 行的排序

## 概述
`PROC SQL` 查询输出的行顺序无法保证，除非你指定了排序顺序。要按特定列的值对行进行排序，可以在 `SELECT` 语句中使用 `ORDER BY` 子句。指定关键字 `ORDER BY`，后面跟上用逗号分隔的一个或多个列名。在接下来的 `PROC SQL` 查询中，`ORDER BY` 子句按 `JobCode` 列的值对行进行排序：

```
proc sql;
   select empid,jobcode,salary,
          salary*.06 as bonus
     from sasuser.payrollmaster
     where salary<32000
      order by jobcode;
```

注意：在例例中，`ORDER BY` 子句是 `SELECT` 语句中的最后一个子句，因此 `ORDER BY` 子句以分号结束。在下方所示的示例查询输出中，行按 `JobCode` 的值排序。默认情况下，`ORDER BY` 子句按升序对行排序![Emplid, jobcode, salary, bonus](img/m10-14-g1.png)。要按降序排序行，请在列名后指定关键字 `DESC`。例如，前面的 `ORDER BY` 子句可以修改如下：

```
order by jobcode desc;
```

在 `ORDER BY` 子句中，你也可以通过列在 `SELECT` 子句列表中的位置而不是通过名称来引用列。使用整数指示列的位置。上述 `PROC SQL` 查询中的 `ORDER BY` 子句已在下方修改，通过列在 `SELECT` 子句列表中的位置（`2`）而不是名称来指定 `JobCode` 列：

```
proc sql;
   select empid,jobcode,salary,
          salary*.06 as bonus
      from sasuser.payrollmaster
      where salary<32000
      order by 2;
```

## 多列排序
要按两个或多个列的值对行进行排序，请在 `ORDER BY` 子句中列出多个列名（或数字），并使用逗号分隔列名（或数字）。在接下来的 `PROC SQL` 查询中，`ORDER BY` 子句按两个列 `JobCode` 和 `EmpID` 的值进行排序：

```
proc sql;
   select empid,jobcode,salary,
          salary*.06 as bonus
      from sasuser.payrollmaster
      where salary<32000
      order by jobcode,empid;
```

行首先按 `JobCode` 排序，然后按 `EmpID` 排序，如下方的所示![Emplid, jobcode, salary, bonus](img/m10-15-g1.png) 注意：你可以在 `ORDER BY` 子句中混合使用两种列引用类型（名称和数字）。例如，前面的 `ORDER BY` 子句可以重写为：

```
order by 2,empid;
```

你还可以在 `ORDER BY` 子句中引用列别名。这里有一个示例：

```
order by 2, empid, bonus;
```

# 多表查询

## 概述
本主题涉及从两个或多个表中提取数据这一更复杂的任务。之前，你已经学习了如何编写 `PROC SQL` 步骤来查询单表。假设你现在想检查存储在两个表中的数据。`PROC SQL` 允许你从水平方向上合并表，换句话说，就是合并数据行![表 a，表 b](img/m10-19-g2.png)。在 SQL 术语中，水平合并表被称为连接表（joining tables）。连接操作不会更改原始表。

假设你想创建一个报告，显示公司员工的以下信息：员工编号、姓氏、原始工资和新工资。没有一个单表包含所有这些列，因此你必须连接 `Sasuser.Salcomps` 和 `Sasuser.Newsals` 这两个表。在你的查询中，你想选择四个列，其中两个来自第一张表，两个来自第二个表。你还需要确保所连接的行属于同一个员工。为了检查这一点，你希望对合并的行的员工编号进行匹配，并只选择匹配的行![SAS 表 Salcomps 和 Newsals](img/m10f1g1.png) 这种连接被称为内连接（inner join）。内连接为所有匹配项返回结果集。假设你想创建一个显示公司员工的以下信息的报告：员工编号、姓氏、原始工资和新工资。没有一个单表包含所有这些列，因此你必须连接 `Sasuser.Salcomps` 和 `Sasuser.Newsals` 这两个表。注意：关于水平 SQL 连接的更多信息，请参见 [Combining Tables Horizontally Using PROC SQL](https://support.sas.com/help/en/libref/le94/procsql/n/combining-tables-horizontally.htm)。在你的查询中，你想选择四个列，其中两个来自第一张表，两个来自第二个表。你还需要确保所连接的行属于同一个员工。为了检查这一点，你希望对合并的行的员工编号进行匹配，并只选择匹配的行。这种连接被称为内连接（inner join）。内连接为所有匹配项返回结果集。





```sql
proc sql;
   select salcomps.empid,lastname,
          newsals.salary,newsalary
      from sasuser.salcomps,sasuser.newsals
      where salcomps.empid=newsals.empid
      order by lastname;
```

部分输出显示所示。![通过 empid 链接的表](img/m10-24-g1.png) 注意：在 `Sasuser.Newsals` 表中，`Salary` 列的标签为 `Employee Salary`，如此输出所示。**注意**：如果将不包含一个或多个与另一个具有匹配数据值的列表进行连接，可能会出现几种意料之外的结果。你可能会产生大量数据，可能会产生所有可能的行组合。

# 对行排序

与仅查询单个表的 `PROC SQL` own 类似，`ORDER BY` 子句指定了使用哪些列（列）对输出中的行进行排序。在下面的查询中，按 `LastName` 排序：

|  

```sql
proc sql;
  select salcomps.empid,lastname,
         newsals.salary,newsalary
     from sasuser.salcomps,sasuser.newsals
     where salcomps.empid=newsals.empid
     order by lastname;
```

 | ![按 LastName 排序的行](img/m10-25-g1.png) |

# 数据组的汇总

我们可以使用 `PROC SQL` 步骤创建详细报告。但你可能还想对数据进行分组汇总。为了为了汇总数据进行分组，可以使用 `GROUP BY` 子句。`GROUP BY` 子句用于包含一个或多个汇总函数的查询。汇总函数为 `GROUP BY` 子句中定义的每个组生成一个统计摘要。

## 示例

下面的示例演示了 `GROUP BY` 子句和汇总函数。假设你想确定常客旅客计划会员在三个会员等级（金牌、银牌和铜牌）中每个等级旅行的总里数数。常客旅客计划信息存储在 `Sasuser.Frequentflyers` 表中。要对你的数据进行汇总，可以提交以下 `PROC SQL` 步骤：

```sql
proc sql;
   select membertype,
          sum(milestraveled) as TotalMiles
      from sasuser.frequentflyers
      group by membertype;
```

在这种情况下，`SUM` 函数对 `MilesTraveled` 列的值求总和以创建 `TotalMiles` 列。`GROUP BY` 子句根据 `MemberType` 的值对数据分组。与 `ORDER BY` 子句类似，在 `GROUP BY` 子句中，你指定关键字 `GROUP BY`，随后是一个或多个由逗号分隔的列名。结果显示了按等级（MemberType）划分的总里程。![MemberType, TotalMiles](img/m10-28-g1.png) 注意：如果你在不包含汇总函数的查询中指定了 `GROUP BY` 子句，该子句将变为 `ORDER BY` 子句，并在 SAS 日志中写入相应信息。

## 汇总函数

要汇总数据，你可以在 `PROC SQL` 中使用以下汇总函数。注意某些函数有多个名称，以适应 SAS 和 SQL 规范。当列出多个名称时，第一个名称是 SQL 名称。

| `AVG,MEAN` | 值的平均数或平均值 |
| `COUNT, FREQ, N` | 非空值的个数 |
| `CSS` | 修正平方和 |
| `CV` | 变异系数（百分比） |
| `MAX` | 最大值 |
| `MIN` | 最小值 |
| `NMISS` | 缺失值的个数 |
| `PRT` | 学生 t 分布绝对值大于概率 |
| `RANGE` | 值的范围 |
| `STD` | 标准差 |
| `STDERR` | 均标准误 |
| `SUM` | 值的总和 |
| `T` | 用于检验总体均值为零假设的学生 t 值 |
| `USS` | 未修正的平方和 |
| `VAR` | 方差 |

### 创建输出表

## 概述

要从查询结果创建新表，请使用 `CREATE TABLE` 语句，该语句包含关键字 `AS` 以及在 `PROC SQL` 查询中使用的子句：`SELECT`、`FROM` 以及任何可选子句（如 `ORDER BY`）。`CREATE TABLE` 语句将你的查询结果存储在表中，而不是作为报告显示结果。

| 通用形式，用于从查询结果创建表的基本 PROC SQL 步骤：`PROC SQL;CREATE TABLE table-name ASSELECT column-1<,...column-n>FROM table-1|view-1<,...table-n|view-n><WHERE expression><GROUP BY column-1<,... column-n>><ORDER BY column-1<,... column-n>>;` 这里是对语法的解释：`table-name` 指定要创建的表的名称。 |

注意：查询还可以包含 `HAVING` 子句，该子句将在本章末尾介绍。要了解更多关于 `HAVING` 子句的信息，请参阅 使用 PROC SQL 执行高级查询。注意：`CREATE TABLE` 语句不产生输出。要查看表的内容，请使用 SELECT 语句 中描述的 `SELECT` 语句。

## 示例

假设你想确定 `Sasuser.Frequentflyers` 每个会员等级（金牌、银牌和铜牌）的旅行总里数，并将这些信息存储在临时表 `Work.Miles` 中。要这样做，你可以提交以下 `PROC SQL` 步骤：

```sql
proc sql;
create table miles as
      select membertype,
             sum(milestraveled) as TotalMiles
      from sasuser.frequentflyers
      group by membertype;
``` SAS 日志

```text
NOTE: 已创建 WORK.MILES，具有三行两列。
```

在此示例中，要永久保存使用 Sasuser

### 附加功能

为了进一步筛选包含 `GROUP BY` 子句的查询，可以使用 `HAVING` 子句。`HAVING` 子句配合 `GROUP BY` 子句根据一个或多个条件进行。例如，下面的 `PROC SQL` 查询使用汇总函数 `AVG` 来指定平均工资大于 40000 的组。

```sql
proc sql;
   select jobcode,avg(salary) as Avg
      from sasuser.payrollmaster
      group by jobcode
      having Avg>40000
      order by jobcode;
```

注意：你可以在使用 PROC SQL 执行高级查询中了解更多关于 `HAVING` 子句的信息。

## 总结

## 文字总结

### PROC SQL 基础

`PROC SQL` 使用结构化查询语言（SQL）编写的语句，SQL 是一种广泛用于检索和更新表以及基于表的视图语言。当你想要检查数据值之间的关系、划分数据或计算值时，SQL 过程提供了一种灵活的方法。PROC SQL 与大多数其他 SAS 过程有几个不同之处：

*   `PROC SQL` 中的许多语句包含子句。

*   `PROC SQL` 步骤不需要 `RUN` 语句。

*   `PROC SQL` 在提交步骤后会继续运行。你需要提交另一个 `PROC` 步骤、`DATA` 步骤或 `QUIT` 语句来结束过程。

### 编写 PROC SQL 步骤

在创建查询之前，必须为要使用的 SAS 库分配 libref。然后提交 `PROC SQL` 步骤。你使用 `PROC SQL` 语句来调用 SQL 过程。

### 选择列

要指定查询中显示的列（列），请在 `SELECT` 语句的第一个子句中写 `SELECT` 子句。在 `SELECT` 子句中，你可以指定现有列并创建包含文本或计算结果的新列。

### 指定表

你在 `FROM` 子句中指定要查询的表。





要根据条件划分子集，请编写一个包含表达式的 `WHERE` 子句。

### 行排序

`PROC SQL` 查询输出的行顺序是无法保证的，除非你指定了排序顺序。要按特定列的值对行排序，请使用 `ORDER BY` 子句。

### 查询多个表

你可以使用 `PROC SQL` 步骤查询存储在两个或多个表中的数据。在 SQL 术语中，这被称为连接表（joining）。按照以下步骤连接多个表：

1. 在 `SELECT` 子句中指定来自一个或两个表的列名；如果你选择的列在多个表中具有相同的名称，请在该列名前前加上表名前缀。
2. 在 `FROM` 子句中指定每个表名。
3. 使用 `WHERE` 子句根据条件从两个或多个表中选择行。
4. 使用 `ORDER BY` 子句根据所选列（或列）的值对从两个或多个表中检索的行进行排序。

### 汇总分组数据

你可以在 `PROC SQL` 步骤中使用 `GROUP BY` 子句对数据进行分组汇总。`GROUP BY` 子句用于包含一个或多个汇总函数的查询。汇总函数会为 `GROUP BY` 子句中定义的每个组生成统计摘要。

### 创建输出表

要根据查询结果创建新表，你可以在 `PROC SQL` 步骤中使用 `CREATE TABLE` 语句。该语句允许你将结果存储在表中，而不是将查询结果作为报告显示。

### 附加功能

若要进一步细化化包含 `GROUP BY` 子句的 `PROC SQL` 查询，你可以使用 `HAVING` 子句。`HAVING` 子句与 `GROUP BY` 子句配合使用，根据一个或多个指定的条件限制输出中显示的组。

## 示例程序

### 查询表

```
proc sql;
   select empid,jobcode,salary,
          salary*.06 as bonus
      from sasuser.payrollmaster
      where salary<32000
      order by jobcode;
quit;
```

### 汇总分组数据

```
proc sql;
   select membertype,
          sum(milestraveled) as TotalMiles
      from sasuser.frequentflyers
      group by membertype;
quit;
```

### 从两个表的查询结果创建表

```
proc sql;
   create table work.miles as
      select salcomps.empid,lastname,
             newsals.salary,newsalary
      from sasuser.salcomps,sasuser.newsals
      where salcomps.empid=newsals.empid
      order by 2;
quit;
```

## 注意事项

- 不要对 SQL 过程使用 `RUN` 语句。
- 不在子句末尾不要加分号，除非它是语句中的最后一个子句。
- 当连接多个表时，务必在 `WHERE` 子句中指定具有匹配数据值的列。
- 要结束 SQL 过程，你可以提交另一个 `PROC` 步骤、一个 `DATA` 步骤或 `QUIT` 语句。

# 练习

为每个问题选择最佳答案。完成练习后，使用附录中的答案检查你的答案。

1. 下面 `PROC SQL` 程序中的哪个子句书写错误？

```
proc sql;
   select style sqfeet bedrooms
      from choice.houses
      where sqfeet ge 800;
```

1. `SELECT`
2. `FROM`
3. `WHERE`
4. `a 和 c 都正确`

2. 下面程序包含多少语句？

```
proc sql;
   select grapes,oranges,
          grapes + oranges as sumsales
      from sales.produce
      order by sumsales;
```

1. `两个`
2. `三个`
3. `四个`
4. `五个`

3. 完成以下 `PROC SQL` 查询，以从 `List.Size` 表中选择列 `Address` 和 `SqFeet`，并从 `List.Price` 表中选择 `Price`。（只有 `Address` 列出现在两张表中。）

```
proc sql;
   _____________
       where size.address = price.address;
       from list.size,list.price;
```

1. `select address,sqfeet,price`
2. `select size.address,sqfeet,price`
3. `select price.address,sqfeet,price`
4. `b 或 c 均`

4. 下面哪个子句正确地按 `Price` 和 `SqFeet` 列的值对行进行排序？

1. `order price, sqfeet`
2. `order by price,sqfeet`
3. `sort by price sqfeet`
4. `sort price sqfeet`

5. 下面哪个子句指定查询 `Produce` 和 `Hardware` 两个表？这两个表都位于分配了 libref `Sales` 的库中。

1. `select sales.produce sales.hardware`
2. `from sales.produce sales.hardware`
3. `from sales.produce,sales.hardware`
4. `where sales.produce, sales.hardware`

6. 完成下面的 `SELECT` 子句，通过从 `Price` 列的值减去 `Cost` 列的值创建一个名为 `Profit` 的新列。

```
select fruit,cost,price,
    ________________
```

1. `Profit=price-cost`
2. `price-cost as Profit`
3. `profit=price-cost`
4. `Profit as price-cost`

7. 在 `PROC SQL` 步骤中使用没有汇总函数的 `GROUP BY` 子句会发生什么？

1. 步骤不执行。
2. 对第一个数值列求和。
3. `GROUP BY` 子句变为 `ORDER BY` 子句。
4. 步骤执行但不分组或排序。

8. 如果在 `PROC SQL` 步骤中指定了 `CREATE TABLE` 语句，

1. 显示查询结果并创建一个新表。
2. 创建新表但不包含 `PROC SQL` 步骤中指定的任何汇总。
3. 创建新表但不显示报告。
4. 结果按汇总列的值进行分组。

9. 关于使用 `PROC SQL` 步骤查询存储在两个或多个表中的数据，哪个陈述是正确的？

1. 连接多个表时，表必须包含公共列。
2. 你必须指定从哪个表中读取每个列。
3. 连接表必须来自相同的数据源。
4. 如果连接的两个表包含相同列，则必须指定从哪个表中读取该列。

10. 下程序中的哪个子句是错误的？

```
proc sql;
   select sex,mean(weight) as avgweight
      from company.employees company.health
      where employees.id=health.id
      group by sex;
```

1. `SELECT`
2. `FROM`
3. `WHERE`
4. `GROUP BY`

# 结束注释

脚注 1：列标签的显示进一步取决于 `LABEL|NOLABEL` 系统选项。如果该选项被设置为 `NOLABEL`，则标签将不会作为输出中的列标题。该选项可以由你的站点管理员设置。返回]

# 第 2 章：使用 PROC SQL 执行高级查询





## 概述

## 引言

`SELECT` 语句是 `PROC SQL` 的主要工具。使用 `SELECT` 语句，你可以从一个或多个表和视图识别、处理和检索数据列。你应该已经熟悉如何使用 `SELECT` 语句及其大部分子句来创建基本的 PROC SQL 查询。在现有技能的基础上，本章介绍了各种实用的查询技术，例如使用子查询对数据进行子集处理。下面所示 PROC SQL 查询说明了一些新的查询技术：

```
proc sql outobs=20;
title 'Job Groups with Average Salary';
title2 '> Company Average';
   select jobcode, 
          avg(salary) as AvgSalary format=dollar11.2,
          count(*) as Count
      from sasuser.payrollmaster
      group by jobcode
      having avg(salary) >
         (select avg(salary)
            from sasuser.payrollmaster)
      order by avgsalary desc;
```

![PROC SQL query](img/m70-1-g1.png)

# 查看 SELECT 语句语法

`SELECT` 语句及其子句是构建所有 PROC SQL 查询的基石。

| 通用形式，`SELECT` 语句：`SELECT column-1<, ... column-n>FROM table-1<, ... table-n | view-n><WHERE expression><GROUP BY column-1<, ... column-n>><HAVING expression><ORDER BY column-1<, ... column-n>>;` 这里是对语法的解释：`SELECT` 指定在输出中出现的列（s）；`FROM` 指定要查询的表（s）或视图（s）；`WHERE` 使用表达式根据一个或多个条件对数据进行子集或限制；`GROUP BY` 根据指定的列（s）将数据分组；`HAVING` 使用表达式根据分组条件对数据组进行子集或限制；`ORDER BY` 根据指定列（s）的值对查询返回的行进行排序。 |

注意：PROC SQL `SELECT` 语句中的子句必须按照所示顺序指定。除了 `HAVING` 子句外，你应该熟悉 `SELECT` 语句的所有子句。`HAVING` 子句的使用将在本章后面介绍。现在，我们来看一些限制和划分查询输出中显示列数的方法。

### 显示所有列

你已经知道如何在 `SELECT` 语句中列出特定列来选择输出列。然而，对于某些任务，你会发现同时显示表的所有列是有用的。例如，在创建复杂查询之前，你可能想查看你正在处理的表的内容。

## 使用 SELECT *

要按照表中存储的顺序显示所有列，请在 `SELECT` 子句中使用星号 (`*`)。默认情况下显示所有行，除非你对其进行限制或划分。以下 `SELECT` 步骤显示了 `Sasuser.Staffchanges` 表中的所有列和行，该表列出了公司所有就业状态发生变化的员工。

```
proc sql;
   select *
      from sasuser.staffchanges;
```

如输出所示，表包含六列六行。![显示 Sasuser.Staffchanges 表中的所有行列](img/m70-3-g1.png)

## 使用 FEEDBACK 选项

当你指定 `SELECT *` 时，也可以 PROC SQL 语句中使用 `FEEDBACK` 选项，它会将扩展列表写入 SAS 日志。例如，以下查询显示了：

```
proc sql feedback;
   select *
      from sasuser.staffchanges;
```

`FEEDBACK` 选项是一个调试工具，让你确切看到提交了什么。它会将星号 (`*`) 扩展为列列表。

### 限制显示的行数

## 概述

在创建 PROC SQL 查询时，有时发现限制显示的行数是有用的。要指定显示的最大行数，你可以在 PROC SQL 语句中使用 `OUTOBS=` 选项。

| 通用形式，带有 `OUTOBS=` 的 PROC SQL 语句：` 这里是对语法的解释：`OUTOBS=` 指定行数。 |

注意：`OUTOBS=` 选项限制的是显示的行，而不是读取的行。要限制 PROC SQL 接收输入的行数，请使用 `INOBS=` 选项。

## 示例

假设你想快速查看表中的值类型，而不必打印所有行。以下 PROC SQL 查询从 `Sasuser.flightschedule` 表中选择数据，该表包含 200 多行。为了只打印输出的前 10 行，你向 PROC SQL 语句中添加了 `OUTOBS=` 选项。

```
proc sql outobs=10;
   select flightnumber, date
      from sasuser.flightschedule;
```

![来自 Sasuser.Staffchanges 表的前 10 行](img/m70-5-g1.png)

当你限制显示的行数时，SAS 日志中会出现类似下面的消息。

```
WARNING: Statement terminated early due to OUTOBS=10 option.
````OUTOBS=` 和 `INOBS=` 选项影响使用 `CREATE TABLE` 语句创建表以及你的报告输出

# 消除输出中的重复行

在某些情况下，你可能只想显示 `SELECT` 子句列出的列（s）中的唯一值或值的组合。你可以通过在 `SELECT` 子句中使用 `DISTINCT` 关键字从查询结果中消除重复行。`DISTINCT` 关键字适用于 `SELECT` 子句列出的所有列且仅这些列。

## 示例

假设你想显示当月飞行的所有国际航班唯一航班号和目的列表。以下 PROC SQL 中的 `SELECT` 语句选择了 `Sasuser.Internationalflights` 表中的 `FlightNumber` 和 `Destination` 列：

```
proc sql outobs=12;
   select flightnumber, destination
      from sasuser.internationalflights;
```




这是输出结果。![Sasuser.Internationalflights](img/m70-6-g1.png)如你所见，仅在前 12 行中，`FlightNumber`（航班号）和`Destination`（目的地）就有几对重复的值。例如，飞往 `YYZ` 的航班号 `182` 出现在第 1 行和第 8 行。整个表格包含许多更多具有重复航班号和目的地的行，因为每班航班都有固定的行程。要删除包含重复值的行，请在 `SELECT` 语句的 `SELECT` 关键字之后添加 `DISTINCT` 关键字，如下例所示：

```
proc sql;
   select distinct flightnumber, destination
      from sasuser.internationalflights
      order by 1;
```

删除重复值后，输出的行数少得多，因此从 `PROC SQL` 语句中删除了 `OUTOBS=` 。此外，为了通过 `FlightNumber`（`SELECT` 子句列表中的第 1 列）排序输出，添加了 `ORDER BY` 子句。这是修改后的程序的输出。![Sasuser.Internationalflights output](img/m70-6-g2.png)输出中没有重复行。该表中有 7 个唯一的 `FlightNumber-Destination` 值对。

# 使用条件运算符对行进行子集

## 概述

在 `PROC SQL` 查询的 `WHERE` 子句中，你可以指定任何有效的 SAS 表达式来子集或限制在输出中显示的数据。该表达式可能包含各种类型的运算符，如下所示。

| 运算符类型 | 示例 |
| --- | --- |
| 比较 | ```sql
where membertype='GOLD'
``` | |
| 逻辑 | ```sql
where visits<=3 or status='new'
``` | |
| 连接 | ```sql
where name=trim(last)||', '||'first
``` | |

注意：有关可在 SAS 表达式中使用的运算符完整列表，请参阅 SAS 文档。

## 在 PROC SQL 中使用运算符

比较、逻辑和连接运算符在 `PROC SQL` 中的用法与其他 SAS 过程中的用法相同。例如，以下 `WHERE` 子句包含：

*   逻辑运算符 `AND`，它用于连接多个条件。
*   两个比较运算符：等号 (`=`) 和大于符号 (`>`) 。

```sql
proc sql;
   select ffid, name, state, pointsused
      from sasuser.frequentflyers
      where membertype='GOLD' and pointsused>0
      order by pointsused;
```

在 `PROC SQL` 查询中，你还可以使用以下条件运算符。除了 `ANY`、`ALL` 和 `EXISTS` 之外，所有这些运算符也可以用于其他 SAS 过程。

| 条件运算符 | 测试对象 | 示例 |
| --- | --- | --- |
| BETWEEN-AND | 发生于闭区间范围内的值 | ```sql
where salary between 70000
             and 80000
``` | |
| CONTAINS 或 `?` | 包含指定字符串的值 | ```sql
where name contains 'ER' 
where name ? 'ER'
``` | |
| IN | 匹配列表中任一值的值 | ```sql
where code in ('PT' , 'NA', 'FA')
``` | |
| IS MISSING 或 IS NULL | 缺失值 | ```sql
where dateofbirth is missing
where dateofbirth is null
``` | | |
| LIKE (带有 `%`, `_`) | 匹配指定模式的值 | ```sql
where address like '% P%PLACE'
``` | | |
| `=*` | 听音类似于指定值的值 | ```sql
where lastname=* 'Smith'
``` | | |
| ANY | 相对于子查询返回的任一值，满足特定条件的值 | ```sql
where dateofbirth < any
   (select dateofbirth
      from sasuser.payrollmaster
      where jobcode='FA3')
``` | | |
| ALL | 相对于子查询返回的所有值，满足特定条件的值 | ```sql
where dateofbirth < all
   (select dateofbirth
      from sasuser.payrollmaster
      where jobcode='FA3')
``` | | |
| EXISTS | 子查询返回的值是否存在 | ```sql
where exists
   (select *
      from sasuser.flightschedule
      where fa.empid=
            flightschedule.empid) 
``` | | |

提示：要创建反向条件，可以在这些条件运算符（`ANY` 和 `ALL` 之外）之前加上 `NOT` 运算符。这些大多数条件运算符及其用法将在接下来的几节中介绍。`ANY`、`ALL` 和 `EXISTS` 将在章节的后部分讨论。

## 使用 BETWEEN-AND 运算符选择范围内的值

要根据数值或字符值的范围来选择行，请在 `WHERE` 子句中使用 `BETWEEN-AND` 运算符。`BETWEEN-AND` 运算符是包含边界的，因此你指定的作为范围限制的值会被包含在查询结果中，外加两个限制之间的任何值。

| 通用形式，`BETWEEN-AND` 运算符：`BETWEEN value-1 AND value-2` 这里是对该语法的解释：`value-1` 是范围一端的值；`value-2` 是范围另一端的值。 |

注意：在指定值范围的限制时，没有必要先指定较小的值。以下是包含 `BETWEEN-AND` 运算符的 `WHERE` 子句示例，显示不需要先指定较小值的情况。

| 示例 | 返回的行 |
| --- | --- |
| ```sql
where salary between 70000
and 80000
``` | 范围在 70000 到 80000 之间的值（包含边界）。 |
| ```sql
where date between '2023-01-01' and '2023-12-31'
``` | 日期在 2023-01-01 到 2023-12-31 之间的值（包含边界）。 |

## 使用 CONTAINS 或问号运算符选择字符串

`CONTAINS` 或问号 (`?`) 运算符通常用于选择包含特定字符串的行。这些运算符是通用的。

| 通用形式，`CONTAINS` 运算符：`sql-expression CONTAINS sql-expression` | 这里是对该语法的解释：`sql-expression` 是字符列、字符串（常量）或表达式。要匹配的字符串必须放在引号内。 |

注意：`PROC SQL` 获取字符串（或第二个表达式）出现在列中的任何位置的位置。匹配是区分大小写的。注意：`CONTAINS` 或问号 (`?`) 运算符不属于 ANSI 标准；它是 SAS 的增强功能。

## 示例

以下 `PROC SQL` 查询使用 `CONTAINS` 来选择 `Name` 列中包含 `ER` 的行。如输出所示，`Name` 列中任何包含 `ER` 的行都会被显示。

```sql
proc sql outobs=10;
   select name
      from sasuser.frequentflyers
      where name contains 'ER';
```

![列中包含 'ER'](img/m70-10-g1.png)





要选择包含缺失值（包括字符和数值）的行，请使用 `IS MISSING` 或 `IS NULL` 运算符。这两个运算符是可以互用的。

| 通用形式，`IS MISSING` 或 `IS NULL` 运算符 |
| :--- |
| `column IS MISSING` <br> `column IS NULL` |
| **以下是语法说明：** <br> `column` 指定所选的列名。 |

注意：`IS MISSING` 运算符并不是 ANSI SQL 标准的一部分。它是 SAS 的增强功能。

## 示例

假设你想查找 `Sasuser. Marchflights` 表的 `Boarded` 列中是否有任何缺失值。你可以使用以下 `PROC SQL` 查询来从表中检索出具有缺失值的行：

```
proc sql;
   select boarded, transferred,
          nonrevenue, deplaned
      from sasuser.marchflights
      where boarded is missing;
```

输出显示表中中有两行的 `Boarded` 缺失值。![Sasuser. Marchflights](img/m70-13-g1.png)

提示：或者，你也可以不使用 `IS MISSING` 或 `IS NULL` 运算符来指定缺失值，如下例所示：

```
where boarded = .
where flight = ' '
```

然而，使用 `IS MISSING` 或 `IS NULL` 运算符的优势在于你不需要指定列的数据类型（字符或数值）。

## 使用 LIKE 运算符选择模式

要选择符合特定字符模式而非固定字符字符串的行，请使用 `LIKE` 运算符。例如，使用 `LIKE` 运算符，你可以选择所有 `LastName` 值以 `H` 开头的行。（如果你想选择所有姓氏中包含字符串 `HAR` 的行，则将需要使用 `CONTAINS` 运算符。）

| 通用形式，`LIKE` 运算符 |
| :--- |
| `column LIKE 'pattern'` |
| **以下是语法说明：** <br> `column` 指定列名 <br> `pattern` 指定要匹配的模式，包含一个或两个特殊字符：下划线 (`_`) 和百分号 (`%`)。 整个模式必须包含在引号中，且匹配是区分大小写的。 |

在查询中使用 `LIKE` 运算符时，`PROC SQL` 使用模式匹配，将指定列中的每个值与你在 `WHERE` 子句中使用 `LIKE` 运算符指定的模式进行比较。查询输出将显示所有匹配的行。你可以使用下所示的一个或两个特殊字符来指定模式。

| 特殊字符 | 表示 |
| :--- | :--- |
| 下划线 (`_`) | 任意单个字符 |
| 百分号 (`%`) | 任意零或多个字符的序列 |

注意：下划线 (`_`) 和百分号 (`%`) 有时被称为通配符。

## 指定模式

要指定模式，请将一个或两个特殊字符与你想要匹配的任何其他字符结合。特殊字符可以出现在其他字符之前、之后或双侧。考虑如何组合这些特殊字符来指定模式。假设你正在处理一个包含以下名称列表的表列：

* Diana
* Diane
* Dianna
* Dianthus
* Dyan

以下是你可以使用的几种模式，用于从列表中选择一个或多个名称。每个模式都使用一个或两个特殊字符。

| LIKE 模式 | 选择的名称 |
| :--- | :--- |
| `LIKE 'D_an'` | Dyan |
| `LIKE 'D_an_'` | Diana, Diane |
| `LIKE 'D_an__` | Dianna |
| `LIKE 'D_an%'` | 列表中所有的名称 |

## 示例

以下 `PROC SQL` 查询使用 `LIKE` 运算符找到所有街道名称以 `P` 开头并 `PLACE` 结尾的常旅客会员。以下 `PROC SQL` 步骤执行了此查询：

```
proc sql;
   select ffid, name, address
      from sasuser.frequentflyers
      where address like '% P%PLACE';
```

模式 `'% P%PLACE'` 指定了以下序列：

* 任意数量字符 (`%`)
* 一个空格
* 字母 `P`
* 任意数量字符 (`%`)
* 单词 `PLACE`。

这是该查询的结果。![PROC SQL query](img/m70-14-g1.png)

## 使用 Sounds-Like (=*) 运算符选择拼写变体

要选择包含你指定的另一个值读似值的行，请在 `WHERE` 子句中使用读似运算符 `=*`。

| 通用形式，sounds-like (`*=`) 运算符 |
| :--- |
| `sql-expression =* sql-expression` |
| **以下是语法说明：** <br> `sql-expression` 是字符列、字符串（字符常量）或表达式。字符串是用于匹配的字符序列，必须包含在引号中。 |

读似运算符 `=*` 使用 `SOUNDEX` 算法将列的每个值（或其他 `sql-expression`）与你指定的单词或词（或其他 `sql-expression`）进行比较。任何包含你指定值的拼写变体的行都会被选中输出。例如，这里有一个包含读似运算符的 `WHERE` 子句：

```
where lastname =* 'Smith';
```

读似运算符 `=*` 并不总是选择所有可能的值。例如，假设你从以下列表中选择读音 似于 `Smith` 的名称：

* Schmitt
* Smithson
* Smitt
* Smythe

列表中的 Schmitt 和 Smithson 没有被选中。注意：`SOUNDEX` 算法是英语偏的，对于其他语言用处较小。关于 `SOUNDEX` 算法的更多信息，请参阅 SAS 文档。

# 使用计算值子集行

## 理解 PROC SQL 处理计算列

你应该已经知道如何通过 `SELECT` 子句执行计算来定义新列。例如，下面的 `PROC SQL` 查询通过添加现有列 `Boarded`、`Transferred` 和 `Nonrevenue` 创建新列 `Total`：

```
proc sql;
   select boarded, transferred,
          nonrevenue, deplaned
      from sasuser.marchflights
```

你还可以在 `WHERE` 子句中使用计算列来划分子集。然而，由于 SQL 查询的处理方式，你不能直接在 `WHERE` 子句中指定别名。为了观察结果，我们对之前的 `PROC SQL` 查询在 `WHERE` 语句中引用计算列 `Total`，如下所示：

```
proc sql outobs=10;
   select date, destination,
          boarded + transferred + nonrevenue
          as Total
      from sasuser.marchflights
      where total < 100;
```

当执行此查询时，SAS 日志中显示以下错误信息。

表 2.3 SAS 日志

|  |
```
519  proc sql outobs=10;
520      select date, destination,
521             boarded + transferred + nonrevenue
522             as Total
523          from sasuser.marchflights
524          where total < 100;
ERROR: The following columns were not found in the contributing tables: total.
``` |

产生此错误是因为在 SQL 查询中，`WHERE` 子句在 `SELECT` 子句之前处理。SQL 处理器会在表中查找 `WHERE` 子句中命名的列。`Sasuser.Marchflights` 表不包含名为 `Total` 的列。

## 使用关键字 CALCULATED

当在 `WHERE` 子句中使用别名引用计算值时，必须配合别名使用 `CALCULATED` 关键字。`CALCULATED` 关键字告知 `PROC SQL` 该值是在查询内部计算的。现在，PROC SQL 查询如下如下：

```
 proc sql outobs=10;
    select flightnumber, date, destination,
           boarded + transferred + nonrevenue
           as Total
       from sasuser.marchflights
       where calculated total < 100;
```




该查询执行成功并产生以下输出。![PROC SQL query](img/m70-18-g1.png)注意：作为使用 `CALCULATED` 关键字的替代方案，可以在 `WHERE` 子句中重复该计算。然而，这种方法的效率较低，因为 `PROC SQL` 必须执行两次计算。在前面的查询中，替代的 `WHERE` 语句将：

```
where boarded + transferred + nonrevenue <100;
```

你也可以在查询的其他部分使用 `CALCULATED` 关键字。在接下来的示例中，`SELECT` 子句计算了新列 `Total`，然后根据 `Total` 计算了第二个新列。要创建第二个计算列，你必须在 `SELECT` 子句中指定关键字 `CALCULATED`。

```
proc sql outobs=10;
   select flightnumber, date, destination,
          boarded + transferred + nonrevenue
          as Total,
          calculated total/2 as Half
       from sasuser.marchflights;
```

该查询产生以下输出。![PROC SQL query](img/m70-18-g2.png)注意：`CALCULATED` 关键字是 SAS 的增强功能，在 ANSI SQL 标准中并未指定。

### 增强查询输出

## 概述
当你使用 `PROC SQL` 时，你可能会发现表中的数据格式并不是你希望出现的样子。幸运的是，通过 `PROC SQL`，你可以使用如下增强功能来改进查询输出的外观：

* 列标签和格式
* 标题（titles）和脚注（footnotes）
* 包含字符常量的列

你如何在如何在 SAS 过程中使用前两种增强方法。你也可以通过处理以下查询来增强 `PROC SQL` 查询输出：

```
 proc sql outobs=15;
     select empid, jobcode, salary,
            salary * .10 as Bonus
        from sasuser.payrollmaster
        where salary>75000
        order by salary desc;
```

此查询将输出限制为 15 个观测值。`SELECT` 子句从表 `Sasuser.Payrollmaster` 中选择了三个现有的列，并计算了第四个（`Bonus`）。`WHERE` 子句仅检索 `salary` 大于 75,000 的行。`ORDER BY` 子句按 `Salary` 列进行排序，并使用关键字 `DESC` 进行降序排列。这是该查询的输出。![PROC SQL output](img/m70-21-g1.png)注意：`Salary` 列在表中指定了 `DOLLAR9.` 格式。仔细观察此输出你会发现可以进行改进。你将通过以下方法学习如何增强此输出：

* 用新标签替换原始列名
* 为 `Bonus` 列指定格式，以便所有值都以相同的小数位数显示
* 在输出顶部显示标题
* 使用字符常量添加一列

## 指定列格式和标签
默认情况下，`PROC SQL` 使用已保存在表中的列属性来格式化输出，如果没有保存任何属性，则使用默认属性。要控制输出中列的格式化，你可以在 `SELECT` 子句中指定的任何列名之后指定列修饰符，例如 `LABEL=` 和 `FORMAT=`。当你在 `SELECT` 子句中定义新列时，如果你愿意，可以分配一个标签而不是别名。

| 列修饰符 | 指定... | 示例 |
| --- | --- | --- |
| `LABEL=` | 为列显示的标签 |  ```
select hiredate
       label='Date of Hire'
``` |
| `FORMAT=` | 用于显示列数据的格式 |  ```
select hiredate
       format=date9.
``` |

注意：`LABEL=` 和 `FORMAT=` 不属于 ANSI 标准的一部分。这些列修饰符是 SAS 的增强功能。提示：若要强制 `PROC SQL` 忽略表中的永久标签，请指定系统选项 `NOLABEL`。你的第一个任务是为前两列指定列标签。下面，在 `EmpID` 和 `JobCode` 之后都添加了 `LABEL=` 选项，并且每个标签的文本都括在引号内。为了方便阅读，`SELECT` 子句中的四个列现在每个都单独列成一行。

```
proc sql outobs=15;
   select empid label='Employee ID',
          jobcode label='Job Code',
          salary,
          salary * .10 as Bonus
      from sasuser.payrollmaster
      where salary>75000
      order by salary desc;
```

接下来，你为 `Bonus` 列添加格式。因为 `Bonus` 值是金额，所以你使用格式 `Dollar12.2.`。`FORMAT=` 修饰符已添加在下面的 `SELECT` 子句中，紧随列别名 `Bonus` 之后：

```
proc sql outobs=15;
   select empid label='Employee ID',
          jobcode label='Job Code',
          salary,
          salary * .10 as Bonus
          format=dollar12.2
   from sasuser.payrollmaster
   where salary>75000
   order by salary desc;
```

现在已经指定了列格式和标签，你可以为此 `PROC SQL` 查询添加一个标题。

## 指定标题和脚注
你应该已经如何在其他 SAS 过程中指定和取消标题和脚注。当你使用 `PROC SQL` 查询指定标题和脚注时，你必须在以下位置之一放置 `TITLE` 和 `FOOTNOTE` 语句：

* `PROC SQL` 语句之前
* `PROC SQL` 语句与 `SELECT` 子句之间

在接下来的 `PROC SQL` 查询中，在 `PROC SQL` 语句和 `SELECT` 子句之间添加了两个标题行：

```
 proc sql outobs=15;
title 'Current Bonus Information';
title2 'Employees with Salaries > $75,000';
    select empid label='Employee ID',
           jobcode label='Job Code',
           salary,
           salary * .10 as Bonus
           format=dollar12.2
       from sasuser.payrollmaster
       where salary>75000
       order by salary desc;
```

现在更改已完成，你可以查看输出。![Bonus Information, Employees with Salaries > $75,000](img/m70-23-g1.png)前两列具有新标签，`Bonus` 值格式统一，且顶部显示了两个标题行。

## 在输出中添加字符常量
另一种增强 `PROC SQL` 查询输出的方法是定义一个包含字符常量的列。为此，句中使用引号包含字符串。提示：你可以以类似的方式定义包含数值常量的列，即在 `SELECT` 子句中列出数值（不带引号）。你可以再次查看之前的 `PROC SQL` 输出，确定可以在哪里添加字符串。![Bonus Information, Employees with Salaries > $75,000](img/m70-24-g1.png)你可以移除列标签 `Bonus`，并在 `Bonus` 列左侧在新列中显示 `bonus is:`。这就是你希望查询输出的样子。![Bonus Information, Employees with Salaries > $75,000](img/m70-24-g2.png)要指定一个包含字符常量的新列，你需要在 `SELECT` 列表中使用引号包含字符串。你修改后的 `PROC SQL` 查询所示：

```
proc sql outobs=15;
title 'Current Bonus Information';
title2 'Employees with Salaries > $75,000';
   select empid label='Employee ID',
          jobcode label='Job Code',
          salary,
          'bonus is:',
          salary * .10 format=dollar12.2
      from sasuser.payrollmaster
      where salary>75000
      order by salary desc;
```

在 `SELECT` 子句列表中，`Salary` 和 `Bonus` 之间添加了字符串 `bonus is:`。注意，`SELECT` 子句最后一行已删除了 `as Bonus` 代码。现在已经添加了字符常量，不再需要列别名 `Bonus`。



与其仅仅列出单独的行，您可以使用摘要函数（也称为聚合函数）来生成表格中数据的统计摘要。例如，在以下查询的 `SELECT` 子句中，`AVG` 函数计算了频繁飞行员俱乐部会员的平均（或平均）里程数。`GROUP BY` 子句告诉 `PROC SQL` 计算并显示每个会员组（`MemberType`）的平均值。

```
proc sql;
   select membertype, 
          avg(milestraveled)
          as AvgMilesTraveled
      from sasuser.frequentflyers
      group by membertype;
```

| | ![每个成员类型的平均里程数](img/m70-26-g1.png) | |

您应该已经熟悉了 `PROC SQL` 查询中可以使用的摘要函数列表。`PROC SQL` 根据多种因素的组合以不同的方式计算摘要函数并输出结果。四个关键因素是：

- 摘要函数是否指定了一个列或多个列作为参数
- 查询是否包含 `GROUP BY` 子句
- 如果在 `SELECT` 子句中指定了摘要函数，是否列出了摘要函数之外的额外列
- 如果存在 `WHERE` 子句，它是否仅包含在 `SELECT` 子句中指定的列

为了确保您的 `PROC SQL` 查询产生预期的输出，理解上述因素如何影响摘要函数的处理至关重要。请考虑对所有因素进行概述，随后通过一个详细的示例来阐述每个因素。

## 参数数量与摘要函数处理

摘要函数在括号中指定一个或多个参数。在本章所示的示例中，参数始终是所查询表中的列。注意：ANSI 标准摘要函数（如 `AVG` 和 `COUNT`）只能与单个参数一起使用。SAS  own 摘要函数（如 `MEAN` 和 `N`）可以使用单个或多个参数。下表显示了指定作为参数的列数如何影响 `PROC SQL` 计算摘要函数。

| 如果摘要函数... | 那么计算将... | 示例 |
| --- | --- | --- |
| 指定一个列作为参数 | 沿列向下执行 | ```sql\nproc sql;\n    select avg(salary)as AvgSalary\n       from sasuser.payrollmaster;\n``` ``` |
| 指定多个列作为参数 | 针对每行跨列执行 | ```sql\nproc sql outobs=10;\n    select sum(boarded,transferred,nonrevenue)\n           as Total\n       from sasuser.marchflights;\n``` ``` |

## 分组与摘要函数处理

摘要函数对数据组进行计算。当 `PROC SQL` 处理摘要函数时，它会寻找 `GROUP BY` 子句：

| 如果存在 `GROUP BY` 子句... | 那么 `PROC SQL`... | 示例 |
| --- | --- | --- |
| 查询中不存在 | 将函数应用于整个表 | ```sql\nproc sql outobs=10;\n    select jobcode, avg(salary)\n           as AvgSalary\n       from sasuser.payrollmaster;\n``` ``` |
| 查询中存在 | 将函数应用到 `GROUP BY` 子句中指定的每个组 | ```sql\nproc sql outobs=10;\n    select jobcode, avg(salary)\n           as AvgSalary\n       from sasuser.payrollmaster\n       group by jobcode;\n``` ``` |

如果查询包含 `GROUP BY` 子句，`SELECT` 子句中所有不包含摘要函数的列都应该列在 `GROUP BY` 子句中，否则可能会返回意外的结果。

## SELECT 子句列与摘要函数处理

包含摘要函数的 `SELECT` 子句还可以列出未在摘要函数中指定的额外列。`SELECT` 列表中这些额外列的存在会导致 `PROC SQL` 以不同的方式显示输出。

| 如果 `SELECT` 子句... | 那么 `PROC SQL`... | 示例 |
| --- | --- | --- |
| 包含摘要函数且摘要函数之外没有列 | 使用摘要函数为整个表计算单个值；或者如果 `GROUP BY` 子句中指定了组，则为每个组将信息合并或汇总为整个表的单行输出；或者如果指定了组，则针对每个组 | ```sql\nproc sql;\n    select avg(salary)\n           as AvgSalary\n       from sasuser.payrollmaster;\n``` ``` |
| 包含摘要函数以及摘要函数外的额外列 | 为整个表计算单个值，或者如果指定了组，则为每个组计算，并带有重复的单值或分组值显示所有输出行 | ```sql\nproc sql;\n    select jobcode,\n            gender,\n           avg(salary)\n           as AvgSalary\n       from sasuser.payrollmaster\n       group by jobcode,gender;\n``` ``` |

注意：`WHERE` 子句的列也会影响摘要函数的处理。如果 `WHERE` 子句仅引用了 `SELECT` 子句中指定的列，`PROC SQL` 将信息合并为单行输出。然而，本章未涵盖此情况。更多信息请参阅 SQL 过程 文 文。在接下来的几节中，请仔细查看上述查询示例，了解前三个因素如何影响摘要函数的处理。比较两个包含摘要函数的 `PROC SQL` 查询：一个带单个参数，另一个带多个参数。为了简单起见，这些查询不包含 `GROUP BY` 子句。

## 使用单参数（列）的摘要函数

下面是一个 `PROC SQL` 查询，用于显示 `Sasuser.Payrollmaster` 表中所有员工的平均薪资：

```sql
 proc sql;
    select avg(salary) as AvgSalary
       from sasuser.payrollmaster;
```

`SELECT` 语句包含摘要函数 `AVG`，并将 `Salary` 作为其参数。因为只有一个列作为参数，该函数沿 `Salary` 列向下计算统计值，显示单个值：所有员工的平均薪资。输出所示![平均薪资](img/m70-29-g1.png)

## 使用多参数（列）的摘要函数

考虑一个包含多个列作为参数的摘要函数的 `PROC SQL` 查询。该查询通过相加 `boarded`、`transferred` 和 `nonrevenue` 乘客的数量，计算 3 月份每个航班的总人数：

```sql
 proc sql outobs=10;
    select sum(boarded,transferred,nonrevenue)
           as Total
       from sasuser.marchflights;
```

`SELECT` 子句包含摘要函数 `SUM`，并将三个列作为参数。由于该函数包含多个参数，统计值针对每行跨这三列进行计算，产生如下输出![来自列的输出](img/m70-29-g2.png) 注意：如果没有 `OUTOBS=` 选项，表中的所有行将显示在输出中。考虑包含 `GROUP BY` 子句和摘要函数外的列如何影响包含摘要函数的 `PROC SQL` 查询。

## 不带 GROUP BY 子句使用摘要函数

再次是这个 `PROC SQL` 查询，用于显示 `Sasuser.Payrollmaster` 表中所有员工的平均薪资。该查询包含摘要函数，但由于目标是显示所有员工的平均值，因此没有 `GROUP BY` 子句。

```sql
 proc sql outobs=20;
    select avg(salary) as AvgSalary
       from sasuser.payrollmaster;
```

注意 `SELECT` 子句仅列出一列：由摘要计算定义的计算列。摘要函数之外没有其他列。这是查询输出![所有员工的平均薪资](img/m70-30-g1.png)

## 在摘要函数外的列使用摘要函数




假设你为每个作业组计算了平均值，并按作业代码对结果进行分组。你的第一步是在 `SELECT` 子句列表中添加一个现有的列（`JobCode`）。修改后的查询显示所示：

```
proc sql outobs=20;
   select jobcode, avg(salary) as AvgSalary
      from sasuser.payrollmaster;
```

现在考虑由于 `SELECT` 语句包含了一个不是汇总函数参数的列（`JobCode`），查询的输出看起来是什么样子的。![带有 JobCode 的平均薪资](img/m70-30-g2.png) 注意：请记住此 `PROC SQL` 查询使用 `OUTOBS=` 选项将输出限制在 20 行。如果没有此限制，此查询的输出将显示表中的所有 148 行。如结果所示，在 `SELECT` 子句中添加一个不在汇总函数内的列会导致 `PROC SQL` 输出所有行，而不是单个值。为了生成此输出，`PROC SQL`

* 计算了整列的平均薪资作为一个单个值（54079.62）
* 在输出中显示了所有行，因为 `JobCode` 未在汇总函数中指定。

因此，`AvgSalary` 的单个值在每行中重复。注意：当提交此查询时，SAS 日志显示一条指示发生数据重新合并（data remerging）的消息。数据重新合并将在本章后部分解释。这个结果很有趣，但你还没有达到目标：按 `JobCode` 对数据分组。下一步是添加 `GROUP BY` 子句。

## 使用 GROUP BY 子句使用汇总函数

下面是前一页的 `PROC SQL` 查询，其中添加了指定列 `JobCode` 的 `GROUP BY` 子句。（在 `SELECT` 子句中，指定了 `JobCode` 但未将其用作汇总函数参数。）查询的其他更改还包括移除 `OUTOBS=` 选项（它是不必要的）并为 `AvgSalary` 列指定格式。

```
 proc sql;
    select jobcode, 
           avg(salary) as AvgSalary format=dollar11.2
       from sasuser.payrollmaster
       group by jobcode;
```

考虑添加 `GROUP BY` 子句如何影响输出。![按 JobCode 分组的平均薪资](img/m70-31-g1.png) 成功！已为每个 `JobCode` 组计算了汇总函数，并且结果按 `JobCode` 分了组。

## 使用 COUNT 汇总函数计数值

有时你想统计整个表或行组的行数。在 `PROC SQL` 中，你可以使用 `COUNT` 汇总函数来计算具有非缺失值的行数。使用 `COUNT` 函数有三种主要方法。

| 使用这种形式的 COUNT... | 返回... | 示例 |
| --- | --- | --- |
| `COUNT(*)` | 组或表中的总行数 | 
```
select count(*) as Count
``` |
| `COUNT(column)` | 选定列中具有非缺失值的组或表中的总行数 | 
```
select count(jobcode) as Count
``` |
| `COUNT(DISTINCT column)` | 列中唯一值的总数 | 
```
select count(distinct jobcode)
       as Count
``` | |

**注意**`COUNT` 汇总函数只计算非缺失值；缺失值会被忽略。许多其他汇总函数也忽略缺失值。例如，`AVG` 函数仅返回非缺失值的平均值。当你对包含缺失值的数据使用汇总函数时，结果可能无法提供你预期的信息。在查询中使用汇总函数之前，熟悉数据是一个好主意。提示：要统计缺失值的数量，请使用 `NMISS` 函数。有关 `NMISS` 函数的更多信息，请参阅 SAS 文档。考虑使用 `COUNT` 函数的三种方法。

## 统计所有行

假设你想知道 `Sasuser. Payrollmaster` 表中列出了多少员工。该表每个员工都有单独的行，因此统计表中的行数即可得到员工人数。以下 `PROC SQL` 查询完成了此任务：

```
 proc sql;
    select count(*) as Count
       from sasuser.payrollmaster;
```

![员工总数](img/m70-34-g1.png) 注意：`COUNT` 汇总函数是唯一允许使用星号（`*`）作为参数的函数。你也可以使用 `COUNT(*)` 来统计数据组内的行。要这样做，你需要在 `GROUP BY` 子句中指定组。考虑一个使用 `COUNT(*)` 进行分组的更复杂的 `PROC SQL` 查询。这次的目标是使用与上面相同的表，找到每个作业类别内的员工总数。

```
proc sql;
   select substr(jobcode,1,2)
          label='Job Category',
          count(*) as Count
      from sasuser.payrollmaster
      group by 1;
```

此查询在 `SELECT` 子句中定义了两个新列。标记为 `JobCategory` 的第一列是通过使用 SAS 函数 `SUBSTR` 从现有的 `JobCode` 字段中提取两个字符的作业类别创建的。第二列 `Count` 是通过 `COUNT` 函数创建的。`GROUP BY` 子句指定结果按第 1 列分组（由于列未命名，故引用 `1`；因为该列未命名——此处原文括号有误）。![按 jobcode 计数](img/m70-34-g2.png) **注意**：当列包含缺失值时，`PROC SQL` 将缺失值视为一个组。这有时会产生意外的结果。

## 统计列中的非缺失值

假设你想统计特定列中的非缺失值，而不是整个表。要这样做，你需要将列名作为 `COUNT` 函数的参数。例如，以下 `PROC SQL` 查询统计 `JobCode` 列的非缺失值：

```
 proc sql;
    select count(JobCode) as Count
       from sasuser.payrollmaster;
```

 | ![缺失值计数](img/m70-35-g1.png) 由于表中没有缺失数据，此查询的结果与使用 `COUNT(*)` 相同。`JobCode` 每行都有非缺失值。然而，如果 `JobCode` 列包含缺失值，此查询产生的 `Count` 值将较低。例如，如果 `JobCode` 有三个缺失值，`Count` 的值为 145。

## 统计列中的唯一值

要统计列中的唯一值，请在作为参数的列之前添加关键字 `DISTINCT`。例如，这里是修改后的查询，仅计算唯一值：

```
proc sql;
   select count(distinct jobcode) as Count
      from sasuser.payrollmaster;
```

此查询统计了 `JobCode` 的 16 个唯一值。![JobCode 的唯一值计数](img/m70-35-g2.png)要显示唯一的 `JobCode` 值，你可以应用之前讨论的去重方法。以下查询列出了唯一的 `JobCode` 值：

```
proc sql;
   select distinct jobcode
      from sasuser.payrollmaster;
```

有 16 个作业代码，因此输出包含 16 行![唯一的 JobCode 值列表](img/m70-35-g3.png)

## 使用 HAVING 子句分组

你已经看到了如何使用 `GROUP BY` 子句对数据分组。例如，以下查询计算了每个作业代码组的平均薪资，并显示每个作业代码的平均值：

```
 proc sql;
    select jobcode, 
           avg(salary) as AvgSalary
           format=dollar11.2
       from sasuser.payrollmaster
       group by jobcode;
```



表中包含 16 个作业代码，因此输出显示了 16 行。![每个 JobCode 的平均工资](img/m70-37-g1.png)现在，假设你只想为查询输出选择一组组的子集。你可以在 `GROUP BY` 子句之后使用 `HAVING` 子句，来选择（或过滤）要显示的组。`HAVING` 子句影响组的方式与 `WHERE` 子句影响单行的方式相似。与 `WHERE` 子句一样，`HAVING` 子句包含一个用于对数据进行子集的表达式。可以使用任何有效的 SAS 表达式。当你使用 `HAVING` 子句时，`PROC SQL` 只会显示满足 `HAVING` 表达式的组。

注意：你可以在 `HAVING` 子句中使用摘要函数，但不能在 `WHERE` 子句中使用它们，因为 `HAVING` 子句用于组，而 `WHERE` 子句只能用于单行。修改上方所示的查询，使其仅选择平均工资超过 $56,000 的 `JobCode` 组。查询末尾已添加了 `HAVING` 子句。

```
 proc sql;
    select jobcode, 
           avg(salary) as AvgSalary
           format=dollar11.2
       from sasuser.payrollmaster
       group by jobcode
       having avg(salary) > 56000;
```

提示：另一种，由于平均工资已经在 `SELECT` 子句中计算过，`HAVING` 子句可以指定列别名 `AvgSalary`：

```
having AvgSalary > 56000
```

注意，你不需要在 `HAVING` 子句中指定 `CALCULATED` 关键字；但在 `WHERE` 子句中必须指定。查询输出如下所示。此输出比之前的输出小，因为只显示了作业代码组的子集![每个 JobCode 超过 $56,000 的平均工资](img/m70-37-g2.png)如果你在包含 `HAVING` 子句的查询中省略了 `GROUP BY` 子句，那么 `HAVING` 子句和摘要函数（如果有指定的话）将把整个表视为一组。如果没有 `GROUP BY` 子句，上述示例中的 `HAVING` 子句将计算整个表的平均工资（公司所有的作业），而不是每个组（每个作业代码）的。输出要么包含表中的所有行（如果整个表的平均工资大于 $56,000），要么不包含表中的任何行（如果整个表的平均工资小于 $56,000）。

## 理解数据重新合并 (Data Remerging)

有时，当你在 `SELECT` 子句或 `HAVING` 子句中使用摘要函数时，`PROC SQL` 必须重新合并数据（对表进行两次扫描）。重新合并需要额外的处理时间，而且通常是不可避免的。然而，在某些情况下，你可能修改查询以避免重新合并。了解重新合并何时以及何时发生可以提高编写高效查询的能力。考虑一个需要重新合并的 `PROC SQL` 查询。该查询计算每个导航员工资占所有导航员工资的百分比：

```
proc sql;
   select empid, salary,
          (salary/sum(salary)) as Percent
          format=percent8.2
      from sasuser.payrollmaster
      where jobcode contains 'NA';
```

当你提交此查询时，SAS 日志会显示以下消息。

表 2.4 SAS Log

| `NOTE: The query requires remerging summary statistics back with the original data.` |

只要存在以下任一条件，就会发生重新合并：

*   摘要函数返回的值被用于计算。
*   `SELECT` 子句指定了一个包含摘要函数的列以及未列在 `GROUP BY` 子句中的其他列。
*   `HAVING` 子句指定了一个或多个列或列表达式，这些列未包含在子查询或 `GROUP BY` 子句中。

在重新合并期间，`PROC SQL` 对表进行两次扫描：

1. `PROC SQL` 计算并返回摘要函数的值。`PROC SQL` 还根据 `GROUP BY` 子句对数据进行分组。
2. `PROC SQL` 获取在输出中显示所需的任何额外列和行，并使用摘要函数的结果来计算任何参与摘要函数的算术表达式。

## 示例

考虑 `PROC SQL` 在处理以下查询时是如何重新合并数据的：

```
proc sql;
   select empid, salary,
          (salary/sum(salary)) as Percent
          format=percent8.2
      from sasuser.payrollmaster
      where jobcode contains 'NA';
```

在第一遍扫描中，对于 `jobcode` 包含 `'NA` 的行，`PROC SQL` 计算并返回 `SUM` 函数的值（在 `SELECT` 子句中指定）。在第二遍扫描中，`PROC SQL` 获取输出中所需的额外列和行（`EmpID`, `Salary`）以及 `JobCode` 包含 `'NA` 的行。`PROC SQL` 还使用 `SUM` 函数的结果来计算算术表达式 `(salary/sum(salary))`。注意：某些 SQL 的实现不支持重新合并，并将上述示例视为错误。提示：你可以通过使用子查询来获得相同的结果。子查询将在本章稍后部分讨论。

# 使用子查询进行数据子集

## 子查询简介

`WHERE` 和 `HAVING` 子句都根据表达式对数据进行过滤。在本章之前的查询示例中，`WHERE` 和 `HAVING` 子句包含了标准的 SAS 表达式。例如，下面的 `WHERE` 子句使用了 `BETWEEN-AND` 条件运算符并将 `salary` 列作为操作数：

```
where salary between 70000 and 80000
```

`PROC SQL` 还提供了另一种用于 `WHERE` 和 `HAVING` 子句过滤数据的表达式类型：子查询。子查询是嵌套在另一个查询中并作为其部分的查询。注意：子查询也被称为嵌套查询、内部查询和子选择。下面的 PROC SQL 查询在 `HAVING` 子句中包含一个子查询，返回平均工资大于公司平均工资的所有作业代码：

```
proc sql;
   select jobcode, 
          avg(salary) as AvgSalary
          format=dollar11.2
      from sasuser.payrollmaster
      group by jobcode
      having avg(salary) >
         (select avg(salary)
            from sasuser.payrollmaster);
```

提示建议将子查询（内部查询）括在括号中，所示。子查询从表中选择一个或多行，然后向外部查询返回单个或多个值。上面的子查询是单值子查询；它向外部查询返回一个值，即该表的平均工资。子查询可以返回多行的值，但只针对单列。子查询引用的表可以是与外部查询引用的表相同，也可以不同。在上述 PROC SQL 查询中，子查询从相同的表中选择数据。

## 子查询的类型

有两种子查询。

| 子查询类型 | 描述 |

| --- | --- |
| 非相关 (noncorrelated) | 独立的子查询，不依赖外部查询执行 |
| 相关 (correlated) | 依赖性子查询，在外部查询向其传递一个或多个值之前，子查询才能向外部查询返回值 |

非相关和相关子查询都可以向外部查询返回单个或多个值。接下来的几节将深入探讨非相关和相关子查询以及它们是如何被处理的。




最简单的子查询是返回单个值的非相关子查询。接下来的 `PROC SQL` 查询与上一节使用的查询相同。该查询显示了平均薪资超过公司平均薪资的职位代码（job codes）。`HAVING` 子句包含一个非相关子查询。

```
proc sql;
   select jobcode, 
          avg(salary) as AvgSalary 
          format=dollar11.2
      from sasuser.payrollmaster
      group by jobcode
      having avg(salary) >
         (select avg(salary)
            from sasuser.payrollmaster);
```

`PROC SQL` 始终会在外部查询之前评估非相关子查询。如果一个查询中包含多个层级的非相关子查询，`PROC SQL` 会先评估最内层的子查询，然后向外进行，最后评估最外层的查询。在上述所示的查询中，内部查询和外部查询的处理方式如下：

1. 为了完成 `HAVING` 子句中的表达式，子查询使用 `AVG` 汇总函数并以 `Salary` 为参数，计算整个公司（表中的所有行）的平均薪资。
2. 子查询将平均薪资的值返回给外部查询。
3. 外部查询计算每个 `JobCode` 组（由 `GROUP BY` 子句定义）的平均薪资（在 `SELECT` 子句中），并仅选择平均薪资大于公司平均薪资的组。

查询输出所示![每个 JobCode 的平均薪资](img/m70-41-g1.png) 该非相关子查询仅向外部查询返回单个值，即整个公司的平均薪资。子查询和外部查询都使用相同的表作为源。

## 使用多值非相关子查询

某些子查询是多值子查询：它们向外部查询返回多个值（行）。如果你的非相关子查询可能为多行返回值，请务必在 `WHERE` 或 `HAVING` 子句中使用以下可以处理多个值的运算符之一：

-  条件运算符 `IN`
- 由 `ANY` 或 `ALL` 修改的比较操作符
-  条件运算符 `EXISTS`

**注意**：如果你创建了一个返回多个值的非相关子查询，但外部查询的 `WHERE` 或 `HAVING` 子句包含上述指定运算符之外的运算符，则查询会失败。SAS 日志中会显示错误信息，指示子查询评估的结果多于一行。例如，如果你使用等号 (`=`) 运算符配合返回多个值的非相关子查询，查询将失败。等号运算符只能处理单个值。请考虑一个既包含条件运算符 `IN` 又包含返回多个值的非相关子查询的查询。（`ANY`、`ALL` 和 `EXISTS` 运算符将在本章稍后介绍。）

## 示例

假设你想向即将过生日的员工发送生日卡片。你决定创建一个 `PROC SQL` 查询，列出所有在 2 月份生日的员工姓名和地址。与上一页所示查询不同，此查询从两个不同的表中选取数据：

- `Sasuser.Staffmaster` 表中的员工姓名和地址
- `Sasuser.Payrollmaster` 表中的员工出生日期

在这两个表中，员工都通过员工识别码 (`EmpID`）来标识。在接下来的 `PROC SQL` 查询中，`WHERE` 子句包含条件运算符 `IN`，后跟一个非相关子查询：

```
 proc sql;
    select empid, lastname, firstname, 
           city, state
       from sasuser.staffmaster
       where empid in
          (select empid
             from sasuser.payrollmaster
             where month(dateofbirth)=2);
```

该查询的处理方式如下：

1. 为了完成外部查询 `WHERE` 子句中的表达式，子查询选取出生日期为 2 月的员工。注意子查询使用了 `MONTH` 函数。
2. 随后，子查询将选定员工的 `EmpID` 值返回给外部查询。
3. 外部查询为子查询标识的员工显示数据（来自 `SELECT` 子句中标识的列）。

如下所示所示列出了六位在 2 月份生日的员工![2 月份生日的员工](img/m70-43-g1.png)尽管使用内连接（inner join）也能产生相同的结果，但在本例中使用子查询更好，因为输出中没有来自 `sasuser.payrollmaster` 表的列。

## 使用子查询进行比较

有时，将一个值与子查询返回的一组值进行比较是有帮助的。当子查询可能返回多个值时，你必须使用条件运算符 `ANY` 或 `ALL` 之一，在 `WHERE` 或 `HAVING` 子句中紧邻子查询之前修改比较运算符。例如，以下 `WHERE` 子句包含小于 (`<`) 比较运算符和条件运算符 `ANY`：

```
where dateofbirth < any
   <subquery...>
```

**注意**：如果你创建了一个返回多个值的非相关子查询，且外部查询的 `WHERE` 或 `HAVING` 子句包含未被 `ANY` 或 `ALL` 修改的比较运算符，则查询会失败。当外部查询包含被 `ANY` 或 `ALL` 修改的比较运算符时，外部查询将将其检索到的每个值与返回的值（值）进行比较。如果指定了 `ANY`，外部查询将与子查询返回的值进行比较。如果指定了 `ALL`，则只有在与子查询返回的所有值比较都为真时，该值才包含在输出中。

## 使用 ANY 运算符

指定 `ANY` 运算符的外部查询会选取与子查询返回的任何值通过测试的值。例如，假设有一个外部查询包含以下 `WHERE` 子句：

`where dateofbirth < any`

该子句指定 `DateofBirth`（操作数）小于子查询返回的 `any` 值（比较运算符）。下表显示了 `ANY` 与这些比较运算符配合：大于 (`>`)、小于 (`<`) 和等于 (`=`)。

| 带 ANY 的比较运算符 | 外部查询选取... | 示例 |
| --- | --- | --- |
| `> ANY` | 大于子查询返回的任何值 | 如果子查询返回 20, 30, 40，则外部查询选取所有 `> 20`（返回的最小值）的值 |
| `< ANY` | 小于子查询返回的任何值 | 如果子查询返回 20, 30, 40，则外部查询选取所有 `< 40`（返回的最大值）的值 |
| `= ANY` | 等于子查询返回的任何值 | 如果子查询返回 20, 30, 40，则外部查询选取所有 `= 20` 或 `= 30` 或 `= 40` 的值 |

**提示**：与其在子查询中使用 `ANY` 运算符，不如可以使用某些 SAS 函数以更高的效率实现相同的结果。与其使用 `> ANY`，不如在子查询中使用 `MIN` 函数。与其使用 `< ANY`，不如在子查询中使用 `MAX` 函数。

## 示例

假设你想识别出比所有 3 级空乘年龄大的 1 级或 2 级空乘。职位类型和级别在 `JobCode` 中标识；每个空乘的代码为 `FA1`、`FA2` 或 `FA3`。接下来的 `PROC SQL` 查询通过子查询和 `ANY` 运算符完成此任务。





```
proc sql;
   select empid, jobcode, dateofbirth
      from sasuser.payrollmaster
      where jobcode in ('FA1','FA2')
            and dateofbirth < any
               (select dateofbirth
                  from sasuser.payrollmaster
                  where jobcode='FA3');
```

当处理此查询时，发生以下情况：

1. 子查询返回所有 3 级空乘员的出生日期。
2. 外部查询仅选择出生日期小于子查询返回的任何日期的 1 级和 2 级空乘员。

注意，外部查询和子查询都使用了同一张表。注意：在内部，SAS 将日期值表示为从 1960 年 1 月 1 日到指定日期的天数。例如，1991 年 10 月 17 日的 SAS 日期为 `11612`。将日期表示为自参考日期的天数便于计算机存储它们并进行日历计算。然而，这些数字对用户没有意义，因此在大多数常用的表示法中，有多种格式用于显示日期和时间值。

下面是查询结果。
![比 3 级年长的 1 级和 2 级空乘员](img/m70-47-g1.png)

**提示** 使用 `ANY` 运算符解决此问题会导致大量的计算，增加处理时间。对于此示例，在子查询中使用 `MAX` 函数会更高效。替代方案如下：

```
where jobcode in ('FA1','FA2') 
      and dateofbirth < 
         (select max(dateofbirth)
            from [...]
```

关于 `MAX` 函数的更多信息，请参见 SAS 文档。

# 使用 ALL 运算符

指定 `ALL` 运算符的外部查询会选择通过与子查询返回的所有值比较测试的值。下表显示了使用 `ALL` 配合常用比较运算符（大于 `>` 和小于 `<`）的效果。

| 带有 `ALL` 的比较运算符 | 子查询返回的示例值 | 表示... |
| :--- | :--- | :--- |
| `> ALL` | `(20, 30, 40)` | `> 40`（大于列表中的最大数字） |
| `< ALL` | `(20, 30, 40)` | `< 20`（小于列表中的最小数字） |

## 示例

在之前的查询中将 `ANY` 替换为 `ALL`。以下查询识别比所有 3 级空乘员都年长的 1 级和 2 级空乘员：

```
proc sql;
   select empid, jobcode, dateofbirth
      from sasuser.payrollmaster
      where jobcode in ('FA1','FA2')
            and dateofbirth < all
               (select dateofbirth
                  from sasuser.payrollmaster
                  where jobcode='FA3');
```

当处理此查询时，发生以下情况：

1. 子查询返回所有 3 级空乘员的出生日期。
2. 外部查询仅选择出生日期小于子查询返回的所有日期的 1 级和 2 级空乘员。

下面的查询结果显示，只有 1 级或 2 级空乘员比所有 3 级空乘员年长。
![比所有 3 级年长的 1 级和 2 级空乘员](img/m70-48-g1.png)

**提示** 对于此示例，使用子查询中的 `MIN` 函数代替 `ALL` 运算符来解决此问题会更高效。替代的 `WHERE` 子句如下：

```
where jobcode in ('FA1','FA2') 
      and dateofbirth <
        (select min(dateofbirth)
           from [...]
```

关于 `MIN` 函数的更多信息，请参见 SAS 文档。

# 使用相关子查询筛选数据

## 概述

相关子查询无法独立评估，其结果取决于外部查询传递它们的值。相关子查询会对外部查询中的每一行进行评估，因此比非子查询需要更多的处理时间。

注意：通常，`PROC SQL` 链接是相关子查询更高效的替代方案。你应该已经熟悉基本的 `PROC SQL` 链接。

## 示例

考虑一个包含相关子查询的 `PROC SQL` 查询示例。以下查询显示所有同时也是经理的导航员名称。子查询中的 `WHERE` 子句列出了 `Staffmaster.EmpID`。外部查询必须将此列传递给相关子查询。

```
proc sql;
   select lastname, firstname
      from sasuser.staffmaster
      where empid = (select empid
                    from sasuser.supervisors
                    where staffmaster.empid = supervisors.empid);
```

注意：当一列出现在多个表时，列名之前会加上表名或别名以避免歧义。在本示例中，`empid` 出现在两个表中，因此在对该列的每次引用之前都指定了相应的表名。此查询的输出如所示。有三个导航员同时也是经理。
![作为经理的导航员列表](img/m70-51-g1.png)

# 使用 EXISTS 和 NOT EXISTS 条件运算符

在 `WHERE` 子句或外部查询的 `HAVING` 子句中，你可以使用 `EXISTS` 或 `NOT EXISTS` 条件运算符来测试子查询返回的值集是否存在。

| 条件 | 如果满足则真 |
| :--- | :--- |
| `EXISTS` | 子查询返回至少一行 |
| `NOT EXISTS` | 子查询未返回数据 |

注意：`EXISTS` 和 `NOT EXISTS` 运算符可以用于相关子查询和非子查询。

## 示例：带有 NOT EXISTS 的相关查询

考虑一个包含 `NOT EXISTS` 条件运算符的示例 `PROC SQL` 查询。假设你有以下表：

* `Flightendants` 包含空乘员的姓名和员工 ID 号。
* `Flightschedule` 每个日期对应一个行数据。

如图所示，这两个表的交集包含了所有已安排工作的空乘员的数据。
![已安排工作的空乘员](img/m70-g1.png)

现在假设你想列出没有安排工作的空乘员。也就是说，你想识别下方高亮区域的数据。
![已安排工作的空乘员，高亮未安排工作的部分](img/m70-g2.png)

以下 `PROC SQL` 查询通过使用相关子查询和 `NOT EXISTS` 运算符完成此任务：

```
proc sql;
    select lastname, firstname
       from sasuser.flightendants
       where not exists
          (select *
             from sasuser.flightschedule
             where flightendants.empid=flightschedule.empid);
```

输出所示。
![未安排航班的员工列表](img/m70-g3.png)

### 验证查询语法

## 概述

当你构建 `PROC SQL` 查询时，可能会发现在不实际执行的情况下检查查询更高效。为了在不执行查询的情况下验证语法以及引用的列和表的存在性，请使用以下任一方法：

* `PROC SQL` 语句中的 `NOEXEC` 选项
* `SELECT` 语句前的 `VALIDATE` 关键字

考虑如何指定 `NOEXEC` 选项和 `VALIDATE` 关键字，并检查它们之间的细微差异。

## 使用 NOEXEC 选项

在以下 `PROC SQL` 语句中指定了 `NOEXEC` 选项：

```
proc sql noexec;
   select empid, jobcode, salary
      from sasuser.payrollmaster
      where jobcode contains 'NA'
      order by salary;
```

如果查询有效且所有引用的列和表存在，SAS 日志将显示以下消息。

表 2.5 SAS 日志

| `NOTE: Statement not executed due to NOEXEC option.` |





或者，如果查询中有任何错误，SAS 会在日志中显示标准错误信息。当你调用 `NOEXEC` 选项时，SAS 会检查该 `PROC SQL` 步骤中所有查询的准确性，但不执行它们。

## 使用 `VALIDATE` 关键字

你在 `SELECT` 语句之前指定 `VALIDATE` 关键字；它不用于任何其他 `PROC SQL` 语句。我们将使用 `VALIDATE` 关键字代替 `NOEXEC` 选项来修改前面的 `PROC SQL` 查询：

```
proc sql;
   validate
   select empid, jobcode, salary
      from sasuser.payrollmaster
      where jobcode contains 'NA'
      order by salary;
```

注意：注意 `VALIDATE` 关键字后面没有分号。如果查询有效，SAS 日志将显示以下消息。

表 2.6 SAS 日志

| `NOTE: PROC SQL statement has valid syntax.` |

如果查询中有错误，SAS 会在日志中显示标准错误信息。`VALIDATE` 关键字与 `NOEXEC` 选项的主要区别在于，`VALIDATE` 关键字仅影响紧随其后的 `SELECT` 语句，而 `NOEXEC` 选项适用于 `PROC SQL` 步骤中的所有查询。如果你正在处理包含多个 `SELECT` 语句的 `PROC SQL` 查询，则必须在你检查的每个 `SELECT` 语句之前指定 `VALIDATE` 关键字。

### 附加功能

除了 `SELECT` 语句外，`PROC SQL` 还支持以下语句。

| 语句 | 用途 ... |
| --- | --- |
| `ALTER TABLE expression;` | 在表中添加、删除和修改列 |
| `CREATE expression;` | 构建新表、视图或索引 |
| `DELETE expression;` | 从表或视图中删除不需要的行 |
| `DESCRIBE expression;` | 显示表和视图的属性 |
| `DROP expression;` | 删除整个表、视图或索引 |
| `INSERT expression` | 向表或视图添加数据行 |
| `RESET <option(s)>;` | 在不重新调用过程的情况下添加或更改 `PROC SQL` 选项 |
| `UPDATE expression;` | 修改表或视图现有行中的数据值 |

## 总结

## 文本总结

### 查看 `SELECT` 语句语法

`SELECT` 语句及其从句是你用于构建所有 `PROC SQL` 查询的构建组件。

### 显示所有列

要按照列在表中的存储顺序显示所有列，请在 `SELECT` 子句中使用 `*`。要将展开的列列表写入 SAS 日志，请在 `PROC SQL` 语句中使用 `FEEDBACK` 选项。

### 限制显示的行数

要限制 `PROC SQL` 输出输出的行数，请在 `PROC SQL` 语句中使用 `OUTOBS=n` 选项。

### 从输出中消除重复行

要从查询结果中消除重复行，请在 `SELECT` 子句中使用 `DISTINCT` 关键字。

### 使用条件运算符划分行子集

在 `PROC SQL` 查询中，使用 `WHERE` 子句配合任何有效的 SAS 表达式对数据划分子集。SAS 表达式可以包含一个或多个运算符，包括以下条件运算符：

- `BETWEEN-AND` 运算符选择闭区间值范围内的值
- `CONTAINS` 或 `?` 运算符选择字符字符串
- `IN` 运算符从固定值列表中选择
- `IS MISSING` 或 `IS NULL` 运算符选择缺失值
- `LIKE` 运算符选择模式
- `sounds-like` (`=*`) 运算符选择拼写变体

### 使用计算值划分行子集

理解 `PROC SQL` 如何处理计算列是非常重要的。当你在 `WHERE` 子句中使用列别名来引用计算值时，你必须配合别名使用 `CALCULATED` 关键字。

### 增强查询输出

你可以通过 SAS 增强功能（如列格式和标签、标题和脚注，以及字符限制）来增强 `PROC SQL` 查询输出。

### 汇总和分组

`PROC SQL` 计算汇总函数并以不同的方式输出结果，这取决于因素的组合：

- 汇总函数是否指定了一个或多个多个列作为参数
- 查询是否包含 `GROUP BY` 子句
- 如果在 `SELECT` 子句中指定了汇总函数，是否还列出了汇总函数之外的其他列
- `WHERE` 子句（如果有）是否仅包含 `SELECT` 子句中指定的列。

要计算非缺失值的计数，请使用 `COUNT` 汇总函数。要选择要显示的组，请在 `GROUP BY` 子句之后使用 `HAVING` 子句。当你在 `SELECT` 子句或 `HAVING` 子句中使用汇总函数时，在某些情况下 `PROC SQL` 必须重新合并数据。当 `PROC SQL` 重新合并数据时，会对数据进行两次扫描，这需要额外的处理时间。

### 使用子查询划分数据

在 `PROC SQL` 查询的 `WHERE` 子句或 `HAVING` 子句中，你可以使用子查询对数据划分子集。子查询是嵌套在另一个查询中并作为其一部分查询。子查询可以向外部查询返回单行或多行的值，但只能返回单列的值。

### 使用非相关子查询划分数据

非相关子查询独立于外部查询执行执行。你可以使用返回单个值或多个值的非相关子查询。为了进一步限定在 `WHERE` 子句或 `HAVING` 子句中指定的比较，可以使用 `ANY` 和 `ALL` 运算符配合非相关（或相关）子查询。

### 使用相关子查询划分数据

相关子查询无法独立评估，因为它们的结果依赖于外部查询返回的值。在外部查询的 `WHERE` 子句或 `HAVING` 子句中，你可以使用 `EXISTS` 和 `NOT EXISTS` 运算符测试子查询返回的值集的存在或不存在性。

### 验证查询语法

要在不实际执行查询的情况下检查查询的有效性，请使用 `NOEXEC` 选项或 `VALIDATE` 语句。

### 附加功能

除了 `SELECT` 语句外，`PROC SQL` 支持许多语句。

## 示例程序

### 在输出中显示所有列并在日志显示展开列表

```
proc sql feedback;
   select *
      from sasuser.staffchanges;
quit;
```

### 从输出中消除重复行

```
proc sql;
   select distinct flightnumber, destination
      from sasuser.internationalflights
      order by 1;
quit;
```

### 使用计算值划分行子集

```
proc sql outobs=10;
   validate
   select flightnumber, destination,
          boarded + transferred + nonrevenue
          as Total
      from sasuser.marchflights
      where calculated total between 100 and 150;
quit;
```

### 使用非相关子查询划分数据

```
proc sql noexec;
   select jobcode,
          avg(salary) as AvgSalary
          format=dollar1.2
      from sasuser.payrollmaster
      group by jobcode
      having avg(salary) >
         (select avg(salary)
            from sasuser.payrollmaster);
quit;
```

### 使用相关子查询划分数据

```
proc sql;
title '不是员工的频繁飞行客';
   select count(*) as Count
      from sasuser.frequentflyers
      where not exists
         (select *
            from sasuser.staffmaster
            where name=
                  trim(lastname)||', '||firstname);
quit;
```

## 注意事项

- 当你使用汇总函数时，注意缺失值。如果表中包含缺失值，你的结果可能不符合预期。许多汇总函数在计算时会忽略缺失值，且 `PROC SQL` 将列中的缺失值视为一个组。
- 当你创建复杂查询时，使用 `NOEXEC` 选项或 `VALIDATE` 语句来验证查询而不执行它是有帮助的。

# 测验




为每个问题选择最佳答案。完成测验后，请使用附录中的答案键检查您的答案。

1. 哪个 `PROC SQL` 查询可以从输出中删除 `MemberType` 的重复值，从而仅列出唯一值？

    1. ```sql
        proc sql nodup;
           select membertype
              from sasuser.frequentflyers;
        ```

    2. ```sql
        proc sql;
           select distinct(membertype) 
                  as MemberType
              from sasuser.frequentflyers;
        ```

    3. ```sql
        proc sql;
           select unique membertype
              from sasuser.frequentflyers
              group by membertype;
        ```

    4. ```sql
        proc sql;
           select distinct membertype
              from sasuser.frequentflyers;
        ```

2. 下列哪种项会导致 `PROC SQL` 列出 `Address` 列中没有数据的行？

    1. ```sql
        WHERE address is missing
        ```

    2. ```sql
        WHERE address not exists
        ```

    3. ```sql
        WHERE address is null
        ```

    4. a 和 c 都对

3. 你正在创建一个 `PROC SQL` 查询，列出所有今年已用完（或超出）分配的 120 小时假期的员工。每位员工使用的小时数存储在现有的列 `Spent` 中。你的查询定义了一个新列 `Balance`，用来计算每位员工的剩余假期小时数。哪个查询生成了你需要的报告？

    1. ```sql
        proc sql;
           select name, spent, 
                  120-spent as calculated Balance
              from Company.Absences
              where balance <= 0;
        ```

    2. ```sql
        proc sql;
           select name, spent, 
                  120-spent as Balance 
              from Company.Absences 
              where calculated balance <= 0;
        ```

    3. ```sql
        proc sql;
           select name, spent, 
                  120-spent as Balance
              from Company.Absences
              where balance <= 0;
        ```

    4. ```sql
        proc sql;
           select name, spent, 
                  120-spent as calculated Balance
              from Company.Absences
              where calculated balance <= 0;
        ```

4. 考虑此 `PROC SQL` 查询：

    ```sql
    proc sql;
       select flightnumber,
              count(*) as Flights,
              avg(boarded) 
              label="Average Boarded"
              format=3.
          from sasuser.internationalflights
          group by flightnumber
          having avg(boarded) > 150;
    ```

    `Sasuser.Internationalflights` 包含 201 行数据、7 个唯一的 `FlightNumber` 值、115 个唯一的 `Boarded` 值，以及 4 个平均 `Boarded` 值大于 150 的不同航班号。该查询共生成了多少行输出？

    1. 150
    2. 7
    3. 4
    4. 1

5. 你正在编写一个 `PROC SQL` 查询，显示所有在图书馆担任志愿者的借证持有者的姓名，以及每位志愿者目前借出的书籍数量。你使用了以下一个或两个表：

    * `Library.Circulation` 列出所有借证持有者的姓名和联系信息，以及每个持证人目前借出的书籍数量。
    * `Library.Volunteers` 列出所有图书馆志愿者的姓名和联系信息。

    假设两个表中的 `Name` 值都是唯一的。下列哪个哪个 `PROC SQL` 查询生成了你的报告？

    1. ```sql
        proc sql;
           select name, checkedout
              from library.circulation
              where * in
                 (select *
                    from library.volunteers);
        ```

    2. ```sql
        proc sql;
           select name, checkedout
              from library.circulation
              where name in
                 (select name
                    from library.volunteers);
        ```

    3. ```sql
        proc sql;
           select name
              from library.volunteers
              where name, checkedout in
                 (select name, checkedout
                    from library.circulation);
        ```

    4. ```sql
        proc sql;
           select name, checkedout
              from library.circulation
              where name in
                 (select name
                    from library.volunteers;);
        ```

6. 根据定义，非相关子查询（noncorrelated subquery）是一种嵌套查询：

    1. 向外部查询返回单个值。
    2. 包含至少一个聚合函数。
    3. 独立于外部查询执行。
    4. 只需要外部查询向其传递单个值。

7. 关于以下 `PROC SQL` 查询，哪个陈述是错误的？

    ```sql
    proc sql;
       validate
       select name label='Country', 
              rate label='Literacy Rate'
          from world.literacy
          where 'Asia' =
             (select continent
                from world.continents
                where literacy.name = 
                      continents.country)
          order by 2;
    ```

    1. 查询语法无效。
    2. 在子查询向外部查询返回值之前，外部查询必须向子查询传递值。
    3. `PROC SQL` 无法执行此查询。
    4. 提交查询后，SAS 日志显示查询有效。

8. 考虑以下 `PROC SQL` 查询：

    ```sql
    proc sql;
       select lastname, firstname, 
              total, since
          from charity.donors
          where not exists
             (select lastname
                from charity.current
                where donors.lastname = 
                      current.lastname);
    ```

    查询引用了两个表：

    * `Charity.Donors` 列出成立以来捐赠者的姓名和联系信息。该表还包含两列：`Total` 显示每位捐赠者的总额，`Since` 首次捐赠年份。
    * `Charity.Current` 列出今年捐款的捐赠者姓名以及今年的捐款金额（`YearTotal`）。

    假设两个表中的 `LastName` 值都是唯一的。此查询的输出显示了

    1. 所有包含缺失值的捐赠者。
    2. 今年捐款的捐赠者。
    3. 今年没有捐款的捐赠者。
    4. `Charity.Current` 中今年的捐款尚未添加到 `Charity.Donors` 的 `Total` 列中。

9. 关于数据合并（data remerging），哪个陈述是正确的？

    1. 当 `PROC SQL` 合并数据时，它合并来自两个表的数据。
    2. 通过使用数据合并，`PROC SQL` 可以避免对数据进行两次扫描。
    3. 当 `PROC SQL` 合并数据时，它会在 SAS 日志中显示相关消息。
    4. 只有使用子查询时，`PROC SQL` 才会尝试合并数据。

10. 公共图书馆有几类书籍。图书馆中的每本书都只分配到一个类别。`Library.Inventory` 表为图书馆中的每本书包含一行。`Checkouts` 列指示每本书被借出的次数。你想显示平均循环次数（借阅次数）小于 2500 的类别。以下 `PROC SQL` 查询生成的你想要的结果吗？

    ```sql
    proc sql;
    title 'Categories with Average Circulation';
    title2 'Less Than 2500';
       select category,
              avg(checkouts) as AvgCheckouts
          from library.inventory
          having avg(checkouts) < 2500
          order by 1;
    ```

    1. 不。此查询无法运行，因为 HAVING 子句不能包含聚合函数。





2. 不。此查询无法运行，因为 `HAVING` 子句必须在汇总函数之前包含 `CALCULATED` 关键字。

3. 不。因为没有 `GROUP BY` 子句，`HAVING` 子句会将整个表视为一组。

4. 是。

# 第 3 章：使用 PROC SQL 水平合并表

## 概述

## 引言
当你需要从多个表中选择数据并将这些表进行水平合并（并列）时，`PROC SQL` 可以作为其他 SAS 过程或 `DATA` 步的高效替代方案。你可以使用 `PROC SQL` 连接（join）来水平合并表：

```
proc sql;
   select *
      from a, b
      where a.x=b.x;
```

![表 A，表 B](img/m71-1g1.png)

`PROC SQL` 连接是一种指定要合并的多个表和/或视图的查询，并且通常指定了匹配行并将其返回到结果集的条件。你应该已经熟悉了使用 `PROC SQL` 连接表的基础知识。在本章中，你将更深入地研究连接表。

### 理解连接
连接通过组合行来水平（并列）地合并表。被连接的表并不要求具有相同的行数或列数。注意：你也可以使用连接来合并视图以及表。以下大多数对表的引用也适用于视图；任何特殊情况均已说明。内联视图将在本章稍后部分介绍。有关 `PROC SQL` 视图的更多信息，请参阅使用 PROC SQL 创建和管理视图。当你使用 `PROC SQL` 查询连接表时，你必须决定你希望如何组合来自不同表的行。连接主要有两种类型，如下文所示。

| 连接类型 | 输出 |
| --- | --- |
| 内连接 (Inner join)![韦图，内连接](img/m71-2-g1.png) | 仅包含跨所有表（或多个表）匹配的行 |
| 外连接 (Outer join)![韦图，外连接](img/m71-2-g2.png) | 跨表匹配的行（如内连接所示）加上来自一个或多个表的不匹配行 |

当处理任何类型的类型的连接时，`PROC SQL` 首先生成笛卡尔积（Cartesian product），它包含所有表中行所有可能的组合。考虑一下笛卡尔积是如何生成的。

### 生成笛卡尔积
最基本的连接类型是合并 `SELECT` 语句 `FROM` 子句中指定的两个表的数据。当你在 `FROM` 子句中指定多个表但不包含用于划分子集的 `WHERE` 语句时，`PROC SQL` 会返回表的笛卡尔积。在笛卡尔积中，第一表中的每一行都与第二个表中的每一行组合。以下是这种类型查询的示例，它连接了 `One` 和 `Two` 表。

```
proc sql;
   select *
      from one, two;
```

![表 One 和 Two 的笛卡尔积](img/m71-3a1.png)

上面的输出显示了 `One` 表中每行与 `Two` 表所有行的所有可能组合。注意，每个表都有一个名为 `X` 的列，这两个列都出现在输出中。笛卡尔积包含了源表的所有列。具有相同名称列不会重叠。在大多数情况下，生成多个表行的所有可能组合并不会产生有用的结果，因此笛卡尔积很少是你想要的查询结果。例如，在包含员工信息的两个表的笛卡尔积中，输出的每行可能包含两个不同员工的信息。通常，你希望连接只返回表中的行子集。笛卡尔积的大小也可能是一个问题。笛卡尔积的行数等于参与表行数的乘积。在前一个示例中使用的 `One` 和 `Two` 表各包含三行，如下所示![表 One 和表 Two](img/m71-4g1.png)。`One` 和 `Two` 笛卡尔积的行数计算方式如下：

```
3 x 3 = 9
```

连接如 `One` 和 `Two` 这样的小表会产生较小的笛卡尔积。然而，连接大表的结果可能是巨大的，并需要大量的系统资源。例如，连接两个各有 1000 行的表将导致输出为：

```
1000 x 1000 = 1,000,000
```

当你运行无法优化的查询时，`PROC SQL` 会将以下警告信息写入 SAS 日志。

表 3.1 SAS 日志
| `注意：此查询的执行涉及一个或多个无法优化的笛卡尔积连接.` |

尽管你通常不会主动选择创建笛卡尔积，但理解它是如何构建的。。在所有类型的连接中，`PROC SQL` 都会生成笛卡尔积，然后消除不符合任何子集标准的行。

### 使用内连接

### 介绍连接语法
内连接根据 `WHERE` 子句中指定的匹配标准（也称为连接条件），合并并仅显示来自第一个表的与第二个表的行匹配的行。连接条件是指定要连接表的列的表达式。以下图说明了两个表的内连接。重叠的阴影区域表示内连接作为输出返回的匹配行（行子集）![韦图，表 1 和表 2 的内连接](img/m71-6g1.png 注意：内连接有时被称为常规连接。内连接语法建立在之前所示的最简单连接类型的语法之上。在内连接中，添加 `WHERE` 子句来限制显示在输出中的笛卡尔积行。

| 通用形式，内连接的 SELECT 语句：`SELECT column-1<,...column-n>FROM table-1 | view-1, table-2 | view-2<,...table-n | view-n>WHERE join-condition(s)<AND other subsetting condition(s)><other clauses>;`
此处语法的解释：
- `join-condition(s)` 指指定要连接表的列或列的一个或多个表达式。
- `other subsetting condition(s)` 指用于划分查询结果行的可选表达式。
- `<other clauses>` 指可选的 `PROC SQL` 子句。 |





当在前面所示 `PROC SQL` 查询中添加 `WHERE` 子句时，只有部分行会被包含在输出中。修改后的查询、表和输出如文所示：

| |
```
proc sql;
   select *
      from one, two
      where one.x = two.x;
```
| ![使用 Where 子句进行内连接](img/m71-6-g1.png) |

由于 `WHERE` 子句的存在，此内连接不会显示来自笛卡尔积（两个表中行的所有可能的组合）的所有行，而只显示行的一个子集。`WHERE` 子句表达式（连接条件）指定结果集应仅包含 `One` 表中列 `X` 的值等于 `Two` 表列 `X` 值的行。只有 `One` 表中的一行和 `Two` 表中的一行具有匹配的 `X` 值。这两行被合并为输出中的某一行。注意：除非连接条件中比较的列（在本例中为 `One.X` 和 `Two.X`）具有相同的数据类型，否则 `PROC SQL` 不会执行连接。然而，这两个列不需要具有相同的名称。例如，如果 `ID` 和 `EmpID` 具有相同的数据类型，则后续 `WHERE` 语句所示的连接是有效的：

```
where table1.id = table2.empid
```

注意：`WHERE` 子句中指定的连接条件通常包含等号 (`=`) 运算符，但表达式可能包含一个或多个其他运算符。基于等号 (`=`) 运算符匹配行的内连接（即一个表中的列或表达式的值必须等于另一个表的列或表达式的值）被称为**等值连接 (equijoin)**。考虑 `PROC SQL` 如何处理此内连接。

## 理解连接是如何处理的

理解 `PROC SQL` 如何处理内连接和外连接，有助于你理解每种连接生成的哪种输出。从概念上讲，`PROC SQL` 遵循以下步骤处理连接：

* 构建指定表的行笛卡尔积
* 根据 `WHERE` 子句中指定的连接条件（以及任何其他子集条件）评估笛卡尔积中的每行，并移除任何不符合指定条件的行
* 如果指定了摘要函数，则对适用行进行汇总
* 返回要在输出中显示的行。

注意：`PROC SQL` 查询优化器遵循比此处描述的概念方法更复杂的过程，通过将笛卡尔积拆分为更小的部分。对于每个查询，优化器根据特定情况选择最有效的处理方法。默认情况下，`PROC SQL` 连接不会重叠同名的列。相反，输出会显示所有具有相同名的列。为了避免在内连接或外连接的输出中出现同名列，你可以消除或重命名重复列。提示：你也可以在内连接或外连接中使用 `COALESCE` 函数来重叠同名的列。本章稍后将与外连接一起讨论 `COALESCE` 函数。

## 消除重复列

考虑使用内连接组合 `One` 和 `Two` 表的示例 `PROC SQL` 查询：

| |
```
proc sql;
    select *
       from one, two
       where one.x = two.x;
```
| ![内连接，表 One 和 Two](img/m71-8-g1.png) |

这两个表都有一个名称相同的列（`X`）。由于上述所示查询中的 `SELECT` 子句包含星号 (`*`)，输出显示了两个表的所有列。要消除重复列，你可以在 `SELECT` 语句中仅指定重复列中的一个。前面的 `PROC SQL` 查询中的 `SELECT` 语句可以修改如下：

```
proc sql;
   select one.x, a, b
      from one, two
      where one.x = two.x
```

在这里，`SELECT` 子句指定仅将 `One` 表中的列 `X` 包含在输出中。只显示一个 `X` 列的输出如下所示![表 One 输出](img/m71-8-g2.png)注意：在内等值连接中（如此处所示），在 `SELECT` 语句中列出哪个同名列并不重要。示例中的 `SELECT` 语句可以指定 `Two.X` 而不是 `One.X`。在上述示例中消除重复 `X` 列的另一种方法如下所示：

```
proc sql;
   select one.*, b
      from one, two
      where one.x = two.x;
```

通过使用星号 (`*`) 选择来自 `One` 表的所有列，并仅从 `Two` 表选择 `B`，此查询生成的与之前的版本相同的输出。

## 使用列别名重命名列

如果你正在处理多个具有相同名称列但数据略有不同的表，你可能希望两个列都出现在输出中。为了避免显示两个同名不同列的混淆，你可以通过在 `SELECT` 语句中指定列别名来重命名重复列之一。例如，你可以如下修改示例查询的 `SELECT` 语句：

```
proc sql;
   select one.x as ID, two.x, a, b
      from one, two
      where one.x = two.x;
```

修改后查询的输出在此处![修改后的查询输出](img/71-8-g3.png)现在 `One.X` 已重命名为 `ID`，输出清晰地指示了两个列。

## 连接具有匹配值的表

考虑当你连接两个在列上具有重复值的表时会发生什么。`Three` 和 `Four` 在 `X` 列上具有多个匹配值。后续 `PROC SQL` 内连接匹配行：

| |
```
proc sql;
    select *
       from three, four
       where three.x=four.x;
```
| ![表和 Four](img/9-g1.png) |

输出显示了此内连接如何处理重复值![PROC SQL 输出](img/9-g2.png)没有其他值的匹配，因此不显示其他行。注意：DATA 步合并只会输出两行，因为它从上到下处理数据。本章稍后将比较 `PROC SQL` 连接和 DATA 步合并。

## 指定表别名

为了让 `PROC SQL` 区分不同表中的同名列，你使用限定列名。要创建限定列名，可以在列名前面加上表名。例如，下面的 PROC SQL 内连接包含多个限定列名：

```
proc sql;
title 'Employee Names and Job Codes';
   select staffmaster.empid, lastname, firstname, jobcode
      from sasuser.staffmaster, sasuser.payrollmaster
      where staffmaster.empid=payrollmaster.empid;
```

包含长限定列名的 `PROC SQL` 代码可能难以阅读。此外，输入长表名可能非常耗时。幸运的是，你可以在任何 `PROC SQL` 查询的任何或所有表使用临时替代名称。此临时名称称为表别名，指定在 `FROM` 子句的表名之后。通常使用 `AS` 关键字，尽管其是可选的。修改后的 PROC SQL 查询在 `FROM` 子句中指定了表别名，然后在 `SELECT` 和 `WHERE` 子句中使用表别名来限定列名：

```
proc sql;
title 'Employee Names and Job Codes';
   select s.empid, lastname, firstname, jobcode
      from sasuser.staffmaster as s, 
           sasuser.payrollmaster as p
      where s.empid=p.empid;
```

在此查询中，可选的 `AS` 关键字用于定义 `FROM` 子句中的表别名。如果省略 `AS`，`FROM` 子句同样有效，如下所示：

```
from sasuser.staffmaster s,
     sasuser.payrollmaster p
```





注意：虽然使用表别名可以帮助你更高效工作，但使用表别名不会导致 SAS 执行查询更快。表别名通常是可选的。然而，在以下两种情况下需要使用它们，如下所示。

| 需要使用表别名的情况... | 示例 |
| --- | --- |
| 表与其自身连接（称为自连接或反射连接）时 | ```sql
from airline.staffmaster as s1,
  	  airline.staffmaster as s2
``` |
| 你需要引用不同库中同名表的列时 | ```sql
from airline.flightdelays as af,
       work.flightdelays as wf
 where af.delay > wf.delay
``` |

到为止，你已经看到了内连接的相对简单的示例。然而，与任何其他 `PROC SQL` 查询一样，内连接也可以包含更高级的组件，例如：

* 标题（titles）和页脚（footers）
* `SELECT` 子句中的函数和表达式
* `WHERE` 子句中的多个条件
* 用于用于排序的 `ORDER BY` 子句
* 带有分组的汇总函数。

这里是一些更复杂的内连接的示例。

## 示例：复杂的 PROC SQL 内连接

假设你想显示居住在纽约的所有公司员工的姓名（首字母和姓氏）、职位代码（job codes）和年龄。你还希望结果按职位代码和年龄进行排序。你需要的数据存储在下面列出的两个表中。

| 表 | 相关列 |
| --- | --- |
| Sasuser.Staffmaster | EmpID, LastName, FirstName, State |
| Sasuser.Payrollmaster | EmpID, JobCode, DateOfBirth |

在你想要显示的三个列中，`JobCode` 是表中已存在的唯一列。另外两个列需要从现有列中创建。这里显示的 `PROC SQL` 查询使用内连接来生成你需要的输出：

```sql
 proc sql outobs=15;
 title 'New York Employees';
    select substr(firstname,1,1) || '. ' || lastname 
           as Name,
           jobcode,
           int((today() - dateofbirth)/365.25)
           as Age
       from sasuser.payrollmaster as p,
            sasuser.staffmaster as s
       where p.empid =
             s.empid
             and state='NY'
       order by 2, 3;
```

![New York Employees](img/m71-13-g1.png)下方显示的 `SELECT` 子句指定了新列 `Name`、现有列 `JobCode` 和新列 `Age`：

```sql
select substr(firstname,1,1) || '. ' || lastname 
       as Name,
       jobcode,
       int((today() - dateofbirth)/365.25)
       as Age
```

为了创建这两个新列，`SELECT` 子句使用了如下函数和表达式：

* 为了创建 `Name`，使用 `SUBSTR` 函数从 `FirstName` 中提取首字母。然后，使用连接运算符将首字母与点、空格，以及 `LastName` 列的内容结合起来。最后，使用关键字 `AS` 为该新列命名。
* 为了计算 `Age`，使用 `INT` 函数返回计算结果的整数部分。在作为 `INT` 函数参数的表达式中，用今天的日期（由 `TODAY` 函数返回）减去员工的出生日期（`DateOfBirth`），并将差除以一年的天数（`365.25`）。

`WHERE` 子句包含两个由逻辑运算符 `AND` 链接的表达式：

```sql
where p.empid =
      s.empid
      and state='NY'
```

此查询仅输出 `EmpID` 匹配且 `State` 值为 `NY` 的行。你不需要用表名修缀列名 `State`，因为 `State` 只出现在其中一个表中。

## 示例：带有汇总函数的 PROC SQL 内连接

你还可以在 `PROC SQL` 连接中对数据进行汇总和分组。为了说明这一点，修改之前的 `PROC SQL` 内连接，使输出显示每个职位代码下纽约员工的以下汇总列：员工人数和平均年龄。修改后的查询所示：

```sql
proc sql outobs=15;
title 'Avg Age of New York Employees';
   select jobcode,
          count(p.empid) as Employees,
          avg(int((today() - dateofbirth)/365.25))
          format=4.1 as AvgAge
      from sasuser.payrollmaster as p,
           sasuser.staffmaster as s
      where p.empid =
            s.empid
            and state='NY'
      group by jobcode
      order by jobcode;
```

为了创建两个新列，`SELECT` 子句使用了如下汇总函数：

* 为了创建 `Employees`，使用 `COUNT` 函数并将 `p.EmpID`（`Payrollmaster.EmpID`）作为其参数。
* 为了创建 `AvgAge`，使用 `AVG` 函数并将表达式作为参数。如前面的示例所示，该表达式使用 `INT` 函数计算每个员工的年龄。

此修改后查询的输出所示。![Average Age of New York Employees](img/m71-14-g1.png)。

### 使用外连接

## 外外连接类型

外连接合并并显示跨表的所有匹配行，基于指定的匹配标准（也称为连接条件），以及部分或所有不匹配的行。你可以认为外连接是内连接的扩展：外连接返回内连接生成的行，加上额外的不匹配行。

| 外连接类型 | 输出 |
| --- | --- |
| 左外连接 | 所有匹配行加上来自 FROM 子句指定的第一个表（左表）的不匹配行![Left Join](img/m71-16g1.png) |
| 右外连接 | 所有匹配行加上来自 FROM 子句指定的第二个表（右表）的不匹配行![Right Join](img/m71-16g2.png) |
| 全外连接 | 所有匹配行加上两边的不匹配行![Full Join](img/m71-16g3.png) |

外连接的语法所示。

| 外连接的通用形式 SELECT 语句： |
| --- |
| `SELECT column-1,...column-n> FROM table-1 view-1 LEFT JOIN | RIGHT JOIN | FULL JOIN table-2 view-2 ON join-condition(s)<other clauses>`;LEFT JOIN`, `RIGHT JOIN`, `FULL JOIN` 是指定外连接类型的关键字。`ON` 指定连接条件，即用于连接表的列或列的表达式。<other clauses>`指的是可选的 PROC SQL 子句。 |

注意：为了进一步过滤查询输出中的行，你可以在 `ON` 子句后跟随一个 `WHERE` 子句。`WHERE` 子句在执行外连接之前对详细行进行过滤。然后 `ON` 子句指定如何选择剩余的行。注意：你每次只能对两个表或视图执行外连接。视图将在本章稍后介绍。考虑每种外连接的工作方式。

## 使用左外连接

左外连接根据指定的匹配标准（连接条件）检索跨表的所有匹配行，加上左表（FROM 子句中指定的第一个表）的不匹配行。假设你正在使用以下 `PROC SQL` 左连接来合并表 One 和 Two。连接条件位于 `ON` 关键字后的表达式中。这两个表和三行输出如下所示：

```sql
proc sql;
    select *
       from one
        left join
        two
       on one.x=two.x;
```

![Left Outer Join Output](img/m71-17-g1.png)




在输出的每一行中，前两列对应于 `table One`（左表），后两列对应于 `table Two`（右表）。因为这是一个左连接，`table One`（左表）的所有行（包括匹配和不匹配的行）都包含在输出中（前两列）。只有当 `table Two`（右表）的行与 `table One` 的某行相匹配时，它们才会显示在输出中（后两列）。

在此示例中，根据 `ON` 子句中指定的匹配准则（连接条件），输出的第二行是唯一的一行 `table One` 的行与 `table Two` 的某行相匹配的行。在输出的第一行和第三行中，`table One` 的某行在 `table Two` 中没有匹配的行。

注意：在所有类型的外连接（左连接、右连接和全连接）中，结果行（合并后的行）中来自未匹配行的列都将被设置为缺失值。

为了消除任何外连接中的其中一个重复列（在本例中为 `X`），正如前面的内连接所示，你可以修改 `SELECT` 子句来列出要显示的特定列。在这里，前面的查询的 `SELECT` 子句已被修改以删除重复的 `X` 列：

```sql
proc sql;
    select one.x, a, b
       from one
       left join
       two
       on one.x=two.x;
```

| ![左连接输出，已删除重复列](img/m71-17-g2.png) |

## 使用右外连接

右外连接根据指定的匹配准则（连接条件）检索跨表中匹配的所有行，加上来自右表（`FROM` 子句中指定的第二个表）的不匹配行。考虑一下当使用右连接合并上一个示例中使用的两个表会发生什么。以下 `PROC SQL` 查询使用右连接根据 `ON` 子句中指定的连接条件合并 `One` 和 `Two` 的行：

```sql
proc sql;
    select *
       from one
       right join
       two
       on one.x=two.x;
```

| ![右连接输出](img/m71-18-g1.png) |

在输出的每一行中，前两列对应于 `table One`（左表），后两列对应于 `table Two`（右表）。因为这是一个右连接，`table Two`（右表）的所有行（包括匹配和不匹配的行）都包含在输出中（后两列）。只有当 `table One`（左表）的行与 `table Two` 的某行相匹配时，它们才会显示在输出中（前两列）。

在此示例中，`table One` 中只有一行与 `table Two` 中的 `X` 值相匹配，这两行匹配行组合形成输出的第一行。在输出的其余行中，没有匹配项，且对应于 `table One` 的列被设置为缺失值。

## 使用全外连接

全外连接从两个表中同时检索匹配的行和不匹配的行。再次合并相同的两个表，这次使用全连接。下文显示 `PROC SQL` 查询、表和输出：

```sql
proc sql;
   select *
      from one 
      full join
      two
      on one.x=two.x;
```

| ![全外连接输出](img/m71-19-g1.png) |

因为这是一个全连接，两个表的所有行（包括匹配和不匹配的行）都包含在输出中。`table One` 和 `table Two` 之间只有一个匹配项，因此只有一行输出在所有列中显示值。输出的所有其余行仅包含来自 `table One` 或 `table Two` 的值。其余列被设置为缺失值。

## 示例：外连接

现在你已经了解了三种外连接的工作原理，请考虑一个需要使用外连接的实际情况。假设你想列出某航空公司在 3 月份的所有航班，以及相应的延迟信息（如果存在）。每班航班都通过航班日期和航班号识别。你的输出应该显示以下数据：航班日期、航班号、目的地以及延迟时长（分钟）。

你需要的数据存储在所示的两个表中。已标识出每个表的适用列。

| 表 | 相关列 |
| --- | --- |
| Sasuser.Marchflights | `Date, FlightNumber, Destination` |
| Sasuser.Flightdelays | `Date, FlightNumber, Destination, Delay` |

你的输出应该包含上述列出的列以及所有以下行：

*   跨两个表的 `Date` 和 `FlightNumber` 具有匹配值的行。
*   `Sasuser.Marchflights` 中在 `Sasuser.Flightdelays` 中没有匹配行的行。

为了生成你想要的输出，以下 `PROC SQL` 查询使用了左外连接。`Sasuser.Marchflights` 被指定为左（第一个）表。

```sql
proc sql outobs=20;
title 'All March Flights';
   select m.date,
          m.flightnumber 
	             label='Flight Number',
          m.destination
          label='Left',
          f.destination
          label='Right',
          delay
          label='Delay in Minutes'
      from sasuser.marchflights as m 
           left join
           sasuser.flightdelays as f
      on m.date=f.date
         and m.flightnumber=
             f.flightnumber
      order by delay;
```

注意以下几点：

*   `SELECT` 子句通过指定来源为 `Sasuser.Marchflights` 消除了重复的 `Date` 和 `FlightNumber` 列。然而，`SELECT` 子句列出了两个表的 `Destination` 列并为每个列分配了表别名。
*   `ON` 子句包含两个连接条件，根据两个列 `Date` 和 `FlightNumber` 匹配表。

查询输出所示 certpgadv/images/m71-21-g1.png。输出的前 12 行显示了 `Sasuser.Marchflights` 中在 `Sasuser.Flightdelays` 中没有匹配行的行。因此，在这 12 行中，最后 2 列被设置为缺失值。注意：可以使用右连接来生成相同的结果。`Sasuser.Marchflights` 被指定为右（第二个）表。





当 `BY` 变量的所有值都匹配时，你可以使用 `PROC SQL` 的内连接（inner join）来产生与 `DATA` 步合并（match-merge）相同的结果。假设你想合并 `One` 和 `Two` 两个表，如下所示![Tables One and Two](img/m71-24-g2.png)。这两个表共有列 `X`，且每个表中每行 `X` 的所有值在两个表中都是匹配的。两个表都已按照 `X` 排序。接下来的 `DATA` 步合并（随后跟跟一个 `PROC PRINT` 步）和 `PROC SQL` 内连接将产生完全相同的报告。

| DATA Step Match-Merge | PROC SQL Inner Join |
| --- | --- |
| | |

```
data merged;
    merge one two;
    by x; run;

  proc print data=merged noobs;
    title 'Table Merged';
 run;
```
 | |

```sql
proc sql;
 title 'Table Merged';
    select one.x, a, b
       from one, two
       where one.x = two.x
       order by x;
```
| |

![DATA step match-merge](img/m71-24-g1.png) 注意：`DATA` 步合并会创建一个数据集，而此处所示的 `PROC SQL` 内连接仅创建一个一个报告作为输出。为了让这两个程序完全相同，可以重写 `PROC SQL` 内连接以创建一个表。关于使用 `PROC SQL` 创建表的详细信息，请参阅使用 PROC SQL 创建和管理表。Note:Note。注意：如果输出中行的顺序不重要，则可以从 `PROC SQL` 连接中删除 `ORDER BY` 子句。没有了 `ORDER BY` 子句，该连接的效率更高，因为 `PROC SQL` 不需要对数据进行第二次扫描。

## 当只有部分值匹配时

当 `BY` 变量的只有部分值匹配时，你可以使用 `PROC SQL` 的全外连接（full outer join）来产生与 `DATA` 步合并相同的结果。然而，与 `DATA` 步合并不同，`PROC SQL` 外连接默认不会重叠两个公共列。要重叠公共列，你必须在 `PROC SQL` 全外连接中使用 `COALESCE` 函数。注意：`COALESCE` 函数也可以用于内连接操作符。考虑一下在没有 `COALESCE` 函数的情况下使用 `PROC SQL` 全外连接会发生什么。假设你想合并 `Three` 和 `Four` 两个表。这两个表共有列 `X`，但 `X` 的大部分值在表之间是不匹配的。两个表都已按照 `X` 排序。接下来的 `DATA` 步合并（随后跟跟一个 `PROC PRINT` 步）和 `PROC SQL` 外连接合并了这些表，但没有生成相同的输出。`COALESCE` 函数也可以用于内连接操作符。

| DATA Step Match-Merge | PROC SQL Full Outer Join |
| --- | --- |
| | |

```sas
data merged;
    merge three four;
    by x;
run;

proc print data=merged noobs;
    title 'Table Merged';
run;
```
 | |

```sql
proc sql;
title 'Table Merged';
    select three.x, a, b
       from three
       full join
       four
       on three.x = four.x
       order by x;
```
| |

![DATA step match-merge](img/m71-25-g1.png) `DATA` 步合并会自动重叠公共列 `X`。`PROC SQL` 外连接仅从一个表（表 `Three`）中选择 `X` 值，因此表 `Four` 中的 `X` 值不会包含在 `PROC SQL` 输出中。然而，`PROC SQL` 外连接默认无法重叠列。两个合并表中发生变化的值在上方已**加粗**。考虑一下 `COALESCE` 函数是如何在 `PROC SQL` 外连接中使用以重叠公共列的。

## 当只有部分值匹配时：使用 COALESCE 函数

当你将 `COALESCE` 函数添加到 `PROC SQL` 外连接的 `SELECT` 子句中时，`PROC SQL` 外连接就可以产生与 `DATA` 步合并相同的结果。

| 通用形式，在基础 `SELECT` 子句中使用 `COALESCE` 函数：`SELECT COALESCE (column-1<,...column-n>)` 这里是对该语法的解释：`column-1` 到 `column-n` 是两个或多个要重叠列的名称。`COALESCE` 函数要求所有参数具有相同的数据类型。 |

`COALESCE` 函数通过以下方式重叠指定的列：：
* 按照列列出的顺序检查每个列的值
* 返回第一个 SAS 非缺失值。

Note:Note。如果所有返回值都是缺失的，`COALESCE` 将返回一个缺失值。当将 `COALESCE` 函数添加到前面的 `PROC SQL` 全外连接中时，`DATA` 步合并（带有 `PROC PRINT` 步）和 `PROC SQL` 全外连接将以相同的方式合并行。这两个程序、表和输出如下所示。

| DATA Step Match-Merge | PROC SQL Full Outer Join |
| --- | --- |
| | |

```sas
data merged;
    merge three four;
    by x;
run;

proc print data=merged noobs;
    title 'Table Merged';
run;
```
 | |

```sql
proc sql;
title 'Table Merged';
    select coalesce(three.x, four.x)
       as X, a, b
       from three
       full join
       four
       on three.x = four.x;
```
|

### 使用内联视图

## 引入内联视图

有时，你可能希望指定内联视图而非表作为 `PROC SQL` 查询的数据。内联视图是指定在外部查询的 `FROM` 子句中的嵌套查询。（你应该已经熟悉子查询，它是指定在 `WHERE` 子句中的嵌套查询。）内联视图从一个或多个表中选择数据，以产生一个临时（或虚拟）表，外部查询随后使用该表。例如，下面的 `FROM` 子句指定了一个内联视图：

```sql
 from (select flightnumber, date,
              boarded/passengercapacity*100 
              as pctfull
              format=4.1 label='Percent Full'
         from sasuser.marchflights)
```

这个内联视图选择了两个现有列（`FlightNumber` 和 `Date`），并根据表 `Sasuser.Marchflights` 定义了新列 `PctFull`。与表不同，内联视图仅存在于查询执行期间。由于它是临时的，内联视图可以在定义它的查询中引用。此外，内联视图可以分配别名，但不能分配永久名称。Note:Note。在 `FROM` 子句中，你还可以指定 `PROC SQL` 视图，视图是已经创建（使用 `CREATE` 语句）并存储的查询。你可以在[使用 SQL 创建和管理视图](../../../../certpgadv/html/n12kcs025dxzdfn147whk5ylt668.htm）学习更多关于创建 `PROC SQL` 视图的信息。Note:Note。与其他查询不同，内联视图不能包含 `ORDER BY` 子句。





- 代码的复杂性通常会降低，因此代码更易编写和理解。
- 在某些情况下，`PROC SQL` 能够更高效地处理代码。

## 在其他视图或表中引用内联视图

前面的 `FROM` 子句来自一个简单的 `PROC SQL` 查询，该查询仅引用了一个数据源：内联视图。然而，`PROC SQL` 查询可以连接多个表和内联视图。例如，下所示的 `FROM` 子句同时指定了表 (`Sasuser.Flightschedule`) 和内联视图。

```
 from sasuser.flightschedule,
      (select flightnumber, date,
              boarded/passengercapacity*100 
              as pctfull
              format=4.1 label='Percent Full'
         from sasuser.marchflights)
```

## 在内联视图中引用多个表

你可以在内联视图的 `FROM` 子句中指定多个表，如下所示：

```
 from (select marchflights.flightnumber, 
               marchflights.date,
               boarded/passengercapacity*100 
               as pctfull
               format=4.1 label='Percent Full',
               delay
           from sasuser.marchflights, 
                sasuser.flightdelays
           where marchflights.flightnumber=
                 flightdelays.flightnumber
                 and marchflights.date=
                 flightdelays.date)
```

换句话说，你可以基于连接创建一个内联视图。注意：请记住，内联视图中引用的每个表都计入 256 个表的内连接限制。

## 为内联视图分配别名

你可以像为表一样为内联视图分配别名。在以下示例中，第一个 `FROM` 子句添加了别名 `f` 以引用表 `Sasuser.Flightschedule`，并将别名 `m` 与内联视图的结果关联。在主 `FROM` 子句之后，添加了一个同时使用这两个别名的 `WHERE` 子句。

```
from sasuser.flightschedule as f,
     (select flightnumber, date
             boarded/passengercapacity*100 
             as pctfull
             format=4.1 label='Percent Full'
         from sasuser.marchflights) as m
where m.flightnumber=f.flightnumber
      and m.date=f.date
```

## 示例：包含内联视图的查询

假设你想识别 3 月份误误最严重的航空旅行目的地。你希望输出显示以下所有数据：

- 目的地 (destination)
- 平均延迟
- 最大延迟
- 延迟概率。

你的 `PROC SQL` 查询使用内联视图来计算除最后一列以外的所有新列：

```
proc sql;
title "Flight Destinations and Delays";
   select destination, 
          average format=3.0 label='Average Delay',
          max format=3.0 label='Maximum Delay', 
          late/(late+early) as prob format=5.2
          label='Probability of Delay'
      from (select destination,
                   avg(delay) as average,
                   max(delay) as max,
                   sum(delay > 0) as late,
                   sum(delay <= 0) as early
                   from sasuser.flightdelays
                   group by destination)
      order by average;
```

考虑外部查询的每个子句，从 `FROM` 子句开始，因为 `PROC SQL` 在评估 `SELECT` 子句之前评估 `FROM` 子句。`FROM` 子句指定了一个内联视图而不是表。内联视图（嵌套查询）指定了 `Sasuser.Flightdelays` 表中或基于该表列的以下列：

- 现有列 `Destination`
- 新列 `Average`
- 新列 `Max`
- 新列 `Late`
- 新列 `Early`。

`Average`、`Max`、`Late` 和 `Early` 列都是通过摘要函数计算的。在 `Late` 和 `Early` 列的计算中，使用布尔表达式作为摘要函数的参数。布尔函数解析为 1（真）或 0（假）。例如，`Late` 是通过对布尔表达式 `delay > 0` 求 `sum` 来计算的。对于每一个大于 0 的 `Delay` 值，布尔表达式解析为 1；等于或小于 0 的值解析为 0。`SUM` 函数相加所有 `Delay` 的值，以指示每个目的地发生的延迟次数。内联视图以 `group by destination` 子句结束，指定内联视图数据应根据 `Destination` 的值进行分组和汇总。如果你提交此内联视图（嵌套查询）作为单独查询，它将生成以下输出。![in-line view (nested query)](img/m71-31-g1.png) 考虑外部查询的 `SELECT` 和 `ORDER BY` 子句：

```
proc sql;
title "Flight Destinations and Delays";
   select destination,
          average format=3.0 label='Average Delay',
          max format=3.0 label='Maximum Delay',
          late/(late+early) as prob format=5.2
          label='Probability of Delay'
      from (select destination,
                   avg(delay) as average,
                   max(delay) as max,
                   sum(delay > 0) as late,
                   sum(delay <= 0) as early
                   from sasuser.flightdelays
                   group by destination)
      order by average;
```





| --- | --- |

| Data | `Sasuser.Flightschedule (EmpID, Date, Destination)` `Sasuser.Staffmaster (EmpID, FirstName, LastName, State)` `Sasuser.Payrollmaster (EmpID, JobCode)` `Sasuser.Supervisors (EmpID, State, JobCategory)` |

注意：主管与他们监管的员工住在同一个州。每个州每个职业类别对应一名主管。完成上述任务需要一个复杂的查询，其中包含多个子查询、连接和内联视图。为了使任务更易于管理，请分四步逐步构建此复杂查询：

1. 确定飞往哥本哈根航班的工作人员。
2. 找到第一个查询返回的机组成员州和职业类别。
3. 根据第二个查询返回的州和职业类别，找到人员主管的员工编号。
4. 根据第三个查询返回的员工编号，找到主管的名字。

注意，在四个步骤中的每一步，都会添加最终查询的一个部分。最终查询包含了这四个独立的部分。

### 查询 1：确定飞往哥本哈根 (CPH) 航班的工作人员

此查询列出了哥本哈根航班上所有六名机组成员的员工 ID：

```
proc sql;
   select empid
      from sasuser.flightschedule
      where date='04mar2000'd
            and destination='CPH';
```

![哥本哈根航班的员工 ID](img/m71-34-g1.png) |

### 查询 2：找到机组成员的州和职业类别

查询 1 变成子查询，并将六名哥本哈根机组成员的员工 ID 返回给外部查询查询 2。（查询 2 为阴影部分）。查询 2 使用内连接合并两个表。查询 2 为六名机组成员选择了职业类别（通过使用 `SUBSTR` 函数从 `JobCode` 中提取职业类别）和州。

```
proc sql;
   select substr(JobCode,1,2) as JobCategory,
          state 
      from sasuser.staffmaster as s,
           sasuser.payrollmaster as p
      where s.empid=p.empid and s.empid in
         (select empid
            from sasuser.flightschedule
            where date='04mar2000'd
                  and destination='CPH');
```

![哥本哈根机组成员的职业类别和州](img/m71-34-g2.png) |

### 查询 3：找到人员主管的员工编号

查询 2 成为查询 3 中的内联视图，并为内联视图分配了别名 `c`。查询 2 向查询 3 返回每个机组成员的职业类别和州。查询 3 选择职业类别和州与机组成员匹配的主管的员工 ID。注意：`Sasuser.Supervisors` 为 `EmpID` 列指定了标签 Supervisor ID，该标签会显示在输出中。

```
proc sql;
   select empid
      from sasuser.supervisors as m,
         (select substr(jobcode,1,2) as JobCategory,
                 state
            from sasuser.staffmaster as s,
                 sasuser.payrollmaster as p
            where s.empid=p.empid and s.empid in
               (select empid
                  from sasuser.flightschedule
                  where date='04mar2000'd
                        and destination='CPH')) as c
      where m.jobcategory=c.jobcategory
            and m.state=c.state;
```

![主管 ID、与机组成员匹配的职业类别和州](img/m71-34-g3.png) |

注意两行包含相同的 `EmpID` 值：`1983`。这种重复两个两个机组成员有同一个经理。总而言，哥本哈根航班的六名机组成员共有五位主管。

### 查询 4：找到主管的名字

查询 3 成为查询 4 中的子查询。查询 3 向查询 4 返回哥本哈根机组成员主管的员工编号（主管 ID）。查询 4 选择主管的名字。

```
proc sql;
  select firstname, lastname
    from sasuser.staffmaster 
    where empid in
      (select empid
        from sasuser.supervisors as m,
          (select substr(jobcode,1,2) 
                  as JobCategory, 
                  state
             from sasuser.staffmaster as s,
                  sasuser.payrollmaster as p
             where s.empid=p.empid
                   and s.empid in
               (select empid
                 from sasuser.flightschedule
                 where date='04mar2000'd
                       and destination='CPH'))
                       as c
        where m.jobcategory=c.jobcategory
              and m.state=c.state);
```

![主管名字](img/m71-34-g4.png) |

注意输出有五行，每个主管对应一行。主管的重复名字已被消除。技术 1 产生了一个包含内容的 `PROC SQL` 查询：

- 四个 `SELECT` 语句
- 四个表，每个表单独读取。

## 示例：技术 2 (PROC SQL 多路连接)

| Task | 列出 3 月 4 日航班的主管。 |
| --- | --- |
| Data | `Sasuser.Flightschedule (EmpID, Date, Destination)` `Sasuser.Staffmaster (EmpID, FirstName, LastName, State)` `Sasuser.Payrollmaster (EmpID, JobCode)` `Sasuser.Supervisors (EmpID, State, JobCategory)` |

注意：主管与他们监管的员工住在同一个州。每个州每个职业类别对应一名主管。你也可以通过自连接的多路连接（将表与其连接）来解决此问题。代码所示：

```
proc sql;
   select distinct e.firstname, e.lastname
      from sasuser.flightschedule as a,
           sasuser.staffmaster as b,
           sasuser.payrollmaster as c,
           sasuser.supervisors as d,
           sasuser.staffmaster as e
      where a.date='04mar2000'd and
            a.destination='CPH' and
            a.empid=b.empid and
            a.empid=c.empid and
            d.jobcategory=substr(c.jobcode,1,2)
            and d.state=b.state
            and d.empid=e.empid;
```

![输出：自连接的多路连接](img/m71-35-g1.png)

技术 2 使用多路连接提供了比技术 1 更高效的解决方案。在多路连接中，`PROC SQL` 每次连接两个表并按最高效顺序执行连接（该顺序最小化了笛卡尔积）。这种多路连接代码比技术 1 的代码更难逐步构建。注意在此查询中 `Sasuser.Staffmaster` 被读取了两次：这就是自连接。如 `FROM` 子句所示，`Sasuser.Staffmaster` 每次读取时都分配了不同的表别名：首先是 `b`，然后是 `e`。第一次读取（名为 `b`）是为了查找哥本哈根机组成员的州，第二次读取（名为 `e`）是为了查找主管的名字。

## 示例：技术 3（传统的 SAS 编程）

| Task | 列出 3 月 4 日航班的主管名字。 |
| --- | --- |
| Data | `Sasuser.Flightschedule (EmpID, Date, Destination)` `Sasuser.Staffmaster (EmpID, FirstName, LastName, State)` `Sasuser.Payrollmaster (EmpID, JobCode)` `Sasuser.Supervisors (EmpID, State, JobCategory)` |

为了对比，请查看解决此问题的传统 SAS 编程。代码如下所示，其后是输出。





```sas
/* 查找航班的机组。 */

proc sort data=sasuser.flightschedule (drop=flightnumber)
          out=crew (keep=empid);
   where destination='CPH' and date='04MAR2000'd;
   by empid;
run;

/* 查找机组的州和职位代码。 */

proc sort data=sasuser.payrollmaster
               (keep=empid jobcode)
          out=payroll;
   by empid;
run;

proc sort data=sasuser.staffmaster
             (keep=empid state firstname lastname)
          out=staff;
   by empid;
run;

data st_cat (keep=state jobcategory);
   merge crew (in=c)
         staff
         payroll;
   by empid;
   if c;
   jobcategory=substr(jobcode,1,2);
run;

/* 查找主管 ID。 */

proc sort
     data=st_cat;
        by jobcategory state;
run;

proc sort data=sasuser.supervisors
          out=superv;
   by jobcategory state;
run;

data super (keep=empid);
   merge st_cat(in=s)
         superv;
   by jobcategory state;
   if s;
run;

/* 查找主管的名字。 */

proc sort data=super;
   by empid;
run;

data names(drop=empid);
   merge super (in=super)
         staff (keep=empid firstname lastname);
   by empid;
   if super;
run;

proc print data=names noobs uniform;
run;
```

![传统的 SAS 编程](img/m71-36-g1.png)此输出与 `PROC SQL` 方法（技术 1 和 2）的输出并不相同。SQL 查询消除了此处看到的重复名称。当你使用技术 3 时，可以通过在最后一个 `PROC SORT` 语句中添加 `NODUPKEY` 选项来消除重复项，如下所示：

```sas
proc sort data=super nodupkey;
```

基于大型机批模式下的基准测试，与此非 SQL 程序相比，SQL 查询使用的 CPU 时间较少，但 I/O 操作更多。

## 总结

## 文本总结

### 理解连接

`PROC SQL` 连接是一种通过组合行来水平（并排）组合表的查询。连接的两种主要类型是内连接（inner joins）和外连接（outer joins）。

### 生成笛卡尔积

当你在 `FROM` 子句中指定多个表但没有包含 `WHERE` 语句来划分数据集时，`PROC SQL` 会返回表的笛卡尔积。在笛卡尔积中，第一个表中的每行都与第二个表中的每行组合。在所有类型的连接中，`PROC SQL` 都会首先生成笛卡尔积，然后删除不符合你指定的任何子集条件的行。

### 使用内连接

内连接根据 `WHERE` 子句中指定的匹配标准（也称为连接条件），合并并显示来自第一个表的与第二个表的行相匹配的行。当连接的表包含具有相同名称的列时，你可能想要消除结果中的重复列，或指定列别名来重命名其中一个重复列。为了在内连接或任何 `PROC SQL` 步骤中引用表，你可以指定一个称为表别名的临时名称。

### 使用外连接

外连接根据指定的匹配标准（也称为连接条件），合并并显示跨表匹配的所有行，加上部分或全部不匹配的行。外连接有三种类型：

*   **左外连接**（left outer join）根据指定的匹配标准（连接条件）检索所有跨表匹配的行，加上来自左表（`FROM` 子句中指定的第一个表）的不匹配行。

*   **右外连接**（right outer join）根据指定的匹配标准（连接条件）检索所有跨表匹配的行，加上来自右表（`FROM` 子句中指定的第一个表*）的不匹配行。

*   **全外连接**（full outer join）从两个表中同时检索匹配和不匹配的行。

### 使用外连接风格语法创建内连接

如果你想对所有连接使用一致的语法，可以使用与外连接相同的语法风格编写内连接。

### 比较 SQL 连接和 DATA 步骤匹配合并

`DATA` 步骤匹配合并和 `PROC SQL` 连接可以产生相同的结果，尽管这两种技术之间存在重要的差异。

*   当 `BY` 变量（列）的所有值都匹配且没有重复的 `BY` 变量时，你可以使用 `PROC SQL` 内连接。

*   当只有部分 `BY` 变量的值匹配时，你可以使用 `PROC SQL` 全外连接。为了重叠公共列，你必须在 `PROC SQL` 连接中配合 `COALESCE` 函数。

### 使用内联视图

内联视图（in-line view）是出现在 `FROM` 子句中的子查询。内联视图从一个或多个表中选择数据生成临时（或虚拟）表，外部查询使用该表选择输出数据。你可以与其他视图或其他表引用内联视图，在内联视图中引用多个表，并为内联视图分配别名。

### 连接多个表和视图

当你执行组合两个以上表或视图的复杂查询时，你可能需要在几种技术之间进行选择。

## 示例程序

### 使用内连接合并表

```sas
proc sql outobs=15;
title '纽约员工';
   select substr(firstname,1) || ' ' || lastname 
          as Name,
          jobcode,
          int((today() - dateofbirth)/365.25) as Age
      from payrollmaster as p,
           staffmaster as s
      where p.empid=s.empid and state='NY'
      order by 2, 3;
quit;
```

### 使用左连接合并表

```sas
proc sql outobs=20;
title '所有航班';
   select m.date,
          m.flightnumber as='Flight Number',
          m.destination as='Left',
          f.destination as='Right',
          delay as='Delay in Minutes'
      from marchflights as m 
           left join 
           flightdelays as f
      on m.date=f.date and m.flightnumber=f.flightnumber
      order by delay;
quit;
```

### 在全连接中重叠公共列

```sas
 proc sql;
    select coalesce(p.empid, s.empid) 
           as ID, firstname, lastname, gender
       from payrollmaster as p 
               full join 
            staffmaster as s
       on p.empid = s.empid
       order by id;
quit;
```

### 使用子查询和内联视图连接表

```sas
 proc sql;
    select empid
       from supervisors as m,
          (select substr(jobcode,1,2) as JobCategory,
                  state
             from staffmaster as s,
                  payrollmaster as p
             where s.empid=p.empid and s.empid in
                (select empid
                   from flightschedule
                   where date='04mar2000'd
                         and destination='CPH')) as c
       where m.jobcategory=c.jobcategory
              and m.state=c.state;
quit;
```

## 注意事项

*   大多数情况下，多个表的所有组合不会产生有用结果，因此笛卡尔积很少是你想要的查询结果。

*   单个内连接的最大表数取决于你的 SAS 版本。如果连接涉及视图，的是视图底层表的数量，而不是视图的数量。外连接一次只能对两个表或视图进行。

# 练习

为每个问题选择最佳答案。完成测验后，使用附录中的答案对照检查你的答案。

1.  当在 `PROC SQL` 连接中未指定连接条件时，会返回笛卡尔积。

    1.  在 `PROC SQL` 连接中未指定连接条件。
    2.  在 `PROC SQL` 集合操作中未指定连接条件。
    3.  在 `PROC SQL` 连接中指定了两个以上的表。
    4.  在使用 `OUTER UNION` 运算符时使用了 `ALL` 关键字。

2.  根据给出的 PROC SQL 查询和表，生成了哪个输出？

    |  





```sql
proc sql;
   select *
      from store1, 
      store2
      where store1.wk=
            store2.wk;
```

| ![Store 1 和 Store 2 表](img/m71-39-g1.png) |

1. ![PROC SQL 查询输出,答案 A](img/m71-39-g2.png)
2. ![PROC SQL 查询输出,答案 B](img/m71-39-g3.png)
3. ![PROC SQL 查询输出,答案 C](img/m71-39-g4.png)
4. ![PROC SQL 查询输出,答案 D](img/m71-39-g5.png)

3. 给定如下所示 `PROC SQL` 查询和表，生成了哪个输出？

```sql
proc sql;
   select s.*, bonus
      from bonus as b 
      right join
      salary as s
      on b.id=
         s.id;
```

| ![Bonus 和 Salary 表](img/m71-39-g6.png) |

1. ![PROC SQL 查询输出,答案 A](img/m71-39-g7.png)
2. ![PROC SQL 查询输出,答案 B](img/m71-39-g8.png)
3. ![PROC SQL 查询输出,答案 C](img/m71-39-g9.png)
4. ![PROC SQL 查询输出,答案 D](img/m71-39-g10.png)

4. 哪个 `PROC SQL` 查询与此处显示的查询产生相同的输出？

```sql
proc sql;
   select a.*,
          duration
      from groupa as a,
           groupb as b
      where a.obs=b.obs;
```

注意：假设表 `Groupa` 包含列 `Obs` 和 `Med`。`Groupb` 包含列 `Obs` 和 `Duration`。

1. ```sql
proc sql;
   select a.obs label='Obs',
              med 
              b.obs label='Obs',
              duration
          from groupa as a, groupb as b
          where a.obs=b.obs;
```
2. ```sql
proc sql;
   select coalesce(a.obs, b.obs)
              label='Obs', med, duration
          from groupa as a
          full join 
          groupb as b
          on a.obs=b.obs;
```
3. ```sql
proc sql;
   select a.*, duration
      from groupa as a
      left join
          groupb as b
      where a.obs=b.obs;
```
4. ```sql
proc sql;
   select a.*, duration
      from groupa as a
          inner join
          groupb as b
          on a.obs=b.obs;
```

5. 下述 `PROC SQL` 查询生成了哪个输出？

```sql
proc sql;
   select *
      from table1 
      left join
      table2
             on table1.g3=
                table2.g3;
```

| ![Table 1 和 Table 2](img/m71-39-g11.png) |

1. ![PROC SQL 查询输出,答案 A](img/m71-39-g12.png)
2. ![PROC SQL 查询输出,答案 B](img/m71-39-g13.png)
3. ![PROC SQL 查询输出,答案 C](img/m71-39-g14.png)
4. ![PROC SQL 查询输出,答案 D](img/m71-39-g15.png)

6. 为了让 `PROC SQL` 执行内连接（inner join），

1. 被连接的表必须包含相同数量的列。
2. 表在连接之前必须进行排序。
3. `WHERE` 子句中连接条件指定的列必须具有相同的数据类型。
4. `WHERE` 子句中连接条件指定的列必须具有相同的列名。

7. 关于内联视图（in-line views）的哪个描述是错误的？

1. 一旦定义，内联视图可以在当前 SAS 会话中的任何 `PROC SQL` 查询中引用。
2. 内联视图可以分配表别名，但不能分配永久名称。
3. 内联视图可以在 `PROC SQL` 连接中与表结合。
4. 此 `PROC SQL` 查询包含一个使用有效语法的内联视图：

```sql
proc sql;
   select name, numvisits
      from (select name, sum(checkin) 
           as numvisits
              from facility as f, members as m
              where area='POOL' and
                    f.id=m.id
              group by name)
      where numvisits<=10
      order by name
```

8. 哪个 `PROC SQL` 查询与所示的 `DATA` 步骤产生相同的输出？

```sas
data merged;
   merge table1 table2;
   by g3;
run;
```

| ![Table1, Table2 和 Merged 表](img/m71-39-g17.png) |

1. ```sql
proc sql;
   select a.*, z
      from table1 as a
      left join
          table2 as b
      on a.g3=b.g3;
```
2. ```sql
proc sql;
   select a.*, z
      from table1 as a
      full join
          table2 as b
      on a.g3=b.g3;
```
3. ```sql
proc sql;
   select a.*, z
      from table1 as a
      inner join
          table2 as b
      on a.g3=b.g3;
```
4. ```sql
proc sql;
   select a.*, z
      from table1 as a
      right join
          table2 as b
      on a.g3=b.g3;
```

9. `PROC SQL` 内连接可以合并

1. 链的表。
2. 最多 256 个表或内联视图。
3. 最多 256 个表，包括任何表。
4. 2 列。

10. 关于使用表别名的哪个描述是错误的？

1. 当引用不同库中的相同名称时，必须使用表别名。
2. 表别名可以通过 `AS` 关键字进行引用。
3. 当引用在两个表中均相同的列名时，必须使用表别名（或完整的表名）。
4. 在使用聚合函数时必须使用表别名。





每个集合操作符以不同的方式合并查询结果。在本章中，你将学习如何使用各种集合操作符（带有或不带可选关键字 `ALL` 和 `CORR`（`CORRESPONDING`））来合并多个查询的结果。注意：在本章中，除非另有说明，对表的引用也适用于视图。

# 理解集合操作

## 概述

一个集合操作包含：
* 查询（每个都以 `SELECT` 子句开头）
* 一个集合操作符
* `ALL` 和 `CORR`（`CORRESPONDING`）关键字中的一个

使用集合操作符的 SQL 查询通用形式：`SELECT column-1<, ... column-n>FROM table-1 | view-1<, ... table-n | view-n><optional query clauses>set-operator <ALL> <CORR>SELECT column-1<, ... column-n>FROM table-1 | view-1<, ... table-n | view-n><optional query clauses>;`

以下是该语法的解释：
`SELECT` 指定将出现在结果中的列。
`FROM` 指定要查询的表或视图。
`optional query clauses` 用于进一步细化查询，包含 `WHERE`、`GROUP BY`、`HAVING` 和 `ORDER BY` 子句。
* `set-operator` 是以下内容之一：`EXCEPT` | `INTERSECT` | `UNION` | `OUTER UNION`。
* 可选关键字 `ALL` 和 `CORR`（`CORRESPONDING`）进一步修改集合操作。

查询或集合操作包含一个分号，放在最后一个 `SELECT` 语句之后。

## 示例

在下面的 PROC SQL 步骤中，`SELECT` 语句包含一个集合操作。该集合操作使用集合操作符 `UNION` 将对表 `Sasuser.Stress98` 的查询结果与对表 `Sasuser.Stress99` 的查询结果合并。

```
proc sql;
   select *
      from sasuser.stress98
   union
   select *
      from sasuser.stress99;
```

你将在本章后面的部分学习使用每个集合操作符的细节。

## 处理单个集合操作

PROC SQL 评估带有一个集合操作的 `SELECT` 语句如下：
1. 评估每个查询以产生中间（内部）结果表。
2. 每个中间结果表然后变成与集合操作符链接的操作数，形成一个表达式（例如，`Table1 UNION Table2`）。
3. PROC SQL 评估整个表达式以产生单个的输出结果集。

## 使用多个集合操作符

单个 `SELECT` 语句可以包含多个集合操作。每个额外的集合操作包含一个集合操作符和一组查询子句，如下所示：

```
proc sql;
   select *
      from table1
   set-operator
   select *
      from table2
   set-operator
   select *
      from table3;
```

此 `SELECT` 语句使用两个集合操作符将三个查询连接在一起。无论 `SELECT` 语句中有多少个集合操作，该语句只包含一个分号，放在最后一个查询之后。

## 示例

下面的 PROC SQL 步骤包含两个集合操作符（都是 `OUTER UNION`），它们合并了三个查询：

```
 proc sql; 
    select *
       from sasuser.mechanicslevel1
    outer union
    select *
       from sasuser.mechanicslevel2
    outer union
    select *
       from sasuser.mechanicslevel3;
```

## 处理多个集合操作

当 PROC SQL 评估包含多个集合操作 `SELECT` 语句时，需要一个额外的处理步骤（下述步骤 3）：
1. 评估每个查询以产生中间（内部）结果表。
2. 每个中间结果表然后变成与集合操作符链接的操作数，形成一个表达式（例如，`Table1 UNION Table2`）。
3. 如果集合操作包含两个以上的查询，则前两个查询的结果（在下面的示例中用括号括起来）将成为下一个集合操作符和操作的操作数。例如：
    * 使用两个集合操作符：`(Table1 UNION Table2) EXCEPT Table3`
    * 使用三个集合操作符：`((Table1 UNION Table2) EXCEPT Table3) INTERSECT Table4`。
4. PROC SQL 评估整个表达式以产生单个的输出结果集。

注意：在处理集合操作符时，PROC SQL 遵循默认的优先级，除非该顺序被表达式中的括号覆盖。默认情况下，`INTERSECT` 先被评估。`OUTER UNION`、`UNION` 和 `EXCEPT` 的优先级相同。

## 介绍集合操作符

四个集合操作符 `EXCEPT`、`INTERSECT`、`UNION` 和 `OUTER UNION` 各都以不同的方式选择行和处理列，如下所示。注意：在下表中，`Table 1` 是第一个查询引用的表，`Table 2` 是第二个查询引用的表。

| 集合操作符 | 行的处理 | 列的处理 | 示例 |
| --- | --- | --- | --- |
| `EXCEPT` | 从第一个表中选择在第二个表中未找到唯一行![Venn Diagram，EXCEPT 操作符](img/m72-4g1.png) | 根据列在 `SELECT` 子句中的位置进行重叠，而不考虑具体的列名。 | <br>```proc sql;
    select *
       from table1
    except
    select *
       from table2;
``` |
| `INTERSECT` | 选择两个表中共有的唯一行![Venn Diagram，INTERSECT 操作符](img/m72-4g2.png) | 根据列在 `SELECT` 子句中的位置进行重叠，而不考虑具体的列名。 | <br>```proc sql;
    select *
       from table1
    intersect
    select *
       from table2;
``` |
| `UNION` | 从两个表中选择唯一行![Venn Diagram，UNION 操作符](img/m72-4g3.png) | 根据列在 `SELECT` 子句中的位置进行重叠，而不考虑具体的列名。 | <br>```proc sql;
    select *
       from table1
    union
    select *
       from table2;
``` | |
| `OUTER UNION` | 选择两个表的所有行。`OUTER UNION` 操作符拼接查询结果![Venn Diagram，OUTER UNION 操作符](img/m72-4g4.png) | 不进行列重叠。 | <br>```proc sql;
    select *
       from table1
    outer union
    select *
       from table2;
``` |

注意：选择唯一行的集合操作符在输出中仅显示一次行。

## 处理唯一行与重复行

在处理仅显示唯一行的集合操作（包含集合操作符 `EXCEPT`、`INTERSECT` 或 `UNION` 的集合操作）时，PROC SQL 默认对数据进行两次扫描：
1. PROC SQL 消除表中的重复（非唯一）行。
2. PROC SQL 选择符合行并在需要时重叠列。

对于同时显示唯一行和重复行的集合操作，只需要对数据进行一次扫描（上述步骤 2）。

## 合并重叠列





您可以使用集合操作来合并列数和行数不同，或者列的顺序不同的表。四个集合操作符中的三个（`EXCEPT`、`INTERSECT` 和 `UNION`）通过叠加（overlaying）来合并列。（集合操作符 `OUTER UNION` 不会进行列重叠。）

默认情况下，集合操作符 `EXCEPT`、`INTERSECT` 和 `UNION` 根据列在 `SELECT` 子句中的相对位置进行列重叠。列名会被忽略。您可以通过在 `SELECT` 子句中按相应的顺序指定列，来控制 `PROC SQL` 如何将一个表中的列映射到另一个表的列。第一个查询的 `SELECT` 子句中指定的第一个列与第二个查询的 `SELECT` 子句中指定的第一个列重叠，依此类推。

当对列进行重叠时，`PROC SQL` 使用来自第一张表（第一个查询中引用的表）的列名。如果第一张表中没有列名，则使用第二张表中的列名。当 `SELECT` 子句中包含星号（`*`）而不是列名列表时，集合操作将根据列在表中的位置合并表（并且，如果适用，重叠列）。

例如，下面的集合操作使用了集合操作符 `EXCEPT`，因此列会被重叠。每个查询的 `SELECT` 子句都使用星号（`*`），因此列根据它们在表中的位置进行重叠。表 `One` 中的第一列（`X`）与表 `Two` 中的第一列（`X`）重叠，依此类推。

| ```
proc sql;
   select *
      from one
   except
   select *
      from two;
``` | ![Tables One, Two, and Combined, Overlaid Table](img/m72-5-g1.png) |

为了能够重叠，两个 `SELECT` 子句中相同相对位置的列必须具有相同的数据类型。如果类型不同，`PROC SQL` 会 SAS 日志中生成警告消息并停止执行。例如，在上述表中，如果列 `One.X` 的数据类型与列 `Two.X` 不同，SAS 日志将显示以下错误信息。

表 4.1 SAS Log

| ```
ERROR: Column 1 from the first contributor of EXCEPT 
is not the same type as its counterpart from the second.
``` | |

接下来，我们使用关键字 `ALL` 和 `CORR` 来修改集合操作符的默认行为。

# 使用关键字修改结果

要修改集合操作符的行为，您可以在集合操作符之后立即使用关键字 `ALL` 或 `CORR` 的其中一个或两者：

```
proc sql;
   select *
      from table1
   set-operator <all> <corr> 
   select *
      from table2;
```

下面描述了每个关键字的用法。

| 关键字 | 操作 | 适用场景... |
| --- | --- | --- |
| `ALL` | 对数据进行单次扫描且不删除重复行。 | 您不在乎是否有重复项。不存在重复项。`ALL` 不能与 `OUTER UNION` 一起使用。 |
| `CORR` (或 `CORRESPONDING`) | 按名而不是按位置比较并重叠列：* 与 `EXCEPT`、`INTERSECT` 和 `UNION` 使用时，移除两个表中名称不相同的任何列。* 与 `OUTER UNION` 使用时，重叠同名列并显示名称不匹配的列而不叠加。如果 `SELECT` 子句中的列分配了别名，`CORR` 将使用别名而不是永久列名。 | 两个表具有某些或所有公共列，但列的顺序不同。 |

在本章的剩余部分，您将学习更多关于每个集合操作符的使用，以及带有关键字 `ALL` 和 `CORR`。

# 使用 EXCEPT 集合操作符

## 概述

集合操作符 `EXCEPT` 同时执行以下操作：

* 从第一张表（第一个查询指定的表）中选择第二张表（第二个查询指定的表）中未找到的唯一行
* 重叠列。

![overlays columns](img/m72-4g1.png) 考虑 `EXCEPT` 在单独使用以及与关键字 `ALL` 和 `CORR` 使用时的工作原理。

## 单独使用 EXCEPT 操作符

假设您想显示表 `One` 中不在表 `Two` 中的唯一行。对应的包含 `EXCEPT` 操作符、表 `One` 和 `Two` 以及集合操作输出的 `PROC SQL` 集合操作所示：

| ```
proc sql;
   select *
      from one
   except
   select *
      from two;
``` | ![Tables One, Two, and Output](img/m72-9-g1.png) |

集合操作符 `EXCEPT` 按位置重叠列。在输出输出中，以下列被重叠了：

* 第一列，`One.X` 和 `Two.X`，两者均为数值型
* 第二列，`One.A` 和 `Two.B`，均为字符型。

使用了来自表 `One` 的列名，因此输出的第二列命名为 `A` 而不是 `B`。考虑 `PROC SQL` 如何从表 `One` 中选择行显示在输出中。在第一次扫描中，`PROC SQL` 消除了表中的任何重复行。如下所示，有一个重复行：在表 `One` 中。`PROC SQL` 从表 `One` 中选择行显示在输出中的过程如下：

```
proc sql;
   select *
      from one
   except
   select *
      from two;
``` ![Tables One and Two](img/m72-9-g2.png)

在第二次扫描中，`PROC SQL` 识别表 `One` 中在表 `Two` 中有匹配的行并消除它们。如下所示，有一个匹配行被消除：

```
proc sql;
   select *
      from one
   except
   select *
      from two;
``` ![Tables One and Two](img/m72-9-g3.png)

表 `One` 中剩余的所有行显示在输出中。![m72-g4.png## 在 EXCEPT 操作符使用关键字 ALL 要选择第一表中所有行（包括唯一和重复的）且在第二表中未出现的行，请在 `EXCEPT` 操作符之后添加关键字 `ALL`。修改后的 `PROC SQL` 集合操作、表 `One` 和 `Two` 以及输出所示：``` ```proc sql;   select *      from one   except all   select *      from two;``` | ![Tables One, Two, and Output](img/m72-10-g1.png) |

输出现在包含六行。`PROC SQL` 再次消除了表 `One` 中在表 `Two` 中匹配的行（第五行）。记住，当与 `EXCEPT` 操作符使用关键字 `ALL` 时，`PROC SQL` 不会对数据进行额外扫描以删除表 `One` 中的重复行。因此，表 `One` 中的第二行现在被包含在输出中。

## 在 EXCEPT 操作符使用关键字 CORR

要显示以下内容，请在集合操作符之后添加关键字 `CORR`：

* 仅名称相同的列
* 第一表中未出现在第二表的所有唯一行

修改后的 `PROC SQL` 集合操作、表 `One` 和 `Two` 以及输出所示：

| ```
proc sql;
   select *
      from one
   except corr
   select *
      from two;
``` | ![Tables One, Two, and Output](img/m72-10-g2.png) |

`X` 是两个表中名称相同的列，因此 `X` 是 `PROC SQL` 检查并显示在输出中的唯一列。在第一次扫描中，`PROC SQL` 从输出中消除了表 `One` 的第二行和第三行，因为它们在表中不是唯一的；它们包含的 `X` 值重复了表 `One` 第一行的 `X` 值。在第二次扫描中，`PROC SQL` 消除了表 `One` 的第一行、第四行和第五行，因为每每行包含的 `X` 值都匹配表 `Two` 中某行的 `X` 值。输出显示了表 `One` 中剩余的两个行，即在表 `One` 中唯一且在表 `Two` 中没有具有匹配 `X` 值的行。




当关键字 `ALL` 和 `CORR` 一起使用时，`EXCEPT` 算符会显示第一个表中所有未在第二个表中出现的唯一和重复行，并叠加且仅显示具有相同名称的列。修改后的 `PROC SQL` 集合操作、表 `One` 和 `Two` 以及输出所示：

```
proc sql;
   select *
      from one
   except all corr
   select *
      from two;
```

|  | ![Tables One, Two, and Output](img/m72-10-g3.png) |

再次，`PROC SQL` 仅查看并显示两个表中具有相同名称的列：`X`。由于使用了 `ALL` ，`PROC SQL` 不会消除表 `One` 中的任何重复行。因此，表 `One` 中的第二行和第三行（它们是表 `One` 第一行的重复）出现在输出中。`PROC SQL` 确实从输出中消除了表 `One` 的第一、第四行和第五行，因为对于这三行中的每一行，表 `Two` 中都有一个具有匹配 `X` 行。正如示例所示，当在使用 `EXCEPT` 算符配合 `ALL` 关键字时，除非表 `One` 中的行在表 `Two` 中有一个独立的匹配行，否则该行无法从输出中消除。表 `One` 包含三行 `X` 值为 1 的行，但表 `Two` 只有一行 `X` 值为 1。表 `Two` 中的那一行导致了表 `One` 中三个具有匹配 `X` 值的第一行被从输出中消除。然而，表 `Two` 并没有另外两个 `X` 值为 1 的行，因此表 `One` 的另外两行没有被消除，并出现在输出中。

## 示例：EXCEPT 算符

`EXCEPT` 算符可以解决真实的业务问题。假设你想显示公司所有新员工的姓名。没有哪个表专门包含新员工的信息，因此你使用了以下两个表的数据。

| 表 | 相关列 |
| --- | --- |
| `Sasuser.Staffchanges` 列出所有新员工以及薪水或职位代码发生变化的现有员工的信息 | `FirstName, LastName` |
| `Sasuser.Staffmaster` 列出所有现有员工的信息 | `FirstName, LastName` |

这两个表之间的关系如下图所示：![EXCEPT Operator](img/m72-12g1.png) 这两个表的交集包含了所有职位代码或薪水发生变化的现有员工的信息。阴影部分（即 `Sasuser.Staffchanges` 中与 `Sasuser.Staffmaster` 不重叠的部分）包含了你想要的信息：新员工。为了将 `Sasuser.Staffchanges` 中的新员工与现有员工隔离开，你创建了一个集合操作，显示第一个表（`Sasuser.Staffchanges`）中不存在于第二个表（`Sasuser.Staffmaster`）的所有行。以下 `PROC SQL` 步骤解决了此问题：

```
proc sql;
   select firstname, lastname
      from sasuser.staffchanges
   except all
   select firstname, lastname
      from sasuser.staffmaster;
```

此 `PROC SQL` 集合操作包含了算符 `EXCEPT` 和关键字 `ALL`。虽然你不希望输出包含重复行，但你已经知道这两个表之间没有重复项。因此，指定 `ALL` 是为了防止 `PROC SQL` 对数据进行额外扫描，从而加快此查询的处理速度。`PROC SQL` 仅比较 `SELECT` 子句中指定的列，并且这些列按照它们指定的顺序进行比较。输出显示了两个新员工的姓和名。![PROC SQL set operation](img/m72-12-g1.png) 注意：在使用 `EXCEPT` 算符的集合操作中，表在 `SELECT` 语句中列出的顺序是有区别的。如果此示例中的表顺序反过来，输出将显示所有薪水或职位代码没有发生变化的现有员工。

## 示例：内联视图中的 EXCEPT 算符

此示例是前一个集合操作的变体。假设你想显示薪水或职位代码没有变化的现有员工人数。再次，查询使用了以下表和列。

| 表 | 相关列 |
| --- | --- |
| `Sasuser.Staffchanges` 列出所有新员工以及薪水或职位代码发生变化的现有员工的信息 | `FirstName, LastName` |
| `Sasuser.Staffmaster` 列出所有现有员工的信息 | `FirstName, LastName` |

以下 `PROC SQL` 查询解决了这个问题：

```
proc sql;
   select count(*) label='No. of Persons'
      from (select EmpID
              from sasuser.staffmaster
            except all
            select EmpID
              from sasuser.staffchanges);
```

此 `PROC SQL` 查询使用了：
- `COUNT` 函数并以星号（`*`）作为参数，用于计算集合操作返回的员工 ID 数量
- 内联视图中的集合算符 `EXCEPT`。

内联视图返回一个包含薪水或职位代码没有变化的员工的虚拟表。然后将此虚拟表传递给 `COUNT(*)` 汇总函数，该函数计算虚拟表中的行数。输出显示了没有薪水或职位代码变化的现有员工人数![PROC SQL with COUNT](img/m72-13)

# 使用 INTERSECT 集合算符

## 概述

`INTERSECT` 算符执行以下两个操作：
- 选择两个表中共同的行
- 叠加列

![overlays columns](img/m72-4g2.png) 以下示例展示了其工作方式

## 单独使用 INTERSECT 算符

`INTERSECT` 算符以与 `EXCEPT` 算符相同的方式比较并叠加列，但按列位置而不是列名。然而，`INTERSECT` 选择行的方式不同，它显示两个表中共同的行。以下 PROC SQL 集合操作使用了之前两个表 `One` 和 `Two`：

|  | |

```
proc sql;
   select *
      from one
   intersect
   select *
      from two;
```

| ![Tables One, Two, and Output](img/m72-15-g1.png) |

表 `One` 和 `Two` 只有一个共同行，该行出现在输出中。（这是包含 `EXCEPT` 算符的示例中被消除的同一行。）

## 在 INTERSECT 算符中使用关键字 ALL

在之前的 `PROC SQL` 查询中添加 `ALL` 关键字可以防止 `PROC SQL` 对数据进行额外扫描。如果表 `One` 和 `Two` 之间存在任何其他共同行的重复项，它们也将被包含在输出中。然而，正如你所看到的，这些表中只有一个共同行。修改后的 `PROC SQL` 查询等所示：

|  | |

```
proc sql;
   select *
      from one
   intersect all
   select *
      from two;
```

| ![Tables One, Two, and Output](img/m72-16-g1.png) |

与之前一样，输出只有一行。

## 在 INTERSECT 算符中使用关键字 CORR

要根据列名而不是列位置显示两个表中共同的唯一行，请在 `PROC SQL` 集合操作中添加 `CORR` 关键字。修改后的查询、表 `One` 和 `Two` 以及输出所示：

|  | |

```
proc sql;
   select *
      from one
   intersect corr
   select *
      from two;
```

| ![Tables One, Two, and Output](img/m72-16-g2.png) |




`X` 是两个表中共同的唯一列名，因此 `X` 是 `PROC SQL` 检查并在输出中显示的唯一列项。在第一轮处理中，`PROC SQL` 删除了每个表内部重复的行：表 `One` 中的第二行和第三行其 `X` 值与第一行相同，而表 `Two` 中的第四行其 `X` 值与第三行相同。在第二轮处理中，`PROC SQL` 删除了任何在两个表间不共同的行：表 `One` 中的第四行、第五行，以及表 `Two` 中的第五行在另一个表中没有匹配的 `X` 值。输出显示了三行 `X` 值唯一的行，且这些行在两个表中都是共有的。

## 在 INTERSECT（交集）运算符上使用 ALL 和 CORR 关键字

如果同时使用 `ALL` 和 `CORR` 关键字，`INTERSECT` 运算符将根据相同名的列，显示两个表中共同的所有唯一和非唯一（重复）行。修改后的查询、表 `One` 和 `Two` 以及输出如下所示：

| |
```
proc sql;
   select *
      from one
   intersect all corr
   select *
      from two;
```
| | ![Tables One, Two, and Output](img/m72-16-g2.png) |

`PROC SQL` 仅检查并显示相同名的列 `X`。两个表中共有三行（在上方已高亮），这三行就是输出中显示的三个行。请注意，每个表都至少包含另一行，该行与共同行中的某行的 `X` 值是重复的。例如，在表 `One` 的第二行和第三行中，`X` 的值为 1，这与共同行之一的值相同。然而，为了被视为共同行并包含在输出中，一个表中的每个重复行必须在另一个表中也有一个单独的重复行。在本例中，没有既具有重复值又在两个表间共有的行。因此，在本例中，使用关键字 `ALL` 和 `CORR` 的集合操作所生成的输出与仅使用关键字 `CORR` 的产生的输出是相同的。

## 示例：INTERSECT 运算符

现在你已经看到了 `INTERSECT` 集合运算符如何在非常小的表上工作，我们可以在一个真实的业务问题中使用 `INTERSECT`。假设你想显示更改过薪资或职位代码的现有员工姓名。（此查询与你使用 `EXCEPT` 运算符解决的查询相反。）再次，你使用以下表：

| 表名 | 相关列 |
| --- | --- |
| `Sasuser.Staffchanges` 列出了所有新员工以及薪资或职位代码发生变化的员工的信息 | `FirstName`, `LastName` |
| `Sasuser.Staffmaster` 列出了所有现有员工的信息 | `FirstName`, `LastName` |

这两个表之间的关系如下图所示：![INTERSECT Operator](img/m72-17g1.png) 正如早之前的 `EXCEPT` 示例所示，这两个表的交集包含了所有更改过职位代码或薪资的现有员工的信息。你想显示的就是这两个表的交集（如上方所示的阴影部分）。为了显示两个表共有的唯一行，你使用一个包含 `INTERSECT` 的 `PROC SQL` 集合操作。已知这些表不包含重复项，因此使用 `ALL` 来加速查询处理。`PROC SQL` 集合操作如下：

```
proc sql;
   select firstname, lastname
      from sasuser.staffchanges
   intersect all
   select firstname, lastname
      from sasuser.staffmaster;
```

注意：在此 `PROC SQL` 步骤中，由于仅包含一个 `INTERSECT` 集合运算符，在 `SELECT` 语句中列出表的顺序没有区别。然而，在包含多个堆叠的 `INTERSECT` 集合运算符的复杂 `PROC SQL` 步骤中，仔细考虑表的顺序是非常重要的，这取决于你想要何时消除不匹配项。输出显示有四位更改过薪资或职位代码的现有员工。![INTERSECT set operator](img/m72-17-g1.png)

# 使用 UNION（并集）集合运算符

## 概述

`UNION` 集合运算符同时执行以下两项操作：

* 从两个表中选择唯一行
* 叠加列。

![overlays columns](img/m72-4g3.png) 下述的示例演示了 `UNION` 在单独使用以及与关键字 `ALL` 和 `CORR` 一起使用时的工作原理。

## 单独使用 UNION 运算符

要显示表 `One` 和 `Two` 中在两个表合并行集中唯一的行，请使用包含 `UNION` 运算符的 `PROC SQL` 集合操作：

| |
```
proc sql;
   select *
      from one
   union
   select *
      from two;
```
| | ![Tables One, Two, and Output](img/m72-20-g1.png) |

使用 `UNION` 运算符，`PROC SQL` 首先拼接并排序来自两个表的行，并消除任何重复行。在本例中，删除了两行：表 `One` 中的第二行是第一行的重复，表 `Two` 中的第四行与第五行匹配。使用 `UNION` 运算符，`PROC SQL` 首先拼接并排序来自两个表的行，并消除任何重复行。

## 在 UNION 运算符上使用 ALL 关键字

当 `UNION` 运算符上添加 `ALL` 关键字时，输出显示两个表中所有的行，包括重复行。修改后的查询、表 `One` 和 `Two` 以及输出如下所示：

| |
proc sql;
   select *
      from one
   union all
   select *
      from two;
```
| | ![Tables One, Two, and Output](img/m72-21-g1.png) |

使用 `ALL` 时，PROC SQL 不移除重复项也不排序行。输出现在包含了上一个示例中被消除的重复行：表 `One` 中的第二行和表 `Two` 中的第四行。列按位置叠加。

## 在 UNION 运算符上使用 CORR 关键字 

要显示表 `One` 和 `Two` 中在两个表合并行集中唯一的行，基于相同的名称而非相同的位置，请在集合运算符后添加 `CORR` 关键字。输出如下所示：

| |
proc sql;
   select *
      from one
   union corr
   select *
      from two;
```
| | ![Tables One, Two, and Output](img/m72-21-g2.png) |

`X` 是两个表中共同的唯一列名，因此 `X` 是 `PROC SQL` 检查并在输出中显示的唯一列项。在两个表的合并行集中，存在值 1、2、3 的重复，这些重复行从输出中消除。输出显示了六个唯一的 `X` 值。

## 在 UNION 运算符上使用关键字 ALL 和 CORR 

如果同时使用 `ALL` 和 `CORR` 关键字，`UNION` 运算符将根据相同的列，显示两个表中共同的所有唯一和重复行。在本例中，输出显示了全部 12 个 `X` 值，即两个表中具有相同名的列。

| |
```
proc sql;
   select *
      from one
   union all corr
   select *
      from two;
```
| | ![Tables One, Two, and Output](img/m72-21-g3.png) |

## 示例：UNION 运算符

`UNION` 运算符可以解决真实的业务问题。假设你正在根据健康诊所的数据生成报告。你想显示 1998 年进行的个体患者压力测试结果，随后是 1999 年进行的压力测试结果。为了实现这一点，你使用 `UNION` 运算符合并表 `Sasuser.Stress98` 和 `Sasuser.Stress99`。这两个表在结构相似：

* 两个表都包含九列名称相同的列
* 每行包含一个个体患者的数据。





你不确定表中是否包含重复记录，但你不希望在输出结果中出现重复项。由于这些表具有相同的列结构，你可以按位置重叠列，且不需要 `CORR` 关键字。下面显示了 `PROC SQL` 设置操作和输出（行按 ID 排序）：

| |
```
proc sql;
  select *
    from sasuser.stress98
  union 
  select *
    from sasuser.stress99;
```
| ![使用带有 UNION 算符的 PROC SQL 输出](img/m72-22-g1.png) |

**提示**：如果你能确定这些表没有重复记录，可以添加关键字 `ALL`，通过避免对数据进行额外的一遍扫描来加快处理速度。

## 示例：UNION 算符和汇总函数

我们可以演示另一个真实的业务问题，以观察如何结合集合操作（在本例中为 `UNION`）使用汇总函数。假设你想为常旅客计划的成员显示以下汇总数据：总获得积分、总已用积分数和总飞行里程数。这三个值都可以使用汇总函数从 `Sasuser.Frequentflyers` 表的列中计算。你可能会奇怪，当只涉及一个表时为什么还需要集合操作。如果你想将三个汇总值水平显示在三个单独的列中，你可以使用集合操作，使用以下简单的 `SELECT` 语句来解决问题：

```
proc sql;
   select sum(pointsearned) format=comma12.
          label='Total Points Earned',
          sum(pointsused) format=comma12.
          label='Total Points Used',
          sum(milestraveled) format=comma12.
          label='Total Miles Traveled'
      from sasuser.frequentflyers;
```

![UNION 算符和汇总函数](img/m72-23-g1.png) 然而，假设你想让三个值垂直显示在单列中。为了生成此输出，你在同一张表上创建三个不同的查询，然后使用两个 `UNION` 集合算符来组合三个查询结果：

```
proc sql;
title 'Points and Miles Traveled';
title2 'by Frequent Flyers'; 
   select 'Total Points Traveled:',
          sum(MilesTraveled) format=comma12.
      from sasuser.frequentflyers
   union
   select 'Total Points Earned:',
          sum(PointsEarned) format=comma12.
      from sasuser.frequentflyers
   union
   select 'Total Points Used:',
          sum(PointsUsed) format=comma12.
      from sasuser.frequentflyers;
```

每个 `SELECT` 子句定义了两列：一个作为标签的字符常量和一个汇总值。输出所示。![UNION 算符和汇总函数](img/m72-23-g2.png) **注意**：前面的程序读取了三次相同的表，因此它不是解决此问题的有效方法。

# 使用 OUTER UNION 集合算符

## 概述

`OUTER UNION` 集合算符通过以下方式连接查询结果：

* 从两个表中选择所有行（包括唯一和非唯一的行）
* 不重叠列。

![不重叠列](img/m72-4g4.png) 我们可以演示 `OUTER UNION` 单独使用以及配合关键字 `CORR` 使用时的工作原理。`OUTER UNION` 使用 `ALL` 关键字，因为该算符的默认操作是在输出中包含所有行。

## 单独使用 OUTER UNION 算符

假设你想显示 `One` 和 `Two` 两个表的所有行，且不重叠列。包含 `OUTER UNION` 算符、两个表以及输出的 `PROC SQL` 设置操作所示：

| |
```
proc sql;
   select *
      from one
   outer union
   select *
      from two;
```
| ![表 One, Two 和输出](img/m72-25-g1.png) |

在输出中，列没有重叠。相反，显示了来自两个表的所有四个列。输出的每行在对应另一个表的两个列中包含缺失值。

## 在 OUTER UNION 算符上使用关键字 CORR

上一个集合操作的输出包含两个同名的列。要重叠具有相同名称列，请在集合操作中添加 `CORR` 关键字：

| |
```
proc sql;
   select *
      from one
   outer union corr
   select *
      from two;
```
| ![表 One, Two 和输出](img/m72-26-g1.png) |

修改后的集合操作的输出仅包含三列，因为两个名为 `X` 的列被重叠了。

## 示例：OUTER UNION 算符

许多业务场景需要连接两个或多个表。例如，假设你想显示在航空公司工作的所有机械师的员工工号、职位代码和薪水。机械师工作有三个级别，并且有一个单独的表包含每个级别机械师的数据：`Sasuser.Mechanicslevel1`、`Sasuser.Mechanicslevel2` 和 `Sasuser.Mechanicslevel3`。这些表都包含相同的三列。下面的 `PROC SQL` 步骤使用两个 `OUTER UNION` 算符来连接表，并使用 `CORR` 关键字来重叠具有共同名称的列：

| |
```
proc sql; 
   select *
      from sasuser.mechanicslevel1
   outer union corr
   select *
      from sasuser.mechanicslevel2
   outer union corr
   select *
      from sasuser.mechanicslevel3;
```
| ![使用 CORR 关键字的 OUTER UNION](img/m72-27-g1.png) |

# 比较 Outer Unions 和其他技术

使用 `OUTER UNION` 算符的 `PROC SQL` 设置操作是连接表的 SAS 技术之一，如下程序所示。程序 1 是之前提到的。程序 2 使用了不同的 SAS 技术来连接 `One` 和 `Two`。

## 程序 1：带有 CORR 的 PROC SQL OUTER UNION 操作

```
proc sql;
   create table three as 
      select * from one 
      outer union
      select * from two;
quit;
```

## 程序 2：DATA Step、SET 语句和 PRINT Step

```
 data three; 
    set one two; 
 run;
 proc print data=three; 
 run;
```

这两个程序创建了相同的输出，如下![DATA Step、SET 语句和 PRINT Step](img/m72-29-g1.png) 当表具有相同列时，除非使用了 `CORR` 关键字，否则 `PROC SQL` 外连接不会产生相同的输出。`CORR` 会导致同名列（在本例中为名为 `X` 的两个列）重叠；如果没有 `CORR`，`OUTER UNION` 算符会在结果集中包含同名列。DATA 程序只生成一个列。

## 总结

## 文字总结

### 理解集合操作

集合操作通过垂直组合（堆叠）来连接表或视图。集合操作是一个包含

* 两个查询（每个查询都以 `SELECT` 子句开始）
* 一个集合算符 `EXCEPT`、`INTERSECT`、`UNION` 和 `OUTER UNION`
* 一个或两个作为修饰符的关键字 `ALL` 和 `CORR` 的单个 `SELECT` 语句可以包含多个集合操作。在处理仅显示唯一行的集合操作（包含集合算符 `EXCEPT`、`INTERSECT` 或 `UNION`）时，`PROC SQL` 默认对数据进行两次扫描。对于显示唯一和重复行的集合操作，只需要扫描一遍数据。对于 `EXCEPT`、`INTERSECT` 和 `UNION` 集合算符，列根据列在 `SELECT` 子句中的相对位置进行重叠，而不是根据列名。为了进行重叠，两个 `SELECT` 子句中相同相对位置的列必须具有相同的数据类型。一个或两个关键字可以用于修改集合算符的默认操作。





### 使用 EXCEPT 集合运算符

集合操作符 `EXCEPT` 从第一个表（第一个查询中指定的表）中选择在第二个表（第二个查询中指定的表）中未找到唯一行，并进行列叠加。此集合操作可以使用 `ALL` 或 `CORR` 关键字（或两者）进行修改。

### 使用 INTERSECT 集合运算符

集合操作符 `INTERSECT` 选择两个表中共同拥有的唯一行并进行列叠加。此集合操作可以使用 `ALL` 或 `CORR` 关键字（或两者）进行修改。

### 使用 UNION 集合运算符

集合操作符 `UNION` 从两个表中选择所有唯一行并进行列叠加。此集合操作可以使用 `ALL` 或 `CORR` 关键字（或两者）进行修改。

### 使用 OUTER UNION 集合运算符

集合操作符 `OUTER UNION` 通过选择两个表中的所有行（包括唯一和非唯一的）来连接两个查询的结果，且不进行列叠加。此集合操作可以使用关键字 `CORR` 进行修改。

### 比较外部联合集和其他 SAS 技术

使用 `OUTER UNION` 集合操作符的 `PROC SQL` 集合操作并不是在 SAS 中连接表的唯一方法。可以使用其他 SAS 技术，例如由 `DATA` 步、`SET` 语句和 `PROC PRINT` 步组成的程序。

## 示例程序

```sas
proc sql;
   select firstname, lastname
      from sasuser.staffchanges
   intersect all
   select firstname, lastname
      from sasuser.staffmaster;
quit;
```

## 注意事项

* 无论 `SELECT` 语句中包含多少个集合操作，该语句只包含一个分号，该分号放置在最后一个查询之后。
* 为了进行叠加，列必须具有相同的数据类型。

# 测验

为每个问题选择最佳答案。完成测验后，使用附录中的答案对照检查您的答案。

1. 对于不使用关键字的 `EXCEPT`、`UNION` 或 `INTERSECT` 集合运算符的集合操作，以下哪个陈是错误的？

    1. 结果集中的列名由第一个表决定。
    2. 为了进行叠加，列必须具有相同的数据类型。
    3. 为了进行叠加，列必须具有相同的名称。
    4. 默认情况下，结果集中仅显示唯一行。

2. 关键字 `ALL` 不能与以下哪个集合运算符一起？

    1. `EXCEPT`
    2. `INTERSECT`
    3. `UNION`
    4. `OUTER UNION`

3. 哪个 `PROC SQL` 步结合了 `Summer` 和 `Winter` 表以产生所示输出？![测验输出](img/m72-32-g1.png)

    1. ```sas
        proc sql;
           select *
              from summer
           intersect all
           select *
              from winter;
        ```
    2. ```sas
        proc sql;
           select *
              from summer
           outer union
           select *
              from winter;
        ```
    3. ```sas
        proc sql;
           select *
              from summer
           union corr
           select *
              from winter;
        ```
    4. ```sas
        proc sql;
           select *
              from summer
           union
           select *
              from winter;
        ```

4. 哪个 `PROC SQL` 步结合了表但没有叠加任何列？

    1. ```sas
        proc sql;
           select *
              from groupa
           outer union
           select *
              from groupb;
        ```
    2. ```sas
        proc sql;
           select *
              from groupa as a
           outer union corr
           select *
              from groupb as b;
        ```
    3. ```sas
        proc sql;
           select coalesce(a.obs, b.obs)
                  label='Obs', med, duration
              from groupa as a
              full join 
              groupb as b
              on a.obs=b.obs;
        ```
    4. ```sas
        proc sql;
           select *
              from groupa as a
           intersect
           select *
              from groupb as b;
        ```

5. 关于关键字 `CORRESPONDING`，哪个陈述是错误的？

    1. 它不能与关键字 `ALL` 一起使用。
    2. 它按名称叠加，而不是按位置叠加。
    3. 在 `EXCEPT`、`INTERSECT` 和 `UNION` 集合操作中使用时，它会移除两个表中均未找到的列。
    4. 在 `OUTER UNION` 集合操作中使用时，它会导致同名的列进行叠加。

6. 哪个 `PROC SQL` 步从 `Dogs` 和 `Pets` 表生成以下输出？![测验输出](img/m72-32-g2.png)

    1. ```sas
        proc sql;
           select name, price
              from pets 
           except all
           select *
              from dogs;
        ```
    2. ```sas
        proc sql;
           select name, price
              from pets 
           except
           select *
              from dogs;
        ```
    3. ```sas
        proc sql;
           select name, price
              from pets 
           except corr all
           select *
              from dogs;
        ```
    4. ```sas
        proc sql;
           select *
              from dogs 
           except corr
           select name, price
              from pets;
        ```

7. `PROG1` 表和 `PROG2` 表分别列出了参加课程的学生。哪个 `PROC SQL` 步给出了参加了 `PROG1` 的学生名称？![测验输出](img/m72-32-g3.png)

    1. ```sas
        proc sql;
           select fname, lname
              from prog1
           intersect
           select fname, lname
              from prog2;
        ```
    2. ```sas
        proc sql;
           select fname, lname
              from prog1
           except all
           select fname, lname
              from prog2;
        ```
    3. ```sas
        proc sql;
           select *
              from prog2
           intersect corr
           select *
              from prog1;
        ```
    4. ```sas
        proc sql;
           select *
              from prog2
           union
           select *
              from prog1;
        ```

8. 哪个 `PROC SQL` 步返回参加了 PROG1、PROG2 或两者的课程的学生名称？![测验输出](img/m72-32-g4.png)

    1. ```sas
        proc sql;
           select fname, lname
              from prog1
           intersect
           select fname, lname
              from prog2;
        ```
    2. ```sas
        proc sql;
           select fname, lname
              from prog1
           outer union corr
           select fname, lname
              from prog2;
        ```
    3. ```sas
        proc sql;
           select fname, lname
              from prog1
           union
           select fname, lname
              from prog2;
        ```
    4. ```sas
        proc sql;
           select fname, lname
              from prog1
           except corr
           select fname, lname
              from prog2;
        ```

9. 哪个 `PROC SQL` 步返回参加参加了 PROG1 和 PROG2 课程的学生名称？![测验输出](img/m72-32-g5.png)

    1. ```sas
        proc sql;
           select fname, lname
              from prog1
           union
           select fname, lname
              from prog2;
        ```
    2. ```sas
        proc sql;
           select fname, lname
              from prog1
           except corr
           select fname, lname
              from prog2;
        ```
    3. ```sas
        proc sql;
           select fname, lname
              from prog1
           intersect all
           select fname, lname
              from prog2;
        ```
    4. ```sas
        proc sql;
           select fname, lname
              from prog1
           union corr
           select fname, lname
              from prog2;
        ```

10. 哪个 `PROC SQL` 步与以下 DATA 步生成相同结果？

    |  





```sas
data allstudents;
   set prog1 prog2;
   by lname;
run;
proc print noobs;
run;
```

| ![PROG1 and PROG2 Tables](img/m72-32-g6.png) |

1.  ```sas
proc sql;
   select fname, lname
      from prog1
   outer union corr
   select fname, lname
      from prog2
   order by lname;
```

2.  ```sas
proc sql;
   select fname, lname
      from prog1
   union
   select fname, lname
      from prog2
   order by lname;
```

3.  ```sas
proc sql;
   select fname, lname
      from prog2
   outer union
   select fname, lname
      from prog1
   order by lname;
```

4.  ```sas
proc sql;
   select fname, lname
      from prog2
   union corr
   select fname, lname
      from prog1
   order by lname;
```

# 第 5 章：使用 PROC SQL 创建和管理表

概述理解创建表的方法通过定义列创建空表显示表的结构创建一个与另一个表相同的空表根据查询结果创建表向表中插入数据行创建具有完整性约束的表处理行插入中的错误显示表的完整性约束更新现有表行值删除表中的行修改表的列删除表总结测验

## 概述

## 引言

通过使用 `PROC SQL`，你可以快速高效地创建、修改和删除表。许多 `PROC SQL` 语句非常多功能，允许你以多种方式执行相同的操作。例如，使用 `CREATE TABLE` 语句创建表有三种方法：

*   通过定义列创建一个空表（不含行的表）
*   创建一个与另一个表具有相同列和属性的空表
*   根据查询结果创建表

接下来的 `PROC SQL` 步骤使用 `CREATE TABLE` 语句通过定义列创建一个空表，并使用 `DESCRIBE TABLE` 语句在 SAS 日志中显示表结构的信息：

```sas
 proc sql;
    create table work.discount 
           (Destination char(3),
           BeginDate num Format=date9.,
           EndDate num format=date9.,
           Discount num);
    describe table work.discount;
```

表 5.1 SAS 日志

|  

```sas
1    proc sql;
2       create table work.discount
3              (Destination char(3),
4              BeginDate num Format=date9.,
5              EndDate num format=date9.,
6              Discount num);
NOTE: Table WORK.DISCOUNT created, with 0 rows and 4 columns.
7       describe table work.discount;
NOTE: SQL table WORK.DISCOUNT was created like:
```

```sas
create table WORK.DISCOUNT( bufsize=4096 )
            ( 
            Destination char(3),
            BeginDate num format=DATE9.,
            EndDate num format=DATE9.,
            Discount num
            );
```

 |

### 理解创建表的方法

你可以使用 `PROC SQL` 以三种方式创建表。所有三种方法都使用 `CREATE TABLE` 语句，尽管该语句的语法随每个方法而异。

| 创建表的方法 | 示例 |

| --- | --- |
| 通过定义列创建空表 |  

```sas
proc sql;
    create table work.discount
           (Destination char(3),
           BeginDate num Format=date9.,
           EndDate num format=date9.,
           Discount num);
```

 |

| 创建与现有表相同（具有相同列和属性）的空表 |  

```sas
proc sql;
    create table work.discount
2(Destination char(3),
           BeginDate num Format=date9.,
           EndDate num format=date9.,
           Discount num);
```

 |
| 根据查询结果创建填充表（包含列和行的表） |  

```sas
proc sql;
   select fname, lname
      from prog1
   union
   select fname, lname
      from prog2
   order by lname;
``` |

`CREATE TABLE` 语句仅生成表，不生成报告。SAS 日志会显示已创建表以及行数和列数。

表 5.2 SAS 日志

|  

```sas
NOTE: Table FLIGHTAYS2 created, with 0 rows and 8 columns.
```

 |

注意：在 `PROC SQL` 中通过 `DESCRIBE TABLE` 语句可以在 SAS 日志中查看表结构的信息。`DESCRIBE TABLE` 语句将在后讨论。

### 通过定义列创建空表

## 概述

有时你想创建一个与任何现有表不同的新表。在这种情况下，你需要定义所有列。为了实现这一点，请使用包含列定义的的 `CREATE TABLE` 语句。注意：此语句创建一个不行的表（空表）。此外，可以在 `CREATE TABLE` 语句中指定完整性约束。完整性约束将在本章稍后讨论。

| 带有列定义的 CREATE TABLE 语句通用形式：CREATE TABLE table-name(column-specification-1,...column-specification-n>); 这里是语法的解释：table-name 指定要创建的表名。column-specification 指定包含在表的列，由 column-definition 组成 <column-constraint-1<...column-constraint-n><MESSAGE='message-string'<MSGTYPE=message-type>> 这里是语法的解释：column-definition 包含以下：column-name data-type<(column-width)><column-modifier-1<... column-modifier-n>>column-name 指定列名。表中存储的列名与 column-name 情况相同。data-type 用括号括起来指定以下类型之一：CHARACTER (or CHAR) | VARCHAR | INTEGER (or INT) | SMALLINT | DECIMAL (or DEC) | NUMERIC (or NUM) | FLOAT | REAL | DOUBLE PRECISION | DATE.column-width 括号内的整数指定列宽。（PROC SQL 仅对 CHARACTER 和 VARCHAR 数据类型处理此值。）column-modifier 是以下类型之一：INFORMAT= | FORMAT= | LABEL= . 可能会指定多个 column-modifier。column-constraint 指定完整性约束。MESSAGE= 和 MSGTYPE 指定与完整性约束相关的错误消息。（此处未详述完整性约束、column-constraint、MESSAGE= 和 MSGTYPE，将在本章稍后详细讨论。） |

注意：所有列-specification 必须在括号内。多个 column-specification 之间用逗号分隔。column-specification 内部的元素之间用空格分隔。

## 示例





假设你想创建一个临时表 `Work.Discount`，该表包含航空公司提供的折扣数据。目前没有现有表包含你想包含的四个列（以及列属性）：`Destination`、`BeginDate`、`EndDate` 和 `Discount`。你使用以下 `PROC SQL` 步骤根据你指定的列定义来创建表：

```
 proc sql;
    create table work.discount 
           (Destination char(3),
           BeginDate num Format=date9.,
           EndDate num format=date9.,
           Discount num);
```

SAS 日志确认表已创建。

表 5.3 SAS 日志

|  
```
NOTE: Table WORK.DISCOUNT created, with 0 rows and 4 columns.
```
 |

**提示** 
在本例以及本章的所有其他示例中，你指示将数据保存到临时表（在 `Work` 库中），该表会在 SAS 会话结束时删除。若要将表永久保存到不同的库中，请在 `CREATE TABLE` 子句中使用适当的 libref 代替 `Work` `。
在接下来的几节中，你将学习更多关于如何在列规范中指定数据类型和列修饰符的知识。
**注意**：你将在本章后面的部分学习向表中插入数据行。

## 指定数据类型

当你通过定义列来创建表时，必须在列名后为每列指定数据类型：`column-name data-type <(column-width)> <column-modifier-1...column-modifier-n>`
例如，以下 `PROC SQL` 步骤（在前节中也显示）定义了四个列：一个字符列（`Destination`）和三个数值列（`BeginDate`、`EndDate` 和 `Discount`）：

```
proc sql;
   create table work.discount 
          (Destination char(3),
          BeginDate num format=date9.,
          EndDate num format=date9.,
          Discount num);
```

SAS 表使用两种数据类型：数值和字符。然而，`PROC SQL` 支持额外的数据类型（SQL 数据库支持的数据类型中的许多，但并非全部）。因此，在 `CREATE TABLE` 语句中，你可以指定 10 种不同类型中的任意一种。在创建表时，`PROC SQL` 将支持但不是 SAS 数据类型的支持类型转换为数值或字符格式。

表 5.4 `PROC SQL` 支持的字符数据类型

| 指定的数据类型 | SAS 数据类型 |
| --- | --- |
| CHARACTER (or CHAR) | CHARACTER |
| VARCHAR | CHARACTER |

表 5.5 `PROC SQL` 支持的数值数据类型

| 指定的数据类型 | 描述 | SAS 数据类型 |
| --- | --- | --- |
| NUMERIC (or NUM) | 浮点 | NUMERIC |
| DECIMAL (or DEC) | 浮点 | NUMERIC |
| FLOAT | 浮点 | NUMERIC |
| REAL | 浮点 | NUMERIC |
| DOUBLE PRECISION | 浮点 | NUMERIC |
| INTEGER (or INT) | 整数 | NUMERIC |
| SMALLINT | 整数 | NUMERIC |
| DATE | 日期 | 带有 DATE.7 信息和格式的 NUMERIC |

以下 `PROC SQL` 步骤与之前的示例非常。唯一的区别是该步骤指定了除 `CHAR` 和 `NUM` 之外的三种支持的数据类型：`VARCHAR`、`DATE` 和 `FLOAT`。

```
proc sql;
   create table work.discount2 
          (Destination varchar(3),
          BeginDate date,
          EndDate date,
          Discount float);
```

`PROC SQL` 将这些数据类型转换为字符或数值，如上表所示。因此，表 `Work.Discount2`（由此 `PROC SQL` 步骤创建）和 `Work.Discount`（由之前的 `PROC SQL` 步骤创建）包含相同的列。通过支持 SAS 数据类型以外的数据类型，`PROC SQL` 可以为你节省时间。在许多情况下，你可以从 SAS 外部的 SQL 实现复制原生代码，而无需修改数据类型。

## 指定列宽

在 SAS 中，字符列和数值列的默认列宽均为 8 字节。然而，字符和数值数据的存储方式不同：

* 字符数据每个字节存储一个字符。
* 数值数据以真实二进制表示的浮点数存储，这允许在 8 字节内实现 16 或 17 位精度。

`PROC SQL` 允许你为字符列指定列宽，但不能为数值列指定。
**注意**：`PROC SQL` 允许在 `DECIMAL`、`NUMERIC` 和 `FLOAT` 数据类型的列规范中包含 `WIDTH` 和 `NDEC`（小数位数）参数。然而，`PROC SQL` 会忽略此规范并使用 SAS 默认值。
在列规范中，列宽紧随数据类型，并以括号内的整数指定：`column-name data-type <(column-width)> <column-modifier-1...column-modifier-n>`
在以下 `PROC SQL` 步骤中，第一个列规范为字符列 `Destination` 指定了 3 的宽度：

```
proc sql;
   create table work.discount 
          (Destination char(3),
          BeginDate num format=date9.,
          EndDate num format=date9.,
          Discount num);
```

由于最后三列是数值型的，没有指定宽度，这些列具有 8 字节的默认列宽。

## 指定列修饰符

在 `CREATE TABLE` 语句中，列规范可能包含以下 SAS 列修饰符的一个或多个：`INFORMAT=`、`FORMAT=` 和 `LABEL=`。如果使用修饰符，指定在列规范的末尾：`column-name data-type <(column-width)> <column-modifier-1...column-modifier-n>`
**注意**：第四种 SAS 列修饰符 `LENGTH=` 不允许用于 `CREATE TABLE` 子句。它可以在 `SELECT` 子句中使用。

## 示例

以下 `PROC SQL` 步骤通过指定 4 个列创建表 `Work.Departments`。列修饰符 `LABEL=` 和 `FORMAT=` 用于指定额外的列属性。

```
proc sql;
   create table work.departments 
          (Dept varchar(20) label='Department',
           Code integer label='Dept Code',
           Manager varchar(20),
           AuditDate num format=date9.);
```

SAS 日志确认表已创建。

表 5.6 SAS 日志

|  
```
NOTE: Table WORK.DEPARTMENTS created, with 0 rows and 4 columns.
```
 |

### 显示表的结构

## 概述

有时你想查看你创建或他人表的结构。当你创建表时，`CREATE TABLE` 语句向 SAS 日志写入消息，指示所创建表的行数和列数。然而，该消息不包含列属性的信息。如果你正在处理包含行数据的现有表，你可以使用 `PROC SQL` 查询生成一个显示表中所有列的报告。然而，报告没有列出列属性，且 PROC SQL 查询不会为空表生成输出。若要在 SAS 日志中显示一个或多个表的列和列属性（无论这些表是否包含行数据），可以使用 `PROC SQL` 中的 `DESCRIBE TABLE` 语句。

| DESCRIBE TABLE 语句通用形式：DESCRIBE TABLE table-name-1<, ... table-name-n>;
以下是对语法的解释：table-names 指定要描述的表可以是以下内容之一：

* 单级名称
* 双级 libref.表名
* 用单引号括起来的物理路径。

 |





`DESCRIBE TABLE` 语句会将指定表的 `CREATE TABLE` 语句（包含列定义）写入 SAS 日志（SAS log）中，无论该表最初是如何创建的。例如，如果 `DESCRIBE TABLE` 语句指定了一个通过 `DATA` 步创建的表，仍然会显示 `CREATE TABLE` 语句。

注意：`DESCRIBE TABLE` 语句还会显示关于表上定义的任何索引的信息。您可以在使用 PROC SQL 创建和管理索引中了解更多关于使用 `DESCRIBE TABLE` 语句显示索引信息的知识。

提示：作为 `DESCRIBE TABLE` 语句的替代方案，您可以使用其他 SAS 过程（procedures），例如 `PROC CONTENTS`来列出表的列和列属性。`PROC CONTENTS` 生成的是报告，而不是像 `DESCRIBE TABLE` 语句那样向 SAS 日志写入消息。

## 示例

在本章的早期部分，使用 `CREATE TABLE` 语句和下所示的列规格创建了空表 `Work.Discount`：

```
proc sql;
   create table work.discount 
          (Destination char(3),
          BeginDate num format=date9.,
          EndDate num format=date9.,
          Discount num);
```

接下来的 `DESCRIBE TABLE` 语句为 `Work.Discount` 表向 SAS 日志写入 `CREATE TABLE` 语句：

```
proc sql;
   describe table work.discount;
```

注意：关于 `BUFSIZE=` 选项的更多信息，请参见使用 BUFSIZE= 选项。

表 5.7 SAS 日志

```
NOTE: SQL table WORK.DISCOUNT was created like:
```

```
create table WORK.DISCOUNT( bufsize=4096 )
            (            
            Destination char(3),
            BeginDate num format=DATE9.,
            EndDate num format=DATE9.,
            Discount num
            )
```

# 创建与另一个表类似的空表

## 概述

有时您想创建一个新表，该表具有与现有表相同的列和属性，但没有数据行。要创建一个类似于另一个表的空表，请使用带有 `LIKE` 子句的 `CREATE TABLE` 语句。

| 带有 LIKE 子句的 CREATE TABLE 语句的一般形式：CREATE TABLE table-nameLIKE table-1;以下是该语法的解释：table-name 指定要创建的表的名称。table-1 指定将它的列和属性复制到新表的表。 |

## 示例

假设您想创建一个名为 `Work.Flightdelays2` 的新表，其中包含有关航班延迟的数据。您希望新表包含与现有表 `Sasuser.Flightdelays` 相同的列和属性，但您不想包含包含任何现有数据。接下来的 `PROC SQL` 步使用 `CREATE TABLE` 语句和 `LIKE` 子句来创建 `Work.Flightdelays2`：

```
proc sql;
   create table work.flightdelays2 
      like sasuser.flightdelays;
```

接下来的 `DESCRIBE TABLE` 语句显示空表 `Work.Flightdelays2` 的结构：

```
proc sql;
   describe table work.flightdelays2;
```

表 5.8 SAS 日志

```
NOTE: SQL table WORK.FLIGHTDELAYS2 was created like:

create table WORK.FLIGHTDELAYS2( bufsize=8192 )
  (
   Date num format=DATE9\. informat=DATE9.,
   FlightNumber char(3),
   Origin char(3),
   Destination char(3),
   DelayCategory char(15),
   DestinationType char(15),
   DayOfWeek num,
   Delay num
  );
```

`Work.Flightdelays2` 包含列出的八个列。

## 从表中指定列的子集

如果您想创建一个仅包含现有表中指定列的子集的空表，请使用 SAS 数据集选项 `DROP=` 或 `KEEP=.`。

| DROP= 和 KEEP= 数据集选项的一般形式：(DROP | KEEP =column-1< ...column-n>)以下是该语法的解释：column 指定要丢弃或保留的列名。多个列名必须用空格分隔。整个选项必须括在括号内。 |

在 `CREATE TABLE` 语句中，`DROP=` 或 `KEEP=` 选项可以插入在以下位置之一：

*   在正在创建的表名与 `LIKE` 子句之间（如下所示）
*   在源表名之后，`LIKE` 子句的末尾。

## 示例

接下来的 `PROC SQL` 步创建新表 `Work.Flightdelays3`，它包含来自 `Sasuser.Flightdelays` 表的列子集。使用 `DROP=` 选项指定除 `DelayCategory` 和 `DestinationType` 之外的所有列都包含在新表中。

```
proc sql;
   create table work.flightdelays3
          (drop=delaycategory destinationtype)
      like sasuser.flightdelays;
```

作为对比，原始表和新表运行 `DESCRIBE TABLE` 语句的结果如下所示。

表 5.9 SAS 日志

```
NOTE: SQL table WORK.FLIGHTDELAYS was created like:

create table SASUSER.FLIGHTDELAYS( bufsize=8192 )
  (
   Date num format=DATE9\. informat=DATE9.,
   FlightNumber char(3),
   Origin char(3),
   Destination char(3),
   DelayCategory char(15),
   DestinationType char(15),
   DayOfWeek num,
   Delay num
  );
```

表 5.10 SAS 日志

```
NOTE: SQL table WORK.FLIGHTDELAYS3 was created like:

create table WORK.FLIGHTDELAYS3( bufsize=4096 )
  (
   Date num format=DATE9\. informat=DATE9.,
   FlightNumber char(3),
   Origin char(3),
   Destination char(
   )
  );
```

如这些消息所示，`Sasuser.Flightdelays` 包含列 `DelayCategory` 和 `DestinationType`。`Work.Flightdelays3` 不包含这些列。注意：在 `PROC SQL` 中，您可以对表应用大多数数据集选项，如 `DROP=` 和 `KEEP=`。但是，由于 `DROP=` 和 `KEEP=` 是 SAS 选项而非 SQL 标准的一部分，您只能在指定表时使用它们。

### 从查询结果创建表

## 概述

有时您想创建一个新表，该表具有与现有表相同的列和行。在这种情况下，您可以提交一个 `PROC SQL` 步来执行以下操作：

*   创建一个新表
*   用查询结果填充表

要从查询结果创建表，请使用包含 `AS` 关键字以及查询中使用的子句的 `CREATE TABLE` 语句：`SELECT`、`FROM` 以及任何可选子句。

| 带有查询子句的 CREATE TABLE 语句的一般形式：CREATE TABLE table-name ASSELECT column-1< ... column-n>FROM table-1 &#124; view-1< ... table-n &#124; view-n><optional query clauses>;以下是该语法的解释：table-name 指定要创建的表的名称。SELECT 指定出现在表中的列。FROM 指定要查询的表或视图。可选子句用于进一步完善查询，包括 ORDER BY, GROUP BY, HAVING。 |

您应该熟悉从查询结果创建表的方法。这里是对该方法的回顾。当从查询结果创建表时：

*   新表由 `FROM` 子句中引用的一个或多个表或视图的数据填充
*   新表包含查询 `SELECT` 子句中指定的列
*   新表的列具有与所选列相同的列属性（类型、长度、信息和格式）

注意：在创建表时，如果您没有为计算列指定列名，SAS 会分配一个列名，例如 `_TEMA001`。当在 `CREATE TABLE` 语句中使用查询子句时，该查询的自动报告生成将关闭。仅生成新表作为输出。

## 示例




假设你想创建一个新的临时表，其中包含航空公司雇佣票务员的数据。你需要的数据是两个现有表 `Sasuser.Payrollmaster` 和 `Sasuser.Staffmaster` 中包含数据的子集。以下 `PROC SQL` 步骤根据对这两个现有表进行查询的结果创建新表 `Work.Ticketagents`。`WHERE` 子句通过匹配 `EMPID` 连接表，并选择 `JobCode` 包含 `TA` 的员工行子集。

```
proc sql;
   create table work.ticketagents as
      select lastname, firstname,
             jobcode, salary
         from sasuser.payrollmaster,
              sasuser.staffmaster
         where payrollmaster.empid
               = staffmaster.empid
               and jobcode contains 'TA';
```

注意：由于此查询在 `FROM` 子句中列出了两个表并根据 `WHERE` 子句对行进行筛选，因此该查询实际上是一个 `PROC SQL` 内连接。新表 `Work.Ticketagents` 不是空的；它包含了数据行。因此，你可以提交一个 `SELECT` 语句将 `Work.Ticketagents` 显示为报告：

```
select *
   from work.ticketagents;
```

`Work.Ticketagents` 的前四行所示。![Work.Ticketagents](img/m73-13-g1.png) SAS 日志还显示了一条消息，表示表已创建。

表 5.11 SAS 日志

|  |

```
NOTE: Table WORK.TICKETAGENTS created, with 41 rows and 4 columns.
```

| |

## 复制表

要快速复制表，可以使用 `CREATE TABLE` 语句配合查询，该查询应返回整个表，而不是列和行的子集。`CREATE TABLE` 语句应仅包含以下子句：

*   一个 `SELECT` 子句，指定选择源表中的所有列
*   一个 `FROM` 子句，指定源表

注意：请记住，除非使用 `ORDER BY` 子句，否则 `PROC SQL` 查询结果中的行顺序是无法保证的。因此，不带 `ORDER BY` 子句的 `CREATE TABLE` 语句可以创建一个包含与原表相同行的表，但行的顺序可能不同。

## 示例

以下 `PROC SQL` 步骤创建新表 `Work.Supervisors2`，它是源表 `Sasuser.Supervisors` 的完全副本：

```
proc sql;
   create table work.supervisors2 as
      select *
         from sasuser.supervisors;
```

两个表的前四行如下所示。图 5.1 源表：`Sasuser.Supervisors`![Sasuser.Supervisors](img/m73-14-g1.png) 图 5.2 新表：`Work.Supervisors2`![Work.Supervisors2](img/m73-14-g2.png)

### 向表中插入数据行

## 概述

在创建空表后，你将想要插入数据行。你可能还想向已经包含数据的表中插入额外的数据行。你可以通过三种方式使用 `INSERT` 语句向现有表（空或已填充）插入数据行。注意：你还可以使用 `INSERT` 语句向 `PROC SQL` 视图底层的单个表中插入数据行。要了解更多关于 `PROC SQL` 视图的信息，请参阅 使用 PROC SQL 创建和管理视图。

| 插入行的方法 | 示例 |
| --- | --- |
| 使用 `SET` 子句按列名插入值 |  |

```
proc sql;
    insert into work.discount
       set destination='LHR',
           begindate='01MAR2000'd,
           enddate='05MAR2000'd,
           discount=.33
```

*(注：原文后半部分存在大量重复和乱码，已根据核心逻辑进行了清理和翻译处理。)*




| ![通过 Set 子句插入行的输出](img/m73-17-g1.png) |

## 使用 VALUES 子句插入行

`INSERT` 语句使用 `VALUES` 子句将一组值插入到表中。与 `SET` 子句不同，`VALUES` 子句不为每个值指定列名，因此必须按照正确的顺序列出这些值。值必须按照列在表中出现的顺序进行指定，或者如果指定了可选的列列表，则按照列在列表列表中出现的顺序指定。向添加到表的每行都使用一个单独的 `VALUES` 子句。

包含 `VALUES` 子句的 `INSERT` 语句的一般形式：`INSERT INTO table-name <(target-column-1<, ... target-column-n)>VALUES (value-1<, ... value-n)><... VALUES (value-1<, ... value-n>)>;`

以下是语法的解释：
- `table-name`：指定插入行的表名。
- `target-column`：指定要插入数据的列名。
- 每个 `VALUES` 子句：列出要插入某行某些或所有列的值，用括号括起来。多个 `VALUES` 子句之间不用逗号分隔。
- `values`：指定要添加的数据值。字符值必须包含在引号中。多个值必须用逗号分隔。值必须按位置顺序列出，要么按照它们在表中出现的顺序，要么如果指定了可选列列表，按照它们在列列表中出现的顺序。

注意：在包含 `VALUES` 子句的 `INSERT TABLE` 语句中，在表名后包含目标列名列表是可选的。列表可以包含表中所有或部分列名。如果指定了可选的目标列名列表，则语句仅为这些列赋值。目标列可以按任何顺序列出，无论它们在表中的位置如何。表中存在但未列出的任何列在插入行中将被赋予缺失值。你可以使用 `VALUES` 子句为表的所有或部分列插入值。

| 如果你想做 ... | 那么 ... | 示例 |
| --- | --- | --- |
| 为表中的所有列插入一个值 | 你可以在 `INSERT` 语句中省略可选的列名列表。`PROC SQL` <br>* 按值在 `VALUES` 子句中指定的顺序读取值 <br>* 按列在表中出现的顺序将值插入列中。 | ```sql
insert into work.newtable
    values ('WI','FLUTE',6)
    values ('ST','VIOLIN',3);
`````` |
| 为表中的部分列插入一个值 | 你必须在 `INSERT` 语句中包含一个列名列表。`PROC SQL` <br>* 按值在 `VALUES` 子句中指定的顺序读取值 <br>* 按列在列名列表中指定的顺序将值插入列中。 | ```sql
insert into work.newtable
        (item,qty)
    values ('FLUTE',6)
    values ('VIOLIN',3);
`````` |

你必须为 `PROC SQL` 插入值的每个列列出一个值（如在表列表或可选列名列表中指定的）。若要指定某个值是缺失，对于字符值请使用用单引号括起的空格，对于数值值请使用句号。例如，以下 `VALUES` 子句指定了要插入三个列的值；其中前两个值是缺失的：

```sql
values (' ', ., 45)
```

在此示例中，指定的第一个值是字符列的缺失值，第二个值是数值列的缺失值。

## 示例

假设你想向 `Work.Discount` 表中再插入两行，该表存储了 3 月份某些航班目的地时间段的航空公司折扣。在上一节中，你使用 `SET` 子句向 `Work.Discount` 插入了两行，因此表现在现在表所示。![Work.Discount](img/m73-20-g1.png) 使用 `VALUES` 子句再添加两行。以下 `PROC SQL` 步骤向 `Work.Discount` 添加了两行新数据，并生成显示更新后表的报告：

```sql
proc sql;
   insert into work.discount (destination, 
          begindate,enddate,discount)
      values ('ORD','05MAR2000'd,'15MAR2000'd,.25)
      values ('YYZ','06MAR2000'd,'20MAR2000'd,.10);
   select *
      from work.discount;
```

![Work.Discount](img/m73-20-g2.png) 刚刚使用 `VALUES` 子句插入的两行是上面的第三行和第四行。你可能注意到此示例中的 `INSERT` 语句包含了一个可选的列名列表。在此示例中，数据被插入到表的所有列中，且值按照列在表中出现的顺序列出，因此没有严格需要使用列列表。然而，包含列名列表使代码更易读，更容易理解代码在做什么。

## 从查询结果插入行

向表中插入数据行最快的方法是使用查询从一个或多个表（或视图）中选择行，并插入另一个表。当你向已包含行的表中添加行时，新行位于最后。若要从查询结果插入行，使用 `INSERT` 语句，它包含 `SELECT`、`FROM` 以及任何可选子句（如 `ORDER BY`）。查询结果的值将按列在表中出现的顺序插入，或者，如果指定了可选列列表，则按列在列列表中出现的顺序插入。

包含查询子句的 `INSERT` 语句的一般形式：`INSERT INTO table-name <(target-column-1<, ... target-column-n)>SELECT column-1<, ... column-n>FROM table-1 ... view-n><optional query clauses>;`

以下是语法的解释：
- `table-name`：指定插入行的表名。
- `target-column`：指定插入数据的列名。
- `SELECT`：指定要插入的列。
- `FROM`：指定要查询的表或视图。
- `optional query clauses`：用于精炼查询。包括 `WHERE`、`GROUP BY` 和 `HAVING` 子句。

注意：在包含查询子句的 `INSERT TABLE` 语句中，在表名后包含目标列名列表是可选的。列表可以包含表中所有或部分列名。如果指定了可选的目标列名列表，则语句仅为这些列赋值。目标列可以按任何顺序列出，无论它们在表中的位置如何。表中存在但未列出的任何列在插入行中将被赋予缺失值。

## 示例

公司的一名机械师从 2 级升到了 3 级，你需要将该员工添加到 `Sasuser.Mechanicslevel3` 表，该表列出了所有 3 级机械师。创建一个 `Sasuser.Mechanicslevel3` 的临时副本 `Work.Mechanicslevel3_New`，并在报告中显示新表：

```sql
proc sql;
   create table work.mechanicslevel3_new as
      select *
         from sasuser.mechanicslevel3;
```

| ![Work.Mechanicslevel3_New 表](img/m73-22-g1.png) |

接下来，你向 `Work.Mechanicslevel3_New` 插入一个新的 3 级员工，其 `EmpID` 为 `1653`。该员工目前列在 `Sasuser.Mechanicslevel2` 中，因此你的 `INSERT` 语句查询 `Sasuser.Mechanicslevel2` 表。你的 `PROC SQL` 步骤以 `SELECT` 语句结束，将修改后的表 `Work.Mechanicslevel3_New` 输出到报告。

```sql
proc sql; 
   insert into work.mechanicslevel3_new
      select empid, jobcode, salary 
         from sasuser.mechanicslevel2
         where empid='1653';
      select *
         from work.mechanicslevel3_new;
```





| ![Revised Work.Mechanicslevel3_New Table](img/m73-22-g2.png) |

你插入到 `Work.Mechanicslevel3_New` 中的行是上面的第 8 行。如你所示，新员工的 `JobCode` 和 `Salary` 值必须更改。更新表中的现有值将在本章稍后介绍。注意：虽然新行显示在表的底部，但如果没有使用 `ORDER BY` 子句，则无法保证 `PROC SQL` 查询中行的顺序。

### 创建具有完整性约束的表

## 概述

完整性约束是你可以指定的规则，用以限制表中列中可以存储的数据值。当添加、更新或删除与列关联的值时，SAS 会强制完整性约束。完整性约束有助于你维护数据的有效性和一致性。你可以使用 `PROC SQL` 或 `PROC DATASETS` 创建完整性约束。`PROC DATASETS` 只能为现有表分配约束。`PROC SQL` 可以在创建新表时或修改现有表时分配约束。本章讨论了使用 `PROC SQL` 在创建表时创建完整性约束。注意：要了解更多关于使用 `PROC DATASETS` 创建完整性约束的信息，请参见修改 SAS 数据集和跟踪更改。有关完整性约束的更多信息，请参见 SAS 文档。注意：使用 `PROC SQL` 向现有表添加完整性约束，请使用 `ALTER TABLE` 语句。当你对表设置完整性约束时，需要指定要创建的约束类型。每个约束都有不同的操作。

| 约束类型 | 操作 |
| --- | --- |
| CHECK | 确保特定的值或范围是列中的唯一值。它还可以根据同一行内另一列的值检查一列值的有效性。 |
| NOT NULL | 保证列每一行都有非空值。 |
| UNIQUE | 强制列值的唯一性。 |
| PRIMARY KEY | 唯一地定义表中的行，可以是单列或一组列。表只能有一个 `PRIMARY KEY`。`PRIMARY KEY` 包含了 `NOT NULL` 和 `UNIQUE` 约束的属性。 |
| FOREIGN KEY | 通过匹配一个表中的列或一组列（`FOREIGN KEY`）与另一个表中的 `PRIMARY KEY`，将表中的一个或多行链接到另一个表的特定行。这种父子关系限制了对 `PRIMARY KEY` 和 `FOREIGN KEY` 约束的修改。`FOREIGN KEY` 接受的值只有 `PRIMARY KEY` 的值或缺失值。 |

注意：当你向数据的表中添加完整性约束时，SAS 会在添加约束之前检查所有数据值，以确定它们是否满足约束。你有两种方式使用完整性约束：通用约束和引用约束。通用约束允许你限制单个表中列接受的数据值。引用约束允许你将一个表中列的数据值链接到另一个表中列的数据值。

## 通用完整性约束

通用完整性约束允许你限制单个表内列的值。以下四个完整性约束可以作为通用完整性约束使用：

* `CHECK`
* `NOT NULL`
* `UNIQUE`
* `PRIMARY KEY`

注意：如果 `PRIMARY KEY` 约束没有任何引用它的 `FOREIGN KEY` 约束，则它是一个通用完整性约束。用通用约束使用的 `PRIMARY KEY` 是分配 `NOT NULL` 和 `UNIQUE` 约束的快捷方式。

## 引用完整性约束

当一个表中的 `PRIMARY KEY` 完整性约束被另一个表中的 `FOREIGN KEY` 完整性约束引用时，就会创建引用完整性约束。创建引用完整性约束必须遵循两个步骤：

1. 在第一个表上定义 `PRIMARY KEY` 约束。
2. 在其他表上定义 `FOREIGN KEY` 约束。

注意：完整性约束
* 符合 ANSI 标准
* 无法为视图定义
* 无法为生成数据集的历史版本定义。

要创建一个具有完整性约束的表，请使用同时指定列和约束的 `CREATE TABLE` 语句。在 `CREATE TABLE` 语句中指定完整性约束有两种方法：

* 在列规范中
* 作为单独的约束规范。

你可以在同一个 `CREATE TABLE` 语句中使用这两种方法中的一种或两者。

## 在列规范中创建约束

在本章前面，你学习了如何使用包含列规范的 `CREATE TABLE` 语句创建表：
```
CREATE TABLE table-name(column-specification-1<,...column-specification-n>);
```
你还学习了列规范由这些元素组成：`column-definition <column-constraint-1<, ... column-constraint-n>> <MESSAGE='message-string' <MSGTYPE=message-type>>`

早期示例中使用的列规范仅包含列定义。现在我们学习如何通过在列规范中指定可选的列约束来创建列创建完整性约束：

| 列规范中列-约束的通用形式：`column-definition <column-constraint-1<, ... column-constraint-n>><MESSAGE='message-string' <MSGTYPE=message-type>>` |

以下是语法的解释：`column-constraint` 是以下内容之一：
* `CHECK (expression)`：指定表中的所有行（在 `CREATE TABLE` 语句中指定）都满足表达式，该表达式可以是任何有效的 where 表达式。
* `DISTINCT`：指定列中的值必须是唯一的。这与 `UNIQUE` 相同。
* `NOT NULL`：指定列不包含空或缺失值，包括特殊的缺失值。
* `PRIMARY KEY`：指定该列为 `PRIMARY KEY`，即不包含缺失值的列。
* `REFERENCES table-name <ON DELETE referential-action> <ON UPDATE referential-action>`：指定该列为 `FOREIGN KEY`，即其值链接到另一个表（`REFERENCES` 指定的）中的 `PRIMARY KEY` 列。当引用的 `PRIMARY KEY` 列被更新或删除时会执行引用操作。referential-action 指定对所有匹配的 `FOREIGN KEY` 值的操作类型，它是以下之一：
    * `CASCADE`：允许更新 `PRIMARY KEY` 数据值，并将匹配的 `FOREIGN KEY` 更新为相同的值。注意：此引用操作目前支持更新。
    * `RESTRICT`：仅当存在匹配的 `FOREIGN KEY` 值时发生。此引用操作是默认值。
    * `SET NULL`：将所有匹配的 `FOREIGN KEY` 值设置为 `NULL`。
* `UNIQUE`：指定列的值在表内必须是唯一的。 |

注意：可选的 `MSGTYPE=` 和 `MESSAGE=` 元素将在本章稍后讨论。与列一样，完整性约束在表中必须具有唯一名称。如果你通过在列规范中指定列约束来创建完整性约束，SAS 会为约束分配名称。约束的形式取决于约束的类型，如下：

| 约束类型 | 默认名称 |
| --- | --- |
| `CHECK` | `_CKxxxx_` |
| `FOREIGN KEY` | `_FKxxxx_` |
| `NOT NULL` | `_NMxxxx_` |
| `PRIMARY KEY` | `_PKxxxx_` |
| `UNIQUE` | `_UNxxxx_` |

注意：`xxxx` 是从 `0001` 开始的计数器。这是一个 `PROC SQL` 步骤的示例，它通过在列规范中指定一个或多个列约束来创建完整性约束。

## 示例





假设你需要创建一个 `Work.Employees` 表，用于存储所有员工的识别号、姓名、性别和入职日期。此外，你还希望确保以下几点：

* `ID` 列只包含非缺失且唯一的值
* `Gender` 列只包含值 `M` 和 `F`

下文的 `PROC SQL` 步骤创建了表 `Work.Employees` 表，该表包含四列，并对其中两列建立了完整性约束：

```
proc sql;
   create table work.employees
      (ID char (5) primary key,
      Name char(10),
      Gender char(1) not null check(gender in ('M','F')),
      HDate date label='Hire Date');
```

在 `ID` 的列规格中，`PRIMARY KEY` 列约束确保 `ID` 列只包含非缺失且唯一的值。`Gender` 的列规格定义了两个完整性约束：

* `NOT NULL` 列约束确保 `Gender` 的值是非缺失的。
* `CHECK` 列约束确保 `Gender` 的值满足表达式 `gender in ('M','F')`。

另一种创建完整性约束的方法是：在 `CREATE TABLE` 语句中指定约束规格。

## 使用约束规格创建约束

有时你可能倾向于在列规格之外创建完整性约束，通过在 `CREATE TABLE` 语句中指定单个约束规格来实现：`CREATE TABLE table-name(column-specification-1<,...column-specification-n><,constraint-specification-1><,...constraint-specification-n>);`。`CREATE TABLE` 语句中的第一个规格必须是列规格。然而，在语句初始列规格之后，你可以包含多个额外的列规格、约束规格或两者兼有。第一个列规格之后的所有规格都可以以任何顺序列出。列规格和约束规格的完整列表遵循与之前介绍列规格的相同准则：

* 整个列规格和约束规格集必须包含在括号内。
* 多个列规格和约束规格之间必须用逗号分隔。

在列规格内指定完整性约束与通过单独的约束规格指定完整性约束之间，有几点重要的区别。使用约束规格具有以下优势：

* 你可以为约束指定名称。事实上，你必须指定一个名称，因为 SAS 不会自动分配名称。
* 对于某些约束类型，你可以在单个规格中为多个列定义约束。

约束规格的语法所示：`CONSTRAINT constraint-name constraint <MESSAGE='message-string' <MSGTYPE=message-type>>`。这为正在指定的约束指定一个名称。该名称必须是有效的 SAS 名称。注意：`PRIMARY`、`FOREIGN`、`MESSAGE`、`UNIQUE`、`DISTINCT`、`CHECK` 和 `NOT` 不能作为 `constraint-name` 的值。`constraint` 是以下之一：

* `CHECK (expression)` 指定 `table-name`（在 `CREATE TABLE` 语句中指定）中的所有行都满足 `expression`，该表达式可以是任何有效的 `where-expression`。
* `DISTINCT (column-1<, ... column-n>)` 指定每列的值的值在表内必须是唯一的。此约束与 `UNIQUE` 相同。
* `FOREIGN KEY (column-1<, ... column-n>)REFERENCES table-name<ON DELETE referential-action><ON UPDATE referential-action>` 指定一个 `FOREIGN KEY`，即一组列，其值与另一个表（为 `REFERENCES` 指定的表名）中 `PRIMARY KEY` 列的值相关联。当被 `FOREIGN KEY` 引用的 `PRIMARY KEY` 列的值被更新或删除时，会执行 `referential-actions`。`referential-action` 指定了在所有匹配的 `FOREIGN KEY` 值上执行的操作类型，如下所示：
    * `CASCADE` 允许 `PRIMARY KEY` 数据值被更新，并将 `FOREIGN KEY` 中的匹配值更新为相同的值。注意：此引用操作目前仅支持更新。
    * `RESTRICT` 仅在存在匹配的 `FOREIGN KEY` 值时发生。此引用操作是默认操作。
    * `SET NULL` 将所有匹配的 `FOREIGN KEY` 值设置为 `NULL`。
* `NOT NULL (column)` 指定列不包含空值或缺失值，包括特殊缺失值。
* `PRIMARY KEY (column-1<, ... column-n>)` 指定一个或多个列为 `PRIMARY KEY` 列，即不包含缺失值且值是唯一的列。
* `UNIQUE (column-1<, ... column-n>)` 指定每列的值在表内必须是唯一的。此约束与 `DISTINCT` 相同。
* `MESSAGE=` 指定一个 `message-string`，用于指定当完整性约束不满足时写入 SAS 日志的错误消息文本。`message-string` 的最大长度为 250 个字符。
* `MSGTYPE=` 指定 `message-type`，用于指定当完整性约束不满足时错误消息在 SAS 日志中的显示方式。`message-type` 是以下之一：

| Value | 描述 |
| :--- | :--- |
| NEWLINE | 除了该完整性约束的默认错误消息外，还会显示为 `MESSAGE=` 指定的文本 |
| USER | 仅显示为 `MESSAGE=` 指定的文本 |

注意：`constraint-specification` 内的元素必须用空格分隔。你可能已经注意到创建完整性约束的两种方法的另一种区别。当你使用列规格创建 `FOREIGN KEY` 完整性约束时，除了 `REFERENCES` 关键字外，还需要使用 `FOREIGN KEY` 关键字。这是一个使用列规格创建约束的示例。

## 示例

在本章之前的示例中，创建了 `Discount` 表存储航空公司提供的折扣数据。假设你现在希望该表

* 只持有小于等于 .5 的折扣
* 不允许 Destination 有缺失值

创建一个 `Discount` 表的新版本，命名为 `Discount3`，包含两个完整性约束。一个完整性约束限制了 Discount 列的值，另一个防止输入缺失值。以下 `PROC SQL` 步骤通过指定四列和两个完整性约束创建了 `Discount3`：

```
proc sql;
   create table work.discount3 
          (Destination char(3),
          BeginDate num Format=date9.,
          EndDate num format=date9.,
          Discount num,
          constraint ok_discount check (discount <= .5),
          constraint notnull_dest not null(destination));
```


在本章的节节中，使用了以下 `PROC SQL` 步骤创建了表 `Work.Discount3`，该表包含两个完整性约束，一个针对 `Discount` 列，另一个针对 `Destination` 列：

```
proc sql;
   create table work.discount3 
          (Destination char(3),
          BeginDate num Format=date9.,
          EndDate num format=date9.,
          Discount num,
          constraint ok_discount check (discount le .5),
          constraint notnull_dest not null(destination));
```

该表尚未包含任何行数据，因此添加一些数据。以下 `INSERT` 语句使用 `VALUES` 子句向表中添加了两个行数据：

```
proc sql;
   insert into work.discount3 
          values('CDG','03MAR2000'd,'10MAR2000'd,.15)
          values('LHR','10MAR2000'd,'12MAR2000'd,.55);
```

当提交此 `PROC SQL` 步骤时，SAS 日志中会显示以下信息。

表 5.14 SAS 日志

|  

```
ERROR: Add/Update failed for data set WORK.DISCOUNT3 
because data value(s) do not comply with integrity constraint 
ok_discount.
NOTE: This insert failed while attempting to add data from 
VALUES clause 2 to the data set.
NOTE: Deleting the successful inserts before error noted above 
to restore table to a consistent state.
```

 |

此消息的三个部分解释了问题所在：

*   错误信息表示尝试添加行的操作失败。`Discount` 的一个或多个数据值不符合完整性约束 `OK_DISCOUNT`，该约束规定 `Discount` 列中的值必须小于或等于 `.5`。

*   第一条注释表明第二个 `VALUES` 子句存在问题。该子句为 `Discount` 列指定了值 `.55`，这不符合规定。注意：即使有多个 `VALUES` 子句指定了不符合规定的数据值，SAS 日志也只会列出违反约束的第一个 `VALUES` 子句。

*   第二条注释表明 SAS 在发生错误之前正在“删除成功的插入”。尽管所有其他指定的数据都是有效的，但没有任何数据被添加到表中。

我们需要考虑为什么 SAS 阻止了任何数据添加到表中。

## 使用 `UNDO_POLICY=` 选项控制 UNDO 处理

当你使用 `INSERT` 或 `UPDATE` 语句向表中添加或修改数据时，如果在插入或更新过程中发生任何错误，你可以控制 `PROC SQL` 如何处理更新后的数据。你可以在 `PROC SQL` 语句中使用 `UNDO_POLICY=` 选项来指定 `PROC SQL` 是否接受或撤销你截至错误发生时提交的更改。你可以为 `UNDO_POLICY=` 选项指定以下值之一。

| `UNDO_POLICY=` 设置 | 描述 |
| --- | --- |
| `REQUIRED` | `PROC SQL` 对 `INSERT` 和 `UPDATE` 语句执行 `UNDO` 处理。如果无法可靠地执行 `UNDO` 操作，`PROC SQL` 将不执行语句并发布 `ERROR` 消息。这是 `PROC SQL` 的默认值。 |
| `NONE` | `PROC SQL` 跳过无法插入或更新的记录，并在 SAS 日志中写入类似于 `PROC APPEND` 写入的警告信息。 |
| `OPTIONAL` | 如果可以，`PROC SQL` 执行 `UNDO` 处理。如果无法可靠地执行 `UNDO` 操作，`PROC SQL` 将不执行语句并发布 `ERROR` 消息。 |





有时，你想向表中添加数据，但你不确定该表具有哪些完整性约束（如果有的话）。要仅显示指定表的完整性约束，请使用 `DESCRIBE TABLE CONSTRAINTS` 语句。（在本章之前讨论的 `DESCRIBE TABLE` 语句会在 SAS 日志中同时列出 `CREATE TABLE` 语句和表的完整性约束。）注意：某些版本的 SAS 会在输出和 SAS 日志中同时显示有关完整性约束的信息。

| `DESCRIBE TABLE CONSTRAINTS` 语句的通用形式： | `DESCRIBE TABLE CONSTRAINTS table-name-1<, ... table-name-n>;` | 以下是该语法的解释：`table-name` 指定要描述的表，可以是以下内容之一：<ul><li>一个单级名称</li><li>一个双级库引用（libref）和表名。</li><li>一个用单引号括起来的物理路径名。</li></ul>

## 示例

要仅显示之前创建的表 `Work.Discount4` 的表约束，你提交以下 `PROC SQL` 步骤：

```
proc sql;
   describe table constraints work.discount4;
```

表 5.16 SAS 日志

```
NOTE: SQL table WORK.DISCOUNT4 ( bufsize=4096 ) has the 
following integrity constraint(s):

-----Alphabetic List of Integrity Constraints-----

      Integrity                            Where
   *  Constraint    Type      Variables    Clause
-------------------------------------------------
1     notnull_dest Not Null Destination
2     ok_discount Check Discount<=0.5
```

![Work.Discount4](img/m73-35-g1.png)所示，`Work.Discount4` 有两个完整性约束：`NotNull_Dest` 和 `OK_Discount`。

# 更新现有表行

## 概述

要修改表中或所有现有行的数据值，你在 `PROC SQL` 中使用 `UPDATE` 语句。在 `UPDATE` 语句中，对于你想要修改的行的每一列，你需要指定一个表达式来指示应如何修改这些值。例如，以下表达式表示 `Units` 列的值应乘以 4：

```
units=units*4
```

你可以通过两种主要方法使用 `UPDATE` 语句。

| 更新表的方法 | 示例 |
| --- | --- |
| 使用相同的表达式更新某一列中的所有（或子集）行 | ```sql
proc sql;
   update work.payrollmaster_new
      set salary=salary*1.05
      where jobcode like '__1';
``` ``` |
| 使用不同的表达式更新同一列中不同的行 | ```sql
proc sql;
   update  work.payrollmaster_new 
      set salary=salary*
         case when substr(jobcode,3,1)='1'
                 then 1.05
              when substr(jobcode,3,1)='2'
                 then 1.10
              when substr(jobcode,3,1)='3'
                 then 1.15
              else 1.08
         end;
``` ``` |

注意：`UPDATE` 语句不会向表中插入新行。要插入行，必须使用 `INSERT` 语句。注意：你也可以使用 `UPDATE` 语句更新 `PROC SQL` 视图底层表中的现有值。详情，请参阅 使用 PROC SQL 创建和管理视图。我们考虑了更新表中现有行的这些每方法。

## 使用相同表达式更新行

要使用相同的表达式更新某一列中的所有（或子集）行，请使用包含 `SET` 子句和可能的 `WHERE` 子句的 `UPDATE` 语句。

| 更新表行的基本 `UPDATE` 语句通用形式： | `UPDATE table-name SET column-1=expression<, ... column-n=expression><WHERE expression>;` | 以下是该语法的解释：`table-name` 指定更新值的表名。`SET` 指定要更新的一个或多个列名对，以及指示如何更新每列的表达式。`WHERE` 用于指定一个用于筛选更新行子集的表达式。 |

警告：如果你只想更新表中的子集行，必须指定 `WHERE` 子句或表中要更新的所有行。

## 示例

假设一家公司正在考虑给所有 1 级员工加薪 5% 员工的薪资存储在 `Sasuser.Payrollmaster` 表中。你不想更新原始表，因此创建了 `Sasuser.Payrollmaster` 的临时副本，称为 `Work.Payrollmaster_New`。以下 `PROC SQL` 步骤根据查询结果创建了 `Work.Payrollmaster_New` 并生成新表的输出报告：

```
proc sql;
   create table work.payrollmaster_new as
      select *
         from sasuser.payrollmaster;
   select *
      from work.payrollmaster_new;
```

下面显示了更新薪资的表 `Work.Payrollmaster_New` 的前 10 行。![Work.Payrollmaster_New](img/m73-38-g1.png)接下来，你编写了一个 `PROC SQL` 步骤来更新指定的行。`UPDATE` 语句包含以下两个部分：

*   一个 `SET` 子句，指定用于更新 `Salary` 的表达式
*   一个 `WHERE` 子句，指定要更新的子集行（1 级员工）

```
proc sql;
   update work.payrollmaster_new
      where jobcode like '__1';
```

最后，你可以使用 `SELECT` 语句显示更新后的表。显示 `Work.Payrollmaster_New` 的前 10 行（已更新）如下所示。如果你想增加所有薪资，只需从 `UPDATE` 语句中删除 `WHERE` 子句：

```
proc sql;
   update payrollmaster_new
      set salary=1.05
```

## 使用不同表达式更新行

有时，你想使用不同的表达式来修改不同子集的值。例如，不是给 1 级员工加薪 5%，你可能还想给 2 级员工加薪 10%，此类推，对每个组使用不同的加薪百分比。使用不同表达式更新不同子集有两种方法。

| 更新表的方法 | 示例 |
| --- | --- |
| 使用多个 `UPDATE` 语句子集行由于单个 `UPDATE` 语句只能包含一个 `WHERE` 子句，因此需要多个 `UPDATE` 语句为多个子集指定表达式 | ```sql
proc sql;
   update work.payrollmaster_new
      set salary=salary*1.05
         where substr(jobcode,3,1)='1';
   update work.payrollmaster_new
      set salary=salary*1.10
         where substr(jobcode,3,1)='2';
   update work.payrollmaster_new
      set salary=salary*1.15
         where substr(jobcode,3,1)='3';
``` ``` |
| 使用一个包含 `CASE` 表达式的单个 `UPDATE` 语句 | ```sql
proc sql;
   update work.payrollmaster_new 
      set salary=salary*
         case 
              when substr(jobcode,3,1)='1'
                 then 1.05
              when substr(jobcode,3,1)='2'
                 then 1.10
              when substr(jobcode,3,1)='3'
                 then 1.15
              else 1.08
         end;
``` ``` |

第一种方法（使用多个 `UPDATE` 语句）非常繁琐，因为 `SET` 语句和表达式在每个 `UPDATE` 语句中重复。在这个示例中，第一种方法的效率很低，因为必须读取三次 `Work.Payrollmaster_New` 表。第二种方法（使用条件处理——`CASE` 表达式）是推荐的。我们现在考虑第二种方法。





# CASE 表达式

通用形式，CASE 表达式：`CASE <case-operand>WHEN when-condition THEN result-expression<...WHEN when-condition THEN result-expression><ELSE result-expression>END;`

以下是该语法的解释：
- `CASE` 执行条件处理。
- `case-operand` 是一个可选表达式，它解析为一个表列，其值将与所有 `when-conditions` 进行比较。
- `WHEN` 指定一个 `when-condition`，这是一种简短的表达式，它假设 `case-operand` 为其操作数之一，并解析为真或假。
- `THEN` 指定一个 `result-expression`，这是一个解析为特定值的表达式。
- `ELSE` 指定一个 `result-expression`，当没有 `when-conditions` 被执行时，它将提供一个备选操作。
- `END` 表示 `CASE` 表达式的结束。

**注意**：虽然 `ELSE` 子句是可选的，但强烈建议使用它。如果你省略了 `ELSE` 子句，则对于未在任何 `WHEN` 子句中描述的行，其正在更新的列都将接收缺失值（missing value）。

**备注**：你还可以在 `INSERT` 和 `SELECT` 语句中使用 `CASE` 表达式。

## 示例

在下面的 `UPDATE` 语句中，`CASE` 表达式包含三个 `WHEN-THEN` 子句，指定了表 `Work.Insure_New` 中三个不同的行子集：

- 由 Acme 保险的房屋
- 由 Reliable 保险的房屋
- 由 Homelife 保险的房屋

```sql
update work.insure_new
   set pctinsured=pctinsured*
      case 
         when company='ACME' 
              then 1.10
         when company='RELIABLE' 
              then 1.15
         when company='HOMELIFE' 
              then 1.25 
         else 1 
      end;
```

`PROC SQL` 会根据相应的 `WHEN-THEN`（或 `ELSE`）子句不同地更新每个指定的行子集。

## PROC SQL 如何根据 CASE 表达式更新行

当你指定一个 `CASE` 表达式时，`PROC SQL` 按如下方式更新每行：

1. 在 `CASE` 表达式中，`PROC SQL` 找到包含该行匹配条件的 `WHEN-THEN` 子句。
2. 随后，`CASE` 表达式将匹配的 `WHEN-THEN` 子句的结果返回给 `SET` 子句。返回的值完成了 `SET` 子句中的表达式。
3. `SET` 子句使用完成后的表达式更新当前行中指定列的值。

`CASE` 表达式之所以高效，是因为 `PROC SQL` 处理 `WHEN-THEN` 子句的方式。`CASE` 表达式中的 `WHEN-THEN` 子句是顺序评估的。当找到匹配的情况时，会评估并设置 `THEN` 表达式，并且不再考虑剩余的 `WHEN` 情况。

## Case 操作数的工作原理

在接下来的几节中，你将学习在 `UPDATE` 语句中使用 `CASE` 表达式，包括带有和不带可选操作数：`CASE <case-operand>`

## 使用不带 Case 操作数的 CASE 表达式更新行

这是一个使用 `CASE` 表达式进行条件处理的 `UPDATE` 语句示例。该示例展示了不包含可选操作数的 `CASE` 表达式形式。

## 示例

假设一家公司正在考虑给所有员工加薪，每个级别的员工加薪比例不同：

- level-1 员工获得 5% 的加薪
- level-2 员工获得 10% 的加薪
- level-3 员工获得 15% 的加薪

首先，你创建一个临时表 `Work.Payrollmaster3`，它是包含员工工资数据的表 `Sasuser.Payrollmaster` 的副本。`Work.Payrollmaster3` 的前 10 行所示：![Work.Payrollmaster3](img/m73-43-g1.png)

接下来，你创建一个 `PROC SQL` 步骤，使用包含 `SET` 子句和 `CASE` 表达式的 `UPDATE` 语句来更新行：

```sql
proc sql;
   update work.payrollmaster3
      set salary=salary*
         case 
            when substr(jobcode,3,1)='1'
                 then 1.05
            when substr(jobcode,3,1)='2'
                 then 1.10
            when substr(jobcode,3,1)='3'
                 then 1.15
            else 1.08
         end;
```

在此示例中，`CASE` 表达式包含三个 `WHEN` 子句，每个对应一个行子集（level-1、level-2 和 level-3 员工），随后跟一个 `ELSE` 子句以处理任何不符合预期条件的行。更新后，`Work.Payrollmaster3` 的前 10 行所示：![Work.Payrollmaster3](img/m73-43-g2.png)

通过比较 `Work.Payrollmaster3` 原始版本和更新版本的 `Salary` 值（如上所示），你可以看到值是如何根据 `JobCode` 中指示的职位级别发生变化的。

## 使用带有 Case 操作数的 CASE 表达式更新行

如果 `SET` 子句中的表达式使用了等号（`=`）比较运算符，你可能会在 `CASE` 表达式中使用可选的操作数。考虑前面的 `PROC SQL` 步骤，查看如何使用可选操作数来重写 `UPDATE` 语句中的 `CASE` 表达式。

## 示例

在下面的 `PROC SQL` 步骤中，`CASE` 表达式包含三个 `WHEN-THEN` 子句，每个子句对应一个行子集，使用了相同的 `SUBSTR` 函数：

```sql
proc sql;
   update work.payrollmaster3
      set salary=salary*
         case 
            when substr(jobcode,3,1)='1'
                 then 1.05
            when substr(jobcode,3,1)='2'
                 then 1.10
            when substr(jobcode,3,1)='3'
                 then 1.15
            else 1.08
         end;
```

由于 `SET` 子句中的表达式使用了等号（`=`）运算符，你可以使用替代语法来重构 `CASE` 表达式。在替代语法中，`SUBSTR` 函数从每个 `WHEN-THEN` 子句中移除，并放在 `CASE` 关键字之后作为操作数：

```sql
proc sql;
   update work.payrollmaster3
      set salary=salary*
         case substr(jobcode,3,1)
            when '1'
                 then 1.05
            when '2'
                 then 1.10
            when '3'
                 then 1.15
            else 1.08
         end;
```

使用替代语法，`SUBSTR` 函数只被评估一次，因此这种 `PROC SQL` 步骤效率更高。

## 在 SELECT 语句中使用 CASE 表达式

你可以在三种不同的 `PROC SQL` 语句中使用 `CASE` 表达式：`UPDATE`、`INSERT` 和 `SELECT`。在 `SELECT` 语句中，你可以在列定义中使用 `CASE` 表达式为不同的行子集指定值。

## 示例

假设你想创建一个显示员工姓名、职位代码和职位级别的输出报告。你的 `PROC SQL` 查询从 `Sasuser.Staffmaster` 中选择 `LastName` 和 `FirstName`，从 `Sasuser.Payrollmaster` 中选择 `JobCode`。`SELECT` 语句必须将 `JobLevel` 定义为新列，因为它在任何一个表中都不作为单独列存在。你想根据 `jobcode` 末尾的数字来分配 `JobLevel` 的值（预期每个 `JobCode` 值的末尾数字为 `1`、`2` 或 `3`）。为了创建 `JobLevel`，你可以使用 `CASE` 表达式的操作数形式来指定三个可能的条件（加上一个防万一的 `ELSE` 条件）。`PROC SQL` 查询所示：

```sql
proc sql outobs=10;
   select lastname, firstname, jobcode, 
          case substr(jobcode,3,1)
             when '1'
                  then 'junior'
             when '2'
                  then 'intermediate'
             when '3'
                  then 'senior'
             else 'none'
          end as JobLevel
      from sasuser.payrollmaster,
           sasuser.staffmaster
      where staffmaster.empid=
            payrollmaster.empid;
```

| ![PROC SQL Query Output](img/m73-46-g1.png) |





`SELECT` 子句使用 `CASE` 表达式为新 `JobLevel` 列中的每行分配 `junior`、`intermediate`、`senior` 或 `none` 的值。

### 删除表中的行

## 概述
要删除表中的部分或所有行，请使用 `DELETE` 语句。当语句成功执行时，SAS 日志会显示一条消息，指示已删除的行数。

| 删除表中行的 `DELETE` 语句的通用形式： |
`DELETE FROM table-name<WHERE expression>;` 此处是语法的说明：`table-name` 指定要删除行所在的表名。`WHERE` 用于指定一个表达式，以划分要删除的行子集。 |

**注意**：如果您只想删除表中的部分行，则必须指定 `WHERE` 子句，否则表中的所有行都将被删除。
**注意**：您还可以使用 `DELETE` 语句删除 `PROC SQL` 视图底层的基础表中的行。有关关于在 `DELETE` 语句中引用 `PROC SQL` 视图的更多信息，请参阅使用 PROC SQL 创建和管理视图。

## 示例
假设您想要删除所有用尽常飞行计划里程或花费里程超过账户余额的常旅客飞行计划成员的记录。首先，您通过从现有表 `Sasuser.Frequentflyers` 复制部分列来创建临时表 `Work.Frequentflyers2`：

```
proc sql;
   create table work.frequentflyers2 as
      select ffid, milestraveled, 
             pointsearned, pointsused
         from sasuser.frequentflyers;
```

下面显示了 `Work.Frequentflyers2` 的前 10 行![Work.Frequentflyers2](img/m73-48-g1.png)。接下来，您编写了一个 `PROC SQL` 步骤来删除指定的行：

```
proc sql;
   delete from work.frequentflyers2
      where pointsearned-pointsused <= 0;
```

SAS 日志中的消息会告诉您删除了多少行。

表 5.17 SAS 日志
```
NOTE: 13 rows were deleted from WORK.FREQUENTFLYERS2
```

**提示**：要删除表中的所有行，请从 `DELETE` 语句中移除 `WHERE` 子句。

## 修改表中的列

## 概述
您已经看到如何使用 `DELETE` 语句删除表中的行。要添加、删除（移除）或修改表中的列，请使用 `ALTER TABLE` 语句。

| `ALTER TABLE` 语句的通用形式： |
`ALTER TABLE table-name<ADD column-definition-1<, ... column-definition-n>><DROP column-name-1<, ... column-name-n>><MODIFY column-definition-1<, ... column-definition-n>>;` 此处是语法的说明：`table-name` 指定要添加、删除或修改列的表名。必须指定以下子句中的至少 `<ADD, DROP, MODIFY>`：`ADD` 指定要添加的列的一个或多个列定义。`DROP` 指定要删除（移除）的列的一个或多个列名。`MODIFY` 指定要修改的列的一个或多个列定义，其中 `column-definition` 指定要添加或修改的列，其格式如下：`column-name data-type <(column-width)> <column-modifier-1 <...column-modifier-n>>` 在所有三个子句中，多个列定义或列名必须用逗号分隔。 |

**注意**：您无法对视图使用 `ALTER TABLE` 语句。
**注意**：`ALTER TABLE` 语句还支持类似的子句，用于添加、删除和修改现有表中的完整性约束。这些子句在本章中没有讨论。要了解有关添加、删除和修改完整性约束的信息，请参阅 SQL 过程 SAS 文档。考虑使用 `ALTER TABLE` 语句对列可以进行的每种类型的修改。

## 向表中添加列
要向表中添加列，请使用 `ALTER TABLE` 语句中的 `ADD` 子句。`ADD` 子句指定一个或多个列定义。列定义的语法与 `CREATE TABLE` 语句中的相同：`column-name data-type <(column-width)> <column-modifier-1< ...column-modifier-n>>`。然而，在 `ALTER` 语句中，整个列定义组没有包含在括号内。

## 示例
假设您正在处理临时表 `Work.Payrollmaster4`，它是现有表 `Sasuser.Payrollmaster` 的完全副本。`Work.Payrollmaster4` 的前 10 行所示![Work.Payrollmaster4](img/m73-51-g1.png)。随后的 `PROC SQL` 步骤使用 `ALTER TABLE` 语句中的 `ADD` 子句向 `Work.Payrollmaster4` 添加了 `Bonus` 和 `Level` 列：

```
proc sql;
   alter table work.payrollmaster4
      add Bonus num format=comma10.2,
          Level char(3);
```

下面显示带有两个新列的 `Work.Payrollmaster4` 前 10 行![Work.Payrollmaster4](img/m73-51-g1.png)。

## 从表中删除列
要从表中删除（移除）列，请使用 `ALTER TABLE` 语句中的 `DROP` 子句。`DROP` 子句指定一个或多个列名，多个列名用逗号分隔。

## 示例
假设您想从临时表 `Work.Payrollmaster4` 中删除 `Bonus` 和 `Level` 列（这些列是在上一个示例中添加的）。`Work.Payrollmaster4` 的前 10 行所示![Work.Payrollmaster4](img/m73-51-g1.png)。下面的 `PROC SQL` 步骤使用 `ALTER TABLE` 语句中的 `DROP` 子句删除 `Bonus` 和 `Level`：

```
proc sql;
   alter table work.payrollmaster4
      drop bonus, level;
```

下面显示了没有 `Bonus` 和 `Level` 的 `Work.Payrollmaster4` 前 10 行![Work.Payrollmaster4](img/m73-51-g1)。

## 修改表中的列
要修改表中一个或多个现有列的属性，请使用 `ALTER TABLE` 语句中的 `MODIFY` 子句。您可以使用 `MODIFY` 子句更改：

* `length`（长度）——仅适用于字符列
* `informat`
* `format`
* `label`

**注意**：您无法使用 `MODIFY` 子句执行以下操作：

* 将字符列更改为数值列或反之。要更改列的数据类型，请删除该列并重新添加（数据），或者使用 `DATA` 步骤。
* 更改列名。您无法通过 `ALTER TABLE` 语句更改此属性。相反，可以使用数据集选项 `RENAME=` 或带有 `RENAME` 语句的 `DATASETS` 过程。要了解有关带有 `RENAME` 语句的 `DATASETS` 过程的信息，请参阅创建索引。与 `ADD` 子句一样，`MODIFY` 子句指定一个或多个列定义，每个定义由以下内容组成：`column-name <data-type (column-width)> <column-modifier-1>`。在每个列定义中，您指定必需元素（列名），然后是您想要修改的任何可选属性。**注意**：当您使用 `ALTER TABLE` 语句中的 `ADD` 子句来添加新列，或在 `CREATE TABLE` 语句中指定新列时，`data-type` 是必需元素。然而，当您在 `ALTER TABLE` 语句的 `MODIFY` 子句中使用列定义时（如下例所示），`data-type` 对于数值列始终不是需要的，对于字符列是可选的。只有当您想要修改字符列的宽度时，才必须指定 `data-type (column-width)`。**注意**：在修改字符变量的宽度时，如果长度规格太小，可能会截断变量的值。

```
alter table work.payrollmaster
modify jobcode char(2);
select * from payrollmaster;
```




假设你想修改临时表 `Work.Payrollmaster4` 中现有列 `Salary` 的属性。下面显示了 `Work.Payrollmaster4` 的前 10 行（如上一个示例结束时的状态）。![修改列](img/m73-53-g1.png) `Salary` 列是一个数值字段，目前格式为 `DOLLAR9`。接下来的 `PROC SQL` 步骤修改了 `Salary` 的格式并添加了标签：

```
proc sql;
   alter table work.payrollmaster4
      modify salary format=dollar11.2 label="Salary Amt";
```

下面显示了具有新 `Salary` 列属性的 `Work.Payrollmaster4` 的前 10 行。![修改列](img/m73-53-g2.png) 

## 在单条语句中添加、删除和修改列

在最后几个示例中，`ALTER TABLE` 语句仅通过一个子句对表列进行了一项更改。然而，你可以在单个 `ALTER TABLE` 语句中包含多个子句，以同时完成添加、删除和修改列的操作。

## 示例

假设你想使用单个 `ALTER TABLE` 语句对表 `Work.Payrollmaster4` 执行以下所有更改：

*   使用 `ADD` 子句添加新列 `Age`
*   使用 `MODIFY` 子句将 `DateOfHire` 列的格式（目前为 `DATE9.`）更改为 `MMDDYY10.`
*   使用 `DROP` 子句删除 `DateOfBirth` 和 `Gender` 列

下面显示了如上一个示例结束时 `Work.Payrollmaster4` 的前 10 行。![在单条语句中添加、删除和修改列](img/m73-54-g1.png) 接下来的 `PROC SQL` 步骤在 `ALTER TABLE` 语句中使用多个子句来完成上述列的所有三个更改：

```
proc sql;
   alter table work.payrollmaster4
      add Age num 
      modify dateofhire date format=mmddyy10.
      drop dateofbirth, gender;
```

下面显示了经过这三项更改的 `Work.Payrollmaster4` 的前 10 行。![在单条语句中添加、删除和修改列](img/m73-54-g2.png) 使用 `UPDATE` 语句填充新列。

# 删除表

## 概述

要删除（移除）一个或多个整个表，请使用 `DROP TABLE` 语句。

| 通用格式，`DROP TABLE` 语句：`DROP TABLE table-name-1 <, ... table-name-n>;` |
以下是对语法的解释：`table-name` 指定要删除的表名，可以是以下内容之一：

*   单级名称
*   两级库引用（libref）和表名
*   用单引号括起来的物理路径名。

## 示例

在最后几个示例中，你对临时表 `Work.Payrollmaster4` 进行了多处更改。现在你决定不再需要这张表了。接下来的 `PROC SQL` 步骤使用 `DROP TABLE` 语句删除 `Work.Payrollmaster4`：

```
 proc sql;
    drop table work.payrollmaster4;
```

SAS 日志显示一条表已删除的消息：

表 5.18 SAS 日志

| ``` NOTE: Table WORK.PAYROLLMASTER4 has been dropped.\n ``` |

## 总结

## 文字总结

### 理解创建表的方法

你可以使用 `CREATE TABLE` 语句以三种不同的方式创建表：

*   通过定义列来创建一个没有行的表（空表）
*   创建一个与另一个表相似的空表
*   根据查询结果创建一个包含行的表

### 通过定义列创建空表

你可以使用包含列规范的 `CREATE TABLE` 语句来创建一个没有行的表。列规范包含以下元素：列名（必需的）、数据类型（必需的）、列宽（可选）、一个或多个列修饰符（可选）以及列约束（可选）。

### 显示表结构

若要在 SAS 日志中显示表的列列表及其属性以及关于表的其他信息，请使用 `DESCRIBE TABLE` 语句。

### 创建与另一个表相似的空表

要创建一个与现有表结构相同的无行表，请使用包含 `LIKE` 关键字的 `CREATE TABLE` 语句。要指定从现有表中复制的列子集，请在你的 `CREATE TABLE` 语句中使用 SAS 数据集选项 `DROP=` 或 `KEEP=`。

### 从查询结果创建表

要创建一个包含源自现有表或多个表的列和行的新表，请使用包含 `AS` 关键字和查询中所用子句的 `CREATE TABLE` 语句。这种方法允许你快速复制现有表。

### 向表中插入数据行

`INSERT` 语句可以用三种方式向现有表（无论是空的还是已填充的）插入数据行。你可以通过以下方式插入行：

*   使用 `SET` 子句成对指定列名和值
*   使用 `VALUES` 子句指定值列表
*   使用查询中用于从现有表中返回行的子句

### 创建具有完整性约束的表

完整性约束是你指定的规则，用于限制存储在列中的数据。要创建一个具有完整性约束的表，请使用 `CREATE TABLE` 语句。完整性约束可以通过两种方式定义：

*   通过规范中的约束
*   使用约束指定

### 处理插入行时的错误

当你向具有完整性约束的表添加行时，`PROC SQL` 会评估新数据以确保符合条件。在使用 `INSERT` 或 `UPDATE` 语句添加或修改数据时，你可以使用 `PROC SQL` 语句中的 `UNDO_POLICY=` 选项来指定 `PROC SQL` 是否撤回到错误点为止提交的更改。

### 显示表的完整性约束

若要在 SAS 日志中显示表的完整性约束，请使用 `DESCRIBE TABLE CONSTRAINTS` 语句。

### 更新现有表的值

要修改表中某些或所有行的值，请使用带有内容的 `UPDATE` 语句：

*   `SET` 子句以及可能的 `WHERE` 子句指定单个更新表达式。若要更新多个表达式，请使用多个 `UPDATE` 语句。
*   `CASE` 表达式指定多个更新表达式。`CASE` 表达式可以不带可选的操作数，或者如果 `SET` 子句中的表达式使用了等号（=）比较运算符，则可以带有操作数。`CASE` 表达式也可以用于新列定义的 `SELECT` 语句，为不同的行集指定不同的值。

删除 删除表行

要删除表中某些或所有行，请使用 `DELETE` 语句。

### 修改表列

要修改表的列，请使用包含以下一个或多个子句的 `ALTER TABLE` 语句：

*   `ADD` 子句，向表添加一个或多个列
*   `DROP` 子句，删除表中的一个或多个列
*   `MODIFY` 子句，修改列的属性

## 示例程序

### 通过定义列创建空表

```
 proc sql;
    create table work.discount 
           (Destination char(3),
           BeginDate num Format=date9.,
           EndDate num format=date9.,
           Discount num);
quit;
```

### 创建与另一个表相似的空表

```
proc sql;
   create table work.flightdelays2
          (drop=delaycategory destinationtype) 
      like sasuser.flightdelays;
quit;
```




```sas
proc sql;
   create table work.ticketagents as
      select lastname, firstname,
             jobcode, salary
         from sasuser.payrollmaster,
              sasuser.staffmaster
         where payrollmaster.empid
               = staffmaster.empid
               and jobcode contains 'TA';
quit;
```

### 显示表的结构

```sas
proc sql;
   describe table work.discount;
quit;
```

### 通过指定列名和值向表中插入行

```sas
proc sql;
   insert into work.discount
        set destination='LHR',
            begindate='01MAR2000'd,
            enddate='05MAR2000'd,
            discount=.33
        set destination='CPH',
            begindate='03MAR2000'd,
            enddate='10MAR2000'd,
            discount=.15;
quit;
```

### 通过指定值列表向表中插入行

```sas
proc sql;
   insert into work.discount (destination, 
          begindate,enddate, discount)
      values ('LHR','01MAR2000'd, 
             '05MAR2000'd,.33)
      values ('CPH','03MAR2000'd,
             '10MAR2000'd,.15);
quit;
```

### 从查询结果向表中插入行

```sas
proc sql; 
   insert into work.payrollchanges2
      select empid, salary, dateofhire
         from sasuser.payrollmaster
         where empid in ('1919','1350','1401');
quit;
```

### 创建具有完整性约束的表

```sas
proc sql;
   create table work.employees
          (Name char(10),
          Gender char(1),
          HDate date label='Hire Date' not null,
          constraint prim_key primary key(name),
          constraint gender check(gender in ('M' 'F')));
quit;
```

### 显示表的完整性约束

```sas
proc sql;
   describe table constraints work.discount4;
quit;
```

### 根据表达式更新表中的行

```sas
proc sql;
   update work.payrollmaster_new
      set salary=salary*1.05
      where jobcode like '__1';
quit;
```

### 使用 CASE 表达式更新表中的行

```sas
proc sql;
   update work.payrollmaster_new 
      set salary=salary*
         case 
            when substr(jobcode,3,1)='1'
                 then 1.05
            when substr(jobcode,3,1)='2'
                 then 1.10
            when substr(jobcode,3,1)='3'
                 then 1.15
            else 1.08
         end;
quit;
```

### 使用 CASE 表达式更新表中的行（另一种语法）

```sas
proc sql outobs=10;
   select lastname, firstname, jobcode, 
          case substr(jobcode,3,1)
               when '1'
                    then 'junior'
               when '2'
                    then 'intermediate'
               when '3'
                    then 'senior'
               else 'none'
          end as JobLevel
      from sasuser.payrollmaster,
           sasuser.staffmaster
      where staffmaster.empid=
            payrollmaster.empid;
quit;
```

### 删除表中的行

```sas
proc sql;
   delete from work.frequentflyers2
      where pointsearned-pointsused<=0;
quit;
```

### 在表中添加、修改和删除列

```sas
proc sql;
   alter table work.payrollmaster4
      add Age num 
      modify dateofhire date format=mmddyy10.
      drop dateofbirth, gender;
quit;
```

### 删除一个表

```sas
proc sql;
   drop table work.payrollmaster4;
quit;
```

## 注意事项

* `CREATE TABLE` 语句仅生成表作为输出，而不是生成报告。
* `UPDATE` 语句不会向表中插入新行。要插入行，你必须使用 `INSERT` 语句。

# 测验

为每个问题选择最佳答案。完成测验后，使用附录中的答案键检查你的答案。

1. 下列哪个 `PROC SQL` 步骤通过仅复制现有表的列结构（但不复制行）来创建一个新表？

    1. \```sas
        proc sql;
           create table work.newpayroll as 
              select *
                 from sasuser.payrollmaster;
        ```
    2. \```sas
        proc sql;
           create table work.newpayroll 
              like sasuser.payrollmaster;
        ```
    3. \```sas
        proc sql;
           create table work.newpayroll 
              copy sasuser.payrollmaster;
        ```
    4. \```sas
        proc sql;
           create table work.newpayroll 
              describe sasuser.payrollmaster;
        ```

2. 下列哪个 `PROC SQL` 步骤创建了一个仅包含 1 级空乘员行的表？

    1. \```sas
        proc sql;
           create table work.newpayroll as
              select *
                 from sasuser.payrollmaster
              where jobcode='FA1';
        ```
    2. \```sas
        proc sql;
           create table work.newpayroll
              select *
                 from sasuser.payrollmaster
              where jobcode='FA1';
        ```
    3. \```sas
        proc sql;
           create table work.newpayroll
              copy sasuser.payrollmaster
              where jobcode='FA1';
        ```
    4. \```sas
        proc sql;
           create table work.newpayroll
              describe sasuser.payrollmaster
              where jobcode='FA1';
        ```

3. 关于 `UNDO_POLICY=REQUIRED` 选项，下列哪个说法是正确的？

    1. 它必须配合约束使用。
    2. 如果要插入或更新的行不符合，则忽略它们。
    3. 如果要插入或更新的行不符合，将表恢复到原始状态。
    4. 它允许符合约束的行，但拒绝不符合的行。

4. 下列哪个不是约束类型？

    1. `CHECK`
    2. `NULL`
    3. `UNIQUE`
    4. `PRIMARY KEY`

5. 下列哪个 `PROC SQL` 步骤删除了所有飞行里程少于 10000 英里的常旅客行？

    1. \```sas
        proc sql;
           delete from work.frequentflyers
              where milestraveled < 10000;
        ```
    2. \```sas
        proc sql;
           drop from work.frequentflyers
              where milestraveled < 10000;
        ```
    3. \```sas
        proc sql;
           drop table work.frequentflyers
              where milestraveled < 10000;
        ```
    4. \```sas
        proc sql;
           delete
              from work.frequentflyers
              where milestraveled < 10000;
        ```

6. 下列哪个 `PROC SQL` 步骤为常旅客计划成员发放积分如下：

    * 飞行里程少于 10000 英里的成员奖励 50% 积分
    * 飞行里程达到 10000 英里及以上的成员奖励 100% 积分

    1. \```sas
        proc sql;
           update work.frequentflyers
           set pointsearned=pointsearned*
              case if milestraveled < 10000
                          then 1.5
                   if milestraveled >= 10000
                          then 2
                   else 1
              end;
        ```
    2. \```sas
        proc sql;
           update work.frequentflyers
           set pointsearned=pointsearned*
              case when milestraveled < 10000
                        then 1.5
                   when milestraveled >= 10000
                        then 2
                   else 1
              end;
        ```




4. ```sql
proc sql;
   update work.frequentflyers
   set pointsearned=pointsearned*
      case if milestraveled < 10000
                      then pointsearned*1.5
                   if milestraveled >= 10000
                      then pointsearned*2
                   else pointsearned*1
              end;
```

7. 下列哪个语句用于向表中添加新行？

    1. `INSERT`

    2. `LOAD`

    3. `VALUES`

    4. `CREATE TABLE`

8. 关于 `ALTER TABLE` 语句，下列哪个陈述是错误的？

    1. 它允许你更新列的属性。

    2. 它允许你向表中添加新列。

    3. 它允许你删除表中的列。

    4. 它允许你将字符列更改为数值列。

9. 下列哪个操作可以在 SAS 日志中显示表的结构？

    1. ```sql
       proc sql;
           describe as
              select *
                 from sasuser.payrollmaster;
       ```

    2. ```sql
       proc sql;
           describe contents sasuser.payrollmaster;
       ```

    3. ```sql
       proc sql;
           describe table sasuser.payrollmaster;
       ```

    4. ```sql
       proc sql;
           describe * from sasuser.payrollmaster;
       ```

10. 下列哪个操作创建了一个包含 `FullName` 和 `Age` 两列的空表？

    1. ```sql
       proc sql;
           create table work.names
                  (FullName char(25), Age num);
       ```

    2. ```sql
       proc sql;
           create table work.names as
                  (FullName char(25), Age num);
       ```

    3. ```sql
           create work.names
                  (FullName char(25), Age num);
       ```

    4. ```sql
       proc sql;
           create table work.names
              set (FullName char(25), Age num);
       ```

# 第 6 章：使用 PROC SQL 创建和管理索引

## 概述

在处理包含子集 `WHERE` 子句或连接多个表的查询时，`PROC SQL` 必须在所引用的表中定位特定行。为表创建索引允许 `PROC SQL` 在某些情况下更快速、更高效地定位特定行。索引是一个辅助文件，用于存储表中一个或多个指定列（键列）值的物理位置。在索引中，键列（列）的每个唯一值都与包含该值的行标识符配对。就像你使用书籍的主题索引查找讨论特定主题的页码一样，`PROC SQL` 使用索引中的引导系统通过索引值直接访问表中的特定行。你可以为单个表创建多个索引。SAS 表的所有索引都存储在一个索引文件中。注意：你不能在视图上创建索引。以下 `PROC SQL` 步骤使用 `CREATE INDEX` 语句为表创建索引，并使用 `DESCRIBE TABLE` 语句在 SAS 日志中显示有关索引的信息以及关于表的其他信息：

```sql
proc sql;
   create unique index empid 
      on work.payrollmaster(empid);
   describe table work.payrollmaster;
```

注意：有关 `BUFSIZE=` 选项的更多信息，请参阅[使用 BUFSIZE= 选项]。

表 6.1 SAS 日志

```sql
create table WORK.PAYROLLMASTER( bufsize=4096 ) 
  ( 
   DateOfBirth num format=DATE9\. informat=DATE9.,
   DateOfHire num format=DATE9\. informat=DATE9.,
   EmpID char(4),
   Gender char(1),
   JobCode char(3),
   Salary num format=DOLLAR9.
  );
create unique index EmpID on WORK.PAYROLLMASTER(EmpID);
```

在本章中，你将学习使用 `PROC SQL` 创建和管理各种类型的索引。

### 理解索引

## 访问表中的行

当你对没有索引的表提交查询时，`PROC SQL` 会按照行在表中的存储顺序读取。然而，如果存在索引，`PROC SQL` 可以使用索引更高效地访问行。例如，如果你在某一列上创建了索引，`PROC SQL` 可以使用索引检索满足 `WHERE` 子句的行，而无需读取所有行。这在表很大时特别有用。

## 简单索引和复合索引

你可以创建两种类型的索引：

- **简单**：简单索引基于一列。
- **复合**：复合索引基于两个或多个列。例如，如果你在 `LastName` 和 `FirstName` 上建立复合索引。

## 唯一索引

如果你要求键列（列）的值对于每行来说必须是唯一的，你可以创建一个简单索引或复合索引作为唯一索引。一旦在表的一个或多个列上定义了唯一索引，SAS 将拒绝任何导致多行在指定列或列组上具有相同值的表表更改操作。

## 示例

假设你正在处理 `Sasuser.Payrollmaster` 表。该表的前八行显示所示：

| DateOfBirth | DateOfHire | EmpID | Gender | JobCode | Salary |
| --- | --- | --- | --- | --- |
| 16SEP1958 | 07JUN1985 | 1919 | M | TA2 | $48,126 |
| 19OCT1962 | 12AUG1988 | 1653 | F | ME2 | $49,151 |
| 08NOV1965 | 19OCT1988 | 1400 | M | ME1 | $41,677 |
| 04SEP1963 | 01AUG1988 | 1350 | F | FA3 | $46,040 |
| 19DEC1948 | 21NOV1983 | 1401 | M | TA3 | $54,351 |
| 29APR1952 | 11JUN1978 | 1499 | M | ME3 | $60,235 |
| 09JUN1960 | 04OCT1988 | 1101 | M | SCP | $26,212 |





| 03APR1959 | 14FEB1979 | 1333 | M | PT2 | $124,048 |

如果你知道列 `JobCode` 经常出现在 `WHERE` 子句表达式中，那么你可能想在 `JobCode` 列上创建一个简单索引。你必须将键列 `JobCode` 的名称指定为索引名称。现在，假设你计划编写许多查询，这些查询在 `WHERE` 子句表达式中同时指定了 `EmpID` 和 `DateOfHire`。在这种情况下，你可能想在这两个列上 true 一个复合索引。由于员工识别码应该是唯一的，因此将此索引创建为唯一索引是合适的。因此，你应该为你的索引指定一个名称，该名称不能与表中任何现有列或索引的名称相同。例如，你可以将此索引命名为 `Whenhired`。

### 决定是否创建索引

## 概述

索引可以缩短定位一组行所需的时间，特别是大型数据文件。然而，创建、存储和维护索引是有成本的。在决定是否创建索引时，你必须权衡性能改进的收益与资源使用增加的成本。注意：本章专门讨论了与使用 `PROC SQL` 索引相关的收益和成本。要了解在其他 SAS 过程中使用索引的成本和收益，请参阅 SAS 文档。

## 可通过索引优化的 PROC SQL 查询

在 `PROC SQL` 中有效使用索引，了解可以使用索引更高效地处理的查询类型至关重要。以下是可以优化的查询类型。

| 当键列出现在以下位置时，查询性能会得到优化 | 示例 |
| --- | --- |
| 包含比较运算符、`TRIM` 或 `SUBSTR` 函数、`CONTAINS` 运算符或 `LIKE` 运算符的 `WHERE` 子句表达式。 | |

```
proc sql;
    select empid, jobcode, salary
       from sasuser.payrollmaster
       where jobcode='FA3'
       order by empid;
```
键列（列）：`JobCode` |
| 返回返回值给 `IN` 运算符的子查询中。 | |
```
proc sql;
    select empid, lastname, firstname,
            city, state
       from sasuser.staffmaster
       where empid in
          (select empid
             from sasuser.payrollmaster
             where salary>40000);
```
键列（列）：`EmpID` |
| 关联子查询，其中与关联引用比较的列已建立索引。 | |
```
proc sql;
    select lastname, firstname
       from sasuser.staffmaster
       where 'NA'=
          (select jobcategory
             from sasuser.supervisors
             where staffmaster.empid =
                    supervisors.empid);
```
键列（列）：`Supervisors.EmpID` |
| 连接，其中连接表达式包含等号（`=`）运算符（等值连接），且连接表达式中的所有列在被连接的表中都建立了索引。 | |
```
proc sql;
    select *
       from sasuser.payrollmaster as p,
            sasuser.staffmaster as s
       where p.empid =
             s.empid
       order by jobcode;
```
键列（列）：`Payrollmaster.EmpID` 或 `Staffmaster.EmpID` |

## 使用索引的收益

对于 `PROC SQL`，直接使用索引访问数据（而不是顺序读取数据）主要有三个收益：

*   可以更快地访问一小部分数据（小于行数的 15%）。随着子集的增大，使用索引的优势会降低。
*   可以在不需要内部排序的情况下执行等值连接。
*   通过创建唯一索引可以强制唯一性。

## 示例：使用索引访问较小数据集

假设你正在编写一个引用 `Work.Payrollmaster` 表的查询。（`Work.Payrollmaster` 是 `Sasuser.Payrollmaster` 表的副本）。`Work.Payrollmaster` 存储员工的工资信息，并在 `JobCode` 列上定义了一个简单索引。你的查询的 `WHERE` 子句表达式引用了键列：

```
proc sql;
   select empid, jobcode, salary
      from work.payrollmaster
      where jobcode='FA3'
      order by empid;
```

如果表中大多数行的 `JobCode` 值为 `FA3`，那么使用索引不会显著提高后续查询的效率。事实上，性能可能会下降。但是，如果只有 10% 的行值为 `FA3`，则 `PROC SQL` 可以通过使用索引更高效地处理查询。注意：在本章中，如果你想提交任何引用临时表（存储在 `Work` 库中的表）的示例代码，首先需要通过复制 `Sasuser` 库中同名的表来创建临时表。

## 理解使用索引的成本

当你决定是否创建索引时，应该考虑相关的资源使用增加，包括：

*   创建索引、在修改表时维护索引以及使用索引从表中读取行需要额外的 CPU 时间。
*   与顺序读取表相比，使用索引从表中读取行可能需要额外的 I/O（输入/输出）请求。
*   使用索引需要额外的内存，用于加载索引页的缓冲区。
*   存储索引文件需要额外的磁盘空间，该文件在 Windows 中显示为独立文件，在 z/OS 中可能是数据文件的一部分。

## 创建索引的指南

为了有效使用索引，请遵循以下创建索引的指南：

*   尽量减少索引数量，以减少存储和更新成本。
*   不要为小表创建索引。小表的顺序访问更快。
*   不要对不同值非常少的列创建索引（例如，只包含 `Male` 和 `Female` 值的性别列）。
*   对检索较小行集（即小于 15%）的查询使用索引。
*   不要对与主键相同的列创建多个索引。

提示许多因素都会影响 SAS 程序的处理。确定是否为特定表或列创建索引的最准确方法是进行基准测试。

### 创建索引

## 概述

要在表的列或多个列上创建索引，请使用 `CREATE INDEX` 语句。

| CREATE INDEX 语句的通用格式： |
| --- |
| `CREATE <UNIQUE> INDEX index-name ON table-name (column-name-1<, ...column-name-n>);` 说明：`UNIQUE` 是一个关键字，指定语句指定的列值必须是唯一的。`index-name` 指定要创建的索引名称。如果你只列列创建索引，则 `index-name` 必须与 `column-name-1` 相同。如果你对多个列创建索引，则 `index-name` 不能与表中任何现有列或索引的名称相同。`table-name` 指定创建索引的表名。`column-name` 指定要索引的列。列可以以任何顺序指定。但是，列的顺序对于数据检索至关重要。第一个名的列是主键，第二个列是辅助键，以此类推。 |





提示：创建复合索引时，指定列的顺序应与您在 `ORDER BY` 子句中指定的顺序相同。
提示：如果您在预排序的表上创建索引，可以提高索引性能。SAS 会对表的所有更改维护索引，无论这些更改源自 `PROC SQL` 还是其他源，只要整个表没有重新创建。如果您修改了列的定义或更新了其值，SAS 也会更新索引。然而，如果表中的键列被删除，则该列上的索引也会随之删除。

## 创建多个索引

您不能基于同一列创建多个简单索引，也不能基于同一组列创建多个复合索引。虽然可以在同一列上同时创建简单索引和复合索引，但通常这样做并没什么优势。如果如果在某列上定义了简单索引，且该列也是复合索引中的主键，则 `PROC SQL` 在处理引用该列的查询时使用复合索引。您可以在同一张表上创建多个索引，但必须为每个想要创建的索引使用单独的 `CREATE INDEX` 。

## 示例：创建简单索引

以下 `PROC SQL` 步骤使用 `CREATE INDEX` 语句在临时表 `Work.Payrollmaster` 中基于列 `EmpID` 创建一个简单的唯一索引。（`Work.Payrollmaster` 是表 `Sasuser.Payrollmaster` 的副本。）

```
proc sql;
   create unique index EmpID
      on work.payrollmaster(empid);
```

指定的索引名称（`EmpID`）必须与键列的名称相同。当提交此步骤时，SAS 日志将显示以下消息。

上表 6.2 SAS 日志

```
NOTE: Simple index EmpID has been defined.
```

## 示例：创建复合唯一索引

以下 `PROC SQL` 步骤使用 `CREATE INDEX` 语句在列 `FlightNumber` 和 `Date` 上创建复合唯一索引 `daily`：

```
proc sql;
   create unique index daily
      on work.marchflights(flightnumber,date);
```

当提交此步骤时，SAS 日志将显示以下消息。

表 6.3 SAS 日志

```
NOTE: Composite index daily has been defined.
```

注意：SAS 日志中的说明信息显示的索引名称与您指定的完全一致。在本例中，索引名称 `daily` 是以小写形式指定的。在上一个示例中，索引名称 `EmpID` 是以大小写指定的。然而，索引名称使用大写或小写并不重要，因为 SAS 无论索引名称在代码中如何格式都能识别。如果键列集 `FlightNumber` 和 `Date` 具有重复值，则不会创建索引。相反，SAS 日志将显示如下所示的消息。

表 6.4 SAS 日志

```
ERROR: Duplicate values not allowed on index daily for file MARCHFLIGHTS.
```

# 显示索引规格

## 概述

有时您想知道现有表是否存在任何索引。为了在 SAS 日志中为一个或多个指定表定义的每个索引显示 `CREATE INDEX` 语句，可以使用 `DESCRIBE TABLE` 语句。（`DESCRIBE TABLE` 语句还会为每个指定的表向 SAS 日志写入 `CREATE TABLE` 语句。）

通用格式，`DESCRIBE TABLE` 语句：`DESCRIBE TABLE table-name-1<, ... table-name-n>;`

以下是对语法的解释：`table-name` 指定要描述的表，可以是以下之一：

*   单级名称
*   两级 libref.table 名称
*   用单引号括起来的物理路径

如果指定的表没有索引，则不会出现 `CREATE INDEX` 语句。

## 示例

在本章前面的部分，使用了以下代码在临时表 `Marchflights` 中对列 `FlightNumber` 和 `Date` 创建了名为 `daily` 的唯一复合索引。

```
proc sql;
   create unique index daily
      on work.marchflights(flightnumber,date);
```

以下 `DESCRIBE TABLE` 语句为 `Marchflights` 表向 SAS 日志写入了一个 `CREATE INDEX` 语句（跟在 `CREATE TABLE` 语句之后）：

```
proc sql;
   describe table marchflights;
```

表 6.5 SAS 日志

```
NOTE: SQL table WORK.MARCHFLIGHTS was created like:

create table WORK.MARCHFLIGHTS( bufsize=8192 )
  (
   Date num format=DATE9\. informat=DATE9.,
   DepartureTime num format=TIME5\. informat=TIME5.,
   FlightNumber char(3),
   Origin char(3),
   Destination char(3),
   Distance num,
   Mail num,
   Freight num,
   Boarded num,
   Transferred num,
   NonRevenue num,
   Deplaned num,
   PassengerCapacity num
  );
create unique index daily on WORK.MARCHFLIGHTS(FlightNumber,Date);
```

如果 `Marchflights` 表没有定义索引，则 SAS 日志中不会出现 `CREATE INDEX` 语句。

## DESCRIBE TABLE 语句的替代方案

`DESCRIBE TABLE` 语句只是列出表上定义的索引信息的多种方法之一。另一种方法是查询特殊表 `Dictionary.Indexes`，它包含了对于当前 SAS 会话已知的所有表所定义的索引信息（`Dictionary.Indexes` 是 `PROC SQL` 初始化时创建的许多只读字典表之一。这些表包含当前 SAS 会话使用的或可用的 SAS 库、SAS 宏和外部文件的信息）。可以使用其他 SAS 过程（如 `PROC CONTENTS` 和 `PROC DATASETS`生成报告。

# 管理索引使用

## 概述

为了有效管理索引，了解以下内容非常重要：

*   SAS 如何决定是否使用索引以及使用哪个索引
*   如何确定 SAS 是否正在使用索引
*   如何控制 SAS 是否使用索引，或它使用哪个索引

## 理解 SAS 如何决定是否使用索引

默认情况下，每当您提交包含 `WHERE` 表达式的查询（或其他 SAS 程序）时，SAS 都会决定使用索引还是读取数据文件中的所有观测值。为了做出此决定，SAS 执行以下操作：

1. 识别可用的一个或多个索引。
2. 估计符合条件的行数。如果有多个索引，SAS 将选择估计返回最小行集的索引。
3. 比较资源使用情况，以决定通过索引还是顺序读取所有观测值来满足 `WHERE` 表达式效率。

接下来考虑如何发现 SAS 是否正在使用索引。

## 确定 SAS 是否正在使用索引

创建索引后，监控该索引是否被使用很重要。如果索引没有被使用，维护索引的成本可能大于收益，您应该考虑删除（drop）该索引。默认情况下，当在 SAS 中提交 `PROC SQL` 查询或任何程序时，SAS 日志只记录备注、警告和错误消息。为了显示附加消息（例如关于已定义并在处理程序期间索引的信息），请指定 SAS 系统选项 `MSGLEVEL=I`。您可以在 `PROC SQL` 语句之前的 `OPTIONS` 语句中指定 `MSGLEVEL=` 选项。




通常，在调试和测试时将选项 `MSGLEVEL=` 设置为 `I`，而在生产作业中将其设置为 `N`。

## 示例：使用索引的查询

假设你正在编写一个引用临时表 `Marchflights` 的 `PROC SQL` 查询。在本章的较早部分中，已在 `Marchflights` 表的 `FlightNumber` 和 `Date` 列上创建了一个名为 `daily` 的唯一复合索引。你的查询中的 `WHERE` 表达式指定了键列 `FlightNumber`。为了确定 `PROC SQL` 在处理你的查询时是否使用了 `daily` 索引，你可以在查询之前指定 `MSGLEVEL=I`：

```
options msglevel=i;
proc sql;
   select *
      from marchflights
      where flightnumber='182';
```

SAS 日志中的信息显示处理过程中使用了该索引。

表 6.6 SAS 日志

| |
```
INFO: Index daily selected for WHERE clause optimization.
```
 |

## 示例：不使用索引的查询

假设你提交了另一个引用键列 `FlightNumber` 的查询：

```
proc sql;
   select *
      from marchflights
      where flightnumber in ('182','202');
```

在此示例中，SAS 日志显示该查询没有使用索引。

表 6.7 SAS 日志

| |
```
INFO: Index daily not used. Sorting into index order may help.
INFO: Index daily not used. Increasing bufno to 8 may help.
```
 |

注意：关于 `BUFSIZE=` 选项的更多信息，请参见使用 BUFSIZE= 选项。注意：SAS 版本 8 显示指示何时使用索引的信息性消息，但不显示指示何时未使用索引的消息。提示：由于 `OPTIONS` 语句是全局的，这些设置将一直有效，直到你修改它们或结束 SAS 会话。因此，在第二个查询或任何后续查询中，你不需要再次指定 `MSGLEVEL=I`，除非你想更改该设置或 SAS 会话结束。

## 控制索引的使用

通常情况下，建议让 SAS 在处理 `PROC SQL` 查询（或其他 SAS 程序）时自行决定是否使用索引或使用哪种索引。然而，在某些情况下（例如测试），你可能会发现控制 SAS 使用索引是有用的。要控制索引的使用，请使用 `IDXWHERE=` 和 `IDXNAME=` SAS 数据集选项来覆盖默认设置。你可以使用这两个选项中的任意一个，但不能同时使用。与其他 SAS 数据集选项一样，你可以在 `PROC SQL` 查询的 `FROM` 子句的表名括号中指定 `IDXWHERE=` 或 `IDXNAME=` 选项。

## 使用 IDXWHERE= 指定 SAS 使用或不使用索引

`IDXWHERE=` 选项允许你覆盖 SAS 关于是否使用索引的决定。

`IDXWHERE=` 选项的标准形式：`IDXWHERE=YES | NO;`

以下是对语法的解释：
`YES` 告诉 SAS 选择最佳索引来优化 `WHERE` 表达式，并忽略对表的顺序搜索可能更节省资源的可能性。
`NO` 告诉 SAS 忽略所有索引，通过对表的顺序搜索来满足 `WHERE` 表达式条件。

注意：当你知道可用索引无法优化 `WHERE` 子句的处理时，请使用 `IDXWHERE=NO` 选项。

## 示例

在之前的示例中，你使用了选项 `MSGLEVEL=I` 来验证 `PROC SQL` 确实使用了索引来处理以下查询：

```
options msglevel=i;     
proc sql;
   select *
      from marchflights
      where flightnumber='182';
```

要强制 SAS 忽略索引并按顺序处理表行，请在查询中指定 `IDXWHERE=NO`：

```
proc sql;
   select *
      from marchflights (idxwhere=no)
      where flightnumber='182';
```

SAS 日志中的信息显示 SAS 被强制按顺序处理数据。

表 6.8 SAS 日志

| |
```
INFO: Data set option (IDXWHERE=NO) forced a sequential pass of the data 
rather than use of an index for where-clause processing.
```
 |

## 使用 IDXNAME= 指定 SAS 使用指定的索引

`IDXNAME=` 选项引导 SAS 使用指定的索引，即使 SAS 原本选择不使用索引或使用不同的索引。

`IDXNAME=` 选项的标准形式：`IDXNAME=index-name;`

以下是对语法的解释：
`index-name` 指定了用于处理的索引名称。

如果满足以下条件，SAS 将使用指定的索引：
* 指定的索引必须存在。
* 指定的索引必须合适，其至少第一列或唯一列匹配 `WHERE` 表达式中的条件。

注意：当你知道更好的索引时，请使用 `IDXNAME=` 选项，这样 SAS 就无需进行评估。

## 示例

在之前的示例中，在临时表 `Marchflights` 的 `FlightNumber` 和 `Date` 列上定义了一个名为 `daily` 的复合索引。假设你通过以下 `PROC SQL` 步骤在 `Date` 列（复合索引中的次要键）上创建第二个索引，即简单索引：

```
proc sql;
   create index Date    
      on marchflights(Date);
```

接下来，你提交了以下查询：

```
proc sql;
   select *
      from marchflights
      where date='MAR2000';
```

此查询的 `WHERE` 子句引用了 `Date`。默认情况下，SAS 决定是否使用索引或使用哪种索引。你决定强制 PROC SQL 使用 `daily` 索引，因此在查询中添加了 `IDXNAME=`：

```
proc sql;
   select *
      from marchflights (idxname=daily)
      where flightnumber='182';
```

提交此查询后，SAS 日志中的信息显示 PROC SQL 使用了索引：

表 6.9 SAS 日志

| |
```
INFO: Index daily selected for WHERE clause optimization.
```
 |

删除一个或多个索引，使用 `DROP INDEX` 语句。

`DROP INDEX` 语句的标准形式：`DROP INDEX index-name <,...index-name> FROM table-name;`

以下是对语法的解释：
`index-name` 指定存在的索引。
`table-name` 指定包含索引的表。`table-name` 可以是以下之一：
*   单级名称
*   双级 libref.表名
*   用单引号括起来的物理路径

## 示例：删除复合索引

以下 `PROC SQL` 步骤使用 `DROP INDEX` 语句删除 `Marchflights` 表中的复合唯一索引 `daily`。（该索引在本章较早的示例中创建。）

```
proc sql;
   drop index daily
      from work.marchflights;
```

当提交此步骤时，SAS 日志显示一条消息指示索引已删除。

表 6.11 SAS 日志

| |
```
NOTE: Index daily has been dropped.
```
 |

## 总结

## 总结

### 理解索引

索引是定义在表的一个或多个列（称为键列）上的辅助文件。索引存储唯一的列值以及允许通过索引值访问表行的系统方向。当使用索引处理 `PROC SQL` 查询时，`PROC SQL` 直接访问（无需读取之前的所有行），而不是顺序访问。你可以创建两种类型的索引：
*   简单索引（单列的索引）
*   复合索引（两个或多个列的索引）

你可以将任何类型的索引定义为唯一索引，这要求键列的值对于每行都是唯一的。

### 决定是否创建索引





在决定是否创建索引时，你必须权衡性能改进的收益与资源使用增加的成本。某些类别的 `PROC SQL` 查询可以使用索引进行优化。为了优化你的 `PROC SQL` 查询的性能，你可以遵循一些创建索引的基本准则。

### 创建索引
要对表的一个列或多个列创建索引，请使用 `CREATE INDEX` 语句。要指定唯一索引，请添加关键字 `UNIQUE`。

### 显示索引规格
要为针对一个或多个指定表定义的每个索引在 SAS 日志（SAS log）中显示 `CREATE INDEX` 语句，请使用 `DESCRIBE TABLE` 语句。

### 管理索引使用
为了有效管理索引，了解 SAS 如何决定是否使用索引以及使用哪个索引非常重要。要检查是否正在使用索引，请在 `PROC SQL` 语句之前的 `OPTIONS` 语句中指定 SAS 选项 `MSGLEVEL=I`。此选项允许 SAS 将有关索引使用的提示信息性消息（以及其他附加信息）写入 SAS 日志中。默认设置 `MSGLEVEL=N` 仅显示备注、警告和错误消息。要强制 SAS 使用最佳可用索引、使用特定索引或完全不使用索引，请在 `PROC SQL` 查询中包含 SAS 数据集选项 `IDXWHERE=` 或 `IDXNAME=`。

### 删除索引
要删除（移除）一个或多个索引，请使用 `DROP INDEX` 语句。

## 示例程序

### 创建简单的唯一索引和复合索引
```
proc sql;
   create unique index EmpID
      on work.payrollmaster(empid);
   create index daily
      on work.marchflights(flightnumber,date);
quit;
```

### 显示索引规格
```
proc sql;
   describe table marchflights;
quit;
```

### 判断 SAS 是否正在使用索引
```
options msglevel=i;
proc sql;
   select *
      from marchflights
      where flightnumber='182';
quit;
```

### 指导 SAS 忽略所有索引
```
proc sql;
   select *
      from marchflights (idxwhere=no)
      where flightnumber='182';
quit;
```

### 指导 SAS 使用指定的索引
```
proc sql;
   select *
      from marchflights (idxname=daily)
      where flightnumber='182';
quit;
```

### 删除一个索引
```
proc sql;
   drop index daily
      from work.marchflights;
quit;
```

## 注意事项
* 索引无法在视图（view）上创建。
* 保持索引数量最少，以减少磁盘存储和更新成本。
* 不要为小表创建索引；小表上的顺序访问更快。
* 不要根据具有极少数不同值（低基数）列创建索引（例如，仅包含 `Male` 和 `Female` 两个值的 `Gender` 列）。
* 对于检索较小行子集的查询——即少于 15% 的行——请使用索引。
* 不要创建与主键基于同一列的多个及以上的索引。

# 测验
为每个问题选择最佳答案。完成测验后，使用附录中的答案键检查你的答案。

1. 下列哪项为 `Sasuser.Staffmaster` 表的 `EmpID` 列创建索引？
    1. ```
       proc sql;
          create simple index(empid) 
             on sasuser.staffmaster;
       ```
    2. ```
       proc sql;
          create empid index 
              on sasuser.staffmaster(empid);
       ```
    3. ```
       proc sql;
          create simple index 
              on empid from sasuser.staffmaster;
       ```
    4. ```
       proc sql;
          create index 
              on sasuser.staffmaster(empid);
       ```

2. 为了确保不存在重复值，你必须在索引定义中添加哪个关键字？
    1. `KEY`
    2. `UNIQUE`
    3. `NODES`
    4. `NODUP`

3. 下列哪项为 `delays` 创建一个复合索引？（`delays` 包含以下列：`Date`、`Origin`、`Destination`、`DayOfWeek`, `Delay`）
    1. ```
       proc sql;
          create index 
              on flightnumber,destination
       ```
    2. ```
       proc sql;
          create composite index 
              on flightnumber,destination
       ```
    3. ```
       proc sql;
          create index 
              on 
              flightnumber,destination
       ```
    4. ```
       proc sql;
          create index 
              on flightnumber,destination
       ```

4. 下列哪项会在 SAS 日志中显示 `PROC SQL` 是否使用了索引？
    1. ```
       options msglevel=i;
       proc sql;
          select *
              from internationalflights
       ```
    2. ```
       options index=yes;
       proc sql;
          select *
              from internationalflights
       ```
    3. ```
       proc sql;
          select * (idxwhere=yes)
              from internationalflights
       ```
    4. ```
       proc sql;
          select * (msglevel=i)
              from internationalflights
       ```

5. 下列哪项用于删除一个或多个索引？
    1. ```
       proc sql;
          drop index 
              from marchflights;
       ```
    2. ```
       proc sql;
          delete index 
              on sasuser.staffmaster(flightnumber,date);
       ```
    3. ```
       proc sql;
          drop index daily
              from work.marchflights;
       ```
    4. ```
       proc sql;
          delete index 
              on marchflights;
       ```

6. 下列哪项语句显示表中定义的所有索引？
    1. `DESCRIBE INDEX`
    2. `DESCRIBE TABLE`
    3. `SELECT`
    4. `IDXNAME`

7. 指定数据集选项 `IDXWHERE=YES` 的目的是什么？
    1. 它强制 SAS 使用最佳可用索引处理 `WHERE` 表达式。
    2. 它根据 `WHERE` 子句创建索引。
    3. 它将有关索引使用的消息写入 SAS 日志。
    4. 它停止 SAS 使用任何索引。

8. 关于使用索引，下列哪项是错误的？
    1. 连接可以在不需要排序的情况下进行。
    2. 索引提供了快速访问较小数据集的方法。
    3. 索引只能为数值列创建。
    4. 索引可以强制执行唯一性。

9. 在何种情况下，使用索引不太可能优化 `PROC SQL` 查询？
    1. 查询包含引用键列的 `IN` 子查询。
    2. 键列指定在 `WHERE` 子表达式中包含比较运算符、`TRIM` 或 `SUBSTR` 函数、`CONTAINS` 运算符或 `LIKE` 运算符。
    3. 查询是一个等连接，且连接表达式中的所有列在被连接的表中都有索引。
    4. 键列仅指定在 `SELECT` 子句中。

10. 关于 `IDXNAME=` 数据集选项，下列哪项是错误的？
    1. 指定的索引必须存在。





2. 指定索引必须是合适的，其至少第一列或唯一列必须匹配 `WHERE` 表达式中的某个条件。

3. 该选项允许你在表上创建并命名索引。

4. 该选项引导 SAS 使用你指定的索引。

# 第 7 节：使用 PROC SQL 创建和管理视图

## 概述

## 引言

`PROC SQL` 视图是一个存储的查询表达式，它从其底层文件读取数据值，这些底层文件可以包括 SAS 数据文件、DATA 步视图、其他 PROC SQL 视图或 DBMS 数据。你可以在查询中引用视图，就像引用表一样。视图的数据源于其 `FROM` 子句中列出的表或视图。视图访问的数据是其底层表（或视图）中数据的子集或超集。

```
proc sql;
   create view sasuser.raisev as
      select empid, jobcode, 
             salary format=dollar12.2, 
             salary/12 as MonthlySalary
             format=dollar12.2
         from payrollmaster;
   select *
      from sasuser.raisev
      where jobcode in ('PT2','PT3');
```

| ![来自 payrollmaster 表的 sasuser.raisev 视图](img/m75-1-g1.png) |

PROC SQL 视图

* 可用于 SAS 程序代替实际 SAS 数据文件
* 可与表或其他视图连接
* 可从一个或多个表、PROC SQL 视图或 DATA 步视图派生
* 可以从 SAS 数据集、DATA 步视图、PROC SQL 视图或关系数据库表访问数据
* 可以提取底层数据，从而让你访问最新的数据。

# 创建和使用 PROC SQL 视图

## PROC SQL 视图

`PROC SQL` 视图是一个存储的查询，当你在 SAS 过程或 DATA 步中使用视图时就会执行。视图仅包含描述符以及从其他 SAS 文件（SAS 数据文件、DATA 步视图或其它 PROC SQL 视图）或外部文件（DBMS 数据文件）检索数据值所需的其他信息。视图仅包含访问数据的逻辑，而不包含数据本身。由于 `PROC SQL` 视图不是数据的独立副本，因此它们被称为虚拟表。它们不像真实表那样作为独立实体存在。然而，视图使用与表相同的命名规范，并可以在 SAS 程序中代替实际 SAS 表。与表一样，视图被视为 SAS 数据集。视图之所以有用是因为它们执行了以下操作：

* 通常可以节省空间（与其访问的数据相比，视图通常非常小）
* 防止用户不断提交查询来忽略不需要的列或行
* 确保输入数据集始终是最新的，因为数据是在执行时从表中派生的
* 为用户屏蔽敏感或机密列，同时允许这些用户查看同一张表中的其他列
* 向用户隐藏复杂的连接或查询。

## 创建 PROC SQL 视图

你使用 `CREATE VIEW` 语句来创建视图。

`CREATE VIEW` 语句的一般：
`CREATE VIEW proc-sql-view AS SELECT column-1<, ... column-n> FROM table-1 | view-1<, ... table-n | view-n><optional query clauses>;`

以下是该语法的解释：

* `proc-sql-view` 指定你正在创建的 `PROC SQL` 视图的名称。
* `SELECT` 指定表中出现的列（列）。
* `FROM` 指定要查询的表（表）或视图（视图）。
* `optional query clauses`（可选查询子句）用于进一步完善查询，包括 `WHERE`、`GROUP BY`、`HAVING` 和 `ORDER BY` 子句。

`PROC SQL` 视图的数据源于 `FROM` 子句中列出的表或视图。视图访问的数据是其底层表（或视图）中数据的子集或超集。当在 SAS 过程或 DATA 步中引用视图时，它会被执行，并且在概念上，会构建一个内部表。`PROC SQL` 处理此内部表就像处理任何其他表一样。

## 示例

以下 `PROC SQL` 步创建了一个包含空乘人员信息的视图。该视图始终返回截至当前的员工年龄。视图 `Sasuser.Faview` 根据伴随的 `SELECT` 语句创建一个虚拟表。虽然底层表 `Sasuser.Payrollmaster` 和 `Sasuser.Staffmaster` 可能会发生，但构成视图的指令保持不变。`FROM` 子句中指定的 libref 是可选的。假设参与的表是可用的。

```
proc sql;
   create view sasuser.faview as
      select lastname, firstname, gender,
             int((today()-datebirth)/365.25) as Age,
             substr(jobcode,1) as Level,
             salary
         from payrollmaster,
              staffmaster
         where jobcode = 'FA';
```

当提交此 `PROC SQL` 步时，SAS 不会实际执行 `AS` 之后的 `SELECT` 语句，而是编译并将语句存储在类型为 VIEW 的数据文件中。SAS 日志中的消息确认视图已定义。

表 7.1 SAS 日志

```
    proc sql;
   create view sasuser.faview as
      select lastname, firstname, gender,
             int((today()-datebirth)/365.25) as Age,
             substr(jobcode,1) as Level,
             salary
         from payrollmaster,
              staffmaster
         where jobcode = 'FA';
NOTE: SQL view SASUSER.FAVIEW has been defined.
```

## 使用 PROC SQL 视图

你可以在 `PROC SQL` 步或同一步的后期使用视图，就像使用实际 SAS 表一样。在以下示例中，`PROC SQL` 视图 `Sasuser.Faview` 用于查询。由于存储在视图中的查询根据当前日期计算空乘人员的年龄，此 `PROC SQL` 步的输出显示每个空乘人员截至当前的年龄。如果 `Sasuser.Faview` 是静态表而不是视图，显示的空乘人员年龄将永远不会改变。

```
proc sql;
   select *
      from sasuser.faview;
```

部分输出所示![Sasuser.Faview](img/m75-4-g1.png)你可以在其他 SAS 过程和 DATA 步中使用 PROC SQL 视图。在以下示例中，`PROC TABULATE` 使用视图 `Sasuser.Faview` 按级别计算空乘人员的平均年龄：

```
proc tabulate data=sasuser.faview;
   class level; 
   var age; 
   table level*age*mean;
run;
```

![按级别的空乘人员平均年龄](img/m75-4-g2.png)注意：变量 `Age` 的值取决于取决于执行代码的日期。注意：有关 `TABULATE` 过程的信息，请参阅 SAS 文档。

# 显示 PROC SQL 视图的定义

## 概述

你可以使用 `DESCRIBE VIEW` 语句在 SAS 日志中显示视图的定义。





# 管理 PROC SQL 视图

## 使用 PROC SQL 视图的准则

### DESCRIBE VIEW
通用格式，`DESCRIBE VIEW` 语句：`DESCRIBE VIEW proc-sql-view-1<,...proc-sql-view-n>;` 
以下是对语法的解释：
`proc-sql-view` 指定一个 `PROC SQL` 视图，它可以是以下内容之一：
* 单级名称
* 二级名称 `libref.view`
* 用单引号括起来的物理路径名。

提示：如果你在基于或派生自另一个视图的 `DESCRIBE VIEW` 语句中使用 `PROC SQL` 视图，那么你可能希望在 `PROC SQL` 语句中使用 `FEEDBACK` 选项。该选项会在 SAS 日志中显示底层视图的定义，并展开在此视图定义中使用的任何表达式。

## 示例
以下 `PROC SQL` 步骤将 `Sasuser.Faview` 的视图定义写入 SAS 日志：

```
proc sql;
   describe view sasuser.faview;
```

表 7.2 SAS 日志

```
NOTE: SQL view SASUSER.FAVIEW is defined as:
      select lastname, firstname, gender,
             INT((TODAY()-dateofbirth)/365.25) as Age,
      SUBSTR(jobcode, 3, 1) as Level, salary
      from SASUSER.PAYROLLMASTER, SASUSER.STAFFMASTER
      where jobcode contains 'FA' and
            (staffmaster.empid=payrollmaster.empid);
```

## 省略 Libref
`FROM` 子句中表或多个表的默认 `libref` 是包含该视图的库的 `libref`。在 `FROM` 子句中使用单级名称，可以避免在您为包含该视图及其贡献表的 SAS 库分配不同的 `libref` 时，仍必须更改视图的麻烦。

以下 `PROC SQL` 步骤创建了视图 `Sasuser.Payrollv`。`FROM` 子句为贡献表 `Sasuser.Payrollmaster` 指定了二级名称。然而，没有必要指定 `libref` `Sasuser`，因为假设贡献表存储在与视图相同的库中。

```
proc sql;
   create view sasuser.payrollv as
      select *
         from sasuser.payrollmaster;
```

当 `FROM` 子句中使用单级名称 `Payrollmaster` 时，实际上指定的是 `Sasuser.Payrollmaster`，尽管看起来像是指定了 `Work.Payrollmaster`。

```
proc sql;
   create view sasuser.payrollv as
      select *
         from payrollmaster;
```

注意：如果您创建的视图与 `FROM` 子句中引用的表存储在不同的库中，则必须为该表（们）指定二级名称。

## 使用嵌入式 LIBNAME 语句
作为在 `FROM` 子句中省略 `libref` 的替代方案，您可以在 `USING` 子句中嵌入 `LIBNAME` 语句，以在视图中存储 SAS `libref`。嵌入 `LIBNAME` 语句是一种更具灵活的方法，因为：
* 无论视图表和底层表是否位于同一个库中，都可以使用。
* 它避免了如果 `FROM` 子句中的表名中省略 `libref` 可能产生的混淆。

嵌入式 `LIBNAME` 语句只能用于 `PROC SQL` 视图。使用嵌入式 `LIBNAME` 语句创建的 `libref` 不与 SAS 会话中同名的 `libref` 冲突。

通用格式，`USING` 子句：`USING libname-clause-1<,... libname-clause-n>;`
以下是对语法的解释：`libname-clause` 是以下内容之一：
* 有效的 `LIBNAME` 语句
* 有效的 SAS/ACCESS `LIBNAME` 语句。

注意：`USING` 子句必须是 `CREATE VIEW` 语句的最后一个子句。

## 示例
在以下示例中，当视图 `Sasuser.Payrollv` 在 `PROC PRINT` 步骤中执行时，`libref` `Airline` 在 `USING` 子句中动态赋值。

```
proc sql;
   create view sasuser.payrollv as
      select*
         from airline.payrollmaster
         using libname airline 'SAS-library-one';
quit;
proc print data=sasuser.payrollv;
run;
```

如果之前存在 `libref` `AIRLINE` 的赋值，`EMBEDDED LIBNAME` 语句视图执行期间覆盖该赋值。视图执行后，原始的 `libref` 赋值将恢复，嵌入式赋值将被清除。

## 创建视图以增强表安全性
`PROC SQL` 视图的一个优势是它们可以从不同的来源汇总数据。这使得视图可以用于向某些用户屏蔽敏感或机密列，同时允许这些用户查看同一张表中的其他列。

注意：虽然可以使用 `PROC SQL` 视图来增强表安全性，但强烈建议您使用操作系统环境中提供的安全功能。

## 示例
以下 `PROC SQL` 步骤创建了视图 `Manager.Infoview`。该视图访问存储在三个库（`Fa1`、`Fa2` 和 `Fa3`）中的空乘人员数据。可以分配访问权限，以防止：
* 1 级空乘人员读取存储在 `Fa2` 和 `Fa3` 中的数据
* 2 级空乘人员读取存储在 `Fa1` 和 `Fa3` 中的数据
* 3 级空乘人员读取存储在 `Fa1` 和 `Fa2` 中的数据

还可以分配访问权限，允许允许访问所有库的经理查看所有信息。

```
proc sql;
   create view manager.infoview as
      select *
         from fa1.info
      outer union corr
      select *
         from fa2.info
      outer union corr
      select *
         from fa3.info;
```

# 更新 PROC SQL 视图

## 概述
您可以在以下条件下使用 `INSERT`、`DELETE` 和 `UPDATE` 语句更新 `PROC SQL` 视图的底层数据：
* 您只能通过视图更新单个表。表不能与其他表连接，也不能包含子查询。
* 您可以使用别名更新列，但不能更新派生列（通过表达式产生的列）。
* 您可以更新包含 `WHERE` 子句的视图。`WHERE` 子句可以在 `UPDATE` 子句中指定，也可以在视图中指定。您不能更新包含其他子句（如 `ORDER BY` 或 `HAVING`）的视图。
* 您不能更新汇总视图（包含 `GROUP BY` 子句的视图）。

更新视图不会更改存储的视图指令。只有底层表的数据会被更新。

## 示例
以下 `PROC SQL` 步骤创建了视图 `Sasuser.Raisev`，它包含 `Salary` 和 `MonthlySalary` 列。随后的引用该视图的查询将显示这些列。

```
proc sql;
   create view sasuser.raisev as
      select empid, jobcode, 
             salary format=dollar12., 
             salary/12 as MonthlySalary
             format=dollar12.
         from payrollmaster;

proc sql;
   select *
      from sasuser.raisev
      where jobcode in ('PT2','PT3');
```





假设你想更新视图，以显示工作代码为 `PT3` 的员工薪资增加。你可以使用 `UPDATE` 语句来更改 `Salary` 列，并在 `UPDATE` 子句中使用 `WHERE` 子句来识别 `JobCode` 值等于 `PT3` 的行。虽然 `MonthlySalary` 是派生列，无法使用 `UPDATE` 语句进行更改，但因为它派生自 `Salary`，所以它也会被更新。当提交 `PROC SQL` 步骤时，SAS 日志中会出现一条注释，指示更新了多少行数据：

```
proc sql;
   update sasuser.raisev
      set salary=salary * 1.20 
      where jobcode='PT3';
```

表 7.3 SAS 日志

| |
| :--- |
| ```
116   proc sql;
117      update sasuser.raisev
118         set salary=salary * 1.20
119         where jobcode='PT3';
NOTE: 2 rows were updated in SASUSER.RAISEV.
``` |

注意：记住，更新是在视图 `Sasuser.Raisev` 的底层表中进行的。当你重新提交查询时，`JobCode` 等于 `PT3` 的行中将出现 `Salary` 和 `MonthlySalary` 的更新值：

| |
| :--- |
| ```
proc sql;
   select *
      from sasuser.raisev
      where jobcode in ('PT2','PT3');
``` | ![带有更新值的 Sasuser.Raisev 视图](img/m75-14-g2.png) |

# 删除 PROC SQL 视图

## 概述

要删除视图，请使用 `DROP VIEW` 语句。

`DROP VIEW` 语句的一般形式：`DROP VIEW view-name-1 <,...view-name-n>;`
以下是对该语法的解释：`view-name` 指定任意类型的 SAS 数据视图（`PROC SQL` 视图或 `DATA` 步骤视图），并可以是以下内容之一：

* 单级名称
* 二级库引用（libref）和视图名
* 用单引号括起来的物理路径名。

## 示例

以下 `PROC SQL` 步骤删除了视图 `Sasuser.Raisev`。提交步骤后，SAS 日志中会出现一条消息，确认视图已删除。

```
proc sql;
   drop view sasuser.raisev;
```

表 7.4 SAS 日志

| |
| :--- |
| ```
21   proc sql;
22      drop view sasuser.raisev;
NOTE: View SASUSER.RAISEV has been dropped.
``` |

## 总结

## 文本总结

### 使用 PROC SQL 视图

`PROC SQL` 视图是一个存储的查询，当你在 SAS 过程或 `DATA` 步骤中使用该视图时会执行它。视图仅包含描述符以及从其他 SAS 文件（SAS 数据文件、`DATA` 步骤视图或其他 `PROC SQL` 视图）或外部文件（DBMS 数据文件）检索数据值所需的其他信息。在执行时，`PROC SQL` 视图的输出可以是一个或多个底层文件的子集或超集。视图不包含数据，但描述或定义了存储在其他处的数据。`PROC SQL` 视图：

* 可以在 SAS 程序中代替实际的 SAS 数据文件
* 可以与表或其他视图进行连接
* 可以派自一个或多个表、`PROC SQL` 视图、`DATA` 步骤视图或 SAS/ACCESS 视图。
* 提取底层数据，使你能够访问最新数据。

由于 `PROC SQL` 视图不是数据的独立副本，因此它们被称为虚拟表。它们不像真实表那样作为独立实体存在。然而，视图使用了与表相同的命名约定，并可以在 SAS 程序中代替实际的 SAS 表。与表一样，视图被视为 SAS 数据集。

### 创建 SQL 视图

你使用 `CREATE VIEW` 语句来创建视图。`PROC SQL` 视图的数据派自 `FROM` 子句中列出的表或视图。视图访问的数据是其底层表（或）或视图（或）中数据的子集或超集。当在 SAS 过程或 `DATA` 步骤中引用视图时，它会被执行，从概念上讲，会构建一个内部表。`PROC SQL` 处理此内部表的方式就像处理任何其他表一样。在随后的 `PROC SQL` 步骤中，可以像使用实际的 SAS 表一样使用视图。

### 显示 PROC SQL 视图的定义

你可以使用 `DESCRIBE VIEW` 语句在 SAS 日志中显示视图的定义。

### 管理 PROC SQL 视图

`FROM` 子句中表或多个表的默认库引用（libref）是包含视图的库的库引用。使用单级名称可以避免在你为包含视图及其组成表的 SAS 库分配不同的库引用时必须更改视图。作为在 `FROM` 子句中省略库引用的更灵活的替代方案，如果你想在视图中存储 SAS 库引用，可以在使用句的 `USING` 子句中嵌入 `LIBNAME` 语句。在 `USING` 子句中嵌入 `LIBNAME` 语句不会与 SAS 会话中同名的库引用发生冲突。`PROC SQL` 视图的一个优势是它们可以从不同的来源汇集数据。这使得视图可以用于防止某些用户访问某些敏感或机密列，同时允许这些用户查看同一张表中的其他列。尽管 `PROC SQL` 视图可以增强数据安全，但建议你使用操作环境中提供的安全功能来维护数据安全。

### 更新 PROC SQL 视图

在满足以下条件下，可以使用 `INSERT`、`DELETE` 和 `UPDATE` 语句更新视图的底层数据：

* 只能通过视图更新单个表。表不能与其他表连接，也不能包含子查询。
* 可以表达式更新列，但不能更新派生列。
* 可以更新包含 `WHERE` 子句的视图。`WHERE` 子句可以在 `UPDATE` 子句中。
* 不能更新汇总视图（包含 `GROUP BY` 子句的视图）。

## 示例程序

### 删除 PROC SQL 视图

要删除视图，请使用 `DROP VIEW` 语句。

### 创建 PROC SQL 视图

```
proc sql;
   create view sasuser.raisev as
      select empid, jobcode, 
             salary format=12., 
             salary/12 as MonthlySalary
             format=12.
         from payrollmaster
         using libname 'c:\data';
quit;
```

### 显示 PROC SQL 视图的定义

```
proc sql;        
   describe view sasuser.raisev;
quit;
```

### 在查询中使用 PROC SQL 视图

```
proc sql;
   select *
      from sasuser.raisev
      where jobcode in ('PT2','PT3');
quit;
```

### 更新 PROC SQL 视图

```
proc sql;
   update sasuser.raisev
      set salary=salary * 1.20 
      where jobcode='PT3';
quit
```

### 删除 PROC SQL 视图

```
proc sql;
   drop view sasuser.raisev;
quit;
```

# 测验

为每个问题选择最佳答案。完成测验后，使用附录中的答案对照检查你的答案。

1. 关于 `PROC SQL` 视图，哪个陈述是错误的？

    1. 视图不能与其他表进行连接。
    2. 视图访问最新的底层数据。
    3. 视图遵循与表相同的命名约定。
    4. 视图可以在 SAS 程序中代替实际的 SAS 数据文件。





## 2. 下述哪个语句描述了使用 PROC SQL 视图的优点？

1. 视图通常可以节省空间，因为与其访问的数据相比，视图通常非常小。
2. 视图可以防止用户不断提交查询来忽略不需要的列或行。
3. 视图可以向用户隐藏复杂的连接或查询。
4. 以上所有。

## 3. 下述哪一个 `PROC SQL` 步骤创建了一个查询表 `Sasuser.Payrollmaster` 的视图？

1. ```sql
proc sql;
   insert into sasuser.newview
      select * from sasuser.payrollmaster;
```
2. ```sql
proc sql;
   create sasuser.newview as
      select * from sasuser.payrollmaster;
```
3. ```sql
proc sql;
   create view sasuser.newview as
      select * from sasuser.payrollmaster;
```
4. ```sql
proc sql;
   select * from sasuser.payrollmaster
      into view sasuser.newview;
```

## 4. 下述哪一个 `PROC SQL` 步骤允许你查看视图定义的描述？

1. ```sql
proc sql;
   select * from sasuser.payrollmasterv;
```
2. ```sql
proc sql;
   describe view sasuser.payrollmasterv;
```
3. ```sql
proc sql;
   list sasuser.payrollmasterv;
```
4. ```sql
proc sql;
   contents view=sasuser.payrollmasterv;
```

## 5. 下述哪一个 `PROC SQL` 步骤正确引用了视图 `Data.Empview`？

1. ```sql
proc sql;
   select *
      from data.empview;
```
2. ```sql
proc sql; 
   select * 
      from view data.empview;
```
3. ```sql
proc sql; 
   select view * 
      from data.empview;
```
4. ```sql
proc sql; 
   select * 
      from data
      where view='empview';
```

## 6. 下述哪一个 `PROC SQL` 步骤正确地将 `LIBNAME` 语句嵌入到视图定义中？

1. ```sql
proc sql;
   insert into sasuser.newview
      select * from airline.supervisors
         libname airline 'c:\mysql';
```
2. ```sql
proc sql;
   create view sasuser.newview as
      from airline.supervisors
         embed libname airline 'c:\mysql';
```
3. ```sql
proc sql;
   using airline 'c:\mysql';
      insert into sasuser.newview
         select * from airline.supervisors;
```
4. ```sql
proc sql;
   create view sasuser.newview as
      select * from airline.supervisors
         using libname airline 'c:\mysql';
```

## 7. `PROC SQL` 视图可以访问来自以下的数据：

1. SAS 数据文件。
2. 另一个 `PROC SQL` 视图。
3. 关系数据库表。
4. 以上所有。

## 8. 当你使用 `PROC SQL` 视图时，最好是：

1. 避免在视图中使用 `ORDER BY` 子句。
2. 避免创建基于结构可能发生变化的表的视图。
3. 如果视图与贡献表位于同一个 SAS 库中，请在 `FROM` 子句中指定单级名称。
4. 以上所有。

## 9. 在下列条件下，你可以使用 `INSERT`、`DELETE` 和 `UPDATE` 语句更新 `PROC SQL` 视图的底层数据：

1. 视图与另一个表连接或链接。
2. 视图包含子查询。
3. 视图包含 `WHERE` 子句。
4. 以上所有。

## 10. 下述哪个程序删除了（drops）一个视图？

1. ```sql
proc sql;
   delete sasuser.newview;
```
2. ```sql
proc sql;
   drop view sasuser.newview;
```
3. ```sql
proc sql;
   erase view sasuser.newview;
```
4. ```sql
proc sql;
   remove newview from sasuser;
```

# 第 8 章：使用 PROC SQL 管理处理

- 概述
- 指定 SQL 选项
- 控制执行
- 控制输出
- 测试和评估性能
- 重置选项
- 使用字典表
- 其他功能
- 总结
- 测验

## 概述

## 引言
`SQL` 过程提供了多种控制处理的选项。某些选项控制执行。例如，你可以限制行数。其他选项控制输出。例如，你可以控制列的显示。选项也用于测试。元数据存储在字典表中，字典是关于 SAS 库、数据集和外部文件的只读 SAS 表。字典表包含设置。

# 指定 SQL 选项
记住 `PROC SQL` 选项是在 `proc sql` 语句中指定的。

通用形式，`proc sql <option(s)>;` 这里的语法 `option(s)` 指定要使用的 `option(s)`。

> 在指定一个选项后，它将一直生效，直到你更改它或重新调用 `PROC SQL`。下表列出了本章涵盖的控制处理选项。每个选项的完整描述出现在后续。

### 表 8.1 控制执行的选项
| 执行操作 | 使用此选项... |
| --- | --- |
| 限制输入行数 | `INOBS=` |
| 限制输出行数 | `OUTOBS=` |

### 表 8.2 控制输出的选项
| 执行操作 | 使用此选项... |
| --- | --- |
| 输出双倍行距 | `DOUBLE` 或 `NODOUBLE` |
| 列内字符换行 | `FLOW`、`NOFLOW` 或 `FLOW=n` |

### 表 8.3 测试和评估性能的选项
| 执行操作 | 使用此选项... |
| --- | --- |
| 指定 `PROC SQL` 将每个语句的时间信息写入 SAS 日志 | `STIMER`, `NOSTIMER` |

注意：完整的选项列表请参阅 SQL 过程文档。

# 控制执行

### 限制行处理
针对大表开发查询时，可以通过减少 `PROC SQL` 处理的行数来缩短查询运行时间。使用 `WHERE` 子句划分表集是一种方法。在 `PROC SQL` 中 `INOBS=` 和 `OUTOBS=` 选项是另一种方法。你已经知道可以使用 `OUTOBS=` 选项限制 `PROC SQL` 显示或写入到表的行数。然而，`OUTOBS=` 选项并不限制读取的行。`INOBS=` 选项限制了 `PROC SQL` 从任何单一源输入的行数。`INOBS=` 选项类似于 SAS 系统选项 `OBS=`，适用于调试大表查询。](p184saqukbcv03n1cd6lhu2v2ias.htm)





在接下来的 `PROC SQL` 操作中，指定了 `INOBS=5`。正如日志所示，每个源表 `Sasuser.Mechanicslevel1` 和 `Sasuser.Mechanicslevel2` 仅使用了前五行。生成的表包含 10 行。

```
proc sql inobs=5;
   select *
      from sasuser.mechanicslevel1
   outer union corr
   select *
      from sasuser.mechanicslevel2;
```

表 8.4 SAS 日志

|     

```
183   proc sql inobs=5;
184     select *
185        from sasuser.mechanicslevel1
186     outer union corr
187     select *
188        from sasuser.mechanicslevel2;

WARNING: Only 5 records were read from SASUSER.MECHANICSLEVEL1
         due to INOBS= option.
WARNING: Only 5 records were read from SASUSER.MECHANICSLEVEL2
         due to INOBS= option.
```

 |

![sas log](img/m76-3-g1.png)提示：你可以将 `PROMPT | NOPROMPT` 选项与 `INOBS=` 和 `OUTOBS=` 选项配合使用，以便在达到这些选项设置的限制时提示停止或继续处理。注意：关于 PROC SQL 设置 操作的更多信息，请参考使用 PROC SQL 垂直合并表。警告：在简单查询中，使用 `INOBS=` 或 `OUTOBS=` 可能没有明显区别。其他时候，选择正确的选项非常重要。例如，对带有 `PROC SQL` 选项 `INOBS=10` 的列使用平均函数，返回的是该列读取的 10 个值的平均值。

# 控制输出

## 包含行号列

`NUMBER | NONUMBER` 选项指定查询输出是否包含一个名为 `ROW` 的列，该列显示行号。`NONUMBER` 是默认值。该选项类似于 `PRINT` 过程中的 `NOOBS` 选项。

## 示例

以下 `PROC SQL` 步骤指定了 `NUMBER` 选项。该步骤的输出包含一个名为 `Row` 的列，其中包含行号。

|     

```
proc sql inobs=10 number;
   select flightnumber, destination 
      from sasuser.internationalflights;
```

 | ![PROC SQL Output with Number Option](img/m76-7-g1.png) |

## 双倍间距输出

在某些情况下，将输出双倍间距可以更容易阅读。`DOUBLE | NODOUBLE` 选项指定 `PROC SQL` 输出是否为双倍间距。默认是 `NODOUBLE`。注意：`DOUBLE | NODOUBLE` 选项不影响 HTML、PDF 或 RTF 输出的外。要查看此选项的效果，请在 SAS Enterprise Guide 中选择文本。

## 示例

以下 `PROC SQL` 步骤指定了 `DOUBLE` 选项。该步骤的列表输出为双倍间距。该步骤的 HTML 输出保持为单倍间距。

```
proc sql inobs=10 double; 
   select flightnumber, destination 
      from sasuser.internationalflights;
```

图 8.1 列表输出![Listing Output](img/m76-8-g2.png)图 8.2 HTML 输出![HTML Output](img/m76-8-g1.png)

## 列内字符流

`FLOW | NOFLOW | FLOW=n | FLOW=n m` 选项控制列表输出中宽字符列的外观。`FLOW` 选项导致文本在列内流，而不是换行整行。指定 `n` 可设置流式列的宽度。指定 `n` 和 `m` 则让列宽在限制之间浮动，以实现平衡布局。注意：`FLOW | NOFLOW | FLOW=n | FLOW=nm` 选项不影响 HTML、PDF 或 RTF 输出的外。要查看此选项的效果，请在 SAS Enterprise Guide 中选择文本输出。

## 示例

以下 `PROC SQL` 步骤未指定 `FLOW` 选项。注意在输出中，由于宽字符列的存在，`ZipCode` 列的名称和值出现在 `FFID` 列的名称和值下方。

```
proc sql inobs=5;
   select ffid, membertype, name, address, city, 
          state, zipcode
      from sasuser.frequentflyers
      order by pointsused;
```

图 8.3 未使用 FLOW 选项 PROC SQL 步骤输出![Output from PROC SQL Step without FLOW Option](img/m76-9-g1.png)指定 `flow=10 15` 会导致字符列内的文本在 10 到 15 个空格之间浮动，防止 `ZipCode` 列换行到 `FFID` 列下方。

```
 proc sql inobs=5 flow=10 15;
    select ffid, membertype, name, address, city, 
           state, zipcode
       from sasuser.frequentflyers
       order by pointsused;
```

图 8.4 使用 FLOW 选项 PROC SQL 步骤输出![Output from PROC SQL Step with FLOW Option](img/m76-9-g2.png)

# 测试和评估性能

## 为每个语句编写计时信息

`PROC SQL` 选项 `STIMER | NOSTIMER` 指定 `PROC SQL` 是否将每条语句的计时信息写入 SAS 日志，而不是写入整个过程的累积值。`NOSTIMER` 是默认值。为了在 `PROC SQL` 中使用 `STIMER` 选项，必须启用 SAS 系统选项 `STIMER`（默认）。某些主机环境要求你指定 SAS 系统选项。`STIMER` 控制 SAS 日志中性能统计信息的打印。如果你仅使用系统选项，结果将包含整个过程的计时信息。你可以使用 `OPTIONS` 过程列出 SAS 的当前设置。要检查是否已启用 `STIMER` 选项，请提交以下语句：

表 8.5 SAS 日志

|    

```
Option Value Information For SAS Option STIMER
    Option Value: STIMER
    Option Scope: SAS Session
    How option set: Shipped Default
```

注意：PROC OPTIONS 会产生特定于你运行 SAS 的操作环境的额外信息。有关此的更多信息以及主机特定选项的说明，请参阅 文档。

## 示例

以下 `PROC SQL` 步骤中的两个查询都列出了 `Sasuser.Frequenters` 表中客户的名称、地址、城市、州和邮政编码。然而，第二个查询仅列出了积分超过 7000 且少于 3000 的客户信息。当提交 `PROC SQL` 语句且没有 `STIMER` 选项时，两个查询的计时信息将作为整个过程的累积值写入 SAS 日志。

```
proc sql;        
   select name, address, city, state, zipcode 
      from sasuser.frequentflyers;
   select name, address, city, state, zipcode 
      from sasuser.frequentflyers  
      where pointarned gt 7000 and pointsused lt 3000;
quit;
```

注意：PROC SQL 步骤的计时信息在提交 `QUIT` 语句或开始另一个 `PROC` 或 `DATA` 步骤之前写入 SAS 日志。

表 8.6 SAS 日志

|     

```
28   proc sql;
29   select name, address, city, state, zipcode
30       from sasuser.frequentflyers;
31   select name, address, city, state, zipcode
32       from sasuser.frequentflyers
33     where pointsearned gt 7000 and pointsused lt 3000;
34   quit;
NOTE: PROCEDURE SQL used (Total process time):
      real time 0.34 seconds 
      cpu time 0.30 seconds
```

 |

当提交带有 `STIMER` 选项的 `PROC SQL` 语句时，计时信息将为每条 `SELECT` 语句写入 SAS 日志。

```
proc sql stimer;        
   select name, address, city, state, zipcode 
      from sasuser.frequentflyers;
   select name, address, city, state, zipcode 
      from sasuser.frequentflyers  
      where pointsearned gt 7000 and pointsused lt 3000;
quit;
```

表 8.7 SAS 日志

|  





```
33   proc sql stimer;
NOTE: SQL Statement used (Total process time):  
      real time           0.00 seconds  
      cpu time            0.00 seconds

34 select name, address, city, state, zipcode 
     from sasuser.frequentflyers;
NOTE: SQL Statement used (Total process time):
      real time 0.22 seconds 
      cpu time 0.17 seconds

35 select name, address, city, state, zipcode
     from sasuser.frequentflyers
36   where pointsearned gt 7000 and pointsused lt 3000;
NOTE: SQL Statement used (Total process time):  
      real time 0.25 seconds
      cpu time 0.08 seconds

37 quit;
NOTE: PROCEDURE SQL used (Total process time): 
      real time 0.29 seconds  
      cpu time 0.03 seconds
```

注意：当在 `PROC SQL` 中使用 `STIMER` 时，写入 SAS 日志的注释（Notes）的确切措辞可能会根据 SAS 版本的不同而变化。注意：当某个操作可以通过多种方式完成且你正在对这些技术进行基准测试时，`PROC SQL` 中的 `STIMER` 选项非常有用。尽管需要考虑代码的可读性和维护性，你可能也想知道哪个 `PROC SQL` 步骤运行最快。

# 重置选项

## 概述

在指定一个选项后，它将一直有效，直到你更改它或重新调用 `PROC SQL`。你可以使用 `RESET` 语句添加、删除或更改 `PROC SQL` 选项，而无需重新调用 SQL 过程。

| 通用格式，`RESET` 语句：`RESET <option(s)>;` 以下是对语法的解释：`option(s)` 以任意顺序列出选项。 |

选项是累加的。例如，你可以在 `PROC SQL` 语句中指定 `NOPRINT` 选项，提交查询，然后提交带有 `NUMBER` 选项的 `RESET` 语句，而不会影响 `NOPRINT` 选项。

## 示例

假设你想在一个 `PROC SQL` 步骤中提交两个 `PROC SQL` 查询。你希望

* 两个查询都只输出前五行
* 第二个查询在输出中显示行号

在接下来的 `PROC SQL` 步骤中，`PROC SQL` 语句指定了 `OUTOBS=` 选项来限制输出的行数。在第一个 `SELECT` 语句之后，`RESET` 语句添加了 `NUMBER` 选项在结果集中显示行号。

```
proc sql outobs=5;
   select flightnumber, destination 
      from sasuser.internationalflights;
reset number;
   select flightnumber, destination 
      from sasuser.internationalflights
      where boarded gt 200;
```

输出包含两个结果集，如下所示。第一个 `SELECT` 语句的结果集仅反映了 `OUTOBS=` 选项的影响。第二个 `SELECT` 语句的结果集则反映了 `OUTOBS=` 选项和 `RESET` 语句中指定的 `NUMBER` 选项。

| ![使用 OUTOBS= 选项的 PROC SQL 输出](img/m76-16-g1.png) | ![使用 OUTOBS= 和 NUMBER 选项的 PROC SQL 输出](img/m76-16-g2.png) |

现在，假设你想修改 `PROC SQL` 步骤，使得仅第一个 `SELECT` 语句的结果集限制为五行输出。在修改后的 `PROC SQL` 步骤中，`RESET` 语句添加了 `OUTOBS=` 选项，以更改（重置）`PROC SQL` 语句指定的 `OUTOBS=` 选项。修改后的步骤如下：

```
 proc sql outobs=5;
    select flightnumber, destination 
       from sasuser.internationalflights;
 reset outobs= number;
    select flightnumber, destination 
       from sasuser.internationalflights
       where boarded gt 200;
```

在输出中，第二个 `SELECT` 语句的结果集现在包含了查询生成的所有行。

| ![带有 OUTOBS=5 的 PROC SQL](img/m76-16-g3.png) | ![重置 OUTOBS= 的 PROC SQL](img/m76-16-g4.png) |

# 使用字典表

## 概述

字典表（Dictionary tables）通常用于监控和管理 SAS 会话，因为 own 数据比来自 `PROC DATASETS` 等过程的输出更容易处理。字典表是特殊的只读 SAS 表，包含有关当前 SAS 会话正在使用或可用的 SAS 库、SAS 宏和外部文件的信息。字典表还包含当前生效的 SAS 系统选项以及 SAS 标题（titles）和脚注（footnotes）。例如，`Dictionary.Columns` 表包含有关当前 SAS 会话已知的所有表中所有列的信息（如名称、类型、长度和格式）。字典表具有以下特点：

* 每次在 SAS 程序中被引用时都会创建
* 自动更新
* 仅限只读

访问字典表会导致 SAS 确定 SAS 会话的当前状态并返回你需要的信息。可以通过针对 `Dictionary` 库引用（libref）运行 `PROC SQL` 查询来访问字典表。虽然 SAS 库引用通常限于 8 个字符，但 `Dictionary` 是一个自动分配的保留字。你也可以通过引用 `PROC SQL` 视图来访问字典表，该视图存储在 `Sashelp` 库中。下表描述了部分字典表及其对应的视图。要查看完整的字典表列表，请参阅 SQL 过程文档。

| 字典表 | Sashelp 视图 | 包含 |
| --- | --- | --- |
| Catalogs | Vcatalg | 目录项信息 |
| Columns | Vcolumn | 变量详细信息 |
| Extfiles | Vextfl | 当前分配的文件引用 |
| Indexes | Vindex | 数据索引信息 |
| Macros | Vmacro | 用户和系统定义的宏变量 |
| Members | Vmember | 库成员信息 |
| Options | Voption | 系统选项设置 |
| Tables | Vtable | 数据集的详细信息 |
| Titles | Vtitle | 分配给标题和脚注的文本 |
| Views | Vview | 数据视图的基本信息 |

## 使用字典表

你可以像查询其他表一样查询字典表，包括使用 `WHERE` 子句进行筛选、排序结果、创建表以及创建 `PROC SQL` 视图。由于字典表是只读对象，你无法为其插入行或列、更改列属性或添加完整性约束。要查看每个字典表的定义，请提交 `DESCRIBE TABLE` 语句。`DESCRIBE TABLE` 语句会在 SAS 日志中写入指定表的 `CREATE TABLE` 语句。在了解表的定义方式后，你可以在 `WHERE` 子句中使用其列名来检索特定信息。

## 示例

`Dictionary.Tables` 表包含表的详细信息。接下来的 `DESCRIBE TABLE` 语句会在日志窗口中显示 `Dictionary.Tables` 表的信息。这些信息包含了表中存储的列名。

```
proc sql;
   describe table dictionary.tables;
```

表 8.8 SAS 日志

|  

```
create table DICTIONARY.TABLES  
  (  
   libname char(8) label='Library Name', 
   memname char(32) label='Member Name', 
   memtype char(8) label='Member Type',  
   memlabel char(256) label='Dataset Label',  
   typemem char(8) label='Dataset Type', 
   crdate num format=DATETIME informat=DATETIME label='Date Created', 
...);
``` |

要显示特定库的文件信息，请在 `SELECT` 语句中指定列名，并在 `FROM` 子句中指定字典表名。例如，接下来的 `PROC SQL` 步骤将显示 Sasuser 库中表的

* Memname（成员名）
* Nobs（观测值数）
* Nvar（变量数）
* Crdate（创建日期）




字典列名在 `SELECT` 语句中指定，而字典表 `Dictionary.Tables` 则在 `FROM` 子句中指定。库名 `Sasuser` 在 `WHERE` 子句中指定。
**注意**：请注意，你必须在 `WHERE` 子句中使用大写字母指定库名（因为 SAS 内部是这样存储的），并用引号括起来。

```
proc sql;
   select memname format=$20., nobs, nvar, crdate
      from dictionary.tables
      where libname='SASUSER';
```

下方显示了部分输出。![Dictionary.Tables](img/m76-20-g1.png)
注意：`ALL` 的 `nobs` 值缺失是因为它是一个视图而不是表。注意：你的输出可能与上述所示有所不同，这取决于你的 `Sasuser` 库中的内容。你也可以使用字典表来确定更具体的信息，例如 SAS 库中的哪些表包含特定的列。

## 示例

`Dictionary.Columns` 表包含关于变量及其属性的详细信息。与 `Dictionary.Tables` 类似，`Dictionary.Columns` 表包含一个名为 `Memname` 的列，列出了库中每个表的名称。

```
proc sql;
   describe table dictionary.columns;
```

表 8.9 SAS 日志

| |

```
create table DICTIONARY.COLUMNS  
  (   
   libname char(8) label='Library Name',  
   memname char(32) label='Member Name', 
   memtype char(8) label='Member Type', 
   name char(32) label='Column Name', 
   type char(4) label='Column Type', 
   length num label='Column Length',
...);
```
 |

下面的 `PROC SQL` 步骤列出了 `Sasuser` 库中所有包含名为 `EmpID` 列的表。字典列名 `Memname` 在 `SELECT` 语句中指定。字典表 `Dictionary.Columns` 在 `FROM` 子句中指定。库名 `Sasuser` 和列名 `EmpID` 在 `WHERE` 子句中指定。

```
proc sql;
   select memname
      from dictionary.columns
      where libname='SASUSER'
            and name='EmpID';
```

下方显示了部分输出。![Partial output](img/m76-21-g1.png)记住，你也可以通过引用存储在 `sashelp` 库中的 `PROC SQL` 视图来访问字典表。在接下来的 `PROC PRINT` 步骤中，`DATA=` 选项指定了 `Sashelp` 视图 `Vcolumn`。`PROC PRINT` 步骤的结果与之前的输出相同。

```
proc print data=sashelp.vcolumn;
   var memname;
   where libname='SASUSER' and name='EmpID';
run;
```

**注意**：请注意 `WHERE` 子句中的列名必须与字典表使用的大小写一致，并必须用引号括起来。注意：你可以在任何 SAS 过程或 `DATA` 步骤中使用 `Sashelp` 视图。然而，字典表只能通过 SQL 过程读取。

### 附加功能

## 限制循环次数

`LOOPS=` 选项限制了 `PROC SQL` 中内部循环的迭代次数。通过设置限制，你可以防止查询消耗过多资源。例如，在连接三个大表时不满足连接匹配条件，可能会创建一个巨大的内部表，处理起来效率极低。使用 `LOOPS=` 选项可以防止这种情况发生。你可以使用 `PROMPT | NOPROMPT` 选项来修改 `LOOPS=` 选项的效果，当达到 `LOOPS=` 选项设置的限制时，提示你停止或继续处理。注意：你可以使用 `SQLOOPS` 宏变量中报告的迭代次数（在执行每个 `PROC SQL` 语句后）来衡量 `LOOPS=` 选项的合适值。有关关于 `SQLOOPS` 宏变量的更多信息，请参阅 SQL 过程的 SAS 文档。

## 在 PROC SQL 中遇到错误后停止执行

你已经知道可以使用 `EXEC | NOEXEC` 选项来指定在通过语法准确性检查后是否执行该语句。如果 `EXEC` 选项生效，SAS 会检查 `PROC SQL` 语法的准确性，如果没有发现错误，则执行 SQL 语句。`ERRORSTOP | NOERRORSTOP` 选项指定 `PROC SQL` 在遇到错误时是否停止执行。该选项仅在 `EXEC` 选项生效时有用。在批处理或非交互式会话中默认为 `ERRORSTOP`，在交互式 SAS 会话中默认为 `NOERRORSTOP`。`ERRORSTOP` 指示 `PROC SQL` 停止执行语句，但在遇到错误后继续检查语法。`ERRORSTOP` 只在 SAS 以批处理或非交互式执行模式运行时有效。`NOERRORSTOP` 指示 `PROC SQL` 执行语句并在发生后继续检查语法。如果你希望批处理作业在遇到错误后继续执行 SQL 过程语句，则 `NOERRORSTOP` 非常有用。

## 总结

## 内容总结

### 指定 SQL 选项

SQL 过程提供了多种影响处理的选项。某些选项控制执行。例如，你可以限制查询期间读取或写入的行数，或者限制 `PROC SQL` 执行的内部循环次数。其他选项控制输出。例如，你可以对输出进行流式处理或编号。还有用于测试和评估性能的选项。这些选项指定在 `PROC SQL` 语句中。

### 限制行处理

`OUTOBS=` 选项限制 `PROC SQL` 显示或写入表的行数。`INOBS=` 选项限制 `PROC SQL` 从任何源获取的行数。`INOBS=` 选项类似于 SAS 系统选项 `OBS=`，对于调试大型表很有用。

### 控制输出

`NUMBER | NONUMBER` 选项指定 `SELECT` 语句是否包含名为 `ROW` 的列，该列是数据检索时的行号。`NONUMBER` 是默认值。该选项类似于 `PRINT` 过程中的 `NOOBS` 选项。在某些情况下，对输出进行双倍行距更容易阅读。`DOUBLE | NODOUBLE` 选项指定 `PROC SQL` 输出是否使用双倍行距。默认值为 `NODOUBLE`。`FLOW | NOFLOW | FLOW=n| FLOW=n m` 选项控制列表输出中宽列的形式。`FLOW` 选项导致文本在列内流动而不是换行整行。指定 `n` 设置流动宽度。指定 `n` 和 `m` 则在范围内浮动宽度以实现平衡布局。

### 测试和评估性能

`STIMER | NOSTIMER` 选项指定 `PROC SQL` 是否向 SAS 日写入每个语句的时间信息，以及整个过程的累计值。`NOSTIMER` 是默认值。为了在 `PROC SQL` 中使用 `STIMER` 选项，必须同时启用 SAS 系统选项 `STIMER`（默认值）。

### 重置选项

指定一个选项后，它将一直有效直到你更改它或重新调用 `PROC SQL`。你可以使用 `RESET` 语句在不重新调用 SQL 过程的情况下添加、删除或更改 `PROC SQL` 选项。

### 使用字典表





SAS 会话元数据存储在字典表（Dictionary tables）中，这些是特殊的只读 SAS 表，包含有关当前 SAS 会话中可用 SAS 库、SAS 宏和外部文件的信息。字典表还包含当前生效的 SAS 系统选项设置，以及 SAS 标题（Titles）和脚注（Footnotes）。访问字典表会导致 `PROC SQL` 确定 SAS 会话的当前状态并返回您想要的信息。可以通过使用 `Dictionary` 库引用对该表运行 `PROC SQL` 查询来访问字典表。您也可以引用存储在 `Sashelp` 库中的表的 `PROC SQL` 视图来访问字典表。

要查看每个字典表的定义情况，请提交 `DESCRIBE TABLE` 语句。在了解表的定义后，您可以在子集 `WHERE` 子句中使用其列名来检索特定信息。要显示特定库中文件的信息，请在 `SELECT` 语句中指定列名，并在 `FROM` 子句中指定字典表名。您还可以使用字典表来确定更具体的信息，例如 SAS 库中的哪些表包含特定列。

###附加功能

`LOOPS=` 选项限制了 `PROC SQL` 中内部循环的迭代次数。通过设置限制，可以防止查询消耗过多资源。`ERRORSTOP | NOERRORSTOP` 选项指定了 `PROC SQL` 在遇到错误时是否停止执行。

## 示例

### 使用 PROC SQL 选项查询表

```sas
proc sql outobs=5;      
   select flightnumber, destination  
      from sasuser.internationalflights;  
reset number;      
   select flightnumber, destination    
      from sasuser.internationalflights
      where boarded gt 200;
quit;
```

### 描述和查询字典表

```sas
proc sql;
   describe table dictionary.columns;
   select memname
      from dictionary.columns
      where libname='SASUSER'
            and name='EmpID';
quit;
```

## 注意事项

- 在指定选项后，该选项将保持生效，直到您更改它或重新调用 `PROC SQL`。
- `DOUBLE | NODOUBLE` 以及 `FLOW | NOFLOW | FLOW=n| FLOW=n m` 选项不会影响使用输出交付系统（Output Delivery System）创建的 HTML、PDF 或 RTF 输出的外观。
- 如果您查询特定库中文件的字典表，则 `WHERE` 子句中使用的库名必须用大写字母指定，因为在 SAS 中是这样存储的。`WHERE` 子句中使用的列名必须与在字典表中出现的大小写一致。

# 测验

为每道题选择最佳答案。完成测试后，使用附录中的答案检查您的答案。

1. `PROC SQL` 选项指定在：
    1. `PROC SQL` 语句中。
    2. `OPTIONS` 语句中。
    3. `SELECT` 语句中。
    4. `OPTIONS` 过程中。

2. 下列哪个 SQL 选项限制了 `PROC SQL` 从任何单一源获取输入的行数？
    1. `OUTOBS=`
    2. `INOBS=`
    3. `OBS=`
    4. 以上都不是

3. 哪一个 `PROC SQL` 步骤创建了所示输出？![包含 EmpID, JobCode, LastName, FirstName 列的表](img/m76-280.png)![带有行号的表](img/m76-27-g1.png)
    1. ```sas
       proc sql nonumber outobs=10;
           select *
              from sasuser.flightattendants
              where jobcode='FA1';
           select *
              from sasuser.flightattendants
              where jobcode='FA2';
       ```
    2. ```sas
       proc sql number;
           select *
              from sasuser.flightattendants
              where jobcode='FA1';
       reset nonumber outobs=10;
           select *
              from sasuser.flightattendants
              where jobcode='FA2';
       ```
    3. ```sas
       proc sql nonumber;
           select *
              from sasuser.flightattendants
              where jobcode='FA1';
       reset number outobs=10;
           select *
              from sasuser.flightattendants
              where jobcode='FA2';
       ```
    4. ```sas
       proc sql;
           select *
              from sasuser.flightattendants
              where jobcode='FA1';
       reset outobs=10;
            select *
               from sasuser.flightattendants
               where jobcode='FA2';
       ```

4. 下列哪个选项不影响 HTML、PDF 或 RTF 输出的外观？
    1. `NUMBER | NONUMBER`
    2. `DOUBLE | NODOUBLE`
    3. `FLOW | NOFLOW | FLOW=n | FLOW=n m`
    4. b 和 c

5. 关于 `PROC SQL` 中的 `STIMER` 选项，以下哪个陈述是正确的？
    1. `PROC SQL` 中的 `STIMER` 选项会将每个语句的计时信息写入 SAS 日志。
    2. `PROC SQL` 中的 `STIMER` 选项仅将整个过程的累积计时信息写入 SAS 日志。
    3. 使用 `PROC SQL` 中的 `STIMER` 选项时，SAS 系统选项 `STIMER` 必须也生效。
    4. a 和 c

6. 字典表包含以下哪些？
    1. 关于 SAS 库的信息。
    2. 关于数据集的信息。
    3. 关于 SAS 宏的信息。
    4. 以上所有

7. 字典表
    1. 每次在 SAS 程序中引用时创建。
    2. 自动更新。
    3. 限于只读访问。
    4. 以上所有

8. 字典表可以通过可以通过访问：
    1. 使用 `Dictionary` 库引用对表运行 `PROC SQL` 查询。
    2. 引用存储在 `Sashelp` 库中的表的 `PROC SQL` 视图。
    3. 引用存储在 `Sasuser` 库中的表的 `PROC SQL` 视图。
    4. a 和 b

9. 下列哪个 `PROC SQL` 步骤显示字典表 `Dictionary.Titles` 的信息？
    1. ```sas
       proc sql;
           describe dictionary.titles;
       ```
    2. ```sas
       proc sql;
           describe table dictionary.titles;
       ```
    3. ```sas
       proc sql describe table dictionary.titles;
       ```
    4. ```sas
       proc sql describe dictionary titles;
       ```

10. 下列哪个 `PROC SQL` 步骤显示 `Sasuser` 库中每个表的名称（Memname）、修改日期（Modate）、变量数（Nvar）和观测值数（Nobs）？
    1. ```sas
       proc sql;
           select memname, modate, nvar, nobs
              from dictionary.tables
              where libname='SASUSER';
       ```
    2. ```sas
       proc sql;
           select memname, modate, nvar, nobs
              from dictionary.tables
              where libname='Sasuser';
       ```
    3. ```sas
       proc sql;
           select memname, modate, nvar, nobs
              from 'SASUSER'
              where table=dictionary.tables;
       ```
    4. ```sas
       proc sql;
           select SASUSER
              from dictionary.tables
              where cols= 'memname, modate, nvar, nobs';
       ```




- 概述基础概念使用自动宏变量使用用户定义宏变量处理宏变量在 SAS Log 中显示宏变量值使用宏函数掩码特殊字符使用宏函数处理字符串结合 SAS 函数与宏变量宏变量引用与文本结合总结练习

## 概述

## 引言

SAS 宏变量允许你在 SAS 程序中替换文本。宏变量可以提供各种信息，包括：

* 操作系统信息
* SAS 会话信息
* 文本字符串。

当你在 SAS 程序中引用宏变量时，SAS 会将引用替换为分配给该宏变量的文本值。通过在程序中替换文本，SAS 宏变量使你的程序更具重用性和动态。下面的示例显示了如何使用宏变量替换整个程序中的年份值，让你能够快速方便地更改整个程序中的 `year` 值：

```
%let year=2002;
proc print data=sasuser.schedule;
   where year(begin_date)=&year;
   title "Scheduled Classes for &year";
run;
proc means data=sasuser.all sum;
   where year(begin_date)=&year;
   class location;
   var fee;
   title1 "Total Fees for &year Classes";
   title2 "by Training Center";
run;
```

# 基础概念

## 概述

在你编写的 SAS 程序中，你可能会发现需要多次引用同一个变量、数据集或文本字符串。

```
title "Total Sales for 2002";
data perm.sales2002;
   set perm.sales;
   if year(enddate)=2002;
run;
proc print data=perm.sales2002;
run;
```

这时，你可能需要更改程序中的引用，以引用不同的变量、数据集或文本字符串。如果你的程序很长，手动扫描特定引用并更新它们将耗费大量时间，而且很容易忽略需要更新的引用。

```
title "Total Sales for 2001";
data perm.sales2001;
   set perm.sales;
   if year(enddate)=2002;
run;
proc print data=perm.sales2001;
run;
```

如果你在程序中使用宏变量，这些更新将变得快速且简单，因为你只需要在一个地方进行更改。

```
%let year=2002;
title "Total Sales for &year";
data perm.sales&year;
   set perm.sales;
   if year(enddate)=&year;
run;
proc print data=perm.sales&year;
run;
```

宏变量的值会被插入到你的程序中，因此你只需要更改一次，更改就会出现在整个程序中。

## 宏变量

宏变量是 SAS 宏功能的一部分，该功能是一种用于扩展和自定义 SAS，并减少为了执行常用任务时必须输入的程序代码数量的工具。宏功能有其自己的语言，允许你将少量或大量的文本封装成具有名称的单元。从那时起，你就可以使用名称而不是文本本身进行工作。宏变量有两种类型：

* 自动宏变量，由 SAS 提供
* 用户定义宏变量，其值由你创建和定义。

无论是自动还是用户定义的，宏变量都独立于 SAS 数据集，并包含一个文本字符串值，该值在你更改它之前保持不变。在程序引用宏变量的地方，宏变量的值就会被替换到程序中。宏变量的值存储在符号表中。自动宏变量始终存储在全局符号表中，这意味着这些值在你的 SAS 会话中始终可用。用户定义宏变量的值通常也存储在全局符号表中。

```
%let city=Dallas;
%let date=05JAN2000;
%let amount=975;
```

![全局符号表](img/m50-3-g1.png)

宏变量可以在 SAS 程序中的任何地方定义和引用，但数据行内部除外。

## 引用宏变量

为了替换宏变量的值，你必须在宏变量名前加上一个符号符号 `&`。宏处理器会在符号表中查找该变量，如果找到，则将其替换为该值。某些宏变量在 SAS 启动时具有固定值。

### 示例：引用宏变量

要引用符号表中的变量 `amount`，你需要在程序中放置 `&amount`：

```
data new;
   set perm.sales;
   where fee=&amount;
run;
```

### 替换后的代码

```
data new;
   set perm.sales;
   where fee=975;
run;
```

### 示例：在标题中引用宏变量

要在标题中引用宏变量 `city`，你需要使用双引号包含标题文本：

```sas
title "Students from &city";
```

当宏处理器无法解析宏变量时，SAS Log 会打印消息。例如，引用不存在的宏变量会导致警告。引用无效变量名会导致错误。

#### 表 9.1 SAS Log

```
34 title "Students from &cityst";
35 WARNING: Apparent symbolic reference CITYST not resolved.
36 title "Students from "the_city_in_which_the_student_is_located";ERROR: Symbolic variable THE_CITY_IN_WHICH_THE_STUDENT_I must be 32 or fewer characters long.
``` 使用自动宏变量

## 概述

SAS 创建并定义若干自动宏变量。自动宏变量包含有关你计算环境的信息，例如会话的日期和时间以及你运行的 SAS 版本。这些自动宏变量

* 在 SAS 启动时创建
* 是全局的（始终可用）
* 通常由 SAS 分配值
* 在某些情况下可以由用户赋值

某些自动宏变量在 SAS 启动时具有固定值。

| 名称 | 值 |
| --- | --- |
| SYSDATE | SAS 启动的日期 (DATE7.) |
| SYSDATE9 | SAS 启动的日期 (DATE9.) |
| SYSDAY | SAS 启动时的星期几 |
| SYSTIME | SAS 启动的时间 |
| SYSENV | FORE（交互式执行）或 BACK（非交互式或批处理执行） |
| SSCP | 使用的操作系统简称，例如 WIN 或 LINUX |
| SYSVER | 使用的 SAS 版本 |
| SYSJOBID | 当前 SAS 会话或当前批处理作业的标识符（主机的系统的用户 ID 或作业名，其他系统的进程 ID PID） |




一些自动宏变量的值会根据提交的 SAS 语句自动发生变化。

| 名称 | 值 |
| --- | --- |
| `SYSLAST` | 最近创建的 SAS 数据集的名称，格式为 `LIBREF.NAME.` .。此值始终以全大写字母存储。如果没有创建任何数据集，则该值为 `NULL`。注意：在本书中，示例程序经常使用关键字 `NULL` 来代替数据集名称。使用 `NULL` 可以抑制输出数据集的创建。在进行基准测试时使用 `NULL`，可以让你确定读取 SAS 数据集时使用了哪些资源。 |
| `SYSPARM` | 在调用 SAS 时指定的文本 |
| `SYSERR` | 包含由 `DATA` 步和某些 SAS 过程设置的返回代码状态，指示该步或过程是否执行成功 |

## 示例

你可以在报告的脚注中使用系统信息，例如调用 SAS 会话的时间、天、日期以及你正在运行的 SAS 版本。

```
footnote1 "Created &systime &sysday, &sysdate9";
footnote2 "on the &sysscp system using Release &sysver";
title "REVENUES FOR DALLAS TRAINING CENTER";
proc tabulate data=sasuser.all(keep=location course_title fee);
   where upcase(location)="DALLAS";
         class course_title;
         var fee;
         table course_title=" " all="TOTALS",
               fee=" "*(n*f=3\. sum*f=dollar10.)
               / rts=30 box="COURSE";
run;
```

![课程信息](img/m50-9-g1.png)

1. 一天的时间 (`SYSTIME`)
2. 星期几 (`SYSDAY`)
3. 日期（日、月、年） (`SYSDATE9`)
4. 操作系统环境 (`SYSSCP`)
5. SAS 版本 (`SYSVER`)

# 使用用户定义的宏变量

## %LET 语句

你已经看到 SAS 为你提供了各种宏变量。你也可以创建自己的宏变量。定义自定义宏变量最简单的方法是使用 `%LET` 语句。`%LET` 语句允许你定义一个宏变量并为其赋值。

| %LET 语句的一般形式： | `%LET variable=value;` |
| 这里是对语法的解释：`variable` 是任何符合 SAS 命名规范的名称。`value` 可以是从 0 到 65,534 个字符的任何字符串。如果 `variable` 或 `value` 包含对另一个宏变量的引用（例如 `&macvar`），该引用将在赋值之前求值。 |

注意：如果 `variable` 已经存在，则 `value` 将替换当前值。

## 示例

要创建一个名为 `time` 的宏变量并为其赋值值 `afternoon`，你将提交以下 `%LET` 语句：

```
%let time=afternoon;
```

当使用 `%LET` 语句定义宏变量时，你应该记住以下规则：

* 所有值都以字符字符串的形式存储。
* 数学表达式不会被求值。
* 值的的大小会被保留。
* 包围字面量的引号将作为值的一部分存储。
* 在赋值之前，会删除值前后的空白字符。

## %LET 语句示例

在定义宏变量时，请记住它的值始终是一个字符字符串。下表提供了宏变量赋值的示例，以说明上一节列出的规则。

| %LET 语句 | 变量名 | 变量值 | 长度 |
| --- | --- | --- | --- |
| `%let name= Ed Norton ` | `name` | ` Ed Norton ` | 9 |
| `%let name2=' Ed Norton ';` | `name2` | `' Ed Norton ` | 13 |
| `%let title="Joan's Report";` | `title` | `"Joan's Report"` | 15 |
| `%let start=;` | `start` | | 0 |
| `%let total=0;` | `total` | `0` | 1 |
| `%let sum=4+3;` | `sum` | `4+3` | 3 |
| `%let total=&total+&sum` | `total` | `0+4+3` | 5 |
| `%let x=varlist;` | `x` | `varlist` | 7 |
| `%let &x=name height;` | `varlist` | `name height` | 15 |

在接下来的示例中，值 `DALLAS` 被赋值给宏变量 `site`。然后宏变量 `site` 被用于控制程序的输出。

```
%let site=DALLAS;
title "REVENUES FOR &site TRAINING CENTER";
proc tabulate data=sasuser.all(keep=location
                         course_title fee);
   where upcase(location)="&site";
   class course_title;
   var fee;
   table course_title=' ' all='TOTALS',
         fee=' '*(n*f=3\. sum*f=dollar10.)
         / rts=30 box='COURSE';
run;
```

![达拉斯培训中心收入](img/14-g1)

# 处理宏变量

## SAS 处理

你已经了解了如何创建和引用宏变量。为了在你编写的程序中使用宏变量，你需要理解宏变量是如何被处理和存储的。首先，理解 SAS 处理是如何工作的至关重要。SAS 程序可以是以下内容的任何组合：

* `DATA` 步和 `PROC` 步
* 全局语句
* SAS 组件语言 (SCL) 代码
* 结构查询语言 (SQL) 代码
* SAS 宏语言代码

当你提交程序时，它会进入一个称为输入栈（input stack）的内存区域。适用于你提交的所有代码，例如 `DATA` 步、`SCL` 代码或 `SQL` 代码![输入栈](img/m50-9-g1) 一旦 SAS 代码进入输入栈，SAS 将：

* 读取输入栈中的文本（从左到右，从上到下）
* 根据需要将文本路由到适当的编译器
* 当遇到如 `RUN` 语句之类的步边界时，暂停此活动
* 如果没有编译错误，则执行编译后的代码
* 对任何后续步重复此过程。

![编译器](img/19-g2)

## 分词

在输入栈和编译器之间，SAS 程序会被分词为更小的部分。SAS 的一个称为单词扫描器会将程序分解为标记（tokens）。

* 标记根据需要传递给编译器。
* 编译器请求标记直到收到分号。
* 编译器对语句进行语法检查。

![编译器](img/20-g1) SAS 停止发送语句到编译器，直到到达步边界。步边界示例包括 `run;` 或新 `DATA` 或 `PROC` 步的开始。一旦整个步编译，就会执行。单词扫描器识别四种标记：

* 字面量标记是被视为整体的字符字符串。该字符串由单引号或双引号包围。例如：`"Any text" 'Any text'`
* 数字标记是包含数字的字符串，可以包含小数点或 E 表示法（实数）。日期常量、时间常量、日期时间常量十六进制常量也是数字标记。例如：`23 109 '01jan2002'd 5e8 42.7`
* 名称标记是以字母或下划线开头，后续下划线、字母或数字的字符串。小数点有时可以是名称的一部分。例如：`infile _n_ item3 univariate dollar10.2`
* 特殊标记是对编译器具有保留含义的任何字符或字符组。例如：`* / + - ** ; ( ) . & %`

当单词扫描器检测到以下内容时，标记结束：

* 另一个标记的开始
* 标记后的空格

任何标记的最大长度为 32,767 个字符。

## 示例

* ``````
    var x1-x10      z   ;
    ```

    此示例包含六个标记：`var x1 - x10 z ;`

* ``````
    title 'Report for May';
    ```

    此示例包含三个标记：`title 'Report for May' ;`

## 宏触发器




宏变量引用和 `%LET` 语句是宏语言的一部分。宏功能包含一个宏处理器，负责处理所有宏语言元素。某些标记符序列被称为宏触发器（macro triggers），它们会通知词法扫描器，随后的代码应被发送给宏处理器。词法扫描器将以下标记符序列识别为宏触发器：

*   `%` 后面紧跟一个名称标记符（例如 `%let`）
*   `&` 后面紧跟一个名称标记符（例如 `&amt`）

当检测到宏触发器时，词法扫描器将其传递给宏处理器进行求值。宏处理器：

*   检查这些标记符
*   根据需要请求额外的标记符
*   执行所指示的动作。

对于宏变量，处理器会执行以下操作中的其中一种：

*   在符号表中创建一个宏变量并为该变量赋值
*   更改符号表中已存在的宏变量的值
*   在符号表中查找已存在的宏变量，并将变量的值返回到输入栈，以替换原始引用。

随后，词法扫描器继续从输入栈处理标记符。注意：词法扫描器不识别包含在单引号中的宏触发器。记住，如果你需要在字面标记符内部引用宏变量（例如 `TITLE` 语句中的标题文本），你必须将文本字符串包含在双引号中，否则宏变量引用将不会被解析。

# 在 SAS 日志中显示宏变量值

## SYMBOLGEN 选项

当提交一个宏变量引用时，宏处理器会解析该引用并将值直接传回输入栈。因此，你无法看到编译器接收到的值。为了调试你的程序，查看替换你的宏变量引用的值可能对你很有帮助。你可以使用 `SYMBOLGEN` 系统选项来监控替换宏变量引用的值。

| 通用格式，带有 SYMBOLGEN 选项的 OPTIONS 语句：`OPTIONS NOSYMBOLGEN | SYMBOLGEN;` |
| :--- | :--- |
| `NOSYMBOLGEN` | 指定不显示关于宏变量引用的日志消息。这是默认设置。 |
| `SYMBOLGEN` | 指定显示关于宏变量引用的日志消息。 |

该系统选项在 SAS 日志中显示解析宏变量引用的结果。换句话之，当开启 `SYMBOLGEN` 选项时，SAS 会为程序中所引用的每个宏变量向日志写入一条消息。该消息说明宏变量名称和解析后的值。注意：记住，由于 `SYMBOLGEN` 是系统选项，它的设置将一直有效，直到你修改它或结束 SAS 会话。

## 示例

假设你之前为宏变量 `amount`、`city` 和 `company` 分配了值，并提交了以下代码：

```sas
data new;
   set sasuser.all;
   where fee>&amount;
   where also city_state contains "&city";
   where also student_company contains '&company';
run;
```

这是一个示例 SAS 日志，显示了该代码由 `SYMBOLGEN` 选项生成的消息。`WHERE ALSO` 条件使用 `AND` 运算符增强了初始的 `WHERE` 条件。在这个示例中，where 处理是针对以下条件进行的：`(fee>&amount) AND (city_state contains "&city") AND (student_company contains '&company')`。

表 9.2 SAS 日志

| |
| :--- |
| ```sas
110 where fee>&amount;
SYMBOLGEN: Macro variable AMOUNT resolves to 975
111 where city_state contains "&city";
SYMBOLGEN: Macro variable CITY resolves to Dallas
112 where student_company contains '&company';
``` |

注意，最后一个宏变量引用（`'&&company'`）没有显示任何消息。因为这个宏变量引用被包含在单引号而不是双引号中，词法扫描器没有调用宏功能来解析它。

## %PUT 语句

验证宏变量值的另一种方法是向 SAS 日志写入你自己的消息。`%PUT` 语句将文本写入 SAS 日志。

| 通用格式，基本 %PUT 语句：`%PUT text;` |
| :--- | :--- |
| `text` | 任意文本字符串。 |

`%PUT` 语句：

*   仅写入 SAS 日志
*   始终写入新的日志行，并从第一列开始
*   如果未指定文本，则写入一个空行
*   文本周围不需要引号
*   在文本写入之前解析文本中的宏触发器
*   除非使用了宏引用函数，否则会移除文本前导和结尾的空格
*   当文本长度大于当前行大小设置时进行换行
*   可以在宏定义内部或外部使用。

## 示例

假设你想验证宏变量 `city` 的值。由于 `%PUT` 语句在将文本写入 SAS 日志之前解析文本中的宏引用，你可以用它显示 `city` 的存储值。

```sas
%put The value of the macro variable CITY is: &city;
```

表 9.3 SAS 日志

| |
| :--- |
| ```sas
120 %put The value of the macro variable CITY is: &city;
The value of the macro variable CITY is: Dallas
``` |

你也可以简单地提交 `&put &city;` 语句而不带任何额外文本。该语句将宏变量 `city` 的解析值写入 SAS 日志。然而，它不会向日志中写入任何额外文本。你可能会发现，在 `%PUT` 语句中添加解释性文本以保持清晰度是一个好主意。`%PUT` 语句有几个可选参数。

| 参数 | 日志结果 |
| :--- | :--- |
| `_ALL_` | 显示所有宏变量的值 |
| `_AUTOMATIC_` | 显示自动宏变量的值 |
| `_LOCAL_` | 显示本地宏变量的值 |
| `_USER_` | 显示用户定义的宏变量的值 |

表 9.4 SAS 日志

| |
| :--- |
| ```sas
121 %let year=2002;
122 %let city=New York;
123 %let region=South;
124 %put _all_;
GLOBAL YEAR 2002
GLOBAL REGION South
GLOBAL CITY New York
AUTOMATIC AFDSID 0
AUTOMATIC AFDSNAME
AUTOMATIC AFLIB
AUTOMATIC AFSTR1
AUTOMATIC AFSTR2
AUTOMATIC FSPBDV
AUTOMATIC SYSBUFFR
AUTOMATIC SYSCC 0
AUTOMATIC SYSCHARWIDTH 1
AUTOMATIC SYSCMD
AUTOMATIC SYSDATE 29MAY02
``` |

注意，可选参数每个宏变量名称都会写入日志，并带有 AUTOMATIC 或 GLOBAL 标签。

# 使用宏函数屏蔽特殊字符

## 宏引用函数

SAS 编程语言使用成对的双引号或单引号来区分常量和名称。引号本身不作为它们定义的标记的一部分存储。例如，在下面的程序中，`var` 被存储为值为 `text` 的四字节变量。如果 `text` 没有包含在引号中，它将被视为一个变量名。`var2` 被存储为值为 `example` 的七字节变量。

```sas
data one;
   var='text';
   text='example';
   var2=text;
run;
```

同样，以下示例中的标题文本是 `Joan's Report`。虽然 `TITLE` 语句包含成对的双引号，但标题本身并不包含这些外部引号。然而，外部引号导致文本内部未匹配的单引号被解释为标题文本的一部分（撇号）。

```sas
proc print;
   title "Joan's Report";
run;
```

## 示例

之前你学习了宏变量值是字符字符串，并看到了包含特殊字符的宏变量示例。现在，假设要在宏变量中存储一个或多个 SAS 语句。例如，你想创建一个名为 `prog` 的宏变量，将其值存储为 `data new; x=1; run;`。




```
options symbolgen;
%let prog=data new; x=1; run;;
&prog
proc print;
run;
```

这里是由上述程序生成的 SAS 日志的一部分。

表 9.5 SAS Log

|  

```
25 options symbolgen;
26
27 %let prog=data new; x=1; run;
27 %let prog=data new; x=1; run;
                       -
                       180
ERROR 180-322: Statement is not valid or it is used out of proper order.
SYMBOLGEN: Macro variable PROG resolves to data new
28      &prog
29      proc print;
30      run;
NOTE: The data set WORK.NEW has 1 observations and 0 variables.
NOTE: The data set WORK.PROC has 1 observations and 0 variables.
NOTE: The data set WORK.PRINT has 1 observations and 0 variables.
NOTE: DATA statement used (Total process time):
      real time           0.25 seconds
      cpu time            0.07 seconds
```

 |

注意，根据日志中的 `SYMBOLGEN` 语句，宏变量 `prog` 已被赋值为 `data new`。SAS 将第一个分号解释为宏赋值语句的结束。在这种情况下，我们希望分号是宏变量值的一部分，但 SAS 无法得知这一点。在这种情况下，你需要掩码掉你想要赋值给宏变量的文本。也就是说，你需要让宏处理器忽略分号的普通含义。你可以使用宏引用函数来实现这一点。

## %STR 函数

`%STR` 函数用于在编译期间对标记（tokens）进行掩码（或在其周围加上引号），以确保宏处理器不会将其解释为宏层面的语法。也就是说，`%STR` 函数会隐藏分号和其他特殊标记，以及比较或逻辑运算符的记忆等效符的普通含义，使它们作为常量文本出现。特殊标记和记忆等效符包括

```
; + - * / , < > = blank ^ ~ # | 
LT EQ GT AND OR NOT LE GE NE IN
```

`%STR` 函数还可以

*   允许宏触发器正常工作
*   保留其参数开头和结尾的空格。

| 通用形式，`%STR` 函数：`%STR (argument)`这里是对该语法的解释：`argument` 是文本和宏触发器的任意组合。 |

将此应用于我们之前的示例，文本有多种被引的方式。请记住，我们想要创建一个名为 `prog` 的宏变量，其赋值值为 `data new; x=1; run;`。

方法一
你可以对所有文本进行引用。`%let prog=%str(data new; x=1; run;);`

方法二
你可以只对分号进行引用。`%let prog=data new%str(;) x=1%str(;)run%str(:);`

方法三
你可以创建一个额外的宏变量，给它分配一个引用值，并在 `prog` 宏变量的赋值语句中引用它。`%let s=%str(;); %let prog=data new&s x=1&s run&s;`

这些方法都实现了相同的功能：它们都将值 `data=new; x=1; run;` 赋值给宏变量 `prog`。`%STR` 函数还可以用于对通常成对出现的标记进行引用：

```
' " ) (
```

## 示例

假设你想给宏变量分配一个包含撇号（` '`）的文本。如果没有任何引用，这会导致错误。

```
options symbolgen;
%let text=Joan's Report;
proc print data=sasuser.courses;
   where days > 3;
title "&text";
run;
```

表 9.6 SAS Log

|  

```
75 %let text=Joan's Report;
                ---------
                32
WARNING 32-169: The quoted string currently being processed has
                become more than 262 characters long. You may
                have unbalanced quotation marks.
```

 |

单词扫描器将撇号解释为由一对单引号定义的字面量的开始。你可以使用 `%STR` 函数来避免此错误。在上一节中，你看到了几种使用 `%STR` 函数来掩码分号普通含义的方法。然而，显示的方法中没有一个能正确地掩码我们当前示例中的撇号。当你引用通常成对出现的标记（如引号或括号）时，你必须额外执行一步。为了执行这种引用，你需要在 `%STR` 函数参数中在你想要引用的标记前面加上一个百分号（`%`）。

```
%let text=%str(Joan%'s Report);
%let text=Joan%str('%')s Report;
```

在两种情况下，`text` 的值都是 `Joan's Report`。

## %NRSTR 函数

有时你想隐藏波浪（`&`）或百分号（`%`）的普通含义。`%NRSTR` 函数执行与 `%STR` 相同的引用功能，因为它还掩码了宏触发器（`&` 和 `%`）。`%NRSTR` 名称中的 NR 代表“不解析”（No Resolution）。`%NRSTR` 的语法与 `%STR` 相同。

## 示例

假设你想创建一个名为 `period` 的宏变量，并为其分配一个 `May&Jun` 的值。如果你尝试在赋值语句中使用 `%STR` 函数，SAS 将 `&` 解释为宏触发器并生成警告消息。你需要使用 `%NRSTR` 函数。

```
%let Period=%str(May&Jun);
%put Period:&period;
%let Period=%nrstr(May&Jun);
%put Period:&period;
```

SAS 日志的后续部分显示了此示例中 `%STR` 函数和 NRSTR 函数的结果。

表 9.7 SAS Log

|  

```
1    %let Period=%str(May&Jun);
WARNING: Apparent reference Jun not resolved.
2    %put Period:&period;
WARNING: Apparent reference Jun not resolved.
Period: May&Jun
3
4    %let Period=%nrstr(May&Jun);
5    %put Period:&period;
Period: May&Jun
```

## %BQUOTE 函数

与 `%STR` 函数一样，`%BQUOTE` 函数用于对特殊字符和记忆运算符进行掩码（或在其加上引号）。`%STR` 函数在编译期间执行，而 `%BQUOTE` 在执行期间执行。也就是说，`BQUOTE` 函数在执行期间掩码字符字符串或解析后的值，使得特殊字符和记忆运算符不会被解释为纯文本以外的任何内容。特殊标记和记忆等效符包括

```
' " ) ( + - * / , < > = blank ^ ~ # | 
LT EQ GT AND OR NOT GE NE IN
```

`%BQUOTE` 函数还可以

*   不需要标记引号
*   允许宏触发器正常工作
*   保留其参数开头和结尾的空格。

| 通用形式，`%BQUOTE` 函数：`%BQUOTE (argument)`这里是对该语法的解释：`argument` 是文本和宏触发器的任意组合。 |

## 示例

记得你想给宏变量分配包含撇号（`'`）文本的示例。你使用了 `%STR` 函数来掩码撇号。你可以使用 `%BQUOTE` 函数完成此任务。`BQUOTE` 函数不需要标记不匹配的引号，因此包含撇号的标题不需要特殊语法。

```
%let text=%bquote(Joan's Report);
```

# 使用宏函数处理字符串

## 宏字符函数

在处理宏变量时，经常需要处理字符串。你可以通过宏字符函数来实现这一点。通过宏字符函数，你可以：

*   将小写字母转换为大写字母
*   产生字符串的子字符串
*   从字符串中提取单词
*   确定字符串的长度等等。

宏字符函数的基本语法与对应的 DATA 步函数相同，并产生相似的结果。重要的是记住，尽管它们可能相似，但宏字符函数与 DATA 步函数是不同的。作为宏语言的一部分，宏函数允许你与宏处理器进行通信，以处理插入你的 SAS 程序中的文本字符串。接下来的几节将详细探讨几个宏字符函数。

## %UPCASE 函数




`%UPCASE` 函数允许您在 SAS 程序中替换该值之前，将宏变量的值从小写转换为大写。由于 SAS 语言中的大多数比较运算符都是区分大小大小的，因此通常需要将值转换为大写。

| `%UPCASE` 函数的通用形式： | `%UPCASE (argument)` | 以下是该语法的说明：`argument` 是一个字符字符串。 |

## 示例

`Sasuser.All` 数据集包含了学生信息和计算机培训课程的注册信息。假设您想创建一个未收缴学费的摘要：

```
%let paidval=n;
proc means data=sasuser.all sum maxdec=0;
   where paid="&paidval";
   var fee;
   class course_title;
title "Uncollected Fees for Each Course";
run;
```

表 9.8 SAS 日志

| |

```
163 %let paidval=n;
164  proc means data=sasuser.all sum maxdec=0;
165       where paid="&paidval";
166       var fee;
167       class course_title;
168  title "Uncollected Fees for Each Course";
169  run;

NOTE: No observations were selected from data set SASUSER.ALL.
```

| |

由于宏变量 `paidval` 的值是以小写指定的，因此 `WHERE` 表达式没有找到匹配的观测值。数据集变量 `Paid` 的所有值都以大写形式存储。现在，我们可以在 `WHERE` 语句中使用 `%UPCASE` 函数：

```
%let paidval=n;
proc means data=sasuser.all sum maxdec=0;
   where paid="%upcase(&paidval)";
   var fee;
   class course_title;
title "Uncollected Fees for Each Course";
run;
```

您看到，这次 `WHERE` 表达式确实找到了匹配的观测值![每门课程的未收缴费用](img/m50-39-g1.png)

## %QUPCASE 函数

如果参数包含特殊字符、助记操作符或宏触发器，您需要使用 `%QUPCASE` 函数。`%QUPCASE` 的语法与 `%UPCASE` 函数相同，其工作原理与 `%UPCASE` 相同，不同在于它还会掩盖函数结果中的助记操作符和特殊字符（包括宏触发器）。

## 示例

这些语句显示了 `%UPCASE` 和 `%QUPCASE` 生成的结果：

```
%let a=begin;
%let b=%nrstr(&a);

%put UPCASE produces: %upcase(&b);
%put QUPCASE produces: %qupcase(&b);
```

在第一个 `%PUT` 语句中，宏引用 `&b` 解析为 `&a`，由于 `%UPCASE` 函数的作用，它被转换为 `&A`。由于解析后的值包含宏触发器，它被视为宏变量引用，因此 `&A` 解析为值 `begin`。第二个 `%PUT` 语句使用了 `%QUPCASE` 函数，该函数掩盖了宏变量 `b` 解析值中的 ampersand 符号（&），使得该值不会被视为另一个宏变量引用。执行这些语句会在 SAS 日志中产生以下消息。

表 9.9 SAS 日志

| |

```
6    %let a=begin;
7    %let b=%nrstr(&a);
8
9    %put UPCASE produces: %upcase(&b);
UPCASE produces: begin
10   %put QUPCASE produces: %qupcase(&b);
QUPCASE produces: &A
```

| |

## %SUBSTR 函数

`%SUBSTR` 函数允许您从宏变量的值中提取字符字符串的一部分。

| `%SUBSTR` 函数的通用形式： | `%SUBSTR (argument, position<,n>)` | 以下是该语法的说明：`argument` 是一个字符字符串或文本表达式，从中返回子字符串。`position` 是一个整数或产生整数的表达式（文本、逻辑或数学表达式），用于指定子字符串中第一个字符的位置。`n` 是可选的整数或产生整数的表达式（文本、逻辑或数学表达式），用于指定子字符串中的字符数。 |

注意：如果 `n` 的长度大于 `argument` 中 `position` 之后的字符数，`%SUBSTR` 会发出警告消息并返回从 `position` 到字符串末尾的子字符串。如果未指定 `n`，`%SUBSTR` 也会返回从 `position` 到字符串末尾的子字符串。例如，假设宏变量 `date` 的值为 `05JAN2002`。

*   代码 `%substr(&date,3)` 返回值 `JAN2002`。
*   代码 `%substr(&date,3,3)` 返回值 `JAN`。
*   代码 `%substr(&date,3,9)` 返回值 `JAN2002` 并产生警告消息。

`position` 和 `n` 的值也可以产生整数的数学表达式的结果。例如，`%substr(&var,%length(&var)-1)` 返回宏变量 `var` 值的最后两个字符。注意：`%LENGTH` 函数接受字符字符串或文本表达式作为参数。如果参数是字符字符串，`%LENGTH` 返回字符串的长度。如果参数是文本表达式，`%LENGTH` 返回解析值的长度。如果参数为空值，`%LENGTH` 返回 0。

## 示例

假设您想打印一份自本月初以来所有课程的报告。您可以使用 `%SUBSTR` 函数来确定月份。（注：此处提供的原始文本存在大量重复和错乱，已根据逻辑进行了清理和翻译）。

[content]
`%UPCASE` 函数允许您在 SAS 程序中替换该值之前，将宏变量的值从小写转换为大写。由于 SAS 语言中的大多数比较运算符都是区分大小写的，因此通常需要将值转换为大写。

| `%UPCASE` 函数的通用形式： | `%UPCASE (argument)` | 以下是该语法的说明：`argument` 是一个字符字符串。 |

## 示例

`Sasuser.All` 数据集包含了学生信息和计算机培训课程的注册信息。假设您想创建一个未收缴学费的摘要：

```
%let paidval=n;
proc means data=sasuser.all sum maxdec=0;
   where paid="&paidval";
   var fee;
   class course_title;
title "Uncollected Fees for Each Course";
run;
```

表 9.8 SAS 日志

| |

```
163 %let paidval=n;
164  proc means data=sasuser.all sum maxdec=0;
165       where paid="&paidval";
166       var fee;
167       class course_title;
168  title "Uncollected Fees for Each Course";
169  run;

NOTE: No observations were selected from data set SASUSER.ALL.
```

| |

由于宏变量 `paidval` 的值是以小写指定的，因此 `WHERE` 表达式没有找到匹配的观测值。数据集变量 `Paid` 的所有值都以大写形式存储。现在，我们可以在 `WHERE` 语句中使用 `%UPCASE` 函数：

```
%let paidval=n;
proc means data=sasuser.all sum maxdec=0;
   where paid="%upcase(&paidval)";
   var fee;
   class course_title;
title "Uncollected Fees for Each Course";
run;
```

您看到，这次 `WHERE` 表达式确实找到了匹配的观测值![每门课程的未收缴费用](img/m50-39-g1.png)

## %QUPCASE 函数

如果参数包含特殊字符、助记操作符或宏触发器，您需要使用 `%QUPCASE` 函数。`%QUPCASE` 的语法与 `%UPCASE` 函数相同，其工作原理与 `%UPCASE` 相同，不同在于它还会掩盖函数结果中的助记操作符和特殊字符（包括宏触发器）。

## 示例

这些语句显示了 `%UPCASE` 和 `%QUPCASE` 生成的结果：

```
%let a=begin;
%let b=%nrstr(&a);

%put UPCASE produces: %upcase(&b);
%put QUPCASE produces: %qupcase(&b);
```

在第一个 `%PUT` 语句中，宏引用 `&b` 解析为 `&a`，由于 `%UPCASE` 函数的作用，它被转换为 `&A`。由于解析后的值包含宏触发器，它被视为宏变量引用，因此 `&A` 解析为值 `begin`。第二个 `%PUT` 语句使用了 `%QUPCASE` 函数，该函数掩盖了宏变量 `b` 解析值中的 ampersand 符号（&），使得该值不会被视为另一个宏变量引用。执行这些语句会在 SAS 日志中产生以下消息。

表 9.9 SAS 日志

| |

```
6    %let a=begin;
7    %let b=%nrstr(&a);
8
9    %put UPCASE produces: %upcase(&b);
UPCASE produces: begin
10   %put QUPCASE produces: %qupcase(&b);
QUPCASE produces: &A
```

| |

## %SUBSTR 函数

`%SUBSTR` 函数允许您从宏变量的值中提取字符字符串的一部分。

| `%SUBSTR` 函数的通用形式： | `%SUBSTR (argument, position<,n>)` | 以下是该语法的说明：`argument` 是一个字符字符串或文本表达式，从中返回子字符串。`position` 是一个整数或产生整数的表达式（文本、逻辑或数学表达式），用于指定子字符串中第一个字符的位置。`n` 是可选的整数或产生整数的表达式（文本、逻辑或数学表达式），用于指定子字符串中的字符数。 |

注意：如果 `n` 的长度大于 `argument` 中 `position` 之后的字符数，`%SUBSTR` 会发出警告消息并返回从 `position` 到字符串末尾的子字符串。如果未指定 `n`，`%SUBSTR` 也会返回从 `position` 到字符串末尾的子字符串。例如，假设宏变量 `date` 的值为 `05JAN2002`。

*   代码 `%substr(&date,3)` 返回值 `JAN2002`。
*   代码 `%substr(&date,3,3)` 返回值 `JAN`。
*   代码 `%substr(&date,3,9)` 返回值 `JAN2002` 并产生警告消息。

`position` 和 `n` 的值也可以产生整数的数学表达式的结果。例如，`%substr(&var,%length(&var)-1)` 返回宏变量 `var` 值的最后两个字符。注意：`%LENGTH` 函数接受字符字符串或文本表达式作为参数。如果参数是字符字符串，`%LENGTH` 返回字符串的长度。如果参数是文本表达式，`%LENGTH` 返回解析值的长度。如果参数为空值，`%LENGTH` 返回 0。

## 示例

假设您想打印一份自本月初以来所有课程的报告。您可以使用 `%SUBSTR` 函数来确定月份。




`%SCAN` 函数允许你从宏变量的值中提取单词。

| 通用格式，%SCAN` 函数：`%SCAN (argument, n<,delimiters>)` | 以下是该语法的解释： |
| :--- | :--- |
| `argument` 由常量文本、宏变量引用、宏函数或宏调用组成。 | `n` 是一个整数或产生整数的文本表达式，用于指定要返回单词的位置。如果 `n` 大于 `argument` 中的单词数，函数将返回空字符串。 |
| `delimiters` 指定一个可选的列表，该列表由一个或多个字符组成，用于分隔“单词”或产生一个或多个字符的文本表达式。 |

注意：如果 `argument` 包含逗号，你必须使用引号函数将 `argument` 括起来。同样地，为了将单个空格或单个逗号作为唯一分隔符，你必须将该字符封装在 `%STR` 函数中。`%SCAN` 识别的分隔符在 ASCII 和 EBCDIC 系统之间有所不同。如果你省略了 `delimiters`，SAS 将以下字符视为默认分隔符：

- ASCII 系统：`blank . < ( + & ! $ * ) ; ^ - / , % |`
- EBCDIC 系统：`blank . < ( + | & ! $ * ) ; ¬ - / , % ¦ ¢`

如果 `delimiters` 列表包含你系统的任何默认分隔符，则剩余的默认分隔符将被视为文本。

## 示例

你可以使用 `PROC DATASETS` 配合 `%SCAN` 函数和 `SYSLAST` 宏变量来调查最近创建的数据集的结构：

```
data work.thisyear;
   set sasuser.schedule;
    where year(begin_date) =
          year("&sysdate9"d);
run;

%let libref=%scan(&syslast,1,.);
%let dsname=%scan(&syslast,2,.);
proc datasets lib=&libref nolist;
title "Contents of the Data Set &syslast";
   contents data=&dsname;
run;
quit;
```

![contents of WORK.THISYEAR](img/m50-46-g1.png)

## %QSCAN 函数

如果 `argument` 包含特殊字符、助记符或宏触发器，你需要使用 `%QSCAN` 函数。`%QSCAN` 的语法与 `%SCAN` 函数相同，其工作方式与 `%SCAN` 相同，但它还会掩码函数结果中的助记符和特殊字符（包括宏触发器）。

## 示例

这些语句显示了 `%SCAN` 和 `%QSCAN` 产生的结果：

```
%let a=one;
%let b=two;
%let c=%nrstr(&a*&b);

%put C: &c;
%put With SCAN: %scan(&c,1,*);
%put With QSCAN: %qscan(&c,1,*);
```

执行这些语句会在 SAS 日志中产生以下消息。

表 9.12 SAS 日志

| |

```
47   %let a=one;
48   %let b=two;
49   %let c=%nrstr(&a*&b);
50
51   %put C: &c;
C: &a*&b
52   %put With SCAN: %scan(&c,1,*);
With SCAN: one
53   %put With QSCAN: %qscan(&c,1,*);
With QSCAN: &a
```

 | |

# 在宏变量中使用 SAS 函数

## %SYSFUNC 函数

你已经学习了通过使用自动宏变量 `SYSDATE9` 和 `SYSTIME` 可以在标题中包含日期和时间：

```
title1 "Report Produced on &sysdate9";
title2 "at &systime";
```

![Report Produced on &sysdate9](img/m50-50-g1.png) `SYSDATE9` 代表 SAS 会话启动时的日期，`SYSTIME` 代表 SAS 会话启动的时间。假设你希望以其他格式查看日期，或者想查看当前的日期或时间。你可以使用 `%SYSFUNC` 函数作为宏机制的一部分执行其他 SAS 函数。

| 通用格式，%SYSFUNC` 函数：`%SYSFUNC (function (argument(s)) <,format>)` | 以下是该语法的解释： |
| :--- | :--- |
| `function` 是要执行的 SAS 函数名称。 |
| `argument(s)` 是函数使用的一个或多个参数。使用逗号分隔所有参数。参数可以是宏变量引用，也可以是产生函数参数的文本表达式。 |
| `format` 是应用到函数结果的可选格式。默认情况下，数值结果将使用 `BEST12.` 格式转换为字符字符串，而字符结果将按原样使用，不进行格式化或翻译。 |

所有的 SAS 函数都可以配合 `%SYSFUNC` 使用，但例外：

| ALLCOMB | LEXCOMB |
| :--- | :--- |
| ALLPERM | LEXCOMBI |
| DIF | LEXPERK |
| DIM | LEXPERM |
| HBOUND | MISSING |
| INPUT | PUT |
| IORCMSG | RESOLVE |
| LAG | SYMGET |
| LBOUND | 变量信息函数 |

注意：变量信息函数包括如 `VNAME` 和 `VLABEL` 等函数。完整的函数列表请参阅“SAS 函数和例程”（Functions and Routines）。注意：可以使用 `INPUTC` 或 `INPUTN` 函数替换 `INPUT` 函数。同样，可以使用 `PUTC` 或 `PUTN` 函数替换配合 `%SYSFUNC` 的 `PUT` 函数。

## 示例

假设在 11 月 4 日（周五）提交了以下代码：

```
title "Report Produced on &sysdate9";
```

## 使用 QSCAN

如果参数包含特殊字符、助记符或宏触发器，你需要使用 `%QSCAN` 函数。`%QSCAN` 的语法与 `%SCAN` 函数相同，其工作方式与 `%SCAN` 相同，但它还会掩码函数结果中的助记符和特殊字符（包括宏触发器）。

## 示例

假设你想创建一个包含当前日期的报告。你可以使用语句：

```
title "Report Produced on %sysfunc(today(),date.)";
```

这将导致标题为：

```
Report Produced on November 4, 2011

```

# 文本引用

## 概述

你可以在程序的任何地方引用宏变量。某些应用程序可能需要将宏变量引用与前导文本（`text&variable`）、后缀文本（`&variabletext`）或相邻宏变量（`&variable&variable`）结合以构建新标记。在组合宏变量引用和文本时，记住 SAS 如何解释标记非常重要。当单词扫描器检测到新标记标记或标记后的空格时，标记结束。你可以将文本放在宏变量引用之前以构建新标记。例如，假设数据集存储在 SAS 库中，使用命名规范 `Yyymon`，其中 `yy` 是两位年份（如 02 或 01），`mon` 是三个字母月份（如 JUN 或 AUG）。你可以编写程序使用宏变量来构建数据集名称的月份部分。

```
%let month=jan;
proc chart data=sasuser.y02&month;
   hbar week / sumvar=sale;
run;
proc plot data=sasuser.y02&month;
   plot sale*day;
run;
```

表 9.14 替换后的代码

| |

```
proc chart data=sasuser.y02jan;
    hbar week / sumvar=sale;
run;
proc plot data=sasuser.y02jan;
    plot sale*day;
run;
```




你可以引用之间没有空格的宏变量来构建新的令牌（tokens）。例如，你可以修改之前的程序，以便允许月份和年份被替换：

```
%let year=02;
%let month=jan;
proc chart data=sasuser.y&year&month;
   hbar week / sumvar=sale;
run;
proc plot data=sasuser.y&year&month;
   plot sale*day;
run;
```

表 9.15 替换后的代码

```
proc chart data=sasuser.y02jan;
    hbar week / sumvar=sale;
run;
proc plot data=sasuser.y02jan;
    plot sale*day;
run;
```

生成的程序与上一个示例中的程序相同。也就是说，编译器在这这两个示例看到的是相同的代码。只要宏变量名称仍然能够被正确分词，你就可以在宏变量引用之后立即放置文本。例如，你可以修改之前的程序以替换分析变量的名称：

```
%let year=02;
%let month=jan;
%let var=sale;
proc chart data=sasuser.y&year&month;
   hbar week / sumvar=&var;
run;
proc plot data=sasuser.y&year&month;
   plot &var*day;
run;
```

表 9.16 替换后的代码

```
proc chart data=sasuser.y02jan;
    hbar week / sumvar=sale;
run;
proc plot data=sasuser.y02jan;
    plot sale*day
run;
```

生成的程序与前两个示例中的程序相同。也就是说，尽管你更改了所提交的代码，但你并没有更改编译器看到的代码。

## 宏变量名称中的分隔符

有时，你可能希望将宏变量名称置于特殊字符以外的文本之前。例如，你可能想修改之前的程序，以便于在 Base SAS 软件的 `CHART` 和 `PLOT` 过程与 SAS/GRAPH 软件的 `GCHART` 和 `GPLOT` 过程之间切换。

```
/* GRAPHICS 应该是 null 或 G */
%let graphics=g;
%let year=02;
%let month=jan;
%let var=sale;
proc &graphicschart data=sasuser.y&year&month;
   hbar week / sumvar=&var;
run;
proc &graphicsplot data=sasuser.y&year&month;
   plot &var*day;
run;
```

写入 SAS 日志的消息显示了该程序存在的问题。

表 9.17 SAS 日志

```
13     %let graphics=g;
14     %let year=02;
15     %let month=jan;
16     %let var=sale;
17     proc &graphicschart data=sasuser.y&year&month;
            -
            10

WARNING: Apparent symbolic reference GRAPHICSCHART not resolved.

ERROR 10-205: Expecting the name of the procedure to be executed.
```

SAS 将宏变量名解释为 `graphicschart` 而不是 `graphics`，因为宏变量引用和后续文本之间没有分隔符。扫描在遇到不能作为名称部分的特殊字符时，会识别宏变量名称的结束。换句话说，特殊字符充当了分隔符的作用。例如，点（`.`）是一个特殊字符，它被视为宏变量引用的一部分，并且在宏变量解析时不会出现。要修正上一个示例中的问题，你需要在宏变量 `graphics` 的引用之后添加点。

```
 %let graphics=g;
 %let year=02;
 %let month=jan;
 %let var=sale;
 proc &graphics.chart data=sasuser.y&year&month;
   hbar week / sumvar=&var;
run;
proc &graphics.plot data=sasuser.y&year&month;
   plot &var*day;
run;
```

当执行这些 SAS 语句时：
- 单词扫描器将 `&graphics.` 处理为引用
- 宏变量 `graphics` 的值返回到输入栈
- 单词扫描器将 `gchart` 处理为一个单一令牌。

表 9.18 替换后的代码

```
proc chart data=sasuser.y02jan;
   hbar week / sumvar=sale;
run;
proc plot data=sasuser.y02jan;
   plot sale*day;
run;
```

我们可以扩展这个示例，并进一步修改之前的程序，包含一个用于定义库引用（libref）的宏变量：

```
%let lib=sasuser;
%let graphics=g;
%let year=02;
%let month=jan;
%let var=sale;
libname &lib 'SAS-data-library';
proc &graphics.chart data=&lib.y&month;
   hbar week / sumvar=&var;
run;
proc &graphics.plot data=&lib.y&month;
   plot &var*day;
run;
```

然而注意，这段代码并没有执行预期的替换。

表 9.19 替换后的代码

```
libname sasuser 'SAS-data-library';
proc chart data=sasuserery2jan;
   hbar week / sumvar=sale;
run;
proc plot data=sasuserery2jan;
   plot sale*day;
run;
```

`&lib` 之后的点被解释为分隔符。你需要在分隔符之后使用第二个点来提供必要的令牌：

```
%let lib=sasuser;
...
libname &lib 'SAS-data-library';
proc &graphics.chart data=&lib..y&month;
...
proc &graphics.plot data=&lib..y&month;
```

第一个点被视为分隔符，而第二个点被视为文本。

表 9.20 替换后的代码

```
proc chart data=sasuser.y02jan;
...
proc plot data=sasuserery2jan;
```

## 总结

## 总结

### 基础概念
宏变量可以提供各种信息，从操作系统信息到 SAS 会话信息，甚至是任何文本字符串。如果你在程序中使用宏变量，更新对变量、数据集或文本字符串的多次引用是一个简单的过程。宏变量是 SAS 宏功能的一部分，该工具用于扩展和自定义 SAS，并减少你为了执行常用操作必须输入的文本量。宏变量存储在符号表中。存储在全局符号表中的值总是可用的。为了在程序中替换宏变量的值，你需要在宏变量名称前加上符号符号（`&`）。你可以在数据行之外任何地方引用宏变量。

### 使用自动宏变量
SAS 提供了包含计算环境信息的自动宏变量。自动宏变量在调用 SAS 时创建。许多此类变量具有固定值，在 SAS 会话期间保持不变。其他变量则根据提交的语句自动更新。

### 使用用户定义宏变量
你可以使用 `%LET` 语句创建并定义自己的宏变量。`%LET` 语句允许为你的新宏变量赋值并将其存储在全局符号表中。宏变量的值是字符字符串；对于前后空格，值按其出现的形式存储。

### 处理宏变量
提交时，SAS 程序进入称为输入栈的内存区域。从那里，单词扫描器将程序分成小的令牌，并将其传递给相应的编译器进行执行。某些令牌序列是宏触发器，会被发送到宏处理器进行解析。一旦宏变量被宏处理器解析，存储的值将回写到程序中，并继续单词扫描。

### 在 SAS 日志中显示宏变量值
你可以使用 `SYMBOLGEN` 选项来监控替换宏变量引用的值。你还可以使用 `%PUT` 语句将包含宏变量值的消息写入 SAS 日志。




可以使用宏字符函数对宏变量的值进行字符字符串操作。`%UPCASE` 函数允许你将值从小写更改为大写。`%QUPCASE` 函数的作用与 `%UPCASE` 相同，不同之处在于它还会掩码函数结果中的特殊字符和助记操作符。`%SUBSTR` 函数允许你从宏变量值中提取字符串的部。`%QSUBSTR` 函数的作用与 `%SUBSTR` 相同，不同之处在于它还会掩码结果中的特殊字符和助记操作符。`%INDEX` 函数允许你确定字符字符串在源数据中第一个字符出现的位置。使用 `%SCAN` 函数，你可以从宏变量的值中提取单词。`%QSCAN` 函数的作用与 `%SCAN` 相同，不同之处在于它还会掩码结果中的特殊字符和助记操作符。

## 在宏变量中使用 SAS 函数

你可以使用 `%SYSFUNC` 函数来执行其他 SAS 函数。`%QSYSFUNC` 函数的作用与 `%SYSFUNC` 函数相同，不同之处在于它还会掩码函数结果中的特殊字符和助记操作符。

## 将宏变量引用与文本结合

你可能需要将宏变量引用与其他文本结合。你可以将文本紧放在宏变量引用的之前或之后。你还可以结合两个宏变量引用以创建一个新的标记。在结合宏变量引用与文本时，你可能需要使用分隔符。

## 示例程序

### 使用 `%LET` 语句创建宏变量

```
options symbolgen; 
%let year=2002;
proc print data=sasuser.schedule;
   where year(begin_date)=&year;
   title "Scheduled Classes for &year";
run;
proc means data=sasuser.all sum;
   where year(begin_date)=&year;
   class location;
   var fee;
   title1 "Total Fees for &year Classes";
   title2 "by Training Center";
run;
```

### 使用自动宏变量

```
footnote1 "Created &systime &sysday, &sysdate9";    
footnote2 "on the &sysscp system using Release &sysver";      
title "REVENUES FOR DALLAS TRAINING CENTER";      
proc tabulate data=sasuser.all(keep=location course_title fee);         
   where upcase(location)="DALLAS";
        class course_title;
        var fee;
        table course_title=" " all="TOTALS",
              fee=" "*(n*f=3\. sum*f=dollar10.)
              / rts=30 box="COURSE";
run;
```

### 在文本之后立即插入宏变量

```
%let year=02;
%let month=jan;
proc chart data=sasuser.y&year&month;
   hbar week / sumvar=sale;
run;
proc plot data=sasuser.y&year&month;
  plot sale*day;
run;
```

### 在文本之前立即插入宏变量

```
%let graphics=g;
%let year=02;
%let month=jan;
%let var=sale;
proc &graphics.chart data=sasuser.y&year&month;
  hbar week / sumvar=&var;
run;
proc &graphics.plot data=sasuser.y&year&month;
  plot &var*day;
run;
```

## 需要事项的点

- 宏变量可以使你的程序更具重用性和动态性。
- 当你向 SAS 提交代码时，宏变量引用由宏处理器解析，其值将替换到你的程序中。
- 你可以使用 `%PUT` 语句将任何文本（包括解析后的宏变量）写入 SAS 日志中。
 如果 如果你在双引号内引用宏变量，则必须使用双引号。包含在单引号中的宏变量引用无法被解析。
- 大多数宏字符函数都有相应的函数（例如 `%QSUBSTR` 和 `%QSCAN`），这些函数也会掩码函数结果中的特殊字符和助记操作符。

# 测验

为每个问题选择最佳答案。完成测试后，使用附录中的答案检查你的答案。

1. 下列哪个陈述是错误的？

    1.  宏变量可以在 SAS 程序中除数据行以外的任何地方定义和引用。
    2.  宏变量始终由用户定义，其值在被用户更改之前保持保持不变。
    3.  宏变量是独立于 SAS 数据集的文本字符串。
    4.  宏变量的值长度可达 65,534 个字符。

2. 下列哪个 `TITLE` 语句正确引用了宏变量 `month`？

    1. ``` ```
       title "Total Sales for '&month' ";
       ```
    2. ``` ```
       title "Total Sales for 'month'";
       ```
    3. ``` ```
       title "Total Sales for &month";
       ```
    4. ``` ```
       title Total Sales for "&month";
       ```

3. 下列哪个陈述在尝试在 SAS 日志显示宏变量 `month` 的值时会生成错误消息？

    1. ``` ```
       options &month;
       ```
    2. ``` ```
       %PUT &month;
       ```
    3. ``` ```
       options symbolgen;
       ```
    4. ``` ```
       %PUT the macro variable MONTH has the value &month.;
       ```

4. 哪个语句创建名为 `location` 值为 `storage` 的宏变量？

    1. ``` ```
       &let location = storage;
       ```
    2. ``` ```
       let location = storage;
       ```
    3. ``` ```
       %let location = "storage";
       ```
    4. ``` ```
       %let location = storage;
       ```

5. 这些语句为宏变量 `reptitle` 赋值了什么值：

    ```
%let area = "Southeast";
%let reptitle = *&area*;
    ```

    1. `Sales Report for Southeast`
    2. `Sales Report for "Southeast"`
    3. `*Sales Report for Southeast*
    4. `* Southeast`

6. 假设你今天开始 SAS 会话，哪个语句正确将宏变量 `currdate` 设置为今天的日期：

    1. ``` ```
       %let currdate = %sysfunc(today(),worddate.);
       ```
    2. ``` ```
       %let currdate = &sysdate;
       ```
    3. ``` ```
       %let currdate = %sysfunc(date());
       ```
    4. 以上都是

7. 宏字符函数

    1. 可用于操作宏变量值的字符串。
    2. 与对应的函数语法相同并产生相似的结果。
    3. 以上都是
    4. 以上都不是

8. SAS 识别的四种标记类型为

    1. 表达式、字面量、名称和特殊字符。
    2. 字面量、名称、数字和特殊字符。
    3. 表达式、名称、数字和特殊字符。
    4. 表达式、字面量、数字和特殊字符。

9. 定义宏变量的结果是什么？

    ```
%let month1 = June;
%let month2 = July;
%let period1 = &month1&month2;
%let period2 = May&month1;
%let period3 = &month2.Aug;
    ```

    1. month1 Junemonth2 Julyperiod1 June Julyperiod2 May Juneperiod3 July Aug
    2. month1 Junemonth2 Julyperiod1 JuneJulyperiod2 MayJuneperiod3 July.Aug
    3. month1 Junemonth2 Julyperiod1 JuneJulyperiod2 MayJuneperiod3 JulyAug
    4. month1 Junemonth2 Julyperiod1 junejulyperiod2 Mayjuneperiod3 julyaug

10. 下列哪个语句正确产生一个标题，其中当前日期左对齐以删除多余的空格？

    1. ``` ```
       title "Report for %sysfunc(left(%sysfunc(today(),worddate.)))";
       ```
    2. ``` ```
       title "Report for %sysfunc(left(today(), worddate.))";
       ```
    3. ``` ```
       title "Report for %sysfunc(left(%qsysfunc(today(),worddate.)))";
       ```
    4. ``` ```
       title "Report for %left(today(), worddate.))";
       ```





## 概述

## 引言
由于宏功能在 SAS 程序执行之前就会完成其任务，因此宏功能提供的信息不依赖于 SAS 程序执行期间访问或计算出的值。然而，有时有必要在 SAS 程序的执行期间访问或创建宏变量。有几种方法可以使宏功能在执行时创建或访问宏变量。在本章中，你将学习在执行以下内容使用宏变量：
* 一个 `DATA` 步骤
* 一个 `PROC SQL` 步骤
* 一个 `SCL` 程序。

![macro variable](img/m51-1-g1.png)

# 在 DATA 步骤执行期间创建宏变量

## 概述
在许多应用程序中，你需要在 `DATA` 步骤执行期间创建宏变量。你可能需要根据以下内容创建宏变量并为其赋值：
* `SAS` 数据集或外部文件中的数据值
* 自身的*编程逻辑
* 计算出的值。

例如，假设你想根据 `Sasuser.All` 数据集中的数据创建一个报告，列出参加了特定课程的学生。假设你想在报告中包含一个脚注，以指示是否有学生未缴纳学费。以下程序使用 `SAS` 编程逻辑来确定给宏变量 `foot` 分赋值什么值。然后在程序稍后的 `FOOTNOTE` 语句中引用 `foot`。

```
options symbolgen pagesize=30;
%let crsnum=3;
data revenue;
   set sasuser.all end=final;
   where course_number=&crsnum;
   total+1;
   if paid='Y' then paidup+1;
   if final then do;
      put total= paidup=; /* Write information
                            to the log. */
      if paidup<total then do; 
         %let foot=Some Fees Are Unpaid;
      end; 
      else do; 
         %let foot=All Students Have Paid; 
      end; 
   end;
run;

proc print data=revenue;
   var student_name student_company paid;
   title "Payment Status for Course &crsnum";
   footnote "&foot";
run;
```

运行该程序产生如下报告：![Payment status for course 3](img/m51-2-g1.png)尽管你可以看到几个学生仍有未缴费用，但脚注显示所有学生都已缴。显然，这个脚注是错误的。也就是说，宏变量 `foot` 在不应该解析的时候解析为了值 `All Students Have Paid`（所有学生已缴）。查看下面的示例。

## 示例
为了理解此示例中的问题，你应该考虑宏变量处理是如何与 `SAS` 处理协同工作的。请记住，当宏语言语句和 SAS 语言语句出现在同一个步骤时，宏处理器会在执行任何 SAS 语言语句之前执行宏语言语句。请记住，你想根据 `Sasuser.All` 数据集中的数据创建一个报告，列出参加了特定课程的学生，并且你想在报告中包含一个脚注，以指示是否有学生未缴纳学费。以下程序使用 `SAS` 编程逻辑来确定给宏变量 `foot` 分赋值什么值。然后在程序稍后的 `FOOTNOTE` 语句中引用 `foot`。

```
options symbolgen pagesize=30;
%let crsnum=3;
data revenue;
   set sasuser.all end=final;
   where course_number=&crsnum;
   total+1;
   if paid='Y' then paidup+1;
   if final then do;
      put total= paidup=; /* Write information
                            to the log. */
      if paidup<total then do;
         %let foot=Some Fees Are Unpaid;
      end;
      else do;
         %let foot=All Students Have Paid;
      end;
   end;
run;

proc print data=revenue;
   var student_name student_company paid;
   title "Payment Status for Course &crsnum";
   footnote "&foot";
run;
```

在这个示例中，`DATA` 步骤内部第一个 `%LET` 语句一旦单词扫描器（word scanner）遇到它，就会传递给宏处理器。宏处理器在符号表中创建一个宏变量 `foot` 并分配值 `Some Fees Are Unpaid`。单词扫描器继续读取程序并将第二个 `%LET` 语句传递给宏处理器。这次，宏处理器在符号表中为 `foot` 重新分配值 `All Students Have Paid`。当遇到 `DATA` 步骤中的 `RUN` 语句时，`SAS` 识别到该步骤已完成。由于 `%LET` 语句始终由宏处理器处理，因此 `foot` 的值始终是最后一个 `%LET` 语句分配的值。以下是替换后的代码表示：

表 10.1

```
data
   set sasuser.all end=final;
   where course_number=3;
   total+1;
   if paid='Y' then paidup+1;
   if final then do;
      put total= paidup=;
      if paidup<total then do;
      end;
      else do;
      end;
   end;
run;
proc print data=revenue;
   var student_name student_company paid;
   title "Payment Status for Course 3";
   footnote "All Students Have Paid";
run;
```

 |我们可以通过以下信息解决这个问题。

## SYMPUT 程
`DATA` 步骤提供了函数和一种 `CALL` 程，允许你在正在执行的 `DATA` 步骤和宏处理器之间传输信息。你可以使用 `SYMPUT` 程创建宏变量，并为其分配 `DATA` 步骤中可用的任何值。

`SYMPUT` 程的一般形式：`CALL SYMPUT(macro-variable,text);`
此处语法解释如下：`macro-variable` 被分配 `text` 的字符值。`macro-variable` 和 `text` 都可以指定为
* 用引号括的字面量
* `DATA` 步骤变量
* `DATA` 步骤表达式。

注意：如果 `macro-variable` 已经存在，`text` 的值将替换旧值。当你在 `DATA` 步骤中使用 `SYMPUT` 程创建宏变量时，在 `DATA` 步骤执行之前，宏变量实际上并没有创建并分配值。因此，在导致 `DATA` 步骤执行的步骤边界之前，你无法通过在前加 & 符号成功引用用 `SYMPUT` 程创建的宏变量。在接下来的章节中，你将看到 `SYMPUT` 程在不同情况下的用法示例。

### 使用字面量 SYMPUT
在 `SYMPUT` 程中，你对以下内容使用字面字符串：
* 第一个参数指定宏变量名称的精确名称
* 第二个参数指定要分配给宏变量的精确字符值。

要在 `SYMPUT` 程中使用字面量，请将字面字符串括在引号中。`CALL SYMPUT('macro-variable', 'text')`





回想之前的示例，其中你想要根据 DATA 步执行期间生成的值，为宏变量 `foot` 条件地赋值一个值。你可以使用 `SYMPUT` 程，并将字面字符串作为两个参数来实现这一目标。

```
options symbolgen pagesize=30;
%let crsnum=3;
data revenue;
   set sasuser.all end=final;
   where course_number=&crsnum;
   total+1;
   if paid='Y' then paidup+1;
   if final then do;
   if paidup<total then do;
      call symput('foot','Some Fees Are Unpaid');
   end;
   else do;
      call symput('foot','All Students Have Paid');
   end;
end;
run;

proc print data=revenue;
   var student_name student_company paid;
   title "Payment Status for Course &crsnum";
   footnote "&foot";
run;
```

这一次，赋值给 `foot` 的值是 `Some Fees Are Unpaid` 或 `All Students Have Paid`，取决于 DATA 步变量 `Paidup` 的值，因为赋值是在 DATA 步执行期间完成的。当你提交这段代码时，将得到如下输出。![Payment status for course 3](img/m51-6-g1.png)

## 在 DATA 步变量中使用 SYMPUT

你可以通过将 DATA 步变量名作为 `SYMPUT` 程的第二个参数，将 DATA 步变量的值赋值给宏变量。要在 `SYMPUT` 程中将 DATA 步变量作为宏变量的值，你需要将 DATA 步变量的名称放在宏变量名称之后，并用逗号分隔。不要给 DATA 步变量名加上引号。

`CALL SYMPUT('macro-variable',DATA-step-variable);` 这种形式的 `SYMPUT` 程创建一个名为 `macro-variable` 的宏变量，并将 `DATA-step-variable` 的当前值赋值给它。当你将 DATA 步变量作为第二个参数时：

*   接收的宏变量最多可以分配 32,767 个字符。
*   DATA 步变量值包含的任何前导或尾尾空格都会存储在宏变量中。
*   数值型变量的值会自动转换为字符型值，并使用 `BEST12.` 格式。

**注意**：如果你给 DATA 步变量名加上引号，SAS 会将该名称解释为字面值而非变量名，导致 DATA 步变量的值无法被解析。

## 示例

再次假设你想要创建一个关于注册了某特定课程的学生的报告。这次，假设你想添加一个包含课程标题和课程编号的标题，并想包含一个总结多少学生已交费情况的脚注。在这个示例中，名为 `paidup` 的 DATA 步变量记录了已缴费的人数，名为 `total` 的 DATA 步变量记录了注册该课程的总人数。创建宏变量来记录 `paidup` 的值、`total` 的值以及 `Course_title` 的值。这些宏变量在程序的后续被引用。

```
%let crsnum=3;
data revenue;
   set sasuser.all end=final;
   where course_number=&crsnum;
   total+1;
   if paid='Y' then paidup+1;
   if final then do;
      call symput('numpaid',paidup);
      call symput('numstu',total);
      call symput('crsname',course_title);
   end;
run;
proc print data=revenue noobs;
   var student_name student_company paid;
   title "Fee Status for &crsname (#&crsnum)";
   footnote "Note: &numpaid Paid out of &numstu Students";
run;
```

这一次，脚注显示了学生缴费人数的正确信息。![Fee status for local area networks (#3)](img/m51-8-g1.png)

## 在 DATA 步表达式中使用 CALL SYMPUT

如果你使用列表输出（listing output）而不是 HTML 输出运行上一个示例，你将在标题的课程标题和课程编号之间以及脚注中看到额外的空格。

表 10.2 SAS 列表输出

```
 Fee Status for Local Area Networks       (#3)                  

 Student_Name                Student_Company                  Paid

 Bills, Ms. Paulette         Reston Railway                    Y
 Chevarley, Ms. Arlene       Motor Communications              N
 Clough, Ms. Patti           Reston Railway                    N
 Crace, Mr. Ron              Von Crump Seafood                 Y
 Davis, Mr. Bruce            Semi;Conductor                    Y
 Elsins, Ms. Marisa F.       SSS Inc.                          N
 Gandy, Dr. David            Paralegal Assoc.                  Y
 Gash, Ms. Hedy              QA Information Systems Center     Y
 Haubold, Ms. Ann            Reston Railway                    Y
 Hudock, Ms. Cathy           So. Cal. Medical Center           Y
 Kimble, Mr. John            Alforone Chemical                 N
 Kochen, Mr. Dennis          Reston Railway                    Y
 Larocque, Mr. Bret          Physicians IPA                    Y
 Licht, Mr. Bryan            SII                               Y
 McKnight, Ms. Maureen E.    Federated Bank                    Y
 Scannell, Ms. Robin         Amberly Corp.                     N
 Seitz, Mr. Jan             Lomax                    Y
 Smith, Mr. Adam             Sailbest                    Y
 Sulbach, Mr. Gene          Snowing Petroleum                 Y
      Note: 14 Paid out of           20 Students
```





```
 局域网费用状态 (#3)

 姓名                        公司                          已支付

Bills, Ms. Paulette         Reston Railway                    Y
Chevarley, Ms. Arlene       Motor Communications              N
Clough, Ms. Patti           Reston Railway                    N
Crace, Mr. Ron              Von Crump Seafood                 Y
Davis, Mr. Bruce            Semi;Conductor                    Y
Elsins, Ms. Marisa F.       SSS Inc.                          N
Gandy, Dr. David            Paralegal Assoc.                  Y
Gash, Ms. Hedy              QA Information Systems  Center    Y
Haubold, Ms. Ann            Reston Railway                    Y
Hudock, Ms. Cathy           So. Cal. Medical Center           Y
Kimble, Mr. John            Alforone Chemical                 N
Kochen, Mr. Dennis          Reston Railway                    Y
Larocque, Mr. Bret          Physicians IPA                    Y
Licht, Mr. Bryan            SII                               Y
McKnight, Ms. Maureen E.    Federated Bank                    Y
Scannell, Ms. Robin         Amberly Corp.                     N
Seitz, Mr. Adam             Lomax Services                    Y
Smith, Ms. Jan              Reston Railway                    N
Sulzbach, Mr. Bill          Sailbest Ships                    Y
Williams, Mr. Gene          Snowing Petroleum                 Y

                  备注：20 名学生中有 14 人已支付
```

## PUT 函数

请记住宏变量的值始终是字符串。你已经看到，在 `DATA` 步中，`SYMPUT` 例程会对你尝试分配给宏变量的任何数值执行自动的从数值到字符的转换。消息会写入 SAS 日志，以提醒你发生了自动转换。请记住，`SYMPUT` 例程在转换时会自动使用 `BEST12\.` 格式。

有时，你可能希望对数值到字符的转换进行显式控制。`PUT` 函数返回一个通过指定格式写入值而形成的字符字符串。你可以使用 `PUT` 函数执行以下操作：

*   执行显式的数值到字符的转换
*   格式化数值表达式的结果。

`PUT` 函数的一般形式：`PUT(source,format.)`
以下是对该语法的解释：
`source` 是常量、变量或表达式（数值型或字符型）。
`format.` 是任何 SAS 格式或用户定义的格式，它决定了：
*   结果字符串的长度
*   字符串是右对齐还是左对齐。

`source` 和 `format.` 必须是相同类型（数值型或字符）。

## 示例

假设你想创建一个报告，显示特定课程未支付的费用金额。在以下示例中，你使用 `SYMPUT` 例程用 `MMDDYY10\.` 格式化数值变量 `Begin_date` 的值，并将该值分配给宏变量 `date`。然后，你再次调用 `SYMPUT` 例程，将涉及 `Fee`、`total` 和 `paidup` 的表达式结果格式化为金额，并将该值分配给宏变量 `due`。

```
%let crsnum=3;
data revenue;
   set sasuser.all end=final;
   where course_number=&crsnum;
   total+1;
   if paid='Y' then paidup+1;
   if final then do;
     call symput('crsname',trim(course_title));
     call symput('date',put(begin_date,mmddyy10.));
     call symput('due',strip(put(fee*(total-paidup),dollar8.)));
   end;
run;
```

你可以在 `PROC PRINT` 步中使用宏变量 `date` 和 `due` 来创建报告。这些宏变量的值在报告中显示为你在创建它们时分配给它们的格式。

```
proc print data=revenue;
   var student_name student_company paid;
   title "Fee Status for &crsname (#&crsnum) Held &date";
   footnote "Note: &due in Unpaid Fees";
run;
```

![2001 年 01 月 08 日举行的局域网费用状态 (#3) 所示](img/m51-13-g1.png)

## SYMPUTX 例程

`SYMPUTX` 例程与 `SYMPUT` 例程非常相似。除了创建宏变量并为其赋值值外，`SYMPUTX` 例程还会自动移除两个参数前导和尾的空格。

`SYMPUTX` 例程的一般形式：`CALL SYMPUTX(macro-variable,expression);`
以下是对该语法的解释：
`macro-variable` 被赋予 `expression` 的字符值，并且会移除 `macro-variable` 和 `expression` 前导或尾的空格。
`macro-variable` 和 `expression` 都可以指定为：
*   用引号括的字面量
*   `DATA` 步变量
*   `DATA` 步表达式

备注：如果 `macro-variable` 已经存在，`expression` 的值将替换旧值。

## 示例

记得之前创建一个关于选修特定课程学生的报告示例。这次，假设你希望标题包含课程名称、课程编号以及课程举办日期。此外，你还希望脚注列出该课程当前的未支付费用金额。

在此示例中，创建了三个宏变量。宏变量 `csrname` 记录 `DATA` 步变量 `Course_title` 的值。宏变量 `date` 记录 `DATA` 步变量 `Begin_date` 以 `MMDDYY10\.` 格式的值。最后，宏变量 `due` 使用 `DATA` 步变量 `paidup`、`total` 和 `fee` 的值，以 `DOLLAR8.` 格式记录当前的未支付费用金额。这些宏变量在程序后的标题和脚注语句中被引用。

```
%let crsnum=3;
data revenue;
   set sasuser.all end=final;
   where course_number=&crsnum;
   total+1;
   if paid='Y' then paidup+1;
   if final then do;
      call symputx('crsname',course_title);
      call symputx('date',put(begin_date,mmddyy10.));
      call symputx('due',put(fee*(total-paidup),dollar8.));
   end;
run;
proc print data=revenue;
   var student_name student_company paid;
   title "Fee Status for &crsname (#&crsnum) Held &date";
   footnote "Note: &due in Unpaid Fees";
run;
```

![2001 年 01 月 08 日举行的局域网费用状态 (#3) 所示](img/m51-9-g1.png)

# 在 DATA 步执行期间创建宏变量

## 使用 CALL SYPUT 创建宏变量

有时你可能希望在一个 `DATA` 步中创建多个宏变量。例如，假设你想编写一个列出特定课程所有安排日期的程序，并使用宏变量记录课程标题。

```
%let crsid=C005;
data _null_;
   set sasuser.courses;
   where course_code="&crsid";
   call symput('title',trim(course_title));
run;

proc print data=sasuser.schedule noobs label;
   where course_code="&crsid";
   var location begin_date teacher;
   title1 "Schedule for &title";
   options nodate nonumber;
run;
```

在此示例中，`Course_code` 为 `C005` 的课程数据集变量 `Course_title` 的值被赋值为宏变量 `title` 的值。`data` 语句中的 `_null_`是因为我们在示例中不需要创建数据集。为了创建另一个课程的列表，你需要更改 `%LET` 语句并重新提交 `DATA` 步以为 `title` 分配新值。然后，你需要重新提交 `PROC PRINT` 步。虽然你需要重新提交 `DATA` 步和 `PROC PRINT` 步，但这两个步骤与你为第一个报告提交的步骤完全相同。这是一个极其低效的程序。

```
%let crsid=C004;
data _null_;
   set sasuser.courses;
   where course_code="&crsid";
   call symput('title',trim(course_title));
run;

proc print data=sasuser.schedule noobs label;
   where course_code="&crsid";
   var location begin_date teacher;
   title1 "Schedule for &title";
   options nodate nonumber;
run;
```




与其通过执行多个 `DATA` 步来更新同一个宏变量，你可以在一个 `DATA` 步中创建相关的宏变量。要创建多个宏变量，你可以使用 `SYMPUT` 程，并对两个参数都使用 `DATA` 步表达式。

| 通用形式，使用 `DATA` 步表达式的 `SYMPUT` 句程：`CALL SYMPUT(expression1,expression2);` | 以下是对该语法的解释：`expression1` 评估为有效宏变量名称的字符值。每当你想要创建另一个宏变量时，该值都应该发生变化。`expression2` 是你想要赋值给特定宏变量的值。 |

## 示例

在本示例中，你通过调用一次 `SYMPUT` 句程，为 `DATA` 步变量 `Course_code` 的每个值创建一个宏变量，并将 `Course_title` 的相应值赋值给每个宏变量。也就是说，对于 `Sasuser.Courses` 中的每个观测值，宏处理器都会创建一个新的宏变量。新宏变量的名称与该观测值的数据集变量 `Course_code` 的值相同。新宏变量的值则是该观测值的数据集变量 `Course_title` 的值。

```
data _null_;
   set sasuser.courses;
   call symput(course_code, trim(course_title));
run;
%put _user_;
```

SAS 日志显示从数据集 `Sasuser.Courses` 中读取了 6 个观测值，并创建并赋值了 6 个全局宏变量。

表 10.4 SAS 日志

| |

```
2   data _null_;
3      set sasuser.courses;
4      call symput(course_code, trim(course_title));
5   run;

NOTE: There were 6 observations read from the dataset 
      SASUSER.COURSES.
NOTE: DATA statement used:
      real time           0.52 seconds
      cpu time            0.13 seconds

7   %put _user_;
GLOBAL C006 Computer Aided Design
GLOBAL C001 Basic Telecommunications
GLOBAL C002 Structured Query Language
GLOBAL C003 Local Area Networks
GLOBAL C004 Database Design
GLOBAL C005 Artificial Intelligence
```

| |

然后你可以使用这些新的宏变量仅通过一个 `DATA` 步来打印各种课程的信息列表，如下：

```
data _null_;
   set sasuser.courses;
   call symput(course_code,trim(course_title));
run; 

%let crsid=C005;
proc print data=sasuser.schedule noobs label;
   where course_code="&crsid";
   var location begin_date teacher;
   title1 "Schedule for &c005";
run;

%let crsid=C002;
proc print data=sasuser.schedule noobs label;
   where course_code="&crsid";
   var location begin_date teacher;
   title1 "Schedule for &c002";
run;
```

这是第一个 `PROC PRINT` 步的输出。![人工智能课程表](img/m51-17-g1.png)这是第二个个 `PROC PRINT` 步的输出。![结构化查询语言课程表](img/m51-17-g2.png)本节中的程序比上一节所示的程序更高效，因为在最新的示例中 `Sasuser.Courses` 数据集仅读取了一次。然而，仍然有改进空间。

# 间接引用宏变量

## 引言

在上一个示例中，你了解了如何使用 `SYMPUT` 句程创建一系列基于 `Course_code` 值的宏变量。然而，你仍然需要修改每个 `PROC PRINT` 步中的 `TITLE` 语句来打印每个课程的输出。假设你想写一个无需任何修改即可重用的 `PROC PRINT` 步，以打印每个课程的信息。你可以通过在 `TITLE` 语句中使用间接引用来实现这一点。

```
data _null_;
   set sasuser.courses;
   call symput(course_code,trim(course_title));
run;

%let crsid=C002;
proc print data=sasuser.schedule noobs label;
   where course_code="&crsid";
   var location begin_date teacher;
   title1 "Schedule for ???";
run;
```

在上面的示例中，宏变量 `C002`（由 `SYMPUT` 句程创建）的值为 `Structured Query Language`。因此，`TITLE` 语句应该引用解析为 `Structured Query Language` 的宏变量。记住，你希望此引用足够灵活，只需更改 `%LET` 语句即可适用于 `SYMPUT` 句程创建的任何宏变量（例如 `C003` 或 `C004`）。为了获取值 `Structured Query Language`，你需要通过宏变量 `crsid` 的引用间接引用宏变量 `C002`。如果宏变量 `crsid` 的值为 `C002`，则你需要执行以下步骤：

1. 将宏变量 `crsid` 解析为值 `C002`。
2. 在解析后的值前面加上一个连接符 (`&`) 以创建一个新的引用（`&C002`）。
3. 将生成的宏变量引用解析为值 `Structured Query Language`。

这一序列意味着你应该使用对宏变量 `crsid` 的引用，将其值转换为 `Structured Query Language`。

## 向前扫描规则 (Forward-Scan Rule)

向前扫描规则可以总结如下：

- 当多个 `&` 或 `%` 位于名称之前，宏处理器会将两个 `&` (`&&`) 解析为一个 `&` (`&`) 并重新扫描该引用。
- 为了重新扫描引用，宏处理器从左到右扫描并解析标记，直到没有更多触发器。

根据向前扫描规则，当宏变量的值是一个名称时，需要在前面使用三个 `&`。

## 示例

假设你想使用宏变量 `crsid` 间接引用宏变量 `C002`![全局符号表](img/m51-20-g1.png)下表显示了几个引用及其解析值![带有解析值的引用](img/m51-20-g2.png)在宏变量引用前面加上两个 `&` 可以延迟引用的解析。当引用第一次被扫描时，只会解析双 `&`（变为单 `&`）。为了创建一个间接引用（其值为另一个宏变量的引用），你必须使用三个 `&`。因此，为了使用解析为 `Structured Query Language` 的间接引用，原始引用必须是 `&&&crsid`。

```
options symbolgen;
data _null_;
   set sasuser.courses;
   call symput(course_code, trim(course_title));
run;

%let crsid=C005;
proc print data=sasuser.schedule noobs label;
   where course_code="&crsid";
   var location begin_date teacher;
   title1 "Schedule for &&&crsid";
run;

%let crsid=C002;
proc print data=sasuser.schedule noobs label;
   where course_code="&crsid";
   var location begin_date teacher;
   title1 "Schedule for &&&crsid";
run;
```




```sas
43   options symbolgen;
44   data _null_;
45      set sasuser.courses;
46      call symput(course_code, trim(course_title));
47   run;
NOTE: There were 6 observations read from the dataset
      SASUSER.COURSES.
NOTE: DATA statement used:
      real time           0.07 seconds
      cpu time            0.05 seconds

48
49   %let crsid=C005;
50   proc print data=sasuser.schedule noobs label;
51      where course_code="&crsid";
SYMBOLGEN: Macro variable CRSID resolves to C005
52      var location begin_date teacher;
SYMBOLGEN:  && resolves to &.
SYMBOLGEN:  Macro variable CRSID resolves to C005
SYMBOLGEN:  Macro variable C005 resolves to Artificial
            Intelligence
53      title1 "Schedule for &&&crsid";
54   run;

NOTE: There were 3 observations read from the dataset
      SASUSER.SCHEDULE.
      WHERE course_code='C005';
NOTE: PROCEDURE PRINT used:
      real time           0.09 seconds
      cpu time            0.04 seconds

55
56   %let crsid=C002;
57   proc print data=sasuser.schedule noobs label;
58      where course_code="&crsid";

SYMBOLGEN:  Macro variable CRSID resolves to C002
59      var location begin_date teacher;
SYMBOLGEN:  && resolves to &.
SYMBOLGEN:  Macro variable CRSID resolves to C002
SYMBOLGEN:  Macro variable C002 resolves to Structured
            Query Language
60      title1 "Schedule for &&&crsid";
61   run;

NOTE: There were 3 observations read from the dataset
      SASUSER.SCHEDULE.
      WHERE course_code='C002';
NOTE: PROCEDURE PRINT used:
      real time           0.06 seconds
      cpu time            0.04 seconds
```

这是第一个 `PROC PRINT` 步骤的输出。![人工智能课程表](img/m51-21-g1.png)这是第二个 `PROC PRINT` 步骤的输出。![结构化查询语言课程表](img/m51-21-g2.png)注意，生成这些报告的 `PROC PRINT` 步骤是相同的。只有每个 `PROC PRINT` 步骤之前的 `%LET` 语句以及宏变量的解析值发生了变化。当你在处理一系列相关的宏变量时，间接引用特别别有用。在介绍宏变量中，你学习了如何通过组合多个宏变量引用来构建新的标记。你也可以将间接宏变量引用与其他宏变量引用结合使用。也就是说，当一个宏变量的值与第二个宏变量名称的部分匹配时，你可以在引用中使用两个 `&` 符号。

## 示例

你可以创建一个系列宏变量 `teach1` 到 `teachn`，每个变量都包含分配给特定课程的导师名称。

```sas
options symbolgen;
data _null_;
   set sasuser.schedule;
   call symput('teach'||left(course_number),
               trim(teacher));
run;
```

注意：连接运算符 `||` 用于合并文本。在上面的示例中，字面字符串 `teach` 被连接到对变量 `Course_number` 的解析值进行左对齐后生成的文本。![全局符号表](img/m51-22-g1.png)然后，当指定课程号时，你可以引用这些变量之一。如果你在 `%LET` 语句中指定了课程号，你可以使用多个 `&` 符号来创建对应当前课程号的 `teachn` 宏变量引用。

```sas
%let crs=3;
proc print data=sasuser.register noobs;
   where course_number=&crs;
   var student_name paid;
   title1 "Roster for Course &crs";
   title2 "Taught by &&teach&crs";
run;
```

SAS 日志显示了导致引用 `&&teach&crs` 解析的步骤。

表 10.6 SAS 日志

|  

```sas
65   %let crs=3;
66   proc print data=sasuser.register noobs;
67      where course_number=&crs;
SYMBOLGEN:   Macro variable CRS resolves to 3
68      var student_name paid;
SYMBOLGEN:   Macro variable CRS resolves to 3
69     title1 "Roster for Course &crs";
SYMBOLGEN:  && resolves to &.
SYMBOLGEN:  Macro variable CRS resolves to 3
SYMBOLGEN:  Macro variable TEACH3 resolves to
            Forest, Mr. Peter
70     title2 "Taught by &&teach&crs";
71   run;
```

 |

这是示例的输出。![Forest 先生执教的第 3 号课程名单](img/m51-22-g2.png)

# 在 DATA 步执行期间获取宏变量值

## SYMGET 函数

之前你已经学习了如何使用 `SYMPUT` 过程在 DATA 步中创建宏变量。你还熟悉使用宏变量引用如 `&var` 来获取值。现在，假设你想在 DATA 步执行期间获取宏变量的值。你可以通过 `SYMGET` 函数在 DATA 步执行期间获取宏变量。`SYMGET` 函数返回数据变量的值。

| SYMGET 的通用形式：`SYMGET(macro-variable)` 以下是语法的解释：`macro-variable` 可以是：

* 带引号的宏变量名

* 数据变量名

* 宏变量表达式 |

## 示例

你可以使用 `SYMGET` 函数在每次 DATA 步迭代时获取宏变量的值。在此示例中，数据集变量 `Teacher` 被赋值为 `Sasuser.Register` 中的值，其中假设宏变量 `teachn` 已经创建。

```sas
data teachers;
   set sasuser.register;
   length Teacher $20;
   teacher=symget('teach'||left(course_number));
run;

proc print data=teachers;
   var student_name course_number teacher;
   title1 "Teacher for Each Student";
```

![使用 SYMGET 函数的输出](img/m51-25-g2.png) | 程序创建的 SAS 输出所示。注意数据集 `Teachers` 包含一个名为 `Teacher` 的变量，其值与全局符号表中的宏变量 `teach1-teach3` 相同。![每个学生的课程表](img/m51-25-g1.png)

# 在 PROC SQL 步骤期间创建宏变量

## INTO 子句和 NOPPRINT 选项

你已经看到过如何在 DATA 步中创建宏变量。你也可以在 `PROC SQL` 步骤期间创建或更新宏变量。记住 `PROC SQL` 步骤中的 `SELECT` 语句检索并显示数据。`INTO` 子句在 `SELECT` 语句中允许你创建或更新宏变量。当你在 `PROC SQL` 执行期间创建或更新宏变量时，你可能不希望有输出。`PRINT | NOPPRINT` 选项指定是否在输出中显示 `SELECT` 语句的结果。`PRINT` 是默认设置。

| NOPPRINT 选项和 INTO 子句的 PROC SQL 通用形式：`PROC SQL NOPPRINT;SELECT column1<,column2,...>INTO :macro-variable-1,:macro-variable-2,...>FROM table-1 || view-1<WHERE expression>;QUIT;` 以下是语法的解释：`column1, column2,...` 指定了 SQL 表 `table-1 || view-1` 的一个或多个列。`:macro-variable-1, :macro-variable-2,...` 指定了要创建的宏变量。`expression` 产生用于子集的值。`other clauses` 是其他用于分组、子集或排序数据的有效子句。注意：宏变量名前带有冒号。注意：有关 `PROC SQL` 的更多信息，请参阅 SAS 文档。这种形式的 `INTO` 子句不能在创建表或视图时使用。





你可以创建一个名为 `totalfee` 的宏变量，其中包含所有课程费的总和，并在后续步骤中使用该宏变量。你使用 `NOPRINT` 选项来抑制 `PROC SQL` 步骤的输出。

```
proc sql noprint;
   select sum(fee) format=dollar10\. into :totalfee
      from sasuser.all;
quit;
%let totalfee=&totalfee;

proc means data=sasuser.all sum maxdec=0;
   class course_title;
   var fee;
   title "Grand Total for All Courses Is &totalfee";
run;
```

注意：这种形式的 `INTO` 子句不会修剪前后的空格，但 `%LET` 语句会移除存储在 `totalfee` 值中的任何前或后空格。`PROC MEANS` 步骤的输出显示了 `DOLLAR10.` 格式的所有课程费总和。![所有课程的总额](img/m51-28-g1.png)

## 使用 INTO 子句创建变量

在此之前你已经学习了如何在 `DATA` 步骤执行期间使用 `SYMPUT` 过程创建一系列相关的宏变量。有时，你可能想在 `PROC SQL` 步骤执行期间创建一系列相关的宏变量。你可以使用 `INTO` 子句为 `SELECT` 语句结果中的每一行创建一个新的宏变量。

| 通用形式，带有 `INTO` 子句且用于宏变量范围的 `SELECT` 语句：`PROC SQL NOPRINT;SELECT column1INTO :macro-variable-1 - :macro-variable-n FROM table-1 | view-1<WHERE expression><other clauses>;QUIT;` 以下是该语法的解释：`column1` 指定由 `table-1 | view-1` 指定的 SQL 表的列。`:macro-variable-1 - :macro-variable-n,...` 指定要创建的宏变量名称。`expression` 生成一个用于数据子集的值。`other clauses` 是其他用于分组、子集化或排序数据的有效子句。 |

在将值存储到宏变量范围中，或使用 `SEPARATED BY` 选项将多个值存储在一个宏变量中时，`PROC SQL` 的 `INTO` 子句会修剪任何前导或尾部空格。如果你希望保留空格，请使用 `NOTRIM` 选项。这种对前导和尾部空格的处理与将 `DATA` 步骤变量的值赋值给宏变量 (SYMPUT 过程的情况不同。 |

## 示例

你可以创建一个系列宏变量，包含 2002 年安排的前三门课程的课程代码、地点和开始日期。在这个示例中，宏变量 `crsid1`-`crsid3` 被赋予 `PROC SQL` 结果前三行中数据集变量 `Course_code` 的值：

```
proc sql;
   select course_code, location, begin_date format=mmddyy10.
   into :crsid1-:crsid3,
        :place1-:place3,
        :date1-:date3
      from sasuser.schedule
      where year(begin_date)=2002
      order by begin_date;
quit;
```

这是 `PROC SQL` 步骤的结果。![课程代码，地点](img/m51-29-g1.png) 这是此 `PROC SQL` 步骤运行后符号表的表示。![全局符号表](img/m51-29-g2.png) 如果不知道创建了多少个宏变量，可以发布查询来确定需要多少宏变量，并创建一个宏变量来存储该数字。然后你可以运行查询，使用该宏变量作为每组宏变量中最后一个宏变量的后缀。

## 示例

假设你想创建一个系列宏变量范围，包含 2002 年安排的所有课程的课程代码、地点和开始日期。你不知道课程的数量。如果你将一个任意大的数字作为最后一个宏变量范围的后缀，则只会创建与查询结果集对应的宏变量。宏变量 `SQLOBS` 被赋予一个反映结果集行数的值，该值与每个范围中创建的宏变量数量相。

```
proc sql noprint;
   select course_code, location,
          begin_date format=mmddyy10.
      into :crsid1-:crsid999,
           :place1-:place999,
           :date1-:date999
      from sasuser.schedule
      where year(begin_date)=2002
      order by begin_date;
   %let numrows=&sqlobs;
   %put There are &numrows courses in 2002;
   %put _user_;
quit;
```

SAS 日志显示 `numrows` 被赋值为 `4`。程序末尾的 `%PUT` 语句显示了 `SELECT` 语句中创建的所有宏变量的名称和值。表 10.7 SAS 日志

```
 114  proc sql noprint;
115    select course_code, location,
116        begin_date format=mmddyy10.
117      into :crsid1-:crsid999,
118           :place1-:place999,
119           :date1-:date999
120      from sasuser.schedule
121      where year(begin_date)=2002
122      order by begin_date;
123   %let numrows=&sqlobs;
124   %put There are &numrows courses in 2002;
125   %put _user_;
126 quit;
```

## 创建分隔值列表

有时，在 `PROC SQL` 步骤执行期间，你可能想创建一个宏变量，包含某个数据集变量的所有值。你可以使用 `INTO` 子句的另一种形式将一列的值合并到一个宏变量中。

| 通用形式，带有 `INTO` 子句且用于将值合并到一个宏变量的 `SELECT` 语句：`PROC SQL NOPRINT;SELECT column1INTO :macro-variable-1SEPARATED BY 'delimiter1'FROM table-1 | view-1<WHERE expression><other clauses>;QUIT;` 以下是该语法的解释：`column1` 指定由 `table-1 | view-1` 指定的 SQL 表的列。`:macro-variable-1` 指定要创建的宏变量名称。`'delimiter1'` 在引号内，指定作为宏变量值中分隔符的字符。`expression` 生成一个用于数据子集的值。`other clauses` 是其他用于分组、子集化或排序数据的有效子句。 |

## 示例

你可以使用 SQL 过程创建一个名为 `sites` 的宏变量，包含 `Sasuser.Schedule` 中出现的所有培训地的名称。这些名称用空格分隔。

```
proc sql noprint;
   select distinct location into :sites separated by ' '
      from sasuser.schedule;
quit;
```

现在你可以在标题中使用新的宏变量。

```
proc means data=sasuser.all sum maxdec=0;
   var fee;
   title1 'Total Revenue';
   title2 "from Course Sites: &sites";
run;
```

# 使用 PROC SQL 视图

当你提交 `PROC SQL` 步骤时，PROC SQL 程序代码被放入输入栈，并对宏触发器进行单词扫描，这与其他 SAS 程序中的过程相同。在以下代码中，宏变量引用 `&crsid` 在创建 `PROC SQL` 视图期间被解析，导致每次使用该视图时都得到一个常数值。例如，如果在提交此代码代码时 `crsid` 的值为 `C003`，则视图 `Subcrsid` 是基于课程代码 C003 的。





```
proc sql;
   create view subcrsid as
      select student_name, student_company,paid
         from sasuser.all
         where course_code="&crsid";
quit;
```

更好的方法是使用 `SYMGET` 函数，使视图能够查找宏变量的值。在接下来的示例中，当使用视图 `Subcrsid` 时，它是基于 `crsid` 的当前值生成的：

```
 proc sql;
   create view subcrsid as
      select student_name,student_company,paid
         from sasuser.all
         where course_code=symget('crsid');
quit;

%let crsid=C003;
proc print data=subcrsid noobs;
   title "Status of Students in Course Code &crsid";
run;

%let crsid=C004;
proc print data=subcrsid noobs;
   title "Status of Students in Course Code &crsid";
run;
```

`PROC SQL` 不执行自动数据转换。如果将宏变量与数值变量进行比较，则必须使用 `INPUT` 函数将宏变量的值转换为数值。以下代码执行了一个基于宏变量 `crsnum` 当前值的数值等价值的查询。在该 `WHERE` 语句中，`INPUT` 函数是必要的，因为数据集变量 `Course_number` 的值是数值，而 `crsnum` 是字符值，因为它是一个宏变量。

```
proc sql;
    create view subcnum as
       select student_name, student_company, paid
          from sasuser.all
          where course_number=input(symget('crsnum'),2.);
quit;

%let crsnum=4;
proc print data=subcnum noobs;
   title "Status of Students in Course Number &crsnum";
run;
```

# 在 SCL 程序中使用宏变量

## 概述

SAS 组件语言 (SCL) 程序被放置在输入栈中，并且在与其他 SAS 相同的相同的过程中，对宏触发器进行单词扫描。在 `SUBMIT` 块之外的宏变量引用在执行执行前会被解析。因此，在接下来的示例中，在 SCL 执行期间，会将常量值与 SCL 变量 `Wage` 进行比较：

```
MAIN:
   erroroff wage;
   if wage gt &max then erroron wage;
return;
```

`SUBMIT` 块内的任何文本都被假认为 SAS 代码，因此在编译 SCL 程序时，SCL 编译器会忽略它们。`SUBMIT` 块内的宏变量引用在 `SUBMIT` 块执行且 `SUBMIT` 块内的 SAS 代码被分词化之前，不会被解析。当 `SUBMIT` 块执行时，SAS 尝试将宏变量引用（`&name`）解析为对应的 SCL 变量。如果没有对应的 SCL 变量，则该引用将传递给宏处理器以在全局符号表中进行查找。你可以通过在名称前加上两个 符号（`&&name`），强制将 `SUBMIT` 块内的引用（`&name`）作为宏变量引用传递。此外，还有几个函数和例程可以使 SCL 程序和宏设施在执行时交换信息。我们将检查这些函数和例程。你已经学习了如何在 `DATA` 步执行如何使用 `SYMPUT` 例程和 `SYMGET` 函数。`SYMPUT` 例程和 `SYMGET` 函数都可以在 SCL 程序中使用。每个者的语法与在 `DATA` 步中完全相同。此外，`SYMPUT` 例程和 `SYMGET` 函数都有用于 SCL 程序的数值等价物。

## SYMPUTN 例程

`SYMPUTN` 例程允许你在 SCL 程序执行期间创建一个宏变量并为其分配一个数值值。

| 通用形式，`SYMPUTN` 例程：`CALL SYMPUTN('macro-variable', value);` |
| :--- |
| 以下是对语法的解释：`macro-variable` 是用单引号括起来的全局宏变量名称，且不带 & 符号。或者，它是一个 SCL 变量的名称（不带引号），其值是全局宏变量的名称。`value` 是分配给 `macro-variable` 的数值值，它可以是一个数字或数值型 SCL 变量的名称。 |

## 示例

假设 SCL 变量 `unitvar` 的值为 `unit`，SCL 变量 `unitnum` 的数值为 200。为了创建一个名称为 `unitvar` 值（在此例中为 `unit`）的宏变量，并分配一个等于 SCL 变量 `unitnum` 值（在此例中为 200）的值，你在 `SUBMIT` 块中提交以下语句：

```
call symputn(unitvar, unitnum);
```

同样，为了创建一个名为 `unitvar` 的宏变量并为其分配数值 500，你在 `SUBMIT` 块中提交以下语句。

```
call symputn('unitvar', 500);
```

## SYMGETN 函数

`SYMGETN` 函数允许你在 SCL 程序执行期间获取宏变量的数值值。

| 通用形式，`SYMGETN` 函数：`SCL-variable = SYMGETN('macro-variable');` |
| :--- |
| 以下是对语法的解释：`SCL-variable` 是一个数值变量的名称，用于接收 `macro-variable` 的值。`macro-variable` 是用单引号括起来的全局宏变量名称，且不带 & 符号。或者，它是一个 SCL 变量的名称（不带引号），其值是全局宏变量的名称。 |

## 示例

假设 SCL 变量 `unitvar` 的值为 `unit`，宏变量 `unit` 的值为 200，而宏变量 `unitvar` 的值为 500。第一个语句创建一个名为 `unitnum` 的 SCL 变量并为其赋值 200。第二个语句创建一个名为 `unit` 的 SCL 变量并为其赋值 500。

```
unitnum=symgetn(unitvar);
unit=symgetn('unitvar');
```

关于使用宏变量的更多信息，请参考宏语言。

## 总结

## 文字总结

### 在 DATA 步中创建宏变量

当你使用 `%LET` 语句创建宏变量时，所有的宏处理都在 `DATA` 步执行之前完成。`SYMPUT` 例程允许在 `DATA` 步期间创建或更新宏变量。根据编码方式的不同，你可以创建一个或多个宏变量。你可以使用字面量通过 `SYMPUT` 例程创建宏变量，并为其分配精确的名称或文本值。你可以使用 `DATA` 变量通过 `SYMPUT` 例程将该 `DATA` 变量的值分配给宏变量。你可以使用 `SYMPUTX` 例程在 `DATA` 步期间创建或更新宏变量，并自动去除宏变量名称和值的两端空格。你还可以将 `DATA` 表达式作为 `SYMPUT` 例程的参数，以便在赋值分配给宏变量之前应用 `DATA` 函数。

### 在 DATA 步中创建多个宏变量

你可以在一个 `DATA` 步中使用两个 `DATA` 表达式通过 `SYMPUT` 或 `SYMPUTX` 例程创建一系列相关的宏变量。

### 间接引用宏变量

有时，间接引用宏变量是有用的。例如，你可能想用一个宏变量来构造另一个宏变量的名称。通过在宏变量名前加上两个或多个 & 符号，你可以间接引用宏变量。





你可以在 `PROC SQL` 步骤中使用 `SELECT` 语句中的 `INTO` 子句来访问宏功能。`INTO` 子句的各种形式允许你创建一系列宏变量、数量变化的宏变量，或者一个通过连接 SQL 变量的唯一值创建的单个宏变量。你可以使用 `NOPRINT` 选项防止 `PROC SQL` 步骤创建输出。

### 使用 PROC SQL 视图

当你提交一个 `PROC SQL` 步骤时，`PROC SQL` 程序代码被放入输入栈中，并与其他 SAS 程序相同的过程中，在同一进程中对宏触发器进行单词扫描。

### 在 SCL 程序中使用宏变量

SAS 组件语言 (SCL) 也有为宏变量赋值以及从宏符号表中获取取值的例程和函数。`SYMPUT` 例程和 `SYMGET` 函数在 `SCL` 程序中的用法与它们在 `DATA` 步骤程序中的用法相同。此外，`SYMPUTN` 例程可以用于在 `SCL` 程序执行期间创建宏变量并为这些变量分配数值。`SYMGETN` 函数可以用于在 `SCL` 程序执行期间获取宏变量的数值。

## 示例程序

### 使用 CALL SYMPUT 创建宏变量

```
 options symbolgen pagesize=30;
 %let crsnum=3;
 data revenue;
    set sasuser.all end=final;
    where course_number=&crsnum;
    total+1;
    if paid='Y' then paidup+1;
    if final then do;
       if paidup<total then do;
          call symput('foot','Some Fees Are Unpaid');
       end;
       else do;
          call symput('foot','All Students Have Paid');
       end;
    end;
run;
proc print data=revenue;
   var student_name student_company paid;
   title "Payment Status for Course &crsnum";
   footnote "&foot";
run;
```

### 间引用宏变量

```
options symbolgen;
data _null_;
    set sasuser.courses;
    call symput(course_code, trim(course_title));
run;

%let crsid=C005;
proc print data=sasuser.schedule noobs label;
    where course_code="&crsid";
    var location begin_date teacher;
    title1 "Schedule for &&&crsid";
run;

%let crsid=C002;
proc print data=sasuser.schedule noobs label;
    where course_code="&crsid";
    var location begin_date teacher;
    title1 "Schedule for &&&crsid";
run;
```

### 使用 SYMGET 获取宏变量值

```
data teachers;
   set sasuser.register;
   length Teacher $ 20;
   teacher=symget('teach'||left(course_number));
run;

proc print data=teachers;
   var student_name course_number teacher;
title1 "Teacher for Each Registered Student";
run;
```

### 使用 INTO 子句创建宏变量

```
proc sql noprint;
   select course_code, location, begin_date format=mmddyy10.
      into :crsid1-:crsid3,
           :place1-:place3,
           :date1-:date3
      from sasuser.schedule
      where year(begin_date)=2002
      order by begin_date;
quit;
```

## 注意事项

- `SYMPUT` 例程可用于在 `DATA` 步骤执行期间创建或更新宏变量。
- 宏变量的值始终字符值。在 `DATA` 步骤中，`SYMPUT`会对你尝试分配给宏变量的任何数值执行自动的从数值到字符的转换。
- `SYMGET` 函数可用于在 `DATA` 步骤、`PROC SQL` 步骤或 `SCL` 程序执行期间获取宏变量的值。
- `INTO` 子句可用于 `SELECT` 语句中，在 `PROC SQL` 步骤执行期间创建或更新宏变量。
- `SYMPUT` 和 `SYMPUTN` 例程可用于在 `SCL` 程序执行期间创建或更新宏变量。

# 测验

为每个问题选择最佳答案。完成测验后，使用附录中的答案键检查你的答案。

1. 下列哪项是错误的？
    1. `%LET` 语句会导致宏处理器在程序编译之前创建宏变量。
    2. 要创建一个基于 `DATA` 步骤计算的数据的宏变量，你使用 `SYMPUT` 函数。
    3. 宏函数始终在 `DATA` 步骤执行期间进行处理。
    4. `DATA` 步骤中的宏变量引用始终在 `DATA` 步骤执行之前被解析。

2. 下列哪项正确创建了一个名为 `region` 的宏变量，并根据数据集变量 `Location` 的值为其分配了一个值？

    1.
        ```
        data new;
           set sasuser.all;
           if location='Boston' then do;
              call symput('region', 'East');
           end;
           else do;
              call symput('region', 'West');
           end;
        run;
        ```
    2.
        ```
        data new;
           set sasuser.all;
           if location='Boston' then do;
              %let region=East;
           end;
           else
              %let region=West;
           end;
        run;
        ```
    3.
        ```
        data new;
           set sasuser.all;
           if location='Boston' then do;
              call symput('region', 'East');
           end;
           else do
              call symput('region', 'West');
           end;
        run;
        ```
    4.
        ```
        data new;
           set sasuser.all;
           if location='Boston' then do;
              %let region=East;
           end;
           else
              %let region=West;
           end;
        run;
        ```

3. `SYMPUT` 例程不能
    1. 将数据集变量赋值给宏变量。
    2. 在 `DATA` 步骤中用于更新宏变量。
    3. 在 `DATA` 步骤执行期间将数值值转换为字符值进行赋值。
    4. 在 `SCL` 程序中用于创建宏变量。

4. 下列哪个程序正确创建了一系列以数据集变量 `Course_code` 为值的宏变量，然后在后续步骤中间接引用这些宏变量？

    1.
        ```
        data _null_;
           set sasuser.courses;
           call symput(course_code, trim(course_title));
        run;

        %let crsid=C005;
        proc print data=sasuser.schedule noobs label;
           where course_code="&crsid";
           var location begin_date teacher;
           title1 "Schedule for &crsid";
        run;
        ```
    2.
        ```
        data _null_;
           set sasuser.courses;
           call symput(course_code, trim(course_title));
        run;

        %let crsid=C005;
        proc print data=sasuser.schedule noobs label;
           where course_code="&crsid";
           var location begin_date teacher;
           title1 "Schedule for &&&crsid";
        run;
        ```
    3.
        ```
        data _null_;
           set sasuser.courses;
           call symput(course_code, trim(course_title));
        run;

        %let crsid=C005;
        proc print data=sasuser.schedule noobs label;
           where course_code="&crsid";
           var location begin_date teacher;
           title1 "Schedule for &&&crsid";
        run;
        ```
    4.
        ```
        data _null_;
           set sasuser.courses;
           call symput(course_code, trim(course_title));
        run;

        %let crsid=C005;
        proc print data=sasuser.schedule noobs label;
           where course_code="&crsid";
           var location begin_date teacher;
           title1 "Schedule for &&&crsid";
        run;
        ```

5. 关于宏变量引用的解析，下列哪个说法是错误的？
    1. 两个 `&` 解析为一个 `&`。
    2. 如果名称标记前连续超过四个 `&`，宏处理器将生成错误消息。
    3. 继续扫描，直到没有剩余的宏处理器可以解析的宏触发器。





4. 宏处理器总是重新扫描前面有多个 `&` 符号或多个 `%` 符号的名称标记（name token）。

6. 在以下哪种情况下，你会使用 `SYMGET` 而不是宏变量引用（`&macvar`）？

    1.  在执行 `DATA` 步期间，从宏变量的值创建一个 `DATA` 步变量
    2.  在 `PROC SQL` 视图中包含宏变量引用
    3.  在执行 `SCL` 程序期间访问宏变量的值
    4.  以上所有情况

7. 下列哪项正确地在 `PROC SQL` 步中创建了宏变量？

    1.  ```sas
       call symput(daily_fee, put(fee/days, dollar8.));
       ```
    2.  ```sas
       %let daily_fee=put(fee/days, dollar8.)
       ```
    3.  ```sas
       select fee/days format=dollar8\. 
       into :daily_fee from sasuser.all;
       ```
    4.  ```sas
       select fee/days format=dollar8\. 
       into daily_fee from sasuser.all;
       ```

8. 根据此处显示的全局符号表，对 `&&teach&crs` 引引用解析值是什么？![Global Symbol Table](img/m51-41-g1.png)

    1.  `&TEACH3`
    2.  TEACH3
    3.  Forest, Mr. Peter
    4.  以上都不是

9. 下列哪条语句正确地在 `DATA` 步执行期间创建一个名为 `Price` 的 `DATA` 步变量，并为其赋值宏变量 `daily_fee` 的值？

    1.  ```sas
       price=&daily_fee;
       ```
    2.  ```sas
       price=symget(daily_fee);
       ```
    3.  ```sas
       price=symget(&daily_fee);
       ```
    4.  ```sas
       price=symget("daily_fee");
       ```

10. 下列哪项是错误的？

    1.  `SYMPUT` 程序可以在执行 `DATA` 步期间或执行 `SCL` 程序期间创建宏变量。
    2.  在 `DATA` 步中，`SYMPUT` 程序会自动将你尝试赋值给宏变量的任何数值值转换为字符值。
    3.  `PROC SQL` 会自动将你尝试与数值进行比较的任何宏变量值转换为数值。
    4.  在 `SCL` 程序中，可以使用 `SYMPUTN` 程序将数值值赋值给宏变量。

# 第 11 章：创建和使用宏程序

概述基础概念开发和调试宏使用宏参数理解符号表条件处理语句迭代处理语句使用算术和逻辑表达式总结测试

## 概述

## 引言

和宏变量一样，宏程序（也称为宏）允许你将文本替换到 SAS 程序中。宏与宏变量不同，因为它们可以使用条件逻辑对你替换到程序中的文本做出决策。使用宏可以帮助你的 SAS 程序更具动态性和可重用性。例如，假设你每天都会提交一个 SAS 程序，为本月晚些时候将举办的课程创建注册列表。然后，假设你每个周五还会提交一个 SAS 程序，以创建本月目前为止产生的收入摘要。通过使用宏，你可以自动化此过程，因此只需要一个 SAS 程序。该程序提交每日报告，并在如果是周五时条件性地提交周报。此外，你可以创建并存储一个宏来自动化此过程，你每天只需要提交这段代码即可：

```sas
%reports
```

# 基础概念

## 定义宏

为了创建一个宏程序，你必须首先定义它。你从 `%MACRO` 语句开始宏定义，用 `%MEND` 语句结束定义。

| 通用格式、`%MACRO`语句和`%MEND`语句： |
| `%MACRO macro-name;text%MEND <macro-name>;` |

以下是对该语法的解释：`macro-name` 为宏命名。`macro-name` 的值可以是任何有效的 SAS 名称，只要它不是 SAS 宏设施中的保留字即可。`text` 可以是：

*   常量文本，可能包括 SAS 数据集名称
*   宏变量，可能包括 SAS 数据集名称
* 宏函数
* 宏语句

提示：`macro-name` 为宏命名。`macro-name` 的值可以是任何有效的 SAS 名称，只要它不是 SAS 宏设施中的保留字即可。`text` 可以是：

*常量文本，可能包括 SAS 数据集名称
* 宏变量，可能包括 SAS 数据集名称
* 宏函数
* 宏语句

提示：`macro-name` 为宏命名。`macro-name` 的值可以是任何有效的 SAS 名称，只要它不是 SAS 宏设施中的保留字即可。`text` 可以是：

*常量文本，可能包括 SAS 数据集名称
* 宏变量，可能包括 SAS 数据集名称
* 宏函数
* 宏语句

提示：`macro-name` 为宏命名。`macro-name` 的值可以是任何有效的 SAS 名称，只要它不是 SAS 宏设施中的保留字即可。`text` 可以是：

*常量文本，可能包括 SAS 数据集名称
* 宏变量，可能包括 SAS 数据集名称
* 宏函数
* 宏语句

提示：`macro-name` 为宏命名。`macro-name` 的值可以是任何有效的 SAS 名称，只要它不是 SAS 宏设施中的保留字即可。`text` 可以是：

*常量文本，可能包括 SAS 数据集名称
* 宏变量，可能包括 SAS 数据集名称
* 宏函数
* 宏语句

提示：`macro-name` 为宏命名。`macro-name` 的值可以是任何有效的 SAS 名称，只要它不是 SAS 宏设施中的保留字即可。`text` 可以是：

*常量文本，可能包括 SAS 数据集名称
* 宏变量，可能包括 SAS 数据集名称
* 宏函数
* 宏语句

提示：`macro-name` 为宏命名。`macro-name` 的值可以是任何有效的 SAS 名称，只要它不是 SAS 宏设施中的保留字即可。`text` 可以是：

*常量文本，可能包括 SAS 数据集名称
* 宏变量，可能包括 SAS 数据集名称
* 宏函数
* 宏语句

提示：`macro-name` 为宏命名。`macro-name` 的值可以是任何有效的 SAS 名称，只要它不是 SAS 宏设施中的保留字即可。`text` 可以是：

*常量文本，可能包括 SAS 数据集名称
* 宏变量，可能包括 SAS 数据集名称
* 宏函数
* 宏语句

提示：`macro-name` 为宏命名。`macro-name` 的值可以是任何有效的 SAS 名称，只要它不是 SAS 宏设施中的保留字即可。`text` 可以是：

*常量文本，可能包括 SAS 数据集名称
* 宏变量，可能包括 SAS 数据集名称
* 宏函数
* 宏语句

|通用格式、`%MACRO`语句和`%MEND`语句： |
| `%MACRO macro-name;text%MEND <macro-name>;` |

*常量文本，可能包括 SAS 数据集名称
* 宏变量，可能包括 SAS 数据集名称
* 宏函数
* 宏语句

| 提示：`macro-name` 为宏命名。`macro-name` 的值可以是任何有效的 SAS 名称，只要它不是 SAS 宏设施中的保留字即可。`text` 可以是：

*常量文本，可能包括 SAS 数据集名称
* 宏变量，可能包括 SAS 数据集名称
* 宏函数
* 宏语句

提示：`macro-name` 为宏命名。`macro-name` 的值可以是任何有效的 SAS 名称，只要它不是 SAS 宏设施中的保留字即可。`text` 可以是：

*常量文本，可能包括 SAS 数据集名称
* 宏变量，可能包括 SAS 数据集名称
* 宏函数
* 宏语句

提示：`macro-name` 为宏命名。`macro-name` 的值可以是任何有效的 SAS 名称，只要它不是 SAS 宏设施中的保留字即可。`text` 可以是：

*常量文本，可能包括 SAS 数据集名称
* 宏变量，可能包括 SAS 数据集名称
* 宏函数
* 宏语句

（此处由于示例内容重复，已按常规逻辑处理翻译）

## 引言

和宏变量一样，宏程序（也称为宏）允许你将文本替换到你的 SAS 程序中。宏与宏变量不同，因为它们可以使用条件逻辑对你替换到程序中的文本做出决策。使用宏可以帮助你的 SAS 程序更具动态性和可重用性。例如，假设你每天都会提交一个 SAS 程序，为本月晚些时候将举办的课程创建注册列表。然后，假设你每个周五还会提交一个 SAS 程序，以创建本月目前为止产生的收入摘要。通过使用宏，你可以自动化此过程，因此只需要一个 SAS 程序。该程序提交每日报告，并在如果是周五时条件性地提交周报。此外，你可以创建并存储一个宏来自动化此过程，你每天只需要提交这段代码即可：

```sas
%reports
```

# 基础概念

## 定义宏

为了创建一个宏程序，你必须首先定义它。你从 `%MACRO` 语句开始宏定义，用 `%MEND` 语句结束定义。

| 通用格式、`%MACRO`语句和`%MEND`语句： |
| `%MACRO macro-name;text%MEND <macro-name>;` |

以下是对该语法的解释：`macro-name` 为宏命名。`macro-name` 的值可以是任何有效的 SAS 名称，只要它不是 SAS 宏设施中的保留字即可。`text` 可以是：

*   常量文本，可能包括 SAS 数据集名称
*   宏变量，可能包括 SAS 数据集名称
*   宏函数
*   宏语句

提示：`macro-name` 为宏命名。`macro-name` 的值可以是任何有效的 SAS 名称，只要它不是 SAS 宏设施中的保留字即可。`text` 可以是：

*   常量文本，可能包括 SAS 数据集名称
*   宏变量，可能包括 SAS 数据集名称
*   宏函数
*   宏语句

（注：原文示例中存在大量重复的提示文本，译文已根据翻译逻辑进行了精简整合，确保核心含义准确且不冗余）

## 示例

这是一个定义宏的示例：

```sas
%macro mymacro;
  put "Hello World";
%mend mymacro;
```

## 编译宏

为了使用一个宏，你必须通过提交其定义来编译它：

```sas
%macro mymacro;
  put "Hello World";
%mend mymacro;
```

## 调用宏

通过以下调用宏：

```sas
%mymacro;
```





当宏成功编译后，你可以在整个 SAS 会话期间在 SAS 程序中使用它，而无需重新提交宏的定义。正如你必须在代码中引用宏变量才能访问它们一样，你必须在 SAS 程序中调用宏程序才能执行它。

### 宏调用

*   通过在宏名称之前放置百分号（`%`）来指定。 
*   可以在程序中的任何地方使用，但 `DATALINES` 语句中的数据行除外（类似于宏变量引用）。
*   不需要分号，因为它们不是 SAS 语句。

要执行宏 `Prtlast`，你可以按照如下方式调用该宏：

```
%prtlast
```

**注意**：在宏调用后加上分号可能会在生成的程序中插入一个不恰当的分号，导致在编译或执行期间出现错误。

根据调用方式的不同，宏分为三种类型：名称样式（name style）、命令样式（command style）和语句样式（statement style）。在这三种类型中，名称样式的效率最高。这是因为对名称样式宏的调用总是以百分号（`%`）开始，这会立即告诉单词扫描器（word scanner）将该标记传递给宏处理器。对于另外两种类型，单词扫描器无法立即判断该标记是否应该发送给宏处理器。因此，在单词扫描器确定这一点时会浪费时间。本章中的所有宏都是名称样式宏。

## 示例

假设一个 SAS 程序由几个几个创建 SAS 数据集的程序步骤组成。假设在这些每个程序步骤执行之后，你都想打印出所创建的数据集。请记住，宏 `Prtlast` 会打印最近创建的数据集。如果 `Prtlast` 已经过编译，你可以在每个步骤之后调用它来打印每个数据集。

```
proc sort data=sasuser.courses out=courses;
   by course_code;
run;

%prtlast

proc sort data=sasuser.schedule out=schedule;
   by begin_date;
run;

%prtlast

proc sort data=sasuser.students out=students;
   by student_name;
run;

%prtlast
```

**注意**：上面的示例仅用于向你展示如何将宏整合到你的 SAS 程序中。虽然这是 `Prtlast` 宏的有效用法，但这可能不是编写此示例的最佳方法。由于 `Prtlast` 宏没有使用条件逻辑或宏编程语句，且它不做出任何决策，因此此示例并没有说明宏程序的全部威力。在本章的其余部分，你将看到比这个更有用的宏程序示例。

## 宏的执行

当你在 SAS 程序中调用宏时，单词扫描器会将宏调用传递给宏处理器，因为宏名称前的百分号是宏触发器。当宏处理器接收到 `%macro-name` 时，它会：

1.  在指定的 SAS 目录（默认为 `Work.Sasmacr`）中查找名为 `Macro-name.Macro` 的项。
2.  执行 `Macro-name` 内部已编译的宏语言语句。
3.  将 `Macro-name` 中的任何剩余文本发送到输入栈中进行单词扫描。
4.  当 SAS 编译器接收到全局 SAS 语句或遇到 SAS 步骤边界时，挂起宏执行。
5.  在 SAS 代码执行后，恢复宏语言语句的执行。

在本章的后半部分，你将看到宏执行的详细示例。一旦你学会了如何编写比本章目前看到的更复杂的宏程序，这些示例就会更有意义。现在，请记住，宏调用会在任何如 `DATA` 步骤等 SAS 语言语句编译或执行之前由宏处理器处理。在宏执行期间，宏处理器可以与以下内容直接通信：

*   全局和局部符号表。例如，宏处理器可以使用 `%LET` 语句存储宏变量值，并解析宏变量引用。
*   输入栈。例如，宏处理器可以生成文本以进行单词扫描。

在本章稍后部分，你将看到宏执行的详细示例。

## 示例

当你在 SAS 程序中调用宏时，单词扫描器会将宏调用传递给宏处理器，因为宏名称前的百分号是宏触发器。当宏处理器接收到 `%macro-name` 时，它：

1.  在指定的 SAS 目录（默认为 `Work.Sasmacr`）中查找名为 `Macro-name.Macro` 的项。
2.  执行 `Macro-name` 内部已编译的宏语言语句。
3.  将 `Macro-name` 中的任何剩余文本发送到输入栈中进行单词扫描。
4.  当 SAS 编译器接收到全局 SAS 语句或遇到 SAS 步骤边界时，挂起宏执行。
5.  在 SAS 代码执行后，恢复宏语言语句的执行。

在本章的后半部分，你将看到宏执行的详细示例。一旦你学会了如何编写比本章目前看到的更复杂的宏程序，这些示例就会更有意义。现在，请记住，宏调用会在任何如 `DATA` 步骤等 SAS 语言语句编译或执行之前由宏处理器处理。在宏执行期间，宏处理器可以与以下内容直接通信：

*   全局和局部符号表。例如，宏处理器可以使用 `%LET` 语句存储宏变量值，并解析宏变量引用。
*   输入栈。例如，宏处理器可以生成文本以进行单词扫描。

**注意**：关于全局和局部符号表，将在稍后介绍。

示例

当你在 SAS 程序中调用宏时，单词扫描器会将宏调用传递给宏处理器，因为宏名称前的百分号是宏触发器。当宏处理器接收到 `%macro-name` 时，它：

1.  在指定的 SAS 目录（默认为 `Work.Sasmacr`）中查找名为 `Macro-name.Macro` 的项。
2.  执行 `Macro-name` 内部已编译的宏语言语句。
3.  将 `Macro-name` 中的任何剩余文本发送到输入栈中进行单词扫描。
4.  当 SAS 编译器接收到全局 SAS 语句或遇到 SAS 步骤边界时，挂起宏执行。
5.  在 SAS 代码执行后，恢复宏语言语句的执行。

## 宏执行

当你在 SAS 程序中调用宏时，单词扫描器会将宏调用传递给宏处理器，因为宏名称前的百分号是宏触发器。当宏处理器接收到 `%macro-name` 时，它：

1.  在指定的 SAS 目录（默认为 `Work.Sasmacr`）中查找名为 `Macro-name.Macro` 的项。
2.  执行 `Macro-name` 内部已编译的宏语言语句。
3.  将 `Macro-name` 中的任何剩余文本发送到输入栈中进行单词扫描。
4.  当 SAS 编译器接收接收全局 SAS  或遇到 SAS  边界时，，挂起执行。
5.  在 SAS SAS 执行后后恢复宏语言语句的执行。

在本章的后半部分，你将看到宏执行的详细示例。一旦你学会了如何编写比本章目前看到的更复杂的宏程序，这些示例就会更有意义。现在，请记住，宏调用会在任何如 `DATA` 步骤等 SAS 语言语句编译或执行之前由宏处理器处理。在宏执行期间，宏处理器可以与以下内容直接通信：

*   全局和局部符号表。例如，宏处理器可以使用 `%LET` 语句存储宏变量值，并解析宏变量引用。
*   输入栈。例如，宏处理器可以生成文本以进行单词扫描。

**注意**：关于全局和局部符号表，将在稍后介绍。

示例

当你在 SAS 程序中调用宏时，单词扫描器会将宏调用传递给宏处理器，因为宏名称前的百分号是宏触发器。当宏处理器接收到 `%macro-name` 时，它：

1.  在指定的 SAS 目录（默认为 `Work.Sasmacr`）中查找名为 `Macro-name.Macro` 的项。
2.  执行 `Macro-name` 内部已编译的宏语言语句。
3.  将 `Macro-name` 中的任何剩余文本发送到输入栈中进行单词扫描。
4.  当 SAS 编译器接收到全局 SAS 语句或遇到 SAS 步骤边界时，挂起宏执行。
5.  在 SAS 代码执行后，恢复宏语言语句的执行。

（由于提供的待翻译文本存在大量重复的乱码，上述翻译已根据核心逻辑进行了结构化处理，并确保格式一致性。）




您可能希望在以下条件下指定 `MPrint` 系统选项：

* 您遇到了 SAS 语法错误或执行错误
* 您想要查看生成的生成的 SAS 代码。

`MPrint` 系统选项通常与 `SOURCE` 系统选项同步，用于显示或隐藏已执行的 SAS 代码。

## 示例

假设你想调用 `Prtlast` 宏，并使用 `MPrint` 系统选项显示宏执行后生成的 SAS 代码。目录项（Catalog Entry）

```
%macro prtlast;
   proc print data=&syslast (obs=5);
      title "Listing of &syslast data set";
   run;
%mend;
```

下面的示例代码创建一个名为 `Sales` 的数据集，指定了 `MPrint` 选项，并引用了 `Prtlast` 宏：

```
data sales;
   price_code=1;
run;
options mprint;
%prtlast
```

写入 SAS 日志的消息显示了发送给编译器的文本。注意，在写入 SAS 日志的 `MPrint` 消息中，宏变量引用（`&SYSLAST`）被解析为值 `Work.Sales`。

表 11.3 SAS 日志

| |
```
101  %prtlast
MPRINT(PRTLAST): proc print data=WORK.SALES (obs=5);
MPRINT(PRTLAST): title "Listing of WORK.SALES";
MPRINT(PRTLAST): run;
NOTE: There were 1 observations read from the dataset WORK.SALES.
NOTE: PROCEDURE PRINT used:
      real time           0.04 seconds
      cpu time            0.04 seconds
```
 |

## MLOGIC 选项

在调试程序时，另一个可能用的系统选项是 `MLOGIC` 选项。`MLOGIC` 选项会打印指示宏执行期间所采取操作的消息。

| 通用格式，`MLOGIC | NOMLOGIC` 选项：`OPTIONS MLOGIC | NOMLOGIC;` 以下是语法解释：`NOMLOGIC` 是默认设置，指定在宏执行期间不将宏操作的消息打印到 SAS 日志中。`MLOGIC` 指定在宏执行期间将宏操作的消息打印到日志中。 |

当 `MLOGIC` 系统选项生效时，SAS 日志消息中显示的信息包括

* 宏执行的开始
* 调用时宏参数的值
* 每条宏程序语句的执行
* 每个 `%IF` 条件是真还是假
* 宏执行的结束。

## 示例

假设你想在仅启用 `MLOGIC` 选项的情况下重复上一个示例。此示例代码创建一个名为 `Sales` 的数据集，设置了 `MLOGIC` 系统选项，并调用了 `Prtlast` 宏。

```
data sales;
   price_code=1;
run;
options nomprint mlogic;
%prtlast
```

当提交此代码时，写入 SAS 日志的消息将显示宏处理的开始和结束。。

表 11.4 SAS 日志

| |
```
107   %prtlast
MLOGIC(PRTLAST): Beginning execution.
NOTE: There were 1 observations read from the dataset WORK.SALES.
NOTE: PROCEDURE PRINT used:
      real time           0.02 seconds
      cpu time            0.02 seconds
MLOGIC(PRTLAST): Ending execution.
```
 |

`MLOGIC` 选项与 `SYMBOLGEN` 选项通常被



* 为了开发和调试目的而开启
* 在应用程序处于生产模式时关闭。

## 宏程序中的注释

与任何其他程序一样，你的宏程序也可以从注释中获益。如果你计划永久保存宏或与其他用户共享宏，注释将特别有帮助。你可以通过宏注释语句在宏定义中放置注释。

| 通用格式，宏注释语句：`%*comment;` 以下是语法解释：`comment` 可以是任何消息。像其他 SAS 语句一样，每个宏注释语句都以分号结束。 |

## 示例

下面的代码使用宏注释来描述宏的功能：

```
%macro printit;
   %* The value of &syslast will be substituted appropriately ;
   %* as long as a data set has been created during this session. ;
   proc print data=&syslast(obs=5);
/* 只打印前 5 个观测 */
   title "Last Created Data Set Is &syslast";
   run;
%mend;
```

注意：你也可以在宏内部使用注释符号 `/*` 和 `*/`。当这些符号出现时，宏处理器会忽略注释内的文本。

# 使用宏参数

你已经看到了宏定义的 Basic 形式。你的宏通常包含宏变量。为了让宏更具动态性，你可以使用 `%LET` 语句更新宏内部使用的宏变量的值。然而，宏定义中的参数列表允许你更方便地更新宏程序中的宏变量。参数列表是 `%MACRO` 语句的可选部分，用于命名一个或多个宏变量，当你在调用宏时指定这些宏变量的值。

## 示例

假设编译后的宏 `Printdsn` 包含了对宏变量 `dsn`（记录数据集名称）和 `vars`（记录数据集变量列表）的引用，如下：

```
%macro printdsn;
   proc print data=&dsn;
      var &vars;
   title "Listing of %upcase(&dsn) data set";
   run;
%mend;
```

你可以通过在调用宏之前使用 `%LET` 语句更改宏变量 `dsn` 或 `vars` 的值来修改 `Printdsn` 的行为。例如，你可以在宏执行时将 `sasuser.courses` 替换为 `dsn`，将 `course_code course_title days` 替换为 `vars`，如下：

```
%let dsn=sasuser.courses;
%let vars=course_code course_title days;
%printdsn
```

如果在提交此代码时开启了 `MPrint` 系统选项，则以下消息被写入 SAS 日志。注意，你在 `%LET` 语句中提供的值在宏出现在 SAS 日志时已替换到宏中。

表 11.5 SAS 日志

| |
```
7     options mprint;
8     %let dsn=sasuser.courses;
9     %let vars=course_code course_title days;
10    %printdsn
NOTE: Writing HTML Body file: sashtm.htm
MPRINT(PRINTDSN): proc print data=sasuser.courses;
MPRINT(PRINTDSN):  var course_code course_title days;
MPRINT(PRINTDSN):  title "Listing of SASUSER.COURSES data set";
MPRINT(PRINTDSN):  run;
NOTE: There were 6 observations read from the dataset
      SASUSER.COURSES.
NOTE: PROCEDURE PRINT used (Total process time):
      real time           6.59 seconds
      cpu time            0.28 seconds
```
 |

然后你可以提交新的 %LET 语句，以便在执行时将 `dsn` 的值更改为 `sasuser.schedule`，并将 `vars` 的值更改为 `course_code location begin_date`，如下：

```
%let dsn=sasuser.schedule;
%let vars=course_code location begin_date;
%printdsn
```

提交此代码时写入 SAS 日志的消息显示，新值已替换宏中的宏变量引用。

表 11.6 SAS 日志

| |
```
11   %let dsn=sasuser.schedule;
12   %let vars=course_code location begin_date;
13   %printdsn
MPRINT(PRINTDSN):   proc print data=sasuser.schedule;
MPRINT(PRINTDSN):   var course_code location begin_date;
MPRINT(PRINTDSN):   title "Listing of SASUSER.SCHEDULE data set";
MPRINT(PRINTDSN):   run;
NOTE: There were 18 observations read from the dataset
      SASUSER.SCHEDULE.
NOTE: PROCEDURE PRINT used (Total process time):
      real time           0.76 seconds
      cpu time            0.08 seconds
```
 |

你可以通过在宏定义中使用参数创建宏变量，从而使这些宏变量更容易更新。这样你就可以每次调用宏时向宏变量传递值，而不是使用独立的 %LET 语句。接下来的几节将介绍如何使用各种类型的参数创建宏变量。

## 包含位置参数的宏





当你在宏定义中包含位置参数时，在调用宏时，会为每个参数自动创建一个宏变量。要定义包含位置参数的宏，你需要在宏定义的 `%MACRO` 语句中列出宏变量的名称。之所以被称为位置参数，是因为你在宏定义中指定它们的顺序决定了它们从宏调用中获取值赋值的顺序。也就是说，当你调用一个包含位置参数的宏时，你必须按照参数在定义中定义的顺序，指定在参数中定义的宏变量的值。

| 通用形式，包含位置参数的宏定义：`%MACRO macro-name(parameter-1<,...,parameter-n>);text%MEND <macro-name>`;这里是对语法的解释：`parameter-1<,...,parameter-n>` 指定一个或多个位置参数，用逗号分隔。你必须为每个参数提供一个名称：你不能使用文本表达式来生成它。 |

要调用包含位置参数的宏，请在宏名称前加上百分号符号，并将参数值括在括号内。按照参数在宏定义中列出的顺序相同的顺序列出这些值，并用逗号分隔，如下：`macro-name(value-1<,...,value-n>)`。宏调用中列出的值：

*   可以为空值、文本、宏变量引用或宏调用
*   通过一对一对应关系赋值给参数变量。

## 示例

你可以使用位置参数在 `Printdsn` 宏定义中创建宏变量 `dsn` 和 `vars`，如下：

```
%macro printdsn(dsn,vars);
   proc print data=&dsn;
      var &vars;
   title "Listing of %upcase(&dsn) data set";
   run;
%mend;
```

在这种情况下，当你调用 `Printdsn` 宏时，你为参数中创建的宏变量分配值。在接后的示例中，值 `sasuser.courses` 被赋值给宏变量 `dsn`，值 `course_code course_title days` 被赋值给宏变量 `vars`。注意，`dsn` 的值列在第一，`vars` 的值列在第二，因为这是它们在宏定义中列出的顺序。

```
%printdsn(sasuser.courses,course_code course_title days)
```

注意：要为一个或多个位置参数替换空值，请使用逗号作为省略值的占位符，如下：

```
%printdsn(,course_code course_title days)
```

## 包含关键字参数的宏

你也可以在宏定义中包含关键字参数。与位置参数一样，关键字参数也会创建宏变量。然而，当你使用关键字参数创建宏变量时，你需要在宏定义中指定每个宏变量的名称、随后的等号以及值。关键字参数可以以任何顺序列出。为 `%MACRO` 语句中的每个参数（或变量）分配的任何值都将成为它的默认值。允许使用空值。

| 通用形式，包含关键字参数的宏定义：`%MACRO macro-name(keyword-1=<value-1><,...,keyword-n=<value-n>>);text%MEND <macro-name>`;这里是对语法的解释：`keyword-1=<value-1><,...,keyword-n=<value-n>` 指定一个或多个宏参数，后面紧跟等号。你可以在等号之后指定默认值。如果你省略了默认值，则关键字参数的值为空值。 |

当你调用定义包含关键字参数的宏时，你需要指定关键字、随后的等号以及每个参数的值。顺序并不重要。如果你在宏调用中省略了关键字参数，则关键字变量将保留其默认值，如下：

```
%macro-name(keyword-1=value-1<,...,keyword-n=value-n>)
```

## 示例

你可以使用关键字参数在 `Printdsn` 宏中创建宏变量 `dsn` 和 `vars`。此示例为宏变量 `dsn` 赋值了默认值 `sasuser.courses`，并为宏变量 `vars` 赋值了默认值 `course_code course_title days`：

```
%macro printdsn(dsn=sasuser.courses,
               vars=
course_code course_title days);
   proc print data=&dsn;
      var &vars;
   title "Listing of %upcase(&dsn) data set";
   run;
%mend;
```

要为 `dsn` 赋值 `sasuser.schedule` 并为 `vars` 赋值 `teacher course_title begin_date` 来调用 `Printdsn` 宏，请执行以下调用：

```
%printdsn(dsn=sasuser.schedule, vars=teacher course_code begin_date)
```

要使用参数的默认值调用 `Printdsn` 宏（`sasuser.courses` 作为 `dsn` 的值，`course_code course_title days` 作为 `vars` 的值），你可以执行以下调用：

```
%printdsn()
```

注意：要使用参数的默认值调用宏 `Printdsn`，你也可以执行一个显式指定这些值的宏调用，如下：

```
%printdsn(dsn=sasuser.courses,vars=course_code course_title days)
```

## 包含混合参数列表的宏

你也可以在宏定义中包含同时含有位置参数和关键字参数的参数列表。`%MACRO` 语句中的所有位置参数变量必须在任何关键字参数变量列出。

| 通用形式，包含混合参数的宏定义：`%MACRO macro-name(parameter-1<,...,parameter-n>,keyword-1=<value-1><,...,keyword-n=<value-n>>);text%MEND`;这里是对语法的解释：`parameter-1<,...,parameter-n>` 列在 `keyword-1=<value-1><,...,keyword-n=<value-n>>` 之前。 |

同样，当你调用包含混合参数列表的宏时，你必须在任何关键字值之前列出位置值，如下：

```
%macro-name(value-1<,...,value-n>,
            keyword-1=value-1<,...,keyword-n=value-n>)
```

## 示例

你可以结合位置参数和关键字参数来在 `Printdsn` 宏定义中创建宏变量。这段代码使用位置参数来创建宏变量 `dsn`，使用关键字参数来创建宏变量 `vars`：

```
%macro printdsn(dsn, vars=course_title code_code days);
   proc print data=&dsn;
      var &vars;
   title "Listing of %upcase(&dsn) data set";
   run;
%mend;
```

对 `Printdsn` 宏的以下调用将 `sasuser.schedule` 赋值给宏变量 `dsn`，并将 `teacher location begin_date` 赋值给宏变量 `vars`。注意 `dsn` 的值列在第一，因为 `dsn` 是位置参数。

```
%printdsn(sasuser.schedule, vars=teacher location begin_date)
```

现在，假设你想执行 `Printdsn` 宏，为宏变量 `vars` 赋值默认值 `course_title code_code days` 并为宏变量 `dsn` 赋值 `sasuser.courses`。你可以执行以下调用：

```
%printdsn(sasuser.courses)
```

由于此调用省略了关键字参数（vars），因此使用了该参数的默认值。

## 包含 PARMBUFF 选项的宏

你可以在宏定义中使用 PARMBUFF 选项来创建一个每次调用接受不同数量参数的宏。PARMBUFF 选项会将宏调用中的整个参数列表（包括名称式调用中的括号）赋值为自动宏变量 `SYSPBUFF` 的值。

| 通用形式，带有 PARMBUFF 选项的宏定义：`%MACRO macro-name /PARMBUFF;text%MEND`;这里是对语法的解释：text 包含了对自动宏变量 `SYSPBUFF` 的引用。 |

## 示例

以下宏定义创建了一个名为 `Printz` 的宏。`Printz` 使用不同数量的参数和自动宏变量 `SYSPBUFF` 来显示宏调用中指定的参数。该宏还使用循环来打印作为参数命的数据集。





```
%macro printz/parmbuff;
   %put Syspbuff contains: &syspbuff;
   %local num;
   %do num=1 %to %sysfunc(countw(&syspbuff));
   %let dsname=%scan(&syspbuff,&num);
      proc print data=sasuser.&dsname;
      run;
   %end;
%mend printz;
```

如果你提交一个包含两个参数的宏调用，`Printz` 宏会在 SAS 日志中写入以下行，并打印两个数据集。

```
%printz(courses, schedule)
```

表 11.7 SAS 日志

| |
```
Syspbuff contains: (courses,schedule)
```
| |

如果你提交一个包含一个参数的宏调用，`Printz` 宏会在 SAS 日志中写入以下行，并打印一个数据集：

```
%printz(courses)
```

表 11.8 SAS 日志

| |
```
Syspbuff contains: (courses)
```
| |

注意：如果宏定义同时包含一组参数和 PARMBUFF 选项，宏调用会导致参数接收值，并将整个值列表分配给 `SYSPBUFF`。

# 符号符号表

## 全局符号表

你已经对全局符号表相当熟悉了。请记住，自动宏变量存储在全局符号表中。你在开放代码（宏定义外部的代码）中使用 `%LET` 语句创建的用户自定义宏变量也存储在全局符号表中。![global 符号表](img/m52-27-g1.png)全局符号表在 SAS 会话初始化期间创建，并在会话结束时删除。全局符号表中的宏变量：

*   在会话期间任何时候都可用
*   可以由用户创建
*   其值可以在会话期间更改（某些自动宏变量除外）。

你可以通过以下方式创建全局宏变量：

*   使用 `%LET` 语句（在宏定义外部）
*   包含 `SYMPUT` 过程的 `DATA` 步
*   包含 `SYMPUTX` 过程的 `DATA` 步
*   `PROC SQL` 中包含 `INTO` 子句的 `SELECT` 语句
*   一个 `%GLOBAL` 语句

你应该已经熟悉 `%LET` 语句、`SYMPUT` 过程和 `INTO` 子句了。让我们检查 `%GLOBAL` 语句。

## %GLOBAL 语句

`%GLOBAL` 语句：

*   在全局符号表中创建一个或多个宏变量并为它们分配空值
*   可以用在宏定义内部或外部
*   对已在全局符号表中的变量没有影响

`%GLOBAL` 语句的通用形式：`%GLOBAL macro-variable-1 <...macro-variable-n>;`

以下是对语法的解释：`macro-variable` 是宏变量的名称，或者是生成宏变量名称的文本表达式。

## 示例

要在宏定义内部创建全局宏变量，可以使用 `%GLOBAL` 语句。以下示例中的 `%GLOBAL` 语句创建了两个全局宏变量 `dsn` 和 `vars`。`%LET` 语句如下为新的全局宏变量分配了值：

```
%macro printdsn;
   %global dsn vars;
   %let dsn=sasuser.courses;
   %let vars=course_title course_code days;
   proc print data=&dsn;
      var &vars;
   title "Listing of &dsn data set";
   run;
%mend;

%printdsn
```

注意：你使用 `%SYMDEL` 语句在 SAS 会话期间从全局符号表中删除宏变量。要从全局符号表中删除宏变量 `dsn`，提交以下语句：

```
%symdel dsn;
```

## 局部符号表

当调用包含参数列表的宏或在宏执行期间请求创建局部变量时，会创建一个局部符号表。宏执行完成后，局部符号表会被删除。也就是说，局部符号表只在宏执行期间存在。![local 符号表](img/m52-29-g1.png)局部符号表包含可以：

*   在宏调用时创建并初始化（即通过参数）
*   在宏执行期间创建或更新
*   在宏内部任何地方引用的

你可以通过以下方式创建局部宏变量：

*   宏定义中的参数
*   宏定义内部的 `%LET` 语句
*   宏定义内部包含 `SYMPUT` 过程的 `DATA` 步
*   宏定义内部包含 `SYMPUTX` 过程的 `DATA` 步
*   宏定义内部 `PROC SQL` 中包含 `INTO` 子句的 `SELECT` 语句
*   一个 `%LOCAL` 语句 

注意：如果已经存在局部符号表，`SYMPUT` 过程可以创建一个局部宏变量。如果在执行 `SYMPUT` 过程时不存在局部符号表，它将创建一个全局宏变量。你已经学习了在宏定义中使用参数。你也应该已经熟悉 `%LET` 语句、`SYMPUT` 过程和 `INTO` 子句了。让我们检查 `%LOCAL` 语句。

## %LOCAL 语句 

`%LOCAL` 语句：

*   只能出现在宏定义内部
*   在局部符号表中创建一个或多个宏变量并为它们分配空值
*   对已在局部符号表中的变量没有影响

在请求创建局部变量之前，不会创建局部符号表。由于局部符号表与全局符号表独立存在，可能存在名称相同但值不同的局部宏变量和全局变量。在这个示例中，第一个 `%LET` 语句创建了一个全局宏变量 `dsn` 并为其分配了值 `sasuser.courses`。宏定义内部的 `%LOCAL` 语句创建了一个局部变量 `dsn`，宏定义内部的 `%LET` 语句为其分配了值 `sasuser.register`。宏定义内部的 `%PUT` 语句将局部 `dsn` 的值写入 SAS 日志：

```
%macro printdsn;
   %global dsn vars;
   %let dsn=sasuser.courses;
   %let vars=course_title course_code days;
   proc print data=&dsn;
      var &vars;
   title "Listing of &dsn data set";
   run;
%mend;

%printdsn
```

当提交此代码时，以下语句将被写入 SAS 日志。

表 11.9 SAS 日志

| |
```
199  %let dsn=sasuser.courses;
200
201  %macro printdsn;
202     %local dsn;
203     %let dsn=sasuser.register;
204     %put The value of DSN inside Printn is &dsn;
205  %mend;
206
207  %printdsn
The value of DSN inside Printn is sasuser.register
208  %put The value of DSN outside Printn is &dsn;
The value of DSN outside Printn is sasuser.courses
```
| |

## 创建和更新变量的规则

当宏处理器在宏执行期间接收到创建或更新宏变量的请求时，宏处理器遵循某些规则。假设宏处理器在宏调用期间接收到如下 `%LET` 语句：

```
%let macvar=value;
```

宏处理器处理以下步骤：

1.  宏处理器检查宏变量 `macvar` 是否已存在于局部符号表中。如果是，宏处理器在局部符号表中更新 `macvar` 值为 value。如果 `macvar` 不在表中，宏处理器跳转到第 2 步。
2.  宏处理器检查宏变量 `macvar` 是否已存在于全局符号表中。如果是，宏处理器在全局符号表中更新 `macvar` 值为 value。如果 `macvar` 不在全局符号表中，宏处理器跳转到第 3 步。
3.  宏处理器在局部符号表中创建一个名为 `macvar` 的宏变量并为其分配值 value。





![macro variable macvar](img/m52-31-g1.png) 同样，假设宏处理器在宏调用期间接收到以下引用：

```
&macvar
```

宏处理器执行以下步骤：

1. 宏处理器检查宏变量 `macvar` 是否存在于本地符号表中。如果存在，则宏处理器从本地符号表中检索 `macvar` 的值。如果 `macvar` 不存在于本地表中，则宏处理器将继续执行到第 2 步。
2. 宏处理器检查宏变量 `macvar` 是否存在于全局符号表中。如果存在，则宏处理器从全局符号表中检索 `macvar` 的值。如果 `macvar` 不存在于全局表中，则宏处理器将继续执行到第 3 步。
3. 宏处理器将标记（tokens）返回给单词扫描器（word scanner）。在 SAS 日志中写入一条警告消息，以指示该引用未解析。

![Warning message](img/m52-31-g2.png) 注意：请记住，如果宏处理器在开放代码（open code）中接收到 `%LET` 语句或宏变量引用（`&macvar`），它仅检查全局符号表中是否存在该宏变量。如果宏程序当前没有执行，则不存在本地符号表。

## 多个本地符号表

如果你使用了嵌套宏，在宏执行期间可以同时存在多个本地符号表。也就是说，如果你定义了一个调用另一个宏程序的宏程序，并且两个宏都创建了本地符号表，那么在执行第二个宏时，会存在两个本地符号表。

## 示例

假设已经编译了以下两个宏：`Outer` 和 `Inner`。名为 `Outer` 的宏创建了一个名为 `variX` 的本地宏变量，并为其赋值值 `one`。然后 `Outer` 调用另一个名为 `Inner` 的宏程序。名为 `Inner` 的宏创建了一个名为 `variY` 的本地宏变量，并将 `variX` 的值赋值给它。

```
%macro outer;
   %local variX;
   %let variX=one;
   %inner
%mend outer;

%macro inner;
   %local variY;
   %let variY=&variX;
%mend inner;
```

我们来检查提交以下代码时，符号表会发生什么：

```
%let variX=zero;
%outer
```

1. 宏处理器接收到 `%let variX=zero;`。它检查全局符号表中是否存在名为 `variX` 的宏变量。不存在，因此宏处理器创建 `variX` 并为其赋值为零。![global symbol table](img/m52-33-g1.png)
2. 宏处理器接收到 `%outer`。宏处理器从 `Work.Sasmacr` 中检索宏 `Outer` 并开始执行它。
3. 宏处理器遇到 `%local variX;`。它创建了一个本地符号表。宏处理器在该本地表中创建宏变量 `variX` 并为其赋值一个空值（null）。这不会影响存储在全局符号表中的宏变量 `variX`。![global symbol table](img/m52-33-g2.png)
4. 宏处理器遇到 `%let variX=one;`。宏处理器检查本地符号表中的 `variX` 并为其赋值为一。![global symbol table](img/m52-33-g3.png)
5. 宏处理器接收到 `%inner`。它从 `Work.Sasmacr` 中检索宏 `Inner` 并开始执行它。
6. 宏处理器遇到 `%local variY;`。它创建了一个本地符号表。宏处理器在该表中创建宏变量 `variY` 并为其赋值一个空值。现在存在两个本地符号表![global symbol table](img/m52-33-g4.png)
7. 宏处理器遇到 `%let variY=&variX;`。它检查最近创建的本地表中的 `variX`。该符号表中不存在该宏变量，因此宏处理器接着检查另一个本地符号表。它从该表中检索值 `one` 并该值替换到 `%LET` 语句中。然后，宏处理器检查最近创建的本地符号表中是否存在名为 `variY` 的宏变量。当它找到该宏变量时，为其赋值为一![global symbol table](img/m52-33-g5.png)
8. `Inner` 宏执行完毕，在该宏内创建的本地符号表被删除。现在只存在一个本地符号表![global symbol table](img/m52-33-g6.png)
9. `Outer` 宏执行完毕，在该宏内创建的本地符号表被删除。现在不存在本地符号表。自从 `variX` 创建并被赋值为零以来，全局符号表没有发生变化![global symbol table](img/m52-33-g7.png)

如你所示，上述示例中的每个宏程序都有自己的本地符号表，只要宏在执行，该表就会存在。当宏执行结束时，它的本地符号表以及该表中包含的所有本地宏变量都会被擦除。全局符号表及其包含的所有全局宏变量保持不变。

## MPRINTNEST 选项

`MPRNEST` 选项允许将嵌套信息写入 MPRINT 输出。请记住，如果宏处理器在开放代码中接收到 `%LET` 语句或宏变量引用（`&macvar`），它仅检查全局符号表中是否存在该宏变量。如果宏程序当前没有执行，则不存在本地符号表。

| 选项 | 说明 |
| :--- | :--- |
| `MPRNEST` | 允许嵌套信息写入 MPRINT 输出。 |
| `MLOGICNEST` | 允许嵌套信息写入 SAS 日志。 |

*(注：原文中 `MPRNEST` 似乎是 `MPRNEST` 的拼写错误，此处保留原样或根据上下文理解为 MPRINTNEST)*

由于原文文本在某些部分存在重复或格式混乱，上述翻译已按照要求进行了逻辑整理。





```
MLOGIC(OUTER):  Beginning execution.
MLOGIC(OUTER):  %PUT THIS IS OUTER
THIS IS OUTER
MLOGIC(OUTER.INNER):  Beginning execution.
MLOGIC(OUTER.INNER):  %PUT THIS IS INNER
THIS IS INNER
MLOGIC(OUTER.INNER.INRMOST):  Beginning execution.
MLOGIC(OUTER.INNER.INRMOST):  %PUT THIS IS INRMOST
THIS IS INRMOST
MLOGIC(OUTER.INNER.INRMOST):  Ending execution.
MLOGIC(OUTER.INNER): Ending execution.
MLOGIC(OUTER): Ending execution.
```

|

# 条件性地处理语句

## 条件执行

你可以使用宏来控制语句的条件条件执行。回想本章开头的示例，在该示例中，你想运行一份每日报告，为在本月晚些时候的课程创建注册列表。请记住，你还想在每个周五运行一份周报，以汇总本月目前为止已产生的收入。如果你使用条件执行来确定是否应该运行第二个报告，你就可以用一个程序完成这些任务。你可以在宏级别通过 `%IF-%THEN` 和 `%ELSE` 语句执行条件执行。

| 通用形式，`%IF-%THEN` 和 `%ELSE` 语句：`%IF expression %THEN text;<%ELSE text;`这里是对该语法的解释：`expression` 可以是任何解析为整数的有效宏表达式。`text`可以指定为 

* 常量文本

* 文本表达式

* 宏变量引用、宏调用或宏程序语句。 |

如果 `expression` 解析结果为零，则它为假，并且不处理 `%THEN` 文本（取而处理可选的 `%ELSE` 文本）。如果它解析结果为除零以外的任何整数，则该表达式为真，并处理 `%THEN` 文本。如果解析结果为空或任何非整数值，则会发出错误消息。`%ELSE` 语句是可选的。然而，宏语言不包含子集形式 `%IF` 语句。因此，你不能在没有 `%THEN` 的情况下使用 `%IF`。

## %IF-%THEN 与 IF-THEN 的比较

尽管它们看起来相似，但 `%IF-%THEN/%ELSE` 语句和 `IF-THEN/ELSE` 语句属于两种不同的语言。适用于 DATA 步 `IF-THEN/ELSE` 语句大部分规则也适用于 `%IF-%THEN/%ELSE` 语句。然而，宏 `%IF-%THEN` 语句与 DATA 步 `IF-THEN` 语句之间存在几个重要的区别。

| %IF-%THEN... | IF-THEN... |

| --- | --- |
| 仅用于宏程序。 | 仅用于 DATA 步程序。 |
| 在宏执行期间执行。 | 在 DATA 步执行期间执行。 |
| 在逻辑表达式中使用宏宏变量，且不能在逻辑表达式中引用 DATA 步变量。 | 在逻辑表达式中使用 DATA 步变量。 |
| 决定哪些文本应该被复制到输入栈。 | 决定应该执行哪些 DATA 步语句(s)。在宏定义内部时，它被作为文本复制到输入栈。 |

简单的 `%DO` 和 `%END` 语句通常与 `%IF-%THEN/%ELSE` 语句结合使用，以根据 `%IF` 条件的真假来指定要处理的宏部分。在 `%THEN` 或 `%ELSE` 之后使用 `%DO` 和 `%END` 语句，以便将包含多个语句的文本条件地放入输入栈。每个 `%DO` 语句必须与一个 `%END` 语句配对。

| 通用形式，带有 `%IF-%THEN` 和 `%ELSE` 语句的 `%DO-%END`：`%IF expression %THEN %DO;text and/or macro language statements%END;%ELSE %DO;text and/or macro language statements%END;`这里是对该语法的解释：`text and/or macro language statements` 可以是常量文本、文本表达式和/或宏语句。 |

注意：语句 `%IF-%THEN`、`%ELSE`、`%DO` 和 `%END` 是宏语言语句，只能在宏程序内部。

## 示例

你可以通过 `%IF-%THEN` 控制复制到输入栈的文本，同时通过 `IF-THEN` 控制 DATA 步逻辑。在这个示例中，宏变量 `status` 的值决定了哪些变量包含在新的数据集中。数据集变量 `Location` 的值决定了新数据集变量 `Totalfee` 的值。

```
%macro choice(status);
   data fees;
      set sasuser.all;
      %if &status=PAID %then %do;
         where paid='Y';
         keep student_name course_code begin_date totalfee;
      %end;
      %else %do;
         where paid='N';
         keep student_name course_code
              begin_date totalfee latechg;
         latechg=fee*.10;
      %end;
      /* add local surcharge */
      if location='Boston' then totalfee=fee*1.06;
      else if location='Seattle'  then totalfee=fee*1.025;
      else if location='Dallas'  then totalfee=fee*1.05;
   run;
%mend choice;
```

如果 `MPRINT` 和 `MLOGIC` 系统选项都设置，SAS 日志将显示发送到编译器的文本。例如，假设你提交了以下宏调用：

```
options mprint mlogic;
%choice(PAID)
```

以下消息被写入日志。注意 `MLOGIC` 选项显示了 `%IF` 语句中表达式的评估，但没有显示 `IF` 语句中表达式的评估。

表 11.12 SAS 日志

|  

```
160  %choice(PAID)
MLOGIC(CHOICE): Beginning execution.
MLOGIC(CHOICE): Parameter STATUS has value PAID
MPRINT(CHOICE): data fees;
MPRINT(CHOICE): set sasuser.all;
MLOGIC(CHOICE): %IF condition &status=PAID is TRUE
MPRINT(CHOICE): where paid='Y';
MPRINT(CHOICE): keep student_name course_code begin_date totalfee;
MPRINT(CHOICE): if location='Boston' then totalfee=fee*1.06;
MPRINT(CHOICE): else if location='Seattle' then totalfee=fee*1.025;
MPRINT(CHOICE): else if location='Dallas' then totalfee=fee*1.05;
MPRINT(CHOICE): run;
```

 |

假设你提交以下宏调用：

```
options m mlogic;
%choice(OWED)
```

以下消息被发送到 SAS 日志。注意这次写入输入栈的文本不同。

表 11.13 SAS 日志

|  

```
161  %choice(OWED)
MLOGIC(CHOICE): Beginning execution.
MLOGIC(CHOICE): Parameter STATUS has value OWED
MPRINT(CHOICE): data fees;
MPRINT(CHOICE): set sasuser.all;
MLOGIC(CHOICE): %IF condition &status=PAID is FALSE
MPRINT(CHOICE): where paid='N';
MPRINT(CHOICE): keep student_name course_code
              begin_date totalfee latechg;
MPRINT(CHOICE): latechg=fee*.10;
MPRINT(CHOICE): if location='Boston' then totalfee=fee*1.06;
MPRINT(CHOICE): else if location='Seattle' then totalfee=fee*1.025;
MPRINT(CHOICE): else if location='Dallas' then totalfee=fee*1.05;
MPRINT(CHOICE): run;
```

 |

早些你学习了宏程序编译时发生的过程。现在你已经看到了更复杂的宏程序，我们可以再次检查这个过程。记住，在宏编译期间会检查宏语句的语法错误。如果宏定义包含宏语句语法错误，则会将错误消息写入 SAS 日志，并创建一个不可执行的（虚拟）宏。

## 示例

假设你尝试编译一个包含语法错误的宏。例如，以下程序在 `%IF-%THEN` 语句中缺少了百分号：

```
%macro printit;
   if &syslast ne _NULL_ then %do;
      proc print data=_last_(obs=5);
      title "Last Created Data Set Is &syslast";
      run;
   %end;
%mend;
```

当你提交此宏定义时，宏处理器会检查 `%IF-%THEN` 语句以及 `%DO`/`END` 语句的语法错误。由于 `%IF-%THEN` 语句存在语法错误，以下错误消息将被写入 SAS 日志。

表 11.14 SAS 日志

|





```
10   %macro printit;
11     %if &syslast ne _NULL_ then %do;
ERROR: Macro keyword DO appears as text. A semicolon or other
       delimiter may be missing.
ERROR: Expected %THEN statement not found. A dummy macro will be
       compiled.
12         proc print data=_last_(obs=5);
13         title "Last Created Data Set Is &syslast";
14         run;
15     %end;
ERROR: There is no matching %DO statement for the %END. This
      statement will be ignored.
16  %mend;
```

## 带条件处理的宏执行

在此之前你学习过，当宏处理器接收到 `%macro-name` 时，它会执行编译后的宏语言语句，例如 `%IF-%THEN`。在 `%IF` 逻辑表达式中使用的宏变量值会在宏执行期间进行解析。`%IF` 逻辑表达式会自动求值。

## 示例

假设 `Printit` 宏已经编译并存储在 `Work.Sasmacr` 目录中。

1.  首先，你提交了对 `Printit` 宏的调用，如下：

    ```
    %printit
    ```

2.  宏处理器在 SAS 目录 `Work.Sasmacr.Catalog` 条目 `Work.Sasmacr.Printit.Macro` 中找到该宏。

    ```
    %macro printit;
       %if &syslast ne _NULL_ %then %do;
          proc print data=_last_(obs=5);
          title "Last Created Data Set Is &syslast";
          run;
       %end;
    %mend;
    ```

3.  宏处理器开始执行来自 `Printit` 的编译后的宏语言语句（即 `%IF-%THEN` 语句）。由于 `%IF` 表达式为真，因此处理 `%DO` 块。

4.  宏处理器将 `%DO` 语句之后的文本（即 `PROC PRINT` 步骤）置于输入栈中。输入栈：

    ```
    proc print data=_last_(obs=5);
       title "Last Created Data Set Is &syslast";
    run;
    ```

5.  单词扫描按常例对 `PROC PRINT` 步骤进行。当遇到如 `&syslast` 这样的宏触发器时，宏引用被传递给宏处理器进行解析。宏处理器将解析后的值返回输入栈。

6.  当单词扫描器将 `PROC PRINT` 步骤的所有标记发送给编译器，并遇到 `RUN` 语句后，`PROC PRINT` 步骤开始执行。

7.  当 `PROC PRINT` 步骤执行时，宏执行会暂停；当遇到 `%MEND` 语句时，宏执行停止。

可以条件地将单个语句插入输入栈中，即使是在步骤的中间。

## 示例

假设你想根据数据集 `Sasuser.All` 中列出的内容，生成一份每个培训中心的注册人数报告。你可以指定宏程序，使得如果请求了特定课程，宏将插入一个 `WHERE ALSO` 语句，以便将报告限制为该课程。此示例还根据是否选择了课程来自定义第二行标题，如下所示：



```
%macro attend(crs,start=01jan2001,stop=31dec2001);
   %let start=%upcase(&start);
   %let stop=%upcase(&stop);
   proc freq data=sasuser.all;
      where begin_date between "&start"d and "&stop"d;
      table location / nocum;
      title "Enrollment from &start to &stop";
      %if &crs= %then %do;
         title2 "for all Courses";
      %end;
      %else %do;
         title2 "for Course &crs only";
         where also course_code="&crs";
      %end;
   run;
%mend;
```

注意：在上面的程序中，当 `crs` 值为空时，`%IF` 语句 `%if &crs=` 为真。假设你提交了以下调用，指定了一个特定课程：

```
%attend(C003)
```

此调用导致如下输出。注意第二个标题是根据宏中的 `%ELSE %DO` 语句编写的。![FREQ 过程输出](img/m52-45-g1.png)

表 11.15 SAS Log

|  

```
18   %attend(C003)
MPRINT(ATTEND):   proc freq data=sasuser.all;
MPRINT(ATTEND):   where begin_date between "01JAN2001"d and "31DEC2001"d;
MPRINT(ATTEND):   table location / nocum;
MPRINT(ATTEND):   title "Enrollment from 01JAN2001 to 31DEC2001";
MPRINT(ATTEND):   title2 "for Course C003 only";
MPRINT(ATTEND):   where also course_code="C003";
NOTE: WHERE clause has been augmented.
MPRINT(ATTEND):   run;

NOTE: Writing HTML Body file: sashtml.htm
NOTE: 从数据集 SASUSER.SCHEDULE 读取了 2 条观测值。
      WHERE (Course_Code='C003') and (Begin_Date>='01JAN2001'D and 
                                                Begin_Date<='31DEC2001'D);
NOTE: 从数据集 SASUSER.STUDENTS 读取了 207 条观测值。
NOTE: 从数据集 SASUSER.REGISTER 读取了 434 条观测值。
NOTE: 从数据集 SASUSER.COURSES 读取了 1 条观测值。
      WHERE Course_Code='C003';
NOTE: 从数据集 SASUSER.ALL 读取了 50 条观测值。
      WHERE (begin_date>='01JAN2001'D and begin_date<='31DEC2001'D) 
                                                 and (course_code='C003');
```

 |

现在假设你提交了以下调用，它指定了开始日期但没有指定课程：

```
%attend(start=01jul2001)
```

此调用导致如下输出。注意在该输出中，第二个标题行是根据宏中的 `%IF-%THEN` 语句编写的。![注册输出](img/m52-45-g2.png)

表 11.16 SAS Log

|  

```
19   %attend(start=01jul2001)
MPRINT(ATTEND):   options mprint;
MPRINT(ATTEND):   proc freq data=sasuser.all;
MPRINT(ATTEND):   where begin_date between "01JAN2001"d and "31DEC2001"d;
MPRINT(ATTEND):   table location / nocum;
MPRINT(ATTEND):   title "Enrollment from 01JAN2001 to 31DEC2001";
MPRINT(ATTEND):   title2 "for all Courses";
MPRINT(ATTEND):   run;

NOTE: 从数据集 SASUSER.SCHEDULE 读取了 6 条观测值。
      WHERE (Course_Code in ('C01', 'C002', 'C003', 'C004', 'C005', 'C006')) and
      (Begin_Date>='01JAN2001'D and Begin_Date<='31DEC2001'D);
NOTE: 从数据集 SASUSER.STUDENTS 读取了 207 条观测值。
NOTE: 从数据集 SASUSER.REGISTER 读取了 434 条观测值。
NOTE: 从数据集 SASUSER.COURSES 读取了 1 条观测值。
NOTE: 从数据集 SASUSER.ALL 读取了 50 条观测值。
      WHERE (begin_date>='01JAN2001'D and begin_date<='31DEC2001'D) 
                                                 and (course_code='C003');
```

 |

## 语句部分的条件处理

作为条件逻辑结果处理的文本可以是语句的一小部分。这使得在语句中间条件地插入文本成为可能。

## 示例

假设从 SAS 数据集中打印频率计数表。你可以根据宏参数的值生成单向表或双向表。此示例在调用中仅指定了 `cols` 参数时，会创建一个单向表。如果也指定了 `rows` 参数，它会创建一个双向表。

```
%counts (cols=_all_,rows=,dsn=&syslast);
   title "Frequency Counts for %upcase(&dsn) data set";
   proc freq data=&dsn;
      tables
      %if &rows ne %then &rows *;
      &cols;
   run;
%mend counts;
```

假设你提交了以下调用，它同时指定了 `cols` 和 `rows`：

```
%counts(dsn=sasuser.all, cols=paid, rows=course_number)
```

此调用的部分输出如下所示。注意宏创建了一个双向表。![频率计数](img/m52-46-g1.png)日志显示了此宏生成的 PROC FREQ 代码。

表 11.17 SAS Log

|  





```
 28   %counts(dsn=sasuser.all, cols=paid, rows=course_number)
MPRINT(COUNTS):   title "Frequency Counts for SASUSER.ALL data set";
MPRINT(COUNTS):   proc freq data=sasuser.all;
MPRINT(COUNTS):   tables course_number * paid;
MPRINT(COUNTS):   run;

NOTE: There were 18 observations read from the data set SASUSER.SCHEDULE.
      WHERE Course_Code in ('C001', 'C002', 'C003', 'C004', 'C005', 'C006');
NOTE: There were 207 observations read from the data set SASUSER.STUDENTS.
NOTE: There were 434 observations read from the data set SASUSER.REGISTER.
NOTE: There were 6 observations read from the data set SASUSER.COURSES.
NOTE: There were 434 observations read from the data set SASUSER.ALL.
NOTE: PROCEDURE FREQ used (Total process time):
```

现在假设你提交了以下调用，它指定了 `cols` 但没有指定 `rows`：

```
%counts(dsn=sasuser.all, cols=paid)
```

该调用产生的输出所示。注意，这次宏创建了一个单向表。![频率计数](img/m52-46-g2.png)日志显示了生成的 TABLES 语句。

表 11.18 SAS 日志

|  

```
 29   %counts(dsn=sasuser.all, cols=paid)
MPRINT(COUNTS):   title "Frequency Counts for SASUSER.ALL data set";
MPRINT(COUNTS):   proc freq data=sasuser.all;
MPRINT(COUNTS):   tables paid;
MPRINT(COUNTS):   run;

NOTE: There were 18 observations read from the data set SASUSER.SCHEDULE.
      WHERE Course_Code in ('C001', 'C002', 'C003', 'C004', 'C005', 'C006');
NOTE: There were 207 observations read from the data set SASUSER.STUDENTS.
NOTE: There were 434 observations read from the data set SASUSER.REGISTER.
NOTE: There were 6 observations read from the data set SASUSER.COURSES.
NOTE: There were 434 observations read from the data set SASUSER.ALL.
NOTE: PROCEDURE FREQ used (Total process time):
```

 |

## 宏比较中的大小写敏感性

记住，在 `%IF` 表达式中进行的比较是大小写敏感的。

## 示例

如果你在程序文本中使用错误的大小写来构造 `%IF` 语句，该语句将永远为真。例如，下面的 `%IF` 语句始终为假，因为 `_null_` 以小写形式指定，但在 SAS 中始终以大写形式存储：

```
%macro prtlast;
   %if &syslast=_null_ %then %do;
      %put No data sets created yet.;
   %end;
   %else %do;
      proc print;
         title "Last Created Data Set is &syslast";
      run;
   %end;
%mend;
options mprint mlogic symbolgen;
%prtlast
```

假设当你提交此示例时 `SYSLAST` 的值为 `_NULL_`。以下信息被写入了 SAS 日志。

表 11.19 SAS 日志

|  

```
29   %prtlast
MLOGIC(PRTLAST): Beginning execution.
SYMBOLGEN: Macro variable SYSLAST resolves to _NULL_
MLOGIC(PRTLAST): %IF condition &syslast = _null_ is FALSE

NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE PRINT used:
      real time           1:32.58
      cpu time            0.05 seconds

MPRINT(PRTLAST): proc print;
ERROR: There is not a default input data set (_LAST_ is _NULL_).
SYMBOLGEN: Macro variable SYSLAST resolves to _NULL_
MPRINT(PRTLAST): title "Last Created Data Set is _NULL_";
MPRINT(PRTLAST): run;

NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE PRINT used:
      real time           0.01 seconds
      cpu time            0.01 seconds
MLOGIC(PRTLAST): Ending execution.
```

 |

提示：在构造 `%IF` 语句时，`%UPCASE` 函数非常有用。关于 `%UPCASE` 函数的更多信息，请参见介绍宏变量。

# 迭代处理语句

## 概述

许多宏应用需要迭代处理。通过迭代 `%DO` 语句，你可以反复：

* 执行宏编程代码
* 生成 SAS 代码

| 带有 `%END` 语句的迭代 `%DO` 语句通用形式：`%DO index-variable=start %TO stop <%BY increment>;text%END;` | 以下是对语法的说明：`index-variable` 是宏变量名或生成宏变量名称的文本表达式。`start` 和 `stop` 指定整数或生成整数的宏表达式，用于控制迭代 `%DO` 和 `%END` 语句之间的宏部分的处理次数。`increment` 指定整数（非 0）或宏表达式 | 迭代 `%DO` 语句可以用于：

* 执行宏编程代码
* 生成 SAS 代码。

（注：由于原文中存在大量重复和错误片段，已根据要求进行清理并翻译核心内容。）




```
MLOGIC(HEX): %DO loop index variable I is now 30; loop will
               iterate again.
MPRINT(HEX): value=30;
MPRINT(HEX): put "Hexadecimal form of 30 is " value hex6.;
MLOGIC(HEX): %DO loop index variable I is now 32; loop will
               not iterate again.
MPRINT(HEX): run;

Hexadecimal form of 20 is 000014
Hexadecimal form of 22 is 000016
Hexadecimal form of 24 is 000018
Hexadecimal form of 26 is 00001A
Hexadecimal form of 28 is 00001C
Hexadecimal form of 30 is 00001E
NOTE: DATA statement used:
      real time           0.06 seconds
      cpu time            0.06 seconds

MLOGIC(HEX): Ending execution.
```

## 生成完整的步骤

你可以使用迭代 `%DO` 语句来构建创建完整 SAS 步骤的宏循环。

## 示例

假设几年的课程设置存储在系列以年份命名的外部文件中，例如 `Raw1999.dat` 和 `Raw2000.dat`。所有文件具有相同的记录布局。假设你想将每个文件读取到独立的 SAS 数据集中。以下宏使用 `%DO` 语句创建一个循环，从每个指定的外部文件中创建一个数据集：

```sas
%macro readraw(first=1999,last=2005);
   %local year;
   %do year=&first %to &last;
      data year&year;
         infile "raw&year..dat";
         input course_code $4.
         location $15.
         begin_date date9.
         teacher $25.;
      run;

      proc print data=year&year;
         title "Scheduled classes for &year";
         format begin_date date9.;
      run;
   %end;
%mend readraw;
```

假设你向 `Readraw` 宏提交了以下调用：

```sas
%readraw(first=2000,last=2002)
```

该宏创建了名为 `Year2000`、`Year2001` 和 `Year2002` 的三个数据集。记住，为了让程序正常运行，原始数据文件必须命名命名，并且必须存储在程序指定的位置。生成的 DATA 步骤显示在日志中。

表 11.22 SAS 日志

```
336  %readraw(first=2000,last=2002)
MLOGIC(READRAW):  Beginning execution.
MLOGIC(READRAW):  Parameter FIRST has value 2000
MLOGIC(READRAW):  Parameter LAST has value 2002
MLOGIC(READRAW):  %LOCAL  YEAR
MLOGIC(READRAW):  %DO loop beginning; index variable YEAR; start value is 2000; 
      stop value is 2002; by value is 1.
MPRINT(READRAW):   data year2000;
MPRINT(READRAW):   infile "raw2000.dat";
MPRINT(READRAW):   input course_code $4\. location $15\. begin_date date9\. 
                          teacher $25.;
MPRINT(READRAW):   run; 
```

# 使用算术和逻辑表达式

## %EVAL 函数

`%EVAL` 函数评估整数算术表达式或逻辑表达式。逻辑表达式和算术表达式是运算符和操作数的序列，形成一组指令，并对其进行评估以产生结果。

* 算术表达式包含一个算术运算符。
* 逻辑表达式包含一个逻辑运算符。

| 通用形式，`%EVAL` 函数：`%EVAL(arithmetic or logical expression)` |

%EVAL` 函数

* 将整数字符串和十六进制字符串转换为整数
* 将代表算术、比较和逻辑运算符的标记转换为宏层级运算符
* 执行算术和逻辑操作。

对于算术表达式，如果操作结果为非整数值，`%EVAL` 将该值截断为整数。此外，当在算术表达式中使用非整数时，`%EVAL` 会返回空值并发出错误消息。`%EVAL` 评估逻辑表达式并返回一个值来表示该表达式是真还是假。值为 `0` 表示表达式为假，值为 `1` 或任何其他数值表示表达式为真。`%EVAL` 函数不将以下内容转换为数值：

* 包含句号或 E 计数法的数值字符串
* SAS 日期和时间常量。

以下是一些示例。

## 示例

下表显示了算术和逻辑表达式的示例，以及 `%EVAL` 在评估这些表达式时产生的结果。

| 如果你提交了这些语句... | 这些消息被写入日志中... |
| --- | --- |
| ```sas
%put value=%eval(10 lt 2);
``` | ```sas
value=0
``` |
| ```sas
%put value=10+2; 
%put value=%eval(10+2);
``` | ```sas
value=10+2 
value=12
``` |
| ```sas
%put value=%eval(10 lt 2);
``` | ```sas
value=0
``` |
| ```sas
%put value=10+2; 
%put value=%eval(10+2);
``` | ```sas
value=10+2 
value=12
``` |
| ```sas
%put value=%eval(10 lt 2);
``` | ```sas
value=0
``` |
| ```sas
%put value=10+2; 
%put value=%eval(10+2);
``` | ```sas
value=10+2 
value=12
``` |
| ```sas
%put value=%eval(10 lt 2);
``` | ```sas
value=0
``` |
| ```sas
%put value=10+2; 
%put value=%eval(10+2);
``` | ```sas
value=10+2 
value=12
``` |
| ```sas
%put value=%eval(10 lt 2);
``` | ```sas
value=0
``` |
| ```sas
%put value=10+2; 
%put value=%eval(10+2);
``` | ```sas
value=10+2 
value=12
``` |
| ```sas
%put value=%eval(10 lt 2);
``` | ```sas
value=0
``` |
| ```sas
%put value=10+2; 
%put value=%eval(10+2);
``` | ```sas
value=10+2 
value=12
``` |

*(注：上述表格是提供文本的紧凑表示)*




宏程序通过宏定义创建，宏由一个 `%MACRO` 语句和一个 `%MEND` 语句组成。`%MACRO` 语句还为宏提供了一个名称。宏语言语句和 SAS 语言语句的任何组合都可以放在宏定义中。宏定义在执行之前必须经过编译。`MCOMPILENOTE=` 选项会在宏编译完成后向 SAS 日志中输出一条备注。要执行名称风格的宏，您需要在宏名称前加上百分号 `%` 来提交对宏的调用。

### 开发和调试宏

两个系统选项 `MLOGIC` 和 `MPRINT` 对宏的开发和调试非常有帮助。`MLOGIC` 选项会将跟踪宏执行情况的消息写入 SAS 日志。`MPRINT` 选项会在所有宏解析完成后打印发送到编译器的文本。`SYMBOLGEN` 选项和宏注释对宏的开发和调试也很有用。

### 使用宏参数

您可以在宏定义中使用参数列表，使您的宏更具活性且易于适应。参数可以是位置参数，也可以是关键字参数。您还可以使用包含位置参数和关键字参数的混合参数列表。参数定义了宏变量，在调用宏时它们可以取不同的值，包括空值。您可以使用 `PARMBUFF` 选项结合自动宏变量 `SYSPBUFF` 来定义一个每次调用时都能接受不同数量参数的宏。

### 理解符号表

当宏执行时，它有时会创建自己的临时符号表，称为局部符号表。除了全局符号表外，还局部符号表。如果宏创建或解析了宏变量，则可能会使用局部符号表。为了完全控制宏的行为，您必须理解宏处理器在特定情况下确定访问哪种符号表的基本规则。`%GLOBAL` 和 `%LOCAL` 等语句允许您显式地定义宏变量的存储位置。`%SYMDEL` 语句允许您在 SAS 会话期间从全局符号表中删除宏变量。您可以在宏定义内部调用另一个宏。也就是说，您可以嵌套宏。当调用嵌套宏时，可能会同时存在多个局部符号表。`MPRINTNEST` 和 `MLOGICNEST` 选项会在为 `MPRINT` 和 `MLOGIC` 选项写入 SAS 日志的消息中提供嵌套信息。

### 条件处理语句

通过 `%IF-%THEN/%ELSE` 语句可以使用条件处理。这些语句控制当表达式求值为真或假时，宏处理器采取的操作。该操作可以是执行其他宏编程语句，也可以是将文本放置在输入栈上。如果描述此操作的代码包含多个语句，则必须将这些代码封装在 `%DO` 语句和 `%END` 语句之间。可以条件地将整个 SAS 步骤、整个 SAS 语句或 SAS 语句的部分放置在输入栈上。

### 迭代处理语句

要执行重复操作，您可以使用 `%DO` 循环。您可以使用迭代处理生成完整的 SAS 步骤、单个语句或依赖于数据的步骤。

### 使用算术和逻辑表达式

您使用 `%EVAL` 函数来评估不包含任何非整数或缺失值的算术或逻辑表达式。需要数值或逻辑表达式宏语言函数和语句会自动使用 `%EVAL` 函数。您使用 `%SYSEVALF` 函数来评估包含非整数或缺失值的算术或逻辑表达式。

## 示例程序

### 定义基础宏

```
%macro prtlast;
   proc print data=&syslast (obs=5);
   title "Listing of &syslast data set";
   run;
%mend;
```

### 定义带有位置参数的宏

```
%macro printdsn(dsn,vars);
   proc print data=&dsn;
      var &vars;
      title "Listing of %upcase(&dsn) data set";
   run;
%mend;
```

### 定义带有关键字参数的宏

```
%macro printdsn(dsn=sasuser.courses,
              vars=course_code 
              course_title days);
   proc print data=&dsn;
      var &vars;
      title "Listing of %upcase(&dsn) data set";
   run;
%mend;
```

### 定义带有混合参数的宏

```
%macro printdsn(dsn, vars=course_title course_code days);
   proc print data=&dsn;
      var &vars;
      title "Listing of %upcase(&dsn) data set";
   run;
%mend;
```

### 使用 %IF-%THEN 语句

```
%macro choice(status);
   data fees;
      set sasuser.all;
      %if &status=PAID %then %do;
         where paid='Y';
         keep student_name course_code begin_date totalfee;
      %end;
      %else %do;
         where paid='N';
         keep student_name course_code
              begin_date totalfee latechg;
         latechg=fee*1.10;
      %end;
      /* add local surcharge */
     if location='Boston' then totalfee=fee*1.06;
     else if location='Seattle' then totalfee=fee*1.025;
     else if location='Dallas' then totalfee=fee*1.05;
   run;
%mend choice;
```

### 使用迭代 %DO 语句

```
%macro hex(start=1,stop=10,incr=1);
   %local i;
   data _null_;
   %do i=&start %to &stop %by &incr;
      value=&i;
      put "Hexadecimal form of &i is ";
   %end;
   run;
%mend hex;
options mprint mlogic symbolgen;
%hex(20,30)
```

## 注意要点

* 宏程序通过使用 `%MACRO` 语句和 `%MEND` 语句来定义。
* 通过在宏名称前输入 `%` 来执行和调用宏。
* `MPRINT`、`MLOGIC` 和 `SYMBOLGEN` 系统选项对开发和调试很有用。
* 参数可以通过创建值可被宏调用更新的宏变量，使您的宏程序更具活性。
* 您可以使用 `%IF-%THEN` 语句条件地处理整个 SAS 步骤、SAS 语句或语句的部分。
* 您可以使用迭代 `%DO` 语句创建可以处理重复任务的宏循环。

# 测试

请为每个问题选择最佳答案。完成测试后，请使用附录中的答案页检查您的答案。

1. 下列哪项是错误的？

    1. `%MACRO` 语句必须与 `%MEND` 语句配对。
    2. 宏定义可以包含宏变量引用，但不能包含 SAS 语言语句。
    3. 编译宏时，只对宏语言语句进行语法错误检查。
    4. 编译后的宏默认存储在临时的 SAS 目录中。

2. 下列哪个示例正确定义了一个名为 `Print` 且实现了名为 `vars` 和 `total` 参数的宏？

    1. ```
       %macro print(vars, total);
           proc print data=classes;
              var vars;
              sum total;
           run;
       %mend print;
       ```
    2. ```
       %macro print('vars', 'total');
           proc print data=classes;
              var &vars;
              sum &total;
           run;
       %mend print;
       ```
    3. ```
       %macro print(vars, total);
           proc print data=classes;
              var &vars;
              sum &total;
           run;
       %mend print;
       ```
    4. ```
       %macro print(vars, total);
           proc print data=classes;
              var :vars;
              sum :total;
           run;
       %mend print;
       ```

3. 下列哪项正确引用了此处所示名为 `Printdsn` 的宏：





```sas
%macro printdsn(dsn,vars);
   %if &vars= %then %do;
      proc print data=&dsn;
      title "Full Listing of %upcase(&dsn) data set";
      run;
   %end;
   %else %do;
      proc print data=&dsn;
             var &vars;
          title "Listing of %upcase(&dsn) data set";
          run;
   %end;
%mend;
```

1. ```sas
%printdsn(sasuser.courses, course_title days);
```

2. ```sas
%printdsn(dsn=sasuser.courses, vars=course_title days)
```

3. ```sas
%printdsn(sasuser.courses, course_title days);
```

4. ```sas
%printdsn(sasuser.courses, course_title, days)
```

4. 如果你在宏程序定义中使用使用了混合参数列表，下列哪项是错误的？

    1. 你必须在任何关键字参数之前列出位置参数。

    2. 位置参数和关键字参数的值都存储在本地符号表中。

    3. 关键字参数的默认值是在宏定义中分配的值，而位置参数的默认值为空值（null）。

    4. 在调用宏时，通过省略调用中的参数可以为关键字参数分配空值（null）。

5. 下列哪项是错误的？

    1. 宏程序在你提交宏定义时会被编译。

    2. 宏程序在你调用它（`%macro-name`）时会被执行。

    3. 宏程序只有在执行执行后才会被存储在 SAS 目录条目中。

    4. 宏程序在编译它的 SAS 会话期间一直是可以执行的。

6. 当你在宏程序中使用 `%IF-%THEN` 语句时，

    1. 如果描述条件动作的代码包含多个语句，你必须在代码周围放置 `%DO` 和 `%END` 语句。

    2. `%ELSE` 语句是可选的。

    3. 你不能在 `%IF` 语句的逻辑表达式中引用 DATA 步变量。

    4. 以上均都是。

7. 下列哪项可以被放入输入栈（input stack）？

    1. 仅完整的步骤（steps）。

    2. 仅完整的步骤或完整的语句。

    3. 仅完整的语句或语句内部的文本片段。

    4. 完整的步骤、完整的语句或语句内部的文本片段。

8. 下列哪项在本地符号表中创建名为 `class` 的宏变量？

    1. ```sas
       data _null_;
          set sasuser.courses;
          %let class=course_title;
       run;
    ```

    2. ```sas
       data _null_;
          set sasuser.courses;
          call symput('class', course_title);
       run;
    ```

    3. ```sas
       %macro sample(dsn);
          %local class;
          %let class=course_title;
          data_null_;
             set &dsn;
           run;
       %mend;
    ```

    4. ```sas
       %global class;
       %macro sample(dsn);
          %let class=course_title;
          data _null_;
             set &dsn;
           run;
       %mend;
    ```

9. 下列哪个示例正确定义了宏程序 `Hex`？

    1. ```sas
       %macro hex(start=1, stop=10, incr=1);
          %local i;
          data _null_;
          %do i=&start to &stop by &incr;
             value=&i;
             put "Hexadecimal form of &i is " value hex6.;
          %end;
          run;
       %mend hex;
    ```

    2. ```sas
       %macro hex(start=1, stop=10, incr=1);
          %local i;
          data _null_;
          %do i=&start %to &stop %by &incr;
             value=&i;
             put "Hexadecimal form of &i is " value hex6.;
          %end;
          run;
       %mend hex;
    ```

    3. ```sas
       %macro hex(start=1, stop=10, incr=1);
          %local i;
          data _null_;
          %do i=&start to &stop by &incr;
             value=&i;
             put "Hexadecimal form of &i is " value hex6.;
          run;
       %mend hex;
    ```

    4. ```sas
       %macro hex(start=1, stop=10, incr=1);
          %local i;
          data _null_;
          %do i=&start %to &stop %by &incr;
             value=&i;
             put "Hexadecimal form of &i is " value hex6.;
          %end
          run;
       %mend hex;
    ```

10. 当你提交对已编译宏的调用时，发生了什么？

    1. 首先，宏处理器检查宏中所有的宏编程语句以是否有语法错误。然后，宏处理器执行宏中的所有语句。

    2. 宏处理器执行编译的宏编程语句。然后，宏处理器执行宏中的所有语句。

    3. 首先，宏处理器检查宏中所有的宏编程语句以是否有语法错误。然后，宏处理器执行宏中的所有语句。

    4. 宏处理器执行编译的宏编程语句。然后，宏处理器执行宏中的所有语句。





永久存储宏程序的一种方法是将其保存到外部文件中。然后，你可以使用 `%INCLUDE` 语句将存储在外部文件的语句插入到程序中。如果外部文件包含宏定义，则在提交 `%INCLUDE` 语句时会编译该宏。之后，你可以在同一个程序的后续再次调用该宏，或者在当前 SAS 会话的后续任何时候再次调用。

| 通用格式，`%INCLUDE`语句：`%INCLUDE file-specification </SOURCE2>;` | 以下是语法的解释：<br>`file-specification` 描述包含要插入的 SAS 代码的文件位置。<br>`SOURCE2` 导致插入到程序中的 SAS 语句显示在 SAS 日志（log）中。如果在 `%INCLUDE` 语句中未指定 `SOURCE2`，则由 SAS 系统选项 `SOURCE2` 的设置来控制是否显示插入的代码。 |

通过在外部存储你的宏程序并使用 `%INCLUDE` 语句，与使用会话编译的宏相比，你获得了几个优势：

- 宏定义的源代码不需要包含在你的程序中。
- 宏定义的单个副本可以被多个程序共享。
- 外部文件中的宏定义可以使用任何文本编辑器轻松查看和编辑。
- 访问存储在外部文件中的宏定义不需要特殊的 SAS 系统选项。

## 示例

你可以通过使用 `%INCLUDE` 语句将宏定义插入程序中来编译宏。然后，你可以调用该宏来执行它。假设以下宏定义存储在外部文件 `C:\sasfiles\prtlast.sas` 中：

```
%macro prtlast;
   %if &syslast ne _NULL_ %then %do;
      proc print data=&syslast (obs=5);
         title "Listing of &syslast data set";
      run;
   %end;
   %else
      %put No data set has been created yet.;
%mend;
```

你可以提交以下代码来访问、编译并执行 `Prtlast` 宏。此示例中包含了 `PROC SORT` 步骤，以便创建一个 `Prtlast` 宏可以打印的数据集。

```
%include 'c:\sasfiles\prtlast.sas' /source2;

proc sort data=sasuser.courses out=bydays;
   by days;
run;

%prtlast
```

注意：外部文件的位置和名称取决于你的操作系统环境。当提交此代码时，以下消息将写入 SAS 日志。请注意，由于在 `%INCLUDE` 语句中指定了 `SOURCE2`，因此宏定义被写入日志。

表 12.1 SAS 日志

```
NOTE: %INCLUDE (level 1) file prtlast.sas is file
              C:\sasfiles\prtlast.sas.
31   +%macro prtlast;
32   +   %if &syslast ne _NULL_ %then %do;
33   +      proc print data=&syslast(obs=5);
34   +      title “Listing of &syslast data set”;
35   +      run;
36   +   %end;
37   +   %else
38   +      %put No data set has been created yet.;
39   +%mend;
NOTE: %INCLUDE (level 1) ending.
40
41   proc sort data=sasuser.courses out=bydays;
42      by days;
43   run;

NOTE: There were 6 observations read from the dataset
      SASUSER.COURSES.
NOTE: The data set WORK.BYDAYS has 6 observations and
      4 variables.
NOTE: PROCEDURE SORT used:
      real time           0.04 seconds
      cpu time            0.04 seconds

44
45   %prtlast
NOTE: There were 5 observations read from the dataset
      WORK.BYDAYS.
NOTE: PROCEDURE PRINT used:
      real time           1.07 seconds
      cpu time            0.26 seconds
```

这里是代码生成的输出。![Listing of WORK.BYDAYS data set](img/m53-4-g1.png)

# 在目录 SOURCE 项中存储宏定义

## 概述

永久存储宏的另一种方法是将宏定义存储在 SAS 目录（catalog）的 `SOURCE` 项。如果你决定将宏程序存储在 SAS 目录中，则必须将每个宏程序存储在单独的 `SOURCE` 项。将每个 `SOURCE` 项命名为与其存储的宏相同的名称是一个好习惯。例如，名为 `Printit` 的宏将存储在同样名为 `Printit` 的 `SOURCE` 项中。

注意：SAS 目录是存储程序源代码和其他类型内容的 SAS 库（libraries）的成员。要将宏定义作为 SAS 目录中的 `SOURCE` 项，你需要使用“另存对象”（Save As Object）窗口。

## 示例

将 `Printit` 宏定义保存到 `Sasuser.Mymacs` 目录，请执行以下步骤：

1. 选择 `File>Save As Object`。在 `Save As Object` 窗口中，选择 `Sasuser` 库。
2. 如果 `Sasuser.Mymacs` 目录尚不存在，你需要创建它。你可以选择“创建新目录”（Create New Catalog）图标，或右键点击 `Save As Object` 窗口并选择 `New` 以打开“新目录”窗口。输入 `Mymacs` 作为新目录的并点击 `OK`。
3. 在 `Entry Name` 字段中输入 `Printit`。确保 `Entry Type` 设置为 `SOURCE`，然后点击 `Save`。

提示：若你使用“程序编辑器”（Program Editor），也可以使用 `SAVE` 命令将宏定义保存为目录项。在 `libref.catalog` 中，`libref` 是库名，`catalog` 是目录名。

## CATALOG 过程

如果你将宏存储在目录中，你可能想查看目录的内容。你可以通过资源管理器（Explorer）窗口双击它来查看目录内容。`CONTENTS` 过程列出了目录的内容。

| 通用格式，带有 `CONTENTS`语句的 `PROC CATALOG`：`PROC CATALOG=libref;CONTENTS;` | 以下是语法的解释：`libref` 是有效的目录。 |

注意：`CAT=` 是 `CATALOG` 的别名。

## 示例

你可以如下所示使用 `PROC CATALOG` 查看临时目录 `Work.Sasmacr` 中的所有宏：

```
proc catalog cat=work.sasmacr;
   contents;
   title "Default Storage of SAS Macros";
quit;
```

此 `PROC CATALOG` 步骤产生的结果类似于。当前 SAS 会话期间编译的宏。Default Storage of SAS Macros `PROC CATALOG` 可以显示宏的名称和属性，但无法查看宏定义本身。

## CATALOG 访问方法

如果你将宏定义存储在 SAS 目录的 `SOURCE` 项，你可以在 `FILENAME` 语句中使用 `CATALOG` 访问方法，结合 `%INCLUDE` 语句将宏定义插入到 SAS 程序中。

| 通用格式，引用单个 `SOURCE`的`CATALOG`访问方法：`FILENAME fileref CATALOG 'libref.catalog.entry-name.entry-type';%INCLUDE fileref;` | 以下是语法的解释：`fileref` 是有效的引用。`libref.catalog.entry-name.entry-type` 是四级目录名。`entry-type` 是 `SOURCE`。 |

## 示例

假设你已将宏定义作为 `SOURCE` 项存储在 `Sasuser.Mymacs` 目录中：

```
%macro prtlast;
   %if &syslast ne _NULL_ %then %do;
      proc print data=&syslast (obs=5);
         title "Listing of &syslast data set";
      run;
   %end;
   %else
      %put No data set has been created yet.;
%mend;
```

你可以使用 `CATALOG` 访问方法结合 `%INCLUDE` 语句来编译 `Prtlast` 宏。然后你可以在程序的后续部分引用该宏。

```sas
filename prtlast catalog 'sasuser.mymacs.prtlast.source';
%include prtlast;
proc sort data=sasuser.courses out=bydays;
   by days;
run;
%prtlast
```

你也可以使用 `CATALOG` 访问方法引用多个 `SOURCE` 项，只要这些项存储在同一个 SAS 目录中即可。





| 通用格式，使用 `CATALOG` 访问方法引用多个 `SOURCE` 条目：`fileref CATALOG 'libref.catalog';%INCLUDE fileref(entry-1);%INCLUDE fileref(entry-2);` 以下是该语法的解释：`fileref` 是有效的 `fileref`。`libref.catalog` 是一个两级目录库名称。`entry-1` 和 `entry-2` 是 `library.catalog` 中 `SOURCE` 条目的名称。 |

## 示例

假设你有两个宏，分别名为 `Prtlast` 和 `Sortlast`，它们被存储在一个 SAS 目录库（catalog）中。目录库条目：`Sasuser.Mymacs.Prtlast.Source`

```
%macro prtlast;
   %if &syslast ne _NULL_ %then %do;
      proc print data=&syslast(obs=5);
      title "Listing of &syslast data set";
      run;
   %end;
   %else
     %put No data set has been created yet.;
%mend;
```

目录库条目：`Sasuser.Mymacs.Sortlast.Source`

```
%macro sortlast(sortby);
   %if &syslast ne _NULL_ %then %do;
      proc sort data=&syslast out=sorted;
         by &sortby;
      run;
   %end;
   %else
     %put No data set has been created yet.;
%mend;
```

你可以结合 `CATALOG` 访问方法和 `%INCLUDE` 语句来编译这两个宏。然后，你可以在程序的后续部分调用这些宏。在此示例中，假设宏的名称与存储它们的的 `SOURCE` 条目名称相同：

```
filename prtsort catalog 'sasuser.mymacs';
%include prtsort(prtlast) / source2;
%include prtsort(sortlast) / source2;

data current(keep=student_name course_title begin_date location);
   set sasuser.all;
   if year(begin_date)=2001;
   diff=year(today())-year(begin_date);
   begin_date=begin_date+(365*diff);
run;

%sortlast(begin_date)
%prtlast
```

此代码产生以下输出：![Listing of WORK.SORTED data set](img/m53-11-g1.png)

# 使用自动调用功能 (Autocall Facility)

## 概述

你可以通过自动调用功能在预定义的源库中搜索宏定义，从而使你的 SAS 会话或程序可以使用宏。这些预定义的源库被称为自动调用库（autocall libraries）。你可以将宏定义永久性地存储在自动调用库中，并且可以设置多个自动调用库。当你使用这种方法时，不需要编译宏即可对其进行执行。也就是说，如果宏定义存储在自动调用库中，那么在提交对宏的调用之前，不需要提交或包含该宏的定义。假设你已经在自动调用库中存储了一个包含宏定义的文件。当提交提交对该宏的调用时：

*   宏处理器会在自动调用库中搜索该宏
*   宏会被编译并存储，方式就像你手动提交了它一样（即编译后的宏存储在 `Work.Sasmacr` 的默认位置）
*   宏会被执行。

一旦宏被编译，就可以在同一个 SAS 会话中根据需要执行。在 SAS 会话结束时，编译后的宏将从 `Work.Sasmacr` 目录库中删除，但源代码仍保留在自动调用库中。

## 创建自动调用库

自动调用库可以是以下任意一种：

*   包含源文件的目录
*   分区数据集 (PDS)
*   SAS 目录库 (catalog)

创建自动调用库的方法取决于你正在使用的操作系统环境。要在基于目录的操作系统（如 Windows 或 UNIX）中创建自动调用库，请创建一个用于存储宏定义的目录。该目录中的每个宏定义都是一个独立的文件，扩展名为 `.sas`，且文件名与其包含的宏同名。

## 示例

假设你想将宏 `Prtlast` 保存到自动自动调用库中。在基于目录的操作系统中，第一步是创建一个存放你的宏源文件的目录。你可以使用“另存为”窗口创建目录，并将宏定义保存到该目录中。在活动的代码编辑窗口中带有 `Prtlast` 定义的情况下，选择`文件>另存为`。在“另存为”窗口中，导航到你想要创建自动调用库的位置。选择`新建文件夹`，输入目录名称并点击`确定`。然后输入文件名 `Prtlast`，确保文件类型为 `.sas`，并点击`保存`。

**提示**：你也可以 `FILE` 命令将你的宏定义保存到自动调用库中。要使用 `FILE` 命令，你需要在命令行中输入 `file '<<path>external-file-name'`。

## 默认自动调用库

SAS 为你提供了几个默认的自动调用库。这里列出了 SAS 提供的自动调用库中的某些宏。

| 宏语法 | 目的 |
| --- | --- |
| `%LOWCASE(argument)` | 将参数中的大写字母转换为小写 |
| `%QLOWCASE(argument)` | 将参数中的大写字母转换为小写，并返回一个掩码特殊字符和助记操作符的结果 |
| `%LEFT(argument)` | 删除参数开头的空格 |
| `%TRIM(argument)` | 删除参数末尾的空格 |
| `%CMPRES(argument)` | 删除参数中的多个空格 |
| `%DATATYP(argument)` | 根据参数是否为整数返回 NUMERIC 或 CHAR |

你可能熟悉 SAS 函数如 `TRIM` 和 `LEFT`。SAS 提供的这些宏看起来像函数，但实际上是宏。这些宏的一个用处是，除了在程序中使用它们，你还可以查看它们的源代码。

## 示例

`lowcase` 的宏定义所示。注意此宏中的注释提供了关于使用该宏的信息。

```
%macro lowcase(string);
%**************************************;
%* 宏：LOWCASE
%* 用法：1) %lowcase(argument)
%* 说明：
%   此宏返回传递给它的参数，并将所有大写字母转换为小写。
%* 例：%let macvar=%lowcase(SAS Institute.);
%* 变量 macvar 的值为 "sas institute inc。"
% 注意：
%   虽然 %UPCASE 函数的参数可以包含逗号，但 %LOWCASE 的参数不能，除非加引号。
%   由于 %LOWCASE 是宏而不是函数，它会将逗号解释为参数的结束。
%**************************************;
%sysfunc(lowcase(%nrbquote(&string)))
%mend;
```





# MAUTOSOURCE 系统选项

| 通用形式，`MAUTOSOURCE` 系统选项 | `OPTIONS MAUTOSOURCE` \| `NOMAUTOSOURCE` |
| :--- | :--- |
| 以下是语法说明：`MAUTOSOURCE` 是默认设置，指定可以使用自动调用（autocall）功能。`NOMAUTOSOURCE` 指定不可用自动调用功能。 |

`SASAUTOS=` 系统选项控制宏处理程序在何处查找自动调用宏。

# SASAUTOS= 系统选项

| 通用形式，`SASAUTOS=` 系统选项 | `OPTIONS SASAUTOS=library-1;` \| `OPTIONS SASAUTOS=(library-1,...,library-n);` |
| :--- | :--- |
| 以下是语法说明：`library-1` 到 `library-n` 的值是对包含宏定义的源库的引用。要指定一个你可以可以

使用的源库，可以： |

*   使用 `fileref`（文件引用名）来引用其位置
*   指定库的 `pathname`（路径，用引号括起来）。

除非您的系统管理员更改了 `SASAUTOS=` 系统选项的默认值，否则它的值为 `fileref` `Sasautos`，且该 `fileref` 指向安装期间创建的默认自动调用库的位置。`Sasautos` `fileref` 可以引用多个连接在一起的位置。通常情况下，将您自己创建的任何自动调用库与 `SASAUTOS=` 系统选项值中的默认自动调用库合并是一个好主意。否则，新的自动调用库将替换 `SASAUTOS=` 值中的默认或现有库，自动调用功能将仅访问新的自动调用库。

## 示例

假设您想访问 `Prtlast` 宏，该宏存储在自动调用库 `C:\Mysasfiles` 中。同时您还想确保默认自动调用库（`fileref` `Sasautos` 指向的位置）仍然可自动调用功能使用。您可以提交以下代码：

```
options mautosource sasautos=('c:\mysasfiles',sasautos);
%prtlast
```

注意：`MAUTOLOCDISPLAY` 选项是一个布尔选项，它会在 SAS 日志中输出一条备注，指示编译自动调用宏时源代码的来源。该备注与使用 `MLOGIC` 选项时显示的信息类似。此选项的默认设置为 `NOMAUTOLOCDISPLAY`。当自动调用功能生效时，如果您调用了一个之前未编译过的宏，宏处理程序将自动

1.  在自动调用库（或如果在 `SASAUTOS=` 系统选项中识别出多个库，则逐一搜索每个自动调用库）中搜索与调用宏同名的成员
2.  如果找到成员，则将源语句引入当前 SAS 会话
3.  如果未找到成员，则输出错误信息
4.  顺序提交成员中的所有语句以编译宏
5.  将编译后的宏存储在临时目录 `Work.Sasmacr` 中
6.  调用该宏

如果宏在当前 SAS 会话期间已经编译过，则自动调用功能将不再自动调用库中搜索。在这种情况下，将执行会话编译的宏。

# 使用存储的编译宏

## 存储编译宏功能

请记住，当宏被编译时，默认存储在临时 SAS 目录 `Work.Sasmacr` 中。您也可以将编译后的宏存储在永久的 SAS 目录中。然后您可以使用存储编译宏功能来访问包含编译宏的永久 SAS 目录。使用存储编译宏有几个优点：

*   当进行宏调用时，SAS 不需要编译宏定义。
*   会话编译的宏和自动调用功能在同一会话中同样可用。
*   用户无法修改编译后的宏。

两个 SAS 系统选项影响存储的编译宏：`MSTORED` 和 `SASMSTORE=`。`MSTORED` 系统选项控制存储编译宏功能可用。

| 通用形式，`MSTORED` 系统选项 | `OPTIONS MSTORED` \| `NOMSTORED` |
| :--- | :--- |
| 以下是语法说明：`NOMSTORED` 是默认设置，指定存储编译宏功能不搜索编译后的宏。`MSTORED` 指定存储编译宏功能在 `SASMSTORE=` 选项引用的 SAS 库目录中搜索存储的编译宏。 |

`SASMSTORE=` 系统选项控制宏处理程序在何处查找存储的编译宏。

| 通用形式，`SASMSTORE=` 系统选项 | `OPTIONS SASMSTORE=libref;` |
| :--- | :--- |
| 以下是语法说明：`libref` 指定包含（或包含存储编译 SAS 宏目录的 SAS 库的 `libref`。`Work.Sasmacr` 是该目录。`MSTORED` 和 `SASMSTORE=` 选项可以在调用时或使用语句时设置。 |

## 创建存储的编译宏

要创建永久存储的宏，您必须执行以下操作：

1.  为存储宏的 SAS 库分配一个 `fileref`
2.  设置系统选项 `MSTORED` 和 `SASMSTORE=`
3.  在 `%MACRO` 语句中使用 `STORE` 选项

| 通用形式，带有 `STORE` 选项的宏定义 | `%MACRO macro-name <parameter list)> /STORE='description>';%MEND macro-name;` |
| :--- | :--- |
| 以下是语法说明：`description` 是目录中的可选文本。`macro-name` 是宏的名字。`parameter list` 是指定的一个或多个宏变量。 |

存储编译宏有几项限制：

*   `Sasmacr` 是可以存储编译宏的唯一目录。您可以在任何 SAS 库中创建它。
*   您无法跨操作系统复制存储的编译宏。您必须复制源程序并重新创建宏。
*   无法从编译宏重新创建源码。

## 使用 SOURCE 选项

将源程序与编译宏分开保存的替代方案是在 `%MACRO` 语句中使用 `SOURCE` 选项，将编译宏的源码与编译代码合并存储。`SOURCE` 选项要求设置 `STORE` 选项和 `MSTORED` 选项。下面的 `%MACRO` 语句显示了使用 `SOURCE` 选项的正确语法。

```
%macro macro-name<(parameter list)> /STORE SOURCE;
```

由 `SOURCE` 选项保存的源码从 `%MACRO` 关键字开始，到 `%MEND` 语句后的分号结束。提示：`SOURCE` 选项用于嵌套宏定义。

## 示例

假设您想在 SAS 库中编译形式存储 `Words` 宏。此示例了 `Words` 宏的定义。该宏接收一个字符串，将其分割，并创建一系列宏变量来存储每个单词。注意，定义中同时使用了 `STORE` 选项和 `SOURCE` 选项，这样 `Words` 就会以编译宏的形式永久存储，并与其源码一起存储，如下：

```
libname macrolib 'c:\storedlib';
options mstored sasmstore=macrolib;

%macro words(text,root=w,delim=%str( ))/store source;
   %local i word;
   %let i=1;
   %let word=%scan(&text,&i,&delim);
   %do %while (&word ne );
      %global &root&i;
      %let &root&i=&word;
      %let i=%eval(&i+1);
      %let word=%scan(&text,%i,&delim);
   %end;
   %global &root.num;
   %let &root.num=%eval(&i-1);
%mend words;
```




如果 `Macrolib` 库中不存在 `Sasmacr` 目录，它将被自动创建。你可以列出 `Macrolib.Sasmacr` 目录的内容以验证编译后的宏是否已创建，如下：

```
proc catalog cat=macrolib.sasmacr;
   contents;
   title "Stored Compiled Macros";
quit;
```

如果 `Macrolib.Sasmacr` 中没有存储其他编译后的宏，则是 `PROC CATALOG` 步骤的输出：![Stored Compiled Macros](img/m53-25-g1.png)

## 访问存储的编译宏

为了访问存储的编译宏，你必须执行以下操作：

1. 为包含存储宏的 `Sasmacr` 目录的 SAS 库分配一个 `libref`。
2. 设置系统选项 `MSTORED` 和 `SASMSTORE=libref`。
3. 调用该宏。

## 示例

以下程序调用了 `Words` 宏。假设 `Words` 宏已经在之前的 SAS 会话中被编译并存储。

```
libname macrolib 'c:\storedlib';
options mstored sasmstore=macrolib;

%words(This is a test)
%put Number of Words (wnum): &wnum;
%put Word Number 1 (w1): &w1;
%put Word Number 2 (w2): &w2;
%put Word Number 3 (w3): &w3;
%put Word Number 4 (w4): &w4;
```

以下是提交此代码时写入 SAS 日志的部分消息。

表 12.2 SAS 日志

```
9    libname macrolib 'c:\storedlib';
NOTE: Libref MACROLIB was successfully assigned as follows:
      Engine:        V9
      Physical Name: c:\storedlib
10       options mstored sasmstore=macrolib;
11
12       %words(This is a test)
13       %put Number of Words (wnum): &wnum;
Number of Words (wnum): 4
14       %put Word Number 1 (w1): &w1;
Word Number 1 (w1): This
15       %put Word Number 2 (w2): &w2;
Word Number 2 (w2): is
16       %put Word Number 3 (w3): &w3;
Word Number 3 (w3): a
17       %put Word Number 4 (w4): &w4;
Word Number 4 (w4): test
```

## 访问存储的宏代码

如果你使用 `%MACRO` 语句的 `SOURCE` 选项将宏源代码与存储的编译宏一起存储，你可以使用 `%COPY` 语句来访问存储的源码。

`%COPY` 语句的通用格式：`%COPY macro-name /SOURCE <other option(s)>;`

以下是对语法的解释：
* `macro-name` 要访问源码的宏名称。
* `SOURCE` 指定将宏的源代码复制到输出目标。如果没有指定输出目标，则源码将写入 SAS 日志。
* `other options` 包括以下选项：
    * `LIBRARY=` 指定包含存储的编译 SAS 宏目录的 SAS 库的 `libref`。如果未指定库，则使用 `SASMSTORE=` 选项指定的 `libref`。该 `libref` 不能为 `Work`。
    * `OUTFILE=` 指定 `%COPY` 语句的输出目标。该值可以是 `fileref` 或外部文件。

## 示例

假设你提交了以下程序创建一个名为 `Words` 的存储编译宏。

```
libname macrolib 'c:\storedlib';
options mstored sasmstore=macrolib;

%macro words(text,root=w,delim=%str( ))/store source;
   %local i word;
   %let i=1;
   %let word=%scan(&text,&i,&delim);
   %do %while (&word ne );
      %global &root&i;
      %let &root&i=$word;
      %let i=%eval(&i+1);
      %let word=%scan(&text,&i,&delim);
      %end;
   %global &root.num;
   %let &root.num=%eval(&i-1);
%mend words;
```

`%COPY` 语句将 `Words` 宏的源码写入 SAS 日志。这是一个示例：

```
%copy words/source;
```

下面的 SAS 日志显示了 `Words` 宏的源码。

表 12.3 SAS 日志

```
17     %copy words/source;
%macro words(text,root=w,delim=%str( ))/store source;

        %local i word;
        %let i=1;
        %let word=%scan(&text,&i,&delim);
        %do %while (&word ne );
           %global &root&i;
           %let &root&i=$word;
           %let i=%eval(&i+1);
           %let word=%scan(&text,&i,&delim);
        %end;
        %global &root.num;
        %let &root.num=%eval(&i-1);
%mend words;
```

存储编译宏功能可以与 `Autocall Facility` 以及会话编译宏结合使用。当你提交如 `Words` 这样的宏调用时，它会搜索：

1. `Work` 库中的 `Sasmacr` 目录。
2. `SASMSTORE=` 选项指定的 `libref` 中的 `Sasmacr` 目录。
3. `SASAUTO=` 选项指定的 `autocall libraries` 中的 `Sasmacr` 目录。





*   你可以通过四种方式为程序提供宏支持：作为会话编译宏、使用 `%INCLUDE` 语句、通过自动调用（autocall）功能，或者作为存储的已编译宏。

*   如果你使用自动调用功能，则必须指定 `MAUTOSOURCE` 和 `SASAUTOS=` 系统选项。

*   如果你使用存储已编译宏功能，则必须指定 `MSTORED` 和 `SASMSTORE=` 系统选项。

*   宏编译发生的时间取决于你使用哪种方法来访问宏。

# 测验

为每个问题选择一个最佳答案。完成测验后，请使用附录中的答案检查你的答案。

1.  `%INCLUDE` 语句
    1.  可以将外部文件的内容插入程序中。
    2.  当该文件的内容插入插入程序并提交时，可以导致存储在外部文件中的宏定义被编译。
    3.  可以使用 `SOURCE2` 选项指定，将插入到程序的外部文件内容写入 SAS 日志中。
    4.  以上所有。

2.  如果你在 SAS 目录的 `SOURCE` 条目中存储宏定义
    1.  可以使用 `FILENAME` 和 `%INCLUDE` 语句提交宏定义进行编译。
    2.  你可以使用 `PROC CATALOG` 语句来编译宏。
    3.  `SOURCE` 条目在会话结束时被删除。
    4.  在程序中调用宏之前不需要编译该宏。

3.  下列哪个程序正确设置了相应的系统选项并调用了宏 `Prtlast`？假设 `Prtlast` 以文本文件形式存储在自动调用库中，且在当前 SAS 会话期间尚未被编译。
    1.  
    ```
    libname mylib 'c:\mylib';
    filename macsrc 'mylib.macsrc';
    options mautosource sasautos=(macsrc, sasautos);
    %prtlast
    ```
    2.  
    ```
    libname mylib 'c:\mylib';
    filename macsrc catalog 'mylib.macsrc';
    %prtlast
    ```
    3.  
    ```
    filename mylib 'c:\mylib';
    options mautosource sasautos=(sasautos,mylib);
    %prtlast
    ```
    4.  
    ```
    libname mylib 'c:\mylib';
    options mautosource sasautos=mylib;
    %prtlast
    ```

4.  如果你使用存储已编译宏功能，
    1.  宏处理器不会在每次使用时都编译宏。
    2.  存储已编译宏功能能够访问的已编译宏只有存储在 `Sasmacr` 目录中的宏。
    3.  你需要指定 `MSTORED` 和 `SASMSTORE=` 系统选项。
    4.  以上所有。

5.  下列哪项操作正确创建了持久化存储的已编译宏？
    1.  
    ```
    libname macrolib 'c:\mylib';
    options sasmstore;
    %macro prtlast; / store
       proc print data=&syslast (obs=5);
          title "Listing of &syslast data set";
       run;
    %mend;
    ```
    2.  
    ```
    libname macrolib 'c:\mylib';
    options mstored sasmstore=macrolib;
    %macro prtlast / store;
       proc print data=&syslast (obs=5);
          title "Listing of &syslast data set";
       run;
    %mend;
    ```
    3.  
    ```
    libname macrolib 'c:\mylib';
    options mstored sasmstore=macrolib;
    %macro prtlast;
       proc print data=&syslast (obs=5);
          title "Listing of &syslast data set";
       run;
    %mend;
    ```
    4.  
    ```
    libname macrolib 'c:\mylib';
    %macro prtlast / store;
       proc print data=&syslast (obs=5);
          title "Listing of &syslast data set";
       run;
    %mend;
    ```

6.  当提交以下代码时，会发生什么？
    ```
    %macro prtlast;
       proc print data=&syslast (obs=5);
          title "Listing of &syslast data set";
       run;
    %mend;
    ```
    1.  一个名为 `Prtlast` 的会话编译宏被存储在 `Work.Sasmacr` 中。
    2.  一个名为 `Prtlast` 的宏存储在自动调用库中。
    3.  `Prtlast` 宏作为存储已编译宏存储。
    4.  `Prtlast` 宏作为持久 SAS 目录中的 `SOURCE` 条目存储。

7.  你为什么想将宏存储在外部文件中？
    1.  你可以轻松地与其他共享你的宏。
    2.  你可以使用任何文本编辑器编辑你的宏。
    3.  你的宏可以在后续 SAS 会话中可用。
    4.  以上所有。

8.  以下 `PROC CATALOG` 步骤做了什么？
    ```
    proc catalog cat=mylib.sasmacr;
       contents;
    quit;
    ```
    1.  将 `Sasmacr` 目录的内容复制到临时集。
    2.  列出 `Sasmacr` 目录的内容。
    3.  将内容复制到 SAS 目录。
    4.  以上都不是。

9.  关于存储宏，下列哪项是不正确的？
    1.  因为这些存储宏是经过编译的，你应该将宏定义保存在不同的位置。
    2.  存储已编译功能编译并将宏保存在指定的持久化目录中。
    3.  使用存储已编译功能不需要指定任何系统选项。
    4.  你无法移动宏。

10. 下列哪项是不正确的？
    1.  自动调用功能将已编译宏存储在外部文件中。
    2.  自动调用库可以连接。
    3.  自动调用功能的一个缺点是，当你第一次调用宏时，宏处理器必须对其进行编译。
    4.  自动调用功能可以与存储已编译功能结合使用。

# 第 13 章：创建索引

*   概述
*   使用索引
*   在 DATA 步中创建索引
*   使用 PROC DATASETS 管理索引
*   使用 PROC SQL 管理索引
*   索引的文档与维护
*   总结
*   测验

## 概述

本章讨论直接访问。例如，你可以根据数据中的值选择子集。你可以通过使用 `INDEX=` 数据集选项创建索引来实现此操作。`WHERE` 子句可以使用该索引。通过直接访问所需的观测值，而不是顺序访问所有观测值，你的程序运行得更快。

### 使用索引

## 概述

索引可以帮助你快速定位想要读取的一个多个观测值。索引根据一个或多个键变量的值对 SAS 数据集中的观测值提供直接访问。索引的应用包括

*   为 `WHERE` 处理提供更快的观测子集访问
*   执行表查找操作
*   连接观测值


如果没有索引，SAS 将按照观测值在数据集中存储的顺序进行顺序访问。例如，为了访问下方示例 SAS 数据集中变量 `Name` 值为 `Smith` 的观测值，SAS 将从第一条观测值开始读取，逐一读取每一条，直到找到满足条件的观测值为止。![示例 SAS 数据集](img/m54-19-g2.png)当对 SAS 数据集建立索引时，SAS 会创建一个索引文件，该文件按特定变量或多个变量的**升序**存储值，并包含有关这些值在数据文件中位置的信息。也就是说，索引由“值/标识符”键值对组成，这允许你通过值来定位观测值。例如，如果你对下方的示例 SAS 数据集基于变量 `Name` 创建了一个索引，SAS 将直接使用该索引找到 `Name` 值为 `Smith` 的观测值，而无需读取之前所有的观测值。![示例 SAS 数据集](img/m54-19-g1.png)

## 索引类型

你可以创建两种类型的索引：

*   简单索引（simple index）
*   复合索引（composite index）

简单索引由一个键变量的值组成，该变量可以是字符型或数值型。当你创建简单索引时，SAS 会用该键变量命名索引。复合索引由多个键变量的值组成，这些变量可以是字符型、数值型或它们的组合。这些键变量的值被拼接成一个单一值。例如，如果在键变量 `Lastname` 和 `Firstname` 上建立索引，则该索引的值将包括 `Lastname` 的值，后跟 `Firstname` 的值。当你创建复合索引时，必须指定一个唯一的索引名称，该名称不能与数据集中任何现有变量或索引重名。通常，复合索引中仅第一个变量会被使用。在示例中，你可以将上文指定的复合索引（`Lastname` 加上 `Firstname`）用于仅使用 `Lastname` 的 `WHERE` 表达式。例如，表达式 `where Lastname='Smith'` 使用了该复合索引，因为 `Lastname` 是该索引中的第一个变量。也就是说，`Lastname` 的值是索引中列出的值的第一部分。

# 在 DATA 步中创建索引

## 概述

要在创建数据集的同时创建索引，请在 `DATA` 语句中使用 `INDEX=` 数据集选项。

| 通用格式，带有 `INDEX=` 选项的 `DATA` 语句：`DATA SAS-data-file-name (INDEX=(index-specification-1<UNIQUE><...index-specification-n></UNIQUE>))` | 以下是语法的解释：`SAS-data-file-name` 是有效的 SAS 数据集名称。简单索引的 `index-specification` 是键变量的名称。复合索引的 `index-specification` 为 `(index-name=(variable-1...variable-n))`。`UNIQUE` 指定每个观测值的键变量值必须是唯一的。 |

你你可以在单个 SAS 数据集上创建多个索引。但是，请记住，创建和存储索引会消耗系统资源。因此，你应该只对经常用于选择观测值的变量创建索引。`UNIQUE` 选项保证了键变量或复合变量组的值对于数据集中的每条观测值都保持唯一。在现有数据集中，如果尝试对其创建唯一索引的变量或多个变量具有重复值，则索引将无法创建。同样，如果更新尝试向该数据集添加一个具有索引变量重复值的观测值，则该更新将被拒绝。

## 示例

以下示例在 `Simple` 数据集上创建了一个简单索引。索引命名为 `Division`，它包含 `Division` 变量的值。

```
data simple (index=(division));
   set sasuser.empdata;
run;
```

以下示例在 `Simple2` 数据集上创建了两个简单索引。第一个索引名为 `Division`，包含 `Division` 变量的值。第二个索引名为 `EmpID`，包含 `EmpID` 变量的唯一值。

```
data simple2 (index=(division empid/unique));
   set sasuser.empdata;
run;
```

以下示例在 `Composite` 数据集上创建了一个复合索引。索引名为 `Empdiv`，它包含 `Division` 变量和 `EmpID` 变量的拼接值。

```
data composite (index=(Empdiv=(division empid)));
   set sasuser.empdata;
run;
```

当你创建或使用索引时，可能想验证它是否已正确创建或使用。要在 SAS 日志中显示有关索引创建或使用的信息，请将系统选项 `MSGLEVEL=` 设置为 `I`。

| 通用格式，`MSGLEVEL=` 系统选项：`OPTIONS MSGLEVEL= N|I` | 以下是语法的解释：`N` 仅打印备注（notes）、警告和错误消息。这是默认设置。`I` 会打印与索引使用、合并处理和排序工具相关的附加备注或 `INFO` 消息，以及标准的备注、警告和错误消息。 |

## 示例

以下代码将 `MSGLEVEL=` 系统选项设置为 `I`，并创建带有两个索引的 `Sasuser.Sale2000` 数据集：

```
options msglevel=i;
data sasuser.sale2000(index=(origin
     flightdate=(flightid date)/unique));
   infile sale2000 dsd;
   input FlightID $ RouteID $ Origin $
         Dest $ Cap1st CapBusiness
         CapEcon CapTotal CapCargo
         Date Psgr1st PsgrBusiness
         PsgrEcon Rev1st RevBusiness
         RevEcon SaleMon $ CargoWgt
         RevEcon Sale;
   format date.;
run;
```

提交上述程序时，写入 SAS 日志的这些如下。

表 13.1 SAS 日志

|  

```
NOTE: The infile SALE000 is:
      File Name=C:\My SAS Files\9.0\sale000.dat,
      RECFM=V,LRECL=256

NOTE: 153 records were read from the infile sale000.
      The minimum record length was 82.
      The maximum record length was 100.
NOTE: The data set SASUSER.SALE2000 has 153 observations
      and 19 variables.
NOTE: Composite index flightdate has been defined.
NOTE: Simple index origin has been defined.
NOTE: DATA statement used (Total process time):
      real time           1.08 seconds
```

## 判断 SAS 是否使用了索引

SAS 并不总是能够或高效地使用索引来访问特定观测值。在以下情况下不会使用索引：

*   在 `DATA` 步中使用过滤 `IF` 语句
*   特定的 `WHERE` 表达式
*   如果 SAS 认为顺序读取数据更高效

## 示例

你可以使用 `MSGLEVEL=` 选项来判断是否使用了索引。以下 SAS 日志显示了指示是否使用的 `INFO` 消息示例。

表 13.2 SAS 日志

|  

```
options msglevel=i;

proc print data=sasuser.revenue;
     where flightid ne 'IA1200';
INFO: Index FlightID not used. Increasing bufno to 3 may help.
```



表 13.3 SAS 日志

|  

```
options msglevel=i;

data somflights;
     set sasuser.revenue;
     where flightid > 'IA1200';
INFO: Index FlightID selected for WHERE clause optimization.
```




## 使用 `PROC DATASETS` 创建和删除索引的通用形式：

```sas
PROC DATASETS LIBRARY= libref <NOLIST>;
MODIFY SAS-data-set-name;
INDEX DELETE index-name;
INDEX CREATE index-specification;
QUIT;
```

以下是语法的解释：
- `libref`:指向包含 `SAS-data-set-name` 的 SAS 库。
- `NOLIST`: 选项抑制在 SAS 日志和 ODS 输出中打印 SAS 文件的目录。
- `index-name`:要删除的现有索引的名称。
- `index-specification`:对于简单索引，格式为键变量的名称。
- `index-specification`:对于复合索引，格式为 `index-name=(variable-1...variable-n)`。

如果要创建的索引已经存在，则无法使用 `PROC DATASETS` 中的 `INDEX CREATE` 语句。在这种情况下，你必须删除同名的现有索引，然后创建新索引。

**提示**：`PROC DATASETS` 按照顺序执行语句。因此，如果你在同一个步骤中删除并创建索引，应该先删除旧索引，这样新创建的索引就可以重用已删除索引占据的空间。

## 示例

下面的示例在 `Sasuser.Sale2000` 数据集上创建一个名为 `Origin` 的索引。`Origin` 是一个基于键变量 `Origin` 的简单索引。

```sas
proc datasets library=sasuser nolist;
   modify sale2000;
   index create origin;
quit;
```

下面的示例首先从 `Sasuser.Sale2000` 数据集中删除 `Origin` 索引，然后在 `Sasuser.Sale2000` 数据集上创建两个新索引。`FlightID` 是一个基于键变量 `FlightID` 值的简单索引。`Fromto` 是一个基于键变量 `Origin` 和 `Dest` 拼接值的复合索引。

```sas
proc datasets library=sasuser nolist;
   modify sale2000;
   index delete origin;
   index create flightid;
   index create Fromto=(origin dest);
quit;
```

# 使用 PROC SQL 管理索引

## 概述

你也可以在 `PROC SQL` 步骤中从现有数据集中创建或删除索引。`CREATE INDEX` 语句允许你对数据集创建索引。`DROP INDEX` 语句允许你从数据集中删除删除索引。

## 使用 `PROC SQL` 创建和删除索引的通用形式：

```sas
PROC SQL;
CREATE <UNIQUE > INDEX index-name ON table-name(column-name-1<...,column-name-n>);
DROP INDEX index-name FROM table-name;
QUIT;
```

以下是语法的解释：
- `index-name`: 如果索引仅基于一列的值，则 `index-name` 与 `column-name-1`相同。
- `index-name`: 如果索引基于多个列，则 `index-name` 与任何 `column-name` 相同。
- `table-name`: `index-name` 关联的数据集的名称。

## 示例

下面的示例在 `Sasuser.Sale2000` 数据集上创建一个名为 `Origin` 的简单索引。该索引基于 `Origin` 列的值。

```sas
proc sql;
   create index origin on sasuser.sale2000(origin);
quit;
```

下面的示例从 `Sasuser.Sale2000` 数据集中删除 `Origin` 索引，并创建一个名为 `Tofrom` 的新索引，该索引基于 `Origin` 和 `Dest` 列值的拼接：

```sas
proc sql;
   drop index origin from sasuser.sale2000;
   create index Tofrom
      on sasuser.sale2000(origin, dest);
quit;
```

# 索引的文档记录与维护

## 概述

索引存储在与被索引的数据集相同的 SAS 库中，但存储在与数据集不同的 SAS 文件中。索引文件的成员类型为 `INDEX`。每个数据集只有一个索引文件；数据集的所有索引都存储在同一个文件中。

下图显示了在 Windows 操作系统环境下 SAS 数据集文件和 SAS 索引文件的关系。请注意，索引文件的名称与其关联的数据集相同，但它们具有不同的文件扩展名。此外，请注意每个索引文件可以包含一个或多个索引，不同的索引文件可以包含名称相同的索引。

![SAS 数据集文件和 SAS 索引文件](img/m54-30-g1.png)

**注意**：索引文件存储在与其关联的数据集相同的位置。然而，请记住以下点：
- 索引文件不会出现在 SAS Explorer 窗口中。
- 在 z/OS 操作系统文件列表中，索引文件不会作为单独的文件显示。

有时，你可能想要查看数据集存在的索引列表。你可能还想查看索引的信息，例如它们是否是唯一的，以及它们使用了哪些键变量。让我们考虑记录索引的一些方法。

索引信息存储在数据集的描述部分（descriptor portion）。你可以使用使用 `CONTENTS` 过程或 `PROC DATASETS` 中的 `CONTENTS` 语句来列出描述部分的信息。`CONTENTS` 过程或 `PROC DATASETS` 中 `CONTENTS` 语句的输出包含关于数据集的以下信息：
- 概要信息
- 引擎相关信息
- 变量属性列表
- 完整性约束列表
- 索引列表

## `PROC CONTENTS` 的通用形式：

```sas
PROC CONTENTS DATA=<libref>;
RUN;
```

## 使用 `PROC DATASETS` 的 `CONTENTS` 语句的通用形式：

```sas
PROC DATASETS LIBRARY= libref <NOLIST>;
CONTENTS <data-set-name>;
QUIT;
```

以下是语法的解释：
- `data-set-name`: 要列出信息的数据集。
- `NOLIST`: 选项抑制在 SAS 日志和 ODS 输出中打印 SAS 文件的目录。

**注意**：如果你使用了 `DATA=` 选项，则不需要指定 `libref`。同样，如果你在 `DATA=` 选项中指定了 `libref`，则不需要使用 `LIBRARY=` 选项。

## 示例

下面的示例打印 `Sasuser.Sale2000` 数据集的信息。请注意，库是在 `PROC DATASETS` 的 `LIBRARY=` 选项中指定的。

```sas
proc datasets library=sasuser nolist;
   contents sale2000;
quit;
```

下面的示例也打印 `Sasuser.Sale2000` 数据集的信息。请注意，库是在 `CONTENTS` 语句中指定的。

```sas
proc datasets nolist;
   contents data=sasuser.sale2000;
quit;
```

下面的示例打印 `Sasuser.Sale2000` 数据集：

```sas
proc contents data=sasuser.sale2000;
run;
```

这些程序的 `PROC DATASETS` 和 `PROC CONTENTS` 输出是相同的。每组输出的最后部分信息是 `Sasuser.Sale2000` 创建的索引列表，如下：

![Sasuser.Sale2000](img/m54-31-g1.png)

你也可以使用这些方法之一列出整个库而不是单个数据集。要使用 `PROC CONTENTS` 或 `PROC DATASETS` 中的 `CONTENTS` 语句列出库中的所有文件，需要在 `DATA=` 选项中指定关键字 `_ALL_`。

## 示例

下面的示例打印 `Work` 库所有文件的信息：

```sas
proc contents data=work._all_;
run;
```

下面的示例也打印 `Work` 库所有文件的信息：

```sas
proc datasets library=work nolist;
   contents data=_all_;
quit;
```

索引存储在单独的文件中。对数据集进行维护操作时，可能会对索引文件产生影响。如果你更改数据集中的变量或值，可能会对特定索引中的值/标识对产生影响。

| 任务 | 影响 |
| --- | --- |
| 向数据集添加观测值或观测值。 | 值/标识对将被添加到索引或多个索引中。 |





| 从数据集中删除一个或多个观测值。 | 从索引或多个索引中删除值/标识符对。 |
| 在数据集中更新一个或多个观测值。 | 在索引或多个索引中更新值/标识符对。 |
| 删除数据集。 | 索引文件被删除。 |
| 使用 `DATA` 步重建数据集。 | 索引文件被删除。 |
| 在 `PROC SORT` 中使用 `FORCE` 对数据进行原地排序。 | 索引文件被删除。 |

让我们考虑你可能对数据集上执行的一些其他常见任务，以及 SAS 结果结果对索引文件执行的操作。

## 复制数据集

你可能希望将带有索引的数据集复制到新位置。你可以在 `PROC DATASETS` 步中使用 `COPY` 语句来复制数据集。当你使用 `COPY` 语句复制具有关联索引的数据集时，SAS 会为新的数据文件自动创建一个新的索引文件。

带有 `COPY` 语句的 `PROC DATASETS` 一般形式：
```
PROC DATASETS LIBRARY=old-libref <NOLIST>;
COPY OUT=new-libref;
SELECT SAS-data-set-name;
QUIT;
```
以下是语法的解释：
- `old-libref`:指定复制数据集的库名。
- `new-libref`:指定数据集复制到的库名。
- `SAS-data-set-name`:指定被复制的数据集名称。

你也可以使用 `COPY` 过程将数据集复制到新位置。通常，`PROC COPY` 的功能与 `DATASETS` 过程中的 `COPY` 语句相同。当你使用 `PROC COPY` 复制具有关联索引的数据集时，SAS 会为新的数据文件自动创建一个新的索引文件。如果你在 `COPY` 过程中使用 `MOVE` 选项，索引文件将从原始位置删除并在位置重建。

`PROC COPY` 步的一般形式：
```
PROC COPY OUT=new-libref IN=old-libref<MOVE>;
SELECT SAS-data-set-name(s);
RUN;
QUIT;
```
以下是语法的解释：
- `old-libref`:指定复制数据集的库名。
- `new-libref`:指定数据集复制到的库名。
- `SAS-data-set-name`:指定被复制的一个或多个数据集名称。

## 示例

以下程序产生相同的结果。两个程序都从 `Sasuser` 库复制 `Sale2000` 数据集并将其放置在 `Work` 库中。同样，这两个程序都会为 `Work.Sale2000` 创建一个新的索引文件，该文件包含了 `Sasuser.Sale2000` 中存在的所有索引。

```
proc datasets library=sasuser nolist;
   copy out=work;
   select sale2000;
quit;

proc copy out=work in=sasuser;
   select sale2000;
run;
```

注意：如果你在 SAS Explorer 或 SAS Enterprise Guide 中复制并粘贴数据集，SAS 会为新的数据文件自动创建一个新的索引文件。

## 重命名数据集

另一个常见任务是重命名带有索引的数据集。为了保留索引，你可以使用 `PROC DATASETS` 中的 `CHANGE` 语句来重命名数据集。索引文件也会自动重命名。

带有 `CHANGE` 语句的 `PROC DATASETS` 一般形式：
```
PROC DATASETS LIBRARY=libref <NOLIST>;
CHANGE old-data-set-name = new-data-set-name;
QUIT;
```
以下是语法的解释：
- `libref`:指定存储数据集的 SAS 库。
- `old-data-set-name`:数据集的当前名称。
- `new-data-set-name`:数据集的新名称。

## 示例

以下示例将 `Revenue` 数据集从 `Sasuser` 复制到 `Work`，并将 `Work.Revenue` 数据集重命名为 `Work.Income`。与 `Work.Revenue` 关联的索引文件也会重命名为 `Work.Income`。

```
proc copy out=work in=sasuser;
   select revenue;
run;

proc datasets library=work nolist;
   change revenue=income;
quit;
```

## 重命名变量

你已经看到如何使用 `PROC DATASETS` 重命名索引数据集。同样，你可能也想重命名索引数据集中的一个或多个变量。为了保留与数据集关联的任何索引，你可以使用 `DATASETS` 过程中的 `RENAME` 语句来重命名变量。

带有 `RENAME` 语句的 `PROC DATASETS` 一般形式：
```
PROC DATASETS LIBRARY=libref <NOLIST>;
MODIFY SAS-data-set-name;
RENAME old-var-name-1 = new-var-name-1<...old-var-name-n = new-var-name-n>;
QUIT;
```
以下是语法的解释：
- `libref`:指定存储数据集的 SAS 库。
- `SAS-data-set-name`:包含要重命名变量的数据集名称。
- `old-var-name`:原始变量名。
- `new-var-name`:分配给变量的新名称。

当你使用 `RENAME` 语句重命名具有简单索引的变量时，该索引也会被重命名。如果你重命的变量用于复合索引，复合索引将自动引用新的变量名。然而，如果你尝试将变量重命名为已用于复合索引的名称，将收到错误。

## 示例

以下示例将 `Work.Income` 数据集的 `FlightID` 变量重命名为 `FlightNum`。如果存在简单索引，它将被重命名。

```
proc datasets library=work nolist;
   modify income;
```

## 总结

### 使用索引

索引是与数据集关联的 SAS 文件，包含数据关键变量的位置和值。索引允许 SAS 直接访问观测值，而无需顺序读取所有观测值。索引可以是简单的，也可以是复合的。

### 在 DATA 步中创建索引

你可以在创建数据集的同时通过 `INDEX=` 选项创建索引。如果数据集中任何关键变量没有重复值，简单索引和复合索引都可以唯一的。你可以在一个数据集上创建多个索引。你可以使用 `MSGLEVEL=` 系统选项向 SAS 日志写入有关索引的消息。索引可以提高效率，但在某些情况下索引不会提高效率，因此不应使用。

### 使用 PROC DATASETS 和 SQL 管理索引

你可以使用 `PROC DATASETS` 中的 `INDEX CREATE` 语句或 `INDEX DELETE` 语句从现有数据创建或删除索引。使用 `PROC DATASETS` 管理索引比在 `DATA` 步中重建数据集并更新索引消耗的系统资源更少。如果你要在同一个 `PROC DATASETS` 步中删除并创建索引，你应该先删除旧索引再创建索引，以便 SAS 重用已删除索引的空间。你也可以使用 `PROC SQL` 创建或删除索引。

### 索引的文档编制和维护

为特定数据集创建的所有索引都存储在与数据集相同的 SAS 库中。你可以使用 `PROC CONTENTS` 打印数据集存在的所有索引列表，以及数据集的其他信息。`PROC DATASETS` 步的 `CONTENTS` 语句可以生成相同的索引列表和数据集信息。你对数据集执行的许多维护任务都会影响与其关联的索引文件。当你使用 `PROC DATASETS` 中的 `COPY` 语句复制数据集时，索引文件将为你重建。当你使用 `PROC DATASETS` 重命名数据集或重命名变量时，索引文件会自动更新以反映此更改。





```
options msglevel=i;
data sasuser.sale2000(index=(origin FlightDate=
                      (flightid date)/unique));
   infile 'sale2000.dat';
   input FlightID $7\. RouteID $7\. Origin $3.
         Dest $3\. Cap1st 8\. CapBusiness 8.
         CapEcon 8\. CapTotal 8\. CapCargo 8.
         Date date9\. Psgr1st 8./
         PsgrBusiness 8\. PsgrEcon 8.
         Rev1st dollar15.2
         RevBusiness dollar15.2
         RevEcon dollar15.2 SaleMon $7.
         CargoWgt 8./ RevCargo dollar15.2;
run;
```

### 使用 PROC DATASETS 管理索引

```
proc datasets library=sasuser nolist;
   modify sale2000;
   index delete origin;
   index create flightid;
   index create Tofrom=(origin dest);
quit;
```

### 使用 PROC SQL 管理索引

```sas
proc sql;
   create index Tofrom on
          sasuser.sale2000(origin, dest);
   drop index origin from sasuser.sale2000;
quit;
```

你也可以使用 `Dictionary.Indexes` 表来生成报告

```
proc sql;
   select *
        from dictionary.indexes
          where libname='SASUSER' and
memname='SALE2000';
   quit;
```

## 注意事项

- 索引可以使 SAS 更高效地访问数据集中的特定观测值。然而，由于索引会使用系统资源，因此只应在经常用于选择观测值的变量上创建索引。
- 索引与数据集关联，但存储为单独的文件。你可以使用 `PROC DATASETS` 或 `PROC CONTENTS` 生成关于数据集索引的报告。你也可以在 SAS Explorer 资源管理器中右键点击数据集并选择“查看列”（view columns）来查看数据集索引的列表。你应该在对数据集执行维护任务后查看此信息，以确保索引文件已得到维护。

# 测验

请为每个问题选择最佳答案。完成测验后，请使用附录中的答案对照检查你的答案。

1. 关于索引的哪种描述是正确的？
    1. 它是一个与数据集关联的可选文件。
    2. 它允许根据一个或多个键变量的值，直接访问数据集的特定观测值。
    3. 它可以被分类为简单索引或复合索引，其中任一种都可以由唯一值组成。
    4. 以上都是。

2. 下列哪项正确地从 `Sasuser.Revenue` 数据集创建了一个名为 `Flights` 的数据集，创建了一个基于 `Origin` 和 `Dest` 值的名为 `Fromto` 的复合索引，并向 SAS 日志打印有关索引的提示消息？
    1. ```sas
        options msglevel=i;
        data flights index=(Fromto=origin dest);
           set sasuser.revenue;
        run;
        ```
    2. ```sas
        options msglevel=n;
        data flights (index=(Fromto=origin dest));
           set sasuser.revenue;
        run;
        ```
    3. ```sas
        options msglevel=i;
        data flights (index=(Fromto=(origin dest)));
           set sasuser.revenue;
        run;
        ```
    4. ```sas
        options msglevel=n;
        data flights (index=Fromto);
           set sasuser.revenue;
        run;
        ```

3. 下列哪项是正确的？
    1. 当你向数据集添加观测值时，索引或多个索引会自动更新添加额外的值/标识符对。
    2. 当你重命名作为简单索引键变量的变量时，必须重新创建索引。
    3. 当你删除数据集时，索引文件将一直保留，直到你也删除它。
    4. 当使用 `COPY` 语句复制数据集时，必须在另一个步骤中复制索引文件。

4. 要在现有数据集上创建索引，你使用以下哪项？
    1. `PROC DATASETS`
    2. `PROC SQL`
    3. 使用带有 `INDEX=` 选项的 `DATA` 步骤重建数据集
    4. 以上任何一项

5. 下列哪项正确地在 `Revenue` 数据集上创建一个名为 `Origin` 的简单索引？
    1. ```sas
        proc sql;
           create index origin on revenue(origin);
        quit;
        ```
    2. ```sas
        proc sql;
           modify revenue;
           index=origin;
        quit;
        ```
    3. ```sas
        proc sql data=revenue;
           create index origin;
        quit;
        ```
    4. ```sas
        proc sql;
           index=origin on revenue;
        quit;
        ```

6. 要查看与数据集关联的索引列表，你使用以下哪项？
    1. `PROC COPY` 或 `PROC DATASETS` 中的 `COPY` 语句
    2. `PROC CONTENTS` 或 `PROC DATASETS` 中的 `CONTENTS` 语句
    3. `MSGLEVEL=` 系统选项和 `PROC PRINT` 步骤
    4. 以上任何一项

7. 假设 `Sasuser.Revenue` 数据集有一个名为 `FlightID` 的简单索引。下列哪些程序使用了索引？
    1. ```sas
        proc print data=sasuser.revenue;
           where index;
        ```
    2. ```sas
        data flights;
           set sasuser.revenue;
           where index;
        run;
        ```
    3. ```sas
        data flights;
           set sasuser.revenue;
           if index;
        run;
        ```
    4. ```sas
        proc print data=sasuser.revenue;
           where origin='';
        ```

# 第 14 章：垂直合并数据

## 概述
## 引言
垂直合并数据指的是拼接或交错数据的过程。在某些情况下，数据可能位于数据集中；在其他情况下，数据可能存储在原始文件中。在本章中，你将学习如何使用 `FILENAME` 和 `INFILE` 语句通过拼接原始文件来创建数据集。你还将学习如何使用 `PROC APPEND` 合并数据集。

## 使用 FILENAME 语句
## 概述
你已经知道可以使用 `FILENAME` 语句将文件引用（fileref）与单个原始文件关联。你也可以使用 `FILENAME` 语句通过将单个文件引用分配给要合并的原始文件来拼接原始文件。

`FILENAME` 一般形式：`FILENAME fileref ('external-file1' 'external-file2' ...'external-filen');` 语法解释：`fileref` 是任何不超过 8 个字符的 SAS 名称。`external-file` 是外部文件的物理名称。物理名称是操作系统识别的名称。

注意：所有文件规范都必须包含在括号内。当在 `INFILE` 语句中指定文件引用时，所引用的每个原始文件都可以使用 `INPUT` 语句顺序读取到数据。提示：如果你不熟悉原始文件的内容和结构，可以使用 `PROC FIST` 查看它们。

## 示例
在下面的程序中，`FILENAME` 语句创建了文件引用 `Qtr1`，它引用了原始文件 `Month1.dat`、`Month2.dat` 和 `Month3.dat`。这些文件存储在 Windows 操作系统的 `C:\Sasuser` 目录下。在 `DATA` 步骤中，`INFILE` 语句标识文件引用，`INPUT` 语句描述数据，就像 `Qtr1` 引用了单个原始文件一样。

```sas
filename qtr1 ('c:\sasuser\month1.dat''c:\sasuser\month2.dat'
               'c:\sasuser\month3.dat');
data work.firstqtr;
   infile qtr1;
   input Flight $ Origin $ Dest
         Date : date9\. RevCargo : comma15.;
run;
```

表 14.1 原始文件 Month1.dat（前五记录）

|  





```
----+----10---+----20---+----30---+----40 
IA10200 SYD HKG 01JAN2000 $191,187.00 
IA10201 SYD HKG 01JAN2000 $169,653.00 
IA10300 SYD CBR 01JAN2000 $850.00 
IA10301 SYD CBR 01JAN2000 $970.00 
IA10302 SYD CBR 01JAN2000 $1,030.00
```

表 14.2 原始数据文件 `Month2.dat`（前五记录）

```
----+----10---+----20---+----30---+----40 
IA10200 SYD HKG 01FEB2000 $177,801.00 
IA10201 SYD HKG 01FEB2000 $174,891.00 
IA10300 SYD CBR 01FEB2000 $1,070.00 
IA10301 SYD CBR 01FEB2000 $1,310.00 
IA10302 SYD CBR 01FEB2000 $850.00
```

表 14.3 原始数据文件 `Month3.dat`（前五记录）

```
----+----10---+----20---+----30---+----40 
IA10200 SYD HKG 01MAR2000 $181,293.00 
IA10201 SYD HKG 01MAR2000 $173,727.00 
IA10300 SYD CBR 01MAR2000 $1,150.00 
IA10301 SYD CBR 01MAR2000 $910.00 
IA10302 SYD CBR 01MAR2000 $1,170.00 
```

SAS 日志显示，`Qtr1` 引用的原始数据文件已顺序读取到 SAS 数据集 `Work.FirstQtr`。注意：三个原始数据文件的读取计数均为 50 条记录。输出 SAS 数据集的写入计数为 150 个观测值。

表 14.4 SAS 日志

```
9    filename qtr1 ('c:\sasuser\month1.dat''c:\sasuser\month2.dat'
10                  'c:\sasuser\month3.dat');

11   data work.firstqtr;
12      infile qtr1;
13      input Flight $ Origin $ Dest $
14      Date : date9\. RevCargo : comma15.;
15   run;

NOTE: The infile QTR1 is:
      File Name=c:\sasuser\month1.dat,
      File List=('c:\sasuser\month1.dat' 'c:\sasuser\month2.dat' 
                 'c:\sasuser\month3.dat'),
      RECFM=V,LRECL=256

NOTE: The infile QTR1 is:
      File Name=c:\sasuser\month2.dat,
      File List=('c:\sasuser\month1.dat' 'c:\sasuser\month2.dat' 
                 'c:\sasuser\month3.dat'),
      RECFM=V,LRECL=256

NOTE: The infile QTR1 is:
      File Name=c:\sasuser\month3.dat,
      File List=('c:\sasuser\month1.dat' 'c:\sasuser\month2.dat' 
                 'c:\sasuser\month3.dat'),
      RECFM=V,LRECL=256

NOTE: 50 records were read from the infile QTR1.
      The minimum record length was 33.
      The maximum record length was 37.
NOTE: 50 records were read from the infile QTR1.
      The minimum record length was 33.
      The maximum record length was 37.
NOTE: 50 records were read from the infile QTR1.
      The minimum record length was 33.
      The maximum record length was 37.
NOTE: The data set WORK.FIRSTQTR has 150 observations 
      and 5 variables.
NOTE: DATA statement used (Total process time):
      real time           4.02 seconds
      cpu time            0.93 seconds
```

以下 `PROC PRINT` 输出显示了 `Work.FirstQtr` 数据集中的部分观测值。

```
proc print 
     data=work.firstqtr (firstobs=45 obs=55);
     format date date9\. 
            revcargo dollar11.2;
run;
```

![Work,FirstQtr Data Set](img/m55-2-g2.png)

# 使用 FILEVAR= 

## 概述

你可以通过使用带有 `FILEVAR=` 选项的 `INFILE` 语句，使合并原始数据的过程更加灵活。`FILEVAR=` 选项允许你动态地更改当前打开的输入文件。

### 带有 FILEVAR= 选项的通用 INFILE 语句

当使用带有 `FILEVAR=` 选项的 `INFILE` 语句时，指定的文件是一个占位符，而不是实际文件名。该变量值的更改会导致 `INFILE` 语句关闭当前输入文件并打开一个新的输入文件。与自动变量一样，该变量不会写入数据集。

## 示例

假设你想创建一个包含三个月原始数据文件数据的 SAS 数据集。这三个月是当前月份以及前两个月![certpgadv/images/m55-5-g1.png]。在接下来的 `INFILE` 语句中，`Temp` 是任意命名的占位符，而不是实际文件名。`FILEVAR=` 变量 `Nextfile` 包含要读取的原始文件名（例如 `Month9.dat`、`Month10.dat` 或 `Month11.dat`）。由于程序尚未完成，因此没有包含 `RUN` 语句。

```
data work.quarter;
   infile temp filevar=nextfile;
   input Flight $ Origin $ Dest
         Date : date9\. RevCargo : comma15.;
```

表 14.5 原始数据文件 `Month9.dat`（前五记录）

```
----+----10---+----20---+----30---+----40 
IA10200 SYD HKG 01SEP2000 $189,441.00 
IA10201 SYD HKG 01SEP2000 $175,473.00 
IA10300 SYD CBR 01SEP2000 $1,370.00 
IA10301 SYD CBR 01SEP2000 $710.00 
IA10302 SYD CBR 01SEP2000 $1,210.00
```

表 14.6 原始数据文件 `Month10.dat`（前五记录）

```
----+----10---+----20---+----30---+----40 
IA10200 SYD HKG 01OCT2000 $182,457.00 
IA10201 SYD HKG 01OCT2000 $160,923.00 
IA10300 SYD CBR 01OCT2000 $1,030.00 
IA10301 SYD CBR 01OCT2000 $870.00 
IA10302 SYD CBR 01OCT2000 $770.00
```

表 14.7 原始数据文件 `Month11.dat`（前五记录）

```
----+----10---+----20---+----30---+----40 
IA10200 SYD HKG 01NOV2000 $176,637.00 
IA10201 SYD HKG 01NOV2000 $164,997.00 
IA10300 SYD CBR 01NOV2000 $1,230.00 
IA10301 SYD CBR 01NOV2000 $1,230.00 
IA10302 SYD CBR 01NOV2000 $790.00
```

注意：你也可以使用多个 `INFILE` 语句或操作系统技术来合并原始数据文件。本章仅讨论 `FILENAME` 语句和带有 `FILEVAR=` 选项的 `INFILE` 语句。

## 分配要读取的文件名

下一步是将要读取的三个文件名赋值给变量 `Nextfile`：

```
 data work.quarter;
    infile temp filevar=nextfile;
    input Flight $ Origin $ Dest 
          Date : date9\. RevCargo : comma15.;
```

在这种情况下，使用原始数据文件 `Month9.dat`、`Month10.dat` 和 `Month11.dat`。注意原始数据文件的标题非常相似。它们都以“Month”开头，后面跟着数字和文件扩展名 .dat：

* `Month9.dat`
* `Month10.dat`
* `Month11.dat`

你可以使用迭代 `DO` 循环和 `PUT` 函数来自动更改赋值给 `Nextfile` 的值。

## 示例

在以下代码中，`DO` 语句创建索引变量 `Month` 并将其赋值为 9、10 和 11。赋值语句随后使用 `Month` 的当前值和 `PUT` 函数将原始数据文件名赋值给 `Nextfile`。`PUT` 函数将 `Month` 的数值值转换为长度为 2 的文本值。`Month9.dat`、`Month10.dat` 和 `Month11.dat` 存储在 Windows 环境下的 `C:\Sasuser` 目录下。在赋值语句的右侧，文本字符串 `c:\sasuser\month` 使用双感叹号（!!）连接运算符与 `Month` 的当前值连接。然后将 `c:\sasuser\monthMonth` 与文本字符串 `.dat` 连接。

```
data work.quarter;
   do Month = 9, 10, 11;
      nextfile="c:\sasuser\month"
               !!put(Month,2.)!!".dat";
      infile temp filevar=nextfile;
      input Flight $ Origin $ Dest 
            Date : date9\. RevCargo : comma15.;
   end;
```

下表显示了当 `Month` 值变化时 `Nextfile` 的值。

| 当 Month= | Nextfile= |
| --- | --- |
| 9 | `c:\sasuser\Month 9.dat` |
| 10 | `c:\sasuser\Month10.dat` |
| 11 | `c:\sasuser\Month11.dat` |





提示：取决于键盘上可用的字符，你用作连接符的符号可以是双竖线 (`||`)、双断开竖线 (`¦¦`) 或双双感叹号 (`!!`)。

## 使用 `COMPRESS` 函数

注意 `c:\sasuser\month 9.dat` 中 `Month` 和 `9` 之间的空格。你可以使用 `COMPRESS` 函数来消除该空格。

| 当 Month= | Nextfile= |
| --- | --- |
| 9 | c:\sasuser\Month 9.dat |
| 10 | c:\sasuser\Month10.dat |
| 11 | c:\sasuser\Month11.dat |

`COMPRESS` 函数的标准形式：`COMPRESS(source, <characters-to-remove>);` 
以下是语法的解释：
`source` 指定包含要删除字符的源字符串。`characters-to-remove` 指定 SAS 从源字符串中删除的字符或字符。

注意：如果省略 `characters-to-remove` 的值，`COMPRESS` 函数将删除源字符串中的空格。

## 示例

在以下代码中，`COMPRESS` 函数删除了 `Nextfile` 值中的空格：

```
data work.quarter;
   do Month = 9, 10, 11;
      nextfile="c:\sasuser\month"!!put(Month,2.)!!".dat";
      nextfile=compress (nextfile,' ');
      infile temp filevar=nextfile;
      input Flight $ Origin $ Dest $ 
            Date : date9\. RevCargo : comma15.;
      end;
```

`COMPRESS` 函数可以与赋值语句结合以提高效率：

```
data work.quarter;
   do Month = 9, 10, 11;
      nextfile="c:\sasuser\month"!!compress(put(Month,2.)!!".dat",' ');
      infile temp filevar=nextfile;
      input Flight $ Origin $ Dest $ 
            Date : date9\. RevCargo : comma15.;
      end;
```

加上 `COMPRESS` 函数后，当 `Month` 的值等于 9 时，`Nextfile` 被赋予正确的值 `c:\sasuser\month9.dat`。

| 当 Month= | Nextfile= |
| --- | --- |
| 9 | c:\sasuser\Month9.dat |
| 10 | c:\sasuser\Month10.dat |
| 11 | c:\sasuser\Month11.dat |

`DO` 循环中的 `OUTPUT` 语句将每个观测值输出到 SAS 数据集 `Work.Quarter`。`STOP` 语句防止 `DATA` 步出现无限循环。

```
data work.quarter;
   do Month = 9, 10, 11;
      nextfile="c:\sasuser\month"
               !!compress(put(Month,2.)!!".dat",' ');
      infile temp filevar=nextfile;
      input Flight $ Origin $ Dest $ Date : date9.
            RevCargo : comma15.;
      output;
   end;
   stop;
```

程序几乎已完成。

## 使用 `END=` 选项

当你读取到输入文件的最后一行之后时，`DATA` 步通常会停止处理。在这个示例中，我们正在读取三个原始数据文件。我们不能读取超过前两个文件的最后记录，因为这会导致 `DATA` 步提前停止处理。你可以使用 `INFILE` 语句中的 `END=` 选项来确定何时读取到最后一个原始数据文件的最后记录。

带有 `END=` 选项的 `INFILE` 语句的标准形式：`INFILE file-specification END=variable;`
以下是语法的解释：
`variable` 是一个 SAS 设置为以下值的变量：
* 当当前输入数据记录不是输入文件的最后记录时，值为 0 (假)
* 当当前输入记录是输入文件的最后记录时，值为 1 (真)

注意：与自动变量一样，`END=` 不会写入 SAS 数据集。你可以测试 `END=` 的值来判断 `DATA` 步是否应该继续处理。

## 示例

`END=` 变量 `Lastobs` 在 `INFILE` 语句中创建。`DO UNTIL` 语句条件执行，直到 `Lastobs` 的值等于 1 (真)。`RUN` 语句完成程序。

```
data work.quarter; 
   do Month = 9, 10, 11; 
   nextfile="c:\sasuser\month"
            !!compress(put(Month,2.)!!".dat",' ');
         do until (lastobs); 
         infile temp filevar=nextfile end=lastobs;
         input Flight $ Origin $ Dest $ Date : date9.
               RevCargo : comma15.;
         output;
      end;
   end;
   stop;
run;
```

`PROC PRINT` 输出显示了 SAS 数据集 `Work.Quarter` 中的部分观测值。注意变量 `Nextfile` 和 `Lastobs` 并没有写入数据集中。

```
 proc print 
     data=work.quarter 
     (firstobs=45 obs=55);
     format date date9\. 
          revcargo dollar11.2;
run;
```

![Work.Quarter Data Set](img/m55-8-g1.png)





```sas
data work.quarter (drop=monthnum midmon lastmon);
   monthnum=month(today());
   midmon=month(intnx('month',today(),-1));
   lastmon=month(intnx('month',today(),-2));
   do Month = monthnum, midmon, lastmon;
      nextfile="c:\sas\month"!!compress(put(Month,2.)!!".dat",' ');
      do until (lastobs); 
         infile temp filevar=nextfile end=lastobs;
         input Flight $ Origin $ Dest $ Date : date9.
               RevCargo : comma15.;
         output;
      end;
   end;
   stop;
run;
```

| ![Values Assigned to the Monthnum, Midmon, and Lastmon Variables](img/m55-14-g3.png) |

以下 `PROC PRINT` 输出显示了 `Work.Quarter` 中部分观测值。

```sas
proc print data=work.quarter 
           (firstobs=45 obs=55);
   format date date9\. 
          revcargo dollar11.2;
run;
```

| ![Work.Quarter Data Set](img/m55-14-g1.png) |

# 追加 SAS 数据集

## 概述

现在你已经学习了合并原始数据文件的几种方法，请使用 `APPEND` 过程来合并两个 SAS 数据集。

通用格式 `PROC APPEND`：`PROC APPEND BASE=SAS-data-set DATA=SAS-data-set;RUN;` 

以下是对语法的解释：
- `BASE=SAS-data-set`：指定你想要添加观测值的数据集。
- `DATA=SAS-data-set`：包含观测值的 SAS 数据集，这些观测值将追加到 `BASE=` 数据集的末尾。

`PROC APPEND` 只读取 `DATA=` SAS 数据集中的数据，而不读取 `BASE=` SAS 数据集。因此，此操作非常高效。即使 `BASE=` 数据集中可能存在 `DATA=` 数据集中不存在的变量，`PROC APPEND` 也会执行数据集合并。当 `BASE=` 数据集包含的变量比 `DATA=` 数据集多时，对于从 `DATA=` 数据集中读入的观测值，额外的变量将被赋予缺失值，并在 SAS 日志中写入警告信息。

## 示例

SAS 数据集 `Work.Cap2001` 和 `Work.Capacity` 都包含以下变量：`Cap1st`、`CapBusiness`、`CapEcon`、`Dest`、`FlightID`、`Origin` 和 `RouteID`。但是，`BASE=` 数据集（`Work.Cap2001`）包含一个 `DATA=` 数据集（`Work.Capacity`）未包含的额外变量 `Date`。当提交以下程序时，SAS 日志显示 `DATA=` 文件未找到变量 `Date`。

```sas
proc append base=work.cap2001 
            data=work.capacity;
run;
```

表 14.8 SAS 日志

```sas
NOTE: Appending WORK.CAPACITY to WORK.CAP2001.
WARNING: Variable Date was not found on DATA file.
NOTE: There were 50 observations read from the data set WORK.CAPACITY.
NOTE: 50 observations added.
NOTE: The data set WORK.CAP2001 has 100 observations and 8 variables.
NOTE: PROCEDURE APPEND used (Total process time):
```

追加后的 `Work.Cap2001` 的 `PROC PRINT` 输出显示，对于从 `DATA=` 数据集中读入的观测值，`Date` 已被赋值为缺失值。

```sas
proc print data=work.cap2001 
           (firstobs=45 obs=55);
run;
```

| ![Work.Cap2001 Data Set](img/18-g1.png) |

注意：你也可以使用 `DATA` 步中的 `SET` 语句来合并数据。如果 `SET` 语句中出现多个数据集名称，输出数据集将是所有数据集的合并。与 `APPEND` 过程不同，`DATA` 步中的 `SET` 语句会读取所有数据集的观测值以进行合并。因此，`APPEND` 过程只读取 `DATA=` 数据集的数据，在合并数据集时更高效。在以下程序中，SAS 读取了 `Work.Cap2001` 的所有观测值，然后读取了 `Work.Capacity` 的所有观测值。

```sas
data work.new;
   set work.cap2001 work.capacity;
run;
```

注意：你还可以使用 `SQL` 过程垂直合并数据。关于使用 `SQL` 过程垂直合并数据的信息，请参阅垂直合并表格。

## 使用 FORCE 选项

在上例中，`DATA=` 数据集（`Work.Capacity`）的变量少于 `BASE=` 数据集（`Work.Cap201`）。然而，当 `DATA=` 数据集的变量多于 `BASE=` 数据集时，可能需要追加。当 `DATA=` 数据集包含 `BASE=` 数据集中不存在的变量时，必须在 `APPEND` 过程中使用 `FORCE` 选项来合并数据集。

带有 `FORCE` 选项的 `PROC APPEND` 通用格式：`PROC APPEND BASE=SAS-data-set DATA=SAS-data-set FORCE>`

注意：`FORCE` 选项会导致数据丢失。

## 示例

在上例中，`DATA=` 数据集（`Work.Capacity`）的变量少于 `BASE=` 数据集（`Work.Cap201`）。然而，当 `DATA=` 数据集的变量多于 `BASE=` 数据集时，可能需要追加。记住 SAS 数据集 `Work.Cap201` 和 `Work.Capacity` 都包含以下变量：`Cap1st`、`CapBusiness`、`CapEcon`、`Dest`、`FlightID`、`Origin` 和 `RouteID`。在这种情况下，`BASE=` 数据集包含一个 `DATA=` 集中没有变量 `Date`。提交以下程序时，SAS 日志显示未找到 `Date` 而未追加数据集。

```sas
proc append base=work.capacity 
            data=work.cap201;
run;
```

表 14.9 SAS 日志

```sas
NOTE: Appending WORK.CAPACITY to WORK.CAP2001.
WARNING: Variable Date was not found in BASE set.
NOTE: data sets were not appended because of above.
```

在 `PROC APPEND` 中使用 `FORCE` 选项时，SAS 日志显示从 `DATA=` 数据集中读取了观测值，但发生了删除或截断。

```sas
proc append base=work.capacity
            data=work.cap201 force;
run;
```

表 14.10 SAS 日志

```sas
NOTE: Appending WORK.CAPACITY to WORK.CAP2001.
WARNING: Variable Date was not found on BASE file.
NOTE: FORCE is specified, so dropping/truncating will occur.
NOTE: There were 50 observations read from the data set WORK.CAPACITY.
NOTE: 50 observations added.
NOTE: The data set WORK.CAPACITY has 100 observations and 7 variables.
NOTE: PROCEDURE APPEND used (Total process time):
      real time 0.03 seconds
      cpu time 0.03 seconds
```

`PROC PRINT` 输出显示变量 `Date` 已从 `Work.Capacity` 的追加版本中删除。

```sas
proc print data=work.capacity 
     (firstobs=45 obs=55);
run;
```

| ![Work.Capacity Data Set](img/m55-19-g1.png) |

## 追加不同长度的变量

如果 `DATA=` 数据集中包含的变量长度大于 `BASE=` 数据集中同名的变量，则必须在 `PROC APPEND` 中使用 `FORCE` 选项。使用 `FORCE` 选项允许你追加数据集，但 `DATA=` 变量的值可能会被截断。

## 示例

在 SAS 数据集 `Work.Acities` 中，变量 `City` 的长度为 22。在 SAS 数据集 `Work.WestAust` 中，`City` 的长度为 50。你可以使用 `CONTENTS` 过程查看每个数据变量的属性。

```sas
proc contents data=work.acities;
run;
```

| ![Work.Acities Data Set](img/m55-20-g1.png) |

```sas
proc contents data=work.westaust;
run;
```

| ![Work.WestAust Data Set](img/m55-20-g2.png) |

当提交以下程序时，SAS 日志显示由于 `BASE=` 和 `DATA=` 数据集中 `City` 的长度不同，未追加数据集。

```sas
proc append base=work.acities 
            data=work.westaust;
run;
```





```
NOTE: Appending WORK.WESTAUST to WORK.ACITIES.
WARNING: Variable City has different lengths on BASE and
         DATA files (BASE 22 DATA 50).
ERROR: No appending done because of anomalies listed above.
       Use FORCE option to append these files.
NOTE: 0 observations added.
NOTE: The data set WORK.ACITIES has 50 observations and 4 variables.
NOTE: Statements not processed because of errors noted above.
NOTE: PROCEDURE APPEND used (Total process time):
      real time           1.44 seconds
      cpu time            0.06 seconds
NOTE: The SAS System stopped processing this step because of errors.
```

当使用 `FORCE` 选项时，SAS 日志显示数据集已追加，但发生了丢弃或截断。

```
proc append base=work.acities 
            data=work.westaust force;
run;
```

表 14.12 SAS 日志

```
NOTE: Appending WORK.WESTAUST to WORK.ACITIES.
WARNING: Variable City has different lengths on BASE and DATA files
         (BASE 22 DATA 50).
NOTE: FORCE is specified, so dropping/truncating will occur.
NOTE: There were 50 observations read from the data set WORK.WESTAUST.
NOTE: 50 observations added.
NOTE: The data set WORK.ACITIES has 100 observations and 4 variables.
NOTE: PROCEDURE APPEND used (Total process time):
      real time           1.44 seconds
      cpu time            0.06 seconds
```

`Work.Acities` 追加版本的 `PROC CONTENTS` 输出显示，变量 `City` 保留了来自 `BASE=` 数据集的长度 22。此外，请注意变量 `Code` 保留了来自 `BASE=` 数据集的标签 `Start Point`。

``````
proc contents 
     data=work.acities;
run;
```

![Work.Acities 数据集](img/m55-20-g3.png)

`PROC PRINT` 输出显示，在 `Work.Acities` 追加版本中，`City` 的某些值被截断了。

```
proc print 
     data=work.acities 
          (firstobs=45 obs=55);
run;
```

![Work.Acities 数据集](img/m55-20-g4.png)

## 追加不同类型的变量

如果 `DATA=` 数据集中包含的变量与 `BASE=` 数据集中对应变量的类型不同，则在使用 `PROC APPEND` 时必须使用 `FORCE` 选项。使用 `FORCE` 选项允许你追加数据集。然而，对于类型不匹配的变量，`DATA=` 变量将被赋值缺失值。

## 示例

在 SAS 数据集 `Work.Allemps` 中，变量 `Phone` 是字符变量。在 SAS 数据集 `Work.Newemps` 中，`Phone` 是数值变量。你可以使用 `PROC CONTENTS` 查看每个数据变量的属性。

```
proc contents data=work.allemps;
run;
```

![Work.Allemps 数据集](img/m55-21-g2.png)

```
proc contents data=work.newemps;
run;
```

![Work.Newemps 数据集](img/m55-21-g1.png)

当提交以下程序时，SAS 日志显示变量 `Phone` 类型不匹配，且数据集未追加。

```
proc append base=work.allemps 
            data=work.newemps;
run;
```

表 14.13 SAS 日志

```
NOTE: Appending WORK.NEWEMPS to WORK.ALLEMPS.
WARNING: Variable Phone not appended because of type mismatch.
ERROR: No appending done because of anomalies listed above.
       Use FORCE option to append these files.
NOTE: 0 observations added.
NOTE: The data set WORK.ALLEMPS has 550 observations and 5 variables.
NOTE: Statements not processed because of errors noted above.
NOTE: PROCEDURE APPEND used (Total process time):
      real time           0.08 seconds    
      cpu time            0.01 seconds
NOTE: The SAS System stopped processing this step because of errors.
```

当使用 `FORCE` 选项时，SAS 日志显示数据集已追加，但由于类型不匹配，变量 `Phone` 未被追加。

```
proc append base=work.allemps 
            data=work.newemps force;
run;
```

表 14.14 SAS 日志

```
NOTE: Appending WORK.NEWEMPS to WORK.ALLEMPS.
WARNING: Variable Phone not appended because of type mismatch.
NOTE: FORCE is specified, so dropping/truncating will occur.
NOTE: There were 19 observations read from the data set WORK.NEWEMPS.
NOTE: 19 observations added.
NOTE: The data set WORK.ALLEMPS has 569 observations and 5 variables.
NOTE: PROCEDURE APPEND used (Total process time):
      real time           0.05 seconds
      cpu time            0.02 seconds
```

`Work.Allemps` 追加版本的 `PROC CONTENTS` 输出显示，变量 `Phone` 保留了来自 `BASE=` 数据集的字符类型。

```
proc contents 
     data=work.allemps;
run;
```

![Work.Allemps 数据集](img/m55-21.png)

`Work.Acities` 追加版本的 `PROC PRINT` 输出显示，`BASE=` 数据集中 `City` 的值是缺失的。

```
proc print 
     data=work.acities 
          (firstobs=45);
```

![Work.Acities 数据集](img/m55-24.png)

### 附加功能

除了本章讨论的追加数据集的方法外，你还可以使用数据集或外部文件来追加数据集。

## 将文件名存储在数据集中

在以下程序中，`Route1.dat`、`Route2.dat`、`Route3.dat`、`Route4.dat` 和 `Route5.dat` 被追加以创建数据集 `Work.NewRoute`。这些文件名存储在 `Sasuser` 数据集中，并使用 `SET` 语句引用。`FILEVAR=` 变量是从 `Rawdata` 读取的变量名。

```sas
data newroute;
  set sasuser.rawdata;
  infile filevar=readit end=lastfile;
  do while(lastfile = 0);       
    input  @1 RouteID $7. @8 Origin $3. @11 Dest $3. 
           @14 Distance 5. @19 Fare1st 4. 
           @23 FareBusiness 4. @27 Farecon 4. 
           @31 FareCargo 5.;	         
    output;
  end;
run;
```

![Sasuser.Rawdata 数据集](img/m55-25.png)

## 将文件名存储在外部文件中

在以下程序中，`Route1.dat`、`Route2.dat`、`Route3.dat`、`Route4.dat` 和 `Route5.dat` 也被追加以创建数据集 `Work.NewRoute`。在本例中，数据集文件名存储在外部文件 `Rawdatafiles.dat` 中，该文件在第一个 `INFILE` 语句中引用。`FILEVAR=` 变量 `readit` 是从 `Rawdatafiles` 读取的变量。`readit` 的值为要读取的文件名。

表 14.15 原始文件 Rawdatafiles.dat

```
1---+----10---+----20
route1.dat  
route2.dat  
route3.dat   
route4.dat   
route5.dat
```

```sas
data newroute;
   infile 'rawdatafiles.dat';
   input readit $10.;
   infile filevar=readit end=lastfile;
   do while(lastfile = 0);       
      input  @1 RouteID $7. @8 Origin $3. @11 Dest $3. 
             @14 Distance 5. @19 Fare1st 4. 
             @23 FareBusiness 4. @27 Farecon 4. 
             @31 FareCargo 5.;	         
      output;
   end;
run;
```

## 总结

### 使用 FILENAME 语句

你可以通过为要合并的所有原始文件分配单个引用来使用 `FILENAME` 语句追加原始文件。当在 `INFILE` 语句中指定引用时，可以使用 `INPUT` 语句顺序读取引用的每个原始文件到数据集。

### 使用 INFILE 语句





通过使用带有 `FILEVAR=`选项的 `INFILE` 语句，可以让原始数据文件的合并过程更加灵活。`FILEVAR=`选项允许你动态地将当前打开的输入文件更改新的输入文件。当 `INFILE` 语句执行时，它从 `FILEVAR=` 变量指定的文件读取数据。

在某些情况下，你可能需要使用 `COMPRESS` 函数来消除生成的文件名中的空格。当读取原始数据文件的最后一条记录时，`DATA` 步通常会停止处理。当你合并原始数据文件时，你不希望在最后一条记录之后停止，直到到达最后一个输入文件的末尾。你可以通过 `INFILE` 语句的 `END=` 选项来判断是否正在读取最后一个原始数据文件的最后一条记录。然后，你可以测试 `END=` 变量的值来确定 `DATA` 步是否应该继续处理。如果你正在处理与日期相关的数据，可以通过消除在 SAS 语句中包含显式月份数字的需求，使你的程序更具灵活性。要创建一个始终读取当前月及前两个月的程序，可以使用 `MONTH` 和 `TODAY` 函数获取今天日期的月份数，以开始滚动季度。在某些情况下，你可能需要结合 `TODAY` 和 `MONTH` 函数使用 `INTNX` 函数来正确确定月份。

## 追加 SAS 数据集

你可以使用 `PROC APPEND` 来合并两个 SAS 数据集。`PROC APPEND` 只读取 `DATA=` SAS 数据集中的数据，而不读取 `BASE=` SAS 数据集中的数据。即使 `BASE=` 数据集中可能存在 `DATA=` 数据集中不存在的变量，`PROC APPEND` 也会对数据集进行合并。如果 `DATA=` 数据集包含以下特征的变量，则必须使用 `FORCE` 选项：

* 它们不在 `BASE=` 数据集中。
* 它们比 `BASE=` 数据集中的变量长。
* 它们的类型与 `BASE=` 数据集中的变量不同。

使用 `FORCE` 选项可能会由于变量的截断或删除导致数据丢失。下表总结了使用 `FORCE` 选项的后果。

| `DATA=` 数据集中变量的特征 | 是否需要 FORCE | 使用 FORCE 选项的后果 |
| --- | --- | --- |
| 它们在 `BASE=` 数据集中，但 `BASE=` 数据集的变量更多。 | 否 | 为额外的 `BASE=` 数据集变量分配缺失值。 |
| 它们不在 `BASE=` 数据集中。 | 是 | 丢额外的 `DATA=` 数据集变量。 |
| 它们比 `BASE=` 数据集中对应的变量长。 | 是 | `DATA=` 数据集的变量值可能会被截断。 |
| 它们的类型与 `BASE=` 数据集中对应的变量不同。 | 是 | 为数据类型不匹配的 `DATA=` 数据集变量分配缺失值。 |

## 其他功能

你还可以使用 SAS 数据集或包含要追加的原始数据文件名的外部文件来追加原始数据文件。

## 示例程序

### 使用 FILENAME 语句合并原始数据文件

```
filename qtr1 ('c:\data\month1.dat''c:\data\month2.dat
               'c:\data\month3.dat');
data work.firstqtr;         
   infile qtr1;'
   input Flight $ Origin $ Dest $   
         Date : date9\. RevCargo : comma15.;
run;
```

### 使用 INFILE 语句合并原始数据文件

```
data quarter (drop=monthnum midmon lastmon);
   monthnum=month(today());
   midmon=month(intnx('month',today(),-1));
   lastmon=month(intnx('month',today(),-2));
   do month = monthnum, midmon, lastmon;  
      nextfile="c:\sasuser\month"
               !!compress(put(month,2.)!!".dat",' ');
      do until (lastobs); 
         infile temp filevar=nextfile end=lastobs; 
         input Flight $ Origin $ Dest $ Date : date9.
               RevCargo : comma15.;
         output; 
      end; 
   end;  
   stop; 
run;
```

### 使用 PROC APPEND 合并 SAS 数据集

```
proc append base=work.acities
            data=work.airports force;
run;
```

## 注意事项

* 当使用带有 `FILEVAR=`选项的 `INFILE` 语句时，文件规范只是一个占位符，而不是之前分配给文件的实际文件名或引用名（fileref）。
* 与自动变量一样，`FILEVAR=`变量和 `END=`变量不会被写入数据集。
* 在 `PROC APPEND` 中使用 `FORCE` 选项可能会由于变量的截断或删除导致数据丢失。
* `BASE=` 数据集的结构将用于追加的数据集。

# 测验

为每个问题选择最佳答案。完成测试后，使用附录中的答案键检查你的答案。

1. 下列哪个语句将引用名 `OnSale` 与原始数据文件 `London.dat`、`Paris.dat` 和 `Zurich.dat` 关联？这些文件存储在 Windows 环境下的 `C:\Routes\New` 目录下。

    1. ```
       filename onsale (c:\routes\new\london.dat,
           c:\routes\new\paris.dat,
           c:\routes\new\zurich.dat);
       ```
    2. ```
       filename onsale 'c:\routes\new\london.dat'
           'c:\routes\new\paris.dat'
           'c:\routes\new\zurich.dat';
       ```
    3. ```
       filename onsale (c:\routes\new\london.dat,
           c:\routes\new\paris.dat
           c:\routes\new\zurich.dat);
       ```
    4. ```
       filename onsale 'c:\routes\new\london.dat
           c:\routes\new\paris.dat
           c:\routes\new\zurich.dat
       ```

2. 下列哪个说法是正确的？

    1. `FILEVAR=`选项可动态更改当前打开的输入文件。
    2. `FILEVAR=`变量不会写入数据集。
    3. `FILEVAR=`必须包含字符字符串。
    4. 以上所有。

3. 给定以下程序，哪个表格显示了对应的 `Month` 值？

    ```
    data work.revenue; 
       do month = 8, 9, 10;
          readfile=compress("c:\data\month"!!put(month,2.)!!".dat");
          do until (lastobs); 
             infile temp filevar=readfile 
               end=lastobs;
             input Date :7. Location $ dollar.;
             output;
          end;
       end;
       stop;
    run;
    ```

    1. 当 `month=8` 时
    2. 当 `month=9` 时
    3. 当 `month=10` 时
    4. 以上均不是

4. 如果当前日期是 2003 年 3 月 30 日，哪个表格正确显示了 `y1`、`y2`、`y3` 和 `Nextfile` 的值？

    ```
    data work.quarter (drop=monthnum midmon lastmon); 
       y3=year(today());
       y2=y3-1;
       y1=y3-2;
       do i = y3, y2, y1;
          nextfile="c:\data\Y"!!put(i,4.)!!".dat";        
          do until (lastobs); 
             infile temp filevar=nextfile 
               end=lastobs; 
             input Flight $ Origin $ Dest $ 
                   Date : date9.;
             output;
          end;
       end;
       stop;
    run;
    ```

    1. `y1=2001`, `nextfile=c:\data\Y2001.dat`
    2. `y2=2002`, `nextfile=c:\data\Y2002.dat`
    3. `y3=2003`, `nextfile=c:\data\Y2003.dat`
    4. 以上所有。





| --- | --- |
| y1 | `c:\data\Y2003.dat` |
| y2 | `c:\data\Y2002.dat` |
| y3 | `c:\data\Y2001.dat` |

4. | `i=` | `Nextfile=` |
| --- | --- |
| y1 | `c:\data\Y3.dat` |
| y2 | `c:\data\Y2.dat` |
| y3 | `c:\data\Y1.dat` |

### 5. 当 SAS 处理输入文件中的最后数据记录时会发生什么？

1. `END=` 变量被设置为 1。
2. `END=` 变量被设置为 0。
3. `END=` 变量被设置为输入文件中的记录数。
4. `END=` 变量写入 SAS 数据集。

### 6. 哪个程序将 `Work.London` 追加到 `Work.Flights` 之后？

1. ```
proc append base=work.london 
            data=work.flights;
run;
```
2. ```
proc append data=work.london 
            base=work.flights;
run;
```
3. ```
proc append data=work.london work.flights;
run;
```
4. ```
proc append data=work.flights work.london;
run;
```

### 7. 提交以下程序时会发生什么？

```
proc append base=staff.marketing
            data=staff.sales force;
run;
```

| Staff.Marketing 的数据集描述 | Staff.Sales 的数据集描述 |
| --- | --- |
| ![](img/m55-27-g11.png) | ![](img/m55-27-g12.png) |

1. `Staff.Marketing` 中的 `LastName` 长度被转换为 20。
2. `Staff.Marketing` 中删除了 `LastName`。
3. 从 `Staff.Sales` 读取的 `LastName` 观测值被分配缺失值。
4. 从 `Staff.Sales` 读取的观测值中，`LastName` 的某些值可能会被截断。

### 8. 哪个程序将 `Work.April` 追加到 `Work.Y2003` 之后？

| Work.Y2003 的数据集描述 | Work.April 的数据集描述 |
| --- | --- |
| ![](img/m55-27-g13.png) | ![](img/m55-27-g14.png) |

1. ```
proc append base=work.y2003 
            data=work.april;
run;
```
2. ```
proc append base=work.april 
            data=work.y2003 force;
run;
```
3. ```
proc append base=work.y2003
            data=work.april force;
run;
```
4. ```
proc append base=work.april 
            data=work.y2003;
run;
```

### 9. 使用 `PROC APPEND` 将 SAS 数据集 `Work.NewHires` 追加到 SAS 数据集 `Work.Employees` 时会发生什么？

| Work.Employees 的数据集描述 | Work.NewHires 的数据集描述 |
| --- | --- |
| ![](img/m55-27-g15.png) | ![](img/m55-27-g16.png) |

1. 从 `Work.NewHires` 读取的观测值的 `Room` 被分配了缺失值。
2. `Work.Employees` 中所有观测值的 `Room` 被分配了缺失值。
3. `Work.Employees` 中删除了 `Room`。
4. 从 `Work.NewHires` 读取的观测值中，`Name` 的值被截断。

### 10. 在以下情况下，你不需要配合 `PROC APPEND` 使用 `FORCE` 选项：

1. `DATA=` 数据集包含 `BASE=` 数据集中不存在的变量。
2. `BASE=` 数据集包含 `DATA=` 数据集中不存在的变量。
3. `DATA=` 数据集中的变量比 `BASE=` 数据集中对应的变量更长。
4. `DATA=` 数据集中的变量类型与 `BASE=` 数据集中对应的变量类型不同。

# 第 15 章：水平合并数据

## 概述

## 引言
水平合并数据是指将多个数据集合并或连接到一个数据集的过程。这个过程被称为水平合并，是因为在最终的数据集中，每个观测值（或水平行）将包含来自多个输入数据集的变量。![水平合并](img/m56-1-g1.png)如果有包含相关信息的数据集，水平合并数据是非常有用的。例如，假设你有一个包含 IDNumber、Name 和 Address 的员工数据数据集，以及另一个包含 Salary 的员工数据数据集。你可以水平地合并这两个数据集的数据，创建一个包含 IDNumber、Name、Address 和 Salary 的输出数据集。本章将重点介绍在 DATA 步中水平合并数据的几种方法，并比较了 DATA 步匹配-合并与 PROC SQL 链接。本章还涵盖了将输入数据集与非数据集值进行水平合并的几种技术。

## 回顾术语

## 概述
在检查水平合并数据的技术之前，这里是对本章使用的一些术语的回顾。

| 术语 | 定义 |
| --- | --- |
| 水平合并数据 | 根据主源变量的值，从辅助源或源检索数据的技术。 |
| 执行表查找 | 根据主源变量的值，从辅助源或源检索数据的技术。 |
| 基表 | 水平合并中的主源。在本章中，基表始终是一个 SAS 数据集。 |
| 查找表或表 | 用于水平合并的基表以外的输入源。 |
| 查找值或返回值 | 水平合并期间从查找表或表中检索的数据值或值。 |
| 键变量或变量 | 基表和查找表中共同存在的多个变量。通常，键值在查找表中唯一的，但在基表中并不唯一。 |
| 键值或值 | 当基表中的键值在查找表中找到匹配的键值时，查找成功。 |

注意：水平合并数据和表查找是同义词，在本章中交替使用。注意：本章将 PROC SQL 技术与 DATA 步技术进行了比较。在 PROC SQL 术语中，SAS 数据集通常称为表，变量通常称为列，观测值通常称为行。下图说明了一个用于水平合并的基表和查找表。键变量是 Num。键值在 Num 下方垂直列出。![水平合并](img/m56-2-g1.png)

## 输入数据源之间的关系





在执行表查找时，需要考虑的一个重要因素是输入数据源之间的关系。为了在水平方向合并数据，你必须能够匹配来自每个输入数据源的观测值。例如，每个输入数据源可能有一个或多个共同的变量。输入数据源之间的关系描述了根据这些键值，一个源中的观测值与另一个源中的观测值之间的关系。以下术语描述了基表和查找表之间可能的关系：

- 一对一匹配
- 一对多匹配
- 多对多匹配
- 不匹配数据

在一对一匹配中，基表和查找表中的键值都是唯一的。因此，对于基表中的每个观测值，查找表中最多有一个观测值具有匹配的键值。![one-to-one match](img/m56-3-g1.png) 在一对多匹配中，基表中的键值是唯一的，但查找表中的键值不是唯一的。也就是说，对于基表中的每个观测值，查找表中可以有一个或多个具有匹配键值的观测值。![one-to-one match](img/m56-3-g2.png) 在多对多匹配中，基表或查找表中的键值均不唯一。也就是说，基表中至少有一个观测值匹配查找表中的多个观测值，且查找表中至少有一个观测值匹配基表中的多个观测值。多对多是一种理论上或数学上的可能性，但很少代表实际的业务应用。如果一个业务应用看起来是多对多的，通常是因为不小心向查找表中添加了重复行。![one-to-one match](img/m56-3-g3a.png) 有时你会遇到一对一、一对多或多对多的匹配，同时也包含不匹配数据。也就是说，基表中存在不匹配查找表中任何观测值的观测值，或者查找表中存在某些观测值在基表中没有匹配的观测值。如果你的基表或查找表包含包含不匹配数据，你将出现以下情况之一：

- 密集匹配（dense match），其中一个表的每个或几乎每个观测值在另一个表中都有匹配的观测值。在底图中，基表中的第一个观测值是未的。![dense match](img/m56-3-g4.png)
- 稀疏匹配（sparse match），其中有很多不匹配的观测值。![sparse match](img/m56-3-g5.png)

# 在 SAS 数据集之外使用查找值

## 概述

请记住，你的查找表并不非是一个 SAS 数据集。假设你想将基表的数据与未存储在 SAS 数据集中的查找值合并。你可以使用以下技术将查找值硬编码到程序中：

- `IF-THEN/ELSE` 语句
- SAS 数组（arrays）
- 用户定义的 SAS 格式（formats）
- 哈希对象（hash objects）

## IF-THEN/ELSE 语句

你应该熟悉 `IF-THEN/ELSE` 语句的语法和用法。总体而言，这种技术易于使用且易于理解。由于其简单性，并且你可以配合它使用其他 DATA step 语法，`IF-THEN/ELSE` 语句作为执行查找操作的技术可以非常灵活。如果你的查找值没有存储在数据集中，可以使用这种技术，并用它来处理基表和查找表之间任何可能的关系。你可以用它检索单个或多个值。例如，你可以使用 DO 组根据条件提供多个值。请记住，这种技术需要维护。如果你预计查找值会发生，或者你有大量的查找值，或者你在多个程序中使用这些查找值，那么维护程序中 `IF-THEN/ELSE` 语句所需的资源可能会使这种技术不再适用。此外，这种技术可能会导致程序冗长得难以接受，甚至导致程序因为超时而无法执行。

## 示例：使用 IF-THEN/ELSE 语句合并数据

假设你有一个数据集 `Mylib.Employees`，其中包含关于员工的信息。`Mylib.Employees` 包含一个名为 `IDnum` 的变量，记录每个员工的唯一识别码。如果你想将 `Mylib.Employees` 中的数据与未存储在数据集中的员工出生日期列表合并，可以使用 `IF-THEN/ELSE` 语句来实现。

```sas
data mylib.employees_new;
   set mylib.employees;
   if IDnum=1001 then Birthdate='01JAN1963'd;
   else if IDnum=1002 then Birthdate='08AUG1946'd;
   else if IDnum=1003 then Birthdate='23MAR1950'd;
   else if IDnum=1004 then Birthdate='17JUN1973'd;
run;
```

## SAS 数组

你应该熟悉 `ARRAY` 语句的语法和用法。通过 `ARRAY` 语句，你既可以将查找值硬编码到程序中，也可以从数据集中读取到数组中。SAS 数组的元素是通过位置引用的。也就是说，你使用数值值作为数组的指针。因此，你必须通过位置或根据另一个数值来标识数组元素。你可以使用多个值或数值表达式来确定返回的数组元素。这种技术能够从查找操作返回单个值。数组的维度必须在编译时通过宏变量提供。

## 示例：使用 ARRAY 语句合并数据

我们将考虑将 `Mylib.Employees` 的数据与查找值列表合并的示例。请记住 `Mylib.Employees` 包含关于员工的信息，其识别码（`IDnum`），但未包含出生日期。你可以使用 `ARRAY` 语句将出生日期硬编码到名为 `Birthdates` 的临时数组中，然后使用该数组与 `Mylib.Employees` 中的数据合并。在下面的 DATA step 中，作为数组下标的值对应于基表 `Mylib.Employees` 中的变量 `IDnum`。新变量 `Birthdate` 的赋值语句根据 `IDnum` 的当前值从 `Birthdates` 数组检索值。

```sas
data mylib.employees_new;
   array birthdates{1001:1004} _temporary_ ('01JAN1963'd
         '08AUG1946'd '23MAR1950'd '17JUN1973'd);
   set mylib.employees;
   Birthdate=birthdates{IDnum};
run;
```

## 用户定义的 SAS 格式

你应该熟悉 `FORMAT` 过程结合 `VALUE` 语句的语法和用法。格式可以在 `FORMAT` 语句、`PUT` 语句以及赋值 `WHERE` 或 `IF` 语句中的 `PUT` 函数中引用。`FORMAT` 过程对查找表使用二进制查找。使用这种技术的另一个优点是维护是集中化的；如果查找值发生变化，你只需要在一个地方（格式中）进行更改，每个使用该格式的程序都会使用新值。

## 示例：使用 FORMAT 过程合并数据

再次假设数据集 `Mylib.Employees` 根据员工识别码（`IDnum`）包含员工信息，但不包含员工的出生日期。你可以使用格式将员工的出生日期与存储在 `Mylib.Employees` 中的数据合并。下面的 `PROC FORMAT` 步骤使用 `VALUE` 语句在 `BIRTHDATE` 格式中硬编码查找值。DATA step 使用 `PUT` 函数将格式查找值与 `IDnum` 的值关联。`INPUT` 函数将查找值与 `DATE9.` 格式关联，并将格式化值分配给新变量 `Birthdate`。





```sas
proc format;
   value birthdate 1001 = '01JAN1963'
                   1002 = '08AUG1946'
                   1003 = '23MAR1950'
                   1004 = '17JUN1973';
   run;

   data mylib.employees_new;
   set mylib.employees;
   Birthdate=input(put(IDnum,birthdate.),date9.);
run;
```

# 使用 DATA 步进行匹配-合并数据

## DATA 步匹配-合并
当每个输入数据集中都有共同的 `BY` 变量时，你应该已经知道如何在 `DATA` 步中合并多个数据集。当你使用 `MERGE` 语句执行表查找操作时，你的查找值必须存储在一个或多个 SAS 数据集中。这种技术要求基准表和查找表（或多个表）都已根据 `BY` 变量或变量进行了排序或建立索引。只要所有输入数据集具有共同的 `BY` 变量，你就可以在 `MERGE` 语句中指定任意数量的输入。`MERGE` 语句可以合并任意大小的数据集。`MERGE` 语句能够返回多个值。你可以使用多个 `BY` 变量来执行依赖于多个一个变量的查找。`MERGE` 语句默认同时返回匹配项和不匹配项，但你可以使用 `DATA` 步语法来仅返回精确匹配项，或仅包含查找表中的特定变量。

**注意**：尽管你可以使用 `MERGE` 语句合并来自任何类型关系源的数据，但在处理多对多匹配时，这种技术可能无法产生预期的结果。在 `DATA` 步中合并数据集时，观测值是按顺序匹配并组合的。一旦某个观测值被读取，它就不会被重新读取。这意味着 `DATA` 步的 `MERGE` 语句不会创建笛卡尔积。因此，在处理多对多匹配时，`DATA` 步 `MERGE` 语句可能不是执行查找操作的合适技术。

## 处理多个查找表
有时，你可能需要合并来自三个或更多相关 SAS 数据集的数据以创建一个新数据集。例如，下面列出的三个数据集都包含关于一家虚拟航空公司航班和机场的不同信息。`Sasuser.Acities` 包含关于各种机场的数据，`Sasuser.Revenue` 包含由各种航班产生的收入的数据，`Sasuser.Expenses` 包含由各种航班产生的费用的数据。这些数据集中的变量列在此处。

![处理多个查找表](img/m56-10-g1.png)

假设你想创建一个名为 `Sasuser.Alldata` 的新数据集，包含来自这三个输入数据集的数据。如下所示，`Sasuser.Alldata` 数据集包含新变量 `Profit`，该变量根据存储在 `Sasuser.Revenue` 中的收入值和存储在 `Sasuser.Expenses` 中的费用值计算得出。

![处理多个查找表](img/m56-10-g2.png)

只要所有输入数据集具有共同的 `BY` 变量，你就可以在 `MERGE` 语句中指定任意数量的输入数据集。然而，从上面的数据集变量列表中可以看出，这三个数据集并没有共同的变量。我们将考虑一种对这三个数据集执行匹配-合并的方法。

尽管 `Sasuser.Acities`、`Sasuser.Revenue` 和 `Sasuser.Expenses` 这三个数据集没有共同的 `BY` 变量，但有几个变量是三个数据集中的两个共有的。如下所示，`Date` 和 `FlightID` 在 `Revenue` 和 `Expenses` 共有。`Acities` 数据集中的变量 `Code` 和 `Revenue` 数据集中的变量 `Dest` 虽然命名不同，但它们包含相同类型和长度的数据。

![处理多个查找表](img/m56-11-g1.png)

注意 `Acities` 中的 `Code` 和 `Revenue` 中的 `Dest` 被列为相互对应，尽管它们的名称不同。当你在这数据集之间寻找共同变量时，变量名并不重要，因为它们可以通过 `MERGE` 语句中的 `RENAME=` 选项进行更改。相反，你应该寻找在每个输入数据集中记录相同信息且具有相同类型的变量。共同变量不需要具有相同的长度，但你应该记住，第一个列出的数据集中的变量长度将决定输出数据集中变量的长度。

**注意**：在 `MERGE` 语句的多个数据集中具有相同名的变量也必须具有相同的类型。如果不同输入数据集中的任何变量具有相同名称但类型不同，SAS 日志中将写入 `ERROR` 和 `WARNING` 信息，且匹配-合并失败。在这种情况下，`Acities` 中的 `Code` 和 `Revenue` 中的 `Dest` 都记录了机场的三字母缩写。

**提示**：你可以使用 `PROC CONTENTS` 查看关于变量的信息，如类型、长度和描述。由于显示的三个数据集之间存在对共有变量，你可以通过在两个后续的 `DATA` 步中使用 `MERGE` 语句将这些数据集合并为一个数据集。也就是说，你可以先对其中两个数据集执行一次匹配-合并以创建一个新数据集，然后对该新数据集和剩余数据集执行另一次匹配-合并。考虑以下示例。

## 示例
在以下程序中，`Sasuser.Expenses` 和 `Sasuser.Revenue` 都按 `FlightID` 和 `Date` 排序，并放入临时数据集以准备合并。然后这两个数据集在 `DATA` 步中创建一个名为 `Revexns` 的临时输出数据集。为了减少输出数据集的变量数，创建了一个新变量 `Profit`，并删除了创建 `Profit` 的变量。

```sas
proc sort data=sasuser.expenses out=expenses;
   by Flightid date;
run;

proc sort data=sasuser.revenue out=revenue;
   by flightid date;
run;

data revexpns (drop=rev1st revecon);
   merge expenses(in=e) revenue(in=r);
   by flightid date;
   if e and r;
   Profit=sum(rev1st, revbusiness, revecon, -expenses);
run;
```

**注意**：上述 `IF` 语句中使用 `IN=` 变量 `E` 和 `R` 确保包含两个数据集数据的观测值被包含在输出集中。

在以下程序中，输出数据集 `Revexns` 按 `Dest` 排序。`Sasuser.Actities` 按 `Code` 排序并放入临时数据集。记住，尽管名称不同，`Dest` 和 `Code` 都是对应的变量。排序后的数据集随后在 `DATA` 步中合并。由于两个数据集必须至少有一个精确匹配的变量才能合并，`RENAME=` 选项将 `Code` 重命名为 `Dest`。`DATA` 步将 `Revexns` 和 `Aities` 合并为名为 `Alldata` 的新输出数据集。

```sas
proc sort data=revexns;
   by dest;
run;

proc sort data=sasuser.acities out=acities;
   by code;
run;

data sasuser.alldata;
   merge revexpns(in=r) acities
         (in=a rename=(code=dest) keep=city name code);
   by dest;
   if r and a;
run;

proc print data=sasuser.alldata(obs=5) noobs;
   title '合并三个数据集的结果';
   format Date date9.;
run;
```

`PROC PRINT` 步骤打印示例中创建的 `Sasuser.Alldata` 数据集的前五个观测值，如下所示![处理多个查找表](img/m56-12-g1.png)

# 使用 PROC SQL 连接数据

## SQL 过程





另一种可以用于连接没有公共变量的数据集的方法是 SQL 过程。你应该已经熟悉如何使用 `PROC SQL` 根据内连接（inner join）的结果来创建表。在 `PROC SQL` 步骤中，你可以从每个输入数据集中仅选择你想要包含在新数据集中的特定变量。输入数据集不需要包含公共的 `BY` 变量，也不需要进行排序或索引。然而，如果查找表具有索引，SQL 过程可以利用索引来提供更快的查找值检索。你可以使用 SQL 过程连接多达 256 个表，从具有任何类型关系（一对一、一对多、多对多或不匹配）的源从水平方向合并数据。

注意：尽管 `PROC SQL` 可以实现许多类型的连接，但本章仅讨论了内连接。因此，在本章的剩余部分中，`PROC SQL` 连接指的是对多个表进行内连接，其结果存储在一个新表中。你可以在使用 PROC SQL 水平合并表 中了解更多关于 `PROC SQL` 连接的知识。

使用 SQL 过程执行表查找的一个缺点是不能在 `PROC SQL` 中使用 `DATA` 步骤语法。因此，复杂的业务逻辑很难纳入连接中。然而，通过使用 `PROC SQL`，你通常一个步骤中完成需要多个 `PROC SORT` 和 `DATA` 步骤才能完成的工作。

## 示例：处理多个查找表

以下示例将 `Sasuser.Revenue`、`Sasuser.Expenses` 和 `Sasuser.Acities` 连接到名为 `Work.Sqljoin` 的新数据集：

```
proc sql;
   create table sqljoin as
      select revenue.flightid, revenue.date format=date9.,
             revenue.origin, revenue.dest,
             sum(revenue.rev1st,
                 revenue.revbusiness,
                 revenue.revecon)
             -expenses.expenses as Profit,
             acities.city,
             acities.name
         from sasuser.expenses, sasuser.revenue,
             sasuser.acities
         where expenses.flightid=revenue.flightid
              and expenses.date=revenue.date
              and acities.code=revenue.dest
         order by revenue.dest,
                 revenue.flightid,
                 revenue.date;
quit;

proc print data=work.sqljoin(obs=5);
   title 'Result of Joining Three Data Sets';
run;
```

`PROC PRINT` 步骤产生上述 `PROC SQL` 步骤中创建的 `Work.Sqljoin` 数据集的前五个观测值，所示：![处理多个查找表](img/m56-16-g1.png) 注意：注意 `Work.Sqljoin` 数据集与之前在 `DATA` 步骤合并中创建的 `Sasuser.Alldata` 数据集相同。

# 比较 DATA 步骤匹配合并与 PROC SQL 连接

## 概述

你已经看到通过 `DATA` 步骤匹配合并（match-merge）和 `PROC SQL` 内连接可以创建相同的结果。尽管结果可能是相同的，但这两个过程非常不同，选择其中一种方法而非另一种方法涉及权衡。下表总结了这两种方法的某些优缺点。

### 表 15.1 DATA 步骤匹配合并

| 优点 | 缺点 |
| --- | --- |
| <ul><li>输入数据集的数量没有限制。</li><li>通过使用 `DATA` 步骤处理（包括数组和 `DO` 循环）以及 `MERGE` 功能，可以将复杂的业务逻辑纳入新数据。</li><li>多个 `BY` 变量允许依赖于多个变量的查找。</li></ul> | <ul><li>数据集在合并之前必须按 `BY` 变量或变量进行排序或索引。</li><li>`BY` 变量或变量必须存在于所有数据集中，且键变量或变量的名称必须完全匹配。</li><li>必须找到键值或键值的精确匹配。</li></ul> |

### 表 15.2 PROC SQL 连接

| 优点 | 缺点 |
| --- | --- |
| <ul><li>数据集不需要排序或索引，但可以使用索引来提高性能。</li><li>可以在一个步骤中连接多个数据集，而无需在所有集中具有公共变量。</li><li>你可以使用合并后的数据创建数据集（表）、视图或报告。</li></ul> | <ul><li>一次可以连接的最大表数为为 256 个。</li><li>复杂的业务逻辑很难纳入连接中。</li><li>对于简单的连接，`PROC SQL` 可能比带有 `MERGE` 语句的 `DATA` 步骤需要更多资源。</li></ul> |

尽管通过 `DATA` 步骤匹配合并和 `PROC SQL` 连接可以产生相同的结果，但这两个过程默认并不总是产生相同的结果。考虑以下简化的示例以查看每种方法在各种情况下的工作原理。以下两个步骤显示了产生具有变量 `X` 的两个数据集 `Data1` 和 `Data2` 相同组合的两种不同方法。如果 `Data1` 包含两个变量 `X` 和 `Y`，而 `Data2` 包含两个变量 `X` 和 `Z`，那么以下两个步骤都会产生一个名为 `Data3` 的包含三个变量 `X`、`Y` 和 `Z` 的输出数据集。注意：以下两个步骤的代码说明了 `DATA` 步骤匹配合并与 `PROC SQL` 连接的简单比较。这种比较将在接几节中探讨。

```
data data3;
   merge data1 data2;
   by x;
run;

proc sql;
   create table data3 as
      select data1.x, data1.y, data2.z
         from data1, data2
         where data1.x=data2.x;
quit;
```

`Data3` 的内容取决于每个输入数据集中的值以及使用的合并方法。考虑以下示例。

## 示例





无论是在 `DATA` 步中合并数据集，还是在 `PROC SQL` 步中连接数据集，一对一匹配产生的结果都是相同的。假设 `Data1` 和 `Data2` 包含相同数量的观测值。同时，假设在每个数据集中 `X` 的值都是唯一的，且每个值在两个数据集中都出现。当这些数据集在 `DATA` 步中合并或在 `PROC SQL` 步中连接时，`Data3` 将为每个唯一的 `X` 值包含一个观测值，且其观测值数量与 `Data1` 和 `Data2` 相同。![Comparing DATA Step Match-Merges](img/m56-19-g1.png)

无论是在 `DATA` 步中合并数据集，还是在 `PROC SQL` 步中连接数据集，一对多匹配产生的结果都是相同的。假设 `Data1` 包含唯一的 `X` 值，但 `Data2` 并不包含唯一的 `X` 值。也就是说，`Data2` 包含多个条具有相同 `X` 值的观测值，因此其观测值数量多于 `Data1`。当这两个数据集在 `DATA` 步中合并或在 `PROC SQL` 步中连接时，`Data3` 的观测值数量与 `Data2` 相同。在 `Data3` 中，`Data1` 中具有特定 `X` 值的观测值可能会与 `Data2` 中多个具有相同 `X` 值的观测值匹配。![Comparing DATA Step Match-Merges](img/m56-19-g2.png)

多对多匹配产生的结果取决于数据集是在 `DATA` 步中合并还是在 `PROC SQL` 步中连接。假设 `Data1` 和 `Data2` 中的 `X` 值均不唯一。当数据集在 `DATA` 步中合并时，这些观测值是按顺序进行匹配和组合的。在下面的示例中，`Data3` 的观测值数量与两个输入集中数量较大的那个相同。在 `BY` 变量值上存在多对多匹配的情况下，`DATA` 步匹配合并可能不会产生预期的输出，因为输出数据集不会包含所有可能的匹配观测值组合。当数据集在 `PROC SQL` 步中连接时，每个匹配项都会作为输出数据集中的一个独立观测值出现。在下面的示例中，`Data1` 中 `X` 值为 `1` 的第一个观测值将与 `Data2` 中每个 `X` 值为 `1` 的观测值匹配并组合。然后，`Data1` 中 `X` 值为 `1` 的第二个观测值也将与 `Data2` 中每个 `X` 值为 `1` 的观测值匹配并组合，依此类推。![Comparing DATA Step Match-Merges](img/m56-20-g1.png)

数据集之间不匹配的数据产生的结果取决于数据集是在 `DATA` 步中合并，还是通过使用 `PROC SQL` 内连接进行组合。当包含不匹配 `BY` 变量值的数据集在 `DATA` 步中合并时，每个数据集中的观测值都按顺序进行处理。`Data3` 将为出现在 `Data1` 或 `Data2` 中的每个唯一的 `X` 值包含一个观测值。对于不匹配的 `X` 值，`Data3` 中的观测值在在来自另一个输入数据集的变量上将具有缺失值。在 `PROC SQL` 步中，输出数据集将仅包含 `BY` 变量具有匹配值的观测值。在下面的示例中，`Data3` 没有带有缺失值的观测值，因为来自 `Data1` 或 `Data2` 的任何包含不匹配 `X` 值的观测值都没有包含在 `Data3` 中。![Comparing DATA Step Match-Merges](img/m56-20-g2.png)

你已经在几个简单场景中看到了 `DATA` 步匹配合并和 `PROC SQL` 连接的结果。为了帮助你更全面地理解这些，请考虑 `DATA` 步如何处理匹配合并，以及 `PROC SQL` 如何处理连接。

## DATA Step Match-Merge

在 `DATA` 步中合并数据集时，每个输入数据集中的观测值被顺序读取，并在输出数据集中进行匹配和组合。下面的示例描述了两个简单输入数据集的 `DATA` 步匹配合并。

## Execution of a DATA Step Match-Merge

1. 此示例展示了下方 `DATA` 步的执行。该 `DATA` 步通过对两个输入数据集执行基础匹配合并创建一个新的数据集。

```sas
data work.data3;
   merge data1 data2;
   by x;
run;
```

2. 在编译阶段，SAS 读取输入数据集的描述部分，并默认创建一个包含来自每个输入数据集每个变量的 `PDV`。

3. 执行开始。SAS 检查每个输入数据集中的第一条观测值，以确定 `BY` 值是否匹配。如果是，SAS 将每个数据集的第一条观测值读取到 `PDV` 中。

4. SAS 将合并后的观测值写入输出数据集。

5. 如果 `BY` 值不匹配，SAS 将从 `BY` 值最低的输入数据集读取。如果 `BY` 值与上一个观测值的 `BY` 值匹配，则 SAS 不会重新初始化 `PDV`，而是覆盖 `PDV` 中的值。如果 `BY` 值与上一个 `BY` 值不匹配，则 SAS 会初始化 `PDV`。此时，`PDV` 和输出数据集对于另一个数据集特有的变量将包含缺失值。

6. SAS 继续匹配合并观测值，直到所有输入数据集的所有观测值都被读取并写入新数据集。在此示例中，`Work.Data3` 包含三个变量和四个观测值。

## PROC SQL Join

`PROC SQL` 连接使用与 `DATA` 步合并不同的过程来组合表。概念上，`PROC SQL` 首先创建所有输入表的笛卡尔积。也就是说，`PROC SQL` 首先将每行与每行匹配。

## Execution of a PROC SQL Join

1. 此示例展示了下方 `DATA` 步的执行。（注：此处应指 `PROC SQL`）。该 `PROC SQL` 步创建一个新表来存储两个输入表之间内连接的结果。

```sas
proc sql;
   create table work.data3 as
      select *
        from data1, data 2
        where data1.x=data2.x;
quit;
```

2. 概念上，`PROC SQL` 首先创建所有输入表的笛卡尔积。也就是说，`PROC SQL` 首先将每行与每行匹配。

3. 然后，`PROC SQL` 消除结果集中任何不满足 `WHERE` 子句的观测值。





## 示例：合并多对多匹配的数据

假设你想合并来自 `Sasuser.Flightschedule` 和 `Sasuser.Flightattendants` 的数据。`Sasuser.Flightschedule` 数据集包含某家虚构航空公司已安排的航班数据。`Sasuser.Flightattendants` 数据集包含该虚构航空公司乘务服务员的信息。下面显示这两个数据集的各个部分列表。

表 15.3 `Sasuser.Flightschedule`（部分列表）

| Date | Destination | FlightNumber | EmpID |
| --- | --- | --- | --- |
| 01MAR2000 | YYZ | 132 | 1739 |
| 01MAR2000 | YYZ | 132 | 1478 |
| 01MAR2000 | YYZ | 132 | 1130 |
| 01MAR2000 | YYZ | 132 | 1390 |
| 01MAR2000 | YYZ | 132 | 1983 |
| 01MAR2000 | YYZ | 132 | 1111 |
| 01MAR2000 | YYZ | 182 | 1076 |
| 01MAR2000 | YYZ | 182 | 1118 |

表 15.4 `Sasuser.Flightattendants`（部分列表）

| EmpID | JobCode | LastName | FirstName |
| --- | --- | --- | --- |
| 1350 | FA3 | Arthur | Barbara |
| 1574 | FA2 | Cahill | Marshall |
| 1437 | FA3 | Carter | Dorothy |
| 1988 | FA3 | Dean | Sharon |
| 1983 | FA2 | Dunlap | Donna |
| 1125 | FA2 | Eaton | Alicia |
| 1475 | FA1 | Fields | Diana |
| 1422 | FA1 | Fletcher | Marie |

假设你想将 `Sasuser.Flightschedule` 数据集中的所有变量与安排在每个航班上的每个乘务服务员的姓和名合并。`Sasuser.Flightschedule` 包含 45 个航班的数据。每个航班安排了 3 名乘务服务员工作。因此，你的输出数据集应该包含 135 条观测值（每个航班三个）。你可以使用以下 `PROC SQL` 步骤来合并 `Sasuser.Flightschedule` 和 `Sasuser.Flightattendants`。

```
proc sql;
   create table flightemps as
      select flightschedule.*, firstname, lastname
         from sasuser.flightschedule, sasuser.flightattendants
            where flightschedule.empid=flightattendants.empid;
quit;
```

生成的 `Flightemps` 数据集包含 135 条观测值。现在，假设你使用以下 `DATA` 步匹配合并（match-merge）来合并这两个数据集。

```
proc sort data=sasuser.flightattendants out=fa;
   by empid;
run;

proc sort data=sasuser.flightschedule out=fs;
   by empid;
run;

data flightemps2;
   merge fa fs;
   by empid;
run;
```

生成的 `Flightemps2` 数据集包含 272 条观测值。`DATA` 步匹配合并没有产生正确的结果，因为它是顺序合并数据的。在正确的结果中，来自 `Sasuser.Flightschedule` 的每个唯一航班对应三条观测值，且任何观测值中均没有缺失值。相比之下，`DATA` 步匹配合并的结果每个唯一航班包含六条观测值，并且许多观测值具有缺失值。在最后一个例子中，数据是从两个具有多对多匹配的数据集合并的。`PROC SQL` 产生产生了正确的结果，但 `DATA` 步匹配合并没有。然而，你可以在 `DATA` 步中产生正确的结果。首先，考虑使用多个 `SET` 语句来合并数据。

## 使用多个 SET 语句

你可以使用多个 `SET` 语句合并来自多个 SAS 数据集的观测值。例如，以下 `DATA` 步创建了一个名为 `Combine` 的新数据集。`Combine` 中的每个观测值包含来自 `Dataset1` 中一条观测值的数据以及 `Dataset2` 中一条观测值的数据。

```
data combine;
   set dataset1;
   set dataset2;
run;
```

当你使用多个 `SET` 语句时，会发生以下结果：

* 当当 SAS 遇到任一数据集的文件结束（EOF）标记时，处理停止（即使另一个数据集还有更多数据）。因此，输出数据集的观测值数量与最小的输入数据集相同。
* 当执行第二个 `SET` 语句时，程序数据向量 (`PDV`) 中的变量不会被重新初始化。
* 对于两个输入数据集共有的任何变量，第二个 `SET` 语句数据集中的值或多个值将覆盖 PDV 中第一个 `SET` 语句数据集的值或多个值。

请记住，使用多个 `SET` 语句合并没有一对一匹配的多个输入源的数据可能是复杂的。如果你处理的数据源没有一对一匹配，或者包含不匹配的数据，你将需要添加额外的 `DATA` 步语法以产生你想要的结果。

## 示例：在多对多匹配中使用多个 SET 语句

回记得，在上一个例子中，你想合并 `Sasuser.Flightschedule` 和 `Sasuser.Flightattendants`。你的生成数据集应该包含 135 条观测值。你可以使用以下 `DATA` 步来执行此操作。

```
data flightemps3(drop=num);
   set sasuser.flightschedule;
   do i=1 to num;
      set sasuser.flightattendants;
      if empid=empid then output;
   end;
run;
```





| JAN1999 | $280,350,393.00 | 1 | $8,593,432,002.35 | |

```
<RevCargo/Cargosum>
```

| FEB1997 | $177,671,530.40 | 2 | $8,593,432,002.35 | |

```
<RevCargo/Cargosum>
```

| FEB1998 | $215,959,695.50 | 2 | $8,593,432,002.35 | |

```
<RevCargo/Cargosum>
```

| FEB1999 | $253,999,924.00 | 2 | $8,593,432,002.35 | |

```
<RevCargo/Cargosum>
```

我们将更仔细地检查此任务。

# MEANS 过程

你应该已经知道如何使用 `MEANS` 过程来生成汇总统计。默认情况下，`PROC MEANS` 会生成一个包含描述性统计的报告。可以使用 `OUTPUT` 语句将描述性统计重定向到 SAS 数据集中。可以使用 `NOPRINT` 选项抑制默认报告。

带有 `OUTPUT` 语句的 `PROC MEANS` 通用形式：
`PROC MEANS DATA=input-SAS-data-set NOPRINT;<VAR variable(s);>OUTPUT OUT= output-SAS-data-set statistic=output-variable(s);RUN;`

以下是对语法的解释：
`input-SAS-data-set` 识别生成汇总统计的数据集。
`variable(s)` 是正在分析的变量或多个变量的名称。
`output-SAS-data-set` 命名存储描述性统计的数据集。
`statistic` 是生成的汇总统计量之一。
`output-variable(s)` 命名在输出数据集中存储 `statistic` 值或多个值的变量或多个变量。

`PROC MEANS` 步骤创建的输出数据集包含请求的统计值作为 `output-variable(s)` 的值，以及自动包含的两个额外变量，如下：

- `_TYPE_` 包含关于类变量的信息
- `_FREQ_` 包含一个输出级别代表的观测值数量

## 示例

以下程序创建了一个名为 `Sasuser.Summary` 的汇总数据集。`Sasuser.Summary` 包含来自 `Sasuser.Monthsum` 的 `Revcargo` 值的和，存储在变量 `Cargosum` 中。

```
proc means data=sasuser.monthsum noprint;
   var revcargo;
   output out=sasuser.summary sum=Cargosum;
run;

proc print data=sasuser.summary;
run;
```

由于使用了 `NOPRINT` 选项，`PROC MEANS` 步骤不会产生报告。打印 `Sasuser.Summary` 数据集产生如下报告。![Comparing DATA Step Match-Merges](img/m56-28-g1.png) 一旦创建了汇总统计，你就将此汇总信息与数据集的详细行结合，以便计算百分比。记住你可以使用多个 `SET` 语句来水平合并数据。考虑通过使用多个 `set` 语句将 `Sasuser.Monthsum` 的详细行与我们在 `Sasuser.Summary` 中创建的汇总数据相结合，了解此过程是如何工作的。

## 示例

此示例创建了一个名为 `Percent1` 的新数据集，它结合了：

- 来自 `Sasuser.Summary` 的汇总数据（三年期货运总收入）
- 来自 `Sasuser.Monthsum` 的详细数据（月份和该月总货量）

`Percent1` 还包含一个名为 `PctRev` 的新变量，记录每个观测值所占总收入的计算百分比。记住自动变量 `_N_` 跟踪 `DATA` 步骤迭代的次数。以下 `DATA` 步骤使用 `_N_` 防止 SAS 在该步骤第一次迭代后到达 `Sasuser.Summary` 的文件末尾。由于从 SAS 数据集读取的变量不会重新初始化，因此在从 `Sasuser.Monthsum` 读取每个观测值时，`Cargosum` 的值会保留在 PDV（程序数据向量）中。

1. 此示例显示了下方 `DATA` 步骤的编译和执行。此 `DATA` 步骤创建了一个新数据集，结合了来自一个输入数据集（`Sasuser.Summary`）的汇总数据和来自第二个输入数据集（`Sasuser.Monthsum`）的详细数据。

```
data sasuser.percent1(drop=cargosum);
   if _N_=1 then set sasuser.summary(keep=cargosum);
   set sasuser.monthsum(keep=salemon revcargo);
   PctRev=revcargo/cargosum;
run;
```

2. 在编译阶段，SAS 读取输入数据集的描述部分并创建 PDV。`_N_` 是 PDV 中的一个临时变量，尽管它不会包含在输出集中。

3. 开始执行。在 `DATA` 步骤的第一次迭代中，`_N_` 的值为 1。`IF` own 语句为真，因此第一个 `SET` 语句从 `Sasuser.Summary` 将 `Cargosum` 的值读入 PDV。

4. 第二个 `SET` 语句将 `Sasuser.Monthsum` 中的第一个观测值读入 PDV。

5. SAS 计算 `PctRev` 的值并记录在 PDV 中。

6. 在 `DATA` 步骤的底部，SAS 将 PDV 中的值写入输出数据集。`_N_` 是临时变量，并从输出集中丢弃。

7. 在 `DATA` 步骤的第二次迭代中，`_N_` 为 2，因此 `IF` 语句为假，第一个 `SET` 语句不执行。然而，`Cargosum` 的值保留在 PDV 中。

8. 第二个 `SET` 语句将 `Sasuser.Monthsum` 中的第二个观测值读入 PDV。

9. 计算并记录 PDV 中的 `PctRev` 的值。SAS 将 PDV 中的值写入输出数据集（`_N_` 除外）。

10. `DATA` 步骤继续执行，直到从 `Sasuser.Monthsum` 读取了所有观测值。

11. 结合汇总数据和详细数据的另一种方法是在同一个 `DATA` 步骤中创建汇总统计并将其结合。这样做你需要：

- 一次读取数据并计算汇总统计
- 再次读取数据以结合汇总统计

## Sum 语句

你可以使用和语句在 `DATA` 步骤中获取汇总统计。和语句将表达式的结果加到累加变量上。

通用形式，和语句：`variable+expression;`

以下是对语法的解释：
`variable` 指定累加变量的名称。该变量必须是数值型的。在读取第一个观测值之前，该变量会被设置为 0。该变量在每次迭代之间保留。
`expression` 是任何数值表达式。

注意：如果表达式产生缺失值，和语句会忽略它。这与表达式产生缺失值时分配缺失值的赋值语句不同。注意：和语句和赋值语句是少数不以关键字开头的 SAS 语句。

和语句将加号（+）右侧表达式的结果加上加号左侧的数值变量。在 `DATA` 步骤的顶部，数值变量的值不像通常读取原始数据那样被设置为缺失。相反，该变量在程序数据向量中保留新值，以便处理下一个观测值。

## 示例

此示例使用和语句在 `DO UNTIL` 循环中生成汇总统计。在 `DATA` 步骤的第一次迭代中，`DO UNTIL` 循环读取 `Sasuser.Monthsum` 的每个观测值，并对每个观测值的 `RevCargo` 总进行进行累加。在 `DATA` 步骤的后续每次迭代中，此累加值（存储在变量 `TotalRev` 中）除以 `RevCargo` 以计算新变量 `PctRev`。注意：记住 `set` 语句选项 `END=` 创建了一个包含文件结束指示器的临时变量。





```
data sasuser.percent2(drop=totalrev);
   if _N_=1 then do until (LastObs);
      set sasuser.monthsum(keep=revcargo) end=lastobs;
      TotalRev+revcargo;
   end;
   set sasuser.monthsum(keep=salemon revcargo);
   PctRev=revcargo/totalrev;
run;
```

2. 在编译阶段，SAS 读取输入数据集的描述部分并创建 PDV。`_N_`、`LastObs` 和 `TotalRev` 是包含在 PDV 中但不会写入输出数据集的临时变量。

3. 执行开始。临时变量被初始化为值。`IF` 语句在 `DATA` 步的第一次迭代中为真，因此 `DO UNTIL` 循环开始执行。请记住，在 `DO UNTIL` 循环中，条件是在循环底部评估的。

4. 第一个 `SET` 语句从 `Sasuser.Monthsum` 中读取第一个观测值，并将 `RevCargo` 的值写入 PDV。

5. `TotalRev` 的值增加了 `RevCargo` 的值，并在 PDV 中被覆盖。

6. 在 `DO` 循环底部，SAS 评估 `UNTIL` 表达式。由于 `LastObs` 的值为 `0`，该表达式为假，因此循环继续执行。

7. 第一个 `SET` 语句从 `Sasuser.Monthsum` 读取第二个观测值，覆盖 PDV 中 `RevCargo` 的值，并将此值加到累加变量 `TotalRev`。

8. `DO UNTIL` 循环继续执行，直到第一个 `SET` 语句从 `Sasuser.Monthsum` 读取最后一个观测值，且 `LastObs` 的值被设置为 `1`。此时，PDV 中 `TotalRev` 的值是 `Sasuser.Monthsum` 中所有 `RevCargo` 值的和。循环满足条件。

9. 第二个 `SET` 语句读取与第一个 `SET` 语句相同的数据。然而，这次 `SaleMon` 和 `RevCargo` 被读入 PDV。`TotalRev` 在 PDV 中保持填充状态。

10. 为观测值 1 计算 `PctRev` 并记录在 PDV 中。然后，SAS 将 PDV 中的值写入输出数据集 `Sasuser.Percent2`，临时变量和 `TotalRev` 变量除外。

11. 在 `DATA` 步的第二次迭代中，`_N_` 的值增加到 `2`，因此 `IF` 表达式为假。第二个 `SET` 语句从 `Sasuser.Monthsum` 的第二个观测值读取到 PDV。

12. 累加变量 `TotalRev` 的值保留自上次迭代，并用于计算 `PctRev` 的新值，结果记录在 PDV 中。SAS 将 PDV 中的值写入输出数据集。

13. `DATA` 步一直迭代到 `Sasuser.Monthsum` 的文件末尾。

# 使用索引合并数据

## 概述

假设你想从两个数据集合并数据，且其中一个数据集比另一个大得多。同时，假设你只想从较大的数据集中选择那些根据一个或多个公共变量的值、与较小数据集中的观测值匹配的观测值。你应该已经知道如何在 SAS 数据集上创建索引。你已经学习过 `PROC SQL` 可以利用索引提高连接的性能。你也可以在 `DATA` 步中利用索引来合并来自多个数据集中匹配观测值的数据，如果该索引是建立在所有输入数据集共有的变量上的。例如，假设你想合并来自 `Sasuser.Dnunder` 和 `Sasuser.Sale2000` 匹配观测值的数据。`Sasuser.Sale2000`（包含 156 个观测值）中的航班只有一部分也存在 `Sasuser.Dnunder`（仅包含 57 个观测值）。假设你只想选择匹配的观测值。假设 `Sasuser.Sale2000` 关联有一个名为 `Flightdate` 的复合索引。`Flightdate` 的值是唯一的，并且基于 `FlightID` 和 `Date` 变量的值。你可以使用 `FLIGHTDATE` 索引通过直接访问高效地仅选择匹配的观测值![使用索引合并数据](img/m56-36-g1.png) 接下来的几个章节将展示如何使用 `Flightdate` 索引合并来自 `Sasuser.Sale2000` 数据集和 `Sasuser.Dnunder` 数据集的匹配观测值。

## KEY= 选项

你已经看到如何在 `DATA` 步中使用多个 `SET` 语句以便在新数据集中合并汇总数据和详细数据。你也可以使用多个 `SET` 语句只读取匹配的观测值。你在 `SET` 语句中指定 `KEY=` 选项来使用索引从查找数据检索匹配的观测值。

`KEY=` 选项的 `SET` 语句的标准形式：`SET SAS-data-set-name KEY= index-name;` 语法解释：`index-name` 是与 `SAS-data-set-name` 数据集关联的索引名称。

使用带有 `KEY=` 选项的 `SET` 语句执行查找操作所需的值必须存储在具有索引的 SAS 数据集中。这种技术适用于当你处理一对一匹配，且查找表大小任意时。当遇到带有 `KEY=` 选项的 `SET` 语句时，SAS 使用索引从查找数据集中检索匹配观测值。这种技术可以结合其他 `DATA` 步语法来返回多个值。例如，如果 `Sasuser.Sale2000` 数据集有一个名为 `Flightdate` 的索引，后续 `SET` 语句使用 `Flightdate` 索引来定位：

```sas
set sasuser.sale000 key=flightdate;
```

当该 `SET` 语句开始执行时，PDV 中必须已经 `FlightID` 的值和 `Date` 的值。SAS 然后使用 `Flightdate` 索引从 `Sasuser.Sale000` 获取观测值。为了在执行带有 `KEY=` 选项的 `SET` 语句之前在 PDV 中分配键值，需要在该语句之前使用另一个 `SET` 语句。

## 示例

记住你想合并 `Sasuser.Sale2000` 和 `Sasuser.Dnunder`，并且 `Sasuser.Sale2000` 有一个基于 `FlightID` 和 `Date` 值的索引 `Flightdate`。你可以使用两个 `SET` 语句合并这两个数据集，并在第二个 `SET` 语句中使用 `KEY=` 选项来利用索引。在以下示例中，发生了这些结果：

* 第一个 `SET` 语句从 `Sasuser.Dnunder` 数据集顺序读取观测值。SAS 将该观测值的值写入 PDV，然后移动到第二个 `SET` 语句。
* 第二个 `SET` 语句使用 `Sasuser.Sale2000` 上的 `Flightdate` 索引在 `Sasuser.Sale2000` 中查找一个观测值，其 `FlightID` 和 `Date` 的值与第一个 `SET` 语句填充的值匹配。
* `Work.Profit` 是输出数据集。

注意：如果你使用 `KEY=` 选项读取 SAS 数据集，则在同一个 `DATA` 步中无法对该数据集使用 `WHERE` 处理。

1. 此示例展示了 `DATA` 步的执行，该步使用两个 `SET` 语句从两个输入数据集（`Sasuser.Sale2000` 和 `Sasuser.Dnunder`）合并到一个输出数据集（`Work.Profit`）。`DATA` 步使用较大的输入数据集之一 `Sasuser.Sale2000` 的索引来查找匹配的观测值。

```sas
data work.profit;
   set sasuser.dnunder;
   set sasuser.sale2000(keep=routeid flightid date rev1st
                        revbusiness revecon revcargo)
                        key=flightdate;
   Profit=sum(rev1st, revbusiness, revecon, revcargo,
                 -expenses);
run;
```

2. SAS 读取输入数据集描述部分并创建 PDV。

3. 第一个 `SET` 语句执行并创建 PDV。SAS 将 `Sasuser.Dnunder` 中的第一个观测值读入 PDV。





4. 当第二个 `SET` 语句执行时，`KEY=` 选项使用 `Flightdate` 索引直接访问 `Sasuser.Sale2000` 中的观测值，该观测值中的 `FlightID` 和 `Date` 必须与 PDV 中已有的值相匹配。随后，将匹配的观测值读入 PDV 中。

5. SAS 计算 `Profit` 的值并将其记录在 PDV 中。然后，SAS 将 PDV 中的当前观测值写入输出数据集。

6. `DATA` 步继续迭代。只有 `Profit` 变量被重新初始化为缺失值。第一个 `SET` 语句将 `Sasuser.Dnunder` 中的第二个观测值读入 PDV，覆盖了之前的值。

7. 第二个 `SET` 语句使用 `Flightdate` 索引在 `Sasuser.Sale2000` 中寻找匹配的观测值。匹配的观测值被读入 PDV，覆盖了之前的值。计算并记录 `Profit` 的新值。将当前观测值写入输出数据集。

8. `DATA` 步继续迭代，直到到达 `Sasuser.Dnunder` 的文件末尾。

记住，当 SAS 遇到带有 `KEY=` 选项的 `SET` 语句时，构建 `KEY=` 索引的关键变量必须已经存在于 PDV 中。因此，这两个 `SET` 语句按照所示精确顺序排列重要。

## 示例

如果你仔细检查 `Work.Profit` 输出数据集，你会发现输出数据集中的最后一个观测值包含的几个变量的值与上一个观测值的值相同。这种情况发生在第二个 `SET` 语句未能在 `sasuser.sale2000` 中找到匹配的观测值时。包含不匹配数据的观测值会被打印到日志中。如下方的日志示例所示，不匹配的观测值包含一个 `_Error_` 变量，其值为 `1`，表示数据不匹配。`_N_` 变量表示发生错误的 `DATA` 步的迭代次数。

表 15.8 SAS 日志

| |

```
FlightID=IA11802 RouteID=0000108 Date=30DEC2000 Expenses=3720
Rev1st=1270 RevBusiness=. RevEcon=5292 RevCargo=1940 Profit=4782

_ERROR_=1 _IORC_=1230015 _N_=57
NOTE: There were 57 observations read from the data set
      SASUSER.DNUNDER.
NOTE: The data set WORK.PROFIT has 57 observations and 9 variables.
NOTE: DATA statement used (Total process time):
      real time           0.38 seconds
      cpu time            0.04 seconds
```

| |

注意，在 SAS 日志中打印的观测值也包含一个名为 `_IORC_` 的变量。

## `_IORC_` 变量

使用 `KEY=` 选项时，SAS 会创建一个名为 `_IORC_` 的自动变量，代表输入/输出返回代码（INPUT/OUTPUT Return Code）。你可以使用 `_IORC_` 判断索引搜索是否成功。如果 `_IORC_` 的值为零，则 SAS 找到了匹配的观测值。如果 `_IORC_` 的值不零，则 SAS 未找到匹配的观测值。为了防止将数据错误写入日志（以及你的输出数据集），请执行以下操作：

* 检查 `_IORC_` 的值以确定是否找到匹配
* 如果没有匹配，将 `_ERROR_` 设置为 `0`
* 删除不匹配的数据或将不匹配的数据写入错误数据集

## 示例

以下示例使用 `Flightdate` 索引将 `Sasuser.Sale2000` 的数据与 `Sasuser.Dnunder` 的数据合并，并将合并后的数据写入名为 `Work.Profit3` 的新数据集。不匹配的观测值被写入 `Work.Errors`。不应该有观测值写入 SAS 日志。

```
data work.profit3 work.errors;
   set sasuser.dnunder;
   set sasuser.sale2000(keep=routeid flightid date rev1st
       revbusiness revecon revcargo)key=flightdate;
   if _iorc_=0 then do;
      Profit=sum(rev1st, revbusiness, revecon, revcargo,
            -expenses);
      output work.profit3;
   end;
   else do;
      _error_=0;
      output work.errors;
   end;
run;
```

如果你检查上述程序的运行结果，你会发现 `Work.Profit3` 输出数据集中的观测值比 `Work.Profit` 输出数据集少一个。不匹配的观测值被写入了 `Work.Errors` 数据集。

# 使用事务数据集

## 概述

有时，你可能不仅仅是合并两个数据集的数据，而是想用另一个数据集中存储的数据来更新一个数据集中的数据。也就是说，你可能想用事务数据集中的值覆盖某些值来更新主数据集。例如，假设数据集 `Mylib.Empmaster` 包含过的数据。当前数据存储在另一个名为 `Mylib.Empchanges` 的数据集中`Mylib.Empmaster` 包含 148 个观测值，而 `Mylib.Empchanges` 包含 6 个观测值。变量 `EmpID` 在两个数据集中都包含唯一值。`Mylib.Empmaster` 的部分列表和 `Mylib.Empchanges` 的完整列表所示。注意，在两个数据集中，有一个观测值具有相同的 `EmpID` 值为 `165`（此处）。对于这些观测值，`JobCode` 和 `Salary` 的值是不同的。

表 15.9 `Mylib.Empmaster`（部分列表）

| DateOfBirth | DateOfHire | EmpID | Gender | JobCode |
| :--- | :--- | :--- | :--- | :--- |
| --- | --- | --- | --- | --- |
| 30JUN1955 | 31JAN1982 | 1639 | F | TA3 |
| 29JAN1942 | 10JAN1985 | 1065 | M | ME2 |
| 03DEC1961 | 10Oct1985 | 1561 | M | TA3 |
| 25SEP1965 | 07OCT1989 | 1221 | F | FA3 |
| 11AUG1970 | 01NOV2000 | 1447 | F | FA1 |
| 13SEP1968 | 05NOV2000 | 1998 | M | SCP |

表 15.10 `Mylib.Empchanges`

| DateOfBirth | DateOfHire | EmpID | Gender | JobCode | Salary |
| :--- | :--- | :--- | :--- | :--- | :--- |
| --- | --- | --- | --- | --- | --- |
| 05MAR1957 | 30MAR1990 | 1009 | M | TA1 | |
| 23MAY1963 | 20OCT1979 | 1017 | M | TA3 | |
| 14APR1962 | 17SEP1990 | 1037 | F | TA3 | |
| 17JUL1967 | 26NOV1989 | 1038 | F | TA1 | |
| 11JUL1961 | 27AUG1984 | 1050 | M | ME2 | |
| 29JAN1942 | 10JAN1985 | 1065 | M | ME2 | |

如果你能看到 `Mylib.Empmaster` 的完整列表，你会发现 `Mylib.Empchanges` 中的每个观测值在 `Mylib.Empmaster` 中都有基于 `EmpID` 的匹配观测值。`Mylib.Empmaster` 中还有许多观测值在 `Mylib.Empchanges` 中没有匹配的观测值。为了更新 `Mylib.Empmaster`，你需要找到所有匹配的观测值，并用 `Mylib.Empchanges` 中的新值更新它们的 `JobCode` 和 `Salary`。你可以使用 `UPDATE` 语句进行这些更改。

## UPDATE 语句

使用 `UPDATE` 语句通过事务数据集更新主数据集。`UPDATE` 语句可以执行以下任务：

* 修改主集中变量的值
* 向数据集添加观测值
* 向数据集添加变量

| `UPDATE` 语句的通用形式：`DATA master-data-set; UPDATE master-data-set transaction-data-set; BY by-variable(s); RUN;` 以下是对语法的解释：`master-data-set` 指定主文件的 SAS 数据集。`transaction-data-set` 指定要应用到主数据集的更改的 SAS 数据集。`by-variable(s)` 指定同时出现在 `master-data-set` 和 `transaction-data-set` 中的变量。`master-data-set` 中的每个观测值对于 `by-variable` 必须是唯一的，但 `transaction-data-set` 可以包含多个具有相同 `by-variable` 值的观测值。 |





`UPDATE` 语句根据每个 `BY` 变量值匹配的观测值，将主数据集中的值替换为来自事务数据集的值。在主数据集或事务数据集中，任何 `BY` 变量值不匹配的观测值都将包含在输出数据集中。此外，默认情况下，如果事务数据集中中的现有值被编码为点（针对数值型变量）或空格（针对字符型变量），SAS 不会将主数据集中的现有值替换为缺失值。当您使用 `UPDATE` 语句时，请记住以下限制：

-   `UPDATE` 语句中最多可以出现两个数据集名称。
-   主数据集必须列在第一个。
-   必须使用指定匹配变量的 `BY` 语句。
-   两个数据集都必须按 `BY` 变量排序，或具有基于 `BY` 变量的索引。
-   在主数据集中，每个观测值的 `BY` 变量值必须是唯一的。

## 示例

请记住，您想要用事务数据集 `Mylib.Empchanges` 更新主数据集 `Mylib.Empmaster`。您可以像下面的程序所示，使用 `UPDATE` 语句完成此任务。记住，两个数据集都必须按 `BY` 变量排序或对其建立索引。

```
proc sort data=mylib.empmaster;
   by empid;
run;

proc sort data=mylib.empchanges;
   by empid;
run;

data mylib.empmaster;
   update mylib.empmaster mylib.empchanges;
   by empid;
run;
```

更新后的 `Mylib.Empmaster` 数据集的前八个观测值如下所示。请注意，`EmpID` 值为 `1065` 的观测值现在包含了 `JobCode` 和 `Salary` 的更新值。

```
 proc print data=mylib.empmaster (obs=8) noobs;
run;
```

![使用事务数据集](img/m56-46-g1.png)

## 总结

## 文本总结

### 复习术语

您可以回顾本章中重要术语的定义。您还可以回顾表查找操作中各种输入源之间各种关系的图表和描述。

### 在 SAS 数据集外部处理查找值

您可以在 `DATA` 步中使用 `IF-THEN/ELSE` 语句将基表数据与未存储在 SAS 数据集中的查找值合并。您还可以使用 `FORMAT` 过程或 `ARRAY` 语句将基表数据与未存储在 SAS 数据集中的查找值合并。

### 使用 DATA Step Match-Merge 合并数据

您可以在 `DATA` 步中使用 `MERGE` 语句合并多个数据集的数据，只要这些输入数据集具有公共变量。如果每个输入数据集至少包含一个与至少另一个数据集相同的变量，则您可以在多个 `DATA` 步中合并两个缺少公共变量的数据集。

### 使用 PROC SQL 链接数据

如果没有所有输入表共有的单个列，您也可以使用 `PROC SQL` 来连接来自多个表的数据。如果您在 `PROC SQL` 步中创建一个带有内连接（inner join）结果的新表，其结果与 `DATA` 步 match-merge 的结果非常相似。

### 比较 DATA Step Match-Merge 和 PROC SQL Join

通过基础的 `DATA` 步 match-merge 和 `PROC SQL` 连接可以创建相同的结果。然而，这两种方法之间存在显著差异，并且各自有优缺点。在某些情况下，例如当输入数据集中的 `BY` 变量值存在一对一或一对多的匹配时，这两种方法会产生相同的结果。在其他情况下，例如当 `BY` 变量值存在多对多的匹配，或者存在 `BY` 变量的不匹配值时，这两种方法会产生不同的结果。这些差异反映了 `DATA` 步 match-merge 和 `PROC SQL` 连接的处理方式不同。即使处理多对多匹配或不匹配的数据，也可以其他的 `DATA` 步技术（例如多个 `SET` 语句）创建与 `PROC SQL` 步创建相同的结果。

### 合并汇总数据和详细数据

为了执行诸如根据数据的汇总统计量计算数据单个值百分比等任务，您需要合并汇总数据和详细数据。创建汇总数据集的一种方法是使用 `PROC MEANS`。一旦有了汇总数据集，您可以使用多个 `SET` 语句将汇总数据与原始数据集中的详细数据合并。还可以在一个 `DATA` 步中使用 `sum` 语句创建汇总数据并将其与详细数据合并。

### 使用索引合并数据

如果索引是基于所有输入数据集共有的变量构建的，则可以使用索引合并多个数据集中匹配观测值的数据。特别是当一个输入数据集非常大时，索引可以提高合并效率。您可以使用 `SET` 语句中的 `KEY=` 选项并结合另一个 `SET` 语句来使用索引合并数据。可以使用 `_IORC_` 变量来防止不匹配的数据包含在输出数据集中。

### 使用事务数据集

有时，您可能用存储在另一个数据集中的数据更新一个数据集的数据。您使用 `UPDATE` 语句根据每个 `BY` 变量值匹配的观测值，将主数据集中的值替换为来自事务数据集的值。

## 示例

### 使用 IF-THEN/ELSE 语句合并数据

```
data mylib.employees_new;
   set mylib.employees;
   if salary > 50000 then status = 'High';
   else status = 'Low';
run;
```

### 使用 ARRAY 语句合并数据

```
data mylib.employees;
   array scores[3] score1 score2 score3;
run
```

### 使用 FORMAT 过程合并数据

```
proc format;
   value status_fmt
   1-5 = 'Low'
   6-high = 'High';
run;
```

### 执行 DATA Step Match-Merge

```
proc sort data=sasuser.expenses out=expenses;
   by flightid date;
run;

proc sort data=sasuser.revenue out=revenue;
   by flightid date;
run;

data revexpns (drop=rev1st revbusiness reconcon)
     expenses);
   merge expenses(in=e) revenue(in=r);
   by flightid date;
   if e and r;
   Profit=sum(rev1st, revbusiness, recon,
          -expenses);
run;
```

### 执行 PROC SQL Join

```
proc sql;
   create table sqljoin as
   select revenue.flightid,
          revenue.date format=date9.,
          revenue.origin, revenue.dest,
          sum(revenue.rev1st,
              revenue.revbusiness,
               revenue.reconcon)
          -expenses.expenses as Profit,
          acities.city, acities.name
   from sasuser.expenses, sasuser.revenue,
        sasuser.acities
   where expenses.flightid=revenue.flightid
         and expenses.date=revenue.date
         and acities.code=revenue.dest
   order by revenue.dest, revenue.flightid,
            revenue.date;
quit;
```





```sas
proc means data=sasuser.monthsum noprint;
   var revcargo;
   output out=sasuser.summary sum=Cargosum;
run;

data sasuser.percent1;
   if _n_=1 then set sasuser.summary
                     (keep=cargosum);
   set sasuser.monthsum
       (keep=salemon revcargo);
   PctRev=revcargo/cargosum;
run;

data sasuser.percent2(drop=totalrev); 
   if _n_=1 then do until(lastobs); 
      set sasuser.monthsum(keep=revcargo) 
          end=lastobs; 
      totalrev+revcargo; 
   end; 
   set sasuser.monthsum (keep=salemon revcargo);
   PctRev=revcargo/totalrev;
run;
```

### 使用索引合并数据

```sas
data work.profit work.errors;
   set sasuser.dnunder;
   set sasuser.sale2000(keep=routeid
       flightid date rev1st revbusiness
       revecon revcargo)key=flightdate;
   if _iorc_=0 then do;
      Profit=sum(rev1st,business, revecon,
             revcargo, -expenses);
      output work.profit;
   end;
   else do;
      _error_=0;
      output work.errors;
   end;
run;
```

### 使用事务数据集

```sas
proc sort data=mylib.empmaster;
   by empid;
run;

proc sort data=mylib.empchanges;
   by empid;
run;

data mylib.empmaster;
   update mylib.empmaster mylib.empchanges;
   by empid;
run;
```

## 注意事项

- 在 `DATA` 步的匹配-合并（match-merge）中，你可以使用 `RENAME=` 为输入数据集中的相同变量赋予相同的名称，前提是这些变量包含相同的数据且具有相同的类型和长度。
- 你可以使用 `OUTPUT` 语句和配合 `MEANS` 过程的 `NOPRINT` 选项将统计数据路由到输出数据集，并抑制默认报告。
- 自动变量 `_N_` 跟踪 `DATA` 步迭代的次数。当将汇总数据集的数据与较大的详细数据集的数据合并时，`_N_` 变量非常有用。
- 当你使用 `UPDATE` 语句时，两个数据集都必须根据 `BY` 变量排序或具有基于 `BY` 变量的索引。

# Quiz

为每个问题选择最佳答案。完成测试后，请使用附录中的答案对照检查你的答案。

1. 根据下方的数据集描述，列出的变量中哪些变量符合 `DATA` 步匹配-合并的 BY 变量条件？
![Variable Type Length](img/m56-49-g2.png)![Variable Type Length](img/m56-49-g3.png)

    1. `Code` 和 `IDnum`
    2. `Manager` 和 `Supervisor`
    3. `Manager` 和 `IDnum`
    4. 这两个数据集之间没有共同变量。

2. 假设你想合并 `Dataset1`、`Dataset2` 和 `Dataset3`。同时假设 `Dataset1` 和 `Dataset2` 有共同变量 `Startdate`，`Dataset2` 和 `Dataset3` 有共同变量 `Instructor`，并且这些数据集没有其他共同变量。你如何使用 `DATA` 步将这三个数据集合并为一个新的数据集？

    1. 你在一个 `DATA` 步中使用 `MERGE` 语句，通过 `Startdate` 和 `Instructor` 合并 `Dataset1`、`Dataset2` 和 `Dataset3`。
    2. 你通过 `Startdate` 对 `Dataset1` 和 `Dataset2` 进行排序，并在 `DATA` 步中将它们合并到一个临时数据集。然后，你通过 `Instructor` 对该临时数据集和 `Dataset3` 进行排序，并在 `DATA` 步中将它们合并到一个新数据集。
    3. 你只能通过 `PROC SQL` 步合并这些数据集。
    4. 你无法合并这三个数据集，因为它们没有共同变量。

3. 下面哪个程序正确创建了一个包含根据 `empcode` 值进行匹配的 `PROC SQL` 内连接（inner join）结果的表？

    1. ```sas
       proc sql;
          select newsals.empcode allemps.lastname
                  newsals.salary contrib.amount
              from sasuser.allemps, sasuser.contrib,
                   sasuser.newsals
              where empcode=allemps.empid
                    and empcode=contrib.empid;
        quit;
       ```
    2. ```sas
       proc sql;
           create table usesql as
              select newsals.empcode allemps.lastname
                     newsals.salsry contrib.amount
                 from sasuser.allemps, sasuser.contrib,
                      sasuser.newsals
        quit;
       ```
    3. ```sas
       proc sql;
           create table usesql as;
              select newsals.empcode, allemps.lastname,
                     newsals.salary, contrib.amount;
                 from sasuser.allemps, sasuser.contrib,
                      sasuser.newsals;
                 where empcode=allemps.empid
                       and empcode=contrib.empid;
         quit;
       ```
    4. ```sas
       proc sql;
           create table usesql as
              select newsals.empcode, allemps.lastname
                     newsals.salary, contrib.amount
                 from sasuser.allemps, sasuser.contrib,
                      sasuser.newsals
                 where empcode=allemps.empid
                       and empcode=contrib.empid;
        quit;
       ```

4. 为了处理 `DATA` 步匹配-合并，SAS 首先读取每个数据集的描述符部分以创建 PDV 和新数据集。下面哪个描述准确描述了后续过程？

    1. 然后，SAS 顺序合并观测值并读入 PDV，然后将其写入新数据集。当 `BY` 值在所有集中变化时，PDV 将初始化为空。变量以及不匹配产生的缺失值将写入数据集。
    2. 然后，SAS 顺序合并观测值并读入 PDV，然后将其写入新数据集。在每次 `DATA` 步迭代后，PDV 将初始化为空。变量以及不匹配产生的缺失值将从数据集中排除。
    3. 然后，SAS 创建所有可能组合的笛卡尔积，将其写入 PDV，然后写入新数据集。然后 SAS 消除具有匹配 `BY` 值的观测值。
    4. 然后，SAS 创建所有可能组合的笛卡尔积，将其写入 PDV，然后写入新数据集。该数据集随后按 `BY` 值排序。

5. 关于使用多个 `SET` 语句，以下哪个说法是错误的？

    1. 你可以使用多个 `SET` 语句合并来自多个数据集的观测值。
    2. 当遇到任何数据集的文件结束（EOF）标记时停止（即使另一个数据集还有数据）。
    3. 只有当每个 `SET` 语句中的数据集具有共同变量时，你才能在一个 `DATA` 步中使用多个 `SET` 语句。
    4. 执行第二个 `SET` 语句时，PDV 中的变量不会重新初始化。

6. 选择正确创建一个名为 `Sasuser.Summary` 且包含一个从 `Sasuser.Empdata` 数据集的 `Salary` 变量创建的汇总观测值的程序。

    1. ```sas
       proc sum data=sasuser.emdata noprint;
          output out=sasuser.summary sum=Salarysum;
       run;
       ```
    2. ```sas
       proc means data=sasuser.empdata noprint;
          var salary;
          output out=sasuser.summary sum=Salarysum;
       run;
       ```
    3. ```sas
       proc sum data=sasuser.empdata noprint;
          var salary;
          output out=sasuser.summary sum=Salarysum;
       run;
       ```
    4. ```sas
       proc means data=sasuser.empdata noprint;
          output=sasuser.summary sum=Salarysum;
       run;
       ```

7. 如果在下方 `DATA` 步第一次迭代结束时 `Cargosum` 的值为 1000，那么当 `DATA` 步处于第三次迭代时，PDV 中的 `Cargosum` 的值是多少？





```
data sasuser.percent1;
   if _n_=1 then set sasuser.summary (keep=cargosum);
   set sasuser.monthsum (keep=salemon revcargo);
   PctRev=revcargo/cargosum;
run;
```

1. $1000
2. $3000
3. 数值缺失。
4. 在未查看 `Sasuser.Summary` 数据的情况下无法确定该值。

8. 根据显示的数据集，在 `DATA` 步第四次迭代结束，`PDV` 中 `Totalrev` 的值是多少？

```sas
data sasuser.percent2(drop=totalrev);
   if _n_=1 then do until(lastobs);
      set sasuser.monthsum2(keep=revcargo) 
          end=lastobs;
      totalrev+revcargo;
   end;
   set sasuser.monthsum2 
       (keep=salemon revcargo);
   PctRev=revcargo/totalrev;
run;
```

| ![Observations](img/m56-49-g1.png) |

1. 数值缺失。
2. $350.00
3. $520.00
4. $1100.00

9. 下列哪个程序正确使用了索引来合并来自两个输入数据集的数据？

1. ```sas
data work.profit;
   set sasuser.sale2000(keep=routeid flightid date
       rev1st revbusiness revecon revcargo)
       key=flightdate;
   set sasuser.dnunder;
   Profit=sum(rev1st, revbusiness, revecon, revcargo,
              -expenses);
run;
```

2. ```sas
data work.profit;
   set sasuser.dnunder;
   set sasuser.sale2000(keep=routeid flightid date
       rev1st revbusiness revecon revcargo)
       key=flightdate;
   where routeid='0000103';
   Profit=sum(rev1st, revbusiness, revecon, revcargo,
              -expenses);
run;
```

3. ```sas
data work.profit;
   set sasuser.dnunder;
   set sasuser.sale2000(keep=routeid flightid date
       rev1st revbusiness revecon revcargo);
       key=flightdate;
   Profit=sum(rev1st, revbusiness, revecon, revcargo,
              -expenses);
run;
```

4. ```sas
data work.profit;
   set sasuser.dnunder;
   set sasuser.sale2000(keep=routeid flightid date
       rev1st revbusiness revecon revcargo)
       key=flightdate;
   Profit=sum(rev1st, revbusiness, revecon, revcargo,
              -expenses);
run;
```

10. 关于 `_IORC_` 变量的下列陈述错误的是？

1. 当你在 `DATA` 步中使用带有 `KEY=`选项的 `SET` 语句或带有 `KEY=`选项的 `MODIFY` 语句时，它会自动创建。
2. `_IORC_` 的值为 0 表示最近一次带有 `KEY=` 的 `SET` 语句（或带有 `KEY=` 的 `MODIFY` 语句）执行失败。
3. `_IORC_` 的值为 0 表示最近一次带有 `KEY=` 的 `SET` 语句（或带有 `KEY=` 的 `MODIFY` 语句）执行成功。
4. 你可以使用 `_IORC_` 变量来防止在使用索引合并多个数据集的数据时，将不匹配的数据也包含在内。

# 第 16 章：使用查找表匹配数据

## 概述

## 引言

有时，你需要根据公共变量的值，将来自两个或多个数据集的数据合并到新数据集的单个观测值。当数据源是具有相同结构的两个或数据集时，可以使用匹配合并（match-merge）来合并数据集。然而，在某些情况下，数据源并不共享共同结构。当数据源没有共同结构时，你可以使用查找表（lookup table）来匹配它们。查找表是一个包含值的表![查找表包含值](img/m56-49-g1.png)

# 使用多维数组

### 多维数组复习

当查找操作依赖于多个键时，可以使用多维数组。你使用 `ARRAY` 语句来创建数组。

| 语法 | 描述 |
| :--- | :--- |
| `ARRAY array-name {rows,cols} initial values;` | `array-name` 为数组命名。`rows` 指定行维度上的元素个数。`cols` 指定列维度上的元素个数。`initial values` 是组成数组的值。 |

注意：在处理数组工作时，请记住以下点：
* 数组的名称必须是 SAS 名称，且不能是函数或变量的名称。
* 列为数组元素的变量类型必须相同（均为数值型或字符型）。
* 指定的初始可以是数字或字符字符串。你必须将字符字符串放在引号中。

如果你使用 `_temporary_` 关键字，数组元素的行为类似于 `DATA` 步变量，但有以下例外：
* 它们没有名称。
* 它们不会出现在输出数据集集中。
* 你不能使用特殊下标 `*` 来引用所有元素。
* 临时数据元素的值始终会被保留，而不是在下一次迭代开始时重置为缺失值。

## 示例

假设你需要确定 `Sasuser.Flights` 数据集中表示的航班的风寒指数（wind chill）。该数据集包含三个变量：`Flight`（航班号）、`Temp`（飞行期间平均环境温度）和 `Wspeed`（飞行期间平均风速）。图 16.1 SAS 数据集 `Sasuser.Flights` ![Obs, Flight, Temp, Wspeed]

风寒指数根据气温和风速得出，如下面的风寒查找表所示。为了确定每个航班的风寒指数，你可以创建一个多维数组，用于存储表中显示的风寒指数。图 16.2 温度（华氏度）![风速](img/m57-3-g1.png)

在以下程序中，`ARRAY` 语句创建了二维数组 `WC` 并指定了数组的维度：四行两列。由于使用了 `_temporary_` 关键字，因此没有从数组创建变量。指定的初始值对应于风寒查找表中的值。对于此示例，风寒查找表中前两列和四行的值包含在数组中。

```sas
data work.wndchill (drop=column row);
  array WC{4,2} _temporary_
        (-22,-16,-28,-22,-32,-26,-35,-29);
  set sasuser.flights;
  row=round(wspeed,5)/5;
  column=(round(temp,5)/5)+3;
  WindChill=wc{row,column};
run;
```





图 16.3 温度（华氏度）
![风速](img/m57-3-g2.png) 

每次航班的 `WindChill`（风寒指数）值是通过根据 `Sasuser.Flights` 数据集中 `Wspeed` 和 `Temp` 的值引用数组来定的。数组引用的行号由 `Wspeed` 的值决定。数组引用的列号由 `Temp` 的值决定。

| WC 数组的表格表示 |
| --- |
|  |

```sas
data work.wndchill (drop = column row);
  array WC{4,2} _temporary_ 
        (-22,-16,-28,-22,-32,-26,-35,-29);
  set sasuser.flights;
  row = round(wspeed,5)/5;
  column = (round(temp,5)/5)+3;
  WindChill= wc{row,column};
run;
```

| ![WC 数组的表格表示](img/m57-3-g3.png) |

`Wspeed` 值的舍入单位为 5，因为风寒表中的风速值是每 5 英里进行一次舍入。然后将 `Wspeed` 除以 5 以得到数组引用的行号。与 `Wspeed` 的值一样，`Temp` 的值也被舍入到最近的 5，然后除以 5。该值加上偏移量 3，因为风寒查找表中的第三列代表 0 度。

```sas
data work.wndchill (drop = column row);
  array WC{4,2} _temporary_ 
        (-22,-16,-28,-22,-32,-26,-35,-29);
  set sasuser.flights;
  row = round(wspeed,5)/5;
  column = (round(temp,5)/5)+3;
  WindChill= wc{row,column};
run;
```

`PROC PRINT` 输出显示完成的数据集。

```sas
proc print data=work.wndchill;
run;
```

| ![proc print 输出](img/m57-4-g1.png) |

# 从 SAS 数据集填充数组

## 概述

在上一节中，当创建数组时，风寒查找表已加载到 `WC` 数组中。在许多情况下，你可能更倾向于使用存储在 SAS 数据中的值填充数组，而不是在 `ARRAY` 语句中加载它们。当满足以下条件时，应将查找值存储在 SAS 数据集中：

*   值太多，无法在数组中轻松初始化
*   值频繁变化
*   相同的值在许多程序中被使用

## 示例

假设你想比较 SAS 数据集 `Sasuser.Monthsum` 中的实际货运收入值与 SAS 数据集 `Sasuser.Ctargets` 中的目标货运收入值。`Sasuser.Monthsum` 包含了 1997 年至 1999 年每月实际货运和客运收入数据。

表 16.1 SAS 数据集 `Sasuser.Monthsum`（选取变量的前五个观测值）

| Obs | SaleMon | RevCargo | MonthNo |
| --- | --- | --- | --- |
| 1 | JAN1997 | $171,520,869.10 | 1 |
| 2 | JAN1998 | $238,786,807.60 | 1 |
| 3 | JAN1999 | $280,350,393.00 | 1 |
| 4 | FEB1997 | $177,671,530.40 | 2 |
| 5 | FEB1998 | $215,959,695.50 | 2 |

SAS 数据集 `Sasuser.Ctargets` 包含了 1997 年至 1999 年每月的目标货运收入数据。

表 16.2 SAS 数据集 `Sasuser.Ctargets`

| Obs | Year | Jan | Feb | Mar | Apr | May | Jun |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 1997 | `192284420` | `86376721` | `28526103` | `260386468` | `109975326` | `102833104` |
| 2 | 1998 | `108645734` | `147656369` | `202158055` | `411607077` | `264294440` | `267135485` |
| 3 | 1999 | `85730444` | `74168740` | `39955768` | `312654811` | `318149340` | `187270927` |

你想创建一个新的 SAS 数据集 `Work.Lookup1`，列出每个月的实际值和目标值。`Work.Lookup1` 的结构应与 `Sasuser.Monthsum` 相同：每个每月一个观测值，以及一个新变量 `Ctarget`（目标货运）。`Ctarget` 的值来源于 `Sasuser.Ctargets` 中的目标值。

表 16.3 SAS 数据集 `Work.Lookup1`

| Obs | SaleMon | RevCargo | Ctarget |
| --- | --- | --- | --- |
| 1 | JAN1997 | $171,520,869.10 | $192,284,420.00 |
| 2 | JAN1998 | $238,786,807.60 | $108,645,734.00 |
| 3 | JAN1999 | $280,350,393.00 | $85,730,444.00 |
| 4 | FEB1997 | $177,671,530.40 | $86,376,721.00 |
| 5 | FEB1998 | $215,959,695.50 | $147,656,369.00 |

`Sasuser.Monthsum` 和 `Sasuser.Ctargets` 无法合并，因为它们的结构不同：

*   `Sasuser.Monthsum` 每个每月一个观测值。
*   `Sasuser.Ctargets` 每个月有一列，每年一个观测值。

然而，数据集具有共同因素：月份和年份。你可以使用多维数组来匹配 `Sasuser.Monthsum` 中的每月实际值与 `Sasuser.Ctargets` 中的每月目标值。

## 创建数组

第一步是创建一个数组来存放目标数据集 `Sasuser.Ctargets`。数组需要两个维度：年份和月份。在下面的程序中，第一个 `ARRAY` 语句创建了二维数组 `Targets`。注意，数组的维度不需要从 1 到元素个数。你可以在定义数组时指定范围。在这种情况下，数组的维度被指定为 3 行（每年：1997、1998 和 1999）和 12 列（每月）。

```sas
data work.lookup1;
  array Targets{1997:1999,12} _temporary_; 
  if _n_=1 then do i= 1 to 3;
         set sasuser.ctargets;
         array mnth{*} Jan--Dec;
         do j=1 to dim(mnth);
            targets{year,j}=mnth{j};
         end;
  end;
  set sasuser.monthsum(keep=salemon revcargo);
  year=input(substr(salemon,4),4.); 
  Ctarget=targets{year,monthno};
  format ctarget dollar15.2; 
run;
```

下表表示数组 `Targets`。注意数组尚未填充。下一步是从 `Sasuser.Ctargets` 加载数组元素。

表 16.4 Targets 数组的表格表示

| | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1997 | | | | | | | | | | | | |
| 1998 | | | | | | | | | | | | |
| 1999 | | | | | | | | | | | | |

注意：`Targets` 数组的行维度可以使用值 3 指定。这是一个示例：

```sas
array Targets{3,12} _temporary_;
```

然而，使用 1997:1999 符号可以简化程序，消除了将数值映射到年份的需求。

## 加载数组元素

`Targets` 数组需要加载 `Sasuser.Ctargets` 中的值。完成此任务的方法是在 `DO` 循环内加载数组。

表 16.5 SAS 数据集 `Sasuser.Ctargets`

| Year | Jan | Feb | Mar | Apr | May | Jun |
| --- | --- | --- | --- | --- | --- | --- |
| 1997 | `192284420` | `86376721` | `28526103` | `260386468` | `109975326` | `102833104` |
| 1998 | `108645734` | `147656369` | `202158055` | `411607077` | `264294440` | `267135485` |
| 1999 | `85730444` | `74168740` | `39955768` | `312654811` | `318149340` | `187270927` |





| --- | --- | --- | --- | --- | --- | --- |
|  |  
```
196728648
```
 |  |
```
236996122
```
 |  |
```
112413744
```
 |  |
```
125401565
```
 |  |
```
72551855
```
 |  |
```
136042505
```
 | |
|  |  
```
208694865
```
 |  |
```
83456868
```
 |  |
```
286846554
```
 |  |
```
275721406
```
 |  |
```
230488351
```
 |  |
```
24901752
```
 | |
|  |  
```
123394421
```
 |  |
```
34273985
```
 |  |
```
151565752
```
 |  |
```
141528519
```
 |  |
```
178043261
```
 |  |
```
181668256
```
 | |

`IF-THEN` 语句指定 `Targets` 数组仅在 `DATA` 步的第一次迭代中加载一次。`DO` 循环执行三次，对应 `Sasuser.Ctargets` 中的每个观测值执行一次。`DO` 循环内部的 `ARRAY` 语句创建了 `Mnth` 数组，它存储了来自 `Sasuser.Ctargets` 的值。`Mnth` 数组的维度使用星号（`*`）指定，这允许 SAS 自动计数数组元素。

注意：如果你使用星号来指定数组的维度，必须列出数组元素。如果数组元素是使用 `_TEMPORARY_` 关键字指定的，则不能使用星号来指定数组的维度。数组元素 `Jan` 到 `Dec` 使用双连线（`--`）列出。双连线（`--`）用于根据指定值在 PDV（程序数据向量）中的位置进行读取。

```sas
data work.lookup1;
  array Targets{1997:1999,12} _temporary_; 
  if _n_=1 then do i= 1 to 3;
	         set sasuser.ctargets;
	         array Mnth{*} Jan--Dec;
	         do j=1 to dim(mnth);
	            targets{year,j}=mnth{j};
	         end;
  end;
  set sasuser.monthsum(keep=salemon revcargo monthno);
  year=input(substr(salemon,4),4.); 
  Ctarget=targets{year,monthno};
  format ctarget dollar15.2;  
run;
```

下表显示了 `DO` 循环第一次迭代后 `Mnth` 数组中的值。

表 16.6 `Mnth` 数组的表表示（`DO` 循环第一次迭代后）

| Jan | Feb | Mar... | ...Oct | Nov | Dec |
| --- | --- | --- | --- | --- | --- |
| --- | --- | --- | --- | --- | --- |
|  |
```
192284420
```
 |  |
```
86376721
```
 |  |
```
26038648
```
 |  |
```
125401565
```
 |  |
```
72551855
```
 |  |
```
136042505
```
在嵌套的 `DO` 循环中，`Targets` 数组引用与 `Mnth` 数组引用匹配，以填充 `Targets` 数组。`DIM` 函数返回 `Mnth` 数组中的元素数量（在此例中 `12`），并为嵌套的 `DO` 循环提供结束点。

```sas
data work.lookup1;
  array Targets{1997:1999,12} _temporary_; 
  if _n_=1 then do i= 1 to 3;
	         set sasuser.ctargets;
	         array Mnth{*} Jan--Dec;
	         do j=1 to dim(mnth);
	            targets{year,j}=mnth{j};
	         end;
  end;
  set sasuser.monthsum(keep=salemon revcargo monthno);
  year=input(substr(salemon,4),4.); 
  Ctarget=targets{year,monthno}; 
  format ctarget dollar15.2; 
run;
```

表 16.7 `Mnth` 数组的表表示（`DO` 循环第二次迭代后）

| Jan | Feb | Mar... | ...Oct | Nov | Dec |
| --- | --- | --- | --- | --- | --- |
| --- | --- | --- | --- | --- | --- |
|  |
```
108645734
```
 |  |
```
14765639
```
 |  |
```
20215805
```
 |  |
```
275721406
```
 |  |
```
230488351
```
 |  |
```
24901752
```
表 16.8 `Mnth` 数组的表示（`DO` 循环第三次迭代后）

| Jan | Feb | Mar... | ...Oct | Nov | Dec |
| --- | --- | --- | --- | --- | --- |
| --- | --- | --- | --- | --- | --- |
|  |
```
85730444
```
 |  |
```
74168740
```
 |  |
```
39955768
```
 |  |
```
141528519
```
 |  |
```
178043261
```
 |  |
```
181668256
```

表 16.9 填充后的 `Targets` 数组表示

| | 1 | 2 | 3... | ...10 | 11 | 12 |
| --- | --- | --- | --- | --- | --- | --- |
| --- | --- | --- | --- | --- | --- | --- |
| 1997 |  
```
192284420
```
 |  |
```
86376721
```
 |  |
```
26038648
```
 |  |
```
125401565
```
 |  |
```
72551855
```
 |  |
```
136042505
```
| 1998 |  
```
108645734
```
 |  |
```
14765639
```
 |  |
```
20215805
```
 |  |
```
275721406
```
 |  |
```
230488351
```
 |  |
```
24901752
```
| 1999 |  
```
85730444
```
 |  |
```
74168740
```
 |  |
```
39955768
```
 |  |
```
141528519
```
 |  |
```
178043261
```
 |  |
```
181668256
```

注意：`Mnth` 数组的维度也可以使用数值 `12` 来指定。然而，星号表示法使程序更具活性。例如，使用星号，如果目标数据集仅包含 11 个月的数据，程序不需要修改。记住，如果你使用星号计算数组元素，必须列出数组元素。

## 读取实际值

最后一步是读取存储在 `Sasuser.Monthsum` 中的实际值。记住，你需要每个观测值的月份和年份，以便找到正确的目标收入值。

表 16.10 SAS 数据集 `Sasuser.Monthsum`（选取变量的前五个观测值）

| SaleMon | RevCargo | MonthNo |
| --- | --- | --- |
| JAN1997 | $171,520,869.10 | 1 |
| JAN1998 | $238,786,807.60 | 1 |
| JAN1999 | $280,350,393.00 | 1 |
| FEB1997 | $177,671,530.40 | 2 |
| FEB1998 | $215,959,695.50 | 2 |





使用数组是一个很好的解决方案，因为数据集的方向不同。另一种解决方案是使用 `PROC TRANSPOSE` 对 `Sasuser.Ctargets` 进行转置，然后根据 `Year` 和 `Month` 的值将转置后的数据集与 `Sasuser.Monthsum` 进行合并。

| 1997 | 192284420 | 86376721 | 28526103 | 260386468 | 109975326 | 102833104 |
| 1998 | 108645734 | 147656369 | 202158055 | 41160707 | 264294440 | 267135485 |
| 1999 | 85730444 | 74168740 | 39955768 | 312654811 | 318149340 | 187270927 |

### PROC TRANSPOSE 的通用形式：

`PROC TRANSPOSE <DATA=input-data-set><OUT=output-data-set><NAME=prefix text><PREFIX=variable-name>;BY <DESCENDING> variable-1<...<DESCENDING> variable-n><NOTSORTED>;VAR variable(s);RUN;`

以下是句的的解释：
- `DATA=input-data-set`: 指定要转置的 SAS 数据集。
- `OUT=output-data-set`: 指定输出数据集名称。
- `NAME=variable-name`: 指定输出集中变量名，该变量包含被转置以创建当前观测值的变量名。
- `PREFIX=variable-name`: 指定在构建输出集中转置变量名称时使用的前缀。例如，如果 `PREFIX=VAR`，则变量名为 `VAR1`、`VAR2`, ..., `VARn`。
- `BY` 语句：用于转置每个 `BY` 组。
- `VAR variable(s)`：指定一个或多个要转置的变量。

**注意：**
- 如果 `output-data-set` 不存在，`PROC TRANSPOSE` 将根据 `DATA` 命名规范创建它。
- 如果省略 `VAR` 语句，`TRANSPOSE` 过程将转置输入集中未在其他语句列出的所有数值变量。
- 如果你想转置字符变量，必须在 `VAR` 语句中列出它们。

`TRANSPOSE` 过程通过重构 SAS 数据中的值来创建一个输出数据集。当数据集被重构时，选定的变量会被转置为观测值。`TRANSPOSE` 过程通常可以消除编写冗长 `DATA` 步来实现相同结果的需求。输出数据集可以在随后的 `DATA` 或 `PROC` 步骤中用于分析、报告或进一步的数据处理。`PROC TRANSPOSE` 不打印输出数据集。请使用 `PROC PRINT`、`PROC REPORT` 或其他 SAS 报告工具打印输出数据集。

![SAS Dat Set Sasuser. Ctargets](img/m57-15-g1.png)

## 示例

以下程序转置了 SAS 数据集 `Sasuser.Ctargets`。`OUT=` 指定了数据集的名称 `Work.Ctarget2`。`Sasuser.Ctargets` 中的所有变量都被转置了，因为所有变量都是数值型，且程序没有没有 `VAR` 语句。

```
proc transpose data=sasuser.ctargets
     out=work.ctarget2;
run;
```

表 16.14 输入数据集 `Sasuser.Ctargets`（选定的变量）

| Year | Jan | Feb | Mar | Apr | May | Jun |
| --- | --- | --- | --- | --- | --- | --- |
| 1997 | 192284420 | 86376721 | 28526103 | 260386468 | 109975326 | 102833104 |
| 1998 | 108645734 | 147656369 | 202158055 | 41160707 | 264294440 | 267135485 |
| 1999 | 85730444 | 74168740 | 39955768 | 312654811 | 318149340 | 187270927 |

表 16.15 输出数据集：`Work.Ctarget2`

| Obs | _NAME_ | COL1 | COL2 | COL3 |
| --- | --- | --- | --- | --- |
| 1 | Year | 1997 | 1998 | 1999 |
| 2 | Jan | 192284420 | 108645734 | 85730444 |
| 3 | Feb | 86376721 | 147656369 | 74168740 |
| 4 | Mar | 28526103 | 202158055 | 39955768 |
| 5 | Apr | 260386468 | 41160707 | 31265481 |
| 6 | May | 109975326 | 264294440 | 318149340 |
| 7 | Jun | 102833104 | 267135485 | 187270927 |
| 8 | Jul | 196728648 | 208694865 | 123394421 |
| 9 | Aug | 239966122 | 83456868 | 34273985 |
| 10 | Sep | 112413744 | 286846554 | 151565752 |
| 11 | Oct | 125401565 | 275721406 | 141528519 |
| 12 | Nov | 72551855 | 230488351 | 178043261 |
| 13 | Dec | 136042505 | 24901752 | 18166825 |

注意输出集中变量名为 `_NAME_`、`COL1`、`COL2`。`_NAME_` 是 `TRANSPOSE` 用于识别每个观测值来源的默认变量，它是输入集的变量名。例如，在 `Work.Ctarget2` 中，`COL1` 和 `COL2` 代表 1997 和 1998 年的收入。

### 添加描述性名称

你可以使用 `PROC TRANSPOSE` 选项为输出数据集赋予更具描述性的名称。`NAME=` 选项指定 `_NAME_` 变量名。`PREFIX=` 选项指定在构建输出集的转置变量名称时使用的前缀。例如，如果 `PREFIX=Ctarget`，则变量名为 `Ctarget1`、`Ctarget2`。

```
proc transpose data=sasuser.ctargets
     out=work.ctarget2
     name=Month
     prefix=Ctarget;
run;
```

表 16.16 输出数据集：`Work.Ctarget2`

| Obs | Month | Ctarget1 | Ctarget2 | Ctarget3 |
| --- | --- | --- | --- | --- |
| 1 | Year | 1997 | 1998 | 1999 |
| 2 | Jan | 192284420 | 108645734 | 85730444 |
| 3 | Feb | 86376721 | 147656369 | 74168740 |
| 4 | Mar | 28526103 | 202158055 | 39955768 |
| 5 | Apr | 260386468 | 41160707 | 31265481 |
| 6 | May | 109975326 | 264294440 | 318149340 |
| 7 | Jun | 102833104 | 267135485 | 187270927 |
| 8 | Jul | 196728648 | 208694865 | 123394421 |
| 9 | Aug | 239966122 | 83456868 | 34273985 |
| 10 | Sep | 112413744 | 286846554 | 151565752 |
| 11 | Oct | 125401565 | 275721406 | 141528519 |
| 12 | Nov | 72551855 | 230488351 | 178043261 |
| 13 | Dec | 136042505 | 24901752 | 18166825 |

**注意：** `RENAME=` 数据集选项也可以用于 `PROC TRANSPOSE` 以更改变量名。

```
proc transpose data=sasuser.ctargets 
     out=work.ctarget2 (rename=(col1=Ctarget1 
         col2=Ctarget2 col3=Ctarget3))
     name=Month;
run;
```

`_NAME_` 的默认标签是 `NAME`。要查看此内容，使用带有 `LABEL` 选项的 `PROC PRINT` 打印转置数据集。你可以使用 `LABEL` 语句覆盖默认。

```
proc transpose data=sasuser.ctargets
     out=work.ctarget2
name=Month;
run;
```

# 合并转置数据集

### 为合并准备数据

记住转置后的数据集 `Work.Ctarget2` 需要根据 `Year` 和 `Month` 的值与 `Sasuser.Monthsum` 进行合并。目前两个数据集都没有为合并做好准备。

表 16.17 输出数据集：`Work.Ctarget2`（选定的变量）

| Obs | _NAME_ | COL1 | COL2 | COL3 |
| --- | --- | --- | --- | --- |
| 1 | Year | 1997 | 1998 | 1999 |
| 2 | Jan | 192284420 | 108645734 | 85730444 |
| 3 | Feb | 86376721 | 147656369 | 74168740 |
| 4 | Mar | 28526103 | 202158055 | 39955768 |
| 5 | Apr | 260386468 | 41160707 | 31265481 |

表 16.18 SAS 数据集 `Sasuer.Monthsum`（选定变量的前观测值）

| Obs | SaleMon | RevCargo | MonthNo |
| --- | --- | --- | --- |
| 1 | JAN1997 | $171520869.10 | 1 |
| 2 | JAN1998 | $238786807.60 | 1 |
| 3 | JAN1999 | $280350393.00 | 1 |
| 4 | FEB1997 | $177671530.40 | 2 |
| 5 | FEB1998 | $215959695.50 | 2 |





```
proc transpose data=sasuser.ctargets 
     out=work.ctarget2
     name=Month
     prefix=Ctarget;
     by year;
run;
```

表 16.19 输入数据集 `Sasuser.Ctargets`（选定的变量）

| Obs | Year | Jan | Feb | Mar | Apr | May | Jun |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 1997 | 192284420 | 86376721 | 28526103 | 260386468 | 109975326 | 102833104 |
| 2 | 1998 | 108645734 | 147656369 | 202158055 | 41160707 | 264294440 | 267135485 |
| 3 | 1999 | 85730444 | 74168740 | 39955768 | 312654811 | 318149340 | 187270927 |

表 16.20 输出数据集 `Work.Ctarget2`（前 12 条观测值）

| Obs | Year | Month | Ctarget1 |
| --- | --- | --- | --- |
| 1 | 1997 | Jan | 192284420 |
| 2 | 1997 | Feb | 86376721 |
| 3 | 1997 | Mar | 28526103 |
| 4 | 1997 | Apr | 260386468 |
| 5 | 1997 | May | 109975326 |
| 6 | 1997 | Jun | 102833104 |
| 7 | 1997 | Jul | 196728648 |
| 8 | 1997 | Aug | 236996122 |
| 9 | 1997 | Sep | 112413744 |
| 10 | 1997 | Oct | 125401565 |
| 11 | 1997 | Nov | 72551855 |
| 12 | 1997 | Dec | 136042505 |

注意：除非使用 `NOTSORTED` 选项，否则在使用 `PROC TRANSPOSE` 的 `BY` 语句之前，原始 SAS 数据集必须排序或索引。

## 对 `Work.Ctarget2` 数据集进行



为合并准备 `Work.Ctarget2` 的最后一步是使用 `SORT` 过程按 `Year` 和 `Month` 对数据集进行排序，如下程序所示：

```
proc sort data=work.ctarget2;
   by year month;
run; 
```

注意，在排序后的 `Work.Ctarget2` 中，`month` 的值在 `year` 内部按字母顺序排序。

表 16.21 SAS 数据集 `Work.Ctarget2`（排序后的，前 12 条观测值）

| Obs | Year | Month | Ctarget1 |
| --- | --- | --- | --- |
| 1 | 1997 | Apr | 260386468 |
| 2 | 1997 | Aug | 236996122 |
| 3 | 1997 | Dec | 136042505 |
| 4 | 1997 | Feb | 86376721 |
| 5 | 1997 | Jan | 192284420 |
| 6 | 1997 | Jul | 196728648 |
| 7 | 1997 | Jun | 102833104 |
| 8 | 1997 | Mar | 28526103 |
| 9 | 1997 | May | 109975326 |
| 10 | 1997 | Nov | 72551855 |
| 11 | 1997 | Oct | 125401565 |
| 12 | 1997 | Sep | 112413744 |

## 重组 `Sasuser.Monthsum` 数据集

`Sasuser.Monthsum` 中的数据也必须为合并进行重组，因为该数据集中的月份和年份值合并在变量 `SaleMon` 中。

表 16.22 SAS 数据集 `Sasuser.Monthsum`（选定变量的前五条观测值）

| Obs | SaleMon | RevCargo | MonthNo |
| --- | --- | --- | --- |
| 1 | JAN1997 | $171,520,869.10 | 1 |
| 2 | JAN1998 | $238,786,807.60 | 1 |
| 3 | JAN1999 | $280,350,393.00 | 1 |
| 4 | FEB1997 | $177,671,530.40 | 2 |
| 5 | FEB1998 | $215,959,695.50 | 2 |

以下程序创建两个新变量 `Year` 和 `Month` 来存储年份和月份值。`Year` 的值是使用 `INPUT` 和 `SUBSTR` 函数从 `SaleMon` 创建的。`Month` 的值是使用 `LOWCASE` 和 `SUBSTR` 函数从 `SaleMon` 提取的。

```
data work.mnthsum2;
   set sasuser.monthsum(keep=SaleMon RevCargo);
   length Month $ 3;
   Year=input(substr(SaleMon,4),4.);
   Month=propcase(SaleMon);
```

表 16.23 SAS 数据集 `Work.Mnth2`（前六条观测值）

| Obs | SaleMon | RevCargo | Month | Year |
| --- | --- | --- | --- | --- |
| 1 | JAN1997 | $171,520,869.10 | Jan | 1997 |
| 2 | JAN1998 | $238,786,807.60 | Jan | 1998 |
| 3 | JAN1999 | $280,350,393.00 | Jan | 1999 |
| 4 | FEB1997 | $177,671,530.40 | Feb | 1997 |
| 5 | FEB1998 | $215,959,695.50 | Feb | 1998 |
| 6 | FEB1999 | $253,999,924.00 | Feb | 1999 |

## 对 `Work.Mnthsum2` 数据集进行排序

对于 `Work.Ctarget2`，准备合并的最后一步是按 `Year` 和 `Month` 值对数据集进行排序，如下所示：

```
proc sort data=work.mnthsum2;
by year month;
```

注意在 `Work.Ctarget2` 的排序版本中，`month` 的值在 `year` 内部按字母顺序排序。

表 16.24 SAS 数据集 `Work.Mnthsum2`（排序后的）

| Obs | SaleMon | RevCargo | Month | Year |
| --- | --- | --- | --- | --- |
| 1 | APR1997 | $380,804,120.20 | Apr | 1997 |
| 2 | AUG1997 | $196,639,501.10 | Aug | 1997 |
| 3 | DEC1997 | $196,504,413.00 | Dec | 1997 |
| 4 | FEB1997 | $177,671,530.40 | Feb | 1997 |
| 5 | JAN1997 | $171,520,869.10 | Jan | 1997 |
| 6 | JUL1997 | $197,163,278.20 | Jul | 1997 |
| 7 | JUN1997 | $190,560,828.50 | Jun | 1997 |
| 8 | MAR1997 | $196,591,378.20 | Mar | 1997 |
| 9 | MAY1997 | $196,261,573.20 | May | 1997 |
| 10 | NOV1997 | $190,228,066.70 | Nov | 1997 |
| 11 | OCT1997 | $196,957,153.40 | Oct | 1997 |
| 12 | SEP1997 | $190,535,012.50 | Sep | 1997 |

## 完成合并

当数据结构正确时，可以通过 `Year` 和 `Month` 值对 `Work.Mnthsum2` 和 `Work.Ctarget2` 进行合并，如下程序所示：

```
data work.merged;
   merge work.mnthsum2 work.ctarget2;
   by year month;
run;
```

表 16.25 SAS 数据集 `Work.Mnthsum2`（前五条观测值）

| Obs | SaleMon | RevCargo | Month | Year |
| --- | --- | --- | --- | --- |
| 1 | APR1997 | $380,804,120.20 | Apr | 1997 |
| 2 | AUG1997 | $196,639,501.10 | Aug | 1997 |
| 3 | DEC1997 | $196,504,413.00 | Dec | 1997 |
| 4 | FEB1997 | $177,671,530.40 | Feb | 1997 |
| 5 | JAN1997 | $171,520,869.10 | Jan | 1997 |

表 16.26 SAS 数据集 `Work.Ctarget2`（前五条观测值）

| Obs | Year | Month | Ctarget1 |
| --- | --- | --- | --- |
| 1 | 1997 | Apr | 260386468 |
| 2 | 1997 | Aug | 236996122 |
| 3 | 1997 | Dec | 136042505 |
| 4 | 1997 | Feb | 86376721 |
| 5 | 1997 | Jan | 192284420 |

`PROC PRINT` 输出显示了数据集 `Work.Merged`。`RevCargo` 的值代表每个月的实际货运收入。`Ctarget1` 的值代表每个月的目标货运值。

```
proc print 
     data=work.merged (obs=10);
   format ctarget1 dollar15.2;
   var month year revcargo ctarget1;
run;
```

![SAS 数据集 Work](img/m57-22-g1.png)

# 使用哈希对象作为查找表

## 概述

从 SAS 9 开始，哈希对象可以在 `DATA step` 中使用。哈希对象提供了一种高效、方便的机制，用于快速存储和检索。与使用一系列连续整数来访问数组元素的数组不同，哈希对象可以使用任何数值和字符值的组合作为地址。与只返回单个值的数组不同，哈希对象可以从指定的查找返回多个值。哈希对象可以从硬编码值或 SAS 数据集加载，它是动态调整大小的，并在整个 `DATA step` 期间存在。对于使用可以放入内存的无序数据的查找，哈希对象是一个很好的选择，因为它提供了内存存储和检索，并且不需要数据进行排序或索引![SAS 数据集，哈希对象](img/m57-25-g1.png)

## 哈希对象的结构

当查找取决于字符键值时，可以使用哈希对象。哈希对象类似于具有行和列的表格，包含键组件和数据组件。键组件具有以下特性：

*   可能由数值和字符值组成
*   将键映射到数据行
*   必须唯一
*   可以是复合的

数据组件具有以下特性：

*   每个键值可以包含多个数据值
*   可以是数值和字符值组成

## 示例





假设你有一个名为 `Sasuser.Contrib` 的数据集，其中列出了退休基金的季度贡献金额。你可以使用哈希对象（hash object）来计算每个季度实际贡献金额与目标金额之间的差异。![SAS Data Set Sasuser. Contrib](img/m57-26-g1.png)以下程序创建一个哈希对象，用于存储员工向退休基金贡献的季度目标。为了计算实际贡献金额与目标金额之间的差异，程序根据键值（key values）从哈希对象中检索目标金额。

```
data work.difference (drop= goalamount);
   if _N_ = 1 then do;
      declare hash goal( );
      goal.definekey("QtrNum");
      goal.definedata("GoalAmount");
      goal.definedone( ); 
      call missing(goalamount);
      goal.add(key:'qtr1', data:10 );
      goal.add(key:'qtr2', data:15 );
      goal.add(key:'qtr3', data: 5 );
      goal.add(key:'qtr4', data:15 );
  end;
  set sasuser.contrib;
  goal.find();
  Diff = amount - goalamount;
run;
```

我们将看到哈希对象是如何设置的。

## DATA 步组件对象

哈希对象是一个 DATA 步组件对象。组件对象是由属性（attributes）和方法（methods）组成的数据元素。属性是用于指定与对象相关信息的属性。方法定义了对象可以执行的操作。要在你的 SAS 程序中使用 DATA 步组件对象，你必须先声明并创建（实例化）该对象。

## 声明哈希对象

你使用 `DECLARE` 语句来声明哈希对象。

| 通用形式，`DECLARE` 语句：`DECLARE object-name <(<argument_tag-1: value-1<, ...argument-tag-n: value-n>>)>;` |
`object` 指定组件对象。 |
`object-name` 指定组件对象的名称。 |
`arg_tag` 指定用于创建组件对象实例的信息。 |
`value` 指定参数标签的值。有效值取决于组件对象。对象的有效值如下： |
| `hash` 表示一个哈希对象。 |
| `hiter` 表示一个哈希迭代器对象（hash iterator object）。 |

注意：哈希迭代器对象按键升序或降序从哈希对象中检索数据。以下 `DECLARE` 语句创建一个名为 `Goal` 的哈希对象。

```
data work.difference (drop= goalamount);
   if _N_ = 1 then do;
      declare hash goal();
```

此时，你已经声明了一个名为 `Goal` 的哈希对象。注意：`DECLARE` 语句是一个可执行语句。

## 定义键和数据

记住，哈希对象使用查找键（lookup keys）来存储和检索数据。键和数据是 DATA 步变量，你通过点符号方法调用（object dot notation method calls）来初始化哈希对象。

| 通用形式，对象点符号方法调用：`object.method(<argument_tag-1: value-1<, ...argument-tag-n: value-n>>);` 这里是对该语法的解释： |
`object` 指定 DATA 步组件对象的名称。 |
`method` 指定要调用的方法名称。 |
`argument-tag` 标识传递给方法的参数。 |
`value` 指定参数值。 |

键组件通过将键变量名传递给 `DEFINEKEY` 方法来定义。数据组件通过将数据变量名传递给 `DEFINEDATA` 方法来定义。当所有键和数据组件定义完成后，会调用 `DEFINEDONE` 方法。键和数据可以由任意数量的字符或数值 DATA 步变量组成。以下代码初始化了键变量 `QtrNum` 和数据变量 `GoalAmount`。

```
data work.difference (drop= goalamount);
   length goalamount 8;
   if _N_ = 1 then do;
      declare hash goal();
      goal.definekey ("QtrNum");
      goal.definedata ("GoalAmount");
      goal.definedone();
```

## 使用 Call Missing 程序

由于变量 `GOALAMOUNT` 不在输入集中，且未出现在赋值语句的等号左侧，SAS 会发出注释，说明该变量未初始化。为了避免接收这些注释，请使用 `CALL MISSING` 程序，并将键和数据变量作为参数。`CALL MISSING` 程序为指定的字符或数值变量分配一个缺失值。

```
data Work.Difference (drop= goalamount);
if _N_ = 1 then do; declare hash goal();
   goal.definekey("QtrNum");
   goal.definedata("GoalAmount");
   goal.definedone();
   call missing(goalamount);
```

## 加载键和数据值

到为止，你已经声明并实例化了哈希对象，并初始化了哈希对象的键和数据变量。你现在准备好使用 `ADD` 方法填充哈希对象。以下代码使用 `ADD` 方法将键值 `qtr1`、`qtr2`、`qtr3` 和 `qtr4` 以及对应的数据值 `10`、`15`、`5` 和 `15` 加载到哈希对象中。

```
data work.difference (drop= goalamount);
if _N_ = 1 then do;
   declare hash goal( );
   goal.definekey("QtrNum");
   goal.definedata("GoalAmount");
   goal.definedone( );
   goal.add(key:'qtr1', data:10 );
   goal.add(key:'qtr2', data:15 );
   goal.add(key:'qtr3', data: 5 );
   goal.add(key:'qtr4', data:15 );
end;
```

## 获取匹配数据

使用 `FIND` 方法从哈希对象中检索数据。`FIND` 方法生成一个返回代码，指示键是否存在于哈希对象中。返回值为 0 表示找到，非零表示查找失败。如果键在哈希对象中，`FIND` 方法还将数据赋值给变量，以便稍后使用。

```
data work.difference (drop= goalamount);
if _N_ = 1 then do;
   declare hash goal( );
   goal.definekey("QtrNum");
   goal.definedata("GoalAmount");
   goal.definedone( );
   call missing(goalamount);
   goal.add(key:'qtr1', data:10 );
   goal.add(key:'qtr2', data:15 );
   goal.add(key:'qtr3', data: 5 );
   goal.add(key:'qtr4', data:15 );
end;
set sasuser.contrib;
goal.find();
Diff = amount - goalamount;
run;
```

## 哈希对象处理

我们将考虑提交程序时会发生什么。

```
data Work.difference (drop= goalamount);
   if _N_ = 1 then do;
      declare hash goal( );
      goal.definekey("QtrNum");
      goal.definedata("GoalAmount");
      goal.definedone( );
      call missing(goalamount);
      goal.add(key:'qtr1', data:10 );
      goal.add(key:'qtr2', data:15 );
      goal.add(key:'qtr3', data: 5 );
      goal.add(key:'qtr4', data:15 );
   end;
   set sasuser.contrib;
   goal.find();
   Diff = amount - goalamount;
run;
```

程序一直执行到 `SET` 语句遇到 `sasuser.contrib` 文件的结束。`PROC PRINT` 显示了完成的数据集。

```
proc print data=work.difference;
run;
```

![proc output](img/m57-31.png)

## 从数据集创建哈希对象

假设你需要创建一个显示收入、支出、利润和机场信息的报告。你有两个包含部分数据的数据集。`Sasuser.Revenue` 数据集包含机票收入。`Sasuser.Acities` 数据集包含机场数据，包括机场代码、地点和名称。

表 16.27 `Sasuser.Revenue` 数据集（前五个观测值）

| Origin | Dest | FlightID | Date | Rev1st | RevBusiness | RevEcon |
| --- | --- | --- | --- | --- | --- | --- |
| ANC | RDU | IA03400 | 02DEC1999 | 15829 | 28420 | 68688 |
| ANC | RDU | IA03400 | 14DEC1999 | 20146 | 26460 | 72981 |
| ANC | RDU | IA03400 | 26DEC1999 | 20146 | 23520 | 59625 |
| ANC | RDU | IA03401 | 09DEC1999 | 15829 | 22540 | 58671 |
| ANC | RDU | IA03401 | 21DEC1999 | 20146 | 22540 | 65826 |

表 16.28 `Sasuser.Acities` 数据集（前五个观测值）

| City | Code | Name | Country |
| --- | --- | --- | --- |
| Auckland | AKL | International | New Zealand |
| Amsterdam | AMS | Schiphol | Netherlands |





| Anchorage, AK | ANC | Anchorage International Airport | USA |
| Stockholm | ARN | Arlanda | Sweden |
| Athens (Athanai) | ATH | Hellinikon International Airport | Greece |

要创建此报告，你可以使用哈希对象（hash object）从 `Sasuser.Acities` 中检索匹配的机场数据。在以下代码中，`DECLARE` 语句创建了 `Airports` 哈希对象并从 `Sasuser.Acities` 加载它。

```sas
data work.report;
   if _N_=1 then do;
      declare hash airports (dataset: "sasuser.acities");
```

## 使用非执行的 SET 语句

为了初始化来自现有 SAS 数据集的哈希变量的属性，你可以使用非执行的 `SET` 语句。因为在执行期间 `IF` 条件为假（false），所以 `SET` 语句会被编译但不会执行。程序数据向量（`PDV`）将根据 `Sasuser.Acities` 中的 `Code`、`City` 和 `Name` 变量进行创建。

```sas
data work.report;
   if _N_=1 then do;
      if 0 then
         set sasuser.acities (keep=Code City Name);
```

当你使用这种技术时，不需要 `CALL MISSING`。

## 处理多个数据变量

你在本章之前处理过的哈希对象包含一个键变量（key variable）和一个数据变量。在这个示例中，你需要为每个键关联多个一个数据值。在以下代码中，`DECLARE` 语句创建了 `Airports` 哈希对象并从 `Sasuser.Acities` 加载它。`DEFINEKEY` 方法调用将键定义为变量 `Code` 的值。`DEFINEDATA` 方法调用将数据定义为变量 `City` 和 `Name` 的值。

```sas
data work.report;
      if 0 then
         set sasuser.acities (keep=Code City Name);
   if _N_=1 then do;
   declare hash airports (dataset: "sasuser.acities")
   airports.definekey ("Code");
   airports.definedata ("City", "Name");
   airports.definedone();
end;
```

### 表 16.29 哈希对象机场

| Key: Code | Data: City | Data: Name |
| --- | --- | --- |
| ANC | Anchorage, AK | Anchorage International Airport |
| BNA | Nashville, TN | Nashville International Airport |
| CDG | Paris | Charles de Gaulle |
| LAX | Los Angeles, CA | Los Angeles International Airport |
| RDU | Raleigh-Durham, NC | Raleigh-Durham International Airport |

注：要将所有数据集变量定义为哈希对象的数据变量，请使用 `ALL:` `"YES"` 选项。示例：`hashobject.DEFINEDATA (ALL:"YES");`。
注：哈希对象可以存储多个键变量以及多个数据变量。

## 检索多个数据值

你可以多次使用 `FIND` 方法来检索多个数据值。在程序中，`FIND` 方法根据 `Origin` 的值从 `Airports` 哈希对象中检索 `City` 和 `Name` 的值。

```sas
data work.report;
   if _N_=1 then do;
        if 0 then set sasuser.acities (keep=Code City Name);
      declare hash airports (dataset: "sasuser.acities");
      airports.definekey ("Code");
      airports.definedata ("City", "Name");
      airports.definedone();
   end;
 set sasuser.revenue;
 rc=airports.find(key:origin);
 OriginCity=city;
 OriginAirport=name;
 rc=airports.find(key:dest);
DestCity=city;
DestAirport=name;
run;
```

`PROC PRINT` 输出显示了完整的数据。

```sas
proc print data=work.report;
   var origin dest flightid date origincity originairport
      destcity destairport;
run;
```

图 16.4 部分输出（所选变量的前五个观测值）![Partial Output (first five observations of selected variables)](img/m57-36-g1.png)

## 在 FIND 方法中使用返回代码

记住，方法调用会生成一个数值返回代码，用于指示方法执行成功还是失败。值 `0` 表示方法成功。非零值表示方法失败。要将返回代码的值存储在变量中，请在方法调用开始指定变量名 `RC`。示例所示：

```sas
 rc=hashobject.find (key:keyvalue);
```

返回代码变量可以用于条件逻辑，以确保 `FIND` 方法在哈希对象中找到了与 `PDV` 中的 `KEY` 值匹配的 `KEY`。

## 示例

提交以下程序时，错误信息将写入日志（log）。

```sas
data work.report;
   if _N_=1 then do;
  	     if 0 then set sasuser.acities (keep=Code City Name);
      declare hash airports (dataset: "sasuser.acities");
      airports.definekey ("Code");
      airports.definedata ("City", "Name");
      airports.definedone();
   end;
set sasuser.revenue;
airports.find(key:origin);
OriginCity=city;
OriginAirport=name;
airports.find(key:dest);
DestCity=city;
DestAirport=name;
run;
```

### 表 16.30 SAS 日志

```text
NOTE: There were 50 observations read from the data set SASUSER.ACITIES.
ERROR: Key not found.
ERROR: Key not found.
ERROR: Key not found.
```





# 使用多维数组

当查找操作依赖于多个一个序数数值键时，可以使用多维数组。使用 `ARRAY` 语句创建数组。`ARRAY` 语句定义了一组你计划作为一个整体处理的元素。

## 使用存储的数组值

在许多情况下，你可能更倾向于加载存储在 SAS 数据集（data set）中的数组值，而不是在 `ARRAY` 语句中加载。当满足以下条件时，查找表应存储在 SAS 数据集中：

*   值过多，无法在数组中轻松进行初始化
*   值频繁变化
*   相同的值在许多程序中被使用

从数据集中加载数组的第一步是创建一个数组来存放源数据集中的值。下一步是加载数组元素。完成此任务的方法之一是在 `DO` 循环中中加载数组。最后一步是读取基础数据集。

## 使用 PROC TRANSPOSE

当数据集的方向不同时，可以使用 `PROC TRANSPOSE` 过程来准备数据。`PROC TRANSPOSE` 通过重构 SAS 数据集中的值来创建输出数据集，从而将选定的变量转置为观测值（observations）。然后可以将转置后的（输出）数据集与另一个数据集合并以匹配数据。输出数据集包含几个默认变量。

*   `NAME` 是 `PROC TRANSPOSE` 创建的变量的默认名称，用于识别输出数据集中每个观测值中值的来源。该变量是一个字符变量，其值是从输入数据集中转置的变量名称。要覆盖默认名称，请使用 `NAME=` 选项。
*   剩余的转置变量默认命名为 `COL1...COLn`。要覆盖默认名称，请使用 `PREFIX=` 选项。

## 合并转置后的数据集

你可能需要在使用 `PROC TRANSPOSE` 时配合 `BY` 语句，以便为合并正确结构化数据。对于每个 `BY` 分组，`PROC TRANSPOSE` 为其转置的每个变量创建一个观测值。`BY` 变量本身不会被转置。为了为合并结构化数据，你可能还需要对输出数据集进行排序。任何其他源数据集可能也需要重新组织和排序。当数据结构化正确后，就可以合并数据集。

## 使用哈希对象作为查找表

从 SAS 9 开始，哈希对象（hash object）可以在 `DATA` 步中使用。哈希对象提供了一种高效、方便的机制，用于快速数据存储和检索。哈希对象类似于具有行和列的表格；它包含一个键（key）组件和一个数据组件。与数组使用一系列连续整数来访问数组元素不同，哈希对象可以使用任何数值和字符值的组合作为寻址。

哈希对象是一个 `DATA` 步组件对象。组件对象是由属性和方法组成的数据元素。要在你的 SAS 程序程序使用 `DATA` 步组件对象，你必须首先声明并创建（实例化）该对象。在声明了哈希对象的键组件和数据组件后，你可以从硬编码的值或 SAS 数据集中填充哈希对象。使用 `FIND` 方法调用的返回代码，该代码是一个数值。该值指定了方法执行是成功还是失败。值为 `0` 表示方法成功。非零值表示方法失败。返回代码变量可用于条件逻辑，以确保 `FIND` 方法在哈希对象中找到了与 PDV 中的 `KEY` 值匹配的 `KEY` 值。

## 示例程序

### 使用多维数组

```
data work.wndchill (drop = column row);
  array WC{4,2} _temporary_ 
     (-22,-16,-28,-22,-32,-26,-35,-29);
  set sasuser.flights;
  row = round(wspeed,5)/5;
  column = (round(temp,5)/5)+3;
  WindChill= wc{row,column};
run;
```

### 使用存储的数组值

```
data work.lookup1;
   array Targets{1997:1999,12} _temporary_; 
   if _n_=1 then do i= 1 to 3;
      set sasuser.ctargets;
      array Mnth{*} Jan--Dec;
      do j=1 to dim(mnth);
         targets{year,j}=mnth{j};
      end;
   end;
   set sasuser.monthsum(keep=salemon revcargo monthno);
   year=input(substr(salemon,4),4.); 
   Ctarget=targets{year,monthno}; 
   format ctarget dollar15.2; 
run;
```

### 使用 PROC TRANSPOSE 和合并

```
 proc transpose data=sasuser.ctargets 
      out=work.ctarget2
      name=Month
      prefix=Ctarget;
    by year;
 run;   

proc sort data=work.ctarget2;
   by year month;
run; 

data work.mnthsum2;
   set sasuser.monthsum(keep=SaleMon RevCargo);
   length Month $ 8;
   Year=input(substr(SaleMon,4),4.);
   Month=substr(SaleMon,1,1)
         ||lowcase(substr(SaleMon,2,2));
run; 

proc sort data=work.mnthsum2;
   by year month;
run;

data work.merged;
   merge work.mnthsum2 work.ctarget2;
   by year month;
run;
```

### 从硬编码值加载哈希对象

```
data work.report;
   declare hash h('hash');
   h.define('key', key);
   h.define('data', amount);
   h.define_end();
   h.add_key(1, amount=10);
   h.add_key(2, amount=20);
   set _null_;
   if (h.find(key) = 0) then output;
run;
```

### 从数据集加载哈希对象

```
data work.report;
   declare hash h('hash');
   h.define('key', key);
   h.define('data', amount);
   h.define_end();
   set sasuser.input;
   h.add_key(key, amount);
   set _null_;
   if (h.find(key) = 0) then output;
run;
```

## 注意事项

*   数组的名称必须是 SAS 名称，且不能是 SAS 函数的名称。
*   数组元素必须全为数值或全为字符。
*   数组指定的初始值可以是数值或字符字符串。你必须为字符字符串加上引号。
*   在使用 PROC TRANSPOSE 时，除非使用 `NOTSORT` 选项，否则必须对输入数据集进行排序。
*   哈希对象是无序数据的良好选择，因为它提供了内存中存储和检索，且不需要对数据进行排序。
*   哈希对象的大小是动态的，并在整个 `DATA` 步期间存在。

# 测验

为每个问题选择最佳答案。完成测试后，请参考附录中的答案检查你的结果。

1. 哪个 SAS 语句正确指定了下表所示的 Sales 数组？表格表示
    1.  ```
        array Sales{3,4} m1-m12;
        ```
    2.  ```
        array Sales{4,3} m1-m12;
        ```
    3.  ```
        array {3,4} Sales m1-m12;
        ```
    4.  ```
        array {4,12} Sales m1-m12;
        ```

2. 下哪个语句创建了临时数组元素？
    1.  ```
         array new {*} _temporary_;
        ```
    2.  ```
         array new {6} _temporary_;
        ```
    3.  ```
         array new {*} _temporary_ Jan Feb Mar Apr May Jun;
        ```
    4.  ```
         array _temporary_ new {6} Jan Feb Mar Apr May Jun;
        ```

3. 哪个 DO 语句处理 Yearx 数组中的所有元素？
    ```
    array Yearx{12} Jan--Dec;
    ```
    1.  ```
        do i=1 to dim(yearx);
        ```





2.
```
do i=1 to 12;
```

3.
```
do i=Jan to Dec;
```

4. a 和 b

4. 鉴于以下程序，数据集 `Work.Results` 中第五个观测值的 `Points` 的值是多少？

| SAS 数据集 `Work.Contest` |
| --- |
| |

```sas
data work.results; 
   array score{2,4} _temporary_            
             (40,50,60,70,40,50,60,70);
   set work.contest;
   Points=score{week,finish}; 
run;
```

| ![data work.results](img/m57-42-g2.png) |

1. 40
2. 50
3. 60
4. 70

5. 当满足下列哪种情况为真时，数组值应该存储在 SAS 数据集中？

1. 数组中的值太多，无法方便地初始化。
2. 数值频繁变化。
3. 相同的值在许多程序中使用。
4. 以上所有情况。

6. 鉴于以下程序，哪条说法是不正确的？

```sas
data work.lookup1;
   array Targets{1997:1999,12} _temporary_; 
   if _n_=1 then do i= 1 to 3;
    	           set sasuser.ctargets;
		           array Mnth{*} Jan--Dec;
	           do j=1 to dim(mnth);
		              targets{year,j}=mnth{j};
		           end;
   end;
   set sasuser.monthsum(keep=salemon revcargo monthno);
   year=input(substr(salemon,4),4.); 
   Ctarget=targets{year,monthno}; 
run;
```

1. `IF-THEN` 语句指定 `Targets` 数组加载一次。
2. 在 `DATA` 步的第一次迭代中，外部 `DO` 循环执行三次。
3. 在 `DO` 循环第一次迭代后，指针会移动到第二个 `SET` 语句。
4. 在 `DATA` 步的第二次迭代中，条件 `_N_=1` 为假。因此，`DO` 循环不执行。

7. 鉴于以下程序，哪些变量名会出现在数据集 `Work.New` 中？

| SAS 数据集 `Work.Revenue` |
| --- |
| |

```sas
proc transpose 
     data=work.revenue
     out=work.new;
run;
```

| ![proc transpose](img/m57-42-g3.png) |

1. `Year, Jan, Feb, Mar, Apr`
2. `Year, 2000, 2001, 2002`
3. `_NAME_, Col1, Col2, Col3`
4. `_NAME_, Jan, Feb, Mar, Apr`

8. 哪个程序创建了输出数据集 `Work.Temp2`？

| SAS 数据集 `Work.Temp` | SAS 数据集 `Work.Temp2` |
| --- | --- |
| ![SAS Data Set Work.Temp](img/m57-42-g4.png) | ![SAS Data Set Work.Temp2](img/m57-42-g5.png) |

1. ```sas
proc transpose data=work.temp
     out=work.temp2
     prefix=Quarter;
run;
```
2. ```sas
proc transpose data=work.temp
     out=work.temp2
     name=Month
     prefix=Quarter;
run;
```
3. ```sas
proc transpose data=work.temp
      out=work.temp2
      prefix=Month
      name=Quarter;
     run;
```
4. ```sas
proc transpose data=work.temp
     out=work.temp2
     prefix=Month
     index=Quarter;
run;
```

9. 下列程序创建了哪个版本的 `Work.Sales2` 数据集？

| SAS 数据集 `Work.Sales` |
| --- |
| |

```sas
proc transpose data=work.sales
     out=work.sales2
     name=Week;
     by employee; 
run;
```

| ![proc transpose](img/m57-42-g6.png) |

1. ![observations](img/m57-42-g7.png)
2. ![Observations](img/m57-42-g8.png)
3. ![Observations](img/m57-42-g9.png)
4. ![Observations](img/m57-42-g10.png) |

10. 哪个程序创建了数据集 `Work.Fishsize`？SAS 数据集 `Work.Fishdata`![Observations](img/m57-42-g11.png)SAS 数据集 `Work.Fishsize`![observations](img/m57-42-g12.png)

1. ```sas
proc transpose data=work.fishdata
     out=fishsize
     prefix=size;
run;
```
2. ```sas
proc transpose data=work.fishdata
     out=fishsize
     prefix=size;
run;
```
3. ```sas
proc transpose data=work.fishdata
     out=fishsize
     prefix=size;
run;
```
4. ```sas
proc transpose data=work.fishdata
     out=fishsize
     prefix=size;
run;
```

# 第 17 章 格式化数据

## 概述

## 引言
自定义格式用于以特定方式显示变量值，例如，假设你有一些航空公司数据并希望使用格式将数值显示为文本。你已经熟悉如何使用 `FORMAT` 过程创建格式，本章将学习如何使用 `VALUE` 语句创建格式，以及如何在 SAS 数据集中存储这些格式。

## 使用 VALUE 语句创建格式

### 非重叠格式的回顾
你可以使用 `VALUE` 语句在 `FORMAT` 过程中创建非重叠格式。例如，假设你有一些航空公司数据并需要创建非重叠格式来执行报告任务。你需要格式来执行以下操作：

* 将航空公司路线分组区域
* 将机场代码标记为国际或国内
* 将货物收入分组范围

以下 `PROC FORMAT` 步骤创建了这些格式：

```sas
proc format;
   value $routes
         'Route1' = 'Zone 1'
         'Route2' - 'Route4' = 'Zone 2'
         'Route5' - 'Route7' = 'Zone 3'
         ' ' = 'Missing'
         other = 'Unknown';
   value $dest
         'AKL','AMS','ATH','BKK',
         'CBR','CCU','CDG','CPT','DEL',
         'DXB','FBU','FRA','GVA',
         'HEL','HKG','HND','JED','JNB',
         'JRS','LHR','LIS','MAD','NBO',
         'PEK','PRG','SIN','SYD','VIE','WLG' = 'International'
         'ANC','BHM','BNA','BOS','DFW','HNL',
         'IAD','IND','JFK','LAX','MCI','MIA',
         'MSY','ORD','PWM','RDU','SEA','SFO' = 'Domestic';
   value revfmt
         . = 'Missing'
         low - 10000 = '最多 $10,000'
         10000 <- 20000 = '$10,000 to $20,000'
         20000 <- 30000 = '$20,000 to $30,000'
         30000 <- 40000 = '$30,000 to $40,000'
         40000 <- 50000 = '$40,000 to $50,000'
         50000 <- 60000 = '$50,000 to $60,000'
         60000 <- HIGH  = '超过 $60,000';
run;
```

`PROC FORMAT` 步骤创建了三个格式：`$ROUTES.` 和 `$DEST.` 是字符格式，而 `REVFMT.` 是数值格式。`$ROUTES.` 将航空公司路线分组。在 `$ROUTES.` 中，以下情况为真：

* 单个值和范围都分配了标签
* 缺失值由引号内的空格指定，并分配了标签“Missing”





- 关键字 `OTHER` 用于对任何未在范围内的值分配标签“Unknown”（未知）

`$DEST.` 将机场代码标记为“International”（国际）或“Domestic”（国内）。在 `$DEST.` 中，以下条件成立：

- 唯一的字符值被包含在引号中，并用逗号分隔
- 此格式不处理缺失值以及未包含在范围内的值

`REVFMT.` 将货运收入数字分组为范围。在 `REVFMT.` 中，以下条件成立：

- 使用小于运算符（`<`）显示不包含边界的范围（`10000<-20000` 表示第一个值不包含在范围内）
- 关键字 `LOW` 用于指定变量值范围的下限，但它包含缺失值
- 缺失值用点（`.`）指定并分配标签 `Missing`（缺失）
- 关键字 `HIGH` 用于指定变量值范围的上限

# 创建具有重叠范围的格式

有时，你需要创建一个格式，将相同的值分到不同的范围内。若要创建重叠范围，请在 `PROC FORMAT` 的 `VALUE` 语句中使用 `MULTILABEL` 选项。

| 通用形式，带有 `MULTILABEL` 选项的 `VALUE` 语句： | `VALUE format-name (MULTILABEL);` |
| --- | --- |
| `format-name` 是正在创建的字符或数值格式的名称。 | |

以下是对语法的解释：`format-name` 是正在创建的字符或数值格式的名称。

## 示例

假设你想创建一个日期分组为重叠类别的格式。在下表中，注意每个月份都出现在两个组中。

| 值 (Value) | 标签 (Label) |
| --- | --- |
| Jan - Mar | 第一季度 |
| Apr - Jun | 第二季度 |
| Jul - Sep | 第三季度 |
| Oct - Dec | 第四季度 |
| Jan - Jun | 上半年 |
| Jul- Dec | 下半年 |

在下方的 `PROC FORMAT` 步骤中，添加了 `MULTILABEL` 选项，表示 `DATES.` 格式具有重叠范围的值：

```
proc format;
   value dates (multilabel) 
         '01jan2000'd - '31mar2000'd = '1st Quarter'
         '01apr2000'd - '30jun2000'd = '2nd Quarter'
         '01jul2000'd - '30sep2000'd = '3rd Quarter'
         '01oct2000'd - '31dec2000'd = '4th Quarter'
         '01jan2000'd - '30jun2000'd = 'First Half of Year'
         '01jul2000'd - '31dec2000'd = 'Second Half of Year';
run; 
```

多标签（Multilabel）格式允许观测值包含在多个行或类别中。要使用多标签格式，你可以在支持它的过程在类变量上指定 `MLF` 选项：

- `PROC TABULATE`
- `PROC MEANS`
- `PROC SUMMARY`

当将多标签格式分配给类变量时，`MLF` 选项会激活多标签格式处理。例如，这些语句对于以下 `TABULATE` 过程代码是正确的：

- `FORMAT=` 选项指定 `DOLLAR15.2` 为每个表格单元格中值的格式
- `CLASS` 语句将 `Date` 识别为类变量，并使用 `MLF` 选项激活多标签格式处理。
- `TABLE` 语句的行维度为每个格式化后的 `Date` 值创建一个行。
- `FORMAT` 语句为类变量 `Date` 引用了新格式 `DATES.`。

```
proc tabulate data = sasuser.sale2000 format = dollar15.2;
   class Date / mlf;
   var RevCargo;
   table Date, RevCargo*(mean median);
   format Date dates.;
run;
```

![RevCargo](img/m58-5-g1.png) 提示：关于使用 `MULTILABEL` 选项的更多信息，请参阅 SAS `FORMAT` 过程文档。

# 使用 PICTURE 语句创建自定义格式

## 概述

你已经学习了 `VALUE` 语句可以将文本标签与离散数值或字符值相关联。假设你想在数值值中插入文本字符。例如，你可能将电话号码存储为数值（如 `1111231234`），并想将其显示为 `(111) 123-1234`。你可以使用 `PICTURE` 语句为打印数字创建一个模板。

| 通用形式，带有 `PICTURE` 语句的 `PROC FORMAT`： | `PROC FORMAT;PICTURE format-namevalue-or-range='picture';RUN;` |
| --- | --- |
| `format-name` 是你正在创建的格式的名称。 | |
| `value-or-range` 是你想标记的单个值或值范围。 | |
| `picture` 指定了格式化数值变量值的模板。该模板是引号括括的字符序列。图片的最大长度为 40 个字符。 |

## 指定图片的方法

图片使用三种类型的字符进行指定：

- 数字选择器（digit selectors）
- 消息字符（message characters）
- 指令（directives）

考虑先使用数字选择器和消息字符。你将在稍后的主题中学习指令。数字选择器是数字（`0` 到 `9`），用于定义数字的位置。如果你使用非零数字选择器，则根据需要向格式化值中添加零。如果你使用零作为数字选择器，则不会向格式化值中添加零。在下方的图片定义中，你可以看到非零选择器（`9`）和零选择器（`0`）的区别。

| 图片定义 | 数据值 | 格式化后的值 |
| --- | --- | --- |
| `picture month 99` | 1 | 11 |
| `picture month 00` | 1 | 01 |

消息字符是要打印的非数字字符。数字选择器必须位于消息字符之前。前缀选项（prefix option）可追加文本。

| 图片定义 | 数据值 | 格式化后的值 |
| --- | --- | --- |
| `picture month='99'` | 1 | JAN |
| `picture month='00'` | 1 | 1 |

## 示例

以下 `PICTURE` 语句包含了数字选择器和消息字符。`RAINAMT.` 格式对带有前导零的值使用零选择器。

```
proc format;
   picture rainamt
           0-2='99 slight'
           2-4='99 moderate'
           4-10='99 heavy'
           other='999 check';
run;
data rain;
   input Amount;
   datalines;
   4
   3.9
   20
   .5
   6
;
proc print data=rain;
   format amount rainamt.;
run;
```

以下输出显示了应用 `RAINAMT.` 格式的值。

# 使用指令使用 PICTURE 语句

指定图片的最后一种方法是使用指令。如果你使用指令，你必须在 `PICTURE` 语句中指定 `DATATYPE=` 选项。该选项指定图片适用于 SAS 日期、SAS 时间或 SAS 日期时间。

| 通用形式，带有 `DATATYPE=` 选项的 `PICTURE` 语句： | `PICTURE format-namevalue-or-range, 'picture' (DATATYPE=SAS-date-value-type);` |
| --- | --- |

## 指定指令的指南

百分号（%）后跟字母表示指令。用于创建图片格式的指令列如下表所示。

| 指令 | 结果 |
| --- | --- |
| %a | 缩写的星期名称 |
| %A | 完整的星期名称 |
| %b | 缩写的月份名称 |
| %B | 完整的月份名称 |
| %d | 日期中的数字（1-31），无前导零 |
| %H | 24 小时制的小时（0-23），无前导零 |
| %I | 12 小时制的小时（1-12），无前导零 |
| %j | 年中的天数（1-366），无前导零 |
| %m | 月份数字（1-12），无前导零 |





| %M | 0-59 之间的分钟小数，不带前导零 |
| %p | AM 或 PM |
| %S | 0-59 之间的秒数，不带前导零 |
| %U | 年周数（星期日为一周的第一天），0-53 之间的数字，不带前导零 |
| %w | 星期几（1=星期日，到 7） |
| %y | 0-99 之间的年份（不世纪），不带前导零 |
| %Y | 带有世纪的年份 |

尽管指令通常返回不带前导零的数字，但你可以在指令中添加 `0`，这样如果返回的是一位数，则会在其前面加一个 `0`。如下所示，当你使用指令创建图形（picture）时，引号内的字符数是格式化后值的最大长度。如果你的值包含的字符比图形多，必须向指令中添加末尾空格。否则，格式化后的值将被截断。![directives](img/m58-8-g2.png)

## 示例

假设你想以 `dd-mmmyyyy` 格式显示员工入职日期（例如 `25-JAN2000`）。该格式需要 10 个字符的空间。以下代码创建了这种格式。关于图形定义，你需要注意以下几点：

- 使用 `LOW` 和 `HIGH` 关键字包含所有值。
- `%d` 指令中的 `0` 表示如果日几为一位数，则应在其前面加一个 `0`。
- 因为单引号内只有八个字符，你必须添加两个空格来将长度设为 10。

```
proc format;
   picture mydate
           low-high='%0d-%b%Y  ' (datatype=date);
run;

proc print data=sasuser.empdata 
     (keep=division hireDate lastName obs=5);
   format hiredate mydate.;
run;
```

下面的输出显示了使用 `MYDATE.` 图形格式化的 `HireDate` 值。![MYDATE. picture format](img/m58-8-g1.png)提示：有关关于使用 `PICTURE` 语句的更多信息，请参阅 `FORMAT` 过程的文档。

# 管理自定义格式

## 使用 PROC FORMAT 配合 FMTLIB 记录格式

当你创建了大量的永久格式时，很容易忘记特定格式名称的精确拼写或其值范围。记住，在 `PROC FORMAT` 语句中添加关键字 `FMTLIB` 可以显示指定目录中所有格式的列表，以及它们取值的描述。

```
libname myfmts 'c:\sas\newfmt';
proc format lib=myfmts fmtlib;
run;
```

你还可以使用 `SELECT` 和 `EXCLUDE` 语句来处理特定的格式，而不是整个目录。

| 通用形式，带有 `FMTLIB` 以及 `SELECT` 和 `EXCLUDE` 语句的 `PROC FORMAT`：`PROC FORMAT LIB=library FMTLIB;SELECT format-name;EXCLUDE format-name;RUN;`这里是对语法的解释：`library` 是存储格式的库名称。如果你未指定 `LIB=` 选项，将列出 `Work` 库中的格式。`format-name` 是你想选择或排除的格式。 |

## 示例

以下代码仅显示 `$ROUTES.` 格式的文档。注意，在 `SELECT` 语句中指定格式时，格式名称末尾不需要加点。

```
libname myfmts 'c:\sas\newfmt';
proc format lib=myfmts fmtlib;
   select $routes;
run;
```

表 17.1 SAS 输出

| FORMAT NAME : $ROUTES LENGTH: 7 NUMBER OF VALUES: 5 MIN LENGTH: 1 MAX LENGTH: 40 DEFAULT LENGTH: 7 FUZZ: 0 |
| --- |
| START | END | LABEL (VER. V7&#124|V8 29AUG2002:11:13:14) |
| | | Missing |
| Route1 | Route1 | Zone 1 |
| Route2 | Route4 | Zone 2 |
| Route5 | Route7 | Zone 3 |
| OTHER | OTHER | Unknown |

提示如果你在 `SELECT` 或 `EXCLUDE` 语句上指定了多个格式，请按如下方式用空格分隔每个格式名称：

```
select $routes newdate;
```

## 使用 PROC CATALOG 管理格式

由于格式是保存为目录项（catalog entries），你可以使用 `CATALOG` 过程来管理你的格式。使用 `PROC CATALOG` 允许你执行以下操作：

- 创建目录内容的列表
- 复制目录或目录中的选项
- 删除或重命名目录中的项

| 通用形式，`PROC CATALOG` 步骤：`PROC CATALOG CATALOG=libref.catalog;CONTENTS <OUT=SAS-data-set>;COPY OUT=libref.catalog <options>;SELECT entry-name.entry-type(s);EXCLUDE entry-name.entry-type(s);DELETE entry-name.entry-type(s);RUN;QUIT;`这里是对语法的解释：带有 `CATALOG=` 参数的 `libref.catalog` 是要处理的 SAS 目录。`SAS-data-set` 是包含目录列表的数据集名称。带有 `OUT=` 参数的 `libref.catalog` 是将项复制到的 SAS 目录。`entry-name.entry-type(s)` 是要处理的目录项全名。 |

## 示例

第一个 `PROC CATALOG` 步骤将 `$ROUTES.` 格式从 `Library.Formats` 目录复制到 `Work` 目录。注意在 `SELECT` 语句中指定了格式名称。

```
proc catalog catalog=myts.formats;
   copy out=work.formats;
   select $routes;
run;
```

`step` 步骤显示了 `Work.Formats` 的内容。当格式被复制时，日志中会写入一条注释。![Contents of WORK.FORMATS](img/m58)
```

# 使用自定义格式

## 概述

在创建自定义格式后，你可以使用 SAS 语句在 `DATA` 步骤中将格式永久分配给变量，可以在 `PROC` 步骤中临时指定格式以确定数据值的显示方式。你应该已经熟悉在 `FORMAT` 语句中引用格式。另一种为现有数据集中的变量分配、更改或删除格式的方法是使用 `DATASETS` 过程。

| 通用形式，带有 `MODIFY` 和 `FORMAT` 语句的 `DATASETS` 过程：`PROC DATASETS LIB=SAS-library <NOLIST>;MODIFY SAS-data-set;FORMAT variable(s) format;QUIT;`这里是对语法的解释：`SAS-library` 是包含要修改数据的 SAS 库名称。`NOLIST` 抑制目录列表。`SAS-data-set` 是要修改的数据集名称。`variable` 是你想分配、更改或删除格式的一个或多个变量的名称。`format` 是应用于前面的变量或变量的格式名称。如果你没有指定格式，则会删除与变量关联的任何格式。 |

注意：`DATASETS` 过程是交互式的，在执行 `QUIT` 语句之前它一直留在内存中。

## 示例

在以下代码中，`Flights` 数据集中的两个变量被更改了。`$DEST.` 格式关联变量 `Dest`，并从变量 `Baggage` 删除了格式。

```
proc datasets lib=Mylib;
   modify flights;
   format baggage;
```

## 使用永久位置存储格式

当你为数据集中的变量永久关联格式时，重要的是确保你引用的格式存储在永久位置。记住格式的存储位置是在 `FORMAT` 过程中创建格式时确定的。当你要在后续 SAS 会话中使用格式时，采取这些步骤非常有用：

1. 在运行 `PROC FORMAT` 步骤的 SAS 会话中将库 `libref` 分配给 SAS 库。
2. 在创建格式的 `PROC FORMAT` 步骤中指定 `LIB=LIBRARY`。




### 3. 在程序中包含引用格式的 `LIBNAME` 语句，将库引用 `libref` 分配给包含永久格式目录的库。

你可以将格式存储在所选择的任何目录（catalog）中。然而，在访问它们之前，你必须向 `SAS` 标识格式目录。你将在后面的主题中学习到这一内容。当引用格式时，`SAS` 会按照以下顺序自动查找这些库：

1. `Work.Formats`
2. `Library.Formats`

建议对格式使用 `Library` 库引用，因为在引用格式时，它会被自动搜索。如果你将格式存储在默认搜索路径中的这些库之外的库或目录中，则你必须使用 `FMTSEARCH=` 系统选项来告诉 `SAS` 在何处找到你的格式。

| 通用形式，`FMTSEARCH=` 系统选项：`OPTIONS FMTSEARCH=(catalog-1 catalog-2...catalog-n);` | 此处是该语法的解释：`catalog` 是要搜索的一个或多个目录的名称。`catalog` 的值可以是 `libref` 或 `libref.catalog`。如果只给出 `libref`，则 `SAS` 假设目录名为 `Formats`。 |

`Work.Formats` 目录总是第一个被搜索，接着搜索 `Library.Formats` 目录，除非其中一个或两个目录出现在 `FMTSEARCH=` 列表中。

## 示例

假设你有一个存储在 `Rpt` 库和 `Prod.Newfmt` 目录中的格式。以下 `OPTIONS` 语句告诉 `SAS` 在何处找到你的格式：

```
options fmtsearch=(rpt prod.newfmt);
```

由于没有为 `Rpt` 库引用指定目录，因此假设了默认目录名 `Formats`。此 `OPTIONS` 语句创建了以下搜索顺序：![Search order](img/m58-18-g1.png) 由于 `FMTSEARCH=` 选项中未指定 `Work` 和 `Library` 库引用，因此将按照默认顺序进行搜索。

#### 避免格式错误

考虑一下如果你忘记在 `FMTSEARCH=` 选项中指定目录、拼写错误的格式名称，或者犯了其他导致 `SAS` 无法找到你指定的格式的错误会发生什么。

默认情况下，`FMTERR` 系统选项生效。如果你使用 `SAS` 无法加载的格式，`SAS` 会发出错误消息并停止处理该步骤。为了防止这种情况，你必须将系统选项 `FMTERR` 改为 `NOFMTERR`。当 `NOFMTERR` 生效时，`SAS` 会用默认格式替换缺失的格式并继续处理。

| 通用形式，`FMTERR` 系统选项：`OPTIONS FMTERR | NOFMTERR;` | 此处是语法的解释：`FMTERR` 指定当 `SAS` 找不到指定的变量格式时，它会生成错误消息并停止处理。不会发生默认格式替换。`NOFMTERR` 将缺失的格式替换为 `w.` 或 `$w.` 默认格式并继续处理。 |

## 示例

假设 `FMTERR` 系统选项生效。在之前的示例中，我们创建了 `$ROUTES.` 格式将航空公司路线分组到不同的区域。在下面的代码中，`$ROUTES.` 格式拼写错误了：

```
proc print data=sasuser.cargorev(obs=10);
   format route $route.;
run;
```

由于 `FMTERR` 生效，无法找到格式，`SAS` 停止处理该步骤。错误消息被写入日志中。

表 17.2 SAS 日志

| |
| ```
30   proc print data=sasuser.cargorev(obs=10);
31      format route $route.;
ERROR: The format $ROUTE was not found or could not be loaded.
32   run;

NOTE: The SAS System stopped processing this step because of errors.
``` | |

如果指定了 `NOFMTERR` 系统选项，则会发生默认格式替换，`SAS` 继续处理该步骤。

```
options nofmterr;
proc print data=sasuser.cargorev(obs=10);
   format Route $route.;
run;
```

`SAS` 用 `$w.` 格式替换了无法找到的 `$ROUTE.` 格式。日志中没有写入消息，处理继续。你可以从输出中看到，你打算使用的格式尚未应用。![RevCargo](img/m58-20-g1.png)

### 从 SAS 数据集创建格式

## 概述

你已经看到可以在 `PROC FORMAT` 步骤中指定值和标签来创建格式。你也可以从包含值信息（称为控制数据集）的 SAS 数据集创建格式。要此此，你使用 `CNTLIN=` 选项读取数据并创建格式。

| 通用形式，`PROC FORMAT` 中的 `CNTLIN=` 选项：`PROC FORMAT LIBRARY=libref.catalog CNTLIN=SAS-data-set;` | 此处是语法的解释：`libref.catalog` 是你想要存储格式的目录名称。`SAS-data-set` 是你用来创建格式的 SAS 数据集的名称。 |

## 示例

假设你有一个名为 `Routes` 的 SAS 数据集，其中包含创建格式所需的变量。你如下所示在 `CNTLIN=` 选项中指定数据集：

```
proc format lib=myfmts cntlin=routes;
run;
```

你可以看到，从数据集创建格式的代码是简单的。然而，在创建格式之前，控制数据集必须包含某些变量。因此，大多数数据集在创建格式之前必须进行重组。

#### 控制数据集的规则

当你使用程序语句来创建格式时，你需要指定格式名称、范围值以及每个范围或值的标签，如 `VALUE` 语句所示：

```
value rainfall 'none';
```

创建格式的控制数据集必须提供这些信息。也就是说，`CNTLIN=` 选项指定的数据集必须满足以下要求：

- 它必须包含 `FmtName`、`Start` 和 `Label` ，分别对应格式名称、范围起始值和标签。
- 如果指定了范围，它必须包含 `End`。如果没有 `End`，`SAS` 假设范围的结束值等于 `Start` 值。
- 对于字符格式，它必须包含 `Type` ，除非 `FmtName` 以 `$` 开头。
- 如果指定了多个格式，它必须按 `FmtName`分组。

## 示例

## 概述

假设你想将三字母机场代码标记为机场所在的城市。你有一个包含机场代码和机场城市的数据集 `Acities`。然而，该数据没有 `CNTLIN=` 选项所需的变量。

表 17.3 SAS 数据集 Sasuser.Acities（部分列表）

| 机场所在城市 | 起点 | 机场名称 | 机场所在国家 |
| --- | --- | --- |
| Auckland | AKL | International | 新西兰 |
| Amsterdam | AMS | Schiphol | 荷兰 |
| Anchorage, AK | ANC | International Airport | 美国 |
| Stockholm | ARN | Arlanda | 瑞典 |
| Athens (Athanai) | ATH | Hellinikon International Airport | 希腊 |
| Birmingham, AL | BHM | Birmingham International Airport | 美国 |
| Bangkok | BKK | Don Muang International Airport | 泰国 |

从该数据集创建格式，你需要：

1. 列出数据集变量。
2. 重组数据。

#### 步骤 1：列出数据集变量

记得你需要 `FmtName`、`Start` 和 `Label`。你可以提交一个 `PROC CONTENTS` 步骤来获取 `sasuser.acities` 数据集的变量列表。

| 部分输出 |
| --- |
| ```
proc contents data=sasuser.acities; 
run;
``` |
![部分输出](img/m58-24-g1.png)

提示你还可以通过 `PROC DATASETS` 配合 `CONTENTS` 语句，或者在 SAS Explorer 窗口中查看 SAS 数据集的属性来获取变量列表。

#### 步骤 2：重组数据




一旦你查看了数据并知道了变量名，就可以准备编写一个 `DATA` 步来处理数据了。变量 `Code` 是三字母机场代码，变量 `City` 是机场所在的城市。你可以将变量 `Code` 重命名为 `Start`，将变量 `City` 重命名为 `Label`，但你还需要创建一个名为 `FmtName` 的变量。以下代码是准备你的数据的一种高效方法。该 `DATA` 步使用了以下语句：

*   使用 `KEEP` 语句仅将指定的变量写入输出数据集。
*   使用 `RETAIN` 语句（保留）创建变量 `FmtName` 并将其值设置为 `'$airport'`。
*   使用 `RENAME` 数据集选项将变量 `Code` 重命名为 `Start`（你不需要名为 `End` 的变量，因为你正在标记离散值，范围范围），并将变量 `City` 重命名为 `Label`。

```
data sasuser.aports;
   keep Start Label FmtName;
   retain FmtName '$airport';
   set sasuser.acities (rename=(Code=Start 
       City= Label));
run;

proc print data=sasuser.aports(obs=10) noobs;
run;
```

下面是新数据集 `Sasuser.Aports` 中前十个观测值的列表![前十个观测值](img/m58-24-g2.png) 该数据集现在已经是正确的格式，可以使用 `CNTLIN=` 选项来创建格式。一旦数据格式正确，你就可以使用 `CNTLIN=` 选项来创建格式。第一个 `PROC FORMAT` 步从数据集 `Sasuser.Aports` 创建了一个格式。第二个 `PROC FORMAT` 步对该新格式进行文档说明。

```
proc format library=sasuser cntlin=sasuser.aports;
run;

proc format library=sasuser fmtlib;
   select $airport;
run;
```

输出的前几行所示所示。

表 17.4 部分 SAS 输出

| FORMAT NAME : $AIRPORT LENGTH: 22 NUMBER OF VALUES: 52 MIN LENGTH: 1 MAX LENGTH: 40 DEFAULT LENGTH: 22 FUZZ: 0 |
| --- |
| START | END | LABEL (VER. V7&#124;V8 21OCT2002:14:13:14) |
| AKL | AKL | Auckland |
| AMS | AMS | Amsterdam |
| ANC | ANC | Anchorage, AK |
| ARN | ARN | Stockholm |
| ATH | ATH | Athens (Athanai) |
| BHM | BHM | Birmingham, AL |
| BKK | BKK | Bangkok |

## 应用格式

考虑应用于数据集 `Sasuser.Cargo99` 的格式。以下 `PROC PRINT` 代码将 `$AIRPORT.` 格式分配给 `Dest` 和 `Origin` 变量：

```
options fmtsearch=(sasuser);
proc print data=sasuser.cargo99 (obs=5);
   var origin dest cargorev;
   format origin dest $airport.;
run;
```

| ![Sasuser.Cargo99](img/m58-25-g1.png) |

提示：有关关于使用 `CNTLIN=` 选项的更多信息，请参阅 `FORMAT` 过程的 SAS 文档。

# 从自定义格式创建 SAS 数据集

## 概述

你知道如何从 SAS 数据集创建格式，但如果你想从格式创建 SAS 数据集怎么办？要实现这一点，你需要使用 `CNLOUT=` 选项。

| `PROC FORMAT` 中 `CNLOUT=` 选项的一形式：`PROC FORMAT LIBRARY=libref.catalog CNTLOUT=SAS-data-set;SELECT format-name format-name...;EXCLUDE format-name format-name...;RUN;` | 这里是对该语法的解释：`libref.catalog` 是格式所在目录的名称。`SAS-data-set` 是你想创建的 SAS 数据集的名称。`format-name` 是你想要选择或排除的格式名称。 |

输出控制数据集将包含完全描述每个格式所有方面的变量，包括可选设置。输出数据集包含指定目录每个每个格式的每个范围一个观测值。你可以使用 `SELECT` 或 `EXCLUDE` 语句将特定格式包含在数据。当你需要修改格式但不再拥有用于创建该格式的 SAS 数据集时，从格式创建 SAS 数据集非常有用。当你需要更新格式时，请采取以下操作：

1.  使用 `CNLOUT=.` 从格式中的值创建 SAS 数据集。
2.  使用任意方法编辑数据集。
3.  使用 `CNTLIN=.` 从更新后的 SAS 数据集创建格式。

## 示例

## 概述

在上一个示例中，你创建了 `$AIRPORT.` 格式。假设你想向格式添加以下机场代码![机场代码](img/m58-31-g2.png)

### 第 1 步：从格式创建 SAS 数据集

首先，将 `$AIRPORT.` 格式写为 SAS 数据集。在下面的代码中，输出数据集命名为 `Sasuser.Fmtdata`。使用 `SELECT` 语句是为了使生成的数据集仅包含 `$AIRPORT.` 的数据。

```
proc format;
   out=sasuser.fmtdata;
   run;
```

当你使用 `CNLOUT=` 选项时，输出数据集包含了关于格式的每个。`sasuser.fmtdata` 数据集具有相同的观测值。在 `PRINT` 过程中，`VAR` 语句指定了其中的几个：

```
proc print data=sasuser.fmtdata (obs=5) noobs;
   var fmtname start end
       default;
run;
```

![Sasuser.Cargo99](img/m58-25-g1.png)

等待，更新格式的下一步是编辑数据集。你可以使用 `PROC SQL` 或 `DATA` 步向数据集添加观测值。无论你选择哪种方法，都必须添加 `Start` 和 `End` 的取值。如果 `Start` 和 `End` 同时存在，SAS 将返回错误。你不需要添加数据集的其他变量。

### 第 3 步：从数据集创建格式

一旦数据集经过编辑并保存，你就可以 `CNTLIN=` 选项从数据集创建格式。以下代码创建 `$AIRPORT.` 格式，然后使用 `FMTLIB` 对其进行文档说明：

```
proc format library=sasuser cntlin=sasuser.fmtdata;
run;

proc format library=sasuser fmtlib;
   select $airport;
run;
```

输出的前几行所示所示。

所示的部分输出包含了格式中的新机场。

表 17.5 部分 SAS 输出

| FORMAT NAME : $AIRPORT LENGTH: 22 NUMBER OF VALUES: 56 MIN LENGTH: 1 MAX LENGTH: 40 DEFAULT LENGTH: 22 FUZZ: 0 |
| --- |
| START | END | LABEL (CONT'D) |
| SYD | END | Sydney, New South Wales |
| VIE | VIE | Wien (Vienna) |
| WLG | WLG | Wellington |
| YQB | YQB | Quebec, QC |
| YUL | YUL | Montreal, QC |
| YYC | YYC | Calgary, AB |
| YYZ | YYZ | Toronto, ON |

## 总结

## 

### 使用 VALUE 语句创建自定义格式

通过 `FORMAT` 过程中的 `VALUE` 语句创建字符和数值格式。当你指定 `libref` 时，格式存储在指定的库中。

### 创建具有重叠范围的格式

使用 `MULTILABEL` 选项创建具有重叠范围的格式。当格式具有重叠范围时，格式中的值可能有多个标签。该格式可以使用支持 `MLF` 选项的过程。

### 使用 PICTURE 语句创建自定义格式

`PICTURE` 语句用于为数值变量的值创建格式化模板。图片使用数字选择器、消息字符和指令来定义。




在 `PROC FORMAT` 语句中使用 `FMTLIB` 关键字可以获取指定目录中格式的文档。输出将显示格式名称、起始和结束值以及标签。您还可以使用 `SELECT` 和 `EXCLUDE` 语句来处理特定格式，而不是整个目录。

## 管理格式

由于格式被存储为目录条目，因此您可以使用 `PROC CATALOG` 来复制、重命名、删除或创建目录中条目的列表。

## 使用自定义格式

一旦您创建了格式，就可以像引用 SAS 格式一样引用它。如果您将格式存储在 ` `Work.Formats` 以外的位置，则必须使用 `FMTSEARCH=` 系统选项将该位置添加到搜索路径中，以便 SAS 能够找到该格式。将默认的 `FMTERR` 系统选项更改为 `NOFMTERR` 可能很有用。更改默认系统选项后，如果 SAS 无法找到您引用的格式，它将替换 `w.` 或 `$w.` 格式并继续处理。您可以通过使用 `PROC DATASETS` 修改数据集，将格式与变量永久关联。

## 从 SAS 数据集创建格式

使用 `CNTLIN=` 选项指定一个用于创建格式的 SAS 数据集。该 SAS 数据集必须包含 `FmtName`、`Start` 和 `Label` 变量。如果值具有范围，则必须存在 `End` 变量。

## 从格式创建 SAS 数据集

使用 `CNTLOUT=` 选项从格式创建 SAS 数据集。这对维护格式非常有用，因为您可以轻松地更新 SAS 数据集。

## 示例

### 创建多标签格式

```
proc format;
   value dates (multilabel)
         '01jan2000'd - '31mar2000'd = '1st Quarter'
         '01apr2000'd - '30jun2000'd = '2nd Quarter'
         '01jul2000'd - '30sep2000'd = '3rd Quarter'
         '01oct2000'd - '31dec2000'd = '4th Quarter'
         '01jan2000'd - '30jun2000'd = 'First Half of Year'
         '01jul2000'd - '31dec2000'd = 'Second Half of Year';
run;
```

### 创建图片格式

```
proc format;
   picture rainamt
           0-2='9.99 slight'
           2<-4='9.99 moderate'
           4<-<10='9.99 heavy'
           other='999 check value';
run;
```

### 使用指令创建图片格式

```
proc format;
   picture mydate
           low-high='%0d-%b%Y  ' (datatype=date);
run;
```

### 重构 SAS 数据集并从数据创建格式

```
data sasuser.aports;
   keep Start Label FmtName;
   retain FmtName '$airport';
   set sasuser.acities (rename=(Code=Start
       City= Label));
run;

proc format library=sasuser cntlin=sasuser.aports;
run;
```

### 从格式创建 SAS 数据集

```
proc format library=sasuser cntout=sasuser.formats;
run;
```

## 注意事项

- 由于格式被存储为目录条目，因此您可以使用 `PROC CATALOG` 来复制、重命名、删除或创建目录中条目的列表。
- 默认情况下，SAS 会搜索格式。如果您将格式存储在 `Work.Formats` 以外的位置，则必须使用 `FMTSEARCH=` 系统选项将该位置添加到搜索路径中。以便 SAS 能够找到该格式。将默认的 `FMTERR` 系统选项更改为 `NOFMTERR` 可能很有用。更改默认系统选项后，如果 SAS 无法找到您引用的格式，它将替换 `w.` 或 `$w.` 格式并继续处理。
- 您可以通过使用 `PROC DATASETS` 修改数据集，将格式与变量永久关联。
- 使用 `CNTLIN=` 选项指定一个用于创建格式的 SAS 数据集。该 SAS 数据集必须包含 `FmtName`、`Start` 和 `Label` 变量。如果值具有范围，则必须存在 `End` 变量。
- 使用 `CNTLOUT=` 选项从格式创建 SAS 数据集。这对维护格式非常有用，因为您可以轻松地更新 SAS 数据集。
- 在 `PROC FORMAT` 语句中使用 `FMTLIB` 关键字可以获取指定目录中格式的文档。

# 测验

1. 使用哪个系统选项来识别格式？
    a. `NOFMTERR`
    b. `FMTLIB`
    c. `CATALOG`
    d. `FMTSEARCH=`

2. 给定以下 OPTIONS 语句，SAS 将以什么顺序搜索以找到用户定义的格式？
    ```
    options fmtsearch=(work abc.newfmt sasuser);
    ```
    a. `Work.Formats>Library.Formats>Abc.Newfmt>Sasuser.Formats`
    b. `Work.Formats>Library.Formats>Abc.Newfmt>Sasuser`
    c. `Work.Formats>Abc.Newfmt>Sasuser.Format`

3. 当 `NOFMTERR` 生效时，当 SAS 遇到无法找到的格式时会发生什么？
    a. 创建默认格式。
    b. 替换 `w.` 或 `$w.` 格式并继续处理。
    c. 停止处理并向日志写入错误。
    d. 跳过下一步。

4. `CNTLIN=` 必须包含以下哪些变量？
    a. `End`
    b. `FmtName`
    c. `Value`
    d. `Description`

5. 给定以下代码，缺少哪个选项？
    ```
    proc format;
       value times
             '00:00'-04:59' = 'Red'
             '05:00'-11:59' = 'Morning'
             '12:00'-17:59' = 'Afternoon'
             '18:00'-23:59' = 'Evening';
    run;
    ```
    a. `MULTABEL`
    b. `MULTIRANGE`
    c. `ML`
    d. `MULTIFMAT`

6. 使用哪个选项从格式创建 SAS 数据集？
    a. `CNTLIN=`
    b. `LIB=`
    c. `CNTLOUT=`
    d. `FMTLIB`

7. `PROC FORMAT` 使用哪个选项来获取特定目录中的格式文档？
    a. `FMTSEARCH`
    b. `FMTERR`
    c. `CATALOG`
    d. `FMTLIB`

8. 将将哪些语句添加到 `PROC CATALOG` 代码中，将 `Sasuser.Formats` 目录中的 `LEVELS.` 和 `$PICKS.` 格式复制到 `Work.Formats` 目录？
    ```sas
    proc catalog cat=sasuser.formats;
        ?
        ?
    run;
    ```
    a. `copy out=sasuser.formats; select levels.format $picks.format;`
    b. `copy out=work.formats; select levels $picks;`
    c. `copy out=work.formats; select levels.format picks.formatc;`
    d. `copy out=work.formats; select levels.format $picks.format;`

9. 给定以下 `PROC FORMAT` 步骤，当应用 `SKICOND` 格式时，值 6.1 如何显示？
    ```
    proc format;
       value skicond
              0-3='Poor'
              3<-6='Fair'
              6<-9='Good'
              9<-high='Excellent';
    run;
    ```
    a. 6.1
    b. Fair
    c. Good
    d. .




## 概述

## 引言

有时，你希望在不替换整个数据集的情况下修改 SAS 数据集的观测值。你可以在 DATA 步中使用 `MODIFY` 语句来实现。通过使用 `MODIFY` 语句，你可以在不创建额外额外副本的情况下，替换、删除或追加现有数据集中的观测值。在本章中，你将学习修改数据集中的所有观测值、使用 `BY` 语句匹配观测值，以及使用索引定位观测值。在修改数据时，保护你的数据并跟踪所做的更改通常是关重要的。在本章中，你将学习如何创建完整性约束来保护你的数据。你还将学习两种跟踪更改的不同方法：审计跟踪（audit trails）和生成数据集（generation data sets）。你使用审计跟踪来跟踪对数据集进行原地修改的更改，并使用生成数据集来跟踪在重建数据集时所做的更改。

# 使用 MODIFY 语句

当你提交一个带有 `MERGE`、`UPDATE` 或 `SET` 语句的 DATA 步时，如果输出数据集已经存在，SAS 会创建输出数据集的第二个副本。执行完成后，SAS 会删除数据的原始副本。结果是原始数据集被具有相同名称的新数据集替换。新数据集可能包含与原始数据集不同的变量集。新数据集中的变量属性可能与原始数据集不同。![set statement](img/m59-2-g1.png) 相此，当你提交一个带有 `MODIFY` 语句的 DATA 步时，输入输出数据集必须相同。SAS 不会创建数据的第二个副本，而是对数据集进行原地更新。新变量可以添加到程序数据向量 (PDV) 中，但它们不会写入数据集。因此，在修改数据时，数据集中的变量集改变。![MODIFY statement](img/m59-2-g2.png) 当你使用 `MODIFY` 语句时，DATA 步底部有一个隐含的 `REPLACE` 语句而不是 `OUTPUT` 语句。使用 `MODIFY` 语句，你可以更新：

* 数据集中的每个观测值
* 使用事务数据集和 `BY` 语句的观测值
* 使用索引定位的观测值

警告：如果使用 `MODIFY` 语句的 DATA 步在处理过程中异常终止，可能会丢失数据并可能损坏主数据集。你可以通过以下操作从失败中恢复：

* 从备份恢复主数据集并重启该步，或
* 保留审计跟踪文件并使用它确定哪些主观测值已更新。

首先我们考虑使用 `MODIFY` 语句修改数据集中的所有观测值。

# 修改 SAS 数据集中所有观测值

## 概述

当 SAS 数据集中的每个观测值都需要相同的修改时，可以使用 `MODIFY` 语句并使用赋值语句指定修改内容。

| 带有赋值语句的 MODIFY 语句通用形式：
```
DATA SAS-data-set;
MODIFY SAS-data-set;
existing-variable = expression;
RUN;
```
以下是对语法的解释：
SAS-data-set 是你想要修改的数据集名称。
existing-variable 是你想要更新的变量名称。
expression 是你想要应用的函数或其他表达式。 |

## 示例

假设某航空公司决定为乘客提供更多空间。该航空公司必须减少商务舱和经济舱的座位数量。SAS 数据集 `Capacity` 具有 `Econ` 和 `Business` 变量，存储了座位数量的值。在下面的程序中，`Econ` 的赋值语句将经济舱的座位数减少到原始数量的 95%，`Business` 的赋值语句将商务舱的座位数减少到原始数量的 90%。两个赋值语句都使用了 `INT` 函数来返回结果的整数部分。注意：如果你选择运行此示例，必须从 `sasuser` 库将数据集 `Capacity` 复制到 `work` 库。

```
proc print data=capacity (obs=4);
run;

data capacity;
    capacity;
   Econ = int(Econ * .95);
   Business = int(Business * .90);
run;

proc print data=capacity (obs=4);
run;
```

以下输出显示 `MODIFY` 语句之前的数据。![output before the modify statement](img/m59-3-g1.png) 以下输出显示 `MODIFY` 语句之后的数据。你可以看到 `Business` 和 `Econ` 中的值已经减少。![output after the modify statement](img/m59-3-g2.png)

# 使用事务数据集修改观测值

## 概述

你可以使用 `MODIFY` 语句更新数据集中的所有观测值，但有时你只想更新选定的观测值。你可以通过使用带有 `BY` 语句的 `MODIFY` 语句通过匹配观测值来应用更新，从而使用事务数据集中的值来修改主数据集。

| 带有 BY 语句的 MODIFY 语句通用形式：
```
DATA SAS-data-set;
MODIFY SAS-data-set transaction-data-set;
BY key-variable;
RUN;
```
以下是对语法的解释：
SAS-data-set 是你想要修改的数据集名称（也称为主数据集）。
transaction-data-set 是包含更新值的数据集名称。
key-variable 是主数据集和事务集中用于匹配的变量名称。 |

注意：在 `MODIFY` 语句中，你必须先列主数据集，然后是事务数据集。`BY` 语句将事务数据集中的观测值与主数据集中的观测值进行匹配。当 `MODIFY` 语句从事务数据集读取一个观测值时，它使用动态 `WHERE` 处理（SAS 内部生成 `WHERE` 语句）在主数据集中定位匹配的观测值。主数据集中的匹配观测值可以被替换（replace）、删除（delete）或追加（append）。默认情况下，该观测值会被替换。注意：由于 `MODIFY` 语句使用 `WHERE` 处理来定位匹配的观测值，因此两个数据集都不排序。然而，让主数据集排序或建立索引并让事务数据集排序可以减少处理开销，特别是对于大文件。




假设你有一个主数据集 `Capacity`，其中包含某航空公司的航线编号。某些航线发生了变化，这些更改存储在事务数据集 `Newrtnum` 中。通过匹配变量 `FlightID` 的值来更新主数据集。

```
proc print data=capacity(obs=5);
run;

data capacity;
   modify capacity sasuser.newrtnum;
   by flightid;
run;

proc print data=capacity(obs=5);
run;
```

以下 `PROC PRINT` 输出显示了在应用更新之前数据集 `Capacity` 的前五行。![Capacity 的输出](img/m59-7-g1.png)对于每个匹配的观测值，`RouteID` 的值都会被更新。![capacity 的输出](img/m59-7-g2.png)

## 处理重复值

当你使用 `MODIFY` 和 `BY` 语句更新数据集时，`WHERE` 处理从主数据集的顶部开始，找到第一个匹配项并对其更新。考虑一下如果主数据集或事务数据集中存在重复值会发生什么。假设你有以下代码，使用事务数据集 `T` 来更新主数据集 `M`：

```
data m;
    modify m t;
    by a;
run;
```

如果主数据集中存在 `BY` 变量的重复值，则只有重复值组中的第一个观测值会被更新。![主数据集](img/m59-10-g1.png)如果 `etransaction` 数据集中存在 `BY` 变量的重复值，则事务将相互覆盖，导致该组中的最后一个事务成为主数据集中的结果。![事务数据集](img/m59-10-g2.png)或者，你可以编写代码来累积每个事务的数值。

## 处理缺失值

如果事务数据集中存在缺失值，SAS 不会用缺失值替换主数据集中的数据，除非它们是特殊缺失值。**注意**：特殊缺失值是一种数值型缺失值，它允许你使用字母 `A-Z` 或下划线来表示不同类型的缺失数据。你可以在 `DATA` 步中使用 `MISSING` 语句来指定特殊缺失值。更多信息，请参阅 SAS 文档。你可以通过使用 `MODIFY` 语句中的 `UPDATEMODE=` 选项指定如何处理事务数据集中的缺失值。

| 通用格式，带有 `UPDATEMODE=` 选项的 `MODIFY` 语句：`MODIFY master-data-set transaction-data-set UPDATODE=MISSINGCHECK &#124; NOMISSINGCHECK;` | 以下是语法的解释：`master-data-set`是你想要修改的 SAS 数据集的名称。`transaction-data-set`是存储更新后值的 SAS 数据集的名称。`MISSINGCHECK` 防止事务数据集中的缺失值替换主数据集中的值，除非它们是特殊缺失值。`MISSINGCHECK` 是默认值。`NOMISSINGCHECK` 允许事务数据集中的缺失值替换主数据集中的值。事务数据集中的特殊缺失值仍然会替换主数据集中的值。 |

# 修改通过索引定位的观测值

## 概述

你已经学习可以使用 `BY` 语句通过匹配来访问主数据集中想要更新的值。当你拥有一个带索引的主数据集时，你可以使用索引直接访问想要更新的观测值。要实现这一点，你需要使用以下语句：

* 一个带有 `KEY=` 选项的 `MODIFY` 语句，用于命名索引以定位要更新的观测值
* 一个 `SET` 语句或 `INPUT` 语句，用于读取具有同名变量或值提供给索引的变量的事务数据集

| 通用格式，带有 `KEY=` 选项的 `MODIFY` 语句：`MODIFY SAS-data-set KEY=index-name;` | 以下是语法的解释：`SAS-data-set`是主数据集，或者你想要更新的数据集。`index-name`是你用于定位观测值的简单或复合索引的名称。 |

使用索引更新与使用 `BY` 语句更新不同。当你使用带有 `KEY=` 选项的 `MODIFY` 语句命名索引时，必须发生以下情况：

* 你必须显式指定想要执行的更新。
* 事务数据集中的每个观测值在主数据集中必须有一个匹配的观测值。如果一个主观测值对应多个事务观测值，则只应用事务中的第一个观测值。其他观测值将产生运行时错误并终止 `DATA` 步（除非使用 `UNIQUE` 选项，该选项在本章稍后部分讨论）。

## 示例

假设 1999 年的航空货物重量存储在主数据集 `Cargo99` 中，它在 `FlightID` 和 `Date` 变量上有一个名为 `FlghtDte` 的复合索引。部分数据是不正确的，数据集需要更新。正确的货物数据存储在事务数据集 `Newcgnum` 中。在下面的程序中，`KEY=` 选项指定了 `FlghtDte` 索引。当在 `Cargo99` 中找到匹配观测值时，三个变量（`CapCargo`、`CargoWgt` 和 `CargoRev`）会被更新。**注意**：如果你选择运行此示例，必须从 `Sasuser` 拷贝数据集 `Cargo99`。

```
proc print data=cargo99(obs=5);
run;

data cargo99;
   set sasuser.newcgnum (rename = (capcargo = newCapCargo
                               cargowgt = newCargoWgt
                               cargorev = newCargoRev));
   modify cargo99 key=flghtdte;
   capcargo = newCapCargo;
   cargowgt = newCargoWgt;
   cargorev = newCargoRev;
run;

proc print data=cargo99(obs=5);
run;
```

下面的输出显示了在应用更新之前数据集 `Cargo99` 的前五行。![Capacity 的输出](img/m59-g1.png) 下面的输出显示了在被 `Newcgnum` 更新后 `Cargo99` 的前五行。注意第一个观测值的三个变量已被更新。![Capacity 的输出](img/m59-g2.png)

## 处理重复值

当你使用索引定位要更新的观测值时，事务数据集中索引变量的重复可能会导致问题。我们考虑当使用以下代码用事务数据集 `T` 更新主数据集 `M` 的各种情况。`M` 数据集上的索引是基于变量 `A` 的：

```
data m;
   set t (rename=(b=newb));
   modify m key=a;
   b=newb;
run;
```

如果主数据集中存在重复，只有第一次出现会被更新。![主数据集中的重复](img/m59-10-g1.png)**提示**：如果你想用事务值更新主数据集中的所有重复，请使用 `DO` 循环多次执行带有 `KEY=` 选项的 `SET` 语句。如果事务集中存在非连续重复，SAS 更新主数据集中的第一个匹配项。最后一个重复事务值是更新后主数据集中的结果。![事务数据集中的非连续重复](img/m59-10-g2.png)如果事务集中存在连续重复（即某些值在主数据集中没有匹配项），则 SAS 将执行一对一更新，直到找到非匹配项。此时，`DATA` 步将因错误终止![事务数据集中的连续重复](img/m59-10-g3.png)在 `MODIFY` 语句中添加 `UNIQUE` 选项可以避免 `DATA` 步中的错误。`UNIQUE` 选项导致 `DATA` 步在每次查找匹配项时都返回索引顶部。`UNIQUE` 选项只能与 `KEY=` 选项一起使用。




| 通用格式，带有 `UNIQUE` 选项的 `MODIFY` 语句：`MODIFY SAS-data-set KEY=index-name /UNIQUE;`
以下是语法解释：`SAS-data-set` 是你想要修改的 SAS 数据集的名称（主数据集）。`index-name` 是你用于定位观测值的简单索引或复合索引的名称。 |

你可以指定 `UNIQUE` 选项来执行以下操作之一：

- 对一个主观测值应用多次事务
- 标识主数据集中的每个观测值都包含一个索引变量的唯一值。

当你使用 `UNIQUE` 选项且事务数据集中存在连续的重复值时，SAS 会更新主数据集中的第一个观测值。这与事务数据集中存在非连续重复值时的情况类似。如果应该将事务数据集中的值累加到主数据集的值上，你可以编写一条语句来累积所有重复值的值。![使用 UNIQUE 选项](img/m59-17-g4.png)

# 控制更新过程

## 概述

当 DATA 步包含 `MODIFY` 语句时，SAS 将当前观测值写入其在 SAS 数据集中的原始位置。此操作默认通过 DATA 步底部的隐式 `REPLACE` 语句执行。然而，你可以通过显式添加 `OUTPUT`、`REPLACE` 或 `REMOVE` 语句来覆盖此默认行为。

| `OUTPUT`、`REPLACE` 和 `REMOVE` 语句的通用格式：`OUTPUT;REPLACE;REMOVE;`
以下是语法解释：`OUTPUT` 将当前观测值添加到数据集的末尾。`REPLACE` 将当前观测值写入数据集的相同位置。`REMOVE` 从数据删除当前观测值。 |

在带有 `MODIFY` 语句的 DATA 步中使用 `OUTPUT`、`REPLACE` 或 `REMOVE` 语句可以更改观测值的默认替换行为。只要顺序逻辑，你就可以同时使用这三个语句。**注意**：如果你将 `OUTPUT` 语句与 `REPLACE` 或 `REMOVE` 语句结合使用，请确保 `OUTPUT` 语句在任何 `REPLACE` 或 `REMOVE` 语句之后执行，以确保索引位置的完整性。

## 示例

假设 SAS 数据集 `Transaction` 有名为 `Code` 的变量，其值为 `yes`、`no` 和 `new`，你可以提交以下程序来执行以下操作之一：

- 删除 `Code` 值为 `no` 的行
- 更新 `Code` 值为 `yes` 的行
- 附加 `Code` 值为 `new` 的行。

```
data master;
   set transaction;
   modify master key = id;
   a = b;
   if code = 'no' then remove;
   else if code = 'yes' then replace;
   else if code = 'new' then output;
run;
```

注意：你无法运行此示例，因为 `Transaction` 和 `Master` 是虚构数据集。

## 监控 I/O 错误状态

当你使用带有 `BY` 语句或 `KEY=` 选项的 `MODIFY` 语句更新数据集时，由于几个原因，错误检查非常。最重要的原因是这些工具使用了非顺序访问方法，因此无法保证观测值所在的位置能够满足请求。错误检查允许你根据 I/O 条件的结果决定是否执行更新。当你配合 `BY` 语句或 `KEY=` 选项使用 `MODIFY` 语句时，会创建自动变量 `_IORC_`（输入输出返回代码）。`_IORC_` 的值是一个数值返回代码，指示最近执行的 I/O 操作的状态。检查此变量的值允许你检测异常的 I/O 条件并按特定方式引导执行，而不是让应用程序异常终止。

## 与 %SYSRC 使用 _IORC_

由于 `_IORC_` 自动变量的值是内部的可能会发生，因此创建了自动调用宏 `%SYSRC`，以便你测试特定的 I/O 条件，同时保护你的代码免受未来 `_IORC_` 值变化的影响。

| 通用格式配合 `%SYSRC` 自动调用宏的 `_IORC_`：`IF _IORC_=%SYSRC (mnemonic) THEN executable_statement;`
以下是语法解释：`mnemonic` 是特定 I/O 条件的代码。 |

注意：`%SYSRC` 自动调用库中。你必须启用 `MACRO` 系统选项才能使用此宏。当你使用 `%SYSRC` 时，可以通过指定下面列出的助符之一来检查 `_IORC_` 的值。

| 助符 | 含义 |
| --- | --- |
| `_DSENMR` | 事务数据集中的观测值在主数据集中不存在（仅用于 `MODIFY` 和 `BY` 语句）。 |
| `_DSEMTR` | 事务数据集中的多个观测值在主数据集中（仅用于 `MODIFY` 和 `BY` 语句）。 |
| `_DSENOM` | 无匹配的观测值（用于 `KEY=` 选项）。 |
| `_SOK` | 已找到观测值。 |

## 示例

假设你正在使用带有 `KEY=` 选项的 `MODIFY` 语句更新 SAS 数据集。在下面的程序中，当 `_IORC_` 的值为 `_SOK` 时，更新观测值。当 `_IORC_` 的值为 `_DSENOM` 时，未找到匹配的观测值，因此通过 `OUTPUT` 语句将观测值添加到数据，并在 `do` 组中 `_ERROR_` 重置为 0。

```
data master;
   set transaction;
   modify master key = id;
   if _IORC_=%sysrc(_sok) then
      do;
         a = b;
         replace;
      end;
   else
      if _IORC_=%sysrc(_dsenom) then
         do;
            output;
            _ERROR_ = 0;
         end;
run;
```

提示：有关 `_IORC_` 自动变量和 `%SYSRC` 的更多信息，请参见 SAS 文档中关于错误检查工具的信息。

# 理解完整性约束

## 概述

现在你已经知道如何原地修改数据，你可能会好奇在修改数据时如何保护或确保数据的完整性。完整性约束是你指定的规则，用于限制数据集中变量可以存储的值。当使用原地修改数据的技术添加、更新或删除与变量关联的值时，SAS 会强制完整性约束，例如：

- 带有 `MODIFY` 语句的 DATA 步
- 交互数据窗口
- 使用 `INSERT INTO`、`SET` 或 `UPDATE` 语句的 PROC SQL
- PROC APPEND

当你向表添加完整性约束时，SAS 会检查所有数据是否满足该约束。

| 类型 | 操作 |
| --- | --- |
| `CHECK` | 确保特定值或范围是该列的唯一值。它还可以根据同一行中的另一个列的值检查一个值的有效性。 |
| `NOT NULL` | 保证列在每行中都有空值。 |
| `UNIQUE` | 强制列值的唯一性。 |
| `PRIMARY KEY` | 唯一定义表中的行，可以是单个列或一组列。表只能有一个主键。`PRIMARY KEY` 约束包含了 `NOT NULL` 和 `UNIQUE` 约束的属性。 |
| `FOREIGN KEY` | 指定其值与另一个数据集的主键变量值关联的变量。这种父子关系限制了对两个表进行的修改。 |

注意：当你对 SAS 数据集放置完整性约束时，你需要指定要创建的约束类型。每个约束都有不同的操作。你可以通过两种方式使用完整性约束：通用和引用。通用约束在数据集内部，引用约束在数据集之间。

## 通用完整性约束

通用完整性约束允许你限制单个数据变量的值。以下约束可以作为通用完整性约束：

- `CHECK`
- `NOT NULL`
- `UNIQUE`
- `PRIMARY KEY`。





注意：只要 `PRIMARY KEY` 约束没有任何引用它的 `FOREIGN KEY` 约束，它就是一种通用的完整性约束。当 `PRIMARY KEY` 作为通用约束使用时，它仅仅是分配 `NOT NULL` 和 `UNIQUE` 约束的快捷方式。

## 引用完整性约束

引用约束允许你将一个数据集中列的值链接到另一个数据集中列的值。当一个数据集中的 `FOREIGN KEY` 完整性约束引用另一个数据集中的 `PRIMARY KEY` 完整性约束时，你就创建了一个引用完整性约束。要创建引用完整性约束，你必须执行以下操作：

1. 在第一个数据集上定义 `PRIMARY KEY` 约束。

2. 在其他数据集上定义 `FOREIGN KEY` 约束。

# 在数据集上放置完整性约束

## 概述

可以使用 `DATASETS` 过程或 `SQL` 过程创建完整性约束。虽然可以使用任一种过程在现有数据集上创建完整性约束，但如果你想在创建数据集的同时创建完整性约束，则必须使用 `PROC SQL`。在本章中，你将学习使用 `PROC DATASETS` 在现有数据集上放置完整性约束。

| 使用 `IC CREATE` 语句的 `DATASETS` 过程通用形式：
```
PROC DATASETS LIB=libref <NOLIST>;
MODIFY SAS-data-set;
IC CREATE constraint-name=constraint<MESSAGE='Error Message'>;
QUIT;
```
以下是对语法的解释：
`libref` 是存储数据集的库。如果你未指定 `LIB=` 选项，过程将使用 `Work` 库。
`NOLIST` 抑制目录列表。
`SAS-data-set` 是你想要应用完整性约束的数据集名称。
`constraint-name` 是你给完整性约束指定的任何名称。
`constraint` 是你正在创建的约束类型，按以下格式指定：

*   `NOT NULL (variable)`
*   `UNIQUE (variables)`
*   `CHECK (where-expression)`
*   `PRIMARY KEY (variables)`
*   `FOREIGN KEY (variables) REFERENCES table-name.`

`Error Message` 是当违反约束时写入日志的可选消息。 |

注意：你可以交叉使用 `IC` 或 `INTEGRITY CONSTRAINT`。提示：要了解如何使用 `SQL` 过程创建完整性约束，请参阅 使用 PROC SQL 创建和管理表。

## 示例

假设你有一个数据集，包含航空公司每个等舱舱的路线信息和乘客容量。你需要创建完整性约束，以确保在更新数据集时满足以下条件：

*   路线 ID 码必须是唯一的且必填的（`PRIMARY KEY`）。
*   商务舱乘客容量必须为空，或大于头等舱乘客容量（`CHECK`）。

在下面的代码中，使用 `IC CREATE` 语句在数据集 `Capinfo` 的变量上创建了两个通用完整性约束：

*   `PRIMARY KEY` 约束放置在 `RouteID` 变量上。该约束确保在更新 `RouteID` 值时，它们必须是唯一且非空的。注意：通过同时应用 `UNIQUE` 和 `NOT NULL` 约束也可以相同的效果，但 `PRIMARY KEY` 约束被用作快捷方式。
*   `CHECK` 约束使用 `WHERE` 表达式来确保 `CapBusiness` 的唯一允许值是大于 `Cap1st` 或缺失的。

注意：如果你选择运行此示例，必须从 `Sasuser` 库将数据集 `Capinfo` 拷贝到 `Work` 库。

```
proc datasets nolist;
   modify capinfo;
   ic create PKIDInfo=primary key(routeid)
      message='You must supply a Route ID Number';
   ic create Class1=check(where=(cap1st<capbusiness or capbusiness=.))
      message='Cap1st must be less than CapBusiness';
quit;
```

注意使用 `NOLIST` 选项来防止 `PROC DATASETS` 默认生成 `Work` 库列表。当创建约束时，消息会写入 SAS 日志。

表 18.1 SAS 日志

|

```
45 modify capinfo;
46 ic create PKIDInfo = primary key (routeid)
47 message = 'You must supply a Route ID Number';
NOTE: Integrity constraint PKIDInfo defined. 
48 ic create Class1 = check (where = (cap1st < capbusiness 
49 or capbusiness = .)) message = 'Cap1st must be less 
50 than CapBusiness'; 
NOTE: Integrity constraint Class1 defined. 
51 run;
```

 |

注意：对于 `UNIQUE` 和 `PRIMARY KEY` 约束，如果不存在适当的索引，SAS 将相关列上构建索引。由完整性约束创建的索引都可以用于其他用途，例如 `WHERE` 处理或 `SET` 语句中的 `KEY=` 选项。提示：有关创建完整性约束的更多信息，请参阅 `DATASETS` 过程的 SAS 文档。

## 如何强制约束

一旦放置了完整性约束，SAS 每当原地修改数据集时就会强制执行它们。原地修改数据的技术包括使用以下元素：

*   带有 `MODIFY` 语句的 `DATA` 
*   交互式数据编辑窗口
*   带有 `INSERT INTO`、`SET` 或 `UPDATE` 语句的 `PROC SQL`
*   `PROC APPEND`

## 示例

上一个示例代码在 `Cap1st` 和 `CapBusiness` 上放置了检查约束，以确保商务舱的容量值大于头等舱或缺失。假设你运行了以下程序将头等舱容量增加三倍。这可能会违反某些观测值的检查约束。

```
data capinfo;
   modify capinfo;
   cap1st=cap1st*3;
run;
```

未通过完整性约束的观测值将写入 SAS 日志。

表 18.2 SAS 日志

|

```
FlightID=IA0100 RouteID=000001 Origin=RDU Dest=LHR Cap1st=42
CapBusiness=30 Econ=163
_ERROR_=1 _IORC_=66130 _N_=1
FlightID=IA0201 RouteID=000002 Origin=LHR Dest=RDU Cap1st=42
CapBusiness=30 Econ=163
_ERROR_=1 _IORC_=66130 _N_=2
FlightID=IA0300 RouteID=000003 Origin=RDU Dest=FRA Cap1st=42
CapBusiness=30 Econ=163
_ERROR_=1 _IORC_=66130 _N_=3
FlightID=IA0400 RouteID=000004 Origin=FRA Dest=RDU Cap1st=42
CapBusiness=30 Econ=163
_ERROR_=1 _IORC_=66130 _N_=4
FlightID=IA2900 RouteID=0000029 Origin=SFO Dest=HNL Cap1st=42
CapBusiness=30 Econ=163
_ERROR_=1 _IORC_=66130 _N_=29
FlightID=IA3000 RouteID=0000030 Origin=HNL Dest=SFO Cap1st=42
CapBusiness=30 Econ=163
_ERROR_=1 _IORC_=66130 _N_=30
FlightID=IA3300 RouteID=0000033 Origin=RDU Dest=ANC Cap1st=42
CapBusiness=30 Econ=163
_ERROR_=1 _IORC_=66130 _N_=33
FlightID=IA3400 RouteID=0000034 Origin=ANC Dest=RDU Cap1st=42
CapBusiness=30 Econ=163
_ERROR_=1 _IORC_=66130 _N_=34
```





要查看数据的描述符部分（包括你对数据集设置的完整性约束），你可以使用 `DATASETS` 过程中的 `CONTENTS` 语句。

| 通用格式，带有 `CONTENTS` 语句的 `DATASETS` 过程：
```
PROC DATASETS LIB=libref <NOLIST>;
CONTENTS DATA=SAS-data-set;
QUIT;
```
以下是语法的解释：`libref` 是存储数据集的库。`NOLIST` 抑制目录列表。`SAS-data-set` 是你想要获取信息的数据集名称。

注意：`DATASETS` 过程中的 `CONTENTS` 语句产生的信息与 `CONTENTS` 过程相同。

## 示例

以下代码显示了关于 `Capinfo` 数据集的信息，包括上一个示例中添加到该数据集的完整性约束。注意，这里使用了 `NOLIST` 选项来抑制 `Work` 库中所有数据集的列表。使用此选项，仅列出 `Capinfo` 数据集的信息。

```
proc datasets nolist;
   contents data=capinfo;
quit;
```

下方仅显示输出中的完整性约束部分。![输出的完整性约束部分](img/m59-31-g1.png)

# 删除完整性约束

## 概述

要从数据删除完整性约束，请使用带有 `IC DELETE` 语句的 `DATASETS` 过程。

| 通用格式，带有 `IC DELETE` 语句的 `DATASETS` 过程：
```
PROC DATASETS LIB=libref <NOLIST>;
MODIFY SAS-data-set;
IC DELETE constraint-name;
QUIT;
```
以下是语法的解释：`libref` 是存储数据集的库名。如果没有指定 `LIB=` 选项，过程将使用 `Work` 库。`NOLIST` 抑制目录列表。`SAS-data-set` 是具有完整性约束的数据集名称。`constraint-name` 是你想删除的完整性约束名称。

## 示例

以下代码删除 `Capinfo` 数据上的完整性约束：

```
proc datasets;
    modify capinfo;
    ic delete pkidinfo;
    ic delete class1;
 quit;
```

当删除完整性约束时，SAS 日志中会写入一条消息。

表 18.3 SAS 日志

|  ```
53      modify capinfo;
54      ic delete pkidinfo;
NOTE: Integrity constraint PKIDInfo deleted.
55      ic delete class1;
NOTE: All integrity constraints defined on WORK.CAPINFO.DATA 
      have been deleted.
56   run;NOTE: Integrity constraint PKIDInfo deleted.
``` |

# 理解审计跟踪

当你修改数据集时，你可能希望通过审计跟踪（audit trail）来跟踪你所做的更改。审计跟踪是一个可选的 SAS 文件，用于记录对 SAS 表的修改。审计跟踪用于跟踪在数据集上直接进行的更改。具体而言，审计跟踪会记录通过以下方式进行的更改：

* `VIEWTABLE` 窗口
* 数据网格
* `DATA` 步中的 `MODIFY` 语句
* `PROC SQL` 中的 `UPDATE`、`INSERT` 或 `DELETE` 语句

对于数据的每次添加、删除和更新，审计跟踪都会自动存储被更新观测值中的变量副本，还会存储诸如谁进行了修改、修改了什么以及何时进行修改等信息。审计跟踪还可以在用户定义的变量中存储额外信息。以下 `PROC CONTENTS` 输出列出了一个具有变量 `A` 和 `B` 的数据集审计跟踪文件中的变量。你将在本章后面学习更多关于这些变量的内容![PROC CONTENTS 输出](img/m59-34-g1.png) 注意：任何替换数据集的过程或操作（例如 `DATA` 步、`PROC SQL` 中的 `CREATE TABLE` 或没有 `OUT=` 选项的 `SORT`）都会删除审计跟踪。不应使用 Windows 资源管理器等系统工具删除审计跟踪。一个 SAS 表只能有一个审计跟踪文件。关于审计跟踪文件：

* 它是只读文件。
* 它是由 `PROC DATASETS` 创建的。
* 它必须与与其关联的数据文件位于同一个库中。
* 它与它监控集集名，但成员类型为 `AUDIT`。

# 启动和读取审计跟踪

## 概述

你使用带有 `AUDIT` 和 `INITIATE` 语句的 `DATASETS` 过程启动审计跟踪。

| 通用格式，启动审计跟踪的 `DATASETS` 过程：
```
PROC DATASETS LIB=libref <NOLIST>;
AUDIT SAS-data-set <SAS-password>;
INITIATE;
QUIT;
```
以下是语法的解释：`AUDIT` 启动并控制向审计文件进行事件记录。`libref` 是被审计数据集所在的库名。`NOLIST` 抑制目录列表。`SAS-data-set` 是你想要审计的 SAS 数据集名称。`SAS-password` 是 SAS 数据集密码（如果存在）。`INITIATE` 在 `AUDIT` 语句指定的数据集上开始审计跟踪。

## 示例

以下代码在 `Capinfo` 数据集上启动审计跟踪。注意：如果你选择运行此示例，必须将 `Capinfo` 数据集从 `Sasuser` 库复制到 `Work` 库。

```
proc datasets nolist;
   audit capinfo;
   initiate;
quit;
```

表 18.4 SAS 日志

|  ```
60   audit capinfo;
61   initiate;
WARNING: The audited data file WORK.CAPINFO.DATA is not
         protected.
62   quit;
NOTE: The data set AUDIT has 0 observations
      and 13 variables.
``` | 注意：审计跟踪使用分配给数据集的密码。因此，建议修改数据集的密码。

# 读取审计跟踪文件

启动审计跟踪后，在第一次修改数据集之前没有观测值。当审计跟踪文件包含数据时，可以使用任何读取数据集的 SAS 组件来读取它。要引用审计跟踪文件，使用 `TYPE=` 数据选项。

| 通用格式，指定审计文件的 `TYPE=` 数据选项：(`TYPE=AUDIT`) |

## 示例

以下 `PROC CONTENTS` 代码显示审计文件的内容：

```
proc contents data=mylib.sales (type=audit);
run;
```

以下 `PROC PRINT` 代码列出 `Capinfo` 数据审计跟踪中的数据：

```
proc print data=capinfo (type=audit);
run;
```

# 控制审计跟踪数据

## 概述

现在你已经了解如何启动审计跟踪和读取审计跟踪文件，请考虑审计跟踪文件包含的信息。审计跟踪文件可以包含三种变量：

* 存储被审计数据集列副本的数据集变量
* 自动存储数据修改信息的审计跟踪变量
* 存储用户输入信息的用户变量

![控制审计跟踪数据](img/m59-39-g1.png) 你可以在 `PROC DATASETS` 步中使用额外的语句来控制审计跟踪中显示的变量。我们考虑在审计跟踪中找到的三类变量。

## 数据集变量

正如你预期的那样，审计跟踪文件与被审计数据集具有相同的变量集。如果数据集包含变量 `A` 和 `B`，那么变量 `A` 和 `B` 也出现在审计跟踪中。接下来考虑自动存储你对数据更改信息的审计跟踪变量。





审计跟踪变量会自动存储有关数据修改的信息。审计跟踪变量名以 `AT` 开头，后跟一个特定字符串，例如 `DATETIME`。

| 审计跟踪变量 | 存储的信息 |
| --- | --- |
| `ATDATETIME` | 修改的日期和时间 |
| `ATUSERID` | 与修改相关的登录用户 ID |
| `ATOBSNO_` | 除非 `REUSE=YES`，否则受修改影响的观测编号 |
| `ATRETURNCODE` | 事件返回代码 |
| `ATMESSAGE` | 修改时的 SAS 日志消息 |
| `ATOPCODE` | 描述操作类型的代码 |

## `ATOPCODE` 变量的值

`ATOPCODE` 变量包含一个描述将观测值写入审计文件的操作类型的代码。例如，如果您修改了受审计数据集中的所有观测值，则审计文件中包含的观测值数量将是原始数据集的两倍。审计文件将包含一个与原始观测值匹配且 `ATOPCODE` 值为 `DR` 的观测值，以及一个 `ATOPCODE` 值为 `DW` 的更新后的观测值。以下是 `ATOPCODE` 变量可能的值。

| `ATOPCODE` | 事件 |
| --- | --- |
| DA | 添加数据记录镜像 |
| DD | 删除数据记录镜像 |
| DR | 更新前的记录镜像 |
| DW | 更新后的记录镜像 |
| EA | 观测值添加失败 |
| ED | 观测值删除失败 |
| EU | 观测值更新失败 |

在启动审计跟踪时可以使用 `LOG` 语句来定义审计文件中存储的信息。

## 使用 LOG 语句控制审计跟踪中的数据

在启动审计跟踪时，`LOG` 语句中的选项决定了存储在审计跟踪中的记录类型及其相应的 `ATOPCODE` 值。`ERROR_IMAGE` 选项控制 `E` 操作代码。`BEFORE_IMAGE` 选项控制 `DR` 操作代码，而 `DATA_IMAGE` 选项控制所有其他 `D` 操作代码。如果您在启动审计跟踪时省略了 `LOG` 语句，默认行为是记录所有镜像。

`LOG` 语句的通用格式：`LOG <audit-settings>;`。以下是对语法的解释：`audit-settings` 是以下任意内容：

* `BEFORE_IMAGE=YES|NO` 控制更新前记录镜像的存储（'DR' 操作）。
* `DATA_IMAGE=YES|NO` 控制更新后记录镜像的存储（例如以 'D' 开头的操作）。
* `ERROR_IMAGE=YES|NO` 控制更新失败记录镜像的存储（例如以 'E' 开头的操作）。

## 示例

以下代码对数据集 `Capinfo` 启动审计跟踪，但仅存储错误记录镜像。这意味着审计文件仅包含发生错误时的记录。`ATOPCODE` 值只能为 `EA`、`ED` 和 `EU`。注意：如果您选择运行此示例，必须将数据集 `Capinfo` 从 `Sasuser` 库复制到 `Work` 库。

```
proc datasets nolist;
   audit capinfo;
   initiate;
   log data_image=NO before_image=NO;
quit;
```

## 用户变量

用户变量允许编辑文件的人输入有关对数据所做更改的信息。虽然数据值存储在审计文件中，但您可以像更新其他变量一样在数据集中更新它们。用户变量通过审计跟踪规范中的 `USER_VAR` 语句创建。

`USER_VAR` 语句的通用格式：`USER_VAR variable-name <$><length><LABEL='variable-label'>;`。以下是对语法的解释：`variable-name` 是您创建的用户变量名。`$` 表示该变量是字符变量。`length` 指定变量的长度（默认为 8）。`variable-label` 指定包含在引号内的变量标签。

注意：您可以在单条 `USER_VAR` 语句中创建多个用户变量。用户变量在 SAS 中是唯一的，因为它们存储在一个文件中（审计文件），并在另一个文件中（数据集）中打开进行更新。当数据集被打开进行更新时，会显示用户变量，您可以像处理数据集的一部分一样编辑它们进行。

## 示例

假设您必须监控数据集 `Capinfo` 的更新。以下代码为数据集 `Capinfo` 启动审计跟踪，并创建两个用户变量 `who` 和 `why`，用于存储是谁更改了数据集以及进行更改的原因。注意：如果您选择运行此示例，必须将数据集 `Capinfo` 从 `Sasuser` 库复制到 `Work` 库。

```
proc datasets nolist;
   audit capinfo;
   initiate;
   user_var who $20 label = 'Who made the change'
            why $20 label = 'Why the change was made';
quit;
```

一旦设置了这些用户变量，就会从审计跟踪中检索并在打开数据集进行更新时显示。您可以像处理任何数据变量一样为用户变量输入数据值。当保存每个观测值时，数据值会被保存到审计跟踪。当数据以浏览或打印模式打开时，用户变量是不可用的。要重命名用户变量或修改其属性，需要修改数据集，而不是审计文件。

# 控制审计跟踪

## 概述

一旦激活审计跟踪，您可以通过重新提交带有附加语句的 `PROC DATASETS` 步骤暂停、恢复日志以及终止（删除）审计跟踪。您使用 `DATASETS` 过程来暂停并恢复审计跟踪。您也可以使用该过程删除审计跟踪。

用于暂停、恢复或终止审计跟踪的 `DATASETS` 过程通用格式：`PROC DATASETS LIB=libref<NOLIST>;AUDIT SAS-data-set <SAS-password>;SUSPEND|RESUME|TERMINATE;QUIT;`。以下是对语法的解释：`libref` 是被审计表所在的库名。`NOLIST` 抑制目录列表。`SAS-data-set` 是您要审计的 SAS 数据集名称。`SAS-password` 是 SAS 数据文件密码（如果存在）。`SUSPEND` 暂停对审计文件的记录，但不删除文件。`RESUME` 恢复对审计文件的记录（如果已暂停）。`TERMINATE` 终止记录并删除审计文件。

提示 由于数据文件的每次更新都会写入审计文件，审计跟踪会对系统性能产生不利影响。您可能考虑在大型定期计划批更新期间暂停审计跟踪。

## 示例

以下代码终止数据集 `Capinfo` 的审计跟踪。注意：如果您选择运行此示例，必须将数据集 `Capinfo` 从 `Sasuser` 库复制到 `Work` 库。

```
proc datasets nolist;
   audit capinfo;
   terminate;
quit;
```

当审计跟踪终止时，日志会写入一条消息。

表 18.5 SAS 日志

|  

```
65   audit capinfo;
66   terminate;
NOTE: Deleting WORK.CAPINFO (memtype=AUDIT).
67 quit;
```





你已经了解到，可以保留审计轨迹来跟踪对单个数据集进行的就地更新。然而，如果你替换了该数据集，审计轨迹就会丢失。生成代数据集（Generation data sets）允许你维护 SAS 数据集的多个版本或代次。每当文件被替换时，就会创建一个新代。默认情况下，生成代数据集是不生效的。当 SAS 数据集 `A` 被替换时，SAS 库中会有 `A` 的两个副本。当 `DATA` 步执行完成时，SAS 会从库中删除数据集 `A` 的原始副本。

![生成代数据集](img/m59-48-g1.png)

当生成代数据集生效状态且 SAS 数据集 `A` 被替换时，SAS 库中会有 `A` 的两个副本。当 `DATA` 步执行完成时，SAS 会在库中保留 SAS 数据集 `A` 的原始副本并对其重命名。

![生成代数据集](img/m59-48-g2.png)

生成代数据集的每一代都存储为代组（generation group）的一部分。代组中的每个生成代数据集具有相同的根成员名，但每个代都有不同的版本号。最新版本被称为基版本（base version）。当代生效状态时，SAS 文件名限制为 28 个字符。最后四个字符保留给版本号使用。

注意：VMS 上不支持生成代数据集。

# 初始化生成代数据集

## 概述

要初始化生成代数据集并指定要维护的最大版本数，你在创建或替换数据集时会使用输出数据集选项 `GENMAX=`。如果数据集已存在，你可以在 `DATASETS` 过程和 `MODIFY` 语句中使用 `GENMAX=` 选项。

带有 `GENMAX=` 选项的 `DATASETS` 过程和 `MODIFY` 语句的通用形式如下：

```
PROC DATASETS LIB=libref <NOLIST>;
MODIFY SAS-data-set (GENMAX=n);
QUIT;
```

以下是对该语法的解释：
- `libref` 是包含你要修改的数据的库。
- `NOLIST` 抑制目录列表。
- `SAS-data-set` 是你想要修改的 SAS 数据集的名称。
- `n` 是你想要保留的历史版本数，包括基版本：
    - `n=0`，不保留任何历史版本（这是默认值）。
    - `n>0`，保留文件指定数量的文件版本。该数量包含基版本。

## 示例

以下 `DATASETS` 过程修改了数据集 `Cargorev`，并请求保留最多四个版本（一个基版本和三个历史版本）。注意：如果你选择运行此示例，你必须从 `Sasuser` 库将数据集 `Cargorev` 复制到 `Work` 库。

```
proc datasets nolist;
   modify cargorev (genmax=4);
quit;
```

当你指定 `GENMAX=` 选项时，日志中不会写入任何信息。

## 创建生成代数据集

记住，生成代数据集的新版本只有在数据集被替换时才会创建，而不是在就地修改时。要创建新代，请使用以下方法之一：

- 带有 `SET` 语句的 `DATA` 步
- 带有 `MERGE` 语句的 `DATA` 步
- 不带 `OUT=` 选项的 `PROC SORT`
- 带有 `CREATE TABLE` 语句的 `PROC SQL`

# 处理生成代数据集

## 概述

一旦你拥有了一个包含多个生成代数据集的代组，你可能想要选择特定的数据集进行处理。要选择特定的代，你使用 `GENNUM=` 数据集选项。

`GENNUM=` 数据集选项的通用形式如下：

```
GENNUM=n
```

以下是对该语法的解释：
- `n` 指定数据集的特定历史版本：
    - `n>0` 是通过代数对历史版本的绝对引用。
    - `n<0` 是对历史版本的相对引用。
    - `n=0` 是当前版本。

## 示例

要打印数据的当前版本，你不需要使用 `GENNUM=` 选项。只需使用如下代码即可：

```
proc print data=year;
run;
```

要打印最年轻的历史版本，你有多种选择。你可以在 `GENNUM=` 选项中指定绝对引用或相对引用，所示：

```
proc print data=year(gennum=4);  /*绝对引用*/
run;
```

```
proc print data=year(gennum=-1);  /*相对引用*/
run;
```

你也可以使用 `PROC CONTENTS` 配合 `GENNUM=` 选项查看有关特定代的信息，所示：

```
proc contents data=year(gennum=-1);  /*相对引用*/
run;
```

现在你已经看到了一些使用 `GENNUM=` 选项的示例，请考虑代数是如何变化的。

## 代数如何变化

当你使用 `GENNUM=` 选项时，可以引用绝对代数或相对代数。理解代数是如何变化的很有帮助，以便识别你想要处理的代。首先，考虑 SAS 如何命名生成代数据集。当启用代状态的数据集第一次被替换时，SAS 保留被替换的数据集，并在其成员名后追加一个四位的版本号。该名称包含井号（`#`）和数字。对于名为 `A` 的数据集，第一次被替换时，SAS 保留替换的数据集并将其变为 `A#001`。当数据集被第二次替换时，替换的数据集变为 `A#002`。对于名为 `A` 的数据集，`A#002` 是最接近基版本的版本。SAS 可以追加的版本号限制是 `#999`。在替换 1000 次后，SAS 将最新版本号重置为 `#000`。现在考虑绝对和相对代数（在 `GENNUM=` 选项中指定）的变化。每当 SAS 创建新代时，绝对代数增加。随着旧代的删除，它们的绝对代数会失效。相比之下，相对代数始终相对于基。基或当前代始终是 0，-1 是最年轻的版本。下表显示了数据集名称。表 18.6 使用 GENNUM 的数据集名称

| 迭代 | SAS 代码 | 数据集名称 | GENNUM 绝对引用 | GENNUM 相对引用 | 解释 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | `data Year (genmax=3);` | Year | 1 | 0 | 创建数据集 Year，并请求三个代。 |
| 2 | `data Year;` | Year#001 | 2 | 0-1 | Year 被替换。迭代 1 的 Year 被重命名为 Year#001。 |
| 3 | `data Year;` | Year#002Year#001 | 3 | 0-1-2 | Year 被替换。迭代 2 的 Year 被重命名为 Year#002。 |
| 4 | `data Year;` | Year#003Year#002 | 4 | 0-1-2 | Year 被替换。迭代 3 的 Year 被重命名为 Year#003。迭代 1 的 Year#001 最旧，被删除。 |
| 5 | `data Year (genmax=2);` | Year#004 | 5 | 0-1 | Year 被替换，且代数改为 2。迭代 4 的 Year 被重命名为 Year#004。两个最旧的版本被删除。 |

你已经了解到使用 `PROC DATASETS` 在现有的 SAS 数据集上初始化生成代数据集。一旦你创建了生成代数据集，可以使用 `PROC DATASETS` 执行管理任务，例如：

- 删除所有或部分代
- 将整个代组或代组中的任何成员重命名为新的基名。





# 通用格式

通用格式带有 `CHANGE` 和 `DELETE` 语句的 `PROC DATASETS` 格式：

```
PROC DATASETS LIB=libref <NOLIST>;
CHANGE SAS-data-set<(GENNUM=n)>=new-data-set-name;
DELETE SAS-data-set<(GENNUM=n | HIST | ALL)>;
QUIT;
```

以下是语法的解释：
- `libref` 是包含你想要修改的数据的库。
- `NOLIST` 抑制目录列表显示。
- `SAS-data-set` 是你想要更改或删除的 SAS 数据集的名称。
- `new-data-set-name` 是 `CHANGE` 语句中 SAS 数据集的新名称。
- `n` 是对生成代号（generation number）的绝对或相对引用。
- `HIST` 指除基础版本以外的所有代。
- `ALL` 指基础版本和所有代。

## 示例

以下代码使用 `CHANGE` 语句将数据集 `SalesData` 重命名为 `Sales`。如果已经创建了多个代数据，则所有代的基础名称都将被重命名。

```
proc datasets library=quarter1 nolist;
   change salesData=sales;
quit;
```

以下代码使用 `GENNUM=` 选项仅重命名第二个历史数据集：

```
proc datasets library=quarter1 nolist;
   change sales(gennum=2)=newsales;
quit;
```

以下代码删除了一个历史版本。此操作可能会在生成组中留下空隙。

``````proc datasets library=quarter1 nolist;
   delete newsales(gennum=-1);
quit;
```

当你在 `DELETE` 语句中使用 `GENNUM=` 选项时，可以使用 `HIST` 和 `ALL` 关键字。以下代码使用 `HIST` 关键字删除所有的历史版本：

```
proc datasets library=quarter1 nolist;
   delete newsales(gennum=HIST);
quit;
```

以下代码在 `GENNUM=` 选项中使用 `ALL` 关键字来删除生成组中的所有 SAS 数据集：

```
proc datasets library=quarter1 nolist;
   delete newsales(gennum=ALL);
quit;
```

**提示**：有关更多关于使用 `DATASETS` 过程处理数据的信息，请参阅 SAS 文档。

## 总结

## 文本总结

### 使用 MODIFY 语句

当你使用 `MODIFY` 语句修改 SAS 数据集时，SAS 不会像使用 `SET`、`MERGE` 或 `UPDATE` 语句那样创建数据的第二个副本。SAS 数据集的描述部分保持不变。更新后的观测值将写回与原始观测值相同的位置。

### 修改 SAS 数据集中所有观测值

你可以使用 `MODIFY` 语句配合赋值语句来修改 SAS 数据集中所有的观测值。

### 使用事务数据集修改观测值

要使用事务数据集修改主数据集，你需要使用 `MODIFY` 语句配合 `BY` 语句指定匹配的变量或变量。当你使用 `MODIFY` 或 `BY` 语句时，SAS 使用动态 `WHERE` 子句定位主数据集中的观测值。你可以通过使用 `MODIFY` 语句中的 `UPDATEMODE=` 选项来指定如何处理事务数据集中的缺失值。

### 通过索引定位观测值

你可以使用 `MODIFY` 语句配合 `KEY=` 选项为正在修改的 SAS 数据集命名简单或复合索引。`KEY=` 参数根据事务数据集中由同名变量提供的索引值从主数据集中检索观测值。如果你在事务集中存在连续的重复（即某些项在主数据集中没有匹配），你可以使用 `UNIQUE` 选项使 `KEY=` 搜索始终从顶部开始。





* 完整性约束仅在对数据进行修改时才会执行。如果替换了数据集，完整性约束将会丢失。

* 审计跟踪文件（Audit trail files）通过以下方式跟踪对数据集进行就地修改的更改：
    * `DATA` 步中的 `MODIFY` 语句
    * `PROC SQL` 中的 `UPDATE`、`INSERT` 或 `DELETE` 语句
* 生成数据集（Generation data sets）用于跟踪通过以下方式替换数据集时所产生的更改：
    * 在 `DATA` 步中使用-`SET`、`MERGE` 或 `UPDATE` 语句
    * 使用 `PROC SORT` 对数据进行就地排序
    * 在 `PROC SQL` 中使用 `CREATE TABLE` 语句

# 测试

请为每个问题选择最佳答案。完成测试后，请使用附录中的答案对照检查你的答案。

1. 你会在变量 `StoreID` 上设置哪种类型的完整性约束，以确保没有缺失值且没有重复值？
    1. `UNIQUE`
    2. `CHECK`
    3. `PRIMARY KEY`
    4. `NOT NULL`

2. 哪段代码为 SAS 数据集 `Reports.Quarter1` 创建审计跟踪？
    1.
    ```
    proc datasets nolist;
       audit quarter1;
       initiate;
    quit;
    ```
    2.
    ```
    proc datasets lib=reports nolist;
       audit initiate reports.quarter1;
    quit;
    ```
    3.
    ```
    proc datasets lib=reports nolist;
       initiate audit quarter1;
    quit;
    ```
    4.
    ```
    proc datasets lib=reports nolist;
       audit quarter1;
       initiate;
    quit;
    ```

3. 哪一个 `DATA` 步使用事务数据集 `Records.Overnight` 通过 `accumAmt` 更新主数据数据集 `Records.Snowfall`？
    1.
    ```
    data records.snowfall;
       modify records.snowfall records.overnight
       key=accumAmt;
    run;
    ```
    2.
    ```
    data records.snowfall;
       modify records.overnight records.snowfall;
       by accumAmt;
    run;
    ```
    3.
    ```
    data records.snowfall;
       modify records.snowfall records.overnight;
       by accumAmt;
    run;
    ```
    4.
    ```
    data records.snowfall;
       modify records.snowfall records.overnight
       update accumAmt;
    run;
    ```

4. 当你使用 `MODIFY` 语句配合 `BY` 语句或 `KEY=` 选项时，会创建变量 `_IORC_`。你如何使用 `_IORC_` 的值？
    1. 确定 `KEY=` 选项指定的索引是否为有效索引
    2. 确定主数据集中被更新的观测数量
    3. 确定 I/O 操作的状态
    4. 确定主数据集中无法更新的观测数量

5. 哪一个 `PROC DATASETS` 步在数据集 `Survey` 上创建一个名为 `val_age` 的完整性约束，以确保变量 `Age` 的值大于或等于 18？
    1.
    ```
    proc datasets nolist;
       modify age;
       ic create val_age=check(where=(age>=18));
    quit;
    ```
    2.
    ```
    proc datasets nolist;
       modify Survey;
       ic create val_age=check(age>=18);
    quit;
    ```
    3.
    ```
    proc datasets nolist;
       modify survey;
       integrity constraint
                 val_age=check(where=(age>=18));
    quit;
    ```
    4.
    ```
    proc datasets nolist;
       modify survey;
       ic create val_age=check(where=(age>=18));
    quit;
    ```

6. 关于在 `DATA` 步中使用 `MODIFY` 语句的哪种描述是正确的？
    1. `MODIFY` 在数据中的变量与 `WHERE` 子句匹配时创建数据的第二个副本，然后删除该第二个副本。
    2. 你不能使用 `MODIFY` 语句修改数据集的描述符部分。
    3. 你可以使用 `MODIFY` 语句更改变量的名称。
    4. 如果使用 `WHERE` 语句的 `DATA` 步在处理过程中异常终止，SAS 会自动保存未修改数据集的副本。

7. 关于审计跟踪，以下哪种说法是正确的？
    1. 它们创建数据的历史版本，因此在每次替换数据时都会保存数据集的副本。
    2. 每次替换数据集时，它们都会记录数据集观测值更改的信息。
    3. 每次对数据集进行就地修改时，它们都会记录数据集观测值更改的信息。
    4. 审计跟踪文件名与其监控的 SAS 数据文件名相同，但在数据集名称末带有 `#AUDIT`。

8. 哪段代码在现有的 SAS 数据集 `Sasuser.Amounts` 上启动生成数据集，并指定除基础版本外保存五个历史版本？
    1.
    ```
    proc datasets lib=sasuser nolist;
       modify Amounts (genmax=6);
    quit;
    ```
    2.
    ```
    proc datasets lib=sasuser nolist;
       modify Amounts (genmax=5);
    quit;
    ```
    3.
    ```
    proc datasets lib=sasuser nolist;
       modify Amounts (gennum=6);
    quit;
    ```
    4.
    ```
    proc datasets lib=sasuser nolist;
       modify Amounts (gennum=5);
    quit;
    ```

9. 关于在 `MODIFY` 语句中使用 `KEY=` 选项的哪种说法正确？
    1. SAS 使用 `KEY=` 选项指定的索引定位要更新的变量，像使用 `MODIFY` 或 `BY` 语句那样自动覆盖非空事务值。
    2. 当你使用 `KEY=` 选项时，必须显式说明你想进行的更新。SAS 不会自动覆盖非空事务值。
    3. `KEY=` 选项用于指定匹配观测值的变量。
    4. `KEY=` 选项命名的索引必须是简单索引。

10. 哪段代码删除了 `Sasuser.Amounts` 的所有生成，包括基础数据集？
    1.
    ```
    proc datasets lib=sasuser nolist;
       delete amounts (gennum=ALL);
    quit;
    ```
    2.
    ```
    proc datasets lib=sasuser nolist;
       delete amounts (gennum=HIST);
    quit;
    ```
    3.
    ```
    proc datasets lib=sasuser nolist;
       delete amounts (gennum=0);
    quit;
    ```
    4.
    ```
    proc datasets lib=sasuser nolist;
       delete amounts;
    quit;
    ```





运行 SAS 程序会使用以下资源：

| 资源 | 说明 |
| --- | --- |
| CPU 时间![clock](img/m80-2-g1.png) | 中央处理器 (CPU) 执行所请求任务（如计算、数据读取和写入、条件逻辑和迭代逻辑）时花费的时间。 |
| 实际时间![clock](img/m80-2-g1.png) | 执行一个作业或步骤所需的时钟时间（经过时间）。实际时间很大程度上取决于系统容量和负载（共享系统资源的用户数）。由于你无法总是控制系统的容量需求和负载需求，有时实际时间作为程序效率的衡量标准不如 CPU 时间 有用。然而，实际时间的过度使用通常会促使程序员提高程序的效率。某些存储过程允许你使用线程处理来缩短实际时间。线程处理可能会增加 CPU 时间。因此，建议同时跟踪 CPU 时间和实际时间。 |
| 内存![work area](img/m80-2-g2.png) | 用于存放可执行程序模块、数据和缓冲区所需的易失性内存中的工作区域大小。 |
| 数据存储空间![disk space](img/m80-2-g3.png) | 存储数据所需的磁盘或磁带空间大小。数据存储空间以多种单位衡量，其中某些单位仅用于特定的操作系统环境，如下所示：<br>* 所有操作系统环境都使用字节 (bytes)、千字节 (kilobytes)、兆字节 (megabytes)、吉字节 (gigabytes) 和太字节 (terabytes)。<br>* z/OS 还使用块、磁道和柱面。 | |
| I/O![storage device to memory](img/m80-2-g4.png) | 数据和程序从存储设备复制到内存（输入）或从内存复制到存储或显示设备（输出）时执行的读写操作测量。 |

# 评估站点的效率需求

优化 SAS 程序的第一步是评估您站点的技术环境、程序以及数据。

## 评估您的技术环境

要确定您的站点哪些资源是稀缺或昂贵的，请与 IT 部门合作分析您技术环境的以下特征：

| 类别 | 特征 |
| --- | --- |
| 硬件 | * 可用内存量<br>* CPU 数量<br>* 外围设备的数量和类型<br>* 通信硬件<br>* 网络带宽<br>* 存储容量<br>* I/O 带宽<br>* 升级能力 |
| 运行环境 | * 资源分配<br>* 调度算法<br>* I/O 方法 |
| 系统负载 | * 共享系统资源的用户或作业数量<br>* 网络流量（预期）<br>* 未来负载的预期增长 |
| SAS 环境 | * 安装了哪些 SAS 软件产品<br>* 为 SAS 编程分配的 CPU 数量和内存量<br>* 您的站点可以使用哪些运行 SAS 程序的方法 |

开发一个高效的程序需要时间和思考。要确定节省的资源是否值得投入时间，请考虑程序的以下特征：

| 特征 | 优化指南 |
| --- | --- |
| 程序大小 | 随着程序增大增大，潜在节省空间随之增加。 |
| 程序运行次数 | 运行一次或少数的低效程序与高效程序之间的差异较小，而运行多次的差异很大。 |

## 评估您的数据

任何效率技术的有效性很大程度上取决于您的数据。当您了解数据的特征时，可以可以选择利用这些特征的技术：

| 特征 | 优化指南 |
| --- | --- |
| 数据量 | 随着容量增加，潜在效率也随之增加。 |
| 数据类型 | 特定技术对某些类型的数据可能效果更好。 |

# 理解效率权衡

在优化 SAS 程序时，理解存在权衡是非常重要的。减少一种资源的使用会增加另一种资源的使用。下表显示了常见权衡的示例：

| 减少此资源的使用 | 增加此资源的使用可能增加 |
| --- | --- |
| 磁盘空间![disk space](img/m80-2-g3.png) | CPU 时间![clock](img/m80-2-g1.png) |
| I/O![storage device to memory](img/m80-2-g4.png) | 内存![work area](img/m80 2-g2.png) |
| 实际时间![clock](img/m80-2-g1.png) | CPU 时间![clock](img/m80-2-g1.png) |

没有单一的最佳优化方法。它取决于您的情况。然而，以下章节提供了可以帮助确定哪些技术最高效的信息：

* 控制内存使用
* 控制数据存储空间
* 使用最佳实践
* [高效查询数据](/certpgadv/html/p034xwg6jtv8n19

# 使用 SAS 系统选项跟踪资源

您可以指定一个或多个 SAS 系统选项 `STIMER`、`MEMRPT`、`FULLSTER` 和 `STATS` 来跟踪并报告资源使用。这些选项的可用性、用法和功能取决于操作系统，如下所示：

| 选项 | z/OS | UNIX 和 Windows |
| --- | --- | --- |
| STIMER | 会话期间跟踪 CPU 时间。仅可以在启动时设置。是默认设置。 | 会话期间跟踪 CPU 时间和实时统计并写入 SAS 日志。可以在启动时或使用 OPTIONS 语句设置。是默认设置。 |
| MEMRPT | 会话期间跟踪内存使用统计。可以在启动时或使用 OPTIONS 语句设置。 | 不作为独立选项可用；此功能是 `FULLSTER` 选项的一部分。 |
| FULLSTER | 会话期间跟踪所有可用的资源使用统计并写入 SAS 日志。可以在启动时或使用 OPTIONS 语句设置。在 z/OS 操作系统环境中，`FULLSTER` 是 `STATS` 选项的别名。除非 `STIMER` 或 `MEMRPT` 有效，否则忽略此选项。 | 在 Windows 操作系统中，除非在启动时指定 `FULLSTER`，否则某些统计数据计算不准确。 |





| STATS | 告诉 SAS 将由前面的选项组合所跟踪的统计数据写入 SAS 日志中。可以在调用时设置，也可以通过 OPTIONS 语句设置。这是默认设置。 | 不作为独立选项可用。 |

SAS 系统选项在调用 SAS 时通过默认设置初始化。然而，某些 SAS 系统选项的默认设置会根据操作系统环境和站点而异。详细信息请参阅适用于您的操作系统环境的 SAS 文档。您可以使用以下选项关闭任何这些系统选项：

* `NOSTIMER`
* `NOMEMRPT`
* `NOFULLSTIMER`
* `NOSTATS`

注意：在 z/OS 环境中，`NOFULLSTIMER` 是 `NOFULLSTATS` 选项的别名。
注意：解释 `FULLSTIMER` SAS 系统选项生成的统计数据的指南也可以在 `support.sas.com` 找到。
注意：您还可以使用 SAS 响应测量 (`ARM`) 宏来监控应用程序的性能。本课程不涵盖 `ARM` 宏。要了解更多关于 `ARM` 宏的信息，请参阅 SAS 文档以及 `support.sas.com` 上关于 `ARM` 宏的详细信息。

# 使用基准测试比较技术

为了决定哪种 SAS 编程技术对于特定任务最高效，您可以对比较的每种技术进行资源测试（测量和比较）。您应该使用实际数据进行基准测试，以确定最高的技术。

## 基准测试指南

遵循以下指南，您的基准测试最可能产生有用结果：

* 在测试编程技术之前，开启报告资源使用的 SAS 系统选项。如前所述，为了跟踪和报告资源使用情况，可以使用 `STIMER`、`MEMRPT`、`FULLSTIMER` 和 `STATS` 部分或全部系统选项。这些选项的可用性、用法和功能取决于操作系统环境。您还可以指定 `MSGLEVEL=I` 在 SAS 日志中显示额外的注释。使用 `FULLSTIMER` 选项记录使用的资源的完整列表。
注意：要开启 `FULLSTIMER` 选项，请使用以下语句：

```
options fullstimer;
```

* 在独立的 SAS 会话中执行每种编程技术的代码。第一次引用程序代码（包括 `DATA` 步、函数、格式和 SAS 过程）时，操作系统可能必须将代码加载到内存或为其分配虚拟地址空间。第一次读取数据时，数据通常会被加载到缓存中，以便下次读取时可以更快地检索。执行这些操作所需的资源使用是开销。为每种技术更改使用独立的 SAS 会话可以最大限度地减少开销对您的资源统计的影响。

* 在您测试的每种编程技术中，仅包含执行任务必需的 SAS 代码。如果您在每种技术的代码中包含过多的元素，您将不知道结果产生的原因。如果您正在进行基准测试的程序不大，可以通过一次一次更改单个编程技术来优化它，并在每次更改后运行整个程序，以测量对资源使用情况的影响。然而，更复杂的程序可能通过识别使用最多资源的步骤并将这些步骤提取到单独的程序中更容易优化。您可以通过反复更改、运行和测量单独程序来衡量不同编程技术的影响。在隔离您的程序部分时，请务必在它们在完整程序中使用的条件下测量它们的资源使用情况。

* 如果您的系统在您运行基准测试时同时在执行其他工作，请确保多次运行每种编程技术的代码。多次运行代码可以减少与系统正在执行的其他工作相关的资源消耗的波动。您如何处理多次测量取决于资源类型，如下所示：

    * 使用最小的实际时间和 CPU 时间测量值，因为这些值最接近您的编程技术实际所需的时间。较大的时间值（特别是在实际时间的情况下）是程序程序运行时计算机正在执行的其他工作干扰的结果。

    * 内存量不应在每次试验之间变化。如果内存确实发生了变化，可能是您的程序有时与另一个程序共享资源。




正如你所学到的，没有哪一组编程技术在所有情况下都是最高效或最合适的。然而，如果减少执行时间是你计算环境中的一个重要考虑因素，那么实现该目标的一种方法是减少 SAS 从存储介质读取或写入的次数。在本章，你将学习使用选项（options）和语句（statement）来控制数据缓冲区的大小和数量，从而减少 SAS 必须执行的 I/O 操作次数来影响你的程序的执行时间。

# 控制页面大小和缓冲区数量

## 测量 I/O
I/O 的改进可能以增加内存消耗为代价。为了理解 I/O 与内存之间的关系，了解数据何时被复制到缓冲区以及何时测量 I/O 会很有帮助。当你使用 `DATA` 步创建 SAS 数据集时，会发生以下操作：

1. SAS 从输入数据集复制一页数据到内存中的缓冲区。
2. 每次将一个观测值从缓冲区加载到程序数据向量（PDV）。
3. 每个观测值从 `PDV` 写入输出缓冲区。
4. 当输出缓冲区满时，将输出缓冲区的内容写入磁盘。

![](img/m81-2-g1.png)读取外部文件的过程也类似。然而，每条记录首先从系统缓冲区读取到单记录输入缓冲区，然后才解析并读取到程序数据向量中。![](img/m81-2-g2.png)在这两种情况下，当输入数据被复制到内存中的缓冲区以及从输出缓冲区复制到输出数据集时，都会测量 I/O。

## 页面大小
将缓冲区视为内存中的一个容器，恰好保存一页数据。页描述如下：

* 它是存储设备和内存之间数据传输的单位。
* 它在创建数据集时大小固定，可以是默认值，也可以是用户指定的值。

较大的页面大小可以通过减少 SAS 从存储介质读取或写入的次数来减少执行时间。然而，执行时间的改进是以增加内存消耗为代价的。

## 报告页面大小
你可以使用 `CONTENTS` 过程或 `DATASETS` 过程中的 `CONTENTS` 语句来报告页面大小和页面数量。

| PROC CONTENTS 部分输出 |
| --- |
| |

```
proc contents 
     data=company.order_fact;
run;
```
![](img/m81-4-g1.png)

数据文件占据的字节总数等于页面大小乘以页面数量。例如，`Company.Order_fact` 的页面大小为 `8192`，页面数量为 `9423`。因此，数据文件占用 `77,193,216` 字节。注意：从 `PROC CONTENTS` 获取的信息取决于操作系统环境。注意：在未压缩的数据文件中，每页有 40 字节的开销（64 位操作系统环境中）或 24 字节的开销（32 位操作系统环境中），外加每个观测值 1 比特的开销（向上舍入到最近字节），用于标记观测值是否已删除。你可以在[控制数据存储空间](../../certpgadv/html/p0bu1zpppbn7win1flrca4h00inw7.htm）中了解未压缩和压缩数据文件的结构。

## 使用 BUFSIZE= 
为了选择默认页面大小，SAS 使用基于观测长度、引擎和操作系统的算法。默认页面大小对于大多数 SAS 活动都是最优的，特别是在支持并发运行多个 SAS 业的计算机上。然而，在某些情况下，选择比默认更大的页面大小或缓冲区大小可以通过减少 SAS 从存储介质读取或写入的次数来加快执行速度。你可以使用 `BUFSIZE=` 系统选项或数据集选项来控制输出 SAS 数据集的页面大小。新的缓冲区大小是数据集的永久属性。一旦指定，每当处理该数据集时都会使用它。

| 通用格式 `BUFSIZE=` 选项：`BUFSIZE= MIN | MAX | n;` |
| --- |
| 以下是该语法的解释：`MIN` 将页面大小设置为你环境中最小可能的数字。`MAX` 将页面大小设置为你环境中最大可能的数字。`n` 指定以字节为单位的页面大小。例如，值 `8` 表示页面大小为 8 字节，值 `4K` 表示页面大小为 `4096` 字节。默认值为 `0`，这会导致 SAS 使用该环境的最优页面大小。 |

注意：`MIN` 可能会导致意外的结果，应避免使用。使用 `BUFSIZE=0` 将缓冲区页面大小重置为你环境中的默认值。注意：此处显示的语法适用于 `OPTIONS` 语句。在命令行或配置文件中，语法取决于你的环境。详细信息请参阅你操作系统环境的 SAS 文档。每个环境只有某些页面大小或缓冲区大小值是有效的。如果你请求一个对环境无效的值，SAS 会自动向上舍入到下一个有效的页面大小或缓冲区大小。`BUFSIZE=0` 被解释为请求默认页面大小或缓冲区大小。在下面的程序中，`BUFSIZE=` 系统选项指定的页面大小为 `30720`。

```
options bufsize=30720;
filename orders 'c:\orders.dat';
data company.order_fact;
   infile orders;
   ...
run;
```

在更改默认页面大小之前，考虑数据的访问模式以及硬件的 I/O 传输率是重要的。某些情况下，增加页面大小可能会降低性能，特别是当使用直接访问数据时。注意：`BUFSIZE=` 的默认值由环境决定，并设置为优化顺序访问。为了提高直接访问的性能，你应该更改 `BUFSIZE=` 值。有关直接访问的默认设置和可能的设置，请参阅操作系统中的 `BUFSIZE=` 系统选项。注意：你可以通过 `BUFSIZE=` 数据集选项覆盖 `BUFSIZE=` 系统选项。注意：如果你使用 `COPY` 过程将数据集复制到通过不同引擎访问的库，则不一定保留原始页面大小或缓冲区大小。

## 使用 BUFNO=
你可以使用 `BUFNO=` 系统或数据集选项来控制读写 SAS 数据集的缓冲区数量。通过增加缓冲区数量，你可以控制每次 I/O 传输加载到内存的页面数。注意：在 Windows 和 UNIX 环境中，增加缓冲区数量可能影响性能，特别是当你处理大型数据集时。默认情况下，Windows 和 UNIX 环境每次读取一个缓冲区。在窗口环境下，你可以在调用 SAS 时开启 `SGIO` 系统选项来覆盖此默认。有关 `SGIO` 系统选项的详细信息，请参阅 Windows 的 SAS 文档。以下技术可能减少 I/O 消耗：

* 当处理小型数据集时，分配与页面数量相同的缓冲区，以便将整个数据集加载到内存中。这种技术在处理过程中多次读取同一观测值时最有效。
* 在 z/OS 环境中，随着数据集增大，应增加分配的缓冲区数量，而不是每个缓冲区的大小。




| 通用格式，`BUFNO=` 选项：`BUFNO=` `MIN` &#124; `MAX` &#124;`n;以下是该语法的解释：`MIN` 导致 SAS 使用操作系统环境的最小优化值。这是默认值。`MAX` 将缓冲区数量设置为操作系统环境中可能的最大数量，最高为最大的 4 字节有符号整数，即 `2³¹-1`，或约 20 亿。`n` 指定了要分配的缓冲区数量。 |

注意：此选项的推荐最大值为 10。注意：此处显示的语法适用于 `OPTIONS` 语句。在命令行或配置文件中，语法取决于您的操作系统环境。详细信息，请参阅适用于您的操作系统环境的 SAS 文档。在以下程序中，`BUFNO=` 系统选项指定可用 4 个缓冲区。

```
options bufno=4;
filename orders 'c:\orders.dat';
data company.orders_fact;
   infile orders;
   <more SAS code>
run;
proc print data=company.orders_fact;
run;
```

缓冲区数量不是数据集的永久属性，仅对当前步骤或 SAS 会话有效。图 20.1 当前 SAS 会话![当前 SAS 会话](img/m81-8-g1.png)注意：您可以使用 `BUFNO=` 数据集选项来覆盖 `BUFNO=` 系统选项。注意：在 SAS 9 及更高版本中，`BUFNO=` 选项对 z/OS 操作系统环境下的启用线程的过程没有影响。`BUFNO=` 和 `BUFSIZE=` 的乘积（而不是任一选项的具体值）决定了单次 I/O 操作可以传输多少数据。增加任一选项的值都会增加单次 I/O 操作传输的数据量。

| `BUFSIZE` | `BUFNO` | 单次 I/O 操作中传输的字节数 |

| --- | --- | --- |
| 6144 | 2 | 12,288 |
| 6144 | 10 | 61,440 |
| 30,720 | 2 | 61,440 |
| 30,720 | 10 | 307,200 |

缓冲区数量和缓冲区大小对 CPU 使用率的影响极小。

## 比较示例：使用 `BUFSIZE=` 选项和 `BUFNO=` 选项

### 示例设置

假设您想比较使用不同缓冲区大小和不同数量缓冲区读取数据集时的资源用用情况。以下示例程序比较了 `BUFNO=` 选项和 `BUFSIZE=` 选项的设置。您可以使用这些示例作为模型，在您自己的环境中创建基准测试程序。您的结果可能会根据数据结构、操作系统环境以及您处的可用资源而异。注意：6144 字节是 z/OS 操作系统环境下的默认页大小。

### 编程技术

| ![1](img/callout01.png) `BUFSIZE=6144, BUFNO=2`此程序读取数据集 `Retail.Order_fact` 并创建数据集 `Work.Orders`。`BUFSIZE=` 选项指定创建 `Work.Orders` 时缓冲区大小为 6144 字节。`BUFNO=` 选项指定每次 I/O 传输时将 2 页数据加载到内存中。 |

```
data work.orders (bufsize=6144 bufno=2);
   set retail.order_fact;
run;
```

 |

| ![2](img/callout02.png) `BUFSIZE=6144, BUFNO=5`此程序读取数据集 `Retail.Order_fact` 并创建数据集 `Work.Orders`。`BUFSIZE=` 选项指定创建 `Work.Orders` 时缓冲区大小为 6144 字节。`BUFNO=` 选项指定每次 I/O 传输时将 5 页数据加载到内存中。 |

```
data work.orders (bufsize=6144 bufno=5);
   set retail.order_fact;
run;
```

 |

| ![3](img/callout03.png) `BUFSIZE=6144, BUFNO=10`此程序读取数据集 `Retail.Order_fact` 并创建数据集 `Work.Orders`。`BUFSIZE=` 选项指定创建 `Work.Orders` 时缓冲区大小为 6144 字节。`BUFNO=` 选项指定每次 I/O 传输时将 10 页数据加载到内存中。 |

```
data work.orders (bufsize=6144 bufno=10);
   set retail.order_fact;
run;
```

 |

| ![4](img/callout04.png) `BUFSIZE=12288, BUFNO=2`此程序读取数据集 `Retail.Order_fact` 并创建数据集 `Work.Orders`。`BUFSIZE=` 选项指定创建 `Work.Orders` 时缓冲区大小为 12288 字节。`BUFNO=` 选项指定每次 I/O 传输时将 2 页数据加载到内存中。 |

```
data work.orders (bufsize=12288 bufno=2);
   set retail.order_fact;
run;
```

 |

| ![5](img/callout05.png) `BUFSIZE=12288, BUFNO=5`此程序读取数据集 `Retail.Order_fact` 并创建数据集 `Work.Orders`。`BUFSIZE=` 选项指定创建 `Work.Orders` 时缓冲区大小为 12288 字节。`BUFNO=` 选项指定每次 I/O 传输时将 5 页数据加载到内存中。 |

```
data work.orders (bufsize=12288 bufno=5);
   set retail.order_fact;
run;
```

 |

| ![6](img/callout06.png) `BUFSIZE=6144, BUFNO=10`此程序读取数据集 `Retail.Order_fact` 并创建数据集 `Work.Orders`。`BUFSIZE=` 选项指定创建 `Work.Orders` 时缓冲区大小为 6144 字节。`BUFNO=` 选项指定每次 I/O 传输时将 10 页数据加载到内存中。 |

```
data work.orders (bufsize=6144 bufno=10);
   set retail.order_fact;
run;
``` |

# 使用 SASFILE 语句

## 概述

另一种改进性能的方法是使用 `SASFILE` 语句将文件保留在内存中，以便供多个步骤使用。保持文件在内存中可以减少 I/O 处理和打开/关闭操作。

| 通用格式，`SASFILE` 语句：`SASFILE SAS-data-file <(password))> `OPEN` &#124; `LOAD` &#124; `CLOSE`;以下是该语法的解释：SAS-data-file 是有效数据集（类型）。password-options 指定一个或多个选项。OPEN 打开文件并分配缓冲区，但推迟将数据加载到内存。LOAD 打开文件、分配缓冲区并将数据加载到内存。CLOSE 关闭文件并释放缓冲区。 |

`SASFILE` 语句打开文件并分配足够的缓冲区来容纳整个文件。一旦文件被读取，数据将保留在内存中，直到发生以下任一情况：

*   执行 `SASFILE CLOSE` 语句，释放缓冲区并关闭文件
*   SAS 会话结束，自动释放缓冲区并关闭文件

在以下程序中，第一个 `SASFILE` 语句打开文件 `Company.Sales`，分配缓冲区并将数据加载到内存。

```
sasfile company.sales load;
proc print data=company.sales;
   var Customer_Age_Group;
run;
proc tabulate data=company.sales;
   class Customer_Age_Group;
   var Customer_BirthDate;
   table Customer_Age_Group,Customer_BirthDate*(mean median);
run;
sasfile company.sales close;
```

注意：`SASFILE` 语句也可用于减少重复读取一个或多个 SAS 视图的 CPU 时间和 I/O。使用 `DATA` 步骤在 Work 库中创建一个视图结果集的 SAS 数据集。然后使用 `SASFILE` 语句将该数据集加载到内存。注意：虽然使用 `SASFILE` 语句打开的文件可用于后续的输入或更新处理，但不支持后续的实用或输出处理。例如，您无法替换文件或重命名其变量。

## 使用 SASFILE 语句的指南

执行 SASFILE 语句时，SAS 根据数据文件索引文件的页数分配缓冲区。如果内存中的文件在处理过程中由于更改或添加而增大，缓冲区数量也会随之增加。重要的是，只有在有足够的实际内存的情况下才能减少 I/O 处理。如果没有足够的实际内存，操作系统可能会使用以下内容：

*   虚拟内存





*   默认缓冲区数量

如果 SAS 使用了虚拟内存，性能可能会下降。如果您需要重复处理部分 SAS 数据文件，且整个文件无法完全装入内存，请使用带有 `SASFILE` 语句的 `DATA` 步创建一个可以完全放入内存的文件子集。然后反复处理该子集。此操作可以在处理步骤中节省 CPU 时间，因为这些步骤读取的是较小的文件，而且还有文件驻留于内存带来的益处。

注意：当使用 `SASFILE` 语句时，请在程序运行时监控分页活动（由您操作环境的虚拟内存管理子系统所执行的 I/O 活动）。如果分页活动大幅增加，请考虑减少内存中的数据量。

## 比较示例：使用 SASFILE 语句

### 使用不同大小的数据文件

假设您想从不同大小的 SAS 数据文件中创建多个报告。通过使用小、中、大尺寸的数据文件，可以比较在运行 `PRINT`、`TABULATE`、`MEANS` 和 `FREQ` 过程时，使用或不使用 `SASFILE` 语句创建报告的资源使用情况。

| 数据文件名称 | 行数 | 页面大小 | 页数 | 字节数 |
| --- | --- | --- | --- | --- |
| Retail.Small | 45,876 | 24,576 | 540 | 13,279,232 |
| Retail.Medium | 458,765 | 24,576 | 5,398 | 132,669,440 |
| Retail.Large | 4,587,654 | 24,576 | 53,973 | 1,326,448,640 |

以下示例程序比较了使用数据文件大小的六种技术。可以使用这些示例作为在自己的环境中创建基准程序的模型。您的结果可能会取决于您的数据结构、操作环境以及您所在地的可用资源。

### 编程技术

| ![1](img/callout01.png) 不使用 SASFILE 语句的小数据文件。此程序使用 `PRINT`、`TABULATE`、`MEANS` 和 `FREQ` 过程创建报告。SAS 数据文件 `Retail.Small` 在每个过程中都会被打开和关闭。 |

```
proc print data=retail.small;
   where cs=100;
   var Customer_Age_Group;
run;
proc tabulate data=retail.small;
   class Customer_Age_Group;
   var Customer_BirthDate;
   table Customer_Age_Group,Customer_BirthDate*(mean median);
run;
proc means data=retail.small;
   var Customer_Age;
   class Customer_Group;
   output out=summary sum=;
run;
proc freq data=retail.small;
   tables Customer_Country;
run;
``` |

| ![2](img/callout02.png) 不使用 SASFILE 语句的中数据文件。此程序使用 `PRINT`、`TABULATE`、`MEANS` 和 `FREQ` 过程创建报告。SAS 数据文件 `Retail.Medium` 在每个过程中都会被打开和关闭。 |

```
proc print data=retail.medium;
   where cm=100;
   var Customer_Age_Group;
run;
proc tabulate data=retail.medium;
   class Customer_Age_Group;
   var Customer_BirthDate;
   table Customer_Age_Group,Customer_BirthDate*(mean median);
run;
proc means data=retail.medium;
   var Customer_Age;
   class Customer_Group;
   output out=summary sum=;
run;
proc freq data=retail.medium;
   tables Customer_Country;
run;
``` |

| ![3](img/callout03.png) 不使用 SASFILE 语句的大数据文件。此程序使用 `PRINT`、`TABULATE`、`MEANS` 和 `FREQ` 过程创建报告。SAS 数据文件 `Retail.Large` 在每个过程中都会被打开和关闭。 |

```
proc print data=retail.large;
   where cl=100;
   var Customer_Age_Group;
run;
proc tabulate data=retail.large;
   class Customer_Age_Group;
   var Customer_BirthDate;
   table Customer_Age_Group,Customer_BirthDate*(mean median);
run;
proc means data=retail.large;
   var Customer_Age;
   class Customer_Group;
   output out=summary sum=;
run;
proc freq data=retail.large;
   tables Customer_Country;
run;
``` |

| ![4](img/callout04.png) 使用 SASFILE 语句的小数据文件。在此程序中，`SASFILE LOAD` 语句打开 SAS 数据文件 `Retail.Small` 并将整个文件加载到内存中。随后 `PRINT`、`TABULATE`、`MEANS` 和 `FREQ` 过程可以使用这些数据。`SASFILE CLOSE` 语句关闭 `Retail.Small` 并释放缓冲区。 |

```sassasfile retail.small load;
proc print data=retail.small;
   where cs=100;
   var Customer_Age_Group;
run;
proc tabulate data=retail.small;
   class Customer_Age_Group;
   var Customer_BirthDate;
   table Customer_Age_Group,Customer_BirthDate*(mean median);
run;
proc means data=retail.small;
   var Customer_Age;
   class Customer_Group;
   output out=summary sum=;
run;
proc freq data=retail.small;
   tables Customer_Country;
run;
``` |

| ![5](img/callout05.png) 使用 SASFILE 语句的中数据文件。此程序中使用 `PRINT`、`TABULATE`、`MEANS` 和 `FREQ` 过程创建报告。`SASFILE LOAD` 语句打开 SAS 数据文件 `Retail.Medium` 并将整个文件加载到内存中。随后 `PRINT`、`TABULATE`、`MEANS` 和 `FREQ` 过程可以使用这些数据。`SASFILE CLOSE` 语句关闭 `Retail.Medium` 并释放缓冲区。 |

```
sasfile retail.medium load;
proc print data=retail.medium;
   where cm=100;
   var Customer_Age_Group;
run;
proc tabulate data=retail.medium;
   class Customer_Age_Group;
   var Customer_BirthDate;
   table Customer_Age_Group,Customer_BirthDate*(mean median);
run;
proc means data=retail.medium;
   var Customer_Age;
   class Customer_Group;
   output out=summary sum=;
run;
proc freq data=retail.medium;
   tables Customer_Country;
run;
``` |

| ![6](img/callout06.png) 使用 SASFILE 语句的大数据文件。在此程序中，`SASFILE LOAD` 语句打开 SAS 数据文件 `Retail.Large` 并将整个文件加载到内存中。随后 `PRINT`、`TABULATE`、`MEANS` 和 `FREQ` 过程可以使用这些数据。`SASFILE CLOSE` 语句关闭 `Retail.Large` 并释放缓冲区。 |

```
sasfile retail.large load;
proc print data=retail.large;
   where cl=100;
   var Customer_Age_Group;
run;
proc tabulate data=retail.large;
   class Customer_Age_Group;
   var Customer_BirthDate;
   table Customer_Age_Group,Customer_BirthDate*(mean median);
run;
proc means data=retail.large;
   var Customer_Age;
   class Customer_Group;
   output out=summary sum=;
run;
proc freq data=retail.large;
   tables Customer_Country;
run;
``` |

### 一般建议

*   如果您需要重复处理完全装入内存的 SAS 数据文件，请使用 `SASFILE` 语句来减少 I/O 和某些 CPU 使用。
*   如果您使用 `SASFILE` 语句但 SAS 数据文件无法完全装入内存，代码可以执行，但性能可能会下降。
*   如果您需要重复处理部分 SAS 数据文件且整个文件无法装入内存，请使用带有 `SASFILE` 语句的 `DATA` 步创建一个可以完全放入内存的文件子集。然后反复处理该子集。此操作可以在处理步骤中节省 CPU 时间，因为这些步骤读取的是较小的文件，而且还有文件驻留于内存带来的益处。

# 其他功能

## 使用 IBUFSIZE 系统选项

从 SAS 9 开始，您可以使用 `IBUFSIZE=` 系统选项来指定索引文件的页面大小。通常情况下，不需要指定索引页面大小。但在出现以下情况时，您可能需要使用 `IBUFSIZE=` 选项：

*   您的应用程序在索引文件中遇到了大量的 I/O
*   索引值的长度非常大

减少索引层级时节省的主要资源是 I/O。如果您的应用程序在索引文件中遇到了大量的 I/O，增加页面大小可能会帮助。但在增加页面大小后，您必须重新创建索引文件。





| 通用格式，系统选项 `IBUFSIZE=`：`IBUFSIZE= MAX` &#124; `n;`；以下是语法说明：`MAX` 将索引文件的页大小设置为最大可能的数值。对于 `IBUFSIZE=`，其最大值为 32,767 字节。`n` 指定以字节为单位的页大小。 |

注意：应避免使用 `MIN` 设置。当使用索引处理请求时（例如用于 `WHERE` 处理时），SAS 会按顺序搜索索引文件，以快速定位请求的记录或记录。页大小影响索引的层数。页数越多，索引的层数就越多。层数越多，索引搜索所需的时间越长。增加页大小允许每页上存储更多的索引值，从而减少页数（以及层数）。使用 `IBUFSIZE=0` 将索引页大小重置为您操作环境中的默认值。注意：有关使用 `IBUFSIZE=` 系统选项的更多详细信息，请参阅 SAS 文档。

## 总结

## 控制页大小和缓冲区数量

当你读取 SAS 数据集或外部文件时，当输入数据被复制到内存中的缓冲区，以及当它从输出缓冲区复制到输出数据集时，就会进行 I/O 操作。页是存储设备与内存之间数据传输的单位。增加页大小可以通过减少 SAS 从存储介质读取或写入介质的次数来缩短执行时间。你可以使用 `CONTENTS` 过程报告页大小和页数。你可以使用 `BUFSIZE=` 系统选项或数据集选项来控制输出 SAS 数据集的页大小。新的缓冲区大小是永久的。一旦指定，每当处理数据集时都会使用它。你可以使用 `BUFNO=` 系统选项或数据集选项来控制读取或写入 SAS 数据集时的可用缓冲区数量。通过增加缓冲区数量，你可以控制每次 I/O 传输将多少页数据加载到内存中。`BUFNO=` 和 `BUFSIZE=` 的乘积（其中任一选项的具体值，决定了单次 I/O 操作可以传输多少数据。增加任何一个选项都会增加单次 I/O 操作可传输的数据量。然而，I/O 性能的提升是以增加内存消耗为代价的。

## 使用 SASFILE 语句

另一种提高性能的方法是使用 `SASFILE` 语句将 SAS 数据文件保留在内存中，以便多个程序步骤可以使用该数据。保持数据集打开可以减少 I/O 处理和打开/关闭操作，包括缓冲区的内存分配和释放。当执行 `SASFILE` 语句时，SAS 会根据数据文件和索引文件的页数分配缓冲区数量。如果内存中的文件在处理过程中由于数据更改或添加而增大，缓冲区数量也会之增加。只有在有足够的物理内存时，I/O 处理才会减少。如果 SAS 使用虚拟内存，性能可能会下降。

### 附加功能

`IBUFSIZE=` 系统选项指定索引文件的页大小。通常，你不需要指定索引页大小。但是，如果符合以下情况，你可能需要使用 `IBUFSIZE=` 选项：

*   你的应用程序在索引文件中经历了大量的 I/O 操作
*   索引值非常大

减少索引层数节省的主要资源是 I/O。如果你的应用程序在索引文件中经历了大量的 I/O 操作，增加页大小可能会帮助。但是，在增加页大小后，你必须重新创建索引文件。所需的页数取决于页大小、索引值的长度以及值本身。

# 测验

为每个问题选择最佳答案。完成测验后，使用附录中的答案键检查你的答案。

1. 关于 `BUFNO=` 选项，以下哪种描述是正确的？

    1. `BUFNO=` 选项指定用于读取或写入 SAS 数据集的每个缓冲区的大小。
    2. `BUFNO=` 选项通过限制所需的输入/输出操作次数来提高执行速度。
    3. 使用 `BUFNO=` 选项会导致数据集发生永久性更改。
    4. 使用 `BUFNO=` 选项增加缓冲区数量会导致内存消耗减少。

2. 关于页（page），以下哪种描述是**不**正确的？

    1. 页是存储设备与内存之间数据传输的单位。
    2. 一页包含了描述符部分、数据值和开销所占用的字节数。
    3. 页的大小比比缓冲区的大小。
    4. 页的大小可以随时更改。

3. 数据集占用的总字节数等于以下哪项？

    1. 页大小乘以页数。
    2. 页大小乘以观测值数量。
    3. 页大小与页数之和。
    4. 页数乘以变量数。

4. 哪条语句打开了文件 `Work.Quarter1`，分配了足够的缓冲区将整个文件加载到内存中，并将数据读入内存？

    1. ```sas
       sasfile work.quarter1 open;
       ```
    2. ```sas
       sasfile work.quarter1 load;
       ```
    3. ```sas
       sasfile work.quarter1 bufno=max;
       ```
    4. ```sas
       sasfile work.quarter1 bufsize=max;
```

5. 关于使用 `SASFILE` 语句打开的文件，以下哪种描述是正确的？

    1. 该文件在 `SASFILE` 语句执行后对后续 DATA 步骤可用。
    2. 该文件在 `END` 语句执行后对后续 DATA 步骤可用。
    3. 该文件在程序结束前对工具或输出可用。
    4. 如果文件在处理过程中增大，缓冲区数量保持不变。

# 第 21 章：控制数据存储空间

## 概述

引言

在许多计算环境中，数据存储空间是有限资源。因此，对于你来说，节省数据存储空间可能比节省其他资源更重要。将数据存储在 SAS 数据文件中时，你会使用以下内容所需的存储空间之和：

*   描述部分
*   观测值（数据部分）
*   任何存储开销
*   任何关联索引

![描述部分](img/m82-1-g1.png) 在本章，你将学习各种技术来尽量减少 SAS 数据文件占用的空间。

## 减少字符变量的数据存储空间

减少数据存储空间（同时也减少 I/O）的一种方法是减少字符变量的长度，从而可能消除浪费的空间。在讨论如何减少长度之前，请考虑 SAS 如何为字符变量分配长度。

### 使用 LENGTH 语句减少字符数据

你可以使用 `LENGTH` 语句来控制字符变量的长度。





| 字符变量的 `LENGTH` 语句通用格式：`LENGTH variable(s) $ length;` 以下是该语法的解释：`variable(s)` 指定一个或多个 SAS 变量的名称，用空格分隔。`length` 是一个从 1 到 32,767 之间的整数，指定 `variable(s)` 的长度。 |

注意：确保 `LENGTH` 语句出现在 `DATA` 步中对该变量的任何引用之前。如果该变量已由其他语句创建，那么稍后使用 `LENGTH` 语句不会更改其长度。

# 减少数值变量的数存储空间

减少数据存储空间的另一种方法是缩短数值变量的长度。除了节省数据存储空间外，缩短长度的数值变量在写入和读取数据时使用更少的 I/O。对于频繁读取的文件，这种节省可能是极其巨大的。然而，为了安全地缩短数值变量的长度，你需要了解 SAS 如何存储数值数据。

## SAS 如何存储数值变量

为了存储大数值的数字并执行对小数点右侧需要许多位精度的计算，SAS 使用双精度浮点表示法存储所有数值。SAS 数值变量的最大长度为 8 字节，最小长度取决于您的操作系统环境为 2 或 3 字节。默认长度为 8 字节。每个字节存储多个数字。浮点表示法是科学计数法的实现。例如，数字 234 可以写为基数为 10 的 `.234*10**3`。在这个示例中，`.234` 被称为尾数，`10` 是基数，`3` 是指数。下面的图显示了 SAS 如何用 8 字节存储一个数值。主机环境使用基数 16。第一位存储符号，接下来的 7 位存储指数，剩余的 56 位存储尾数。![浮点表示法](img/m82-3-g1.png) 非主机环境使用基数 2。第一位存储符号，接下来的 11 位存储指数，剩余的 52 位存储尾数。![浮点表示法](img/m82-3-g2.png) 注意：数值变量在主机环境中的最小长度为 2 字节，在非主机环境中为 3 字节。现在你已经看到了 SAS 如何存储数值变量，请考虑你如何为你的数值变量分配一个小于默认长度 8 字节的长度。

## 为数值变量分配长度

你可以使用 `LENGTH` 语句为数值变量分配 2 到 8 字节的长度。记住，数值变量的最小长度取决于操作系统环境。此外，请记住 `LENGTH` 语句仅影响输出数据集中数值变量的长度。在程序数据向量（program data vector）和处理过程中，数值变量的长度始终为 8 字节。

| 数值变量的 `LENGTH` 语句通用格式：`LENGTH variable(s) length <DEFAULT=n>;` 以下是该语法的解释：`variable(s)` 指定一个或多个 SAS 数值变量的名称，用空格分隔。`length` 是指定 `variable(s)` 长度的整数。`DEFAULT=n` 此可选参数更改了 SAS 用于存储任何新创建的数值变量的默认字节数。如果你使用 `DEFAULT=` 参数，则不需要列出任何变量。 |

`DEFAULT=` 仅适用于 `LENGTH` 语句之后创建的数值变量。如果你希望列出的变量接收指定的长度，请列出特定的变量及其长度，以及 `DEFAULT=` 参数。然后，未列出的变量将接收 `DEFAULT=` 长度。**注意**：数值在截断时会丢失精度。你将在本章的下一节学习更多关于缩短长度数值变量导致精度丢失的内容。

## 示例

以下程序为 `ReducedSales` 数据集中的新变量 `Sale_Percent` 分配了 4 的长度。该 `DATA` 步中的 `LENGTH` 语句不适用于从 `Sales` 数据集中读取的变量；这些变量在读取到 `ReducedSales` 时将保持它们在 `Sales` 中原有的任何长度。

```
data reducedsales;
   length default=4;
   set sales;
   Sale_Percent=15;
run;
```

## 在缩短长度的数值变量中保持精度

缩短长度的数值变量中可以精确存储的值是有限制的。你已经了解到，减少用于存储数值变量的字节数不会影响数字在程序数据向量中的存储方式。相反，在 `LENGTH` 语句中指定小于 8 的值会导致该数字在写入 SAS 数据集时被截断为指定的长度。如果值不是整数，则永远不要使用 `LENGTH` 语句来减少数值变量的长度。小数在截断时会丢失精度。即使值是整数，你也应该记住，缩短数值变量的长度限制了可以作为值准确存储的整数值。下表列出了在 UNIX 或 Windows 操作系统环境中整数值可能的光存储长度。

表 21.1 UNIX 或 Windows

| 长度（字节） | 精确表示的最大整数 |
| --- | --- |
| 3 | 8,192 |
| 4 | 2,097,152 |
| 5 | 536,870,912 |
| 6 | 137,438,953,472 |
| 7 | 35,184,372,088,832 |
| 8 | 9,007,199,254,740,992 |

下表列出了在 z/OS 环境下整数值可能的存储长度。

表 21.2 z/OS

| 长度（字节） | 精确表示的最大整数 |
| --- | --- |
| 2 | 256 |
| 3 | 65,536 |
| 4 | 16,777,216 |
| 5 | 4,294,967,296 |
| 6 | 1,099,511,627,776 |
| 7 | 281,474,946,710,656 |
| 8 | 72,057,594,037,927,936 |

假设你存储了一个等于或小于上述列出的精确表示的整数。在这种情况下，SAS 会截断全零字节。如果存储在缩短长度变量中的整数大于限制，SAS 会截断非零字节，整数值会发生变化。同样，你不应该减少非整数数据的存储大小，因为这会导致截断引起的精度丢失。

## 使用 PROC COMPARE

你可以使用 `PROC COMPARE` 来衡量存储在缩短数值变量中的精度。你通过比较原始变量与缩短后的变量来实现这一点。`COMPARE` 过程比较两个 SAS 数据集、不同数据集中的选定变量或同一个数据集中的变量。

| 比较数据集的 `PROC COMPARE` 步：`PROC COMPARE BASE=data-set1 COMPARE=data-set2; RUN;` 以下是该语法的解释：`data-set1` 和 `data-set2` 指定要比较的两个 SAS 数据集。 |

`PROC COMPARE` 是衡量缩短数值变量精度损失的好技术，因为它即使在数值变量格式化后这些差异不再出现，它也能显示存储的数值之间是否存在差异。`PROC COMPARE` 查看两个数据集并比较以下内容：

*   数据集属性
*   匹配变量的属性
*   观测值
*   匹配变量的值

`COMPARE` 过程输出包含以下信息：

*   数据集摘要
*   变量摘要
*   具有不同属性的共同变量列表
*   观测值摘要
*   值比较摘要
*   值不等的变量列表





- `变量值比较结果的详细列表`

## 示例

数据集 `Company.Discount` 包含某些零售产品的销售日期和折扣数据。`Company.Discount` 中有 `35` 个观测值，描述如下。

| 变量 | 类型 | 长度 | 描述 |
| --- | --- | --- | --- |
| `Product_ID` | num | 8 | 产品 ID 号 |
| `Start_Date` | num | 4 | 销售开始日期 |
| `End_Date` | num | 5 | 销售结束日期 |
| `Unit_Sales_Price` | num | 8 | 单位折扣售价 |
| `Discount` | num | 8 | 正常销售价格的折扣百分比 |

假设你缩短了数值变量 `Discount` 的长度。下面的 `DATA` 步创建一个名为 `Company.Discount_Short` 的新数据集，它与 `Company.Discount` 的区别在于变量 `Discount` 的长度为 4 而不是 8。

```
data company.discount_short;
   length Discount 4;
   set Company.Discount;
run;
```

你可以使用 `PROC COMPARE` 通过比较 `Company.Discount` 和 `Company.Discount_Short` 来评估缩短 `Discount` 长度是否影响了其值的精度。

```
proc compare base=company.discount
             compare=company.discount_short;
run;
```

如果你打印这两个数据集（`Company.Discount` 和 `Company.Discount_Short`），这些值看起来可能是完全相同的。然而，它们在存储的值上存在差异，但这些差异在格式化输出中并不明显。在下方的部分输出中，你可以看到缩短 `Discount` 的长度会导致其值的精度丢失；`Company.Discount_Short` 中 `Discount` 的值最大差异为 `1.9073E-07`。值比较结果显示，尽管前五个观测值中的 `Discount` 值在两个数据集中都显示为 `70%`，但精确的（未格式化的）值差异为 `-1.907E-7`。图 21.1 `PROC COMPARE` 部分输出![PROC COMPARE Output](img/m82-6-g1.png)![Values Comparison Summary](img/m82-6-g2.png)![Value Comparison Results](img/m82-6-g3.png)

## 对比示例：创建一个包含缩短数值变量的 SAS 数据集

### 默认长度与缩短数值变量

假设你想创建一个 SAS 数据集来存储一组订单的零售数据。假设你想包含在数据集中的数据都是数值数据，并且它们目前存储在原始数据文件中。以下示例程序比较了两种技术。你可以将这些示例作为模型，在你自己的环境中创建基准程序。你的结果可能会根据数据结构、操作系统环境以及你所在位置的可用资源有所不同。注意：在本书中，示例程序中经常使用 `_NULL_` 关键字代替数据集名称。使用 `_NULL_` 会抑制输出数据集的创建。在进行基准测试时使用 `_NULL_` 可以让你确定读取 SAS 数据集时使用了哪些资源。

### 编程技术

| ![1](img/callout01.png) 默认长度数值变量此程序读取由文件引用符 `Flat1` 引用的外部数据文件，并创建一个名为 `Retail.Longnums` 的新数据集，其中包含 `12` 个数值变量。`Retail.Longnums` 中的每个变量都有 8 字节的默认存储长度。该程序的第二个 `DATA` 步从 `Retail.Longnums` 中读取数值变量。 |

```
data retail.longnums;
   infile flat1;
   input  Customer_ID          12.
          Employee_ID          12.
          Street_ID            12.
          Order_Date           date9.
          Delivery_Date        date9.
          Order_ID             12\. 
          Order_Type           comma16.
          Product_ID           12\.     
          Quantity             4\.     
          Total_Retail_Price   dollar13.2
          CostPrice_Per_Unit   dollar13.2
          Discount             5\.        ;
run;

data _null_;
   set retail.longnums;
run;
```

| ![2](img/callout02.png) 缩短长度数值变量此程序读取由文件引用符 `Flat1` 引用的外部数据文件，并创建一个名为 `Retail.Shortnums` 的 SAS 数据集，其中包含 `12` 个数值变量。使用 `LENGTH` 语句缩短 `Retail.Shortnums` 中大多数数值变量的存储长度，如下： |

* `Total_Retail_Price` 和 `CostPrice_Per_Unit` 的存储长度为 8 字节。
* `Product_ID` 的存储长度为 7 字节。
* `Street_ID` 和 `Order_ID` 的存储长度为 6 字节。
* `Employee_ID` 的存储长度为 5 字节。
* `Customer_ID`、`Order_Date`、`Delivery_Date` 和 `Discount` 的存储长度为 4 字节。
* `Order_Type` 和 `Quantity` 的存储长度为 3 字节。

第二个 `DATA` 步从 `Retail.Shortnums` 中读取缩短长度的数值变量。

```
data retail.shortnums;
   infile flat1;
          length Quantity  Order_Type   3
          Customer_ID  Order_Date
          Delivery_Date  Discount       4
          Employee_ID                   5
          Street_ID  Order_ID           6
          Product_ID                    7
          Total_Retail_Price
          CostPrice_Per_Unit
   input  Customer_ID          12.
          Employee_ID          12.
          Street_ID            12.
          Order_Date           date9.
          Delivery_Date        date9.
          Order_ID             12\. 
          Order_Type           comma16.
          Product_ID           12\.     
          Quantity             4\.     
          Total_Retail_Price   dollar13.2
          CostPrice_Per_Unit   dollar13.2
          Discount             5\.        ;
run;

data _null_;
   set retail.shortnums;
run;
```

# 压缩数据集

## 概述

默认情况下，SAS 数据文件是未压缩的。你可以压缩数据文件以节省空间，尽管某些文件并不是适合压缩的。压缩数据文件的结构与未压缩文件不同。你使用 `COMPRESS=` 数据集选项或系统选项来压缩数据文件。使用 `POINTOBS=` 数据选项可以允许 SAS 直接访问观测值，而不是顺序访问。使用 `REUSE=` 数据集选项或系统选项来指定在添加或更新观测值时 SAS 应该重用空间。

## 查看未压缩文件结构

默认情况下，SAS 数据文件未压缩。在未压缩数据文件中，以下语句是正确的：

* 特定变量的每个值占据的字节数与该变量的任何值相同。
* 每个观测值占据的字节数与任何观测值相同。
* 字符填充空格。
* 数值填充零。
* 每个页末尾有一个观测值的 1 位开销（四舍五入到字节），该位表示观测值的已删除或未删除状态。
* 新观测值添加到文件的末尾。如果新观测值无法放入当前最后一个页，则会添加一个新的数据集页。
* 文件的描述部分存储在文件的第一页。

下图显示了未压缩数据文件的结构![未压缩数据文件](img/m82-10-g1.png)注意：在 64 位操作系统环境中，每页有 40 字节的开销。在 32 位操作系统环境中，每页有 24 字节的开销。

## 压缩文件结构




在压缩数据文件中，以下语句是正确的：

*   通过忽略变量类型和边界，每个观测值被视为单个字节字符串。
*   连续重复的字符和数字被合并为更少的字节。
*   在 32 位操作系统环境中，每页的开头有 24 字节的开销；在 64 位操作系统环境中则有 40 字节的开销。
*   页开销之后每个观测值有 12 字节或 24 字节的开销。该空间用于删除状态、压缩长度、指针和标志。

压缩数据文件中的每个观测值长度不同，这意味着数据文件中某些页存储的观测值比其他页更多。当更新的观测值大于原始大一时，它将存储在相同的数据文件页上并使用可用空间。如果原始页没有足够的空间，观测值将存储在具有足够空间的下一页，并在原始页上存储一个指针。下图描述了压缩数据文件的结构。![压缩数据文件](img/m82-11-g1.png)

## 决定是否压缩数据文件

并不是所有数据文件都是压缩的良好候选者。记住，为了让 SAS 读取压缩文件，每个观测值都必须解压缩。这比读取未压缩文件需要更多的 CPU 资源。然而，当数据文件具有以下一个或多个属性时，压缩是有益的：

*   它很大。
*   它包含许多长字符值。
*   它包含许多具有重复字符或二进制零的值。
*   它包含许多缺失值。
*   在物理相邻相邻的变量中包含重复值。

在字符数据中，最经常遇到的重复值是空格。长文本字段（如注释和地址）通常包含重复的空格。同样，二进制零用于填充可以存储在更少字节中的数值值。这通常发生在为 8 字节数值变量分配较型或中型整数时。

注意：如果节省磁盘空间至关重要，请考虑将缺失数据存储为小整数（如 `0` 或 `9`），而不是 SAS 缺失值。小整数的压缩程度比 SAS 缺失值更高。

如果数据文件具有以下任何特征，则不是压缩的良好候选者：

*   重复字符较少
*   物理尺寸较小
*   缺失值较少
*   文本字符串较短

下文探讨了如何压缩数据文件。

## COMPRESS= 系统选项和 COMPRESS= 数据集选项

要压缩数据文件，您可以使用 `COMPRESS=` 数据集选项或 `COMPRESS=` 系统选项。您使用 `COMPRESS=` 系统选项来压缩在 SAS 会话期间创建的所有数据文件。同样地，您使用 `COMPRESS=` 数据集选项来压缩单个数据文件。

| `COMPRESS=` 系统选项的通用形式：`OPTIONS COMPRESS= NO` | `YES` | `CHAR` | `BINARY;` |
| :--- | :--- | :--- | :--- |
| 此处是对该语法的解释：`NO` 是默认设置，不压缩数据集。 | `CHAR` 或 `YES` 使用行程长度编码 (RLE) 压缩算法，该算法可以压缩连续重复的字节，例如尾随空格或重复的零。 | `BINARY` 使用 Ross 数据压缩 (RDC)，它结合了行程长度编码和滑动窗口压缩。 | |

注意：如果您将 `COMPRESS=` 系统选项设置为 `NO` 以外的值，SAS 将压缩当前 SAS 会话期间创建的每个数据集，包括 `Work` 库中的临时数据集。虽然这可能节省数据存储空间，但会消耗更多的其他资源。

| `COMPRESS=` 数据集选项的通用形式：`DATA SAS-data-set (COMPRESS= NO` | `YES` | `CHAR` | `BINARY);` |
| :--- | :--- | :--- | :--- |
| 此处是对该语法的解释：`SAS-data-set` 指定要压缩的数据集。 | `NO` 是默认设置，不压缩数据集。 | `CHAR` 或 `YES` 使用行程长度编码 (RLE) 压缩算法，该算法可以压缩连续重复的字节，例如尾随空格或重复的零。 | `BINARY` 使用 Ross 数据压缩 (RDC)，它结合了行程长度编码和滑动窗口压缩。 |

注意：`COMPRESS=` 数据集选项会覆盖 `COMPRESS=` 系统选项。`COMPRESS=` 选项的 `YES` 或 `CHAR` 设置使用 RLE 压缩算法。RLE 通过将连续重复的字符（包括空格）减少为双字节或三字节表示来压缩观测值。因此，RLE 通常对于包含重复空格的字符数据最有用。`YES` 或 `CHAR` 设置也适用于压缩大多数值均为零的数值数据。

`COMPRESS=` 选项的 `BINARY` 设置使用 RDC，它结合了行程长度编码和滑动窗口压缩。该方法对于压缩中等较大的二进制数据块（数值变量）非常有效。使用 `COMPRESS=` 选项的 `BINARY` 设置压缩的文件，其解压缩时间比使用 `YES` 或 `CHAR` 设置压缩的文件消耗更多的 CPU 时间。`BINARY` 对于长度为几百字节或以上的观测值效率更高。`BINARY` 对于包含模式而非简单重复的字符数据也非常有效。

当您创建压缩数据文件时，SAS 会比较压缩文件与相同页大小的未压缩文件的大小。然后 SAS 会在日志中写入注释，指示通过压缩文件获得的尺寸减少百分比。

当您使用 `COMPRESS=` 选项时，SAS 会计算引入的开销大小以及您尝试压缩的数据集中观测值的最大大小。如果原始页没有足够的空间，观测值将存储在具有足够空间的下一页，并在原始页上存储一个指针。如果观测值的最大大小小于引入的开销，SAS 将禁用压缩，创建一个未压缩数据集并发出警告消息。一旦文件被压缩，该设置就是文件的永久属性。为了将设置改为未压缩，您必须重新创建文件。注意：并不是所有 SAS 引擎都支持观测值的压缩。更多信息请参见 `COMPRESS=` 数据集选项。

## 示例

数据集 `Company.Customer` 包含有关零售公司的人口统计信息。该数据集包括 `Name`、`FirstName`、`LastName` 和 `Address` 等字符变量。这些字符变量可能包含许多空格。即使 `COMPRESS=` 系统选项设置为 `NO`，以下程序也会创建一个名为 `Company.Customers_Compressed` 的压缩数据集。

```
data company.customer_compressed (compress=char);
   set company.customer;
run;
```

SAS 在日志中写入关于新数据集压缩的注释，如下所示

表 21.3 SAS 日志

| |
| :--- |
| NOTE: 从 `COMPANY.CUSTOMER` 读取了 89954 个观测值。 |
| NOTE: 数据集 `COMPANY_CUSTOMER_COMPRESSED` 包含 89954 个观测值和 11 个变量。 |
| NOTE: 压缩数据集 `COMPANY_CUSTOMER_COMPRESSED` 尺寸减少了 32.81%。 |
| 压缩后为 991 页；未压缩需要 1475 页。 |
| NOTE: 使用 DATA 语句（总处理时间）： |
| 实际时间 3.90 秒 |
| CPU 时间 0.96 秒 |

通常情况下，您在程序中使用压缩数据集的方式与使用未压缩数据集的方式相同。但是，有两个选项专门适用于压缩数据集。

## 在压缩数据集中直接访问观测值



默认情况下，`DATA` 步按顺序处理 SAS 数据集中的观测值。然而，有时你可能希望直接访问观测值，而不是按顺序访问，因为这样做可以节省 CPU 时间、I/O 和实时等资源。你可以在 `MODIFY` 或 `SET` 语句中使用 `POINT=` 选项来直接访问观测值而非按顺序访问。你可以在创建索引中查看有关 `POINT=` 选项的信息。你也可以使用 `FSEDIT` 过程来直接访问观测值。

在压缩数据集中允许直接访问观测值会增加创建或更新数据集所需的 CPU 时间。你可以设置一个选项不允许对压缩数据集进行直接访问。如果对于你来说，在压缩数据集中通过编号直接指向某个观测值并不重要，那么禁止直接访问以提高创建和更新数据集的效率是一个好做法。下主题将解释如何禁止对压缩数据集的观测值的直接访问。

## POINTOBS= 数据集选项

当你处理压缩的数据集时，你使用 `POINTOBS=` 数据集选项来控制是否可以使用直接访问（通过观测编号）处理观测值，而不是仅通过顺序访问。

| `POINTOBS=` 数据集选项的一格式：`DATA SAS-data-set (COMPRESS=YES | CHAR | BINARY POINTOBS= YES | NO);` |
| :--- |
| 以下是该语法的解释：`SAS-data-set` 指定你要压缩的数据集。`YES` 是默认设置，允许对数据集进行随机访问。`NO` 不允许对数据集进行随机访问。 |

**注意：** 为了使用 `POINTOBS=` 数据集选项，指定的 `SAS-data-set` 的 `COMPRESS=` 选项取值必须为 `YES`、`CHAR` 或 `BINARY`。

允许对数据集进行随机访问不会影响从数据集中检索信息的效率，但在创建或更新压缩数据集时，它会增加约 10% 的 CPU 使用率。也就是说，允许随机访问会降低写入压缩数据集的效率，但不会影响从压缩数据集中读取的效率。因此，如果你不需要通过观测编号访问数据，请指定 `POINTOBS=NO`。这样，在创建压缩数据集以及更新或向其添加观测值时，你可以提高性能约 10%。

## 示例

以下程序从 `Company.Customer` 数据集创建了一个名为 `Company.Customer_Compressed` 的数据集，并确保不允许对压缩数据集进行随机访问。

```
data company.customer_compressed (compress=yes pointobs=no);
   set company.customer;
run;
```

下主题将解释如何进一步减少压缩数据集所需的数据存储空间。

## REUSE= 系统选项和 REUSE= 数据集选项

SAS 默认将新观测值附加到所有数据集的末尾。如果你删除了数据集中的某个观测值，该位置将留下空磁盘空间。然而，仅在压缩集中可以在添加或更新观测值时跟踪并重用可用空间。通过重用数据集内部的空间，你可以节省数据存储空间。

`REUSE=` 系统选项和 `REUSE=` 数据集选项指定了在向压缩数据集添加观测值时 SAS 是否重用空间。如果你在 `DATA` 语句中将 `REUSE=` 数据集选项设置为 `YES`，SAS 将跟踪并重用在该 `DATA` 步中创建的压缩数据集中的空间。如果你将 `REUSE=` 系统选项设置为 `YES`，SAS 将跟踪并重用当前 SAS 会话剩余期间创建的所有压缩数据集中的可用空间。

| `REUSE=` 系统选项的一格式：`OPTIONS REUSE= NO | YES;` |
| :--- |
| 以下是该语法的解释：`NO` 是默认设置，指定 SAS 不跟踪压缩数据集中的未使用空间。`YES` 指定每当向现有压缩数据集添加观测值时，SAS 跟踪可用空间并重用它。 |

| `REUSE=` 数据集选项的一格式：`DATA SAS-data-set (COMPRESS=YES REUSE=NO | YES);` |
| :--- |
| 以下是该语法的解释：`SAS-data-set` 指定你要压缩的数据集。`NO` 是默认设置，指定 SAS 不跟踪压缩数据集中的未使用空间。`YES` 指定每当向现有压缩数据集添加观测值时，SAS 跟踪可用空间并重用它。 |

**注意：** `REUSE=` 数据集选项会覆盖 `REUSE=` 系统选项。

如果 `REUSE=` 选项设置为 `YES`，添加到 SAS 数据集中的观测值将插入到任何存在足够可用空间的地方，而不是在 SAS 数据集的末尾。如果在 SAS 数据集中删除或更新了许多观测值，为 `REUSE=` 选项指定 `NO` 会导致空间效率降低，因为数据集内部存在未使用空间。当 `REUSE=` 选项设置为 `NO` 时，`APPEND` 过程、`FSEDIT` 过程和其他向 SAS 数据集添加观测值的过程会将观测值添加到数据集的末尾，就像它们处理未压缩数据集一样。

你无法在创建压缩数据集后更改其 `REUSE=` 属性。这意味着压缩 SAS 数据集中的空间跟踪和重用是根据创建 SAS 数据集时指定的 `REUSE=` 选项值，而不是根据你添加和删除观测值时。此外，你应该注意，即使 `REUSE=` 选项设置为 `YES`，`APPEND` 过程仍会将观测值添加到数据集的末尾。

**注意：** 指定 `REUSE=` 选项的值为 `YES` 会导致 `POINTOBS=` 选项的值变为 `NO`。插入新观测值（而非数据集末尾）与使用直接访问是不兼容的。

## 示例

以下程序从 `Company.Customer` 数据集创建了一个名为 `Company.Customer_Compressed` 的数据集。因为 `REUSE=` 选项设置为 `YES`，SAS 将跟踪并重用压缩数据集中的空空间。

```
data company.customer_compressed (compress=yes reuse=yes);
   set company.customer;
run;
```

## SAS 如何压缩数据

查看 SAS 如何压缩数据。下表描述了一个名为 `Roster` 的虚拟数据集。![Roster](img/m82-16-g1.png)

在未压缩格式下，`Roster` 中的每个观测值总共 35 字节存储这两个变量：第一个变量 `LastName` 占用 20 字节，第二个变量 `FirstName` 占用 15 字节。下图显示了未压缩版本 `Roster` 的观测值存储情况。![Roster](img/m82-16-g2.png)

假设你使用 `CHAR` 设置的 `COMPRESS=` 选项来压缩 `Roster`。在压缩格式下，重复空格被移除。`Roster` 的第一个观测值总共仅使用 13 字节：第一个变量 `LastName` 占用 7 字节，第二个变量 `FirstName` 占用 6 字节。下图显示了压缩版本 `Roster` 的观测值存储情况。![Roster](img/m82-16-g3.png)

`@` 表示随后的未压缩字符数量。`#` 表示观测值该处重复的空格数量。只有 SAS 引擎可以访问这些字节。你无法打印或操作它们。

二进制数据压缩（`COMPRESS=BINARY`）同时使用行程编码和滑动窗口压缩。假设一个 SAS 数据具有以下变量：

| 名称 | 类型 | 长度 |
| --- | --- | --- |
| Answer1 | Num | 8 |
| Answer2 | Num | 8 |
| ... | ... | ... |
| Answer200 | Num | 8 |

在未压缩格式下，SAS 数据文件类似于：

```
 1     2     3     4     5     6     7     8     9
@     +/1   1     #     @    +/1    2     #     %
```




`@` 符号表示后面跟着多少个未压缩字符。在文件中，`+/1` 是符号和指数。`#` 表示移除的二进制零的数量。`%` 表示这些值重复的次数。
注意：请记住，在压缩数据集中，观测值的长度可能并不完全相同，因为观测值的长度取决于观测值中每个值的长度。

## 比较示例：创建和读取压缩数据文件

假设你想从存储在两个原始数据文件中创建两个 SAS 数据集。由文件引用 `Flat1` 引用的原始数据文件包含关于某零售公司客户订单的数值数据；你想从该原始数据文件创建一个名为 `Retail.Orders` 的 SAS 数据集。由文件引用 `Flat2` 引用的原始数据文件包含关于某零售公司客户的字符数据；你想从该原始数据文件创建一个名为 `Retail.Customers` 的 SAS 数据集。在两种情况下，你都可以使用 `DATA` 步来创建未压缩的数据文件或压缩数据文件。此外，在任何情况下你都可以使用二进制压缩或字符压缩。以下示例程序比较了六种技术。你可以将这些示例作为在你自己的环境中创建基准测试程序的模型。你的结果可能会取决于数据结构、操作系统环境以及你所在地的资源。

### 编程技术

| 1. 数值数据，无压缩 | 下一个程序创建 SAS 数据集 `Retail.Orders`，它包含数值数据且未经过压缩。第二个 `DATA` 步读取未压缩的数据文件。 |
```
data retail.orders(compress=no);
   infile flat1;
   input  Customer_ID          12.
          Employee_ID          12.
          Street_ID            12.
          Order_Date           date9.
          Delivery_Date        date9.
          Order_ID             12\. 
          Order_Type           comma16.
          Product_ID           12\.     
          Quantity             4\.     
          Total_Retail_Price   dollar13.
          CostPrice_Per_Unit   dollar13.
          Discount             5\.            ;
run;

data _null_;
   set retail.orders;
run;
``` |
| 2. 数值数据，二进制压缩 | 下一个程序创建 SAS 数据集 `Retail.Orders_binary`，它包含数值数据并使用 `BINARY` 压缩。第二个 `DATA` 步读取压缩的数据文件。 |
```
data retail.orders_binary(compress=binary);
   infile flat1;
   input  Customer_ID          12.
          Employee_ID          12.
          Street_ID            12.
          Order_Date           date9.
          Delivery_Date        date9.
          Order_ID             12\. 
          Order_Type           comma16.
          Product_ID           12\.     
          Quantity             4\.     
          Total_Retail_Price   dollar13.
          CostPrice_Per_Unit   dollar13.
          Discount             5\.       ;
run;

data _null_;
   set retail.orders_binary;
run;
``` |
| 3. 数值数据，字符压缩 | 下一个程序创建 SAS 数据集 `Retail.Orders_char`，它包含数值数据并使用 `CHAR` 压缩。第二个 `DATA` 步读取压缩的数据文件。 |
```
data retail.orders_char(compress=char);
   infile flat1;
   input  Customer_ID          12.
          Employee_ID          12.
          Street_ID            12.
          Order_Date           date9.
          Delivery_Date        date9.
          Order_ID             12\. 
          Order_Type           comma16.
          Product_ID           12\.     
          Quantity             4\.     
          Total_Retail_Price   dollar13.
          CostPrice_Per_Unit   dollar13.
          Discount             5\.       ; 
run;

data _null_;
   set retail.orders_char;
run;
``` |
| 4. 字符数据，无压缩 | 下一个程序创建 SAS 数据集 `Retail.Customers`，它包含字符数据且未经过压缩。第二个 `DATA` 步读取未压缩的数据文件。 |
```
data retail.customers(compress=no);
   infile flat2;
   input  Customer_Country     $40.
          Customer_Gender      $1.
          Customer_Name        $40.
          Customer_FirstName   $20\.  
          Customer_LastName    $30.
          Customer_Age_Group   $12.
          Customer_Type        $40.
          Customer_Group       $40\.    
          Customer_Address     $45\.   
          Street_Number        $8\.           ;
run;

data _null_;
   set retail.cutomers;
run;
``` |
| 5. 字符数据，二进制压缩 | 下一个程序创建 SAS 数据集 `Retail.Customers_binary`，它包含字符数据并使用 `BINARY` 压缩。第二个 `DATA` 步读取压缩的数据文件。 |
```
data retail.customers_binary(compress=binary);
   infile flat2;
   input  Customer_Country     $40.
          Customer_Gender      $1.
          Customer_Name        $40.
          Customer_FirstName   $20.
          Customer_LastName    $30.
          Customer_Age_Group   $12.
          Customer_Type        $40.
          Customer_Group       $40\.    
          Customer_Address     $45\.   
          Street_Number        $8\.           ;
run;

data _null_;
   set retail.customers_binary;
run;
``` |
| 6. 字符数据，字符压缩 | 下一个程序创建 SAS 数据集 `Retail.Customers_char`，它包含字符数据并使用 `CHAR` 压缩。第二个 `DATA` 步读取压缩的数据文件。 |
```
data retail.customers_char(compress=char);
   infile flat2;
   input  Customer_Country     $40.
          Customer_Gender      $1.
          Customer_Name        $40.
          Customer_FirstName   $20.
          Customer_LastName    $30.
          Customer_Age_Group   $12.
          Customer_Type        $40.
          Customer_Group       $40\.    
          Customer_Address     $45\.   
          Street_Number        $8\.           ;
run;

data _null_;
   set retail.customers_char;
run;
``` |




另一种节省磁盘空间的方法是将数据保留在原始位置，并使用 SAS 数据视图（SAS data view）来访问它。首先，我们检查 SAS 数据视图以及它与 SAS 数据文件的比较。

SAS 数据文件和 SAS 数据视图都是 SAS 数据集的类型。SAS 数据文件同时包含描述符信息和数据。相比之下，SAS 数据视图仅包含描述符信息以及检索存储在其他处数据的指令。

![SAS data view](img/m82-19-g1.png)

SAS 数据文件和 SAS 数据视图的主要区别在于数据存储的位置。SAS 数据文件包含数据，而 SAS 数据视图不包含数据。如果你处理经常变化的数据，数据视图会特别有用。

假设你有一个读取到 SAS 数据文件中的平面文件（flat file）。如果平面文件中的数据发生变化，你需要更新数据文件以反映这些变化。然而，假设你使用 SAS 数据视图而不是 SAS 数据文件来访问该平面文件。当平面文件中的数据发生变化时，你不需要更新 SAS 数据视图，因为每次引用该视图时，它访问的都是平面文件中的最新数据。

在大多数情况下，你可以像使用 SAS 数据文件一样使用 SAS 数据视图，尽管在使用数据视图时有几点需要注意。

**注意：** SAS 数据视图有多种类型。本章仅讨论 `DATA` 视图。要了解更多关于 `PROC SQL` 视图的信息，请参见使用 PROC SQL 创建和管理视图。有关 SAS 数据视图和 SAS 数据文件的更多信息，请参阅 SAS 文档。现在来看 `DATA` 步视图。

## DATA Step Views

`DATA` 视图包含一个部分编译的 `DATA` 步，它可以从各种源读取数据，例如：

* 原始数据文件
* SAS 数据文件
* `PROC SQL` 视图
* `SAS/ACCESS` 视图
* `DB2`、`ORACLE` 或其他 DBMS 数据

`DATA` 视图只能在 `DATA` 步中创建。`DATA` 视图不能包含全局语句、主机特定的数据集选项，或大多数主机特定的 `FILE` 和 `INFILE` 语句选项。此外，`DATA` 视图不能被索引或压缩。

你可以使用 `DATA` 视图执行以下操作：

* 始终访问变化文件中的最新数据
* 避免存储大型数据文件的副本
* 合并来自多个源的数据

编译后的 `DATA` 步不占用大量存储空间，因此你可以创建 `DATA` 视图来节省磁盘空间。另一方面，使用 `DATA` 视图可能会增加 CPU 使用，因为 SAS 在每次使用视图时都必须执行存储的 `DATA` 步。要创建 `DATA` 视图，在 `DATA` 语句中最后一个数据集名称之后指定 `VIEW=` 选项。

创建 `DATA` 视图的 `DATA` 步通用格式：

```
DATA SAS-data-view <SAS-data-file-1 ... SAS data-file-n> /VIEW=SAS-data-view;
<SAS statements>
RUN;
```

| 语法 | 描述 |
| :--- | :--- |
| `SAS-data-view` | 指定要创建的数据视图名称。 |
| `SAS-data-file-1 ... SAS-data-file-n` | 可选列表，指定要创建的任何数据文件。 |
| `SAS statements` | 包括用于创建数据视图以及 `DATA` 语句中列出的任何数据文件的其他 `DATA` 步语句。 |

`VIEW=` 选项告诉 SAS 编译但不执行源程序，并将编译后的代码存储在选项中指定的 `DATA` 视图中。

**注意：** 如果你在 `DATA` 语句中指定了额外的数据文件，SAS 在随后的 `DATA` 或 `PROC` 步处理视图时创建这些数据文件。因此，在尝试后续步骤中引用数据文件之前，你需要先引用数据视图。

## Example

以下程序创建一个名为 `Company.Newdata` 的 `DATA` 视图，该视图从 `INFILE` 语句中 `fileref` 所引的文件读取。

```
data company.newdata / view=company.newdata;
   infile <fileref>;
   <DATA step statements>
run;
```

## The DESCRIBE Statement

`DATA` 视图保留了源语句。你可以使用 `DESCRIBE` 语句检索这些语句。以下示例在 `DATA` 步中使用 `DESCRIBE` 语句，将数据视图 `Company.Newdata` 的源代码副本写入 SAS 日志：

```
data view=company.newdata;
   describe;
run;
```

## Creating and Referencing a SAS DATA Step View

为了成功使用 `DATA` 视图，你需要了解创建和引用它时会发生什么。

当你创建一个 `DATA` 视图时，会发生以下操作：

* `DATA` 步被部分编译。
* 中间代码存储在指定的 SAS 库中，成员类型为 `VIEW`。

![Company Library](img/m82-21-g1.png)

以引用数据文件的方式引用 `DATA` 视图。当你在随后的 `DATA` 或 `PROC` 步中引用视图时，会发生以下操作：

* 编译器解析中间代码并生成可执行代码。
* 当 `DATA` 或 `PROC` 步请求观测值时，执行生成的代码。

![Extended file](img/m82-21-g2.png)

你可以像使用其他数据集一样使用 `DATA` 视图，但在极少数情况下无法向视图写入数据。此外，你应该记住，SAS 数据视图每次被使用时都会从源文件读取数据。因此，如果数据发生变化，结果也会随之变化。同样，如果视图的数据结构发生变化，你可能需要修改视图以适应变化。

**注意：** `OBSBUF=` 数据集选项允许你指定从视图源数据一次读取多少观测值。视图缓冲区的默认大小为 32K，这意味着每次读取到缓冲区的观测值数量取决于观测长度。如果观测长度大于 32K，则每次只能读取一个观测值。

记住，尽管数据视图节省空间，但处理它们可能比处理数据文件消耗更多资源。查看一些使用数据视图可能不利于处理效率的情况。

### 在一个程序中多次引用数据视图

SAS 在每次引用视图时都会执行一次，即使在同一个程序内。因此，如果数据多次多次，创建一个临时 SAS 数据文件比创建和引用视图更有效。

#### Example

与其在程序中的每个步骤中引用数据视图，你可以在程序开头添加一个 `DATA` 步创建一个临时数据文件并将数据视图读取其中。然后你可以在后续的步骤中引用该数据集。通过在每个 `PROC` 步中引用临时数据文件而不是数据视图，SAS 只执行一次数据视图，而不是多次执行。

将数据提取到临时数据文件还有其他主意。假设你提交这段代码并运行需要很长时间。如果视图引用的平面文件在代码运行期间发生了变化，除非你在提交 `PROC PRINT`、`PROC FREQ` 和 `PROC MEANS` 步之前创建了 SAS 数据文件并在程序中引用它，否则结果将是不一致的。

### 在数据视图中多次遍历数据




当在使用需要对数据进行多次扫描的过程配合 SAS 数据视图（data view）时，性能可能会下降。当请求多次扫描时，视图必须构建一个包含所有生成观测值的缓存（溢出文件，spill file）。然后，SAS 在对数据的多次扫描的每一次中都会读取溢出文件中的数据，以确保后续扫描读取的是与之前扫描读取的相同数据。例如，`PRINT`语句的 `UNIFORM`选项通过确定每个变量的最长值，使所有列在页页之间保持一致。为了实现这一点，SAS 必须对数据进行两次扫描：第一次找到每个变量的最长值，第二次打印数据。如果你使用 `UNIFORM` 选项打印数据视图，SAS 在从视图中生成观测值的同时会创建一个溢出文件。然后，SAS 会对溢出文件中的观测值进行两次扫描。![溢出文件](img/m82-24-g1.png)
注意：某些统计过程会对数据进行多次扫描。

## 在不稳定的数据上创建数据视图

避免在结构经常变化的文件上创建视图。如果视图描述原始数据文件的结构，则每次文件发生变化时，你都需要更改视图。例如，假设你创建了一个视图，合并了数据文件 `Company.Roster` 和 `Company.Demog`。`Roster` 包含变量 `LastName` 和 `FirstName`，而 `Company.Demog` 包含变量 `LastName`、`Address` 和 `Age`，如下所示![Company.Roster](img/m82-24-g2.png)。假设 `Company.Roster` 和 `Company.Demog` 都按 `LastName` 排序。你可以使用 `MERGE` 语句将这两个数据文件合并为名为 `Company.Roster_View` 的视图，如下所示。

```
data company.roster_view/view=company.roster_view;
   merge company.roster company.demog;
   by lastname;
run;
```

现在假设 `Company.Roster` 发生了变化，将 `LastName` 改名为 `Surname`。你的数据视图也必须更新。![Company.Roster](img/m82-24-g3.png)

```
data roster_view/view=roster_view;
   merge company.roster company.demog(rename=(LastName=Surname));
   by lastname;
run;
```

如果 `Company.Roster` 再次变化，将 `Surname` 和 `FirstName` 合并为一个名为 `FullName` 的变量，那么你的数据视图代码将需要额外的更改。虽然这是一个简单的示例，但你可以看到，基于不稳定数据的数据视图需要额外的维护工作。

## 比较示例：创建和读取 SAS 数据视图

## 概述

假设你有两个从同一个原始数据文件创建的 SAS 数据集：`Retail.Custview` 和 `Retail.Custdata`。`Retail.Custview` 是 `DATA` 步视图，而 `Retail.Custdata` 是数据文件。你可以使用这两个数据集来比较它们所需的磁盘空间，以及从每个视图或文件读取数据时所使用的资源。以下示例程序比较了两种技术。你可以将这些示例作为模型，在你自己的环境中创建基准程序。你的结果可能会根据数据结构、操作环境以及你所在位置的可用资源而异。

### 编程技术

| ![1](img/callout01.png) 数据视图 | 此程序从原始数据文件读取数据，创建一个名为 `Retail.Custview` 的 SAS `DATA` 步视图，然后从新的 `DATA` 步视图读取。第一个 `DATA` 步创建数据视图 `Retail.Custview`。第二个 `DATA` 步从该 `DATA` 步视图读取。 |

```
data retail.custview / view = retail.custview;
   infile flat1;
   input @1   Customer_ID         12.
         @13  Country             $2.
         @15  Gender              $1.
         @16  Personal_ID        $15.
         @31  Customer_Name      $40.
         @71  Customer_FirstName $20.
         @91  Customer_LastName  $30.
         @121 Birth_Date       date9.
         @130 Customer_Address   $45.
         @175 Street_ID           12.
         @199 Street_Number       $8.
         @207 Customer_Type_ID     8.;
 run;

data _null_;
   set retail.custview;
run;
```

| ![2](img/callout02.png) 数据文件 | 此程序从原始数据文件读取数据，创建一个名为 `Retail.Custdata` 的 SAS 数据文件，并从新的 SAS 数据文件读取。第一个 `DATA` 步创建数据文件 `Retail.Custdata`。第二个 `DATA` 步从该数据文件读取。 |

```
data retail.custdata;
   infile flat1;
   input @1   Customer_ID         12.
         @13  Country             $2.
         @15  Gender              $1.
         @16  Personal_ID        $15.
         @31  Customer_Name      $40\. 
         @71  Customer_FirstName $20.
         @91  Customer_LastName  $30.
         @121 Birth_Date       date9.
         @130 Customer_Address   $45.
         @175 Street_ID           12.
         @199 Street_Number       $8.
         @207 Customer_Type_ID     8.;
run;

data _null_;
   set retail.custdata;
run;
```

## 通用建议

-   创建数据视图以避免存储数据的副本。
-   如果文件结构是动态的，请使用数据视图。
-   创建数据视图合并多个数据集。
-   创建数据视图访问频繁使用的子集。

## 总结

## 减少字符变量的空间

SAS 以每个字节一个字符存储数据。你可以使用 `LENGTH` 语句减少字符变量的长度。你还可以使用其他技术来减少字符数据空间。

## 减少数值变量的空间

SAS 以浮点表示存储数值数据。数值变量的默认长度为 8 字节。你可以使用 `LENGTH`语句减少数值变量的长度。与读取全长度数值变量相比，读取短长度数值变量需要更少的 I/O 但更多的 CPU 资源。你可以使用 `PROC COMPARE` 查看精度损失。

## 压缩数据文件

默认情况下，SAS 数据文件是不压缩的。你可以压缩数据文件以节省空间，尽管某些文件不是良好的压缩对象。使用 `COMPRESS=` 数据选项或系统选项压缩数据文件。使用 `POINBS=YES` 数据选项允许 SAS 直接访问压缩文件而非顺序访问。使用 `REUSE=YES` 数据选项或系统选项指定 SAS 在添加或更新观测值时重用压缩文件的空间。

## 使用 SAS DATA 视图节省存储

你可以将数据保留在原始存储位置，并使用 SAS 数据视图访问数据以减少磁盘所需的空间。DATA 视图是在 `DATA` 步中使用 `VIEW=` 选项创建的特定类型视图。使用 `DESCRIBE` 语句将数据视图的代码写入 SAS 日志。使用 DATA 视图而不是数据文件的优点之一是它们始终访问动态文件的最新数据，并且所需的磁盘空间较少。然而，这对性能可能会影响

# 测试

为每个问题选择最佳答案。完成测试后，使用附录中的答案检查你的答案。

1.  关于未压缩 SAS 数据文件，以下哪个是正确的？
    1. 描述部分存储在任何足够的空间的页面上。
    2. 新观测值总是添加到第一个足够的可用空间。
    3. 已删除的观测值空间会被跟踪。
    4. 新观测值总是添加到数据集的末尾。

2.  关于压缩 SAS 数据文件，以下哪个是正确的？





1. 描述符部分存储在任何具有足够空间的数据页上。
2. 已删除的观测空间可以被重用。
3. 压缩的 SAS 数据文件比未压缩的 SAS 数据具有更小的开销。
4. 在压缩的 SAS 数据集中，每个观测值的大小必须相同。

3. 下面哪个程序正确地创建了长度减少的数值型变量？
1. ```sas
data temp;
   infile file1;
   input x 4.
         y 3.
         z 2.;
 run;
```
2. ```sas
data temp;
   format x 4.
          y 3.
          z 2.;
   infile file1;
   input x 4.
         y 3.
         z 2.;
run;
```
3. ```sas
data temp;
   length x 4
          y 3
          z 2;
   infile file1;
   input x 4.
         y 3.
         z 2.;
 run;
```
4. ```sas
data temp;
   informat x 4.
            y 3.
            z 2.;
   infile file1;
   input x 4.
         y 3.
         z 2.;
run;
```

4. 关于 SAS 数据视图（data views）的以下陈述哪个是正确的？
1. SAS 数据视图比 SAS 数据文件占用更磁盘空间，但消耗更多 CPU 资源。
2. SAS 数据视图只能在永久性 SAS 库中创建。
3. SAS 数据视图比 SAS 数据文件消耗更 CPU 资源，但占用更多的磁盘空间。
4. SAS 数据视图只能在临时 SAS 库中创建。

5. 你应该使用以下哪个程序来检测 `Company.Regular` 中默认长度数值型变量与数据集 `Company.Reduced` 中长度减少的数值型变量之间是否存在精度损失？
1. ```sas
proc contents data=company.regular;
   compare data=company.reduced;
run;
```
2. ```sas
proc compare base=company.regular
   compare=company.reduced;
run;
```
3. ```sas
proc print data=company.regular;
run;

proc print data=company.reduced;
run;
```
4. ```sas
proc datasets library=company;
   contents data=regular compare=reduced;
run;
```

# 第 22 章：使用最佳实践

## 概述

## 引言
本章演示了如何使用 SAS 最佳编程实践来优化性能。在比较本章描述的技术时，请记住，资源使用的差异受你所工作的操作环境以及数据特征的影响。每个主题都包含了可以提高程序效率的示例。编写程序来生成你自己的基准测试，并采用能为你节省最多开的编程技术。注意：本章不涵盖 SAS 可扩展性能数据引擎（SAS SPD Engine），这是一种用于线程处理的 SAS 9.1 技术。关于使用 SAS SPD Engine 提高性能的详情，请参阅 SAS 文档。

# 执行必要的语句

## 概述
当以最有效的顺序执行最少量的语句时，你可以减少 SAS 使用的硬件资源。受影响的资源包括磁盘占用、内存使用和 CPU 使用。这里有两个需要记住的技巧：
* 在逻辑允许的情况下对数据进行子集划分。
* 使用最合适的技术根据条件条件处理你的数据。

## 子集划分 IF 语句的位置
为了根据新派生或计算的变量对数据进行子集划分，请在 `DATA` 步中使用子集 IF 语句，以便仅处理符合特定条件的观测值。子集 IF 语句会导致 `DATA` 步继续处理满足该语句中指定的表达式条件的观测值。生成的 SAS 数据集或数据集包含原始外部文件或 SAS 数据集的子集。将子集 IF 语句放置在程序中，使其在逻辑允许的情况下尽快检查子集条件。结果是不必要的语句将不会执行。当子集条件为假时，该观测值将不再处理后续语句。此外，请记住在执行计算之前对数据进行子集划分，并尽量减少函数调用或算术运算符的使用。对不需要的观测值进行不必要的处理会导致硬件资源的消耗。

## 比较示例：创建数据子集

## 概述
假设你想通过读取 SAS 数据 `Retail.Order_fact` 创建数据子集，计算六个新变量并根据条件输出数据。输出数据集应包含以下内容的新变量：
* 订单月份
* 订单日期与交付日期之间的时间
* 基于零售价、折扣和单价的利润
* 总利润
* 总折扣
* 总等待时间
仅包含 12 月订单的数据子集约占数据的 10%。你可以通过子集 IF 语句完成此任务。该语句在 `DATA` 步中的位置会影响 `DATA` 步在 CPU 时间和实时方面的效率。以下示例程序比较了两种技术。你可以将这些示例作为模型在你自己的环境中创建基准测试程序。你的结果可能会根据数据结构、操作环境以及你所在地的可用资源而异。

### 编程技术

#### 底部的子集 IF 语句
该程序在子集 IF 语句选择 `Month` 值为 12 的观测值之前，计算了六个新变量。

```sas
data profit;
   retain TotalProfit TotalDiscount TotalWait Count 0;    
   set retail.order_fact;
   MonthOfOrder=month(order_date);
   WaitTime=sum(delivery_date,-order_date);
   if discount gt . then
      CalcProfit=sum((total_retail_price*discount),-costprice_per_unit)
                 *quantity;
   else CalcProfit=sum(total_retail_price,-costprice_per_unit)
                 *quantity;
   TotalProfit=sum(totalprofit,calcprofit);
   TotalDiscount=sum(totaldiscount,discount);
   TotalWait=sum(totalwait,waittime);
   Count+1;    
   if monthoforder=12;
run;
```

#### 顶部的子集 IF 语句
在该程序中，子集 IF 语句位于计算出 `MonthofOrder` 值之后之后。如果该值不是 12，则对该观测值不再处理后续语句。在该程序中，计算在较少的观测值上进行，从而产生了更高的程序效率。





```
data profit;
   retain TotalProfit TotalDiscount TotalWait Count 0;  
   set retail.order_fact;
   MonthOfOrder=month(order_date);
   if monthoforder=12;
   WaitTime=sum(delivery_date,-order_date);
   if discount gt . then
      CalcProfit=sum((total_retail_price*discount),-costprice_per_unit)
                 *quantity;
   else CalcProfit=sum(total_retail_price,-costprice_per_unit)
                 *quantity;
   TotalProfit=sum(totalprofit,calcprofit);
   TotalDiscount=sum(totaldiscount,discount);
   TotalWait=sum(totalwait,waittime);
   Count+1;
run;
```

|

## 高效使用条件逻辑

你可以使用条件逻辑来改变 SAS 处理可选观测的方式。两种技术——`IF-THEN/ELSE` 语句和 `SELECT` 语句可以交叉使用且性能相当。根据你的数据特征并取决于你的环境，其中一种技术可能会为你提供更好的性能。选择一种能够节省你编程时间并使程序最易读的技术。注意：测试的条件数量以及测试的变量类型会影响 CPU 资源。为了最佳实践，请遵循以下指南编写高效的 `IF/THEN` 或 `SELECT` 语句逻辑：

*   在使用 `IF/THEN` 语句处理互斥条件时，除第一个条件外的所有条件请使用 `ELSE IF` 语句而非 `IF` 语句。
*   首先检查频率最高的条件，并按频率降序继续检查条件。
*   当你根据条件执行多个语句时，将这些语句放在 `DO` 组中。

在编写条件逻辑之前，确定你的数据值的分布。你可以使用以下过程：

*   `FREQ` 过程检查数据值的分布
*   `GCHART` 或 `GPLOT` 过程以图形形式显示分布
*   `UNIVARIATE` 过程检查分布统计并以图形形式显示信息

## 对比示例：使用 DO 组条件地创建变量

## 概述

假设你想根据数据集 `Retail.Order_fact` 中变量 `Order_Type` 的值来计算调整后的利润。对于值为 1 的零售销售，调整后的利润应计算为利润的 105%。对于值为 2 的目录销售，调整后的利润应计算为利润的 103%。对于值为 3 的互联网销售，调整后的利润应等于利润。下表显示变量 `Order_Type` 的值并非均匀分布。![使用 DO 组条件地创建变量](img/m83-7-g1.png) 下表显示变量 `Discount` 的值也不是均匀分布。![使用 DO 组条件地创建变量](img/m83-7-g2.png) 以下示例程序比较了两种技术。你可以将这些示例作为模型，在你自己的环境中创建基准程序。你的结果可能会根据你的数据结构、操作系统环境以及你所在地的资源而有所不同。

### 编程技术

| ![1](img/callout01.png) IF-THEN/ELSE 语句此程序使用 `IF-THEN/ELSE` 语句结合 `DO` 组，有条件地执行多个计算调整后利润的语句。条件按频率降序检查。 

```
data retail.order_info_1;
   set retail.order_fact;
   if order_type=1 then 
      do;                     /* 零售销售 */
         Float=delivery_date-order_date;
         RevenueQuarter=qtr(order_date);
         AveragePrice=total_retail_price/quantity;
         if discount=. then NetPrice=total_retail_price;
         else NetPrice=total_retail_price-discount;
         Profit=netPrice-(quantity*costprice_per_unit)*1.05;
      end;
   else if order_type=2 then
      do;                    /* 目录销售 */
         Float=delivery_date-order_date;
         RevenueQuarter=qtr(order_date);
         AveragePrice=total_retail_price/quantity;
         if discount=. then NetPrice=total_retail_price;
         else NetPrice=total_retail_price-discount;
         Profit=netprice-(quantity*costprice_per_unit)*1.03;
      end;
   else 
      do;                    /* 互联网销售 */
         Float=delivery_date-order_Date;
         RevenueQuarter=qtr(order_date);
         AveragePrice=total_retail_price/quantity;
         if discount=. then NetPrice=total_retail_price;
         else NetPrice=total_retail_price-discount;
         Profit=netprice-(quantity*costprice_per_unit);
      end;
run;
```

 |

| ![2](img/callout02.png) SELECT 语句此程序使用 `SELECT` 和 `WHEN` 语句结合 `DO` 组，有条件地执行多个计算调整后利润的语句。条件按频率降序检查。 

```
data retail.order_info_2;
   set retail.order_fact;
   select(order_type);
      when (1)
          do;                                    /* 零售销售 */
            Float=delivery_date-order_date;
            RevenueQuarter=qtr(order_date);
            AveragePrice=total_retail_price/quantity;
            if discount=. then NetPrice=total_retail_price;
            else NetPrice=total_retail_price-discount;
            Profit=netprice-(quantity*costprice_per_unit)*1.05;
         end;
      when (2)
          do;                                   /* 目录销售 */
            Float=delivery_date-order_date;
            RevenueQuarter=qtr(order_date);
            AveragePrice=total_retail_price/quantity;
            if discount=. then NetPrice=total_retail_price;
            else NetPrice=total_retail_price-discount;
            Profit=netprice-(quantity*costprice_per_unit)*1.03;
         end;
      otherwise
         do;                                  /* 互联网销售 */
            Float=delivery_date-order_date;
            RevenueQuarter=qtr(order_date);
            AveragePrice=total_retail_price/quantity;
            if discount=. then NetPrice=total_retail_price;
            else NetPrice=total_retail_price-discount;
            Profit=netprice-(quantity*costprice_per_unit);
         end;
   end;
run;
```

## 通用建议

*   无论使用 `IF-THEN/ELSE` 还是 `SELECT` 和 `WHEN` 语句，首先检查频率最高的条件，并按频率降序继续检查条件。
*   当你根据条件执行多个语句时，将这些语句放在 `DO` 组中。

## 对比示例：调用函数条件地创建变量

## 概述

假设你想创建一个报告，其中包含一个基于 SAS 数据集 `Retail.Order_fact` 中现有变量的新变量。新 `Month` 变量的值是通过使用 `MONTH` 函数从现有变量 `Order_Date` 中提取的。下表显示 `Month` 的值分布均匀。![调用函数条件地创建变量](img/m83-9-g1.png)





```
data retail.orders;
   set retail.order_fact;
   if month(order_date)=1 then Month='Jan';
   if month(order_date)=2 then Month='Feb';
   if month(order_date)=3 then Month='Mar';
   if month(order_date)=6 then Month='Jun';
   if month(order_date)=7 then Month='Jul';
   if month(order_date)=8 then Month='Aug';
   if month(order_date)=9 then Month='Sep';
   if month(order_date)=10 then Month='Oct';
   if month(order_date)=11 then Month='Nov';
   if month(order_date)=12 then Month='Dec';
run;
```

|

| ![2](img/callout02.png) ELSE IF 语句，多次函数引用此程序使用了调用 `MONTH()` 函数的 `ELSE IF` 语句。一旦找到真条件，后续的 `ELSE IF` 语句将不再执行。这比使用并行的 `IF` 语句效率更高，但 `MONTH()` 函数被执行了多次。 |

```
data retail.orders;
   set retail.order_fact;
   if month(order_date)=1 then Month='Jan';
   else if month(order_date)=2 then Month='Feb';
   else if month(order_date)=3 then Month='Mar';
   else if month(order_date)=4 then Month='Apr';
   else if month(order_date)=5 then Month='May';
   else if month(order_date)=6 then Month='Jun';
   else if month(order_date)=7 then Month='Jul';
   else if month(order_date)=10 then Month='Oct';
   else if month(order_date)=11 then Month='Nov';
   else if month(order_date)=12 then Month='Dec';
run;
```

 |

| ![3](img/callout03.png) ELSE IF 语句，单次函数引用此程序使用 `MONTH()` 函数查找 `Order_Date` 的值，但只调用一次。`MONTH()` 函数在读取数据集后、在任何 `IF-THEN/ELSE` 语句执行之前立即调用。这种做法是高效的。 |

```
data retail.orders(drop=mon);
   set retail.order_fact;
   mon=month(order_date);
   if mon=1 then Month='Jan';
   else if mon=2 then Month='Feb';
   else if mon=3 then Month='Mar';
   else if mon=4 then Month='Apr';
   else if mon=5 then Month='May';
   else if mon=6 then Month='Jun';
   else if mon=7 then Month='Jul';
   else if mon=8 then Month='Aug';
   else if mon=9 then Month='Sep';
   else if mon=10 then Month='Oct';
   else if mon=11 then Month='Nov';
   else if mon=12 then Month='Dec';
run;
```

 |

| ![4](img/callout04.png) SELECT 分组在此程序中，`SELECT` 语句在 `WHEN` 语句执行并为 `Month` 赋值之前，仅调用了一次 `MONTH()` 函数。这种做法是高效的。 |

```
data retail.orders;
   set retail.order_fact;
   select(month(order_date));
      when (1) Month='Jan';
      when (2) Month='Feb';
      when (3) Month='Mar';
      when (4) Month='Apr';
      when (5) Month='May';
      when (6) Month='Jun';
      when (7) Month='Jul';
      when (8) Month='Aug';
      when (11) Month='Nov';
      when (12) Month='Dec';
      otherwise;
   end;
run;
```

 |

### 一般建议

- 避免使用并行的 `IF` 语句，这种方式消耗资源最多，是条件执行语句效率最低的方法。
- 使用 `IF-THEN/ELSE` 语句和 `SELECT` 块来提高效率。
- 为了显著减少资源消耗，请编写只调用一次函数的程序，而不是在许多语句中重复使用同一个函数。SAS 函数虽然方便，但在 CPU 资源方面可能代价昂贵。

## 高效使用 DO 组

你可以通过将必要的语句放在与 `IF-THEN/ELSE` 语句或 `SELECT/WHEN` 语句相关的 `DO` 组中，从而根据条件执行必要的语句。语句组仅在特定条件为真时执行。在使用 `IF-THEN/ELSE` 语句配合 `DO` 组时，在 `THEN` 子句之后添加 `DO`，并在所有想要分组执行的语句之后添加 `END` 语句。

```
data orders;
   set company.orders;
   if order_type = 1 then 
      do;
      <此处有多个可执行语句>
      end;
   else if order_type = 2 then 
      do;
      <此处有多个可执行语句>
       end;
   else if order_type = 3 then 
       do;
       <此处有多个可执行语句>
       end;
run;
```

注意：根据条件创建多个变量时，请使用 `IF-THEN DO` 组。在使用带有 `SELECT/WHEN` 语句的 `DO` 组时，在 `WHEN` 条件之后添加 `DO`，并在所有想要执行的语句之后添加 `END` 语句。使用 `OTHERWISE` 语句来指定未满足任何 `WHEN` 条件时执行的语句。

```
data orders;
   set company.orders;
   select(order_type)
      when (1) 
         do;
         end;
      when (2) 
         do;
         end;
      when (3) 
         do;
         end;
      otherwise;
   end;
run;
```
记住 `IF-THEN/ELSE` 和 `SELECT/WHEN` 需要对应的语句。

## 比较示例：使用 DO 组创建数据

## 概述

假设你想根据数据集识别哪些客户组是 `Club Members`、`Club Gold Members` 或 `Internet/Catalog`。你还想根据活动性质识别 `inactive`、`low activity`、`medium activity` 或 `high activity`。![创建数据](img/m8-12-g1) 以下示例比较了不同的技术。你可以将这些示例作为你自己环境的参考。

### 编程技术

| ![1](img/callout01.png) 并行 IF 语句此程序通过读取 `Customer_hybrid` 数据集创建一个名为 `Retail.Customers` 的永久 SAS 数据集。串行 `IF` 语句用于填充 `Customer_Group` 和 `Customer_Activity` 变量。 |

```
data retail.customers;
   length Customer_Group $26 Customer_Activity $15;
   set retail.customer_hybrid;
   if substr(put(customer_type_ID,4),1,2)='10' then
      customer_group='Orion Club members';
   if substr(put(customer_type_ID,4),1,2)='20' then
      customer_group='Orion Club Gold members';
   if substr(put(customer_type_ID,4),1,2)='30' then
      customer_group='Internet/Catalog Customers';
   if substr(put(customer_type_ID,4),1,2) in ('10', '20') and
      substr(put(customer_type_ID,4),3,2)='10' then
         customer_activity='inactive';
   if substr(put(customer_type_ID,4),1,2) in ('10', '20') and
      substr(put(customer_type_ID,4),3,2)='20' then
         customer_activity='low activity';
   if substr(put(customer_type_ID,4),1,2) in ('10', '20') and
      substr(put(customer_type_ID,4),3,2)='30' then
         customer_activity='medium activity';
   if substr(put(customer_type_ID,4),1,2) in ('10', '20') and
      substr(put(customer_type_ID,4),3,2)='40' then
         customer_activity='high activity';
run;
```

 |

| ![2](img/callout02.png) SELECT, IF/SELECT 语句此程序通过读取 `Customer_hybrid` 数据集创建一个名为 `Retail.Customers` 的永久 SAS 数据集。`SELECT/WHEN` 逻辑和 `IF/THEN DO` 组中的 `SELECT/WHEN` 语句用于填充 `Customer_Group` 和 `Customer_Activity` 变量。如果 `Customer_Type_ID` 的前两位是 `10`、`20` 或 `30`，则填充 `Customer_Group`。如果 `Customer_Type_ID` 的前两位是 `10` 或 `20`，则通过读取 `Customer_Type_ID` 的后两位来填充 `Customer_Activity`。 |




```
data retail.customers;
   length Customer_Group $ 26 Customer_Activity $ 15;
   set retail.customer_hybrid;
      select(substr(put(customer_type_ID,4.),1,2));
         when ('10') customer_group='Orion Club members';
         when ('20') customer_group='Orion Club Gold members';
         when ('30') customer_group='Internet/Catalog Customers';
         otherwise;
      end;
   if substr(put(customer_type_ID,4.),1,2) in ('10', '20') then
      do;
         select(substr(put(customer_type_ID,4.),3,2));
            when ('10') customer_activity='inactive';
            when ('20') customer_activity='low activity';
            when ('30') customer_activity='medium activity';
            when ('40') customer_activity='high activity';
            otherwise;
         end;
      end;
run;
```

## 嵌套 SELECT 语句
该程序通过读取 `Retail.Customer_hybrid` 数据集创建一个名为 `Retail.Customers` 的永久 SAS 数据集。嵌套的 `SELECT` 语句用于填充 `Customer_Group` 和 `Customer_Activity` 变量。

```sas
data retail.customers;
   length Customer_Group $ 26 Customer_Activity $ 15;
   set retail.customer_hybrid;
   select(substr(put(customer_type_ID,4.),1,2));
      when ('10')
         do;
            customer_group='Orion Club members';
            select(substr(put(customer_type_ID,4.),3,2));
               when ('10') customer_activity='inactive';
               when ('20') customer_activity='low activity';
               when ('30') customer_activity='medium activity';
               when ('40') customer_activity='high activity';
               otherwise;
            end;
         end;
      when ('20')
         do;
            customer_group='Orion Club Gold members';
            select(substr(put(customer_type_ID,4.),3,2));
               when ('10') customer_activity='inactive';
               when ('20') customer_activity='low activity';
               when ('30') customer_activity='medium activity';
               when ('40') customer_activity='high activity';
               otherwise;
            end;
         end;
      when ('30') customer_group='Internet/Catalog Customers';
      otherwise;
   end;
run;
```

## 带有链接的 IF-THEN/ELSE IF 语句
该程序通过读取 `Retail.Customer_hybrid` 数据集创建一个名为 `Retail.Customers` 的永久 SAS 数据集。使用带有链接的 `IF-THEN/ELSE IF` 语句填充 `Customer_Group` 和 `Customer_Activity` 变量。

```sas
data retail.customers;
   length Customer_Group $ 26 Customer_Activity $ 15;
   set retail.customer_hybrid;
   if substr(put(customer_type_ID,4.),1,2)='10' then
      do;
         customer_group='Orion Club members';
         link activity;
      end;
   else if substr(put(customer_type_ID,4.),1,2)='20' then
      do;
         customer_group='Orion Club Gold members';
         link activity;
      end;
   else if substr(put(customer_type_ID,4.),1,2)='30' then
      customer_group='Internet/Catalog Customers';
   return;
   activity:
   if substr(put(customer_type_ID,4.),3,2)='10' then
      customer_activity='inactive';
   else if substr(put(customer_type_ID,4.),3,2)='20' then
      customer_activity='low activity';
   else if substr(put(customer_type_ID,4.),3,2)='30' then
      customer_activity='medium activity';
   else if substr(put(customer_type_ID,4.),3,2)='40' then
      customer_activity='high activity';
   return;
run;
```

### 一般建议
- 避免并行的 `IF` 语句，因为它们会消耗额外的资源。

# 消除不必要的数据扫描
最佳实践规定，你应该消除不必要的数据扫描。为了最大限地减少 I/O 操作和 CPU 时间，请避免比必要的多次读取或写入数据。

## 比较示例：创建 SAS 数据集的多个子集

## 概述
假设你想从 `Retail.Customer` 数据集中创建五个子集。你需要为五个国家中的每个国家创建一个子集。以下示例程序比较了两种技术。你可以将这些示例作为在你自己的环境中创建基准程序的模型。你的结果可能会取决于数据结构、操作系统环境以及你所在地的可用资源。

### 编程技术

#### 1. 多个 DATA 步
该程序包含多个 `DATA` 步，并随后从同一个 `Retail.Customer` 数据集中读取了五次数据。各个子集 `IF` 语句出现在五个独立的 `DATA` 步中。

```sas
data retail.UnitedStates;
   set retail.customer;
   if country='US';
run;

data retail.France;
   set retail.customer;
   if country='FR';
run;

data retail.Italy;
   set retail.customer;
   if country='IT';
run;

data retail.Germany;
   set retail.customer;
   if country='DE';
run;

data retail.Spain;
   set retail.customer;
   if country='ES';
run;
```

#### 2. 单独 DATA 步
该程序使用单个 `DATA` 步创建五个输出。`Retail.Customer` 数据集仅读取了一次。使用 `IF-THEN/ELSE` 语句输出到特定的数据集。

```sas
data retail.UnitedStates 
     retail.France 
     retail.Italy 
     retail.Germany 
     retail.Spain;
   set retail.customer;
   if country='US' then output retail.UnitedStates;
   else if country='FR' then output retail.France;
   else if country='IT' then output retail.Italy;
   else if country='DE' then output retail.Germany;
   else if country='ES' then output retail.Spain;
run;
```

#### 3. 使用 WHERE 语句的 SORT 过程
良好的编程习惯是利用 `SORT` 过程在同一个步骤中进行排序和筛选的能力。这比使用两个独立的步骤（一个 `DATA` 步后接一个 `procedure` 步）更高效。

```sas
proc sort data=retail.customer out=retail.CountrySubset;
   by country;
   where country in('US','FR','IT','DE','ES');
run;
```

### 一般建议
当从数据集创建多个子集时，使用带有 `IF-THEN/ELSE` 逻辑的单个 `DATA` 步输出到适当的数据集。




*   当你需要用过程处理数据的子集时，请在过程中使用 `WHERE` 语句，而不是创建一个数据的子集后再用过程读取该数据。
*   编写一个既能排序又提取子集的程序步骤。这种方法比编写两个单独的提取子集和排序的程序步骤更节省程序员的时间和调试时间。

## 使用 DATASETS 过程修改变量属性

使用 `PROC DATASETS` 代替 `DATA` 步来修改数据属性。`PROC DATASETS` 过程比 `DATA` 步消耗的资源更少，因为它只处理数据集的描述符部分，而不处理数据部分。`PROC DATASETS` 会保留排序标记以及索引。注意：你无法使用 `DATASETS` 过程来修改变量的类型、长度或位置，因为这些属性会直接影响数据集的数据部分。要执行这些操作，请使用 `DATA` 步。

## 比较示例：更改 SAS 数据集的变量属性

## 概述

假设你想更改 `Retail.NewCustomer` 中的变量属性，使其使其与 `Retail.Customer` 数据集中的属性保持一致。`Retail.NewCustomer` 数据集包含 89954 条观测值和 12 个变量。下表显示了每个 SAS 数据集的变量名和格式。

| SAS 数据集 | 变量名 | 变量格式 |
| --- | --- | --- |
| `Retail.Customer` | `Country` | `$COUNTRY.` |
| `Retail.Customer` | `Birth_Date` | `DATE9.` |
| `Retail.NewCustomer` | `Country_ID` | `$COUNTRY.` |
| `Retail.NewCustomer` | `Birth_Date` | `MMDDYYP10` |

以下示例程序比较了两技术。你可以将这些示例作为在你自己的环境中创建基准程序的模型。你的结果可能会取决于数据的结构、操作系统环境以及你所在地可用的资源。

### 编程技术

| ![1](img/callout01.png) 一个 DATA 步 此程序使用带有 `RENAME` 语句和 `FORMAT` 语句的 `DATA` 步来修改变量 `Country_ID` 和 `Birth_Date` 的属性。 |

```
data retail.newcustomer;
   set retail.newcustomer;
   rename Country_ID=country;
   format birth_date date9.;
run;
```

| ![2](img/callout02.png) PROC DATASETS 此程序使用 `PROC DATASETS` 修改变量 `Country_ID` 和 `Birth_Date` 的名称和格式。 |

```
proc datasets lib=retail nolist;
   modify newcustomer;
   rename Country_ID=country;
   format birth_date date9.;
quit;
```

### 一般建议

*   为了节省大量资源，请使用带有 `NOLIST` 选项的 `DATASETS` 过程代替 `DATA` 步来更改 SAS 数据集的属性。

## 只读写必要数据

## 概述

最佳实践规定，你应该编写只读取和写入必要数据的程序。如果你处理更少的观测值和变量，就能节省资源。本主题涵盖了许多提高性能的各种技术。

## 使用子集 IF 代替 WHERE 语句选择观测值

你可以使用 `WHERE` 语句或子集 `IF` 语句来提取子集。虽然这两个语句都会测试条件以确定 SAS 是否应该选择观测值，但 `WHERE` 语句效率更高。下面的图说明了这些语句之间的区别。![使用子集 IF 代替 WHERE 语句选择观测值](img/m83-22-g1.png) I/O 操作是根据数据在包含输入 SAS 数据的磁盘与内存中的输入缓冲区之间移动，以及数据从输出缓冲区移动到包含输出数据集的磁盘来衡量的。输入数据不受 `WHERE` 语句或子集 `IF` 语句的影响。然而，输出数据受两者的影响。当数据必须在程序数据向量中处理时，会测量 CPU 时间。如果处理更少的观测值，就可以节省 CPU 时间。`WHERE` 语句和子集 `IF` 语句对程序数据向量的使用方式不同。`WHERE` 语句在观测值加载到程序数据向量之前进行选择，这节省了 CPU 操作。子集 `IF` 语句将每个观测值顺序加载到程序数据向量中。如果子集条件为真，则处理该观测值并将其写入输出页面缓冲区。`WHERE` 语句作用于现有 SAS 数据集中的现有变量。子集 `IF` 语句可以作用于程序数据向量中的任何变量，包括新变量或现有变量。

## 比较示例：创建 SAS 数据集的子集

## 概述

假设你想创建 `Retail.Customer` 数据集的子集。你只想包含英国的数据。该子集包含 `Retail.Customer` 约 6% 的。以下示例程序比较了两技术。你可以将这些示例作为在你自己的环境中创建基准程序的模型。你的结果可能会取决于数据的结构、操作系统环境以及你所在地可用的资源。

### 编程技术

| ![1](img/callout01.png) 子集 IF 语句 此程序使用 `IF` 语句在 `Country` 值为 `GB` 时选择观测值。 |

```
data retail.UnitedKingdom;
   set retail.customer;
   if country='GB';
run;
```

| ![2](img/callout02.png) WHERE 语句 此程序使用 `WHERE` 语句在 `Country` 值为 `GB` 时选择观测值。这比使用子集 `IF` 语句更高效。 |

```
data retail.UnitedKingdom;
   set retail.customer;
   where country='GB';
run;
```

### 一般建议

*   当子集较小时，请使用 `WHERE` 语句代替子集 `IF` 语句来提取 SAS 数据集。

## IF 和 WHERE 语句的其他区别

查看下表注意 `IF` 语句和 `WHERE` 语句的其他区别。

| 操作 | 子集 IF 语句 | WHERE 语句 |
| --- | --- | --- |
| 选择数据 | 可以从外部文件选择记录、从 SAS 数据集选择观测值、通过 `INPUT` 语句创建观测值或根据计算或派生变量选择 | 只能从 SAS 数据集选择观测值 |
| 条件执行 | 是执行语句 | 不是执行语句 |
| 使用 BY 语句分组 | 对 `FIRST.` 或 `LAST.` 标记没有影响 | 影响 `FIRST.` 或 `LAST.` 标记，这些标记在处理表达式后设置 |
| 合并数据 | 在合并当前观测值后选择 | 在合并观测值之前对每个输入数据集应用选择 |

注意：如果你在同一个 `DATA` 步中使用了 `WHERE=` 数据选项和 `WHERE` 语句，SAS 会忽略输入数据集的 `WHERE` 语句。`WHERE=` 数据选项和 `WHERE` 语句调用相同的 SAS 程。

##  OBS= 和 FIRSTOBS= 使用 WHERE 语句

另一种只读写必要数据的方法是处理子集的片段。你通过结合 `WHERE` 表达式和 `OBS=` 以及 `FIRSTOBS=` 数据选项来完成这项任务。在下面的示例中，`WHERE` 表达式在应用 `OBS=` 和 `FIRSTOBS=` 之前选择。`OBS=` 和 `FIRSTOBS=` 指定的值是子集中的逻辑观测值，而不是数据集中的物理观测值。

| |

```
options fmtsearch=(formats);

proc print 
     data=company.organization_dim(firstobs=5 obs=8);
     var employee_id employee_gender salary;
     where salary>40000;
run;
``` |





`FIRSTOBS = 5` 是子集中第 5 个观测值，而它是数据集中第 101 个观测值；`Company.Organization.OBS = 8` 是子集中第 8 个观测值，而它是数据集中第 159 个观测值。

## 从外部文件读取数据时选择观测值

在 `DATA` 步中放置子集 `IF` 语句，使其在读取所有数据之前，仅读取选择子集所必需的变量，可以减少处理数据所需的开销。接下来的图表展示了数据如何从外部文件读取、加载到输入缓冲区，并读取到程序数据向量（PDV）中![](img/m83-28-g1.png)。请记住，I/O 操作是通过数据在磁盘和缓冲区之间的移动来衡量的——对于输入和输出数据。每条记录在移动到程序数据向量进行处理之前，都会加载到输入缓冲区，因此 I/O 不受 `DATA` 步中子集 `IF` 语句位置的影响。你可以通过限制读取到程序数据向量的内容，来减少处理数据所需的 CPU 资源。将子集 `IF` 语句放置在 `INPUT` 语句之后，该 `INPUT` 语句仅读取检查特定条件所需的数据。对于不需要的观测值，后续语句将不会执行。注意：将原始字符字段转换为 SAS 字符变量所需的 CPU 时间比将原始数值字段转换为 SAS 数值变量的实际二进制编码所需的少。

## 比较示例：通过从外部文件读取数据创建数据子集

## 概述

假设你想通过从由文件引用 `Customerdata` 引用的外部文件中读取数据子集，来创建一个 SAS 数据集。你希望该子集仅包含英国的客户。该子集约占外部文件中国家数的 6%，该文件包含 89,954 条记录和 12 个字段。以下几个示例程序比较了两种技术。你可以将这些示例作为模型，在你自己的环境中创建基准程序。你的结果可能会根据数据结构、你的操作系统环境以及你所在地的可用资源而异。

### 编程技术

| ![1](img/callout01.png) 读取所有变量并进行子集化在此程序中，`INPUT` 语句在子集 `IF` 语句检查 `Country` 值之前读取所有变量。然后，如果 `Country` 的值为 `GB`，则将该观测值写入输出数据集 `Retail.UnitedKingdom`。

```sas
data retail.UnitedKingdom;
   infile customerdata;
   input @1   Customer_ID         12.
         @13  Country             $2.
         @15  Gender              $1.
         @16  Personal_ID        $15.
         @31  Customer_Name      $40.
         @71  Customer_FirstName $20.
         @91  Customer_LastName  $30.
         @121 Birth_Date       date9.
         @130 Customer_Address   $45.
         @175 Street_ID           12.
         @199 Street_Number       $8.
         @207 Customer_Type_ID     8.;
    if country='GB';
run;
```

| |

| ![2](img/callout02.png) 读取选定变量并进行子集化在此程序中，第一个 `INPUT` 语句仅读取 `Country` 并使用单个末尾 `@` 符号将记录保留在输入缓冲区中。然后程序使用子集 `IF` 语句检查 `Country` 的值。如果 `Country` 的值不是 `GB`，则其他变量不会被读取或写入输出数据集 `Retail.UnitedKingdom`。如果 `Country` 的值为 `GB`，则输入其他变量的值并写入输出数据集 `Retail.UnitedKingdom`。

```sas
data retail.UnitedKingdom;
   infile customerdata;
   input @13 Country $2\. @;
   if country='GB';
   input @1   Customer_ID         12.
         @15  Gender              $1.
         @16  Personal_ID        $15.
         @31  Customer_Name      $40.
         @71  Customer_FirstName $20.
         @91  Customer_LastName  $30.
         @121 Birth_Date       date9.
         @130 Customer_Address   $45.
         @175 Street_ID           12.
         @199 Street_Number       $8.
         @207 Customer_Type_ID     8.;
run;
```

| |

### 一般建议

*   在 `DATA` 步中放置子集 `IF` 语句，使得在进行子集处理之前只读取选择记录所必需的变量。这可以节省大量的 CPU 时间。两种技术在 I/O 或内存使用上没有区别。

*   当从外部文件选择记录时，在将所有字段读取到程序数据向量之前，先读取用于选择的字段或多个字段。

*   使用单个末尾 `@` 符号来滞留输入缓冲区，以便当变量或多个变量满足 `IF` 条件时，你可以继续读取该记录。

*   使用 `@1 Customer_ID` 重置指针，以便能够从第一个位置开始读取记录。

除了子集观测值外，你还可以通过语句或选项高效地只读写核心数据来筛选变量。

## 使用 KEEP 和 DROP 语句及选项筛选变量筛选

要筛选变量，可以使用以下任一：

*   `DROP` 和 `KEEP` 语句

*   `DROP=` 和 `KEEP=` 数据集选项

![使用 KEEP 和 DROP 语句筛选变量](img/m83-g1.png)使用 `KEEP=` 数据集选项和 `DROP=` 数据集选项对资源使用的影响取决于它们是用于 `SET` 或 `MERGE` 语句还是 `DATA` 语句。下面的图显示了这些选项如何处理数据。![使用 KEEP 和 DROP 语句筛选变量](img/m83-g2.png)在 `SET` 或 `MERGE` 语句中使用，`KEEP=` 和 `DROP=` 数据集选项影响读取到程序数据向量的变量。在 `DATA` 步中只读取需要的变量有时提高效率。在 `DATA` 语句中使用，这些相同的选项会对要排除的变量标记并影响写入输出数据集的变量。`DROP` 和 `KEEP` 语句的作用与 `DATA` 语句中的 `KEEP=` 或 `DROP=` 选项相似。下表描述了 `KEEP` 语句和 `KEEP=` 数据集选项将变量写入 SAS 数据集时的差异。

| DROP 或 KEEP 语句 | DROP= 或 KEEP= 输出数据集选项 | DROP= 或 KEEP= 输入数据集选项 |
| --- | --- | --- |
| 将选定的变量写入所有输出数据集。 | 可以向不同的数据集写入不同的变量。 | 将选定的变量读取到 PDV。 |
| 仅适用于 `DATA` 步。 | 适用于 `DATA` 步或大多数 `PROC` 步。 | 适用于 `DATA` 步或大多数 `PROC` 步。 |

## 比较示例：创建包含平均值和中位数统计的报告

## 概述

假设你想通过由文件引用 `Customerdata` 引用的外部文件中读取数据子集，来创建一个 SAS 数据集。你希望该子集仅包含英国的客户。该子集约占外部文件中数的 6%，该文件包含 89,954 条记录和 12 个字段。以下示例程序比较了读取和写入数据集变量的两种技术。

| ![1](img/callout01.png) 未使用 KEEP= 选项此程序从数据集 `Retail.Order_fact` 读取所有变量，且不限制写入输出数据集 `Retail.Profit` 的变量。`PROC MEANS` 读取数据集中的所有变量。





```
data retail.profit;
   set retail.order_fact;  
   if discount=. then    
      Profit=(total_retail_price-costPrice_Per_Unit)*quantity;  
   else Profit=((total_retail_price*discount)-costprice_per_unit)*quantity;
run;
proc means data=retail.profit mean median maxdec=2;
   title 'Order Information';
   class employee_id;
   var profit;
run;
```

| ![2](img/callout02.png) 在 DATA 语句中使用 KEEP= | 该程序在 `DATA` 语句中使用 `KEEP=` 数据集选项，将两个变量写入输出数据集 `Retail.Profit`。`PROC MEANS` 仅从数据集中读取两个变量。 |

```
data retail.profit(keep=employee_id profit);
   set retail.order_fact;
   if discount=. then
      Profit=(total_retail_price-costprice_per_unit)*quantity;
   else Profit=((total_retail_price*discount)-costprice_per_unit)*quantity;
run;
proc means data=retail.profit mean median maxdec=2;
   title 'Order Information';
   class employee_id;
   var profit;
run;
```

| ![3](img/callout03.png) 在 DATA 和 SET 语句中使用 KEEP= | 该程序在 `SET` 语句中使用 `KEEP=` 选项从 `Retail.Order_fact` 读取六个变量，并在 `DATA` 语句中使用 `KEEP=` 数据集选项将两个变量写入输出数据集 `Retail.Profits`。`PROC MEANS` 仅从数据集中读取两个变量。 |

```
data retail.profits(keep=employee_id profit);  
   set retail.order_fact(keep=employee_id total_retail_price discount 
                              costprice_per_unit quantity);  
      if discount=. then  
         Profit=(total_retail_price-costprice_per_unit)*quantity;  
      else Profit=((total_retail_price*discount)-costprice_per_unit)*quantity;
run;
proc means data=retail.profit mean median maxdec=2;
   title 'Order Information';
   class employee_id;
   var profit;
run;
```

| ![4](img/callout04.png) 在 SET 和 MEANS 语句中使用 KEEP= | 该程序在 `SET` 语句中使用 `KEEP=` 选项从 `Retail.Order_fact` 读取选定的变量，并在 `MEANS` 语句中使用 `KEEP=` 数据集选项处理统计报告所需的变量。如果你在 `Retail.Profits` 中需要额外的变量进行后续处理，但 `PROC MEANS` 只需处理两个变量，可以这样做。 |

```
data retail.profit;
  set retail.order_fact(keep=employee_id total_retail_price discount
                             costprice_per_unit quantity);
  if discount=. then
     Profit=(total_retail_price-costprice_per_unit)*quantity;
  else Profit=((total_retail_price*discount)-costprice_per_unit)*quantity;
run;
proc means data=retail.profit(keep=employee_id profit) mean median maxdec=2;
   title 'Order Information';
   class employee_id;
   var profit;
run;
```
```

### 通用建议

* 为了减少 CPU 时间和 I/O 操作，请避免读取和写入不需要的变量。

### 比较示例：创建一个仅包含特定变量的 SAS 数据集

## 概述

假设你想从由文件引用 `Rawdata` 引用的外部文件中读取数据，并创建一个仅包含 `Customer_ID`、`Country`、`Gender` 和 `Customer_Name` 变量的 SAS 数据集。以下示例程序比较了两种技术。你可以将这些示例作为模型，在你自己的环境中创建基准程序。你的结果可能会根据数据结构、你的操作系统环境以及你所在地的可用资源而有所不同。

### 编程技术

| ![1](img/callout01.png) 读取所有字段 | 在此程序中，`KEEP=` 数据集选项仅将需要的变量写入输出数据集，而 `INPUT` 语句从外部文件中读取所有字段。 |

```
data retail.customers(keep=Customer_ID Country Gender Customer_Name);
   infile rawdata;
   input @1   Customer_ID         12.
         @13  Country             $2.
         @15  Gender              $1.
         @16  Personal_ID        $15.
         @31  Customer_Name      $40.
         @71  Customer_FirstName $20.
         @91  Customer_LastName  $30.
         @121 Birth_Date       date9.
         @130 Customer_Address   $45.
         @175 Street_ID           12.
         @199 Street_Number       $8.
         @207 Customer_Type_ID     8.;
run;
```

| ![2](img/callout02.png) 读取选定字段 | 在此程序中，`INPUT` 语句从外部文件中读取选定的字段，默认情况下，这些字段会被写入输出数据集。该程序是高效处理的示例。 |

```
data retail.customers;
   infile rawdata;
   input @1   Customer_ID         12.
         @13  Country             $2.
         @15  Gender              $1.
         @31  Customer_Name      $40.
run;
```

### 通用建议

* 为了减少 CPU 时间和 I/O 操作，请避免读取和写入不需要的变量。
* 为了节省 CPU 资源，请从外部文件中仅读取需要的字段。
* 为了节省 CPU 时间，请避免转换不需要的数据。





```
data _null_;
   infile rawdata;
   input @1   Customer_ID         12.
         @13  Country             $2.
         @15  Gender              $1.
         @16  Personal_ID        $15.
         @31  Customer_Name      $40.
         @71  Customer_FirstName $20.
         @91  Customer_LastName  $30.
         @121 Birth_Date       date9.
         @130 Customer_Address   $45.
         @175 Street_ID           12.
         @199 Street_Number       $8.
         @207 Customer_Type_ID     8.;
run;
```

| ![2](img/callout02.png) 从 SAS 数据集读取 | 在此程序中，`SET`语句直接从现有的 SAS 数据集中读取数据。与上一个程序一样，`DATA`语句使用 `_NULL_` 而不是命名数据集。 |

```
data _null_;  
   set retail.customer;
run;
```

### 通用建议

* 为了节省 CPU 资源，请读取 SAS 数据集而不是外部文件。
* 为了减少 I/O 操作，请读取 SAS 数据集而不是外部文件。I/O 操作的减少很大程度上取决于外部文件的块大小和 SAS 数据集的页大小。

# 避免不必要的过程调用

## 概述

最佳实践规定您应避免不必要的过程调用。实现此点的方法是利用一次调用即可完成多个任务的过程。几个过程允许您通过调用一次过程来执行多个任务或创建多个报告。这些包括：

* `SQL` 过程
* `DATASETS` 过程
* `FREQ` 过程
* `TABULATE` 过程。

注意：`BY` 组处理也可以减少不必要的过程调用。为了说明这一原理，请查看 `DATASETS` 过程的特性。

## 执行 DATASETS 过程

`DATASETS` 过程可以使用 `RUN-group` 处理来处理多组语句。`RUN-group` 处理允许您在不结束过程的情况下提交一组语句。当 `DATASETS` 过程执行时，会发生以下操作：

* SAS 读取与一个任务相关的程序语句，直到遇到 `RUN` 语句或隐含的 `RUN` 语句。
* SAS 执行之前的所有语句，然后继续读取直到遇到另一个 `RUN` 语句或隐含的 `RUN` 语句。

要执行最后一个任务，您必须使用 `RUN` 语句或 `QUIT` 语句。

```
proc datasets lib=company;
   modify orders;
      rename quantity=Units_Ordered;
      format costprice_per_unit dollar13.2;
      label delivery_date='Date of Delivery';
   run;
   modify customers;
      format customer_birthdate mmddyy10.
   run;
quit;
```

您可以通过提交 `DATA` 语句、`PROC` 语句或 `QUIT` 语句来终止 `PROC DATASETS` 的执行。

## RUN 组处理

`RUN-group` 处理避免了不必要的过程调用。支持 `RUN-group` 处理的过程包括：

* `CHART`, `GCHART`
* `PLOT`, `GPLOT`
* `GIS`, `GMAP`
* `GLM`
* `REG`
* `DATASETS`

## 使用 PROC DATASETS 使用不同类型的 RUN 组

`DATASETS` 过程支持四种类型的 `RUN groups`。每个 `RUN group` 都由组成其并导致其执行的语句定义。`PROC DATASETS` 中的某些语句充当隐含的 `RUN` 语句，因为它们会导致它们之前的 `RUN`组执行。以下语句构成了一个 `RUN`组，以及导致每个 `RUN`组执行的原因：

* `PROC DATASETS` 语句始终立即执行。不需要其他语句即可触发 `PROC DATASETS` 语句的执行。因此，`PROC DATASETS` 语句本身就是一个 `RUN`组。
* `MODIFY` 语句及其任何从属语句形成一个 `RUN`组。这些 `RUN`组总是立即执行。不需要其他语句即可触发 `MODIFY RUN`组的执行。
* `APPEND`、`CONTENTS` 和 `COPY` 语句（包括存在的 `EXCLUDE` 和 `SELECT`）形成它们各自独立的 `RUN groups`。每个 `APPEND` 语句形成一个单语句 `RUN group`，每个 `CONTENTS` 语句形成一个单语句 `RUN group`，每个 `COPY` 步形成一个 `RUN`组。过程中的任何其他语句（属于 `COPY` 或 `MODIFY` 语句的从属语句外）都会导致 `RUN`组执行。

此外，以下一个或多个语句形成一个 `RUN`组：

* `AGE`
* `EXCHANGE`
* `CHANGE`
* `REPAIR`

如果这些任何语句顺序出现在 `PROC` 步中，该序列就会形成一个 `RUN`组。例如，如果 `REPAIR` 语句紧跟在 `SAVE` 语句之后，`REPAIR` 语句不会强制 `SAVE` 语句执行；它成为同一个 `RUN`组的一部分。要执行该 `RUN`组，请提交以下语句之一：

* `PROC DATASETS`
* `MODIFY`
* `APPEND`
* `QUIT`
* `CONTENTS`
* `RUN`
* `COPY`
* 其他 `DATA` 或 `PROC` 步

## 示例：修改 SAS 数据集的描述部分

## 概述

假设您想使用 `DATASETS` 过程修改数据集 `NewCustomer`、`NewOrders` 和 `NewItems`。以下示例程序比较了两种技术。您可以将这些示例作为在您自己的环境中创建基准程序的模型。您的结果取决于数据结构、您的操作环境以及现场的资源。

### 编程技术

| ![1](img/callout01.png) 多次 DATASETS 过程 | 此程序调用三次 `PROC DATASETS` 来修改数据集 `NewCustomer` 的描述部分，调用两次修改 `NewOrders` 的描述部分，并调用一次数据集 `NewItems` 的名称。 |

```
proc datasets lib=company nolist;
   modify newcustomer;
   rename Country_ID=Country
          Name=Customer_Name;
quit;

proc datasets lib=company nolist;
   modify newcustomer;
   format birth_date date9.;
quit;

proc datasets lib=company nolist;
   modify newcustomer;
   label  birth_date='Date of Birth';
quit;

proc datasets lib=company nolist;
   modify neworders;
   rename order=Order_ID
          employee=Employee_ID
          customer=Customer_ID;
quit;

proc datasets lib=company nolist;
   modify neworders;
   format order_date date9.;
quit;

proc datasets lib=company nolist;
   change newitems=NewOrder_Items;
quit;
``` |

| ![2](img/callout02.png) 单次 DATASETS 过程 | 此程序调用一次 `PROC DATASETS` 来修改数据集 `NewCustomer` 和 `NewOrders` 的描述部分，并修改数据集 `NewItems` 的名称。这种技术更高效。 |

```
proc datasets lib=company nolist;
   modify newcustomer;
   rename country_ID=Country
          name=Customer_Name;
   format birth_date date9.;
   label  birth_date='Date of Birth';
   modify neworders;
   rename order=Order_ID
          employee=Employee_ID
          customer=Customer_ID;
   format order_date date9.;
   change newitems=NewOrder_Items;
quit;
``` |




通过以最高效的顺序执行最少的语句，您可以度地减少 SAS 使用的 CPU 时间。在创建数据子集时，请将子集 `IF` 语句放在逻辑上尽可能早的 `DATA` 步骤中。查阅有关如何高效使用 `IF-THEN/ELSE` 语句或 `SELECT` 语句进行条件逻辑的指南。请记要尽量减少使用 SAS 函数或算术运算符的语句数量。通过将语句放在与 `IF-THEN/ELSE` 语句或 `SELECT/WHEN` 语句相关的组中，仅条件地执行必要的语句。语句组仅在特定条件为真时执行。查阅有关高效使用 `DO` 组的标准。

## 消除不必要的数据扫描

为了尽量减少 I/O 操作，您应该避免比必要的多次读取或写入数据。您可以使用多种技术。例如，使用单个 `DATA` 步骤通过对输入数据进行一次扫描来创建多个输出数据集，而不是在每次创建输出数据集时都使用多个 `DATA` 步骤来处理输入数据。通过使用 `SORT` 过程对数据进行子集处理来创建排序后的子集，而不是在 `DATA` 步骤中进行子集处理后再进行排序。使用 `PROC DATASETS` 而不是 `DATA` 步骤来更改变量属性。

## 只读写核心数据

如果处理的观测值和变量少，SAS 会执行更少的 I/O 操作。要限制处理的观测值数量，可以使用子集 `IF` 语句和 `WHERE` 语句。理解子集 `IF` 语句和 `WHERE` 语句之间的其他差异，就可以应用最佳编程实践。您还可以通过结合 `WHERE` 语句应用 `OBS=` 和 `FIRSTOBS=` 处理来提高性能。从外部文件读取数据时选择观测值，请在 `DATA` 步骤中放置子集 `IF` 语句，使其在读取所有数据之前仅读取选择子集所需的变量。这可以减少处理数据所需的开销。要限制处理的变量数量，可以使用以下任一种方法：

*   `DROP` 和 `KEEP` 语句
*   `DROP=` 和 `KEEP=` 数据集选项

在 `SET` 语句中，`DROP=` 或 `KEEP=` 数据集选项控制哪些变量被读取并随后处理。在 `DATA` 语句中，`DROP=` 或 `KEEP=` 数据集选项控制哪些变量在处理后写入输出数据集。使用带有这些选项的 `SET` 语句是最高效的最佳实践。

## 将 SAS 数据存储在 SAS 数据集中

当使用 SAS 重复分析或操作任何特定组的数据时，创建一个 SAS 数据集而不是每次读取原始数据。从外部文件读取数据而不是从 SAS 数据集中读取会大幅增加 CPU 使用。

## 避免不必要的过程调用

调用一次过程而不是多次。多个过程允许您在仅调用一次过程的情况下创建多个报告。使用单个 `DATASETS` 过程代替多个 `DATASETS` 过程来修改数据集的描述部分可以显著节省 CPU 和 I/O 操作。此外，您还可以利用 `RUN` 组处理在不结束过程的情况下提交语句组。

# 练习

为每个问题选择最佳答案。完成测试后，使用附录中的答案键检查您的答案。

1. 将子集 `IF` 语句放在 `DATA` 步骤的顶部而不是底部可以节省 CPU 使用。如果子集很大而不是很小会发生什么？
    1. 随着子集增大，CPU 使用的节省也会增加，因为 I/O 随之增加。
    2. 随着子集增大，CPU 使用的节省会减少。然而，将子集 `IF` 语句放在 `DATA` 步骤的顶部始终比放在底部消耗更少资源。
    3. 随着子集增大，CPU 使用的节省保持不变。然而，将子集 `IF` 语句放在数据集的底部更为理想。
    4. 随着子集增大，CPU 使用的节省会减少。然而，将子集 `IF` 语句放在数据集的底部会增加 I/O。

2. 关于修改数据和属性的技术，以下哪种描述是正确的？
    1. 您可以使用 `PROC DATASETS` 修改数据值和变量属性。
    2. 您可以使用 `PROC DATASETS` 仅修改数据值。
    3. 您可以使用 `DATA` 步骤同时修改数据值和变量属性。
    4. 您可以使用 `DATA` 步骤仅修改变量属性。

3. 对于选择观测值，子集 `IF` 语句还是 `WHERE` 语句更高效？为什么？
    1. 子集 `IF` 语句更高效，因为它将所有观测值顺序加载到程序数据向量（PDV）中。
    2. 子集 `IF` 语句更高效，因为它检查输入缓冲区中的内容并在它们加载到程序数据向量之前选择观测值，从而节省了 CPU 操作。
    3. `WHERE` 语句更高效，因为它将所有观测值顺序加载到程序数据向量中。
    4. `WHERE` 语句更高效，因为它检查输入页缓冲区中的内容并在它们加载到程序数据向量之前选择观测值，从而节省了 CPU 操作。

4. 在什么情况下创建临时 SAS 数据集比创建永久 SAS 数据集更有优势？
    1. 当基于数据集的外部文件在 SAS 会话之间可能会发生时。
    2. 当基于数据集的外部文件在 SAS 会话之间不会变化时。
    3. 当数据集需要在多个 SAS 会话中使用。
    4. 当您将原始数值转换为 SAS 数据值时。

5. 将使用多个 `DATASETS` 过程的技术与使用单个 `DATASETS` 过程修改数据集描述部分进行比较，哪项是正确的？
    1. 单个 `DATASETS` 过程会导致 I/O 操作增加。
    2. 多个 `DATASETS` 过程会导致 I/O 操作减少。
    3. 单个 `DATASETS` 过程会导致 CPU 使用减少。
    4. 多个 `DATASETS` 过程会导致 CPU 使用减少。




注意：本章不涵盖 SAS 可扩展性能数据引擎 (SAS SPD Engine)。有关使用 SAS SPD Engine 提高性能的详细信息，请参 SAS 文档。

# 使用索引进行高效的 WHERE 处理

## 概述

在处理 `WHERE` 表达式时，SAS 会确定以下哪种访问方法可能最有效：

| ![顺序访问](img/m85-2-g1.png) | SAS 按照物理顺序顺序检查所有的观测值。 |

| ![直接访问](img/m85-2-g2.png) | SAS 使用索引直接访问特定的观测值。使用索引处理 `WHERE` 表达式被称为优化 `WHERE` 表达式。 |

使用索引处理 `WHERE` 表达式在某些情况下可以提高性能，但在其他情况下则不会。例如，使用索引选择较小的子集比选择大型子集更有效。此外，索引在消耗某些资源的同时也节省了其他资源。在 SAS 决定是否创建索引之后，您在决定 SAS 可以使用哪种访问方法方面也起着决定作用。当您的程序包含 `WHERE` 表达式时，您应该检查程序，看看您是否同意直接访问可能更有效。如果是，您可以通过创建新索引或维护现有索引来确保索引可用。为了帮助您对是否创建索引做出更有效的决策，本主题以及接下来的几个主题将让您深入了解以下内容：

*   SAS 执行顺序访问和直接访问的步骤
*   使用索引的益处和成本
*   SAS 确定哪种访问方法最高效执行的步骤
*   影响索引访问资源使用的因素
*   决定是否创建、使用和维护索引的指南

注意：您应该已经知道如何通过 `DATA` 语句中的 `INDEX=` 数据集选项、`DATASETS` 过程和 `SQL` 过程来创建和维护索引。要查看这些 SAS 元素，请参见使用 PROC SQL 创建和管理索引 和 创建索引。注意：SAS 还可以使用索引来处理 `BY` 语句。`BY` 处理允许您根据 `BY` 语句中指定的一个或多个变量的值按特定顺序处理观测值。对数据文件建立索引允许您无需排序数据文件即可使用 `BY` 语句。当您指定 `BY` 语句时，SAS 会检查 `Sorted` 指示器的值。如果 `Sorted` 指示器设置为 `NO`，则 SAS 将寻找合适的索引。如果存在合适的索引，软件将按照索引顺序从数据文件中自动检索观测值。使用索引处理 `BY` 语句并不总是比简单排序数据文件更有效。因此，对 `BY` 语句使用索引通常是为了方便，而不是为了性能。

## 顺序访问数据

在顺序访问观测值时，SAS 必须在数据文件中按照其物理顺序检查所有的观测值。

## 示例

假设您想创建一个新的数据集 `Company.D02jul2000`，该数据集包含来自 `Company.Dates` 数据集的观测值子集。以下 `DATA` 步使用 `WHERE` 语句选择所有 `Date_ID` 为 `02JUL2000` 的观测值：

```
data company.d02jul2000;
   set company.dates;
   where date_id='02JUL2000'd;
run;
```

数据集 `Company.Dates` 不包含定义在变量 `Date_ID` 上的索引，因此 SAS 必须使用顺序访问来处理 `WHERE` 语句。注意：如果数据集 `company.dates` 已经按 `date_id` 排序，则 SAS 将顺序搜索数据，直到满足 `WHERE` 标准（`date_id='02JUL2000'd`）。

## 直接访问数据

使用索引进行 `WHERE` 处理时，SAS 会访问每个所需的观测值，而无需读取数据集中的每个观测值。

## 示例

假设您已经在 `Company.Dates` 数据集的变量 `Date_ID` 上定义了一个索引。这一次，当您提交以下 `DATA` 步时，SAS 使用索引来处理 `WHERE` 语句：

```
data company.d02jul2000;
   set company.dates;
   where date_id='02JUL2000'd;
run;
```

通过索引（直接访问）检索数据的过程比顺序访问更复杂，因此直接访问每个检索到的观测值所需的 CPU 时间比顺序访问更多。然而，对于较小的子集，使用索引可以减少 SAS 加载到输入缓冲区页面数量，从而减少 I/O 操作次数。注意：当数据集中的值按照它们在索引中出现的顺序排序时，符合条件的观测值是相邻的。在这种情况下，SAS 加载到输入缓冲区页面比数据随机分布在集中要少。因此，当数据集排序时，所需的 I/O 操作更。

## 使用索引的益处和成本

如前面的示例所示，使用索引既有益处也有成本。权衡这些益处和成本是决定使用索引是否高效的重要部分。使用索引的主要益处包括：

*   提供对较小观测值子集的快速访问
*   按排序顺序返回值
*   可以强制唯一性

使用索引的主要成本包括：

*   创建和维护索引需要额外的 CPU 周期和 I/O 操作
*   读取数据需要额外的 CPU 时间
*   存储索引需要额外的磁盘空间
*   加载索引页需要额外的内存

注意：使用索引时，SAS 需要额外的缓冲区。当打开数据文件时，SAS 打开的是数据文件而不是索引。除非使用索引，否则不需要缓冲区，但 SAS 为准备使用索引会分配缓冲区。索引的层数决定了分配的缓冲区数量。如果这些缓冲区未用于索引，则可以用于其他处理。

## SAS 如何选择访问方法

当 SAS 处理 `WHERE` 表达式时，它首先通过执行以下步骤确定是使用直接访问还是顺序访问：

1.  识别可用索引
2.  识别可以优化的条件
3.  估计符合条件的观测值数量
4.  比较两种方法的资源使用

# 识别可用索引

## 概述

SAS 的第一步是确定是否存在可以处理 `WHERE` 表达式的索引。具体来说，SAS  `WHERE` 表达式中每个条件的变量，以确定该变量是否是索引的键变量![Order_Date 索引](img/m85-8-g1.png)SAS 可以简单索引或复合索引来优化 `WHERE` 表达式。要用于优化单个 `WHERE` 条件，必须满足以下要求之一：

*   `WHERE` 条件中的变量是简单索引的键变量
*   `WHERE` 条件中的变量是复合索引的第一个键变量

SAS 识别定义在 `WHERE` 表达式中任何变量上的所有索引。然而，无论有多少可用索引，SAS 只能使用一个索引来处理 `WHERE` 表达式。因此，如果有多个索引，SAS 必须在它们之间进行选择。当 SAS 寻找可用索引时，有三种结果：

| 索引 | 结果 |

| --- | --- |





| WHERE 表达式中的任何变量均未定义索引。 | SAS 不继续执行决策过程。SAS 必须使用顺序访问来处理 WHERE 表达式。 |
| WHERE 表达式中的一个或多个变量上定义了一个可用索引。 | SAS 继续执行决策过程，并确定使用可用索引是否比使用顺序访问更高效。 |
| 存在多个可用索引。每个索引都定义在 WHERE 表达式中的一个或多个变量上。 | SAS 继续执行决策过程。SAS 必须在接下来的几步中在可用索引之间进行选择。SAS 尝试选择满足最多条件且选出最小观测值子集的索引。 |

注意：如果程序同时指定了 `WHERE` 表达式和 `BY` 语句，SAS 会寻找一个同时满足这两个者条件的索引。如果没有找到此类索引，则 `BY` 语句具有优先权，以便 SAS 能够确保返回的数据按排序排列。使用 `BY` 语句时，如果优化会破坏 `BY` 顺序，则 SAS 无法使用索引来优化 `WHERE` 表达式。

## 示例：识别单个可用索引

假设你提交了一个包含以下 `WHERE` 语句的程序，并假设数据集有一个索引，如下所示：

| WHERE 语句 | 可用索引 |
| --- | --- |
| |
```
where delivery_date='02jul2000'd
```
| 定义在 `Delivery_Date` 上的简单索引 |

此 `WHERE` 表达式包含一个条件，该条件中的变量（`Delivery_Date`）是简单索引中的键变量。如果后续步骤满足优化的所有其他要求，则 SAS 就可以使用此索引来优化 `WHERE` 表达式。同样，如果唯一的可用索引是 `Delivery_Date` 为第一个键变量的复合索引，只要满足所有其他优化要求，SAS 就可以使用该索引。即使 `WHERE` 语句有多个条件，SAS 也可以使用简单索引或复合索引来优化其中某一个条件。例如，假设你的程序包含一个两个条件的 `WHERE` 语句，并假设数据集有一个索引，如下所示：

| WHERE 语句 | 可用索引 |
| --- | --- |
| |
```
where order_date='01jan2000'd and 
delivery_date='02jul2000'd';
```
| 定义在 `Delivery_Date` 上的简单索引 |

假设满足了所有其他优化要求，SAS 可以此索引来优化该 `WHERE` 表达式中的第二个条件。

## 示例：识别多个可用索引

假设你的程序包含一个带有两个条件的 `WHERE` 语句，并假设每个条件都引用了不同索引中的键变量，如下所示：

| WHERE 语句 | 可用索引 |
| --- | --- |
| |
```
where order_date='01jan2000'd and 
delivery_date='02jul2000'd';
```
| |
* - 定义在 `Order_Date` 上的简单索引
* - 定义在 `Delivery_Date` 上的简单索引。 |

尽管有两个可用索引，但 SAS 只能使用一个索引来优化 `WHERE` 语句。在过程的后续步骤中，SAS 会尝试选择满足最多条件且选出最小观测值子集的索引。

## 复合优化

无论 `WHERE` 表达式包含多少个条件和变量，SAS 通常只使用一个索引来处理一个条件。但在一个被称为“复合优化”的过程中，SAS 可以使用复合索引来优化多个变量上的多个条件，这些条件通过逻辑运算符（如 `AND`）连接。构建 `WHERE` 表达式以利用单个索引中的多个键变量，可以大大提高性能。为了发生复合优化，复合索引中的至少前两个键变量必须被用于 `WHERE` 条件中。在本章的后后部分，你将学习到要发生复合优化必须满足的其他要求。注意：`WHERE` 表达式也可以包含非索引变量，且键变量和非索引变量可以以任何顺序出现在表达式中。

## 示例：用于优化多个条件的复合索引

假设你的程序包含一个带有两个条件的 `WHERE` 语句，并假设每个条件都引用了复合索引中的前两个键变量之一：

| WHERE 语句 | 可用索引 |
| --- | --- |
| |
```
where order_date='01jan2000'd and 
delivery_date='02jul2000'd';
```
| 定义在以下变量上的复合索引：
* - `Order_Date`（第一个键变量）
* - `Delivery_Date`（第二个键变量）
* - `Product_ID`（第三个键变量） |

由于 `WHERE` 表达式中引用的两个变量是复合索引的前两个键变量，只要 `WHERE` 条件满足所有其他优化要求，SAS 就可以使用复合索引进行复合优化。

## 示例：用于优化一个条件的复合索引

以下 `WHERE` 语句也包含两个条件，每个条件都引用了复合索引中的变量之一：

| WHERE 语句 | 可用索引 |
| --- | --- |
| |
```
where order_date='01jan2000'd and 
product_id='220101400106';
```
| 定义在以下变量上的复合索引：
* - `Order_Date`（第一个键变量）
* - `Delivery_Date`（第二个键变量）
* - `Product_ID`（第三个键变量） |

与上一个 `WHERE` 语句一样，`Order_Date` 是索引中的第一个键变量。然而，在这种情况下，复合索引仅可以优化第一个条件。第二个条件引用了第三个键变量 `Product_ID`，但 `WHERE` 表达式没有引用第二个键变量 `Delivery_Date`。由于缺乏第一个和第二个键变量的引用，无法进行复合优化。

## 示例：无法用于优化的复合索引

现在假设你的程序包含一个引用复合索引中第二个和第三个键变量的 `WHERE` 语句，如下：

| WHERE 语句 | 可用索引 |
| --- | --- |
| |
```
where delivery_date='02jul2000'd and 
product_id='220101400106';
```
| 定义在以下变量上的复合索引：
* - `Order_Date`（第一个键变量）
* - `Delivery_Date`（第二个键变量）
* - `Product_ID`（第三个键变量） |

在这种情况下，由于 `WHERE` 语句没有无法无法无法无法索引无法优化。

# 识别可以优化的条件

除了包含键变量，`WHERE` 条件还需要满足其他要求才能成为优化候选。SAS 只对包含某些运算符和函数的 `WHERE` 条件使用索引。因此，SAS 的下一步是考虑包含键变量的条件的运算符和函数。

## 优化单个 WHERE 条件的要求

SAS 会对包含以下任何运算符和函数的 `WHERE` 条件使用索引：注意：对于以下所有示例，假设数据集在 `Quarter`、`Date_ID` 和 `Region` 变量上有简单索引。

| 运算符 | 示例 |
| --- | --- |
| 比较运算符 | |
```
where quarter = '1998Q1';
```
```
where date_id < '03JUL2000'd;
```
```
where quarter in ('1998Q2','1998Q3');
``` |
| 带有 NOT 的比较运算符 | |
```
where quarter ne '1999Q1';
```
```
where quarter not in ('1999Q1','1999Q4');
``` |
| 带有冒号修符的比较运算符可以在任何比较运算符上添加冒号修符 (:) 以比较字符字符串的指定前缀。冒号修符不能与 PROC SQL 使用；请应使用 `LIKE` 运算符。 | |
```
where quarter =: '1998';
``` |
| CONTAINS 运算符 | |
```
where quarter contains 'Q4';
``` |





| 指定了上限和下限的完全边界范围条件，包括 `BETWEEN-AND` 运算符 | |

```
where '01Jan1999'd < date_id
      < '31Dec1999'd;
```

```
where date_id between '01Jan1999'd
              and '31Dec1999'd
``` |
| 模式匹配运算符 `LIKE` | |

```
where quarter like '%Q%';
``` |

| `IS NULL` 或 `IS MISSING` 符 | |

```
where quarter is null;
```

```
where quarter is missing;
``` |

| 函数 | 示例 |
| --- | --- |
| `TRIM` 函数 | |
```
where trim(region) = 'Queensland';
``` |
| 形式为 `WHERE SUBSTR(variable,position,length)='string';` 的 `SUBSTR` 函数，满足以下条件：<br>*position = 1` <br>*length` 小于等于 `variable` 的长度 <br>*length` 等于 `string` 的长度 | |
```
where substr(quarter,1,4) = '1998';
``` |

**注意**：上述列出的部分但并非所有要求也适用于复合优化。复合优化要求将在在本章后文中介绍。

## 无法优化的 WHERE 条件

SAS 不使用索引来处理包含下列表任何元素的 `WHERE` 条件。注意：对于以下所有示例，假设数据集在变量 `Date_ID`、`Quarter` 和 `Quantity` 上建有简单索引。

| WHERE 条件中的元素 | 示例 |
| --- | --- |
| 除 `TRIM` 或 `SUBSTR` 外的任何函数 | |
```
where weekday(date_id)=2;
``` |
| 从第一个位置之后的任何位置开始搜索字符串的 `SUBSTR` 函数 | |
```
where substr(quarter,6,1)='1';
``` |
| 似音运算符 (`=*`) | |
```
where quarter=*'1900Q0';
``` |
| 算术运算符 | |
```
where quantity=quantity+1;
``` |
| 变量与变量之间的条件 | |
```
where quantity gt threshold;
``` |

## 复合优化要求

对于优化单个条件时接受的大多数相同运算符也适用于复合优化。然而，复合优化对出现在 `WHERE` 表达式中的运算符有特殊要求：

* `WHERE` 条件必须使用 `AND` 运算符连接，或者（如果所有条件都引用同一个变量）则使用 `OR` 运算符连接。
* 包含键变量的 `WHERE` 条件中至少有一个必须包含 `EQ` 或 `IN` 运算符。

## 示例：复合优化

假设你的程序包含以下 `WHERE` 语句，它选择所有名字为 John Smith 的人。`WHERE` 语句包含两个条件。每个条件引用不同的变量：

```
where lastname eq 'Smith' and 
      frstname eq 'John';
```

假设 `Lastname` 是复合索引中的第一个键变量`Frstname` 是第二个键变量。该 `WHERE` 语句满足复合优化的所有要求：

* `WHERE` 表达式引用了一个复合索引中的至少两个键变量。
* 两个 `WHERE` 条件通过 `AND` 运算符连接。
* 条件中至少一个包含 `EQ` 运算符。

如果 `WHERE` 语句中的两个条件调换位置如下所示，该语句仍然满足复合优化的所有要求。键变量出现的顺序并不重要。

```
where frstname eq 'John' and 
      lastname eq 'Smith';
```

现在假设 `WHERE` 语句中的条件是用运算符 `OR` 而不是 `AND` 组合的：

```
where frstname eq 'John' or
      lastname eq 'Smith';
```

这些条件无法被优化，因为它们通过 `OR` 连接，但没有引用同一个变量。

# 估计观测值数量

## 概述

对于较小的子集，使用索引访问比对较大的子集使用顺序访问更高效。因此，在识别出任何可用索引并评估 `WHERE` 表达式中的条件后，SAS 会估计符合索引的观测值数量。SAS 是否使用索引取决于符合条件的观测值的百分比（子集相对于数据集的大小），如下所示![SAS 索引](img/m85-17-g1.png)

* 如果子集小于数据集的 3%，则直接访问几乎比顺序访问更有效，SAS 将使用索引。在这种情况下，SAS 不会继续比较可能的资源使用。
* 如果子集在数据集的 3% 到 33% 之间，直接访问可能比顺序访问更有效，SAS 可能会使用索引。
* 如果子集大于数据集的 33%，则直接访问比顺序访问更有效的概率较低，SAS 可能使用也可能不使用。

当存在多个索引时，SAS 选择产生符合观测值最少（子集最小）的一个。即使每个索引返回的子集小于数据集的 3%，SAS 也会这样做。

## 输出分位数信息

为了帮助 SAS 估计通过 `WHERE` 表达式选择的观测值数量，每个索引都存储 21 个称为累计百分位数（centiles）的统计数据。分位数提供了变量分布的信息。理解数据值的分布可以帮助你提高 `WHERE` 处理的效率。你可以通过以下位置之一指定 `CENTILE` 选项来打印索引文件的分位数：

* `CONTENTS` 过程
* `DATASETS` 过程中的 `CONTENTS` 语句

| `PROC CONTENTS <options>`; `RUN;` | `PROC DATASETS <options>`; `QUIT;` |

## 示例

以下 SAS 程序为数据集 `Company.Organization` 打印分位数信息：

```
proc contents data=company.organization centiles;
run;
```

此程序的部分输出所示。如左侧所示，`Employee_ID` 上定义了索引。右侧列出了 21 个分位数。

| 列表位置 | 显示的值 | 描述 |
| --- | --- | --- |
| 1 (第一个) | 120101 | 索引的最小值（0% 的值小于此值） |
| 2-20 | 120152 - 121097 | 从底部 5% 到底部 95% 的 19 个百分位数中的每个值 |
| 21 (最后一个) | 9999999 | 索引的最大值（100% 的值小于或等于此值） | ![索引和属性字母列表](certpgadv/images/m85-18-g1.png

注意：关于更新和刷新数据文件分位数的信息，请参 SAS 文档。

# 比较可能的资源使用

## 概述

在 SAS 估计了符合条件的观测值数量并选择了符合观测值最少的索引后，SAS 必须确定通过索引或顺序读取所有观测值来满足 `WHERE` 表达式更快（更高效）。具体而言，SAS 会预测为了通过每种访问方法满足 `WHERE` 表达式需要多少 I/O 操作。然后比较这两种资源成本。注意：记住，如果 SAS 估计子集小于数据集的 3%，则 SAS 不需要估计资源使用。在这种情况下，SAS 使用索引来处理 `WHERE` 语句。

## SAS 如何比较资源使用

为了比较资源使用，SAS 执行以下步骤：





1. SAS 会预测如果使用索引来满足 `WHERE` 表达式，需要多少次 I/O 操作。为此，SAS 将索引定位到包含符合值的第一个条目处。在考虑当前可用缓冲区数量的缓冲区管理模拟中，将处理该索引页上的 `RIDs`（记录标识符），这指示了读取数据文件中的观测值需要多少次 I/O。
2. SAS 计算对整个数据文件进行顺序扫描的 I/O 成本。
3. SAS 比较这两种资源成本，并确定哪种访问方法的成本更低。

注意：如果比较资源成本的结果相等，SAS 将选择索引。

## 影响 I/O 的因素

多个因素会影响 `WHERE` 处理所需的 I/O 操作次数，包括以下因素：

* 子集大小相对于数据集的大小
* 数据文件中的页数
* 数据的顺序
* 为了顺序读取而对压缩文件解压缩的成本

这些因素在下文中得到了更详细的讨论。

## 子集大小相对于数据集的大小

正如本章前面解释的那样，SAS 更有可能使用索引来访问一小部分观测值。使用索引检索数据的过程本质上比顺序处理数据更复杂。然而，对于小型子集，仅读取少数观测值的益处大于复杂处理的成本。子集越小，性能增益越大。请记住，如果子集小于数据集的 3%，SAS 将使用索引；如果子集在数据集的 3% 到 33% 之间，SAS 可能会使用索引。

## 数据文件中的页数

对于较小的数据文件，顺序处理通常与索引处理一样高效。如果数据文件的页数少于三页，即使子集小于整个数据集的 3%，顺序访问也会更快。

注意：在单次 I/O 操作中可以传输到单个缓冲区的数据量称为页大小。要查看数据文件中有多少页，请使用 `CONTENTS` 过程或 `DATASETS` 过程中的 `CONTENTS` 语句。有关关于报告数据文件页大小的更多信息，请参阅控制内存使用。

## 数据的顺序

数据的顺序（排序顺序）按下文所示影响 I/O 操作次数：

| 数据的顺序 | 对 I/O 操作的影响 |
| --- | --- |
| 观测值随机分布在整个数据文件中 | 符合条件的观测值位于较多的数据文件页上。每当 SAS 加载一个页，就需要一次 I/O 操作。因此，数据文件中的数据随机性越高，使用索引所需的 I/O 操作就越多。 |
| 观测值按索引变量或变量排序 | 数据的顺序更像索引（按值升序），因此符合条件的观测值位于较少的数据文件页上。因此，数据文件中的数据随机性越低，使用索引所需的 I/O 操作就越少。 |

注意：通常，在索引之前按键变量对数据集进行排序会产生更高的效率。数据文件相对于键变量的顺序性越高，索引的利用效率就越高。如果数据文件有多个索引，则按最常用的键变量对数据进行排序效率最高。即使 SAS 不使用索引，对数据集也会产生更高效的 `WHERE` 处理。

## 为了顺序读取而对压缩文件解压缩的成本

当 SAS 读取压缩数据文件时，SAS 在将观测值读入程序数据向量（PDV）时会自动将其解压缩。这需要额外的 CPU 资源，但由于数据集页较少，所需的 I/O 操作较少。对压缩数据文件进行顺序读取时，SAS 必须解压缩文件中的所有观测值。然而，使用直接访问时，SAS 只需要解压缩符合条件的观测值。因此，顺序读取解压缩观测值的资源成本比直接访问更高。

注意：压缩文件是一个减少表示每个观测值所需的字节数的过程。默认情况下，SAS 数据文件是不压缩的。有关压缩文件的更多信息，请参阅控制数据存储空间。

## 影响资源使用的其他因素

数据类型和长度是影响索引效率的其他两个因素。数值型键变量通常比字符型键变量消耗更多的 CPU ，因为当值读入索引或从索引中检索时，数值型变量必须转换为可以排序的格式。字符值已经是可以排序的格式了。

### 决定是否创建索引

在之前的节中，你学习了 SAS 如何确定对于 `WHERE` 处理，是顺序访问还是直接访问可能最有效。你还学习了可以进行评估的各种因素，以确定哪种访问方法最有效。做出判断后，你可以使用以下指南来决定创建索引是否高效。

## 决定是否创建索引的指南

* 尽量减少索引数量，以减少磁盘存储和更新成本。仅对查询中经常使用的变量或（当数据无法排序时）在 `BY`-组处理中使用的变量创建索引。
* 当你打算从大型数据文件中检索一小部分观测值时，请创建索引。
* 如果数据文件的页数少于三页，请不要创建索引。顺序访问数据更快。
* 在具有区分性的变量上创建索引。区分变量具有许多不同的值，可以精确识别观测值。基于区分变量的 `WHERE` 表达式生成的子集比引用非区分变量的更小。非区分变量是指只有两个值的变量（例如，性别不是创建索引的良好变量）。
* 为了减少 I/O 操作，在创建索引之前按键变量对数据进行排序。然后，为了提高性能，按键变量的顺序维护数据文件。注意：如果你选择不使用索引且数据集很大，对数据集进行排序仍然更有效。
* 考虑你的应用程序频繁使用索引。索引必须频繁使用，才能补偿创建和维护它所消耗的资源。
* 考虑经常更改的数据文件的索引成本。
* 当你为处理 `WHERE` 表达式创建索引时，不要尝试用一个索引满足所有查询。

考虑三个示例查询，以查看如何应用上一节列出的指南。这些查询说明了一个因素——子集大小相对于数据集的大小——对访问方法选择的影响。对于每个查询，你将了解到：

* SAS 可能选择哪种访问方法
* 你是否可以通过创建索引提高性能

## 示例：从不同大小的数据集中选择不同大小的子集

假设你正在处理两个数据集。每个数据集都包含公司订单的信息：

| 数据集名称 | 页数 | 观测值 |
| --- | --- | --- |
| Company.Orders_large | 285,500 | 19,033,380 |
| Company.Orders_small | 2 | 140 |

你想创建查询来生成三个子集详细报告，每个对应以下类型的子集之一：

* 大型数据集中的小型子集





- 来自大型数据集的大型子集
- 来自小型数据集的小型子集

在这三个查询中，`WHERE` 表达式都指定了变量 `Order_Date`。你已知该变量在查询中频繁使用，并且是一个区分性变量。根据上一节的指南，这两点都是在该变量上创建索引的准则。然而，目前两个数据集中都没有为该变量定义索引。

## 查询 1：大型数据集中的小型子集

第一份报告显示了 `Company.Orders_large` 中所有在 1998 年 1 月 10 日生成的订单。你的查询如下所示，以及你估计的子集大小：

| 查询 | 子集大小 |
| --- | --- |
| | |
```
data _null_;
    set company.orders_large;
    where order_date='10JAN1998'd;
run;
```
| 2232 条观测值（共 19,033,380 条）<.02% 的数据集 | |

由于子集小于整个数据集的 3%，在 `Order_Date` 上使用索引应该比使用顺序访问更高效。如果可用索引，SAS 会使用索引进行 `WHERE` 处理。为了提高性能，你应该在运行此程序之前在 `Order_Date` 上创建一个索引。

## 查询 2：大型数据集中的大型子集

第二份报告显示了 `Company.Orders_large` 中所有在 2000 年 1 月 1 日之前生成的订单。你的查询和预估的子集大小如下所示：

| 查询 | 子集大小 |
| --- | --- |
| | |
```
data _null_;
   set company.orders_large;
   where order_date<'01JAN2000'd;
run;
```
| 12,752,365 条观测值（共 19,033,380 条）≈ 数据集的 67% | |

由于子集超过了整个数据集的 33%，使用索引可能没有使用顺序访问效率高。SAS 可能不会在 `WHERE` 处理中使用该索引。

## 查询 3：小型数据集中的小型子集

第三份报告显示了较小数据集 `Company.Orders_small` 中所有在 1998 年 6 月 30 日生成的订单。你的查询和预估的子集大小如下所示：

| 查询 | 子集大小 |
| --- | --- |
| | |
```
data _null_;
   set company.orders_small;
   where order_date='30JUN1998'd;
run;
```
| 2 条观测值（共 140 条）<= 2 % 的数据集 | |

由于子集小于整个数据集的 3%，SAS 将使用索引进行 `WHERE` 处理。然而，数据文件的页数少于三页，因此使用顺序访问更高效。在这种情况下，最好不要创建索引。

## 使用 IDXWHERE= 和 IDXNAME= 数据集选项

在大多数情况下，让 SAS 决定是否在 `WHERE` 处理中使用索引是是最好的。但是，有时你可能想控制 SAS 是否使用已有的索引。例如，如果你知道你的查询选择了一个大型子集，因此索引访问并不高效，你可以告诉 SAS 忽略任何索引，并通过对数据集进行顺序搜索来满足 `WHERE` 表达式的条件。或者，如果你的查询选择了一个小型子集且有多个可用索引，你可以确保 SAS 使用特定的索引来处理你的 `WHERE` 语句。最后，在你进行基准测试时，可能希望强制 SAS 使用（或不使用）索引。数据集选项 `IDXWHERE=` 和 `IDXNAME=` 控制索引的使用。

| 选项 | 操作 |
| --- | --- |
| `IDXWHERE=` | 指定 SAS 是否应该使用索引来处理 `WHERE` 表达式，无论 SAS 估计哪种访问方法更快。你不能使用 `IDXWHERE=` 来覆盖处理 `BY` 语句时对索引的使用。 |
| `IDXNAME=` | 导致 SAS 使用特定的索引。 |

注意：你可以使用 `IDXWHERE=` 或 `IDXNAME=`，但不能同时使用两者。有关 `IDXWHERE=` 和 `IDXNAME=` 数据集选项的更多信息，请参阅 使用 PROC SQL 创建和管理索引。

## 指定 MSGLEVEL=I 来确定 SAS 是否使用了索引

要确定 SAS 是否使用了索引处理 `WHERE` 表达式，请将 `I` 指定为 `MSGLEVEL=` 系统选项的值。`MSGLEVEL=I` 会导致 SAS 在 SAS 日中显示有关索引使用的信息。注意：为了最有效地利用资源，请仅将 `MSGLEVEL=I` 用于调试和验证索引使用。注意：有关 `MSGLEVEL=` 系统选项的更多信息，请参阅 创建索引 或 使用 PROC SQL 创建和管理索引。

## 示例：使用 IDXWHERE=NO 防止索引使用

假设你编写了以下查询，列出所有在销售部门工作的员工。

```
proc print data=company.orders
   where department='Sales';
run;
```
现在假设 `Company.organization` 的 `department` 变量上定义了索引。你知道你的查询选择了一个大型子集，因此索引访问并不高效，你可以告诉 SAS 忽略任何索引，并通过对数据集进行顺序搜索来满足 `WHERE` 表达式的条件。或者，如果你的查询选择了一个小型子集且有多个可用索引，你可以确保 SAS 使用特定的索引来处理你的 `WHERE` 语句。最后，在你进行基准测试时，可能希望强制 SAS 使用（或不使用）索引。数据集选项 `IDXWHERE=` 和 `IDXNAME=` 控制索引的使用。

修改后的程序如下：

```
options msglevel=i;
proc print data=company.organization (idxwhere=no);
   where department='Sales';
run;
```

当你运行此程序时，SAS 日志显示没有使用索引。

表 23.1 SAS 日志

| |
```
INFO: Data set option (IDXWHERE=NO) forced a sequential pass of the data
rather than use of an index for where-clause processing.
```
|





```
proc sql;
   select product_id product_name
          supplier_name
      from company.products
      where supplier_country='SE';
quit;
```

这两个步骤都使用 `WHERE` 处理来对数据进行子集划分。在这种情况下，`PROC PRINT` 程序可能比 `PROC SQL` 程序消耗少的 CPU 和内存资源。I/O 资源的使用大致相同。

## 报告 3：排序详细报告

排序后的详细报告列出了所有产品的产品 ID、产品名称和供应商名称，按供应商国家对观测值进行了排序。生成此报告的 `PROC PRINT` 程序和 `PROC SQL` 程序所示：

| PROC PRINT | PROC SQL |
| --- | --- |
| | |
```
proc sort data=company.products
     out=product;
   by supplier_country;
run;

proc print data=product;
   var product_id product_name
       supplier_name;
run;
``` | | ```
proc sql;
   select product_id product_name
          supplier_name
      from company.products
      order by supplier_country;
quit;
``` |

为了对数据进行排序，`PROC PRINT` 程序中添加了一个 `PROC SORT` 步骤，并且 `PROC SQL` 程序中添加了 `ORDER BY` 子句。在这种情况下，`PROC PRINT` 程序可能比 `PROC SQL` 程序消耗少的 CPU 和内存资源。I/O 资源的使用大致相同。

## 报告 4：排序子集详细报告

排序后的子集详细报告列出了所有来自瑞典（SE）的产品 ID、产品名称和供应商名称，按供应商名称对观测值进行了排序。生成此报告的 `PROC PRINT` 程序和 `PROC SQL` 程序所示：

| PROC PRINT | PROC SQL |
| --- | --- |
| | |
```
proc sort data=company.products
     (keep=Product_ID Product_Name
     Supplier_Name Supplier_Country)
     out=product;
     where supplier_country='SE';
   by supplier_name;
run;

proc print data=product;
   var product_id product_name
       supplier_name;
run;
``` | | ```
proc sql;
   select product_id product_name
          supplier_name
      from company.products
      where supplier_country='SE'
      order by supplier_name;
quit;
``` |

为了对数据进行排序，`PROC PRINT` 程序中添加了一个 `PROC SORT` 步骤。`PROC SORT` 步骤使用 `KEEP=` 选项对观测值进行子集划分，这提高了效率。`PROC SQL` 步骤使用 `ORDER BY` 子句排序并使用 `WHERE` 子句进行划分。在这种情况下，`PROC PRINT` 程序和 `PROC SQL` 程序的 CPU 和内存使用大致相同。

# 比较数据汇总工具

## 概述

SAS 提供了多种汇总数据的工具。这些汇总工具生成的输出相似但并不相同，且它们的效率各不相同。注意：在本节中，对 `MEANS` 过程的所有引用也适用于 `SUMMARY` 过程。

| 工具 | 说明 |
| --- | --- |
| `MEANS` 过程或 `SUMMARY` 过程 | - 计算数值变量的描述性统计<br>- 可以生成打印报告并创建输出数据集 |
| `TABULATE` 过程 | - 以表格形式生成描述性统计<br>- 可以生成带有描述性统计的 1、2 或 3 维表格<br>- 也可以创建输出数据集 |
| `REPORT` 过程 | - 将 `PRINT`、`MEANS` 和 `TABULATE` 过程的功能与 `DATA` 步骤的功能结合到单一报告编写工具中，可以生成各种报告<br>- 也可以创建输出数据集 |
| `SQL` 过程 | - 计算一个或多个 SAS 数据集或 DBMS 表的描述性统计<br>- 可以生成打印报告或创建 SAS 数据集 |
| `DATA` 步骤 | - 可以生成打印报告<br>- 也可以创建输出数据集 |

注意：还可以使用 `FREQ` 和 `UNVARIATE` 过程生成汇总数据报告，但本章未涵盖这些过程。有关这些汇总工具的任何一个的更多信息，请参阅《Base SAS Procedures Guide》中 `PROC FREQ` 和 `PROC UNIVARIATE` 的 SAS 文档。这些工具中的任何一个都可以汇总整个数据集，或按一个或多个类变量的任意组合进行汇总。要对数据分组，`PROC MEANS`、`PROC SUMMARY` 和 `PROC TABULATE` 使用 `CLASS` 语句。`PROC SQL` 使用 `GROUP BY` 子句。除 `PROC SQL` 之外的所有工具都接受 `BY` 语句。

## 跨汇总工具的资源使用比较

在对一个或多个类变量汇总数据时，以下组中的工具在资源使用上是类似的：

- `PROC MEANS`（或 `PROC SUMMARY`）、`PROC REPORT` 和 `PROC TABULATE`
- `PROC SQL` 和带有 `PROC SORT` 的 `DATA` 步骤

然而，这两组工具的相对效率可能会根据 `CLASS` 变量的值而变化。你需要用你的数据测试这些技术。

## 对比示例：显示单个类变量的汇总统计

## 概述

假设你想通过计算每个类变量 `Order_Type` 取值的销售产品平均数量来汇总 `Retail.Orders` 数据集。你可以使用多种技术来生成汇总报告。以下程序比较了五种技术。你可以将这些示例作为创建基准程序的模型。你的结果可能取决于数据结构、运行环境以及可用资源。

### 编程技术

| ![1](img/callout01.png) `PROC MEANS` | 此 `PROC MEANS` 步骤创建一个报告，显示类变量 `Order_Type` 每个值的分析变量平均值。
```
proc means data=retail.orders
     (keep=order_type quantity)
     meand=2;
class order_type;
var quantity;
run;
``` |
| ![2](img/callout02.png) `PROC REPORT` | 此 `PROC REPORT` 步骤创建一个报告，显示类变量 `Order_Type` 每个值的分析变量平均值。
```
proc report data=retail.orders
     (keep=order_type quantity);
column order_type quantity;
define order_type / group width=13
          'Order Type';
define quantity / mean format=5.2
          'Average Quantity'
          width=8;
run;
``` |
| ![3](img/callout03.png) `PROC SORT` 和 `DATA` 步骤 | 此程序使用 `PROC SORT` 步骤和 `DATA` 步骤创建一个报告。`PROC SORT` 步骤对数据排序，保留必要的变量并生成临时输出数据集 `Orders`。`DATA` 步骤计算 `Order_Type` 每个值的分析变量 `Quantity` 的平均值，并在报告中显示这些值。
```
proc sort data=retail.orders
     (keep=order_type quantity)
     out=orders;
   by order_type;
run;

data _null_;
   set orders;
   by order_type;
   format average_order 5.2;
   if first.order_type then do;
      num=0;
      sum=0;
   end;
   num+1;
   sum+quantity;
   if last.order_type then do;
      average_order=sum / num;
      file print;
      put @5 'Order Type' @20 'Average Order';
      put;
      put @13 order_type 1\. @27 average_order 5.2;
   end;
run;
``` |
| ![4](img/callout04.png) `PROC SQL` | 此 `PROC SQL` 步骤创建一个报告显示分组变量 `Order_Type` 每个值的分析变量平均值。
```
proc sql;
   select order_type,
     avg(quantity) label='Average Order'
                   format=5.2
     from retail.orders
     group by order_type;
quit;
``` |
| ![5](img/callout05.png) `PROC TABULATE` | 此 `PROC TABULATE` 步骤创建一个报告，显示类变量 `Order_Type` 每个值的分析变量平均值。
```
proc tabulate data=retail.orders
     (keep=order_type quantity)
     format=comma8.2;
class order_type;
var quantity;
table order_type, quantity*mean;
run;
``` |

### 一般建议





- 当对单个类变量进行数据汇总时，请测试您的数据以确定哪种汇总工具效率最高。

## 使用 PROC MEANS 显示类变量组合的汇总统计

要为类变量的组合生成汇总统计数据，你可以通过以下方式使用 `PROC MEANS`。这些技术在资源使用上有所不同。

| 类变量组合 | 技术 | 示例 |
| --- | --- | --- |
| 所有可能的组合：abca * ba * cb * ca * b * c | 基础 `PROC MEANS` 步骤 | |

```
proc means data=lib.dataset mean;
   class a b c;
   var salary;
   output out=summary1 
          mean=average;
run;
```
| 特定组合：a * b 和 a * c | `PROC MEANS` 中的 `TYPES` 语句 | |

```
proc means data=lib.dataset mean;
   class a b c;
   var salary;
   types a*b a*c;
   output out=summary2 
          mean=average;
run;
```
| 特定组合：a * b 和 a * c | 多个 `PROC MEANS` 步骤中的 `NWAY` 选项 | |

```
proc means data=lib.dataset nway;
   class a b;
   var salary;
   output out=summary3a 
          mean=average;
run;

proc means data=lib.dataset nway;
   class a c;
   var salary;
   output out=summary3b
          mean=average;
run;
```
| 特定组合：a * b 和 a * c | `PROC MEANS` 中 `OUTPUT` 语句的 `WHERE=` 选项 | |

```
proc means data=lib.dataset;
   class a b c;
   var salary;
   output out=summary4
          (where=(_type_ in (5,3)))
          n=employees
          mean=average;
run;
```

## 三种 PROC MEANS 技术的资源使用

汇总特定类变量组合数据的三种技术（基础 `PROC MEANS` 步骤之外）在资源使用上如下：

- `PROC MEANS` 步骤中的 `TYPES` 语句使用的资源最少。
- 包含多个 `PROC MEANS` 步骤并带有 `NWAY` 选项的程序使用的资源最多，因为 SAS 必须为每个 `PROC MEANS` 步骤单独读取数据集。单个 `PROC MEANS` 步骤中的 `NWAY` 选项是高效的。
- `PROC MEANS` 步骤中的 `WHERE=` 数据集选项使用的资源比 `PROC MEANS` 中的 `TYPES` 语句，因为 SAS 在子集之前必须计算类变量的所有可能组合。然而，`PROC MEANS` 中的 `WHERE=` 数据集选项使用的资源少于多个 `PROC MEANS` 步骤中的 `NWAY` 选项。

我们将学习如何使用基础 `PROC MEANS` 步骤以及上述列出的其他三种技术。

## 使用基础 PROC MEANS 步骤合并所有类变量

`PROC MEANS`（或 `PROC SUMMARY`）会创建：

- 一个输出报告，对数据分组并显示所有类变量组合的汇总统计。这是默认操作。
- 如果出现 `OUTPUT` 语句，`PROC MEANS` 会创建一个输出数据集，包含所有 `n` 个类变量的可能组合（从 1 维到 `n` 维）以及整个整个数据集的汇总统计数据。

## 示例：显示类变量所有组合的汇总统计

假设你想计算平均员工薪资，并根据三个类变量 `Employee_Country`、`Department` 和 `Employee_Gender` 的组合对结果分组。以下 `PROC MEANS` 程序同时创建了一个报告数据集和一个 SAS 数据集：

```
proc means data=company.organization_dim mean;
   class employee_country department 
         employee_gender;
   var salary;
   output out=summary mean=average;
run;
```

报告显示了三个类变量每种组合的汇总统计。下方显示了部分报告：![Analysis Variable: Salary](img/m85-35-g1.png) 输出数据集包含以下内容的汇总统计数据：

- 三个类变量的所有可能组合（1 维、2 维和 3 维）：
    - `Employee_Gender`
    - `Department`
    - `Employee_Country`
    - `Department` 和 `Employee_Gender`
    - `Employee_Country` 和 `Employee_Gender`
    - `Employee_Country` 和 `Department`
    - `Employee_Country` 和 `Department` 和 `Employee_Gender`
- 整个数据集

输出数据集的部分视图所示：![partial output](img/m85-35-g2.png)

## 理解 Types

用于 `PROC MEANS` 计算和分组统计的每种类变量组合被称为一个 `type`（类型）。例如，以下基础 `PROC MEANS` 步骤指定了三个类变量 `a`、`b` 和 `c`：

```
proc means data=lib.dataset mean;
   class a b c;
   var salary;
   output out=summary1 
          mean=average;
run;
```

此 `PROC MEANS` 步骤生成七种可能的类型（三个变量的组合）：

| 组合变量 | 维度 |
| --- | --- |
| `a` | 1-way |
| `b` | 1-way |
| `c` | 1-way |
| `b * c` | 2-way |
| `a * b` | 2-way |
| `a * c` | 2-way |
| `a * b * c` | 3-way

`_TYPE_` 变量为 `PROC MEANS` 中的每种类变量组合分配一个唯一的值，基于 `CLASS` 语句中的顺序。例如：

| `_TYPE_` 值 | 组合描述 | 维度 |
| --- | --- | --- |
| 1 | 仅右侧变量 | 1-way |
| 2 | 仅中间变量 | 1-way |
| 3 | 右侧和中间变量 | 2-way |
| 4 | 左侧变量 | 1-way |
| 5 | 左侧和右侧变量 | 2-way |
| 6 | 左侧和中间变量 | 2-way |
| 7 | 三者变量组合 | 3-way |

随着类变量数量的增加，类型的数量也会增加。然而，上述示例中的七种类型包含了类变量的组合。![types](img/m85-36-g2.png) 输出数据集中的第一个观测值的 `_TYPE_` 值为 0，表示为整个数据集生成统计。默认情况下，`PROC MEANS` 生成的数据集包含每个类型中类变量值的每个唯一组合的单独观测值。类型中的每个唯一值组合被称为该类型的 level（级别）。在上述输出的数据集中，类型 2 有 17 个 level。因此，17 个观测值的 `_TYPE_` 值为 2。`PROC MEANS` 生成的报告仅包含组合。

## 使用 TYPES 语句合并类变量

`TYPES` 语句指定类变量的所需组合。使用 `TYPES` 语句时需要 `CLASS` 语句。

`TYPES` 语句的通用形式：`TYPES request(s);` 语法说明如下：`request(s)` 指定类变量的组合或组合。请求包括：

- 单个类变量名
- 用星号分隔的多个类变量名
- `( )` 请求总体结果（`_TYPE_=0`）

为了更简洁地请求类变量组合，可以使用分组语法，将多个变量括起来并与其他变量或变量组合连接。以下 `TYPES` 语句示例说明了分组语法的使用：

| 使用分组语法的示例 | 等效的未使用分组语法的示例 |
| --- | --- |
| ```sas
types a*(b c);
``` | ```sas
types a*b a*c;
``` |
| ```sas
types (a b)*(c d);
``` | ```sas
types a*c a*d b*c b*d;
``` |
| ```sas
types (a b c)*d;
``` | ```sas
types a*d b*d c*d;
``` |
| ```sas
types () a*(b c);
``` | |





```
types a*b*c a*b a*c;
```

## 示例：在 PROC MEANS 中使用 TYPES 

假设你想像上一个示例一样计算员工的平均薪水。这次，你想要下面的两个类变量组合：

- `Employee_Country` 和 `Department`
- `Employee_Country` 和 `Employee_Gender`

要实现这一点，你可以在 `PROC MEANS` 步骤中添加 `TYPES` 语句：

```
proc means data=company.organization_dim mean;
   class employee_country department 
         employee_gender;
   var salary;
   types employee_country*department
         employee_country*employee_gender;
   output out=summary mean=average;
run;
```

此 `PROC MEANS` 步骤会生成一个报告数据集和一个输出数据集。下所示报告为 `TYPES` 语句中指定的两种组合中的每一个提供了一个单独的表格：![分析变量：工资年薪](img/m85-37-g1.png) 输出数据集仅包含 `TYPES` 语句中指定的组合。输出数据集的部分视图所示：![部分输出](img/m85-37-g2.png)

## 在 PROC MEANS 中使用 NWAY 选项合并类变量

指定类变量组合另一种方法是使用 `PROC MEANS` 中的 `NWAY` 选项：

| `PROC MEANS` 语句中 `NWAY` 选项的通用形式：`PROC MEANS NWAY;` | 语法说明：`NWAY` 指定输出数据集包含所有指定类变量组合的统计信息（仅具有最高 `_TYPE_` 值的观测值）。 | `NWAY` 选项为所有类变量的每种组合生成摘要统计。因此，为了为不同的类变量组合生成统计信息，可以为每个组合指定一个单独的带有 `PROC MEANS` 步骤。 |

## 示例：在多个 PROC MEANS 步骤中使用 NWAY 选项

假设你想计算员工的平均薪水，并对以下类变量组合的结果分组：

- `Employee_Country` 和 `Department`
- `Employee_Country` 和 `Employee_Gender`

你可以使用两个 `PROC MEANS` 步骤，每个步骤都包含 `NWAY` 选项，如下所示。第一个 `PROC MEANS` 步骤为第一种类变量组合生成统计信息，第二个 `PROC MEANS` 步骤为第二种类变量组合生成统计信息。

```
proc means data=company.organization_dim nway;
   class employee_country department;
   var salary;
   output out=summary1
          n=employees
          mean=average;
run;

proc means data=company.organization_dim nway;
   class employee_country  employee_gender;
   var salary;
   output out=summary2
          n=employees
          mean=average;
run;
```

在处理此程序时，SAS 为每个 `PROC MEANS` 步骤读取一次数据集。这种处理效率不高。该程序生成两个报告和两个输出数据集。部分所示报告为每个 `PROC MEANS` 步骤提供了一个单独的表格：![分析变量：工资年薪](img/m85-38-g1.png)![部分输出](img/m85-38-g2.png) 每个输出数据集的部分视图所示：图 23.2 SAS 数据集 Work.Summary1![数据集 Work.Summary1](img/m85-38-g3.png)图 23.3 SAS 数据集 Work.Summary2![SAS 数据 Work.Summary2](img/m85-38-g4.png)

## 在 PROC MEANS 中使用 WHERE= 输出数据集选项选择所需的类型

选择所需类型的另一种方法是使用 `OUTPUT` 语句中的 `WHERE=` 输出数据集选项：

| 基础 `OUTPUT` 语句中 `WHERE=` 输出数据集选项的通用形式：`OUTPUT <OUT=SAS-data-set> (WHERE=(where-expression-1 <logical-operator where-expression-n>));` | 语法说明：`SAS-data-set` 指定输出数据集的 1 层或 2 层名称。`where-expression` 是算术或逻辑表达式，由运算符、操作数和 SAS 函数序列组成。该表达式必须括在括号内。`logical-operator` 可以是 AND、AND NOT、OR 或 OR NOT。 |

当你在 `OUTPUT` 语句中使用 `WHERE=` 输出数据集选项时，SAS 必须计算类变量的所有可能组合。在结果写入输出数据集之前不会进行子集划分。

## 示例：在 PROC MEANS 中使用 WHERE= 输出数据集选项

假设你想计算员工平均薪水，并为三个类变量 `Employee_Country`、`Department` 和 `Employee_Gender` 的两个双向组合选择结果。这些变量的所有可能组合列如下：

| `_TYPE_` 值 | 组合变量 | 维度 |
| --- | --- | --- |
| 1 | `Employee_Gender` | 1 向 |
| 2 | `Department` | 1 向 |
| 3 | `Department * Employee_Gender` | 2 向 |
| 4 | `Employee_Country` | 1 向 |
| 5 | `Employee_Country * Employee_Gender` | 2 向 |
| 6 | `Employee_Country * Department` | 2 向 |
| 7 | `Employee_Country * Department * Employee_Gender` | 3 向 |

要通过 `_TYPE_` 值指定类型，你可以如下所示在 `OUTPUT` 语句中使用 `WHERE=` 输出数据集选项：

```
proc means data=company.organization_dim;
   class employee_country department 
         employee_gender;
   var salary;
   output out=summary 
          (where=_type_ in (5,6))
          n=employees
          mean=average;
run;
```

报告的部分所示。`PROC MEANS` 报告代表最高类型，即 `NWAY` 组合类型 7，这并不是请求的![部分输出](img/m85-39-g1.png) 输出数据集 Work.Summary 部分视图所示。数据集包含了请求的类型 5 和 6![Work.Summary](img/m85-39-g2.png)

## 比较示例：显示类变量组合的摘要统计

## 概述

假设你想通过计算四个类变量的两个三向组合的员工平均薪水来汇总 `Retail.Organization` 数据集：

- `Employee_Country`、`Department` 和 `Employee_Gender`
- `Department`、`Section` 和 `Employee_Gender`

你可以使用多种技术来生成报告和多个输出数据集。以下程序比较了三种技术。你可以将这些示例作为在你自己的环境中创建基准程序的模型。

### 编程技术

| ![1](img/callout01.png) PROC MEANS 中的 TYPES 语句 | 此程序计算类变量 `Employee_Country`、`Department` 和 `Employee_Gender` 的两个三向组合的平均薪水。`TYPES` 语句请求了这两个组合。程序生成一个报告和一个名为 `Summary` 的输出数据集。```
proc means data=retail.organization mean;
   class employee_country department
         employee_gender section;
   var salary;
   types employee_country*department*employee_gender
         department*section*employee_gender;
   output out=summary
          n=employees
          mean=average;
run;``` | ![2](img/callout02.png) 多个 PROC MEANS 步骤中的 NWAY 选项 | 此程序的两个 `PROC MEANS` 步骤分别为四个类变量 `Employee_Country`、`Department` 和 `Section` 的三向组合计算平均薪水。在每个步骤中，`NWAY` 选项指定 `CLASS` 语句中指定的三个变量进行组合。程序生成两个报告和名为 `Summary1` 和 `Summary2` 的两个输出数据集。```
proc means data=retail.organization nway;
   class employee_country department;
   var salary;
   output out=summary1
          n=employees
          mean=average;
run;

proc means data=retail.organization nway;
   class employee_country  employee_gender;
   var salary;
   output out=summary2
          n=employees
          mean=average;
run;
``` |




```
proc means data=retail.organization nway;
   class employee_country department
         employee_gender;
   var salary;
   output out=summary1
          n=employees
          mean=average;
run;

proc means data=retail.organization nway;
   class department section
         employee_gender;
   var salary;
   output out=summary2
          n=employees
          mean=average;
run;
```

| ![3](img/callout03.png) WHERE= Option in PROC MEANS 此程序计算了类变量 Employee_Country、Department、Employee_Gender 和 Section 的两种三路组合的平均员工薪资。`OUTPUT` 语句中的 `WHERE=` 数据集通过其 `TYPE` 值指定了这两个组合。该程序生成了一个报告和一个名为 Summary3 的输出数据集。 |

```
proc means data=retail.organization;
   class employee_country department
         employee_gender section;
   var salary;
   output out=summary3 (where=(_type_ in (7,14)))
          n=employees
          mean=average;
run;
```

### 通用建议

- 要为类变量的特定组合汇总数据，请使用 `PROC MEANS` 中的 `TYPES` 语句。

### 附加功能

`PROC MEANS` 中的 `WAYS` 语句提供了另一种显示类变量组合的摘要统计量的方法。在 `WAYS` 语句中，您指定一个或多个整数，用于定义组合类变量的数量，以形成类变量的所有唯一组合。例如，以下程序使用 `WAYS` 语句为三个类变量 `Employee_Country`、`Department` 和 `Employee_Gender` 的以下组合创建摘要统计量：

- 每个单独变量（所有 1 路组合）
- 所有 2 路组合（`Employee_Country` 与 `Department`、`Employee_Country` 与 `Employee_Gender` 以及 `Employee_Gender` 与 `Department`）

```
proc means data=company.organization mean;
   class employee_country department
         employee_gender;
   var salary;
   ways 1 2;
   output out=summary
          mean=average;
run;
```

`WAYS` 语句可以替代 `TYPES` 语句，也可以与其结合使用。注意：有关关于 `WAYS` 语句的更多信息，请参阅 SAS 文档。

## 总结

## 使用索引进行高效 WHERE 处理

在处理 `WHERE` 表达式时，SAS 会确定是顺序访问（通过检查所有观测值）还是直接访问（使用索引访问特定观测值）更高效。使用索引处理 `WHERE` 表达式可能会提高性能，这被称为优化 `WHERE` 表达式。通过决定是否创建索引，您决定了 SAS 可以使用何种访问方法。为了决定是否使用索引，您必须评估使用索引的收益和成本。SAS 会执行一系列步骤，以确定是使用索引处理 `WHERE` 表达式还是按顺序读取所有观测值。

## 识别可用索引

首先，SAS 确定是否存在可以用于处理 `WHERE` 表达式的现有索引。具体而言，SAS 会检查 `WHERE` 表达式中每个条件中的变量，以确定该变量是简单索引中的键变量，还是复合索引中的第一个键变量。无论有多少可用索引，SAS 只能使用一个索引来处理 `WHERE` 表达式。因此，如果存在多个索引，SAS 必须在它们之间进行选择。最常见的情况是 SAS 使用索引仅处理 `WHERE` 表达式中的一个条件。然而，在名为“复合优化”的过程中，SAS 可以使用复合索引优化多个变量上的多个条件，这些条件是使用 `AND` 等逻辑运算符连接的。

## 识别可优化的条件

其次，SAS 在包含键变量的 `WHERE` 条件中寻找可以被优化的运算符和函数。也有某些运算符和函数是无法优化的。对于复合优化，`WHERE` 条件必须满足略有不同的标准才能成为优化候选。

## 估算观测值数量

第三，SAS 估计符合索引的观测值数量。当存在多个索引时，SAS 会选择似乎产生最少符合观测值（最小子集）的索引。SAS 是否使用索引取决于符合观测值的百分比（子集相对于数据集的大小）。对于小子集使用直接访问、对于大子集使用顺序访问更高效。如果 SAS 估计符合观测值少于数据文件的 3%，它将自动使用索引，而不比较可能的资源使用情况。为了帮助 SAS 估计 `WHERE` 表达式将选择多少观测值，每个索引都存储了 21 个称为累积百分位数（centiles）的统计数据。分位数提供了有关索引变量值分布的信息。

## 比较可能的资源使用情况

第四，SAS 决定使用索引还是顺序读取所有观测值来满足 `WHERE` 表达式更高效。为了做出决定，SAS 会预测每种访问方法满足 `WHERE` 表达式需要多少 I/O 操作，然后比较两种资源成本。影响 `WHERE` 处理所需的 I/O 操作数量的因素包括：

- 子集大小相对于数据集的大小
- 数据文件中的页数
- 数据顺序
- 顺序读取压缩文件的代价

数据类型和长度是影响索引效率的两个因素。

### 决定是否创建索引

当您使用 `WHERE` 表达式选择子集时，可以使用特定指南决定创建索引是否高效。取决于子集相对于数据集的大小等因素，您可能会选择或不创建索引。在大多数情况下，让 SAS 决定是否对 `WHERE` 使用索引是。但有时您可能希望控制 SAS 使用现有索引。可以使用数据集选项 `IDXWHERE=` 或 `IDXNAME=` 中的任意一个，但不能同时使用。您可以指定 `MSGLEVEL=I` 以让 SAS 在日志中显示索引使用信息。

## 比较生成详细报告的过程

当您生成详细报告时，可以在 `PRINT` 过程和 `SQL` 过程之间进行选择。为了执行特定任务，单用途工具如 `PROC PRINT` 通常比多功能工具如 `PROC SQL` 使用更少的资源。对于详细报告，`PROC PRINT` 步骤通常（并非总是）比 `PROC SQL` 步骤消耗更少：

- 生成简单详细报告、子集详细报告和排序详细报告时，`PROC PRINT` 比 `PROC SQL` 更高效。
- `PROC PRINT` 和 `PROC SQL` 在生成排序子集详细报告时可能消耗相似。

## 数据汇总工具比较

SAS 提供了多种汇总工具，包括 `MEANS` 过程（或 `SUMMARY` 过程）、`TABULATE` 过程、`REPORT` 过程、`SQL` 过程和 `DATA` 步骤。如果您为一个类变量汇总数据，以下组工具的资源使用是相似的：

- `PROC MEANS`（或 `PROC SUMMARY`）、`PROC REPORT` 和 `PROC TABULATE`
- `PROC SQL` 和 `DATA` 步骤




然而，这两组工具的相对效率取决于数据的形状。你可以以多种方式使用 `PROC MEANS` 为类变量（class variables）的组合生成摘要统计。每个类变量的组合被称为一个类型（type）。要对所有类变量的所有组合进行数据汇总，你可以使用基础的 `PROC MEANS` 步骤（或 `PROC SUMMARY` 步骤）。要为特定的类变量组合生成摘要统计，你可以按以下方式使用 `PROC MEANS`：

*   `PROC MEANS` 步骤中的 `TYPES` 语句
*   多个 `PROC MEANS` 步骤中的 `NWAY` 选项
*   `PROC MEANS` 步骤中的 `WHERE=` 输出数据集选项

这三种技术的效率各不相同；`PROC MEANS` 中的 `TYPES` 语句效率最高。你也可以使用 `PROC MEANS` 中的 `WAYS` 语句来为特定的类变量组合生成摘要统计。

# 测验

为每个问题选择一个最佳答案。完成测验后，请使用附录中的答案页检查你的答案。

1. 为什么使用索引可以减少访问较小子集所需的 I/O 操作次数？
    1. 使用索引需要更大的 I/O 内存缓冲区，它可以容纳更多页面。
    2. 索引不需要加载到内存缓冲区中。
    3. SAS 必须加载到程序数据向量 (`PDV`) 中的观测值数量减少了。
    4. SAS 必须加载到 I/O 缓冲区中的页面减少了。

2. 你想从数据集 `Company.Products` 中选择观测值的子集，并且你已经在变量 `Rating` 上定义了一个简单索引。SAS 无法使用索引处理以下哪个 `WHERE` 语句？
    1. ```sas
       where rating is missing;
       ```
    2. ```sas
       where rating=int(rating);
       ```
    3. ```sas
       where rating between 3.5 and 7.5;
       ```
    4. ```sas
       where rating=5.5;
       ```

3. 在以下情况下，顺序访问在 `WHERE` 处理中可能比直接访问更高效？
    1. 子集包含数据集中 75% 以上的观测值。
    2. `WHERE` 表达式在单个复合索引中指定了两个键变量。
    3. 数据已按键变量排序。
    4. 数据集非常大。

4. 你想汇总数据并按一个变量进行分组。以下哪个工具不能？
    1. 带有 `BY`-组处理的 `DATA` 步骤。
    2. 不带 `BY`-组处理的 `DATA` 步骤。
    3. 带有 `GROUP BY` 子句的 `PROC SQL`。
    4. 带有 `CLASS` 语句的 `PROC MEANS`。

5. 下哪些技术没有为类变量的特定组合汇总数据？
    1. 多个 `PROC MEANS` 步骤中的 `NWAY` 选项。
    2. `PROC MEANS` 步骤中的 `TYPES` 语句。
    3. `PROC MEANS` 步骤中的 `WHERE=` 输出数据集选项。
    4. 基础的 `PROC MEANS` 步骤。

# 第 24 章：使用 PROC FCMP 创建函数

## 概述

## 引言

SAS 函数编译器 (`FCMP`) 过程允许你创建、测试和存储用户定义的函数、`CALL` 例和子程序，以供其他 SAS 过程和 `DATA` 步骤使用。

# 使用 PROC FCMP

## 概述

`FCMP` 过程使用 SAS 语言编译器来创建用户定义的函数。编译器子系统为运行 SAS 的计算机生成机器语言代码。你可以在 `PROC FCMP` 中创建的函数和子程序可以用于 `DATA` 步骤、`WHERE` 语句、输出交付系统 (`ODS`) 以及以下过程：

| `PROC CALIS` | `PROC OPTLSO` |
| :--- | :--- |
| `PROC GA` | `PROC QUANTREG` |
| `PROC GENMOD` | `PROC REPORT` COMPUTE 块 |
| `PROC GLIMMIX` | SAS Risk Dimensions 过程 |
| `PROC MCMC` | `PROC SEVERITY` |
| `PROC MODEL` | `PROC SIMILARITY` |
| `PROC NLIN` | `PROC SQL` (不支持带有数组参数的函数) |
| `PROC NLMIXED` | `PROC SURVEYPHREG` |
| `PROC NLP` | `PROC VARMAX` |

## 编写 PROC FCMP 步骤

以下是 `PROC FCMP` 的语法：

创建和保存函数的基础 `PROC FCMP` 步骤的一般形式：
```sas
PROC FCMP OUTLIB= libref.data-set.package;
Function function-name(argument-1<$>,...,argument-n<$><length>);
```

`OUTLIB=` 选项指定存储编译函数的包。`PROC FCMP` 语句开始 `FCMP` 步骤。必须指定 `OUTLIB=` 。

`FUNCTION` 语句开始定义函数并以 `ENDSUB` 语句结束。下面的示例创建了一个名为 `ReverseName` 的函数。

```sas
proc fcmp outlib=orion.functions.dev;
function ReverseName(name $) $40;
```

`RETURN` 语句指定函数的返回值。

```sas
return(catx('',scan(name,2,','),scan(name,1,)));
```

# 关于 PROC FCMP

`FCMP` 过程使用 SAS 语言编译器创建用户定义的函数。编译器子系统为运行 SAS 的计算机生成机器语言代码。你可以在 `PROC FCMP` 中创建的函数和子程序用于 `DATA` 步骤、`WHERE` 语句、输出交付系统 (`ODS`) 以及以下过程：

| `PROC CALIS` | `PROC OPTLSO` |
| :--- | :--- |
| `PROC GA` | `PROC QUANTREG` |
| `PROC GENMOD` | `PROC REPORT` 块 |
| `PROC GLIMMIX` | Risk Dimensions 过程 |
| `PROC MCMC` | `PROC SEVERITY` |
| `PROC MODEL` | `PROC SIMILARITY` |
| `PROC NLIN` | `PROC SQL` (不支持带有数组参数的函数) |
| `PROC NLMIXED` | `PROC SURVEYPHREG` |
| `PROC NLP` | `PROC VARMAX` |

# PROC FCMP 语句

`PROC FCMP` 语句开始 `FCMP` 步骤。`OUTLIB=` 选项指定存储编译函数的包。函数和子程序名称在包内必须是唯一的。

```sas
proc fcmp outlib=orion.functions.dev;
```

# FUNCTION 语句

`FUNCTION` 语句开始定义函数并以 `ENDSUB` 语句结束。下面的示例创建了一个名为 `ReverseName` 的函数。

```sas
function ReverseName(name $) $40;
```

# RETURN 语句

`RETURN` 语句指定函数的返回值。

```sas
return(catx('',scan(name,2,','),scan(name,1,)));
```

# 使用定义的函数

为了在 `DATA` 步骤或支持的 `PROC` 步骤中使用新函数，必须指定 `CMPLIB=` 系统选项。`CMPLIB=` 选项指定一个或多个存储用户定义的函数。在这个示例中，函数 `ReverseName` 保存到 `orion.functions`。

```sas
options cmplib=orion.functions;
```

在以下代码中调用函数 `ReverseName`：

```sas
options cmplib=orion.functions;
data work.emplist;
    set orion.employeeaddresses;
    NewName=ReverseName(EmployeeName);
run;
```

# 使用 PROC FCMP 创建子程序

`ROUTINE` 语句命名处理的代码块并指定参数。`OUTARGS` 语句指定子程序更新的参数。在下面的示例中，子程序 `CALC_YEARS` 用于从日期变量计算到期时间（years）：

```sas
subroutine calc_years(maturity, current_date, years);
   outargs years;
   years=(maturity - current_date) / 365.25;
endsub;
```

下面的代码是调用 `CALC_YEARS` 子程序的示例：

```sas
data _null_;
  myCD='23jul2017'd;
  now=today();
  how_many_years=.;
  call calc_years(myCD,now,how_many_years);
  put how_many_years=;
run;
```

# 测验

为每个问题选择一个最佳答案。完成测验后，请使用附录中的答案页检查你的答案。

1. 为什么使用索引可以减少访问较小子集所需的 I/O 操作次数？
    1. 使用索引需要更大的 I/O 内存缓冲区，它可以容纳更多页面。
    2. 索引不需要加载到内存缓冲区中。
    3. SAS 必须加载到程序数据向量 (`PDV`) 中的观测值数量减少了。
    4. SAS 必须加载到 I/O 缓冲区中的页面减少了。

2. 你想从数据集 `Company.Products` 中选择观测值的子集，并且你已经在变量 `Rating` 上定义了一个简单索引。SAS 无法使用索引处理以下哪个 `WHERE` 语句？
    1. ```sas
       where rating is missing;
       ```
    2. ```sas
       where rating=int(rating);
       ```
    3. ```sas
       where rating between 3.5 and 7.5;
       ```
    4. ```sas
       where rating=5.5;
       ```

3. 在以下情况下，顺序访问在 `WHERE` 处理中可能比直接访问更高效？
    1. 子集包含数据集中 75% 以上的观测值。
    2. `WHERE` 表达式在单个复合索引中指定了两个键变量。
    3. 数据已按键变量排序。
    4. 数据集非常大。

4. 你想汇总数据并按一个变量进行分组。以下哪个工具不能？
    1. 带有 `BY`-组处理的 `DATA` 步骤。
    2. 不带 `BY`-组处理的 `DATA` 步骤。
    3. 带有 `GROUP BY` 子句的 `PROC SQL`。
    4. 带有 `CLASS` 语句的 `PROC MEANS`。

5. 下哪些技术没有为类变量的特定组合汇总数据？
    1. 多个 `PROC MEANS` 步骤中的 `NWAY` 选项。
    2. `PROC MEANS` 步骤中的 `TYPES` 语句。
    3. `PROC MEANS` 步骤中的 `WHERE=` 输出数据集选项。
    4. 基础的 `PROC MEANS` 步骤。





| 特性 | `FUNCTION` | `SUBROUTINE` |
| :--- | :---: | :---: |
| 接受参数 | 是 | 是 |
| 修改参数 | 否 | 是 |
| 返回值 | 是 | 否 |
| 是表达式 | 是 | 否 |
| 是语句 | 否 | 是 |
| 可以作为语句的一部分 | 是 | 是（等等，不是，`CALL` 是语句） |
| 以 `CALL` 开头 | 否 | 是 |

有关 `PROC FCMP` 的更多信息，请参阅《Base SAS 过程指南》中的“PROC FCMP”。

# 测验

为每个问题选择最佳答案。完成测验后，请使用附录中的答案对照检查您的答案。

1. 下列特征不适用于子程序（subroutines）的是？
    1. 参数按值传递。
    2. `ENDSUB` 语句结束子程序的定义。
    3. 可以修改参数。
    4. 不返回结果。

2. 你可以在单个 `FCMP` 过程步骤中创建一个函数和一个 `CALL` 例程。
    2. 正确
    2. 错误

3. `OUTLIB=` 选项是 `PROC FCMP` 函数中的必要选项。
    1. 正确
    2. 错误

4. `OUTARGS` 语句与 `FUNCTION` 和 `SUBROUTINE` 语句配合使用。
    1. 正确
    2. 错误

# 附录 1：测验答案

第 1 章：使用 PROC SQL 执行查询第 2 章：使用 PROC SQL 执行高级查询第 3 章：使用 PROC SQL 水平合并表第 4 章：使用 PROC SQL 垂直合并表第 5 章：使用 PROC SQL 创建和管理表第 6 章：使用 PROC SQL 创建和管理索引第 7 章：使用 PROC SQL 创建和管理视图第 8 章：使用 PROC SQL 管理处理第 9 章：宏变量介绍第 10 章：执行时处理宏变量第 11 章：创建和使用宏程序第 12 章：存储宏程序第 13 章：创建索引第 14 章：垂直合并数据第 15 章：水平合并数据第 16 章：使用查找表匹配数据第 17 章：数据格式化第 18 章：修改 SAS 数据集并跟踪更改第 19 章：高效 SAS 编程介绍第 20 章：控制内存使用第 21 章：控制数据存储空间第 22 章：使用最佳实践第 23 章：高效查询数据第 24 章：使用 PROC FCMP 创建函数

# 第 1 章：使用 PROC SQL 执行查询

1. 正确答案：a 程序中的 `SELECT` 子句编写错误。子句中列出的列必须用逗号分隔，而不仅仅是空格。

2. 正确答案：a 有两个语句，`PROC SQL` 语句和 `SELECT` 语句。`SELECT` 语句包含三个子句。

3. 正确答案：b `SELECT` 子句列出了要查询的列。`OUTLIB=` 选项不是 `PROC FCMP` 函数的必要选项。

4. 正确答案：b `OUTARGS` 语句与 `FUNCTION` 和 `SUBROUTINE` 语句配合使用。





8. 正确答案：c 在此 `PROC SQL` 查询中，外部查询使用了带有相关子查询的 `NOT EXISTS` 运算符。外部查询选择了 `Charity.Donors` 中所有名称未出现在 `Charity.Current` 表中的行。换句话说，此 `PROC SQL` 查询的输出列出了所有今年没有进行捐赠的捐赠者。

9. 正确答案：c 关于数据重新合并（remerging）的第三条语句是正确的。

10. 正确答案：c `PROC SQL` 可以执行此查询，但查询不会产生你想要的结果。如果你在包含 `HAVING` 子句的查询中省略了 `GROUP BY` 子句，那么 `HAVING` 子句和任何汇总函数会将整个表视为一组。在没有 `GROUP BY` 子句的情况下，此示例中的 `HAVING` 子句计算的是整个表的平均循环次数（图书馆中的所有书籍），而不是每个组（每类书籍）的。输出要么包含表中的所有行（如果整个表的平均循环次数小于 2500），要么不包含表中的任何行（如果整个表的平均循环次数大于 2500）。

# 第 3 章：使用 PROC SQL 水平合并表

1. 正确答案：a 当在 `PROC SQL` 链接中未指定连接条件时，将返回笛卡尔积。在笛卡尔积中，第一表中的每一行都与第二个表中的每一行进行组合。

2. 正确答案：b 此 `PROC SQL` 查询是一个内连接（inner join）。它根据 `WHERE` 子句中指定的匹配标准，将第一表中与第二个表匹配的行组合在一起。列不会重叠，因此会显示所引用表中的所有列（包括任何重名列）。任一表中的任何未匹配的行都不会被显示。

3. 正确答案：d 此 `PROC SQL` 查询是一个右外连接（right outer join），它根据 `ON` 子句中的连接条件，检索跨表匹配的所有行，外加上右侧（第二个）表中不匹配的行。

4. 正确答案：d 编写 `PROC SQL` 内连接有两种有效格式。问题顶部显示的 `PROC SQL` 查询使用了第一种内连接格式，该格式没有使用关键字来指示连接类型。另一种格式类似于外连接，并使用了关键字 `INNER JOIN`。

5. 正确答案：a 此 `PROC SQL` 查询是一个左外连接（left outer join），它检索跨表匹配的所有行（基于 `ON` 子句中的连接条件），外加上左侧（第一个）表中不匹配的行。列不会重叠，因此会显示两个表中的所有列。

6. 正确答案：c 内连接根据 `WHERE` 子句中的一个或多个连接条件，将第一表中与第二个表匹配的行组合在一起。被匹配的列必须具有相同的数据类型，但并不要求具有相同的名称。对于连接来说，被连接的表可以具有不同数量的列，且不需要进行排序。

7. 正确答案：a 与表不同，内联视图（in-line view）仅在查询执行期间存在。由于它是临时的，内联视图只能在定义它的查询中引用。

8. 正确答案：c 为了生成与 `DATA` 和 `PRINT` 步骤相同的输出，`PROC SQL` 全外连接必须使用 `COALESCE` 函数，并将指定的重复列作为参数。

9. 正确答案：c 单个内连接最多可以合并 256 张表。如果连接涉及视图（内联视图或 `PROC SQL` 视图），则视图底层的表数量（而不是视图数量）计入 256 的限制中。

10. 正确答案：d 使用汇总函数不需要使用表别名。这里显示的所有关于表别名的其他语句都是正确的。

# 第 4 章：使用 PROC SQL 垂直合并表

1. 正确答案：c 在使用运算符 `EXCEPT`、`INTERSECT` 或 `UNION` 且没有关键字的集合操作中，列根据它们在 `SELECT` 子句中的位置进行重叠。重叠列是否具有相同名称无关。当列重叠时，列名取自 `SELECT` 子句中指定的第一个表。

2. 正确答案：d 默认情况下，在处理包含 `EXCEPT`、`INTERSECT` 和 `UNION` 集合运算符的集合操作时，`PROC SQL` 对数据进行额外扫描以消除重复行。关键字 `ALL` 用于抑制这种对表的额外扫描，允许重复行出现在结果集中。由于 `OUTER UNION` 集合运算符显示所有行，因此关键字 `ALL` 是无效的，且不能与 `OUTER UNION` 一起使用。

3. 正确答案：d 输出包含两个表合并行集中所有唯一的行，且列已根据位置进行了重叠。此输出是由一个使用集合运算符 `UNION` 且无关键字的集合操作生成的。

4. 正确答案：a 使用无关键字的集合运算符 `OUTER UNION` 的 `PROC SQL` 集合操作是显示的唯一没有在输出中重叠任何列的代码。

5. 正确答案：a 关键字 `CORRESPONDING` (`CORR`) 可以单独使用，也可以与关键字 `ALL` 一起使用。

6. 正确答案：b 此 `PROC SQL` 输出包含了 `Pets` 表中未出现在 `Dogs` 表中的所有行。不显示重复项。包含无关键字的集合运算符 `EXCEPT` 的 `PROC SQL` 集合操作产生这些结果。

7. 正确答案：b `EXCEPT` 运算符返回第一表中未出现在第二个表中的行。关键字 `ALL` 抑制 `PROC SQL` 为消除重复行而对数据的额外扫描。单独使用 `EXCEPT` 也会产生问题中指定的输出。

8. 正确答案：c 集合运算符 `UNION` 返回两个表合并行集中所有唯一的行。

9. 正确答案：c 集合运算符 `INTERSECT` 返回两个表共有的行。指定关键字 `ALL` 抑制 `PROC SQL` 为消除重复行而对数据的额外扫描。

10. 正确答案：a `DATA` 步骤返回第一表的所有行以及第二个表的所有行，并保持 `BY` 语句指定的顺序。默认情况下同名列会重叠。`OUTER UNION` 运算符返回两个表的所有行。`CORR` 关键字导致同名列重叠。

# 第 5 章：使用 PROC SQL 创建和管理表

1. 正确答案：b 包含 `LIKE` 子句的 `CREATE TABLE` 语句将现有表的列和属性复制到新表中。不插入任何数据行。

2. 正确答案：a 包含 `AS` 关键字和查询子句的 `CREATE TABLE` 语句创建一个并将查询结果加载到新表中。`WHERE` 子句选择了层级为空空乘员的行。

3. 正确答案：c `UNDO POLICY=REQUIRED` 是 `PROC SQL` 的默认设置。如果一个或多个行违反完整性约束标准，此设置将撤销所有插入或更新，并将表恢复到插入或更新之前的状态。

4. 正确答案：b `NOT NULL` 完整性约束指定数据是必须的且不能为空（缺失）值。

5. 正确答案：d `DELETE` 语句从表中删除 `WHERE` 子句指定的行。如果没有指定 `WHERE` 子句，则删除所有行。`DROP TABLE` 语句删除整个表；选项 c 中的语法无效。

6. 正确答案：b 包含 `SET` 子句的 `UPDATE` 语句用于修改表中的行。`CASE` 表达式中的 `WHEN-THEN` 子句允许你根据指定的标准更新列值。





### 7. 正确答案：a
`INSERT` 语句用于向新表或现有表插入新行。`PROC SQL` 中没有 `LOAD` 语句，`VALUES` 是子句，而 `CREATE TABLE` 语句用于创建表。

### 8. 正确答案：d
`ALTER TABLE` 语句用于修改现有列的属性（包括 `MODIFY` 子句）、添加新定义（包括 `ADD` 子句）或删除现有列（包括 `DROP` 子句）。

### 9. 正确答案：c
`DESCRIBE TABLE` 语句列指定表的列属性。

### 10. 正确答案：a
`CREATE TABLE` 语句可以包含列规范以创建一个空表。整组列规范必须封装在一个括号内。你必须列出每个列的名称、数据类型以及（对于字符列）长度。长度以括号中的整数形式指定。多个列规范之间必须用逗号分隔。

# 第 6 章：使用 PROC SQL 创建和管理索引

### 1. 正确答案：d
指定的索引基于一列，因此它是一个简单索引。在 `CREATE INDEX` 语句中，你在关键字 `CREATE INDEX` 之后指定索引名称。你不需要包含关键字来指定这是一个简单索引。键列的名称在表名后的括号中指定。简单索引的名称必须与键列的名称相同。

### 2. 正确答案：b
要创建唯一索引，需要在 `CREATE INDEX` 语句中在关键字 `CREATE` 和 `INDEX` 之间添加 `UNIQUE` 关键字。

### 3. 正确答案：d
复合索引基于两个或多个列。在 `CREATE INDEX` 语句中，你在关键字 `CREATE INDEX` 之后指定索引名称。你不需要包含关键字来指定这是一个复合索引。键列的名称在表名后的括号中指定。复合索引的名称不能与表中任何列的名称相同。

### 4. 正确答案：a
指定选项 `MSGLEVEL=I` 会导致关于索引使用的信息性消息写入 SAS 日志。

### 5. 正确答案：c
`DROP INDEX` 语句从表中删除一个或多个指定的索引。你在关键字 `DROP INDEX` 之后指定要删除的每个索引的名称。表名在关键字 `FROM` 之后指定。语句中不指定索引类型和被索引列的名称。

### 6. 正确答案：b
`DESCRIBE TABLE` 语句列出你指定的的一个或多个表的所有索引，以及关于这些表的其他信息。

### 7. 正确答案：a
`IDXWHERE=YES` 数据集选项告诉 SAS 使用最佳可用索引，即使该索引没有优化性能。

### 8. 正确答案：c
索引可以在字符列或数值列上创建。

### 9. 正确答案：d
使用索引将优化特定类别的 `PROC SQL` 查询。键列仅在 `SELECT` 子句中指出的查询不属于这些查询之一。

### 10. 正确答案：c
`IDXNAME=` 数据集选项引导 `PROC SQL` 使用你指定的索引。指定的索引必须存在，并且必须通过至少第一列或唯一列匹配 `WHERE` 表达式中的条件是有效的。

# 第 7 章：使用 PROC SQL 创建和管理视图

### 1. 正确答案：a
`PROC SQL` 视图访问最新的底层数据，并可以与表或其他视图连接。此外，`PROC SQL` 视图可以：

*   在 SAS 程序中代替实际的 SAS 数据文件
*   从一个或多个表、`PROC SQL` 视图或 `DATA` 步骤视图派生。

### 2. 正确答案：d
`PROC SQL` 视图很有用，因为它们：

*   通常可以节省空间（与其访问的数据相比，视图通常很小）
*   防止用户不断提交查询来忽略不需要的列或行
*   向用户隐藏复杂的连接或查询。

此外，`PROC SQL` 视图：

*   确保输入数据集始终是最新的，因为数据是在执行时从表中派生的。
*   可以用于向用户屏蔽敏感或机密列，同时允许这些用户查看同一表中的其他列。

### 3. 正确答案：c
你使用 `CREATE VIEW` 语句创建视图。关键字 `CREATE VIEW` 之后是视图名称和关键字 `AS`。

### 4. 正确答案：b
`DESCRIBE VIEW` 语句在 SAS 日志中显示视图定义。

### 5. 正确答案：a
你可以像使用实际的 SAS 表一样在 `PROC SQL` 步骤中使用视图。

### 6. 正确答案：d
`USING` 子句允许你在视图定义中嵌入 `LIBNAME` 语句。`USING` 子句必须是 `CREATE VIEW` 语句中的最后一个子句。

### 7. 正确答案：d
`PROC SQL` 视图可以从 SAS 数据文件、`DATA` 步骤视图、`PROC SQL` 视图或关系数据库表访问数据。

### 8. 正确答案：d
当你处理 `PROC SQL` 视图时，最好：

*   避免在视图中使用 `ORDER BY` 子句。如果你指定了 `ORDER BY` 子句，则每次引用视图都必须对数据进行排序。
*   避免创建基于结构可能会变化的表的视图。当视图引用不存在的列时，该视图将失效。
*   如果视图与贡献表位于同一个 SAS 数据库中，在 `FROM` 子句中指定单级名称。在 `FROM` 子句中使用单级名称可以防止你在为包含视图及其贡献表（或表）的 SAS 数据库分配不同的 `libref` 时必须更改视图。

### 9. 正确答案：c
你可以更新 `PROC SQL` 视图，前提是视图没有连接或链接到另一个表、视图没有子查询，或者你正尝试更新派生列。你可以更新包含 `WHERE` 子句的视图。`WHERE` 子句可以在 `UPDATE` 子句中也可以在视图中。你不能更新包含任何其他子句（如 `ORDER BY` 或 `HAVING` 子句）的视图。

### 10. 正确答案：b
`DROP VIEW` 语句从指定的库删除视图。

# 第 8 章：使用 PROC SQL 管理处理

### 1. 正确答案：a
`PROC SQL` 选项在 `PROC SQL` 语句中指定。指定选项后，它一直有效直到你更改它或重新调用 `PROC SQL`。

### 2. 正确答案：b
`INOBS=` 选项限制 `PROC SQL` 从单个源输入的行数。`INOBS=` 选项类似于 SAS 系统选项 `OBS=`，对于大表的查询很有用。`OUTOBS=` 选项限制 `PROC SQL` 显示或写入的行数。

### 3. 正确答案：c
指定选项后，它一直有效直到你更改它或重新调用 `PROC SQL`。你可以使用 `RESET` 语句在不重新调用 SQL 过程的情况下添加、删除或更改 SQL 选项。在正确答案中，`RESET` 语句添加了 `NUMBER` 选项和 `OUTOBS=` 选项。结果输出列出了 `Sasuser.Flightattendants` 表中 `Jobcode` 等于 `FA2` 的前 10 行，并包含一个名为 `Row` 的列。

### 4. 正确答案：d
`DOUBLE | NODOUBLE` 选项指定列表输出中 `PROC SQL` 输出的双倍行距。`FLOW | NOFLOW | FLOW=n | FLOW=n m` 选项控制列表输出中宽字符列。这两个选项都不影响 HTML 输出。

### 5. 正确答案：d
`PROC SQL` 中的 `STIMER | NOSTIMER` 选项指定 `PROC SQL` 是否将每个语句的计时信息写入 SAS 日志，而不是作为整个过程的累计值。`NOSTIMER` 是默认值。为了在 `PROC SQL` 中使用 `STIMER` 选项，SAS 系统选项 `STIMER`（默认值）也必须生效。如果你只使用系统选项，你将获得整个过程的计时信息，而不是逐个语句的计时。





## 第 8 章（续）

6. 正确答案：dA `Dictionary` 表是一个特殊的只读 SAS 数据视图，它包含有关当前 SAS 会话中正在使用或可用的 SAS 数据库、SAS 数据集、SAS 宏和外部文件的信息。`Dictionary` 表还包含当前生效的 SAS 系统选项的设置。

7. 正确答案：d-`Dictionary` 表在每次于 SAS 程序中被引用时都会创建，并自动更新，且仅限于只读访问。访问 `Dictionary` 表会使 SAS 确定 SAS 会话的当前状态，并返回您想要的信息。

8. 正确答案：d-可以通过使用 `Dictionary` libref 针对该表运行 `PROC SQL` 查询来访问 `Dictionary` 表。虽然 SAS librefs 通常限制为 8 个字符，但 `Dictionary` 是一个自动分配的保留字。您也可以通过引用存储在 `Sashelp` 库中的该表的 `PROC SQL` 视图来访问 `Dictionary` 表。

10. 正确答案：b-要查看 `Dictionary` 表是如何定义的，请提交 `DESCRIBE TABLE` 语句。`DESCRIBE TABLE` 语句会在 SAS 日志中为 `DESCRIBE TABLE` 语句中指定的表写入 `CREATE TABLE` 语句。

11. 正确答案：a-要显示特定库中文件的信息，请在 `SELECT` 语句中指定列名并在 `FROM` 子句中指定 `Dictionary` 表名。`WHERE` 子句中的库名必须大大写，因为这是它在 SAS 中的存储方式，并且必须包含在引号中。

# 第 9 章：宏变量简介

1. 正确答案：b-宏变量始终独立于 SAS 数据集的文本字符串。宏变量的值长度可达 65,534 个字符，宏变量的名称长度可达 32 个字符。宏变量可以在 SAS 任何地方（数据行除外）定义或引用。宏变量有两种类型：自动宏和用户定义宏。

2. 正确答案：c-要引用宏变量，请在名称前加一个 `&` 符号。您不需要将宏变量引用括在引号中。

3. 正确答案：a-在 SAS 日志中显示宏变量值有两种方法：您可以开启 `SYMBOLGEN` 系统选项来列出所有使用的宏变量的值，或者可以使用 `%PUT` 语句将特定文本（包括宏变量值）写入日志。

4. 正确答案：d-您使用 `%LET` 语句来定义宏变量。您不需要将值括在引号中。如果您在赋值给宏变量的值中包含了引号，则引号将作为值的一部分被存储。

5. 正确答案：d-宏变量以字符字符串的形式存储。引号和大多数特殊字符按照其赋值的方式精确存储，但赋值值中的前空格会被删除。您还可以在 `%LET` 语句中包含对其他宏变量的引用。

6. 正确答案：d-`SYSDATE9` 是一个自动宏变量，它以 `ddmmmyyyy` 格式存储 SAS 会话开始的日期。您可以使用 `%SYSFUNC` 函数配合任何 DATA 步函数，因此 `TODAY()` 函数和 `DATE()` 函数都会产生当前日期。

7. 正确答案：c-诸如 `%UPCASE` 和 `%SUBSTR` 等宏字符函数允许您对宏变量值进行字符操纵。

8. 正确答案：b-`scanner` 单词识别四种类型的标记（tokens）。表达式不是标记的一种类型。

9. 正确答案：c-您可以将宏变量引用与文本结合以创建新的文本字符串。如果您在宏变量之前加上文本，宏变量名称开头的 `&` 符号表示文本的结束和宏变量名称的开始。如果您想让文本紧随宏变量值，必须用句点 `.` 标记宏变量名称的结束。

10. 正确答案：c-在这种情况下，您使用 `%QSYSFUNC` 函数来掩盖由 `worddate.` 格式产生的逗号。您必须掩盖这个逗号，因为 `LEFT()` 函数只接受一个参数。

# 第 10 章：执行时处理宏变量

1. 正确答案：c-大多数宏函数在 `DATA` 步中的任何 SAS 语言语句执行之前已由宏处理器处理。例如，`%LET` 语句和任何宏变量引用（`&macvar`）在程序编译之前传递给宏处理器。为了在 DATA 步执行期间创建或更新宏变量，您需要使用 `SYMPUT` 过程。

2. 正确答案：a-要创建一个宏变量并为其赋值一个基于 DATA 步变量的值，您需要使用 `SYMPUT` 过程。在 `SYMPUT` 过程中，要将字面量作为宏变量名，请将字面量括在引号中。要将字面量作为宏变量的值，请将字面量括在引号中。

3. 正确答案：d-`SYMPUT` 过程允许您将数据集变量作为宏变量的值。您还可以使用 `SYMPUT` 过程创建一系列相关的宏变量。由于所有宏变量值都是字符字符串，`SYMPUT` 会自动转换您尝试赋值给宏变量的任何数值值。在 SCL 程序中，如果您尝试将数值值赋值给宏变量，必须使用 `SYMPUTN` 而不是 `SYMPUT`。

4. 正确答案：b-当一个宏变量的值是另一个宏变量的名称时，可以使用多个 `&` 来创建间接引用。如果在 SYMPUT 过程中将 DATA 变量名括在引号中，则新宏变量将与该 DATA 变量同名，而不是以该 DATA 变量的值作为名称。使用 `SYMGET` 函数在 DATA 步执行期间获取宏变量的值。

5. 正确答案：b-如果连续四个以上的 `&` 在标记之前，重新扫描将从左到右持续直到可以解析更多标记。向前扫描规则（Forward Re-scan）描述了宏处理器如何解析以多个 `&` 或多个 `%` 开头的宏变量引用。

6. 正确答案：dA 宏变量引用（`&macvar`）在向编译器发送任何 SAS 语言语句之前解析。`SYMGET` 函数允许您在 DATA 步或 PROC SQL 步执行期间获取宏变量的值。`SYMGET` 函数还可以用于在 SCL 程序执行期间获取宏变量的值。

7. 正确答案：c-要在 PROC SQL 步执行期间创建宏变量，请使用 `SELECT` 语句的 `INTO` 子句。在 `INTO` 子句中，宏变量名称前加 `:`。

8. 正确答案：c-您可以使用多个 `&` 来延迟宏变量引用的解析。您还可以结合宏变量引用创建新的标记。在这个示例中，引用 `&&teach&crs` 在第一次扫描时解析为 `&teach3`。在下一次扫描中，`&teach3` 解析为 `Forest, Mr. Peter`。





10. 正确答案：c `SYMPUT` 例程可以在 `DATA` 步或 SCL 程序中使用。在 `DATA` 步中，`SYMPUT` 例程将对你尝试赋值给宏变量的数值值进行自动转换，并使用 `BEST12. ` 格式。在 SCL 程序中，如果你想将数值赋值为宏变量的值，则应该使用 `SYMPUTN` 例程。在 `PROC SQL` 步中，你需要在将宏变量的值与其他数值进行比较之前，使用 `INPUT` 函数将宏变量的值转换为数值。

# 第 11 章：创建和使用宏程序

1. 正确答案：b 宏定义必须以 `%MACRO` 语句开始，并以 `%MEND` 语句结束。宏定义可以包含宏语言语句，也可以包含 SAS 语言语句。当编译宏时，系统会检查宏语言语句是否有语法错误。编译后的宏默认存储在临时的 SAS 目录中。

2. 正确答案：c 将要在宏定义中包含位置参数，你需要在括号中列出这些参数并用逗号分隔。当宏执行时，宏变量将在局部符号表中创建，且其名称与参数相同。然后你可以在宏内部使用这些宏变量。

3. 正确答案：c 调用包含位置参数的宏时，要在宏名称前加一个百分号。你需要在括号中列出由参数定义的宏变量的值。请按参数列出的相同顺序列出这些值，并用逗号分隔。记住，宏调用不是 SAS 语言语句，因此不需要分号。

4. 正确答案：d 在混合参数列表中，位置参数必须列在任何关键字参数之前。位置参数和关键字参数都会在局部符号表中创建宏变量。若要为关键字参数分配空值，你可以在宏调用中不带任何值地列出该参数。

5. 正确答案：c 当你提交一个宏定义时，该宏会被编译并存储在 SAS 目录中。然后当你调用该宏时，该宏会被执行。该宏在当前 SAS 会话期间任何时候都可以用于执行。

6. 正确答案：d 你可以使用 `%IF-%THEN` 语句对代码进行条件处理。在 `%IF-%THEN` 语句内部，你必须使用 `%DO` 和 `%END` 语句来封装多个语句。`%IF-%THEN` 语句与 `DATA` 步中的 `IF THEN` 语句类似，但它们属于宏语言。

7. 正确答案：d 通过使用 `%IF-%THEN` 语句，你可以将整个步、单个语句或语句的一部分放入输入栈中。

8. 正确答案：c 有多种方法可以在局部符号表中创建宏变量。通过宏定义中的参数或 `%LOCAL` 语句创建的宏变量始终在局部表中创建。在宏定义内部，通过 `%LET` 语句或 `SYMPUT` 例程创建的宏变量也可能创建在局部表中。

9. 正确答案：b 要定义带有 `%DO` 循环的宏，你需要使用一个 `%DO` 语句和一个 `%END` 语句。请确保在语句中的所有关键字前都加上百分号，因为 `%DO` 和 `%END` 语句是宏语言语句。此外，请确保这些语句以分号结束。

10. 正确答案：d 当你提交对一个已编译宏的调用时，该宏会被执行。具体而言，宏处理器首先执行编译后的宏语言语句。当遇到任何 SAS 语言语句时，宏处理器会将这些语句放入输入栈并暂停，直到它们传递给编译器并执行。然后，宏处理器继续重复这些步骤，直到遇到 `%MEND` 语句。

# 第 12 章：存储宏程序

1. 正确答案：d `%INCLUDE` 语句可以将外部文件的内容插入到 SAS 程序中。如果宏定义存储在外部文件中，当它被插入到 SAS 程序时，`%INCLUDE` 语句会导致宏定义被编译。只有在指定了 `SOURCE2` 选项时，宏定义的内容才会写入 SAS 日志。

2. 正确答案：a 当宏定义存储为目录 `SOURCE` 条目时，你必须在从 SAS 程序调用它之前对其进行编译。你通过使用 `CATALOG` 访问方法来编译存储为目录 `SOURCE` 条目的宏。这会创建一个会话编译的宏，它将在 SAS 会话结束时被删除。`PROC CATALOG` 语句允许你查看 SAS 目录内容的列表。

3. 正确答案：c 要调用存储在自动调用（autocall）库中的宏，你必须同时指定 `MAUTOSOURCE` 系统选项和 `SASAUTOS=` 系统选项。`SASAUTOS=` 系统选项可以设置为包含多个路径或文件引用。一旦设置了这两个系统选项，你就可以在宏名称前加百分号来调用该宏。

4. 正确答案：d 存储编译宏设施（Stored Compiled Macro Facility）允许你永久存储编译后的宏，以便在后的 SAS 会话中重复使用它们而无需再次编译。编译宏必须存储在名为 `Sasmacr` 的目录中，并且必须指定 `MSTORED` 系统选项和 `SASMSTORE=` 系统选项。

5. 正确答案：b 为了创建一个永久存储的编译宏，你必须指定 `MSTORED` 系统选项。必须指定 `SASMSTORE=` 系统选项指向你想要存储宏的库。你还在 `%MACRO` 语句中使用 `STORE` 选项。

6. 正确答案：a 当你提交宏定义时，SAS 会创建一个会话编译的宏并将其存储在临时 SAS 目录 `Sasmacr` 中。该宏将在会话结束时删除。

7. 正确答案：d 如果你将宏定义存储在外部文件中，你就可以与他人共享这些文件。此外，你可以使用任何文本编辑器编辑存储在外部文件中的宏定义，并在其他 SAS 会话中重用它。

8. 正确答案：b `PROC CATALOG` 步骤允许你查看 SAS 目录内容的列表。如果你将宏定义存储永久 SAS 目录中的 `SOURCE` 条目，这可能特别有用。你可能还会使用 `PROC CATALOG` 步骤查看存储在 `Sasmacr` 中的会话编译宏列表。

9. 正确答案：c 要使用存储编译宏设施，你需要指定 `MSTORED` 和 `SASMSTORE=` 系统选项。存储编译宏设施将编译宏保存在永久 SAS 目录中，但它不保存宏定义。你无法跨操作系统移动编译宏。由于无法从编译宏重新创建宏定义，建议永久保存源程序。

# 第 13 章：创建索引

1. 正确答案：d 索引是数据集的一个独立文件，包含数据集内观测的信息。具体而言，索引包含值/标识符对，指示数据集内观测的位置以及该观测中一个或多个键变量的值。





## 索引概念

2. 正确答案：c 要在创建数据集的同时创建索引，你可以使用 `DATA` 语句中的 `INDEX=` 选项。你必须为复合索引分配一个唯一的名称，而简单索引会自动将键变量的名称作为其名称。你可以将系统选项 `MSGLEVEL=` 的值设置为 `I`，以便在 SAS 日志中查看有关索引的消息。

3. 正确答案：a 对于你对数据集执行的许多维护任务，SAS 会自动对索引文件执行相应的任务。例如，如果你删除了一个数据集，索引文件也会被删除。如果你在 `DATASETS` 过程中使用 `CHANGE` 语句重命名一个数据集，SAS 会自动重命名索引文件。如果你在 `DATASETS` 过程中使用 `COPY` 语句将数据集复制到新位置，SAS 会在新位置自动重建索引文件。

4. 正确答案：d 你可以使用 `DATASETS` 过程或 `SQL` 过程从现有数据集中创建或删除索引。你还可以使用 `DATA` 步重建索引，并使用 `INDEX=` 选项在重建的数据集上创建索引。然而，重建数据集比使用 `DATASETS` 或 `SQL` 过程向现有数据集添加索引消耗更多的系统资源。

5. 正确答案：a 你使用 `SQL` 过程的 `CREATE INDEX` 语句在现有数据集上创建索引。在 `SQL` 过程中，你必须在 `CREATE INDEX` 语句中命名索引；对于简单索引，索引名称必须与键变量的名称匹配。

6. 正确答案：b 你可以使用 `CONTENTS` 过程或 `DATASETS` 过程中的 `CONTENTS` 语句生成有关数据集的信息列表，包括现有索引列表。一个数据集的所有索引都存储在一个单独文件中，该文件与数据集分离，但名称相同。

7. 正确答案：b 索引可以提高 SAS 访问数据集中某些观测值的效率。然而，索引并不总是有用。SAS 不会使用索引来处理子集 `IF` 语句，或其他 SAS 认为不使用索引处理可能更高效的其他语句。

# 第 14 章：垂直合并数据

1. 正确答案：c 当使用 `FILENAME` 语句将文件引用（fileref）分配给多个原始数据文件时，文件列表必须包含在一对括号内。指定的每个文件名必须包含在引号中。

2. 正确答案：d `FILEVAR=` 选项允许你将当前打开的输入文件动态更改新的输入文件。`FILEVAR=` 变量必须包含物理文件名的字符字符串。与自动变量一样，`FILEVAR=` 变量不会写入数据集。

3. 正确答案：b `DO` 语句创建索引变量 `x` 并为其赋值值 `8`、`9` 和 `10`。赋值语句使用 `x` 的当前值和 `PUT` 函数将原始数据文件的名称分配给 `Readfile`，`PUT` 函数将 `x` 的值与文本字符串 `c:\data\month` 和 `.dat` 拼接。`COMPRESS` 函数删除了 `Readfile` 值中的空格。

4. 正确答案：a `TODAY` 函数从系统时钟返回当前日期作为 SAS 日期值。然后使用 `YEAR` 函数从当前日期中提取年份数字。当前年份值 `2003` 被赋值给 `y3`。年份值 `2002` 和 `2001` 分别赋值给 `y2` 和 `y1`。`PUT` 函数将文本字符串 `c:\data\Y` 与年份值以及文本字符串 `.dat` 拼接。

5. 正确答案：a `END=` 选项命名了一个值由 SAS 控制的变量。当你读取输入文件中的最后记录时，该变量的值为 `1`。否则为 `0`。你可以测试 `END=` 变量的值来判断 `DATA` 步是否应该继续处理。与自动变量一样，`END=` 变量不会写入 SAS 数据集。

6. 正确答案：b `PROC APPEND` 使用 `BASE=` 和 `DATA=` 参数。`BASE=SAS-data-set` 指定你想要从中添加观测值的数据集。`DATA=SAS-data-set` 指定包含观测值的 SAS 数据集，你想将这些观测值追加到 `BASE=` 数据集的末尾。

7. 正确答案：d 如果 `DATA=` 数据集包含比 `BASE=` 数据集中对应变量长的变量，则必须在 `PROC APPEND` 中使用 `FORCE` 选项。使用 `FORCE` 选项允许你合并数据集。然而，从 `DATA=` 数据集中读取的观测值中，某些变量值可能会被截断。

8. 正确答案：c 当 `DATA=` 数据集包含一个与 `BASE=` 数据集中对应变量类型不同的变量时，你必须在 `PROC APPEND` 中使用 `FORCE` 选项。

9. 正确答案：a 当 `BASE=` 数据集包含变量多于 `DATA=` 数据集时，额外变量的缺失将被赋值给从 `DATA=` 数据集中读取的观测值。

10. 正确答案：b 如果 `BASE=` 数据集包含 `DATA=` 数据集中不存在的变量，则不需要使用 `FORCE` 选项。在以下情况下必须使用 `FORCE` 选项：
    - `DATA=` 数据集包含 `BASE=` 数据集中不存在的变量
    - `DATA=` 数据集的变量比 `BASE=` 数据集的对应变量长
    - `DATA=` 数据集的变量与 `BASE=` 数据集的对应变量类型不同

# 第 15 章：水平合并数据

1. 正确答案：c 记住共同变量可能可能不同。`Manager` 和 `IDnum` 是两个类型匹配的变量。你可以使用 `RENAME=` 选项重命名其中一个变量，以便其作为 `MERGE` 语句的 `BY` 变量。

2. 正确答案：b 为了在 `DATA` 步中合并多个数据集，数据集必须具有共同变量。然而，如果存在至少两个数据集具有共同变量，且每个输入数据集至少包含这些变量之一，那么你可以使用后续的 `DATA` 步合并数据集。你也可以使用 `PROC SQL` 步合并没有共同变量的数据集。

3. 正确答案：d 你可以使用 `PROC SQL` 连接没有单一共同变量的数据集。如果你在 `PROC SQL` 步通过内连接（inner join）的结果创建一个新表，生成的内存可能与 `DATA` 步合并的结果相似或相同。

4. 正确答案：a 在 `DATA` 步合并中，SAS 按顺序读取输入数据集的观测值，并与其他数据集的观测值合并。当 SAS 将所有输入数据集的观测值读入 `PDV` 时，会创建观测值。这些观测值以及任何包含缺失或未匹配值的观测值将被写入新数据集。`PROC SQL` 连接创建匹配的笛尔积然后消除非匹配数据。

5. 正确答案：c 你可以在一个 `DATA` 步中使用多个 `SET` 语句合并来自多个数据集的观测值。这些数据集不需要具有共同变量。

6. 正确答案：b 你可以使用 `MEANS` 过程创建一个包含摘要统计的新的数据集。`NOPRINT` 选项抑制默认报告。`OUTPUT` 语句将 `MEANS` 过程的结果路由到新的数据集。`VAR` 语句指定输入数据集中的一个或多个数值变量。





7. 正确答案：a `N` 变量记录了 `DATA` 步迭代的次数。在示例中，`N` 被用于确保第一个 `SET` 语句只执行一次，从而从 `Sasuser.Summary` 中读取一个观测值，但不读取文件末尾标记。由于 PDV 中的值在每次 `DATA` 步迭代后不会重新初始化，因此 `CARGOSUM` 的值在整个 `DATA` 步执行过程中都会被保留。因此，如果 `Cargosum` 的值在第一次迭代中为 $1000，那么在随后的每次迭代中它也将是 $1000。

8. 正确答案：d `Totalrev` 是 `sum` 语句的累加变量，它会自动初始化为值 0。如果 `sum` 语句中的表达式产生缺失值，SAS 将用 0 替换缺失值。随着 `DATA` 步的迭代，`sum` 语句会保留累加变量，以便累加出一个总和。

9. 正确答案：d 你在 `SET` 语句中使用 `KEY=` 选项，使 SAS 使用索引来合并来自多个数据集的数据。当带有 `KEY=` 选项的 `SET` 语句执行时，程序数据向量必须包含索引变量的值。你不能在同一个 `DATA` 步中对使用 `KEY=` 选项读取的数据集使用 `WHERE` 处理。

10. 正确答案：b 当使用 `KEY=` 选项时，SAS 会创建一个名为 `IORC_` 的自动变量，代表输入输出返回代码（INPUT/OUTPUT Return Code）。如果 `IORC` 的值为零，则索引搜索成功。当你在 `DATA` 步中使用 `MODIFY` 语句时，也会自动创建 `IORC` 变量。

# 第 16 章：使用查找表匹配数据

1. 正确答案：a 使用关键字 `ARRAY` 后面跟数组名称和数组维度来指定数组。在二维数组中，两个维度可以被视为一个行和列组成的表格。`ARRAY` 语句中的第一个维度指定行数，第二个维度指定列数。

2. 正确答案：b 要创建临时数组元素，在数组名称和维度之后指定 `TEMPORARY` 关键字。记住，如果你使用星号 `*` 来计算数组元素，则必须列出数组元素。你不能在 `ARRAY` 语句中同时使用星号和 `TEMPORARY` 关键字。

3. 正确答案：d 要处理数组中的所有元素，你可以使用以数组名为参数的 `DIM` 函数，或者指定数组维度。

4. 正确答案：a `ARRAY` 语句创建了二维数组 `Score` 并指定了数组的维度：两行四列。每个观测值的 `Points` 值是根据 `Work.Contest` 数据集中 `Week` 和 `Finish` 的值并引用数组来确定的。数组引用的行号由 `Week` 的值决定，数组引用的列号由 `Finish` 的值决定。

5. 正确答案：d 当值过多而无法在数组中轻松初始化、值频繁变化、或者相同的值在许多程序中使用时，应该将查找表存储在 SAS 数据集中。

6. 正确答案：c 这里的 `IF-THEN` 语句指定 `Targets` 数组仅在 `DATA` 步的第一次迭代中加载一次。在 `DATA` 步的第一次迭代中，条件 `_N_=1` 为真，因此外层 `DO` 循环执行三次；对应 `Sasuser.Ctargets` 中的每个观测值。在 `DO` 循环第三次迭代后，指针移动到第二个 `SET` 语句，并将 `Sasuser.Monthum` 中第一个观测值读取到程序数据向量中。在 `DATA` 步的第二次迭代中，条件 `_N_=1` 为假。因此，`DO` 循环不再执行。

7. 正确答案：c `PROC TRANSPOSE` 过程通过重构输入 SAS 数据集的值来创建一个输出数据集。当数据集被重构时，选定的变量会被转置为观测值。该过程默认创建几个变量名。`NAME_` 是 `PROC TRANSPOSE` 创建的默认变量，用于识别输出数据集中每个观测值的来源。其余转置变量默认命名为 `COL1...COLn`。

8. 正确答案：b 你可以使用 `PROC TRANSPOSE` 的多个选项来为输出数据集中的变量提供描述性名称。`NAME=` 选项为 `NAME_` 变量指定名称。`PREFIX=` 选项指定在构建输出数据集中其他变量名称时使用的前缀。

9. 正确答案：b `PROC TRANSPOSE` 可以与 `BY` 语句配合使用。对于每个 `BY` 组，`PROC TRANSPOSE` 为其转置的每个变量创建一个观测值。`BY` 变量本身不会转置。在使用 `PROC TRANSPOSE` 的 `BY` 语句之前，必须对原始数据集进行排序或索引。

10. 正确答案：d `Work.Fishsize` 中的观测值按 `Location` 和 `Date` 分组。对于每个 `BY` 组，`PROC TRANSPOSE` 创建四个观测值，对应其转置的每个变量（`Length1`、`Weight1`、`Length2` 和 `Weight2`）。

# 第 17 章：数据格式化

1. 正确答案：d 默认，SAS 在 `Work` 和 `Library` 库中搜索自定义格式。`FMT=` 系统选项指定引用格式时搜索的其他库。

2. 正确答案：c 使用非包含范围，使得范围的高端不被包含。为了创建图片格式，使用了三个零。因为零作为位选择器而非非零值，前导零不包含在内。

3. 正确答案：b 默认情况下，`FMTERR` 是有效的，如果找不到引用的格式将停止处理。当 `NOFMTERR` 有效时，SAS 会替换格式并继续处理。

4. 正确答案：b 使用 `CTL=` 选项创建格式的数据集具有 `FmtName`、`Start` 和 `Label`。如果指定了范围，还必须包含 `End`。

5. 正确答案：a 此值语句创建格式具有重叠范围，因此必须使用 `LABEL` 选项。多标签格式可以使用支持 `MLF` 选项的过程。

6. 正确答案：c `CNLOUT=` 选项用于从格式创建 SAS 数据。

7. 正确答案：b SAS 将按照 `FMTSEARCH` 指定的顺序进行搜索。默认，SAS 先搜索 `Work` 和 `Library` 库，除非在选项中另有指定。此处未指定 `Library`，它将在 `Work` 之后搜索。

8. 正确答案：d `FMTLIB` 关键字用于记录目录中的格式。你可以使用 `SELECT` 和 `EXCLUDE` 语句处理特定的格式而不是整个目录。

9 `OUT=` 指定你想要拷贝格式项的目标目录。在 `SELECT` 语句中，你通过完整名称指定目录项。记住，数字格式以 `.FORMAT` 扩展存储，字符格式以 `.FORMATC` 扩展存储。

10. 正确答案：c 值 6.1 落在范围 6<-9 之内，标签为 'Good.'。非包含范围不包含值 6，但包含 6 以上的值。

# 第 18 章：修改 SAS 数据和跟踪更改

1. 正确答案：c `PRIMARY KEY` 完整性约束包含了 `NOT NULL` 和 `UNIQUE` 约束。

2. 正确答案：d 要使用 `DATASETS` 过程对现有 SAS 数据启动审核，需要在 `AUDIT` 语句中指定数据集，然后指定 `INITI` 语句。使用 `LIB=` 选项指定库。

3. 正确答案：c 在 `MODIFY` 语句中，先指定主数据集，后指定事务数据集。然后在 `BY` 语句中指定键变量。





4. 正确答案：c `_IORC_` 的值是一个数值返回代码，指示最近执行的 I/O 操作的状态。检查此变量的值允许你检测异常的 I/O 情况，并以特定方式引导执行。

5. 正确答案：d 在 `MODIFY` 语句中，你列出想要修改的 SAS 数据集。然后，你使用 `IC CREATE` 语句创建完整性约束。该完整性约束是一个带有 `WHERE` 子句的 `CHECK` 约束，用于指定变量必须满足的条件。

6. 正确答案：b `DATA` 步中的 `MODIFY` 语句只能修改数据集中的值。它不能修改数据集的描述部分。

7. 正确答案：c 审计跟踪（Audit trails）用于跟踪对数据集进行的现场更改。

8. 正确答案：a 你使用 `DATASETS` 过程和 `MODIFY` 语句为数据集指定多个生成数据集。`GENMAX=` 选项用于指定要保存的版本。你指定的数字包含基础版本。

9. 正确答案：b 当你使用 `KEY=` 选项时，你必须指定对数据集执行的更新。

10. 正确答案：a 关键字 `ALL` 用于表示你想删除指定数据集的所有生成版本，包括基础版本。关键字 `HIST` 删除生成数据集，但保留基础版本。

# 第 19 章：高效 SAS 编程导论

本章没有测验题。

# 第 20 章：控制内存使用

1. 正确答案：b 你可以使用 `BUFNO=` 系统选项或数据集选项来控制可用于读取或写入 SAS 数据集的可用缓冲区数量。使用 `BUFNO=` 可以通过限制特定 SAS 数据集所需的输入/输出操作来缩短执行时间。然而，I/O 的改进是以增加内存消耗为代价的。缓冲区数量不是数据集的永久属性，仅对当前步步或 SAS 会话有效。

2. 正确答案：d 数据集在创建时页大小是固定的，可以是默认值或指定值。你可以使用 `BUFSIZE=` 选项来控制输出 SAS 数据集的页大小。新的缓冲区大小是永久的。一旦指定，每当处理该数据集时都会使用它。

3. 正确答案：a 数据集占据的字节总数等于页大小乘以页数。你可以使用 `CONTENTS` 过程报告页大小和页数。

4. 正确答案：b `SASFILE LOAD` 语句打开文件、分配缓冲区并将数据读入内存。

5. 正确答案：a 当使用 `SASFILE` 语句打开 SAS 数据文件时，数据保留在内存中，供后续的 `DATA` 和 `PROC` 步或应用程序使用，直到执行 `SASFILE CLOSE` 语句或 SAS 会话结束。虽然使用 `SASFILE` 语句打开的文件可以用于后续的输入或更新处理，但不能用于后续的实用或输出处理。如果内存中的文件在处理过程中增大，缓冲区数量流量。

# 第 21 章：控制数据存储空间

1. 正确答案：d 未压缩数据文件的描述部分始终存储在数据集的末尾。
2. 正确答案：b 未压缩数据文件的描述部分始终存储在数据集的末尾。如果你指定 `REUSE=YES`，SAS 会跟踪并重用删除的观测值。
3. 正确答案：c 使用 `LENGTH` 语句分配长度。
4. 正确答案：a SAS 数据视图使用的空间比数据文件少得多。
5. 正确答案：b 使用 `COMPARE` 过程检测任何差异。

# 第 22 章：使用最佳实践

1. 正确答案：b 随着 SAS 处理更大的子集，需要更多的 CPU 资源。
2. 正确答案：c `DATA` 步是唯一可以同时修改数据值和变量属性的技术。
3. 正确答案：d `SELECT` 语句更高效，因为它在加载之前对其进行检查。
4. 正确答案：a 当外部文件频繁更新数据集时，创建临时数据集比创建永久数据集更有优势。
5. 正确答案：c 单步 `DATASETS` 过程可以节省 CPU 和 I/O 操作。

# 第 23 章：高效查询数据

1. 正确答案：d 当使用索引选择子集时，SAS 只加载包含至少一个观测值的页。当顺序访问观测值时，SAS 必须加载所有页。加载更多页需要更多的 I/O 操作。
2. 正确答案：b 对于包含 `TRIM` 或 `SUBSTR` 以外函数的 `WHERE` 条件，SAS 不使用索引。
3. 正确答案：a 子集的大小相对于数据集的大小是决定哪种访问方法最有效的重要因素。如果子集很大（超过数据集的 33%），使用顺序访问可能比直接访问更高效。当你选择小子集（小于数据集的 33%）时，直接访问更高效，特别是当数据集很大（页数很多）时。然而，如果数据集非常小（小于三页），使用索引并不高效。
4. 正确答案：b
5. 正确答案：d

# 第 24 章：使用 PROC FCMP 创建函数

1. 正确答案：a
2. 正确答案：False
3. 正确答案：True
4. 正确答案：False

## 索引

## 特殊字符

`ATDATETIME_` 审计跟踪变量





# 审计跟踪变量

- `ATMESSAGE_` 审计跟踪变量
- `ATOBSNO_` 审计跟踪变量
- `ATOPCODE_` 审计跟踪变量

## `ATOPCODE_` 变量的值

- `ATRETURNCODE_` 审计跟踪变量
- `ATUSERID_` 审计跟踪变量

## `DSEMTR` 助符
## `DSENMR` 助符
## `DSENOM` 助符

## `IORC` 自动变量

### `IORC` 变量
### 监控 I/O 错误条件
### 在 `%SYSRC` 使用 `IORC`

## `SOK` 助符

## TEMPORARY_ 关键字

## TYPE_` 变量

### 理解类型
### 在 `PROC MEANS` 中使用 `TYPES` 语句合并类变量

## `;` (分号)
`?` 条件运算符

### 在 `PROC SQL` 中使用运算符
### 使用 `CONTAINS` 或问号 (`?`) 运算符选择字符串

`.` (点)
`&` (和符号)
`%` (百分号)

## 宏程序与指定指令

### 宏程序与指定指令
- 标记 (tokens)
- `%a` 指令
- `%A` 指令
- `%b` 指令
- `%B` 指令
- `%QUOTE` 函数
- `%CMPRES` 语句
- `%COPY` 语句
- `%d` 指令
- `%DATATYP` 语句

### `%DO-%END`
%IF-%THEN` 转 `IF-THEN`
- 概述
- 生成完整的步骤
- `%EVAL` 函数
- `%GLOBAL` 语句
- `%H` 指令
- `%I` 指令

## `%IF-%THEN/%ELSE` 宏语句

### 条件执行
### `%IF-%THEN` 转 `IF-THEN`
### 带条件处理的宏执行
### 语句部分的条件处理
### 宏比较中的大小敏感性

## `%INCLUDE` 语句
## `%INDEX` 函数
## `%j` 指令
## `%LEFT` 语句
## `%LENGTH` 函数
## `%LET` 语句

### 用户定义变量以及
- `%LOCAL` 语句
- `%LOWCASE` 语句
- `%m` 指令
- `%M` 指令

## `%MACRO` 语句

### 创建编译宏
- 一般形式
- 宏参数支持
- 包含位置参数的宏
- 包含关键字参数的宏
- 包含混合参数列表的宏

### `PARMBUFF` 选项
### 使用 `SOURCE` 选项
### 存储的宏代码
### `STORE` 选项
### `%MEND` 语句

### `%NRSTR` 函数
`%p` 指令
`%PUT` 语句
`%QLOWCASE` 语句
`%QSCAN` 函数
`%SUBSTR` 函数
`%SCAN` 函数
`%SYSEVAL` 函数
`%SYSFUNC` 函数
`%SYSRC` 自动宏
`TRIM` 语句
`%U` 指令
`%UPCASE` 函数
`%w` 指令
`%y` 指令
`%Y` 指令




# 条件运算符

## 通用形式

## WHERE 条件和

## A

### 访问方法，选择
### 累加变量

### ADD 子句，ALTER TABLE 语句 (SQL)
#### ADD 方法
- 别名
- 列

## 创建新列
## 使用关键字 CALCULATED
## 使用列别名重命名列
### 内联视图
- 表

## ALL 条件运算符

## 在 PROC SQL 中使用运算符
# 使用 ALL 运算符
- ALL 关键字

### DELETE 语句 (DATASETS)

### EXCEPT 集合运算符和
### 在 EXCEPT 运算符上使用 ALL 关键字
### 在 EXCEPT 运算符上使用关键字 ALL 和 `CORR`

### INTERSECT 集合运算符和
### 在 INTERSECT 运算符上使用 ALL 关键字
### 在 INTERSECT 运算符上使用关键字 ALL 和 `CORR`

### 集合操作和

### UNION 集合运算符和
### 在 UNION 运算符上使用 ALL 关键字
### 在 UNION 运算符上使用关键字 ALL 和 `CORR`

## ALTER TABLE 语句，SQL 过程

### ADD 子句
### DROP 子句
- 功能
- 通用形式
- `ALTER=` 数据集
- `DATA=` 数据集
- `FORCE` 选项

### ANY 条件运算符
- 描述

## APPEND 过程

### ARRAY 语句
### 合并数据
### 创建数组
- 通用形式
### 加载数组元素
- 查找值和
- 存储的数组值和
- 在...中合并数据
- 创建
- 定义
- 加载元素
- 多维
- 读取值
- 存储的值

### 带有长度的变量追加
### 带有类型的变量追加
- 通用形式

## 参数，摘要函数
### 参数数量与摘要函数处理处理
## 使用单参数（列）的摘要函数
## 使用多参数（列）的摘要函数

## 宏程序中的算术表达式
### %EVAL 函数
### 自动求值

## ATTRIB 语句
- DATA Step 对象
### 使用 DATASETS 过程设置变量属性

## AUDIT 语句，DATASETS 过程
- 概述
- 概述 [2]

## 审计轨迹
### 控制
### 控制...中的数据
- 概述
- 数据集变量
- 审计轨迹变量
- `_ATOPCODE_` 变量的值
### 使用 LOG 语句控制审计轨迹中的数据
- 初始化
- 概述
- 读取文件

## USER_VAR 语句
- 审计轨迹变量
- `_ATOPCODE_` 变量的值

## autocall 库
### 访问宏
- 创建
- 默认
- 定义

## 自动宏变量
- 功能
- 全局符号表和




# 宏变量

# 全局符号表

# AVG 函数

## B

### 基础表

### BASE= 数据集选项

### BEFORE_IMAGE 选项，LOG 语句

### 基准测试指南

### 最佳实践

### 条件逻辑

### DO 组

### 消除数据扫描次数

### 消除数据流中不必要的扫描

### 使用带有 WHERE 语句的 SORT 过程创建排序子集

### 使用 DATASETS 过程修改变量属性

### 仅执行必要的语句

### 读取/写入核心数据

## 概述

### 使用子集 IF 语句与 WHERE 语句选择观测值

### IF 和 WHERE 语句之间的其他差异

### 使用 WHERE 语句配合 OBS= 和 FIRSTOBS= 

### 从外部文件读取数据时选择观测值

### 使用 KEEP 和 DROP 语句及选项子集变量

### 变量子集

### 使用 KEEP 和 DROP 语句及选项进行变量子集

### 使用 KEEP 和 DROP 语句及选项进行变量子集 [2]

### BETWEEN-AND 条件运算符

### 描述

### 一般形式

### 识别待优化的条件

### 二分查找

### 控制 I/O 数量

### `BUFSIZE=`
### `FNO=`
### `BUFNO=`

### `BY` 语句，DATA 步

### 处理重复值

### `MODIFY` 语句

## 概述

### 监控 I/O 错误

### `TRANSPOSE` 过程

### `BY` 变量

### DATA 步合并 (match-merge)

### DATA 步合并

### DATA 步合并的执行

### 并表

## 概述

### 当所有值都匹配时

### 当部分值匹配时

## C

### CALCULATED 关键字

### CALL MISSING 程序

### 笛卡尔积

### 生成笛卡尔积

### PROC SQL 连接

# CASE 表达式

### 一般形式

### INSERT 语句 (SQL)

### SELECT 语句 (SQL)

### 通过不同的表达式更新行

## PROC SQL 如何根据 CASE 表达式更新行

### 通过无操作数的 CASE 表达式更新行

### 通过带操作数的 CASE 表达式更新行

### `case` 表达式，UPDATE 语句 (SQL)

### 通过无操作数的 CASE 表达式更新行

### 通过带操作数的 CASE 表达式更新行

### 宏比较中的大小敏感性

### CATALOG 方法，FILENAME 语句

### CATALOG 过程

### 使用 CATALOG 管理格式

### 格式管理

### catalogs，存储宏定义

## 概述

### CATALOG 过程

### CATALOG 访问方法

### CENTILES 选项，CONTENTS 过程

### CHANGE, DATASETS 过程

### 重命名数据集

### 生成号的变化

### 字符常量

### 字符数据类型

### 列宽与定义

### 列中的流字符

### 字符字符串

### `INDEX()` 函数

### `LENGTH()` 函数

### `SUBSTR()` 函数

### `UPCASE()` 函数

### `SCAN()` 函数




# `SUBSTR` 函数

# `UPCASE` 函数

# 宏字符函数

## 字符变量，存储

## CHART 过程

## 概述
### 宏变量名中的分隔符

## CHECK 约束类型功能

## 概述
### 普通完整性约束

## 概述
### `column` 规范中的

## `CLASS` 语句

### `TABULATE` 过程
### 类变量
### `_TYPE_` 值

### 理解类型
### 在 `PROC MEANS` 中使用 `TYPES` 语句合并类变量
### 合并汇总统计和
### 使用 `PROC MEANS` 显示类变量组合的汇总统计
### 使用基础 `PROC MEANS` 步骤合并所有类变量

## `CNTLIN=` 选项，`FORMAT` 过程
## 概述
### 控制数据集规则

### `CNTLOUT=` 选项，`FORMAT` 过程

## `COALESCE` 函数
### 当仅部分值匹配时
 当仅部分值匹配时：使用 `COALESCE` 函数

## 列别名
### `CALCULATED` 关键字和定义
### 使用 `aliases` 约束重命名列
### 列修饰
### 列宽
### 添加到表中
### 在表中修改
## 多列排序
### 汇总函数之外
### 叠加
### 处理计算列
### 使用列别名重命名
### 输出中的行数

## 键
### 简介
### 可通过 `Index` 优化的 `PROC SQL` 查询
### 在表中修改
## 多列排序
### 汇总函数之外
### 叠加
### 处理计算列
### 使用列别名重命名
### 输出中的行数

## `COMPARE` 过程
### 比较运算符
### `ALL` 条件运算符
### `ANY` 条件运算符
### 识别用以优化的条件
### 子查询和

## 编译宏程序
### 编译宏
### `MCOMPILOTE=` 选项

## 复合索引
## 创建多个索引
### 示例：创建复合唯一索引
### 简单和复合索引
### 简介
### 索引类型

## `COMPRESS` 函数
### `COMPRESS=` 数据集选项
### `COMPRESS=` 系统选项

## 压缩数据文件
### ...的成本
### 压缩数据文件
### 未压缩数据结构回顾
### 压缩数据结构
### 决定是否压缩数据文件
### `COMPRESS=` 系统选项和 `COMPRESS=` 数据集选项
### 直接在压缩数据集中观测值
### `POINTOBS=` 数据集选项
### `REUSE=` 系统选项和 `REUSE=` 数据集选项
### SAS 如何压缩数据





## 概述

## 使用 FORCE 选项
### 拼接不同长度的变量
### 拼接不同类型的变量
### 创建值的分隔符列表
### 已定义

## `FILENAME` 语句

## INFILE 语句
## 概述
### 为待读取的文件命名
### 使用 `COMPRESS` 函数
### 使用 `END=` 选项
### 使用日期函数
### 使用 `INTNX` 函数
### 条件运算符

## 条件处理
### 最佳实践
### 宏程序中的大小写敏感性

## 宏程序 循环
### 条件执行
### `%IF-%THEN` 与 IF-THEN 的比较
### 带有条件处理的宏执行
### 语句部分的条件处理
### 宏比较中的大小写敏感性

## 常量
### 向输出中添加字符常量
### 宏引用函数

## CONTAINS 条件运算符
### 描述
### 通用形式
### 识别待优化的条件
### `CENTILES` 选项
### 显示索引
### 维护索引
### 报告缓冲区

## `CATALOG` 过程

## `DATASETS` 过程
## 概述
### 概述 [2]
### 页大小
### 打印分位数信息
### `COPY` 过程
### `DATASETS` 过程中的 `COPY` 语句

## 复制数据集
### 复制数据集
### 复制数据集并保留完整性约束
### 表

## `CORR` 关键字

## `EXCEPT` 集合运算符
### 在 `EXCEPT` 运算符上使用关键字 `CORR`
### 在 `EXCEPT` 运算符上使用关键字 `ALL` 和 `CORR`

## `INTERSECT` 运算符
### 在 `INTERSECT` 运算符上使用关键字 `CORR`
### 在 `INTERSECT` 运算符上使用关键字 `ALL` 和 `CORR`

## `OUTER UNION` 集合运算符
### 在 `OUTER UNION` 运算符上使用关键字 `CORR`
### 外连接与其他 SAS 的比较

## 集合操作与
### `UNION` 集合运算符
### 在 `UNION` 运算符上使用关键字 `CORR`
### 在 `UNION` 运算符上使用关键字 `ALL` 和 `CORR`

## 相关查询
### `EXISTS` 条件运算符
### `NOT EXISTS` 条件运算符
### 子集化
### `COUNT` 函数

## `CREATE INDEX` 语句，SQL 过程
### 创建复合索引
## 创建多个索引
### 示例：创建唯一复合索引
## 创建多个索引
### 创建简单索引
## 示例：创建简单索引
### 示例：创建唯一复合索引
### 显示索引规范
### 功能

## 通用形式

## `CREATE` 语句，SQL 过程
### `AS` 关键字
## 复制表
### 创建约束
### 在列规范之外创建约束
### 创建空表
### 创建类似于其他表的表
### 创建输出表
### 从查询结果创建表
### 显示表结构
### `FORMAT=` 选项
### `FROM` 子句





# 带有约束指定的通用形式

## 带有 LIKE 子的通用形式

## 带有查询句的通用形式

## INFORMAT= 选项

## LABEL= 选项

## LIKE 子

### MESSAGE= 选项

## 在列规范中创建约束

### 使用约束规范创建约束

### MSGTYPE= 选项

## 在列规范中创建约束

### 使用约束规范创建约束

### SELECT 子

### 指定列修饰符
## 指定列宽
### 指定类型
### 如其他表一样指定空表
### 指定列子集

# CREATE VIEW 语句，SQL 过程

# FROM 子

### 通用形式

### USING 子

## D

### 数据文件

### 直接访问观测值

### COMPRESS= 数据集选项

### COMPRESS= 系统选项

### 压缩结构

## 压缩过程

### 压缩数据文件

### SAS 如何压缩数据

### 页面数

### POINTOBS= 数据集选项

### 压缩原因
### REUSE= 数据集选项
### REUSE= 系统选项
### 未压缩结构

### 数据集
### 直接追加观测值

## 概述
### 使用 FORCE 选项

### 以不同长度追加
### 以不同类型追加

### 审计跟踪
### 审计审计跟踪
### 启动审计跟踪
### 读取审计跟踪文件

## 控制过程

## 概述
### 监控 I/O 条件
### 在 %SYSRC 中使用 IORC

## 复制

### 复制数据集
### 复制数据集并保留完整性约束

## 从...创建格式

## 概述
### 控制数据集的规则
### 应用格式

# 在处理重复值时
### 处理重复值 [2]

## 生成

### 理解生成数据集

## 概述
### 创建生成集




# 通过索引修改观测值

# 重命名

# 存储数据

# 存储原始文件名

# 事务

## 概述

## 使用 UPDATE 语句

## 概述

## 转置

### 为合并构建数据结构
### 在 `PROC TRANSPOSE` 使用 BY 语句
### 排序 `Work.Ctarget2` 数据集
### 整理 `Sasuser.Monthsum` 数据集
### 排序 `Work.Mnthsum2` 数据集
### 完成合并

## DATA step

### ATTRIB 语句
### 最佳实践

## BY 语句

## 概述
### 处理重复值
### 监控 I/O 错误状态

## 比较连接和

## 概述
### 当所有值匹配时
## 当只有部分值匹配时

### `COMPRESS=` 数据集选项

## 节省存储空间

## 概述
### DATA 视图 (Views)
### `DESCRIBE` 语句
### 创建和引用 `DATA` 视图
### 在程序中多次引用 `DATA` 视图
### 对 `DATA` 视图进行多次扫描
### 在不稳定数据上创建 `Views`
### 创建索引
### 创建宏变量
### 创建多个宏变量
### `DROP` 语句
### 使用 `KEEP` 和 `DROP` 语句筛选子集
### 使用 `KEEP` 和 `DROP` 语句筛选子集 [2]
### `FORMAT` 过程
### `hash` 对象
### `IF-THEN/ELSE` 语句
### `INDEX=` 选项
### `KEEP` 语句
### 步骤 2：重构数据
### 使用 `KEEP` 和 `DROP` 语句筛选子集
### 使用 `KEEP` 和 `DROP` 语句筛选子集 [2]

### LENGTH 语句
### 使用 `LENGTH` 语句减少字符数据的长度
### 为数值变量分配长度

## 匹配合并 (Match-merges)

## 概述
### 当所有值匹配时
## 当只有部分值匹配时

### `DATA` Step 匹配合并
### 使用多个查找表
## 概述
### `DATA` Step 匹配合并
### `DATA` Step 匹配合并的执行
### `PROC SQL` 的执行
### 使用多个 `SET` 语句
### `DATA` Step 匹配合并
### 使用多个查找表
### 获取宏值
### `OUTPUT` 语句
### `%PUT` 函数
### `PUT` 函数
### `REMOVE` 语句
### `RENAME` 语句
### `REPLACE` 语句
### `RETAIN` 语句
### `REUSE=` 数据集选项
### `SET` 语句
### 子集 IF 语句
### `sum` 语句
### `SYMGET` 函数

## SYMPUT 例程和

### `SYMPUT` 例程
### 使用字面量 `SYMPUT`
### 使用 `DATA` 变量 `SYMPUT`
### 在 DATA Step 表达式中使用 `CALL SYMPUT`
### 使用 `CALL SYMPUT` 创建多个宏变量
### `SYMPUTX` 例程和

### 表查找和

### 数据汇总工具
### `UNIQUE` 选项
### `UPDATE` 语句
### `VIEW=` 选项

## WHERE 语句

### 使用子集 `IF` 对比 `WHERE` 语句选择观测值



# IF 和 WHERE 语句的其他区别

## 概述

## 直接访问数据

## 示例
## 概述
#### 复合优化

## 数据类型

#### 追加带有不同字符的变量
#### 字符
## 指定数据类型
## 指定列宽
#### 列中的字符流
#### 通过定义列创建表

#### 数值
## 指定数据类型
## 指定列宽

## `DATA_IMAGE` 选项，`LOG` 语句

## `DATA=` 数据集选项

## DATALINES 语句

## 宏变量
### 调用宏

## DATASETS 过程

## AUDIT 语句
## 概述
### 概述 [2]

## 最佳实践
### 使用 DATASETS 过程修改变量属性
### 执行 DATASETS 过程
### 在 `PROC DATASETS` 使用不同类型的 RUN 组

## CHANGE 语句
### 重命名数据集
### 生成号的变化

## CONTENTS 语句
## 概述
### 概述 [2]
### 页面大小
### 打印分位数信息
`COPY` 语句
### 创建带有完整性约束的表
### 生成号如何
## 示例
### 显示索引规范
### 一般形式
`IC CREATE` 语句
`IC DELETE` 语句
`INDEX CREATE` 语句
`INDEX DELETE` 语句
`INITIATE` 语句
`LIBRARY=` 选项
### 管理索引

## MODIFY 语句
## 概述
### 概述 [2]
### 永久分配格式
`RENAME` 语句
`DATATYPE=` 选项，`PICTURE` 语句 (`FORMAT`)
`DATE` 函数

## 调试
### `FEEDBACK` 选项，`SQL` 过程

## 宏程序
### 使用系统选项监控执行
### `MLOG` 选项
### 宏程序中的注释
`DECLARE` 语句
`DEFAULT=` 选项，`LENGTH` 语句 (`DATA`)
### 定义键
### 处理多个变量
`DEFINE` 方法
### 定义键
### 处理多个变量
`DELETE` 语句，`DATASETS` 过程
### 生成号如何
## 示例
`DELETE` 语句，`SQL` 过程
### 审计轨迹
### 功能
### 一般形式
### 更新视图

## 删除
## 从表中删除列
## 索引
### 表中的行
### 表
### 视图

## 分隔符
### 宏程序中
### 宏变量名中
### 密密匹配

## DESCRIBE 语句
### `DATA` 步
### `SQL` 过程
`DESCRIBE TABLE` 语句，`SQL` 过程



## 概述

## 查询

### 数字选择器
### 直接访问

指令，指定图片

## 指定图片的方法

## 示例

### DISTINCT 关键字

### DO 循环

## 加载数组元素

## 高效使用 DO 组

## DO UNTIL 循环

## 点符号方法

## DOUBLE 选项，SQL 过程

## DROP 子句，ALTER TABLE 语句 (SQL)

### DROP INDEX 语句，SQL 过程

## 概述

### 概述 [2]

### DROP 语句

DATA 步

### 使用 KEEP 和 DROP 语句及选项筛选变量
### 使用 KEEP 和 DROP 语句及选项筛选变量 [2]

### SQL 过程

### DROP 语句，SQL 过程

### DROP TABLE 语句，SQL 过程

### DROP VIEW 语句，SQL 过程

DROP= 数据集选项

### 通用形式
变量子集

### 使用 KEEP 和 DROP 语句及选项筛选变量
### 使用 KEEP 和 DROP 语句及选项筛选变量 [2]
消除重复列，从输出中消除重复行
数据集中的唯一性
处理重复值
处理重复值 [2]

## 效率

### 评估所在站点的需求
评估技术环境
评估程序
评估你的数据
基准测试
比较资源使用

## 概述
SAS 如何比较资源使用
影响 I/O 的因素
子集相对于数据量的大小
数据文件中的页数
数据的顺序
顺序读取时压缩文件的解压缩成本
影响资源使用的其他因素
计算机资源
详尽报告
估算观测值

## 识别可用索引

## 概述
### 复合优化

识别优化的条件
识别可以优化的条件
无法优化的 WHERE 条件
复合优化的要求
索引
直接访问数据
示例
汇总工具
跨汇总的资源使用比较
理解类型
权衡
空表
概述 [2]
END= INFILE 语句
错误处理
用于行插入
监控 I/O 条件
停止 SQL 过程
ERROR_IMAGE 选项，LOG 语句
ERRORSTOP 选项，SQL 过程
评估性能

## EXCEPT 集合运算符

ALL 关键字和
在 EXCEPT 运算符上使用 ALL 关键字
在 EXCEPT 运算符上联合使用 ALL 和 CORR 关键字

CORR 关键字和
在 EXCEPT 运算符上使用 CORR 关键字
在 EXCEPT 运算符上联合使用 ALL 和 CORR 关键字

## 功能

### 介绍集合运算符

## 概述
EXCLUDE 语句，FORMAT 过程
使用 PROC FORMAT 中的 FMTLIB 记录格式
概述
EXEC 选项，SQL 过程

### EXISTS 条件运算符
关联查询和
描述
外部文件
从...选择观测值




# 存储宏定义
# 存储原始数据文件名

## F

### FEEDBACK 选项，SQL 过程
FILENAME 语句

### CATALOG 访问方法
## 概述
#### FILEVAR= 选项，INFILE 语句
FIND 方法
#### 获取匹配的数据
#### 获取多个数据值
#### 在 FIND 方法中使用返回代码
#### FIRSTOBS= 选项，WHERE 语句 (PRINT)
#### FLOW 选项，SQL 过程
#### FMTERR 系统选项
#### FMTLIB 关键字，FORMAT 过程
#### FMTSEARCH= 系统选项
#### FOOTNOTE 语句，SQL 过程

### FORCE 选项，APPEND 过程
#### 使用 FORCE 选项
#### 追加不同长度的变量
#### 追加不同类型的变量

### FOREIGN KEY 外键约束类型
#### 约束规范
#### 功能
## 概述
#### 普通完整性约束
## 引用完整性约束
## 概述
#### 列规范中的

### FORMAT 过程
#### 二进制搜索
#### CNTLIN= 选项
#### 控制数据的规则
#### CNTLOUT= 选项
#### 在 `PROC FORMAT` 文档中使用 `FMTLIB`
#### FMTLIB 关键字
#### LIB= 选项
#### PICTURE 语句
#### 指定指令的指南
#### 在 `PROC FORMAT` 文档中使用 `FMTLIB`
#### VALUE 语句
#### 用户定义的 SAS 格式
#### 示例：使用 `FORMAT` 过程合并数据
#### 创建非重叠格式的评审
#### 创建具有重叠范围的格式
## 示例
#### `FORMAT` 语句，TABULATE 过程
#### FORMAT= 选项

### CREATE TABLE 语句 (SQL)
#### SELECT 语句，SQL 过程
#### TABULATE 过程

### 格式
#### 与变量关联
#### 从创建数据集
#### 控制数据集规则
#### 应用格式
#### PICTURE 语句
#### 指定指令的指南
#### VALUE 语句
#### 创建非重叠格式的评审
#### 创建具有重叠范围的格式
#### FMTERR 系统选项
#### FMTSEARCH= 系统选项
#### 在 `PROC FORMAT` 文档中使用 `FMTLIB`
#### 使用 `PROC CATALOG` 管理格式
#### NOFMTERR 系统选项
#### 永久分配
#### 使用格式永久存储位置
#### 避免格式错误
#### 为列指定
#### 替换以避免错误
#### 使用重叠范围
#### 前向重扫描规则

### FREQ 过程
#### 高效使用条件逻辑
## 概述

### FROM 子句
#### 创建表 (SQL)
#### VIEW 语句 (SQL)
#### INSERT 语句 (SQL)

### SELECT 语句 (SQL)
### 指定表
#### 指定多个表名
### 生成笛卡尔积
## 引入内联视图
#### FSEDIT 过程
#### FSLIST 过程

### 全外连接
#### 介绍外连接类型
## 使用全外连接





# `FULLSTIMER` 系统选项

## functions

### `%QSYSFUNC` 函数
### `%SYSFUNC` 函数
### 宏变量支持

## G

### GCHART 过程
#### 宏变量名中的分隔符
#### 高效使用条件逻辑

## 通用完整性约束
## 通用完整性约束
#### 通用完整性约束 [2]

### 生成数据集
#### 创建
#### 定义
#### 初始化

### 处理
## 概述
#### 生成号如何变化
#### `GENMAX=` 选项，`MODIFY` 语句 (`DATASETS`)

#### `GENNUM=` 数据集选项
## 概述
#### 生成号如何变化
## 示例

### 全局符号表
#### `%GLOBAL` 语句
#### 定义

### 宏变量与
#### 宏变量
#### 全局符号表

### GPLOT 过程
#### 宏变量名中的分隔符
#### 高效使用条件逻辑

### `GROUP BY` 子句，`SELECT` 语句 (SQL)
#### 选择分组
#### 数据组汇总
## 概述
#### 数据组汇总
#### 在不使用 `GROUP BY` 子句的情况下使用函数和汇总函数
#### 在 `GROUP BY` 子句中使用汇总函数
#### 分组，选择

## H

### 哈希对象
#### `CALL MISSING` 例程
#### 从数据集创建
#### `DATA` 步对象
#### 声明
#### 定义
#### 定义键和数据
#### 加载 `key/data` 值
#### 多个数据变量
#### 处理
#### 获取匹配数据
#### 获取多个数据值
#### 使用 `FIND` 方法的返回代码
#### `SET` 语句和结构

### `HAVING` 子句，`SELECT` 语句 (SQL)
#### 其他功能
#### 使用 `HAVING` 子句分组
#### `HIST` 关键字

## I

### I/O 处理
#### 比较资源使用
## 概述
#### SAS 如何比较资源使用
#### 影响 I/O 的因素
#### 子集大小与数据集大小
#### 数据文件的页数
#### 数据顺序
#### 顺序读取解压缩文件的成本
#### 影响资源使用的其他因素
#### 测量
#### `IC CREATE` 语句，`DATASETS` 过程
#### `IC DELETE` 语句，`DATASETS` 过程

#### `IDXNAME=` 数据集选项
#### `IDXWHERE=` 数据集选项

### `IF-THEN/ELSE` 语句
#### `%IF-%THEN` 比较
#### 最佳实践
#### 高效使用条件逻辑
#### 高效使用 `DO` 组

### 数据外部查找值
## 概述
#### `IF-THEN/ELSE` 语句
#### SAS 数组 

### `IN` 条件运算符
#### 描述
#### 通用形式
#### 识别优化条件

### 内联视图
#### 分配别名
#### 功能
#### 多个表与
#### 使用其他视图或表引用内联视图
#### 在内联视图引用多个表
#### `INDEX CREATE` 语句，`DATASETS` 过程
#### `INDEX DELETE` 语句，`DATASETS` 过程

#### `INDEX=` 选项，`DATA` 步

## 索引
## 访问表中的行
#### 优势




## 概述

## 使用索引的优势

## 使用索引的收益与成本

## 与...合并数据

## 概述

## KEY= 选项

## `IORC` 变量

## 复合

## 简单索引复合复合

## 创建多个索引

## 示例：创建复合唯一索引

## 引言

## 索引类型

## 控制使用

## 复制数据集

## 使用成本

## 理解使用索引的成本

## 使用索引的收益与成本

## 创建

## 在 DATA step 中创建

## 创建多个

## 创建指南

## 创建索引的指南

### 决定是否创建索引

## 定义

## 引言

## 引言 [2]

## 概述

## 显示规范

## 记录

## 删除

## 识别可用

## 概述

## 复合优化

## 维护

## 管理使用

## 概述

## 控制索引使用

## 使用 DATASETS 过程管理

## 使用 SQL 过程管理

## 修改位于...的观测值

## 查询可以被索引优化的 PROC Queries

## 概述

## 顺序访问

## 直接访问

## 使用索引的收益与成本

## SAS 如何选择访问方法

## 不使用索引的原因

## 重命名数据

## 重命名变量

## 简单索引复合索引

## 示例：创建简单索引

## 引言

## 索引类型

## 数据子集

## 简单和复合索引的类型

## 索引类型

## 唯一索引

## 内连接

## 水平合并数据

## 概述

## DATA Step Match-Merge

## DATA Step Match-Merge 的执行

## PROC SQL Join 的执行

## 使用多个 SET Statement

## 定义

## 概述

## 介绍内连接语法

## `INFILE` 语句

## 为读取的文件命名

## `COMPRESS` 函数

## 日期函数

## `END=` 选项

## `FILE=` 选项

## 一般形式

## `INTNX` 函数

## `FORMAT=` 选项，`CREATE TABLE` 语句 (SQL)

## `INITIATE` 语句，`DATASETS` 过程




## 概述

# 概述 [2]

# 使用 SET 子句插入行

## 使用 VALUES 子句插入行

# SELECT 子句

## SET 子句

## 概述
### 使用 SET 子句插入行
### 更新视图

## VALUES 子句

## 概述
## 使用 VALUES 子句插入行
## 示例

## 完整性约束

### 在列规范之外创建
### 创建表带有
### 显示表
### 文档
### 强制功能

## 功能

## 概述
## 通用完整性约束
## 引用完整性约束

### 通用

## 通用完整性约束
### 通用完整性约束 [2]
### 带有规范的通用形式
在列规范中

### 放置数据集

## 概述
### 约束如何强制
### 复制数据集并保留完整性约束

### 引用

## 引用完整性约束
### 引用完整性约束 [2]
### 

## INTERSECT 集合运算符

### ALL 关键字和

### 在 INTERSECT 运算符上使用 ALL 关键字

### 在 INTERSECT 运算符上使用 `ALL CORR` 关键字

### 在 INTERSECT 运算符上使用 `ALL` 和 `CORR` 关键字

### 在 INTERSECT 运算符上使用 `ALL` 和 `CORR` 关键字

## 引入运算符

## 概述
### `INT` 函数
### `INTO` 子句 (`SQL`)
### 带有 `NOP` 选项的 `INTO` 子句
### 创建分隔值列表
### `SQL` 中的 `IS MISSING` 条件运算符
### 使用 `IS MISSING` 或 `NULL` 运算符选择缺失值
### `SQL` 中的 `IS NULL` 条件运算符
### 使用 `IS MISSING` 或 `NULL` 运算符选择缺失值
### 优化单个 `WHERE` 条件的要求

## 合并数据集

### 汇总/详细数据
## 概述
### `MEANS` 过程
### `Sum` 语句

### DATA 步 match-merge
### DATA 步 Match-merge
### 处理多个查找表

### 定义

 索引和

## 概述
### `KEY=` 选项
### `_IORC_` 变量

### 查找值和

## 概述
### `IF-THEN/ELSE` 语句
### SAS 数组

### 定义
### 使用多个 `SET` 语句

### 使用 `SET` 语句
### 使用多个 `SET` 语句：多对多

### 事务数据集

## 概述
### `UPDATE` 语句

### 转置数据集

### 用于合并的数据结构化
## 概述
### 在 `PROC TRANSPOSE` 中使用 `BY` 语句
### 排序 `Work.Ctarget2` 数据集
### 重组 `Sasuser.Monthsum` 数据
### 排序 `Work.Mnthsum2` 数据集
### 完成合并

## 合并表

### 优势

### `COALESCE` 函数

## 当只有部分值匹配时





# 当只有部分值匹配时：使用 `COALESCE` 函数

对比 `DATA` 步的匹配合并 (match-merges)

## 概述

## 当所有值都匹配时

## 当只有部分值匹配时

### 定义

## 概述
### 理解连接 (Joins)
### `EXCEPT` 集合运算符
### 对于匹配值的行
内联视图和

## 引入内联视图
### 使用其他视图或表引用内联视图
### 索引与内连接

## 概述
### 介绍内连接语法
### 外连接通用形式的内连接
### `INTERSECT` 集合运算符
### 外连接
### `OUTER UNION` 集合运算符

## 概述
### 比较外连接与其他 SAS 技术
### 定义的过程
### 集合操作
### `UNION` 集合运算符
### 结合视图

## K

`KEEP` 语句，`DATA` 步

### 步骤 2：重构数据
### 使用 `KEEP` 和 `DROP` 语句及选项划分变量子集
### 使用 `KEEP` 和 `DROP` 语句及选项 `KEEP=` 数据集通用形式划分变量子集
### 使用 `KEEP` 和 `DROP` 语句划分变量子集
### 使用 `KEEP` 和 `DROP` 语句划分键列子集
### 可通过索引优化的 `PROC SQL` 查询，键值定义

## 概述
### `LEFT` 函数返回代码
`KEY=` 选项 `MODIFY` 语句 (`DATA`）
# 测验
## 概述
### 处理重复值
### 监控 I/O 错误状态
### `SET` 语句 (`DATA`）
### 包含关键字参数的宏
### 包含混合参数列表的宏
### 关键字，修改集合操作

## L

`LABEL=` 选项

### `CREATE TABLE` 语句 (`SQL`）
### `SELECT` 语句，`SQL` 过程
### 标签，列
### `LEFT` 函数

左连接

### 介绍外连接的类型
## 使用左外连接

`LENGTH` 语句，`DATA` 步
### 使用 `LENGTH` 语句减少字符数据的长度
### 为数值变量分配长度 `LIB=` 选项，过程
`LIBNAME` 语句
`LIBRARY=` 选项，`DATASETS` 过程
`librefs`，视图
### `LIKE` 子句，`CREATE TABLE` 语句 (`SQL`）
`LIKE` 条件
### 条件
## 指定模式
### 字面量标记
本地符号表
### `%LOCAL` 语句
### 多个本地符号表

`LOG` 语句
### `BEFORE_IMAGE` 选项，控制审计轨迹中的数据
### `DATA_IMAGE` 选项
### `ERROR_IMAGE` 选项

宏程序中的逻辑表达式
### `%EVAL` 函数
### 自动求值

查找表定义

## 概述
### 介绍
### 将哈希对象作为多维数组和多个
存储的数组值
## 概述
### 创建数组
### 加载数组元素
### 读取实际值

`TRANSPOSE` 函数

## 概述
### 添加描述性变量名
转置数据集





# 为合并构建数据结构

## 在 PROC TRANSPOSE 中使用 BY 语句

## 对 Work.Ctarget2 数据集排序

## 重新组织 Sasuser.Monthsum 数据集

## 对 Work.Mnthsum2 数据集排序

## 完成合并

## SQL 过程中的 LOOPS 选项

# M

### 宏字符函数

- `%INDEX` 函数
- `%LENGTH` 函数
- `%QSCAN` 函数
- `%QSUBSTR` 函数
- `%QUPCASE` 函数
- `%SCAN` 函数
- `%SUBSTR` 函数
- `%UPCASE` 函数

- 处理字符字符串
- 宏定义

### 宏设施

- 宏变量
- 宏触发器
- 宏语言

### 宏处理器

- 功能
- 宏设施以及
- 宏变量规则
- 引用宏变量
- `%DO-%END` 宏程序
- `%EVAL` 函数
- `%GLOBAL` 语句
- `%IF-%THEN/%ELSE` 宏语句
- `%IF-%THEN` 与 `IF-THEN` 的对比
- 带有条件处理的宏执行
- 语句部分内容的条件处理
- 宏比较中的大小敏感性
- `%LOCAL` 语句
- `%SYSEVAL` 函数
- 算术/逻辑表达式
- `%EVAL` 函数
- 自动评估
- 自动评估
- 调用
- 大小敏感性以及
- ...中的注释

### 编译

- 编译宏
- `MCOMPILENOTE=` 选项

### 条件处理语句

- 条件执行
- `%IF-%THEN` 与 `IF-THEN` 的对比
- 带有条件处理的宏执行
- 语句部分内容的条件处理
- 宏比较中的大小敏感性
- 使用系统监控执行
- `MLOGIC` 选项
- 宏程序中的注释
- 执行

### 迭代处理

- 概述
- 生成完整的步骤
- 使用系统监控执行
- `MLOGIC` 选项
- 宏程序中的注释

### 嵌套

- 多个本地符号表
- `MPRINTNEST` 选项 

### 使用宏参数

- 包含位置参数的宏
- 包含关键字参数的宏
- 包含混合参数列表的宏
- 包含 `PARMBUFF` 选项的宏

# 存储编译宏设施

- 存储编译宏设施
- 创建存储编译宏
- 使用 `SOURCE` 选项
- 访问存储编译
- 访问存储的宏代码
- 将定义存储在目录（catalog）中
- `CATALOG` 过程
- `CATALOG` 访问方法
- 存储在自动调用库（autocall libraries）中
- `CATALOG` 过程
- 概述
- 创建自动调用库
- 默认自动调用库
- 访问自动调用宏
- 将宏存储在外部文件中





# 存储已编译的宏

## 符号表

### 全局符号表
### %GLOBAL 语句
### 局部符号表
### %LOCAL 语句
### 创建和更新变量的规则
### 多个局部符号表
### MPRINTNEST 选项
### MLOGICNEST 选项

## 宏引用函数

### %BQUOTE 函数
### %NRSTR 函数
### %STR 函数
### 特殊字符屏蔽
### 宏触发

## 宏变量

### %PUT 语句
### 自动

### 宏变量
### 宏变量 [2]
## 概述
#### 全局符号表
- 将引用与文本结合
- 创建分隔符值列表
- 在 DATA 步期间创建
- 在 PROC SQL 执行期间创建
- 在 DATA 步期间创建多个
- 使用 `INTO` 子句创建
- `DATALINES` 语句和分隔符名称
- 在 SAS 日中显示值
- `SYMBOLGEN` 选项
- `%PUT` 语句

#### 前向扫描功能
- 简介
- 概述

#### 符号表
#### 全局符号表
#### `%GLOBAL` 语句
#### 局部符号表
#### `%LOCAL` 语句
#### 创建和更新变量的规则
#### 多个局部符号表
#### `MPRNEST` 选项
#### `MLOGICNEST` 选项

## 宏功能和

### 宏参数和
#### 使用宏参数
- 包含位置参数的宏
- 包含关键字参数的宏
- 包含混合参数列表的宏
- 包含 `PARMBUFF` 选项的宏

### 宏处理器规则
- 在 DATA 步期间获取值
- 处理
- `%SYSFUNC` 函数
- `%PUT` 函数
- 引用宏变量
- 间接引用
- SAS 支持

### SCL 程序
## 概述
#### `SYMPUTN` 例程
#### `SYMGETN` 函数
#### `SYMBOLGEN` 系统选项
#### `SYMGET` 函数
#### `SYMGETN` 函数
#### `SYMPUT` 例程
- 使用字面量 `SYMPUT`
- 使用 DATA 步变量 `SYMPUT`
- 使用 DATA 步表达式 `CALL SYMPUT`
- 使用 `CALL SYMPUT` 创建多个宏变量
- `SYMPUTN` 例程
- `SYMPUTX` 例程

## 分词
### ...的触发器

## 用户定义

### 宏变量
### `%LET` 语句
### 全局符号表
### 多对多匹配
- 输入源之间的关系
- 示例

### 特殊字符屏蔽
- `%BQUOTE` 函数
- `%NRSTR` 函数
- `%STR` 函数

### 宏支持
- `MAUTOLDISPLAY` 系统选项
- `MAUTOSOURCE` 系统选项
- `MCOMPILENOTE=` 系统选项

## MEANS 过程
- 一般形式
- 多标签格式
- `NOPRINT` 选项





# NWAY 

## OUTPUT 语句

## MEANS 过程

### 在 `PROC MEANS` 中使用 `WHERE=` 输出数据集选项来选择所需的类型

## 数据汇总工具

## 概述
### 使用 `PROC MEANS` 显示类变量组合的统计摘要
### 比较三种使用 `PROC MEANS` 技术的资源消耗

### TYPES 语句
### WAYS 语句
### `WHERE=` 数据选项

## 内存

### 控制缓冲区数量
### 测量 I/O
### 使用 `BUFSIZE=` 选项
### 使用 `BUFNO=` 选项

### 控制页面大小
### 测量 I/O
### 页面大小
### 报告页面大小
### `MEMRPT` 系统选项

## MERGE 语句，DATA 步

### 数据步匹配合并 (Match-Merge)
### 处理多个查找表
### 消息字符

### `MESSAGE=` 选项，`CREATE TABLE` 语句 (`SQL`)

## 在列规范中创建约束
### 使用约束规范创建约束

### 元数据
### 方法
### 数据集中的缺失值
### `MLF` 选项，`TABULATE` 过程
### `MLOGIC` 系统选项
### `MLOGICNEST` 系统选项
### `MODIFY` 子句，`ALTER TABLE` 语句 (`SQL`)
### `MODIFY` 语句，`DATA` 步
### 审计轨迹
## 概述
### 处理重复值
### 监控 I/O 错误

### 简介
### 使用 `MODIFY` 语句
### 一般形式
### `KEY=` 选项
# 练习
## 概述
### 处理重复值
### 监控 I/O 错误
### `POINT=` 选项
### `UNIQUE` 选项
### `UPDATEMODE=` 选项

## MODIFY 语句，DATASETS 过程

## 概述
### 概述 [2]
### `MONTH` 函数
### `MPRINT` 系统选项
### `MPRINTNEST` 系统选项
### `MSGLEVEL=` 系统选项
### 判断 SAS 是否使用了 `MSGLEVEL=I`
### `MSGTYPE=` 选项，`CREATE TABLE` 语句 (`SQL`)
## 在列规范中创建约束
### 使用约束规范创建约束
### `STORE` 系统选项
### 存储的宏
### 访问存储的宏
### 多维数组
### 多标签格式
### `MULTILABEL` 选项，`VALUE` 语句 (`FORMAT`)
### 多列
### 按多列排序
### 使用带有多个参数（列）的汇总函数
### 多个索引
### 多个表
### 查询
### 在...中指定列
### 指定名称视图和
### 使用其他视图或表引用内联视图
## 在内联视图中引用多个表
### 连接多个表和视图

## N

### 名称标识符
### 分词
### 宏触发器
### `NAME=` 选项，`TRANSPOSE` 过程

### 嵌套宏
### 多个本地符号表
### `MPRINTNEST` 选项
### `NMISS` 函数
### `NODOUBLE` 选项，`SQL` 过程
### `NOERRORSTOP` 选项，`SQL` 过程
### `NOEXEC` 选项，`SQL` 过程
### 使用 `NOEXEC` 选项
### 在 `PROC SQL` 错后停止执行
### `NOFLOW` 选项，`SQL` 过程
### `NOFMTERR` 系统选项
### `NOFULLSTIMER` 系统选项
### `NOMEMRPT` 系统选项





# 非相关子查询

- 定义
- 多值
- 单值
- 数据筛选（子）
- 不匹配数据

## 输入数据源之间的关系

## 示例

### NONUMBER 选项，SQL 过程
- `NOPRINT` 选项

### MEANS 过程

### SELECT 语句 (SQL)
- `NOPROMPT` 选项，SQL 过程

## 示例

### 限制循环次数

### `NOSTATS` 系统选项

### `NOSTIMER` 选项，SQL 过程
- `NOSTIMER` 系统选项

### `NOT EXISTS` 条件运算符
- NOT NULL 约束类型

### 约束规范

## 功能性

## 概述
#### 普通完整性约束
## 概述
- 在列规范中
- `NOTSORTED` 选项

### `TRANSPOSE` 过程

### `NUMBER` 选项，SQL 过程
- 数字标记
- 数值类型

## 指定数据类型
## 指定列宽
- 数值类型、减少数值变量的存储空间、SAS 数值变量
- 为数值变量分配长度
- 在缩短长度的数值变量中保持精度
- 使用 `PROC COMPARE`,`WAYS` 过程

### `OBS=` 选项，`WHERE` 语句
- `OBS=` 数据集
- 输入源之间的一对多关系
- 输入源之间一对一关系

#### `OPTIONS` 语句，SQL 过程
- `BUFNO=` 选项
- `BUFSIZE=` 选项
- `COMPRESS=` 选项
- `FMTERR` 选项
- `FMTSEARCH=` 选项
- `FULLSTIMER` 选项
- `MAUTOLOCDISPLAY` 选项
- `MAUTOSOURCE` 选项
- 访问自动调用宏
- 访问自动调用宏 [2]
- `MCOMPILENOTE=` 选项
- `MEMRPT` 选项
- `MLOGIC` 选项
- `MLOGIC` 系统选项
- `MLOGICNEST` 选项
- `MLOGICNEST` 系统选项
- `MPRINT` 选项

## STD

### `MSGLEVEL=` 选项
- 确定 SAS 是否使用索引
- `MSGLEVEL=` 系统选项
- `STORED` 选项
- 存储编译宏设施
- 访问存储的编译宏
- `NOFMTERR` 选项
- `NOFULLSTIMER` 选项
- `NOMEMRPT` 选项
- `NOSTATS` 选项
- `NOSTIMER` 选项
- `REUSE=` 选项
- `SASAUTOS` 选项
- `SASAUTOS=` 选项
- `SASMSTORE` 选项
- `SASMSTORE=` 选项
- `STATS` 选项
- STIMER 选项
- 为每个语句写入计时信息





## 概述

## 单独使用 OUTER UNION 运算符
`OUTOBS`=选项，SQL 过程

### 通用格式

### 限制行处理

### 汇总函数与输出

### 添加字符常量

### 控制

### 详细报告

### 双倍行距

### 从...消除重复行

### 增强查询

### 列中的流动字符

### 包含行号

### SYMPUT 的支持

# OUTPUT 语句

## DATA 步

## MEANS 过程
### MEANS 过程
在 `PROC MEANS` 中使用 `WHERE=` 输出选项选择所需的类型，创建表

### 宏程序中的参数
### 位置参数
### 关键字参数
### 混合列表
### `PARM` 选项

### 关键字参数
### 混合列表
### `PARM` 选项

### 位置参数
### 混合列表
### `PARM` 选项，`%MACRO` 语句

### 模式
使用 `LIKE` 运算符选择模式
## 指定模式

### 百分号 (`%`)
宏程序和
### 指定指令

### 标记与性能

测试与评估
### 点号 (`.`)

# PICTURE 语句，FORMAT 过程

### `DATATYPE=` 选项
### 通用格式
### 指定指令
### 指定图片
### `PLOT` 过程
### `POINT=` 选项
### `SET (DATA)`
### `POINTO=` 数据集
### 位置参数
### 混合列表
### `PREFIX=` 选项，`TRANSPOSE` 过程

# PRIMARY KEY 约束
### 指定
### 一般完整性约束
## 概述
### 列规格

详细报告
### `UNIFORM` 选项
### `WHERE` 语句

# PROC FCMP
过程管理
## 概述
### 执行 `DATASETS` 过程
### RUN 组处理
### 使用 `PROC DATASETS` 使用不同 RUN 组

## 宏程序的条件处理
### 条件执行
### `%IF-%THEN` 与 `IF-THEN` 的比较
### 带条件处理的宏执行
### 语句语句部分的条件处理
### 大写敏感性





# 哈希对象

宏程序的迭代处理

## 概述

## 生成完整步骤

### 宏变量

## SAS 处理

## 创建和更新变量的规则

### SCL 程序中的宏变量

## 概述

### ``SYMPUTN` 过程

### `SYMGETN` 函数

### 在 DATA 步中获取宏变量值

`PUT` 函数

### `%SYSFUNC` 函数

### `PUT` 函数

### 间接引用宏变量

### 重置选项

### 限制循环次数

### 指定 SQL 选项

`SYMGET` 函数

`SYMGETN` 函数

`SYMPUT` 过程

### `SYMPUT` 过程

### 使用字面量配合 `SYMPUT`

### 使用 DATA 步变量配合 `SYMPUT`

### 使用 DATA 步表达式配合 `CALL SYMPUT`

### 使用 `CALL SYMPUT` 创建多个宏变量

### `SYMPUTN` 过程

### `SYMPUTX` 过程

### 性能测试与评估

### 使用视图 `PROMPT` 选项、SQL 过程

### 限制循环次数

`SYMPUT` 函数

`%SYSFUNC` 函数

`PUT` 函数

`User-Defined Formats`（自定义格式）

`PUTC` 函数

`PUTN` 函数

## 查询

比较资源使用

## 概述

### SAS 如何比较资源使用

### 影响 I/O 的因素

### 相对于数据集的子集

### 数据文件的页数

### 数据顺序

### 顺序读取解压缩压缩文件的成本

### 影响资源使用的其他因素

### 创建输出表

### 从详细报告创建表

### 字典表和

### 显示所有列

### 从输出中消除重复行

### 增强输出

### 估计观测值

### 可用索引

## 复合优化

SQL 查询可以通过索引进行优化

## 概述

### 节点

### 识别可以优化的条件

`WHERE` 条件无法被优化

### 顺序访问数据

### 直接访问数据

### 使用索引的收益与成本

### SAS 如何选择访问方法

### 选择列

### 指定子集标准

### 指定表

### 用于划分子数据的子查询

### 使用相关子查询划分子集

### 使用非相关子查询划分子集

### 使用计算值划分子行

### 插入行

### 排序行

## 概述

### 排序行

### 查询多个表

### 限制显示的行数

视图中的

#### 简介





# PROC SQL 视图

## 编写 SQL 过程步

## 引号

### 字面量标记

### 宏引用函数和

### 宏触发器和

### 引用宏变量

# R

## 原始数据文件名，存储

### 在 SAS 数据集中存储原始数据文件名
### 在外部文件中存储原始数据文件名

## 引用完整性约束

## 引用完整性约束
### 引用完整性约束 [2]

## REMOVE 语句，DATA 步

## RENAME 语句

### DATA 步步
### DATASETS 过程
### RENAME= 数据集选项
### REPLACE 语句，DATA 步

## REPORT 过程

## RESET 语句，SQL 过程

### 附加功能

## 概述

### 资源管理

### 评估需求

### 评估所在地的效率需求
### 评估您的技术环境
### 评估你的程序
### 评估您的数据

### 基准指南

### 比较可能的用量

## 概述
### SAS 如何比较资源使用情况
### 影响 I/O 的因素
### 子集相对于数据集的大小
### 数据文件中的页数
### 数据文件的顺序
### 顺序读取时解压缩文件的成本
### 影响资源使用的其他因素

### 比较汇总

### 比较不同汇总工具的资源使用情况
### 比较使用 PROC 的三种技巧的资源使用情况
### 计算机资源
### 效率权衡
### 系统选项

### RETAIN 语句，DATA 步
### `FIND` 方法
### REUSE= 数据集
### REUSE= 系统选项

### 右外连接

介绍外连接的类型
### 使用右连接
### 在表中的访问
### 计数所有
### 计数数量
### 在表中删除

### 从输出中消除重复行
处理唯一行与重复行
### 从输出中消除重复项
### 估算数量
### 处理插入错误

### 在表内插入

## 概述
### 概述 [2]
### 使用 SET 子句插入行
## 使用 VALUES 子句插入行
### 链接具有匹配值的表
### 限制显示数量

### 排序

## 概述
### 排序
### 对列排序
### 重复





# `MCOMPILENOTE` 选项
# `SYMBOLGEN` 系统选项
# `SASAUTOS=` 系统选项
# `SASMSTORE` 系统选项
# `SASMSTORE=` 系统选项

## SCL 程序
## 宏变量中的

## 概述
### `SYMPUTN` 过程
### `SYMGETN` 函数
### `SYMGETN` 函数
### `SYMPUTN` 过程
### 安全、表视图

## `SELECT` 子句
### `CREATE TABLE` 语句 (SQL)
### `INSERT` 语句 (SQL)

## `SELECT` 语句 (SQL)
## 概述
### 指定出现在多个表中的列
### 使用 `SELECT *`
### 使用 `FEEDBACK` 选项
### 从输出中消除重复行
## 概述
### `SELECT` 子句列和摘要函数处理

## `SELECT` 语句、`FORMAT` 过程
### 最佳实践
管理格式
### 使用 `PROC FORMAT` 配合 `FMTLIB` 记录格式
## 概述

## `SELECT` 语句、`SQL` 过程
### 最佳实践
### `CASE` 表达式
## 创建新列
### `DISTINCT` 关键字
### `FEEDBACK` 选项
### `FROM` 子句
### 指定表
### 指定多个表
### 生成笛卡尔积
### 引入联视图
### `SELECT` 函数
### 简介
### 一般形式
### 内连接
### 引入内连接语法
### 使用外连接风格语法创建内连接
### 外连接的一般形式
### 集合操作般形式

## `GROUP BY` 子句
### 数据分组
## 概述
### 分组和摘要函数处理
### 在没有 `GROUP BY` 子句的情况下使用摘要函数
配合 `GROUP BY` 子句使用摘要函数
### 使用 `HAVING` 子句分组

## `HAVING` 子句
### 其他功能
### 使用 `HAVING` 子句分组

## `INTO` 子句
### `INTO` 子句和 `NOPRINT` 选项
### 使用 `INTO` 子句创建变量
### 创建分隔的值列表
### `LABEL=` 选项
### `NOPRINT`

## `ORDER BY` 子句
## 概述
## 多列排序
### 行排序

### `SELECT` 子句
## 概述
### 指定出现在多个表中的列
### 使用 `SELECT *`
### 使用 `FEEDBACK` 选项
### 从输出中消除重复行
## 概述
### `SELECT` 子句列和摘要函数处理
### 选择列
### 在多个表中中的指定列
### 指定多个表名
### 指定子集标准
### 指定表

## 汇总数据
## 概述
### `SELECT` 子句列和摘要函数处理
### `VALIDATE` 关键字
查看所有列
### 显示所有列
### 使用 `SELECT *`





# 会话编译宏

## SET 子句

### INSERT 语句 (SQL)
## 概述
### 使用 SET 子句插入行

### UPDATE 语句 (SQL)

## SET 操作
### 列的合并与叠加
### 定义

## EXCEPT 集合操作符
### 介绍集合运算符
## 概述
### 在 `EXCEPT` 运算符上使用关键字 `ALL`
### 在 `EXCEPT` 运算符上使用关键字 `CORR`
### 在 `EXCEPT` 运算符上使用关键字 `ALL` 和 `CORR`

## INTERSECT 集合操作符
### 介绍集合运算符
## 概述
### 在 `INTERSECT` 运算符上使用关键字 `ALL`
### 在 `INTERSECT` 运算符上使用关键字 `CORR`
### 在 `INTERSECT` 运算符上使用关键字 `ALL` 和 `CORR`
### 通过关键字修改结果

## OUTER UNION 集合操作符
### 介绍集合运算符
## 概述
### 外外并与其他 SAS 技术

## 处理多个操作
### 使用多个集合运算符
### 处理多个集合操作
### 处理单条操作
### 处理唯一行与重复行

## UNION 操作符
### 介绍集合运算符
## 概述
### 在 `UNION` 运算符上使用关键字 `ALL`
### 在 `UNION` 运算符上使用关键字 `CORR`
### 在 `UNION` 运算符上使用关键字 `ALL` 和 `CORR`

## SET 语句，DATA 步
### `KEY=` 选项
### 使用多个 SET 语句
### 示例：在多多关系中使用 SET 语句
### `POINT=` 选项

## 简单索引
### 创建
### 简单索引与复合索引
### 介绍
### 索引类型

## SORT 过程
### `WHERE` 语句
### 排序
## 多列排序
### 行排序

## 类似 sounds-like 条件操作符
### 描述
### 通用形式
### `WHERE` 条件与 SOURCE 条目的存储

## SOURCE 条目，存储
## 概述
### CATALOG 过程
### CATALOG 方法
### `SOURCE` 选项，`%MACRO` 语句
### 访问存储宏
### 特殊字符，掩码
### `QUOTE` 函数 `NR` 函数
### `STR` 函数
### 宏支持
### 特殊标记
### 拼写

## 访问元数据
### 合并数据
### `DATA` 步合并
### `DATA` 步合并的执行
### `PROC` 连接的执行
### 使用多个 SET 语句

## 创建宏
### `INTO` 子句与 `NOPRINT` 选项
### 使用 `INTO` 子句创建变量
### 创建分隔值列表
### 详细报告
### `DOUBLE` 选项
### `ERRORSTOP` 选项
### `EXEC` 选项
### `FEEDBACK` 选项
### `FLOW` 选项
### 功能

## 表单 (form)
## 概述
### 当部分值匹配时
### `INOBS=` 选项
### INSERT 语句
### 数据连接
### `LOOPS=` 选项
### 索引管理
### `NODOUBLE` 选项
### `NOERRORSTOP` 选项

### NOEXEC 选项
## 使用 NOEXEC 选项





# 在 PROC SQL 报错后停止执行

## NOFLOW 选项

## NONUMBER 选项

## NOPROMPT 选项

## 示例

## 限制循环次数

## NOSTIMER 选项

## NUMBER 选项

## OUTOBS= 选项

## 概述

## 限制行处理

## PROMPT 选项

## 示例

## 限制循环次数

## 指定选项

## STIMER 选项

## 数据汇总工具

## UNDO_POLICY 选项

## 特性

## 步骤

## SQLOOPS 宏变量

## STATS 系统选项

## STIMER 选项，SQL 过程

STIMER 系统选项

## 为每个语句编写计时信息

## 使用 SAS 系统选项跟踪资源

存储

数组值

## 概述

## 创建数组

## 加载数组

## 读取实际值

## 最佳实践

压缩数据

## 压缩文件

## 未压缩数据的回顾

## 压缩后的数据结构

## 决定是否压缩文件

`COMPRESS=` 系统选项和 `COMPRESS=` 数据集

## 直接访问压缩数据集中的观测值

`POINTOBS=` 数据集选项

`REUSE=` 系统选项和 `REUSE=` 数据集选项

## SAS 如何压缩数据

## 使用 DATA 步视图节省空间

## 概述

## DATA 视图

## `DESCRIBE` 语句

## 创建和引用 SAS DATA 步视图

## 在一个程序中多次引用数据视图

## 在数据视图对数据进行多次处理

## 在不稳定数据上创建数据视图

在 autocall 库中

## CATALOG 过程

## 概述

## 创建 Autocall 库

## 默认 Autocall 库

## 访问 Autocall 宏

## 概述

## CATALOG 过程

## CATALOG 访问方法

## 外部文件宏定义

## 格式的永久位置

## 数据集中的文件名

## 外部文件文件名

## 减少字符变量

## 减少数值变量的空间

## SAS 如何存储数值变量

## 为数值变量分配长度

## 在短长度数值变量中保持精度

## 使用 PROC COMPARE

## 会话编译宏

# 存储编译宏机制

## 存储编译宏机制

## 创建存储编译宏

## 使用 `SOURCE` 选项

## 访问存储编译宏

## 访问存储宏代码

## `STORE` 选项，%MACRO` 语句





# 关联子查询与

# 索引与

# 非关联子查询与

# 子查询与

## 子集 IF 语句

### 子集 IF 语句的位置
### 使用子集 IF 语句与 WHERE 语句选择观测值
### IF 和 WHERE 语句之间的其他区别

## 子集行

### 功能
### 指定筛选标准
### 使用计算后的值
### 使用条件运算符

## 子集变量

### 使用 KEEP 和 DROP 语句及选项子集变量
### 使用 KEEP 和 DROP 语句及选项子集变量 [2]

## SUBSTR 函数

### 读取实际值
### 优化单个 WHERE 条件的优化
### 无法优化的 WHERE 条件

## sum 语句

## 数据汇总

### 工具比较

## 概述
### 各汇总工具的资源使用情况比较
### 使用 PROC MEANS 的三种技术的资源使用情况比较
### 理解类型

## GROUP BY 子句，SELECT 语句 (SQL)

### 汇总数据组
## 概述
### 分组与汇总函数处理
### SELECT 子句

## 汇总函数

## 概述
## 汇总函数
### GROUP BY 子句
### 在没有 GROUP BY 子句的情况下使用汇总函数
### 配合 BY 子句使用汇总函数
### 参数数量
### 针对数据组
### SELECT 子句
### 包含外部列
### 包含多个参数
### 包含参数

## SUMMARY 过程
### 多表格式
### 数据汇总工具

## 汇总统计量

### 类变量
### 使用 PROC MEANS 显示类变量的汇总统计
### 使用基础 PROC Step 合并所有类变量

## 数据合并

## 概述
### MEANS 过程
### Sum 语句

## MEANS 过程

### MEANS 过程
### 使用 PROC MEANS 显示类变量组合的汇总统计
### sum 语句

##符号表

### %GLOBAL 语句
### %LOCAL 语句
### 已定义
### 全局表
### 本地表
### 多个本地表
### %LOCAL 语句
### SYMBOLGEN 选项
### SYMGET 函数
## 概述
### SYMGET
### SYMPUT 过程
### 创建多个宏变量
### DATA step 表达式
### DATA step 变量
### 一般形式
### SYMPUT 过程
### 使用 CALL SYMPUT 创建多个宏变量
### SCL 程序支持
### SYMPUTN 过程
### SYMPUTX 过程

## SYSDATE 自动宏变量

## SYSDATE9 自动宏变量
## 概述
## 示例
### %SYSFUNC 函数
### SYSDAY 自动宏变量
### SYSERR 自动宏变量
### SYSJOBID 自动宏变量

## SYSLAST 自动宏变量
## 概述
## 示例
### SYSPARM 自动宏变量
### SYSSCP 自动宏变量
### 系统选项，跟踪资源
### SYSTENV 自动宏变量

## SYSTIME 自动宏变量
## 概述





# %SYSFUNC 函数

# `SYSVER` 自动宏变量

## T

### 表别名，指定

### `TABLE` 语句，`TABULATE` 过程

#### 表
#### 基础
#### 复制
#### 从查询结果创建
#### 仿其他创建
### 创建输出表

#### 带有完整性约束创建
## 概述
## 通用完整性约束
##### 显示完整性约束
##### 显示结构
##### 删除

#### 空表
## 概述
##### 概述 [2]
#### 生成卡卡尔积
#### 使用 SQL 过程连接
#### 创建方法
#### 查询多个
#### 指定
## 指定数据类型
#### 指定多个表名
#### 符号
#### 更新值

#### 视图
#### 使用其他视图引用内联视图
## 在内联视图中引用多个表
#### 合并表和视图
## 引言
##### 创建视图以增强安全性
##### 虚拟
`TABULATE` 过程
`CLASS` 语句
`FORMAT` 语句
`FORMAT=` 选项
`MLF` 选项
`multilabel` 格式
`TABLE` 语句
#### 数据汇总工具
#### 性能测试
#### 文本、宏变量引用和
#### `TITLE` 语句，`SQL` 过程
#### 标题，指定

#### 标记
#### 字面量
#### 宏触发器和
#### 宏变量和

#### 名称
#### 标记化
#### 宏触发器
#### 数字
#### 百分号和
#### 特殊

#### 事务集
## 概述
##### 使用 `UPDATE` 语句
#### 为合并构建数据
#### 在 `PROC TRANSPOSE` 中使用 `BY` 语句
#### 排序 `Work.Ctarget2` 数据集
#### 重组 `Sasuser.Monthsum` 数据集
#### 排序 `Work.Mnthsum2` 数据集
#### 完成合并
`TRIM` 函数
`TYPE=` 数据集选项
`TYPES` 语句，`MEANS` 过程

## U

`UNDO_POLICY` 选项，`SQL` 过程
`UNIFORM` 选项，`PRINT` 过程

`UNION` 运算符
`ALL` 关键字和
#### 在 `UNION` 运算符上使用关键字 `ALL`
#### 在 `UNION` 运算符上使用关键字 `ALL` 和 `CORR`
#### 在 `UNION` 运算符上使用关键字 `CORR`
#### 在 `UNION` 运算符上使用关键字 `ALL` 和 `CORR`

#### 介绍集合运算符
## 概述
`UNIQUE` 约束类型
##### 约束指定
## 通用完整性约束
## 概述
##### 列指定中

#### 唯一索引
#### 唯一索引
#### 示例：创建复合唯一索引

`UNIQUE` 选项





# DATA 步

# MODIFY 语句 (DATA)

## UNIVARIATE 过程（单变量分析）

### 高效使用条件逻辑
## 概述
更新过程
控制

## 概述
##### 监控 I/O 错误状态
##### 在 `%SYSRC` 使用 `_IORC_`
##### 用于视图 (views)

### UPDATE 语句，DATA 步

## UPDATE 语句，SQL 过程

#### 审计轨迹和
CASE 表达式

### 使用不同的表达式更新行
## PROC SQL 如何根据 CASE 表达式更新行
## Case 操作数的工作原理
#### 控制 UNDO 处理
#### 功能
#### 通用形式
#### SET 子句
#### 更新表行值
#### 更新视图

### WHERE 子句
#### 使用相同的表达式更新行
#### 使用不同的表达式更新行
## 概述
#### UPDATEMODE= 选项，MODIFY 语句 (DATA)
#### 用户变量
#### 用户定义宏
`%LET` 语句和
定义的全局表以及
`USER_VAR` 语句
`USING` 子句，`CREATE VIEW` (SQL)

### `VALIDATE` 关键字
#### `VALUE` 语句，合并数据
#### 用户定义格式
#### 创建非重叠范围的审查
#### `MULTILABEL` 选项创建具有重叠范围的格式
#### 值/标识符对

### 审计轨迹
#### 审计变量
#### `_ATOPCODE_` 变量的值
#### 最佳实践
#### 字符

class
#### 使用 PROC MEANS 显示类变量组合的汇总统计
#### 使用基础的 PROC MEANS 步合并所有类变量
#### 理解类型
#### 在 PROC MEANS 中使用 `TYPES` 语句合并类变量
#### 在 PROC MEANS 中使用 `NWAY` 选项合并类变量

### 哈希对象 (hash objects) 和
key
#### 在数据中列出
#### 减少数值数据空间
#### 为数值分配长度
#### 在 SAS 中保持精度
`PROC COMPARE`
#### 子集

### `VIEW=` 选项，DATA 步
#### 视图
#### 优势
节省存储空间
## 概述
#### DATA 步视图
#### `DESCRIBE` 语句
#### 创建和引用 SAS DATA 步视图
#### 在程序中多次引用数据视图
#### 对数据视图中的数据进行多次扫描





# 在不稳定数据上创建数据视图

## 创建
- 删除
- 显示定义
- 丢弃
- 增强表安全功能

## 使用 PROC SQL 视图
- 使用 `PROC SQL` 视图 [2]
- 使用 `PROC SQL` 视图
- 在查询中使用

## 内联
## 引入内联视图
- 通过其他视图或表引用内联视图
- 在内联视图中引用多个表
-为内联视图分配别名
- librefs 以及管理表和
- 通过其他视图或表引用内联视图
- 在内联视图中引用多个表
- 关联多个表和视图

### 简介
### 创建视图以增强表安全
- 更新
`VIEWTABLE` 窗口
- 虚拟表

## W
### `WAYS` 语句，`MEANS` 过程

### `WHERE` 子句
`SELECT` 语句 (SQL)
- 指定子集筛选标准
- 指定连接条件
- 概述
使用 `CALCULATED` 关键字
`UPDATE` 语句 (SQL)
- 使用相同的表达式更新行
- 使用不同的表达式更新行
- 概述
`WHERE` 条件复合优化和索引使用控制
- 未优化
- 优化中
- 打印分位数信息

### `WHERE` 语句 `DATA` 步
- 使用子集 `IF` 与 `WHERE` 语句选择观测值
- `IF` 和 `WHERE` 语句之间的其他差异
- 概述
- 直接访问数据
- 示例
- 概述
- 复合优化
`PRINT` 过程
`SORT` 过程
`WHERE=` 数据集选项

### 扫描器 (Word scanner)
- 宏触发和分词以及

