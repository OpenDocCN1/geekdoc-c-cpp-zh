

## 5-54 第 5 章 数据转换

根据需要参考 SAS 文档以了解更多关于生成所需结果的函数。查看 SAS 语言字典中的“按分类划分函数和 CALL 过程”可能会特别有用。

部分 PROC PRINT 输出（共 9 个观测值）

# 高频客户每月统计数据

| Customer_ID | month1 | month2 | month3 | month4 | month5 | month6 | 月度中位数 | 月度最高 | 月度次高值 |
|---|---|---|---|---|---|---|---|---|---|
| 5 | 213.10 | | 478.00 | 525.80 | 394.35 | 191.790 | 394.35 | 525.80 | 478.00 |
| 10 | 188.10 | 414.09 | 2876.9 | 3164.59 | 2373.44 | 169.290 | 1393.77 | 3164.59 | 2876.90 |
| 12 | 135.60 | | 117.6 | 129.36 | 97.02 | 122.040 | 122.04 | 135.60 | 129.36 |
| 34 | 642.50 | | 86.3 | 94.93 | 71.20 | 578.250 | 94.93 | 642.50 | 578.25 |
| 41 | 134.00 | 119.20 | 313.0 | 344.30 | 258.23 | 120.600 | 196.11 | 344.30 | 313.00 |

## 5.5 转换变量类型

- 解释 SAS 用于在数据类型之间转换值的自动转换。
- 显式地转换数据类型之间的值。

![](img/d3bde6e6ab06b1fc622215d982111742_227_0.png)

# 业务场景：转换 HR 数据

创建数据集 orion.convert 时的数据类型和变量名，这些名称在未来的报告和分析中必须进行更改。

部分现有 orion.convert 数据集

| ID | GrossPay | Code | Hired |
| --- | --- | --- | --- |
| ⚠ | | (12) | ⚠ |

部分转换后的 work.hrdata 数据集

| EmplID | GrossPay | Phone | HireDate |
| --- | --- | --- | --- |
| (12) | (12) | ⚠ | (12) |

# 数据转换

数据类型可以通过两种方式转换：

- **自动地**：允许 SAS 为你完成
- **显式地**使用这些函数：

| INPUT | 字符到数值转换 |
| --- | --- |
| ⚠ → f(x) → (12) | |
| PUT | 数值到字符转换 |
| (12) → f(x) → ⚠ | |

# 自动字符到数值转换

当 ID 的字符值被用于算术表达式时，会发生什么？

```
data hrdata;
  keep EmpID;
  set orion.convert;
  EmpID=ID + 11000;
run;
```

# orion.convert

| ID | GrossPay | Code | Mobile | Hired |
|---|---|---|---|---|
| 36 | $5 | 52,000 | 303 | 393-0956 | 04/13/2008 |
| 48 | $6 | 32,000 | 919 | 770-8292 | 08/25/2010 |
| 52 | $8 | 49,000 | 301 | 449-5239 | 06/08/2009 |

# 自动字符到数值转换

部分日志

```
28 data hrdata;
29 keep EmpID;
30 set orion.convert;
31 EmpID=ID + 11000;
32 run;
```

NOTE: 字符值已在此位置转换为数值值：列)。
NOTE: 从数据集 ORION.CONVERT 读取了 3 个观测值。
NOTE: 数据集 WORK.HRDATA 有 3 个变量。

# 自动字符到数值转换

```
proc print data=hrdata noobs;
run;
```

| PROC PRINT 输出 |
| EmpID |
| 36
| 48 |
| 52 |

ID 的自动转换效果很好。

# 自动字符到数值转换

当 GrossPay 的字符值被用于算术表达式时，会发生什么？

```
data hrdata;
  keep GrossPay Bonus;
  set orion.convert;
  Bonus=GrossPay * .10;
run;
```

orion.convert

| ID | GrossPay | Code | Mobile | Hired |
| $5 | $6 | $8 | $10 |
| 36 | 52,000 | 303 | 393-0956 | 04/13/2008 |
| 48 | 32,000 | 919 | 770-8292 | 08/25/2010 |
| 52 | 49,000 | 301 | 449-5239 | 06/08/2009 |

# 自动字符到数值转换

```
proc print data=hrdata noobs;
run;
```

PROC PRINT 输出

| Gross Pay | Bonus |
|---|---|
| 52,000 | . |
| 32,000 | . |
| 49,000 | . |

为什么 GrossPay 的值没有进行自动转换？
![](img/d3bde6e6ab06b1fc622215d982111742_231_0.png)

# 自动字符到数值转换

当字符值被用于数值上下文时，SAS 会自动将其转换为数值值，例如：
- 赋值给数值变量
- 算术运算
- 与数值比较
- 接收数值参数的函数

WHERE 语句和 WHERE= 不执行任何自动转换。

# 自动字符到数值转换

自动转换 informat 会从不符合标准的字符值产生数值缺失值。
![](img/d3bde6e6ab06b1fc622215d982111742_232_0.png)

# 自动字符到数值转换

| 字符值 | 数值值 |
|---|---|
| 52,000 | 52,000 |
| -8.96 | -8.96 |
| 1,243.64 | |

GrossPay 中的值包含逗号，无法通过 informat 转换，因此 GrossPay 被赋值为缺失值。要显式转换 GrossPay 中的值，请使用 INPUT 函数。
![](img/d3bde6e6ab06b1fc622215d982111742_232_1.png)

# INPUT 函数

INPUT 函数返回使用指定 informat 读取源时产生的值。

```
data conversions;
CV1='32000';
CV2='32000';
CV3='032008';
CV4='030508';
Var1=input(CV1,5.);
Var2=input(CV2,comma.);
Var3=input(CV3,date.);
Var4=input(CV4,ddmm.);
run;
```

如果你使用 INPUT 函数创建一个之前未定义的变量，该变量的类型和长度由 informat 定义。

# INPUT 函数

```
proc contents data=conversions;
run;
```

部分 PROC CONTENTS 输出变量和属性字母列表

| | 变量 | 类型 | 长度 |
|---|---|---|---|
| 1 | CV1 | Char | 5 |
| 2 | CV2 | Char | 6 |
| 3 | CV3 | Char | 9 |
| 4 | CV4 | Char | 6 |
| 5 | Var1 | Num | 8 |
| 6 | Var2 | Num | 8 |
| 7 | Var3 | Num | 8 |
| 8 | Var4 | Num |

```
proc print data=conversions;
run;
```

PROC PRINT 输出

| CV1 | CV2 | CV3 | CV4 | Var1 | Var2 | Var3 | Var4 |
|---|---|---|---|---|---|---|---|
| 32000 | 32000 | 032008 | 030508 | | | | |

# 5.11 答案

通过在 DATA 步骤创建 EmpID、Bonus 和 HireDate 变量，并使用 INPUT 函数显式将值转换为数值来继续业务场景。

填充下方表达式中的缺失部分：
EmpID=input(ID,5.)+10000;
Bonus=input(GrossPay,comma.)*10;
HireDate=input(Hired,mmddyy10);

NOTE:
: 读取了 3 个观测值来自 ORION.CONVERT。
: 数据集 WORK.HRDATA 有 3 个变量。

