

注释（Annotation）技术可用于自定义使用 GPLOT、GCHART 和其他类似过程创建图表。在这种技术中，你创建一个包含图形命令的注释数据集（Annotation Data Set），然后将这些命令应用于现有的图表（或创建一个完全自定义的图表）。

GTL 是用于指定 ODS 图表创建细节的 SAS 子语言。每个 ODS 图表都有一个默认模板，这些 GTL 命令就位于其中。你可以编辑此模板语言，以对图表进行定制，以满足特定需求。

这两种技术都超出了本书的范围，但如果你想更深入探索 SAS 图表的功能，可以在 SAS 文档中找到关于这些技术的更多信息。

## 18.10 总结

本章描述了 SAS 中提供的许多图形选项中的一小部分。然而，本章对图表（以及书中其他部分）的讨论涵盖了数据分析中常用的许多图表。

## 练习题

### 18.1 绘制均值比较图。

使用文件 AANOVA1.SAS 中的数据和由 AGRAP9.SAS 所示的示例，创建一个以条状图显示均值并带有标准误差标记的图表。

### 18.2 显示比较箱线图。

以 AGRAP9.SAS 为指南，为 CARS 数据集创建按 CYLINDERS（CYLINDERS > 1）分组的 CITYMPG 比较箱线图。

```
OPTIONS RESET=ALL;
PROC SORT DATA=C:\SASDATA\CARS OUT=MPFILE;
  BY;
PROC
  PLOT DATA=MPFILE;
    *CYLINDERS;
  WHERE CYLINDERS GT;
RUN;
QUIT;
```

### 18.3 使用交互式 ODS 图。

- a. 打开 AGRAP11.SAS。将图表类型从 HBAR 改为 PIE 并运行程序。测试 HTML 链接是否有效。
- b. 将图表类型改为 VBAR 并运行程序。测试 HTML 链接是否有效。
- c. 将图表类型改为 VBAR3D 并运行程序。测试 HTML 链接是否有效。
- d. 同样，尝试 BLOCK、HBAR3D、PIE3D 和 STAR 图表类型。

### 18.4 使用 SGPLOT 创建散点图。

使用下方的 SGPLOT 骨代码，显示 X=HWYMPG 和 Y=CITYMPG 的散点图，并在散图中拟合一条带有单个置信限（CLI）的回归线。

```
PROC SGPLOT DATA="C:\SASDATA\CARS";nSCATTER X=CITYMPG Y=;
YAXIS LABEL="City"
YAXIS;
REG X=Y=HWYMPG / CLI;
TITLE "SGPLOT Scatter Plot for Miles Per Gallon"
RUN;
```

## 19 创建自定义报告

学习目标

- 能够使用 PROC TABULATE 创建自定义报告
- 能够使用 PROC REPORT 创建自定义报告
- 能够使用 DATA 创建自定义报告

在整本书中，PROC PRINT 和 PROC FREQ 等过程被用于生成数据的简单摘要。然而，这些过程具有局限性。本章介绍了两个高级报告过程，旨在帮助你创建专业的报告。

### 19.1 使用 PROC TABULATE

PROC TABULATE 用于制作摘要表。与 PROC FREQ 不同，它可以处理行和列中的多个层级。你可以使用 PROC TABULATE 创建专业且达到出版标准的表格。PROC TABULATE 的简写语法如下：

```
PROC TABULATE <options>;
CLASS variables / options;
VAR variables / options;
TABLE row=column / options;
RUN;
```

PROC TABULATE 的基本构建模块是 TABLE、CLASS 和 VAR 语句。

TABLE 语句：该语句是 PROC TABULATE 中最重要的组件。它用于定义表格中显示哪些信息。例如，这个简单的 PROC TABULATE 语句定义了类变量 (GP) 和一个表格。

```
PROC TABULATE DATA=dataset;
CLASS GP;
TABLE GP;
RUN;
```

Class 语句：该语句识别用于表格的分类变量。你必须在 TABLE 语句之前识别你将要使用的变量。上面的 TABLE 语句告诉过程使用 GP 变量创建一个表格。

Var 语句：VAR 语句识别定量（数值型）数据。该变量用于指示表格单元格中的摘要统计量，如均值、总和或中位数。例如，

```

 NAME1 NAME2;
VAR OBS;
TABLE NAME1, NAME2*MEAN OBS;
```

此代码中添加的 MEAN 告诉过程将 OBS 的均值按 NAME1 和 NAME2 变量放在每个单元格中。PROC TABULATE 的这些构建模块将在接下来的系列操作示例中进行说明。

在进行接下来的练习之前，了解一下所使用数据集 MYSASLIB.REGION 会很有帮助。要查看 SAS 数据集的前几记录，请运行以下 PRINT 代码。

```
PRINT DATA=MYSASLIB.REGION(OBS=20);
```

结果将显示在表 19.3 中。

### 表 19.3 Regions 数据集

| Obs | REGION | AREA | SITE | MONTH | SALES_K |
|---|---|---|---|---|---|
| 1 | | | | | |
| 2 | | | | | |
| 3 | | | | | |
| 4 | | | | | |
| 5 | | | | | |
| 6 | | | | | |
| 7 | | | | | |
| 8 | | | | | |
| 9 | | | | | |
| 10 | | | | | |
| 11 | | | | | |
| 12 | | | | | | |
| 13 | | | | | | |
| 14 | | | | | | |
| 15 | | | | | | |
| 16 | | | | | | |
| 17 | | | | | | |
| 18 | | | | | | |
| 19 | | | | | | |
| 20 | | | | | | |

（注：此处为占位符，实际输出应根据数据集内容填充）

### 表 19.3 Regions 数据集（续）

| Obs | REGION | AREA | SITE | MONTH | SALES_K |
|---|---|---|---|---|---|
| 11 | | W | | | | |
| 12 | | W | | | | |
| 13 | | N | | | | |
| 14 | | N | | | | |
| 15 | | N | | | | |
| 16 | | S | | | | |
| 17 | | S | | | | |
| 18 | | S | | | | |
| 19 | | E | | | | |
| 20 | | E | | | | |

（注：此处为占位符，实际输出应根据数据集内容填充）

### 表 19.1 PROC TABULATE 的常用选项

| 选项 | 解释 |
|---|---|
| DATA=datename | 指定输入数据集 |
| OUT=datename | 指定输出数据集 |
| STYLE=stylename | 指定 ODS 样式 |
| FORMAT=option | 指定变量的显示格式 |
| ORDER=option | 指定排序方式 |
| MISSING=option | 指定缺失值如何被处理 | 

### 表 19.2 PROC TABULATE 的常用语句

| 语句 | 解释 |
|---|---|
| VAR variables; | 识别用于计算统计量的定量变量 |
| CLASS variables; | 识别用于表格分类的分类变量 |
| TABLE specification; | 定义表格的结构和显示内容 |
| RUN; | 结束并执行过程 过程 |
| BY, LABEL, WHERE, FREQ | 这些语句在大多数过程中是通用的 |

