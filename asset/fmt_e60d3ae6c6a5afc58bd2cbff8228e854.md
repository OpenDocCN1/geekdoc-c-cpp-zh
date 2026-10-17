
| 10 | Female | O | Young | 7710 | 5.55 | |

## 18.2 简单的 PROC TABULATE 表格

尽管 `PROC TABULATE` 可以创建复杂的表格，但只有三个操作符可以控制表格的外观。让我们从使用所有默认值运行 `PROC TABULATE` 并选择单个 `CLASS` 变量开始，如下：

程序 18.1：带有所有默认值单个 CLASS 变量的 PROC TABULATE

```
title "All Defaults with One CLASS Variable";
proc tabulate data=Learn.Blood;
class Gender;
table Gender;
run;
```

`PROC TABULATE` 使用 `CLASS` 语句，在其中您指定代表类别（通常是字符变量）的变量来计算频率或百分比。在程序 18.1 中，`Gender` 被选为 `CLASS` 变量。`TABLE` 语句指定表格的外观。`TABLE` 语句中列出的任何变量必须列在 `CLASS` 语句或 `VAR` 语句中（稍后将讨论）。以下是输出：

图 18.2：程序 18.1 的输出

### 带有单个 CLASS 变量的所有默认值

| Female | Male |

|---|---|

| N | N |

| 440 | 560 |

在 `TABLE` 语句中列出一个 `CLASS` 变量时，`PROC TABULATE` 计算选中变量每个值的频率。它还将这些频率作为列显示。您可以在这里看到数据集中有 440 个女性和560 个男性。

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

`TABLE` 语句中 `Gender` 和 `BloodType` 之间的空格代表合并。如果您指定逗号，过程将显示每个单元格的频率。这里是表格：

图 18.3：程序 18.2 的输出

| Gender | BloodType |

|---|---|

| Female | A B O |

| Male | N N N |

| 440 560 | | |

### 18.3.2 表格维度（页、行和列）

`TABLE` 语句控制表格的维度。如果没有逗号，所有变量将作为列显示。如果包含单个逗号，逗号之前的生成行，逗号之后的生成列。为了演示：

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

第三个操作符使用星号（`*`）。如果您指定变量 1 * 2，变量 2 将嵌套在变量 1 中。为了演示，这里是将 `BloodType` 嵌套在 `Gender` 中的请求：

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

与其他许多 SAS 过程不同，`PROC TABULATE` 使用了一些保留关键字（这意味着您必须小心不要将任何变量命名为与 `PROC TABULATE` 关键字相同）。其中一个关键字是 `ALL`。当您在表格请求中变量之后放置 `ALL` 时，`PROC TABULATE` 会包含一个代表该变量所有层级的列。为了演示，您可以在程序 18.3 生成的表格的两个维度都添加 `ALL`，如下：

程序 18.5：在表格请求中添加关键字 ALL

```
title "Adding the Keyword ALL to the TABLE Request";
proc tabulate data=Learn.Blood format=6;
class Gender BloodType;
table Gender ALL,
    BloodType ALL;
run;
```

304 实例化的 SAS 学习：程序员指南，第二版

以下是生成的表格：

图 18.6：程序 18.5 的输出

在 TABLE 请求中添加关键字 ALL

| 血型 | All | |

|---|---|

| | A AB B O |

| | N N N N |

| 性别 | | |

| 女性 | 178 20 34 208 440 |

| 男性 | 234 24 62 240 560 |

| 全部 | 412 44 96 448 1000 |

由于 `ALL` 与前一个变量之间存在空格，与 `ALL` 相关的频率将与相应的变量合并。

## 18.5 生成描述性统计数据

`PROC TABULATE` 也可以生成总和和平均值等描述性统计。要指定你想生成描述性统计而不是频率计数，你需要在 `VAR` 语句中列出所有的分析变量（即你想要进行统计分析的变量）。

> 注意：描述性统计可能出现在表格的任何维度，但你只能在表格的单个维度上定义统计。

程序 18.6 计算了 `RBC`（红细胞）和 `WBC`（白细胞）计数的描述性统计数据：

程序 18.6：使用 PROC TABULATE 生成描述性统计数据

```sas
title "Demonstrating Analysis Variables";
proc tabulate data=Learn.Blood;
var RBC WBC;
table RBC WBC;
run;
```

生成的输出如下：

### 图 18.7：程序 18.6 的输出

| RBC | WBC |

| Sum | Sum |

| 5022.91 | 6395020.00 |

