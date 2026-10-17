
`set learn.Blood(obs=5)`

| Subject | WBC | RBC | Percent_RBC | Percent_WBC |
|---|---|---|---|---|
| 1 | 7710 | 7.40 | 135% | 109% |
| 2 | 6560 | 4.70 | 86% | 93% |
| 3 | 5690 | 7.53 | 137% | 81% |
| 4 | 6680 | 6.85 | 125% | 95% |
| 5 | | 7.72 | 141% | |
| 6 | 6140 | 3.69 | 67% | 87% |
| 7 | 6550 | 4.78 | 87% | 93% |
| 8 | 5200 | 4.96 | 90% | 74% |
| 9 | | 5.66 | 103% | |
| | 7710 | 5.58 | 104% | 109% |

- 1. 使用 `PROC PRINT` 来列出数据集中的前五个观测值。使用系统宏变量 `&SYDAY`（返回星期几）、`&SYSDATE` 和 `&SYSTIME` 来自定义标题（参见下例，该例是在周五运行的）：

> Listed Produced on Sunday, 10DEC2017 at 10:02

| Date | Price |
|---|---|
| 01/01/2017 | $34 |
| 01/02/2017 | $39 |
| 01/03/2017 | $39 |
| 01/04/2017 | $30 |
| 01/05/2017 | $35 |

- 2. 使用 `%LET` 重写以下程序，将 DO 循环的起始和结束值赋值给宏变量。请确保这些值也打印在 `PROC PRINT` 输出中。

```
data Sqrt_Table;

 n = 1 to 5;

 Sqrt_n = sqrt(n);

 output;

run;
```

```
data Sqrt_Table;

 n = 1 to 5;

 Sqrt_n = sqrt(n);

 output;

run;
```

- 3. 创建一个宏 `call Stats`，使其变为通用。使用作为参数的数据集 `DS`、类变量 `Classes` 以及 `VAR` 语句中的变量 `Vars`：

```
title "Statistics from Data Set";

proc means data=DS dec=1;

Class;

var;

run;
```
`%Stats(DS=Bicycles, Class=Country, Vars=Units)`

使用列出数据集的前四个观测值。你的输出应该所示：

```
data _null;

  set learn.Blood(obs=5)

```
```

| Subject | WBC | RBC | Percent_RBC | Percent_WBC |

|---|---|---|---|---|

| 1 | 7710 | 7.40 | 135% | 109% |

| 2 | 6560 | 4.70 | 86% | 93% |

| 3 | 5690 | 7.53 | 137% | 81% |

| 4 | 6680 | 6.85 | 125% | 95% |

| 5 | | 7.72 | 141% | |

| 6 | 6140 | 3.69 | 67% | 87% |

| 7 | 6550 | 4.78 | 87% | 93% |

| 8 | 5200 | 4.96 | 90% | 74% |

| 9 | | 5.66 | 103% | |

| | 7710 | 5.58 | 104% | 109% |
- 5. 对于 `fitness` 数据集列出三个变量（`TimeMile`, `RestPulse`, `MaxPulse`）。除了这些变量外，创建三个新变量（调用 `TimeMile`, `RestPulse`, `MaxPulse`），表示平均值的百分比。首先通过 `PROC MEANS` 计算平均值。接下来，在 `DATA _NULL_` 步中使用 `CALLPUT` 创建宏变量。

## 第 26 章：介绍结构化查询语言

26.1 介绍 ................................................................ 437

26.2 基础知识 ................................................................ 437

26.3 连接两个表 (Merge)................................................................ 439

26.4 左连接、右连接和全连接...................................................... 444

26.5 连接数据集........................................................... 446

26.6 使用汇总函数........................................................... 449

26.7  ORDER 子句............................................................... 450

26.8 模糊匹配示例.................................................. 451

26.9 习题 ................................................................ 452

### 26.1 介绍

`PROC SQL`（结构化查询语言——通常读作 sequel）为查询和合并 SAS 数据提供了替代方案。某些任务 `PROC SQL` 执行得比 `DATA` 步更好、更简单。其他任务使用 `DATA` 步可能更简单或更高效。你可能对 SQL 比 `DATA` 步熟悉，或者反之。最好的建议是学习两者，并在情况下使用最适合你的工具。

本章仅涉及 `PROC SQL` 的基础知识。SAS 出版了一些优秀的书籍你可能需要。请访问 SAS Help Center http://go.documentation.sas.com 或 SAS Press 系列书籍获取更多关于 `PROC SQL` 的信息。

### 26.2 基础知识

熟悉 SAS 语法的程序员在开始使用 `PROC SQL` 时可能会遇到困难。例如，在 `PROC SQL` 中使用逗号而不是空格来分隔变量和数据集名称。你可能会发现自己在不该用的地方使用了分号。让我们从一些简单的查询数据集和从较大的 SAS 数据集子集创建 SAS 数据集的示例开始。

# 438 实例学习 SAS：程序员指南，第二版

在向您展示程序之前，有必要先介绍一些术语。下表列出了 SAS 术语对应的 SQL 术语：

| SAS 术语 | SQL 等效项 |
|---|---|
| 数据集 `Data set` | 表 `Table` |
| 观测 `Observation` | 行 `Row` |
| 变量 `Variable` | 列 `Column` |

在第一个示例中，我们将使用名为 `Health` 的 SAS 数据集。列表如下：

# 图 26.1：数据集 Health 的列表

![](img/6f22e781b7ad899a8ef005cc7e22e7e0_444_0.png)

如果你想打印此数据的子集（选择所有身高超过 65 英寸的主体），可以提交以下查询：

# 程序 26.1：演示来自单个数据的简单查询

```
title "Subjects from Health with Height > 65%";
proc sql;
  select Subj,
         Weight
  from Learn.Health
  where Height gt 65;
