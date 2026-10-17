
## 显示外部辅助轴

`DISPLAYSECONDARY` 选项可用于 `ROWAXIS` 语句以便在晶格右侧显示行。它可以用于 `COLUMNAXIS` 语句以便在晶格顶部显示列轴。这些外部辅助轴是外部主轴的副本，而不是真正的独立轴。然而，你可以更改在辅助轴上显示的特征。在以下示例中，刻度和刻度值在晶格右侧重复，但通过不列出请求的特征来抑制轴标签。

```
layout lattice / columns=2 colgutter=5px
columdatarange=unionall
rowdatarange=union;

histogram mpg_city;

histogram mpg_highway;

rowaxes;
rowaxis / griddisplay=on secondary=(ticks tickvalues);
endrowaxes;
endlayout;
```

![](img/a9ccb6123dee40d424cb295a3a99c16c_247_0.png)

## 次要轴

## 外部轴与空单元

如果 `LATTICE` 布局生成了空单元且存在外部轴，则行轴或列轴可能会显示在一个多个空单元附近。以下示例显示了默认情况：

```
layout lattice / columns=2 rows=2
rowgutter=5px columngutter=5px
rowdatarange=unionall columndatarange=unionall;

/* overlay blocks define cells 1-3 */
layout overlay;
  entry "Spline Fit" / valign=top;
  scatterplot y=weight x=height;
  pbspline y=weight x=height;
endlayout;

layout overlay;
  entry "Loess Fit" / valign=top;
  scatterplot y=weight x=height;
  loessplot y=weight x=height;
endlayout;

layout overlay;
  entry "Regression Fit" / valign=top;
  scatterplot y=weight x=height;
  regressionplot y=weight x=height;
endlayout;

rowaxes;
rowaxis;
rowaxis;
endrowaxes;

columnaxes;
columnaxis;
columnaxis;
endcolumnaxes; /* 注意：修正了 OCR 中的写错误 */
endlayout;
```

## 创建跨行或列的统一轴

![](img/a9ccb6123dee40d424cb295a3a99c16c_248_0.png)

在 `LAYOUT LATTICE` 语句中添加 `SKIPEMPTYCELLS=TRUE` 设置可以消除通常为空单元留的空间。在这种情况下，原本可能显示在空单元附近的外部轴将显示在有数据的单元附近：

```
layout lattice / columns=2 rows=2
rowgutter=5px columngutter=5px
rowdatarange=unionall columndatarange=unionall
skipemptycells=true;
```

## 使用 SKIPEMPTYCELLS=TRUE 的外部轴与空单元

![](img/a9ccb6123dee40d424cb295a3a99c16c_249_0.png)

## 定义带有额外功能的 Lattice

### 概述：定义 Lattice

接下来的章节解释了如何生成第 241 页的图 10.3，这需要完成以下任务：

- 转换输入数据
- 使用外部轴代替内部单元格轴
- 添加显示描述性文本的侧边栏
- 使用列标题
- 调整行大小。

### 图 10.3 股票图

![](img/a9ccb6123dee40d424cb295a3a99c16c_250_0.png)

### 转换输入数据

Lattice 的常见用途是创建一个显示相同输入数据不同子集的图表。在某些情况下，这些子集已经在输入数据中定义好了。然而，你经常需要转换输入数据，以适应你尝试创建的图表。这可能需要以下任何或全部操作：

- 汇总数据
- 转置数据
- 缩放数据值
- 创建代表数据子集的新变量。

第 241 页图 10.3 显示的图基于 `Sashelp.stocks` 中的数据，该数据包含三家公司多年的每月股票信息。数据包含 `Stock`（股票）、`Date`（日期）、`Volume`（量）和 `AdjClose`（调整收盘价）列。然而，它并没有图表所需的量和价格格式。`LATTICE` 布局不支持按单元格划分输入数据的子集。因此，为了使单元格内容不相同，必须为每个单元创建唯一的变量，以提供适当的数据、量和价格信息。以下 `DATA` 步执行了必要的数据转换。

