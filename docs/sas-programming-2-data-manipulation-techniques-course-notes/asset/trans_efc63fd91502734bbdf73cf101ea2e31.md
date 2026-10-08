

# 执行重复计算

```sas
data charity;
set orion.employee_donations;
keep employee id qtr1-qtr4;
Qtr1=Qtr1*1.25;
Qtr2=Qtr2*1.25;
Qtr3=Qtr3*1.25;
Qtr4=Qtr4*1.25;
run;
proc print data=charity noobs;
run;
```

# 部分 PROC PRINT 输出

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |
|---|---|---|---|---|
| 120267 | 18.75 | 18.75 | 18.75 | 31.25 |
| 120269 | 25.00 | 25.00 | 25.00 | 25.00 |
| 120270 | 25.00 | 12.50 | 6.25 | - |

![](img/d3bde6e6ab06b1fc622215d982111742_309_0.png)

# 执行重复计算

这四个计算无法用 DO 循环内部的单个计算代替，因为它们是不相同的。

```sas
data charity;
set orion.employee_donations;
keep employee id qtr1-qtr4;
Qtr1=Qtr1*1.25;
Qtr2=Qtr2*1.25;
Qtr3=Qtr3*1.25;
Qtr4=Qtr4*1.25;
do i=1 to 4;
?
end;
run;
proc print data=charity noobs;
run;
```

可以使用 SAS 数组（Array）来简化这段代码。

# 使用数组简化重复计算

数组提供了访问 PDV（程序数据变量）中值的另一种方式，简化了重复计算。

```sas
data charity;
  set orion.employee_donations;
  keep employee qtr1-qtr4;
 Qtr1=qtr1*1.25;
 Qtr2=qtr2*1.25;
 Qtr3=qtr3*1.25;
 Qtr4=qtr4*1.25;
run;
proc print data=charity noobs;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_310_0.png)

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |

# 什么是 SAS 数组？

SAS 数组

- - 是按特定顺序排列的 SAS 变量的临时分组
- 由数组名称标识
- 必须包含全数值型或全字符变量
- 仅存在于当前 DATA 步执行期间
- 它**不是**一个变量。

# 为什么要使用 SAS 数组？

创建一个名为 Contrib 的数组，并使用它来访问四个数值变量 Qtr1 – Qtr4。

![](img/d3bde6e6ab06b1fc622215d982111742_311_0.png)

| PDV Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |
|---|---|---|---|---|

SAS 数组与许多其他编程语言中的数组不同。在 SAS 中，数组不是数据结构。它只是临时标识一组变量的方便方法。

# 数组元素

数组中的每个值都称为元素（element）。

![](img/d3bde6e6ab06b1fc622215d982111742_311_1.png)

| PDV Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |
|---|---|---|---|---|
| 第一个元素 | 第二个元素 | 第三个元素 | 第四个元素 |

# 引用数组元素

每个元素都通过下标（subscript）标识，下标代表该元素在数组中的位置。当你使用数组引用时，相应的值将替换该引用。

![](img/d3bde6e6ab06b1fc622215d982111742_312_0.png)

| PDV Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |
|---|---|---|---|---|
| | Contrib{1} | Contrib{2} | Contrib{3} | Contrib{4} |

# 定义数组

ARRAY 语句是一个编译语句，用于定义数组中的元素。

```sas
ARRAY array-name {subscript} $< <length> <array-elements>;
array Contrib{4} Qtr1 Qtr2 Qtr3 Qtr4;
```

| PDV Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |
|---|---|---|---|---|
| | Contrib{1} | Contrib{2} | Contrib{3} | Contrib{4} |

array-name 指定数组的名称。

{subscript} 使用星号（*）、数字、用逗号分隔的数字（用于多维数组）、数字范围或表达式来描述数组中元素的数量和排列方式。下标括在大括号 `{}` 中。也允许方括号 `[]` 和圆括号 `()`。

$ 表示数组中的元素是字符元素。如果数组中的元素之前已定义为字符元素，则不需要美元符号。

length 指定数组中未赋值长度的元素的长度。

array-elements 命名构成数组的元素。数组元素可以任意顺序列出。

- - 数组引用不能用于 LABEL、FORMAT、DROP、KEEP 或 LENGTH 等编译时语句。

如果你将函数名作为数组名，SAS 在 DATA 步期间会将括号内的引用视为数组引用而非函数引用。

- 四个变量 Qtr1、Qtr2、Qtr3 和 Qtr4 现在可以通过数组名 Contrib 配合适当的下标进行引用。

![](img/d3bde6e6ab06b1fc622215d982111742_313_0.png)

- 你可以使用特殊名称引用在同一 DATA 步中定义的变量。CHARACTER 列表引用字符，NUMERIC 列表引用数值。避免使用 ALL 特殊名称，因为数组中的元素必须全字符或全数值。

# 定义数组

数组的元素不需要满足：
- 相似的名称
- 相关的名称
- 顺序存储

```sas
array Amt(*) Q1 Q2 Q3 Qtr4;
PDV
ID Q1 Q2 Q3 Qtr4
Amt{1} Amt{2} Amt{3} Amt{4}
```

# 7.07 问

错误的原因是什么？

```sas
data charity (keep=Employee ID Qtr1-Qtr4);
set orion.employee_donations;
array Contrib(3) Qtr1-Qtr4;
array Contrib(5) qtr;/* additional SAS statements */
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_314_0.png)

