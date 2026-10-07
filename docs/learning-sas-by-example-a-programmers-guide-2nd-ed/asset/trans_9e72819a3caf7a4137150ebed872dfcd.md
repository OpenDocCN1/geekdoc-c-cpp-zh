

## 第 18 章：创建表格报告

- 18.1 引言 ................................................................................ 299
- 18.2 简单的 PROC TABULATE 表格 ............................................................ 300
- 18.3 描述三个 PROC TABULATE 操作符 ................................................ 301
- 18.3.1 合并......................................................................................... 301
- 18.3.2 表格维度（页、行和列）............................................................... 302
- 18.3.3 嵌套...................................................................................................... 302
- 18.4 使用关键字 ALL ...................................................................... 303
- 18.5 产生描述性统计 ........................................................ 304
- 18.6 在表格中结合 CLASS 和分析变量 ................................................ 306
- 18.7 定制您的表格 ....................................................................... 307
- 18.8 演示更复杂的表格....................................................... 309
- 18.9 计算行和列百分比 ................................................... 310
- 18.10 在二维表格中显示百分比 ........................ 312
- 18.11 计算列百分比 ................................................... 313
- 18.12 计算数值变量的百分比......................................... 314
- 18.13 理解缺失值如何影响 PROC TABULATE 输出 ...... 315
- 18.14  ...................................................................... 318

## 18.1 引言

PROC TABULATE 是一个被低估、低利用的过程，它可以创建各种类型的表格报告，根据一个或多个 CLASS 变量显示频率、百分比和描述性统计（如总和和平均值）。有几本关于 PROC TABULATE 的优秀书籍。我推荐 E. Haworth 的书籍 *PROC TABULATE By Example* (Cary, NC: SAS Institute Inc., 1999)，这是关于该主题最好、最全面的书籍之一。

本章将向您介绍这个过程，并希望它能激发您的兴趣。

为了演示 PROC TABULATE 的许多功能，我们将使用一个名为 Blood 的数据集，该数据集包含类型、性别、年龄组、红/白细胞计数以及胆固醇水平的信息。以下是该数据集的前 10 条观测值的列表：

图 18.1：数据集 Learn.Blood 的列表（前 10 条观测值）

| Subject | Gender | BloodType | AgeGroup | WBC | RBC | Chol |
|---|---|---|---|---|---|---|
| 1 | Female | AB | Young | 7710 | 7.40 | 258 |
| 2 | Male | AB | Old | 6560 | 4.70 | |
| 3 | Male | A | Young | 5690 | 7.53 | 184 |
| 4 | Male | B | Old | 6680 | 6.85 | |
| 5 | Male | A | Young | | 7.72 | 187 |
| 6 | Male | A | Old | 6140 | 3.69 | 142 |
| 7 | Female | A | Young | 6550 | 4.78 | 290 |
| 8 | Male | O | Old | 5200 | 4.96 | 151 |
| 9 | Male | O | Young | | 5.66 | 311 |
| 10 | Female | O | Young | 7710 | 5.55 | |

## 18.2 简单的 PROC TABULATE 表格

尽管 PROC TABULATE 可以创建复杂的表格，但只有三个操作符可以控制表格的外观。让我们从使用所有默认值运行 PROC TABULATE 并选择单个 CLASS 变量开始，如下：

程序 18.1：带有所有默认值单个 CLASS 变量的 PROC TABULATE

```
title "All Defaults with One CLASS Variable";
proc tabulate data=Learn.Blood;
class Gender;
table Gender;
run;
```

PROC TABULATE 使用 CLASS 语句，在其中您指定代表类别（通常是字符变量）的变量来计算频率或百分比。在程序 18.1 中，Gender 被选为 CLASS 变量。TABLE 语句指定表格的外观。TABLE 语句中列出的任何变量必须列在 CLASS 语句或 VAR 语句中（稍后将讨论）。以下是输出：

图 18.2：程序 18.1 的输出

### 带有单个 CLASS 变量的所有默认值

| Female | Male |
|---|---|
| N | N |
| 440 | 560 |

在 TABLE 语句中列出一个 CLASS 变量时，PROC TABULATE 计算选中变量每个值的频率。它还将这些频率作为列显示。您可以在这里看到数据集中有 440 个女性和560 个男性。

## 18.3 描述三个 PROC TABULATE 操作符

### 18.3.1 合并

我们使用的第一个操作符是合并（Concatenation）。如果您想在表格中将变量并排，请在变量之间使用空格。为了演示，我们提交以下内容：

程序 18.2：使用 PROC TABULATE 演示合并

```
title "Demonstrating Concatenation";
proc tabulate data=Learn.Blood format=6;
class Gender BloodType;
table Gender BloodType;
run;
```

TABLE 语句中 Gender 和 BloodType 之间的空格代表合并。如果您指定逗号，过程将显示每个单元格的频率。这里是表格：

图 18.3：程序 18.2 的输出

| Gender | BloodType |
|---|---|
| Female | A B O |
| Male | N N N |
| 440 560 | | |

### 18.3.2 表格维度（页、行和列）

TABLE 语句控制表格的维度。如果没有逗号，所有变量将作为列显示。如果包含单个逗号，逗号之前的生成行，逗号之后的生成列。为了演示：

程序 18.3：使用 PROC TABULATE 演示维度

```
title "Demonstrating Dimensions";
proc tabulate data=Learn.Blood format=6;
class Gender BloodType;
table Gender,
    BloodType;
run;
```

生成的表格如下：

图 18.4：程序 18.3 的输出

| | BloodType |
|---|---|---|
| Female | A B O |
| Male | A B O |
| 440 560 | | |

### 18.3.3 嵌套

第三个操作符使用星号 (*)。如果您指定变量 1 *  2，变量 2 将嵌套在变量 1 中。为了演示，这里是将 BloodType 嵌套在 Gender 中的请求：

程序 18.4：使用 PROC TABULATE 演示嵌套

```
title "Demonstrating Nesting";
proc tabulate data=Learn.Blood format=6;
class Gender BloodType;
table Gender * BloodType;
run;
```

这里是生成的表格：

图 18.5：程序 18.4 的输出

| Gender | BloodType | |
|---|---|---|
| Female | A B O | |
| Male | A B O | |
| 178 20 34 208 | 234 24 62 240 | |

## 18.4 使用关键字 ALL

与其他许多 SAS 过程不同，PROC TABULATE 使用了一些保留关键字（这意味着您必须小心不要将任何变量命名为与 PROC TABULATE 关键字相同）。其中一个关键字是 ALL。当您在表格请求中变量之后放置 ALL 时，PROC TABULATE 会包含一个代表该变量所有层级的列。为了演示，您可以在程序 18.3 生成的表格的两个维度都添加 ALL，如下：

程序 18.5：在表格请求中添加关键字 ALL

```
title "Adding the Keyword ALL to the TABLE Request";
proc tabulate data=Learn.Blood format=6;
class Gender BloodType;
table Gender ALL,
    BloodType ALL;
run;
```

