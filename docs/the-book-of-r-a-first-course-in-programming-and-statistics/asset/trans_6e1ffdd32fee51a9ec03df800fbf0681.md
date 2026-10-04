

+   b. 现在，打开一个 8 × 7 英寸的新图形设备。将图形边距设置为底部、顶部和右侧分别为两、五、三和五行。也允许在除底部外的每侧留出一条外边距线空间，底部应留出两行外边距。

+   i. 制作一个散点图，纵轴为钻石价格，横轴为克拉重量。使用红色、绿色和蓝色区分认证的点。抑制初始绘图中的所有轴、框、标签和标题，然后添加一个 U 形框。

+   ii. 添加水平轴。使用从 0.2 到 1.1 的等间距克拉值序列作为刻度标记，步长为 0.1。使用粗体、斜体、无衬线风格字体为标签，并将标签添加到距离轴仅半行处。然后在现有刻度之间添加较小的向外刻度标记。为此，对轴函数进行第二次调用，并将刻度放置在从 0.15 到 1.05 的值序列上，步长为 0.1。将这些次要刻度标记的长度设置为一行长度的四分之一，并抑制轴。

+   iii. 添加垂直轴。在左侧，刻度应出现在 SGD$1000–17000 处。标签应水平可读且字体样式与水平轴相同。在右侧，轴刻度应以美元（USD$）等价形式制作，序列为 SGD$1000–11000，步长为 SGD$100，并应如此标记。为此，使用转换 USD = 1.37 × SGD$。标签方向和字体应与其它轴匹配。

+   iv. 对数据拟合价格关于克拉重量的二次多项式的线性模型。提供模型对覆盖观测值范围的克拉值序列的预测；包括 95% 预测区间的估计。使用此信息在散点图上叠加一条灰色实线表示拟合值，以及灰色虚线表示预测区间。

+   v. 设置用于标记近似美元转换和回归方程的表达式对象。将转换命名为 expr1；它应看起来像 USD ≈ 1.37 × SGD$。回归方程应看起来类似 Price = $\beta_0 + \beta_1Carat + \beta_2Carat^2$，命名为 expr2。

+   vi. 使用 mtext 添加三个单独轴的适当名称和标题。你可能需要为每个轴尝试一点行深度，以及是否在外边距或图形边距中书写，取决于你自己的间距偏好。最右侧的轴标题应使用 expr1。
vii. 要么通过反复试验找到合适的坐标，要么使用练习 23.1 中的 interactive.arrow 函数，放置一个指向拟合多项式线的箭头并用 expr2 标记它。
viii. 最后，使用 locator 在任何合适的位置放置图例，引用点的颜色根据适当的认证。

我的绘图版本看起来像这样：

![](img/b2cfc85cbb129f60fe595a2bae074fe4_641_0.png)

## 本章的重要代码

| Function/operator | Brief description | First occurrence |
|---|---|---|
| dev.new | Open new graphics device | Section 23.1.1, p. 576 |
| dev.set | Change active device | Section 23.1.2, p. 577 |
| dev.off | Close device | Section 23.1.3, p. 578 |
| par | Set graphical parameters | Section 23.1.4, p. 579 |
| layout | Open new graphics device | Section 23.1.4, p. 580 |
| box | Add box to plot | Section 23.2.1, p. 583 |
| mtext | Write text in margins | Section 23.2.2, p. 584 |
| locator | Interpolate coordinates | Section 23.3.1, p. 587 |
| axis | Add axis to plot | Section 23.4.3, p. 594 |
| expression | Render Greek/math in plot | Section 23.5.2, p. 598 |
| title | Add main/axis titles | Section 23.5.2, p. 598 |
| italic | Italicize text | Section 23.5.3, p. 600 |
| grid | Add grid to plot | Section 23.6, p. 605 |

# 24

# 使用图形语法
进一步探索

![](img/b2cfc85cbb129f60fe595a2bae074fe4_642_0.png)

你在第 7.4 节和第 14 章中介绍了 ggplot2 包的基础知识——它提供了传统 R 绘图的替代方案。本章中，你将查看该包的一些更受欢迎和有用的功能，以及它的相对年轻的表亲 ggvis，它提供基于浏览器的交互式体验。

## 24.1 ggplot 或 qplot？

到目前为止，在创建相对简单的 ggplot 绘图时，你一直使用 qplot 函数来初始化视觉对象。事实上，更通用的 ggplot 命令是 ggplot2 的核心函数。这两个初始化函数之间有几个关键区别：

- qplot 是 ggplot 的快捷版本；如果你只是想快速查看数据或直接在 R 控制台中工作时使用它。

