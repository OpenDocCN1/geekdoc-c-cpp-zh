

## 第 22 章：使用自定义格式和输入格式的高级功能

## 程序 22.15：在 DATA Step 中使用嵌套格式

```sas
data Conference;
  input @1 Name $10;
    @11 Date mmddyy10;
  format Date Registration;
datalines;
Smith 10/21/2018
Jones 11/13/2017
Harris 01/03/2018
Arnold 02/12/2019
;
```

此处显示了数据集 Conference 的列表：

## 图 22.16：数据集 Conference 的列表

| Name | Date |
| --- | --- |
| Smith | 10/21/2018 |
| Jones | Not Open |
| Harris | 01/03/2018 |
| Arnold | Too Late |

这是 PROC FORMAT 的一个非常强大的功能。它避免了在 DATA Step 中编写 IF-THEN-ELSE 语句的必要性。

下一个示例使用了用户自定义的输入格式（informats）。在这个示例中，你被提供了关于苯暴露的数据。其中某些值是每百万部分的实际苯水平，而另一些值是工人暴露的年份。对于 1946 年到 1952 年的每一年，苯水平都制表了。对于范围之外的年份，报告了实际苯水平。接下来显示了来自 Benzene.txt 的一些样本数据，包含年份或苯水平：

```
001 90
002 1950
003 217
004 1952
005 177
```

所有的苯水平都远小于任何年份值，因此不会混淆是将某个值读作年份还是苯水平。通过像这样嵌套输入格式，可以极大地简化创建 ID 和苯水平的数据集创建过程：

## 程序 22.16：创建苯水平数据集

```sas
proc format;
  value YearExp 1946 = 250
                    1947 = 244
                    1948 = 240
                    1949 = 200
                    1950 = 188
                    1951 = 150;
  1952 -;
  value Exp Low - <1946 = [7.1]
                    1946 - 1952 = [Yearexp].
                    1952< high = [7.1];

data Benzene;
  infile 'C:\Learning\Benzene.txt';
  input Exposure = Exp4.;
```

第一个输入格式 YAREXP 为 1946 年到 1952 年的每一年替换一个苯水平。输入格式 EXP 对于小于 1946 或大于 1952 的值使用 SAS 7.1 输入格式。否则，使用 YAREXP 输入格式。

以下是该数据集的列表：

## 图 22.17：数据集 Benzene 的列表

## 数据集 Benzene 的列表

| ID | Exposure |
| --- | --- |
| 1 | 9.0 |
| 2 | 188.0 |
| 3 | 21.7 |
| 4 | 100.0 |
| 5 | 17.7 |

这个问题也可以使用格式（formats）而不是输入格式（informats）来解决。使用格式，你需要读取原始数据值并使用 PUT 函数来获取格式化后的值。由于 PUT 函数的结果是字符值，你还需要使用 INPUT 函数来获取作为数值形式的苯水平。创建格式会使该过程变得简单得多。

## 22.10 多标签格式 (Multilab Formats)

在正常情况下，如果你的任何格式范围发生重叠，你将收到错误消息。但是，如果你在 VALUE 语句中使用 MULTILABEL 选项，就可以创建一个具有重叠范围的格式。某些使用多标签的过程随后可以使用 MULTILABEL 格式 (MLF) 来生成显示所有格式范围的表格。这里有一个示例。

你想以两种方式对变量 Age（来自 Survey 数据集）进行细分：一种是每 20 年一个间隔，另一种是按 50 岁作为分界点进行划分。你首先像这样创建一个 MULTILABEL 格式：

## 程序 22.17：创建一个 MULTILABEL 格式

```sas
proc format;
  value AgeGroup (multilabel)
    0 <20 = '00 to <20'
    20 <40 = '20 to <40'
    40 <60 = '40 to <60'
    60 <80 = '60 to <80'
    80 - high = '80 +'

    0 <50 = 'Less than 50'
    50 - high = '> or = to 50';
run;
```

如果没有 MULTILABEL 选项，PROC FORMAT 会发出关于范围重叠的错误消息并无法创建格式。

你可以在 PROC MEANS、PROC SUMMARY 和 PROC TABULATE 中使用此格式。这是一个 PROC MEANS 示例：

## 程序 22.18：在 PROC MEANS 中使用 MULTILABEL 格式

```sas
title "Demonstrating Multilabel Format"
title2 "PROC MEANS Example";
proc means data=Learn.Survey / MLF;
  class Age;
  var Salary;
  format AgeGroup;
run;
```

如果你想使用格式的这一功能，在 CLASS 语句中使用 MLF 选项是重要的。以下是输出：

## 图 22.18：程序 22.18 的输出

## 多标签格式 PROC示例

