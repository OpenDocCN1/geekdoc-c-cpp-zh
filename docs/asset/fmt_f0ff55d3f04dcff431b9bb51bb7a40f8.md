
| 0.0375 | $115.87 | 4 |
| 0.0375 | $120.21 | 5 |
| 0.0375 | $124.74 | 6 |
| 0.0375 | $129.39 | 7 |
| 0.0375 | $134.25 | 8 |
| 0.0375 | $139.28 | 9 |
| 0.0375 | $144.50 | 10 |
| 0.0375 | $149.92 | 11 |
| 0.0375 | $155.55 | 12 |
| 0.0375 | $161.38 | 13 |
| 0.0375 | $167.43 | 14 |
| 0.0375 | $173.71 | 15 |
| 0.0375 | $180.22 | 16 |
| 0.0375 | $186.98 | 17 |
| 0.0375 | $193.99 | 18 |
| 0.0375 | $201.27 | 19 |

**注意：** 关于 `DO UNTIL` 需要记住的一个重要点是，放置在关键字 `UNTIL` 后括号中的条件是在循环的**底部**测试的。因此，`DO UNTIL` 循环始终**执行至少一次**。

为了清楚这一点，假设你起初资金是 $300。当你运行程序时会发生什么？

## 程序 8.14：演示 DO UNTIL 循环始终至少执行一次

```
data Double;
  Interest = .0375;
  Total = 300;
  do until (Total gt 200);
    Year + 1;
    Total = Total + Interest*Total;
    output;
  end;
  format Total dollar10.2;
run;

proc print data=double noobs;
  title "Listing of Double";
run;
```

即使在循环开始之前条件就已经为真，但由于条件是在循环底部测试的，此程序仍输出一个观测值（如下所示）：图 8.11：程序 8.14 的输出 (`img/6f22781b0ad998ef00cc7e227.png`)

`DO UNTIL` 的替代方案是 `DO WHILE`。正如你预期的，只要 `WHILE` 后后的条件为真，`DO WHILE` 循环就会迭代。`DO WHILE` 和 `DO UNTIL` 之间没有区别——**条件是在循环的顶部测试的**，而不是底部。

与至少执行一次的 `DO UNTIL` 块不同，如果条件为假，`DO WHILE` 块就不会执行。你可以像这样使用 `DO WHILE` 语句重写程序 8.13：

## 程序 15：演示 DO WHILE 语句

```
data Double;
Interest = .0375;
Total = 100;
do while (Total le 200);
  Year + 1;
  Total = Total + Interest*Total;
  output;
end;
format Total dollar10.2;
run;

proc print data=double noobs;
  title "Listing of Double";
run;
```

`WHERE` 和 `END` 之间的代码块只要 `Total` 小于 200 就会执行。此程序的输出与 8.13 相同。为了强化 `DO WHILE` 条件在循环顶部测试的观点，请看此程序：

## 程序 8.16：演示 DO WHILE 循环在顶部求值

```
data Double;
Interest = .0375;
Total = 300;
do while (Total lt 200);
  Year + 1;
  Total = Total + Interest*Total;
  output;
end;
format Total dollar10.2;
run;
```

因为 `WHILE` 条件永远为假，`DO` 块内的语句不会执行。

## 8.7 使用 DO UNTIL 语句的注意事项

`DO UNTIL` 语句上的条件在某点变为真是非常重要的。例如，如果你如下所示更改程序 8.14 中的 `DO UNTIL` 语句，条件将永远为真，你就有了所谓的无限循环：这取决于你是否为时间付费，这可能是很糟糕（昂贵的）。在 PC 平台上，你可以点击停止图标或同时点击 `CTRL` 键来中断程序。防止无限循环的一种方法是将普通循环与 `UNTIL` 条件结合。你可以这样重写程序：

## 程序 17：将 DO UNTIL 和迭代循环结合

