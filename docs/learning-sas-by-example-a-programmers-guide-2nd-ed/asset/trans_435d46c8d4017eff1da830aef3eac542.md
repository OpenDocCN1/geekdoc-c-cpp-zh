

## 第 8 章：执行迭代处理：循环 105

## 程序 8.6：使用 SUM 语句创建累积总量

```sas
data Revenue;
  input Day : $3.
  Revenue : dollar6;
  Total = Revenue;
  format Revenue Total dollar8;
datalines:
Mon $1,000
Tue $1,500
Wed
Thu $2,000
Fri $3,000
;
```

该程序的输出与程序 8.5 的输出相同。

SUM 语句的另一个非常常用的用途是创建计数器，例如：

## 程序 8.7：使用 SUM 语句创建计数器

```sas
data Test;
  input x;
  if missing(x) then MissCounter + 1;
datalines:
2
7
;
```

以下是输出结果：

## 图 8.5：数据集 Test 的列出

| 数据集 Test 列出 |
| x | MissCounter |
| 2 | 0 |
| | 1 |
| 7 | 1 |
| - | 2 |

MissCounter 正在统计 x 的缺失值数量。

## 106 实例型 SAS 学习：程序员指南，第二版

## 8.4 迭代 DO 循环

虽然当条件为真时执行一组代码的能力非常有用，但在某些情况下，你可能希望多次执行一组 SAS 语句。这里的程序没有编写任何迭代循环。

程序 8.8：不带迭代循环的程序

```sas
data Compound;
  Interest = .0375;
  Total = 100;

  Year + 1;
  Total + Interest*Total;
  output;

  Year + 1;
  Total + Interest*Total;
  output;

  Year + 1;
  Total + Interest*Total;
  output;

  format Total dollar10.2;
run;

title "Listing of Compound";
proc print data=compound noobs;
run;
```

这个程序的目的应该是显而易见的：你想要计算从 $100 开始，并以 3.75% 的利率投资 3 年后的总金额。（是的，复利有公式，也有 SAS 函数，但这只是一个很好的例子。）

正如我们讨论过的，`Year + 1` 语句是一个 SUM 语句。它每执行一次就会增加 Year 的值。Total 的值也是使用 SUM 语句计算的。注意，这里的增量可以是一个表达式（Interest * Total）。请记住 SAS 会在加法之前执行乘法，因为乘法的优先级更高。如果这有助于你理解程序，请随时加上括号。

`OUTPUT` 语句是指令 SAS 向输出数据集写入一个观测值。`output` 通常在 DATA 步的底部自动发生。但在这里，你希望在每次计算出新的 Total 时输出一个观测值。

> 注意：当你在 DATA 步的任何地方包含 OUTPUT 语句时，SAS 不会在 DATA 步的底部执行自动输出。

接下来，注意从这个 SUM 语句开始的三条语句组重复了三次。这暗示可能有一个更好的编写此程序的方法。更好的方法是使用迭代 DO 循环，如下所示：

## 程序 8.9：演示迭代 DO 循环

```sas
data Compound;
Interest = .0375;
Total = 100;
do Year = 1 to 3;
  Total = Total + Interest;
  output;
end;
format Total dollar10.2;
run;

title "Listing of Data Set Compound";
proc print data=Compound noobs;
run;
```

当此程序执行时，Year 首先被设置为 1，即迭代 DO 范围的下限。所有到 `END` 语句为止的语句都会执行，Year 会自动增加 1（默认增量值）。SAS 会测试 Year 的新值是否小于上限（关键字 TO 之后的值）。如果是，DO 组中的语句将再次执行；如果不是，程序将从 END 之后的第一行继续执行。

是时候提一下，此程序中的 `FORMAT` 语句是在编译时执行的，你可以将此语句放在 DATA 语句和结束 DATA 步的 RUN 语句之间的任何位置。

以下是输出结果：

## 图 8.6：程序 8.9 的输出

## 数据集 Compound 列出

| Interest | Total | Year |
|---|---|---|
| 0.0375 | $103.75 | 1 |
| 0.0375 | $107.64 | 2 |
| 0.0375 | $111.68 | 3 |

`OUTPUT` 语句的每次执行都会向数据集 Compound 写入一个观测值，并且每个 Year 的 Interest 值都会被加到 Total 中。

迭代 DO 语句的一种形式如下：

```
do index-variable = start to stop by increment;
```

