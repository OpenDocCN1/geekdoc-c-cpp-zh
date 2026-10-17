
其中 $a_i$ 和 $p_i$ 分别表示构成余弦波的振幅和相位。因此，$c(t)$ 的频域表示为两幅图——振幅图显示 $a_i$ 随 $f_i$ 变化，相位图显示 $p_i$ 随 $f_i$ 变化。它们一起显示了频率为 $f_i$ 的每个波的振幅和相位。典型的 1D 频率响应图如图 1.8 所示。由于较高频率的波只产生尖锐特征，它们通常以非常小的振幅存在。因此，大多数振幅图，尤其是自然信号，在较高频率处衰减，如 1.8 所示。

![](img/66c45bbed85bb7ba7f7b05dff49b5060_26_1.png)

图 1.9. 左：2D 信号频域响应振幅部分的非正式表示。右：左侧相同图的灰度表示。

让我们现在尝试将这一概念直观地扩展到 2D 信号（例如灰度图像）。请注意，当考虑 2D 中的这些波时，它们不仅可以在频率 $f$ 上不同，还可以在方向 $o$ 上不同。即使频率相同，水平余弦波也与垂直余弦波完全不同。因此，2D 信号的频率响应导致 2D 图，其中振幅/相位是频率和方向的函数。然而，理解一个轴为频率、另一轴为方向的 2D 图对我们来说非常困难。一种更简单的绘图方法是使用极坐标 $g$ 和 $h$，使得坐标 $(g, h)$ 处的频率 $f$ 由长度 $\sqrt{g^2 + h^2}$ 给出，而方向由角度 $\tan^{-1} \frac{h}{g}$ 给出。这意味着 $(g, h)$ 中的一个圆将提供相同频率但不同方向的余弦波，而从原点发出的射线将提供相同方向但不同频率的余弦波。图 1.9 显示了一个示例 2D 振幅图。请注意，这里较高的频率也具有比较低频率更小的振幅，由图的径向递减值给出。或者，相同的图可以可视化为灰度图像，其中振幅归一化并作为介于黑色和白色之间的灰度值绘制（图 1.9）。

### 1.3.1 几何数据

几何实体（例如线、平面或曲面）可以进行解析表示。也可以使用离散表示。连续表示可以是隐式的、显式的或参数化的。

显式表示是指一个因变量表示为所有自变量和常数的函数。2D 直线的显式方程为

$$y = m x + c$$

其中 $m$ 和 $c$ 分别为直线的斜率和 y 截距。类似地，2D 二次曲线的显式表示可以为

$$y = a x^2 + b x + c$$

其中 $a$、$b$ 和 $c$ 是表示曲线的二次函数的系数。物理和信号处理中出现的另一个流行的显式函数是

$$y = A \sin(\omega t + \phi).$$

这表示振幅为 $A$、频率为 $\omega$、相位为 $\phi$ 的正弦波。请注意，显式表示允许在自变量的不同值处轻松求值函数。

然而，更复杂的函数有时不便于使用显式形式表示。隐式表示认为点 $\mathbf{p}$ 在满足方程 $F(\mathbf{p}) = c$ 时是有意义的，其中 $c$ 是常数。2D 直线的隐式方程为

$$a x + b y + c = 0,$$

![](img/66c45bbed85bb7ba7f7b05dff49b5060_28_0.png)

### 顶点

`V₁` `(x₁, y₁, z₁)`

`V₂` `(x₂, y₂, z₂)`

●

●

●

`V₈` `(x₈, y₈, z₈)`

### 三角形

`V₁, V₂, V₄; V₁, V₄, V₃; V₃, V₄, V₇;`

`V₄, V₈, V₇; V₄, V₂, V₈; V₂, V₆, V₈;`

`V₁, V₅, V₂; V₂, V₅, V₆; V₃, V₅, V₁;`

`V₃, V₇, V₅; V₅, V₇, V₆; V₆, V₇, V₈`

