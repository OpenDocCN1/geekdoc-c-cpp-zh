
这里的关键点在于，y 的计算并不是作为 x 的直接结果得到的，就像你在绘图（例如线性回归模型）时可能会在 x 中获得一个细密的、均匀间隔的递增序列并评估 y。相反，(26.1) 中的方程共同定义了 2D 空间中轨迹的规则。

## 3D 柱体

绘制三维曲面的方法非常相似，只是你的方程为 x、y、z 轴上所有满足条件的点设定了规则。

例如，位于空心圆柱上的点可以通过以下方程定义：

```
x = r cos(theta), y = r sin(theta), and z = z  (26.2)
```

为了实际绘制出满足规则的图表，你需要确定一个固定的半径 $r$，识别出 $0 \le theta < 360$（度），并定义一个固定的最大高度 $h$ 以确保 $0 \le z \le h$。为了生成 x、y 和 z 的向量，你首先需要设置覆盖 theta 和 z 可能值的数值范围。考虑以下内容：

```
r <- 3
h <- 10
zseq <- 0:h
theta <- 0.360*(pi/180)
```

这些行显示将半径 $r$ 设置为 3，最大高度 $h$ 设置为 10。zseq 中的序列设置为从 0 到 10 的 11 个整数值——这将允许你在每个定义的 z 值的轴上放置点。theta 的序列设置为 $0 \le theta < 2\pi$（在 theta 中进行了到弧度的必要转换）。然后，你需要这些参数 (x,y,z) 坐标的所有唯一组合来进行绘图。你已经在第 25.3 节学习过如何使用 `expand.grid` 这一点。

```
zheta <- expand.grid(zseq, theta)
nrow(zheta)
[3971]
```

对结果调用 `nrow` 显示你现在拥有 $11 \times 361 = 3971$ 个唯一的高度-角度值。你能够根据 (26.2) 生成 x、y 和 z 的值。你可以使用 `for` 循环（第 10.2.1 节）遍历 zheta 的每一行，但更好的方法是使用 `apply` 中的隐式循环（详情请参考第 10.2.3 节）。

```
x <- apply(zheta,1,function(vec) r*cos(vec[2])
y <- apply(zheta,1,function(vec) r*sin(vec[2])
z <- apply(zheta,1,function(vec) vec[1])
```

注意，这里使用了匿名函数（参见第 11.3.2 节）来处理组成 zheta 每一行的两个元素的高度-角度（按此顺序）向量。

你可以使用 `rgl` 包中的 `persp3d` 来绘制这种参数定义的曲面，但方法与本章早些章节略有不同。计算出的 x、y 和 z 坐标现在必须以相同大小、适当排列的矩阵提供。这是因为 x 和 y 坐标中不再有均匀间隔的评估网格——与 z 值一样，x 和 y 值都是通过应用 (26.2) 定义的。在这些图中，你实际上拥有一个由参数值唯一组合（在本例中高度和角度）定义的潜在评估网格。

x、y 和 z 坐标中的矩阵由三个 $11 \times 361$ 的矩阵给出，以典型的列优先方式填充 x、y 和 z。

```
x <- matrix(x,length(zseq),length(theta))
ym <- matrix(y,length(zseq),length(theta))
zm <- matrix(z,length(zseq),length(theta))
```

此时，值得提到的是内置的 `outer` 函数，它接受两个变量的值序列并产生所有值的唯一组合，计算每个组合的结果，然后将结果作为矩阵返回——一次性完成了由 `expand.grid`、`apply` 和 `matrix` 所完成的三项任务。通过这种方法，你只需调用以下代码即可创建 xm、ym 和 zm：

```
xm <- outer(zseq,theta,function(z,t) r*cos(t))
ym <- outer(zseq,theta,function(z,t) r*sin(t))
zm <- outer(zseq,theta,function(z,t) z)
```

这里唯一的区别是，作为第三参数提供的匿名函数必须显式定义为两个独立的参数，分别代表必要的高度和角度参数的值。

无论你如何获得 xm、ym 和 zm，只需用这些坐标矩阵调用 `persp3d` 即可。额外调用 `points3d` 以强调这些矩阵中的精确评估点。后续几行的结果所示图 26-17 的左侧。

