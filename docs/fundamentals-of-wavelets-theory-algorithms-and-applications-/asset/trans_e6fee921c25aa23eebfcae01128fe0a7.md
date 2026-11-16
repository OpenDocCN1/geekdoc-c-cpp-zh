

## 第二章

## 数学预备知识

本章的目的是使读者熟悉一些有助于理解小波理论的数学符号和工具。由于小波是满足某些可接受性条件的连续函数，因此在本章讨论函数空间的一些定义和性质是审慎的。有关函数空间的更详细讨论，读者可参考实分析的标准教材。后续章节中讨论的小波算法涉及系数序列的数字处理。对数字信号处理主题（如采样、z变换、线性时不变系统和离散卷积）的基本理解对于掌握小波理论是必要的。此外，还包含了线性代数和矩阵运算的简要讨论，这对于滤波器组的离散时域分析非常有用。已经熟悉其内容的读者可以跳过本章。

### 2.1 线性空间

从最广义的意义上说，函数空间仅仅是满足某些数学结构模式的函数集合。例如，有限能量空间 \( L^2(-\infty, \infty) \) 是平方可积函数的集合；即，

(2.1) \int_{-\infty}^{\infty} |f(x)|^2 dx < \infty，

线性空间的一些要求和运算规则如下：

- 1. 空间 S 不能为空。
- 2. 如果 x \in S 且 y \in S，则 x + y = y + x。
- 3. 如果 z \in S，则 (x + y) + z = x + (y + z)。
- 4. 在 S 中存在唯一元素 0，使得 x + 0 = x。
- 5. 在 S 中存在另一个唯一元素 -x，使得 x + (-x) = 0。

除了这些简单而重要的规则之外，我们还定义标量乘法 y = cx，使得如果 x \in S，则对于每个标量 c，y \in S。对于空间 S，我们有以下附加规则：

- 1. c(x + y) = cx + cy。
- 2. (c + d)x = cx + dx，其中 c 和 d 为标量。
- 3. (cd)x = c(dx)。
- 4. 1 \cdot x = x。

满足这些附加规则的空间称为线性空间。然而，到目前为止，我们尚未定义一个度量来衡量线性空间中元素的大小。如果我们为 S 中的每个函数分配一个称为 x 的范数的数值 $||x||$，则该空间成为一个 *规范线性空间*（即带有关联度量的空间）。空间的范数也必须满足某些数学性质：

- 1. $||x|| \ge 0$ 且 $||x|| = 0 \Leftrightarrow x = 0$。
- 2. $||x + y|| \le ||x|| + ||y||$。
- 3. $||ax|| = |a| ||x||$，其中 a 为标量。

函数的范数仅仅是函数到原点（即 0）的距离的一种度量。换句话说，我们可以使用范数

(2.2) $||x - y||$

来衡量两个函数 x 和 y 之间的差异（或距离）。

可以选择多种范数作为特定线性空间的度量。例如，有限能量空间 $L^2(-\infty, \infty)$ 使用范数

(2.3) $||x|| = \left[ \int_{-\infty}^{\infty} |f(x)|^2 dx \right]^{\frac{1}{2}} < \infty$

我们将其称为 $L^2$-范数。该范数也用于衡量两个有限能量函数之间的总体差异（或误差）。该度量称为均方根误差（RMSE），定义为

RMSE = \left[ \lim_{T \to \infty} \frac{1}{T} \int_{-T/2}^{T/2} |f(x) - f_a(x)|^2 dx \right]^{\frac{1}{2}}
(2.4)

其中 \(f_a(x)\) 是 \(f(x)\) 的近似函数。(2.4) 中的表达式是在 \(L^2\) 意义下的近似误差。

### 2.2 向量与向量空间

基于前一节讨论的函数空间基本概念，我们现在介绍向量空间的一些基础知识。我们首先简要回顾几何向量分析。

三维欧几里得向量空间中的向量 \(V\) 由三个复数 \(\{v_1, v_2, v_3\}\) 定义，这些复数与三个正交单位向量 \(\{a_1, a_2, a_3\}\) 相关联。

有序集 \(\{v_j\}_{j=1}^3\) 表示向量 \(V\) 的标量分量，其中单位向量集 \(\{a_j\}_{j=1}^3\) 张成三维欧几里得向量空间。该空间中任何向量 \(U\) 都可以分解为三个向量分量 \(\{u_j a_j\}_{j=1}^3\)（图 2.1d）。

图 2.1：欧几里得空间中向量的正交分解。

![](img/f73ae67732328dc36596b27ffe8d0152_37_0.png)

![](img/f73ae67732328dc36596b27ffe8d0152_37_1.png)

![](img/f73ae67732328dc36596b27ffe8d0152_37_2.png)

![](img/f73ae67732328dc36596b27ffe8d0152_37_3.png)

该空间中向量的加法和标量乘法定义为：