`RBC` 和 `WBC` 之间的操作符是空格，分析列被合并了。默认的描述性统计是总和（对于血计数来说，这不是一个非常有用的统计量）。要为每个变量指定一个或多个分析，你可以使用关键字（sum, mean, min, max, std 等）来指定你想要的统计数据，并使用嵌套运算符（星号 `*`）将这些统计数据与变量关联。例如，要为 `RBC` 和 `WBC` 指定平均值而不是总和，你可以使用程序 18.7 中的代码。

### 程序 18.7：使用 PROC TABULATE 在分析变量上指定统计数据

```sas
title "Specifying Statistics";
proc tabulate data=Learn.Blood;
var WBC;
table RBC*mean WBC=mean;
run;
```

为了节省输入时间，你也可以像这样写 `TABLE` 语句：

```sas
table (RBC WBC)*mean;
```

无论哪种方式，你现在都有了一个显示平均（平均）血计数的表格：

### 图 18.8：程序 18.7 的输出

| RBC | WBC |

| Mean | Mean |

| 5.48 | 7042.97 |

输出现在显示的是而不是默认的总和统计。你也可以为每个变量指定多个统计数据。例如，如果你想获得血计数的平均值、最小值和最大值，你可以编写程序 18.8：

### 程序 18.8：使用 PROC TABULATE 指定多一个描述性统计数据

```sas
title "Specifying More than One Statistic";
proc tabulate data=Learn.Blood format=comma9.2;
var RBC WBC;
table (RBC WBC) * (mean min max);
run;
```

现在每个两个变量都列出了每个统计数据，如下所示：

### 图 18.9：程序 18.8 的输出

指定多一个统计数据

| RBC | | WBC |

| Mean Min Max | Min Max |

| 5.48 1.71 8.75 | 4.07.00 10.5500 |

此程序使用 `PROC TABULATE` 选项 `FORMAT=COMMA9.2` 来提高输出的可读性。现在你有了 `RBC` 和 `WBC` 计数的平均值、最小值和最大值，每个值都以 9.2 数值格式显示。

## 18.6 在表格中结合 CLASS 变量和分析变量

如果你想按一个或多个 `CLASS` 变量（如性别或血型）查看 `RBC` 和 `WBC` 的平均值怎么办？你可以将频率和描述性统计合并在单个表格中。这就是一些人抱怨 `PROC TABULATE` 很难使用的原因所在。实际上，问题更有可能是用户在开始编写 `TABULATE` 语句之前没有决定表格应该什么样。安排表格以使列不跨页划分（这使得阅读非常困难）也需要一些练习。

下一个程序是请求按性别（`Gender`）和年龄组（`AgeGroup`）细分的平均 `RBC`、`WBC` 和 `Chol`（胆固醇）。

### 程序 18.9：在表格中结合 CLASS 变量和分析变量

```sas
title "Combining CLASS and Analysis Variables";
proc tabulate data=Learn.Blood;
class Gender AgeGroup;
var RBC WBC Chol;
table (RBC WBC Chol)*mean by=Gender*AgeGroup;
run;
```

此程序按 `Gender` 和 `AgeGroup` 细分 `RBC`、`WBC` 和 `Chol` 的平均值。`RBC` 和 `WBC` 的平均值显示在表格中：

### 图 18.10：程序 18.9 的输出

结合 CLASS 和分析变量

| | | WBC | Chol |

|---|---|---|---|

| Gender | Mean | Mean | Mean |

| Female | 5.48 | 7042.97 | 195 |

| | Male | 5.53 | 7112 | 202 |

| AgeGroup | | | | |

| 20-29 | 5.46 | 7039.54 | 198 |

| 30-39 | 5.47 | 7061.66 | 201 |

| 40-49 | 5.52 | 7088.09 | 207 |

| 50+ | 5.50 | 7047.55 | 203 |

# 310 实例实例学习 SAS：程序员指南，第二版

选择这些选项是为了使列标题或标签不会在行之间拆分，而不是为了显示特定值而选择最优值。以下是该程序生成的紧凑表格：

图 18.14：程序 18.13 的输出

| | | RBC N 平均 | WBC N 平均 | 胆固 N 平均 |

|---|---|---|---|---|---|---|

| 女性 | 老年 | 242 | 5.5 | 7,106 | 208 | 195.9 |

| | | 年轻 | 167 | 5.5 | 7,121 | 141 | 212.3 |

| | | 总计 | 409 | 5.5 | 7,112 | 349 | 202.5 |

| 男性 | 老年 | 309 | 5.4 | 6,939 | 279 | 199.1 |

| | | 年轻 | 198 | 5.5 | 7,062 | 167 | 203.1 |

