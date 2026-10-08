
| ID | Sex | Age | ID | Height | Weight |
|---|---|---|---|---|---|
| 1129 | F | 48 | 1129 | 61 | 137 |
| 1274 | F | 50 | 1387 | 64 | 142 |
| 1387 | F | 57 | 2304 | 61 | 102 |
| 2304 | F | 16 | 5438 | 62 | 168 |
| 2486 | F | 63 | 6488 | 64 | 154 |
| 4425 | F | 48 | 9012 | 63 | 157 |
| 4759 | F | 60 | 9125 | 64 | 159 |
| 5438 | F | 42 | | | |
| 6488 | F | 59 | | | |
| 9012 | F | 39 | | | |
| 9125 | F | 56 | | | |

以下程序会创建哪个输出？

```sas
data.merged;
merge health.set1(in=in1) health.set2(in=in2);
by id;
if in1 and in2;
run;
proc print data=work.merged;
run;
```

- a.

| Obs | ID | Sex | Age | Height | Weight |
|---|---|---|---|---|---|
| 1 | 1129 | F | 48 | 61 | 137 |
| 2 | 1274 | F | 50 | | |
| 3 | 1387 | F | 57 | 64 | 142 |
| 4 | 2304 | F | 16 | 61 | 102 |
| 5 | 2486 | F | 63 | | |
| 6 | 4425 | F | 48 | | |
| 7 | 4759 | F | 60 | | |
| 8 | 5438 | F | 42 | 62 | 168 |
| 9 | 6488 | F | 59 | 64 | 154 |
| 10 | 9012 | F | 39 | 63 | 157 |
| 11 | 9125 | F | 56 | 64 | 159 |

- b.

| Obs | ID | Sex | Age | Height | Weight |
|---|---|---|---|---|---|
| 1 | 1129 | F | 48 | 61 | 137 |
| 2 | 1387 | F | 50 | 64 | 142 |
| 3 | 2304 | F | 57 | 61 | 102 |
| 4 | 5438 | F | 16 | 62 | 168 |
| 5 | 6488 | F | 63 | 64 | 154 |
| 6 | 9012 | F | 48 | 63 | 157 |
| 7 | 9125 | F | 60 | 64 | 159 |
| 8 | 5438 | F | 42 | | |
| 9 | 6488 | F | 59 | | |
| 10 | 9012 | F | 39 | | |
| 11 | 9125 | F | 56 | | |

- c.

| Obs | ID | Sex | Age | Height | Weight |
|---|---|---|---|---|---|
| 1 | 1129 | F | 48 | 61 | 137 |
| 2 | 1387 | F | 57 | 64 | 142 |
| 3 | 2304 | F | 16 | 61 | 102 |
| 4 | 5438 | F | 42 | 62 | 168 |
| 5 | 6488 | F | 59 | 64 | 154 |
| 6 | 9012 | F | 39 | 63 | 157 |
| 7 | 9125 | F | 56 | 64 | 159 |

- d. 以上均都不是

- 7. 数据集 `Spring` 和 `Summer` 都包含一个名为 `Blue` 的变量。如何在合并两个数据集时防止 `Blue` 的值被覆盖？

- a. `data ensemble.merged;`
`merge spring(in=blue) summer;`
`run;`

- b. `data ensemble.merged;`
`merge spring(out=blue) summer;`
`run;`

- c. `data ensemble.merged;`
`merge spring(blue=navy) summer;`
`run;`

- d. `data ensemble.merged;`
`merge spring(rename=(blue=navy)) summer;`
`run;`

- 8. 如果提交以下程序来合并 `BloodDonors1` 和 `BloodDonors2`，会发生什么？

```sas
data work.merged;
merge blood.donors1 blood.donors2;
by id;
run;
```

| BloodDonors1 ID Type Units | BloodDonors2 ID Code Units |
|---|---|---|---|---|---|
| 2304 | O | 16 | 6488 | 65 | 27 |
| 1129 | A | 48 | 1129 | 63 | 32 |
| 1129 | A | 50 | 5438 | 62 | 39 |
| 1129 | A | 57 | 2304 | 61 | 45 |

- a. 合并后的数据集包含一些缺失值，因为并不是所有的观测在另一个数据集中都有对应的观测。
- b. 合并后的数据集包含八个观测。
- c. 数据产生错误。
- d. `BloodDonors2` 中的 `Units` 覆盖了 `BloodDonors1` 中的值。

- 9. 如果你通过 `ID` 比较下述 `Company.Staff1` 和 `Company.Staff2`，会有多少条观测？

| Company.Staff1 ID Dept | Company.Staff2 ID Code Units |
|---|---|---|---|---|---|
| 000 | Miguel | | | |
| 111 | Steve | | | |
| 222 | Diana | | | |
| 888 | Monique | | | |

- a. 4
- b. 5
- c. 6
- d. 9

