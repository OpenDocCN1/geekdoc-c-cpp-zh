

DO I=1 to 50;

IF ANSWER(I) = -9 then ANSWER(I) =;

END;

## 动手示例

此示例说明了如何在 SAS 程序中使用数组（ARRAYS）和 DO 循环。假设你有一份关于反复光诊诊所的受试者的测量记录。然而，每位患者就诊的次数并不相同。你想知道受试者上次在诊所时所观察到的测量值（任何非缺失值）。

- 1. 打开程序文件 DDOLOOP.SAS。

```sas
DATA CLINIC;
INPUT ID $3. @4 VISIT1 4. @7 VISIT2 4;
@10 VISIT3 4. @13 VISIT4 4. @16 VISIT5 4;
ARRAY TIME (5) VISIT1-VISITS;
LAST=VISIT;
DO I=1 TO 5;
IF TIME(I) > 0 LAST=TIME(I);
END;
DROP I;
DATALINES;
001 34 54 34 54 65
002 23 43 54 34
003 23 43 . 43
004 45 55 21 43 23
005 54
;
PROC PRINT DATA=CLINIC; RUN;
```

- 2. 运行此程序并观察表 7.4 中的输出。注意变量 `LAST` 包含了就诊列表中最后一个“有效”值的观测值。

- 3. 如果你还想知道每个受试者记录数值的次数，可以在 DATA 步骤中使用 `N( )` 函数添加以下语句来获取该值。重新提交代码。你应该会得到一个包含就诊次数的新列。

```sas
NUMVISITS=N(OF TIME(*));
```

- 4. 同样，使用 `MAX` 函数找到每个受试者的最大值。重新提交代码并观察结果。

```sas
MAXVISITS=MAX(OF TIME(*));
```

## 第 7 章：SAS® 高级编程主题部分 2

| 表 7.4 数组和 DO 循环示例：说明了 DO 循环和数组的使用 |
| Obs | ID | VISIT1 | VISIT2 | VISIT3 | VISIT4 | VISIT5 | LAST |
|---|---|---|---|---|---|---|---|
| 1 | 001 | 34 | 54 | 34 | 54 | 65 | 65 |
| 2 | 002 | 23 | 43 | | 54 | | 34 |
| 3 | 003 | 23 | 43 | | 43 | | 43 |
| 4 | 004 | 45 | 55 | 21 | 43 | 23 | 23 |
| 5 | 005 | 54 | | | | | 54 |

## 动手示例

此示例说明了在不知道数组的上下界界时如何使用 DO 循环。使用的数据集是 1978 年至 2007 年间华盛顿特区的犯罪报告。该数据将原始的缩进值转换为百分比（人口/x 100.）。

- 1. 打开程序文件 DARRAY3.SAS。

```sas
DATA CRIME;SET MYSASLIB.DC_CRIME78_07;
FORMAT TOTAL 6.;
ARRAY INCIDENTS (*) VIOLENT-CARTHEFT;
DO I = LBOUND(INCIDENTS) to HBOUND(INCIDENTS);
TOTAL=SUM(of TOTAL, INCIDENTS(i));
END;
DROP I;
RUN;
PROC PRINT DATA=CRIME;
VAR YEAR POP-CARTHEFT TOTAL;
RUN;
```

注意这段代码中，名为 `INCIDENTS` 的数组使用了 `(*)` 而不是固定元素数量。也就是说，我们没有在代码中指定 `VIOLENT - CARTHEFT` 列表中包含多少个变量。即使我们不知道 `INCIDENTS` 数组的边界，我们仍然可以在 DO 循环中使用 `LBOUND` 和 `HBOUND` 函数来遍历整个列表。

提交此代码并观察结果。注意在显示的结果中，大数字显示时不带逗号，

- 2. 你还想找到每年的犯罪总数，以及按人口计算的犯罪百分比。

```sas
TOTALCRIMES=SUM(of INCIDENTS (*));
PCTTOTAL=TOTALCRIMES/POP*100;
```

## 表 7.5 DO 循环中 LBOUND 和 HBOUND 的结果

