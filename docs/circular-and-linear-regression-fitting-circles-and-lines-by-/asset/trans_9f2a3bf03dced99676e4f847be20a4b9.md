
该式由 (3.7) 中构造得出。对 $a$ 和 $b$ 求导可得：

$$\mathbf{J}=\left[\begin{array}{cc}-u_{1}+\bar{u} & -v_{1}+\bar{v} \\ \vdots & \vdots \\ -u_{n}+\bar{u} & -v_{n}+\bar{v}\end{array}\right],$$

其中我们使用样本均值符号 $\bar{u}=\frac{1}{n} \sum u_{i}$ 等。由此得到：

$$\mathbf{N}=n\left[\begin{array}{cc}\overline{u u}-\bar{u}^{2} & \overline{u v}-\bar{u} \bar{v} \\ \overline{u v}-\bar{u} \bar{v} & \overline{v v}-\bar{v}^{2}\end{array}\right].$$

我们还得到：

$$\mathbf{J}^{T} \mathbf{g}=n\left[\begin{array}{cc}-\overline{u r}+\bar{u} \bar{r} & \\ -\overline{v r}+\bar{v} \bar{r}\end{array}\right]=n\left[\begin{array}{cc}a-\bar{x}+\bar{u} \bar{r} & \\ b-\bar{y}+\bar{v} \bar{r}\end{array}\right].$$

可以很容易地识别出这些矩阵的元素为相应变量的样本协方差。

![](img/86db288e3c266985d1648282179ae4b5_114_0.png)

**图 4.2** Levenberg-Marquardt 圆拟合的两种版本，初始猜测为 $(1, 1)$：完整版本（带星号标记的实线）和简化版本（带菱形标记的虚线）在 7 步内收敛到相同的极限；这里 20 个模拟点由叉号标记。

**数值测试。** 这种简化版本的 Levenberg-Marquardt 圆拟合比上一节中介绍的完整版本略微简单且速度更快。图 4.2 展示了一个典型示例，其中在单位圆 $x^{2}+y^{2}=1$ 的 $130^{\circ}$ 圆弧上随机生成了 20 个点，噪声水平为高斯噪声 $\sigma=0.05$，且 Levenberg-Marquardt 拟合的两个版本均从 $a=b=1$ 开始。它们都在 7 次迭代内收敛到 $\mathscr{F}$ 的（唯一）最小值点 $\hat{a}=-0.057$ 和 $\hat{b}=0.041$，但通往极限的路径略有不同。

在 [43] 报告的计算机实验过程中进行的数值测试表明，虽然这两个版本在典型情况下表现几乎相同，但在不利情况下，简化版本显得略微较差：如果提供给它的初始猜测值不佳，它不幸地倾向于在平台中途停滞。

## 4.7 Levenberg-Marquardt 圆拟合的改进

计算 (4.8) 中的海森矩阵 **H** 的精确值也有吸引力，即不丢弃其中的第二项求和，从而可能提高收敛性。本节探讨这一方法。

展开 (4.23) 中的平方项得到：

$$\mathscr{F}(a,b) = \sum_{i=1}^{n} r_i^2 - n\bar{r}^2 = \sum_{i=1}^{n} (x_i^2 + y_i^2) + n(a^2 + b^2 - \bar{r}^2). \quad (4.24)$$

为了使公式更简洁，我们假设数据已中心化，即 $\bar{x} = \bar{y} = 0$（一些作者声称 [53, 176]，在拟合前对数据进行中心化有助于减少舍入误差）。

由于 (4.24) 中的第一个求和项与参数无关，我们可以忽略它，同时也忽略第二项中的常数因子 *n*，因此我们得出最小化一个新函数的问题：

$$\mathscr{F}_1(a,b) = a^2 + b^2 - \bar{r}^2. \quad (4.25)$$

对 *a* 和 *b* 求导可得：

$$\frac{1}{2}\nabla\mathscr{F}_1 = \begin{bmatrix} a + \bar{u}\bar{r} \\ b + \bar{v}\bar{r} \end{bmatrix}. \quad (4.26)$$

二阶偏导数为：

$$\begin{aligned} \frac{1}{2} \frac{\partial^2 \mathscr{F}_1}{\partial a^2} \quad & = \quad 1 - \bar{u}^2 + \bar{r} \frac{\partial \bar{u}}{\partial a} \\ \frac{1}{2} \frac{\partial^2 \mathscr{F}_1}{\partial b^2} \quad & = \quad 1 - \bar{v}^2 + \bar{r} \frac{\partial \bar{v}}{\partial b} \\ \frac{1}{2} \frac{\partial^2 \mathscr{F}_1}{\partial a \partial b} \quad & = \quad -\bar{u}\bar{v} + \bar{r} \frac{\partial \bar{u}}{\partial b}. \end{aligned} \quad (4.27)$$

再次使用样本均值符号，我们有：

$$\begin{align*} -\frac{\partial \bar{u}}{\partial a} & = \frac{1}{n}\sum \frac{v_i^2}{r_i} = \overline{vv}/r \\ -\frac{\partial \bar{v}}{\partial b} & = \frac{1}{n}\sum \frac{u_i^2}{r_i} = \overline{uu}/r \end{align*}$$

以及

$\frac{\partial \bar{u}}{\partial b} = \frac{1}{n} \sum \frac{u_i v_i}{r_i} = \overline{uv/r}.$

因此，

$\mathbf{N} = \frac{1}{2} \mathbf{H} = \begin{bmatrix} 1 - \bar{u}^2 - \overline{rv/r} & -\bar{u\bar{v}} + \overline{rv/r} \\ -\bar{u\bar{v}} + \overline{rv/r} & 1 - \bar{v}^2 - \overline{ru/r} \end{bmatrix}.$

