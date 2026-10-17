
```
%let DATA_DIR=C:\Users\baileraj\BAILERAJ\Classes\Web-Classes\STA402\FALL-2007\data;

data nitrofen;
  infile "&DATA_DIR\ch2-dat.txt" firstobs=16 expandtabs missover pad;
  input @9 animal 2.    @17 conc 3.    @25 brood1 2.
        @33 brood2 2.  @41 brood3 2.  @49 total 2.;
run;

ods rtf BODYTITLE file="&DATA_DIR\Display-4.1.rtf";
proc tabulate data=nitrofen format=3.;  * include default format for;
  class conc;                         *   numeric summaries;
  var brood1 brood2 brood3 total;
  table (brood1 brood2 brood3 total)*conc,
        n min q1 median*f=4.1 q3 max;
run;
ods rtf close;
```

Display 4.2 中的表格为每个窝以及每个浓度条件下的总幼体数提供了五数概括。

¹ `Nitrofen` 数据集来自 Bailer, A. John., and James T. Oris. 1994. "Assessing Toxicity of Pollutants in Aquatic Systems." Chapter 2 in Case Studies in Biometry: Nicholas Lange, Louise Ryan, Lynne Billard, David Brillinger, Loveday Conquest, Joel Greenhouse, eds. New Jersey: John Wiley & Sons, Inc. 经 John Wiley & Sons, Inc. 许可重印。

#### Display 4.2 暴露于 nitrofen 的 C. dubia 所产幼体数的浓度特异性五数概括

|  |  | N | Min | Q1 | Median | Q3 | Max |
|---|---|---|---|---|---|---|---|
| brood1 | conc |  |  |  |  |  |  |
|  | 0 | 10 | 3 | 5 | 5.5 | 6 | 6 |
|  | 80 | 10 | 3 | 5 | 5.0 | 6 | 8 |
|  | 160 | 10 | 2 | 6 | 6.0 | 6 | 6 |
|  | 235 | 10 | 2 | 4 | 6.0 | 6 | 7 |
|  | 310 | 10 | 0 | 5 | 5.5 | 6 | 7 |
| brood2 | conc |  |  |  |  |  |  |
|  | 0 | 10 | 10 | 11 | 12.0 | 14 | 15 |
|  | 80 | 10 | 9 | 11 | 12.0 | 12 | 13 |
|  | 160 | 10 | 8 | 10 | 12.0 | 12 | 13 |
|  | 235 | 10 | 0 | 0 | 3.5 | 10 | 13 |
|  | 310 | 10 | 0 | 0 | 0.0 | 0 | 10 |
| brood3 | conc |  |  |  |  |  |  |
|  | 0 | 10 | 10 | 12 | 15.0 | 15 | 17 |
|  | 80 | 10 | 12 | 14 | 14.5 | 16 | 18 |
|  | 160 | 10 | 10 | 11 | 11.0 | 12 | 13 |
|  | 235 | 10 | 0 | 6 | 6.5 | 9 | 10 |
|  | 310 | 10 | 0 | 0 | 0.0 | 0 | 0 |
| total | conc |  |  |  |  |  |  |
|  | 0 | 10 | 24 | 30 | 32.5 | 34 | 36 |
|  | 80 | 10 | 26 | 29 | 32.5 | 33 | 36 |
|  | 160 | 10 | 23 | 27 | 29.0 | 30 | 31 |
|  | 235 | 10 | 7 | 13 | 16.5 | 21 | 27 |
|  | 310 | 10 | 0 | 5 | 6.0 | 6 | 15 |

此表在行维度上包含四个不同变量的汇总（`BROOD1`、`BROOD2`、`BROOD3` 和 `TOTAL`），每个变量的汇总都按另一个变量（`CONC`）的值进行分层。列包括样本量以及与窝和 `TOTAL` 变量相关的五数概括（最小值、第一四分位数、中位数、第三四分位数、最大值），这些概括均按 nitrofen 浓度分层。例如，第一行（`BROOD1` 和 `CONC=0`）中的条目对应于暴露于对照条件下的生物体在第一窝中产出的幼体数量的汇总统计量。这里，对照生物体在第一窝中产出的幼体数量的中位数为 5.5。让我们探讨生成此表的语句。

