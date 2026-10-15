

**显示 2.11（续）**

|  | 城市 | JanTemp | JulyTemp | RelHum | pop | pop_per_house | income |
|---|---:|---:|---:|---:|---:|---:|---:|
| 22 | Grand Rapids, MI | 24 | 72 | 61 | 601680 | 3.37 | 29915 |
| 23 | Greensboro-Winston-Salem-High Point, NC | 40 | 77 | 53 | 851851 | 3.45 | 29450 |
| 24 | Hartford, CT | 27 | 72 | 56 | 715923 | 3.25 | 37565 |
| 25 | Houston, TX | 55 | 84 | 59 | 2735766 | 3.35 | 39558 |

### 2.2.5 直接读取 Excel 电子表格

虽然可以将 Excel 文件保存为逗号分隔值文件，并使用上一节中的方法读取，但如果无需进行数据操作 gymnastics，直接读取数据总是更容易的。如果你的计算机上已许可 SAS/ACCESS 软件，则用于读取 Excel 文件和其他文件（如关系数据库）的引擎可在 LIBNAME 语句中使用。此外，导入向导使你能够选择一个 Excel 文件并将其读入 SAS 数据集。两种读取 Excel 文件的方法的代码均显示在显示 2.12 中。

**显示 2.12 使用 PROC IMPORT 或指定 EXCEL 引擎的 LIBNAME 语句导入 Excel 电子表格**

```
/* Assumes SAS/ACCESS engines are available */
/* IMPORT code produced by the IMPORT WIZARD */

PROC IMPORT OUT= WORK.DASL_FROM_EXCEL2
    DATAFILE= "C:\Documents and Settings\baileraj\Desktop\DASL-SMSA.xls"
    DBMS=EXCEL REPLACE;
    SHEET="Sheet15";
    GETNAMES=YES;
    MIXED=NO;
    SCANTEXT=YES;
    USEDATE=YES;
    SCANTIME=YES;
RUN;

/* ... via EXCEL engine with LIBNAME */
options nodate;
title ;

libname spreads excel
"C:\Documents and Settings\baileraj\Desktop\DASL-SMSA.xls" header=yes;

ods rtf bodytitle file='C:\Users\baileraj.IT\Desktop\ch2-fig2.12.rtf';
/* list the contents of the spreadsheet that was read */
proc contents data=spreads._all_ varnum;
run;

/* set contents of the 1st worksheet to SAS data set */
data DASL_from_Libname_Excel_engine;
set spreads.'sheet1$'n;
run;

proc print data=DASL_from_Libname_Excel_engine;
run;
ods rtf close;
```

**显示 2.13 使用 LIBNAME 语句指定 EXCEL 引擎引用 Excel 电子表格时产生的 SAS 库内容**

| 目录 |  |
|---|---|
| Libref | SPREADS |
| Engine | EXCEL |
| Physical Name | C:\Documents and Settings\baileraj\Desktop\DASL-SMSA.xls |
| Schema/Owner | Admin |

| # | 名称 | 成员类型 | DBMS 成员类型 |
|---|---|---|---|
| 1 | Sheet1$ | DATA | TABLE |
| 2 | Sheet2$ | DATA | TABLE |
| 3 | Sheet3$ | DATA | TABLE |

| 数据集名称 | SPREADS.'Sheet1$'n | 观测数 |  |
|---|---|---|---|
| 成员类型 | DATA | 变量数 | 17 |
| Engine | EXCEL | 索引 | 0 |
| 创建 | . | 观测长度 | 0 |
| 最后修改 | . | 已删除观测 | 0 |
| 保护 |  | 压缩 | NO |
| 数据集类型 |  | 已排序 | NO |
| 标签 |  |  |  |
| 数据表示 | Default |  |  |
| 编码 | Default |  |  |

### 按创建顺序排列的变量

| # | 变量 | 类型 | Len | 格式 | Informat | 标签 |
|---:|---|---:|---|---|---|---|
| 1 | city | Char | 39 | $39. | $39. | city |
| 2 | JanTemp | Num | 8 |  |  | JanTemp |
| 3 | JulyTemp | Num | 8 |  |  | JulyTemp |
| 4 | RelHum | Num | 8 |  |  | RelHum |
| 5 | Rain | Num | 8 |  |  | Rain |
| 6 | Mortality | Num | 8 |  |  | Mortality |
| 7 | Education | Num | 8 |  |  | Education |
| 8 | PopDensity | Num | 8 |  |  | PopDensity |
| 9 | _NonWhite | Num | 8 |  |  | %NonWhite |
| 10 | _WC | Num | 8 |  |  | %WC |
| 11 | pop | Num | 8 |  |  | pop |
| 12 | pop_per_house | Num | 8 |  |  | pop/house |
| 13 | income | Num | 8 |  |  | income |
| 14 | HCPot | Num | 8 |  |  | HCPot |
| 15 | NOxPot | Num | 8 |  |  | NOxPot |
| 16 | SO2Pot | Num | 8 |  |  | SO2Pot |
| 17 | NOx | Num | 8 |  |  | NOx |

