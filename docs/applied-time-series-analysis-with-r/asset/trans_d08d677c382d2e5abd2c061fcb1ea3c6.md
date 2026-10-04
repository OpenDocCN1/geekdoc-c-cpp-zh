

g(x) = \sum_{k=-\infty} s_{j,k}\phi_{j,k}(x) + \sum_{j=-\infty} \sum_{k=-\infty} d_{j,k}\psi_{j,k}(x), \quad (12.17)

其中 $\phi_{j,k}$ 是父小波或尺度函数 $\varphi(x)$ 的伸缩和平移，对应于母小波 $\psi(x)$。尺度函数（父小波）具有性质

\int \varphi(x)dx = 1, \quad (12.18)

并且它们的伸缩和平移定义与方程 12.9 类似，即

\varphi_{j,k}(x) = 2^{-j/2}\varphi(2^{-j}x-k), \quad (12.19)

对于整数 $j$ 和 $k$。因此，对于所有整数 $j$ 和 $k$，有

\int \varphi_{j,k}(x)dx = 1. \quad (12.20)

作为示例，Haar 小波为

\varphi(x) = 1, \quad x \in[0, 1] = 0, otherwise.

图 12.6 右侧显示了与左侧面板所示的每个母小波对应的父小波。随着 $k$ 变大，父小波变得更平滑且支撑变宽。

需要注意的是，小波（母小波和父小波）通常没有解析形式。它们通常使用伸缩方程计算。参见 Daubechies (1992)、Bruce 和 Gao (1996) 以及 Strang 和 Nguyen (1997)。方程 12.17 写为

g(x) = S_j(x) + \sum_{j=-\infty} D_j(x), \quad (12.21)

其中 $S_j(x)=\sum_{k=-\infty}^{\infty} s_{j,k}\varphi_j(x)$ 且 $D_j(x)=\sum_{k=-\infty}^{\infty} d_{j,k}\psi_j(x)$。方程 12.21 中的第一项给出 $g(x)$ 到水平 $j$ 的“平滑”近似（即涉及较大的 $j$ 值）。$s_{jk}$ 被称为平滑系数。正如我们之前讨论的，$d_{j,k}$ 是细节系数，较小的 $j$ 值对应于更精细的细节。

## 12.3.4 有限长度数据集的离散小波变换

为了表述清晰，迄今为止关于小波的讨论涉及连续体上的数据。然而，对于分析有限长度的离散数据，$\mathbf{x}=(x_1, x_2,...,x_n)$（例如来自离散时间序列的实现），我们将使用离散小波变换（DWT）。给定一个正交小波基集，DWT 将向量 $\mathbf{x}=(x_1, x_2,...,x_n)$ 映射到 $n$ 个小波系数的向量。令 $\mathbf{w}$ 表示小波系数的向量，则可以证明

$$\mathbf{w} = \mathbf{Mx}, \quad (12.22)$$

其中 $\mathbf{M}$ 是一个正交矩阵，可以写成

$$\mathbf{M}=\begin{pmatrix} \mathbf{M}_1 \ \mathbf{M}_2 \ \vdots \ \mathbf{M}_{j_0} \ \mathbf{V}_{j_0} \end{pmatrix} \quad (12.23)$$

其中

$$\mathbf{M}_1=\begin{pmatrix} \tilde{\Psi}_{1,1}(1) & \tilde{\Psi}_{1,1}(2) & \dots & \tilde{\Psi}_{1,1}(n) \ \tilde{\Psi}_{1,2}(1) & \tilde{\Psi}_{1,2}(2) & \dots & \tilde{\Psi}_{1,2}(n) \ \vdots & \vdots & \ddots & \vdots \ \tilde{\Psi}_{1,n/2}(1) & \tilde{\Psi}_{1,n/2}(2) & \dots & \tilde{\Psi}_{1,n/2}(n) \end{pmatrix}, \ \mathbf{M}_2=\begin{pmatrix} \tilde{\Psi}_{2,1}(1) & \tilde{\Psi}_{2,1}(2) & \dots & \tilde{\Psi}_{2,1}(n) \ \tilde{\Psi}_{2,2}(1) & \tilde{\Psi}_{2,2}(2) & \dots & \tilde{\Psi}_{2,2}(n) \ \vdots & \vdots & \ddots & \vdots \ \tilde{\Psi}_{2,n/2^2}(1) & \tilde{\Psi}_{2,n/2^2}(2) & \dots & \tilde{\Psi}_{2,n/2^2}(n) \end{pmatrix}, \ \mathbf{M}_{j_0}=\begin{pmatrix} \Phi_{j_0,1}(1) & \Phi_{j_0,1}(2)\cdot\dots & \Phi_{j_0,1}(n) \end{pmatrix}, \ \mathbf{V}_{j_0}=\begin{pmatrix} \Phi_{j_0,1}(1) & \Phi_{j_0,1}(2)\cdot\dots & \Phi_{j_0,1}(n) \end{pmatrix}$$

