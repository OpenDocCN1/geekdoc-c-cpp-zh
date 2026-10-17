
- 括号中的 `DROP=` 或 `KEEP=` 选项位于包含要删除或保留变量的数据集名称之后。
- `variable` 标识要删除或保留的变量。

## 示例：DROP 数据集选项

假设你想使用 `TimeMin` 和 `TimeSec` 变量来计算 `TotalTime` 变量中的总和，但你不想在输出数据集中保留它们。只想保留 `TotalTime` 变量。当你使用 `DROP` 数据集选项时，`TimeMin` 和 `TimeSec` 变量不会被写入输出数据集：

```sas
data work.stressstest(drop=timin timesec);
set cert.tests;
if resthr<70 then delete;
TotalTime=(timin*60)+timesec;
retain SumSec 5400;
sumsec+=totalime;
length TestLength $6;
if totalime>800 then TestLength='Long';
else if 750<=totalime<=800 then TestLength='Normal';
else if totalime<750 then TestLength='Short';
proc print data=work.stressstest;
run;
```

157 数据子集

## 输出 9.6 带有已删除变量的数据集（部分输出）

| ID | Name | RestHR | MaxHR | RecHR | Tolerance | TotalTime | SumSec | TestLength |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 2458 | Murray, W. | 72 | 185 | 128 | D | 758 | 6158 | Normal |
| 2501 | Bonaventure, T. | 77 | 187 | 139 | I | 673 | 6831 | Short |
| 2539 | LaMance, C. | 75 | 168 | 141 | D | 706 | 7537 | Short |
| 2544 | Jones, M. | 79 | 187 | 136 | N | 746 | 8283 | Short |
| 2555 | King, E. | 70 | 167 | 122 | I | 793 | 9076 | Normal |
| 2579 | Underwood, K. | 72 | 165 | 127 | S | 799 | 14639 | Normal |
| 2584 | Takahashi, Y. | 76 | 163 | 135 | D | 967 | 15606 | Long |
| 2588 | Ivan, H. | 70 | 182 | 126 | N | 941 | 16547 | Long |
| 2589 | Wilcox, E. | 78 | 189 | 138 | I | 897 | 17444 | Long |
| 2595 | Warren, C. | 77 | 170 | 136 | S | 730 | 18174 | Short |

另一种从数据集中排除变量的方法是使用 `DROP` 或 `KEEP` 语句。然而，`DROP=` 和 `KEEP=` 选项与 `DROP` 和 `KEEP` 语句不同，用于删除或保留变量。

- 你可以在 SAS 过程中使用 `DROP` 和 `KEEP` 语句。
- `DROP` 和 `KEEP` 语句适用于 `DATA` 语句指定的输出数据集。要从某些数据集排除变量，请在 `DATA` 语句中使用 `DROP=` 和 `KEEP=` 选项。

`KEEP` 语句类似于 `DROP` 语句，但它指定了要写入输出数据集的变量列表。如果保留的变量数少于删除的变量，请使用 `KEEP` 语句。

语法，`DROP` 和 `KEEP` 语句：

```sas
DROP variable(s);
KEEP variable(s);
```

`variable(s)` 标识要删除或保留的变量。

## 示例：使用 DROP 语句

下面的示例使用 `DROP` 语句删除不需要的变量。

```sas
data work.stressstest;
set cert.tests;
if tolerance='D'
drop timemin timesec;
TotalTime=(timemin*60)+timesec;
retain SumSec 5400;
sumsec+=totalime;
length TestLength $6;
if totalime>800 then TestLength='Long';
else if 750<totalime<800 then TestLength='Normal';
else if totalime>750 then TestLength='Short';
proc print data=work.stest;
run;
```

158 第 9 章 • 创建和管理变量

# 将变量转换为观测值

## TRANSPOSE 过程

### PROC TRANSPOSE 的基础

`TRANSPOSE` 过程通过重构数据中的观测值来创建一个输出数据集。通过使用 `PROC TRANSPOSE`，你可以避免编写复杂的 `DATA` 步骤来实现相同的结果。输出数据集可以在后续的 `DATA` 或 `PROC` 过程中用于分析、报告或进一步的数据处理。`PROC TRANSPOSE` 不产生输出。要打印 `PROC TRANSPOSE` 步骤的输出数据集，请使用 `PROC PRINT`。

### PROC TRANSPOSE 语法

要创建一个转换变量，过程将输入数据集中的观测值转换为输出数据集中的变量。

```sas
PROC TRANSPOSE<DATA=input-data-set><OUT=output-data-set><PREFIX=prefix>;
BY <DESCENDING>; variable-l <NOTSORTED>;
ID variable(s);
VAR variable(s);
```

- `input-data` 指定数据集。如果 `output-data` 不存在，`PROC TRANSPOSE` 将按照 `DATA` 命名规则创建。默认是 `DATA`。
- `prefix` 是用于构建输出集中转换变量名称的前缀。例如，如果 `PREFIX=VAR`，名称为 `VAR1`, `VAR2`...。默认是 `COL`。

> 注意：当你在 `ID` 语句中使用 时，变量名将以前缀开头。