显示 2.13 包含了电子表格在 SAS 库中的内容，如同其出现的那样。每个工作表在 SAS 中成为一个单独的数据集。只有 Sheet1$ 填充了数据；其他两个电子表格为空。有趣的是，Excel 列标签如果也是有效的 SAS 变量名，则会被分配 SAS 变量名作为其标签。无法映射到有效 SAS 变量名的 Excel 列（例如 %WC）会被修改为具有有效的 SAS 名称，通过用下划线替换百分号（例如 _WC）。Excel 列标题在 IMPORT 过程中被分配为变量的标签。

### 2.2.6 读取 SPSS 数据文件——那个能干的小 SPSS 引擎

之前描述的 IMPORT 过程可使用 DBMS=SPSS 选项读取 SPSS 数据集。或者，你可以指定带有 SPSS 引擎的 LIBNAME 语句。由于此信息与上一节的信息平行，证明其有效性的工作留给读者。（我一直想在论文或报告中写下这句话。）

## 2.3 写入文件或制作简单报告

本章从强调将数据导入 SAS 开始。下一节讨论生成分析数据集并通过添加观测值（连接数据集或向数据集添加行）和添加变量（合并数据集或向数据集添加列）来更改它。本节讨论如何将用于从外部文件创建 SAS 数据集的一些思想反转，以写入或创建供其他程序分析的数据集，或构建简单报告。

PUT 语句可以被视为 INPUT 语句的输出类比。它指定变量的值、文本等应如何写入。如果指定了文件名，则 PUT 语句写入此位置。如果未指定，则 PUT 语句写入 SAS 日志。PUT 语句用于回显 SAS 数据集中所有变量的值。_NULL_ 数据集用于允许在 DATA 步编程而不存储数据集。_ALL_ 指定选择所有变量以显示。诸如 _NUMERIC_ 或 _CHARACTER_ 之类的替代指定选择与数据类型相对应的所有变量。以下语句写入文本字符串 `'-'` 50 次：

```
put 50*'-';
```

**显示 2.14 使用 PUT 语句回显数据集中的变量值**

```
libname myfiles "C:\Users\baileraj.IT\BAILERAJ\Classes\Web-CLASSES\sta402\data";

proc sort data=myfiles.nitrofen;
  by conc;
run;

data _null_; set myfiles.nitrofen; by conc;
  if FIRST.CONC then do; * first observation in concentration group;
    put 50*"-";           * add separator line of 50 dashes + column headings;
    put "Animal" @10 "Conc" @20 "Total" @30 "First?" @40 "Last?";
  end;
  put animal @10 conc @20 total @30 FIRST.CONC @40 LAST.CONC;

* put _all_;  /* useful to check values during input */
run;
```

除了生成报告外，显示 2.14 还介绍了在操作已排序数据集时有用的两个指示变量——FIRST.VARNAME 和 LAST.VARNAME，其中 VARNAME 是用于对数据集排序的 SAS 变量的名称。这两个指示变量是在使用 BY CONC 将 nitrofen 数据集的内容添加到 _NULL_ 数据集时定义的（FIRST.CONC 和 LAST.CONC）。这些变量指示当前观测是否为 BY 变量 CONC 的每个级别的第一或最后观测。如显示 2.15 所示，CONC=0 条件中的第一个观测——动物 1——具有 FIRST.CONC=1（TRUE）和 LAST.CONC=0（FALSE）。动物 2 到 9 具有 FIRST.CONC=0 和 LAST.CONC=0。CONC=0 条件中的最后一个观测——动物 10——具有 FIRST.CONC=0 和 LAST.CONC=1。此程序在它是浓度组中的第一个动物时（即当 FIRST.CONC=1 时）写入一条由破折号组成的分隔线和列标题。@# 指定变量值或列标题应从第 # 列开始打印。

**显示 2.15 SAS 日志中 nitrofen 变量值的回显**

| Animal | Conc | Total | First? | Last? |
|---:|---:|---:|---:|---:|
| 1 | 0 | 77 | 1 | 0 |
| 2 | 0 | 83 | 0 | 0 |
| ... | ... | ... | ... | ... |
| 9 | 0 | 74 | 0 | 0 |
| 10 | 0 | 81 | 0 | 1 |
| ... | ... | ... | ... | ... |
| Animal | Conc | Total | First? | Last? |
| 41 | 310 | 6 | 1 | 0 |
| 42 | 310 | 6 | 0 | 0 |
| ... | ... | ... | ... | ... |
| 49 | 310 | 6 | 0 | 0 |
| 50 | 310 | 5 | 0 | 1 |

