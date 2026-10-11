
| `CONTAINS` | 匹配子字符串 | `where Name contains Mac` |

| `LIKE` | 使用通配符匹配 | `where Name like R_*` |

| `*=` | 匹配 | `where Nicki` |

> 注意：使用 `LIKE` 运算符时，下划线 (`_`) 代表单个字符，而百分号 (`%`) 可以替换为任意长度的字符串。以下是一些示例：

| 表达式 | 匹配 |

|---|---|

| `where Gender is null` | 字符缺失 |

| `where Age is null` | 数值缺失 |

| `where Age is missing` | 数值缺失 |

| `where Age between 20 and 40` | 在 20 到 40 之间的所有值 |

| `where Name contains 'mac'` | immaculate |

| `where Name like R_*` | Running |

| `where *= Nick` | Nicki |

说明：

- `NULL` 或 `MISSING` 表达式匹配字符或数值缺失值。
- `AND` 表达式匹配所有大于第一个值的值。
- `CONTAINS` 表达式匹配任何字符值。
- `LIKE` 表达式使用了两个下划线。
- 百分号 (`%`) 匹配字符串长度。

## 7.10 练习

答案位于书末。要获取有关问题的信息，请访问辅助网站。

## 第7章：条件处理

1. 运行此处程序创建一个临时数据集：

```sas
data School;
input Age Quiz $ Midterm Final;
/* 在此处添加语句 */
datalines;
12 A 92 95
12 B 88 88
13 C 78 75
12 A 92 93
12 F 55 62
13 B 88 82
;
```

使用 `IF` 和 `ELSE IF` 语句创建两个新变量：`Grade`（数值），如果年龄为12为6，如果年龄为13为8。成绩的等值为：`A = 95`, `B = 85`, `C = 75`, `D = 70`, `F = 65`。

2. 使用 `Sales` 数据集使用 `PROC PRINT` 列出 `Subject` 为 5、10、150 和 200 的观测值。执行两次，分别使用 `OR` 运算符和 `IN` 运算符。**注意：**`Subject` 是数值变量。

3. 使用 `Sales` 数据集，创建一个新的临时数据集 `Sales`，并添加一个新变量 `Weight`，其中北部地区为1.5，南部地区为1.7，西部和东部地区为2.0。使用 `SELECT` 语句来实现。

4. 从 `Blood` 数据集开始，创建一个包含 `Blood` 所有变量以及一个新变量 `CholGroup` 的临时数据集。定义此新变量如下：

| `CholGroup` | `Chol` |

|---|---|

| Low | Low – 110 |

| Medium | 111 – 140 |

| High | 141 – High |

5. 使用 `Sales` 数据集，列出所有区域为 **North** 且数量小于 **60** 的观测值。在该列表中，包含任何客户名称（`Customer`）为 **Pet's** 或 ** Us** 的观测值。

## 第 8 章：迭代处理：循环

+ 8.1 引言 .......................................................................................................... 99
+ 8.2 DO 组 ............................................................................................................ 99
+ 8.3 Sum 语句 ........................................................................................... 101
+ 8.4 迭代 DO 循环............................................................................... 106
+ 8.5 迭代 DO 循环的其他形式 ................................................................ 110
+ 8.6 DO WHILE 和 DO UNTIL 语句 ................................................................ 112
+ 8.7 使用 DO UNTIL 语句时的注意事项 ................................... 115
+ 8.8 LEAVE 和 CONTINUE 语句 ................................................................ 116
+ 8.9 问题 ................................................................................................ 117

### 8.1 引言

许多编程任务要求代码块运行多次。SAS 提供了几种方法来实现这一点。本章涵盖了 DO 组、DO 循环、DO WHILE 语句以及 DO UNTIL 语句。

## 8.2 DO 组

为了演示 DO 组，我们从一个包含学生信息的数据文件开始：他们的年龄、性别、期中成绩、测验和考试成绩。以下是数据文件 `C:\books\learningGrades.txt` 的列示：

```
21 M 80 B - 82
  F 90 A - 93
35 M 87 B+ - 85
48 F - 76
59 F 95 A+ 97
15 M 88 - 93
67 F 97 A - 91
  M 62 F - 61
35 F 77 C- 77
49 M 59 C - 81
```

你想从此文件中读取值并计算两个新变量——年龄组（`AgeGroup`）以及一个根据期中和期末考试计算出的数值（`Grade`）。如果年龄小于或等于 39，你想将 `AgeGroup` 设置为 "Younger group"（年幼组），并将成绩计算为期中成绩（40%）和期末考试（60%）的加权平均值。如果年龄大于 39，你想将 `AgeGroup` 设置为 "Older group"（年长组），并将成绩计算为期中和期末考试的简单平均值。

来看解决此问题的程序 8.1：

### 程序 8.1：不使用 DO 组的程序示例

```
data Grades;
  length Gender $ 1
  Quiz $ 2
  AgeGroup $ 13;
  infile 'C:\books\learning\Grades.txt' mov;
  input Age Gender Midterm Quiz FinalExam;
  if missing(Age) then delete;
  if le 39 then AgeGroup = 'Younger group';
  if le 39 then Grade = .4*Midterm + .6*FinalExam;
  if gt 39 then AgeGroup = 'Older group';
  if gt 39 then Grade = (Midterm + FinalExam)/2;
run;
```

注意前两个 `IF` 语句和最后两个 `IF` 语句测试的是同一个条件。你想测试一个条件并执行若干操作。通过使用 `DO` 和 `END` 语句，你可以做到。程序 8.2 的工作方式与程序 8.1 相同，但它使用 `DO` 和 `END` 语句使代码更高效、更易读：

