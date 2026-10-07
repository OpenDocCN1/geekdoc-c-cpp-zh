

# 使用 PROC SORT

```
1 1.5
1 1.8
PROC SORT DATA=MYDATA OUT=S1; BY RECTIME;
Title 'Sorting Example - Ascending';
PROC PRINT DATA=S1;
RUN;
```

注意，此程序对数据进行排序并将结果存储在名为 S1 的 SAS 数据文件中。提交代码并观察排序后的输出。

2. 使用以下代码编写第二个 PROC SORT 和 PROC PRINT 语句，对 MYDATA 进行降序排序，并将结果保存在 S2 中：

```
PROC SORT DATA=MYDATA OUT=S2; BY DESCENDING RECTIME;
```

提交修改后的程序。注意，这两个 PROC 例程产生了两个不同的结果：数据集 S1 按升序排序，数据集 S2 按降序排序，如表 4.10 所示。

# 表 4.10 SAS 输出：升序和降序排序示例 - 升序示例 - 降序示例

| Obs | GROUP | RECTIME | Obs | GROUP | RECTIME |
|---|---|---|---|---|---|---|
| 1 | 2 | 1.5 | 1 | 2 | 4.2 |
| 2 | 1 | 1.8 | 2 | 2 | 3.8 |
| 3 | 1 | 2.1 | 3 | 2 | 3.6 |
| 4 | 1 | 2.8 | 4 | 1 | 3.1 |
| 5 | 2 | 3.1 | 5 | 1 | 2.8 |
| 6 | 2 | 3.6 | 6 | 1 | 2.1 |
| 7 | 1 | 4.2 | 7 | 1 | 1.8 |

PROC SORT 还有 DROP、KEEP 和 RENAME 等其他选项。这些将在下面的示例中进行说明。

# 动手示例

假设你正在对数据集进行排序以便进行合并（将在下一节讨论），并且你需要将变量名 ID 改为 CASE。

1. 打开程序文件 DSORT2.SAS。

```
PROC SORT DATA="C:\SASDATA\SOMEDATA"
OUT=ANALYSIS;
(KEEP=ID AGE GENDER RENAME=( ID=SUBJECT AGE=DXAGE) );
BY ID;
RUN;
PROC PRINT DATA=ANALYSIS;RUN;
```

（继续）

# 第 4 章：为分析准备数据

（继续）

注意，OUT= 语句后面有一组括号。括号内是一个 KEEP= 语句，用于指定在输出文件 ANALYSIS 中保留的变量。括号内是另一个语句 RENAME，它后面有自己的参数。在 RENAME= 的括号内有两个语句，将旧变量重命名为新名称。该 RENAME 语句的语法为：

```
RENAME = (oldname1=newname1 oldname2=newname2, etc...)
```

因此，此代码重命名两个变量并在输出中保存了四个变量。提交此代码并观察表 4.11 显示（部分）结果。

然而，注意 KEEP 必须是原始变量名，而不是新名称。注意 ID 和 AGE 被保留了，但在新数据集中，它们被命名为 SUBJECT 和 GENDER。

- 2. 从 KEEP 语句中删除变量 GENDER。重新运行程序，查看结果不再包含 GENDER 列。

- 3. 将 GP 改为 GROUP。重新运行代码并观察变化后的结果。

表 4.11 SAS 输出：显示升序和降序
| Obs | SUBJECT | GP | DXAGE | GENDER |
|---|---|---|---|---|
| 1 | 101 | A | 12 | Female |
| 2 | 102 | A | 11 | Female |
| 3 | 104 | B | 12 | Female |
| 4 | 110 | A | 12 | Male |
| 5 | 103 | B | 0 | Male |

# 4.7 追加和合并数据集

其他有用的 SAS 数据处理能力是追加（Appending）和合并（Merging）。

- Adding（追加）向现有数据集中添加记录。
- Merging（合并）通过两个数据集中存在的键标识符（通常是标识代码）向数据集添加变量。

# 4.7.1 追加两个数据集

追加数据集将两个或多个数据集的记录结合在一起（有时被称为垂直合并）。例如，假设数据在两个地点收集，你想将这些数据集合并成一个 SAS 数据集进行分析。这些数据集必须至少有一些共同的变量。追加通过在 SET 语句中包含多个数据集名称来实现。例如：

# 追加和合并数据集

DATA NEW; SET OLD1 OLD2;

创建了数据集 NEW，它由 OLD1 数据集中的记录以及 OLD2 数据集中的记录组成。

# 动手示例

在此示例中，程序将其中一个 SAS 数据集追加到另一个之后，创建一个更大的数据集。

- 1. 打开程序文件 DAPPEND1.SAS。

```
DATA MYDATA;
DATA OLD1;
INPUT SUBJ $ AGE YRS_SMOKE;
DATALINES;
001 34 12
003 44 14
004 55 35
006 21 3
;
DATA OLD2;
INPUT SUBJ $ AGE YRS_SMOKE;
DATALINES;
011 33 11
012 25 19
023 65 45
032 71 55
;
RUN;
```

此程序创建了两个数据集，一个名为 OLD1，另一个名为 OLD2。它没有产生任何输出。运行程序并通过查看日志（Log）窗口的内容来验证数据集已创建。观察日志窗口中的以下语句：

> NOTE: The data set WORK.OLD1 has 4 observations and 3 variables.
> NOTE: The data set WORK.OLD2 has 4 observations and 3 variables.

- 2. 返回编辑器窗口，在该 SAS 程序末尾添加以下语句：

```
DATA NEW; SET OLD1 OLD2; RUN
PROC PRINT DATA=NEW;
```

- 3. 运行 SAS 程序并观察结果。OLD2 数据集追加到 OLD1 数据集，合并后的数据集存储在 NEW 中。结果在 NEW 中。

（继续）

- 4. 打开程序文件 DAPPEND2.SAS。注意在此程序中，数据集是 NEW。

（继续）

- 5. 运行 SAS 程序并观察结果。OLD2 数据集追加到 OLD1 数据集，合并后的数据集存储在 NEW 中。结果在 NEW 中。

# 4.7.2 通过键标识符合并数据集

合并数据集的另一种方法是通过键标识符进行合并（有时被称为水平合并）。例如，假设你在两个场合收集了数据，并合并这些数据集。

- 1. 打开程序文件 DMERGE1.SAS。此示例创建的第一个数据集是 PRE。

```
DATA PRE;
INPUT CASE $PREREAT;
DATALINES;
001 1.02
002 2.10
etc...
```
程序中的第二个数据集是 POST：
DATA POST;
INPUT CASE $POSTREAT;
DATALINES;
001 1.94
002 1.63
etc...
```

- 2. 注意每个数据集都包含一个变量 CASE。这是告诉 SAS 在合并时匹配哪些记录的键标识符。在合并数据集之前，必须对相同的标识符进行排序：

```
PROC SORT DATA=PRE; BY CASE;
PROC SORT DATA=POST; BY CASE;
```

在 SAS 中打开的代码是不完整的。你需要完成代码以使其运行。例如，在第二个 PROC SORT 中添加 BY CASE; 语句。此外，完成程序中的 DATA 语句以执行所需的合并：

```
DATA PREPOST;
* 创建新数据集;
MERGE PRE POST; BY CASE;
DIFF=POSTREAT - PREREAT; * 在新数据集中计算 DIFF;
```

- 3. 运行完成后的程序并观察表 4.12 中的结果。

- 4. 修改 MERGE 语句，将变量 PREREAT 重命名为 BASE-LINE。

```
MERGE PRE (RENAME=(PREREAT = BASELINE)) POST;
```

