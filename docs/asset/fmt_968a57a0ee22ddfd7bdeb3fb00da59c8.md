
这是一张使用 VBARM 语句显示销量预测的图。在这里，我们将两种统计数据包含在图中。使用轴偏移为统计数据留出空间。我们使用散点图绘制了位于右侧 10% 的统计数据。

```
/* Forecasts */
proc sgplot data=sasbook.survival;
vbarm category=product stat=mean
errbar / attrs=GraphData(size=4);
errbar / attrs=GraphData(size=4);
axis display=(notlabel) grid;
run;
```

![](img/0c09161c0be53934e5708cffbdcc441f_138_0.png)

## 图 4.17.12：水平柱状图与统计数据 (HBARPARM with Statistics)

此图类似于 4.17.11，使用 HBarParm 限制以及散点图来显示统计数据。使用轴偏移为统计数据留出空间。X2 数据被限制在右侧 20%。

```
/*  X2 Data */
proc sgplot data=sasbook.survival;
hbarparm category=product stat=mean
errbar / attrs=GraphData(size=4);
errbar / attrs=GraphData(size=4);
axis display=(notlabel) grid;
x2axis display=(notlabel) offsetmin=0.64 offsetmax=0.83;
run;
```

# 第 5 章

## 拟合与置信图

- 5.1 引言 129

- 5.2 拟合图的作用与选项 130

- 5.3 回归图 131

- 5.4 Loess 平滑图 138

- 5.5 惩罚 B 样条图 145

- 5.6 椭圆图 152

- 5.7 组合图表 157

![](img/0c09161c0be53934e5708cffbdcc441f_140_0.png)

> “要做，或者不做。没有所谓的‘尝试’。”

~  Yoda

Matange, Sanjay and Heath, Dan. Statistical Graphics Procedures by Example: Effective Graphs Using SAS®. Copyright © 2011,
SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 如需更多 SAS ，请访问 `support.sas.com/publishing`。

# 第 5 章：拟合与置信图

在本章中，我们将研究 `SGPLOT` 和 `SGPANEL` 过程的拟合和置信图。本章将详细介绍每个图表及其相关选项的基本语法。此组中的图表可以相互组合，并与“基础图”组中的许多 X-Y 图进行混合。

## 5.1 引言

`SGPLOT` 和 `SGPANEL` 过程支持下列的多种拟合和置信图。这些图表通常还会以散点图的形式显示原始数据，并支持置信带。这些图表可以与许多基础 X-Y 图（最常用散点图）结合。

| REG | LOESS |

|---|---|

| PBSPLINE | ELLIPSE |

![](img/0c09161c0be53934e5708cffbdcc441f_141_0.png)

## 5.2 拟合图的作用与选项

所有拟合图语句具有以下语法：

```
FitPlotName required-data-roles </options>;
```

所有图表语句都具有创建视觉效果所需的必需和可选参数。这些参数分为以下大类：

1. 必需数据角色

2. 可选数据角色

3. 选项

4. 通用选项

以下是常用选项的列表：

### 通用选项：

| | | 描述 |

|---|---|---|

| ATTRID | =string | 用于分组变量的属性映射 ID。 |

| CURVELABELATTRS | =line-attrs | 标签的外观属性。 |

| CURVELLABOC | =keyword | 曲线标签位置 - INSIDE（内部） | OUTSIDE（外部） |

| CURVELABELPOS | =keyword | 曲线标签位置 - AUTO | MAX | MIN 显示 Y 变量的标签或可选值。 |

| DATABEL | <<column> | DataLabel 的外观属性。 |

| DATALATTRIBUTES | =text-attrs | 用于拟合计算的分类变量。 |

| GROUP | =column | 标签出现在图例中，表示此（非分组）图。 |

| LEGEND | | 拟合的外观属性。 |

| LINEARTS | =line-attrs | 标记的外观属性。 |

| MARKERATTRS | =marker-attrs | 预测点的最小数量。 |

| MAXPOINTS | =positive-integer | 为此语句指定一个名称。其他语句（如 KEYLEGEND）可以通过其名称引用此图表。 |

| NAME | =string TRANSPARENCY | =value | 指定视觉元素的透明度。 |

### 通用布尔选项：

| | 描述 |

|---|---|

| NOMARKERS | 不显示带拟合线的散点标记。 |

| X2AXIS | 将 X 值分配给 X2（顶端）轴。 |