```
proc tabulate data=nitrofen format=3.;
  class conc;
  var brood1 brood2 brood3 total;
  table (brood1 brood2 brood3 total)*conc,
        n min q1 median*f=4.1 q3 max;
run;
```

`class conc` 语句将浓度变量标识为用于构建表格的分类变量。`var brood1 brood2 brood3 total` 语句将这四个变量标识为要进行汇总的数值变量。以下是 `table` 语句的一般形式：

```
table page dimension, row dimension, column dimension;
```

页面、行和列维度用逗号分隔。并非所有页面、行和列维度都是必需的。（在前面的代码示例中，只给出了行和列规格。）在生成此输出的 `TABLE` 语句中，行是四个数值变量与分类变量 `CONC` 之间的嵌套。列包括样本量和五个描述性统计量（最小值、第 25 百分位数、中位数、第 75 百分位数和最大值）。有一个用于格式化其中一个表条目的规格（`median*f=4.1`）。其他条目（例如 `n`、`min`、`q1`、`q3` 和 `max`）根据 `proc tabulate data=nitrofen format=3.` 语句中设置的默认格式进行格式化。

### 4.2 从简单规格构建

逐步构建一个复杂的最终表格是一次良好的学习体验。复杂的最终表格通常是由一系列简单的表格构建而成，最终达到最终表格。在逐步接近 Display 4.2 中的表格的过程中，我们将探讨这一系列简单表格。通常，你从要显示的变量的一般想法开始，但在开始处理之前，列的结构和格式尚未确定。

显示。简单的草图可以帮助你起草一个目标表格。假设你希望将变量列在行上，而将汇总统计量显示在列上。例如：

| Variable | Sample Size | Min | Q1 | Median | Q3 | Max |
|---|---|---|---|---|---|---|
| Brood 1 |  |  |  |  |  |  |
| Brood 2 |  |  |  |  |  |  |
| Brood 3 |  |  |  |  |  |  |
| Total |  |  |  |  |  |  |

要使用 `PROC TABULATE` 实现此目的，请在 `VAR` 语句中识别你希望使用描述性统计进行汇总的数值变量。在行维度中识别这些变量。在 `TABLE` 语句的列维度中识别描述性统计。显示 4.3 展示了编码命令的第一次尝试。

#### 显示 4.3 用于硝基酚数据分析的草表代码

```
%let DATA_DIR=C:\Users\baileraj.IT\BAILERAJ\Classes\Web-Classes\STA402\data;

data nitrophen;
  infile "&DATA_DIR\ch2-dat.txt" firstobs=16 expandtabs missover pad;
  input @9 animal 2.    @17 conc 3.    @25 brood1 2.
        @33 brood2 2.    @41 brood3 2.    @49 total 2.;
run;
ods rtf BODYTITLE file="&DATA_DIR\Display-4.3.rtf";
proc tabulate data=nitrophen;
  var brood1 brood2 brood3 total;
  table brood1 brood2 brood3 total, n min q1 median q3 max;
run;
ods rtf close;
```

不要担心在表格初稿中格式化表格条目或浓度特定的汇总。你希望在开始润色之前先有一个可用的草稿。此表格在显示 4.4 中展示。

#### 显示 4.4 硝基酚数据分析的草表——未格式化且在浓度上汇总

|  | N | Min | Q1 | Median | Q3 | Max |
|---|---|---|---|---|---|---|
| brood1 | 50 | 0.00 | 5.00 | 6.00 | 6.00 | 8.00 |
| brood2 | 50 | 0.00 | 0.00 | 11.00 | 12.00 | 15.00 |
| brood3 | 50 | 0.00 | 6.00 | 11.00 | 14.00 | 18.00 |
| total | 50 | 0.00 | 15.00 | 27.00 | 31.00 | 36.00 |

