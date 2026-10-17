
重新提交代码并观察结果。注意 `CTEXT=` 选项带来的变化![](61344fee6085d6edba5f406f12_07.png) 使用 `PROC GPLOT` 的默认散点图

## 18.1.2 管理你的 SAS 图表

如前所述，当你在 SAS 中创建图表时，结果会被于结果查看器（Results Viewer）中。以下是在结果查看器中工作的一些实用提示。

### 表 18.3 `PROC GPLOT` `PLOT` 语句的常用选项

| 选项 | 解释 |
| --- | --- |
| `CAXIS=color` | 指定线条和刻度线的颜色。颜色在附录 A 中描述。例如，`CAXIS=BLUE` |
| `FRAME=color` | 指定背景框的颜色。颜色在附录 A 中描述 |
| `CTEXT=color` | 指定文本颜色。颜色在附录 A 中描述。指定水平或垂直轴的信息，包括刻度的值和间距。例如，`HAX=AXISK` – 表示将 `AXIS` 定义应用到水平轴。例如，`HAX=AXIS1` 表示应用 `AXIS1` 定义。`VARIS=AXISK` 表示将 `AXIS` 定义应用到垂直轴。例如，`VARIS=AXIS2` 表示应用 `AXIS2` 定义 |
| `HREF=value list` | 在指定的轴值处绘制水平线或垂直线或 |
| `VREF=value list` | |
| `LEGEND=legend<n>` | 指定图表使用哪种图例定义。本章给出了一个示例 | 抑制标准的图表图例 |
| `SYMBOL<n>` | 允许你指定用于点的符号，以及该符号的属性（如颜色和大小）。符号列表请参阅附录 A。详见下文“使用 `SYMBOL` 语句增强 `GPLOT`”节 |
| `NOFRAME GRID` | 抑制图表周围（默认）的框。在主刻度处绘制网格线 |

这些选项出现在 `/` 之后。

- 复制图表：要复制到剪贴板并粘贴到 Word、PowerPoint 或其他程序中，点击图表并从菜单栏选择“编辑 → 复制”（或右键点击图表并选择复制）。
- 导出图表：要将图表导出为标准图形文件，右键点击图表，选择“另存为……”，根据所需的输出类型选择文件类型。有 `PNG` 和 `BIT`（位图）。查看本节后面的“保存图表”部分了解如何通过程序以其他格式保存图表。
- 打印：使用“文件 → 打印”菜单选项打印图表的纸质副本。（或选择右键...)

## 18.1.3 使用 `SYMBOL` 语句增强 `GPLOT`

显示散点图的目的是为了两个变量之间的关联。你可能希望在散点中包含一条回归线，或者想对图表进行改进。以下示例展示了如何使用 `SYMBOL` 语句来增强图表。该语句可以出现在 `PROC GPLOT` 语句之前或内部。`SYMBOL` 语句的简写语法如下：

```
SYMBOL=1...255
<COLOR=symbol-color>
<appearance-option(s)>
<INTERPOLATION=interpolation-option>;
```

示例语句为 `SYMBOL1VARRL CBLUE L2`;

数字表示将选项应用于哪个图。`SYMBOL` 的常用选项见表 18.4。以下示例说明了 `SYMBOL` 语句及其部分选项。

### 表 18.4 `PROC GPLOT` `SYMBOL` 语句的常用选项

| 选项 | 解释 |
| --- | --- |
| `COLOR=color` (or `C=`) | 指定图中点的颜色。`CBLUE` 使图中的点变为蓝色。其他常用选项有 `RED`、`GREEN` 和 `BLACK`。更多颜色列表请参阅附录 A |
| `INTERPOLATION=type` (or `I=`) | 指示 SAS 在图中包含插值曲线。有多种类型的插值曲线。常用选项是 `RL` 或线性拟合。常用选项如下：<br>- `RL` - 线性回归<br>- `RQ` - 二次回归<br>- `RC` - 三次回归<br>- `STDK` - 长度为 k 的标准误差棒 `STDEV` [在连接处添加 J]，`B` [包含误差棒]，`T` [在误差棒顶部添加]。例如，`STJK` 连接误差棒<br>- `STDM` - 同 `STDK` 但使用均值标准误差<br>- `JOIN` - 连接<br>- `BOXT` - 框 |
| `LINE=n` (or `L=`) | 指定图中线条的模式。例如，`LINE=1` 产生实线。值2 产生小点，3 更大。更多选项请参阅附录 A |
| `VALUE=n` (or `V=`) | 指定图表上点使用的符号。例如，`V=STAR` 使用星号代替默认字符 (+)。常用符号有正方形、星号、圆形、加号和点。更多选项请参阅附录 A |

