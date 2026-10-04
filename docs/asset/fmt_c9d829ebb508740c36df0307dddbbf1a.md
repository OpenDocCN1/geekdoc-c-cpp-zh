
欲了解更多信息，请参阅第 157 页第 7 章“在图中添加和更改文本”。

对于柱状、曲线和数据标签，许多图表支持某些选项，允许将长标签分成多行以避免碰撞。下表列出了这些选项。

| 选项 | 说明 |
| --- | --- |
| `BARLABELFITPOLICY=AUTO | NONE` | 指定垂直柱状图中避免标签碰撞的策略。当设置为 `AUTO` 时，发生碰撞时标签将旋转。 |
| `DATALABELSPLIT=TRUE | FALSE` | 指定在必要时是否将数据标签分成多行，以使标签适应在可用空间内。 |
| `DATALABELSPLITCHAR="character-list"` | 指定一个或多个可用于拆分数据标签的字符。 |
| `DATALABELSPLITCHDROP=TRUE | FALSE` | 指定在发生拆分的拆分字符是否从显示的数据标签中移除。 |

## 许多图表语句支持的功能 41

| 选项 | 说明 |
| --- | --- |
| `DATALABELSPLITJUSTIFY="justification"` | 指定拆分后的数据标签每行的对齐方式。 |
| `CURVELABELSPLIT=TRUE | FALSE` | 指定在必要时是否将曲线标签分成多行，以使标签适应在可用空间内。 |
| `CURVELABELSPLITCHAR="character-list"` | 指定一个或多个可用于拆分曲线标签的字符。 |
| `CURVELABELSPLITCHDROP=TRUE | FALSE` | 指定在发生拆分的拆分符是否从显示的标签中移除。 |
| `CURVELABELSPLITJUSTIFY="justification"` | 指定拆分后的曲线标签每行的对齐方式。 |
| `VALUEFITPOLICY="fit-policy"` | 指定如何调整块状图的文本值以适应包含它的块。 |
| `VALUESPLITCHAR="character-list"` | 指定在块状图中使用值拆分时，指定一个或多个可用于拆分块标签的字符。 |
| `VALUESPLITDROP=TRUE | FALSE` | 指定在块状图中使用值拆分时，在发生拆分的拆分符是否从显示的块标签中移除。 |

对于轴，提供了某些选项允许您将长标签分成多行以避免截断。下表列出了这些选项。

| 选项 | 说明 |
| --- | --- |
| `LABELFITPOLICY=AUTO | SPLIT | SPLITWAYS` | 指定轴标签的拟合方式。如果原始标签太长，`AUTO` 指定使用较短标签（指定的），而 `SPLIT` 指定根据需要将原始标签分成多行以适应可用空间。`SPLITWAYS` 指定无论可用空间如何，原始标签始终被分成多行。 |
| `LABELSPLITCHAR="character-list"` | 当使用 `SPLIT` 或 `SPLITWAYS` 策略时，指定一个或多个可用于拆分轴标签的字符。 |
| `LABELSPLITCHDROP=TRUE | FALSE` | 当使用 `SPLIT` 或 `SPLITWAYS` 拟合策略时，指定发生拆分的拆分字符是否从显示的轴标签中移除。 |
| `LABELSPLITJUSTIFY="justification"` | 指定在使用上述策略时，拆分后的轴标签每行的对齐方式。 |

## 分组

许多图表支持 `GROUP=` 选项，为每个不同的数据值显示不同的标记、线条或区域。您可以使用 `INDEX=` 选项更改分组的外观。还可以使用 `GROUPDISPLAY=` 选项更改分组的方式。

| 选项 | 说明 |
| --- | --- |
| `GROUP=column` | 指定分组列，始终视为离散值。示例请参阅第 30 页的“图例语句”。 |
| `INDEX=positive-integer-column` | 指定将整数列关联到预定义的图形元素 `GraphData1`、`GraphData2`... |
| `GROUPDISPLAY=STACK | CLUSTER | OVERLAY` | 指定每个类别的分组显示为柱状簇还是堆叠柱状，或者对于其他图类型显示为标记簇或标记叠加 |

