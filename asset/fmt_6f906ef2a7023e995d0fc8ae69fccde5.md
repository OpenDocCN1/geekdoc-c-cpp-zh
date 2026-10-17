
```sas
%INCLUDE C:\SASDATA\KW_MC.SAS;
DATA NPAR;
INPUT GROUP WEIGHT @@;
DATALINES;
1 50.8 157.0 144.6 51.7 48.2 51.3 149.0
2 68.7 267.2 66.3 69.8 66.9 65.2 62.0
3 82.6 374.1 80.5 80.3 81.5 78.6 76.1
4 76.9 472.2 73.7 74.2 70.6 75.3 69.8
;
* 使用 SAS 宏 KW MC 的起始信息
%LET NUMGROUPS=4;
%LET DATAMAME=NPAR;
%LET OBSVAR=WEIGHT;
%LET GROUP=GROUP;
%LET ALPHA=0.05;
Title "Kruskal-Wallis Multiple Comparisons"
****************************************************
调用 KW MC 宏
****************************************************
%KW MC (source=&DATAMAME, groups=&NUMGROUPS, obsname=&OBSVAR, gpname=&GROUP, sig=&alpha);
```

此程序使用的数据集与之前关于随机分配到四种处理的动物增重的 KW 示例中的数据集相同。

# 第 15 章：非参数分析

一系列 `LET` 语句用于指定 SAS 宏所需的某些参数的 SAS 宏值。在这种情况下，组数 `NUMGROUPS` 为 4。包含用于分析数据的数据集名为 `NPAR`。因变量是 `WEIGHT`，分组变量命名为 `GROUP`。用于执行检验的显著性水平由 `ALPHA=.05` 指示。

以 `%KW_MC(source=)` 开头的语句是“调用” SAS 宏的语句。若要将该宏用于任何其他数据，你不需要更改此语句的任何内容。如果你将此过程用于其他分析，你必须更改的项目是 `%LET` 语句中的四个值。

- 2. 运行程序并观察结果。KW 结果与上一个示例中的相同。多重比较检验的结果见表 15.5。

表 15.6 显示了一系列多重比较检验的结果。该检验被称为 Dunn 检验，与第 13 章：方差分析中所示的 Tukey 多重比较程序相似。在 0.05 显著性水平下进行检验。例如，检验表明，对于组 3 和组 1 的比较，我们拒绝两组来自同一分布的零假设。对于组 3 和组 2 的比较也得相同的结论。因此，基于此检验的结论是：组 3 的体重增加与组 1 和组 2 不同，但与组 4 无异。组 4 的体重增加与组 1 有显著差异，但与组 2 无差异。最后，组 2 的体重增加与组 1 无异。SAS 还显示了并排箱线图，与图 15.1 相同。该图提供了视觉确认，证明治疗 3 优于治疗 1 和治疗 2，这是根据第 13 章使用相同数据集的实践示例得出的结论。

表 15.6 Kruskal–Wallis 分析的多重比较检验

| 比较 (Compare) | 差异 (Diff) | 标准误 (SE) | q | q(0.05) | 结论 (Conclude) |
|---|---|---|---|---|---|
| 3 vs 1 | 20.43 | 4.4 | 4.64 | 2.638 | 拒绝 (Reject) |
| 3 vs 2 | 13.36 | 4.4 | 3.04 | 2.638 | 拒绝 (Reject) |
| 3 vs 4 | 5.93 | 4.4 | 1.35 | 2.638 | 不拒绝 (Do not reject) |
| 4 vs 1 | 14.5 | 4.4 | 3.2 | 2.638 | 拒绝 (Reject) |
| 4 vs 2 | 7.43 | 4.4 | 1.69 | 2.638 | 不拒绝 (Do not reject) |
| 2 vs 1 | 7.07 | 4.4 | 1.61 | 2.638 | 不拒绝 (Do not reject) |

组大小不等，或存在某些秩并列。已执行 Dunn 检验，alpha = 0.05；比较组 = `GROUP`。

> 参考文献：生物统计学分析，第 4 版，J. Zar，2020。

## 15.6 总结

本章介绍了了几种替代标准参数分析的非参数替代方案。当正态性假设存疑时，这些过程非常有用，在样本量较小时尤为重要。

## 练习题

### 15.1 运行中位数检验

- a. 使用 `ANPAR2.SAS` 中的 SAS 程序，将选择从 Wilcoxon (KW) 检验更改为中位数检验，如下：

