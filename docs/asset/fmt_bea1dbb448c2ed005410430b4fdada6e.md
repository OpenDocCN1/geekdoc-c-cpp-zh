
是的，`IF` 语句看起来确实是假的，`SET` 语句从不执行。`NOBS=` 选项在编译时起了作用。`CALL SYMPUTS` 将 `Number_of_obs` 的值赋值给宏变量 `N_of_obs`。

## 任务：确定 SAS 数据集中的观测数（使用库表）

### 关键词

- 观测数
- 库表

`SAS` 表包含与你的数据集相关的元数据，你可以通过指定 `LIBNAME` 和数据集名称从 `SAS8.VTABLE` 中获取这些信息。这种确定观测数的方法比到目前为止描述的其他方法具有优势。即，如果你（或其他人）正在修改数据集，你需要知道总观测数，以及被标记为删除的观测数（但在使用 `NOBS=` 选项时它们仍会被计入内）。

### 程序 12.4：使用库表确定数据集的观测数

```sas
data _null;
set sashelp.vtable;
where libname="WORK" and memname="STOCKS";
Note:you必须对 libname 和 memname 使用大写值;
**Num_nobs= 总观测数，包括已删除的
Delobs 是已删除的观测数；
put Delobs: = num_obs;
run;
```

## 任务：确定 SAS 数据集中的观测数（使用 SAS 函数）

### 关键词

- 观测数
- `Exist` 函数
- `Attrn` 函数

还有什么方法可以确定 SAS 数据集的观测数？文件 I/O 类别中的一组函数允许你获取有关 SAS 数据集的信息。

# 120 Cody 常用 SAS 编程任务合集及解决方案

以下是程序，随后附有相关解释：

## 程序 12.5：使用 SAS 函数确定 SAS 数据集中的观测值数量

```sas
*Using SAS functions;
data_null;
  Exist = exist("Stocks");
  if Exist then do;
    Num_obs = attrn(Dsid,"Nobs");
    *Nobs 是逻辑观测值的数量，
      未标记为删除的观测值；
    put "Number of observations in STOCK is: " Num_obs;
  end;
  else put "Data set STOCK does not exist";
  RC = close(Dsid);
run;
```

当数据集存在时，`EXIST` 函数返回真值，不存在则返回假值。接下来，使用 `OPEN` 函数打开数据集。该函数返回一个数据 ID，你可以将其与其他 I/O 函数一起使用。将数据集 ID 作为 `ATTR` 函数的第一个参数，并将该函数的多个字符值中的任何一个作为第二个参数。`NLOBS` 给你逻辑观测值的数量（未标记为删除的观测值）。该第二个参数的另一个有用值是 `NVAR`，它返回数据集中变量的数量。

此程序中由 `PUT` 语句在 SAS 日志中产生的行如下：

`Number of observations in STOCK is: 42`

建议在完成后关闭该数据集（使用 `CLOSE` 函数）。

## 任务：在变量列表中统计特定响应的数量

### 关键词

- `CATS` 函数
- `COUNTN` 函数

在变量列表中统计特定值

在示例示例中，你有一个包含五个变量（`Q1`–`Q5`）的数据集（`Questionnaire`）。每个变量为‘Y’或‘N’（是或否），且这些值可能是大写的，也可能是小写的。任务是统计 Y 和 N 的数量。此第一个程序演示了实现这一目标的“旧式”方法。以下是该程序：

`Cody, Ron. Cody’s Collection of Popular SAS® Programming Tasks and How to Tackle Them. Copyright © 2012, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/bookstore.`

## 第 12 章：杂项任务 121

### 程序 12.6：统计 SAS 变量列表中 Y 和 N 的数量（使用数组和循环）

```sas
*Counting the number of a specific response in a list of variables;
*Old Fashioned; solution;

data Count_YN;
  set Questionnaire;
  array Q[5];
  Num_Y = 0;
  Num_N = 0;
  do i = 1 to 5;
    if upcase(Q[i]) eq 'Y' then Num_Y = Num_Y + 1;
    else if upcase(Q[i]) eq 'N' then Num_N = Num_N + 1;
  end;
  drop i;
run;
```

你首先创建一个包含五个变量的数组。接下来，你将存储计数的两个变量 `Num_Y` 和 `Num_N` 初始化为零。最后，你使用 `DO` 循环检查每个变量的值，并检查它是否为 'Y' 或 'N'。需要使用 `UPPERCASE` 函数，因为某些值可能是小写的。

下面是 `Q_YN` 数据集的列出：