图 1.10. 该图显示了立方体 3D 网格的表示。它由顶点列表后跟三角形列表组成。每个三角形由构成它的顶点的索引描述。

而 3D 平面的方程为

`ax + by + cz + d = 0.`

类似地，2D 圆的隐式方程为

$$(x − a)² + (y − b)² = r²$$

其中 $(a, b)$ 是圆心，$r$ 是圆的半径。3D 球体的隐式方程为

$$(x − a)² + (y − b)² + (z − c)² = r²$$

其中 $(a, b, c)$ 是球心，$r$ 是球的半径。在显式函数中，有时需要交换因变量和自变量以表示特殊情况。例如，使用显式方程 `y = mx + c` 不可能表示垂直线，因为 `m = ∞`。因此我们需要将 `x` 更改为因变量以表示这条垂直线 `x = m′y + c′`，其中 `m′ = 0`。另一方面，隐式函数表示中没有特殊情况。隐式表示的优点是易于进行内部或外部测试。如果 `F(p) < 0`，则该点在表面‘上方’或‘外部’，如果 `F(p) > 0`，则该点在表面‘下方’或‘内部’。

最后，参数方程允许使用一个或多个参数表示函数。例如，线段上的点 `p = L(t)`

![](img/66c45bbed85bb7ba7f7b05dff49b5060_29_0.png)

流形  

带边界的流形  

非流形

**图 1.11.** 本图说明了流形（封闭物体）、带边界的流形（带孔的物体）和非流形（带折痕和褶皱的物体）。

两点 `P` 和 `Q` 之间的线段可以用参数形式表示为

```
L(t) = P + t(Q - P)
```

其中参数为 `t` 且 `0 ≤ t ≤ 1`。类似地，由 `P`、`Q` 和 `R` 形成的三角形内部一点的参数方程由双参数方程给出

```
p = P + u(Q - P) + v(R - P)
```

其中参数为 `u` 和 `v` 满足 `0 ≤ u, v ≤ 1` 且 `u + v ≤ 1`。参数方程允许轻松采样参数空间并在这些不同采样值上求值任意函数。

在离散表示中，几何实体被表示为其他几何实体的集合，而不是解析方程。例如，2D 正方形可以由嵌入 2D 空间的一组线段定义；3D 立方体可以由嵌入 3D 空间的一组四边形或三角形定义。这种表示称为网格。例如，当使用三角形定义 3D 物体时，我们称之为三角网格。构成网格的实体（例如线段、三角形或四边形）称为基元。

尽管有许多不同的 3D 几何表示方法，但最常见的是三角网格。因此，我们在此讨论三角网格表示的一些关键要素。其他几何表示的更多细节及其用途将在后续章节中介绍。三角网格由一组顶点和由这些顶点连接形成的一组三角形定义。因此表示包含两个部分：（a）由其 3D 坐标表示的顶点列表；以及（b）由其角顶点的顶点索引定义的三角形列表。图 1.10 显示了简单 3D 物体立方体的网格表示示例。顶点的坐标定义了网格的*几何*。换句话说，改变这些坐标会改变物体的几何形状。例如，如果我们想将立方体变为长方体或更大的立方体，顶点的 3D 坐标将被改变。然而请注意，这不会改变三角形列表，因为构成三角形的顶点的连接性不会改变。因此后者被称为网格的*拓扑*属性。拓扑指的是在数据几何属性发生变化时保持不变的连接性。

接下来，我们将定义网格的某些几何和拓扑属性，但不是以严格的方式。我们将给出直观和非正式的定义。闭合网格（非正式地定义为没有孔）具有在计算机图形学操作如变形、网格简化与编辑方面的若干优良特性。此类网格是流形，其中每条边恰好有两个相邻三角形。每条边具有一个或两个相邻三角形的网格称为带边界的流形。例如，由两个三角形表示的一张纸，其构成纸张四边的四条边仅有一个相邻三角形，这就是带边界的流形。请注意，带边界的流形比流形限制更少，因而是流形的超集。边可以有超过两个相邻三角形的网格称为非流形。请注意，非流形是带边界流形的超集。图 1.11 说明了这一点。

