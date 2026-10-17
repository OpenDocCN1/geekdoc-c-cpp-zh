
```sas
proc sort data=orion.sales out=work.sort;
by Country descending Gender_Name;
run;

proc freq data=work.sort;
tables Gender;
run;
```

## 11.11 测验 – 正确答案

这个程序有什么问题？

```sas
ods pdf file='myreport.pdf';
proc print data=orion.sales;
run;
ods pdf close;
```

## 11.12 投票 – 正确答案

你是否注意到两种样式定义在演示方面的差异？

- 是
- 否

第一组样式定义没有使用颜色。

第二组样式定义使用了颜色。

## 章节练习题的解答

章节练习解答

1. 哪些全局语句可以增强报告？

- `OPTIONS`
- `TITLE`
- `FOOTNOTE`
- `ODS`

2. 标题或脚注的最大行数是多少？

10

章节练习解答

3. 如何在 `PROC PRINT` 步骤的列标题中强制换行？

在 `PROC PRINT` 语句中使用 `SPLIT=` 选项，结合 `LABEL` 语句或永久标签。

4. 在 `PROC` 步骤和 `DATA` 步骤中使用 `FORMAT` 语句有什么区别？

在 `PROC` 步骤中使用 `FORMAT` 语句定义临时格式。在 `DATA` 步骤中使用 `FORMAT` 语句定义永久格式。

5. 如何为变量的值创建描述性标签（例如部门名称而不是部门代码）？

在 `PROC FORMAT` 中使用 `VALUE` 语句创建用户定义的格式。

# TABLES 语句

单向频数表生成频率、累计频率、百分比和累计百分比。

```sas
proc freq data=orion.sales;
tables Gender Country;
run;
```

| 性别 | 频率 | 百比 | 累计频率 | 累计百分比 |
| --- | --- | --- | --- | --- |
| M | 68 | 41.21 | 68 | 41.21 |
| | 97 | 58.79 | 165 | 100.00 |
| 国家 | 频率 | 百比 | 累计频率 | 累计百分比 |
| AU | 63 | 38.18 | 63 | 38.18 |
| US | 102 | 61.82 | 165 | 100.00 |

# TABLES 语句

多路频数表生成单元格频率、单元格百分比、行频率的百分比和列频率的百分比，以及总频率和百分比。

```sas
proc freq data=orion.sales;
tables Gender*Country;
run;
rows columns;
```

# TABLES 语句

FREQ 过程

| 性别 | | | 总计 |
|---|---|---|---|
| 频率 | 百比 | 行百分比 | 列百分比 AU | US | |
| F | 27 | 41 | 68 |
| | 16.36 | 24.85 | 41.21 |
| | 39.71 | 60.29 | |
| | 42.86 | 40.20 | |
| M | 36 | 61 | 97 |
| | 21.82 | 35.97 | 58.79 |
| | 37.11 | 62.89 | |
| | 57.14 | 59.80 | |
| 总计 | 63 | 102 | 165 |
| | 38.18 | 61.82 | 100.00 |

# 12.01 多项选择调查

下列哪个陈述**不能**被添加到 `PROC FREQ` 步骤中以增强报告？

- a. `FORMAT`
- b. `SET`
- c. `TITLE`
- d. `WHERE`

# 额外的 SAS 语句

可以添加额外的语句来增强报告。

```sas
proc format;
    value $ctryfmt 'AU'Australia'
           'US'=United States';
run;
options nodatepage=1;
ods html file='p12d01.html';
proc freq data=orion.sales;
    tables Job Title Gender=Country;
    where Job Title contains 'Rep';
    format Country $ctryfmt;
    title 'Sales Rep Frequency Report';
run;
ods html close;
```

![](img/1698e3a97543d6895ff5297aae8fd042_672_0.png)

# 额外的 SAS 语句

HTML 输出

销售代表频率报告

FREQ 过程

| 频率 百比 行百分比 列百分比 | 国家 澳大利亚 美国 总计 |
|---|---|---|---|---|
| F | | 27 | 40 | 67 |
| | 15.98 | 25.18 | 42.14 |
| | | 40.30 | 59.70 |
| | | 44.20 | 80.82 |
| M | | 34 | 58 | 92 |
| | 21.38 | 36.46 | 57.86 |
| | | 35.26 | 63.44 |
| | | 55.74 | 59.18 |
| 总计 | | 51 | 98 | 159 |
| | 36.36 | 61.64 | 100.00 |

![](img/1698e3a97543d6895ff5297aae8fd042_672_1.png)

# 抑制统计显示的选项

选项可以放在 `TABLES` 语句中的正斜杠之后，用以抑制默认统计数据的显示。