| Subj | Q1 | Q2 | Q3 | Q4 | Q5 | Num_Y | Num_N |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | y | n | n | y | | 3 | 2 |
| 2 | N | n | Y | n | | 1 | 3 |
| 4 | y | Y | n | Y | | 3 | 2 |
| 5 | y | Y | n | y | | 5 | 0 |

该任务更优雅的解决方案是使用两个 SAS 函数：`CATS` 和 `COUNTC`。`CATS` 函数可以接受每个参数，去除首部和尾的空格，并拼接字符串。`COUNTC` 函数统计特定字符（或多个字符）在字符串中出现的次数。这两个函数共同提供了一个非常紧凑且优雅的解决方案，如下所示：

## 程序 12.7：使用 CATS 和 COUNTC 函数统计响应

```sas
*Solution using the Count and Cats functions;
data Count_YN;
  set Questionnaire;
  Num_Y = countc(cats of Q1-Q5),'Y','i');
  Num_N = countc(cats of Q1-Q5),'N','i');
run;
```

`Cody, Ron, Cody's Code of Popular SAS® Programming Tasks and How to Tackle Them. Copyright © 2012, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/bookstore.`

`COUNTC` 函数的第一个参数是你想要查询的字符串，第二个参数指定了你想要统计的一个或多个字符，第三个参数是修饰符。'I' 修饰符意味着忽略大小写。运行此程序的输出与之前描述的较长程序相同。

`Cody 常用 SAS 编程任务合集及解决方案`

## 任务：计算移动平均值

### 关键词

- 移动平均
- `LAG` 函数

移动平均用于观察可能存在大幅波动的数据趋势。在示例中，你希望平均三天的数据以观察波动难以观察的趋势，第二个是四天，以此类推。由于你需要平均三个观测值，可以使用 `LAG` 函数来获取：

### 程序 12.8：计算移动平均值

```sas
*To compute average;
set Stocks;
Last = lag(Price);
Twoback = lag(Price);
if _n >= 3 then Moving = mean(Last, Twoback);
```

`Cody, Ron. Cody's Collection of Popular SAS® Programming Tasks and How to Tackle Them. Copyright © 2012, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/bookstore.`

`Cody, Ron. Cody's Collection of Popular SAS Programming Tasks and How to Tackle Them. Copyright © 2012, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/bookstore.`

为了帮助观察点和移动平均值之间的差异，可以使用下方的 `PROCPLOT`：

## 价格与日移动平均图

![](img/ac68221c9b510d4f92_144.png)

你可以看到，代表移动平均的虚线没有原始数据那么波动。

`Cody, Ron. Cody’s Collection of Popular SAS® Programming Tasks and How to Tackle Them. Copyright © 2012, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/bookstore.`

124 `Cody 常用 SAS 编程任务合集及解决方案`

## 任务：提供一个用于计算移动平均的宏

### 关键词

移动平均

如果你经常需要计算移动平均值，或者你想对大量数据点的平均值，你可能希望使用这里提供的宏。调用宏 `Moving_Ave` 时需要输入数据集名称、包含输入数据集所有变量以及移动平均值的新数据集名称、要赋值的变量名称，以及每个平均值包含的观测值数量。

随后是该宏工作原理的简要说明：

### 程序 12.9：提供一个用于计算移动平均的宏

```sas
*Presenting a macro to compute a moving average;
*macro Moving_ave(In_ds=, /*输入数据集 */
Out_ds=, /*输出数据集 */
Var=, /*计算平均值的变量 */ /*移动平均值变量 */
Moving=, /*计算平均值的观测值数量 */);
data &Out_ds;
set &In_ds;
n=1;
var &Var;
do i = 1 %to &n - 1;
let Num = %eval(&i + 1);
&xNum = lag(Num)(&&Var);
end;

****如果观测值数量大于或等于计算平均值所需的数量，输出;
if _n >= &n then do;
&Moving = mean(_x1 - _xn);
output;
end;
drop _x_;
run;
%end Moving_ave;
```

你从一个 `DATA` 步开始，从数据引入每个观测值。你需要为原始变量及其每个延迟值赋值。你使用变量 `_x1` 作为非延迟值，使用 `_x2` 作为 `LAG1` 值，`_x3` 作为 `LAG2` 值。

## 第 12 章：杂项任务 125

以此类推。`_x1` 的值在 `%DO` 循环外部设置，而其他每个 `_x` 值都是通过连接前缀 `_x` 与 `%DO` 循环计数器加 1 来分配的。例如，在 `%DO` 循环的第一次迭代中，`i` 等于 1、2，赋值语句解析为 `_x2 = lag(variable)`。一旦你计算了所有的 lag 值，你就可以使用 `MEAN` 函数来计算移动平均值。

