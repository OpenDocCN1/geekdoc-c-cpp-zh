
| Employee_Term_Date | Frequency | Percent | Cumulative Frequency | Cumulative Percent |
|---|---|---|---|---|
| None | 308 | 72.64 | 308 | 72.64 |
| 2002 | 6 | 1.42 | 314 | 74.06 |
| 2003 | 29 | 6.84 | 343 | 80.90 |
| 2004 | 18 | 4.25 | 361 | 85.14 |
| 2005 | 21 | 4.95 | 382 | 90.09 |
| 2006 | 20 | 4.72 | 402 | 94.81 |
| JAN2007 | 3 | 0.71 | 405 | 95.52 |
| FEB2007 | 3 | 0.71 | 408 | 96.23 |
| MAR2007 | 7 | 1.65 | 415 | 97.78 |
| APR2007 | 3 | 0.71 | 418 | 98.58 |
| MAY2007 | 4 | 0.94 | 422 | 99.53 |
| JUN2007 | 2 | 0.47 | 424 | 100.00 |

## 11.4 观测值的筛选与分组

### 目标

- 使用 `WHERE` 语句在报告中显示指定的观测值。
- 使用 `BY` 语句在报告中显示观测值分组。

## WHERE 语句（回顾）

为了筛选报告中的观测值，`WHERE` 语句用于选择满足特定条件的观测值。

`WHERE` 语句的通用形式：

```
WHERE where-expression;
```

`where-expression` 是操作数和运算符的序列，构成了一组定义选择观测值选择的指令。

- 操作数包括常数和变量。
- 运算符是请求比较、算术计算或逻辑操作的符号。

## 11.4 观测值的筛选与分组

## 11.08 测验

以下哪些 `WHERE` 语句的语法不正确？

- a. `where Salary ne ;`
- b. `where Hire_Date >= '01APR2008'd;`
- c. `where Country in (AU US);`
- d. `where Salary + Bonus <= 10000;`
- e. `where Gender ne 'M' Salary >= 50000;`
- f. `where Name like '%N';`

### 筛选观测值

```
proc print data=orion.sales;
  var First Name Last Name
  Job Title Country Salary;
  where Salary > 75000;
run;
```

| Obs | Name | Last_Name | Job_Title | Country | Salary |
|---|---|---|---|---|---|
| 1 | Tom | Zhou | Sales Manager | AU | 108255 |
| 2 | Wilson | Dawes | Sales Manager | AU | 67972 |
| 64 | Harry | Highpoint | Delta Sales Officer | US | 243190 |
| 163 | Louis | Favaron | Senior Sales Manager | US | 85090 |
| 164 | Agnes | Caprichetti | Sales Manager | US | 83500 |
| 165 | Dennis | Lansberry | Sales Manager | US | 84260 |

### 筛选观测值

```
proc means data=orion.sales;
var Salary;
where Country = 'AU';
run;
```

MEANS 过程

分析变量 : Salary

| N | Mean | Std Dev | Minimum | Maximum |
|---|---|---|---|---|
| 63 | 30158.97 | 12699.14 | 25185.00 | 108255.00 |

## 投票准备

- 获取并提交程序 `p111a02`。
- 查看日志（log），确定 SAS 如何处理多个 `WHERE` 语句。

```
proc freq data=orion.sales;
tables Gender;
where Salary > 75000;
where Country = 'US';
run;
```

## 11.09 多选题投票

关于多个 `WHERE` 语句，哪种描述是正确的？

- a. 所有的 `WHERE` 语句都被使用了。
- b. 没有任何 `WHERE` 语句被使用。
- c. 第一个 `WHERE` 语句被使用了。
- d. 最后一个 `WHERE` 语句被使用了。

> 不能使用 2 个 `WHERE` 语句！

## BY 语句

为了对报告中的观测值分组，`BY` 语句用于为每个 `BY` 组生成独立的报告章节。

`BY` 语句的通用形式：

```
BY <DESCENDING> by-variable(s);
```

数据集中的观测值必须按照 `BY` 语句指定的变量进行排序。

### 分组观测值

```
proc sort data=orion.sales out=work.sort;
by Country descending Gender Last Name;
run;

proc print data=work.sort;
by Country descending Gender;
run;
```

### 分组观测值

部分 `PROC PRINT` 输出

| Obs | Employee_ID | First_Name | Last_Name | Salary |
|---|---|---|---|---|
| 1 | 120145 | Sandy | Aisbitt | 26060 |
| 2 | 120144 | Judy | Barbis | 30265 |
| 3 | 120146 | Wendall | Cederlund | 25985 |

