

# 344 实例实例学习 SAS：程序员指南，第二版

# 程序 20.7：时间序列图

```sas
data Moving_Average;
  set Learn.Stocks;
  Previous = lag(Price);
  Two_Back = lag2(Price);
  if n ge 3 then Moving=mean(Price, Previous, Two_Back);
run;

title "Series Plot";
proc sgplot data=Moving_Average;
  series x=Date y=Price;
  series x=Date y=Moving;
run;
```

价格与日期的对比图从 2017 年 1 月 1 日开始——移动平均线图从第 3 天开始。

以下是输出结果：

# 图 20.7：程序 20.7 的输出

![](img/e9e15d853989558188e1c83b0ae655b0_351_0.png)

你可以看到，使用移动平均可以平滑掉每日的一些波动。

第 20 章：创建图表和图形 345

## 20.7 说明生成平滑曲线的两种方法

除了通过直线连接数据点的功能外，PROC SGPLOT 还提供了两种非线性曲线拟合方法。这两种方法都使用局部回归模型生成平滑曲线。

第一种方法使用局部点拟合曲线的部分。为了控制平滑曲线跟随数据点的紧密程度，请在 PBSPLINE 中指定 `SMOOTH=` 数值选项。

## 20.8：平滑曲线 - 样条

```sas
title "Smooth Curve - Splines"
proc sgplot data=SASHelp.Iris;
  bspline x=PetalWidth y=PetalLength;
run;
```

你使用 PBSPLINE 语句，并使用所需的选项 X 和 Y 指定两个坐标轴上的变量。此程序使用了鸢尾花花瓣数据（见第 20.4 节），并在散点图中添加了一条平滑线，如下所示：

图 20.8：程序 20.8 的输出

![](img/e9e15d853989558188e1c83b0ae655b0_352_0.png)

如前所述，你可以通过 PBSPLINE 语句中的选项来控制“抖动”的程度。

346 实例学习 SAS：程序员指南，第二版

下一种平滑方法称为 LOESS 方法。虽然这不是一个精确的缩写，但该方法的多数文档代表“局部回归”（Local Regression）。接下来显示的程序使用了与程序 20.8 相同的鸢尾花数据，但使用了 LOESS 方法代替了 PBSPLINE。

# 程序 20.9：平滑曲线 - LOESS 方法

```sas
title "Smooth Curve - LOESS Method"
proc sgplot data=SASHelp.Iris;
loess x=PetalWidth y=PetalLength;
run;
```

此程序生成了下面的图表：

图 20.9：程序 20.9 的输出

![](img/e9e15d853989558188e1c83b0ae655b0_353_0.png)

与 PBSPLINE 一一样，你可以为 LOESS 语句添加选项，以控制线条跟随数据点的紧密程度。

## 20.8 生成直方图

如果你想查看变量的直方图，请使用 `HISTOGRAM` 语句后跟响应变量。该程序为 Learn 数据集中变量 RBC（红细胞计数）生成直方图。此外，带有响应变量的 `DENSITY` 语句会在直方图上叠加一条正态曲线。默认正态密度的替代方案是核密度（KERNEL density）。你可以通过 `TYPE=KERNEL` 选项生成核密度曲线。以下是带有默认正态密度曲线的程序：

第 20 章：创建图表和图形 347

# 程序 20.10：叠加正态曲线的直方图

```sas
title "Histogram with a Normal Curve Overlaid"
proc sgplot data=Learn.Blood;
histogram RBC;
density RBC;
```

输出显示了直方图和叠加的正态密度曲线。你可以包含选项来控制图中箱（bins）的数量或大小。你使用 `BINWITH=` 选项选择箱宽——`NBINS=` 选项允许你指定直方图中箱的数量。

# 图 20.10：程序 20.10 的输出

![](img/e9e15d853989558188e1c83b0ae655b0_354_0.png)

此图表是在没有任何选项的情况下生成的。也有用于 x 轴和 y 轴外观的选项。

## 20.9 生成简单的箱线图

箱线图（也称为箱须图）是统计学中一个称为探索性数据分析（EDA）的领域常用的技术。该图显示了重要值，如中位数、第一分位数和第三分位数，以及被称为离群值的数据点。

为了演示箱线图，下面的程序为 Blood 数据集中的变量 RBC 生成箱线图。如果你想要水平图表，请使用 `HBOX` 语句；如果你偏好垂直图表，请使用 `VBOX` 语句。

348 实例学习 SAS：程序员指南，第二版

# 程序 20.11：简单箱线图

```sas
title "Simple Box Plot"
proc sgplot data=Learn.Blood;
hbox RBC;
```

这是输出结果：

图 20.11：输出

![](img/e9e15d853989558188e1c83b0ae655b0_355.png)

箱内的垂直线代表中位数，从两侧延伸的线分别代表第一分位数和第三分位数。箱外的菱形点代表四分位距。

## 20.10 生成分组箱线图

若要为每个分组值生成箱线图，请在 `HBOX` 或 `VBOX` 语句中使用 `GROUP=` 选项。下面的程序生成了如下：

# 程序 20.12：分组箱线图

```sas
title "Box Plot with Grouping Variable"
proc sgplot data=Learn.Blood;
hbox RBC / group=Blood;
```

此程序生成了这里的图表：

图 20.12：

![](img/e9e15d853989558188e1c83b0ae655b0_356_0.png)

## 20.11 展示叠加与透明度

如前所述，PROC SGPLOT 的每个图都是叠加的。你可以使用关键字设置任何图的透明度。

# 程序 20.13：展示叠加与透明度

```sas
title "Demonstrating Overlays and Transparency"
proc sgplot data=SASHelp.Iris;
vbar Species / Response=PetalWidth width=.8;
vbar Species / Response=PetalLength width=.3 transparency=.2;
run;
```

这是输出结果：

![](img/e9e15d853989558188e1c83b0ae655b0_357_0.png)

本章仅接触了 PROC SGPLOT 的基础。SAS 网上有几本书籍和大量的文档讨论了该过程。对于那些使用 SASGRAPH 生成图表和图形的人来说，你会发现使用 PROC SGPLOT 要简单得多。

## 20.12 练习

奇数题解答位于书末。所有题目的解答向教授提供。如果你是教授，请访问书籍配套网站 support.sas.com 获取有关获取所有题目解答的信息。

- 使用 SASHelp 数据集，为变量 `Status` 生成频率条形图。其显示如下：
![](img/e9e15d853989558188e1c83b0ae655b0_358_0.png)

- 使用 SASHelp 数据集，为男性和女性生成平均 `Cholesterol` 的条形图。变量名为 `Cholesterol` 和 `Sex`。其显示如下：
![](img/e9e15d853989558188e1c83b0ae655b0_358_1.png)

- 使用 SASHelp 数据集，为男性和女性生成平均 `Height` 的水平条形图。使用选项使条形不填充（仅轮廓）并使条形大小为最大值的 25%。其显示如下：
![](img/e9e15d853989558188e1c83b0ae655b0_359_0.png)

- 使用 SASHelp 数据集，生成一个 x 轴为 `Height`、y 轴为 `Weight` 的散点图。其显示如下：
![](img/e9e15d853989558188e1c83b0ae655b0_359_1.png)

