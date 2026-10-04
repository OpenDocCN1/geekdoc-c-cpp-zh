

然后，在加载 ggplot 之后，执行以下代码以生成图 24-1 左侧的图像。

```
R> ggplot(surv, aes(x=Wr.Hnd,y=Height)) +
 geom_point(aes(col=Sex,shape=Sex)) + geom_smooth(method="loess")
```

对 ggplot 的调用初始化了对象并设置了 Wr.Hnd 默认映射到 x 轴、height 默认映射到 y 轴。添加 geom_point 会添加点，使用颜色和点类型来区分男性与女性。添加 geom_smooth 会叠加 LOESS 平滑器。默认情况下，估计趋势的 95% 置信区间由半透明的灰色阴影区域标出。

![](img/b2cfc85cbb129f60fe595a2bae074fe4_645_0.png)

图 24-1：展示 ggplot2（左）和 base R 绘图（右）用于显示使用 LOESS 的非参数估计趋势

现在我将演示如何使用基础绘图产生类似的结果。虽然存在 base R 函数，例如 scatter.smooth，可以相对快速地生成带有平滑趋势的散点图，但为了能够对置信区间区域进行此类阴影处理，能够按块构建绘图是有帮助的。与 ggplot2 方法相比，使用此 base R 代码的相对简易性，生成了图 24-1 右侧的图像：

```
R> plot(surv,Wr.Hnd,survHeight,col=survSex,pch=c(16,17),survSex)
R> smoother <- loess(Height~Wr.Hnd,data=surv)
R> handseq <- seq(min(surv$Wr.Hnd),max(surv$Wr.Hnd),length=100)
R> sm <- predict(smoother,newdata=data.frame(Wr.Hnd=handseq),se=TRUE)
R> lines(handseq,sm$fit)
R> polygon(x=c(handseq,rev(handseq)),
 y=c(sm$fit+2*sm$se,rev(sm$fit-2*sm$se)),
 col=adjustcolor("gray",alpha=0.5), border=NA)
```

第一行绘制数据，语法使用内置的 loess 函数来生成平滑趋势——语法与 lm 相同。就像由 lm 拟合的线性模型一样，为了开始绘制，你需要

设置 x 轴变量的精细序列值，以便在该处获得点估计值及其标准误差；这通过第三行的 seq 实现，随后在第四行使用 se 参数设置为 TRUE 的 predict 实现。这会产生对象 sm，一个列表，其中包含组件 $fit 和 $se，如常。

然后使用 smooth 在对 lines 的调用中绘制平滑趋势。最后，为预测值计算一个粗略的 95% 置信区间，即预测值减去相应的标准误差 se 中的两倍。这是在对 polygon 的调用中直接完成的，polygon 通过置信区间形成的顶点绘制灰色带；颜色通过对即用型 adjustcolor 的调用赋予灰色填充形状以使其透明，参数 alpha 的取值范围为 0，即完全透明；alpha=0.5 设置指定 "gray" 的 50% 不透明度

全部完成，且图例尚未添加！此示例暴露了 base R 版本的图像，在脚本长度方面并不需要，也需要整个构建过程的思考；例如，适当地组合置信区域的多边形顶点并记住调整填充形状的偏移以防止预先绘制的覆盖。这在你对此类功能变得稍微更有雄心时变得更加明显。假设你想分别叠加每个性别的平滑器；这将需要分别估计 LOESS 函数并重新思考绘图策略。然而，在 ggplot 术语中，此添加是简单的，只需更改相关 geom 的美学映射即可。以下代码生成

图 24-2：

```
R> ggplot(surv, aes(x=Wr.Hnd, y=Height, col=Sex, shape=Sex)) + 
  geom_point() + geom_smooth(method="loess")
```

所需的一切就是颜色和点类型的美学映射（分别为 col=Sex 和 shape=Sex）已转移，因此它不再仅特定于绘制的点，而是成为初始化调用 ggplot 中声明的默认映射的一部分。之后添加的任何图层如果未分配映射，将遵循此默认值，就像 geom_point 和 geom_smooth 的情况一样。

NOTE LOESS 及其他趋势平滑器的实现取决于你指定想要的平滑量；这是通过控制用于每个局部加权子集的数据比例来控制的，对于估计过程中的每一步/每个位置。较大的比例会导致比较小比例更平滑、变化更小的趋势。此值称为 span，可以通过 loess 或 geom_smooth 中的可选参数 span 来设置；然而，对于快速数据探索，默认值为 0.75 通常足够。你可以尝试在本节的示例绘图上尝试此操作，以查看其对各自的影响。

![](img/b2cfc85cbb129f60fe595a2bae074fe4_647_0.png)

## 24.2.2 构建平滑密度估计

平滑的想法不仅限于散点图趋势。核密度估计（KDE）是一种基于观测数据生成概率密度函数的平滑估计的方法。简而言之，KDE 涉及对数据集中的每个观测值应用一个缩放的概率函数（核）并将它们全部求和，以给出整个数据集分布的印象。它基本上是直方图的复杂版本。有关理论细节，Wand 和 Jones（1995）的文本是一个很好的参考。

为了说明此方法，请考虑内置的 airquality 数据框；在提示符下输入 ?airquality 以打开文档，其中告诉你它包含在几个月内对纽约空气进行的若干测量。以下行提供的温度测量的核密度估计的基本绘图显示在图 24-3 上：

```
R> ggplot(data=airquality,aes(x=Temp)) + geom_density()
```

使用 R 绘图也可以相对容易地创建此类绘图，使用内置命令为给定的数据向量实现 KDE。然而，ggplot2 让你能够使用美学映射相对轻松地装饰绘图——这是 ggplot2 的一大吸引力。例如，假设你想根据观测月份分别可视化温度的密度估计。首先，执行以下代码：

```
R> air <- airquality
R> air$Month <- factor(air$Month, labels=c("May", "June", "July", "August", "September"))
```

![](img/b2cfc85cbb129f60fe595a2bae074fe4_648_0.png)

**图 24-3：** *使用 ggplot2 功能通过 KDE 可视化 airquality 数据框中的温度分布*

这在你的工作区中创建了 airquality 数据框的副本，并将原本为数值的 Month 向量重新编码为因子向量（ggplot 映射所需），并适当地标记条目。使用 air，以下代码生成图 24-3 中的右图：

```
R> ggplot(data=air,aes(x=Temp, fill=Month)) + geom_density(alpha=0.4) + ggtitle("Monthly temperature probability densities") + labs(x="Temp (F)",y="Kernel estimate")
```

不同的密度通过不同的颜色清晰标识，使用在绘图初始化中由 ggplot 映射的 fill=Month in aes。你还向 geom_density 提供了 alpha=0.4 以设置 40% 不透明度，以便可以看到全部五条曲线。剩余的对 ggtitle 和 labs 的调用只是整理主标题和轴标题。这些测量的分布特征与你预期的相同——七月，即最热的月份的温度，集中在远高于例如五月的数值范围内。

> 就像 LOESS 技术一样，核估计概率密度函数的精确外观取决于所启用的平滑量。与直方图中的 binwidth 类似，KDE 中感兴趣的量称为带宽或平滑参数——较大的带宽会在数据范围内施加更平滑的平滑。默认情况下，这些示例中的带宽使用数据驱动技术自动选择。此默认平滑水平通常足以进行数据的简单探索。