```
PROC NPAR1WAY MEDIAN;
```

- b. 运行程序并观察结果。结果有差异吗？

### 15.2 运行非参数分析

一家零售连锁店希望停止其位于科罗拉多州丹佛市的 11 家门店的损耗。通过盗窃导致的货物损失。管理层认为，在入口处配备一名制服警察将震慑盗窃。11 家门店中随机选择了 6 家门店让警察驻守一个月。在下个月，这些警察被分配到其他 5 家门店驻守一个月。在每个月底确定损耗情况，得出表 15.7 中的数据。注意：所选的两个月的每月销售量大致相同。

- a. 编写一个 SAS 程序使用适当的过程分析这些数据。从以下代码开始：

```
DATA STORE;
INPUT STORE $ WITHOUT WITH;
DIFF=WITH-WITHOUT
001 1.3 .9
002 .9 .46
...;
PROC VAR;
RUN;
```

- b. 观察输出并做出决策。是否有证据表明在警察在场时损耗较低？

表 15.7 门店损耗（单位：千）

| 门店编号 (Store Number) | 无警察 (Without Officer) | 有警察 (With Officer) |
|---|---|---|
| 001 | 1.3 | .9 |
| 002 | .9 | .46 |
| 003 | 2.6 | 2.5 |
| 004 | 8.2 | 4.1 |
| 005 | 2.2 | 2.1 |
| 006 | 0.89 | 0.9 |
| 007 | 1.6 | 1.5 |
| 008 | 2.4 | 2.2 |
| 009 | 3.2 | 1.1 |
| 010 | 0.5 | 0.4 |
| 011 | 1.1 | 0.5 |

# 16 逻辑回归

## 学习目标

- 能够使用 `PROC LOGISTIC` 执行逻辑回归
- 能够创建一个执行简单逻辑回归的 SAS 程序
- 能够创建一个执行多因素逻辑分析的 SAS 程序
- 能够使用 SAS 评估模型的拟合程度和预测能力

二分类逻辑回归模型基于只能取两个值的因变量，例如疾病的出现或缺席、死亡或未死亡、已婚或未婚。在这种情况下，自变量被用于预测结果发生的概率。逻辑回归模型有时称为 logit 模型。

## 16.2 使用 PROC LOGISTIC 进行逻辑回归分析

`PROC LOGISTIC` 是允许你使用二分类模型对数据进行分析 SAS 过程。该语句的简写语法如下：

```
PROC LOGISTIC < options >;
CLASS variables;
MODEL dependentvar < (variable_options) > =
< independentvars > / options ;
```

`PROC LOGISTIC` 和 `MODEL` 语句是必须的，且一次只能指定一个 `MODEL` 语句。`CLASS` 语句如果使用必须在 `MODEL` 语句之前。请注意，因变量必须是二分类的。为了简单起见，本章中的所有示例都使用取值为 0 或 1 的响应变量。

默认情况下，SAS 假设逻辑回归方程中的结果对应于因变量为 0 的情况。例如，如果你有一个名为 `DISEASE` 的变量，其中 `DISEASE=0` 表示疾病不存在，`DISEASE=1` 表示疾病存在，那么 SAS 默认将返回“疾病不存在”的概率。

表 16.1 列出了与 `PROC LOGISTIC` 一起常用的选项和语句。

`MODEL` 语句是逻辑过程的核心。它指定了因变量以及自变量。对于：

```
MODEL DEPVAR = INDVAR1 INDVAR2/options;
```

如前所述，在本章中因变量将始终是二分类的。这种因变量通常编码为 0 和 1，但该变量也可以取任何两个值，例如 1 和 2、A 和 B、存活和死亡等。

由于逻辑模型是基于预测事件的，因此必须考虑 `DEPVAR` 是如何设置。默认情况下，SAS 基于因变量的最小值进行预测。因此，如果你的因变量是 `FAIL`，其中 0 表示失败，1 表示成功，SAS 默认将对 `FAIL=0` 进行建模预测。要反转因变量，请使用 `DESCENDING` 选项。当在 `PROC LOGISTIC` 语句中包含该选项时，将对 `FAIL=1` 进行建模而非 `FAIL=0`。选择模型值的另一种方法是在 `MODEL` 语句中显式定义它。对于：

```
MODEL FAIL(EVENT='1') = independentvars;
```