```
data stock;
set sashelp.stocks;
where stock = "Microsoft" and year(date) in (2004 2005);
format Date2004 Date2005 date.;
format Price2004 Price2005 dollar8.;
label Date2004="2004" Date2005="2005";
if year(date) = 2004 then do;
  Date2004=date;
  Vol2004=volume/10**6;
  Price2004=adjclose;
end;
else if year(date)=2005 then do;
  Date2005=date;
  Vol2005=volume/10**6;
  Price2005=adjclose;
end;
keep Date2004 Date2005 Vol2004 Vol2005 Price2004 Price2005;
run;
```

数据对微软在 2004 年和 2005 年的数据进行了过滤。接下来，为每年的量和股票价格创建了新变量。由于量很大，因此它们被缩放了。这种缩放会导致产生“稀疏”数据，但对于缺失 X 或 Y 值的 lattice 观测值来说是正确的组织。

| Date2004 | Date2005 | Price2004 | Vol2005 |
|---|---|---|---|
| 1 | 01DEC | $26 | 62.8924 |
| 2 | 01NOV | $27 | 71.4692 |
| 3 | 03OCT | $25 | 72.1325 |
| 4 | 01SEP | $25 | 66.9765 |
| 5 | 01AUG | $25 | 65.5300 |
| 6 | 01JUL | $25 | 69.0466 |
| 7 | 01JUN | $25 | 62.9567 |
| 8 | 02MAY | $25 | 62.6998 |
| 9 | 01APR | $25 | 77.0902 |
| 10 | 01MAR | $74 | 72.8997 |
| 11 | 01FEB | $25 | 75.9923 |
| 12 | 01JAN | $26 | 79.6428 |
| 13 | 01DEC | $26 | 84.4881 |
| 14 | 01NOV | $26 | 86.4461 |
| 15 | 01OCT | $25 | 65.7429 |
| 16 | 01SEP | $24 | 57.7253 |
| 17 | 01JAN | $24 | 52.1046 |
| 18 | 01JUL | $25 | 76.6667 |
| 19 | 01JUN | $25 | 77.0683 |
| 20 | 03MAY | $23 | 58.9425 |
| 21 | 01APR | $23 | 77.3867 |
| 22 | 01MAR | $23 | 77.1119 |
| 23 | 02FEB | $23 | 57.3859 |
| 24 | 02JAN | $24 | 63.6359 |

需要注意的关键点是每个单元都使用包含其重要信息的变量。不能在模板定义中使用 `WHERE` 来形成数据的子集。以下初始模板定义了 lattice：

```
proc template;
define statgraph lattice;
begingraph;
entrytitle "Microsoft Stock";
layout lattice / columns=2 rows=2;
/* row 1 */
layout overlay;
  seriesplot y=Price2004 x=Date2004 / lineattrs=GraphData;
endlayout;
layout overlay;
  seriesplot y=Price2005 x=Date2005 / lineattrs=GraphData;
endlayout;
/* row 2 */
layout overlay;
  needleplot y=Vol2004 x=Date2004 / lineattrs=GraphData(thickness=2px pattern=solid);
endlayout;
layout overlay;
  needleplot y=Vol2005 x=Date2005 / lineattrs=GraphData(thickness=2px pattern=solid);
endlayout;
endlayout;
endgraph;
end;
run;

proc sgrender data=stock template=lattice;
run;
```

注意，由于 `Date2004` 和 `Date2005` 关联了 SAS 格式，因此使用了时间轴，变量标签用于 X 轴标签。

### 图 10.4 图表的初始 Lattice

![](img/a9ccb6123dee40d424cb295a3a99c16c_252_0.png)

### 使用外部轴

第 243 页的图 10.4 将受益于 X 轴和 Y 轴的外部化，因为外部轴减少了冗余 X 轴信息并统一了 Y 轴范围。我们还希望为所有轴添加网格线。为了节省 X 轴空间，在下面的模板代码中关闭了每个时间轴的自动格式。`TICKVALUEFORMAT=MONNAME1.` 设置指示了如何格式化时间轴值。