| Y2AXIS | 将 Y 值分配给 Y2（右侧）轴。 |

这些通用选项适用于每个图表语句，并可以像上面一样完全使用。为了避免重复，我们不会列出本章讨论的各个图表的所有通用选项。

## 5.3 回归图

回归图显示原始数据的线性或非线性拟合。

语法为：

```
reg x=column y=column </options>
```

在每个 `(x, y)` 位置都会显示一个标记。会计算并显示一条拟合线。可选情况下，还可以显示不同的置信限。

![](img/0c09161c0be53934e5708cffbdcc441f_143_0.png)

必需数据角色：

| | 描述 |

|---|---|

| X =num-column | 沿水平轴的位置 |

| Y =num-column | 沿垂直轴的位置 |

可选数据角色：

| | 描述 |

|---|---|

| FREQ =num-column | 当前观测值的频率 |

| WEIGHT =num-column | 回归拟合的优先权重 |

外观选项：

| | 描述 |

|---|---|

| ALPHA =positive-number | 置信水平 |

| CLIATTRS =cli-attr | CLI 的外观属性。 |

| CLMATTRS =cli-attr | CLM 的外观属性。 |

| DEGREE =positive-integer | 多项式阶数。 |

其他选项：

| | 描述 |

|---|---|

| CLI =string | 使用图例标签显示单个预测值的置信限。 |

| CLM =string | 使用图例标签显示平均预测值的置信限。 |

布尔选项：

| | 描述 |

|---|---|

| CLI | 显示单个预测值的置信限。 |

| CLM | 显示平均预测值的置信限。 |

| NOLEGCLI | 从图例中排除 CLI。 |

| NOLECLM | 从图例中排除 CLM。 |

| NOLEGFIT | 从图例中排除拟合线。 |

标准选项支持 `ATTRID`, `CURVELABEL`, `CURVELLABOC`, `CURVELABELPOS`, `DATABEL`, `DATALATTRIBUTES`, `GROUP`, `LEGEND`, `LINEARTS`, `MARKERATTRS`, `MAXPOINTS`, `NAME`, `NOMARKERS`, `TRANSPARENCY`, `X2AXIS`, `Y2AXIS`。当存在 `GROUP` 变量或叠加多个图表语句时，使用 `GraphData` 元素绘图。

### 图 5.3.1：基础线性拟合

此图包含基础回归拟合。默认情况下，`REG` 语句会生成线和散点。此行为可以通过 `NOMARKERS` 选项控制。

![](img/0c09161c0be53934e5708cffbdcc441f_144_0.png)

```
title "The Impact of Horsepower on MPG"
proc sgplot data=sashelpcar, noautlegend;
where type="Sedan" and origin="USA";
reg x=horsepower y=mpg_city;
axis grid;
yaxis grid;
run;
```

### 图 5.3.2：CLM 带

除了线性拟合和散点外，此图显示平均值的置信限 (`CLM`)。默认情况下，计算的 alpha 值为 `.05` (95% 置信)。该值可以通过 `ALPHA` 选项调整。

![](img/0c09161c0be53934e5708cffbdcc441f_144_1.png)

```
title "The Impact of Horsepower on MPG"
proc sgplot data=sashelpcar, noautlegend;
where type="Sedan" and origin="USA";
reg x=horsepower y=mpg_city / clm;
axis grid;
yaxis grid;
run;
```

Matange, Sanjay and Heath, Dan. Statistical Procedures by Example: Effective Graphs Using SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 如需更多 SAS ，请访问 `support.sas.com/publishing`。

### 图 5.3.3：CLI 带

除了线性拟合、散点和 CLM 带外，此图显示单个值的预测限 (`CLI`)。默认情况下，计算的 alpha 值为 `.05` (95% 置信)。该值可以使用 `ALPHA` 选项调整，它会影响 CLM 和 CLI。

![](img/0c09161c0be53934e5708cffbdcc441f_145_0.png)

```
title "The Impact of Horsepower on MPG"; proc sgplot data=sashelp.cars noautolegend; where type='Sedan' and origin='USA'; reg x=horsepower y=mpg_city / clm cli; xaxis grid; yaxis grid; run;
```

### 图 5.3.4：自动图例

此图显示包含拟合信息的图例。该图例默认出现，可以通过 `NOAUTLEG` 选项或指定自定义图例来禁用。

