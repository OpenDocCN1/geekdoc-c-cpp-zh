
因此，方程 (4.7) 和 (4.9) 变为如下形式

\mathbf{D_b} = \mathbf{A}^T \mathbf{D_a} \quad \text{以及} \quad \mathbf{H_b}^{\circ} = \mathbf{A}^T \mathbf{H_a}^{\circ} \mathbf{A} 。

接着，(4.10) 变为如下形式

\mathbf{A}^T \mathbf{D_a} + \mathbf{A}^T \mathbf{H_a}^{\circ} \mathbf{A} \mathbf{h_b} = \mathbf{0} . \qquad \qquad \qquad \qquad (4.40)

消去 \(\mathbf{A}^T\) 得到 \(\mathbf{h_a} = \mathbf{A}\mathbf{h_b}\)，也就是说，对于任意非奇异矩阵 \(\mathbf{A}\)，我们再次具有不变性。

Levenberg-Marquardt 校正（第 4.2 节）用 \((\mathbf{H}^{\circ} + \lambda\mathbf{I})\) 替换矩阵 \(\mathbf{H}^{\circ}\)，因此方程 (4.40) 变为

\mathbf{A}^T \mathbf{D_a} + (\mathbf{A}^T \mathbf{H_a}^{\circ} \mathbf{A} + \lambda \mathbf{I}) \mathbf{h_b} = \mathbf{0} 。

如果 \(\mathbf{A}\) 是一个正交矩阵，那么 \(\mathbf{I} = \mathbf{A}^T\mathbf{A}\)，我们再次得到 \(\mathbf{h_a} = \mathbf{A}\mathbf{h_b}\)，即所需的不变性成立。否则，不变性将失效。这并不令人惊讶，因为 Levenberg-Marquardt 是 Gauss-Newton 和梯度下降法的混合体，而后者仅对正交矩阵 A 具有不变性。

**圆拟合算法的不变性证明。** 基于我们的普遍分析，Levenberg-Marquardt 方法在正交变换（特别是平移和旋转）下总是具有不变性的。当我们拟合圆时，可以在 \(xy\)（数据）平面上平移或旋转坐标系；此时在具有坐标 \((a, b, R)\) 的三维参数空间中，我们在 \(ab\) 平面上平移或旋转坐标系，但保持 \(R\) 轴固定。因此，我们处理的是 \(\mathbb{R}^3\) 中坐标系的（特定）平移或旋转，正如我们上面所确立的那样，Levenberg-Marquardt 算法对此具有不变性。

Späth 算法和 Landau 算法在 \(xy\)（数据）平面坐标系的平移和旋转下也具有不变性。事实上，关于平移的不变性是显而易见的，因为这两种算法都要求将原点移动到数据集的质心。

要检查关于旋转的不变性，应当观察到，将坐标系旋转角度 \(\theta\) 会导致每个 \((u_i, v_i)\) 向量旋转 \(-\theta\)，参见 (4.20)–(4.21)；因此它们的平均向量 \((\tilde{u}, \tilde{v})\) 也将旋转 \(-\theta\)。现在从 (4.34) 和 (4.37) 中可以清楚地看出，向量 \((a, b)\) 将相应地旋转；我们邀请读者将此论证的细节作为练习进行验证。

## 4.12 已知角度差的情况

在第 4.8 节中，我们使用了角度坐标 \(\varphi_1, \dots, \varphi_n\)，并将目标函数写为

\mathscr{F} = \sum_{i=1}^n (x_i - a - R \cos \varphi_i)^2 + (y_i - b - R \sin \varphi_i)^2 \qquad \qquad \qquad \qquad (4.41)

其中 \(\varphi_{i}\) 被视为未知量，除了圆的参数 \((a, b, R)\) 之外。对 (4.41) 关于其所有变量进行最小化是 Späth 算法的主要思想。

**Berman 模型。** 在某些应用中，连续数据点之间的角度坐标差 \(\varphi_{i+1}-\varphi_{i}\) 是已知的。此信息可用于简化目标函数 (4.41)，随后模型变为完全线性，从而导出参数估计的显式公式。

事实上，如果我们用以下公式表示已知的差值

\tau_{i} = \varphi_{i} - \varphi_{1} = \sum_{j=1}^{i-1} (\varphi_{j+1} - \varphi_{j})

那么我们可以表示为 \(\varphi_{i} = \varphi + \tau_{i}\)，其中 \(\varphi = \varphi_{1}\) 是唯一的未知角度参数。现在，目标函数 (4.41) 变为如下形式

\mathcal{F} = \sum_{i=1}^{n} (x_{i} - a - \alpha \cos \tau_{i} + \beta \sin \tau_{i})^{2} \\
\quad + (y_{i} - b - \alpha \sin \tau_{i} - \beta \cos \tau_{i})^{2}, \quad (4.42)

其中

\alpha = R \cos \varphi \quad \text{以及} \quad \beta = R \sin \varphi \quad (4.43)

可以被视为临时替代 \(R\) 和 \(\varphi\) 的辅助参数。

由于 \(\mathcal{F}\) 是其未知数 \(a, b, \alpha, \beta\) 的二次函数，模型变为完全线性的。\(a, b, \alpha, \beta\) 的估计值可以通过令 \(\mathcal{F}\) 的偏导数为零并求解由此产生的包含 4 个未知数的 4 个方程的线性方程组来轻松找到。由于这些内容是初等的，我们将不提供细节。

