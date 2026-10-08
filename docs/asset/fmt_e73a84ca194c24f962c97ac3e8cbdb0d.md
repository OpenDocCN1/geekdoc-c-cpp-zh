
```
title 'City and Highway by Country';
proc sgplot data=sashelp.cars;
where type='Sedan' or type='Sports';
vbar origin / response=mpg_city discreteoffset=-0.2 barwidth=0.4;
vbar origin / response=mpg_high discreteoffset=0.2 barwidth=0.4;
axis (nolabel);
run;
```

## 图 3.2.26: 带有图案的柱状图

此图显示了按产地类型作为分组变量的里程垂直柱状图。分组值默认堆叠。

此图使用了 `Journal2` 样式。柱体没有填充颜色，只有填充图案。

```
ods listing style=journal2;
title "MPG by Country and Type";
proc sgplot data=sashelp.cars;
where type='Sedan' or type='Sports';
vbar origin / group=type;
axis (nolabel);
run;
```

### 图 3.2.27：带有皮肤效果的分组柱状图

此图使用 `GROUP=type` 的垂直柱状图显示里程数。`GROUPDISPLAY=cluster` 用于显示每组相邻的条形。

此图使用了 `DATASKIN=Sheen`。

![](img/0c09161c0be53934e5708cffbdcc441f_63_0.png)

```sas
title 'City and Highway Mileage by Country';
proc sgplot data=sashelp.cars;
where type='Sedan' or type='Sports';
vbar origin / response=mpg_city stat=mean group=type
groupdisisplay=cluster dataskin=sheen transparency=0;
axis display=(nolabel);
run;
```

### 图 3.2.28：带有图案、填充颜色和皮肤效果的多柱状图

此图通过带有填充图案、填充颜色和皮肤效果的相邻条形来显示城市和高速公路数。

Journal 样式使用了颜色深浅和填充图案。`DISCRETEOFFSET` 和 `BARWIDTH` 用于将两个响应并排定位。

![](img/0c09161c0be53934e5708cffbdcc441f_63_1.png)

```sas
ods listing=journal;
title 'City and Highway Mileage by Country';
proc sgplot data=sashelp.cars;
where type='Sedan' or type='Sports';
vbar origin / response=mpg_city stat=mean barwidth=0.4
dataskin=pressed discreteoffset=-0.22;
vbar origin / response=mpg_highway stat=mean barwidth=0.4
dataskin=pressed discreteoffset+=0.22;
axis display=(nolabel);
axis label1='mileage';
run;
```

### 图 3.2.29：水平柱状图

这是一个按汽车类型分类里程数的基础水平柱状图，带有数据标签。

水平柱状图更适用于条形较多且刻度值较长的情况。

隐藏了 x 轴和 y 轴标签，因为是冗余的。

![](img/0c09161c0be53934e5708cffbdcc441f_64_0.png)

```sas
title 'Mileage by Type';
proc sgplot data=sashelp.cars;
mpg_city 5.1;
hbar type / response=mpg_city stat=mean databel;
axis grid=(nodelabel)
yaxis display=(nodelabel)
run;
```

### 图 3.2.30：带有限制的水平条形

这是一个使用 `STAT` 和 `LIMIT` 选项显示汽车类型的基础水平柱状图，带有限制条形。

通过 `DISPLAY` 选项禁用了 y 轴标签。

![](img/0c09161c0be53934e5708cffbdcc441f_64_1.png)

```sas
title 'Mileage by Type';
proc sgplot data=sashelp.cars;
hbar type / response=mpg_city stat=mean limits=both;
axis grid=(nodelabel)
yaxis display=(nodelabel)
run;
```

Matange, Sanjay and Heath, Dan. Statistical Procedures by Example: Effective Graphs Using SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

### 图 3.2.31：高低点图 (HighLow Plot)

股票图

这是一个按日期生成的传统股票图，使用带有 `OPEN` 和 `CLOSE` 选项的高Low 图显示最高价、最低价、开盘价和收盘价。