如果你省略了增量，它默认为 1。

假设你想生成一个从 1 到 10 整数的表格，以及它们的平方和平方根。迭代 DO 循环可以轻松地完成这项工作，如下所示：

## 108 实例型 SAS 学习：程序员指南，第二版

## 程序 8.10：使用迭代 DO 循环创建平方和平方根表

```sas
data Table;
  do n = 1 to 10;
    Square = n*n;
    SquareRoot = sqrt(n);
    output;
end;
title "Table of Squares and Roots";
proc print data=table noobs;
```

注意这个程序没有 input。它在 DO 循环中生成 n 的值，计算平方和平方根（SQRT 是平方根函数），并为 1 到 10 的所有值输出观测值。以下是输出：

## 图 8.7：程序 8.10 的输出

## 平方和根

| n | Square | SquareRoot |
|---|---|---|
| 1 | 1 | 1.0000 |
| 2 | 4 | 1.4142 |
| 3 | 9 | 1.7321 |
| 4 | 16 | 2.0000 |
| 5 | 25 | 2.2361 |
| 6 | 36 | 2.4495 |
| 7 | 49 | 2.6458 |
| 8 | 64 | 2.8284 |
| 9 | 81 | 3.0000 |
| 10 | 100 | 3.1623 |

如果你想要一个 n 的值为 0, 10, 20, 30 直到 100 的表格怎么办？下面的 DO 语句可以做到：

```sas
do n = 0 to 100 by 10;
```

DO 循环也可以倒数。例如，后面的语句产生了索引变量值为 10, 8, 6：

```sas
do index = 10 to 2 by -2;
```

当你使用负增量值时，索引值每次迭代都会减少该值。当索引变量小于停止值时，循环停止。

这是另一个例子。有一个关于 X 和 Y 的方程，并想要从 -10 到 +10 的值的 Y 对 X 图。再次，迭代 DO 循环让这非常简单：

## 程序 8.11：使用迭代 DO 循环绘制方程

```sas
data Equation;
  do X = -10 to 10 by .01;
  Y = 2*X**3 - 5*X**2 + 15*X - 8;
  output;
end;
title "Plot of Y = 2*X**3 - 5*X**2 + 15*X - 8";
proc sgplot;
  series x=X y=Y;
run;
```

DO 循环从 -10 开始 X，并增加 .01 直到 X 达到 +10。循环内部的 OUTPUT 语句每次迭代都会向数据集写入一个观测值。PROC SGPLOT 用于绘制线条。你可以在第 20 章获取有关 PROC SGPLOT 的信息。以下是图表：

## 图 8.8：程序 8.11 的输出

![](img/e9e15d8539895818e1c83b0ae65b0_121_0.png)

## 8.5 迭代 DO 循环的其他形式

SAS 提供了其他方法来指定 DO 循环如何运行。你可以在索引变量后提供数值或字符列表。是一些示例：

```sas
do x = 1,2,5,10;
(x 的值为：1, 2, 5 和 10)
do Month = 'Jan', 'Feb', 'Mar';
(Month 的值为：'Jan', 'Feb' 和 'Mar')
do n = 1,3, 5 to 9 by 2, 100 to 200 by 50;
(n 的值为：1, 3, 5, 7, 9, 100, 150 和 200)
```

如果你在 DO 语句中使用字符值，第一个字符值的长度决定了索引变量的存储长度。因此，你可能需要使用 LENGTH 语句为索引变量设置长度。

使用字符值进行 DO 循环特别有用，正如这个示例所示。

你有五个接受安慰剂患者的得分，和五个接受活性药物患者的得分。数据值排列如下：

250 222 230 210 199
166 183 123 129 234

读取这些值的一种简单方法是使用带有 DO 索引值的循环，如下所示：

## 程序 8.12：使用字符作为 DO 循环索引值

```sas
data Easyway;
do Group = 'Placebo','Active';
  do Subj = 1 to 5;
    input Score @;
    output;
end;
datalines;
250 222 230 210 199
166 183 123 129 234

title "Listing of Data Set Easyway";
proc print data=Easyway noobs;
run;
```

为了保持程序紧凑，将多个得分放在同一行是方便的。如果没有 @ 符号，每次 SAS 执行 INPUT 语句时，都会跳到数据的新的一行。末尾的 @ 符号是指令为 DATA 步中的另一个 INPUT 语句“留住行”。

