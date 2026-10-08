
![](img/0c09161c0be53934e5708cffbdcc441f_218_0.png)

```sas
title "Avg. Number of Electrical Workers";
proc sgplot data=sashelper.workers;
format date year;
yaxis grid;
axis label="Workers (in thousands)";
hline date / response=electric stat=mean
lineattrs=(color=gray thickness=2);
```

# 图 7.6.2: 带标记的折线图

`MARKERS` 选项在沿线的数据点上显示标记。

`MARKERATTR` 选项用于独立于线条属性控制标记的属性。

![](img/0c09161c0be53934e5708cffbdcc441f_218_1.png)

```sas
title "Avg. Number of Electrical Workers";
proc sgplot data=sashelper.workers;
format date year;
yaxis grid;
axis label="Workers (in thousands)";
line date / response=electric stat=mean
lineattrs=(color=gray thickness=2)
markerattrs=(color=gray symbol=circlefilled) markers;
```

Matange, Sanjay and Heath, Dan. Statistical Procedures by Example: Effective Graphs Using SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 如需更多 SAS资源，请访问 `support.sas.com/publishing`。

## 图 7.6.3: 带断点的折线图

默认情况下，折线图连接所有非缺失的响应值。然而，您可能希望通过使用 `BREAK` 选项断开线条来显示缺失值。

在此示例中，1979 年的所有值均为缺失值。线条将从下一个非缺失值开始继续。

```sas
title "Avg. Number of Electrical Workers"
proc sgplot data=sgbook.workers_missing;
format date year;
axis grid;
axis label="Workers (in thousands)"
hline date /response=break stat=mean lineattrs=(thickness=2)
markers markerattrs=(symbol=circlefilled);
```

![](img/0c09161c0be53934e5708cffbdcc441f_219_0.png)

## 图 7.6.4: 带数据标签的折线图

此示例通过使用 `DATABEL` 选项在沿线显示响应值。该选项可以指定一个变量来显示线条响应值以外的信息。

`DATABELATTRS` 可用于覆盖标签的默认文本属性。

```sas
title "Avg. Number of Electrical Workers"
proc sgplot data=sashelp.workers;
format date year;
axis grid;
axis label="Workers (in thousands)"
hline date /response=electric stat=mean lineattrs=(thickness=2)
markers markerattrs=(symbol=circlefilled) databel
datalabelattrs=(weight=bold style=italic);
```

![](img/0c09161c0be53934e5708cffbdcc441f_219_1.png)

9.3

# 图 7.6.5: 带参考线的折线图

通过指定 `REFLINE` 语句可以在折线图上添加参考线。语句的顺序非常重要。

由于 `REFLINE` 语句在 `HLINE` 语句之后指定，因此参考线画在折线图之前。

![](img/0c09161c0be53934e5708cffbdcc441f_220_0.png)

```sas
title="Avg. Number of Electrical Workers"
proc ggplot data=sashelp.workers;
format date year;
xaxis label="Workers (in thousands)"
hline date /response=electric stat=mean lineattrs=(thickness=2)
marker(symbol=circlefilled);
refline 300;
```

# 图 7.6.6: 带置信间的折线图

此示例显示了均值的置信限（CLM）。标准误差和标准差也是可用的。

`ALPHA` 选项用于指定 CLM 计算的置信度。默认值为 0.05。

![](img/0c09161c0be53934e5708cffbdcc441f_220_1.png)

```sas
title="Avg. Number of Electrical Workers"
proc ggplot data=sashelp.workers noautolegend;
format date year;
xaxis label="Workers (in thousands)" grid;
hline date / response=electric stat=mean limitstat=clm
lineattrs=(thickness=2);
run;
```

Matange, Sanjay and Heath, Dan. Statistical Procedures by Example: Effective Graphs Using SAS®. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA. 保留权利。如需更多 SAS资源，请访问 `support.sas.com/publishing`。

# 图 7.6.7: 带上限的折线图

可以使用 `LIMITS` 选项控制显示哪一侧的限。此示例使用 `STDERR` 统计值显示两个标准误差，而不是一个。

![](img/0c09161c0be53934e5708cffbdcc441f_221_0.png)

# 图 7.6.8: 带响应排序的折线图

```sas
proc sgplot data=sashelp.workers noautolegend;
format date year;
axis label="Workers (in thousands)" grid;
hline date /response=electric stat=mean limits=upper
limitstat=stderr lineattrs=(thickness=2);
```

使用 `CATEGORYORDER` 选项根据响应值的升序对您的类别进行排序。在此示例中，销量最高的产品排在顶部。

![](img/0c09161c0be53934e5708cffbdcc441f_221_1.png)

“1993年产品销售”:

```sas
proc sgplot data=sashelp.sales (where=(year=1993))
yaxis grid;
hline date /response=actual categoryorder=desc
markerattrs=(symbol=circlefilled);
run;
```

# 图 7.6.9: 分组折线图

`GROUP` 选项用于指定额外的分类级别。图线和标记会自动为每个组值分配唯一属性。可以使用 `attribute map` 或 `ODS style` 修改这些属性。

![](img/0c09161c0be53934e5708cffbdcc441f_222_0.png)

```sas
title "Avg. Number of Electrical Workers";
proc sgplot data=sashelp.workers_group;
format date year;
label label_name="Type of Work";
axis label="workers";
hline date / response=col group=name;
run;
```

# 图 7.6.10: 带标签的折线

此分组示例使用 `CURVELABEL` 选项为线条标记标签。当折线图没有分组变量时，可以通过指定 `CURVELABEL="string"` 来指定曲线标签。曲线标签可以放置在数据区域内部或线条图的开始或结束。

![](img/0c09161c0be53934e5708cffbdcc441f_222_1.png)

