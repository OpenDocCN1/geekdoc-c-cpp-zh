
现成可用的 R 数据，即著名的 iris（鸢尾）数据。该数据收集于 20 世纪 30 年代中期，是一个包含 150 行 5 列的数据框，由三个多年生植物的花瓣和花萼测量值组成——藻鸢尾（Iris setosa）、大花鸢尾（Iris virginica）和三彩鸢尾（Iris versicolor）（(Anderson, 1935; Fisher, 1936）。你可以在这里查看前几记录：

```
R> iris[1:5]
Sepal.Width Sepal.Length Petal.Width Petal.Length Species
1 5.1 3.5 1.4 0.2 setosa
2 4.9 3.0 1.4 0.2 setosa
3 4.7 3.2 1.3 0.2 setosa
4 4.6 3.1 1.5 0.2 setosa
5 5.0 3.6 1.4 0.2 setosa
```

通过查看 iris，你可以发现每个物种的变量都有 50 个观测值，单位为厘米（cm）。

## 14.4.1 单幅图

你可以修改简单的散点图，将绘制的点按分类变量拆分，从而揭示连续变量与任何可见关系之间潜在的差异。例如，使用基础 R 图形，你可以根据三个物种检查花瓣测量值。使用第 7 章中首次解释的“设置石头”方法，你可以通过使用 `type="n"` 生成正确尺寸的空绘图区域，随后为每个物种添加点，并根据需要更改点的形状和颜色。

```
R> plot(iris[4],iris[3],type="n",xlab="Petal Width (cm)",ylab="Petal Length (cm)")
R> points(iris[iris$Species=="setosa",4], iris[iris$Species=="setosa",3],pch=19,col="black")
R> points(iris[iris$Species=="virginica",4], iris[iris$Species=="virginica",3],pch=19,col="gray")
R> points(iris[iris$Species=="versicolor",4], iris[iris$Species=="versicolor",3],pch=19,col="black")
R> legend("topleft",legend=("setosa","virginica","versicolor"), col=c("black","gray","black"),pch=c(19,19,19))
```

你可以在图 14-8 中找到该图。注意，大花鸢尾（Iris virginica）的花瓣最大，其次是三彩鸢尾，最小的花瓣属于藻鸢尾。然而，这段代码虽然可以运行，但相当繁琐。你可以通过先设置指定每个观测值所需点形状和颜色的向量来生成相同的图像。

![](img/b2cfc85cbb129f60fe595a2bae074fe4_335_0.png)

**图 14-8：** 使用内置 iris 数据框按物种划分的花瓣测量值散点图

## 考虑这里创建的两个对象：

第一行创建了一个名为 *iris_pch* 的向量，其长度等于 iris 中的观测值数量，每个条目均为 19。向量子集随后覆盖了对应于 *Iris versicolor* 的条目，并将点形状设置为 1。按照相同的步骤创建 col_col；填充一个大小合适的向量，内容为字符字符串 "black"，并将那些对应于 *Iris virginica* 的条目重写并设置为 "gray"。此后，注意接下来显示的单行代码，紧接相同的 `legend` 调用，将产生一个完全相同的图：

```r
plot(iris[,4,3],col=iris_col,pch=iris_pch, xlab="Petal Width (cm)",ylab="Petal length (cm)")
```

## 14.2 散点图矩阵

“单幅”类型的平面散点图仅在比较两个数值型连续变量时才真正有用。当有更多感兴趣的连续变量时，无法显示……一种简单且常用的解决方案是每对变量生成双变量散点图，并以结构化的方式将它们在一起；这被称为*散点图矩阵*（scatterplot matrix）。利用之前创建的 iris_pch 和 iris_col 向量，你可以为 iris 中的所有四个连续变量生成散点图矩阵，保留物种之间的区别。使用基础 R 图形，请使用 `pairs` 函数。

```
R> pairs(iris[,1:4],pch=iris_pch,col=iris_col,cex=0.75)
```

你可以在图 14-9 中找到该行的结果。

![](img/b2cfc85cbb129f60fe595a2bae074fe4_336_0.png)

图 14-9：数据框中所有四个连续测量值的散点图矩阵

使用 `pairs` 最简单的方法是将原始观测值的矩阵或数据框作为其第一个参数，这是通过选择 iris 中除 Species 列以外的所有列（iris[,1:4]）完成的。图的解释取决于对角线面板的标记，从左上角到右下。它们出现的顺序与作为第一个参数给出的列顺序相同。“标记面板”（label panels）允许你确定矩阵中的每张单独图对应于哪对变量。例如，图 14-9 中散点图矩阵的第一列对应于花萼长度（Sepal Length）x 轴变量；矩阵的第三行对应于花瓣长度（Petal Length）y 轴变量。

