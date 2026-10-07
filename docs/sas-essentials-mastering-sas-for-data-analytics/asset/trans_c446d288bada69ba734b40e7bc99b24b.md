
(续)

```
AXIS1 ORDER=(4 TO 12 BY 1)
LABEL=('Number of Cylinders' F=SWISS HEIGHT=4)
OFFSET=(5);
AXIS2 ORDER=(0 TO 90 BY 5)
LABEL=(A=90 'Highway Miles Per Gallon' F=SWISS
HEIGHT=4)
OFFSET=(5);
PROC GPLOT DATA=MYSALIB.CARS
 PLOT HWYMP*CYLINDERS/AXIS=AXIS1 VAXIS=AXIS2;
 SYMBOL1=STD1JT H=1 LINE=1 VALUE=NONE;
```

RUN;
QUIT;
```
此图根据汽车发动机气缸数（CYLINDERS）绘制高速公路每加英里英数（HWYMP）。注意，SYMBOL1语句中的 `I=STD1JT` 插值选项请求显示 1 个标准差误差棒。`VALUE=NONE` 选项会压缩单个点的图表。`AXIS1`语句要求 x 轴仅包含 4 到 12 之间的值，因为这是数据集中气缸的数量。

- 2. 运行程序并观察图18.4中的输出。
3. 修改插值选项，以请求在须末端带有顶部的箱线图：

```
I=BOXT
运行修改后的程序并观察输出。
```

![](img/6113440fee6085d6edba5f406f541c12_415_0.png)

**图 18.4** 显示误差棒的 PROC GPLOT

自定义 SAS GPLOT 其他方法。请参阅附录 A 和 SAS 文档获取更多选项。

## 18.2 创建条形图和饼图

你可以生成条形图和饼图来显示频率数据的计数或百分比。这些图表是使用 SAS GCHART 过程创建的。简写语法如下：

```
PROC GCHART <DATA=dataset>;
HBAR|HBAR3D VBAR|VBAR3D chartvar(s) / chartoption(s);
PIE|PIE3D|DONUT|STAR chartvar(s) / chartoption(s);
```

图表类型规格（如 HBAR 和 VBAR）指的是水平条形图、垂直条形图、饼图以及这些图表的三维（3D）版本。例如：

```
PROC GCHART DATA=MYDATA;
HBAR STATUS/DISCRETE OUTLINE=BLUE OUTLINE=3;
```

表18.7 列出了一些 GCHART 语句。条形选项的常用选项列在表18.8 中。其他语句和选项请参阅 SAS 文档。

PROC GCHART 的简单示例是水平条形图（HBAR），在接的实例示例所示。

## 表格 18.7 PROC GCHART 常用选项

| 选项 | 解释 |
| --- | --- |
| DATA=*datame | 指定要使用的数据集 |
| HBAR, HBAR3D, VBAR, VBAR3D, PIE, PIE3D, DONUT, 或 STAR | 指定要创建的图表类型。`/HTML=variable` 指定一个包含 HTML 链接地址的变量。 |
| AXIS, FOOTNOTE, PATTERN, TITLE | 这些是可以用于增强图表的语句。本章中的示例说明了这些选项 |
| BY, FORMAT, LABEL, WHERE | 这些语句适用于大多数过程，此处可以使用 | |

## 表格 18.8 条形图的常用 GCHART 选项

| 选项 | 解释 |
| --- | --- |
| CAXIS=color | 指定用于轴、框架或文本的颜色。例如，CAXIS=BLUE |
| CFRAME=color | OUTLINE 指定条形轮廓的颜色（或 SAME），OUTLINE 指定轮廓宽度。默认宽度为 1。例如， |
| CTEXT=color | |
| OUTLINE=color OUTLINE=n | OUTLINE=BLUE OUTLINE=3 |
| DISCRETE | 将数值变量视为离散的（分类的） |
| GROUP variable | 使用指定的分类变量将条形拆分组 |

(续)

## 第 18 章：创建自定义图表

## 表格 18.8（续） |
| 选项 | 解释 |
|---|---|
| SUBGROUP variable | 根据 GROUP 变量定义的组内的子组，指定条形的特征（即为每个子组显示不同的颜色） |
| WIDTH=n | WIDTH 指定条形宽度，SPACE 指定条形之间的空间 |
| INSIDE=statistic | 决定是否在图表中显示统计数据。统计数据为 MEAN、SUM、PERCENT (PCT) 或 FREQ。定义要计算的统计数据（显示在图表上）。选项包括 SUM、MEAN、PERCENT (PCT) 和 FREQ（默认） |
| TYPE=statistic | 定义响应变量。当你使用此选项 TYPE= 时，为 MEAN 或 SUM |
| NOLEGEND | 抑制图表图例 |
| CLM=p | 指定要显示的置信区间水平。例如，CLM=95 |
| ERRORBAR=type | 指定 TOP、BARS 或 BOTH |
| HTML= | 为显示的类别定义 HTML 链接。当点击代表组的图表图像（由条形、饼图等表示）时，将激活为该组定义的 HTML 地址。例如，HTML="http://www.cnn.com" |

这些选项出现在 `/` 之后。

## 实际上练的示例

此示例说明了如何创建水平条形图。

- 1. 打开程序 FILE AGRAPH4.SAS。
```sas
OPTIONS RESET=ALL;
Title "Horizontal Bar Chart";
PROC GART DATA="C:\SASDATA\SOMEDATA";
HBAR STATUS=DISCRETE;
RUN;
QUIT;
```
此代码请求在 STATUS 变量上生成水平条形图。`/DISCRETE` 选项告诉 SAS STATUS 变量的数值应被视为离散值。否则，SAS 可能会假设数值是范围，并使用中点而非实际值创建图表。
- 2. 运行程序并观察图 18.5 中的输出。
3. 将 HBAR 改为 VBAR 并重新运行程序，观察输出。
4. 通过添加 `WIDTH=10` 修改语句：

```sas
VBAR STATUS=DISCRETE WIDTH=10;
```

## 定义图表模式

重新运行程序并观察输出。WIDTH 语句是如何改变图表的？
移除 `WIDTH=10` 语句并将 HBAR 改为 VBAR，重新运行程序并观察输出。
如果女性和男性条形使用不同的颜色，此图的视觉冲击可能可能剧烈。为了实现这一点，我们可以使用 SUBGROUP=GENDER 命令，并使用 PATTERN2 语句定义第二个条形的颜色。
打开程序文件 AGRAPH6.SAS。

```sas
OPTIONS RESET=ALL;
TITLE 'Bar Chart by Group with different bar colors';
PROC GCHART DATA="C:\SASDATA\SOMEDATA";
VBAR GENDER/GROUP=GP SUBGROUP=GENDER;
PATTERN1 VALUE=R1 COLOR=RED;
RUN;
QUIT;
```