```sas
title "Avg. Number of Electrical Workers";
proc sgplot data=sashelp.workers_group;
format date year;
axis label="workers";
hline date / response=col stat=mean
group=name curvelabel;
run;
```

# 图 7.6.11: 叠加折线图

此示例通过为每个变量叠加一个折线图来绘制两个响应变量。每个语句都有自己的一组视觉属性，并可以分配给不同的轴。此外，可以使用 `LEGENDLABEL` 选项更改每个图的图例标签。

![](img/0c09161c0be53934e5708cffbdcc441f_223_0.png)

```sas
title "Avg. Number of Electrical Workers"
proc sgplot data=sashelp.workers;
format date year;
axis label="Workers (in thousands)"
line date / response=electric stat=mean markerattrs=(color=black symbol=circle) lineattrs=(thickness=2);
line date / response=masonry stat=mean markerattrs=(color=gray symbol=square) lineattrs=(pattern=solid thickness=2);
```

# 图 7.6.12: 带离散偏移的叠加折线图

通常，叠加线条的响应值绘制在类别轴沿刻度位置，这可能会重叠。要将值移离刻度，请使用 `DISCRETEOFFSET` 选项。负值低至 -0.5 个点。正值高至 0.5 单位。

![](img/0c09161c0be53934e5708cffbdcc441f_223_1.png)

```sas
title "Avg. Number of Electrical Workers"
proc sgplot data=sashelp.workers;
format date year;
axis label="Workers (in thousands)" offset=0.05 offsetmax=0.05;
line date / response=electric stat=mean markers discreteoffset=-0.1 markerattrs=(color=black symbol=circle) lineattrs=(thickness=2);
line date / response=masonry stat=mean markers discreteoffset=0.1 markerattrs=(color=gray symbol=circle) lineattrs=(pattern=);
```

点图显示按类别对响应的汇总情况或类别的频率计数。语法为：

```sas
dot column / options;
```

默认情况下，数据按每个唯一类别值进行汇总；然而，可以使用用户定义的格式创建汇总类别范围。为结果类别绘制一个标记。如果指定了分组，则为每个组值绘制一个标记，要么叠加在刻度值上，要么偏移刻度值产生簇效果（参见 `GROUPDISPLAY` 选项）。

![](img/0c09161c0be53934e5708cffbdcc441f_224_0.png)

## 图 7.7.1：基础点图

点点图（Dot plots）是比较大量类别值非常有效的图表。

此示例展示了使用平均值（MEAN）统计量的基础点图。使用 `axis LABEL` 选项可以覆盖数据集中的列标签。

![](img/0c09161c0be53934e5708cffbdcc441f_225_0.png)

```sas
title "Avg. Number of Electrical Workers";proc sgplot data=sashelp.workers;
format date year;
axis label="workers (in thousands)"
dot date / response=electric stat=mean;
run;
```

## 图 7.7.2：带有标记属性的点图

`MARKERATTRS` 选项用于控制图中标记的属性。

在此示例中，修改了标记的形状和标记的大小。

![](img/0c09161c0be53934e5708cffbdcc441f_225_1.png)

```sas
title "Avg. Number of Electrical Workers";proc sgplot data=sashelp.workers;
format date year;
axis label="workers (in thousands)"
dot date / response=electric stat=mean
markerattrs=(symbol=diamondfilled size=11px);
run;
```

## 图 7.7.3：带有数据标签的点图

此示例通过 `DATALABEL` 选项显示点图的响应值。该选项可以指定变量来显示绘图响应值以外的信息。

`DATALABELATTRs` 可覆盖标签的默认文本属性。

![](img/0c09161c0be53934e5708cffbdcc441f_226_0.png)

```sas
title "Avg. Number of Electrical Workers";proc sgplot data=esgbook.workers_missing;
format date year;
axis label="Workers (in thousands)";
date / response=electric stat=mean
datalabelattrs=(weight=style=italic);
run;
```

![](img/0c09161c0be53934e5708cffbdcc441f_226_1.png)

## 图 7.7.4：带有参考线的点图

通过指定 `REFLINE` 语句可以在点图中添加参考线。

语句的顺序非常重要。如果 `REFLINE` 语句在 `DOT` 语句之前指定，则线将绘制在点图之后。在 `DOT` 语句之后指定的 `REFLINE` 语句绘制在点图之前。

![](img/0c09161c0be53934e5708cffbdcc441f_226_2.png)

```sas
title "Avg. Number of Electrical Workers";
proc sgplot data=sashelp.workers;
format date year;
axis label="Workers (in thousands)";
date / response=electric stat=mean;
refline 300 / axis=X;
run;
```

Matange, Sanjay and Heath, Dan. Statistical Procedures by Example: Effective Graphs Using SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 如需更多 SAS 资源，请访问 `support.sas.com/publishing`。

## 图 7.7.5：带有置信限的点图

此示例展示了一个显示均值置信限（CLM）的点图。标准误差和标准差统计量也可用。

可以使用 `ALPHA` 选项来指定 CLM 计算的置信度。默认值为 0.05。

![](img/0c09161c0be53934e5708cffbdcc441f_227_0.png)

```sas
/* Avg. Number of Electrical Workers*
proc sgplot data=help.workers noautolegend;
format date year;
xaxis label="Workers (in thousands)" grid;
dot date / response=electric stat=mean limitstat=clm;
run;
```

## 图 7.7.6：带有上限的点图

你可以使用 `LIMITS` 选项来控制显示限制的哪侧。

此示例使用 `STDERR` 统计量配合 `NUMSTD` 乘数显示两个标准误差而不是一个。

![](img/0c09161c0be53934e5708cffbdcc441f_227_1.png)

```sas
```
