
（续）

```
OUT=CARDATA; BY CYLINDERS;
PROC BOXPLOT DATA=CARDATA;
PLOT HWYMPG*CYLINDERS CBOXFILL=LIGHTGREEN;
WHERE CYLINDERS GT 1;
```

注意，在对比比较箱线图时，在运行 `PROC BOXPLOT` 过程之前，必须对分组变量上的数据进行排序。另外注意，`WHERE` 语句是必要的，因为有一辆车（马自 RX-8）被列为 -1 气缸，因为它使用的是转子发动机。你也可以将 -1 重新编码为缺失值以获得相同的结果。

2. 运行此程序并观察图 18.10 中的输出。

![](img/6113440fee6085d6edba5f406f54c127_0.png)
图 18.10 按气缸显示高速公路 MPG 的箱线图

3. 修改 `PLOT` 语句以包含以下内容：

```
PLOT HWMPG*CYLINDERS/
CBOXFILL=VLIG
CBOXES=BLACK
BOXSTYLE=SCHEMATIC
NOTCHES;
```

`CBOXFILL` 和 `CBOXES` 选项分别指定箱体的填充颜色和轮廓颜色。`BOXSTYLE` 请求 `SCHEMATIC` 样式，它指定图中显示的离群点类型。`SCHEMATIC` 选项将离群点定义为超过箱顶部或底部 1.5 倍（四分位距）的值。运行程序并观察图 18.11。

![](img/6113440fee6085d6edba5f40c128_0.png)
图 18.11 增强型箱线图

- 4. 为了显示离群点的 ID，将样式更改为 `SCHEMATIC` 并包含此处所示代码的 `ID MODEL` 语句。重新运行。（在这种情况下，某些 ID 文本重叠，导致结果难以阅读。）

```
PLOT HWYMPG*CYLINDERS/
CBOXFILL=VLIGE
CBOXES=BLACK
BOXSTYLE=SCHEMATICID
NOTCHES;
ID MODEL;
```

- 5. 为了在图上显示汇总统计数据，包含此处所示代码的 `INSETGROUP` 语句。重新运行并观察结果。

```
INSETGROUP (5) MIN MAX /
header = 'Mean and Extremes';
```

缺口是衡量两个位数差异的方法。如果两个图对应的缺口没有重叠，则表明在约 0.95 置信水平下位数显著不同。

第18章：创建图表

## 18.7 深入探索：使用 ODS 创建交互式条形图

第8章引入 ODS 的一个有用功能是在 HTML 模式下图形内部创建交互链接。要实现这一点，你需要创建一个超链接变量，然后将该链接应用于图表的一部分。以下示例使用 `PROC GCHART` 过程创建图形，其中每个条形都是指向报告的链接。

## 实践示例

此示例说明了如何在 SAS 图表中使用 HTML 链接。

- 1. 在编辑器窗口中，打开 `AGRAP10.SAS` 文件。

```sas
TITLE "Bar Chart";
PROC GCHART DATA=MYSASLIB.SOMEDATA;
HBAR GP/ DISCRETE;
RUN;
QUIT;
```

2. 运行此程序并观察它创建了一个由变量 `GP` 的三个类别组成的标准水平条形图。见图 18.12。

| 干预组 | FREQ. | FREQ. | PCT. | PCT. |
|---|---|---|---|---|
| A | | 11 | 22 | 22 |
| B | | 29 | 40 | 58 | 80 |
| C | | 10 | 50 | 20 | 100 |

图 18.12 钻取图，首次运行

假设对于图中由条形表示的每个“组”，你想提供一组背景统计数据。你可以将图上的每个条形关联到独立的网页上。因此，每个条形都变成了一个网页链接，当你点击图上的条形时，会打开一个 HTML 页面。图 18.13 所示的代码创建了一个包含你想与组 A 关联的报告（来自 `PROC MEANS`）的 HTML 文件（我们将在稍后的示例中再次看到此代码）。注意 HTML 报告保存在名为 `GPA.HTM` 的文件中，并且包含关于 `GP="A"` 的信息。（记住在 ODS HTML 中格式化文件是使用 `BODY=`）。

图 18.13 创建的报告见表 18.12。我们将在稍后的示例中创建此和其他表。

要定义引导用户到此报告的链接，可以在 `DATA` 步中使用标准的 `IF` 语句，如下：

## 深入探索：创建交互式条形图

ODS 代码指定了保存输出的 HTML 文件。

```
ODS HTML BODY="C:\SAS\GPA.HTM"
PROC MEANS DATA="C:\SAS\SOMEDATA"
VAR AGE;
WHERE GP="A";
RUN;
ODS CLOSE;
```

图 18.13 创建 HTML 的代码

### 表 18.12 A 的报告

| 变量 | 标签 | 平均值 | 标准差 |
|---|---|---|---|
| A 的汇总 | | | |
| MEANS过程 | | | |
| AGE | | | |
| N | | 11 | |
| Mean | | 22.0 | |
| Std Dev | | 1.5 | |

HTML 代码创建了我们要保存的报告。

HTML 语句指定了保存输出的 HTML 文件。

```
ODS HTML BODY="C:\SAS\GPA.HTM"
PROC MEANS DATA="C:\SAS\SOMEDATA"
VAR AGE;
WHERE GP="A";
RUN;
ODS CLOSE
;

| Summary for A | | | |
| Procedure MEANS | | | |
| AGE | | | |
| N | | 11 | |
| Mean | | 22.0 | |
| Std Dev | | 1.5 | |

