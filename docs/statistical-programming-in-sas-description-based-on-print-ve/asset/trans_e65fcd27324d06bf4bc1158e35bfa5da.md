

+   1. 统计每个个体的转换次数。
+   2. 记录每个个体在项目中的总时间。
+   3. 记录个体在项目中的首次入组时长。

Display 9.6A 中的代码解决了这些目标。

## Display 9.6A 处理个体的多次观测

```
data test;
input id xstart xstop;
datalines;
1 15 25
2 10 12
2 18 22
3 6 12
3 14 15
3 17 23
;
run;

* make sure that data are sorted by ID and XSTART;
proc sort data=test;
  by id xstart;
run;

proc print data=test;
run;

data test2; set test; by id;          **** Comment 1;
  array start{9} start1-start9;       * (explained on next page);
  array stop{9} stop1-stop9;
  array times{9} times1-times9;

  retain count 0;                     **** Comment 2;
  retain start1-start9 stop1-stop9 times1-times9;

* initialize count and arrays with new ID;
if FIRST.id then do;                 **** Comment 3;
  count = 0;
  do ii=1 to 9;
    start{ii} = .;
    stop{ii} = .;
    times{ii} = .;
  end;
end;

count = count + 1;                   **** Comment 4;
start{count} = xstart;
stop{count} = xstop;
times{count} = xstop - xstart;
```

## Display 9.6A (continued)

```
if LAST.id=1 then do;            **** Comment 5;
    first_time = times(1);
    total_time = sum(of times1-times9);
    output;  * output results if last obs for ID;
end;

keep id count first_time total_time;
run;

proc print data=test2;
run;
```

处理观测后得到以下输出：

| Obs | id | count | first time | total_time |
|---|---|---|---|---|
| 1 | 1 | 1 | 10 | 10 |
| 2 | 2 | 2 | 2 | 6 |
| 3 | 3 | 3 | 6 | 13 |

### **** Comment 1

原始数据集 test 的内容通过变量 id 复制到新的数据集 test2 中。这创建了两个内部变量 FIRST.id 和 LAST.id。FIRST.ID=1 如果记录对应于特定 ID 的第一条记录。FIRST.ID=0 用于所有其他记录。LAST.ID=1 如果记录对应于特定 ID 的最后一条记录。LAST.ID=0 用于所有其他记录。对于第一个个体（id=1）。FIRST.ID=1 且 LAST.ID=1 因为该个体只有一条记录。对于第三个个体（id=3）。FIRST.ID=1 且 LAST.ID=0 用于数据行 3 6 12。FIRST.ID=0 且 LAST.ID=0 用于数据行 3 14 15。且 FIRST.ID=0 且 LAST.ID=1 用于数据行 3 17 23。

### **** Comment 2

以 retain 开头的两行定义了个体入组次数的计数器，以及入组（start）、退出（stop）和入组时间（times）数组元素的定义。RETAIN 语句确保这些值在处理同一个体的多条数据行时不会被重置为缺失。数组最多可容纳九次独立的入组时间。

### **** Comment 3

当为个体的第一条记录时，计数器和数组元素会被初始化。数组元素最初被设为缺失，因为预计大多数个体的入组次数少于最大值。

### **** Comment 4

数组被当前记录的信息填充。入组时间被计算。

### **** Comment 5

当为个体的最后一条记录时，个体的转换次数会被计数。总时间会被累积（缺失值会被 **sum** 函数忽略）。首次停留的时长被定义。并且，结果会被输出。

一种替代且更简洁的编码方式涉及对 RETAIN 语句的更简洁使用。Display 9.6B 中的代码产生相同的结果。DATA 步定义了 **test2** 数据集。你不需要知道每个受试者的最大记录数。你不需要定义数组。Kudos 归功于 Kathy Roggenkamp 建议了这种替代代码。

## Display 9.6B 不使用数组处理个体的多次观测

```
```sas
data test;
input id xstart xstop;
datalines;
1 15 25
2 10 12
2 18 22
3 6 12
3 14 15
3 17 23
;
run;

proc print data=test;
run;

*** make sure data are sorted by ID and XSTART variables;
proc sort data=test;
    by id xstart;
run;

data test2;
    set test;
        by id;

    retain count total_time first_time;

    if first.id then do;
        count=0;
        total_time=0;
        first_time=0;
    end;
```
```

## Display 9.6B (continued)

```
count=count+1;
total_time=total_time + (xstop-xstart);
if first.id then first_time=xstop-xstart;
if last.id then output;
keep id count total_time first_time;
run;
proc print data=test2;
run;
```

## 9.4 案例研究 2：两总体相等性的随机化检验

随机化检验（Edgington 1995 和 Good 2001）也可以用于获得 p 值。假设你想检验两个正态分布的相等性，假设每个分布具有相同的未知方差。在这种情况下，通常使用合并方差 t 检验。如果你从第一个（第二个）总体中获得 n1（n2）个观测值，则检验统计量可以写成如下形式：