欲了解有关分组的更多信息，请参阅第 111 页第 6 章“图形外观：原则”。

## 轴分配

所有二维图都有四个潜在的轴：`X`、`X2`、`Y` 和 `Y2`。您可以选择图表使用的轴。轴选项通常在包含图表的 `LAYOUT` 语句中指定。

| 选项 | 说明 |
| --- | --- |
| `XAXIS=X | X2` | 指定 `X` 列显示在 `X` 还是 `X2` 轴上。 |
| `YAXIS=Y | Y2` | 指定 `Y` 列显示在 `Y` 还是 `Y2` 轴上。 |

欲更多信息，请参阅第 63 页第 5 章“叠加中的轴”。

## 数据提示

数据提示（工具提示）是当您的指针悬停在图形组件（如线条、标记或填充区域）上时在 HTML 页面显示的气泡。要获得默认数据提示，只需指定 `ODS GRAPHICS / IMAGEMAP` 以及相应的 ODS 目标。您可以自定义数据提示信息。

| 选项 | 说明 |
| --- | --- |
| `ROLENAME=(role=column ...)` | 创建额外的角色以自定义数据提示。 |
| `TIP=(role-names)` | 指定哪些图表角色用于数据提示。 |
| `TIPFORMAT=(role=format ...)` | 指定应用于图表角色的数据的格式。 |
| `TIPLABEL=(role="string")` | 指定应用于图表角色的列的标签。 |

欲了解更多信息和示例，请参阅第 467 页的“控制数据提示”。

## LAYOUT OVERLAY 语句

`LAYOUT OVERLAY` 语句通过叠加布局块中包含的语句的结果，构建一个 2D 单单元图。它是 GTL 中几种可能的布局容器之一。其他容器提供了其他布局类型的详细信息。建议先学习这种布局类型，因为大多数其他布局容器都会将其功能集与 `OVERLAY` 布局进行对比。

任何模板的最外层布局块定义了图形区域的内容，如下图所示：

![](img/a9ccb6123dee40d424cb295a3a99c16c_55_0.png)

下一图中的图形是由一个开启了边框的 `OVERLAY` 布局定义的。该布局包含单个散图。布局容器的边界由浅灰色边框显示。边框内的所有内容都由布局管理。

| 标题一 | |
| 标题二 | |
| --- | --- |
| 权重 140 | |
| 120 | |
| 80 | |
| 60 | |
| 50 55 60 65 70 高度 | |
| 脚注一 | |
| 脚注二 | |

`OVERLAY` 容器控件可以包含布局块中：

- 哪些语句（绘图、图例、文本）
- 哪些语句可以在轴边界的绘图区域内组合
- 各种轴特征
- 使用哪些轴（共有四个可用轴：`X` 和 `Y`，以及 `X2` 和 `Y2`）
- 使用哪些轴类型（轴类型为 `LINEAR`、`DISCRETE`、`LOG` 和 `TIME`）
- 轴标签、轴数据范围、刻度和刻度值
- 其他轴特征（如偏移量）
- 边框、内边距和背景属性
- 所有包含的绘图、文本、图例和嵌套布局的定位和对齐
- 生成绘图的默认外观（`CYCLEATTRS=` 选项）
- 绘图墙矩形区域的比例（`ASPECTRATIO=` 选项）

布局容器还会查询包含的语句，以查找可能会更改组合图形默认内部规则的图形。

## Overlay 组合

在熟悉 GTL 提供的绘图语句后，你会将它们视为基本组件，可以通过许多方式堆叠以形成更复杂的图形。例如，GTL 中没有“BARLINE”语句。你通过在 `BARCHART` 或 `BARCHARTPARM` 上使用 `SERIESPLOT` 来设计这类图形。