# 使用 `GPLOT` 创建散点图和折线图

### 实例演示

本示例演示了如何更改图表中点和回归线的样式。

- 1. 打开程序文件 `AGRAPH2.SAS`。

```sas
OPTIONS RESET=ALL;
Title "Simple Scatterplot, Change symbol";
PROC GPLOT DATA=MYASLIB.CARS
PLOT HWY*CITYMPG
SYMBOL V1=STAR I=RL C=BLUE;
RUN;
QUIT;
```

- 2. 运行此程序并观察图18.2。注意屏幕上显示的以下项目（更多信息见附录 A）：
  * 显示的符号为星形 (`V=STAR`)。
  * 显示的符号为蓝色 (`C=BLUE`)。
  * 显示回归线 (`I=RL`)。
  * 显示的线条为虚线 (`L=2`)。

- 3. 通过附录 A 列出的定义值更改 `C`、`V` 和 `L` 选项，并重新运行程序以观察这些选项如何修改图表。

![](img/61344fee6085d6ba5f406c12_410_0.png)

图18.2 指定了点和线的 `GPLOT`

## 18.1.4 图中的轴自定义

如果你正在为项目演示或出版准备图表，可能想要更改图轴的特征。以下实例演示了一些基本技术。`AXIS` 语句的语法为：

```
AXIS<n> <options>;
```

其中 `n` 定义特定轴的选项，例如 `AXIS1`、`AX2` 等。将轴定义应用于图表需要以下两个步骤：

- 步骤1：使用 `AXIS<n>` 语句定义轴。
- 步骤2：将定义的轴关联到图中的特定轴。`GPLOT` 和 `GCHART`（后续章节讨论）具有不同的轴名称，见表18.5。

轴选项定义了轴的“外观”：比例、外观、刻度和文本。作为 `GPLOT` 过程的一个示例，以下代码定义了 `AXIS1`。这是使用轴的步骤1。

```sas
AXIS1=C ORDER=(0 TO 80 BY 5)
LABEL=('City Miles Per Gallon' FONT=SWISS)
OFFSET=(5) WIDTH=2 VALUE=(H=2);
```

要将此应用于图表（使用轴的步骤2），可以使用如下代码：

```sas
PROC GPLOT DATA=CARS;
PLOT HWY+CITYMG/HAXIS=AXIS;
```

## 18.5 `GPLOT` 和 `GCHART` 的轴名称

| `GPLOT` 轴名称 | 指代哪个？ |
|---|---|
| `HAXIS` | `AXIS=AXIS<n>` 将 `axis<n>` 的定义应用于水平轴，在标准 X-Y 图中称为 X 轴。 |
| `VAXIS` | `AXIS=AXIS<n>` 将 `axis<n>` 的定义应用于垂直轴，在标准 X-Y 图中称为 Y 轴。 |
| `GCHART` 轴名称 | |
| `MAXIS` | `AXIS=AXIS<n>` 将 `axis<n>` 的定义应用于中点轴，该轴与分组（分类）相关。 |
| `GAXIS` | `AXIS=AXIS<n>` 将 `axis<n>` 的定义应用于分组轴，当你使用 `GROUP=` 语句时（见下方示例）。 |
| `RAXIS` | `RAXIS=AXIS<n>` 将 `axis<n>` 的定义应用于响应轴，该轴与计数、百分比或频率相关。 |

## 18.6 `PROC GPLOTS` `AXIS` 语句的常用选项

