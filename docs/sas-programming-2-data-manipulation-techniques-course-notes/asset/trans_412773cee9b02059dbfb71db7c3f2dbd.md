

# 2-18 第 2 章 控制输入和输出

| | | | | | | |
|---|---|---|---|---|---|---|
| 6 | TR | 土耳其 | 905 | 95 | N |
| 7 | US | 美国 | 926 | 91 | N |
| 8 | ZA | 南非 | 801 | 94 | N |

## 2.2 写入多个 SAS 数据集

### 目标

- 在单个 DATA 步句中创建多个 SAS 数据集。
- 使用条件处理控制观测值写入哪个数据集（或多个数据集）。

### 业务场景

使用输入数据集创建三个新的数据集。

![](img/d3bde6e6ab06b1fc622215d982111742_45_0.png)

### 浏览输入数据集

```
proc print data=orion.employee addresses;
var EmployeeName City Country;
run;
```

部分 PROC 输出（共计 424 条观测值）

| Obs | Employee_Name | City | Country |
|---|---|---|---|
| 1 | Abbott, Ray | Miami-Dade | US |
| 2 | Aisbitt, Sandy | Melbourne | AU |
| 3 | Akinfarin, Tameaka | Philadelphia | US |
| 4 | Angus, Sally | San Diego | US |
| 5 | Anger, Rose | Philadelphia | US |
| 6 | Ansley, David | Miami-Dade | US |
| 7 | Antoine, Doris | Miami-Dade | US |
| 8 | Apr, Nishan | San Diego | US |
| 9 | Arskdin, Elizabeth | Miami-Dade | US |
| 10 | Area, Avril | Miami-Dade | US |
| 11 | Arizmendi, Gilbert | San Diego | US |
| 12 | Armant, Debra | San Diego | US |

### 创建多个 SAS 数据集

通过在 DATA 语句中列出输出数据集名称，可以在 DATA 步中创建多个数据集。

使用 usa, australia, 和 other 创建新数据集。

```
DATA <SAS-data-set-1 ... SAS-data-set-n>;
```

```
data usa australia;
set orion.employee_addresses;
if Country='AU' then output australia;
else if Country='US' then output usa;
else output other;
run;
```

您可以通过在 OUTPUT 语句中列出数据集名称，将输出重定向到特定的数据集或多个数据集。

OUTPUT 语句中命的数据集必须出现在 data 语句中。

要在单个 OUTPUT 语句中指定多个数据集，请用空格分隔数据集名称。

```
data au us other;
set orion.employee_addresses;
if country ('AU') then output us;
else output other;
run;
```

### 检查 SAS 日志

创建了三个数据集。日志显示 US 是出现频率最高的值。

### 部分 SAS 日志

```
NOTE: There were 424 observations read from the data set
ORION.EMPLOYEE_ADDRESSES.
NOTE: The data set WORK.USA has 311 observations and 9 variables.
NOTE: The data set WORK.AUSTRALIA has 105 observations and 9 variables.
NOTE: The data set WORK.OTHER has 6 observations and 9 variables.
```

### 高效条件处理

按频率递减的顺序检查值效率更高

```
data usa australia other;
set orion.employee addresses;
if Country='US' then output usa;
else if Country='AU' then output australia;
else output other;
run;
```

```
NOTE: There were 424 observations read from the data set
ORION.EMPLOYEE_ADDRESSES.
NOTE: The data set WORK.USA has 311 observations and 9 variables.
NOTE: The data set WORK.AUSTRALIA has 105 observations and 9 variables.
NOTE: The data set WORK.OTHER has 6 observations and 9 variables.
```

### 2.04 简答轮调查

考虑上一个 DATA 步的结果。
是否可以使用单个 PRINT 过程打印所有三个数据集？

### 部分 SAS 日志

```
NOTE: There were 424 observations read from the data set
ORION.EMPLOYEE_ADDRESSES.
NOTE: The data set WORK.USA has 311 observations and 9 variables.
NOTE: The data set WORK.AUSTRALIA has 105 observations and 9 variables.
NOTE: The data set WORK.OTHER has 0 observations and 9 variables.
```

### 显示多个数据集

PRINT 过程只能打印一个数据集。
每个数据集都需要单独的 PROC 步。

```
title 'Employees in the States';
proc print data=usa;
run;
title 'Employees in Australia';
proc print data=australia;
run;
title 'Non US Employees';
proc print data=other;
run;
title;
```

### 创建多个数据集

p202d3 演示了多个数据集的创建。

1. 打开 p202d3 并提交 DATA 步以创建三个数据集：usa, australia 和 other。检查日志。大多数观测值被写入 usa 和 australia，而只有少数观测值被写入 other。

### 部分 SAS 日志

```
NOTE: There were 424 observations read from the data set
ORION.EMPLOYEE_ADDRESSES.
NOTE: The data set WORK.USA has 311 observations and 9 variables.
NOTE: The data set WORK.AUSTRALIA has 105 observations and 9 variables.
NOTE: The data set WORK.OTHER has 6 observations and 9 variables.
```

2. 使用 SELECT 语句显示多个数据集。提交修改后的程序以处理大小写。UPCASE 函数可以处理大小写。

3. 提交 DATA 步来使用 UPCASE 函数，将 Country 值转换为大写。

4. 检查日志。哪些观测值被写入了 other？