| Obs | Employee_ID | First_Name | Last_Name | Salary |
|---|---|---|---|---|
| 37 | 120168 | Selina | Barcoe | 25275 |
| 38 | 120198 | Meera | Body | 28025 |
| 39 | 120149 | Sharryn | Clarkson | 26396 |
| 40 | 120127 | Sharryn | 28100 |
| 41 | 120138 | Shani | Duckett | 25795 |
| 42 | 120121 | Irenie | Elvish | 26600 |
| 43 | 120154 | Caterina | Hayawardhana | 30490 |
| 44 | 120123 | Kimiko | Hotstone | 26190 |

## 11.10 测验

对于 `PROC FREQ` 步骤，哪个是有效的 `BY` 语句？

- a. `by Country Gender;`
- b. `by Gender Last Name;`
- c. `by Country;`
- d. `by Gender;`

```
proc sort data=orion.sales out=work.sort;
  by Country descending Gender Last_Name;
run;

proc freq data=work.sort;
  tables Gender;
run;
```

## 练习

### 1级

10. 观测值的筛选与分组

- a. 获取初始程序 `p111e10`。
- b. 添加一个 `PROC SORT` 步骤，根据 `Order_Type` 变量对 `orion.order_fact` 中的观测值进行排序。

> 为了避免覆盖 `orion.order_fact` 数据集，请务必使用 `OUT=` 选项创建一个包含排序后观测值的新数据集。记得在 `PROC MEANS` 步骤中使用数据集。

- c. 将 `PROC MEANS` 分析限制为两个 `Order_Type` 值。
- d. 修改 `PROC MEANS` 步骤为每个 `Order_Type` 值生成摘要。
- e. 提交程序产生以下结果：

| Orion Star Sales |
|---|
| Type=2 |
| Analysis Variable : Total_Retail_Price |
| N | Mean | Std Dev | Minimum | Maximum |
| 170 | 199.591765 | 282.968017 | 270.00 | 1937.2 |
| Type=3 |
| Analysis Variable : Total_Retail_Price |
| N | Mean | Std Dev | Minimum | Maximum |
| 123 | 174.728048 | 214.352833 | 270.000 | 1542.6 |

### 2级

11. 按变量分组

- a. 获取初始程序 `p111e11`。
- b. 按 `Order_Type`（升序）和 `Order_Date`（降序）排序 `orion.order_fact` 数据集。

> 创建一个新的数据集。不要覆盖 `orion.order_fact` 数据集。在 `PROC PRINT` 步骤中使用该数据集。

- c. 使用 `BY` 语句划分 `PROC PRINT` 报告。
- d. 按标准限制 `PROC PRINT` 报告：

  1) 2005 年前几个（1 月至 4 月）下单的订单
  2. 恰好两天后交付的订单

- e. 为 `PROC` 添加第二个标题。
- f. 提交程序产生以下结果：

| Orion Star Details |
|---|
| Type=2 |
| Analysis Variable : Total_Retail_Price |
| N | Mean | Std Dev | Minimum | Maximum |
| 409 | 123.596175 | 282.968017 | 270.00 | 1937.2 |
| Type=3 |
| Analysis Variable : Total_Retail_Price |
| N | Mean | Std Dev | Minimum | Maximum |
| 568 | 174.728048 | 214.352833 | 270.000 | 1542.6 |

### 3级

12. 添加筛选条件

- a. 获取初始程序 `p111e12`。
- b. 调整 `PROC PRINT` 语句中的变量，使 `BY` 行显示 `Supplier_Name`、`Supplier_ID` 和 `Supplier_Country`。输入数据保持按这些变量分组但未排序。

> 必须在 `BY` 语句中添加选项以支持使用分组未排序的数据。

- c. 扩展现有的 `WHERE` 条件，进一步限制报告为包含 `Street` 或 `Running` 单词的产品名称。

> 要要在不重写或编辑现有 `WHERE` 语句的情况下，在同一步骤的另一个独立的 `WHERE` 语句中使用 `SAME-AND` 运算符添加子句。

- d. 提交程序产生以下结果：

# 11.5 将输出重定向到外部文件

### 目标

- 使用 `ODS` 语句将输出重定向到 `ODS` 目标。
- 使用 `STYLE=` 选项指定样式定义。
- 创建可以在 Microsoft Excel 中打开的 `ODS` 文件。