提示：当 `VALIDNAME=ANY` 时，可以使用名称字面量（n-literals）作为前缀。

170 将变量转换为观测值

### PROC TRANSPOSE

### 输出数据集变量

`TRANSPOSE` 过程无论你是否指定 `OUT=` 选项都会产生一个输出数据集。

输出数据集包含以下变量：

- 由转换每个观测值产生的变量。
- 其值标识每个观测值来源的变量。这是一个字符变量，其值为从数据集中转换的变量名。默认情况下，`PROC TRANSPOSE` 将此变量命名为 `NAME`。要覆盖默认名称，请使用 `NAME=` 选项。`_NAME_` 变量的标签为 `NAME OF FORMER VARIABLE`。
- 其值为转换变量标签的字符（如果转换的变量中有任何标签）。使用 `LABEL=` 选项指定变量名称。默认是 `_LABEL`。
- 当你使用 `BY` 或 `COPY` 语句时，`TRANSPOSE` 从输入集中复制变量。这些变量与输入集中中的名称和值相同。这些变量具有相同的属性（例如：类型、长度、标签、信息和格式）。

> 注意：如果 `LABEL=` 选项或 `NAME=` 选项与 `BY` 或 `COPY` 语句中的变量相同，则输出数据集将不包含转换变量名称或标签的变量。

### 转换变量的属性

转换变量包含以下属性：

- 所有转换变量具有相同的类型和长度。
- 如果过程转换的所有变量都是数值型，则转换变量是数值型。因此，如果数值变量具有字符字符串的格式化值，则转换其未格式化的变量。
- 如果过程转换的任何变量是字符型，则所有转换变量都是字符型。如果你正在转换一个具有字符字符串格式化值的数值型变量，则转换的是格式化值。
- 转换变量的长度等于正在转换的最长变量的长度。

### 示例：执行简单的转换

以下是转换之前的 `Cert.Class` 数据集。

## 第 9 章 • 创建与管理变量

图 9.4 Cert.Class 数据集

| Obs | Name | Score1 | Score2 | Score3 | Homework |
| --- | --- | --- | --- | --- | --- |
| 1 | LINDA | 53 | 60 | 66 | 42 |
| 2 | DEREK | 72 | 64 | 56 | 32 |
| 3 | KATHY | 98 | 82 | 100 | 48 |
| 4 | MICHAEL | 80 | 55 | 95 | 50 |

此示例执行了默认转置且没有使用任何子过程。

```sas
proc transpose data=cert.class out=score_transposed; /* #1 **/
run;
proc print data=score_transposed noobs;
ntitle 'Scores for the Year'; /* #2 **/
run;
```

- 1. `PROC TRANSPOSE` 仅复制了数值变量 `Score1`、`Score2`、`Score3` 和 `Homework`。`OUT=` 将转置结果存入数据集中。`NOOBS` 选项抑制了观测值的打印。
- 2. `PROC PRINT` 打印了 `Score_Transposed` 数据集。

在输出数据集 `Score_Transposed` 中，变量 `COL1` 到 `COL4` 包含了每个学生当年的 `Score1`、`Score2`、`Score3` 和 `Homework` 的值。变量 `_NAME_` 包含了从输入数据集中被转置的变量名称。

输出 9.7 变量中的学生测试分数

## 年度分数

| _NAME_ | COL1 | COL2 | COL3 | COL4 |
| --- | --- | --- | --- | --- |
| Score1 | 53 | 72 | 98 | 80 |
| Score2 | 60 | 64 | 82 | 55 |
| Score3 | 66 | 56 | 100 | 95 |
| Homework | 42 | 32 | 48 | 50 |

## 转置特定变量

使用 `VAR` 语句来列出要转置的变量。如果省略 `VAR` 语句，则 `TRANSPOSE` 过程将复制数据集中所有未在其他语句中列出的数值变量。如果你想转置字符变量，必须在 `VAR` 语句中列出它们。

注意：如果过程正在转置任何字符变量，则所有转置变量都是字符变量。

## 将变量转置为观测值

语法：`VAR` 语句：

```sas
VAR variable(s);
```

- `variable(s)` 指定一个或多个要转置的变量。

以下是 `Cert.Trials` 数据集：

图 9.5 Cert.Trials 数据集

| Obs | Name | TestDate | Sex | Cholesterol | Trigly | Uric |
|---|---|---|---|---|---|---|
| 1 | Johnson | 22MAY2000 | YES | 200 | 180 | 3.7 |
| 2 | Eberhardt | 22MAY2000 | NO | 244 | 320 | 4.6 |
| 3 | Nunnelly | 22MAY2000 | YES | 210 | 300 | 4.0 |
| 4 | Johnson | 01AUG2000 | YES | 205 | 185 | 3.8 |
| 5 | Eberhardt | 01AUG2000 | NO | 249 | 325 | 4.7 |
| 6 | Nunnelly | 01AUG2000 | YES | 215 | 305 | 4.1 |
| 7 | Johnson | 09AUG2000 | YES | 215 | 190 | 3.9 |
| 8 | Eberhardt | 09AUG2000 | NO | 254 | 330 | 4.8 |
| 9 | Nunnelly | 09AUG2000 | YES | 220 | 310 | 4.2 |

