
![](34e5708cffbdcc441f_277_1.png)

Matange, Sanjay and Heath, Dan. Statistical Procedures by Example: Effective Graphs Using SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 请访问 support.sas.com/publishing.

## 10.5 大尺寸面板的分页

### 图 10.5.1：布局面板

此图按产地和类型分类的面板。有八种组合，我们指定了 `2x2` 网格。

过程创建了两个图形输出以覆盖所有组合。注意，`欧洲-卡`组合被完全丢弃（包括标题）。

![](34e5708cffbdcc441f_278_0.png)

### 图 10.5.2：布局晶格

此图与图 10.5.1 相同，除了 `LAYOUT Lattice`。在这种情况下，显示了所有组合（包括标题）。然而，缺失数据的单元格是空的。

![](34e5708cffbdcc441f_278_1.png)

```sas
title *Vehicle Mileage by Origin ...*;

proc sgpanel data=sashelp.cars;

where (origin='USA' or
origin='Europe') and
type='Sedan' or type='Sports' or
type='SUV' or type='Truck');

panelby origin type / columns=2
rows=2;

histogram mpg_city;
```

```sas
title *Vehicle Mileage by Origin ...*;

proc sgpanel data=sashelp.cars;

where (origin='USA' or
origin='Europe') and
type='Sedan' or type='Sports' or
type='SUV' or type='Truck');

panelby origin type / layout=lattice
columns=2 rows=2;

histogram mpg_city;
```

![](34e5708cffbdcc441f_278_2.png)

![](34e5708cffbdcc441f_278_3.png)

# 第 11 章

## 比较图与矩阵图

- 11.1 引言 269
- 11.2 SGATTER 过程 269
- 11.3 PLOT 语句 270
- 11.4 COMPARE 语句 276
- 11.5 MATRIX 语句 281

![](img/0c09161c0be53934e5708cffbdcc441f_280_0.png)

> “如果你不知道自己要去去哪里，你最终会到达另一个地方。”
~ Yogi Berra

Matange, Sanjay and Heath, Dan. *Statistical Graphics Procedures by Example: Effective Graphs Using SAS®*. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。欲更多 SAS 资源，请访问 support.sas.com/publishing。

# 第 11 章：比较图与矩阵图

在本章中，我们将继续探索多单元图的世界。然而，我们不再创建按一个或多个分类变量分类的图表，而是将查看图网格，以提供数据的快速比较视图。

## 11.1 引言

比较图和矩阵图主要由数据集中多个响应变量或测量的散点图组成。这些图对于理解从现场获取的原始数据非常有价值。分析师通常希望通过“视觉”手段对数据建立感觉，并发现数据集之间的关系。这在项目的预分析阶段可以是一个非常有用的工具。

`SGATTER` 过程专门设计用于创建比较图或矩阵图形式的散点图。现在，你当然可以使用 `SGATTER` 过程创建带有拟合曲线和置信带的单单元散点图。然而，使用之前章节见过的 `SGPLOT` 过程来创建单单元图会更好。`SGATTER` 过程更适合创建带有少量拟合和置信图的散点图矩阵。

## 11.2 SGATTER 过程

该过程与 `SGPLOT` 和 `SGPANEL` 过程非常不同。该过程的语法更类似于 `GPLOT` 过程，如下：

```
proc sgcatter <options>;
nplot or compare or matrix statement;
run;
```

| 列 | 说明 |
| :--- | :--- |
| `DATA=`sas-data-set | 可选数据集 |
| `DESCRIPTION=`string | 描述字符串 |
| `DATTRMAP=`sas-data-set | 定义属性映射的数据 |
| `PAD=`value | 图表外围的填充 |
| `SGANNO=`sas-data-set | 包含注释的数据集 |
| `TMPLOUT=`string | 生成的图模板代码的文件 |

`SGATTER` 过程支持以下三个独立语句：

- `PLOT`– 创建多图面板
- `COMPARE`– 创建比较面板
- `MATRIX`– 创建正方形散点图矩阵

## 11.3 PLOT 语句