由于 M 是正交的，因此也有

$$x = M'\mathbf{w}, (12.24)$$

其中 M' 是 M 的转置。也就是说，知道 M 允许我们从数据变换到小波系数（DWT），而 M' 允许我们执行逆离散小波变换（IDWT），即从小波系数变换回数据。

注意：虽然 DWT 可以应用于长度不是 2 的幂的数据集，但在说明性材料中，我们假设 $n = 2^Jo$ 对于某个 $J0$。

关于离散小波和尺度函数的讨论，参见 Percival 和 Walden (2000)、Strang 和 Nguyen (1997) 以及 Bruce 和 Cao (1996)。需要注意的是，小波的离散版本具有连续小波的一般形式，但并非其简单离散化。大多数作者将 M 的元素称为小波和尺度滤波器系数。由于小波和尺度滤波器系数是对连续伸缩和平移小波的离散化版本的良好近似，我们使用符号 $\psi_{j,k}$ 和 $\phi_{j,k}$（参见 Percival 和 Walden, 2000, 方程 469 和 477a）。

利用 12.23 中的划分，我们可以写出

| w1 | M1 |
| w2 | M2 |
| : | : |
| w Jo | MJo |
| v Jo | VJo | = x_r, (12.25)

其中

| w1 = (d_{1,1} d_{1,2} d_{1,n/2}), |
| w2 = (d_{2,1} d_{2,2} ... d_{2,n/2}), |
| w Jo = d_{Jo,1} v Jo = s_{Jo,1}. |

参见 Percival 和 Walden (2000) 讨论构造矩阵 M 所涉及的问题。

## 示例 12.2：离散 Haar 小波

考虑使用 Haar 小波的数据集，大小为 $n = 8$。在这种情况下 $Jo = 3$，八个小波系数为 $w = (d_{1,1}, d_{1,2}, d_{1,3}, d_{1,4}, d_{2,2}, d_{3,3}, s_{3,3})$，且方程 12.22 取形式

$$\begin{pmatrix} -1/\sqrt{2} & 1/\sqrt{2} & 0 & 0 & 0 & 0 & 0 & 0 \ d_{11} & 0 & -1/\sqrt{2} & 1/\sqrt{2} & 0 & 0 & 0 & 0 & x_1 \ d_{12} & 0 & 0 & 0 & -1/\sqrt{2} & 1/\sqrt{2} & 0 & 0 & x_2 \ d_{13} & 0 & 0 & 0 & 0 & 0 & -1/\sqrt{2} & 1/\sqrt{2} & x_3 \ d_{14} & -1/\sqrt{2} & -1/\sqrt{2} & 1/2 & 1/2 & 0 & 0 & 0 & x_4 \ d_{21} & 0 & 0 & 0 & 0 & -1/\sqrt{2} & 1/2 & 1/2 & x_5 \ d_{22} & -1 & -1 & -1 & -1 & 1 & 1 & 1 & 1 & x_6 \ d_{31} & 1/\sqrt{8} & 1/\sqrt{8} & 1/\sqrt{8} & 1/\sqrt{8} & 1/\sqrt{8} & 1/\sqrt{8} & 1/\sqrt{8} & x_7 \ s_{31} & 1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 & x_8 \end{pmatrix}$$

（参见 Percival 和 Walden, 2000）。因此我们看到 $\psi_{1,1}(1)=-1/\sqrt{2}$，$\psi_{1,2}(2)=1/\sqrt{2}$，且 $\psi_{1,1}(t)=0, t=3, \dots, 8$。类似地，$\psi_{31}(t)=-1/\sqrt{8}, t=1, \dots, 4$ 且 $\psi_{31}(t)=1/\sqrt{8}, t=5, \dots, 8$ 而 $\phi_{13}(t)=1/\sqrt{8}, t=1, \dots, 8$。利用方程 12.23 我们写出方程为