t^* = \frac{\bar{Y}_1 - \bar{Y}_2}{s_p \sqrt{\frac{1}{n_1} + \frac{1}{n_2}}}

合并方差估计表示如下：

s_p^2 = \frac{(n_1 - 1)s_1^2 + (n_2 - 1)s_2^2}{n_1 + n_2 - 2}

检验统计量与自由度为 n1 + n2 - 2 的 t 分布进行比较。

随机化检验提供了一种获得 p 值的替代方法。如果两个分布相同，则组别归属的标签（即组 1 与组 2）可以被视为随机分配给每个观测值。在两组随机化检验中，考虑所有 \binom{n1 + n2}{n1} 种可能的标签分配给观测值。对于每种分配，你计算检验统计量的值并将其与

观测到的检验统计量值进行比较。来自随机化检验的检验统计量超过（或至少与）观测到的检验统计量值相同的比例即为随机化 p 值。作为完全随机化的替代，你可以从（n₁ + n₂ choose n₁）种可能的标签分配中抽取样本。你可以从该样本中计算 p 值。完成此任务的代码在以下示例中显示。

数据从外部永久 SAS 库的成员 NITROFEN 中读取。这些数据是 Ceriodaphnia dubia（水蚤）暴露于不同浓度硝基酚后产生的幼体数量。¹ 控制条件和 160 µg 每升条件被选用于分析。

```
libname class 'C:\Users\baileraj.IT\Desktop';

data test; set class.nitrofen;
    if conc 0 | conc=160;
run;

proc print data=test;
    title "NITROFEN: print of (0, 160) concentrations";
    var conc total;
run;
```

| NITROFEN: print of (0, 160) concentrations |
| Obs | conc | total |
| 1 | 0 | 27 |
| 2 | 0 | 32 |
| 3 | 0 | 34 |
| 4 | 0 | 33 |
| 5 | 0 | 36 |
| 6 | 0 | 34 |
| 7 | 0 | 33 |
| 8 | 0 | 30 |
| 9 | 0 | 24 |
| 10 | 0 | 31 |
| 11 | 160 | 29 |
| 12 | 160 | 29 |
| 13 | 160 | 23 |
| 14 | 160 | 27 |
| 15 | 160 | 30 |
| 16 | 160 | 31 |
| 17 | 160 | 30 |
| 18 | 160 | 26 |
| 19 | 160 | 29 |
| 20 | 160 | 29 |

¹ Nitrofen 数据集来自 Bailer, A. John., and James T. Oris. 1994. “Assessing Toxicity of Pollutants in Aquatic Systems.” Chapter 2 in Case Studies in Biometry. Nicholas Lange, Louise Ryan, Lynne Billard, David Brillinger, Loveday Conquest, Joel Greenhouse, eds. New Jersey: John Wiley & Sons, Inc. Reprinted with permission of John Wiley & Sons, Inc.

比较对照条件和 160 µg 每升条件下平均响应的 t 检验结果被检查。从 Display 9.7 中的代码和结果可以看出，两组 t 检验的结果 p 值为 0.035（假设方差相等）。

```
proc ttest;
title "NITROFEN:  t-test of (0, 160) concentrations";
class conc;
var total;
run;
```

## Display 9.7 PROC TTEST 的输出

NITROFEN:  t-test of (0, 160) concentrations
The TTEST Procedure

Statistics
conc  N  Lower CL Mean  Upper CL Mean  Lower CL SD  Upper CL SD  Std Err
0     10  28.827  31.4  33.973  2.4737  3.5963  6.5654  1.137
160   10  26.612  28.3  29.988  1.6229  2.3594  4.3073  0.7461
Diff (1-2) 0.2424 3.1 5.9576 2.2981 3.0414 4.4777 1.361

T-Tests
Variable  Method  Variances  DF  t Value  Pr > |t|
total     Pooled   Equal     18   2.28     0.0341
total     Satterthwaite Unequal 15.5 2.28     0.035

Equality of Variances
Variable  Method  Num DF  Den DF  F Value  Pr > F
total     Folded F 9       9       2.32     0.12

构建了一个与之前 t 检验类似的这些分布相等性的随机化检验。在此随机化检验中，检验统计量（本质上是 t 检验的分子）是关注的重点（即，d = Ȳ₁ - Ȳ₂）。PROC PLAN 生成 1 到 20 的索引排列的集合。排列集中前 10 个索引对应的 10 个观测值被分配到特定排列的组 1。剩余的观测值被分配到组 2。这些排列被读入 SAS 数据集以进行进一步处理。PROC TRANSPOSE 将每组排列的数据放置到单行上。原始测试数据集有 20 (=n₁+n₂) 行观测值，并且包含 conc 和 total 变量的列。