该草稿已捕捉到表格的本质。然而，所有浓度组在此显示中都被汇总在一起，且小数位数是不必要的。在下一轮代码中，按每个浓度组分层分析。使用 `CLASS` 语句识别浓度，然后通过将 `CONC` 指定为页规格或 `TABLE` 语句中的第一个参数，为每个浓度构造单独的表格：

```
proc tabulate data=nitrofen;
  class conc;
  var brood1 brood2 brood3 total;
  table conc, brood1 brood2 brood3 total, n min q1 median q3 max;
run;
```

此代码生成五个表格，每个浓度组一个，如显示 4.5 所示。

#### 显示 4.5 硝基酚数据分析的第二次尝试——未格式化的表格条目和按每个浓度汇总的单独页面

##### conc 0

|  | N | Min | Q1 | Median | Q3 | Max |
|---|---|---|---|---|---|---|
| brood1 | 10 | 3.00 | 5.00 | 5.50 | 6.00 | 6.00 |
| brood2 | 10 | 10.00 | 11.00 | 12.00 | 14.00 | 15.00 |
| brood3 | 10 | 10.00 | 12.00 | 15.00 | 15.00 | 17.00 |
| Total | 10 | 24.00 | 30.00 | 32.50 | 34.00 | 36.00 |

##### conc 80

|  | N | Min | Q1 | Median | Q3 | Max |
|---|---|---|---|---|---|---|
| brood1 | 10 | 3.00 | 5.00 | 5.00 | 6.00 | 8.00 |
| brood2 | 10 | 9.00 | 11.00 | 12.00 | 12.00 | 13.00 |
| brood3 | 10 | 12.00 | 14.00 | 14.50 | 16.00 | 18.00 |
| total | 10 | 26.00 | 29.00 | 32.50 | 33.00 | 36.00 |

注意：`CONC=160` 和 `CONC=235` 的表格已从显示中省略。

##### conc 310

|  | N | Min | Q1 | Median | Q3 | Max |
|---|---|---|---|---|---|---|
| brood1 | 10 | 0.00 | 5.00 | 5.50 | 6.00 | 7.00 |
| brood2 | 10 | 0.00 | 0.00 | 0.00 | 0.00 | 10.00 |
| brood3 | 10 | 0.00 | 0.00 | 0.00 | 0.00 | 0.00 |
| total | 10 | 0.00 | 5.00 | 6.00 | 6.00 | 15.00 |

以下代码将分类变量 `CONC` 移入行维度（将其与四个分析变量嵌套 `(brood1 brood2 brood3 total)*conc`，以便对每个浓度分别汇总四个变量）。表格条目也被格式化。

```
proc tabulate data=nitrofen format=3.;
class conc;
var brood1 brood2 brood3 total;
table (brood1 brood2 brood3 total)*conc,
n min q1 median*f=4.1 q3 max;
run;
```

如果在 `TABLE` 语句的行规格中切换嵌套顺序会怎样？如果请求以下表格，表格会如何变化？

```
table conc*(brood1 brood2 brood3 total),
n min q1 median*f=4.1 q3 max;
```

你更喜欢哪一个表格？

### 4.3 增强 `PROC TABULATE` 输出

到目前为止，你可能已经受够了硝基酚数据集。接下来使用不同国家的预期寿命数据作为示例。请求一个样本量、均值和标准差的表格，用于男性和女性的预期寿命。此外，还请求识字百分比和 `LOG10(GNP)`。数据代表人口密度稀疏的国家（处于人口密度第一四分位）、人口密度中等（处于人口密度中间 50%）和人口密度稠密的国家（处于人口密度前 25%）。该程序在显示 4.6 中展示。

#### 显示 4.6 针对人口密度不同四分位分别构建预期寿命、`GNP` 和识字百分比的数值统计汇总
