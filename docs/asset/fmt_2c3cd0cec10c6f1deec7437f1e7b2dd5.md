
Matange, Sanjay and Heath, Dan. Statistical Graphics Procedures by Example: Effective Graphs Using SAS. Copyright © 2011, SAS Institute, Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 如需更多 SAS 资源，请访问 `support.sas.com/`.

## 4.16 瀑布图 (9.3)

`WATERFALL` 语句具有以下语法：

```sas
waterfall category=column response=column <options/>
```

瀑布图绘制的片段相对于之前观测值的累积和定位。每个观测值的响应值（response value）预期为沿轴累加的增量（delta）。可以指定累加的初始值。最终柱形的值从数据中计算。

![](img/0c09161c0be53934e5708cffbdcc441f_129_0.png)

### 必需数据角色：

| CATEGORY | 沿水平轴的投影 |

|---|---|

| RESPONSE | num-column | 沿垂直轴的柱状图增量 |

### 可选数据角色：

| COLORGROUP | 柱状颜色的分类 |

|---|---|

| DATABEL | =column | 每个观测值的标签字符串 |

| URL | =column | 每个观测值的 URL |

### 外观选项：

| DATABELATTRS | =text-attrs | 标签的外观属性 |

|---|---|

| FILLATATTRS | =fill-attrs | 气泡内部的外观属性 |

| FINALBARATTRS | =line-attrs | 气泡轮廓的外观属性 |

| INITIBARATTRS | =line-attrs | 气泡轮廓的外观属性 |

### 其他选项：

| BARWIDTH | =value | 最大气泡的像素半径 |

|---|---|

| DATASKIN | =string-value | 定义类型之一 |

| FINALBARVALUE | =string | 轴上最终柱形标签的字符串 |

| INITIALBARVALUE | =string | 轴上初始柱形标签的字符串 |

| INITIALBARVALUE | =value | 初始柱形的响应值 |

| STAT | =keyword | MEAN | SUM |

### 布尔选项：

| FILL | =NOFILL | 是否显示填充柱形 |

|---|---|

| OUTLINE | =NOLINE | 是否显示柱形轮廓 |

| MISSING | | 显示缺失类别值 |

支持标准常用选项：

`ATTRID`, `LEGENDLABEL`, `NAME`, `NOMISSINGGROUP`, `TRANSPARENCY`, `URL`, `X2AXIS`, `Y2AXIS`

相关样式元素：使用 `GraphDefault` 样式元素绘制图元素。

当存在分组变量时，使用 `GraphData1-GraphData12` 元素，每个组使用一个。

## 图 4.16.1：基础瀑布图

此图显示了交易期间的累计现金余额。每个观测值都相对于之前的累积统计量（在本例中为 `SUM`）从零绘制。

最终柱形的值从数据中计算并显示在末尾。

![](img/0c09161c0be53934e5708cffbdcc441f_130_0.png)

```sas
title "Auto Dealership Balance for March";proc sgplot data=esbook.transactions;
waterfall category=transaction response=amount;
yaxis display=(nolabel);
run;
```

## 图 4.16.2：带有初始值的瀑布图

此图显示与图 4.16.1 相同的数据，但设置了初始柱形。

![](img/0c09161c0be53934e5708cffbdcc441f_130_1.png)

```sas
title "Auto Dealership Balance for March";proc sgplot data=esbook.transactions;
waterfall category=transaction response=amount;
yaxis display=(nolabel);
run;
```

## 图 4.16.3：分组瀑布图

此图显示与图 4.16.1 相同的数据，但设置了初始柱形。

![](img/0c09161c0be53934e5708cffbdcc441f_131_0.png)

## 图 4.16.4：带有标签的瀑布图

此图显示与图 4.16.1 相同的数据，但设置了初始柱形。

![](img/0c09161c0be53934e5708cffbdcc441f_131_1.png)

# 图 4.17.11：散点-散点图叠加 (Scatter-Scatter Overlay)

这是两个散点图的组合，分别用于按平均马力显示最小和最大里程数。

系统会自动生成图例，我们通过 `KEYLEGEND` 将其放置在数据区域的右上角。

![](img/0c09161c0be53934e5708cffbdcc441f_133_0.png)

```
* '按平均马力计算里程范围'
proc sgplot datasashelp.carMeans;
where type_id=1;
scatter x=mean_horsepower y=min_mpg_city;
scatter x=mean_horsepower y=max_mpg_city;
keylegend / location=inside position=topright across=1;
yaxis grid;
yaxis grid label='MPG';
run;
```

# 图 4.17.2：散点-序列图叠加 (Scatter-Series Overlay)

这是原始数据与线性图的叠加。预测曲线之前已使用 `REG` 过程计算过。

拟合线应用了标准的 `GRAPHFFIT` 样式元素。

![](img/0c09161c0be53934e5708cffbdcc441f_133_1.png)

```
* '类别健康统计'
proc sgplot datashelp.classfit;
scatter x=height y=weight;
serline x=height y=predict / lineattrs=GraphFit;
keylegend / location=inside position=bottomright across=1;
yaxis grid;
yaxis grid;
run;
```

Matange, Sanjay, and Heath, Dan. Statistical Procedures by Example: Effective Graphs using SAS®. Copyright of 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 `support.sas.com/publishing`。

# 图 4.17.3：散点、序列与带状 (Scatter, Series, and Band)

这是带有置信区间限制的标准拟合图。预测曲线和限制之前已使用 `REG` 过程计算过。`KEYLEGEND` 上的 `VALUEATTRS` 选项用于创建较小的字体。

![](img/0c09161c0be53934e5708cffbdcc441f_134_0.png)