```
persp3d(x=xm,y=ym,z=zm,col="red")
points3d(x=xm,y=ym,z=zm)
```

![](img/b2cfc85cbb129f60fe595a2bae074fe4_758_0.png)

图 26-1：使用 `persp3d` 绘制圆体和锥体，三个坐标方向上都使用了矩阵参数。轨迹由相应的参数方程定义。圆体上的黑环代表存储在矩阵、ym 和 zm 中的实际评估点。

## 3D 锥体

此示例将说明，一旦理解了设置 x、y 和 z 矩阵的方法，就可以使用它们显示任何 3D 形状或曲面。将 r、h 和 theta 分别作为底半径、最大高度和角度，锥体遵循这些方程：

```
x = \frac{-z}{h}r\cos(\theta), \quad y = \frac{h-z}{h}r\sin(\theta), \quad \text{and} \quad z = z \quad (26.3)
```

使用相同的对象 r、h、zseq，以下代码修改了匿名函数以反映 (26.3)。图 26-7 的右侧显示了结果。

```
xm <- outer(zseq,function(z,t), (h-z)/h*r*cos(t))
ym <- outer(zseq,function(z,t), (h-z)/h*r*sin(t))
zm <- outer(zseq,function(z,t), z)
persp3d(x=xm,y=ym,z=zm,col="green")
```

## 抽象

数学、应用数学建模和统计学的许多领域都利用了高维形状。为了结束本节以及整本书，让我们使用 `rgl` 来利用第 26.4.1 节的技能观察一些著名的抽象。

## 莫比乌带

一个经典的例子是莫比乌带——一种只有一个面和一条边的连续曲面。它可以使用参数方程表示：

```
$x = F(v,\theta) \cos\theta, \quad y = F(v,\theta) \sin\theta, \quad \text{and} \quad z = \frac{v}{2} \sin\left(\frac{\theta}{2}\right) \quad (26.4)$
```

其中

$F(v,\theta) = 1 + \frac{v}{2} \sin\left(\frac{\theta}{2}\right)$

$-1 \le v \le 1$ 且 $0 \le \theta < 2\pi$（弧度）。参数 $v$ 控制沿宽度的位置，$\theta$ 控制旋转。你可以以绘制圆体的方法设置 vseq 和 theta。分辨率为 200：

```
res <- 200
vseq <- seq(-1,1,length=res)
theta <- seq(0,2*pi,length=res)
```

接下来，使用 `outer` 获取根据 (26.4) 的 $200 \times 200$ 矩阵。

```
xm <- outer(vseq,theta,function(v,t) (1+v/2)*cos(t))
ym <- outer(vseq,theta,function(v,t) (1+v/2)*sin(t))
zm <- outer(vseq,theta,function(v,t) v/2)
```

然后，在 `rgl` 包中快速调用 `plot3d` 将向你显示莫比乌带上的 40000 个位置。后续行的结果所示图 26-17 的左侧：

```
plot3d(xm,ym,zm)
```

让我们使用 `persp3d` 将带显示为连续曲面，以充分理解单面/单边的现象。图 26-18 的右侧显示了以下代码的结果：

```
persp3d(x=xm,y=ym,z=zm,col="orange",axes=FALSE,xlab="",ylab="",zlab="")
```

注意使用 `axes` 来抑制默认框，并使用空字符串轴来移除表示 xm、ym 和 zm 的默认轴。

![](img/b2cfc85cbb129f60fe595a2bae074fe4_760_0.png)

你还可以更有趣的方式使用颜色来强调莫比乌带的环绕特性。从第 25.1.3 节定义的颜色获取灵感，创建以下自定义调色板：

```
patriot.colors <- colorRampPalette("red4", "red", "white", "blue", "white", "red", "red4")
```

此调色板专门用于从深红色到白色，还可以从蓝色绕回深红色。这对于 `patriot.colors` 中的颜色以逐点方式分配给绘制的带的方法是必要的。

给定预设值 `res`（控制 vseq 和 theta 的长度），绘制曲面的颜色向量长度为 $200^2 = 40000$。为了填充该向量，执行以下操作：

```
stripcols <- patriot.colors(2+res-1)
stripcols <- rep(NA,res^2)
for(i in 0:(res-1)){
  stripcols[1:res+res+i] <- stripcols[1:res+i]
}
```