这将导致 SAS 使用 1 作为因变量 `FAIL` 的模型值。`EVENT=` 选项被指定为“响应选项”。当响应是二分类时，`EVENT= FIRST` 或 `EVENT= LAST` 指定使用第一个或最后一个排序的值作为预测事件。你可以在引号中指定一个值。我们建议你如果需要，选择 `DESCENDING` 选项或 `EVENT=` 选项来指定要预测的响应变量值。

与之前几个章节中的 model 语句一样，因变量出现在等号左侧，自变量出现在右侧。

### 表 16.1 PROC LOGISTIC 常用选项

| 选项 | 解释 |
| :--- | :--- |
| `DATA = dataname` `DESCENDING` | 指定要使用的数据集，并反转响应变量层级的排序顺序。默认情况下，该过程将预测对应于二分类变量较小的值。因此，如果因变量取值为 0 和 1，除非使用 `DESCENDING` 选项，否则 SAS 默认预测因变量为 0 的概率。 |
| `EVENT='option'` | 指定二分类响应变量的哪个值被视为建模值。例如，`MODEL` 语句等号左侧 `DEATH='Event'`。 |
| `ALPHA= value` `NOPRINT` | 指定显著性水平、置信限，抑制输出 |
| `SIMPLE` `PLOTS= option` | 显示描述性统计。在 SAS 的当前视图中，默认显示优势比。使用 `PLOTS=NONE` 抑制此图。`PLOTS=ALL` 产生多个图表。 |

### PROC LOGISTIC 常用语句

| 语句 | 解释 |
| :--- | :--- |
| `MODEL devar=indvar(s);` | 指定因变量=自变量(s)。 |
| `CLASS variable;` | 指定分类变量。 |
| `BY variable;` | 按变量分组。 |
| `FORMAT variable=format;` | 指定变量的格式映射。 |
| `OUTPUT=name;` | 输出到数据集。 |
| `OUTROC=name` | 输出 ROC 曲线。 |

### 16.2 MODEL 语句常用选项

| 选项 | 解释 |
| :--- | :--- |
| `SELECTION=type` | 指定变量选择方法，例如 `STEPWISE`, `BACKWARD`, 和 `FORWARD`。 |
| `SLENTRY=value` | 指定进入变量的显著性水平。默认 0.05。 |
| `SLSTAY=value` | 指定移除变量的显著性水平。默认 0.1。 |
| `EVENT=option` | 指定二分类响应变量的哪个值被视为建模值。 |
| `DESCENDING` | 反转默认预测方向。 |
| `ALPHA= value` | 指定显著性水平。 |
| `NOPRINT` | 抑制输出。 |
| `PLOTS= option` | 指定绘图选项。 |
| `LACKFIT` | 请求拟合检验。 |
| `RISIMITS` | 请求优势比的置信区间。 |
| `CTABLE` | 请求分类表。 |
| `INCLUDE=n` | 包含 n 个变量。 |
| `EXPB` | 显示优势比的估计值。 |

## 16.3 使用简单逻辑回归分析

简单逻辑模型是指只有一个预测变量的模型。该预测变量可以是二分类的或定量的。以下上手操作示例说明了简单逻辑模型。

> 上手操作示例
>
> 本示例使用名为 `ACCIDENTS` 的模拟创伤数据集来寻找一个预测死亡 `DEAD=1` 的模型，使用 `PENETRATE` 变量。

1. 打开程序文件 `ALOG1.SAS`。

```
PROC LOGISTIC DATA="C:SASDATA\ACCIDENTS" DESCENDING;
MODEL DEAD=PENETRATE / RISKLIMITS;
TITLE 'Trauma Data Model by Penetration Wound';
RUN;
```

在此示例中，独立变量 `PENETRATE` 是一个 0, 1 变量，用于预测死亡 `DEAD=1`，因此使用了 `DESCENDING` 选项。

2. 运行此程序。在输出中，请注意以下语句：

`Probability modeled is dead=1.`

该语句告诉您预测概率所基于依赖变量值。观察表 16.3 所示的简略输出。

### 表 16.3 逻辑回归输出

| 响应概况 (Response Profile) | | |
|---|---|---|
| 序数值 (Ordered Value) | dead | 总频率 (Total Frequency) |
| 1 | 1 | 103 |
| 2 | 0 | 3580 |

Probability modeled is dead=1.

| 极大似然估计分析 (Analysis of Maximum Likelihood Estimates) |