![](img/0c09161c0be53934e5708cffbdcc441f_65_0.png)

HighLow 图的默认 `TYPE` 为 'Line'。

### 图 3.2.32：高低点图 (HighLow Plot)

药物图

这是一个显示临床试验中使用药物时间的图表。绘制了每种药物的持续时间。

![](img/0c09161c0be53934e5708cffbdcc441f_65_1.png)

在此示例中，HighLow 图的 `TYPE` 设置为 'Bar'。`HIGHCAP` 和 `LOWCAP` 选项设置为 'cap' 数据以显示条形末端。

```sas
title 'Stock Plot';
proc sgplot data=sashelp.stocks;
where type='IBW' and date='01Jan2004'd;
highlow x=date high=high low / open=open close=close
lineattr(display=(noabel));
yaxis grid display=(noabel);
yaxis grid display=(noabel);
run;
```

```sas
title 'Medications Plot';
proc sgplot data=sashelp.highlow autolegend;
highlow y=drug low=high / group=drug
lineattr(pattern=solid) highcap=cap lowcap=cap
transparency=0.2 type=bar barwidth=0.4;
yaxis display=(noabel) grid;
yaxis display=(noabel) min=0 max=100 grid;
run;
```

### 图 3.2.33：气泡图 (Bubble Plot)

这是一个分组气泡图，通过大小显示响应。使用参考线来划分象限。

最大和最小响应值被映射到最大和最小气泡半径。

![](img/0c09161c0be53934e5708cffbdcc441f_66_0.png)

```sas
title 'Response Plot';
proc sgplot data=sashelp.bubble;
refline 5 / axis=x transparency=0.7;
refline 2 / axis=y transparency=0.7;
bubble yyvalue group=group transparency=0.4;
keylegend title="Drug" inside=topright;
yaxis display=(nodelabel) min=4;
yaxis display=(nodelabel) max=10;
run;
```

图 3.2.34：气泡图

这是一个分组气泡图，通过大小显示响应。这里的气泡是不填充的，使用线条显示。使用了 Journal 样式和 `NOFILL` 选项。`BUBBLEMAX` 将图中气泡的最大大小设置为 50 像素。

![](img/0c09161c0be53934e5708cffbdcc441f_66_1.png)

```sas
title 'Response Plot';
proc sgplot data=sashelp.bubble;
bubble yyvalue group=group bubblemax=50 nofill;
keylegend title="Drug" inside=bottomleft;
yaxis display=(nodelabel) min=4;
yaxis display=(nodelabel) max=10;
run;
```

### 3.3 分类面板 (Classification Panels)

#### 3.3.1：柱状图面板

这是一个使用 `origin` 作为类变量的分类面板。每个单元格包含一个按类型分类的里程柱状图。皮肤效果和透明度可以实现不同的效果。

![](img/0c09161c0be53934e5708cffbdcc441f_67_0.png)

```sas
title 'Mileage by Type and Country';
proc sgpanel data=sashelp.cars;
where (type='Sedan' or type='Sports') and (origin='USA' or origin='Asia');
panelby origin / varname;
vbar type / response=mpg_city stat=mean dataskin=gloss
transparency=0.6;
xaxis;
run;
```

![](img/0c09161c0be53934e5708cffbdcc441f_67_1.png)

#### 3.3.2：箱线图网格

这是一个使用 `type` 作为类变量的分类面板。每个单元格包含里程的箱线图。它使用 `LAYOUT=ROWLATTICE` 在单列中创建多行。`COLAX` 用于显示列轴的网格线。

```sas
title 'Mileage by Type and Country';
proc sgpanel data=sashelp.cars nolegend;
where (type='Sedan' or type='Sports') and (origin='USA' or origin='Asia');
panelby type / layout=rowlattice varname;
hbox mpg_city / category=origin group=origin;
axis;
run;
```

![](img/0c09161c0be53934e5708cffbdcc441f_67_2.png)

![](img/0c09161c0be53934e5708cffbdcc441f_67_3.png)