| 选项 | 说明 |
|---|---|
| `NOCUM` | 抑制累计频率和累计百分比的显示。 |
| `NOPERCENT` | 抑制百分比、累计百分比和总百分比的显示。 |
| `NOFREQ` | 抑制单元格频率和总频率的显示。 |
| `NOROW` | 抑制行百分比的显示。 |
| `NOCOL` | 抑制列百分比的显示。 |

# 抑制统计显示的选项

![](img/1698e3a97543d6895ff5297aae8fd042_673_0.png)

# 抑制统计显示的选项

| 性别 | 国家 | | | |
|---|---|---|---|---|
| 频率 百比 行百分比 列百分比 | `NOROW` 抑制 | `NOFREQ` 抑制总计 |
| F | AU 27 41 | 68 41.21 |
| | | `NOCOL` 抑制 | |
| M | 36 61 97 58.79 | `NOPERCENT` 抑制 | 21.82 36.97 |
| | | 37.11 62.89 |
| | | 57.14 59.80 |
| 总计 | 63 102 165 38.18 61.82 100.00 |

# 12.02 题

哪个 `TABLES` 语句正确创建了报告？

- a. `tables Gender nocum;`
- b. `tables Gender nocum nopercent;`
- c. `tables Gender / nopercent;`
- d. `tables Gender / nocum nopercent;`

| 性别 | 频率 |
|---|---|
| F | 68 |
| M | 97 |

# 额外的 TABLES 语句选项

额外的选项可以放在正 语句之后之后来控制输出。

| 选项 |  |
|---|---|
| `LIST` | 以列表格式显示多路表。 |
| `CROSSLIST` | 以列格式显示多路表。 |
| `FORMAT=` | 格式化多路表中的频率。 |

# LIST 和 CROSSLIST 选项

| 性别 | 国家 | 频率 | 百比 | 累计频率 | 累计百分比 |
|---|---|---|---|---|---|
| F | 澳大利亚 | 27 | 16.36 | 27 | 36.36 |
| F | 美国 | 41 | 24.85 | 68 | 41.51 |
| M | 澳大利亚 | 36 | 21.82 | 104 | 63.53 |
| M | 美国 | 61 | 37.18 | 165 | 100.00 |

# 性别的国家表

| 性别 | 国家 | 频率 | 百比 | 行百分比 | 列百分比 |
|---|---|---|---|---|---|
| F | 澳大利亚 | 27 | 16.36 | 39.71 | 42.86 |
| F | 美国 | 41 | 24.85 | 60.29 | 40.20 |
| 总计 | | 68 | 41.21 | 100.00 |
| M | 澳大利亚 | 36 | 21.82 | 37.11 | 57.14 |
| M | 美国 | 61 | 35.97 | 62.89 | 59.80 |
| 总计 | | 97 | 58.79 | 100.00 |

# FORMAT= 选项

部分 FREQ 输出

| 频率 百比 行百分比 列百分比 | 澳大利亚 美国 总计 |
|---|---|---|---|---|
| F | | 27 | 40 | 67 |
| | | | 15.98 | 25.18 | 42.14 |
| | | | 40.30 | 59.70 |
| | | | 44.20 | 80.82 |
| M | | 34 | 58 | 92 |
| | | | 21.38 | 36.46 | 57.86 |
| | | | 35.26 | 63.44 |
| | | | 55.74 | 59.18 |
| 总计 | | 51 | 98 | 159 |
| | | | 36.36 | 61.64 | 100.00 |

`tables Gender*Country;`

| 频率 百比 行百分比 列百分比 | 澳大利亚 美国 总计 |
|---|---|---|---|---|
| F | | | 27 | 41 | 68 |
| | | | 16.36 | 24.85 | 41.21 |
| | | | | 38.71 | 60.29 |
| | | | | 42.86 | 40.20 |

`tables Gender*Country / format=12;`

# PROC FREQ 语句选项

选项也可以放在 `PROC FREQ` 语句中。

| 选项 | 说明 |
|---|---|
| `NLEVEL` | 显示 `TABLES` 语句中指定的每个变量的级别数。 |
| `PAGE` | 每页仅显示一个表。 |
| `COMPRESS` | 如果空间足够，则在上一个表的同一页开始显示下一个单向频数表。 |

# NLEVELS 选项

```sas
proc freq data=orion.sales nlevels;
tables Gender Country Employee_ID;
run;
```

部分 PROC 输出

| 变量 | 级别 |
|---|---|
| `Gender` | 2 |
| `Country` | 2 |
| `Employee_ID` | 165 |

要显示级别数而不显示频率计数，在 `TABLES` 语句中添加 `NOPINT` 选项。

```sas
proc freq data=orion.sales nlevels;
tables Gender Country Employee_ID / noprint;
run;
```

要显示所有变量的级别数而不显示任何频率计数，在 `TABLES` 语句中使用 `_ALL_` 关键字和 `NOPINT` 选项。