# 使用 DO 循环处理数组

```sas
data charity;
  set orion.employee_donations;
  keep Qtr1-Qtr4;
  array Contrib{4} Qtr1-Qtr4;
  do i=1 to 4;
    Contrib{i}=Contrib{i}*1.25;
  end;
run;
```

为了引用元素，索引变量通常用下标：array-name{index-variable}。要处理数组的特定元素，请指定迭代范围。默认情况下，SAS 将索引变量包含在输出集中。使用 DROP 或 KEEP 选项防止索引变量写入输出集。

# DO 循环第一次迭代

```sas
data charity;
  set orion.employee_donations;
  keep Qtr1-Qtr4;
  array Contrib{4} Qtr1-Qtr4;
  do i=1 to 4;
    Contrib{i}=Contrib{i}*1.25;
  end;
run;
```

# DO 循环第二次迭代

```sas
data charity;
  set orion.employee_donations;
  keep Qtr1-Qtr4;
  array Contrib{4} Qtr1-Qtr4;
  do i=1 to 4;
    Contrib{i}=Contrib{i}*1.25;
  end;
run;
```

# DO 循环第三次迭代

```sas
data charity;
  set orion.employee_donations;
  keep Qtr1-Qtr4;
  array Contrib{4} Qtr1-Qtr4;
  do i=1 to 4;
    Contrib{i}=Contrib{i}*1.25;
  end;
run;
```

# DO 循环第四次迭代

```sas
data charity;
  set orion.employee_donations;
  keep Qtr1-Qtr4;
  array Contrib{4} Qtr1-Qtr4;
  do i=1 to 4;
    Contrib{i}=Contrib{i}*1.25;
    when i=4
    Contrib{4}=Contrib{4}*1.25;
  end;
```

# 输出：使用 Do 循环处理数组

```sas
proc print data=charity noobs;
run;
```

部分 PROC PRINT 输出

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |
|---|---|---|---|---|
| 120267 | 18.75 | 18.75 | 18.75 | 31.25 |
| 120269 | 25.00 | 25.00 | 25.00 | 25.00 |
| 120270 | 25.00 | 12.50 | 6.25 | - |

# 练习

如果你自上次练习以来重启了 SAS 会话，请打开并提交文件夹中的 libname.sas 程序。

# 等级 1

5. 使用数组进行重复计算

上半年的每月订单数据存储在 orion.orders_midyear 数据集中。Orion Star 销售经理考虑明年降价10%。经理想看看这种折扣如何影响今年的收入。

部分 orion.orders_midyear

| Obs | Customer_ID | Month1 | Month2 | Month3 | Month4 | Month5 | Month6 |
|---|---|---|---|---|---|---|
| 1 | | 213.10 | | 478.0 | 525.80 | 394.35 | 191.79 |
| 2 | 10 | 188.10 | 414.09 | 2876.9 | 3164.59 | 2373.44 | 169.29 |
| 3 | 11 | 78.20 | | | | 70.38 |
| 4 | 12 | | 135.60 | | 117.6 | 129.36 | 122.04 |
| 5 | 18 | | | | 29.4 | 32.34 | 24.26 |
| 6 | 24 | 93.00 | 265.80 | | | | 83.70 |
| 7 | 27 | 310.70 | 782.90 | | | | 279.63 |
| 8 | 31 | 1484.30 | 293.30 | | | | 1335.87 |
| 9 | 34 | 642.50 | | | 86.3 | 94.93 | 71.20 | 578.25 |
| 10 | 41 | | 134.00 | 119.20 | 313.0 | 344.30 | 258.23 | 120.60 |
| 11 | 45 | 443.88 | 216.20 | 40.2 | 44.22 | 33.17 | 399.49 |
| 12 | 49 | 24.80 | | | 111.72 | 122.89 | 92.17 | 115.94 |
| 18 | | | | | 27.93 | 30.72 | 23.04 | |

部分 PROC PRINT 输出（共24个观测值）

a. 创建一个折扣数据集以计算5%的折扣。创建一个数组 Mon 来调整 Month1 到 Month6。使用 DO 循环调整每个客户的每月数据。应用5%的折扣。
b. 打印结果数据集并验证你的结果。添加适当的标题。对每月销售金额使用 DOLLAR 格式。