- 10. 如果你通过 `ID` 合并 `Sales.Reps`、`Sales.Close` 和 `Sales.Bonus`，第三个观测的 `Bonus` 值是多少？

| Reps ID Name | Close ID Sale | Bonus Sale |
|---|---|---|---|---|
| 1 | Ray | 28 | 1 | 28 |
| 2 | Kelly | 30 | 2 | 30 |
| 3 | Julio | 40 | 3 | 40 |
| 4 | Richard | 15 | 4 | 15 |
| | | | 5 | 20 |
| | | | 6 | 25 |
| | | | 7 | 35 |

# 理解 SAS 函数

| 函数 | 描述 | 格式 | 示例值 |
|---|---|---|---|
| `MONTH` | 从 SAS 日期值中提取月份。 | `MONTH(date)` | 12 |
| `DAY` | 从 SAS 日期值中提取日期值。 | `DAY(date)` | 5 |

# 目标

在本章中，你将学习：

- 将字符数据转换为数值数据
- 将数值数据转换为字符数据
- 创建 SAS 日期值
- 从 SAS 日期值中提取月份、年份和间隔
- 使用日期、日期时间值和时间间隔进行计算
- 提取、编辑和搜索字符变量的值
- 替换或删除字符字符串中特定单词的所有出现处。

# 理解 SAS 函数

## 概述

SAS 函数是内置例程，能够让你快速、方便地完成许多类型的数据操作。通常来说，函数提供了编程的快捷方式。SAS 函数有许多类型：算术函数、财务函数、字符函数、概率函数等。

表 13.2 SAS 函数分类

| | 概率 (Probability) |
|---|---|
| 数组 (Array) | |
| 按位逻辑运算 (Bitwise Logical Operations) | 分位数 (Quantile) |
| 字符 (Character) | 随机数 (Random Number) |
| 字符串匹配 (Character String Matching) | 样本统计 (Sample Statistics) |
| 日期和时间 (Date and Time) | SAS 输入输出 (SAS File I/O) |
| 动态链接库 (Dynamic Link Library) | 特殊 (Special) |

# 第 13 章 使用 SAS 函数转换数据

| SAS 函数分类 | |
|---|---|
| 外部文件 (External Files) | 州和邮编 (State and ZIP Code) |
| 财务 (Financial) | 三角函数 (Trigonometric) |
| 双曲 (Hyperbolic) | 截断 (Truncation) |
| 宏 (Macro) | 变量控制 (Variable Control) |
| 数学 (Mathematical) | 变量信息 (Variable Information) |
| 多字节字符集 (MultiByte Character Set) | |

| 计算样本统计的 SAS 函数... | |
|---|---|
| 函数 | 语法 | 计算... |
|---|---|---|
| `SUM` | `sum(argument, argument,...)` | 值的和 |
| `MEAN` | `mean(argument, argument,...)` | 非空值的平均值 |
| `MIN` | `min(argument, argument,...)` | 最小值 |
| `MAX` | `max(argument, argument,...)` | 最大值 |
| `VAR` | `var(argument, argument,...)` | 值的方差 |
| `STD` | `std(argument, argument,...)` | 值的标准差 |

# SAS 函数的

使用 SAS 函数，你可以：

- 计算样本统计
- 创建 SAS 日期值
- 将美国邮编转换为州邮政编码
- 对数值进行舍入
- 生成随机数
- 提取字符值的一部分
- 将数据从一种数据类型转换为另一种数据类型。

本章重点关注：

- 转换数据
- 操作 SAS 日期值
- 修改字符变量的值。

然而，请务必探索 SAS 文档中描述许多其他 SAS 函数。

# SAS 函数示例

SAS 函数可以用于 DATA 步编程语句。只要该函数是 SAS 语句的一部分，就可以在任何可以使用 SAS 表达式（expression）的地方指定 SAS 函数。

让我们来看一个简单的 SAS 函数示例。下面的赋值语句使用 `MEAN` 函数计算存储在变量 `Exam1`、`Exam2` 和 `Exam3` 中的三个考试成绩的平均值。

```
AvgScore=mean(exam1,exam2,exam3);
```

当你引用 SAS 函数时，函数返回基于函数参数的值。上面的 `MEAN` 函数包含三个参数：变量 `Exam1`、`Exam2` 和 `Exam3`。该函数计算列为参数的三个变量的平均值。

某些函数需要特定数量的参数，而其他函数可以包含任意数量的参数。某些函数不需要参数。

# SAS 函数的通用格式

# 参数、变量列表、数组

使用 SAS 函数时，指定函数名，后跟括在括号内的函数参数。

通用格式，SAS 函数：

`function-name(argument-1,<argument-n>);`

其中，参数可以是：

- 变量，`mean(x,y,z)`
- 常量，`mean(456,502,612,498)`
- 表达式，`mean(37*2/19/5,mean(22,34,36))`

> 即使函数不需要参数，函数名也必须带有括号（例如，`function-name`）。

当函数包含多个参数时，参数通常用逗号分隔。