```sas
/* proc data=cert.trials out=translials1;
var Cholesterol Trigly Uric;
run;

proc print data=translials1;
run;
*/
```

- 1. 运行 `Cert.Trials` 数据集并将转置结果放入 `Translials1` 数据集中。
- 2. `VAR` 语句指定 `Cholesterol`、`Trigly` 和 `Uric` 变量为要转置的变量。
- 3. 使用 `PROC PRINT` 语句打印 `Translials1` 数据集。

在后续输出中，`Translials1` 数据中的变量 `Cholesterol`、`Trigly` 和 `Uric` 是唯一被转置的变量。该过程使用默认变量名 `COLN`。

输出 9.8 `PROC PRINT` 结果：`Translials1` 数据集

| Obs | NAME_ | COL1 | COL2 | COL3 | COL4 | COL5 | COL6 | COL7 | COL8 | COL9 |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Cholesterol | 200.0 | 244.0 | 210.0 | 249.0 | 215.0 | 215.0 | 254.0 | 220.0 | |
| 2 | Trigly | 180.0 | 320.0 | 300.0 | 325.0 | 305.0 | 190.0 | 330.0 | 310.0 | |
| 3 | Uric | 3.7 | 4.6 | 4.0 | 3.8 | 4.7 | 4.1 | 3.9 | 4.8 | 4.2 |

## 命名转置变量

使用 `ID` 语句根据输入数据集中的一个或多个变量在输出集中创建名称。

在形成名称时，所有列出的 `ID` 变量的格式值按照它们在 `ID` 语句中的顺序进行拼接。`PREFIX=` 选项指定位于变量开头的公共字符或字符串。

语法，`ID` 语句：

```sas
ID variable(s);
```

- `variable(s)` 一个或多个格式值用于形成输出数据集中的变量名。

> 如果任何 `ID` 变量的值缺失，`PROC TRANSPOSE` 会向日志写入警告信息。该过程不会转置具有 `ID` 变量缺失值的观测值。以下示例使用了用户提供的值进行命名。

```sas
proc transpose data=cert.trials out=tranials2; /* #1 */
var cholesterol trigly uric /* #2 */
id name testdate; /* #3 */
run;
proc print data=tranials2; /* #4 */
```

- 1. 转置 `Cert.Trials` 并转置结果放入 `Tranials2` 数据集中。
- 2. `VAR` 语句指定 `Cholesterol`、`Trigly` 和 `Uric` 为唯一的要转置变量。
- 3. `ID` 语句指定 `Name` 和 `TestDate` 为输出数据集 `Tranials2` 的变量。由于 `ID` 语句指定了两个变量，这些变量的值被拼接创建新名称。
- 4. 使用 `PROC PRINT` 打印 `Tranials2` 数据。

## 将变量转置为观测值

输出 9.9 `PROC PRINT` 结果：`Tranials2` 数据集

| Obs | _NAME_ | Johnson22MAY2000 | Eberhart22MAY2000 | Nunelly22MAY2000 | Johnson01AUG2000 |
|---|---|---|---|---|---|
| 1 | Cholesterol | 200.0 | 244.0 | 210.0 | 205.0 |
| 2 | Trigly | 180.0 | 320.0 | 300.0 | 185.0 |
| 3 | Uric | 3.7 | 4.6 | 4 | 3.8 |
| Eberhart01AUG2000 | Nunelly01AUG2000 | Johnson09AUG2000 | Eberhart09AUG2000 | Nunelly09AUG2000 |
|---|---|---|---|---|---|
| 4 | 249.0 | 215.0 | 254.0 | 220.0 |
| 5 | 325.0 | 305.0 | 190.0 | 330.0 | 310.0 |
| 6 | 4.7 | 4.1 | 3.9 | 4.8 | 4.2 |

## 转置 BY组

在 `PROC TRANSPOSE` 步骤中使用 `BY` 语句定义并转置 BY组。

语法，`BY` 语句：

```sas
BY <DESCENDING> variable-<NOTSORTED>;
```

- `variable` 指定 `PROC TRANSPOSE` 用于形成 BY组的变量。你可以指定多个变量。如果不使用 `NOTSORTED` 选项，观测值将按你指定的所有变量进行排序。`DESCENDING` 指定数据集按 `BY` 语句中紧跟 `DESCENDING` 的变量降序排序。`NOTSORTED` 指定观测值不一定按字母或数字顺序排序。使用 `NOTSORTED` 选项时，暂停 BY 处理。过程将 BY组定义为变量值相同的连续观测值集合。如果 变量值相同的观测值不连续，过程会将每个连续集合视为一个独立的 BY组。

```sas
proc transpose data=cert.trials out=transtrials; /* 1 */
var cholesterol trigly uric;
id name;
by testate;
run;
proc print data=transtri3; /* 2 */
/* 3 */
/* 4 */
/* 5 */
```

- 1 转数据集。`OUT=` 选项将转置结果放入 `Transtri3` 数据集中。
