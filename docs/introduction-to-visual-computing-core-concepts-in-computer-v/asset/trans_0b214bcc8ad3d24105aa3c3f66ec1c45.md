

![](img/66c45bbed85bb7ba7f7b05dff49b5060_165_0.png)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_165_1.png)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_165_2.png)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_165_3.png)

图 6.14。左边的两幅图像显示了使直线变为曲线的非线性镜头畸变。右边的两幅图像显示了颜色管理过程中立方体 3D 色域（左）到非线性变换（右）的过程。

完全独立。因此，该矩阵的自由度为三个，尽管可以改变的矩阵项数为六个。

然而，自由度不能大于受变换影响的矩阵元素的数量。让我们考虑用 3 × 3 矩阵表示的 2D 仿射变换。由于仿射变换允许缩放和剪切，似乎除了刚体变换的三个参数外，我们还可以控制额外的四个参数（缩放和剪切各 2 个）。因此，该变换具有 7 个自由度。然而，由于只有矩阵的六个条目受到影响，因此它具有 6 个自由度。深入分析后，你可以看到旋转可以表示为缩放和剪切的组合。例如，x 坐标将被变换为 ax + by，其中 a 被认为是缩放因子，b 是剪切因子。但它们将类似于旋转角度的余弦和正弦。因此，旋转自由度被缩放和剪切参数所吸收，从而使变换仅具有六个自由度。

从矩阵计算的角度来看，对矩阵施加的任何约束都会降低其自由度。因此，例如，如果你有一个 7 阶矩阵，并带有特殊约束，即矩阵是秩亏的（即矩阵的行列式为 0），每个秩的不足都会导致自由度减少一个。随着我们进入下一章关于几何视觉计算的内容，我们将在多个场合讨论自由度，以提供更全面的理解。

## 6.9 非线性变换

如果没有讨论非线性变换，本章的讨论是不完整的。任何改变曲线次数的变换（例如直线变为曲线）称为非线性变换。相机镜头引起的畸变是非线性畸变的一个很好的例子。这是

由相机镜头在 3D 到 2D 的透视变换后引入的畸变。这种畸变如图 6.14 所示，针对棋盘图案和建筑工地。

非线性变换不能像矩阵乘法那样简单地实现。通常，物体上的点应被采样；每个点都应被变换，然后通过曲面拟合找到另一个曲面以找到变换后的物体。此类变换在建模、曲面设计、颜色管理和仿真等应用中很常见。在本书中，我们将主要关注线性变换。

## 有趣的事实

单词 geometry 来自希腊语 geo，意为地球，和 metria，意为测量。几何学是前现代数学的两个领域之一，另一个是数字研究（算术）。几何学的最早记录可以追溯到早期的人们，他们在大约公元前 3000 年的古代印度河谷文明（现在印度和巴基斯坦）和古代巴比伦（现在伊朗）发现了钝角三角形。古埃及人早在公元前 3000 年就使用几何原理，使用方程来近似圆的面积等公式。巴比伦人可能知道测量面积和体积的一般规则。他们将圆的周长测量为直径的三倍，面积测量为周长的平方的十二分之一，这在 π 估计为 3 时是正确的。希腊哲学家和数学家毕达哥拉斯生活在公元前 500 年左右，以其关于直角三角形的三条边的毕达哥拉斯定理而闻名：a² + b² = c²。叙拉古的阿基米德生活在公元前 250 年左右，在几何学史上发挥了重要作用，包括确定不规则形状物体体积的方法。

当欧洲开始从黑暗时代走出来时，在伊斯兰图书馆中发现的希腊化和伊斯兰几何学文本被从阿拉伯语翻译成拉丁语。欧几里得《几何原本》中发现的几何学的严格演绎方法被重新学习，并且在欧几里得（欧几里得几何）和凯伊亚姆（代数几何）的风格下，几何学的进一步发展由勒内·笛卡尔（1596 - 1650）和皮埃尔·德·费马（1601 - 1665）在解析几何中以及吉拉尔·德萨格（1591 - 1661）在射影几何中继续。

## 6.10 结论