```
proc template;
  define statgraph barline;
  begingraph;
    entrytitle "Overlay OF REFERENCELINE, BARCHARTPARM and SERIESPLOT";
    layout overlay;
      referenceline y=25000000 / curvelabel="Target";
      barchartparm category=year response=retail / dataskin=matte
        fillattrs=(transparency=0.5)
        fillpatterns=(pattern=R1 color=light-gray);
      seriesplot x=year y=profit / name="series";
      discretelegend "series";
    endlayout;
  endgraph;
end;
run;
```

```
* 计算每个产品线的总和;
proc summary data=sashelp.orsales nway;
  class year;
  var total_retail_price profit;
  output out=orsales sum=Retail Profit;
run;
```

```
* 关闭 ODS HTML 目标;
ods html close;
```

```
* 打开 LISTING 目标并指定 JOURNAL3 样式;
ods listing style=journal3;
```

```
* 生成图形;
proc sgrender data=orsales template=barline;
  format retail profit com2.;
run;
```

```
* 关闭 ODS LISTING 并打开 ODS HTML;
ods listing close;
ods html;
```

## 48 第 4 章 • 使用简单的单单元布局

输出反映了请求的堆叠顺序。

![](img/a9ccb6123dee40d424cb295a3a99c16c_57_0.png)

**图形方向。** 在创建柱状图时，有时希望将图形从垂直旋转为水平。GTL 没有为垂直和水平图提供单独的语句——每个都被视为相同类型但方向不同。要创建水平版本的折线图，你需要在 `BARCHARTPARM` 语句中指定 `ORIENT=HORIZONTAL`：

```
proc template;
  define statgraph sgbar2;
  begingraph;
    entrytitle "Overlay of REFERENCELINE, BARCHARTPARM and SERIESPLOT";
    layout overlay / yaxisopts=(reverse=true);
      referenceline x=250000 / label="Target";
      barchartparm category=year response=retail / orient=horizontal
        fillattrs=(pattern=R1 color=light-gray);
      seriesplot x=profit y=year / name="series"
        legendlabel="Profit in USD";
      discretelegend "series";
    endlayout;
  endgraph;
end;
run;
```

```
/* 计算每个产品线的总和 */
proc summary data=sashelp.orsales nway;
  class year;
  var total_retail_price profit;
  output out=orsales sum=Retail;
run;
```

```
/* 关闭 ODS HTML */
ods html close;
```

```
/* 打开 LISTING 目标并指定 JOURNAL3 样式 */
ods listing style=journal3;

/* 生成图形 */
proc sgrender data=orsales template=barline;
  format retail profit com2.;
run;
```

```
/* 关闭 ODS LISTING 并打开 ODS HTML */
ods listing;
ods html;
```

在这里，`Y` 轴变成了（`DISCRETE`）轴，`X` 轴用于响应值。`REFERENCELINE` 和 `SERIESPLOT` 都通过更改映射到 `X` 轴和 `Y` 轴的变量反映了这一点。`BARCHARTPARM` 的变量映射保持不变，但我们添加 `ORIENT=HORIZONTAL` 来交换轴映射。数据集和布局保持不变。

## REFERENCELINE、BARCHARTPARM 和 SERIESPLOT 的叠加

![](img/a9ccb6123dee40d424cb295a3a99c16c_58_0.png)

相同的策略用于创建水平箱图或直方图。如果你想反转 `Y` 轴的排序，可以在轴选项中添加 `REVERSE=TRUE`：

```
layout overlay / yaxisopts=(reverse=true);
```

**多个轴。** 有时你有不同比例的等效数据（货币、测量值），或要在独立轴上显示的可比较数据。`OVERLAY` 布局支持多四个独立轴，其中 `Y2` 轴位于 `Y` 轴的右侧，`X2` 轴位于 `X` 轴的上方。

以下是生成此类图形的完整程序。我们希望在显示摄氏度的 `Y` 轴独立的 `Y2` 轴上显示华氏温度。对于这个特定的示例，没有输入两个温度变量，因为可以使用 `EVAL` 函数在模板上下文中计算新列数据。

