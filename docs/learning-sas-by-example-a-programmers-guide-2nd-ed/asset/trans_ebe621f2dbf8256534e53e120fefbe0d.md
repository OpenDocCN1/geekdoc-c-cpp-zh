

# 以 SAS 为例的学习：程序员指南，第二版

从永久 SAS 数据集 `Survey` 中提取 `Gender` 值为 `F` 的观测值。使用 `WHERE` 语句实现此操作的方法如下：

## 程序 10.1：使用 WHERE 语句子集 SAS 数据集

```sas
data Females;
  set Learn.Survey;
  where Gender = 'F';
```

请记住，`WHERE` 语句中变量必须全部来自 SAS 数据集。通过读取原始数据或赋值语句创建的变量不能以此方式使用。在程序 10.1 中，数据集 `Females` 包含了 `Survey` 数据集中所有 `Gender` 值为 `F` 的观测值。以下是该数据集的列表：

## 10.1：数据集 Females 列表

| ID | Gender | Age | Salary | Ques1 | Ques2 | Ques3 | Ques4 | Ques5 |
|---|---|---|---|---|---|---|---|---|
| 002 | Female | 51+ | $76,123 | | | Strongly agree | | Disagree |
| 004 | Female | 51+ | $128,000 | Strongly agree | | No option | | Disagree |
| 007 | Female | 30 to 50 | $76,100 | Strongly agree | | No option | | Agree |

注意，数据集 `Females` 包含了 `Survey` 数据集中存在的所有变量。如果你不需要输入数据集（`SET` 语句中的数据）中的所有变量，可以使用 `KEEP=` 或 `DROP=` 数据集选项。例如，为了保留 `ID`、`Gender`、`Age` 和 `Ques1-Ques5`，可以使用以下方法：

## 程序 10.2：演示 KEEP= 数据集选项

```sas
data Females;
  set Learn.Survey(keep= ID Gender Age Ques1-Ques5);
  where Gender = 'F';
```

在输入数据集上使用 `KEEP=` 数据集选项与在 `DATA` 语句某处放置 `KEEP` 语句之间存在重要区别。在这个示例中，变量 `Salary` 不在程序数据向量 (PDV) 中，因为没有没有包含在保留变量列表中。使用 `KEEP=` 数据集选项列出八个变量的替代方案是使用 `DROP=` 数据集。虽然这可以节省输入量，但使用 `KEEP=` 数据集选项而不是 `DROP=` 可以让阅读程序的人知道你从 `Survey` 数据集中引入了哪些变量。如果你使用 `DROP=Salary`，除非你已经有了该数据集的变量列表，否则不知道从 `Survey` 数据集中引入了哪些变量。参见第 2 章“SAS 如何工作（内部原理）”。

## 第 10 章：子集与合并 SAS 数据集

> **注意：** 如果你使用 `KEEP` 语句列八个变量而不是 `KEEP=` 数据集选项，所有变量（包括 `Salary`）都会位于 PDV 中，但不会写入 `Females` 数据集中。如果输入数据集包含大量变量，而你只需要在新数据集中包含几个，使用 `KEEP=` 数据集选项比 `KEEP` 语句更高效。

你必须记住，当你使用 `KEEP=` 数据集选项时，不在保留列表中的变量在 DATA 步中也不可用。

## 10.3 在一个 DATA 步中创建多个子集

你可以从一个输入数据集创建多个 SAS 数据集（SQL 无法做到）。参考上一个示例，你可以在一步中创建一个只包含女性的数据集和一个只包含男性的数据集，如下：

## 程序 10.3：在一个 DATA 步中创建两个数据集

```sas
data Males;
  set Learn.Survey;
  if Gender = 'F' then output Females;
  else if Gender = 'M' then output Males;
run;
```

注意，你必须在 `OUTPUT` 语句之后命名数据集。如果没有，SAS 将观测值输出到 `DATA` 语句列出的所有数据。

## 10.4 向 SAS 数据集添加观测值

假设你想从几个相似的数据集创建一个数据集。例如，你的公司可能每月将数据收集到单独的数据集中，而你想分析全年的数据。你可以在 `SET` 语句上列出任意数量的数据集，SAS 将将所有观测值合并形成单个数据集。例如，查看这里数据集 `One` 和 `Two` 的列表：

## 图 10.2：数据集 One 和 Two 列表

| Data Set One | | | | Data Set Two | | | | |
|---|---|---|---|---|---|---|---|---|
| Obs | ID | Name | Weight | Obs | ID | Name | Weight |
| 1 | 7 | Adams | 210 | 1 | 9 | Shea | 120 |
| 2 | 1 | Smith | 190 | 2 | 3 | O'Brien | 180 |
| 3 | 2 | Schneider | 110 | 3 | 5 | Bessler | 207 |
| 4 | 4 | Gregory | 90 | | | | | |

每个数据集都包含相同的变量。此外，两个数据集中 `Name` 的存储长度也是相同的。合并这些数据集的一种方法如下：

## 程序 10.4：使用 SET 语句合并两个数据集的观测值

```sas
data One_Two;
  set One Two;
run;
```

这是输出结果：

## 图 10.3：数据集 One_Two 列表

| Obs | ID | Name | Weight |
|---|---|---|---|
| 1 | 7 | Adams | 210 |
| 2 | 1 | Smith | 190 |
| 3 | 2 | Schneider | 110 |
| 4 | 4 | Gregory | 90 |
| 5 | 9 | Shea | 120 |
| 6 | 3 | O'Brien | 180 |
| 7 | 5 | Bessler | 207 |

数据集 `One` 的所有观测值之后是数据集 `Two` 的所有观测值。SAS 将此过程称为数据集连接。这看起来足够简单。但如果你在两个不包含相同变量的数据集上使用 `SET` 语句会发生什么呢？为了查看结果，这里是数据集 `Three`：

## 图 10.4：数据集 Three 列表

| Obs | ID | Gender | Name |
|---|---|---|---|
| 1 | 10 | M | Hovath |
| 2 | 15 | F | Stevens |
| 3 | 20 | M | Brown |

数据集 `Three` 包含一个新的变量 `Gender`，且不包含 `Weight`。从列表中无法看出，但两个数据集中的 `Name` 变量是相同的。让我们对 `One` 和 `Three` 使用 `SET` 语句看看会发生什么。

## 程序 10.5：对包含不同变量的数据集使用 SET 语句

```sas
data One_Three;
  set One Three;
run;
```

这是输出：

## 图 10.5：数据集 One_Three 列表

| Obs | ID | Name | Weight | Gender |
|---|---|---|---|---|
| 1 | 7 | Adams | 210 | |
| 2 | 1 | Smith | 190 | |
| 3 | 2 | Schneider | 110 | |
| 4 | 4 | Gregory | 90 | |
| 5 | 9 | Shea | 120 | |
| 6 | 3 | O'Brien | 180 | |
| 7 | 5 | Bessler | 207 | |
| 8 | 10 | Hovath | | M |
| 9 | 15 | Stevens | | F |
| 10 | 20 | Brown | | M |

