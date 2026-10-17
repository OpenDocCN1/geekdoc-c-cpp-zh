
```
data triangular;
call streaminit(34567);
do inum = 1 to 1400;
    mynum = RAND('Triangle', 0.70);
        * h=0.70 is a parameter of the triag. distn.;
    output;
end;
run;
ods rtf bodytitle file="C:\Users\baileraj.IT\Desktop\Display-8-60.rtf";
ods graphics on;
proc sgplot data=triangular;
histogram mynum;
run;
ods graphics off;
ods rtf close;
```

显示 8.60 中显示了 1400 个三角偏差的随机样本的直方图。

### 显示 8.60 1400 个随机三角偏差的直方图

![](img/26474180ee55914c13fb9156a7678157_336_0.png)

另一个在入门统计学中常见的（也许是痛苦地常见）例子是掷两颗骰子。在显示 8.61 中，模拟了 6000 次掷两颗骰子。当骰子面上点数之和大于等于 7 时，记录该值。随机掷骰是通过生成 1 到 6 的整数实现的。每次掷骰的概率为 1/6，使用 `RAND('Table',...)`，其中指定 `p(1)=p(2)=...=p(5)=1/6`。掷出 6 的概率从其他五个概率的指定中隐含得出（即，`p(6)=1-[p(1)+...+p(5)]`）。

### 显示 8.61 模拟掷一对骰子

```
data diceroll;    * rolling two six-sided balanced dice;
    call streaminit(34567);
    do inum = 1 to 6000;
        die1 = RAND('Table', 1/6, 1/6, 1/6, 1/6, 1/6);
        die2 = RAND('Table', 1/6, 1/6, 1/6, 1/6, 1/6);
        sum7plus = (die1+die2)>=7;
        output;
    end;
run;

ods rtf bodytitle file="C:\Users\baileraj.IT\Desktop\Display-8-62.rtf";
proc freq data=diceroll;
    table die1 / nocum testf=(1000,1000,1000,1000,1000,1000);
    table sum7plus;
run;
ods rtf close;
```

显示 8.62 包含每个骰子面的相对频率以及 X² 拟合优度检验的结果。这些结果表明数据与 `die1` 为公平一致（X²=0.6020, df=5, p-value=0.9879）。

### 显示 8.62 6000 次第一次骰子掷骰结果的频率

| die1 | Frequency | Test Frequency | Percent |
|---|---|---|---|
| 1 | 998 | 1000 | 16.63 |
| 2 | 985 | 1000 | 16.42 |
| 3 | 998 | 1000 | 16.63 |
| 4 | 1002 | 1000 | 16.70 |
| 5 | 998 | 1000 | 16.63 |
| 6 | 1019 | 1000 | 16.98 |

虽然你知道独立掷两颗平衡六面骰子时，骰子面上点数之和大于等于 7 的概率应为 58.33%（21/36 次掷骰会产生此事件），但你在 6000 次模拟中观察到该事件的比例为 58.60%。

其他值得探索的例程和函数包括用于生成参数排列的 `RANPERM` 例程。此例程可用于构建随机化和排列检验。即将上演的预告：你能使用 `RANPERM` 例程来重新编码第 9 章中的随机化检验示例吗？

## 8.12 总结

本章是从使用内置过程到构建自己的定制解决方案的过渡。格式化和表示数据值在开始时进行了讨论。随后讨论了使用公式和重新编码变量。伪编码和模块用于描述编写用户定义程序。随后在一系列案例研究中充实了这些程序。本章结束时讨论了与概率分布相关的 SAS 函数。

## 8.13 参考文献

Bilenas, Jonas. 2005. *The Power of PROC FORMAT*. Cary, NC: SAS Institute Inc.

Cody, Ron, and Ray Pass. 1995. *SAS Programming by Example*. Cary, NC: SAS Institute Inc.

Efron, Bradley, and Robert J. Tibshirani. 1994. *An Introduction to the Bootstrap*. New York, NY: Chapman & Hall/CRC.

Miller, Rupert G. 1986. *Beyond ANOVA: Basics of Applied Statistics*. New York, NY: John Wiley & Sons Inc.

Wicklin, Rick. 2008. “SAS Stat Studio: A Programming Environment for High-End Data Analysts.” *Proceedings of the SAS Global Forum 2008 Conference*. Cary, NC: SAS Institute Inc. Available at http://www2.sas.com/proceedings/forum2008/362-2008.pdf.

## 8.14 练习