```
data Double;
Interest = .0375;
Total = 100;
do Year = 1 to 100 until (Total gt 200);
Total = Total + Interest*Total;
output;
end;
format Total dollar10.2;
run;
```

这种结构有两个优点：首先，即使 `UNTIL` 条件变为真，循环在 `Year` 达到 100 时结束，你不需要像程序 8.13 那样在循环内部为 `Year` 赋值。

## 8.8 LEAVE 和 CONTINUE 语句

`DO` 循环中的 `LEAVE` 语句会将控制转移到循环底部 `END` 语句之后的语句。`CONTINUE` 语句停止 `DO` 循环内语句的执行并继续循环迭代。**注意：** 你也可以在 `SELECT` 中使用 `LEAVE` 语句。程序 8.18 展示了 `LEAVE` 语句的工作原理。

## 程序 8.18：演示 LEAVE 语句

```
data Leave_it;
Interest = .0375;
Total = 100;
do Year = 1 to 100;
  Total = Total + Interest*Total;
  output;
  if Total ge 200 then leave;
end;
format Total dollar10.2;
run;
```

在此程序中，循环持续到 `Total` 大于或等于 200。此时，`LEAVE` 语句终止了循环，你处于 `DATA` 步底部的 `RUN` 语句。为了演示 `CONTINUE` 语句，请看以下程序：

## 程序 8.19：演示 CONTINUE 语句

```
data Continue_on;
Interest = .0375;
Total = 100;
do Year = 1 to 100 until (Total ge 200);
  Total = Total + Interest*Total;
  if Total le 150 then continue;
  output;
end;
format Total dollar10.2;
run;

title "Listing of Data Set_on";
proc print data=Continue_on noobs;
run;
```

只要 `Total` 小于等于 150，`CONTINUE` 语句就会执行跳转到循环底部（跳过 `OUTPUT` 语句）并继续循环。当 `Total` 大于 150 时，发生输出，外层循环持续到 `Total` 大于 200。因此，此程序打印大于 150 的 `Total` 值，直到 `Total` 达到或超过 200。以下是输出：

图 8.12：程序 8.19 的输出

| Listing of Data Set Continue_on | | |
| Interest | Total | Year |
| --- | --- | --- |
| 0.0375 | $155.55 | 12 |
| 0.0375 | $161.38 | 13 |
| 0.0375 | $167.43 | 14 |
| 0.0375 | $173.71 | 15 |
| 0.0375 | $180.20 | 16 |
| 0.0375 | $186.98 | 17 |
| 0.0375 | $193.99 | 18 |
| 0.0375 | $201.27 | 19 |

正如你在本章看到的，SAS 中的迭代语句可以使程序更短、更易理解。它们还允许你编写 `DATA` 步为创建表格或绘图函数生成数据。

## 8.9

奇数题的解答位于书的末尾。所有题目的解答对教授开放。如果你是教授，请访问书籍的辅助网站 `support.sas.com/cody` 了解如何获取所有问题的解答。

- 在此处运行程序创建一个名为 `Vitals` 的临时 SAS 数据集：

```
data Vitals;
  input ID : $3.
  Age
  Pulse
  DBP;
label SBP = "Systolic Blood Pressure"
       DBP = "Diastolic Blood Pressure";\datalines
  001 23 68 120 80
  002 55 72 188 96
  003 78 82 200 100
  004 18 58 110 70
  005 43 52 120 82
  006 37 74 150 98
  007 . 82 140 100;
```

# 118 以学习 SAS 为例：程序员指南，第二版

使用此数据集，创建一个包含以下变量的新数据集 (`NewVitals`)：

对于年龄小于 50 岁的受试者：

- 如果 `Pulse`（脉搏）小于 70，将 `PulseGroup` 设置为 Low（低）；
- 否则，将 `PulseGroup` 设置为 High（高）。
- 如果 `SBP`（收缩压）小于 130，将 `SBPGroup` 设置为 Low（低）；
- 否则，将 `SBPGroup` 设置为 High（高）。