(4.28)

然后将矩阵 $\mathbf{N}$ 扩展为 $\mathbf{N}_\lambda$ 并求解方程组：

$\mathbf{N}_\lambda \mathbf{h} = -\frac{1}{2} \nabla \mathcal{F}_1.$

我们注意到，在这里，与经典的高斯-牛顿算法不同，矩阵 $\mathbf{N}$ 不一定是半正定的；因此，对于小的 $\lambda > 0$，$\mathbf{N}_\lambda$ 不一定是正定的。但对于足够大的 $\lambda$，由 (4.15) 计算出的扩展矩阵 $\mathbf{N}_\lambda$ 将是正定的。

**实用说明。** 这种 Levenberg-Marquardt 圆拟合版本比前两种版本更复杂且开销更大：计算 $\overline{uv/r}$、$\overline{rv/r}$ 和 $\overline{uv/r}$ 这些项会有额外的计算成本。

该算法的性能也在 [43] 报告的计算机实验过程中进行了测试。发现其收敛所需的迭代次数少于完整或简化的 Levenberg-Marquardt 拟合，但鉴于每次迭代的成本更高，总体改进令人存疑。另一方面，如果该算法发散（沿着前一章描述的“逃逸谷”），则与 Levenberg-Marquardt 圆拟合的完整版本相比，其移动速度非常缓慢。因此，上述提出的改进方案似乎不具备实用性。

**进一步改进。** 然而，这导致了另一个非常有趣的简化方案。回想经典的高斯-牛顿方法在计算海森矩阵时会抑制单个项 $g_i(\mathbf{a})$ 的二阶偏导数，参见 (4.8) 和 (4.9)。本着这种精神，让我们在计算海森矩阵 (4.27) 时忽略二阶偏导数 $\partial^2 \bar{r} / \partial a^2$、$\partial^2 \bar{r} / \partial b^2$ 和 $\partial^2 \bar{r} / \partial a \, \partial b$。这消除了 (4.27) 中三个公式中每式的最后一项，此时矩阵 $\mathbf{N}$ 简化为：

$\mathbf{N}_0 = \begin{bmatrix} 1 - \bar{u}^2 & -\bar{u\bar{v}} \\ -\bar{u\bar{v}} & 1 - \bar{v}^2 \end{bmatrix}.$

(4.29)

好消息是，矩阵 $\mathbf{N}_0$ 与 (4.28) 中的 $\mathbf{N}$ 不同，总是半正定的。确实，利用琴森不等式（Jensen's inequality）可得：

$\begin{aligned} \det \mathbf{N}_0 &= 1 - \bar{u}^2 - \bar{v}^2 \\ &\ge 1 - \overline{uu} - \overline{vv} = 0. \end{aligned}$

事实上，除非数据点共线，矩阵 $\mathbf{N}_0$ 都是正定的。

现在，让我们通过设置 $\lambda = 0$ 来进一步简化问题，即从现代 Levenberg-Marquardt 方法回到传统的高斯-牛顿方法。那么向量 $\mathbf{h} = (h_1, h_2)^T$ 将是以下方程的解：

$\mathbf{N}_0 \mathbf{h} = -\frac{1}{2} \nabla \mathscr{F}_1.$

用坐标形式表示，该方程为：

$\begin{bmatrix} 1 - \bar{u}^2 & -\bar{u}\bar{v} \\ -\bar{u}\bar{v} & 1 - \bar{v}^2 \end{bmatrix} \begin{bmatrix} h_1 \\ h_2 \end{bmatrix} = \begin{bmatrix} -a - \bar{u}\bar{r} \\ -b - \bar{v}\bar{r} \end{bmatrix}.$

求解该方程组并计算下一次迭代：

$(a_{\text{new}}, b_{\text{new}}) = (a, b) + (h_1, h_2)$

得到：

$a_{\text{new}} = -\bar{u}R, \quad b_{\text{new}} = -\bar{v}R \quad (4.30)$

其中我们使用以下符号：

$R = \frac{a\bar{u} + b\bar{v} + \bar{r}}{1 - \bar{u}^2 - \bar{v}^2} \quad (4.31)$

（将该分数记为 $R$ 有很好的理由，我们将在下一节揭示）。因此，我们得到了一个简单的迭代过程 (4.30)-(4.31)。

由于缺少 Levenberg-Marquardt 修正的高斯-牛顿方案不保证收敛，该算法看起来前景不明。奇迹般地，如上所述的方法结果非常稳健，我们将在下一节中看到。

## 4.8 圆拟合的 Späth 算法

Späth 于 1996 年提出了一种原始的圆拟合方法，参见 [170, 171]。首先，他扩大了参数空间。

**潜参数的使用**。对于每个 $i$，他用 $(\hat{x}_i, \hat{y}_i)$ 表示圆上距离数据点 $(x_i, y_i)$ 最近的点。点 $(\hat{x}_i, \hat{y}_i)$ 可以被视为圆上“真实”点的最佳估计，其带噪声的观测值为 $(x_i, y_i)$。点 $(\hat{x}_i, \hat{y}_i)$ 有时被称为数据校正 [95]。每个点 $(\hat{x}_i, \hat{y}_i)$ 可以由一个角度参数 $\varphi_i$ 指定，使得：

$\hat{x}_i = a + R \cos \varphi_i, \qquad \hat{y}_i = b + R \sin \varphi_i$

除了描述圆的三个参数 $a, b, R$ 之外，Späth 建议估计 $n$ 个角度参数 $\varphi_1, \ldots, \varphi_n$ 以指定数据校正