`PLOT` 语句根据“绘图请求”创建常规的散点图网格。该语句的语法如下：

```
plot plot-request < options>
```

绘图请求为下面列出的形式之一。根据绘图请求创建常规散点图网格：

- `y *` : 创建单个散点图。
- `y1 * x1 y2 * x2` : 创建包含两个定义的散点图的图。
- `(y1 y2) * x` : 创建包含两个独立图表 `y1 * x` 和 `y2 * x` 的图。
- `y * (x1 x2)` : 创建包含两个独立图表 `y * x1` 和 `y * x2` 的图。
- `(y1 y2) (x1 x2)` : 创建包含四个散点图的图。

### 要求的绘图请求：

| 绘图请求 | `y * x` or `(y1 y2) * x` or `(x1 x2)` or `(y1 y2) * (x1 x2)` |  |
| :--- | :--- | :--- |
| `ATTRID` | `=variable` | 用于视觉属性的相关映射 |
| `COLUMNS` | `=value` | 面板中的列数 |
| `DATABEL` | `=variable` | 用于标记点的变量 |
| `ELLIPSE` | `<=options>` | 为数据拟合置信椭圆 |
| `GROUP` | `= value` | 分组变量 |
| `JOIN` | `<=options>` | 连接数据点 |
| `LEGEND` | `=(options)` | 图例特征 |
| `LOESS` | `=(options)` | 为数据拟合曲线 |
| `MARKERATTRS` | `=marker-attr` | 指定属性 |
| `PBSLINE` | `=(options)` | 为数据拟合惩罚性样条 |
| `REG` | `=(options)` | 为数据拟合回归线 |
| `ROWS` | `=value` | 面板中的行数 |
| `SPACING` | `=value` | 行列之间的间距 |
| `TRANSPARENCY` | `=value` | 透明度 |
| `UNISECAL` | `=keyword` | X / Y 的统一缩放，默认为 NONE |

### 布尔选项：

| 选项 | 说明 |
| :--- | :--- |
| `GRID` | 显示边界 |
| `NOLEGEND` | 隐藏图例 |
| `REFTICK` | 显示刻度 |

### 图 11.3.1：基础散点图

这是一个身高与胆固醇的基础双单元散点图。每个图都指定为一个独立的请求。每个单元都有自己独立的数据范围轴。

![](img/0c09161c0be53934e5708cffbdcc441f_283_0.png)

```sas
title "Blood Pressure by Age";
proc sgscatter data=sashelp.heart;
plot height*cholesterol*agestart;
```

### 图 11.3.2：带有属性的散点图

这是与 11.3.1 相同的图，增加了标记属性和透明度。高透明度允许我们看到观测值的聚集情况。

![](img/0c09161c0be53934e5708cffbdcc441f_283_1.png)

```sas
title "Blood Pressure by Age";
proc sgscatter data=sashelp.heart;
plot height*cholesterol*agestart/
markerattrs=(symbol=circlefilled) transparency=0.96;
run;
```

Matange, Sanjay and Heath, Dan. *Statistical Graphics by Example: Effective Graphs Using SAS*. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。欲更多 SAS 资源，请访问 support.sas.com/publishing。

### 图 11.3.3：图网格 - 1 行 2 列

此图显示了随年龄变化的收缩压和收缩压。已启用网格线。注意两个 Y 轴的数据范围是统一的。

![](img/0c09161c0be53934e5708cffbdcc441f_284_0.png)

```sas
title "Patient Blood Pressure";
proc sgscatter data=sashelp.heart;
where sex="Male"
plot (diastolic systolic) * agestart / grid
markerattrs=(symbol=circlefilled) transparency=0.96;
run;
```

### 图 11.3.4：图网格 - 1 行 2 列

此图与图 11.3.3 相同。我们使用 `UNISCALE=Y` 使所有 Y 轴相同，显示测量的相对值。每个单元都有自己的 X 和 Y 轴。

![](img/0c09161c0be53934e5708cffbdcc441f_284_1.png)

