
# 第 17 章 • 向图表添加内嵌

```
/* 计算 BARCHART 数据和内图信息 */
proc summary data=sashelp.cars
  where ("Sedan" "Truck" "SUV")
  class cylinders (4 8)
  types cylinders*origin cylinders*type;
  var mpg_city;
  output out=mileage(drop=freq) mean=nobs inherit;
  types cylinders*origin*type;
```

`SUMMARY` 过程计算 `TYPES` 语句列出的每个分类交互的观测值数量和平均 MPG。`cylinders*origin` 是单元汇总的交叉项，而 `cylinders*origin*type` 是每个单元柱状图的交叉项。`COMPLETE` 在分类交互频率为零时创建汇总观测值。此外，该代码在数据中创建了子集，以限制每个柱状图的柱的数量并减少分类面板中的单元格数量。有三个产地（亚洲、欧洲和美国）和三个气缸数。为了让内图显示准确的数据，必须确保数据中的观测顺序与 `CLASS` 语句的顺序对应。在填充面板单元格之前，`cylinders` 的值必须在 `SUMMARY` 过程的 `CLASS` 语句中指定，以便确定计算的顺序。

以下列表显示了观测值的顺序。

### 输出 17.1 数据集的部分列表

| Obs | Cylinders | Origin | Type | _TYPE_ | Mean | Nobs |
|---|---|---|---|---|---|---|
| 1 | 4 | 亚洲 | | 6 | 25.842 | 57 |
| 2 | 4 | 欧洲 | | 6 | 23.444 | 18 |
| 3 | 4 | 美国 | | 6 | 24.000 | 34 |
| 4 | 6 | 亚洲 | | 6 | 18.300 | 60 |
| 5 | 6 | 欧洲 | | 6 | 17.612 | 18 |
| 6 | 6 | 美国 | | 6 | 18.475 | 61 |
| 7 | 8 | 亚洲 | | 6 | 15.200 | 10 |
| 8 | 8 | 欧洲 | | 6 | 16.167 | 24 |
| 9 | 8 | 美国 | | 6 | 15.154 | 35 |
| 10 | 4 | 亚洲 | SUV | 7 | 21.400 | 5 |
| 11 | 4 | 亚洲 | 轿车 | 7 | 26.512 | 49 |
| 12 | 4 | 亚洲 | 卡车 | 7 | 22.333 | 3 |

注意，前九个观测值（`_TYPE_` 等 6）是单元汇总。剩余的 27 个观测值（`_TYPE_` 等 7）用于每个单元柱状图。为了给内图分离列，您需要将 `_TYPE_=6` 的观测值存储在新列中。为了实现这一点，必须先将数据提取到名为 `Overall` 的单独数据并重命名列。必须重命名列以防止与 `Mileage` 数据合并时覆盖任何值。以下是将信息写入 `Overall` 数据集的 DATA 步：

```
/* 提取信息，重命名列，将其写入 OVERALL 数据集 */
data mileage (drop=_type_)
overall(rename(origin=cellOrigin cylinders=cellCyl mean=cellMean
nobs=cellNobs));
set mileage; by _type_;
if _type_ = 6 then output output
else output mileage;
run;
```

最后，您必须使用一对一合并（不使用 `BY` 语句）将 `Mileage` 和 `Overall` 数据集合并到 `Summary` 数据中。

```
/* 合并 MILEAGE 和 OVERALL 并写入 SUMMARY */
data summary;
 merge mileage overall;
label Mean="MPG (City)" CellNOBS="Nobs" CellMean="Mean"
 format mean cellMean 4.1;
run;
```

以下列表显示了合并数据的样本。

### 输出 17.2 Summary 数据集的部分列表

| Obs | Cylinders | Origin | Type | Mean | Nobs | Cyl | Origin | Mean | Nobs |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 4 | 亚洲 | SUV | 21.4 | 5 | 4 | 亚洲 | 25.8 | 57 |
| 2 | 4 | 亚洲 | 轿车 | 26.5 | 4 | 4 | 欧洲 | 23.4 | 18 |
| 3 | 4 | 亚洲 | 卡车 | 22.3 | 3 | 4 | 美国 | 24.0 | 34 |
| 4 | 4 | 欧洲 | SUV | - | - | 0 | 亚洲 | 18.0 | 60 |
| 5 | 4 | 欧洲 | 轿车 | 23.4 | 18 | 6 | 欧洲 | 18.8 | 34 |
| 6 | 4 | 欧洲 | 卡车 | - | 0 | 6 | 美国 | 18.5 | 61 |
| 7 | 4 | 美国 | SUV | 20.5 | 2 | 8 | 亚洲 | 15.2 | 10 |
| 8 | 4 | 美国 | 轿车 | 24.7 | 29 | 8 | 欧洲 | 16.2 | 24 |
| 9 | 4 | 美国 | 轿车 | 26.0 | 3 | 8 | 美国 | 15.5 | 35 |
| 10 | 6 | 亚洲 | SUV | 17.2 | 15 | - | - | - | - |
| 11 | 6 | 亚洲 | 轿车 | 19.0 | 41 | - | - | - | - |
| 12 | 6 | 亚洲 | 卡车 | 15.5 | 4 | - | - | - | - |

```
linearopts=(tickvaluepriority=true
tickvaluesequence=(start=5 end=30 increment=5))
gridplay=on offsetmin=0 offsetmax=.1);
layout prototype=;
barchart category=type response=mean / orient=horizontal
width=.5 barlabel=true;
endlayout;
endlayout;
endgraph;
run;
```