```
title Class Health Statistics;
proc sgplot data=classfit;
band x=height yupper=upper lower=lower label1=Confidence nofill;
band x=height yupper=upper lower=lower label1=Prediction;
series x=height y=predict;
line x=height lineattrs=GraphFit;
keylegend location=inside position=bottomright across=1 valueattrs=(size=6);
yaxis;
run;
```

# 图 4.17.4：阶梯图与散点图 (Step and Scatter Plot)

这是一张随时间变化的生存图。两种处理统计数据以列的形式呈现。这允许我们使用散点图来显示风险标记。使用隐藏的 `REFLINE` 并配合“label”功能来标记风险人数，同时抑制线条本身。可见绘图（Visible Plot）用于计数。

```
title Survival by Time
proc sgplot data=sasbook.survival;
step x=days y=survival markerrattrs=GraphData(size=4) name="D" label="Drug";
step x=days y=survivalP markerrattrs=GraphData(size=4) name="P" label="Placebo";
step x=days y=placebo lineattrs=left markerrattrs=(size=3) freeplot;
step x=days y=placebo lineattrs=left markerrattrs=(size=3) freeplot;
refline -0.1 -0.2 / label="Placebo" labeloc=outside sidelabels=inside
keylegend "D" / "P" location=inside position=topright across=1 valueattrs=(size=5);
yaxis grid;
```

# 图 4.17.5：序列与带状 (Series and Band)

这是体重指数图，使用带状图显示分类为“正常”、“体重轻”等区域。每个受试者的实际数据使用带有标记的 `SERIES` 语句随时间绘制。`CURVELABEL` 和 `CURVELABELPOS` 选项用于描述曲线。

```
title Three Charts vs BMI;
proc sgplot data=bmi;
band x=weight yupper=upper_h lower=lower_h / groupname="bmi" transparency=.7;
series x=weight lineattrs=(thickness=1) markers
keylegend="b" position=bottomright location=inside
axis min=0 max=300 label="Weight (lbs)" grid;
axis min=40 max=80 label="Height (in)" grid;
run;
```

# 图 4.17.6：散点与带状 (Scatter and Band)

这是两个带状图和一个针状图的叠加，显示了全年的数据以及上下限制。每个带的上限已标记，从而避免了对图例的需求。

```
title "Sales with Limits";
proc sgplot data=sales autolegend;
band x=date upper=low / fillattrs=graph1 outline curvelabelopts="high";
band x=date upper=low / fillattrs=graph5 outline curvelabelopts="low";
needle x=date y=sales lineattrs=(thickness=2) transparency=.5;
xaxis grid=(notabel)
yaxis grid;
run;
```

Matange, Stanley and Heath, Dan. Statistical Graphics Procedures by Example: Effective Graphs Using SAS(). Copyright of 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 `support.sas.com/publishing`。

# 图 4.17.7：分组带状 (Grouped Band)

这是一个使用分组带状图创建的 Theme River 图示例。每个带的数据覆盖了带的高度。因此，我们使用了 `TRANSPARENCY` 来确保所有带都可见。

```
title 'Theme River Group';
proc sgplot data=sgbook.themeriverGroup;
band x=time upper=upper lower=lower / group=name transparency=.7
fill outline lineattrs=(pattern=solid);
keylegend/position=right location=inside axis=1
axis display=(nlabel) grid;
axis grid label='Relative Frequency' display=(novuseticks);
run;
```

# 图 4.17.8：带状叠加 (Band Overlay)

此图类似于图 4.17.7。这里每个带的数据都在单独列中。因此，我们使用了带叠加来创建此图。由于已知每个带的数据范围，我们可以指定绘制顺序，确保最小的带最后绘制。此示例未使用 `TRANSPARENCY` 选项。

```
title 'Theme River Overlay';
proc sgplot data=sgbook.resiliency;
band x=time upper=upper lower=lower / fill outline lineattrs=(pattern=solid);
band x=time upper=upper lower=lower / fill outline lineattrs=(pattern=solid);
band x=time upper=upper lower=lower / fill outline lineattrs=(pattern=solid);
band x=time upper=upper lower=lower / fill outline lineattrs=(pattern=solid);
keylegend/position=right location=inside axis=1 valueattrs=(size=4);
axis display=(nlabel) grid;
axis grid label='Relative Frequency' display=(novuseticks);
run;
```

Matange, Sanjay and Heath, D. Statistical Procedures by Example: Effective Graphs using SAS(). Copyright of 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 `support.sas.com/publishing`。

# 图 4.17.9：帕托图 (Pareto Chart)

这是一个使用 `VBARM` 和 `SERIES` 语句的帕托图。设置 `BARWIDTH=0.8` 和 `DISOFFSET=0.4` 是为了确保累计线位于柱状图的右上角。序列图显示标记，并为每个观测值提供数据标签。

![](img/0c09161c0be53934e5708cffbdcc441f_137_0.png)

# 图 4.17.10：浮动柱与带状 (Floating Bars and Bands)

这是一年内（210）每月温度的图，与 30 年平均值进行了对比。30 年平均值使用 `TYPE=Bar` 的 Highlow 图发布。高值和低值通过带状图显示。

```
/* Monthly Temperatures for 210 */
proc sgplot data=sashelp.stocks;
highlow x=month high=low type=bar label='30 Year Average' transparency=.5;
band x=month upper=thisyear lower=thisyear;
keylegend='This Year' location=inside;
axis display=(nlabel) grid;
axis grid label='Temperature';
run;
```

![](img/0c09161c0be53934e5708cffbdcc441f_137_1.png)

# 图 4.17.11：柱状图与统计数据 (VBARM with Statistics)