![](img/0c09161c0be53934e5708cffbdcc441f_145_1.png)

`NOLEGFIT` 选项防止拟合线显示在图例中。

```
title "The Impact of Horsepower on MPG"; proc sgplot data=sashelp.cars; where type='Sedan' and origin='USA'; reg x=horsepower y=mpg_city / clm nolegeffit; xaxis grid; yaxis grid; run;
```

Matange, Sanjay and Heath, Dan. Statistical Procedures by Example: Effective Graphs Using SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 如需更多 SAS ，请访问 `support.sas.com/publishing`。

### 图 5.3.7：散点数据标签

默认情况下，`DATABEL` 选项显示散点的非缺失 Y 值。你可以向选项分配一列以显示替代值。

在此示例中，只有离群点的 Y 值被复制到名为 "`outlier`" 的列中。该列中的缺失值不会显示。

![](img/0c09161c0be53934e5708cffbdcc441f_147_0.png)

```
/* The Impact of Horsepower on MPG*
proc sgplot data=dataset.carlabel noutelegend;
where type='Sedan' and origin='USA';
reg x=horsepower y=mpg_city / clm datalabel=outlier;
xaxis grid;
yaxis grid;
run;
```

### 图 5.3.8：多项式回归拟合

`DEGREE` 选项可更改回归拟合的多项式。

在此示例中，通过将 `DEGREE` 选项设置为 2，对散点进行了二次拟合。

![](img/0c09161c0be53934e5708cffbdcc441f_147_1.png)

```
/* The Impact of Horsepower on MPG*
proc sgplot data=dataset.carlabel noutelegend;
where type='Sedan' and origin='USA';
reg x=horsepower y=mpg_city / degree=2;
xaxis grid;
yaxis grid;
run;
```

## 图 5.3.9: 分组拟合

在 `REG` 语句中指定 `GROUP` 列时，散点和拟合线都会被分组。

使用两个语句来控制标记的透明度。`NOMARKER` 选项用于禁用默认散点。

![](img/0c09161c0be53934e5708cffbdcc441f_148_0.png)

```
title "The Impact of Horsepower on MPG"
proc sglplot datasashelp.cars;
where type="Sedan";
scatter x=horsepower y=mpg_city / group=origin transparency=0.85
reg x=horsepower y=mpg_city / group=origin nomarkers name="reg"
keylegend="scat" / titles="origin"
keylegend="reg" / location=inside across=1
xaxis grid;
run;
```

## 图 5.3.10: 带有分组的单次拟合

要创建一个通过所有分组散点数据的拟合，请使用 `SCATTER` 语句绘制分组数据，并使用不带 `group` 列且带有 `NOMARKER` 选项的 `REG` 语句。

![](img/0c09161c0be53934e5708cffbdcc441f_148_1.png)

```
title "The Impact of Horsepower on MPG"
proc sglplot datasashelp.cars;
where type="Sedan"
scatter x=horsepower y=mpg_city / group=origin transparency=0.85
name="scat"
reg x=horsepower y=mpg_city / nomarkers degree=3 name="reg"
keylegend="scat" / location=inside across=1 title="origin"
xaxis grid;
run;
```

## 图 5.3.11: 叠加拟合

可以通过对所有 `REG` 语句使用 `NOMARKER` 选项来叠加拟合进行比较，但可以使用单独的 `SCATTER` 语句来控制散点图。

注意 `REG` 语句被分配了一个自定义图例。`LEGENDLABEL` 选项覆盖了每个的默认标签

![](img/0c09161c0be53934e5708cffbdcc441f_149_0.png)

```
title "The Impact of Horsepower on MPG";
proc sgplot data=sashelp.cars;
where type="Sedan";
scatter x=horsepower y=mpg_city / transparency=0.85;
legendlabel1="degree=2";
reg x=horsepower y=mpg_city / nomarkers degree=2 name="reg1"
reg x=horsepower y=mpg_city / nomarkers degree=3 name="reg2"
legendlabel1="degree=3";
keylegend="reg2" location=inside;
xaxis grid; yaxis grid;
run;
```

## 图 5.3.12: 曲线拟合

与其使用图例来识别每个拟合，不如可以使用 `CURVELABEL` 选项直接为拟合线标记。当线条不拥挤时，这种方法效果良好。

![](img/0c09161c0be53934e5708cffbdcc441f_149_1.png)
