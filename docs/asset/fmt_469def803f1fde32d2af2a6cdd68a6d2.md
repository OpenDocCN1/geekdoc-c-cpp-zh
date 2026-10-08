
![](img/0c09161c0be53934e5708cffbdcc441f_110_0.png)

```
title 'Random Vectors';
proc sgplot data=sgbook.vector;
vector x=x y=y;
run;
```

### 图 4.10.2: 向量图

这是一个向量图，所有向量都具有通过 `XORIGIN` 和 `YORIGIN` 角色指定的用户定义的共同原点 (0.4, 0.4)。

`LINEATTRS` 选项用于将线宽设置为 2。注意箭头的尺寸与线宽成正比。

![](img/0c09161c0be53934e5708cffbdcc441f_110_1.png)

```
title 'Random Vectors';
proc sgplot data=sgbook.vector;
vector x=x y=y / xorigin=0.4 yorigin=0.4 lineattrs=(thickness=2);
run;
```

### 图 4.10.3: 垂直向量图

此股票图通过使用向量绘制随时间变化的每月收盘价创建，这提供了另一种创建此类箭头的方法。

`ARROWHEADSHAPE` 选项用于获取刺状箭头。

SAS 9.3 支持一种新的 `HIGHLOW` 图，它提供了创建此类图表的另一种方法。

![](img/0c09161c0be53934e5708cffbdcc441f_111_0.png)

```
title 'Stock Plot':
proc sgplot data=sgbook.Stock;
vector x=date y=close xorigin=date yorigin=open
arrowheadshape=barbed;
axis grid;
run;
```

### 图 4.10.4: 分组向量图

该图使用分组绘图，每个向量都有自己的原点。不同组之间存在上升和下降趋势。组用不同的视觉属性表示。

使用了 `NOARROWHEADS` 选项。

SAS 9.3 支持一种新的 High-Low 图，它提供了创建此类图表的另一种方法。

![](img/0c09161c0be53934e5708cffbdcc441f_111_1.png)

```
title 'Stock Plot':
proc sgplot data=sgbook.Stock;
vector x=date y=close xorigin=date yorigin=open
noarrowheads lineattrs=(thickness=2);
axis grid;
run;
```

Sanjay and Heath, Statistical Graphs by Example: Effective Graphs Using SAS. © 2011, SAS Institute Inc., Cary, North Carolina. ALL RIGHTS RESERVED. 更多 SAS 资源访问 sas.com/publishing。

## 4.11 VBarParm 和 HBarParm (9.3)

这些预汇总的柱状图语句具有以下语法：

```
vbarparam column / responses=column;
hbarpar column / response=column;
```

`VBARM` 和 `HBARPARM` 语句在显示响应和限制值时创建特殊的柱状图。相关样式元素：当多个绘图语句叠加时，使用 `GraphData` 样式元素，每个组或绘图语句使用 `GraphData12` 元素。![](img/0c09161c0be53934e5708cffbdcc441f_112_0.png) **必需数据**

| 角色 | 语法 | 描述 |
| :--- | :--- | :--- |
| Category | =column | 沿类别轴的位置 |
| Response | =num-column | 响应变量 |

**可选数据:**

| 角色 | 语法 | 描述 |
| :--- | :--- | :--- |
| DATABEL | =column | 每个观测值的标签字符串 |
| GROUP | =column | 多级分类 |
| LABEL | =column | 每个观测值的标签 |
| LOWER | =column | 下限值 |
| UPPER | =-column | 上限值 |

**外观选项：**

| 角色 | 语法 | 描述 |
| :--- | :--- | :--- |
| FILLATTRS | =fill-attrs | 柱内部的外观 |
| LIMITATTRS | =line-attrs | 限制柱的外观 |

**其他选项：**

| 角色 | 语法 | 描述 |
| :--- | :--- | :--- |
| BARWIDTH | =value | 刻度间距的比例 |
| DATASKIN | =skin-value | 预定义的皮肤类型 |

**布尔选项：**

| 选项 | 描述 |
| :--- | :--- |
| DATABEL | 显示默认柱标签 |
| FILL | NOFILL | 显示填充/未填充柱 |
| OUTLINE | NOUTLINE | 显示柱轮廓或不显示 |
| MISSING | 接受类别值 |

**支持标准常用选项**

`ATTRID`, `CLUSTERWIDTH`, `DISCRETEOFFSET`, `GROUPDISPLAY`, `GROUPORDER`, `LEGENDLABEL`, `NAME`, `MISSINGGROUP`, `TRANSPARENCY`