| Obs | YCP | Index | Violent | Property | Rape | Assault | Burgundy | Larceny | CarThe | TOTALCRIMES | PCTTOTAL |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 1978 | 64000 | 50950 | 9155 | 4136 | 189 | 489 | 6920 | 2642 | 12497 | 25744 | 101.900 | 15.187 |
| 2 | 1979 | 65000 | 56430 | 10563 | 5847 | 153 | 568 | 6920 | 1352 | 28819 | 3066 | 112.860 | 17.203 |
| 3 | 1980 | 632535 | 63668 | 12772 | 6086 | 200 | 439 | 8287 | 13262 | 34325 | 127.376 | 20.046 |
| 4 | 1981 | 636000 | 67910 | 12371 | 63448 | 223 | 414 | 9137 | 3645 | 14774 | 33435 | 135.820 | 20.216 |
| 5 | 1982 | 632100 | 65666 | 13937 | 52395 | 195 | 421 | 9134 | 3645 | 14674 | 33435 | 131.384 | 21.353 |
| 6 | 1983 | 632000 | 57776 | 11933 | 55483 | 185 | 376 | 6068 | 7698 | 14263 | 29405 | 115.552 | 18.547 |
| 7 | 1984 | 632000 | 53010 | 10725 | 20994 | 179 | 306 | 6087 | 7098 | 10954 | 24071 | 107.047 | 18.827 |
| 8 | 1985 | 632000 | 52605 | 9195 | 17305 | 147 | 335 | 6028 | 5095 | 20483 | 24054 | 105.100 | 16.954 |
| 9 | 1986 | 632000 | 52530 | 9425 | 12791 | 194 | 420 | 4720 | 5189 | 10981 | 25612 | 104.468 | 16.976 |
| 10 | 1987 | 632000 | 52569 | 10016 | 49567 | 225 | 245 | 4462 | 5084 | 11254 | 25012 | 105.138 | 16.902 |
| 11 | 1988 | 632000 | 62172 | 11937 | 49265 | 369 | 165 | 5690 | 5690 | 11280 | 28624 | 122.942 | 19.824 |
| 12 | 1989 | 640000 | 62172 | 12937 | 49265 | 436 | 180 | 6542 | 5775 | 11780 | 124.568 |

## 7.3 使用 RETAIN 语句

RETAIN 语句用于 DATA 步骤，以便在变量被读入数据集时跨迭代保留其变量值。RETAIN 的基本语法为：

```sas
RETAIN <var <initial-value(s)> var2 <initial-values(s)> and on;
```

例如，要指示 SAS 记住变量的值，您可以使用以下语句：

```sas
RETAIN SCORE;
```

一个保留多个变量值的语句可以是：

```sas
RETAIN TIME-TIME10 SCORE VISIT;
```

默认情况下，保留变量的初始值是缺失的。一个保留 SCORE 值且初始值为 1 的语句是：

```sas
RETAIN SCORE 1;
```

在以下实例中，CATEGORY 的初始值为 NONE，而 TIME-TIME10 变量的初始值为 0。

```sas
RETAIN CATEGORY "NONE" TIME-TIME10 0;
```

要设置列表的值，请使用此格式：

```sas
RETAIN TIME-TIME4 (1 2 3 4);
```

或者

```sas
RETAIN TIME-TIME4 (1, 2, 3, 4);
```

或者

```sas
RETAIN TIME-TIME4 (1:2:4);
```

要保留所有变量，请使用

```sas
RETAIN __;
```

在启动 RETAIN 语句之前，你也可以为变量设置值，以便在第一次迭代中使用。例如，假设你有一系列日期观测值，并计算自第一次访问以来的数。一种方法是使用 RETAIN 语句，假设数据已按日期排序，考虑以下代码：

```sas
DATA DAYS; SET MYDATA;
IF _N_=1 THEN FIRST=VISIT_DATE;
RETAIN FIRST;
DAYS=VISIT_DATE-FIRST;
```

- IF _N_=1 语句创建一个名为 FIRST 的新变量，并将 VIS_DATE 设置为初始值。
- RETAIN 语句告诉 SAS 从上一次记录中保留 FIRST 的值（否则它将缺失）。
- DAYS= 语句使用 FIRST 变量计算当前记录的 VISIT_DATE 差值，从而得到自第一次访问以来的天数。

## 动手示例

此示例计算自第一次访问以来的天数。

- 1. 打开程序文件 DRETAIN1.SAS。

```sas
DATA MYDATA;
INPUT VISIT_DATE ANYDTD0;
DATALINES
01/04/2015
01/29/2015
03/07/2015
04/25/2015
07/06/2015
08/30/2015
;
DATA DAYS;SET MYDATA;
IF _N_=1 THEN FIRST=VISIT_DATE;
RETAIN FIRST;
DAYS=VISIT_DATE-FIRST;
RUN;
PROC PRINT DATA=DAYS;
Title ‘These are the contents of the dataset DAYS’;
FORMAT VISIT_DATE DATE10.
RUN;
```

- 2. 运行此示例并观察表 7.6 中的输出。
- 3. 删除 RETAIN 语句并重新运行程序。注意 FIRST 变量在第一次迭代后丢失值，而 DAYS 变量在第一个记录之后均为缺失。

作为使用 RETAIN 语句的第二个示例，假设你在户外商场经营一个柠檬水摊。你有前 7 天的销售数据，并想创建一个提供累计销售额并跟踪最高销售额的报告