## NEEDLEPLOT 和 SCATTERPLOT 的叠加 SCATTERPLOT 使用 Y2 轴

![](img/a9ccb6123dee40d424cb295a3a99c16c_59_0.png)

此时，关于模板代码最重要的概念是独立轴是通过映射数据到它们来创建的。注意 `SCATTERPLOT` 语句使用了 `YAXIS=Y2` 选项。这导致 `Y2` 使用代表华氏度的变量进行显示和缩放。重要的是叠加中的多个图形共享同一个轴（例如 `X` 轴）。因此，控制轴属性的选项不在绘图语句中，而是在 `LAYOUT` 语句中。包含大多数 `Y` 和 `Y2` 轴选项是为了强制两个不同的轴刻度准确对比。许多其他问题在第 63 页的第 5 章“OVERLAY 中的轴”中进行了详细讨论。

```
data temp;
  input City $1-11 Celsius;
  datalines;
New York 11
Sydney 12
Mexico City 18
Paris 8
Tokyo 6;
run;
```

```
proc template;
  define statgraph Yaxis;
  begingraph;
    entrytitle "Overlay of NEEDLEPLOT and SCATTERPLOT";
    entrytitle "SCATTERPLOT uses Y2 axis";
    layout overlay /
      yaxisopts=(display=(tickvalues))
      y2axisopts=(griddisplay=on offset=0
        linearopts=(viewmin=0 viewmax=20
          thresholdmin=0 thresholdmax=0))
      yaxisopts=(label="Fahrenheit" offset=0
        linearopts=(viewmin=32 viewmax=68
          thresholdmin=0 thresholdmax=0));
      needleplot x=City y=Celsius;
      scatterplot x=City y=32+(9*Celsius/5) / yaxis=y2
        markerattrs=(symbol=circlefilled);
    endlayout;
  endgraph;
end;
run;
proc sgrender data=temp template=y2axis;
run;
```

通常，输入数据的组织会影响你在 `OVERLAY` 布局中选择绘图语句。在第 21 页的第 3 章“基本语句和选项概述”中，你会根据拟合图输入数据的性质选择不同的绘图语句。

## 回归拟合图

![](img/a9ccb6123dee40d424cb295a3a99c16c_60_0.png)

**计算参数化图形。** 如果数据具有身高和重量的原始数值列，创建拟合线和置信带简单的方法是使用 `REGRESSIONPLOT`、`LOESSPLOT` 或 `PBSPLINEPLOT` 语句以及 `MODELBAND` 语句。

```
layout overlay;
  modelband "mycm";
  scatterplot x=height y=weight / primary=true;
  regressionplot x=height y=weight / alpha=.01 clm="mycm";
endlayout;
```

如果你通过分析过程计算拟合线和带的点，你会选择 `SERIESPLOT` 和 `BANDPLOT` 来绘制图形。当期望的拟合线无法通过 `REGRESSIONPLOT`、`LOESSPLOT` 或 `PBSPLINEPLOT` 语句选项计算时，需要这种技术。

```
layout overlay;
  bandplot x=height upper=uclm lower=lclm / fillattrs=GraphConfidence;
  scatterplot x=height y=weight / primary=true;
  seriesplot x=height y=p / lineattrs=GraphFit;
endlayout;
```

此外，注意使用了额外的选项来设置拟合线和带的外观，使其与 `REGRESSIONPLOT` 和 `MODELBAND` 的细节匹配。

**分组数据。** 另一种常见的做法是叠加系列线条以进行比较。如果你的数据除 `X` 和 `Y` 变量外还包含分类变量，你可以使用带有 `GROUP=` 选项的 `SERIESPLOT` 语句：

```
proc template;
  define statgraph seriesgroup;
  begingraph;
    entrytitle="Overlay of SERIESPLOTS with GROUP=";
    layout overlay;
      seriesplot x=date y=close / group=stock name="s";
      discretelegend "s";
    endlayout;
  endgraph;
end;
run;
```
