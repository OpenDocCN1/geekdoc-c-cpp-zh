

# 第 9 章：处理日期 127

## 程序 9.6：从 SAS 日期中提取星期几、日期、月份和年份

```sas
data Extract;
  set Four_Dates;
  Day = weekday (DOB);
  DayOfMonth = day (DOB);
  Month = Month (DOB);
  Year = year (DOB);
run;

title "Listing of Extract";
proc print data=Extract noobs;
  var DOB -- Year;
run;
```

`WEEKDAY` 函数返回星期，其中 1 = 周日，2 = 周一，以此此类推；`DAY` 函数返回月份中的几（1 到 31 之间的数字）。`MONTH` 函数返回 1 到 12 之间的数字，`YEAR` 函数返回四位年份值。

如果你以前没见过它，`VAR` 语句中的变量列表使用了双横线（--）形式的变量列表。此 `VAR` 语句包含了从 `Day` 到 `Year` 的所有变量，并按照它们在 SAS 数据集中存储的顺序排列。使用变量列表的双横线形式时要小心，因为变量的顺序可能不是你预期的。在使用这种表示法之前，最好运行 `PROC CONTENTS`（使用 `VARNUM` 选项）生成 SAS 数据集的变量列表。

接下来显示数据集 `Extract` 的列表：

## 程序 9.5：程序 9.6 的输出

### Extract 列表

| DOB | Day | DayOfMonth | Month | Year |
|---|---|---|---|---|
| 21OCT1950 | 7 | | 10 | 1950 |
| 01JAN1960 | 6 | | 1 | 1960 |

## 9.8 从月、日、年值创建 SAS 日期

一个非常有用的函数 `MDY`（月、日、年）允许你通过提供月、日、年值来创建 SAS 日期值。如果你有一个包含这些值但没有包含相应 SAS 日期的值的 数据集，或者你的原始数据文件中月、日、年值不符合任何 SAS 日期格式（informats），那么这个函数就特别有用。数据集 `Month_Day_Year` 包含变量 `Month`、`Day` 和 `Year`。你可以像这样创建 SAS 日期：

## 128 实例实例学习 SAS：程序员指南（第二版）

## 程序 9.7：使用 MDY 函数从月、日、年创建 SAS 日期

```sas
data MDY_Example;
set Learn.Month_Day_Year;
  Date = mdy (Month, Day, Year);
  format Date mmddyy10.
run;
```

在此程序中，`MDY` 函数的三个参数是来自输入数据集的 `MONTH`、`DAY` 和 `YEAR` 值。

这里是数据集 `MDY_Example` 的列表：

图 9.6：数据集 MDY_Example 列表

| Obs | Month | Day | Year | Date |
|---|---|---|---|---|
| 1 | 10 | 21 | 1950 | |
| 2 | | 3 | | 2005 | |
| 3 | 5 | 7 | 2000 | 05/07/2000 |

在观测值 2 中，由于日期缺失，`Date` 的值也是缺失的。

## 9.9 当日期值缺失时用每月 15 号代替

在某些情况下，你可能缺少日期值，但仍想计算一个近似日期。许多人用每月 15 号来代替缺失的 `Day` 值。你可以使用上一节的日期来演示如何操作。以下是程序：

## 程序 9.8：当日期值缺失时用每月 15 号代替

```sas
data Substitute;
  set Learn.Month_Day_Year;
  if missing(Day) then Date = mdy(Month,15,Year);
  else Date = mdy(Month, Day, Year);
  format Date mmddyy10.
run;
```

`MISSING` 函数测试变量 `Day` 是否缺失值。如果是，则将数字 15 作为 `MDY` 函数的第二个参数。结果列表显示了第二个观测值的日期为该月的 15 号：

## 第 9 章：处理日期

图 9.7：数据集 Substitute 列表

### Substitute 数据列表

| Obs | Month | Day | Year | Date |
|---|---|---|---|---|
| 1 | 10 | 21 | 1950 | 10/21/1950 |
| 2 | | 3 | 2005 | 03/15/2005 |
| 3 | 5 | 7 | 2000 | 05/07/2000 |

## 9.10 使用日期间隔函数

两个函数 `INTCK` 和 `INTNX` 处理日期间隔（如月份、季度、年份）。`INTCK` 函数计算从一个日期到另一个日期之间跨越的间隔边界数量；`INTNX` 函数则计算在给定间隔数量后的日期。

首先，没有人知道这两个函数该怎么读——这得靠你自己了。要理解这些函数最基本的用法，请看下表。例如，`INTCK` 取三个参数：第一个是间隔类型，第二个是起始日期，第三个是结束日期。