对于年龄大于或等于 50 岁的受试者：

- 如果 `Pulse` 小于 74，将 `PulseGroup` 设置为 Low（低）；
- 否则，将 `PulseGroup` 设置为 High（高）。
- 如果 `SBP` 小于 140，将 `SBPGroup` 设置为 Low（低）；
- 否则，将 `SBPGroup`为 High（高）。

你可以假设 `Pulse` 或 `SBP` 没有缺失值。

- 2. 运行程序创建一个临时 SAS 数据集 (`MonthSales`)：

```sas
data MonthSales;
input month sales @@;
/* 在此处添加你的代码 */
datalines;
1 1400 2 2500 3 4500 5 5000 6 6000 7 6500 8 4500
9 5100 10 5700 11 6500 12 7500
;
```

修改程序，向数据集中添加一个新变量 `SumSales`，代表截至目前的销售额。确保第 3 个月的 `Sales` 缺失值不会导致 `SumSales` 缺失。

- 3. 修改下面的程序，使每个观测值包含一个受试者编号 (`Subj`)，并从 `I` 开始：

```sas
data Test;
input Score1-Score3;
/* 在此处添加你的代码 */
datalines;
90 88 92
75 76 88
88 82 91
72 68 70
;
```

- 4. 统计 `Missing` 数据集中变量 `A`、`B` 和 `C` 的缺失值数量。在每个观测值中添加缺失值的累计数量（变量名为 `MissA`、`MissB`、`MissC`）。使用 `MISSING` 函数测试缺失值。

- 5. 创建并打印一个包含变量 `N` 和 `LogN` 的数据集，其中 `LogN` 是 `N` 的自然对数（函数为 `LOG`）。使用 `DO` 循环创建一个显示从 1 到 20 的 `N` 和 `LogN` 值的表格。

- 6. 重复问题 5，但 `N` 的范围从 5 到 100，步长为 5。

# 第 8 章：执行迭代处理：循环 119

7. 使用迭代 `DO` 循环绘制方程：

```sas
y = 3*x^2 - 5*x + 10
```

使用从 0 到 10 的 `x` 值，步增量为 0.10。使用下面的代码显示生成的方程。

```sas
title "Problem 7";
proc sgplot data=plotit;
series x=x y=y;
run;
```

8. 使用迭代 `DO` 循环绘制方程：

```sas
Logit = log(p / (1 - p))
```

使用从 0 到 1 的 `p` 值（每 0.05 有一点）。使用以下 `SGPLOT` 语句将产生一个非常精美的图表。

```sas
title "Logit Plot";
proc sgplot data=Logit;
series x=p y=Logit;
run;
```

9. 你有每周每天的七个温度值，从周一开始：70, 72, 74, 76, 77, 78 和 85。创建一个临时 SAS 数据集 (`Temperatures`)，其中变量 (`Day`) 等于 Mon, Tue, Wed, Thu, Fri, Sat，变量 `Temp` 等于列出的值。使用 `DO` 循环创建 `Day` 变量。

10. 你正在测试三种读取方法（A、B 和 C），通过将 100 个受试者随机分配到这三种方法中的每一种。给结果是三行读取速度，每行分别代表这三种方法的结果。结果如下：

| 250 | 255 | 256 | 300 | 244 | 268 | 301 | 312 | 252 | 253 | 333 |
| 267 | 275 | 256 | 320 | 250 | 340 | 345 | 290 | 280 | 300 |
| 350 | 350 | 340 | 350 | 377 | 401 | 380 | 310 | 299 | 399 |

从这三行数据创建一个临时 SAS 数据集。每个观测值应包含 `Method` (`A`、`B` 或 `C`) 和 `Score`。此数据中有 30 个观测值。使用 `DO` 循环创建该变量，并在 `INPUT` 语句中使用单个末尾的 `@`。使用 `PROC PRINT` 为每个数据集提供列表。