最后，半径 \(R\)（以及基底角 \(\varphi\)，如果需要）可以从方程 (4.43) 中求出。无需复杂的迭代方案。该模型由 Berman [15] 在 1983 年提出并求解。

**Berman 模型的应用。** Berman [15] 指出了两个角度差确实已知的特定应用：

- 1. 微波工程中阻抗测量装置的校准；
- 2. 英国巨石遗址的分析，其中考古学家需要拟合圆圈到石环上。

许多不同的例子都具有这一重要特征，这很有趣。

Berman、Griffiths 和 Somlo [15, 19, 20] 对具有已知角度差的模型的结果参数估计进行了详细的统计分析。

**进一步扩展。** 最近，Yin 和 Wang [194] 将异方差错误纳入 Berman 模型；他们假设 \(x\) 和 \(y\) 方向上的扰动具有不同的（且未知的）方差。这种类型的数据也出现在微波工程中。

Wang 和 Lam [188] 将 Berman 模型扩展到同时拟合多个圆，其中检验多个圆形物体是否具有相同大小的假设。此类问题出现在制造机械零件的质量控制中。

似乎已知角度差的情况并不像看起来那样罕见，但它仍然是通用圆拟合问题的一个特例。

## 第 5 章
## 代数圆拟合

- 5.1 简单代数拟合（Kåsa 方法） ... 100
- 5.2 Kåsa 方法的优点 ... 101
- 5.3 Kåsa 方法的缺点 ... 104
- 5.4 Chernov-Ososkov 修正 ... 107
- 5.5 Pratt 圆拟合 ... 109
- 5.6 Pratt 拟合的实现 ... 111
- 5.7 Pratt 算法的优点 ... 114
- 5.8 实验测试 ... 117
- 5.9 Taubin 圆拟合 ... 121
- 5.10 Taubin 拟合的实现 ... 124
- 5.11 通用代数圆拟合 ... 127
- 5.12 一个真实数据示例 ... 130
- 5.13 迭代方案的初始化 ... 132

回顾一下，我们将解决圆拟合问题的所有实际方案分为两大组：(A) 几何拟合，它最小化数据点到圆的几何（正交）距离；以及 (B) 代数拟合，它最小化其他一些主要是代数的表达式，参见第 4 章的前言。这里我们处理 B 类方法。

为什么 B 类方法值得关注？

首先，几何拟合（即 A 类方法）是迭代的，它们需要在开始工作前提供初始猜测；其性能极大地依赖于初始猜测的准确性。代数拟合是非迭代的、经济实惠的过程，能够提供良好的初始猜测。

其次，某些应用以大规模数据处理为特征（例如，在高能物理中，来自加速器的数百万个圆形粒子轨迹需要被处理）。在这种条件下，人们很少能承受缓慢的迭代几何拟合，因此非迭代的代数拟合可能成为唯一的选择。

最后但同样重要的是，设计良好的代数拟合（如本章描述的 Taubin 和 Pratt 算法）在统计上似乎与几何拟合具有近乎相同的精度（这将在第 7 章的详细误差分析中得到证实）。在许多应用中，良好的代数拟合就能完成出色的工作，随后的几何拟合不会带来明显的改进。

## 5.1 简单代数拟合（Kåsa 方法）

解决圆拟合问题最简单且最显而易见的方法是最小化

\mathscr{F}_1(a, b, R) = \sum_{i=1}^{n} \left[ (x_i - a)^2 + (y_i - b)^2 - R^2 \right]^2. \quad \quad \quad \quad (5.1)

换句话说，我们正在最小化 \(\mathscr{F}_1 = \sum f_i^2\)，其中

f_i = (x_i - a)^2 + (y_i - b)^2 - R^2. \quad \quad \quad \quad (5.2)

显然，当且仅当点 \((x_i, y_i)\) 位于圆上时，\(f_i = 0\)；同样，当且仅当点位于圆附近时，\(f_i\) 很小。因此，最小化 (5.1) 听起来是一个合理的想法。一些作者 [62, 67, 150] 称 \(f_i\) 为点 \((x_i, y_i)\) 到圆 \((x - a)^2 + (y - b)^2 + R^2 = 0\) 的*代数距离*。

目标函数 (5.1) 的导数关于 \(a, b, R\) 是非线性的，但简单的参数变换使它们变为线性的。令

B = -2a, \quad \quad C = -2b, \quad \quad D = a^2 + b^2 - R^2. \quad \quad \quad \quad (5.3)

然后我们得到

\mathscr{F}_1 = \sum_{i=1}^{n} (z_i + Bx_i + Cy_i + D)^2 \quad \quad \quad \quad (5.4)

为了简洁，我们也记 \(z_i = x_i^2 + y_i^2\)。

现在，对 \(\mathscr{F}_1\) 关于 \(B, C, D\) 求导得到一组*线性*方程

\begin{array}{rrcl} \overline{x x}B + \overline{x y}C + \overline{x}D &=& -\overline{x z} \\ \overline{x y}B + \overline{y y}C + \overline{y}D &=& -\overline{y z} \\ \overline{x}B + \overline{y}C + D &=& -\overline{z}, \end{array} \quad \quad \quad \quad (5.5)

其中我们再次使用“样本均值”记号

\overline{x x} = \frac{1}{n} \sum x_i^2, \quad \quad \overline{x y} = \frac{1}{n} \sum x_i y_i, \quad \text{等等}