$$\begin{pmatrix} w_1 & M_1 \ w_2 & M_2 \ w_3 & M_3 \ v_3 & V_3 \end{pmatrix}$$

其中

$M_1 = \begin{pmatrix} -1/\sqrt{2} & 1/\sqrt{2} & 0 & 0 & 0 & 0 & 0 & 0 \ 0 & 0 & -1/\sqrt{2} & 1/\sqrt{2} & 0 & 0 & 0 & 0 \ 0 & 0 & 0 & 0 & -1/\sqrt{2} & 1/\sqrt{2} & 0 & 0 \ 0 & 0 & 0 & 0 & 0 & 0 & -1/\sqrt{2} & 1/\sqrt{2} \end{pmatrix}$

$M_2 = \begin{pmatrix} -1/2 & -1/2 & 1/2 & 1/2 & 0 & 0 & 0 & 0 \ 0 & 0 & -1 & -1 & -1/2 & -1/2 & 1/2 & 1/2 \end{pmatrix}$

$M_3 = \begin{pmatrix} -1/\sqrt{8} & -1/\sqrt{8} & -1/\sqrt{8} & -1 & 1/\sqrt{8} & 1/\sqrt{8} & 1/\sqrt{8} & 1/\sqrt{8} \end{pmatrix}$

且

$V_3 = \begin{pmatrix} 1/\sqrt{8} & 1/\sqrt{8} & 1/\sqrt{8} & 1/\sqrt{8} & 1/\sqrt{8} & 1/\sqrt{8} & 1/\sqrt{8} & 1/\sqrt{8} \end{pmatrix}$

**w** 的一些元素在下面的方程 12.27 中给出：

$d_{1,1}=-\frac{1}{\sqrt{2}}x_1+\frac{1}{\sqrt{2}}x_2$,
$d_{2,1}=-\frac{1}{2}(x_1+x_2)+\frac{1}{2}(x_3+x_4)$,
$d_{3,1}=-\frac{1}{\sqrt{8}}(x_1+x_2+x_3+x_4)+\frac{1}{\sqrt{8}}(x_5+x_6+x_8)$,
$s_{3,1}=\frac{1}{\sqrt{8}}(x_1+x_2+x_3+x_4+x_5+x_6+x_8)$.
(12.27)

为了说明这一点，我们使用方程 12.24 和 12.26，值 $x_i$ 给出为

$x_i=-\frac{1}{\sqrt{2}}d_{1,1}-\frac{1}{2}d_{2,1}-\frac{1}{\sqrt{8}}d_{3,1}$,
(12.28)

这可使用方程 12.27 验证（参见问题 12.5）。

## 12.3.5 金字塔算法

虽然小波系数可以由方程 12.22 计算，但 Mallat (1989) 在小波环境中引入的金字塔算法为计算它们提供了一种有效的方法。金字塔算法概述如下，适用于长度为 $n=2^l$ 的集合：

**步骤 1：** 从数据值 $x_1, x_2, \dots, x_n$ 开始（方便地表示为 $s_{0,1}, s_{0,2}, \dots, s_{0,n}$），将它们‘下采样’为两个集合，每个包含 $n/2$ 个值以获得

- $n/2$ 个系数：$d_{1,k}, k=1, \dots, n/2$
- $n/2$ 个系数：$d_{1,k}, k=1, \dots, n/2$

**步骤 2：** 保留 $d_{1,k} k=1, \dots, n/2$ 并对 $s_{1,k} k=1, \dots, n/2$ 进行下采样以获得

- $n/4$ 个系数：$s_{2,k}, k=1, \dots, n/4$
- $n/4$ 个系数：$d_{2,k}, k=1, \dots, n/4$

**步骤 3：** 保留 $d_{2,k} k=1, \dots, n/4$，并对 $s_{2,k} k=1, \dots, n/4$ 进行下采样以获得

- $n/8$ 个系数：$s_{3,k} k=1, \dots, n/8$
- $n/8$ 个系数：$d_{3,k} k=1, \dots, n/8$

...