为了直观地了解它的工作原理，让我们把这个宏命名为：

### 程序 12.10：调用 moving_ave 宏

```
*Testing the macro;
moving_Ave(In_name=Stocks,
out=moving_stocks,
Var=Price,
Moving=Average,
n=5)
```

并检查 SAS 日志以查看宏生成的代码（通过开启 `MPRINT` 选项实现）。以下是生成的代码：

```
MPRINT (MOVING_AVE) : data Moving_Stocks;
MPRINT (MOVING_AVE) : set Stocks;
MPRINT (MOVING_AVE) : **compute the lags;
MPRINT (MOVING_AVE) : x1 = Price;
MPRINT (MOVING_AVE) : x2 = lag(Price);
MPRINT (MOVING_AVE) : x3 = lag2(Price);
MPRINT (MOVING_AVE) : x4 = lag3(Price);
MPRINT (MOVING_AVE) : x5 = lag4(Price);
MPRINT (MOVING_AVE) : **if the number is greater than or
equal to the number of values needed for the moving average, output;
MPRINT (MOVING_AVE) : if n_ = 5 then do;
MPRINT (MOVING_AVE) : Average = mean of (_x1 _x5);
MPRINT (MOVING_AVE) : output;
MPRINT (MOVING_AVE) : end;
MPRINT (MOVING_AVE) : drop _x;
MPRINT (MOVING_AVE) : run;
```

记住，你可以通过 SAS 网站 (`support.sas.com/cody`) 复制此宏以及书中的所有程序。

`Cody, Ron. Cody's Collection of Popular SAS® Programming Tasks and How to Tackle Them. Copyright © 2012, SAS Institute Inc.`

`Cary, North Carolina, USA. ALL RIGHTS RESERVED. 如需更多 SAS 资源，请访问 support.sas.com/bookstore。`

## 任务：用星号替换信用卡号的前八位数字

### 关键字

- 掩码字符
- `SUBSTR` 函数
- `CATS` 函数
- 符号左侧的 `SUBSTR` 函数

此任务不仅限于掩码信用卡号中的数字——你任何想要替换字符串中字符的时刻都可以使用这种技术。你将看到此任务的两种解决方案：一个简单直观，另一个非常优雅。

在第一个解决方案中，你使用 `SUBSTR` 函数提取信用卡号的最后 4 位数字，然后使用 `CATS` 函数将星号与这四个数字连接起来。以下是代码：

```
Program 12.11: Replacing the first eight digits of a credit card number with asterisks (method 1)
*Replacing the first 8 digits of a credit card number
with asterisks;
*Using substrings and concatenation functions;
data Credit_Report;
length Last_Four $ 12;
set Credit;
Last_Four = cats('******',substr(Account, 9));
run;
```

一个更优雅的解决方案是像这样在等号左侧使用 `SUBSTR` 函数：

```
Program 12.12: Replacing the first eight digits of a credit card number with asterisks (method 2)
*Using the SUBSTR function on the left-hand side of the equal sign;
data Credit_report;
set Credit;
Last_Four = Account;
substr(Last_Four,1,8) = '******';
run;
```

回顾一下，等号左侧的 `SUBSTR` 函数将等号右侧字符放入等号左侧命名的变量中，起始位置由函数的第二个参数指定，长度由函数的第三个参数指定。是的，这个程序只比上一个程序少了一行，但这位作者认为这是一个更优雅的解决方案——难道编写优雅的程序不是你的目标吗？

## 任务：在观测值内排序（使用 ORDINAL 函数）

### 关键字

- 观测值内排序
- `Ordinal` 函数

在许多情况下，你希望对观测值内的值进行排序。例如，你可能有每个人的若干分数，并希望从低到高对分数排序。这里提供的第一个解决方案使用 `ORDINAL` 函数来实现此目标。该函数接受数字作为第一个参数，并将值列表作为剩余参数。当数字等于 1 时，函数返回最小的值；当数字等于 2 时，函数返回第二小的值；当数字不忽略缺失值时，最小值可能是一个缺失值。另一个排序函数 `SMALLEST` 则会忽略缺失值——它返回值列表中的最小值，不计算任何缺失值。

你想对 10 个分数（`Score1-Score10`）从低到高排序。这些分数存储在数据中，如下所示：

| Name | Score1 | Score2 | Score3 | Score4 | Score5 | Score6 | Score7 | Score8 | Score9 | Score10 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| John | 95 | 92 | 87 | 100 | 96 | 88 | 89 | 78 | | 95 |
| Mary | | 98 | 96 | 93 | 89 | 95 | 94 | | 99 |