quit;
```

该查询以 `SELECT` 关键字开始，您在其中列出您需要的变量。注意，列表中的变量之间用逗号分隔的（空格无效）。`FROM` 关键字指定了您想要读取的数据集。`WHERE` 子句描述了您想要的特定子集。

`SELECT`、`FROM` 和 `WHERE` 构成了一个单一查询，并用分号结束。在您的示例中，您没有创建输出数据集，因此默认情况下，此查询的结果将作为列表发送到 Output 窗口（或您指定的任何输出位置）。最后，查询以 `QUIT` 语句结束。您不需要 `RUN` 语句，因为 `PROC SQL` 在指定完整查询后会立即执行。如果你不包含 `QUIT` 语句，`PROC SQL` 将留在内存中以供下一个查询使用。

第 26 章：介绍结构化查询语言 439

以下是该程序产生的输出：

图 26.2：程序 26.1 的输出

| Subj | Height | Weight |
| --- | --- | --- |
| 001 | 68 | 155 |
| 003 | 74 | 250 |

如果你想从数据选择所有变量，可以使用星号 `*`，如下：

程序 26.2：使用星号选择数据集中的变量

```
proc sql;
  select *\  from Learn.Health
  where Height gt 65;
quit;
```

如果你想将查询结果存储在 SAS 数据集中，请包含一个 `CREATE TABLE` 语句，如下：

程序 26.3：使用 `PROC SQL` 创建 SAS 数据集

```
proc sql;
  create table Height65 as
  select *\  from Learn.Health
  where Height gt 65;
quit;
```

## 26.3 合并两个表 (Merge)

使用两个表（上一个示例中使用）和 `Demographic` 来演示使用 `PROC SQL` 执行连接的各种方法。以下是这两个表的列表：

图 26.3：表 Health 和 Demographic 的列表

| Subj | Height | Weight |
| --- | --- | --- |
| 001 | 68 | 155 |
| 003 | 74 | 250 |
| 004 | 63 | 110 |
| 005 | 60 | 95 |

| Subj | DOB | Gender | Name |
| --- | --- | --- | --- |
| 001 | 10/15/1960 | M | Friedman |
| 002 | 08/01/1955 | M | Stern |
| 003 | 12/25/1988 | F | McGoldrick |
| 005 | 05/28/1949 | F | Chien |

你可以通过列出 `SELECT` 子句中的所有变量以及 `FROM` 子句中的两个数据集从表中选择变量。如果两个数据集中具有相同的变量，你需要一种方法来区分使用哪个数据集。方法如下：

# 程序 26.4：合并两个表（笛卡尔积）

```
title "Demonating a Cartesian Product";
proc sql;
    select Health.Subj,
         Demographic.Subj,
         Height,
         Weight,
         Name,
         Gender
    from Learn.Health,
         Learn.Demographic;