在本章中，我们介绍了构成计算机视觉和图形学基础的几何变换。矩阵为我们在这些领域处理困难的几何问题提供了一个正式的框架。可以在像 [Faugeras 93] 这样的计算机视觉书籍或像 [Hughes et al. 13, Shirley and Marschner 09] 这样的计算机图形学书籍中探索这些方向的高级概念。

## 参考文献

[Faugeras 93] Olivier Faugeras. *Three-dimensional Computer Vision: A Geometric Viewpoint*. MIT Press, 1993.

[Hughes et al. 13] John F. Hughes, Andries van Dam, Morgan McGuire, David F. Sklar, James D. Foley, Steven K. Feiner, and Kurt Akeley. *Computer Graphics: Principles and Practice (3rd ed.)*. Addison-Wesley Professional, 2013.

[Shirley and Marschner 09] Peter Shirley and Steve Marschner. *Fundamentals of Computer Graphics, Third edition*. A. K. Peters, Ltd., 2009.

## 总结：你知道这些概念吗？

- Homogeneous Coordinates
- Linear Transformations
- Euclidean Transformations
- Rigid Body Transformations
- Affine Transformations
- Projective Transformations
- Degrees of Freedom
- Concatenation of Transformations
- Coordinate Systems
- Changing Coordinate Systems
- Creating Coordinate Systems
- Global vs Local Coordinate Systems
- Non-Linear Transformation

## 练习

1. 考虑以下矩阵 [ 注：1/2 = 0.707]。

$$
\begin{pmatrix} 0.707 & 0 & 0.707 & 0 \\ 0 & 2 & 0 & 0 \\ -0.707 & 0 & 0.707 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}
$$ (6.58)

该矩阵实现了什么变换？在局部坐标系中该变换的顺序是什么？

2. 考虑下图。给出一个矩阵，或矩阵的乘积，将正方形 ABCD 变换为正方形 ABCD。展示如果将相同的变换应用于正方形 ABCD 会发生什么。

![](img/66c45bbed85bb7ba7f7b05dff49b5060_169_0.png)

3. 考虑一个 2D 矩形 ABCD，其中 A = (0,0)，B = (2,0)，C = (2,1) 和 D = (0,1)。我们想对这个矩形应用一个 2D 变换，使其成为平行四边形 ABEF，其中 E = (4,1) 和 F = (2,1)。 a. 这是什么样的变换？实现该变换的 3x3 矩阵 M 是什么？ c. 我们需要对 ABEF 应用什么额外的变换 N 才能得到平行四边形 A'B'E'F'，其中 A' = (1,2)，B' = (3,2)，E' = (5,3)，和 F' = (3,3)？ d. 用 M 和 N 表示的最终连接矩阵是什么，它将 ABCD 变换为 A'B'E'F'？

4. 推导沿由向量 u = (1,2,1) 给出的任意方向以缩放因子 3 缩放物体的缩放矩阵，该向量以 (5,5,5) 为根。

5. 解释当应用于 4x1 齐次坐标时，以下每个矩阵产生的变换是什么。

$$
\begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 1 & 0 \end{pmatrix} \quad
\begin{pmatrix} 1 & 0 & p & -p(1+r) \\ 0 & 1 & q & -q(1+r) \\ 0 & 0 & 1+r & -r(1+r) \\ 0 & 0 & 1 & -r \end{pmatrix}
$$ (6.59)

6. 考虑 3 × 3 变换

T = \begin{pmatrix} 2a & a & a \\ a & a & 0 \\ 2a & a & a \end{pmatrix} \quad (6.60)

这是一个欧几里得、仿射还是透视变换？证明或证明你的答案。

![](img/66c45bbed85bb7ba7f7b05dff49b5060_170_0.png)

7. 考虑上面的房子。假设 Z 轴从页面中出来，假设页面为 XY 平面。在局部坐标系中执行以下变换后绘制房子：T(1,0,0), R_z(90), T(0,2,0)。

![](img/66c45bbed85bb7ba7f7b05dff49b5060_170_1.png)

8. 在上面的 2D 空间中，考虑点 P 和三个不同的坐标轴 A、B 和 C。点 P 在坐标系