| 选项 | 解释 |
| --- | --- |
| `COLOR=color` (or `C=`) | 指定图表中轴的颜色。例如，`C=BLUE` 使轴变为蓝色。其他常用颜色有 `RED`（红色）、`GREEN`（绿色）和 `BLACK`（黑色）。可用颜色列表见附录 A。 |
| `LABEL=(specifications)` | 指定轴标签的特征。文本参数定义了标签外观的部分，包括角度、颜色、字体、对齐和旋转角度 (`A`)，其中 `A=90` 表示以 90° 角显示标签（垂直）。`LABEL=NONE` 抑制标签。标签语句示例为 `LABEL=(H=4 J=C C=BLUE "My Axis")`；其中 `H=4` 指定文本高度，`J=C` 居中对齐，`C=BLUE` 指定文本颜色。 |
| `ORDER=(list)` | 指定轴上值的顺序。例如，`ORDER=(1 to 100 by 5)` 指定轴将包含 1-100 的数字，标签增量为 5。 |
| `VALUE=(options)` | 指定文本的高度（以及其他项目）——例如，`VALUE=(H-4)`。 |
| `WIDTH=thickness` | 指定轴的宽度（影响整个框架的宽度，无 `NOFRAME` 选项时定义所示）。 |
| `OFFSET=(x, y) <UNITS>` | 将轴水平方向远离 X 轴，例如，`OFFSET=(3,4)` 将 X 轴水平移动 3%，Y 轴垂直移动 4%。你也可以指定 `(3,4)pct`、`cm (3,cm)` 或英寸 `(3,4)in`。百分比是默认文本格式。例如，使用 `A=90` 将水平轴置于 90° 角以对齐轴。 |
| `A=n` | 控制刻度。例如，`MAJOR=(COLOR=BLUE HEIGHT=3 WIDTH=2)`。 |
| `MIN=(options)` | 控制刻度。`MIN=NONE` 不显示刻度。例如，`MIN=(NUMBER=4 COLOR=RED HEIGHT=1)`。 |
| `JUSTIFICATION=type` (`J=`) | 对齐方式，`L=Left`（左对齐），`C=Center`（居中对齐），`R=Right`（右对齐）。 |

`AXIS` 语句创建一个红色的水平轴（`HAXIS`），刻度从 0 到 80，步长为 5。轴标签为 "City Miles Per Gallon" 并使用 Swiss 字体。

(续)