### 程序 8.2：演示 DO 组

```sas
data Grades;
  length Gender $ 1
  Quiz $ 2
  AgeGroup $ 13;
  infile 'C:\books\learning\Grades.txt' mov;
  input Age Gender Midterm Quiz FinalExam;
  if missing(Age) then delete;
  if le 39 then do;
    AgeGroup = 'Younger group';
    Grade = .4*Midterm + .6*FinalExam;
  end;
  else if gt 39 then do;
    AgeGroup = 'Older group';
    Grade = (Midterm + FinalExam)/2;
  end;
run;
```

```sas
title "Listing of Grades";
proc print data=Grades noobs;
run;
```

`DO` 和 `END` 之间的语句形成了一个 `DO` 组。当 `IF` 条件成立时，组内的所有语句都会执行。一种很好的思考方式是：“如果条件成立，则执行以下语句直到结束。”将 `DO` 组中的所有语句缩进是标准做法。

`DO` 组的编码不仅比多个 `IF` 语句高效，而且更易读。以下是数据集的列表：

图 8.1：程序 8.2 的输出

| Gender | Quiz | AgeGrp | Age | Midterm | FinalExam | Grade |

|---|---|---|---|---|---|---|

| M | B- | Younger group | 21 | | 82 | 81.2 |

| M | B+ | Younger group | 35 | 87 | 85 | 85.8 |

| F | | | 48 | | 76 | - |

| F | A+ | Older group | 59 | 95 | 97 | 96.0 |

| M | | Younger group | 15 | 88 | 93 | 91.0 |

| F | A | Older group | 67 | 97 | 91 | 94.0 |

| F | C- | Older group | 35 | 77 | 77 | 77.0 |

| M | C | Older group | 49 | 59 | 81 | 70.0 |

你应该注意，当年龄存在缺失值时，这两个程序都能正常工作。如果参数是缺失的字符或数值，`MISSING` 函数会返回真值。`DELETE` 语句起两个作用：首先，它防止处理当前观测值。

### 8.3 Sum 语句

（注：此处后续内容原文中存在大量重复，已按要求仅翻译核心部分）

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

`SUM` 语句的另一个非常常用的用途是创建计数器，例如：

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

`MissCounter` 正在统计 `x` 的缺失值数量。

## 106 实例型 SAS 学习：程序员指南，第二版

### 8.4 迭代 DO 循环

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

正如我们讨论过的，`Year + 1` 语句是一个 `SUM` 语句。它每执行一次就会增加 `Year` 的值。`Total` 的值也是使用 `SUM` 语句计算的。注意，这里的增量可以是一个表达式（`Interest * Total`）。请记住 SAS 会在加法之前执行乘法，因为乘法的优先级更高。如果这有助于你理解程序，请随时加上括号。

`OUTPUT` 语句是指令 SAS 向输出数据集写入一个观测值。`output` 通常在 DATA 步的底部自动发生。但在这里，你希望在每次计算出新的 `Total` 时输出一个观测值。

> 注意：当你在 DATA 步的任何地方包含 `OUTPUT` 语句时，SAS 不会在 DATA 步的底部执行自动输出。

接下来，注意从这个 `SUM` 语句开始的三条语句组重复了三次。这暗示可能有一个更好的编写此程序的方法。更好的方法是使用迭代 `DO` 循环，如下所示：

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

当此程序执行时，`Year` 首先被设置为 1，即迭代 `DO` 范围的下限。所有到 `END` 语句为止的语句都会执行，`Year` 会自动增加 1（默认增量值）。SAS 会测试 `Year` 的新值是否小于上限（关键字 `TO` 之后的值）。如果是，`DO` 组中的语句将再次执行；如果不是，程序将从 `END` 之后的第一行继续执行。

是时候提一下，此程序中的 `FORMAT` 语句是在编译时执行的，你可以将此语句放在 `DATA` 语句和结束 `DATA` 步的 `RUN` 语句之间的任何位置。

以下是输出结果：

## 图 8.6：程序 8.9 的输出

## 数据集 Compound 列出

| Interest | Total | Year |

|---|---|---|

| 0.0375 | $103.75 | 1 |

| 0.0375 | $107.64 | 2 |

| 0.0375 | $111.68 | 3 |

`OUTPUT` 语句的每次执行都会向数据集 `Compound` 写入一个观测值，并且每个 `Year` 的 `Interest` 值都会被加到 `Total` 中。

迭代 `DO` 语句的一种形式如下：

```
do index-variable = start to stop by increment;
```

如果你省略了增量，它默认为 1。

假设你想生成一个从 1 到 10 整数的表格，以及它们的平方和平方根。迭代 `DO` 循环可以轻松地完成这项工作，如下所示：

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

注意这个程序没有 `input`。它在 `DO` 循环中生成 `n` 的值，计算平方和平方根（`SQRT` 是平方根函数），并为 1 到 10 的所有值输出观测值。以下是输出：

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

如果你想要一个 `n` 的值为 0, 10, 20, 30 直到 100 的表格怎么办？下面的 `DO` 语句可以做到：

```sas
do n = 0 to 100 by 10;
```

`DO` 循环也可以倒数。例如，后面的语句产生了索引变量值为 10, 8, 6：

```sas
do index = 10 to 2 by -2;
```

当你使用负增量值时，索引值每次迭代都会减少该值。当索引变量小于停止值时，循环停止。

这是另一个例子。有一个关于 `X` 和 `Y` 的方程，并想要从 -10 到 +10 的值的 `Y` 对 `X` 图。再次，迭代 `DO` 循环让这非常简单：

## 程序 8.11：使用迭代 DO 循环绘制方程