```
function-name(argument-1,argument-2,argument-n)
```

然而，对于某些函数，变量列表和数组也可以作为参数使用。

# 第13 章 • 使用 SAS 函数转换数据

# SAS 日志

```
4 data hrd.newtemp;
5 set hrd.temp;
6 Salary=payrate*hours;
7 run;
```

NOTE: 字符值已在以下位置转换为数值值：(行):(列)。

```
6:11
```

NOTE: 数据集 `HRD.NEWTEMP` 包含 40 观测观测值和 19 个变量。

NOTE: `data` 语句花费了 0.78 秒。

# 发生自动转换的情况

当字符值满足以下条件时，会发生字符到数值的自动转换

- 赋值给之前定义的数值变量，例如数值变量 `Rate=payrate;`；
- 用于算术运算，如 `Salary=payrate*hours;`；
- 使用比较运算符与数值值进行比较，如 `if payrate>=rate;`；
- 在需要数值参数的函数中指定。

`NewRate=sum(payrate, raise);`

自动转换

- 使用 `w.` inform，其中 `w` 是不符合标准数值表示法的字符值的宽度（带有可选的小数点、前导符号或科学计数法的数字）。
- 从任何不符合标准数值表示法的字符值产生数值缺失值。

表 13.3 字符变量的自动转换

| 字符值 | 自动转换 | 数值 |
|---|---|---|
| 12.47 | → | 12.47 |
| -8.96 | → | -8.96 |
| 1.243E1 | → | 12.43 |
| 1,742.64 | → | . |

# WHERE 表达式的限制

`WHERE` 语句在比较时不执行自动转换。下面的简单程序演示了当 `WHERE` 表达式遇到错误的数据类型时发生的情况。变量 `Number` 包含一个数值，变量 `Character` 包含一个字符值，但两个 `WHERE` 语句指定了错误的数据类型。

```
data work.convest;
Number=4;
Character='4';
run;
proc data=work.convest;
where character=4;
run;
proc data=work.convest;
where number='4';
run;
```

这种字符变量与数值变量的不匹配阻止了程序处理 `WHERE` 语句。不会执行自动转换。相反，程序会停止，并将错误信息写入 SAS 日志。

# SAS 日志

| 1 | `data work.convest;` |
| 2 | `Number=4;` |
| 3 | `Character='4';` |
| 4 | `run;` |
| NOTE: 数据集 Work.ConvTest 包含 1 个观测观测值和 2 个变量。 |
| 5 | `proc data=work.convest;` |
| 6 | `where character=4;` |
| 7 | `run;` |
| ERROR: Where 子句运算符需要兼容的变量。 |
| NOTE: SAS 系统因错误停止了此步的处理。 |
| 8 | `proc data=work.convest;` |
| 9 | `where number='4';` |
| 10 | `run;` |
| ERROR: Where 子句运算符需要兼容的变量。 |
| NOTE: SAS 系统因错误停止了此步的处理。 |

# 显式字符转数值转换

# INPUT 函数

为了避免我们已经过的问题，使用 `INPUT` 函数将字符数据值转换为数值值。要学习如何使用此函数，让我们检查 `Hrd.Temp` 所需的某种数据集修改。如前所述，你需要通过将字符变量 `PayRate` 乘以数值 `Hours` 来计算员工薪资。

| 城市 | 州 | 邮编 | 电话 | 开始日期 | 结束日期 | PayRate | 天数 | 小时 |
|---|---|---|---|---|---|---|---|---|
| CARY | NC | 27513 | 6224549 | 14567 | 14621 | 10 | 11 | 88 |
| CARY | NC | 27513 | 6223251 | 14524 | 14565 | 8 | 25 | 200 |
| CHAPEL HILL | NC | 27514 | 9974749 | 14570 | 14608 | 40 | 26 | 208 |
| RALEIGH | NC | 27612 | 6970450 | 14516 | 14527 | 15 | 10 | 80 |

为了计算薪资，你编写了以下 DATA step。它创建了一个新数据集 `Hrd.Newtemp`，包含原始数据加上新变量 `Salary`。

```
data hrd.newtemp;
  set hrd.temp;
  Salary=payrate*hours;
```

然而，现在提交此 DATA 步会导致自动的字符到数值转换，因为字符变量 `PayRate` 被用于数值上下文中。你可以使用 `INPUT` 函数显式地将 `PayRate` 的字符值转换为数值。

`INPUT` 函数的一般形式：**`INPUT(source,format)`**，其中

- `source` 表示要转换为数值的字符变量、常量或表达式
- 必须还指定一个数值格式符（informat），如例所示：

```
input(payrate,2.)
```

在选择格式符时，务必选择一个能够读取值格式的数值格式符。

表 13.4 字符值及关联格式符

| 字符值 | 格式符 (Informat) |
|---|---|
| 115233 | 7. |
| 2,115,233 | COMMA9. |

示例

这里有一个 `INPUT` 函数的示例：