## 输出交付系统 (Output Delivery System)

可以使用 `ODS` 语句将输出发送到各种目标。

![](img/1698e3a97543d6895ff5297aae8fd042_610_0.png)

## 输出交付系统

| 目标 | 文件类型 | 查看位置 |
| --- | --- | --- |
| LISTING | | SAS 输出窗口或 SAS/GRAPH 窗口 |
| HTML | 超文本标记语言 | Internet Explorer 等网络浏览器 |
| PDF | 便携式文档格式 | Acrobat Reader 等 Adobe 产品 |
| RTF | 丰富文本格式 | Microsoft Word 等文字处理器 |

## 默认 ODS 目标

`LISTING` 目标是默认的 `ODS` 目标。

```
ods listing;
nproc freq data=orion.sales;
tables Country;
run;

proc gchart data=orion.sales;
hbar Country / nostats;
run;
```

## 默认 ODS 目标

`LISTING` 目标将输出定向到 OUTPUT 窗口和 GRAPH 窗口。

![](img/1698e3a97543d6895ff5297aae8fd042_612_0.png)

## 默认 ODS 目标

`ods LISTING CLOSE` 语句停止向 OUTPUT 窗口和 GRAPH 窗口发送输出。

```
ods listing close;

proc freq data=orion.sales;
tables Country;
run;

proc gchart data=orion.sales;
hbar Country / noostats;
run;
```

## 默认 ODS 目标

如果关闭了 `LISTING` 目标且没有其他活动的目标，SAS 日志中将出现警告。

## 部分 SAS 日志

```
23 ods listing close;
24
25 proc freq data=orion.sales;
26   tables Country;
27 run;

WARNING: No output destinations active.
NOTE: There were 165 observations read from the data set ORION.SALES.
```

## HTML, PDF 和 RTF 目标

HTML、PDF 和 RTF 等 `ODS` 目标以以下方式打开和关闭：

```
ODS destination FILE = '*filename.ext*' <options>;

用于生成报告(s)的 SAS 代码

ODS destination CLOSE;
```

`FILE=` 选项中指定的文件名取决于你的操作系统环境。

## 11-5 将输出重定向到外部文件

## HTML 目标

```
ods html file='myreport.html'; proc freq data=orion.sales; tables Country; ods html close;
```

![](img/1698e3a97543d6895ff5297aae8fd042_614_0.png)

在关闭目标之前，务必使用显式的步骤边界结束步骤。否则，文件将在步骤执行之前被关闭。

## PDF 目标

```
ods pdf file='myreport.pdf'; proc freq data=orion.sales; tables Country; ods pdf close;
```

![](img/1698e3a97543d6895ff5297aae8fd042_614_1.png)

## RTF 目标

```
ods rtf file='myreport.rtf';
proc freq data=orion.sales;
tables Country;
run;\ods rtf close;
```

![](img/1698e3a97543d6895ff5297aae8fd042_615_0.png)

传统的 `RTF` 目标不控制垂直测量，因此分页是由文字处理器控制的。从 SAS 9.2 开始有了一个新目标 `TAGSETS.RTF`，它可以控制垂直测量。关于 `TAGSETS.RTF` 目标的文档可以在 SAS 帮助（产品 -> SAS 9.2 输出交付系统 -> ODS 语句 -> TAGSETS.RTF）中找到。

## 测验 1.1

这个程序的问题在哪里？

```
ods pdf file='myreport.pdf';
proc freq data=orion.sales;
run;
```

## 单目标

输出仅发送到一个目标。

```
ods listing close;
ods html file='example.html';
proc freq data=orion.sales;
tables Country;
run;
ods html close;
```

在程序结束时打开 `LISTING` 目标是一个良好的习惯，以确保下次提交时开启。

## 多目标

输出可以发送到多个目标。

```
ods listing;
ods pdf file='example.pdf';
ods rtf file='example.rtf';
proc freq data=orion.sales;
tables Country;
run;
ods pdf close;
ods rtf close;
```

要查看结果，除 `LISTING` 以外的所有目标必须关闭。

## 多目标

在 `ODS CLOSE` 语句中使用 `ALL` 关闭包括 `LISTING` 在内的所有打开的目标。

```
ods listing;
ods pdf file='example.pdf';
ods rtf file='example.rtf';
proc freq data=orion.sales;
tables Country;
run;
ods all close;
ods listing;
```

## 多过程

来自多个过程的输出可以发送到 `ODS` 目标。