```
ods html style=statistical;
proc sgrender data=summary template=panel;
run;
```

输出结果在第 376 页的图 17.2 中。

## 创建轴对齐的内嵌

有时，你希望内嵌能够提供关于沿轴数值的信息。这些信息与轴上的值对齐。你可以使用块状图（block plot）或表格来显示与轴值对齐的信息。

## 使用块状图创建轴对齐的内嵌

本节提供了如何使用 `BLOCKPLOT` 语句创建轴对齐内嵌的示例。有关 `BLOCKPLOT` 语句的信息，请参阅《SAS Graph Template Language: Reference》中的“BLOCKPLOT Statement”。在以下示例中，“events”已随时间定义，图表顶部的内嵌信息提供了关于这些事件的信息。该示例使用了 `BLOCKPLOT` 语句，它会创建一个或多个包含文本值的矩形块的条带。每个块的宽度对应 X 轴上指定的数值间隔。

这里是该示例的输出。

**图 17.3** 使用块状图创建的轴对齐内嵌

![](img/a9ccb6123dee40d424cb295a3a99c16c_390_0.png)

此示例的输入数据必须同时包含序列图和块状图的数据。构建相应数据最简单的方法是将微软发布数据和微软股票数据进行匹配合并（match-merge）。第一步是创建数据集 `Msevents`，它包含微软的发布日期。下一步是对微软股票数据进行排序，将其与 `Msevents` 进行匹配合并，并将其写入数据集 `Events` 中。

**示例代码 17.1** 生成 Events 数据集的 SAS 代码

```
/* 创建发布日期集合。 */
data Msevents;
    input date9. Release $;
datalines;
09dec1987 2.0
22may1989 3.0
01aug1993 NT 3.1
24aug1995 95
25jun1998 98
17feb2000 2000
25oct2001 XP
;
run;

/* 按日期对微软股票数据排序。 */
proc sort data=sashelp.stocks(keep=date stock adj)
out=MSstock;
where stocks="Microsoft"
    by date;
run;

/* 合并发布数据和股票数据。 */
data events;
merge MSstock Msevents;
by date;
run;
```

### 输出 17.3 Events 数据集的部分列表

| Obs | Stock | Date | Close | Release |
|---|---|---|---|---|
| 15 | Microsoft | 01OCT87 | $0.30 | |
| 16 | Microsoft | 02NOV87 | $0.27 | |
| 17 | Microsoft | 01DEC87 | $0.33 | |
| 18 | | 03DEC87 | | 2.0 |
| 19 | Microsoft | 04JAN88 | $0.34 | |
| 20 | Microsoft | 01FEB88 | $0.36 | |
| 21 | Microsoft | 01MAR88 | $0.34 | |
| 22 | Microsoft | 04APR88 | $0.33 | |
| 23 | Microsoft | 02MAY88 | $0.35 | |
| 24 | Microsoft | 01JUN88 | $0.40 | |

如 Events 数据集的部分列表所示，第一次发布发生在观测值 18 中。在发布日期的观测值中，Stock 值是缺失的。在微软股票的观测值中，Release 列是缺失的。以下是定义此示例模板并渲染图表的代码。

```
/* 创建图表模板。 */
proc template;
define graph blockplot;
begin;
  entitle "Microsoft Share Prices";
  entitle "Significant OS Releases";
  layout overlay / yaxis=(offset=0.05);
  blockplot x=date block=release /
  display=(outline)
  valuealignment=top valuealign=left
  labelposition=top
  extendblockmissing=true
  valueattrs=GraphDataText(weight=bold
  color=GraphData2:contrastcolor);
  labelattrs=GraphValueText(weight=bold
  color=GraphData2:contrastcolor);
  outlineattrs=(color=GraphLines:color);
  seriesplot x=date y=adjclose / lineattrs=GraphData;
end;
end;
run;
```

```
/* 渲染图表。 */
proc sgrender data=events template=blockplot;
format date year4;
run;
```

在模板中，块状图与序列图叠加以创建一个轴对齐的内嵌。为 Y 轴指定了 `OFFSET` 选项以为块值留出空间。`BLOCKPLOT` 语句需要两个输入列：一个用于 X 参数，另一个用于 BLOCK 参数。`EXTENMISSING=TRUE` 选项允许块跨越 Release 列的缺失值进行扩展。`BLOCK` 列控制每个块的边界和显示的文本。在这种情况下，每当 Release 列出现一个新的非空值时，就会开始一个新块。块点之间 X 值的范围决定了每个块的宽度。

`BLOCKPLOT` 语句指定了许多选项来控制块和文本的内容、位置和外观。`DISPLAY=<OUTLINE><VALUES>` 指定要显示的特征。`EXTENMISSING=TRUE` 指定当在 Block 列中遇到缺失值时，块是延续上一个非空值还是启动一个新块。`VALUEALIGN=TOP | CENTER | BOTTOM` 指定文本在块内的垂直位置。`VALUEALIGN=LEFT | RIGHT | TOP` 指定文本在块内的水平位置。`LABELPOSITION=LEFT | RIGHT | BOTTOM` 指定适用于块的块标签位置。`VALUEATTRS=style-element` 指定值的字体属性。`LABELATTRS=style-element` 指定块标签的字体属性。