Matange, Sanjay, and Dan. Statistical Procedures by Example: Effective Graphs Using SAS®. Copyright 2011,

SAS Institute, Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

### 图 3.3.3：直方图网格 (Histogram Lattice)

这是一个使用 `HISTOGRAM` 和 `DENSITY` 语句的 2x2 网格，按性别和血压状态显示胆固醇分布。`ROWAX` 和 `COLAX` 语句用于显示网格线。

![](img/0c09161c0be53934e5708cffbdcc441f_68_0.png)

```sas
title 'Cholesterol Panel';
proc sgpanel data=sashelp.heart noautlegend;
  where bp_status='Normal' or bp_status='High';
  panelby sex bp_status / layout=lattice varname;
  histogram cholesterol / transparency=0.5;
  density cholesterol;
  xaxis grid; colaxis grid;
run;
```

### 图 3.3.4：散点面板 (Scatter Panel)

此图有三个类变量：type、origin 和 drivetrain。每个单元格有三个标题，每个对应一个类变量。标题标签可以占据单元格空间的大部分。我们减小了标题字体大小（在样式中），为图表留出更多空间。

![](img/0c09161c0be53934e5708cffbdcc441f_68_1.png)

```sas
title 'Mileage by Horsepower';
proc sgpanel data=sashelp.cars;
  where (type='Sedan' or type='Sports') and (origin='USA' or origin='Asia') and (drivetrain='Front' or drivetrain='Rear');
  panelby origin type / varname onpanel columns=4;
  scatter x=horsepower y=mpg_city / transparency=0.6;
  xaxis grid; colaxis grid;
run;
```

### 3.4 比较和矩阵图 (Comparative and Matrix Graphs)

#### 3.4.1：对比散点图 (Comparative Scatter Plot)

这是一个散点图网格，按胆固醇和体重比较收缩压和舒张压。图使用共同轴，因此数据在行列之间是统一的。

![](img/0c09161c0be53934e5708cffbdcc441f_69_0.png)

```sas
title 'Comparative Graph';
proc sgscatter data=sashelp.heart;
where ageatstart > 58;
compare x=(cholesterol weight) y=(diastolic systolic) /
transparency=0.8 markerattrs=(symbol=circlefilled);
run;
```

#### 3.4.2：散点矩阵 (Scatter Plot Matrix)

这是一个散点矩阵，显示 58 岁以上患者变量之间的关联。可以使用透明度来查看数据分布。对角线显示每个变量自身的分布。

![](img/0c09161c0be53934e5708cffbdcc441f_69_1.png)

```sas
title 'Variable Association';
proc sgscatter data=sashelp.heart;
label weight='weight' cholesterol='Cholesterol'
diastolic='Diastolic' systolic='Systolic';
where ageatstart > 58;
matrix cholesterol diastolic systolic weight / diagonal=(histogram)
transparency=0.8 markerattrs=(symbol=circlefilled);
run;
```

Matange, Sanjay 和 Heath, Dan. 《Statistical Graphics Procedures by Example: Effective Graphs Using SAS®》。版权 © 2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。欲需更多 SAS 资源，请访问 support.sas.com/publishing。

## 第4 章

## 基础图表

- 4.1 引言 61

- 4.2 SGPLOT 过程 62

- 4.3 图表角色与选项 63

- 4.4 散点图 64

- 4.5 带有数据标签的散点图 74

- 4.6 折线图 78

- 4.7 阶梯图 84

- 4.8 区域图 89

- 4.9 针状图 94

- 4.10 矢量图 97

- 4.11 VBarParm 和 HBarParm 图 (9.3) 100

- 4.12 气泡图 (9.3) 105

- 4.13 高低图 (9.3) 108

- 4.14 参考线 112

- 4.15 参数化线图 (9.3) 115

- 4.16 瀑布图 (9.3) 117

- 4.17 合并图表 120

![](img/0c09161c0be53934e5708cffbdcc441f_72_0.png)

> “如果你不能简单地解释它，说明你还没有足够地理解它。”

~ 阿尔伯特·爱因斯坦