11. 你有每天每小时的每日数据（达拉斯和休斯顿）。48 个温度值存储在如下行中：

```
80 81 82 83 84 87 88 89
91 92 93 94 95 96
97
```

这 48 个值代表达拉斯和休斯顿的温度。创建一个临时数据集 (`Temperatures`)，其中变量 (`City`) 等于 Dallas 或 Houston，变量 `Temp` 等于对应的值。使用 `DO` 循环创建 `Day` 变量。

12. 你正在测试三种读取方法（A、B 和 C），通过将 100 个受试者随机分配到这三种方法中的每一种。给结果是三行读取速度，每行分别代表这三种方法的结果。结果如下：

（注：此处原文似乎存在逻辑重复或错乱，已根据上下文尽量翻译）

[此处重复了部分内容]

13. 你以 4.25% 的利率投资 1000。需要多少年能达到 30000？使用 `DO` way `WHILE` 语句来完成此任务。

14. 生成一个从 1 开始大于 100 的平方。

# 第 9 章：处理日期 123

缩写和四位年份。用于这些日期的列数为 9，且输入格式（informat）为 `DATE`。

这些日期中的每一个都是通过相应的 SAS 输入格式（informat）读取的。在读取这些日期时，SAS 会将所有日期转换为其对应的数值。要查看此内容，有一个由 `PROC PRINT` 生成的列表：

# 图 9.1：数据集 Four_Dates 的列表

| Subject（受者） | DOB | VisitDate | TwoDigit | LastDate |
| --- | --- | --- | --- | --- |
| 001 | -3359 | 15837 | 2048 | 16793 |
| 002 | 0 | 18213 | 15596 | 1 |

此列表中的数字代表 SAS 从原始数据中读取并转换的四个日期的内部存储值。这些值的存储方式与 SAS 存储数值的方式相同。

你可以选择任何 SAS 日期格式（format）来显示这些值——它们不需要与读取日期时使用的输入格式（informat）匹配。为了演示这一点，下一个程序在 `DATA` 步中添加了一个 `FORMAT` 语句，如下：

# 程序 9.2：为每个数据值添加 FORMAT 语句

```
data Four_Dates;
infile C:\windows\Dates.txt truncate;
input @1 Subject $;
@5 DOB mmddy10;
@16 VisitDate mmddyy8;
@26 TwoDigit mmddyy8;
@34 LastDate date9;
format DOB VisitDate date9;
TwoDigit LastDate mmddy10;
```

两种非常流行的日期格式是 `DATE9` 和 `MMDYY10`。再次，重要的是根据你选择的显示方式将日期隔开。以下是带有格式化日期值的列表：

# 图 9.2：带有格式化日期的 Four_Dates 列表

| Subject（受者） | DOB | VisitDate | TwoDigit | LastDate |
| --- | --- | --- | --- | --- |
| 001 | 21OCT1950 | 12MAY2003 | 08/10/1965 | 12/23/2005 |
| 002 | 01JAN1960 | 12NOV2009 | 09/13/2002 | 01/02/1960 |

关于 SAS 如何读取这四个日期值，有几点需要注意。首先，其中两个日期（`VisitDate` 和 `TwoDigit`）都使用了相同的输入格式（`MMDDYY8`），因为这两个日期值都占据了 8 列。SAS 足够聪明，能够意识到 `VisitDate` 使用了分隔符，因此年份必须是四位数。`TwoDigit` 的值包含分隔符；年份值必须是两位数。如果月份、日期或值不包含 0，所有这些值也都会被正确读取。

接下来，注意此列表中 `TwoDigit` 的值。第一个观测值显示年份为 1965，而第二个观测值显示年份为 2002。SAS 是如何判断是将这两个数字设为 19 还是 20 的？