| Analysis Variable : Salary | Obs | Mean | Std Dev | Maximum |
| --- | --- | --- | --- | --- |
| Age of 1/1/2006 | N | | | |
| 20 to <40 | 3 | 3 | 29186.67 | 6798.13 | 36560.00 |
| 40 to <60 | 2 | 2 | 76111.50 | 16234.56 | 76100.00 |
| 60 to <80 | 2 | 2 | 109000.00 | 26870.06 | 90000.00 |
| > or = to 50 | 3 | 3 | 98041.00 | 26857.01 | 76123.00 |
| Less than 50 | 4 | 4 | 40915.00 | 24104.46 | 76100.00 |

你可以将 MULTILABEL 格式配合 PROC TABULATE 创建有趣的表格。这里有一个按性别计算年龄频率的程序：

## 程序 22.19：多标签格式

```sas
title "Demonstrating Multabel Format";
title2 "PROC TABULATE Example";
proc tabulate data=Learn.Survey;
  class Age / MLF;
  table Age * Gender;
  format AgeGroup;
run;
```

这产生了以下输出：

## 程序 22.19：程序 22.19 的输出多标签格式 PROC TABULATE 示例

| | Female | Male |
| --- | --- | --- |
| | N | N |
| Age as 1/1/2006 | | |
| 20 to <40 | | 3 |
| 40 to <60 | 2 | |
| 60 to <80 | 1 | 1 |
| or = to 50 | 2 | 1 |
| Less than 50 | 1 | 3 |

注意某些年龄组没有显示在表中。例如，没有 0 <20 年龄组。要在表中显示所有格式范围，可以使用 CLASS 语句中的 PRELOADFMT 选项。预加载格式允许 PROC TABULATE 列出没有数据的类别。

## 程序 22.20：在 PROC TABULATE 使用 PRELOADDFMT, PRINTMISS 和 MISSTEXT 选项

```sas
title "Demonstrating a Multilabel Format";
title2 "PROC TABULATE Example";
proc tab data=Learn.Survey;
  class Age / MLF preloadfmt;
  table Age;
    Gender / printmiss misstext=' ';
  format AgeGroup.;
run;
```

PRELOADDFMT 选项强制过程列出所有格式范围。该选项对 TABLE 语句中的 PRINTMISS 选项无效。记住 PRINTMISS 是包含一个多个 CLASS 变量缺失值的指令。最后，MISSTEXT= 告诉过程使用哪个字符（或字符）来表示缺失值（点）。在这里你选择一个空格来表示缺失值。最后是输出：

## 图 22.20：程序 22.20 的输出

| Gender | Female | Male |
| --- | --- | --- |
| Age as 1/1/2006 | N | N |
| 0 to <20 | | |
| 20 to <40 | | 3 |
| 40 to <60 | 2 | |
| 60 to <80 | 1 | 1 |
| 80 + | | |
| > or = to 50 | 2 | 1 |
| Less than 50 | 1 | 3 |

现在所有的年龄范围都出现在表中，缺失值打印为空格。

## 22.11 使用 INPUTN 函数执行更复杂的查找

问题：你有一张年份（1944年到1949年）和工作代码的表格。每个年份和工作代码的组合都有对应的苯暴露（百万部分）。以下是表值：

| Year | A | B | C | D | E |
| --- | --- | --- | --- | --- | --- |
| 1944 | 220 | 180 | 210 | 110 | 90 |
| 1945 | 202 | 170 | 208 | 100 | 85 |
| 1946 | 150 | 110 | 150 | 60 | 50 |
| 1947 | 105 | 56 | 88 | 40 | 30 |
| 1948 | 60 | 30 | 40 | 20 | 10 |
| 1949 | 45 | 22 | 22 | 10 | 8 |

给定年份和工作代码计算暴露量的一种方法是为每一年创建一个输入格式，为每个工作代码分配一个包含暴露值的标签。使用输入格式而不是格式，是因为你可以配合自定义输入格式使用 INPUT（或你将看到的 INPUTN）函数来直接获取数值。如果你“手动”操作，将如下所示：

## 程序 22.21：显示创建多个输入格式的部分程序

```sas
proc format;
  invalidate Exp1944fmt (upcase);
    'A' = 220
    'B' = 180
    'C' = 210
    'D' = 110
    'E' = 90
  other = ;
  invalidate Exp1945fmt (upcase);
    'A' = 202
    'B' = 170
    'C' = 208
    'D' = 100
    'E' = 85
  other = ;
  invalidate Exp1946fmt (upcase);
    'A' = 150
run;
```

创建一个输入控制数据集（CNTLIN）来创建所需的输入格式工作量更少。你按照如下操作：