### 图 4.11.1: 参数柱状图

这是所有汽车 MPG (City) 的基础柱状图。数据已使用 `MEANS` 过程汇总，以创建此图所需的数据。由于数据已按源和类型进行汇总，我们按源选取了 `_TYPE=2`。

![](img/0c09161c0be53934e5708cffbdcc441f_113_0.png)

### 图 4.11.2: 带有限制和标签的参数柱状图

这是按类型的 MPG (City) 垂直图。由于显示了限制条件，数据标签显示在柱下方。可以使用 `DATABELPOS` 移动标签。

![](img/0c09161c0be53934e5708cffbdcc441f_113_1.png)

```
*Vehicle Mileage by Type*
proc sgplot data=sgbook.car_means;
where _type=1;
varparm category=type response=mean_mpg_city / databel
limitupper=max_mpg_city limitlower=min_mpg_city
databelpos=bottom;
yaxis grid;
```

### 图 4.11.3: 分组参数柱状图

![](img/0c09161c0be53934e5708cffbdcc441f_114_0.png)

这是按源和类型的里程数分组图。`GROUPDISPLAY` 设置为 Cluster 以并排显示组值。此柱使用了 `DATASKIN`。设置 `YAXIS OFFSETMAX` 为内部数据区域留出空间。

```
title 'Vehicle Mileage by Origin and Type';
proc sgplot data=sasbook.carans;
where type=3 and (type = 'Sedan' or type='Sports' or type='SUV');
vbarparam category=origin response=mean_mpg_City / group=type
transparency=50;
keylegend /locations=index position=topright;
axis display=(nolabel); xaxis grid offsetmax=0.2;
run;
```

![](img/0c09161c0be53934e5708cffbdcc441f_114_1.png)

### 图 4.11.4: 带有数据标签的分组参数柱状图

![](img/0c09161c0be53934e5708cffbdcc441f_114_2.png)

此按类型分组的柱与图 4.11.3 相同。`DATABEL` 选项用于显示柱统计数据。设置 `YAXIS OFFSETMAX=2` 为图例留出空间。

### 图 4.11.5: 叠加参数柱状图

![](img/0c09161c0be53934e5708cffbdcc441f_115_0.png)

该图使用了两个 `VARPARM` 语句的叠加，分别用于城市和公路里程。对于共同类别，第二个语句的柱直接叠加在第一个语句上，因此最好将第二个柱的 `BARWIDTH` 设置为较小值。

```
ods style=journal;
title 'Vehicle Mileage by Origin':
proc sgplot data=cars.mileage;
  where type=2;
  varparm category=origin response=mean_mpg_City /
    dataskin=pressed discreteoffset=-0.2 barwidth=0.4;
  varparm category=origin response=mean_mpg_highway /
    dataskin=pressed discreteoffset=0.2 barwidth=0.4;
  xaxis displays=(nolabel);
  yaxis grid; run;
```

### 图 4.11.6: 带有填充和偏移的叠加参数柱状图

![](img/0c09161c0be53934e5708cffbdcc441f_115_1.png)

通过设置 `DISCRETEOFFSET` 选项的值，每组柱都从中心点偏移。柱宽已相应缩小。类别间距的比例。

### 图 4.11.7：水平参数条形图

该图使用 `HBARPARM` 绘图（plot）来显示药物不良事件的平均频率。

当类别名称较长时，水平条形特别有用。

![](img/0c09161c0be53934e5708cffbdcc441f_116_0.png)

```
title Most Frequent Adverse Events:
proc sgplot data=sgbook.AdverseEvents;
hbarparm category=response=mean;
yaxis display=(nolabel);
axis grid label='Relative Risk with 95% CL';
run;
```

![](img/0c09161c0be53934e5708cffbdcc441f_116_1.png)

### 图 4.11.8：带有限制的水平参数条形图

该图使用 `HBARPARM` 图显示具有高低置信限的药物不良事件平均频率。

我们使用 `LIMITATTRS` 选项来设置限制条的视觉属性。

![](img/0c09161c0be53934e5708cffbdcc441f_116_2.png)

```
title Most Frequent Adverse Events:
proc sgplot data=sgbook.AdverseEvents;
hbarparm category=response=mean / limitlower=low limitupper=high
limitattrs=(color=grey pattern=dashed);
yaxis display=(nolabel);
axis grid label='Relative Risk with 95% CL';
run;
```