- qplot 设计为让人联想到基础 R plot 函数——传递 x 和 y 坐标向量并告诉它做什么。相比之下，ggplot 希望其数据为数据框对象，并通过显式添加 geom 层来告诉你做什么。

- 单独调用 qplot 即可生成图形。使用 ggplot 时，必须在任何可见内容之前添加层。

- 要访问 ggplot2 绘图的全部功能和灵活性，ggplot 是推荐的函数；这以提供比 qplot 要求更多的指令为代价。

总的来说，你可以使用 qplot 或 ggplot 创建绘图。许多用户根据数据的形式（即数据框或作为全局环境中的单独向量）以及他们是否想要精美的视觉效果（例如用于出版目的）或只是想在控制台中工作时快速查看数据来做出决定。

作为语法的一个快速示例，翻回第 297 页的代码，该代码用于创建图 14-5 右侧的直方图。你可以认为对该特定绘图所做的众多修改证明了使用 qplot 之外的更模块化的方法。加载 ggplot2 并创建以下三个：

```
R> gg.static <- ggplot(mtcars, aes(x=hp)) + 
ggtitle("Horsepower") + labs(x="HP")
R> mtcars.mm <- data.frame(mm=mean(mtcars$hp),median(mtcars$hp),
  stats=factor(c("mean", "median")))
R> gg.lines <- geom_vline(mapping=aes(xintercept=mm, linetype=stats),
  show.legend=TRUE,data=mtcars.mm)
```

第一个对象 gg.static 表示如果以后想要尝试添加其他功能，绘图中将保持不变的部分。注意 ggplot 的调用与 qplot 不同之处在于第一个参数是感兴趣的整个数据框，允许在后续的 geoms 或注释中访问框架内的所有数据列。然后添加 ggtitle 和 labels 以设置主标题和水平轴标题。第二个对象 mtcars.mm 将马力均值和中位数存储为“虚拟”数据框。然后通过第三个对象将均值和中位数线叠加在直方图上，该对象是对 geom_vline 函数的单次调用，使用了早期代码中相同的内容，只是形式略有修改以忠实于 ggplot 的初始使用。

直到你进行打印 ggplot2 对象（正如第 7.4 节所述）的调用之前，什么都不会显示。以下调用重现了图 14-5 右侧的图像：

```
R> gg.static <- geom_histogram(color="black",fill="white") + 
breaks=seq(0,400,25),closed="right") + gg.lines + 
scale_linetype_manual(values=c(2,3)) + labs(linetype="")
```

创建图 14-5 的各个部分以相同的方式组合在一起：向 gg_static 添加 geom_histogram 层会调用绘图，并通过 scale_linetype_manual 在均值和中位数上添加 gg_lines 线型。如果你想在没有这些线的情况下生成直方图，你只需打印 gg_static 对象 plot_histogram。

随着你对 ggplot2 越来越熟练，你会发现自己根据应用的不同在 ggplot 或 dplyr 之间切换。帮助文件中的 ?ggplot 提供了 ggplot 通常使用的类型以及它与 ?plot 的比较的良好描述。有关更多信息，请参阅 Wickham (2009) 的 ggplot2: Elegant Graphics for Data Analysis。我将在本章的其余绘图中继续使用 ggplot，以提供一些 ggplot 语法的示例，以便与早期使用 ggplot 的情况进行比较。

## 24.2 平滑和着色

使用 ggplot2 包进行数据可视化特别是在你想按一个或多个分类变量拆分绘图特征时。这在你用 R 命令更难实现的功能增强绘图时尤其明显。

### 24.2.1 添加 LOESS 趋势

当你查看原始数据时，有时很难在不拟合参数模型（例如通过线性回归）的情况下获得趋势的整体印象，这意味着要对这些趋势的性质做出假设。这就是非参数平滑发挥作用的地方——你可以使用某些方法来确定你的数据似乎如何表现，而无需拟合特定模型。这些方法是在解释所有趋势形式时具有灵活性的辅助手段，代价是你没有提供响应与预测变量之间关系的特定数值细节（因为你没有估计任何系数，例如异常值和截距），并且你失去了任何可靠的外推能力。

局部加权散点平滑（LOESS 或 LOWESS）是一种非参数平滑技术，它通过在解释变量的整个范围内逐步对数据的局部子集进行回归方法来生成趋势。

> 有关理论细节，《Applied Nonparametric Regression》（Härle，1990）第 6 章以及《Introduction to Nonparametric Regression》（Takazawa，2006）第 2 章和第 3 章提供了 LOESS 方法的清晰讨论。

作为一个说明，加载 MASS 包并返回到 survey 数据框。首先，创建一个新的数据框或返回并删除任何缺失值以避免警告信息：

```
R> surv <- na.omit(survey[,c("Sex", "Wr.Hnd", "Height")])
```

