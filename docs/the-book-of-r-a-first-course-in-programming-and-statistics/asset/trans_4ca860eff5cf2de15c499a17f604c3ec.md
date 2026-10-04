
供你参考，我的结果在这里。

![](img/b2cfc85cbb129f60fe595a2bae074fe4_712_0.png)

## 25.6 透视图 (Perspective Plots)

在本章中，你将查看的最后一种图表是*透视图*，它有时也被称为*框图*（wireframe）。与等高线和像素图像不同（后者通过线条模式和颜色颜色强调表面的波动），透视图使用物理第三维度，并在其上绘制 z 值。

### 25.6.1 基础图表与角度调整

当你想要强调 z 矩阵中数值的波动特性时，透视图会特别有用。例如，在某些应用中，你可能希望对绘制表面上的任何峰值和或谷值的相对极端程度有一个良好的印象，这在像素图像或等高图中很难实现。

回想第 25.4.1 节和第 25.5.1 节中以等高线和像素图像绘制的 mtcars 响应面。你在马力（horsepower）和重量（weight）变量中创建了一个 20 x 20 的评估网格，以及相应的包含 400 个元素的 z 矩阵，给出预测的平均 MPG ：

```r
R car.fit <- lm(mpg+hp+wt,data=mtcars)
R len <- 20
R hp.seq <- seq(min(mtcars$hp),max(mtcars$hp),length=len)
R wt.seq <- seq(min(mtcars$wt),max(mtcars$wt),length=len)
R hp.wt <- expand.grid(hp=hp.seq,wt=wt.seq,newdata=hp.wt,nrow=len,ncol=len)
R car.pred.mat <- matrix(predict(car.fit,hp.wt))
```

内置的 R 函数 `persp` 用于创建透视图。它的基本用法与 `contour`、`filled.contour` 和 `image` 相同。你在 x 和 y 轴方向上的递增序列定义了评估网格，并传递给 `x` 和 `y`，相应的 z 矩阵传递给 `z`。使用以下代码显示 20 x 20 mtcars 表面的默认外观：

```r
persp(x=hp.seq,y=wt.seq,z=car.pred.mat)
```

这出现在图 25-19 的左上角。

解释透视图非常直观。默认的视角显示 x 轴在前景，从左到右增加，y 轴在左侧，从前景向深层背景增加。这样，评估网格平铺在底部，你的表面从底部垂直到顶部在其上绘制。

视角是此类图表最重要的方面之一。在 `persp` 中，你可以通过两个选项 `theta` 和 `phi` 来控制它：`theta` 水平旋转图表，`phi` 调整垂直视角位置。两者都以度为单位；`theta` 默认为 0，`phi` 默认为 15，提供一个略微抬高的视角，让你看到 y 轴从前景延伸到背景。通常，你可以将 `theta` 的可能值认为是从 0 到 360 度之间的任何值，代表绕图表的完全旋转；将 `phi` 的可能值认为是从 90 到 -90 度之间的任何值，其范围是从直接从顶部向下俯视的鸟视角到直接从顶部向上观察的潜艇视角。

第二个示例演示了这种行为：

```r
persp(x=hp.seq,y=wt.seq,z=car.pred.mat,theta=30,phi=23,
xlab="Horsepower",ylab="Weight",zlab="mean MPG")
```

事实上，这行代码最初生成了第 92 页图 25-19 中右侧的图像（当你接触线性回归模型中两个连续预测变量之间的交互项概念时）。该图重现在图 25-19 的右上角。使用 `xlabel` 和 `ylab` 为轴命名，并使用 `zlab` 控制第三个垂直轴的标题。在这里，`theta` 和 `phi` 的使用使得视角比默认值略高，并旋转了图表，使原点（换说，表示 x-y 平下限的顶点）在前景中很显著。值得注意的是，`theta` 从 0 开始增加会顺时针旋转图表，但你也可以提供一个负值来反方向旋转图表。此处所示，设置 `theta=-30` 的效果与 `theta=30` 相同。