网格可以定义几何属性或属性。在图 1.10 中每个顶点都有 3D 空间坐标。除了此基本信息外，每个顶点可以具有 RGB 颜色、法向量、或用于贴到网格上的图像的 2D 坐标（正式称为纹理坐标），或对给定应用有用的任何其他基于顶点的属性。拓扑属性是在几何属性改变时不发生变化的属性。对于网格处理，少数拓扑属性非常重要。第一个是*欧拉示性数*定义为 `V − E + F`，其中 `V` 是顶点数，`E` 是边数，`F` 是网格的面数（不一定是三角形）。请注意，如果你通过改变顶点位置将立方体改为平行六面体，这是一个几何属性，`E` 不会改变。

本质上，`E` 只有在物体经历网格连接性变化时才会改变。网格的亏格定义为柄的数量。例如，球面亏格为零，甜甜圈亏格为 1，双甜甜圈亏格为 2。要从一个亏格变为另一个亏格，需要改变网格的拓扑，而仅几何变化就足以将一个物体变为同一亏格的另一个物体（图 1.12）。

![](img/66c45bbed85bb7ba7f7b05dff49b5060_30_0.png)

**图 1.12.** 左图：这显示了亏格 1 的甜甜圈如何仅通过改变几何形状就变为亏格 1 的杯子。右图：莫比乌斯带的示意图。

最后，如果你从网格顶部开始行走并最终到达其背面，则网格不可定向。不可定向网格的例子是莫比乌斯带（图 1.12）。

### 有趣的事实

![](img/66c45bbed85bb7ba7f7b05dff49b5060_31_0.png)

对拓扑学家来说引人入胜的不可定向曲面是克莱因瓶。与莫比乌斯带不同，它没有任何边界。它是将两个莫比乌斯带放在一起得到的。克莱因瓶最早由德国数学家费利克斯·克莱因于 1882 年描述。它不能嵌入 3D 空间，只能嵌入 4D 空间。

克莱因瓶会容纳自身，在嵌入 4D 空间时会包含自身！这并没有阻止人们尝试将其嵌入 3D 空间，而且伦敦科学博物馆展出了一些精美制作的 3D 模型！

到目前为止，我们只考虑了网格的三角形基元。虽然可以使用其他基元（例如，用六个四边形代替 12 个三角形来表示立方体的网格），但三角形因多种原因而被偏好。首先，三角形总是平面的，因为三个非共线点定义一个平面。因此建模软件包在输出网格表示时无需确保曲面符合顶点。其次，正如我们在下一章将看到的，在计算机图形学中，重要的是通过称为插值的技术，从基元的顶点属性推断出位于基元内部点的属性，而在这种情况下三角形基元具有很大优势。

## 1.4 噪声

任何关于数据的讨论都不能不讨论噪声。噪声可能由多种因素引起，如机械不精确、传感器不精确（例如偶尔总是死掉或总是活着的像素）等等。不同系统的噪声来源不同。它最好被描述为在数据的随机位置添加随机值。在本章中我们将讨论一些常见的噪声类型。

![](img/66c45bbed85bb7ba7f7b05dff49b5060_32_0.png)

**图 1.13.** 本图说明了 1D 音频数据（左）、2D 图像数据（中）和 3D 曲面数据（右）中的随机噪声。在每个示例中，左侧显示干净数据，右侧显示对应的噪声数据。

最常见和最一般的噪声是我们称之为随机噪声，即在数据的任何位置添加小的随机值。图 1.13 显示了一些示例。减少数据中此类噪声的常用技术是我们称之为低通滤波，它将在第 3 章中详细讨论。

![](img/66c45bbed85bb7ba7f7b05dff49b5060_32_1.png)

另一种常见的噪声类型源于数据中存在异常值，即明显不属于数据样本。例如，在相机中某些传感器像素可能已损坏，从而阻挡或允许所有光线，提供始终为黑色或始终为白色的像素。此类像素的位置可能是随机的。在 2D 图像的特定情况下，这种噪声称为椒盐噪声（见图 1.14）。此类异常值可通过中值滤波器或其他顺序统计滤波器得到充分处理。我们将在第 5 章看到其中的一些。