```sas
proc freq data=orion.sales nlevels;
tables _all_ / noprint;
run;
```

# PAGE 选项

```sas
proc freq data=orion.sales;
tables Gender Country Employee_ID;
run;
page 1    page 1    pages 2-5
```

```sas
proc freq data=orion.sales page;
tables Gender Country Employee_ID;
run;
page 1    page 2    pages 3-6
```

# COMPRESS 选项

```sas
proc freq data=orion.sales;
tables Gender Country Employee_ID;
run;
page 1    page 1    pages 2-5
```

```sas
proc freq data=orion.sales compress;
tables Gender Country Employee_ID;
run
```

# 输出数据集 (自学)

`PROC FREQ` 使用两种不同的方法生成输出数据集：

- `TABLES` 语句配合 `OUT=` 选项创建包含频率和百分比的数据集。

```sas
TABLES variables / OUT=SAS-data-set <options>;
```

- `OUTPUT` 语句配合 `OUT=` 选项创建包含特定统计数据（如卡方统计量）的数据集。

```sas
OUTPUT OUT=SAS-data-set <options>;
```

# TABLES 语句 OUT= 选项 (自学)

`TABLES` 语句中的 `OUT=` 选项创建一个包含以下变量的输出数据集：

- `BY` 变量
- `TABLES` 变量
- 自动变量 `COUNT` 和 `PERCENT`
- 在 `TABLES` 语句选项中请求的其他频率和百分比变量

```sas
TABLES variables / OUT=SAS-data-set <options>;
```

如果在 `TABLES` 语句中出现多个表格请求，数据集的内容对应最后一个表格请求。

# TABLES 语句 OUT= 选项 (自学)

```sas
proc freq data=orion.sales noprint;
    tables Gender Country / out=work.freql;
run;

proc print data=work.freql;
run;
```

# PROC PRINT 输出

| Obs | Country | COUNT | PERCENT |
|---|---|---|---|
| 1 | AU | 63 | 38.1818 |
| 2 | US | 102 | 61.8182 |

`NOPRINT` 选项抑制所有输出显示。

# TABLES Statement OUT= 选项（自学）

在 `TABLES` 语句的正斜杠之后可以添加选项，以控制输出数据集中添加的额外统计信息。

| 选项 | 描述 |
| --- | --- |
| `OUTCUM` | 在输出数据集中为单向表包含累计频率和累计百分比。 |
| `OUTPCT` | 在多维频率表的输出数据集中包含列频率和行频率百分比。 |

# TABLES Statement OUT= 选项（自学）

```sas
proc freq data=orion.sales noprint;
  tables Gender Country / out=work.freq3
  outcum;
run;
proc print data=work.freq3;
run;
```

# PROC PRINT 输出

| Obs | Country | 计数 | 百分比 | 累计频率 | 累计百分比 |
| --- | --- | --- | --- | --- | --- |
| 1 | AU | 63 | 38.182 | 63 | 38.182 |
| 2 | US | 102 | 61.818 | 165 | 100.000 |

# TABLES Statement OUT= 选项（自学）

```sas
proc freq data=orion.sales noprint;
    tables Gender*Country / out=work.freq4
    outpct;

run;

proc print data=work.freq4;
    run;
```

# PROC PRINT 输出

| Obs | Gender | Country | 计数 | 百分比 | 行百分比 | 列百分比 |
|---|---|---|---|---|---|---|
| 1 | F | AU | 27 | 16.3638 | 39.7059 | 42.8571 |
| 2 | F | US | 41 | 24.8485 | 60.2941 | 40.1961 |
| 3 | M | AU | 36 | 21.8182 | 37.1134 | 57.1429 |
| 4 | M | US | 61 | 36.9697 | 62.8866 | 59.8039 |

![](img/1698e3a97543d6895ff5297aae8fd042_682_0.png)

# OUTPUT Statement OUT= 选项（自学）

`OUTPUT` 语句中的 `OUT=` 选项创建一个包含以下变量的输出数据集：

- `BY` 变量
- `TABLES` 语句中请求的变量
- 包含指定统计信息的变量。

```sas
OUTPUT OUT=SAS-data-set <options>;
```

如果 `TABLES` 语句中出现多个表格请求，则数据集的内容对应于最后一个表格请求。

# OUTPUT Statement OUT= 选项（自学）

为了指定输出数据集包含特定的统计数据量，你必须在 `TABLES` 语句中使用相应的选项，让 `PROC FREQ` 计算该统计数据量。

```sas
proc freq data=orion.sales;
tables Country / chisq;
output out=work.freq5 chisq;
run;

proc print data=work.freq5;
run;
```

`CHISQ` 请求卡方检验和基于卡方的关联性量。

![](img/1698e3a97543d6895ff5297aae8fd042_683_0.png)

# OUTPUT Statement OUT= 选项（自学）
