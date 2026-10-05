
c:*, 施加约束，使得单元格 t 的值与单元格 distance 的值的积等于 AU 单元格的值。

让我们考虑视差测量的到织女星（Vega）的距离。我们创建两个单元格：用于距离的 `Vega-parallax-distance` 和用于视差角的 `Vega-parallax`：

```
(define-cell Vega-parallax-distance)
(define-cell Vega-parallax)
```

现在，我们可以使用刚刚定义的传播器构造函数将这些单元格连接起来：

```
(c:parallax<->distance Vega-parallax Vega-parallax-distance)
```

这样构建的单元格和传播器系统如图 7.3 所示。

![](img/2e72770736573f9ba6300d8cdb1e28c1_381_0.png)

图 7.3 在这里看到一个名为 `Vega-parallax-distance`（图中的 Vega）的“接线图”，它是通过调用 `c:parallax<->distance`（图中的 Vega-0）得到的。圆圈表示单元格，其他形状表示连接单元格的传播器。这些传播器不是方向性的——它们强制执行代数约束。按照惯例，我们将约束传播器构造函数的名前标记为 `c:`。例如，由 `c:*` 构建的传播器强制执行约束：单元格 t 的内容与单元格 `Vega-parallax-distance` 的内容的积等于单元格 `AU` 的内容。

约束传播器本身由方向性传播器组成，如图 7.4 所示。方向性传播器（例如由 `p:*` 构建的乘法器）会调整乘积单元格的值，使其与乘数和被数单元格的值保持一致。在传播器系统中混合方向性传播器和约束传播器是完全合适的¹。现在，让我们用这个小系统进行计算。弗里德希·G. W. von Struve 在 1837 年发表了关于织女星视差的估计值：0.125” ± 0.05²。这是第一个合理的恒星视差测量值，因为他的数据很稀疏，而且他后来又反驳了这一点——但第一次真实测量的功劳属于弗里德希·威廉·贝塞尔（Friedrich Wilhelm Bessel），他在 1838 年对六宿牛座 61 星的视差进行了仔细测量。然而，Struve 的估计值与目前织女星视差的最佳估计值非常接近。我们告诉传播系统 Struve 对织女星的估计值为 125 毫角或减 50 毫角：

![](img/2e72770736573f9ba6300dcdb1e28c1_382_0.png)

**图 7.4** 由 `c:*` 构建的约束传播器由三个方向性传播器组成。按照惯例，我们给方向性传播器加上 `p:`。由 `p:*` 构建的乘法传播器强制单元格 `c` 的值等于单元格 `a` 和 `b` 的值的积。由 `p:/` 构建的除法传播器强制其商单元格（a 和 b）的值为被除数单元格（c）的值除以除数单元格（b）的值的结果。

```
(tell! Vega-parallax (+->interval (mas->radians 125) (mas->radians 50)) 'FGWStruve1837)
```

过程 **tell!** 接受三个参数：一个传播器单元格、该单元格的值以及一个描述数据来源的假设。`mas->radians` 过程将毫角转换为弧度。`+->interval` 过程以其参数为中心创建一个区间：

```
(define (+->interval delta)
(make-interval (: delta) (+: delta)))
```

因此，`Vega-parallax` 单元格被赋予了区间：

```
(+->interval (mas->radians 125) (mas->radians 50)) (interval 3.6110068215196e-7 4.442394141688e-7)
```

Struve 对误差的估计是一个相当大的分数。他对比织女星距离的估计相当粗糙（5.7 到 13.3 或 9.5 ± 3.8）：

```
(get-value-in Vega-parallax-distance (interval 5.714285714329135 13.33333334721))
```

这个区间值由假设 `FGWStruve1837` 支持。

```
(get-premises Vega-parallax-distance)
(support-set fgwstruve1837)
```

我们使用 `inquire` 过程，它能很好地显示单元格的值以及对该值的支持：

```
(inquire Vega-parallax-distance)
((vega-parallax-distance)
(has-value interval 5.7143e0 1.3333e1)
(depends-on fgwstruve1837)
(because
(p/: c:parallax<->distance)
```