| 表达式 | 值 |
|---|---|
| INTCK('year','31Dec2005d','01Jan2006d') | 0 |
| INTCK('month','31Dec2005d','01Jan2006d') | 1 |
| INTCK('month','31Jan2005d','01Jan2006d') | 0 |
| INTCK('day','31Jan2005d','01Feb2005d') | 1 |
| INTCK('qtr','25Mar2005d','15Apr2005d') | 1 |

`INTCK` 函数计算从一个日期到另一个日期跨越的间隔边界数量；`INTNX` 函数计算给定间隔数量后的日期。首先，没有人知道这两个函数该怎么读——这得靠你自己了。关于这些函数的更完整处理，请参见《实例学习 SAS》。

`INTCK` 函数计算从一个日期到另一个日期跨越的间隔边界数量；`INTNX` 函数计算给定间隔数量后的日期。

`INTCK` 函数计算从一个日期到另一个日期跨越的间隔边界数量；`INTNX` 函数计算给定间隔数量后的日期。

`INTCK` 函数计算从一个日期到另一个日期跨越的间隔边界数量；`INTNX` 函数计算给定间隔数量后的日期。

`INTCK` 函数计算从一个日期到另一个日期跨越的间隔边界数量；`INTNX` 函数计算给定间隔数量后的日期。

`INTCK` 函数计算从一个日期到另一个日期跨越的间隔边界数量；`INTNX` 函数计算给定间隔数量后的日期。

`INTCK` 函数计算从一个日期到另一个日期跨越的间隔边界数量；`INTNX` 函数计算给定间隔数量后的日期。

`INTCK` 函数计算从一个日期到另一个日期跨越的间隔边界数量；`INTNX` 函数计算给定间隔数量后的日期。

`INTCK` 函数计算从一个日期到另一个日期跨越的间隔边界数量；`INTNX` 函数计算给定间隔数量后的日期。

`INTCK` 函数计算从一个日期到另一个日期跨越的间隔边界数量；`INTNX` 函数计算给定间隔数量后的日期。

`INTCK` 函数计算从一个日期到另一个日期跨越的间隔边界数量；`INTNX` 函数计算给定间隔数量后的日期。

`INTCK` 函数计算从一个日期到另一个日期跨越的间隔边界数量；`INTNX` 函数计算给定间隔数量后的日期。

`INTCK` 函数计算从一个日期到另一个日期跨越的间隔边界数量；`INTNX` 函数计算给定间隔数量后的日期。

`INTCK` 函数计算从一个日期到另一个日期跨越的间隔边界数量；`INTNX` 函数计算给定间隔数量后的日期。

## 130 实例学习 SAS：程序员指南（第二版）

除了 `YEAR`、`MONTH` 和 `QUARTER`，两个日期函数 `INTCK` 和 `INTNX` 还支持多种类型。以下是 `INTCK` 和 `INTNX` 支持的间隔部分列表：

图 9.8：INTCK 和 INTNX 支持的间隔列表：

| 间隔 | 描述 |
|---|---|
| Week | 以周日为第一天的周间隔 |
| Weekday | 周几（默认不包含周六） |
| Month | 月份（每月第一天为边界） |
| Qtr | 季度（1月1日、4月1日、7月1日和10月1日） |
| Semi-year | 半年度间隔 |
| Year | 年度间隔 |

这是一个示例。数据集 `Hosp` 包含1000个观测值。该数据集中的变量包括出生日期（DOB）和入院日期（Admit）。你想看一张图，显示从2003年1月1日到2006年6月30日每个季度的入院人数。如果不使用 `INTCK` 函数，这将需要大量的编程工作；而现在这变成了一个更直接的问题。以下是其中一种解决方案：

## 程序 9.9：演示 INTCK 函数

```sas
data Frequency;
  set Learn.Hosp(Keep=AdmitDate)
  where=(AdmitDate) between '01Jan2003'd and '30Jun2006'd);
  Quarter = intck('qtr','31Dec2002'd,AdmitDate);
run;

title "Admissions from January 1, 2003 to June 30, 2006";
proc sgplot data=Frequency;
  vbar Quarter;
run;
```

程序的关键在于使用 `INTCK` 函数来计算从2002年12月31日开始开始的季度数。（使用该日期是为了让2003年第一季度的任何入院都被视为第一季度。）`PROC SGPLOT` 可以产生垂直柱状图（因此使用关键字 `VBAR`），显示每个季度发生了多少次访问。结果如图所示：

图 9.9：程序 9.9 的输出

![](img/e9e15d853989558188e1c83b0ae655b0_143_0.png)

`INTCK` 函数的反函数是 `ITTNX`。该函数接收一个起始日期并返回跨越了给定数量间隔边界后的日期。这里有一个示例。

你有一个数据集（Hosp_Discharge），包含患者编号（Patient）和出院日期（Discharge）。你想在出院6个月后的每月第一天通知每位患者。首先，这里是 `Hosp_Discharge` 数据集的列表：