| | | 总计 | 507 | 5.5 | 6,988 | 446 | 200.6 |

| 总计 | 老年 | 551 | 5.5 | 7,012 | 487 | 197.7 |

| | | 年轻 | 365 | 5.5 | 7,089 | 308 | 207.3 |

| | | 总计 | 916 | 5.5 | 7,043 | 795 | 201.4 |

## 18.9 计算行列百分比

统计量 `PCTN` 与 `CLASS` 变量配合用于计算百分比。程序 18.14 展示了如何使用该统计量。该程序在一维表格中计算四种血型各的数量和百分比。

程序 18.14：在一维表格中计算百分比

```
title "Counts and Percentages";
proc tabulate data=Learn.Blood format=6;
class BloodType;
table BloodType*(n pctn);
run;
```

输出结果虽然不太漂亮，但格式如下：

### 图 18.15：程序 18.14 的输出

# 计数与百分比

| 血型 | | | | | | |

|---|---|---|---|---|---|

| A | AB | O | | | |

| N | Pctn | N | Pctn | N | Pctn |

| 412 | 41 | 4 | 96 | 10 | 448 | 45 |

Pct 数字的总和为 100%。

是时候改进这个表格的外观了。让我们添加一个 `ALL` 列，重命名 `N` 和 `Pctn`，并在百分比数字后加上百分号。如下：

程序 18.15：改进程序 18.14 输出的外观

```
proc format;
  picture pctfmt low-high='009.9%%';
run;

title "Counts and Percentages";
proc tabulate data=Learn.Blood;
class BloodType;
table(BloodType ALL)*(n*f=5. pctn*f=pctfmt7.1);
  keylabel n = 'Count'
  pctn = 'Percent';
run;
```

此程序中进行了几项改进。通过 `PROC FORMAT` 创建了用户定义的图片格式。这允许在小数点前显示最多三位数字，并打印最右侧的数字（即使它为 0）。格式中的 0 是占位符；9 也是占位符，但会在必要时打印前导 0。图片格式中的百分号按原样打印。您可以在 SAS 帮助中心 http://go.documentation.sas.com 了解更多关于图片格式的信息。

为 `N` (5) 和 `Pctn` (Pctfmt.1) 分别创建了单独格式。最后，使用 `KEYLABEL` 语句将 `N` 和 `Pct` 分别重命名为 Count 和 Percent。顺便提一下，百分比值的 7 位格式宽度是由百分比列标题选定的。以下是表格：

### 图 18.16：程序 18.15 的输出

# 计数与百分比

| 血型 | | | | | | | | |

|---|---|---|---|---|---|---|---|---|

| A | AB | B | O | | | | |

| Count Percent Count Percent Count Percent Count Percent |

| 412 | 41.2% | 44 | 4.4% | 96 | 9.6% | 448 | 44.8% | 1000 | 100.0% |

312 实例实例学习 SAS：程序员指南，第二版

## 18.10 在二维表格中显示百分比

这里情况变得复杂了。让我们创建一个按性别（行）和血型（列）分类的表格并请求 `N` 和 `PCTN`，如下所示：

程序 18.16：二维表格中的计数与百分比

```
proc format;
    picture pctfmt low-high='009.9%%';
run;

title "Counts and Percentages in a Two-way Table";
proc tabulate data=Learn.Blood;
class Gender BloodType;
table (BloodType ALL)*
      (Gender ALL*n=f5. pctn*f=pctfmt7.1)/rows=25;
keylabel ALL='Both Genders'
      n = 'Count'
      pctn = 'Percent';
run;
```

`TABLE` 选项 `RTS=25` 增加了行标题空间（行标题所在的空间）。在表格中，从最左侧线到“Female”之前的线有 25 个空格。以下是输出：

程序 18.17：程序 18.16 的输出

# 二维表格中的计数与百分比

![](img/e9e15d85398955188e1c30ae5550_321.png)

此表中的百分比值代表单元格中受试者（例如，A 型血女性）占所有受试者的百分比。因此，A 型血的女性人数（178）代表了 17.8%。这意味着拥有 A 型血的女性人数（178）代表了总人数（1000）的 17.8%。假设让百分比代表每个性别内的血型分布。

18.11 列百分比

如果你想表格包含列百分比，需要修改 18.16。为了实现这一点，另一种方法是提供分母。Haworth 的书中在介绍中讨论了分母定义。另一种方法是使用 `COLPN`。具体来说，18.17 使用 `COLPN` 来计算列百分比。

18.17：使用 COLPN 计算列百分比