```sas
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
`RUN;`
`QUIT;`

此图根据汽车发动机气缸数（`CYLINDERS`）绘制高速公路每加英里英数（`HWYMP`）。注意，`SYMBOL1`语句中的 `I=STD1JT` 插值选项请求显示 1 个标准差误差棒。`VALUE=NONE` 选项会压缩单个点的图表。`AXIS1`语句要求 x 轴仅包含 4 到 12 之间的值，因为这是数据集中气缸的数量。

- 2. 运行程序并观察图18.4中的输出。

3. 修改插值选项，以请求在须末端带有顶部的箱线图：

```
I=BOXT
```
运行修改后的程序并观察输出。

![](img/6113440fee6085d6edba5f406f541c12_415_0.png)

**图 18.4** 显示误差棒的 `PROC GPLOT`

自定义 SAS `GPLOT` 其他方法。请参阅附录 A 和 SAS 文档获取更多选项。

## 18.2 创建条形图和饼图

你可以生成条形图和饼图来显示频率数据的计数或百分比。这些图表是使用 SAS `GCHART` 过程创建的。简写语法如下：

```
PROC GCHART <DATA=dataset>;
HBAR|HBAR3D VBAR|VBAR3D chartvar(s) / chartoption(s);
PIE|PIE3D|DONUT|STAR chartvar(s) / chartoption(s);
```

图表类型规格（如 `HBAR` 和 `VBAR`）指的是水平条形图、垂直条形图、饼图以及这些图表的三维（3D）版本。例如：

```
PROC GCHART DATA=MYDATA;
HBAR STATUS/DISCRETE OUTLINE=BLUE OUTLINE=3;
```

表18.7 列出了一些 `GCHART` 语句。条形选项的常用选项列在表18.8 中。其他语句和选项请参阅 SAS 文档。

`PROC GCHART` 的简单示例是水平条形图（`HBAR`），在接的实例示例所示。

## 表格 18.7 `PROC GCHART` 常用选项

| 选项 | 解释 |
| --- | --- |
| `DATA=datame` | 指定要使用的数据集 |
| `HBAR, HBAR3D, VBAR, VBAR3D, PIE, PIE3D, DONUT, 或 STAR` | 指定要创建的图表类型。`/HTML=variable` 指定一个包含 HTML 链接地址的变量。 |
| `AXIS, FOOTNOTE, PATTERN, TITLE` | 这些是可以用于增强图表的语句。本章中的示例说明了这些选项 |
| `BY, FORMAT, LABEL, WHERE` | 这些语句适用于大多数过程，此处可以使用 |

## 表格 18.8 条形图的常用 `GCHART` 选项

| 选项 | 解释 |
| --- | --- |
| `CAXIS=color` | 指定用于轴、框架或文本的颜色。例如，`CAXIS=BLUE` |
| `CFRAME=color` | `OUTLINE` 指定条形轮廓的颜色（或 `SAME`），`OUTLINE` 指定轮廓宽度。默认宽度为 1。例如， |
| `CTEXT=color` | |
| `OUTLINE=color OUTLINE=n` | `OUTLINE=BLUE OUTLINE=3` |
| `DISCRETE` | 将数值变量视为离散的（分类的） |
| `GROUP variable` | 使用指定的分类变量将条形拆分组 |

(续)

## 第 18 章：创建自定义图表

## 表格 18.8（续）

| 选项 | 解释 |
|---|---|
| `SUBGROUP variable` | 根据 `GROUP` 变量定义的组内的子组，指定条形的特征（即为每个子组显示不同的颜色） |
| `WIDTH=n` | `WIDTH` 指定条形宽度，`SPACE` 指定条形之间的空间 |
| `INSIDE=statistic` | 决定是否在图表中显示统计数据。统计数据为 `MEAN`、`SUM`、`PERCENT (PCT)` 或 `FREQ`。定义要计算的统计数据（显示在图表上）。选项包括 `SUM`、`MEAN`、`PERCENT (PCT)` 和 `FREQ`（默认） |
| `TYPE=statistic` | 定义响应变量。当你使用此选项 `TYPE=` 时，为 `MEAN` 或 `SUM` |
| `NOLEGEND` | 抑制图表图例 |
| `CLM=p` | 指定要显示的置信区间水平。例如，`CLM=95` |
| `ERRORBAR=type` | 指定 `TOP`、`BARS` 或 `BOTH` |
| `HTML=` | 为显示的类别定义 HTML 链接。当点击代表组的图表图像（由条形、饼图等表示）时，将激活为该组定义的 HTML 地址。例如，`HTML="http://www.cnn.com"` |

这些选项出现在 `/` 之后。

## 实际上练的示例

此示例说明了如何创建水平条形图。

- 1. 打开程序 `FILE AGRAPH4.SAS`。

```sas
OPTIONS RESET=ALL;
Title "Horizontal Bar Chart";
PROC GART DATA="C:\SASDATA\SOMEDATA";
HBAR STATUS=DISCRETE;
RUN;
QUIT;
```

此代码请求在 `STATUS` 变量上生成水平条形图。`/DISCRETE` 选项告诉 SAS `STATUS` 变量的数值应被视为离散值。否则，SAS 可能会假设数值是范围，并使用中点而非实际值创建图表。

- 2. 运行程序并观察图 18.5 中的输出。

3. 将 `HBAR` 改为 `VBAR` 并重新运行程序，观察输出。

4. 通过添加 `WIDTH=10` 修改语句：

```sas
VBAR STATUS=DISCRETE WIDTH=10;
```

## 定义图表模式

重新运行程序并观察输出。`WIDTH` 语句是如何改变图表的？

移除 `WIDTH=10` 语句并将 `HBAR` 改为 `VBAR`，重新运行程序并观察输出。

如果女性和男性条形使用不同的颜色，此图的视觉冲击可能可能剧烈。为了实现这一点，我们可以使用 `SUBGROUP=GENDER` 命令，并使用 `PATTERN2` 语句定义第二个条形的颜色。

打开程序文件 `AGRAPH6.SAS`。

```sas
OPTIONS RESET=ALL;
TITLE 'Bar Chart by Group with different bar colors';
PROC GCHART DATA="C:\SASDATA\SOMEDATA";
VBAR GENDER/GROUP=GP SUBGROUP=GENDER;
PATTERN1 VALUE=R1 COLOR=RED;
RUN;
QUIT;
```

`PATTERN2 VALUE=R1 COLOR=BLUE;`

`RUN;`

`QUIT;`

新增的 `SUBGROUP=` 语句。它告诉 SAS 使用不同的颜色为每个子组的条形染色。`PATTERN` 语句指定了男性的颜色，因为模式是按照字母顺序分配的。

![](img/6113440fee6085d6edba5f406f541c12_420_0.png)

- 4. 运行程序并观察输出。注意每个 `GENDER` 的条形现在是不同的颜色。由于两个 `PATTERN` 语句中都使用了 `VALUE=R1` 指定，`PATTERN` 保持不变。

- 5. 将 `PATTERN1` 中的语句更改为 `VALUE=X4` 并重新运行程序，查看这将如何改变输出。

- 6. 将 `VBAR` 改为 `VBAR3D`。注意条形的颜色仍然保留，但 `PATTERN` 选项不再生效。