- 1. 进行蒙特卡洛模拟以检验泊松分布均值的 *t* 基置信区间的行为。泊松随机变量可用于建模无界计数（0, 1, 2, 3, …）。如果 Y ~ Poisson(μ)，则 E(Y)=V(Y)=μ。比较两种置信区间程序在覆盖率和长度方面的表现。

  - a. $\bar{Y} \pm t_{1-\alpha/2,n-1}\dfrac{s_y}{\sqrt{n}}$

  - b. $\left\{\bar{X} \pm t_{1-\alpha/2,n-1}\dfrac{s_x}{\sqrt{n}}\right\}^2$ where $X_i=\sqrt{Y_i}$

  - 选择至少三个 μ 值（例如，2、10 和 25）和三个 n 值（例如，n=15、30 和 50）进行此说明。

- 2. 构建 FITNESS 数据集中 Display 8.49 中使用的均值 AGE 变量的 95% BCa 自助置信区间。

- 3. 构建 FITNESS 数据集中 Display 8.49 中使用的 AGE 变量方差的 95% 置信区间。使用基于百分位数的自助方法获得该区间。

- 4. 使用蒙特卡洛积分估计 π。提供此估计的适当误差界限。

## DATA 步编程

![](img/26474180ee55914c13fb9156a7678157_340_0.png)

- 9.1 用于值集合的存储箱 ......................................................... 326

- 9.2 案例研究 1：空间随机性检验的蒙特卡洛 p 值 ......................................................... 332

- 9.3 跨观测记住变量值 ........................ 336

- 9.4 案例研究 2：两总体相等性的随机化检验 ......................................................... 340

- 9.5 总结 ......................................................... 346

- 9.6 参考文献 ......................................................... 346

- 9.7 练习 ......................................................... 347

第 8 章介绍了基本编程思想（例如，模块化编程和伪编码）。此外，它还提供了使用 DO-END 语句对重复执行编程步骤块进行编码的方法。还讨论了使用 IF-THEN 语句有条件地执行程序语句的方法。

在本章中，您将了解到一种可在 DATA 步中使用的数据结构（数组）。数组可以存储一组相似类型的元素。提供了涉及这些数据结构的各种操作。一系列示例说明了数组的强大功能和灵活性。默认情况下，SAS 逐条处理数据，忘记前一条记录中变量的值。（抱歉拟人化了 SAS。我知道它实际上并没有忘记值，但这是一个有用的形象。）然而，保留值以便处理未来的记录通常很重要。`RETAIN` 语句解决了这一需求。对 ARRAY 和 RETAIN 的描述和基本说明辅以案例研究，强调了它们的强大功能。

### 9.1 用于存储值集合的存储箱

数组是一种临时数据结构，包含一组变量或值。数组常用于存储变量列表。可以将数组概念化为一个被划分为许多隔间的盒子，每个隔间包含信息。定义数组中变量及其值的方式有很多。那么，如何告诉 SAS 您想要设置一个用于存储值的数组呢？以下是基本语法：

```
ARRAY arrayname{number of array elements} variable-list;
```

（符号 { }、[ ] 和 ( ) 都可以在数组定义中使用。）如果您想直接定义变量的值，可以在变量列表之后进行定义。

#### 9.1.1 在变量列表中定义值

在此示例中，一个数组（`tempF`）用四个华氏温度初始化。该数组被循环遍历一个摄氏温度数组（`tempC`），以计算对应于华氏值的数值。

##### Display 9.1 使用数组转换温度尺度

```
data temps;
  array tempF(4) tempF1-tempF4 (32,50,68,86);
  array tempC(4) tempC1-tempC4;

  do itemp = 1 to 4;
    tempC(itemp) = 5/9*(tempF(itemp)-32);
  end;
  drop itemp;
end;
run;

proc print data=temps;
run;
```

Display 9.1 的打印输出包括以下输出行：

| Obs | temp F1 | temp F2 | temp F3 | temp F4 | temp C1 | temp C2 | temp C3 | temp C4 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 32 | 50 | 68 | 86 | 0 | 10 | 20 | 30 |

#### 9.1.2 在变量列表中输入值

您可以从数据行或外部文件中读取变量值到数组中。假设每位养老院居民在连续七个季度中能够进行的日常生活活动（ADL）数量被测量。很自然地将每位居民的数据视为分组。在下图中，一个七元素数组包含一位居民的数据，其前两个 ADL 测量值为 6，其后三个 ADL 测量值为 5，其后一个 ADL 测量值为 4，最后一个 ADL 测量值为 3。

| ADL[1] | ADL[2] | ADL[3] | ADL[4] | ADL[5] | ADL[6] | ADL[7] |
| --- | --- | --- | --- | --- | --- | --- |
| 6 | 6 | 5 | 5 | 5 | 4 | 3 |

对于此示例，以下代码可用于将这些数据读入数组：