```sas
title "Patient Blood Pressure";
proc sgscatter data=sashelp.heart;
where sex="Male"
plot (diastolic systolic) * agestart / grid uniscale=y
markerattrs=(symbol=circlefilled) transparency=0.96;
run;
```

### 图 11.3.5：带有拟合的图

此图与图 11.3.3 相同，增加了回归拟合和置信带。增加了标记的透明度，使拟合线和带更易可见。

![](img/0c09161c0be53934e5708cffbdcc441f_285_0.png)

```sas
# "Male Patients Blood Pressure Profile":
proc sgscatter data=sashelp.heart;
where sex='Male';
plot (diastolic systolic) * agestart / grid transparency=0.98
markerattrs=(symbol=circlefilled) uniscale=Y reg=(degree=2 cli);
run;
```

### 图 11.3.6：带有拟合和椭圆的图

此图使用了 B 样条拟合和置信椭圆。增加了标记的透明度，使拟合线和椭圆更容易可见。![](img/0c09161c0be53934e5708cffbdcc441f_285_1.png)

```sas
# "Male Patients Vital Signs Profile":
proc sgscatter data=sashelp.heart;
where sex='Male';
plot (diastolic systolic) * agestart / grid
pbspline=(cl degree=1) ellipse uniscale=Y
markerattrs=(symbol=circlefilled) transparency=0.98;
run;
```

Matange, Sanjay and Heath, Dan. *Statistical Procedures by Example: Effective Graphs Using SAS*. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。欲更多资源，请访问 support.sas.com/publishing。

### 图 11.3.7：多图请求

此图通过绘图请求在行内显示了随年龄变化的收缩压、收缩压以及胆固醇体重。显示了回归拟合。增加了标记的透明度，使拟合线和带更容易可见![](img/0c09161c0be53934e5708cffbdcc441f_286_0.png)

### 图 11.3.8：多图请求

此图显示了随年龄变化的收缩压、收缩压以及“随年龄变化的胆固醇”和“随死亡年龄”。显示了惩罚性 B 样条。设置标记透明度以使拟合线和椭圆更容易可见。

```sas
title "Male Patients Vital Signs Profile"
proc sgscatter data=sashelp.heart;
plot (diastolic systolic) * agestart cholesterol=*weight / grid Reg=(cli degree=2) markerattrs=(symbol=circlefilled) transparency=0.98 rows=1;
```

```sas
title "Male Patients Vital Signs Profile"
proc sgscatter data=sashelp.heart;
plot (diastolic cholesterol) * agestart ageatdeath * agestart ageatdeath / grid bsppline=(clm degree=1) ellipse uniscale=Y
markerattrs=(symbol=circlefilled) transparency=0.98 rows=1 ellipse;
```

![](img/0c09161c0be53934e5708cffbdcc441f_286_1.png)

### 图 11.3.9：对齐的并列图

这是一张关于女性和男性患者“药物 A”随时间变化的响应图。

我们使用了 `JOIN`、`UNISCALE` 和 `GRID` 选项。

![](img/0c09161c0be53934e5708cffbdcc441f_287_0.png)

```sas
title "Response over Time for Drug A";
proc sgscatter data=sggbook.seriesGroup2;
where drug="A";
plot (female male)*date / group grid unscale=Y join;
run;
```

### 图 11.3.10：对齐的并列图

这是一张按治疗方案女性和男性患者随时间变化的响应图。

我们使用了 `JOIN`、`UNISCALE` 和 `GRID` 选项。通过设置 `size=0` 抑制标记显示。

![](img/0c09161c0be53934e5708cffbdcc441f_287_1.png)

```sas
title "Response by Treatment over Time";
proc sgscatter data=sggbook.seriesGroup2;
plot (female male)*date / group drug grid unscale=Y join
markerattrs=(size=0);
run;
```

## 11.4 COMPARE 语句

`COMPARE` 语句创建散点图的网格。可以包含拟合线和椭圆。图形具有共同的行轴和列轴。默认情况下，单独列的 x 轴具有统一的数据范围。单独行的 y 轴具有统一的数据范围。

```
compare x=(var <var> ...) y=(var <var> ...) / options;
```