quit;
```

由于 `Subj` 列于两个表中，你为变量加上了表名前缀。稍后你会发现可以稍微简化。此查询的结果被称为笛卡尔积，代表了第一个表的行与第二个表的行的所有组合。列表显示了两个具有 `Subj` 表头的列。以下是结果的列表：

图 26.4：程序 26.4 的输出

# 演示笛卡尔积

| Subj | Subj | Height | Weight | Name | Gender |
| --- | --- | --- | --- | --- | --- |
| 001 | 001 | 68 | 155 | Friedman | M |
| 001 | 002 | 68 | 155 | Stern | M |
| 001 | 003 | 68 | 155 | McGoldrick | F |
| 001 | 005 | 68 | 155 | Chien | F |
| 003 | 001 | 74 | 250 | Friedman | M |
| 003 | 002 | 74 | 250 | Stern | M |
| 003 | 003 | 74 | 250 | McGoldrick | F |
| 003 | 005 | 74 | 250 | Chien | F |
| 004 | 001 | 63 | 110 | Friedman | M |
| 004 | 002 | 63 | 110 | Stern | M |
| 004 | 003 | 63 | 110 | McGoldrick | F |
| 004 | 005 | 63 | 110 | Chien | F |
| 005 | 001 | 60 | 95 | Friedman | M |
| 005 | 002 | 60 | 95 | Stern | M |
| 005 | 003 | 60 | 95 | McGoldrick | F |
| 005 | 005 | 60 | 95 | Chien | F |

如果你使用此查询创建 SAS 数据集，将只有一个名为 `Subj` 的变量。如果你想保留每个数据集的 `Subj` 值，可以像这样重命名列：

# 程序 26.5：重命名两个 Subj 变量

```
title "Renaming the Two Subj Variables";
proc sql;
  select Health.Subj as Health_Subj,
       Demographic.Subj as Demog_Subj,
       Height,
       Weight,
       Name,
       Gender
from Learn.Health,
     Learn.Demographic;
quit;
```

运行此查询的结果如下：

图 26.5：程序 26.5 的部分输出

| Health_Subj | Demog_Subj | Height | Weight | Name | Gender |
|---|---|---|---|---|---|
| 001 | 001 | 68 | 155 | Friedman | M |
| 001 | 002 | 68 | 155 | Stern | M |
| 001 | 003 | 68 | 155 | McGoldrick | F |
| 001 | 005 | 68 | 155 | Chien | F |
| 003 | 001 | 74 | 250 | Friedman | M |
| 003 | 002 | 74 | 250 | Stern | M |
| 003 | 003 | 74 | 250 | McGoldrick | F |

注意两个主体列已被重命名。

除了添加 `WHERE` 子句外，下一个程序还展示了如何区分两个标题为 `Subj` 的列。最后，接下来的程序使用了更简单的方法在 `SELECT` 子句中命名两个 `Subj` 变量。它是这样的：

程序 26.6：使用别名简化变量命名

```
title "Matching Subj Numbers from Both Tables";
proc sql;
   select H.Subj as Subj_Health,
         D.Subj as Subj_Demog,
         Height,
         Weight,
         Name,
         Gender
   from Learn.Health as H,
        Learn.Demographic as D
   where H.Subj eq D.Subj;
quit;
```

首先查看 `FROM` 子句。为了方便命名两个数据集中同名的变量，你为变量加上了表名前缀。在此程序中，添加了 `WHERE` 子句，限制结果为两个表中具有相同的编号。以下是其结果：

```
proc sort data=Learn.Health out=Health
  by Subj;
run;

proc sort data=Learn.Demographic out=Demographic;
  by Subj;
run;

data Inner;
  merge Health(in=in_Health)
         Demographic(in=in_Demographic));
  by Subj;
  if in_Health and in_Demographic;
run;

title "Performing an Inner Join Using DATA Step";
proc print data=Inner;
  id Subj;
run;
```

# 444 实例学习 SAS：程序员指南，第二版

使用 时不需要先对数据集排序很好吗？（尽管 SQL 会为你完成。）以下是 `Inner` 数据集的列表：

图 26.7：程序 26.7 的输出

| Subj | Height | Weight | DOB | Gender | Name |
|---|---|---|---|---|---|
| 001 | 68 | 155 | 10/15/1960 | M | Friedman |
| 003 | 74 | 250 | 12/25/1988 | F | McGoldrick |
| 005 | 60 | 95 | 05/28/1949 | F | Chien |

这与 `PROC SQL` 表相同，区别在于只有一个 `Subj` 变量。

## 26.4 左连接、右连接和全连接

程序 26.6 的另一种方案是使用 `INNER JOIN` 术分隔两个表名，如下：

程序 26.8：执行内连接
