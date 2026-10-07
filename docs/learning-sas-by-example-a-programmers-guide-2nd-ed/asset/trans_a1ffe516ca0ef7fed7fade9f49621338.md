
SELECT、FROM 和 WHERE 构成了一个单一查询，并以分号结束。在你的示例中，你没有创建输出数据集，因此默认情况下，此查询的结果将以列表的形式发送到输出窗口（或你指定的任何输出位置）。最后，查询以一个 `QUIT` 语句结束。你不需要 `RUN` 语句，因为 PROC SQL 在指定一个完整的查询后就会执行。如果你不包含 `QUIT` 语句，PROC SQL 将留在内存中以便进行另一个查询。

# 第 26 章：介绍结构化查询语言 439

以下是该程序产生的输出：

图 26.2：程序 26.1 的输出

| Subj | Height | Weight |
|---|---|---|
| 001 | 68 | 155 |
| 003 | 74 | 250 |

如果你想从数据集中所有变量，可以使用星号 (`*`)，如下所示：

程序 26.2：使用星号选择数据集中的所有变量

```
proc sql;
select *
from Learn.Health
where Height gt 65;
quit;
```

如果你想将查询结果存储在 SAS 数据集中，请包含一个 `CREATE TABLE` 语句，如下所示：

程序 26.3：使用 PROC SQL 创建 SAS 数据集

```
proc sql;
create table Height65 as
select *
from Learn.Health
where Height gt 65;
quit;
```

## 26.3 合并两个表 (Merge)

使用两个表（上一个示例中的表）和 Demographic 表，用于演示使用 PROC SQL 执行连接的各种方法。以下是这两个表的列表：

图 26.3：Health 和 Demographic 表的列表

| Subj | Height | Weight | Subj | DOB | Gender | Name |
|---|---|---|---|---|---|---|
| 001 | 68 | 155 | 001 | 10/15/1960 | M | Friedman |
| 003 | 74 | 250 | 002 | 08/01/1955 | M | Stern |
| 004 | 63 | 110 | 003 | 12/25/1988 | F | McGoldrick |
| 005 | 60 | 95 | 005 | 05/28/1949 | F | Chien |

440 实例教程学习 SAS：程序员指南，第二版

你可以通过在 `SELECT` 子句中列出所有感兴趣的变量，并在 `FROM` 子句中列出两个数据集，从两个表中选择变量。如果一个变量在两个数据集中具有相同的名称，你需要一种方法来区分使用哪一个数据集。操作方法如下：

# 程序 26.4：连接两个表（笛卡尔积）

```
title "Demonstrating a Cartesian Product";
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

因为 `Subj` 列存在于两个表中，所以你在变量名前前面加上了表名。你几分钟后就会发现你可以简化这部分。此查询的结果被称为笛卡尔积，它代表了第一个表的行与第二个表的行之间所有可能的组合。列表显示了两个列，标题都为 `Subj`。

以下是结果的列表：

# 图 26.4：程序 26.4 的输出

# 演示笛卡尔积

| Subj | Subj | Height | Weight | Name | Gender |
|---|---|---|---|---|---|
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

如果你使用此查询来创建 SAS 数据集，将只有一个名为 `Subj` 的变量。如果你想保留每个数据集中的 `Subj` 值，你可以重命名这些列，如下所示：

程序 26.5：重命名两个 Sub 变量

```
title "Renaming the Two Sub Variables";
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

运行此查询得到结果结果：

442 实例教程学习 SAS：程序员指南，第二版

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

注意，两个主题列已重命名。

当你想要对两个表中相似的名称进行匹配（有时是模糊合并）时，笛卡尔积特别有用。此表中的行数等于第一张表的行数乘以第二个表的行数。在实践中，你可能希望添加一个 `WHERE` 子句来限制选择的行。在我们的程序中，我们添加了 `WHERE` 子句，仅选择两个表中主题相同的行。

除了添加 `WHERE` 子句外，下一个程序还展示了如何区分两个标题为 `Subj` 的列。最后，下一个程序使用更简单的方法在 `SELECT` 子句中命名两个 `Subj` 变量。其代码如下：

# 程序 26.6：使用简化命名变量

```
title "Matching Subj Numbers from Both Tables";
proc sql;
    select H.Subj as Subj_Health,
         D.Subj as Subj_Demog,
         Height,
         Name,
         Gender
    from Learn.Health as H,
         Learn.Demographic as D
    where H.Subj eq D.Subj;
quit;
```

首先查看 `FROM` 子句。为了给不同表中具有相同名称的变量命名，在这个程序中为它们每个都 使用了别名 `H` 和 `D`。你可以将这些别名作为 `SELECT` 子句中的前缀（`H.Subj` 和 `D.Subj`）。在程序程序中，添加了 `WHERE` 子句，将结果限制为两个表中主题编号相同的行。结果如下：

# 第 26 章：介绍结构化查询语言 439

图 26.6：来自两个表的主题编号

| Subj_Health | Subj_Demog | Height | Weight | Name | Gender |
|---|---|---|---|---|---|
| 001 | 001 | 68 | 155 | Friedman | M |
| 001 | 002 | 68 | 155 | Stern | M |
| 001 | 003 | 68 | 155 | McGoldrick | F |
| 001 | 005 | 68 | 155 | Chien | F |
| 003 | 001 | 74 | 250 | Friedman | M |
| 003 | 002 | 74 | 250 | Stern | M |
| 003 | 003 | 74 | 250 | McGoldrick | F |