```
data D1;
ARRAY ADL{7} ADL1-ADL7;
    input ADL1-ADL7;
    datalines;
6 6 5 5 5 4 3
;
run;
```

在此代码段中，数组名为 `ADL`，元素名为 `ADL1` 至 `ADL7`。通过在数组名 `ADL` 声明后使用 `{7}`，显式声明数组的大小为 7 个元素。您可以通过使用星号，如 `{ * }`，来定义数组的大小，而无需计算数组中的元素数。这在下一段代码中进行了说明：

```
data D2;
ARRAY ADL{*} ADL1-ADL7;
    input ADL1-ADL7;
    datalines;
6 6 5 5 5 4 3
;
run;
```

此数组中的变量定义为 `ADL1` 至 `ADL7`。您可以基于一组变量名定义数组。例如：

```
data D3;
ARRAY ADL{*} t1 t2 t3 t4 t5 time6 time_7;
input t1 t2 t3 t4 t5 time6 time_7;
datalines;
6 6 5 5 5 4 3
;
run;
```

数组常用于处理变量列表。也许数组最常见的用途是将缺失值代码重新分配为 SAS 内部表示。要处理数组的所有元素，请使用带 DO-END 语句对和索引的循环结构。下一节中的示例说明了这种策略。

#### 9.1.3 重新编码数值变量的缺失值代码 “.”

数据集通常继承自数据收集者，或来自对其他目的的初级数据收集后的二级数据分析的某个部分。假设 -999 在 ADL 研究中用作缺失值代码。您希望在进行进一步分析之前将所有 -999 的出现替换为 .。以下代码通过循环遍历数组来实现这一点。

##### Display 9.2 重新编码数值变量中的缺失值

```
data D4;
ARRAY ADL{*} t1 t2 t3 t4 t5 time6 time_7;
input t1 t2 t3 t4 t5 time6 time_7;
DO ielement = 1 to dim(ADL);
    if ADL{ielement}=-999 then ADL{ielement}=.;
END;
datalines;
6 6 5 5 5 4 3
7 -999 4 4 3 -999 2
;
run;
proc print data=D4;
title "Recoding missing values using arrays and DO loop";
run;
```

Display 9.2 的打印输出包括以下输出行：

```
Recoding missing values using arrays and DO loop
Obs    t1    t2    t3    t4    t5    time6    time_7    ielement
1      6     6     5     5     5     4        3         8
2      7     .     4     4     3     .        2         8
```

请注意输出数据集中的索引变量 `ielement`。该索引的值为 8，超出循环范围，这是每次观察循环停止时的情况。您可以通过使用 DROP 语句从输出数据集中消除索引变量。（例如，在前面的代码中，在 datalines 语句之前插入 drop ielement 语句）。数组中包含的变量列表可以隐式定义为所有数值变量、所有字符变量或所有变量，分别使用 `_NUMERIC_`、`_CHARACTER_` 和 `_ALL_` 选项。以下示例说明了这种构造的强大功能。

#### 9.1.4 重新编码所有数值和字符变量的缺失值

假设 ADL 数据集包含居民姓名和性别的字符变量以及随时间记录的七个 ADL 测量值。以下程序将所有数值变量分组到名为 `num_array` 的数组中。它将所有字符变量分组到名为 `char_array` 的数组中。程序循环遍历每个数组，将所有缺失值更改为数值变量的 .，并将所有缺失值更改为字符变量的空白。`dim` 函数确定每个数组中元素的数量以供循环使用。该程序显示在 Display 9.3 中。

##### Display 9.3 重新编码数值和字符变量中的缺失值

```
data D5;
    input name $ sex $ t1 t2 t3 t4 t5 time6 time_7;

ARRAY num_array{*} _NUMERIC_;
ARRAY char_array{*} _CHARACTER_;

/* recode the numeric variables */
DO inum = 1 to dim(num_array);
    if num_array{inum}==-999 then num_array{inum}=.;
END;

/* recode the character variables */
Do ichar = 1 to dim(char_array);
```

##### Display 9.3 (continued)

```
if char_array{ichar}="-999" then char_array{ichar}=" ";
END;

drop inum ichar;
datalines;
MrSmith -999 6   6 5 5 5    4 3
-999      F 7 -999 4 4 3 -999 2
;
run;

proc print data=D5;
title "Recoding missing values using arrays and DO loop";
run;
```

Display 9.3 的打印输出包括以下输出行：

```
Recoding missing values using arrays and DO loop
Obs    name    sex    t1    t2    t3    t4    t5    time6    time_7
1      MrSmith         6     6     5     5     5     4        3
2                   F     7     .     4     4     3     .        2
```

#### 9.1.5 从单条记录创建多个观测值