**图 1.14.** 这显示了 1D（左）、2D（中）和 3D（右）数据中的异常值或椒盐噪声。左侧，我们展示了中值滤波器去除红色异常值的效果。

最后，一些噪声在空间域看起来是随机的，但在频谱域可被隔离到少数几个频率。这种噪声的一个例子如图 1.15 所示。此类噪声可通过在频域应用称为陷波滤波器的滤波器来去除，我们将在第 4 章中详细讨论。

## 1.5 结论

在本章中，我们讨论了表示和可视化不同类型视觉数据如图像、3D 曲面和点云的基础。我们还了解了数据在时空域和频域的两种替代表示。我们谈到了数据中噪声的实际问题。

![](img/66c45bbed85bb7ba7f7b05dff49b5060_33_0.png)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_33_1.png)

Figure 1.15. 该图显示了可通过陷波滤波器去除或降低的频域噪声。

以及如何根据具体情况进行处理。以下是一些关于熟悉某些高级概念的参考资料。 [Ware 04] 详细探讨了信息可视化的所有内容。 [Goldstein 10] 为与感觉和人类感知相关的主题提供了极佳的入门阅读。 [Ferguson 01] 中关于 3D 图形数据结构的章节提供了 3D 模型表示的详细描述。 [Gonzalez and Woods 06] 中关于噪声的章节提供了值得阅读的关于噪声的非常详细的论述。

## Bibliography

[Ferguson 01] R. Stuart Ferguson. Practical Algorithms for 3D Computer Graphics. A. K. Peters, 2001.

[Goldstein 10] Bruce E. Goldstein. Sensation and Perception. Thomas Wadsworth, 2010.

[Gonzalez and Woods 06] Rafael C. Gonzalez and Richard E. Woods. Digital Image Processing (3rd Edition). Prentice-Hall, Inc., 2006.

[Ware 04] Colin Ware. Information Visualization: Perception for Design. Morgan Kaufmann Publishers Inc., 2004.

## Summary: Do you know these concepts?

- Height Field

- Discretization

- Sampling and Nyquist Sampling Theorem

- Decomposition and Reconstruction

- Aliasing

- Quantization

- Time and frequency domain representation

- Mesh - Geometry and Topology

- Manifold, manifold with boundaries and non-manifolds

- Euler characteristics, genus, orientability

- Random Noise

- Salt and Pepper Noise

## Exercises

- 1. Consider an 8-bit grayscale image `I(x, y)` whose size is 256 × 256. Each column of the image has the same gray value which starts from 0 for the left most column and increases by 1 as we sweep from left to right. What kind of shape does the height field of this image form? Find its equation?

- 2. Consider a height field `H(x, y)` of size 256 × 256 given by the function `H(x, y) = (x mod 16) * 16`. What kind of shape would this height field have? How many gray levels would this image have? Create a table to show the percentage of pixels that belong to each of these gray levels.

- 3. Consider a gray scale spatial function `A(x, y)` which does not vary in the y-direction but form a sine wave as we go from left to right in x-direction making 50 cycles. What will be the minimum horizontal resolution of an digital image that can sample this function adequately? Consider another function `B(x, y)` formed by rotating `A` about the axis perpendicular to the plane formed by `x` and `y`. Now consider the function formed by adding `A` and `B`. What is the minimum horizontal and vertical resolution of the image required to sample `A + B` adequately?

- 4. Consider an object moving at 60 units per second. How many frames per second video is required to adequately capture this motion? What kind of artifact would you expect if the frame rate is lesser than this desired rate? What is this artifact more commonly known as?

- 5. The image of your TV looks washed out. The technician says that the intensity response curve of the TV is linear and hence the problem. To correct the problem, he has to make it non-linear. Why? What kind of non-linear response do you think he will put in?
