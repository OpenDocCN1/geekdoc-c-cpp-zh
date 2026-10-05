

# 第2章 数值算法 45

![](img/fefa42765c0b410af6705110aea7c0cb_68_0.png)

**图 2-4：** `AdaptiveMidpointIntegration` 程序使用自适应梯形规则实现了比 `TrapezoidRule` 程序更好的近似结果。

以下伪代码展示了该算法：

```
// 通过 IntegrateAdaptiveMidpoint(Float: function()) 积分
Float: xmin, Float xmax, Integer: num_intervals,
Float: max_slice_error
// 计算初始梯形的宽度。
Float: dx = (xmax - xmin) / num_intervals
double total = 0

// 累加梯形的面积。
Float: total_area = 0
Float: x = xmin
For i = 1 To num_intervals
  // 加上此切片的面积。
  total_area = total_area +
  SliceArea(function, x, x + dx, max_slice_error)
  x = x + dx
Next i

Return total_area
End IntegrateAdaptiveMidpoint
```

```
// 返回此切片的面积。
Float: SliceArea(Float: function(), Float: x1, Float: x2,
Float: max_slice_error
```

```
// 计算端点和中点的函数值。
Float: y1 = function(x1)
Float: y2 = function(x2)
Float: xm = (x1 + x2) / 2
Float: ym = function(xm)
```

```
// 计算大切片和两个子切片的面积。
Float: area1 = (x2 - x1) * (y1 + y2) / 2.0
Float: arealm = (xm - x1) * (y1 + ym) / 2.0
Float: area2 = (x2 - xm) * (ym + y2) / 2.0
Float: arealm2 = area1 + area2
```

```
// 查看我们离有多近。
Float: error = (area2 - area1) / area1
```

```
// 查看这个误差是否足够小。
If (Abs(error) < max_slice_error) Then Return arealm2
```

```
// 误差太大。划分切片并再次尝试。
SliceArea(function, x1, xm, max_slice_error) +
SliceArea(function, xm, x2, max_slice_error)
SliceArea
```

如果你使用两个初始切片运行 `AdaptiveMidpointIntegration`，程序将它们划分为图 2-4 所示的 24 个切片，并以 -0.035% 的误差估计曲线下的面积。如果你使用具有 24 个等宽切片的 `TrapezoidRule` 程序，程序的误差为 -0.072%，是自适应程序产生误差的两倍。这两个程序使用的切片数量相同，但自适应程序放置的位置更有效。

`AdaptiveTrapezoidIntegration` 示例程序使用了不同的方法来决定何时将一个切片拆分为切片。它计算函数在起始 x 值处的二阶导数，并将区间划分为一个切片加上每个二阶导数值一个切片。例如，如果二阶导数为 2，程序会将切片分为三部分（选择切片数量的公式有些随意。你使用不同的公式可能会获得更好的结果。）

> 在你的情况下这种方法有点粗糙，导数告诉你在任何给定点的斜率。而它的二阶导数告诉你是斜率的变化率，或者说曲线弯曲得有多快。二阶导数越高，意味着曲线弯曲越紧密，因此 `AdaptiveTrapezoidIntegration` 程序使用了更多的切片。

当然，如果你无法计算二阶导数，这种技术就无法起作用。`AdaptiveMidpointIntegration` 使用的技术在任何情况下似乎都运行良好，因此你可以回退到该技术。

# 第2章 数值算法 47

自适应技术在许多算法中都非常有用，因为它们可以在不需要的地方不浪费精力，就能产生更好的结果。图 2-5 所示的 `AdaptiveIntegration` 程序使用自适应技术来估计阴影区域的面积。该区域包括垂直椭圆和水平椭圆的并，减去椭圆内部三个圆覆盖的面积。

![](img/fefa42765c0b410af6705110aea7c0cb_70_0.png)

**图 2-5：** `AdaptiveGridIntegration` 程序使用自适应积分估计阴影区域的面积。

该程序将整个图像划分为一个框，并在框内定义一个点网格。对于图 2-5 中的每个点，程序使用一个具有四行四列点的网格。对于网格中的每个点，程序确定该点位于阴影区域内部还是外部。

如果框中没有任何点位于阴影区域内，程序假设该框不在区域内并忽略它。

如果框中的每个点都在阴影区域内，程序认为该框完全位于区域内，并将框的面积加到区域的估计总面积中。

如果框中的某些点位于阴影区域内，某些点位于区域外，程序会将框细分为更小的框，并使用相同的技术计算这些较小框的面积。

在图 2-5 中，`AdaptiveGridIntegration` 程序绘制了框以便你可以看到它们。你可以看到，程序在阴影区域边缘考虑的框比在区域深处或外部多得多。总之，这个例子考虑了 19,217 个框，主要集中在它所积分区域的边缘。

# 蒙特卡洛积分

蒙特卡洛积分数值积分的一种形式，程序在区域内均匀生成一系列伪随机点，并确定每个点是否位于目标区域内。完成后，程序使用位于区域内的点占的百分比来估计区域的总面积。

例如，假设生成点的区域是 20 × 20，因此其面积为 400 平方单位， 37% 的伪随机点位于区域内。该区域的面积约为 0.37 × 400 = 148 平方单位。

图 2-6 所示的 `MonteCarloIntegration` 示例程序使用这种技术来估计与 `AdaptiveGridIntegration` 程序使用的相同形状的面积。

![](img/fefa42765c0b410af6705110aea7c0cb_71_0.png)

**图 2-6：** 阴影区域内部的点为黑色，区域外的点为灰色。蒙特卡洛积分通常比自适应方法更容易产生误差。

# 第2章 数值算法 49

## 寻找零

有时程序需要找出方程与 x 轴的交点。换句话说，给定方程 $y = f(x)$，你可能想找到 $f(x)=0$ 的 $x$。这样的值被称为根。

牛顿法（也称为牛顿法）是一种迭代近似根的方法。该方法从初始猜测 $X_i$ 开始。如果 $f(X_i)$ 不足够接近 0，算法沿着 $X_i$ 处的切线移动直到遇到 x 轴。它将交点的坐标作为新的猜测 $X_{i+1}$。

然后重复该过程。

困难的部分是确定如何跟随切线。如果你使用微积分找到函数的导数 $f'(x)$（也写作 $dfdx(x)$），以下方程显示了算法如何通过切线更新猜测：

```
X_{i+1} = X_i - \frac{f(X_i)}{f'(X_i)}
```

> 注意：遗憾，解释如何寻找函数的导超出本书的范围。更多信息请搜索网络或参考微积分书籍。

图 2-7 图地展示了这一过程。对应初始猜测的点标记为 1。该点的值远离 0，因此算法沿着切线移动直到遇到 x 轴。它计算新猜测的函数值，得到图 2-7 中标记为 2 的点。该点的纵坐标也远离 0，因此算法重复过程找到下一个猜测，标记为 3。算法再次重复过程找到标记为 4 的点。点 4 的纵坐标足够接近 0，算法停止。

以下伪代码描述了它：

```
// 使用牛顿法找到函数 f(x) 的根。
Float: FindZero(Float: f(), Float: dfdx(x), Float: initial_guess,
Float: maxError)
float x = initial_guess
For i = 1 To 100 // 以防出现问题，在 100 次后停止。
// 计算此点。
float y = f(x)
```