- 1. \(\boldsymbol{U} + \boldsymbol{V} = \{u_1 + v_1, u_2 + v_2, u_3 + v_3\}\)。
- 2. \(k\boldsymbol{V} = \{kv_1, kv_2, kv_3\}\)。

除了这些运算之外，三维欧几里得空间中的向量也遵守交换律和结合律：

- 1. \(\boldsymbol{U} + \boldsymbol{V} = \boldsymbol{V} + \boldsymbol{U}\)。
- 2. \((\boldsymbol{U} + \boldsymbol{V}) + \boldsymbol{W} = \boldsymbol{U} + (\boldsymbol{V} + \boldsymbol{W})\)。

我们可以用列矩阵表示向量

$$\mathbf{V} = \begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix},$$

因为上述所有数学规则都适用于列矩阵。我们定义向量的长度，类似于函数范数的定义，如下

$$|\mathbf{V}| = \sqrt{v_1^2 + v_2^2 + v_3^2}.$$

两个向量的标量积（内积）是向量代数中非常重要的运算，我们在此应予考虑。它定义为

$$\begin{aligned} \mathbf{U} \cdot \mathbf{V} &:= |\mathbf{U}||\mathbf{V}| \cos \angle \mathbf{U}, \mathbf{V} \\ &= u_1 v_1 + u_2 v_2 + u_3 v_3 \\ &= [u_1 \ u_2 \ u_3] \begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix} \\ &= \begin{bmatrix} u_1 \\ u_2 \\ u_3 \end{bmatrix}^t \begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix}, \end{aligned}$$

其中上标 \(t\) 表示矩阵转置，\(:=\) 是定义符号。已知标量积遵守交换律：\(\mathbf{U} \cdot \mathbf{V} = \mathbf{V} \cdot \mathbf{U}\)。如果 \(\mathbf{U} \cdot \mathbf{V} = 0\)，则两个向量 \(\mathbf{U}\) 和 \(\mathbf{V}\) 互相 *正交*。

我们定义向量在另一个向量上的 *投影* 为

\(\frac{\boldsymbol{U} \cdot \boldsymbol{V}}{|\boldsymbol{V}|} = \boldsymbol{U} \cdot \boldsymbol{a}_v\)
\(= \text{projection of } \boldsymbol{U} \text{ in the direction of } \boldsymbol{a}_v\)
\(= \text{a component of } \boldsymbol{U} \text{ in the direction of } \boldsymbol{a}_v.\)
(2.8)

投影是一个重要概念，将在后续讨论中频繁使用。如果需要找到向量在给定方向上的分量，只需将向量与所需方向的单位向量取标量积，即可将向量投影到该方向上。

我们现在可以将基和投影的概念从三维欧几里得空间扩展到 \(N\) 维向量空间。该空间中向量的分量形成一个 \(N \times 1\) 列矩阵，而基向量 \(\{ \boldsymbol{a}_j \}_{j=1}^N\) 形成一个正交集，使得

(2.9) \(\boldsymbol{a}_k \cdot \boldsymbol{a}_\ell = \delta_{k,\ell}, \quad \forall k, \ell \in \mathbb{Z}\)

其中 \(\delta_k\) 是克罗内克 delta，定义为

(2.10) \(\delta_{k,\ell} = \begin{cases} 1, & k = \ell \\ 0, & k \neq \ell. \end{cases}\)

并且 \(\mathbb{Z}\) 是所有整数的集合，\(\{..., -1, 0, 1, ...\}\)。

可以使用内积获得向量 \(\boldsymbol{V}\) 的特定分量 $v_j$（或 \(\boldsymbol{V}\) 在 \(\boldsymbol{a}_j\) 方向上的投影）

**(2.11)** $$v_j = \boldsymbol{V} \cdot \boldsymbol{a}_j,$$

并且向量 \(\boldsymbol{V}\) 表示为其向量分量的线性组合

**(2.12)** $$\boldsymbol{V} = \sum_{k=1}^N v_k \boldsymbol{a}_k.$$

众所周知，可以通过逐个求取分量，将向量沿基向量方向分解为初等向量。图 2.1 说明了这一过程。图 2.1a 中的向量 \(\boldsymbol{V}\) 分解为 \(\boldsymbol{V}_p = \boldsymbol{V} - v_3 \boldsymbol{a}_3\) 及其正交互补向量 \(v_3 \boldsymbol{a}_3\)。向量 \(\boldsymbol{V}_p\) 进一步分解为 \(v_1 \boldsymbol{a}_1\) 和 \(v_2 \boldsymbol{a}_2\)。图 2.1d 表示从分量重构向量 \(\boldsymbol{V}\)。

图 2.1 中所示的示例虽然基础，但与小波分解和重构算法类似。在那里，正交分量是不同分辨率的小波函数。

### 2.3 基函数、正交性与双正交性

我们将欧几里得几何向量空间的概念扩展到规范线性空间。也就是说，与其思考