![](img/0c09161c0be53934e5708cffbdcc441f_116_3.png)

## 4.12 气泡图 (9.3)

`BUBBLE` 语句具有以下语法：

```
bubble x=column y=column size=num-column </ options>;
```

气泡图在图中的 X 和 Y 位置绘制根据 Size 角色缩放大小的圆形气泡。气泡的半径由 `SIZE` 变量线性缩放。

![](img/0c09161c0be53934e5708cffbdcc441f_117_0.png)

| 必需的数据角色： | | |
|---|---|---|
| | column | 沿水平轴的位置 |
| | Y | 沿垂直轴的位置 |
| SIZE | num-column | 气泡的大小 |

| 可选的数据角色： | | |
|---|---|---|
| DATABEL | =column | 每个观测结果的标签字符串 |
| GROUP | =column | 气泡颜色的分类 |
| URL | =column | 每个观测结果的 URL |

| 外观选项： | | |
|---|---|---|
| DATABELATTRS | =ext-attr | 标签的外观属性 |
| FILLATTRS | =fill-attr | 气泡内部的的外观属性 |
| LINEATTRS | =line-attr | 气泡轮廓的外观属性 |

| 其他选项： | | |
|---|---|---|
| BRADIUSMAX | =value | 最大气泡的半径（像素为单位） |
| BRADIUSMIN | =value | 最小气泡的半径（像素为单位） |

| 布尔选项： | | |
|---|---|---|
| FILL | =NOFILL | 是否显示填充气泡 |
| OUTLINE | =NOUTLINE | 是否显示气泡轮廓 |

| 标准常用选项： | | |
|---|---|
| ATTRID, LEGENDLABEL, NAME, NOMISSGROUP, TRANSPARENCY, URL, X2AXIS, Y2AXIS |

必需的样式元素：使用 `GraphDefault` 样式元素来绘制图表元素。当存在 `GROUP` 变量时，或当多个绘图语句叠加时，使用 `GraphData1-GraphData12` 元素。

Sanjay and Heath, Dan. Statistical Procedures by Example: Effective Graphs Using SAS®. Copyright ©2011, SAS Institute., Cary, North Carolina. USA. ALL RIGHTS RESERVED. 其他资源请访问 support.sas.com/publishing.

### 图 4.12.1：基础气泡图

这是年龄与体重的基础气泡图。该图用于 `sashhelp` 数据集中的女性学生。

使用 `INSET` 语句识别数据的子集。

![](img/0c09161c0be53934e5708cffbdcc441f_118_0.png)

```
title 'Student Age by Height and Weight';
proc sgplot data=sashhelp.class;
where sex='F';
bubble x=height y=weight size=age;
inset 'Females only' / position=bottomright;
axis grid; yaxis grid;
run;
```

### 图 4.12.2：分组气泡图

这是按类型汇总的马力与里程分组气泡图。

使用 `KEYLEGEND` 语句将图例放置在数据区域的右下角。

![](img/0c09161c0be53934e5708cffbdcc441f_118_1.png)

```
title 'Vehicle Profile by Type';
proc sgplot data=sgbook.carmeans;
where type='hybrid';
bubble x=mean_city y=mean_highway size=mean_horsepower
group=type transparency=0.5;
keylegend location=inside-bottomright across=1;
axis grid; yaxis grid;
run;
```

### 图 4.12.3：分组气泡图

该图与图 4.12.2 相同，通过 `GROUP` 变量标记每个气泡。使用 `NOLEGEND` 选项移除自动图例，因为更倾向于直接标记。

![](img/0c09161c0be53934e5708cffbdcc441f_119_0.png)

```
*Vehicle Profile by Type*;
proc sgplot data=sasbook.carmeans nolegend;
where type=1 and type <> 'Hybrid';
bubble x=mean_mpg y=mean_highway size=mean_horsepower
group=type transparency=0.5;
xaxis grid; yaxis grid;
run;
```

![](img/0c09161c0be53934e5708cffbdcc441f_119_1.png)

### 图 4.12.4：带负数据的气泡图

该气泡图使用虚线表示负大小值。这是通过对 `size` 角色使用绝对值实现的。`GROUP` 变量根据数据的符号设置并与 `group` 角色一起使用。气泡最小值和最大值按比例映射数据。带有 `MARKERLABEL` 的散点图用于标签。
