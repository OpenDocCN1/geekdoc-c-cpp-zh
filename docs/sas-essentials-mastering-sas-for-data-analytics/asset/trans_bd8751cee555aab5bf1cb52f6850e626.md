

# 表 9.2 PROC MEANS 统计关键字

| 选项 | 含义 |
|---|---|
| CLM | 双侧置信区间 |
| CSS | 修正后的平方和 |
| CV | 变异系数 |
| KURTOSIS | 峰度 |
| LCLM | 下置信限 |
| MAX | 最大值（最大） |
| MEAN | 算术平均值 |
| MEDIAN (P50) | 第50百分位数 |
| MIN | 最小值（最小） |
| MODE | 数态 |
| N | 观测值数量 |
| NMISS | 缺失值数量 |
| P1 | 第1百分位数 |
| P5 | 第5百分位数 |
| P10 | 第10百分位数 |
| P90 | 第90百分位数 |
| P95 | 第95百分位数 |
| P99 | 第99百分位数 |
| PROBT | 与选项相关的 t 检验 p 值 |
| Q1 (P25) | 第1分位数 |
| Q3 (P75) | 第3分位数 |
| QRANGE | 四分位距 |
| RANGE | 范围 |
| SKEW (SKEW) | 偏度 |
| STDDEV (STD) | 标准差 |
| STDERR | 标准误 |
| SUM | 观测值总和 |
| SUMWT | WEIGHT 变量的总和 |
| T |  的 t 值 |
| UCLM | 上置信限 |
| USS | 未修正的平方和 |
| VAR | 方差 |

## 9.1.2 PROC MEANS 常用语句

与 PROC MEANS 相关的语句出现在初始 PROC MEANS 语句的分号之后。表 9.3 列出了 PROC MEANS 的常用语句。欲更多信息，请参阅 SAS 文档。以下示例说明了 PROC MEANS 选项和语句的使用：

- * 最简单的调用 - 针对所有数值变量 *;
PROC MEANS;

- * 指定的统计量和变量 *;
PROC MEANS N MEAN STD;
VAR SODIUM CARBO;

# 第 9 章：评估定量数据

# 表 9.3 PROC MEANS 常用语句

| 语句 | 含义 |
| --- | --- |
| VAR variable(s); | 识别一个或多个要分析的变量。可以是任何标准 SAS 变量列表，如 AGE SBP GENDER，或范围如 TIME1-TIME10 |
| CLASS variable(s); | 指定用于将数据分组为分类级的变量 |
| OUTPUT OUT=dataname; | 指定一个 SAS 输出数据集，其中包含 PROC MEANS 计算的统计量。OUTPUT OUT=SAS-data-set；若要指定特定变量的输出名称，使用以下格式：OUTPUT=<SAS-data-set> statistic-keyword-n-name(s) ... <percentiles-specification>; |
| FREQ weight variable; | 指定代表观测值计数的变量 |
| BY, FORMAT, LABEL, WHERE | 这些语句是大多数过程共，可以在此处使用 |

- * 使用 BY 语句在单独表格中进行子组描述统计；
PROC SORT; BY GENDER;RUN;
PROC MEANS; BY GENDER;
VAR FAT PROTEIN SODIUM;

- * 使用 CLASS 语句在同一张表中进行子组描述统计；
PROC MEANS; CLASS GENDER;
VAR FAT PROTEIN SODIUM;

# 动手实例

在本示例中，你将学习如何使用 PROC MEANS 中的一些基本选项。假设你有一个关于几个儿童测量值（体重、身高和年龄）的数据集。你将使用 PROC MEANS 执行以下任务：

- * 报告简单的描述统计。
- * 将输出限制为两位小数。
- * 请求选定的统计量列表。

1. 打开程序文件 ANS1.SAS。

```
DATA CHILDREN;
INPUT WEIGHT HEIGHT AGE;
DATALINES;
```

```
64 57 8
71 59 10
53 49 6
67 62 11
55 51 8
58 50 8
77 55 10
57 48 9
56 42 10
51 42 6
76 61 12
68 57 9

; PROC MEANS DATA=CHILDREN;TITLE 'PROC MEANS, simplest use';RUN;PROC MEANS MAXDEC=2; VAR HEIGHT;TITLE 'PROC MEANS, limit decimals';RUN;PROC MEANS MAXDEC=2 N STDERR; VAR HEIGHT;TITLE 'PROC MEANS, statistics to report';RUN;
```

# 9.4 PROC MEANS 输出

PROC MEANS, simplest use

| 变量 | N | 平均值 | 标准差 | 最小值 | 最大值 |
|---|---|---|---|---|---|
| HEIGHT | 12 | 62.750000 | 8.986194 | 51.000000 | 77.000000 |
| HEIGHT | 12 | 62.750000 | 6.824084 | 42.000000 | 62.000000 |
| AGE | 12 | 8.916667 | 1.831954 | 6.000000 | 12.000000 |

# PROC MEANS, limit decimals, specify variables

The Means Procedure

| 变量 | N | 平均值 | 标准差 | 最小值 | 最大值 |
|---|---|---|---|---|---|
| WEIGHT | 12 | 62.75 | 8.99 | 51.00 | 77.00 |
| HEIGHT | 12 | 52.75 | 6.82 | 42.00 | 62.00 |

# PROC MEANS, specify statistics to report

The Means Procedure

| 变量 | N | 平均值 | 标准误 | 中位数 |
|---|---|---|---|---|
| WEIGHT | 12 | 62.75 | 2.59 | 61.00 |
| HEIGHT | 12 | 52.75 | 1.97 | 53.00 |

(续)

- 运行程序并观察表 9.4。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

## 9.1.3 使用 BY 和 CLASS 语句

使用 BY 和 CLASS 语句是常见的。使用 BY 和 CLASS 比较均值。以下示例显示了：

- 在第一个输出表中，统计量保留到七位小数。注意以下内容：

## 9.1.4 从 PROC MEANS 提取统计量

PROC MEANS 允许你将统计量捕获到一个新的 SAS 数据文件中，你可以在另一个 DATA 步或过程中使用。OUTPUT 语句用于指定输出数据集的名称。该语句的语法为

```
OUTPUT OUT=filename <varname>;
```

你可以指定多个统计量和名称，或者省略名称如 MEAN=. 。例如，

```
PROC MEANS DATA="C:\SASDATA\SOMEDATA";
OUTPUT=TIMEMEAN MEAN=T1;
VAR TIME1;
RUN;
```

将 TIME1 的均值输出到名为 TIMEMEAN 的 sas 数据集，并赋予其 SAS 变量名 T1。