```
proc template;
define statgraph lattice2;
begingraph / width=495px height=370px;
entrytitle "Microsoft Stock Performance";
layout lattice / columns=2 rows=2
rowdatarange=union columndatarange=union
rowgutter=3px columngutter=3px;

/* define row 1 */
layout overlay;
  seriesplot x=Date2004 y=Price2004 / lineattrs=GraphData;
endlayout;
layout overlay;
  seriesplot x=Date2005 y=Price2005 / lineattrs=GraphData;
endlayout;

/* define row 2 */
layout overlay;
  needleplot x=Date2004 y=Vol2004 / lineattrs=GraphData(thickness=2px pattern=solid);
endlayout;
layout overlay;
  needleplot x=Date2005 y=Vol2005 / lineattrs=GraphData(thickness=2px pattern=solid);
endlayout;

rowaxes;
rowaxis / griddisplay=on display=(label tickvalues) label="Price" labelattrs=(weight=bold);
rowaxis / griddisplay=on display=(label tickvalues) label="Volume" labelattrs=(weight=bold);
endrowaxes;

columnaxes;
columnaxis / griddisplay=on display=(label tickvalues) label="Date" labelattrs=(weight=bold) timeopts=(tickvalueformat=monname1.);
columnaxis / griddisplay=on display=(label tickvalues) label="Date" labelattrs=(weight=bold) timeopts=(tickvalueformat=monname1.);
endcolumnaxes;
endlayout;
endgraph;
end;
run;

proc sgrender data=stock template=lattice2;
run;
```

### 图 10.5 带有外部轴的网格

![](img/a9ccb6123dee40d424cb295a3a99c16c_254_0.png)

### 使用单元格轴

在轴外部化可以改善图表外观并简化代码编写的情况下。然而，如果某些轴选项无法统一应用于列或行中的所有轴，则你需要以单元格为单位使用标准轴选项，而不是外部轴。

例如，如果你希望 X 轴网格线出现在图表的第一行，而不是第二行，你就不能使用外部轴。相反，你将把单元格内容封装在覆盖层（overlay）类型的布局块中，并在布局语句上添加 `XAXISOPTS=` options，如下所示块所示：

```
/* overlay 块为第 1 行定义 X 轴选项 */
layout overlay / xaxisopts=(display=none) griddisplay=on;
  seriesplot x=Date2004 y=Price2004 / lineattrs=GraphData;
endlayout;

layout overlay / xaxisopts=(display=none) griddisplay=on;
  seriesplot x=Date2005 y=Price2005 / lineattrs=GraphData;
endlayout;

/* overlay 块为第 2 行定义 X 轴选项 */
layout overlay / xaxisopts=(display=(label tickvalues)) timeopts=(tickvalueformat=monname1.);
  needleplot x=Date2004 y=Vol2004 / lineattrs=GraphData2(thickness=2px pattern=solid);
endlayout;

layout overlay / xaxisopts=(display=(label tickvalues)) timeopts=(tickvalueformat=monname1.);
  needleplot x=Date2005 y=Vol2005 / lineattrs=GraphData2(thickness=2px pattern=solid);
endlayout;
```

### 添加侧边栏

第 245 页图 10.5 的图表进展顺利，`ENTRYTITLE` 在整个图表上居中。如果它能在网格区域内居中效果会更好。这可以通过移除 `ENTRYTITLE` 块并将其替换为 `SIDEBAR` 块来实现。共有四个侧边栏区域：两个跨列的（一个在顶部，一个在底部），以及两个跨行的（一个在右侧，一个在左侧）。

```
sidebar / align=top;
  entry "Microsoft Stock Performance" / textattrs=GraphLabelText pad=(bottom=5px);
endsidebar;
```

最后，我们需要一种方法来解释第一行的价格代表调整后的收盘价。我们还需要解释第二行的轴缩放是以百万股为单位的。提供这些信息有两种策略可用。

第一种策略是创建一个外部图例。对于这种策略，我们必须在两个绘图语句中定义图例文本，并在底部侧边栏添加 `DISCRETELEGEND` 语句。

```
seriesplot x=Date2004 y=Price2004 /
  lineattrs=GraphData(thickness=2px pattern=solid)
  name="series" legendlabel="Adjusted Close";

needleplot x=Date2004 y=Vol2004 /
  lineattrs=GraphData(thickness=2px pattern=solid)
  name="needle" legendlabel="Millions of Shares";

sidebar / align=bottom;
  discretelegend "series" "needle" / border=off pad=(top=10px);
endsidebar;
```

接下来的图表显示了修改后的效果：

### 微软股票性能

![](img/a9ccb6123dee40d424cb295a3a99c16c_256_0.png)

另一种策略是将信息添加到行中。乍一看，通过扩展轴标签可以很好地做到这一点：

```
rowaxes;
rowaxis / griddisplay=on display=(tickvalues)
```
