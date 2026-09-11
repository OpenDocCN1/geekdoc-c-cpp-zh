
# 随机波线性系统的命中概率

Robert C. Dalang

Marta Sanz-Solé

![](img/05476fb9f1f834e6e3ed1a310fdf5f50_0_0.png)

Robert C. Dalang

Marta Sanz-Solé

![](img/05476fb9f1f834e6e3ed1a310fdf5f50_1_0.png)

Dalang, Robert C., 1961-

本期刊致力于纯数学和应用数学领域的研究。

本出版物被 `Mathematical Reviews`, `Zentralblatt MATH`, `Science Citation Index`, `Science Citation Index Expanded`, `ISI Alert Services`, `SciSearch`, `Research Alert`, `CompuMath Index`, `Current Contents` 收录。

书中使用的论文不含酸，并符合持久性和耐用性的指南。访问 AMS 首页：`http://www.ams.org/`

- 第一章 引言 ... 1
- 第二章 命中概率的上界 ... 9
  - 2.1 增量的界限 ... 10
  - 2.2 概率密度函数的均匀上界 ... 14
- 第三章 马尔可夫矩阵特征值的下界条件 ... 21
  - 3.1 联合密度的上界 ... 22
  - 3.2 命中概率下界的证明 ... 27
- 第四章 马尔可夫矩阵特征值与下界的研究 ... 31
  - 4.1 小特征值的研究 ... 31
  - 4.2 大特征值的研究 ... 38
- 附录 A ... 47
  - A.1 马尔可夫范数的界限 ... 47
  - A.2 协方函数的积分增量 ... 56
  - A.3 马尔可夫范数与内积的进一步界限 ... 68

# 摘要

我们考虑一个 $d$ 维随机场 $u=\{u(t,x)\}$，它在空间维度 $k\in\{1,2,3\}$ 上满足非线性随机波方程，由时间白空间均匀噪声驱动。我们主要考虑空间协方差由指数 $\beta$ 的 Riesz 核给出的情况。利用马尔可夫微积分，我们建立了随机场访问确定子集 $\mathbb{R}^d$ 的概率，分别相对于豪斯多夫测度和牛顿容量。该维度是最优的，并表明当 $d(2-\beta) > 2(k+1)$ 时，点对于 $u$ 是极点。相反，在低维 $d$ 下，点不是极点。然而，点的极性问题存在一个未解决的区间。

2012年5月8日编辑收稿，2013年9月修订。

2015年1月22日电子版发表。

**关键词和短语。** 命中概率、随机波方程组、空间均匀噪声、容量、豪斯多夫测度。

第一作者受瑞士国家基金会支持。第二作者受加泰罗尼亚政府资助，西班牙科学部支持。Robert C. Dalang，瑞士洛洛昂联邦学院数学研究所。

Marta Sanz-Solé，巴塞罗纳大学数学学院。电子邮箱：`marta.sanz@ub.edu`。

# 1. 引言

在本文中，我们考虑 $d$ 维随机场 $u=(u_1(t,x), \dots, u_d(t,x))$，它是 $d$ 维随机波方程组的解：

```
(\frac{\partial^2}{\partial t^2} - \Delta) u_i(t,x) = \sum_{j=1}^d \int_0^t \int_{\mathbb{R}^k} G(t-s,y) \sigma_{i,j}(u(s,y)) M^j(ds,dy) + \int_0^t \int_{\mathbb{R}^k} G(t-s,y) b_i(u(s,y)) ds,
```

$i=1,\dots,d; (t,x) \in [0,T] \times \mathbb{R}^k, k \in \{1, 2, 3\}$，其中 $\Delta$ 表示 $\mathbb{R}^k$ 上的普拉斯拉斯。我们给出研究该系统的动机：一个完全概率空间 $(\Omega, \mathcal{F}, P)$，对于任意 $j \in \{1,\dots,d\}$，我们考虑一个中心高斯变量族 $M^j = \{M^j(\varphi)\, \varphi \in C_0^{\infty}(\mathbb{R}^{1})\}$。$M^j$ 是独立的，且每个 $M^j$ 的协方函数为：

```
(1.2) \quad E(M^i(\varphi)M^j(\psi)) = \int_{\mathbb{R}_+} \int \Gamma(dx) (\varphi(s) \star \dot{\psi}(s)) (x),
```

“$\star$”表示空间参数上的卷积算子，$\dot{\psi}(t,x) = \psi(t,x)$。

如[7]所示，公式(1.2) 也可以写为：

```
(1.3) \quad E(M^i(\varphi)M^j(\psi)) = \int_0^{\infty} \int \mu(d\xi) \mathcal{F}\varphi(\xi) \mathcal{F}\psi(\xi),
```

其中 $\mu$ 表示谱测 ($\mu = \mathcal{F}^{-1}$)，$\mathcal{F}$ 表示 $\mathbb{R}^k$ 上的傅叶变换算子。

方程组(1.1) 的严格解释如下：

```
u_i(t,x) = \sum_{j=1}^d \int_0^t \int_{\mathbb{R}^k} G(t-s,y) \sigma_{i,j}(u(s,y)) M^j(ds,dy),
```

```
(1.4) \quad + \int_0^t \int_{\mathbb{R}^k} G(t-s,y) b_i(u(s,y)) ds,
```

$i=1,\dots,d$，$G$ 表示波方程的基本解，$M^i$ 被扩展为适定的鞅尔格测度，且随机积分见于 [7]。对于 $k = 1, 2, 3$ 的 $G$ 表达式及其傅里叶变换，分别参见 (1.9) 和 (1.10)。

假设谱测度 $\mu$ 满足

```
(1.5) \int_{\mathbb{R}^d} \frac{\mu(d\xi)}{1+|\xi|^2} < \infty
```

其中 $|\cdot|$ 是欧几里得范。那么，根据 [7] 中定理 13 的简单扩展，存在 $d$ 维随机过程 $u = (u(t,x))_{1\leq i\leq d}$ 的唯一随机场解，$(t,x) \in [0,T] \times \mathbb{R}^k$，该解适应于与鞅尔格测度 $\{M_i\}, (t \in [0,T], B \in \mathcal{B}(\mathbb{R}^k))$ 相关的自然滤波，并在 $L^2(\Omega)$ 中连续。这里，$\mathcal{B}(\mathbb{R}^k)$ 表示 $\mathbb{R}^k$ 上有界波雷尔集的集合。

我们的目标是建立过程 $u$ 命中集合 $A \in \mathcal{B}(\mathbb{R}^k)$ 概率的上下界，并为过程 $u$ 开发一个概率势。这将根据 $A$ 的豪斯多夫测度和贝塞尔-Roe 容积得到。

在 [18] 中，研究了任意固定维 $k$ 下高斯波的命中概率。该文献涵盖了当 $(a,\sigma)$，$\sigma=(\sigma_{ij})_{1\leq i,j\leq d}$，$b=(b^i, i=1,\dots,d) \equiv 0$ 且 $k \in \mathbb{N}$ 时的情况。证明了以下结论：假设协方差 $\sigma$ 相对于勒格测度绝对连续，且其密度由 $f(x)=|x|^\beta$ 给出，其中 $t_0 \in [0,T]$，令 $I, J$ 为 $[0,T]$ 和 $\mathbb{R}^k$ 的紧集，且均具有正勒格测度。固定 $N>0$。存在依赖于 $I, J, N \beta, k$ 和 $d$ 的常数 $c$ 和 $C$，对于任意波雷尔集 $A \subset [-N,N]^d$，

```
(1.6) C_{d-k(1+\beta)/(2-\beta)}P(u(I) \cap A \neq \emptyset) \leq cH_{d-k(1+\beta)/(2-\beta)}(A)。
```

这里，下界包含 $A$ 的 $d-k(1+\beta)/(2-\beta)$ 容积，上界包含 $A$ 的豪斯多夫测度（在章末尾，我们将回顾这些概念的定义）。参数 $d-k(1+\beta)/(2-\beta)$ 给出了在该方程可能推广到 (1.4) 时可以预期的最优值。

(1.6) 的证明是通过应用 [18] 中建立的命中概率的一些通用准则（另见 [2]）完成的。这些准则由随机场 $u_i$ 中随机变量的密度和联合密度性质描述，还由其路径的正则性描述。由下式给随机场

```
u_i(t,x)=\int_0^t\int_{\mathbb{R}^d} G(t-s,y)\sigma_{ij}M^i(ds,dy), \quad i=1,\dots,d，
```

检查应用上述准则的必要假设是通过直接对（高斯）密度的显式公式进行。

非线性随机偏微分方程系统的命中概率在 [16], [10], [11] 和 [18] 中被研究过（高斯）随机弦见 [31]，带反射的热方程见 [15]，以及由加性分维布朗运动驱动的一类热方程见 [36]）。在第一篇文献中，考虑了一个由布朗面驱动的二参数 Itô 方程组。通过 45 度旋转，该系统被转化为一个由时空白噪声驱动的、空间维 $k=1$ 的高斯方程组成的新系统。文献 [10, 11] 涉及由时空白噪声驱动的空间维 $k=1$ 的热方程组。[12] 考虑了由描述类型的高斯噪声驱动的 $k \geq 1$ 的非线性热方程组，其协方差测度为 $\Gamma(dx)=|x|^{-\beta}$ $\beta \in [0,2 \wedge k]$（并在此发展了一些想法）。与 [18] 和 [2] 不同，在非高斯情况下，度的存在性、表达式和性质是通过 Malliavin 积分得到的。为此，我们将使用这一工具。为此，我们考虑系统 (1.4) 的以下条件：

- (P1) 函数 $\sigma_{i,j}$ 和 $b_i$，$1 \leq i,j \leq d$ 是无限次可微的，且任意正阶偏导数都是有界的。此外，$\sigma_{i,j}$，$1 \leq i,j \leq d$ 是有界的。
- (P2) 矩阵值函数 $\sigma$ 是一致椭性的。这意味着对于任何 $\|v\|=1$ 的 $v \in \mathbb{R}^d$

```
(1.7) \inf_{x \in \mathbb{R}^d} v^T \sigma(x)v \geq \rho > 0。
```

第 2 章致力于根据豪斯多夫测度建立上界。根据 [18] 定理 2.4，只需证明对于任意变量 $u(t,x) \in [0,T] \times \mathbb{R}^k$，存在密度 $p_{u,x}(z)$，且该密度在紧集上一致有界。我们必须从距离 $|t-s|+|x-y|$ 的幂来限制增量 $u(t,x)-u(s,y)$ 的 $L^p$ 矩，对于任意 $q \in [1, \infty[$（参见 (R1) 和 (R2)）。

$u(t,x) \in [0,T] \times \mathbb{R}^k$，$z$ 变量的光滑性存在，对于 $k=2$ 和 $k=3$ 的波方程分别在 [30] 和 [38] 中得到证明。然而，据我们所知，对于 $k=1$ 的空间均匀噪声不存在此类证明，且一致有界性尚未解决。

由于分析增量 $u(t,x)-u(s,y)$ 的 $L^p$ 矩，我们考虑协方差测度 $\Gamma$ 的不同类型。两种情况——加性噪声和乘性噪声被分别处理。后者允许更一般的协方差，且估计更尖锐。对于乘性噪声，我们依赖于 $k=2$ [29,30] 和 $k=3$ [17] 的已知结果，但对于 $k=1$，我们给出了一个完整的证明。最后，我们关于上界的结论在定理 2.1 中给出。

本文的主要部分致力于根据 $A$ 的贝塞尔-Roe 容积建立命中概率的下界。为此，我们假设 $\Gamma(dx)=|x|^{-\beta}$，其中 $\beta \in[0,2 \wedge k]$。第 2 章中的假设 (C1) 比列出的其他条件 (C1'), (C3) 更严格。

命中概率的下界通过使用 [18] 中定理 2.1 的修正得到如下。当应用于系统 (1.4) 的随机解时，该定理的两个假设是：

- (a) 对于 $(s,y), (t,x) \in [0,T] \times \mathbb{R}^k$，$u(s,y), u(t,x)$ 的联合密度具有高斯类型上界；
- (b) 密度 $p_{t,x}$ 在 $\mathbb{R}^d$ 上严格正。

性质 (b) 最近在 [35] 中建立。对于 (a) 中的上界，我们在这里展示该假设可以显著放宽。事实上，高斯类型的指数因子可以用单项式代替（参见定理 3.5 和备注 3.1(b)），这仍然导致相同的命中概率下界。

正如 [11]，本文的主要技术工作是建立联合密度的这种上界。我们遵循文献中相同的通用方法，尽管我们遇到的困难及其解决方式存在显著差异。令 $Z = (u(s,y), u(t,x)-u(s,y))$，并用 $\gamma_Z$ 表示 $Z$ 的 Malliavin 矩阵。我们分析的核心在于根据 $|t-s|$ 的负幂估计 $\gamma_Z$ 特征值倒数的 $L^p$ 矩。正如 [11] 指出的，这仅对于“小”值是必要的。对于“大”特征值，只需证明它们具有有界的 $L^p$ 矩。

在第 3 章中，我们强调了这一事实。事实上，定理 3.1 提供了命中概率的下界，假设之前大小特征值的条件（见 (3.5)-(3.6)）被满足。虽然定理 3.1 的证明使用了 [11] 中的论证，但我们想强调两个新点。首先是上述关于条件 (a) 的备注。事实上，在文献以前分析的例子中，指数因子是通过应用指数不等式得到的。这通过消除漂移项是不可能的；对于 $k > 1$ 不存在该定理的版本。幸运的是，可以获得单项式因子，我们 $u(t,x)-u(s,y)$ 关于 $|t-s|+|x-y|$ 幂的 $L^p$ 估计。这个问题与通过柯尔莫哥夫连续性分析样本正则性自然地出现。第二点是，该定理解释了我们提到的特征值退化率（由某些正参数 $\rho$ 描述，见 (3.5)）与命中概率下界中贝塞尔-Roe 容积维度之间的关系（见 (3.5)）。特别是，我们从定理 3.1 观察到获得下界的最优结果需要小特征值退化率的最优结果。

第 4 章致力于分析 Malliavin 矩阵 $\gamma_Z$ 的特征值，以检查假设 (3.5)-(3.6) 对于某些速率参数 $\rho$ 的有效性。执行此任务的主要工作是 [11, Proposition 3.5]。然而，我们在定理 4.1 中得到的 $\rho$ 值接近 $3-\beta$，而最优值应该是 $2-\beta$。

建立特征值边界 (3.6) 的证明依赖于热核的半群性质及其性质，并反复使用 [11, Proposition 3.5]。我们也使用这一工具，但证明的整体结构非常不同。由于缺乏半群性质，引理 A.12 起了至关重要的作用。该引理告诉我们对于 $\epsilon > 0, x, y \in \mathbb{R}^k, x \neq y$：

```
\lim_{|x-y| \to 0} \int_0^{\epsilon} dr (G(r, y-*), G(h+r, x-*))_{\mathcal{H}} = 0，
```

对于 $r \in [0,1]$ 一致成立（等等，文中说的是 $[0,1]$）。这一结果与经典的黎曼-勒贝格引理具有相似性。在 [11] 中，空间 $\mathcal{H}$（与空间平稳噪声的协方差相关）被 $L^2([0,1])$ 替换。最后，我们关于下界的主要结果在定理 4.3 中给出。

附录 A 收集了前面的章节中使用的辅助估计。这些估计具有不同类型。引理 A.4、A.5、A.7、A.8、A.9 涉及协方函数的积分增量。它们通过显式地引入对时间变量积分域长度的依赖关系，扩展了 [17] 中证明的结论。引理 A.1 和 A.11 确定了波方程基本解 $G$ 在 $\mathcal{H}$-范数下积分的上界和下界。命题 A.3 和 A.6 提供了在大小为 $\epsilon$ 的区域上，随机过程 $\mathcal{H}$-范数积分的 $L^p$-测度上界，该过程是解的增量与一个 $L^p$ 有界过程的乘积。引理 A.12 已经提到过。

我们通过简要讨论与 (1.6)（高斯情况）对比所获得的结果，结束了对本文结果与之前结果之间差异的描述。上界 (2.1) 是**几乎最优的**。事实上，通过取 $\Gamma(\delta) = |x|^{-\beta}$，其中 $\beta \in [0, 2]$，豪斯夫测度对 (2.1) 右侧的依赖关系严格小于 $d - \frac{2(k-1)}{2-\beta}$。同样的现象也出现在 [11] 与 [10] 的对比中。考虑到下界，根据 (3.7)，如果 (3.5) 中的参数 $\rho$ 等于 $2-\beta+\delta$，对于 $\delta$ 任意趋于零，那么 (3.7) 中容量的依赖将是 $d - \frac{2(k-1)}{2-\beta} + \eta$，其中 $\eta$ 任意趋于零，因此任意接近高斯情况。我们在 (4.1) 中看到，对于任何任意小的 $\delta$，我们可以取 $\rho = 3-\beta+\delta$。这在定理 4.3 中给出了容量维 $d (1 + \frac{2\delta}{2-\beta}) + \delta - \frac{2(k-1)}{2-\beta}$，这距离最优值相当远。这是由于我们为了控制特征值的大小而使用的时间局部化类型（例如参见 (4.3), (4-4)）。确定一个能提供下界最优维的更好局部化方法是一个开放问题。

命中概率研究的一个目标是确定哪些 $d$ 和 $\beta$ 是极点（polar），哪些不是。记得，点 $z \in \mathbb{R}^d$ 对于 $u$ 是极点，当且仅当 $\mathbb{P}(\tau(z,t) \in [0,T] \times \mathbb{R}^k : u(t,x)=z)=0$，否则不是极点。通常情况下，点在较大的 $d$ 和/或较小的 $k$ 下是极点的，而非不是。以下是定理 2.1 和 4.3 的直接推论。

推论 1.1. 假设上述 (P1) 和 (P2)，令 $u$ 和 $k$ 为 (1.4) 的解。



- (a) 假设 $d > \frac{2(k+1)}{2-\beta}$。点对于 $u$ 是极点的。
- (b) 假设 $d(1 + \frac{2\delta}{2-\beta}) < \frac{2(k+1)}{2-\beta}$。点对于 $u$ 是极点的。

我们现在定义后续使用的符号和概念。

设 $\gamma \in \mathbb{R}$。对于博尔集 $A \subset \mathbb{R}^d$，$\gamma$ 维豪斯夫测度定义为：如果 $\gamma < 0$，则 $\mathcal{H}_\gamma(A) = \infty$，而对于 $\gamma \geq 0$，

```
$\mathcal{H}_\gamma(A) = \liminf_{\epsilon \to 0^+} \left\{ \sum_{i=1}^\infty (2r_i)^\gamma : A \subset \bigcup_{i=1}^\infty B_{r_i}(x_i), \sup r_i \leq \epsilon \right\}$.
```

Bessel-Riesz 核定义为：

```
$K_\gamma(r) = \begin{cases} r^{\gamma} & \text{if } \gamma > 0, \log(\frac{1}{r}) & \text{if } \gamma = 0, \frac{1}{r^{\gamma}} & \text{if } \gamma < 0.\end{cases}$
```

其中 $c$ 为正数。对于每一个博尔集 $A \subset \mathbb{R}^d$，令 $\mathcal{P}(A)$ 为 $A$ 上的概率测集。对于 $\mu \in \mathcal{P}(A)$，我们设定：

```
$\mathcal{E}_\gamma(\mu) = \int_A \int_A K_\gamma(|x - y|) \mu(dx)\mu(dy)$.
```

博尔集 $A \subset \mathbb{R}^d$ 的 Bessel-Riesz 容量定义如下：$Cap_{\gamma}(A) = [\inf_{\mu \in \mathcal{P}(A)} \mathcal{E}_\gamma(\mu)]^{-1}$，规定 $1/\infty = 0$。存在一个与空间协方差相关的希尔伯特空间（参见 (1.3)）。事实上，令 $\mathcal{H}$ 为赋予以下内积的实值测试函数 Schwartz空间 $S(\mathbb{R}^k)$ 的完备：

```
$\langle \varphi, \psi\rangle = \int_{\mathbb{R}^k} \varphi(\xi)\overline{\psi(\xi)} d\xi.$
```

我们定义 $\mathcal{H}^d = \{h = (h^1, \dots, h^d) : h^i \in \mathcal{H}, i=1, \dots, d\}$,$\mathcal{H}_t = L^2([0,t]; \mathcal{H})$, $t \in [0,t]$。假设 $\varphi \in \mathcal{H}$ 是有限变分的符号测度。假设 $\Gamma(x) = |x|^{-\beta}$，其中 $\beta \in [0, 2]$，因此 $\mu(\xi) = c|\xi|^{-\beta}$（参见 [7]）。那么通过对 $\varphi$ 的正负部分应用 [2] 中的极化方法：

```
$\|\varphi\|_{\mathcal{H}}^2 = \int_{\mathbb{R}^k} |\varphi(\xi)|^2 \frac{d\xi}{|\xi|^{\beta}}$.
```

这一基本等式将出现多次。我们回顾空间维 $k \in \{1, 2, 3\}$ 下波方程基本解的表达式：

```
k=1: G(t,x) = \frac{1}{2}|t-|x|$
k=2: G(t,x) = \frac{1}{2\pi}(t^2 - |x|^2)^{+\frac{1}{2}},
k=3: G(t,x) = \frac{1}{4\pi}\sigma_t(dx),$
```

其中 $\sigma_t(dx)$ 表示以原点为中心、半径为 $t$ 的球面上的均匀分布，总质量为 $4\pi t^2$。对于任意维 $k \in \mathbb{N}^*$，$G(t)$ 的傅里叶变换给出：

$(1.10) \quad \mathcal{F}G(\xi) = |\xi|^{-1} \sin(t|\xi|)$

读者可以参考 [21] 获取这些公式。在全文中，我们使用符号 $T$ 表示一般的区间 $[t_1, t_2]$，其中 $0 < t_1 < t_2 \leq T < \infty$，$O$ 表示 $\mathbb{R}^d$ 的紧子集，$K$ 表示 $\mathbb{R}^k$ 的紧子集。

我们通过提供研究波方程组的几个动机来结束本引言。记得，确定性波方程是基础二阶偏微分方程之一 [20]。它通过牛顿运动方程，作为均匀弹性介质中波传播（可以是声波、电磁波等）的通用模型而出现。例如，三个波方程组可以用于描述弹性弦在三维空间中的运动。如果这条弦“浮”在流体中，它将受到（随机）分子激发的，由随机噪声驱动的波方程组为弦的运动提供了更详细的描述（这里，$d=3$ 且 $k=1$）；更详细的描述参见 [8]；22] 提供了生物学动机，[42] 提供了该问题的一些数学结果。当然，描述 $N$ 个分子的运动将涉及方程组！

在信号传输 [3] 和海洋学 [1, 28] 中的某些情况下使用了空间相关随机噪声。这种类型的随机噪声在数学文献 [9, 19, 24] 中也很重要。在 $d=1, k=2$ 的情况下，波方程出现在对落在水的雨滴产生的表面波感兴趣。$d=1, k=3$ 的情况（14）出现在对雨滴产生的声波向水深传播感兴趣：水下的听音设备希望过滤掉这种噪声，为此，描述这种声传播的模型是很有用的。

最后一个例子涉及波在总和内部的传播。这将是 $d=1, k=3$ 的情况，噪声是“球面平稳”的而非空间平稳的：[8] 对该问题提供了更详细的描述，[13] 是该方向的一些数学结果。

最后，考虑阻尼波算子，以及将波算子 $a\frac{\partial^2}{\partial t^2}+b\frac{\partial}{\partial t}-c\Delta$ 替换为



在这里，参数 $a, b$ 和 $c$ 具有物理意义，例如单位质量、摩擦系数或弹性系数。在各种极限情况下，例如 $a\downarrow0$ 或 $b\downarrow0$，分别对应零质量极限和无摩擦极限，可以得到热算子或波算子（[4] 及其参考文献包含了相应方程解的收敛性以及该研究的几个动机）。因此，研究如 (1.1) 的波方程组可以被视为研究更一般的随机偏微分方程组的重要一步。

## 第二章 命中概率的上界

我们假设控制系统 (1.4) 的高斯过程的协方测度 $\Gamma$ 对于 $\mathbb{R}^k$ 上的勒贝测度绝对连续的，我们将考虑关于其密度函数 $f$ 的以下假设：

- (C1) 协方测度的形式为 $\Gamma(dx) = f(|x|)dx$，其中 $f(x) = |x|^{-\beta}$，且 $\beta \in [0, 2 \wedge k]$。
- (C2) 协方测度的形式为 $\Gamma(dx) = f(|x|)dx$，其中 $f: \mathbb{R}_+ \to \mathbb{R}_+$ 满足 $\int_{0}^{\infty} r^{\eta-1}f(r)dr < \infty$，对于某些 $\eta \in [0,1]$。
- (C3) 噪声的谱测满足
$$\int_{\mathbb{R}^k} \frac{\mu(d\xi)}{(1+|xi|^2)^\alpha} < \infty$$
对于某些 $\alpha \in [0, 1]$。
- (C3) 协方测度的形式为 $\Gamma(dx)=f(|x|)dx$，当 $x \neq 0$ 时，$f(x)=\varphi(x)|x|^{-\beta}$，其中 $\beta \in[0,\wedge k]$ 且 $\varphi$ 是属于 $C^\varphi[\mathbb{R}^k]$ 的有界正函数（指数为 $\mu \in[0,1]$ 的有界且 Hölder 连续函数空间）。

注意，当 $\Gamma(dx)=|x|^{-\beta}$ 且 $\beta \in[0,\wedge k]$、$\alpha \in[\beta/2,1]$ 时，满足 (C1)。同样，当 $f: \mathbb{R}_+ \to \mathbb{R}_+$ 定义为 $f(r)=r^{-\beta}$、$\beta \in[0,\wedge k]$ 且 $\eta < 2-\beta$ 时，满足 (C2)。

我们设计了以下结论：

**定理 2.1.** 令 $u(t,x), \in [0,T] \times \mathbb{R}^k$ 是由 $k \in\{1,2,3\}$ 的随机偏微分方程 (SPDEs) 系统 (1.4) 给出的随机过程。令 $I$ 和 $K$ 分别为 $[0,T]$ 和 $\mathbb{R}^k$ 的正勒贝测度紧集。

考虑以下情况：

- (1) 加性噪声：矩阵 $\sigma=(\sigma_{ij})_{1\le i,j\le d}$ 具有常数项且 $\sigma \neq 0$；函数 $b_i,1\le i \le d$ 是有界的、无限可微的且任意阶偏导数有界。协方测度满足 (C1) 或 (C1')。
- (2) 乘性噪声：系数 $\sigma_{ij}$ 和 $b_i,1\le i,j \le d$ 满足假设 (P1) 和 (P2)。对于 $k=2$，我们假设协方满足满足 (C2)。对于 $k \in\{1,3\}$，我们假设满足 (C3)。

固定 $\zeta \in[0,d]$。则存在正常数 $c=c(I,K,\Gamma,k,d,\zeta)$，使得对于任何博尔集 $A \in \mathbb{R}^d$，

- (2.1) $P\{u(I \times K) \cap A \neq \emptyset\} \le c cH_{d-\zeta-\frac{k}{2}}(A), \quad i=1,2$。

其中 $\delta_i$ 取值为：在情况 (1) 中，在 (C1) 下 $\delta_1 = \frac{2-\beta}{2}$，在 (C1') 下 $\delta_1 = 1-\alpha$。在情况 (2) 中，对于 $k=1$，$\delta_2 = \frac{2-\beta}{2}$；对于 $k=2$，$\delta_2 = \frac{2}{2}$；对于 $k=3$，$\delta_2 = \frac{2-\beta}{2} \wedge \frac{1+\mu}{2}$。

根据 [18] 中的定理 2.4，为了证明定理 2.1，我们必须证明两个事实：

- (R1) 对于任何 $(t,x) \in \mathcal{T}_0 \times K$，随机向量 $u(t,x)$ 具有密度 $p_{t,x}$，且
$$(2.2) \sup_{t \in \mathcal{T}_0, (t,x) \in \mathcal{T}_0 \times K} p_{t,x} \le C$$
- (R2) 存在 $u \in [0,1]$ 和常数 $C$，使得对于任何 $q \in [1, \infty，$s, t \in \mathcal{T}_0$ 和 $y \in K$，
$$(2.3) |u(t,x) - u(s,y)|^q \le C(|t-s| + |x-y|)^q$$

这两个事实推出了将 $\delta_i$ 替换为 $\delta$ 的 (2.1)。我们注意到 $\zeta$ 是任意小的，只要建立了任意 $\delta < \delta_i$ 的 (2.3)，即可得到 (2.1)。

### 2.1. 增界的

在本节中，我们将证明 (R2)。读者会注意到，在不假设强假设 (P1) 和 (P2) 的情况下，$\sigma_{ij}, b_i (1 \le i, j \le d)$ 仅连续连续。

#### 情况 (1)：加性噪声

**引理 2.2.** 令 $\{u(t,x), (t,x) \in [0,T] \times \mathbb{R}^k\}, k\in\{1,2,3\}$ 为由 (1.4) 定义的系统解。在假设 (C1)（或 (C')）下，性质 (R2) 对于 $\delta = \frac{2-\beta}{2}$（或 $\delta < 1-\alpha$）成立，因此省略索引 $i$。

**证明.** 无一般性，我们在证明中假设 $d=1$ 且 $v(t,x) = \int_0^t \int_{\mathbb{R}} G(t-r, x-z)dz$。固定 $q \in [1, \infty)$ 并考虑 $x \in [0,T]$ 和 $h > 0$ 使得 $t+h \in [0,T]$。则
$$(2.4) E(u(t,x) - u(t+h,x+y))^q \le C(q)(T_1+T_2),$$
其中
$$T_1 = E(|v(t,x) - v(t+h,y)|^q),$$
$$T_2 = E\left(|\int_0^t \int_{\mathbb{R}} G(t-r, x-z)b(r)dz - \int_0^{t+h} \int_{\mathbb{R}} G(t+h-r, y-z)b(r)dz\right).$$

由于过程 $\{v(t,x), (t,x) \in [0,T] \times \mathbb{R}\}$ 是高斯过程，
$$T_1 = C(q)E[|v(t,x) - v(t+h,y)]^{q/2}.$$

那么，根据 [18] 中的引理 4.1，在 (C1) 下得到
$$(2.5) T_1 = C(q)(h + |y|)^{\delta}, \quad \text{其中 } \delta = \frac{2-\beta}{2},$$
且在 (C') 下，这是 [5] 中计算、引理 7.3 和定理 7.4 的结论：
$$(2.6) T_1 = C(q)(h + |y|)^{\delta}, \quad \text{其中 } \delta < 1-\alpha.$$

对于 $T_2$ 的分析，我们首先写下：
$$\int_0^{\mathbb{R}} dr dG(t-r,x-z)b(r) = \int_0^{\mathbb{R}} dr \int_{\mathbb{R}} G(t-r,dz)b(r),$$
$$\int_0^{t+h} dr \int_{\mathbb{R}} dG(t+h-r,y-z)b(r) = \int_0^{t+h} dr \int_{\mathbb{R}} G(t+h-r,dz)b(r),$$
以及项
$$T_{2,1} = E\left|\int_0^{\mathbb{R}} dr G(r,dz) \times [b(u(t-r,x-z)) - b(u(t+h-r,y-z)]\right|^q,$$
$$T_{2,2} = E\left|\int_0^{t+h} dr \int_{\mathbb{R}} G(r,dz)b(u(t+h,y))\right|^q.$$

在 [7] 中证明了零初始条件的随机波方程解在空间上是平稳的。因此，通过对有限测度 $G(r,dz)dr$ 应用 Hölder 不等，利用 $b$ 的 Lipschitz 连续性进行变量替换 $r \to t-r$，我们得到：
$$T_{2,1} \le C \int_0^{\mathbb{R}} dr G(r,dz) \times E(|u(t-r,x-z) - u(t+h-r,y-z)|^q),$$
$$\le C \int_0^{\mathbb{R}} dr E(|u(t-r,x-z) - u(t+h-r,y-z)|^q),$$
$$= C \int_0^{\mathbb{R}} dr (|u(r,x) - u(r+h,x+y)|^q).$$

对有限测度 $G(r,dz)dr$ 应用 Hölder 不等式，利用 $b$ 的 Lipschitz 连续性进行变量替换 $r \to t-r$，得到：
$$T_{2,1} \le C \int_0^{\mathbb{R}} dr G(r,dz) \times E(|u(t-r,x-z) - u(t+h-r,y-z)|^q),$$
$$\le C \int_0^{\mathbb{R}} dr E(|u(t-r,x-z) - u(t+h-r,y-z)|^q),$$
$$= C \int_0^{\mathbb{R}} dr (|u(r,x) - u(r+h,x+y)|^q).$$

在最后一个不等式中，我们有：
$$(2.9) E(u(t,x) - u(t+h,x+y))^q \le C(q)(T_1+T_2),$$
其中
$$(2.8) E(u(t,x) - u(t+h,x+y))^q \le C(q)(h + |y|)^{\delta},$$
$$(2.7) E(u(t,x) - u(t+h,x+y))^q \le C(q)(h + |y|)^{\delta}.$$

因此，我们有：
$$(2.9) E(u(t,x) - u(t+h,x+y))^q \le C(q)(h + |y|)^{\delta}.$$

### 2.2. 命中概率的上界

#### 情况 (2)：乘性噪声

我们首先列出维度 $k\in\{1,2,3\}$ 的已知结果。

假设协方测度 $\Gamma$ 噪声满足 (C2)。则性质 (R2) 对于 $\delta = \frac{2-\beta}{2}$ 成立。

假设 $\Gamma$ 满足 (C3)。对于 $d=1$， [17] 中的定理 4.1 得出了 (R2)，其中 $\delta \in[\frac{2-\beta}{2}, \frac{1-\alpha}{2}]$。扩展到方程方程组是易的。

对于 $k=1$，假设 $\Gamma$ 满足 (C3)。则 (R2) 对于 $\delta = \frac{2-\beta}{2}$ 成立。

对于 $k=2$，假设 $\Gamma$ 满足 (C2)。则 (R2) 对于 $\delta = \frac{2}{2}$ 成立。

对于 $k=3$，假设 $\Gamma$ 满足 (C3)。则 (R2) 对于 $\delta = \frac{2-\beta}{2} \wedge \frac{1+\mu}{2}$ 成立。

### 2.1. 增量矩的界

由于 $k=1, G(r, z) = \frac{1}{2}\{|z|<r\}$，因此根据赫尔德不等式可知 $\||...\|_H^q$ 被以下式界：

$$ \int_{\mathbb{R}} dz \int_{\mathbb{R}} dw |G(t-r, x-z) - G(t-r, y-z)| |\sigma(u(r,z))| \varphi(z-w) \\
|z-w|^{-\beta}| |G(t-r, x-w) - G(t-r, y-w)| |\sigma(u(r,w))|^{\frac{q}{2}} $$
$$ \int_{\mathbb{R}} dz \int_{\mathbb{R}} dw |G(t-r, x-z) - G(t-r, y-z)| |\varphi(z-w)| \\
|z-w|^{-\beta}| |G(t-r, x-w) - G(t-r, y-w)| \\
|E(\sigma(u,z))|^{q/2} |\sigma(u(r,w))|^{q/2}. $$

由于 $\varphi$ 是有界的且 $\sigma$ 是 Lipschitz连续连续，我们使用柯西-施瓦茨不等式可知：

$$ E(|T_1|^q) \le C \int_{z\in\mathbb{R}} dr (1 + |\sigma(u(r,z))|^q) \\
\times \int_{z\in\mathbb{R}} dw |G(t-r, x-z) - G(t-r, y-z)| \\
|z-w|^{-\beta}| |G(t-r, x-w) - G(t-r, y-w)|^{q/2} $$

不失一般性地假设 $x \le y$。区分 $t-r < \frac{y-x}{2}$ 和 $t-r \ge \frac{y-x}{2}$ 情况是有用的。我们考虑后一种情况。对于 $t-r \ge \frac{y-x}{2}$，平行积分等于：

$$ (2.10) \int_{A(x,y,t,r)} dz dw |z-w|^{-\beta}, $$

其中 $A(x,y,t,r) = [x-(t-r), y-(t-r)] \cup [x+t-r, y+t-r]$。

该积分可以写成四个积分之和，前两个为：

$$ I_1 = \int_{x-(t-r)}^{y-(t-r)} dz \int_{x-(t-r)}^{y-(t-r)} dw |z-w|^{-\beta} $$
$$ I_2 = \int_{x+t-r}^{y+t-r} dz \int_{x+t-r}^{y+t-r} dw |z-w|^{-\beta} $$

注意到由于 $\beta \in [0,1]$，

$$ I_1 = \int_{x-(t-r)}^{y-(t-r)} dz dw(z-w)^{-\beta} + \int_{x+t-r}^{y+t-r} dw(w-z)^{-\beta}, $$

显式积分显示：

$$ I_1 = c(x-y)^{2^{-\beta}}. $$

为了界定 $I_2$，我们进一步区分两种情况：$t-r \ge y-x$ 和 $y-x>t-r \ge \frac{y-x}{2}$。当 $t-r \ge y-x$ 时，

$$ I_2 = \int_{x-(t-r)}^{y-(t-r)} dz \int_{x+t-r}^{y+t-r} dw |y-x|^{-\beta} = c|x-y|^{2^{-\beta}}. $$

### 2. 命中概率的上界

当 $y-x > t-r \geq \frac{y-x}{2}$ 时，直接积分显示：

$$ I_2 = c\{(y-x+2(t-r))^{2-\beta} - 2(2(t-r))^{2-\beta} + (x-y+2(t-r))^{2-\beta}\} \\
\leq C|y-x|^{2-\beta}. $$

其他积分源于 (2.10) 并由对称性被界定。我们得出：

$$ E(|T_1|^q) \leq C \int_{z\in\mathbb{R}} (1 + \sup E(|u(r,z)|^q)) |y-x|^{\frac{2-\beta}{2}}q. $$

利用 (2.7)，我们看到：

$$ E(|T_1|^q) \leq C|y-x|^{\frac{2-\beta}{2}}q. $$

我们留给读者检查 $E(|T_2|^q)$ 是否满足类似的界。这得出了界：

$$ E(|u(t,x)-u(t,y)|^q) \leq C|y-x|^{\frac{2-\beta}{2}}q. $$

这完成了在 $k=1$ 且假设 (C3) 下对于 $\delta = \frac{2-\beta}{2}$ 时 (R2) 的证明。

### 2.2. 概率密度函数的均匀界

本节的目的是证明性质 (R1)。我们在这里考虑具有乘积噪声的方程 (1.4)，并假设 $k \in\{1,2,3\}$ 且函数 $\sigma_{i,j}$ 和 $b_i,j=1,\dots,d$ 满足 (P1) 和 (P2)。

我们在 [39] 的背景下使用 Malliavin 微积分（概念和符号）。根据 [11] 中的命题 3.4，性质 (R1) 由以下性质建立：

- (1) $u(t,x) \in\mathbb{D}^{1,\infty}(\mathbb{R}^d)$。
- (2) 对于所有 $p \in[1,\infty[$，存在正数 $c_1$ 使得 $\sup_{(t,x)\in\mathbb{T}\times\mathbb{K}} \|Du(t,x)\|_{\mathcal{H}^p} \leq c_1$。
- (3) 对于所有 $p \in[1,\infty[$，存在正数 $c_2$ 使得 $\sup_{(t,x)\in\mathbb{T}\times\mathbb{K}} E[\det(\gamma_{u(t,x)})^{-p}] \leq c_2$。

其中 $\gamma_{u(t,x)}$ 表示 $u(t,x)$ 的 Malliavin 导数。

在定理 2.1 的两种情况下，性质 (1) 和 (2) 继承自 [39] 中定理 7 对系统的扩展。在这里，我们关注性质 (3) 的证明。为了后续使用，通过 $Du(t,x)$ 的第 $i$ 分量写方程。记住这是一个 $\mathcal{H}^p$ 取值的随机变量。根据 [39] 定理 7.1，对于 $t \leq r, D_{r,z}u(t,x)=0$，而对于 $0 \le r \le t, j=1 \dots d,$

$$D_{r,z}^{(j)}u_i(t,x) = G(t-r, x-z)\sigma_{i,j}(u,x) + \sum_{l=1}^d \int_{\mathbb{R}^k} G(t-s, x-y)\nabla\sigma_{i,j}(u(s,y)) D_{r,z}^{(j)}u(s,y) + \int_0^t ds \int_{\mathbb{R}^k} G(t-s, x-y)\nabla b_i(u(s,y)) D_{r,z}^{(j)}u(s,y),$$

其中符号“$\cdot$”是 $\mathbb{R}^d$ 中的欧几里得积，$D^{(j)}$ 表示对噪声第 $j$ 分量的 Malliavin 导数。

**2.3.** 令 $k \in \{1, 2, 3\}$。如第 1 章所示，固定一个紧集 $\mathbb{T}_0 \times K \subset [0, T] \times \mathbb{R}^k$。假设函数 $\sigma_{i,j}, b_i, i=1 \dots d$ 满足 (P1) 和 (P2)。在定理 2.1 的两种情况下，对于 $p>0$，

$$\sup_{(t,x) \in \mathbb{T}_0 \times K} E \left[ (\det \gamma_{u(t,x)})^p \right] < +\infty.$$

**证明.** 注意到 $\gamma_{u(t,x)} \ge \left( \inf_{|v|=1} v^\top\gamma_{u(t,x)}v \right)^d$。令 $q=pd$。只需检查

$$\sup_{(t,x) \in \mathbb{T}_0 \times K} E \left[ \frac{\inf_{|v|=1} v^\top\gamma_{u(t,x)}v}{q} \right] < +\infty.$$

根据定义，

$$v^\top\gamma_{u(t,x)} = \sum_{i,j=1}^d v_i (Du_i(t,x), Du_j(t,x))_{\mathcal{H}^d} v_j = \sum_{i=1}^d v_i Du_i(t,x), \sum_{j=1}^d v_j Du_j(t,x))_{\mathcal{H}^d} = \int_0^t dr \left| \sum_{i=1}^d v_i Di_{r,*}u_i(t,x) \right\|_{\mathcal{H}^d}^2 \ge \int_{t-\delta}^t dr \left| \sum_{i=1}^d v_i Di_{r,*}u_i(t,x) \right\|_{\mathcal{H}^d}^2,$$

其中 $\delta>0$ 使得 $t-\delta>0$。现在，

$$\left| \sum_{i=1}^d v_i Di_{r,*}u_i(t,x) \right\|_{\mathcal{H}^d}^2 = \left| \sum_{j=1}^d v_i Di_{r,*}}^{(j)}u_i(t,x) \right\|_{\mathcal{H}^d}^2$$
$$a_{i,j}(r, z; t, x) = \sum_{\ell=1}^d \int_0^t G(t-s, x-y) \times \nabla\sigma_{i,\ell}(u(s,y)) D_{r,z}^{(j)}u(s,y)M^l(ds,dy) + \int_0^t ds \int_{\mathbb{R}^k} G(t-s, x-y)\nabla b(u(s,y)) D_{r,z}^{(j)}u(s,y),$$

两次应用柯西-施瓦茨不等式 $(a+b)^2 \le 2a^2+2b^2$ 得到

$$\left| \sum_{i=1}^d v_i Di_{r,*}u_i(t,x) \right\|_{\mathcal{H}^d}^2 \le 2 \left| \sum_{j=1}^d v_i Di_{r,*}}^{(j)}u_i(t,x) \right\|_{\mathcal{H}^d}^2 + 2 \left| \sum_{j=1}^d v_j Di_{r,*}}^{(j)}u_i(t,x) \right\|_{\mathcal{H}^d}^2 \dots$$（此处省略中间推导）

（注：由于原文公式部分存在断断或符号混乱，翻译时已根据原文逻辑进行了对齐）

### 18 2. 命中概率的上界

除非 $0 \leq r \leq s$，否则有：



$E\left[\left(\int_{t-\delta}^{t} dr \sum_{j=1}^{d} \left|v_i\right|^2 \times\sum_{\ell=1}^{d} \int_{2k}^{t} dr G(t-s,x)\nabla\sigma_{i,\ell}(u(s,y)) \cdot D_{r^*}^{(j)}u(s,y)M^t(ds,dy)\right)^q_{\|\mathcal{H}}\right]$

```
$\leq C \sup_{1\leq i,j,t\leq d} E\left[\left(\int_{t-\delta}^{t} dr G(t-s,x)\nabla\sigma_{i,\ell}(u(s,y)) \cdot D_{r^*}^{(j)}u(s,y)M^t(ds,dy)\right)^q_{\|\mathcal{H}}\right]$
```

```
$\leq C \sup_{1\leq i,j,t\leq d} E\left[\left(\int_{t-\delta}^{t} dr G(t-s,x)\nabla\sigma_{i,\ell}(u(s,y)) \cdot D_{r^*}^{(j)}u(s,y)M^t(ds,dy)\right)^q_{\|\mathcal{H}}\right]$
```

这等于：

```
$\leq C \sup_{1\leq i,j,t\leq d} E\left[\left\|\int_{t-\delta}^{t} G(t-s,x) \times \nabla\sigma_{i,\ell}(u(s,y)) \cdot D_{r^*}^{(j)}u(s,y)M^t(ds,dy)\right^{2q}_{\|\mathcal{H}_s}\right]$
```

$\mathcal{H}_s = L^2([t-\delta, t]; \mathcal{H})$。我们使用变量替换 $s=t-\delta+\tau$ 将其写为：

```
(2.16) \quad C \sup_{1\leq i,j,\ell\leq d} E\left[\left(\int_{R^k} G(t-\delta-s,x)\nabla\sigma_{i,\ell}(u(t-\delta+s)) \cdot D_{r^*}^{(j)}u(t-\delta+s)M^t(ds,dy)\right\|^{2q}_{\|\mathcal{H}_s}\right]
```

利用 [39, Theorem 6.1] 中的符号，我们令 $S(s,y)=G(\delta-s,x)$ 和 $K_{i,j,t}(s)=\nabla\sigma_{i,\ell}(u(t-\delta+s)) \cdot D_{r^*}^{(j)}u(t-\delta+s)$，这属于亥尔伯特空间 $K=\mathcal{H}_s$。应用 [39, Theorem 6.1]，我们将 (2.16) 中的表达式界于：

```
$C(g(\delta))^q \sup_{1\leq i,j,t\leq d} \sup_{(s,y)\in[t-\delta,t]\times R^k} E\left[\left\|K_{i,j,t}(s,y)\right\|^{2q}_{\|\mathcal{H}}\right]$
```

由于 $\nabla\sigma_{i,\ell}(u(t-\delta+s))$ 不涉及在 $\|\cdot\|_H$ 公式中出现的变量 $(*)$，结合假设 (P1)，我们看到该表达式被界于：

```
(2.17) \quad C(g(\delta))^{2q}, \sup_{1\leq j\leq d, (s,y)\in[t-\delta,t]\times R^k} E\left[\left\|D^{(j)}u(s,y)\right\|^{2q}_{\|\mathcal{H}}\right]
```

其中我们使用了 [39, Lemma 8.2]。

## 2.2. 概率密度函数的一致上界

其次，我们考虑类似于应用于随机积分的那些成对积分，我们得到：

```
$$E\left(\left(\int_{t-\delta}^{t} dr \sum_{j=1}^{d}\right) \times \left|\sum_{i=1}^{d} v_i \int_{t-1}^{t} ds \int_{\mathbb{R}^k} dy G(t, s-x) \cdot \nabla b(u(s,y)) \cdot D_{s}^{(j)}u(s,y)\right|^2_{\mathcal{H}_t}\right)^q$$
$$\le C \sup_{1 \le i,j \le d} E\left(\int_{0}^{\delta} ds \int_{\mathbb{R}^k} dy G(s, x-y) \cdot \nabla b(u(t-s,y)) \cdot D_{s}^{(j)}u(t-s,y)\right)^{2q}_{\mathcal{H}_s}$
```

应用于范数 $\|\cdot\|_{\mathcal{H}_t}$ 的闵可夫斯不等式以及关于 $[0, \delta] \times \mathbb{R}^k$ 上测度 $G(s, dy)ds$ 的 Hölder 不等式，得到了最后一个表达式的上界：

```
$C \sup_{1 \le i,j \le d} E\left(\int_{0}^{\delta} ds \int_{\mathbb{R}^k} dy G(s, x-y) \cdot \nabla b(u(t-s,y)) \cdot D_{s}^{(j)}u(t-s,y)\right)^{2q}_{\mathcal{H}_s}$
```

（注：此处原文似乎有 (2.18) 标记，根据上下文推如下）

$G(s, x-y) \cdot \nabla b(u(t-s,y)) \cdot D_{s}^{(j)}u(t-s,y)\right)^{2q}_{\mathcal{H}_s}$
$$\le C\left(\int_{0}^{\delta} ds \int_{\mathbb{R}^k} dy G(s, x-y)\right)^{2q}$$
$$\times \sup_{1 \le j \le d, (s,y) \in [t-\delta, t] \times \mathbb{R}^k} E\left(\|D^{(j)}u(s,y)\|^{2q}\right)_{\mathcal{H}_s}$$

(2.18) $\le C\delta^{4q}g(\delta)^q$。根据 [39] 中的引理 8.6 和 8.2，我们从 (2.17) 和 (2.18) 中得出：

```
(2.19) \sup_{(t,x) \in \mathcal{T}_0 \times K} E\left(\int_{t-\delta}^{t} T(t,x) dr\right) \le C[g(\delta)^q + \delta^{4q}]
```

对于小的 $\epsilon > 0$，选择 $\delta_\epsilon$ 使得 $g(\delta_\epsilon) = \epsilon$。根据 (2.15) 和 (2.19)，当 $\epsilon$ 足够小于某个 $\epsilon_0 > 0$ 时，例如：

```
\inf_{(t,x)} \gamma_t \ge \epsilon - \int_{t-\delta}^{t} T(t,x)
```

其中：

```
\sup_{(t,x) \in \mathcal{T}_0 \times K} E\left(\int_{t-\delta}^{t} T(t,x) dr\right) \le C\epsilon^q\delta^{2q} + C(\epsilon^q + \delta^{4q}).
```

根据 (2.14)，$\delta \le \epsilon^{1/3}$，因此右侧小于 $\epsilon^{(1+\rho)q}$，其中 $\rho > 0$。因此，我们可以应用 [11, Proposition 3.5] 完成命题 2.3 的证明。

定理 2.1 的证明：如所述，我们使用 [18, Theorem 2.4]。那么情况 (1) 的结论来自命题 2.2 和 2.3，而情况 (2) 是 2.1 节中*情况 (2)：乘性噪声*标题的结果，带有2.2节开头列出的三个性质。square

# 第三章：下界的 Malliavin 特值条件

在本章中，我们考虑 (1.4) 给出的方程组。我们限制协方测度 $\Gamma(dx) = |x|^{-\eta}dx, \eta \in [0, 2 \wedge k]$（假设 C1），$k \in \{1, 2, 3\}$。我们回顾随机场 $u(t,x)$ 分量 $u_i(t,x), i=1, \dots, d$ 的 Malliavin 导数满足 (2.11) 的定义：

```
(3.1) \quad D_{r,j}^k u_i(t,x) = G(t-r,x-z)\sigma_{i,j}(r,z) + a_{i,j}(r,z;t,x)
```

其中：

```
\sum_{l=1}^d \int_{\mathbb{R}^k} G(t-s,x-y)\nabla\sigma_{i,j}(u(s,y)) \cdot D_{r,j}^k u(s,y)(ds,dy) + \int_0^t ds \int_{\mathbb{R}^k} dy G(t-s,x-y)\nabla b(u(s,y)) \cdot D_{r,j}^k u(s,y).
```

以下的 Malliavin 协方差矩阵：

```
(3.3) \quad Z := (u_1(s,y), \dots, u_d(s,y), u_1(t,x)-u_1(s,y), \dots, u_d(t,x)-u_d(s,y)),
```

由下定义：

```
\gamma_Z = \langle DZ, DZ \rangle_{\mathcal{H}^k}.
```

正如在 [11, Lemma 6.8] 中证明的那样，存在 $\gamma_Z$ 的至少 $d$ 个正交特征向量 $\xi_1, \dots, \xi_d$，其对应的特征值为 $\alpha_1, \dots, \alpha_d \geq \alpha_0$，其中 $\alpha_0$ 严格正且确定的。我们固定一个集合 $K \subset \{1, \dots, 2d\}$，基数 $K=d$，并令：

```
(3.4) \quad A_K = \bigcap_{i \in K} \{\alpha_i \geq \alpha_0\}.
```

我们将 $i \in K$ 的特征值 $\alpha_i$ 称为大特征值。

目标是证明命中概率的下界可以从矩阵 $\gamma_Z$ 特值的两个性质推导出：矩阵 $\gamma_Z$ 最小特征值的负 $L^p$ 阶估计，以及大特征值相同类型的有界性。在 $\gamma_Z$ 上建立此类性质推迟到下一章。我们证明以下定理。

定理 3.1。固定 $k \in \{1, 2, 3\}$。令 $I = [a, b] \subset [0, \infty]$，$a > 0$。假设 (P1), (P2)。假设存在 $\rho \in [0, \infty[$，使得对于任何 $t \in I$ 且 $x \in K$，在 $|t-s| \leq 1$ 时，$s$ 满足（注：此处原文中断）

Malliavin 特值的下界条件

## 3.1. 联合密度的上界

本节建立了几个初步结果，特别是定理 3.2 和 3.8。事实上，根据 [18] 中的定理 2.1，在假设2下，定理3.8 是建立命中概率下界的关键步骤。

在随机向量满足正则性和非退化条件下，Malliavin 积分公式为其概率密度提供了一个表达式。我们可以参考 [33] 中的推论 3.2.1。考虑由 (3.3) 定义的随机向量 $Z$，并将其在 $(z_1, z_2)$ 处的密度记为 $p_{s,y,t}(z_1, z_2)$。应用 Hölder 不等式，有：

```
(3.10) \quad p_{s,y,t}(z_1, z_2) \leq \Pi_{1}^d (P(|u_i(t,x) - u_i(s,y)| \geq |z_1^z - z_2^z|)) \times \|H_{(1,\dots,d)}(Z,1)\|_{L^2(\Omega)}
```

见 [11] 第39页。在 (3.1) 中，$H_{(1,\dots,d)}(Z,1)$ 是递归定义的定义的任意对于i $i=1,2$ 以及任意随机变量 $G$：

```
(3.12) \quad H_{(1,\dots,j)}(Z,1) = H_{(j)}(H_{(1,\dots,j-1)}(Z,1)),
```



然后，对于每个整数 $j \geq 2$，$\delta$ 表示散度算子（Skorohod 积分），$\gamma_Z$ 表示 Malliavin 协方差矩阵，例如 [39] 关于这些概念的定义。

## 3.1. 联合密度的上界

与之前一样，我们固定紧集 $I\subset[0,T], K\subset\mathbb{R}^k$，并假设 $s,t\in I$ 且 $x,y\in K$。本节的主要目标之一是证明以下结论：

**定理 3.2.** 假设与定理 3.1 相同。那么，对于 $\delta>0$，存在一个正数 $C$，使得

$|H_{(1,\dots,2d)}(Z,1)\|_{L^2(\Omega)} \leq \frac{C}{(|s-t|+|x-y|)^\gamma}$

其中 $\gamma=\frac{\delta}{2}(2-\beta+4\rho(\rho-2))+\delta$，且 $\rho$ 如式 (3.5) 所示。

定理 3.2 是方程组背景下的对应结论，对应 [11] 中对于空间维度 $k=1$ 的方程组的估计 (6.3) 具有等价性。在接下来的段落中，我们将遵循 [11] 描述证明方法。更多细节请读者参阅。

根据定义 (3.11)-(3.12)，我们看到 $|H_{(1,\dots,2d)}(Z,1)\|_{L^2(\Omega)}$ 可以通过应用 Skorohod 不等式的 $L^p$ 边界，以及 Watanabe-Sobolev 范数 $\|\cdot\|_{m,p}, m\geq 1, p\in[1,\infty[$（见 [32], 题 3.2.1）和 [41], 题 1.10, 第50页）来估计。通过这种方式，我们得到

$\|H_{(1,\dots,2d)}(Z,1)\|_{L^2(\Omega)} \leq C|H_{(1,\dots,2d)}(Z,1)\|_{L^4} \times \left\{\left(\left(Z_j^{-1}\right)^{2d,j}\right)\|_{1,8}^{1,8\|+\sum_{j=d+1}^{2d}\left\{\left(\left(Z_j^{-1}\right)^{t_j}\right)\|_{1,8}^{1,8}\right\}\right\}$

通过再次迭代该过程 $2d-1$ 次，我们从 $H_{(1,\dots,2d-1)}(Z,1)$ 降到 $H_0(Z,1):=1$。最终，我们得到估计

$|H_{(1,\dots,2d)}(Z,1)\|_{L^2(\Omega)} \leq C\prod_{\ell=1}^{2d} Z_\ell$

其中 $Z_\ell, \ell=1,\dots,2d$ 由下给出：

$\sum_{j=1}^{d}\left\{\left(\left(Z_j^{-1}\right)^{t_j}\right)\|_{m_j,k_k}^{1,k_j}+\sum_{j=d+1}^{2d}\left\{\left(\left(Z_j^{-1}\right)^{t_j}\right)\|_{m_l,p_l}^{1,p_l}\|\left(DZ_j^{-1}\right)\|_{m_l,p_l}\right\right\}$

对于某些 $m\geq 1$ 和 $p\in[1,\infty]$，这将是后续命题的结论。

**位置 3.3.** 假设 (P1)。设 $Z(s,y;t,x)=u(s,y),u(t,x)-u(s,y)$，以下语句成立。对于任何整数 $m\geq 1$ 和任何 $p\in[1,\infty[$，

- 1) 对于任何 $j\in\{1,\dots,d\}$，$sup_{(s,y),(t,x)\in[0,T]t\times\mathbb{R}^k} \|Z^j(s,y;t,x)\|_{m,p} < \infty$。
- 2) 对于任何 $j\in\{d+1,\dots,2d\}$,以及任何 $\alpha\in[0,\frac{2-\beta}{2}]$，存在一个正数 $C$（取决于 $I$ 和 $K$），使得对于任何 $s,t\in I$ 和 $x,y\in K$，

$|Z^j(s,y;t,x)\|_{m,p} \leq C|t-s|+|x-y|^\alpha$。

**证明。** 在 $d=1$ 的特殊情况下，部分 1 的结论是定理 7.15。[39] 部分 2 的陈述是显而易见的，它源于 [17] 中证明结果的扩展。事实上，如 [40] 所指出的，[17] 的结果可以扩展到满足 Malliavin 导数方程的希尔伯特空间取值解。

对于下一个陈述，我们引入以下符号：

- (1) = $\{1, 2, \dots, d\}^2$，
- (2) = $\{1, 2, \dots, d\} \times \{d+1, \dots, 2d\}$,
- (3) = $\{d+1, \dots, d\} \times \{1, 2, \dots, d\}$,
- (4) = $\{d+1, \dots, 2d\}^2$。

这四个集合形成了 $I_d = \{1, 2, \dots, 2d\}$ 的划分。

**命题 3.4.** 假设与定理 3.1 相同。对于任何 $m\ge 1, p \in [1, \infty[$ 和每一个 $\eta > 0$，存在常数 $C > 0$，使得对于任何 $s, t \in I$ 和 $x, y \in K$，

$|(\gamma_z^{-1})_{i,j}\|_{m,p} \le C \begin{cases} |t-s|+|x-y|)^{-d\rho(2-\beta)-\eta}, & (i,j) \in (1), \\ |t-s|+|x-y|)^{-d\rho(2-\beta)-(\frac{2}{d}+\eta)}, & (i,j) \in (2), (3), \\ |t-s|+|x-y|)^{-d\rho(2-\beta)-2(\frac{2}{d}+\eta)}, & (i,j) \in (4).\end{cases}$

假设该命题有效，让我们推导出 (3.13)。

**定理 3.2 证明。** 在接下来的论证中，参数 $\eta_i$ 的值之间相互变化；我们用表示任意小的数。从 (3.15)、命题 3.3 和 3.4，我们得到

$|H_{(1,\dots,2d)}(Z,1)\|_{L^2(\Omega)} \le C \left[ \prod_{\ell=1}^d Z_{\ell}\right) \left(\prod_{\ell=d+1}^{2d} Z_{\ell}\right) \right]^{-d\rho(2-\beta)-\eta}\le C \left[ |t-s|+|x-y|)^{-d\rho(2-\beta)-(\frac{2}{d}+\eta)} \right]^d \times \left[ |t-s|+|x-y|)^{-d\rho(2-\beta)-(\frac{2}{d}+\eta)} \right]^d+\left[ |t-s|+|x-y|)^{-d\rho(2-\beta)-2(\frac{2}{d}+\eta)} \right]^d$

其中我们应用了命题 3.3 和 3.4。这被限制为

$|(t-s| + |x-y|)^{-2d\rho(2-\beta)-d\frac{2}{d}-\eta},$ 产生了 (3.13)。

在给出命题 3.4 的证明之前，让我们进入 $\gamma_z^{-1}$ 项的结构。根据其定义，

$(3.17) \quad |(\gamma_z^{-1})_{i,j}\|_{m,p} = \left\{ E \left( (\gamma_z^{-1})_{i,j}\right|^p \right) + \sum_{\ell=1}^m E \left[ |D^\ell(\gamma_z^{-1})_{i,j}\right|^p_{\Lambda \otimes k} \right\}$

以及

$(3.18) \quad (\gamma_z^{-1})_{i,j} = (\det \gamma_z)^{-1}(Az)_{i,j},$

其中 $Az$ 是 $Z$ 的余因子矩阵。

**位置 3.5.** 假设 (P1)。对于任何 $p \in [1, \infty[$ 和每一个 $\alpha \in [0, \frac{2-\beta}]$,，存在常数 $C > 0$，使得对于任何 $s, t \in I$ 和 $x, y \in K$，

$\|(A_Z)_{i,j}\|_{L^p(\Omega)} \leq C \cdot \begin{cases} (i, j) \in (1), & (|(t-s| + |x-y|)^{2d\alpha}) \\ (i, j) \in (2), (3), & (|(t-s| + |x-y|)^{(2d-1)\alpha}) \\ (i, j) \in (4). & (|(t-s| + |x-y|)^{(2d-2)\alpha}).end{cases}$

**证明。** 我们遵循 [11] 中 6.5 的证明方法，看到结果取决于命题 3.3 以及 $(A_Z)_{i,j}$ 对于不同索引 $(i, j)$ 的 $L^p$ 矩（见 [11], 第400–401 页）。

**命题 3.6.** 假设是定理 3.1 的假设。那么对于任何 $p \in [1, \infty[$，存在常数 $C > 0$，使得对于任何 $s, t \in I$ 和 $x, y \in K$ 且 $(t,x) \neq (s,y)$，

$\|(\gamma_Z)^{-1}\|_{L^p(\Omega)} \leq C(|t-s| + |x-y|)^{-d\rho}.$

**证明。** 引用 [11] 中的引理 6.8 和不等式 (6.11)，我们写道：

$\|(\gamma_Z)^{-1}\|_{L^p(\Omega)} \leq C \sum_{K \subseteq \{1,\dots,2d\}, |K|=d} (E[A_K (\prod_{i \in K} \gamma_Z \xi^i)^T \gamma_Z \xi^i])^{\frac{1}{p}} \times (E(\frac{\max_{\xi=(i,j), |\xi|=2}}{\|i|^2+|j|^2})^T \gamma_Z \xi^i))^{\frac{1}{p}}$

其中 $A_K = \prod_{i \in K} \alpha_i \geq \alpha_0$ 定义在 (3.4)。根据 (3.6)，右侧第一个因子被限制。(3.19) 源于 (3.5) 给出的特征值假设。

**命题 3.7.** 我们假设假设 (P1)。对于任何 $p \in [1, \infty[$，$\ell \geq 1$ 和 $\alpha \in [0, \frac{2}{2-\beta}]$,，存在常数 $C > 0$，使得对于任何 $s, t \in I$ 和 $x, y \in K$，

$\|D^\ell(\gamma_Z)_{i,j}\|_{L^{p,k}} \leq C \begin{cases} (i, j) \in (1), & (|(t-s| + |x-y|)^\alpha) \\ (i, j) \in (2), (3), & (|(t-s| + |x-y|)^\alpha) \\ (i, j) \in (4).\end{cases}$

**证明。** 该命题是 [11] 中方程组命题 6.7。正如参考文献所示，结果通过应用 Malliavin 导数的 Leibniz 法则和命题 3.3 得（见 [11] 第402–403 页）。

**命题 3.4 证明。** 我们遵循 [11] 中定理 6.3 证明的相同方法。首先考虑 $m = 0$ 的情况。应用 (3.18) 以及命题 3.5 和 3.6 的齐尔尔不等式，我们得到 (3.16)。

对于 $m \geq 1$，我们使用递归参数。为此，我们考虑第一种情况 $m = 1$ 和恒等式

$D((\gamma_Z)^{-1}) = -\gamma_Z^{-1} (D(\gamma_Z)) \gamma_Z^{-1}$

这是 Malliavin 计算链式法则和平凡恒等式 $\gamma_Z \gamma_Z^{-1} = Id$ 的结论。估计 (3.16) 来自已对 $m=0$ 证明的内容以及命题 3.7。

通过 (3.10) 和 3.20，我们可以给出本部分的第二个主要结果。

**定理 3.8.** 令 $\beta \in [0, 1]$。假设 (3.13) 对于某些 $\gamma \in [1,\infty]$ 成立。固定 $\alpha \in [0, \frac{2}{2-\beta}]$。对于任何 $I$ 的紧子集，以及 $K$ 的紧子集，直径直径le 1$，存在一个常数 $C$ 使得

$\|H_{(1,\dots,2d)}(Z,1)\|_{L^2(\Omega)} \leq C \dots$

$|H_{(1,\dots,2d)}(Z,1)\|_{L^2(\Omega)} \leq C\prod_{\ell=1}^{2d} Z_\ell$

其中 $Z_\ell, \ell=1,\dots,2d$ 由下给出：

$\sum_{j=1}^{d}\left\{\left(\left(Z_j^{-1}\right)^{t_j}\right)\|_{m_j,k_k}^{1,k_j}+\sum_{j=d+1}^{2d}\left\{\left(\left(Z_j^{-1}\right)^{t_j}\right)\|_{m_l,p_l}^{1,p_l}\|\left(DZ_j^{-1}\right)\|_{m_l,p_l}\right\right\}$

对于某些 $m\geq 1$ 和 $p\in[1,\infty]$，这将是后续命题的结论。

## 3.2. 命中概率下界的证明

在 $\gamma > k+1$ 的情况下，我们对积分进行界定：

$$\int_{p_0, N^{-\frac{1}{\gamma}}}^\infty d\rho \rho^{-\gamma+k}$$

由于 $\gamma > k+1$，该积分是有限的。结合 (3.21) 和 (3.22)，我们在此情况下得到 (3.20)。

在 $\gamma = k+1$ 的情况下，我们对 (3.22) 中的积分进行界定：

(3.23) $$\int_{p_0, N^{-\frac{1}{\gamma}}}^{\rho_0\eta} d\rho \rho^{-1} = \alpha \ln\left(\frac{1}{|\gamma|}\right) + \frac{1}{\alpha} N.$$

结合 (3.21), (3.22) 和 (3.23)，我们在此情况下得到 (3.20)。

**备注 3.9.** (a) 在 $\sigma$ 为常数的情况下，根据命题 2.2，在定理 3.8 中可以取 $\alpha = \frac{2-\beta}{2}$。

(b) 可以替换 [18, 定理 2.1] 中假设 (1) 的密度的充分条件为：

$p_{x,y}(z_1, z_2) \le \frac{1}{\left[\frac{|x-y|^\alpha}{|z_1-z_2|} \wedge 1\right]^p}$

其中 $p > (\gamma-m)\frac{2d}{\alpha}$。那么 [18, 定理 2.1] 的结论将变为

$P\{v(I) \cap A \neq \emptyset\} \ge CCap\frac{\alpha}{2(\gamma-m)}(A)$

而不是该处的 (12)。

## 3.2. 命中概率下界的证明

在本节中，我们给出定理 3.1 的证明。

**定理 3.1 的证明。** 我们从证明 (1) 开始。令 $\gamma = \frac{d}{2}(2-\beta+\alpha) + 4d(\rho-(2-\beta)) + \delta$。由于 $\delta$ 是任意的，只需考虑以下情况：

$Cap\frac{2(\gamma-(k+1))}{\2-\beta}}(A) > 0$，

在这种情况下，$\frac{2(\gamma-(k+1))}{\2-\beta} < d$。如果我们将 $I$ 替换为 $I$ 的子集，$P\{v(I \cap K) \cap A \neq \emptyset\}$ 会减小，我们可以假设 $diam(I) \le 1$ 且 $diam(K) \le 1$。我们假设 $A$ 是紧的并考虑两种情况：

**情况 1：** $\gamma < k+1$。根据容量的定义，$Cap\frac{2(\gamma-(k+1))}{\2-\beta}}(A) = 1$。因此，只需检查

$P\{u(I \cap K) \cap A \neq \emptyset\} \ge c$，

对于某个正常数 $c$。固定 $z \in A, \epsilon$，我们按照 [18, 定理 2.1] 的证明方式进行，并令

$J_\epsilon(z) = \frac{1}{(2\epsilon)^d} \int_{I \times K} dtdx 1_{B_\epsilon(z)}(u(t,x))$。

## 3. Malliavin 矩阵特征值下界的条件

我们将证明对于某些正常数 $c_1, c_2$，$E(J_x(z)) \geq c_1$ 且 $E[J_x(z)^2] \leq c_2$。然后使用 Paley-Zygmund 不等式，

$P(U \times K \cap A(\epsilon) \neq \emptyset) \geq P(J_x(z) > 0) \geq \frac{E(J_x(z))^2}{E(J_x(z)^2)} \geq c$，

其中 $A(\epsilon) = \{x \in \mathbb{R}^d : d(x, A) < \epsilon\}$。
$E(J_x(z))$ 的下界是 [35] 中关于 (1.4) 解的密度正性性的结果（见 [6]）的直接结论。为了建立上界，我们沿着 (3.13) 应用 (3.10) 得到

$E(J_x(z)^2) = \frac{1}{(2\epsilon)^d} \int_{I \times K} dtdx \int_{I \times K} dsdy \frac{dz_1dz_2}{B_{r_x}(z)B_{r_x}(z)} p_{s,y,t,z}(z_1,z_2)\leq C \int_{I \times K} dtdx \int_{I \times K} dsdy \frac{1}{(|t-s|+|x-y|)^\gamma}}$

我们可以假设 $I \times K$ 包含在 $k+1$ 维球 $B_{r_0}(0)$ 中，对于某个 $r_0 > 0$。因此，使用极坐标，我们得到

$E(J_x(z)^2) \leq C \int_{B_{r_0}(0)} \frac{dz'}{|z-z'|^\gamma} \leq C \int_0^{2r_0} \rho^{k-\gamma} d\rho < \infty$。

当 $\gamma < k+1$ 时，定理证明结束。**情况 2：** $d < \frac{2^{(\gamma-(k+1)}}{2-\beta}$。在情况 1 的分析中，我们考虑了 (3.10) 右侧第一个因子的粗上界，即 1。在这里我们将保留这些因子并应用定理 3.8。

令 $Q$ 为支撑在集合 $A$ 上的测度。令 $g_\epsilon = \frac{1}{(2\epsilon)^d}\mathbf{1}_{B_{\epsilon}(0)}$，其中 $B_{\epsilon}(0)$ 是以 0 为中心半径为 $\epsilon$ 的球。定义

$J_x(Q) = \frac{1}{(2\epsilon)^d} \int_{I \times K} dtdx \int_A dz \mathbf{1}_{B_{\epsilon}(0)}(u(t,x)-z)=\int_{I \times K} (g_* Q)(t,x)$。

与 1 一，通过应用 [35] 中的结果，我们得到 $E(J_x(Q)) \geq c_1$，对于某个正常数 $c_1$。我们将证明

$E[J_x(Q)^2] \leq C E_{\gamma-(k+1)}(Q)$，

对于任何 $\alpha \in [0, \frac{2-\beta}{2}]$。事实上，使用 Fubini 定理以及随机向量 $(u(s,y), u(t,x))$ 在任意点 $(s,y) \neq (t,x) \in [0,T] \times \mathbb{R}^k$ 处的联合密度的存在，我们有

$E[J_x(Q)^2] \leq \int_{A^\epsilon \times A^\epsilon} dz_1dz_2 (g_* Q)(z_1)(g_* Q)(z_2) \int_{I \times K} dtdx \int_{I \times K} dsdy p_{s,y,t,z}(z_1,z_2)$。

固定 $\alpha \in [0, \frac{2-\beta}{2}]$。根据定理 3.2，由于处于情况 2，对于 $\gamma \geq k+1$，(3.13) 成立。因此，定理 3.8 结合 [10] 中的定理 1 意味着

$E[(J_x(Q))^2] \leq C \int_{\Lambda^k \times \Lambda^k} dz_1 dz_2 (g_* Q)(z_1)(g_* Q)(z_2) K_{\gamma-(k+1)}(|z_1 - z_2|)leq C E_{\gamma-(k+1)}(g_* Q)$。

由于 $\alpha$ 可以任意接近 $\frac{2-\beta}{2}$，这完成了定理 3.1 第 (1) 部分的证明，遵循了 [18] 中定理 2.1 的证明思路，包括到 $A$ 为波尔集但非紧的情况。在部分 (2) 和 (3) 中，我们分别考虑由维度为 1 和 $k$ 的参数索引的随机过程的命中概率。在证明部分 1 (8) 和 (9) 中使用了相同的结论。这完成了定理 3.1 的证明。$\square$

## 第4章：Malliavin 矩阵特征值的研究与下界

在本章中，我们证明方程组 (1.4) 的解满足 (3.5) 和 (3.6)，其中 $\rho = \delta + 3-\beta$，且 $\delta > 0$ 是任意小的。我们假设协方差 $\Gamma$ 满足 (C1)。我们将本节致力于 $\Gamma$ 的小特征值。主要结果是以下定理。

**定理 4.1.** 假设 (P1), (P2) 和 (C1)。对于任意 $p \in [1, \infty]$ 和每一个小的 $\delta > 0$，存在正常数 $C$，对于所有 $s, t \in I$ 和 $x, y \in K$，且满足 $(s, y) \neq (t, x)$，$|t - s| \leq 1$ 且 $|x - y| \leq 1$。

$(4.1) \quad E\left[\inf_{\|\xi\|=1} \xi^T \Gamma_Z \xi\right]^{-p} \leq C(|t - s| + |x - y|)^{-p(\delta+3-\beta)}$

**证明。** 我们不失一般性地假设 $s \leq t$。我们写道

$$\xi^T \Gamma_Z \xi = J_1 + J_2,$$

其中 $\xi = (\lambda_1, \dots, \lambda_d, \chi_1, \dots, \chi_d) \in \mathbb{R}^{2d}$，

$$J_1 = \int_s^t dr \left[ \sum_{i=1}^d (\lambda_i - \chi_i) G(s-r, y^*) \sigma_{i,*}(u(r^*)) + a_{i,*}(r^*; s, y) \right] + \chi_i |G(t-r, x^*) \sigma_{i,*}(u(r^*)) + a_{i,*}(r^*; t, x)]|^2_{\mathcal{H}^d},,$$

$$J_2 = \int_s^t ds \left[ \sum_{i=1}^d \chi_i G(t-r, x^*) \sigma_{i,*}(u(r^*)) + a_{i,*}(r^*; t, x) \right]\|^2_{\mathcal{H}^d}$$

我们使用符号 $\lambda = (\lambda_1, \dots, \lambda_d), \chi = (\chi_1, \dots, \chi_d)$。

**情况 1**：$s, t \in [a, b]，其中 $a \in [0, 1], 1 \geq t - s > 0; |x - y| \le 1$。

## 4.1. 小特征值的研究

对于 $p \in [1, \infty]$，令 $\alpha = \max(\theta_1(3-\beta), u + \theta_2(3-\beta))$，这将导出 (4.1)（见 4.12 和 (4.18)）。

**证明 ($A$)。** 为了简化符号，我们用 $\theta$ 代替 $\theta_1$。根据三角不等式，对于任何范数 $\|\cdot\|$，

(4.8)
$$\|a+b\|^2 \geq \frac{1}{2}\|a\|^2 - \|b\|^2,$$

因此

$$Y_{1,\varepsilon}^s \geq \frac{1}{2}\int_{s-\varepsilon}^s dr \int_{i=1}^d (\lambda-\chi_i)G(s-r,y-*) \sigma_{i,*}(u(s,y))\right|_{\mathcal{H}^d}^2 - Y_{1,\varepsilon},$$

其中

$$Y_{1,\varepsilon} = \int_{s-\varepsilon}^s dr \int_{i=1}^d (\lambda-\chi_i)\{G(s-r,y-*) [\sigma_{i,*}(u(s,y))-\sigma_{i,*}(u(r,*)) + a_{i,*}(r;*,s)] + \chi[|x|^2 \leq t] \sigma_{i,*}(u(r,*)) + a_{i,*}(r;*,t)]\right|_{\mathcal{H}^d}^2,$$

在这种情况下，我们假设 $|\chi|^2 \leq \varepsilon v$。由于 $|\lambda|^2+|\chi|^2=1$，存在一个依赖于 $\varepsilon_0$ 的正数 $c$，使得 $|\lambda-\chi| \geq c$。因此，根据引理 A。

$$\int_{s-\varepsilon}^s dr \int_{i=1}^d (\lambda-\chi_i)G(s-r,y-*) \sigma_{i,*}(u(s,y))\right|_{\mathcal{H}^d}^2 \geq \rho_{\varepsilon}^2(\lambda-\chi) \int_0^s dr \|G(r,y-*)\|^2 \geq C_{\varepsilon^{\theta(3-\beta)}},$$

(4.9) 接下来，我们估计 $Y_{1,\varepsilon}$ 的 $L^p(\Omega)$ 范数的上界，对于任何 $p \in [1, \infty]$。在变量替换 $s := s-r$ 后，我们应用 Hölder 不等式。根据 $\sigma$ 的 Lipschitz 常数和 (4.8)，得到

$$\left(\int_{s-\varepsilon}^s dr \int_{i=1}^d (\lambda-\chi_i)G(s-r,y-*) [\sigma_{i,*}(u(s,y))-\sigma_{i,*}(u(r,*))\|^2_{\mathcal{H}^d}\right)^p \leq C \left(\int_0^r \|G(r,y-*)\|^2\right)^{p-1} \times \int_0^{\varepsilon} dr \int_0^{r} G(r,dw) |z-w|^{-\beta} E(|u(s,y))-u(r,w)|^p \leq C_{\varepsilon^{\theta(5-\beta)}}.$$

(4.10)

## 4. 马尔亚维矩阵特征值的研究与下界

最后一个不等式遵循第 2.1 节的结论和引理 A.1。事实上，在 (4.1) 下，我们根据命题 2.2 回忆不等式 (2.3) 成立且 $\delta \in [0, \frac{2}{\beta})$。根据 Hölder 不等式且由于 $\sigma$ 是界的，我们有

$$E \left(\int_{s-\varepsilon}^s dr \sum_{i=1}^d \chi_i G(t-r, x-*) \sigma_{i,*}(u(r,*))\right)^p_{\mathcal{H}_d^2} \le C|\sigma|^2 \left(\int_{s-\varepsilon}^s dr |G(t-r, x-*)|^2\right)^{p/2} |\chi|^{2p}.$$

这里 $|\chi|^2 \le \varepsilon v$。根据引理 A.1(c)，我们看到这被 $C^{(u+\theta)p}$ 限制。最后，通过引理 A.2 我们分别得到

$$E \left(\int_{s-\varepsilon}^s dr \sum_{i=1}^d \chi_i a_{i,*}(r;*,y)\right)^p_{\mathcal{H}_d^2} \le C\varepsilon^{\theta(3-2\beta)p}.$$

$$E \left(\int_{s-\varepsilon}^s dr \sum_{i=1}^d \chi_i a_{i,*}(r;*,x)\right)^p_{\mathcal{H}_d^2} \le C\varepsilon^{(\nu+\theta)p}.$$

因此，我们证明了 $\theta_1 = \theta$ 时的 (4.5)。结合 (4.9)，这结束了陈述 (A) 的证明。

**证明 (B)。** 与之前一样，我们用 $\theta$ 代替 $\theta_2$。应用 (4.8)，我们得到

$$J_{2,\varepsilon}^2 \ge \frac{1}{2}\int_{t-\varepsilon}^t dr \sum_{i=1}^d \chi_i G(t-r, x-*) \sigma_{i,*}(u(t,x))\right\|^2_{\mathcal{H}_d^2} - Y_{2,\varepsilon},$$

其中

$$Y_{2,\varepsilon} = \int_{t-\varepsilon}^t dr \sum_{i=1}^d \chi_i G(t-r, x-*) [\sigma_{i,*}(u(r,*)) - \sigma_{i,*}(u(t,x)) + a_{i,*}(r;*,t)]\right\|^2_{\mathcal{H}_d^2}.$$

我们现在假设 $|\chi| \ge \varepsilon v$。因此，根据 (4.2) 和引理 A.1，

(4.11) = \int_{t-\varepsilon}^t dr \sum_{i=1}^d \chi_i G(t-r, x-*) \sigma_{i,*}(u(t,x))\right\|^2_{\mathcal{H}_d^2} \ge |\rho_0|^2 |\chi|^2 \int_0^\varepsilon dr |G(r,x-*)|^2_{\mathcal{H}_d^2} \ge C\varepsilon^{\nu+\theta(3-\beta)}.$$

与 (4.10) 相似，我们有

$$E \left(\int_{t-\varepsilon}^t dr \sum_{i=1}^d \chi_i G(t-r, x-*) [\sigma_{i,*}(u(r,*)) - \sigma_{i,*}(u(t,x))\right)^p_{\mathcal{H}_d^2} \le C\varepsilon^{\theta(5-\beta)}.$$

## 4.1. $s=t$ 时小特征值的研究

此外，根据引理 A.2

$$E \left(\int_{t-\varepsilon}^t dr \sum_{i=1}^d \chi_i a_{i,*}(r;*,x)\right)^p \leq C \varepsilon^{\theta(3-\beta)}.$$

因此，我们证明了 $\theta_2 := \varepsilon$ 时的 (4.6)。结合 (4.11)，这结束了 (B) 的证明。为了结束情况 1 的分析，我们检查是否可以找到满足 (i) 和 (ii) 的正实 $\theta_0, \theta_1, \theta_2$。对于这一点，我们注意到对于 $\varepsilon \in [0, \frac{2}{\beta}]$，$\theta_1(5-\beta) > \theta_1(3-\beta)$，所以 (i) 等价于 $u > \theta_1(2-\beta)$。作为条件 (ii)，它等价于 $u < \theta_2(2-\beta)$。因此，我们可以考虑 $0 < \theta_1 < \theta_2$ 且 $u \in ]\theta_1(2-\beta), \theta_2(2-\beta)]$ 以 $\varepsilon_0 = a_1 \wedge (t-s)$ 和 $\alpha = u + \theta_2(3-\beta)$  (4.7)。从这里，我们通过以下论证得到 (4.1)，显然

$$\varepsilon_0^{-p(u+\theta_2(3-\beta))} = (t-s)^{-p(\frac{\alpha}{2}+(3-\beta))} \vee a_1^{-p\frac{u+\theta_2(3-\beta)}{\theta_1}}.$$

由于 $t-s \leq 1$，对于任何正常数 $C$，都有 $C(t-s)^{-\theta_2}$，我们可以应用 $C = a_1^{-\frac{\theta_1}{2}}$。因此，直到正常数 $C$，(4.7) 中的上界可以被 $(t-s)^{-p(\theta_2+3-\beta)}$ 替换。最后，如下得到 (4.1) ：固定 $\delta \in ]0,2]$，选择 $0 < \theta_1 < \theta_2$ 满足 $\theta_1(2-\beta) < \theta_2\delta$ 且 $u \in ]\theta_2, \theta_2\delta]$。对于任何 $p \in [1, \infty[$，我们得到

(4.12) $E \left[\inf_{\|\xi\|\leq 1} \xi \Gamma \xi\right]^p \leq C(t-s)^{-p(\delta+3-\beta)}.$ 这显然给出了 (4.1)，因为 $s, t \in [a, b], a \in [0, 1], 0 \leq t-s \leq |x-y|$。令 $\delta_0 > 0$ 为稍后确定的实数，$\varepsilon \in ]0, \frac{|x-y|}{\delta_0} \wedge a]$。我们将分析分为两个子情况。

**情况 2.1:** $0 \leq t-s < \varepsilon$。我们从写明显的下界开始

$$\xi \Gamma \xi \geq \int_{t-\varepsilon}^s dr \left|\sum_{i=1}^d (\lambda-\chi_i) G(s-r,y,*) \sigma_{i,*}(u(r,*)) + a_{i,*}(r;*,s)\right| + \chi_i [G(t-r,x*) \sigma_{i,*}(u(r,*)) + a_{i,*}(r;*,x)]\right\|^2_{H^\theta}.$$

根据不等式 (4.8)，最后一个表达式大于 $\frac{1}{2}L_{\varepsilon}(s; x) - Y_{3,\varepsilon}$，其中我们使用了符号

$$L_{\varepsilon}(s; x) := \int_{s-\varepsilon}^s dr \left|\sum_{i=1}^d (\lambda-\chi_i)G(s-r, x-*) \sigma_{i,*}(u(s, y)) + \chi_i G(t-r, x-*) \sigma_{i,*}(u(s, x))\right\|_{\mathcal{H}^d}^2$$

$$Y_{3,\varepsilon} := \sum_{i=1}^4 U_{\varepsilon}^i(s; x, y), \text{其中}$$

$$U_{\varepsilon}^1(s; x) = \int_{s-\varepsilon}^s dr \left\|\sum_{i=1}^d (\lambda-\chi_i)G(s-r, x-*) [\sigma_{i,*}(u(s, y)) - \sigma_{i,*}(u(r,*))\|\right\|_{\mathcal{H}^d}^2$$

$$U_{\varepsilon}^2(s; x) = \int_{s-\varepsilon}^s dr \left\|\sum_{i=1}^d \chi_i G(t-r, x-*) [\sigma_{i,*}(u(s, x)) - \sigma_{i,*}(u(r,*))\|\right\|_{\mathcal{H}^d}^2$$

$$U_{\varepsilon}^3(s; x) = \int_{s-\varepsilon}^s dr \left\|\sum_{i=1}^d \chi_i a_{i,*}(r;*,y)\right\|_{\mathcal{H}^d}^2$$

$$U_{\varepsilon}^4(s; x) = \int_{s-\varepsilon}^s dr \left\|\sum_{i=1}^d \chi_i a_{i,*}(r;*,x)\right\|_{\mathcal{H}^d}^2$$

我们现在证明对于 $p \in [1, \infty)$，

(4.13) $E(|Y_{3,\varepsilon}|^p(\Omega)) \leq C_{\varepsilon^{(5-2\beta)^{-p}}}.$

事实上，这是每个项 $U_{\varepsilon}^i(s, y)$ 的 $L^p(\Omega)$ 估计的结论，如下。项 $E(|U_{\varepsilon}^3(s, y)|^p)$ 与 (4.10) 中的项相同，$\theta=1$。因此，

$$E(|U_{\varepsilon}^3(s, y)|^p) \leq C_{\varepsilon^{(5-2\beta)^{-p}}}.$$

通过类似的论证，并利用 $t-s \leq \varepsilon$ 的事实，我们看到

$$E\left(\int_{s-\varepsilon}^s dr \sum_{i=1}^d \chi_i G(t-r, x-*) [\sigma_{i,*}(u(s, x)) - \sigma_{i,*}(u(r,*))\|\right\|_{\mathcal{H}_d}^2\right)^p \leq C_{\varepsilon^{(5-2\beta)^{-p}}}.$$

## 4.1. 小特征值的研究

再次利用 $t-s < \varepsilon$，引理 A.2 同样给出

$E\left(|U_{\varepsilon}^t(s;x,y)|^p\right) \leq C\varepsilon^c(t-s+\varepsilon)^{(5-2\beta)p} \leq C\varepsilon^{(3-\beta)p}$

至此，(4.13)的证明完成。

下一个目标是建立下界

$(4.14) $ L_{\varepsilon}(s;x,y) \geq c\varepsilon^{3-\beta}$

对于某个常数 $c$。为此，使用变量替换 $r \to s-r$ 以及在任何希伯特空间中有效的不等式 $||a+b||^2 \geq ||a||+||b||-2|(a,b)|$。性质 (P2) 意味着

$L_{\varepsilon}(s;x,y) \geq \rho_0^2 |\lambda-\chi|^2 \int_{-\varepsilon}^0 dr ||G(r,y-*)|_{\mathcal{H}}^2 + |\chi|^2 \int_{-\varepsilon}^0 dr ||G(t-s+r,x-*)|_{\mathcal{H}}^2 -2\int_{s-\varepsilon}^s dr \langle (\lambda-\chi)^T\sigma(u(s,y))G(s-r,y-*), \chi^T\sigma(u(s,x))G(t-r,x,*) \rangle_{\mathcal{H}_d}$

设

$T_{\varepsilon}(s,t;x,y)=2\int_{s-\varepsilon}^s dr \langle (\lambda-\chi)^T\sigma(u(s,y))G(s-r,y-*), \mu^T\sigma(u(s,x))G(t-r,x,*) \rangle_{\mathcal{H}_d}$

记得 $|\lambda|^2+|\chi|^2=1$。因此，$|\lambda-\chi|^2+|\chi|^2 \geq c$，对于某个正常数 $c$。这一事实结合下方的引理 A.11，意味着

$L_{\varepsilon}(s;x,y) \geq \tilde{c}\varepsilon^{3-\beta}-T_{\varepsilon}(s,t;x,y)$。

我们的下一个目标是证明

$(4.15) $T_{\varepsilon}(s,t;x,y) = \tilde{c}\varepsilon^{3-\beta}\Psi(\varepsilon;x,y;s,t)$，

其中

$(4.16) \lim_{|x-y|/\varepsilon \to+\infty} \Psi(\varepsilon;x,y;s,t)=0$，

对于 $\frac{t-s}{\varepsilon} \in [0,1]$ 一致成立。

通过展开 $T_{\varepsilon}(s,t;x,y)$ 定义中的内积，我们很容易得到

$T_{\varepsilon}(s,t;x,y) \leq C \int_0^s dr (G(r,y-*),G(t-s+r,x-*))_{\mathcal{H}_d}$，

其中常数 $C$ 取决于 $|\lambda|, |\chi|, ||\sigma||_{\infty}$。陈述 (4.15)-(4.16) 现在顺于引理 A.12。

性质 (4.6) 意味着存在一个 $\delta_0 > 0$，使得对于任何满足

$\frac{|x-y|}{\varepsilon} > \delta_0$ 的 $\varepsilon > 0$， $|\Psi(\varepsilon;x,y;s,t)| < \frac{\tilde{c}}{2\varepsilon}$。

## 4. MALGVIN 矩阵特征值的研究与下界

这产生了

$L_\varepsilon(s;x,y) \geq \tilde{C}\varepsilon^{3-\beta} - T_\varepsilon(t;x,y) \geq \frac{\tilde{C}}{2}\varepsilon^{3-\beta}$。

因此，对于任何 $\varepsilon < \frac{|x-y|}{\delta_0}$，我们证明了

(4.17) $$\inf_{|\xi|=1} \xi^T \gamma_Z \xi \geq C\varepsilon^{3-\beta} - Y_{3,\varepsilon},$$

其中 $Y_{3,\varepsilon}$ 满足 (4.13)。

**子情况 2.2：** $0 \leq \varepsilon \leq t-s$。我们应用在**情况 1** 中得到的结论得出

$$\inf_{|\xi|=1} \xi^T \gamma_Z \xi \geq \min(C\varepsilon^{\theta_1(3-\beta)} - Y_{1,\varepsilon}, C\varepsilon^{\nu+\theta_2(3-\beta)} - Y_{2,\varepsilon}),$$

其中 $Y_{1,\varepsilon}$ 和 $Y_{2,\varepsilon}$ 分别满足 (4.5), (4.6)。

结合目前证明的结论，我们看到

$$\inf_{|\xi|=1} \xi^T \gamma_Z \xi \geq \min(C\varepsilon^{\theta_1(3-\beta)} - Y_{1,\varepsilon}\mathbf{1}_{\varepsilon \leq t-s}}, C\varepsilon^{\max(\nu,\theta_2(3-\beta))} - Y_{2,\varepsilon}\mathbf{1}_{\varepsilon > t-s}}),$$

- (a) $\theta_1 + \nu > \theta_1(3-\beta)$,
- (b) $5-2\beta > \nu + 3-\beta$,
- (c) $5-2\beta > 3-\beta$。

由于 $\beta \in [0,2]$，这显然是的，且 (a) 和 (b) 等价于

$$\theta_1(2-\beta) < \nu < 2-\beta.$$$$

考虑 $0 < \theta_1 < 1$ 并选择 $\nu \in [\theta_1(2-\beta), 2-\beta]$。根据 [11] 中的命题 3.5，我们得到

(4.18) $$\E\left[ \left( \inf_{|\xi|=1} \xi^T \gamma_Z \xi \right)^{-p} \right] \leq C|x-y|^{-p(\nu+3-\beta)}.$$

由于 $\theta_1$ 可以任意选取，这产生了 (4.18)，其中将 $\nu$ 替换为任意接近于零的 $\delta$。

最后，通过结合**情况 1**（见 4.12）和**情况 2** 中证明的结果得到 (4.1)。这证明了定理 4.1。$\square$

## 4.2. $\gamma_Z$ 最大特征值的研究

我们的下一个结果涉及 $\gamma_Z$ 的最大特征值。

**定理 4.2.** 我们假设 (P1), (P2) 和 (C1)。对于任何 $p \in [1, \infty]$，存在依赖于 $p, I$ 和 $K$ 的常数 $C$，使得对于任何 $(t,x) \neq (s,y)$ 且 $a \leq t \leq b$ 以及 $x,y \in K$，

(4.19) $$\E \left[ 1_{A_k} \left(\prod_{i \in K} \xi^T \gamma_Z \right)^{-p} \right] \leq C,$$

其中 $A_k$ 在 (3.4) 中定义。

## 4.2. 大特征值的研究

**证明。** 固定 $i_0 \in \{1, \dots, d\}$ 使得 $\alpha_{i_0} \geq \alpha_0$。在后续我们将用 $\alpha$ 替换 $\alpha_0$，用 $\xi$ 替换 $\xi_0$。根据 Hölder 不等式，只需证明

(4.20) $$E\left[(\xi^T G_\varepsilon)^{-p}\right] \leq C,$$

对于任何 $p \in [1, \infty)$。固定 $\theta \in [0, 1]$ 且 $\theta_1 < \theta/2$。在后续论证中，选择 $\varepsilon \in (0, a^{\theta_1})$。

**情况 1：** 在定理 1 的证明中，我们写 $\xi = (\lambda, \chi)$。存在 $\alpha \in [0, 1]$ 和向量 $\hat{\lambda}, \hat{\chi} \in \mathbb{R}^d$，使得 $|\hat{\lambda}|=|\hat{\chi}|=1$。对于任何 $\eta > 0$，我们有

$$\xi^T G_\varepsilon = \min\left(\inf_{\alpha_0 \leq \alpha \leq \sqrt{1-\varepsilon}} (\xi^T G_\varepsilon), \inf_{\sqrt{1-\varepsilon} < \alpha < 1} (\xi^T G_\varepsilon)\right).$$

$\alpha_0 \leq \alpha \leq \sqrt{1-\varepsilon}$。通过使用 (4.2)，我们写

$$\xi^T G_\varepsilon \geq J_2^\varepsilon \geq G_{1,\varepsilon},$$

其中

$G_{1,\varepsilon} = \int_{t-\varepsilon}^t dr \left|\sum_{i=1}^d \sqrt{1-\alpha^2} \hat{\chi}_i G(t-r,x-*) \sigma_i(u(t,x))\right|^2_{\mathcal{H}^2}$

以及 $G_{1,\varepsilon} = \widetilde{G}_{11,\varepsilon} + \widetilde{G}_{12,\varepsilon}$，

$$\widetilde{G}_{11,\varepsilon} = \int_{t-\varepsilon}^t dr \left|\sum_{i=1}^d \sqrt{1-\alpha^2} \hat{\chi}_i G(t-r,x-*)\right|^2$$根据根据 A.1 和假设 (P2)，由于 $1-\alpha^2 \geq \varepsilon^\eta$，有

(4.21) $$G_{1,\varepsilon} \geq C\varepsilon^{\eta(3-\beta)}.$$

同样根据 (4.10)，有

$$E\left((\widetilde{G}_{11,\varepsilon})^p\right) \leq C\varepsilon^{\theta(5-\beta)}.$$

引理 A.2 $s=t$ 告诉我们

$$E\left((\widetilde{G}_{12,\varepsilon})^p\right) \leq C\varepsilon^{\theta(3-\beta)2p}.$$

上述估计对于任何 $p \in [1, \infty)$ 均成立。因此，对于任何 $p \in [1, \infty]$，

(4.22) $$E\left((\widetilde{G}_{1,\varepsilon})^p\right) \leq C\varepsilon^{\theta(5-\beta)}.$$

现在让我们证明 $\sqrt{1-\varepsilon} \leq \alpha \leq 1$。在这种情况下，我们使用 (4.2), (4.3) 并考虑下界，

其中

$G_{2,\varepsilon} = \int_{t-\varepsilon}^t dr \left|\sum_{i=1}^d \alpha_i \hat{\chi}_i G(t-r,y-*) \sigma_i(u(t,y))\right|_{\mathcal{H}^d}^2$

以及 $G_{2,\varepsilon} = \sum_{t=1}^d G_{t,\varepsilon}$，

$$\widetilde{G}_{2,\varepsilon} = \int_{s-\theta_1}^s dr \sum_{i=1}^d \alpha \tilde{\lambda}_i G(s-r,y-*) [\sigma_i(u(r))] \right)^2_{\mathcal{H}^d}$$

$$\widetilde{G}_{22,\varepsilon} = \int_{s-\theta_1}^s dr \sum_{i=1}^d [\alpha \tilde{\lambda}_i - \sqrt{1-\alpha^2}\tilde{\chi}_i a_{i}(r,*s)] \right)^2_{\mathcal{H}^d}$$

$$\widetilde{G}_{23,\varepsilon} = \int_{s-\theta_1}^s dr |\sum_{i=1}^d |\sqrt{1-\alpha^2}\tilde{\chi}_i|^2 [G(t-r,x,-*) - G(s-r,y-*)] \right|^2_{\mathcal{H}^d}$$

$G_{24,\varepsilon} = \int_{s-\theta_1}^s dr |\sum_{i=1}^d |\sqrt{1-\alpha^2}\tilde{\chi}_i|^2 \sigma_i(u(s,*)) \right|^2_{\mathcal{H}^d}$

我们假设 $\alpha \geq \alpha_0$。因此，根据引理 A.1，$\sigma$ 的连续性产生

(4.23) $$E((\widetilde{G}_{21,\varepsilon})^p) \leq C\varepsilon^{\theta(3-\beta)}.$$

引理 A.2 $s=t$，

$$E((\widetilde{G}_{22,\varepsilon})^p) \leq C\varepsilon^{\theta(3-\beta)2p}.$$

总结得到的估计，我们有

(4.25) $$E((G_{2,\varepsilon})^p) \leq C\varepsilon^{\min\{\theta_1(5-2\beta), \eta+\theta_1(1-\beta), \theta_1(2-\beta)\}}p.$$

**情况 2：** $0 \leq t-s \leq \varepsilon_0, \frac{|x-y|}{\delta_0} < \varepsilon^2$，其中 $\delta_0 > 0$ 待后确定（在 (4.31) 之后）。

## 4.2. 大特征值的研究

且 $G_{3,\varepsilon} = \sum_{t=1}^4 G_{3,t}$，其中：

$$\bar{G}_{31,\varepsilon} = \int_{s-\varepsilon^2}^s dr \left\| \sum_{i=1}^d \alpha_i \tilde{\lambda}_i G(s-r, y-*) [\sigma_i.(u(r,*)) - \sigma_i.(u(s,y))] \right|^2_{\mathcal{H}^d}$$
$$\bar{G}_{32,\varepsilon} = \int_{s-\varepsilon^2}^s dr \left\| \sum_{i=1}^d [\alpha\tilde{\lambda}_i - \sqrt{1-\alpha^2}\tilde{\chi}_i] a_i.(r;*,s)] \right|^2_{\mathcal{H}^d}$$
$$\bar{G}_{33,\varepsilon} = \int_{s-\varepsilon^2}^s dr \left\| \sum_{i=1}^d \sqrt{1-\alpha^2}\tilde{\chi}_i \right\| \times [G(t-r, x-*) - G(s-r, y-*)] \sigma_i.(u(r,*)] \right|^2_{\mathcal{H}^d}$$

如前多次论过的，应用引理 A.1 且 $\alpha \geq \alpha_0$，我们得到：

$$G_{3,\varepsilon} \geq C\varepsilon^{\theta_2(3-\beta)}.$$

同样在 (4.10) 中，我们有：

$$E\left((G_{31,\varepsilon})^p\right) \leq C\varepsilon^{\theta_2(5-2\beta)p},$$

而得益引理 A.2 且 $s=t$，

$$E\left((G_{32,\varepsilon})^p\right) \leq C\varepsilon^{\theta_2(3-\beta)p}.$$

这两个界限对于任何 $p \in [1, \infty[$ 均成立。

根据命题 A.3 和 A.6 以及推论 A.10 之后的讨论（参见 (A.40), (A.43) 和 (A.45))），可知对于任何 $p \in [1, \infty[$，

$$E\left((\bar{G}_{33,\varepsilon})^p\right) \leq C \left{\varepsilon^{\theta_2(2-\beta)-\theta_2} + \varepsilon^{2\theta_0+\theta_2(1-\beta)} + \varepsilon^{\theta_0(2-\beta)} + \left{\varepsilon^{\theta_0(2-\beta)}-\theta_2}\right}^p_{\beta_i \in[0,1], + \left{\varepsilon^{\theta_0(2-\beta)}-\theta_2} + \varepsilon^{\theta_2(2-\beta)}\right}^p + \varepsilon^{\frac{2\theta_0(2-\beta) + 2\theta_2}{4}}\right}^p_{\beta_i \in[1,2]}.$$

通过应用引理 A.2，由于我们处于 $t-s \leq \varepsilon^0$ 的情况，我们得到：

$$E\left((\bar{G}_{34,\varepsilon})^p\right) \leq C\varepsilon^{\theta_2p(t-s) + \varepsilon^{\theta_2(5-2\beta)}} \leq C \left{\varepsilon^{\theta_0(5-2\beta)p} + \varepsilon^{\theta_2(3-\beta)p}}\right\}$$

对于任何 $p \in [1, \infty[$。

因此，

$$E\left((\bar{G}_{3,\varepsilon})^p\right) \leq C\varepsilon^{\min[\theta_2(5-2\beta),-\theta_2+\theta_0(2-\beta),\pi(\theta_0,\theta_2,\beta)]p},$$

## 4. MALIAAVIN 矩阵特征值的研究与下界

其中：

$$\pi(\theta$$

**情况 3：** $0 \le t-s \le \varepsilon^0$ 且 $0 < \varepsilon^0 < \frac{|x-y|}{d}$。使用 $(4.2)-(4.4)$我们得到：

$$\xi^T\gamma_Z\xi \ge J_1^d - \frac{1}{2}G_{4,\varepsilon}-G_{4,\varepsilon},$$

其中，

$$G_{4,\varepsilon} = \int_{s-\varepsilon}^d dr ||\left[(\alpha\lambda_i-\sqrt{1-\alpha^2}\chi_i)G(s-r,y-*)u(s,y))\right|^2 + |\sqrt{1-\alpha^2}\chi_i|G(t-r,x-*)\sigma_i.(u(s,x))\right|^2_{\mathcal{H}^d}$$

且 $\bar{G}_{4,\varepsilon}=\sum_{i=1}^4 G_{4,\varepsilon}$，

$$\bar{G}_{41,\varepsilon} = \int_{s-\varepsilon}^d dr ||\sum_{i=1}^d ((\alpha\lambda_i-\sqrt{1-\alpha^2}\chi_i)G(s-r,y-*) \times [\sigma_i.(u(r,*)-\sigma_{i,y}(u(s,y))]||^2_{\mathcal{H}^d}$$

$$\bar{G}_{42,\varepsilon} = \int_{s-\varepsilon}^d dr ||\sum_{i=1}^d \sqrt{1-\alpha^2}\chi_iG(t-r,x-*) \times [\sigma_i.(u(r,*})-\sigma_{i,y}(u(s,y))]||^2_{\mathcal{H}^d}$$

$$\bar{G}_{43,\varepsilon} = \int_{s-\varepsilon}^d dr ||\sum_{i=1}^d (\alpha\lambda_i-\sqrt{1-\alpha^2}\chi_i)a_i.(r;*,s)]||^2_{\mathcal{H}^d}$$

$$\bar{G}_{44,\varepsilon} = \int_{s-\varepsilon}^d dr ||\sum_{i=1}^d \sqrt{1-\alpha^2}\chi_i.(r;*,x)]||^2_{\mathcal{H}^d}$$

我们固定 $p\in[1, \infty]$ 并给出上述项的 $L^p(\Omega)$ 上界。

我们已经从 (4.10) 看到 $E((G_{41,\varepsilon})^p)\le C\varepsilon^{\theta_2}$。对于第二项，我们使用路径的 Hölder 连续性、引理 A.1 以及 $G(t-r,x-*)$ 的支撑集 $\{z\in\mathbb{R}^d : |x-z| \le t-r\}$，得到 $E((G_{42,\varepsilon})^p)\le C(t-s+\varepsilon^0)^{(2-\beta)}(t-s+\varepsilon^0)^{(3-\beta)} = C\varepsilon^{\theta(5-2\beta)}$，因为 $t - s < \varepsilon^0$。对于第三项，我们应用引理 A.2（$t=s$）得到 $E((G_{43,\varepsilon})^p)\leq C\varepsilon^{\theta(3-\beta)p}$。最后，对于第四项，我们使用引理 A.2。得到 $E((G_{44,\varepsilon})^p)\leq C\varepsilon^{(t-s+\varepsilon^0)^{(5-2\beta)}} \leq C\varepsilon^{\theta(3-\beta)p}$。

从上述估计，我们得出 $(4.30) \quad E\left[\sum_{l=1}^4 G_{4l,\varepsilon}\right] \leq C\varepsilon^{\theta(5-2\beta)p}$。

我们的主要目标是找到 $G_{4,\varepsilon}$ 的下界。为此，我们应用变量替换 $r \to s-r$，然后展开 $\mathcal{H}^d$ 上的范数得到：

$$G_{4,\varepsilon} \geq \int_0^\varepsilon dr \|G(r, y-*\|^2_{\mathcal{H}^d} |\alpha\lambda^T - \sqrt{1-\alpha^2}\chi^T\sigma(u,y)|^2 + \int_0^\varepsilon dr \|G(t-s+r, x-*\|^2_{\mathcal{H}^d} |\sqrt{1-\alpha^2}\chi^T\sigma(u,x)|^2 - 2 \int_0^\varepsilon dr \langle G(r, y-*), G(t-s+r, x-*) \rangle_{\mathcal{H}^d} \times |(\alpha\lambda - \sqrt{1-\alpha^2}\chi)\sigma(u,y)), \sqrt{1-\alpha^2}\chi\sigma(u,x)|.$$

性质 (P2) 结合引理 A.1 和 A.2 得到：

$$G_{4,\varepsilon} \geq c\rho_0^\theta\varphi(\alpha,\lambda,\tilde{\chi})\varepsilon^{\theta(3-\beta)}- 2 \|\psi(\alpha,\lambda,\tilde{\chi})I(\varepsilon;t,s,y)\|$$

其中：

$$\varphi(\alpha,\lambda,\tilde{\chi}) = \left|\alpha\lambda^T - \sqrt{1-\alpha^2}\tilde{\chi}^T\right|^2 + \left|\sqrt{1-\alpha^2}\tilde{\chi}^T\right|^2,$$
$$\psi(\alpha,\lambda,\tilde{\chi}) = \left\langle(\alpha\tilde{\lambda} - \sqrt{1-\alpha^2}\tilde{\chi})\sigma(u(s,y)), \sqrt{1-\alpha^2}\tilde{\chi}\sigma(u(s,x))\right\rangle,$$
$$I(\varepsilon;t,s,y) = \int_0^\varepsilon dr \langle G(r, y-*), G(t-s+r, x-*) \rangle_{\mathcal{H}^d},$$

且 $c = \frac{1}{3-\theta} \int_{\mathbb{R}^d} \frac{\sin^2(|u|)}{|u|^2} du$。

很容易检查出 $\varphi_0 := \inf_{\alpha\in[0,1],\|\chi\|=1} \varphi(\alpha,\lambda,\tilde{\chi}) > 0$。

同样，$\sup_{\alpha\in[0,1],\|\chi\|=1} |\psi(\alpha,\lambda,\tilde{\chi})| \leq 2\|\sigma\|_\infty$。

因此，4.31) \quad G_{4,\varepsilon} \geq c\rho_0^\theta\varepsilon^{\theta(3-\beta)}-2\|\sigma\|_\infty|I(\varepsilon;t,s)|$.

由于 $0 \leq t-s \leq \varepsilon^\theta$，由引理 A.1，存在 $\delta_0 > 0$ 使得满足 $\frac{|x-y|}{\varepsilon} > \delta_0$ 的 $\varepsilon > 0$，我们有 $|I(\varepsilon;t,s)| \leq \frac{c\rho_0^\theta\varphi_0}{2\|\sigma\|_\infty}$。

从 (4.31) 得到 $(4.32) \quad G_{4,\varepsilon} \geq c\rho_0^\theta\varepsilon^{\theta(3-\beta)}-2\|\sigma\|_\infty|I(\varepsilon;t,s)|$。

由于 $0 \leq t-s \leq \varepsilon^\theta$，由引理 A.1，存在 $\delta_0 > 0$ 使得满足 $\frac{|x-y|}{\varepsilon} > \delta_0$ 的 $\varepsilon > 0$，我们有 $|I(\varepsilon;t,s)| \leq \frac{c\rho_0^\theta\varphi_0}{2\|\sigma\|_\infty}$。

**定理 4.3 的证明。** 定理 4.1 和 4.2 表明假设 (3.5) 和 (3.6) 在 $\rho = \delta + 3 - \beta$ 时定理 3.1 成立，其中 $\delta$ 是任意极小的正实数。

# 附录 A

## 技术估计

在本章中，我们收集了在前章节中使用的重要技术结果。除非另有说明，我们假设 (C1) 和 (P1)。

**引理 A.1.** 对于 $k \in \mathbb{N}^*$ 和 $\beta \in [0, 2k]$，我们有以下结论：

- (A) 对于任意 $r > 0$ 和 $x \in \mathbb{R}^k$，
  $(A.1) \|G(r, x - *)\|_{\mathcal{H}_t}^2 = cr^{2-\beta}, \text{其中 } c = \int_0^r \frac{\sin^2(|w|)}{|w|^{2k-\beta+2}} dw.$

- (B) 对于任意 $r_0 > 0$，存在 $C > 0$ 使得
  $\sup_{(t,x) \in [0,T] \times \mathbb{R}^k} \int_t^{r_0} dr \|G(t-r, x - *)\|_{\mathcal{H}_t}^2 \leq c \sup_{t \in [0,T]} (t-r)^{2-\beta} dr \leq Cr_0,$

- (C) 对于任意 $0 < s \leq t \leq T$ 和每个 $\varepsilon \in [0, s]$,
  $\sup_{x \in \mathbb{R}^k} \int_s^t dr \|G(t-r, x - *)\|_{\mathcal{H}_t}^2 \leq C ((t-s+\varepsilon))^{3-\beta} (t-s)^{3-\beta}$.

**证明。** 根据其定义（见 (1.10)）。

$\|G(r, x - *)\|_{\mathcal{H}_r}^2 = \int_0^r \frac{\sin^2(|\xi|)}{|\xi|^{2k-\beta+2}} d\xi$.

通过变量代换 $\varepsilon \to r$，我们得到 (A.1)。其余陈述显易成立。

**引理 A.2.** 令 $k \in \{1, 2, 3\}$，并 $\{a_{ij}(r; z; t), x)_{0 \leq r \leq t, x, y \in \mathbb{R}^k, 1 \leq i \leq j}$ 为 (3.2) 中定义的随机过程。固定 $0 \leq s \leq t \leq T$。那么对于任意 $\varepsilon \in [0, s], \chi \in \mathbb{R}^k$，以及每个 $p \in [1, \infty)$。

特别，当 $s = t$ 时，

$\sup_{x \in \mathbb{R}^k} \int_s^d dr \sum_{i=1}^d \chi a_{ij}(r; *; s, x)|^p_{\mathcal{H}_t^d} \leq C|\chi|^2 p \varepsilon (t-s+\varepsilon)^{(3-\beta)p}$。

## A. 技术估计

**证明。** 设

$D_{i,j}^t(r,*,t,x) = \sum_{\ell=1}^d \int_{\mathbb{R}^k}^t G(t-\rho, x-z) \nabla\sigma_{i,t}(u(\rho, z)) \cdot D_{r,*u}^{(j)}(u(\rho, z)) \times M^\ell(d\rho, dz),$
$D_{i,j}^t(r,*,t,x) = \int_{\mathbb{R}^k}^t d\rho \ G(t-\rho, x-z) \nabla b_i(u(\rho, z)) \cdot D_{r,*u}^{(j)}(u(\rho, z)).$

我们将证明，对于任意 $p \in [1, \infty]$，

(A.2) $\sup_{(t,x) \in [0,T] \times \mathbb{R}^k} E \left( \int_{s-\varepsilon}^s d\rho \sum_{i=1}^d \chi_{i,t}^1(r,*,x) \right)^p_{\mathcal{H}^d} \leq C|X|^{2p}(s+\varepsilon)^{(5-2\beta)p},$

(A.3) $\sup_{(t,x) \in [0,T] \times \mathbb{R}^k} E \left( \int_{s-\varepsilon}^s d\rho \sum_{i=1}^d \chi_{i,t}^2(r,*,x) \right)^p_{\mathcal{H}^d} \leq C|X|^{2p}(s+\varepsilon)^{(6-\beta)p}$。

对应 (3.2)，引理的结论将得出的。为了证明 (A.2)，我们写下

(A.4) $E \left( \int_{s-\varepsilon}^s d\rho \sum_{i=1}^d \chi_{i,t}^1(r,*,x) \right)^p_{\mathcal{H}^d} \leq E \left( \sum_{\ell=1}^d \int_{s-\varepsilon}^s \int_{\mathbb{R}^k} G(t-\rho, x-z) (\chi^t\sigma(u(\rho,z))]_{\ell} \cdot D_{r,*u}^{(j)} M^\ell(d\rho, dz) \right)^{2p}_{L^2([s-\varepsilon];\mathcal{H})}$
$= E \left( \sum_{\ell=1}^d \int_{s-\varepsilon}^s \int_{\mathbb{R}^k} G(t-\rho, x-z) (\chi^t\sigma(u(\rho,z))]_{\ell} \cdot D_{r,*u}^{(j)} M^\ell(d\rho, dz) \right)^{2p}_{L^2([s-\varepsilon];\mathcal{H})}$

然后对 $L^2([s-\varepsilon];\mathcal{H})$ 随机过程 $(\nabla[\chi^t\sigma(u(\rho,z))]_{\ell}) \cdot D_{r,*u}^{(j)}(\rho,z) \in [s-\varepsilon,t] \times \mathbb{R}^k$ 应用 [39] 中的定理。

## A.1 MALLIAVIN 范数的界

$\ell = 1, \dots, d$。表明 (A.4) 中的表达式被

$\sum_{\ell=1}^d \left( \int_{s-\epsilon}^s d\rho \int_{\mathbb{R}^k} \mu(d\xi) |\mathcal{F}G(t-\rho(\xi))|^2 \right)^{p-1} \int_{s-\epsilon}^s d\rho \sup_{z \in \mathbb{R}^k} E (\|\nabla [\chi^t\sigma(u(\rho,z))]) \cdot D_{\rho,u}u(\rho,z)\|_{L^2([s-\epsilon];\mathcal{H})}^{2p}$

(A.5) $\int_{s-\epsilon}^s d\rho \mu(d\xi) |\mathcal{F}G(t-\rho(\xi))|^2$。根据 [39] 中引理 8.2 的证明，我们可以证明

(A.6) $E (\|Du(\rho,z)\|_{L^2([s-\epsilon,s];\mathcal{H})})^{2p} \leq C (\int_{s-\epsilon}^s dr |G(\rho-r)\|_{\mathcal{H}^d}^2)^p$

对于 $\rho \in [s-\epsilon, t]$。(A.1) 得到

$\int_{s-\epsilon}^s dr |G(\rho-r)\|_{\mathcal{H}^d}^2 \leq \int_{(\rho-s)^+}^{s} dr |G(r,*)\|_{\mathcal{H}^d}^2 = c \int_{(\rho-s)^+}^{s+\epsilon} dr r^{2-\beta}$。结合 (P1)，得到

$E (\|[\chi^T \sigma(u(\rho,z))]) \cdot D_{\rho,u}u(\rho,z)\|_{L^2([s-\epsilon,s];\mathcal{H})}^{2p} \leq C|X|^{2p} \sup_{\rho \in [s-\epsilon,t]} (\rho-s+t)^{(2-\beta)p}$。使用 (A.5) 中的方法得到

$E (\int_{s-\epsilon}^s dr |\sum_{i=1}^d \chi_i T_{1,\epsilon}^d(r*,t,x)\|_{\mathcal{H}^d}^2)^p \leq C|X|^{2p}(\rho-s+t)^{(2-\beta)p} (\int_{s-\epsilon}^s d\rho \int_{\mathbb{R}^k} \mu(d\xi) |\mathcal{F}G(t-\rho(\xi))|^2)^p \leq C|X|^{2p}(\rho-s+t)^{(5-2\beta)}$，其中在最后，我们应用了引理 A.1。我们现在证明 (A.3)。为此，我们写下

$E (\int_{s-\epsilon}^s dr \sum_{i=1}^d \chi_i T_{1,\epsilon}^d(r*,t,x)\|_{\mathcal{H}^d}^2)^p \leq E (\sum_{j=1}^d \int_{s-\epsilon}^s d\rho \int_{\mathbb{R}^k} G(t-\rho, dz) |\nabla(\chi^T b(u(\rho,z))) \cdot Du(\rho,z)\|_{L^2([s-\epsilon,s];\mathcal{H}^d})^{2p}$。

根据闵可夫斯不等式，最后一个表达式被界为

$E\left(\left(\int_{s-\epsilon}^s d\rho \int_{\mathbb{R}^k} G(t-\rho, x-z) |\nabla(\chi^T b(\rho,z))|^2\right) \times \|Du(\rho,z)\|_{L^2([s-\epsilon,s];\mathcal{H}^d)}^{2p}\right)$

由于 $\int_{s-\epsilon}^s d\rho \int_{\mathbb{R}^k} G(t-\rho, dz) = \int_{s-\epsilon}^s d\rho \leq C(t-s+\epsilon)^2$，我们得到 (A.3)。

我们像 (A.5) 一样对其进行界，然后使用 (A.6) 和假设 (P1) 找到

$E\left(\int_{s-\epsilon}^s d\rho \sum_{i=1}^d \chi_i T_{1,\epsilon}^d(r*,t,x)\|_{\mathcal{H}^d}^2\right)^p \leq C|X|^{2p}(t-s+\epsilon)^{(5-\beta)p}$。在后续中，我们将多次使用性质

$(A.7) \|G(r,x)-*\|_{\mathcal{H}^d}^2 = \int_{\mathbb{R}^k\times\mathbb{R}^k} G(r,du)G(r,dv)|u-v|$，对于一个 $L^2$-连续过程 $Z(t)$，使得 $\sup_{(t\in[0,T]\times\mathbb{R}^k} |E|Z(t)| < \infty$。该性质是 (8) 应用于符号测度 $\varphi(dx)=Z(t,x)G(r,dx)$ 的结论。

**命题 A.3.** 令 $k\in\{1, 2, 3\}$，并 $Z=\{Z(t,x), (t,x)\in[0,T]\times\mathbb{R}^k\}$ 为满足下列条件的随机过程：

- (a) 存在 $\rho\in[0,1]$对于每个 $p\in[1,\infty]$存在 $C<\infty$使得对于任意 $x,y\in\mathbb{R}^k$，$\sup_{t\in[0,T]} |E|Z(t,x)-Z(t,y)|^p \leq C|x-y|^p$；
- (b) 对于每个 $p\in[1,\infty]$，存在 $C<\infty$使得 $\sup_{(t\in[0,T]\times\mathbb{R}^k)} |E|Z(t,x)|^p \leq C$。

那么对于任意 $p\in[1,\infty]$，存在常数 $C>0$对于任意 $\epsilon\in[0,1], s\in[\epsilon,T]$ 和 $x,y\in\mathbb{R}^k$，

$\mathbb{E}\left(\int_{\epsilon}^t d\rho \|G(r,x)-G(r,y)|^2_{\mathcal{H}^d}\right)^p \leq C\{|x-y|^{2p}\epsilon^{p(3-\beta)}, |x-y|^{\alpha}\epsilon^{p[3-(\alpha+\beta)]}\}$，其中 $\alpha\in(0, (2\wedge\beta)-\beta)\wedge1$。

## A.1. MALLIAVIN 范数的界

**证明。** 根据 [17] 中命题 3.5 第一部分的思想并使用 (A.7)，我们写下

$E\left[\left(\int_0^t \|G(r, x-*) - G(r, y)\|Z(s-r)\|^2_{\mathcal{H}}\right)^p\right] \leq C \sum E(|J_i^x(x, y)|^p)$，其中对于 $i=1, \dots, 4$，

$J_i^x(x, y) = \int_0^t dr \int_{\mathbb{R}^k} \int_{\mathbb{R}^k} G(r, du)G(r, dv)h_i(\varepsilon, r, u, v)$，其中

$h_1(\varepsilon, r, u, v) = f(y-r+x+v-u)Z(s-r, u) - Z(s-r, v)) \times (Z(s-r, x) - Z(s-r, v))$,$
$h_2(\varepsilon, r, u, v) = Df(v-u, x)Z(s-r, u) \times (Z(s-r, x) - Z(s-r, v)),$
$h_3(\varepsilon, r, u, v) = D^2f(u-y, x)Z(s-r, v) \times (Z(s-r, x) - Z(s-r, v)),$
$h_4(\varepsilon, r, u, v) = -D^2f(u-y, x)Z(s-r, v)$。

在这些表达式中，$f(x) = |x|^\beta$ $\beta \in [0, 2] \wedge k$ 且 $D^2f(u, x) = f(u+x) - 2f(u) + f(u-x)$。对于 $k\in\{1, 2, 3\}$，$G(r,du) \geq 0$。那么，根据 Hölder 不等式、Z 的性质、(A.7) 和 (A.1)，得到

$E(|J_1^x(x, y)|^p) \leq \sup_{t\in[0,T]} E\{|Z(t, x) - Z(t, y)|^{2p}\} \times \left(\int_{s-\epsilon}^s d\rho \int_{\mathbb{R}^k} G(t-\rho, dz) |Df(v-u+x-v)|^2\right)^p$

(A.8) 设

(A.9) $\mu_2(x, y) = \int_0^t dr \int_{\mathbb{R}^k \times\mathbb{R}^k} G(r, du)G(r, dv) |Df(v-u, x-y)|$

[17] 中引理 6.1 的变体在引理 A.4 中显示

$\mu_2(x$ 对于任意 $\alpha \in(0, ((2-\beta)^\wedge1])$。因此，Hölder 不等式结合过程 Z 的假设得到 $E(|J_2^x(x, y)|^p) \leq C(\mu_2(x, y))^\rho |x-y|^{\rho}$。

(A.10) 上界对于 $E(|J_2^x(x, y)|^p)$ 成立。

## A. 技术估计

对于剩余项的分析，我们考虑：



(A.11) \quad \mu_4(x,y) = \int_{\mathbb{R}^k\times\mathbb{R}^k} dr G(r,du)G(r,dv) |D^2f(u,x-y)|.

通过应用 [17] 中 Lemma A.5 给出的引 6.2 的修改版本，我们得到：

```
E(|J_4^u(x,y)|^p) \leq C \mu^k(x,y)^p \sup_{(t,x)\in[0,T]\times\mathbb{R}^k} E(|Z(t,x)|^{2p})
```

(A.12) \quad \leq |x-y|^{\epsilon p[3-(\alpha+\beta)]}_p,

对于 $\bar{\alpha} \in [0, (2\wedge k)-\beta]$。
根据 (A.8),(A.10) 和 (A.12)，我们完成了命题 A.3 的证明。

这两个引理用于命题 A.3 的证明。

**引理 A.4.** 对于 $\alpha \in [0, (2\wedge k)-\beta)\wedge1$，存在 $C$ 使得对于所有的 $x,y \in \mathbb{R}^k$：

```
\mu_2(x,y) \leq |x-y|^\alpha e^{-3(\alpha+\beta)},
```

**证明.** 与 [17, Lemma 6.1] 相比，此结果量化了 $\mu_2(x,y)$ 在积分域上的差异，它是在正则化 $G_n$ 作用的波方程的基本解 $G$，且函数 $f$ 不包含平滑因子 $\rho$。两者的证明过程非常相似。
我们给出主要思路。

应用引理 2.6(a)，取 $d:=k, b:=\alpha, a:=k(\alpha+\beta), u:=v-u, c:=|x-y|, x:=|[x-y|]$，在使用 (A.7) 后，我们得到：

```
\mu_2(x,y) \leq |x-y|^\alpha \int dr \int d\xi |FG(\xi)|^2 |\xi-(k-(\alpha+\beta))|^2
```

对于 $\alpha \in [0, 2\wedge k]$，直到一个正系数，最后一个积分被 $\epsilon^{-3(\alpha+\beta)}$ 限制（见引理 A.1）。这完成了证明。

**引理 A.5.** $\mu_4(x,y)$ 由 (A.11) 定义。对于每个 $\alpha \in [0, (2\wedge k)-\beta]$，存在正常数 $C$ 使得对于 $x,y \in \mathbb{R}^k$：

```
\mu_4(x,y) \leq C|x-y|^\alpha e^{-3(\alpha+\beta)},
```

**证明.** 在与 [17] 中的 Lemma 6.2 进行比较时，适用于 Lemma A.4 证明中提到的相同差异。应用 [17] 中的 Lemma 2.6(c)，取 $d:=k, b:=\alpha, a:=k(\alpha+\beta), \alpha+\beta \in [0, 2\wedge k], u:=v-u, x:=x-y$， 得到：

```
\mu_4(x,y) \leq |x-y|^\alpha x
```

```
\times (\sup_{w\in\mathbb{R}^k} \int dw \int_{\mathbb{R}^k\times\mathbb{R}^k} G(r,du)G(r,dv) |y-w+u|^{-(\alpha+\beta)})
```

```
\times \int_{\mathbb{R}^k} dw |D^2(|\cdot-(k-\alpha))| (w,e)|,
```

其中 $e$ 表示 $\mathbb{R}^k$ 的单位向量。
根据引理 A.1, [17] 中的 Lemma 2.6(d),(A.7) 和 (A.1)，最后一个表达式被 $|x-y|^\alpha e^{-3(\alpha+\beta)}$ 限制。

## A.1. Malliavin 范数的界

**位置 A.6.** 设 $k \in\{1, 2, 3\}$，令 $Z=\{Z(t, x), (t, x) \in[0, T] \times \mathbb{R}^k$ 为满足命题 A.3假设的随机过程。那么对于任何 $np \in[1, \infty]$，存在常数 $C > 0$ 使得对于 $0 \leq s \leq t \leq T$ 和 $\epsilon \in]0, s]$：

```
$E\left(\int_{s-\epsilon}^s dr \|\|G(t-r, x,*) - G(s-r, x,*)Z(r,*)\|_{\mathcal{H}}^p\right)^p\\n\leq C\left[\frac{(4-\beta)}{2pp}|t-s|^{2pp}|t-s+\epsilon|^{\frac{(2-\beta)}{p}}\right]\\n+|t-s|^\beta|t-s+\epsilon|^{1-\beta}\beta_{\in[0,1]}+\epsilon|+|t-s|^{2-\beta}\beta_{\in[1,2]}\\

+|t-s|^{\alpha_1}|t-s+\epsilon|^{-(\alpha_1+\beta)}+\epsilon^{\frac{\alpha_2}{2}}|t-s|^{\alpha_1}|t-s+\epsilon|^{1-\frac{\alpha_1+\alpha_2}{2}}\\

+\beta_{\in[1,2]}|t-s|^2-|t-s+\epsilon|^{2-(\alpha_2+\beta)}+\epsilon^{\frac{\alpha_2}{2}}|t-s|^{\alpha_2}|-(\alpha_2+\beta)|t-s+\epsilon|^{1-\frac{\alpha_2+\alpha_3}{2}}\\

+\beta_{\in[0,1]}|t-s|^{1-\alpha_3}|t-s|^{\alpha_3}|(t-s+\epsilon-(\alpha_3+\beta))-|t-s|^2-(\alpha_3+\beta))+\epsilon^{\frac{\alpha_3}{2}}|t-s+\epsilon|^{1-\frac{\alpha_3+\alpha_4}{2}}\\

+|t-s|^{\alpha_4}|t-s+\epsilon|^{2-(\alpha_4+\beta)}+\epsilon^{\frac{\alpha_4}{2}}|t-s+\epsilon|^{1-(\alpha_4)}\right\},
```

(A.13)

其中 $\alpha_i \in[0,1], i=1, 2,3$ 且 $\alpha_1 \in[0,(2\wedge k)-\beta], \alpha_2 \in[0,2-\beta], \alpha_3 \in[0,(2\wedge k)-\beta], \alpha_4 \in[0,(2\wedge k)-\beta]$。

**证明.** 我们遵循 [17] 中定理 3.8 的证明方案（特别是定理中的 $T_t^p(t,x)$ 项），并对该证明中的引理进行了适当修改。根据 (A.7) 和 [17] 的参数，我们写道：

```
$E\left(\int_{s-\epsilon}^s dr \|\|G(t-r, x,*) - G(s-r, x,*)Z(r,*)\|_{\mathcal{H}}^p\right)^p\leq C\sum_{i=1}^4 E(|R_i^s(s,t,x)|^p)
```

其中：

```
$R_i^s(s,t,x)=\int_{s-\epsilon}^s dr \int_{\mathbb{R}^k} G(s-r,du)G(s-r,dv)r_i(s,t,r,v),
```

以及 $r_1(s)$：

```
$r_2(s,t,r,v) = \left(\left(\frac{t-r}{s-r}\right)^2\right)f\left(\frac{t-r}{s-r}\right)(v-u)\left(\frac{t-r}{s-r}\right)f\left(\frac{t-r}{s-r}\right)\\
\left[Z\left(s,x-\frac{t-r}{s-r}u\right)\left[Z(r,x-\frac{t-r}{s-r}v\right]\right],$
```

$r_3(s)$：

```
$r_4(s,t,r,v) = \left(\left(\frac{t-r}{s-r}\right)^2\right)f\left(\frac{t-r}{s-r}\right)(v-u)\left(\frac{t-r}{s-r}\right)f\left(\frac{t-r}{s-r}\right)\right)\\
\left[-\frac{t-r}{s-r}f\left(\frac{t-r}{s-r}v-u\right)+f(v-u)\right]\\
\left[Z(r,x-u)Z(r,x-v)\right,$
```

且 $f(x)=|x|^{-\beta}, \beta \in[0, 2k]$。

令：

$\nu_1(s,t,\varepsilon) = \int_{s-\varepsilon}^{s} \int_{\mathbb{R}^k}^{\mathbb{R}^k} G(s-r,du)G(s-r,dv)f\left(\frac{t-r}{s-r}v-u\right)\left(\frac{t-r}{s-r}\right)$

根据下述引理 A.7，我们可以应用第一个 Hölder 不式，然后应用 Cauchy-Schwarz 不式得到：

$E\left(|R_1^t(s,t,x)|^p\right) \le(\nu_1(s,t,\varepsilon))^{p-1}\\
\times\int_{s-\varepsilon}^{s} dr \int_{\mathbb{R}^k}^{\mathbb{R}^k} G(s-r,du)G(s-r,dv)f\left(\frac{t-r}{s-r}v-u\right)\left(\frac{t-r}{s-r}\right)\\
\times\left(E\left(\left[Z\left(r,x-\frac{t-r}{s-r}u\right)\right]\right)^{p}\right)\\
\times\left(E\left(\left[Z\left(r,x-\frac{t-r}{s-r}v\right)\right]\right)^{p}\right)$

## A. Malliavin 范数的界

根据对过程的假设，最后两项的乘积为：

```
|x-y|^\alpha
```

对于 $|u| \leq s-r, |v| \leq s-r$，它被 $|x-y|^\alpha$ 限制。因此，通过应用 A.7，我们得到：

```
$E(|R_1^t(s,t,x)|^p) \leq C\epsilon^{\frac{\alpha_1}{2}}|t-s|^{\alpha_1}|t-s+\epsilon|^{1-\frac{\alpha_1}{2}},
```

(A.14)

令

$\nu_2(s,t,\varepsilon) = \int_{s-\varepsilon}^{s} \int_{\mathbb{R}^k}^{\mathbb{R}^k} G(s-r,du)G(s-r,dv)\left(\frac{t-r}{s-r}\right)^2 f\left(\frac{t-r}{s-r}\right)(v-u)\left(\frac{t-r}{s-r}\right)f\left(\frac{t-r}{s-r}\right)\\
\left[Z\left(s,x-\frac{t-r}{s-r}u\right)\left[Z(r,x-\frac{t-r}{s-r}v\right]\right],$

根据引理 A.8、Hölder 不式、Cauchy-Schwarz 不式以及 Z 的性质，我们得到：

```
$E(|R_2^s(s,t,x)|^p) \leq C|t-s|^{\rho}(\nu_2(s,t,\varepsilon))^p\\

\leq C|t-s|^{\rho} [\epsilon^{|t-s|^{2-\beta}}1_{\{\beta\in[0,1]\}}+\epsilon|t-s|^{2-\beta}1_{\{\beta\in[1,2]\}}+\t-s|^{\alpha}|t-s+\epsilon|^{2-(\alpha+\beta)}|t-s+\epsilon|^{1-\frac{\alpha+\beta}{2}}]^p,
```

(A.15)

对于 $\alpha\in[0,1]$ 使得 $\alpha+\beta\in[0,2]$。相同的结果适用于 $E(|R_3^s(s,t,x))$。

对于项 $R_4^s(s,t,x)$ 的研究，我们采用与之前相同的方法。我们定义：

```
$\nu_3(s,t,\varepsilon) = \int_{s-\varepsilon}^{s} dr \int_{\mathbb{R}^k\times\mathbb{R}^k} G(s-r,du)G(s-r,dv)\\
\times \left[\left(\frac{t-r}{s-r}\right)^2 f\left(\frac{t-r}{s-r}\right)(v-u)\left(\frac{t-r}{s-r}\right)f\left(\frac{t-r}{s-r}\right)-\frac{t-r}{s-r}f\left(\frac{t-r}{s-r}v-u\right)-\frac{t-r}{s-r}f\left(\frac{t-r}{s-r}\right)u+f(v-u)\right],
```

然后，使用引理 A.9 和对 Z 的假设，我们得到如下。如果 $k\in\{2,3\}$ 且 $\beta\in[1,2]$：

```
$E(|R_4^s(s,t,x)|^p) \leq C[\epsilon^{|t-s|^{2-\beta}}+\epsilon|t-s|^{2-\beta}+\epsilon^2|t-s|^{2-\beta}]+|t-s|^{\alpha}\left[\epsilon^{2-(\alpha+\beta)}|t-s+\epsilon+\epsilon^{\frac{\alpha+\beta}{2}}|t-s+\epsilon|^{1-\frac{\alpha+\beta}{2}}\right]^p,
```



## A. 技术估计

若 $k \in\{1, 2, 3\}$ 且 $\beta \in [0, 1]$，则

$$
E\left((\mathcal{R}_4^s(s, t, x))^\beta\right) \le C\left[|s|^{1-\beta}|t-s|^2 + |t-s|^{1+\alpha}||[t-s+\varepsilon|^{2-(\alpha+\beta)}-|t-s|^{2-(\alpha+\beta)}| + \varepsilon^{\frac{1+\alpha}{2}}|t-s+\varepsilon| + \varepsilon^{1-\alpha-\beta}|t-s+\varepsilon| + |t-s|^\alpha[\varepsilon^{2-(\alpha+\beta)}|t-s+\varepsilon|+\varepsilon^{\frac{\alpha+\beta}{2}}|t-s|^{1-\frac{\alpha+\beta}{2}}] + \varepsilon^2(t-s+\varepsilon)^{1-(\alpha+\beta)}\right]
$$

(A.17) 对于任意 $\alpha \in\{0, (k-\beta)\}$ 和 $\varepsilon \in\{0, \beta\}$ 成立。

估计 (A.14), (A.15), (A.16) 给出 (A.13)。

### A.2. 协方函数的积分增量

下三个引理被用于命题 A.6 的证明。

**引理 A.7.** 对于 $0 \le s < t \le T, \varepsilon \in[0, s]$，令

$$
\nu_1(s, t, \varepsilon)=\int_{s-\varepsilon}^{s+\varepsilon} dr \int_{\mathbb{R}^k} d\xi G(s-r, du)G(t-r, dv)\left(\frac{t-r}{s-r}-u\right)\frac{t-r}{s-r}
$$

存在常数 $C>0$ 使得：

$$
\nu_1(s, t, \varepsilon) \le C\varepsilon^{\frac{3-\beta}{2}}((t-s+\varepsilon)^{3-\beta}-(t-s)^{3-\beta})
$$

**证明。** 我们遵循 [17] 中引理 6.3 的证明。考虑变量替换 $v \mapsto \frac{t-v}{t-r}$，将 $G(s-\cdot,r)$ 映射到 $G(t-r,\cdot)$。因此

$$
\nu_1(s, t, \varepsilon)=\int_{s-\varepsilon}^{s+\varepsilon} dr \int_{\mathbb{R}^k} d\xi G(s-r, du)G(t-r, dv)(u-v)
$$

使用 (A.7)，通过施瓦茨不等式得到：

$$
\nu_1(s, t, \varepsilon) = \int_{s-\varepsilon}^{s+\varepsilon} dr \int_{\mathbb{R}^k} d\xi \frac{|FG(s-r)| |FG(t-r)|}{|\xi|^{k-\beta}}
$$

$$
= \int_{s-\varepsilon}^{s+\varepsilon} dr \int_{\mathbb{R}^k} d\xi \frac{|FG(s-r)| |FG(t-r)|}{|\xi|^{k-\beta}} \le \int_{s-\varepsilon}^{s+\varepsilon} dr \int_{\mathbb{R}^k} d\xi \frac{|FG(s-r)|^2}{|\xi|^{k-\beta}}\left(\int_{s-\varepsilon}^{s+\varepsilon} dr \int_{\mathbb{R}^k} d\xi \frac{|FG(t-r)|^2}{|\xi|^{k-\beta}}\right)^{1/2}
$$

根据引理 A.1，

$$
= \int_{s-\varepsilon}^{s+\varepsilon} dr \int_{\mathbb{R}^k} d\xi \frac{|FG(s-r)|^2}{|\xi|^{k-\beta}}=\int_{0}^{s+\varepsilon} dr ||G(r,*)|_{\mathcal{H}}^2 \le C\varepsilon^{3-\beta}.
$$

以及

$$
= \int_{s-\varepsilon}^{s+\varepsilon} dr \int_{\mathbb{R}^k} d\xi \frac{|FG(t-r)|^2}{|\xi|^{k-\beta}}=\int_{0}^{s+\varepsilon} dr ||G(r,*)|_{\mathcal{H}}^2 \le C((t-s+\varepsilon)^{3-\beta}-(t-s)^{3-\beta}),
$$

这证明了该引理。

### A.2. 协方函数的积分增量

**引理 A.8.** 对于任意 $0 \le s < t \le T$ 和 $\epsilon \in [0, s]$，令

$$
\nu_2(s,t,\epsilon) = \int_{s-\epsilon}^s dr \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(s-r,dv) \times \left[ f\left(\frac{t-r}{s-r}\right)f\left((v-u)\right) - f\left(\frac{t-r}{s-r}\right)f\left((v-u)\right)\right]
$$

那么，对于任何满足 $\alpha+\beta \in [0, 2]$ 的 $\alpha \in [0, 1]$：

$$
\nu_2(s,t,\epsilon) \le C|\epsilon|^{t-s+\epsilon|^{1-\beta}\beta_1[0,|\epsilon||+|epsilon|^{2-\beta}\beta_1[1,2] + |\epsilon|^{t-s+\epsilon|^{2-(\alpha+\beta)}+\epsilon|^{2-\beta{\3}}|t-s|\alpha|^{1-\beta{\3}}
$$

**证明。** 我们遵循 [17] 中引理 6.4 的方案。这里 $\nu_2^*(s,t,\epsilon)$ 的定义方式与 $\nu_2(s,t,\epsilon)$ 相同，但将绝对值替换为：

$$
\left(f\left(\frac{t-r}{s-r}\right)^2 - f\left(\frac{t-r}{s-r}\right)\right)f\left((v-u)\right)
$$

以及

$$
\left[f\left(\frac{t-r}{s-r}\right)f\left((v-u)\right) - f\left(\frac{t-r}{s-r}\right)f\left((v-u)\right)\right]
$$

分别。变量替换 $(u,v) \to \frac{sr}{s-r}(u,v)$、(A.7) 和 (A.1) 得到：

$$
\nu_2^*(s,t,\epsilon) = |t-s| \int_{s-\epsilon}^s dr \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(t-r,dv)f(v-u)
$$

$$
\le C|t-s| \int_{s-\epsilon}^s \frac{dr}{t-r} |t-r|^{2-\beta} \le C|t-s|((t-s+\epsilon)^{2-\beta}-(t-s)^{2-\beta})
$$

根据中值定理：

$$
(t-s+\epsilon)^{2-\beta}-(t-s)^{2-\beta} \le \begin{cases} C\epsilon(t-s+\epsilon)^{1-\beta}, & \text{if } \beta < 1 \\ C\epsilon(t-s)^{1-\beta}, & \text{if } \beta \ge 1 \end{cases}
$$

因此，$\nu_2^*(s,t,\epsilon) \le C|t-s||t-s+\epsilon|^{1-\beta}\beta_1[0,|\epsilon||+|t-s|^{2-\beta}\beta_1[1,2]$。

考虑变量替换 $(u,v) \to \frac{sr}{s-r}(u,v)$。令 $\alpha > 0$ 使得 $\alpha+\beta \in [0, 2]$。我们写 $f(u) = |u|^{-\beta}, \beta \in [0, 2]$。通过应用 [17] 引理 6.4，取 $d=\alpha, b=\alpha, a=\alpha+\beta, c=t-s, u=v-u$，得到：

$$
\nu_2^*(s,t,\epsilon) \le C|t-s|^{\alpha} \int_{s-\epsilon}^s dr \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(t-r,dv) \times \int_{s-\epsilon}^s dw K_{\alpha+\beta}((t-s)w-(v-u))D_{k-\alpha}\left(\frac{u}{s-r}\right)
$$

接下来，建立上述积分的上界。我们按照 [17] 引理 6.4 的证明进行。考虑区域 $|w| \le 3$，我们将 (A.20) 中的绝对值拆分为不同的项。遵循 [17] 引理 6.4 的计算并使用 (A.7)，我们找到：

$$
\int_{s-\varepsilon}^s dr \int_{\mathbb{R}^k \times \mathbb{R}^k} dw G(s-r,du)G(t-r,dv) \times \int_{|w| \le 4} dw \kappa_{\alpha+\beta}((t-s)w-(v-u))\kappa_{-\alpha}\left(\frac{u}{s-r}-w\right) \le \int_{|w| \le 4}\frac{dw}{|w|^{k-\alpha}} \int_{s-\varepsilon}^s dr \int_{\mathbb{R}^k} d\xi \frac{|FG(t-r)(\xi)|^2}{|\xi|^{k-(\alpha+\beta)}}
$$

我们假设 $\alpha+\beta \in[0,2]$。应用引理 A.1 并令 $\beta:=\alpha+\beta$，可以看出该表达式是有有界的：

$$
C \int_{|w| \le 4}\frac{dw}{|w|^{k-\alpha}} \left[(t-s+\varepsilon)^{3-(\alpha+\beta)}-t-s)^{3-(\beta)}\right] \le C(t-s+\varepsilon)^{2-(\alpha+\beta)}.
$$

同样地，

$$
\int_{|w| \le 4} dr \int_{\mathbb{R}^k \times \mathbb{R}^k} dw G(s-r,du) \times \int_{|w| \le 4} dw \kappa_{\alpha+\beta}((t-s)w-(v-u))\kappa_{-\alpha}(w) \le \int_{|w| \le 4}\frac{dw}{|w|^{k-\alpha}} \int_{s-\varepsilon}^s dr \int_{\mathbb{R}^k} d\xi \frac{|FG(s-r)(\xi)|||FG(t-r)(\xi)|}{|\xi|^{k-(\alpha+\beta)}}
$$

通过对 $d\xi$-积分应用施瓦茨不等式并使用引理 A.1，我们发现：

$$
(A.22) \int_{\mathbb{R}^k} d\xi \frac{|FG(s-r)(\xi)|||FG(t-r)(\xi)|}{|\xi|^{k-(\alpha+\beta)}} \le C(s-r)^{1-\frac{\alpha+\beta}{2}}(t-r)^{1-\frac{\alpha+\beta}{2}}.
$$

因此 (A.21) 是有界的：

$$
C \int_{|w| \le 4}\frac{dw}{|w|^{k-\alpha}} \int_{s-\varepsilon}^s dr (t-s+\varepsilon)^{2-(\alpha+\beta)} \le C(t-s+\varepsilon)^{2-(\alpha+\beta)}.
$$

为了完成 $\nu_2^*$ 的估计，我们现在考虑区域 $|w|>3$。使用 (A.22)，

$$
(A.23) \dots
$$

## A. 技术估算

证明。我们将遵循 [17, 引理 6.5] 的方法。

**情况 1：** $k \in \{2,3\}$ 且 $\beta \in [1,2]$。令

$$
\Delta^1 f(r, s, t, u) = \left| \frac{t-r}{s-r}^2 f\left(\frac{t-r}{s-r}(v-u)\right) - \frac{t-r}{s-r} f\left(\frac{t-r}{s-r}v-u\right) \right|,,
$$

$\Delta^2 f(r, s, t, u) = 1 - \frac{t-r}{s-r} f(v-u),,$

$\Delta^3 f(r, s, t, u) = \frac{t-r}{s-r} f(v-u) - f\left(v-\frac{t-r}{s-r}u\right).$

我们考虑界限

$$
\nu_3(s, t, \varepsilon) \le \nu_2^2(s, t, \varepsilon) + \nu_2^2(s, t, \varepsilon) + \nu_3^2(s, t, \varepsilon),
$$

其中每个 $\nu_i(s, t, \varepsilon)$，$i=1,2,3$ 的定义方式与 $\nu_3(s, t, \varepsilon)$ 相同，仅将积分函数中的

$$
\Delta f := \frac{t-r}{s-r}^2 f\left(\frac{t-r}{s-r}(v-u)\right) - \frac{t-r}{s-r} f\left(\frac{t-r}{s-r}v-u\right) - \frac{t-r}{s-r} f\left(v-\frac{t-r}{s-r}u\right) + f(v-u)
$$

(A.26)

分别替换为 $\Delta^i f(r, s, t, u)$，$i=1,2,3$。

注意 $\nu_3(s, t, \varepsilon)$ 与引理 A.8 中的 $\nu_2(s, t, \varepsilon)$ 一致，且假设 $\beta \in [1,2]$。因此

$$
\nu_3^2(s, t, \varepsilon) \le C \left[|t-s|^{2-\beta} + \varepsilon|t-s|^{\alpha} |t-s|^{2-(\alpha+\beta)}\right] + \varepsilon^{2-\frac{\alpha}{2}}|t-s|^{\alpha} |t-s|^{1-\frac{\alpha}{2}},
$$

(A.27)

对于任何 $\beta \in [1,2]$ 和 $\alpha \in (0, (2-\beta) \wedge 1)$。

根据 $\Delta^2 f(r, s, t, u)$ 的定义，利用 (A.7)，我们得到

$$
\nu_3^2(s, t, \varepsilon) \le C|t-s| \int_s^t \frac{dr}{s-r} \int_{R^k} d\xi \frac{|FG(s-r)(\xi)|^2}{\|\xi|^{k-\beta}} = C|t-s| \int_s^t dr(s-r)^{1-\beta} = C\varepsilon^{2-\beta}|t-s|
$$

(A.28)

考虑变量替换 $(u, v) \mapsto (\frac{t-r}{s-r}u, v)$。那么

$$
\nu_3^2(s, t, \varepsilon) = \int_s^t dr \int_{R^k \times R^k} G(t-r, du)G(s-r, dv) \times |Df\left(v-u,\frac{t-r}{s-r}u\right)|.
$$

该项与引理 A.8 证明中的 $\nu_2^2(s, t, \varepsilon)$ 相似，但 $s$ 和 $t$ 的角色发生了变化。因此，我们将进行类似的计算。为了完整性，我们给出细节：

### A.2. 协方差函数的积分增量

令 $\alpha > 0$ 使得 $\alpha + \beta \in [0, 2]$。通过应用 [17, 引理 2.6(a)]，其中 $d:=k, b:=\alpha, a:=k-(\alpha+\beta), c:=t-s, u:=\frac{u}{t-r}$，我们得到

$$
\nu_{\lambda}^2(s,t,\varepsilon) = |t-s|^\alpha \int_{s-\varepsilon}^s \int_{R^k \times R^k} G(t-r,du)G(s-r,rv) \times \int_{|w|\le3}^s dw\kappa_{\alpha+\beta}((t-s)w(w-u))D\kappa_{k-\alpha}(w, \frac{u}{t-r}).
$$



# A. 技术估算

证明。我们将遵循 [17, 引理 6.5] 的方法。

**情况 1：** $k \in \{2,3\}$ 且 $\beta \in [1,2]$。令

```
$$\Delta^1 f(r, s, t, u) = \left| \frac{t-r}{s-r}^2 f\left(\frac{t-r}{s-r}(v-u)\right) - \frac{t-r}{s-r} f\left(\frac{t-r}{s-r}v-u\right) \right|,,$$
$\Delta^2 f(r, s, t, u) = 1 - \frac{t-r}{s-r} f(v-u),,$$
$\Delta^3 f(r, s, t, u) = \frac{t-r}{s-r} f(v-u) - f\left(v-\frac{t-r}{s-r}u\right)..$
```

我们考虑界限

```
$\nu_3(s, t, \varepsilon) \le \nu_2^2(s, t, \varepsilon) + \nu_2^2(s, t, \varepsilon) + \nu_3^2(s, t, \varepsilon)$,
```

其中每个 $\nu_i(s, t, \varepsilon)$，$i=1,2,3$ 的定义方式与 $\nu_3(s, t, \varepsilon)$ 相同，仅将积分函数中的

```
$$\Delta f := \frac{t-r}{s-r}^2 f\left(\frac{t-r}{s-r}(v-u)\right) - \frac{t-r}{s-r} f\left(\frac{t-r}{s-r}v-u\right)$$
-\frac{t-r}{s-r} f\left(v-\frac{t-r}{s-r}u\right) + f(v-u)$$
(A.26)
```

分别替换为 $\Delta^i f(r, s, t, u)$，$i=1,2,3$。

注意 $\nu_3(s, t, \varepsilon)$ 与引理 A.8 中的 $\nu_2(s, t, \varepsilon)$ 一致，且假设 $\beta \in [1,2]$。因此

```
$\nu_3^2(s, t, \varepsilon) \le C \left[|t-s|^{2-\beta} + \varepsilon|t-s|^{\alpha} |t-s|^{2-(\alpha+\beta)}\right]$
+\varepsilon^{2-\frac{\alpha}{2}}|t-s|^{\alpha} |t-s|^{1-\frac{\alpha}{2}}],$
(A.27)
```

对于任何 $\beta \in [1,2]$ 和 $\alpha \in (0, (2-\beta) \wedge 1)$。

根据 $\Delta^2 f(r, s, t, u)$ 的定义，利用 (A.7)，我们得到

```
$\nu_3^2(s, t, \varepsilon) \le C|t-s| \int_s^t \frac{dr}{s-r} \int_{R^k} d\xi \frac{|FG(s-r)(\xi)|^2}{\|\xi|^{k-\beta}}$
= C|t-s| \int_s^t dr(s-r)^{1-\beta}$
= C\varepsilon^{2-\beta}|t-s|

(A.28)
```

考虑变量替换 $(u, v) \mapsto (\frac{t-r}{s-r}u, v)$。那么

```
$\nu_3^2(s, t, \varepsilon) = \int_s^t dr \int_{R^k \times R^k} G(t-r, du)G(s-r, dv)
\times |Df\left(v-u,\frac{t-r}{s-r}u\right)|.
```

该项与引理 A.8 证明中的 $\nu_2^2(s, t, \varepsilon)$ 相似，但 $s$ 和 $t$ 的角色发生了变化。因此，我们将进行类似的计算。为了完整性，我们给出细节：

## A.2. 协方差函数的积分增量

令 $\alpha > 0$ 使得 $\alpha + \beta \in [0, 2]$。通过应用 [17, 引理 2.6(a)]，其中 $d:=k, b:=\alpha, a:=k-(\alpha+\beta), c:=t-s, u:=\frac{u}{t-r}$，我们得到

```
$$\nu_{\lambda}^2(s,t,\varepsilon) = |t-s|^\alpha \int_{s-\varepsilon}^s \int_{R^k \times R^k} G(t-r,du)G(s-r,rv)
\times \int_{|w|\le3}^s dw\kappa_{\alpha+\beta}((t-s)w(w-u))D\kappa_{k-\alpha}(w, \frac{u}{t-r})\.
```

我们按照 $u_{\lambda}^2(s,t,\varepsilon)$ 的估计进行（参见 (A.20)）；但请注意变量 $s$ 和 $t$ 的位置略有不同，我们得到的界限也不同。我们分别考虑区域 $|w|\le 3$ 和 $|w|>3$。考虑变量替换 $w \to w+\frac{u}{t-r}, u \to \frac{u}{t-r}$。然后利用 (A.7)，

```
$$\int_{s-\varepsilon}^s dr \int_{R^k \times R^k} G(t-r,du)G(s-r,rv)
\times \int_{|w|\le3}^s dw\kappa_{\alpha+\beta}((t-s)w(w-u))D\kappa_{k-\alpha}(w, \frac{u}{t-r})
```

（注：由于原始文本存在大量重复和格式错误，此处翻译保留核心数学逻辑）

## A. 技术估计

我们还有：

```
$$\int_{s-\varepsilon}^{s} s-r \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(t-r,dv)$$
$$\times \int_{|w|\le3} dw \kappa_{\alpha+\beta}(v-(t-s)w)\kappa_{k-\alpha})$$
$$\leq C\varepsilon^{1-\frac{\alpha+\beta}{2}}(t-s+\varepsilon)^{1-\frac{\alpha+\beta}{2}}$$
```

其中最后一个不等式是使用 (A.22) 得到的。

为了完成 $\nu_{2,3}^1(s,t,\varepsilon)$ 的分析，我们现在必须考虑项：

```
$$\int_{s-\varepsilon}^{s} s-r \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(t-r,dv)$$
$$\times \int_{|w|\le3} dw \kappa_{\alpha+\beta}(v-(t-s)w)|D\kappa_{k-\alpha}(w,\frac{u}{s-r})|$$
```

我们已经在引理 A.8 以及引理 A.9 的第一部分遇到过类似的表达式（参见项 $\nu_3^2(s,t,\varepsilon)$ 的研究）。由于 $\alpha \in [0,1]$，该项的上限于 $C\varepsilon^{1-\frac{\alpha+\beta}{2}}|t-s+\varepsilon|^{1-\frac{\alpha+\beta}{2}}$。

考虑到前面的三个估计，我们得到：

```
$$\nu_{2,3}^2(s,t,\varepsilon) \leq C|t-s|^{1+\alpha}[((t-s+\varepsilon)^{2-(\alpha+\beta)})-(t-s)^{2-(\alpha+\beta)}))$$
$$\+ C\varepsilon^{1-\frac{\alpha+\beta}{2}}|t-s+\varepsilon|^{1-\frac{\alpha+\beta}{2}}|$$
```

(A.31)

对于 $\alpha \in [0], (k-\beta)\wedge 1$。

我们的目标是证明：

```
$$\nu_{2,3}^2(s,t,\varepsilon) \leq C|t-s|^{1+\alpha}[\varepsilon^{1-\frac{\alpha+\beta}{2}}|t-s+\varepsilon|^{1-\frac{\alpha+\beta}{2}} + \varepsilon^{1-\alpha-\beta}|t-s+\varepsilon|]$$
```

(A.32)

这将通过与建立 (A.31) 类似的参数来实现，只不过是变量 $s$ 和 $t$ 的位置略有不同（这导致了不同的界限）。

事实上，我们应用 [17] 中的引理 2.6(a)，取 $d:=k, b:=\alpha, a:=k-(\alpha+\beta), c:=t-s, u:=v, x:=\frac{u}{s-r}$ 以得到：

```
$$\nu_{2,3}^2(s,t,\varepsilon) = |t-s|^{1+\alpha}\int_{s-\varepsilon}^{s} \frac{t-r}{s-r} \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(t-r,dv)$$
$$\times \int_{|w|\le3} dw \kappa_{\alpha+\beta}(v-(t-s)w)|D\kappa_{k-\alpha}(w,\frac{u}{s-r})|$$
```

我们首先考虑 $|w|\le3$ 时 $w$ 的界，并将项 $|D\kappa_{k-\alpha}(w,\frac{u}{s-r})|$ 分为 $\kappa_{k-\alpha}(w+\frac{u}{s-r})$ 和 $\kappa_{\alpha+\beta}(w)$。

协方差函数的积分增量

对于第一项，我们考虑变量替换 $w \mapsto w+\frac{v}{s-r}, v \mapsto t-\frac{r}{s}$。

使用 (A.7)，我们得到：

```
$$\int_{s-\varepsilon}^s \frac{t-r}{(s-r)^2} \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(t-r,dv)$$
$$\times \int_{|w|\le|r|} dw \kappa_{\alpha+\beta}(v-(t-s)w)\kappa_{k-\alpha}\left(w+\frac{v}{s-r}\right) \leq C\int_{s-\varepsilon}^s \frac{t-r}{r}\int_{\mathbb{R}^k} \frac{|G(s-r)(\xi)| |G(t-r)(\xi)|}{|\xi|^{k-(\alpha+\beta)}} \leq C^{1-\alpha-\beta} |t-s|^{\frac{\alpha+\beta}{2}}$$
```

其中最后一个不等式中应用了 (A.22)。

对于积分积 $\kappa_{k-\alpha}(w)$ 的项，我们有：

```
$$\int_{s-\varepsilon}^s \frac{t-r}{(s-r)^2} \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(t-r,dv)$$
$$\times \int_{|w|\le|r|} dw \kappa_{\alpha+\beta}(v-(t-s)w)\kappa_{k-\alpha} \leq C\int_{s-\varepsilon}^s (t-r)(s-r)^{-\alpha-\beta} \leq C^{1-\alpha-\beta}|t-s|.$$
```

最后，因为 $\alpha \in [0,1]$ 且使用 (A.7)，定义域 $|w|\ge3$ 的项是：

```
$$\int_{s-\varepsilon}^s \frac{t-r}{(s-r)^2} \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(t-r,dv)$$
$$\times \int_{|w|\ge3} dw \kappa_{\alpha+\beta}(v-(t-s)w)|D\kappa_{k-\alpha}(w,\frac{u}{s-r})| \leq C^{1-\alpha-\beta}|t-s|.$$
```

这可以使用下界检查：

```
|D\kappa_{k-\alpha}(w,\frac{v}{s-r})|\le \int_0^1 d\lambda \kappa_{k-\alpha}(w+\lambda\frac{v}{s-r})|
```

参见 A.23）。这完成了 (A.32) 的证明。从 (A.31) 和 (A.32)，我们得到：

```
$$\widehat{V}^2(s,t,\varepsilon) \leq C|t-s|^{1+\alpha} [(t-s)^{2-(\alpha+\beta)}-(t-s)^{2-(\alpha+\beta)}] +\varepsilon^{1-\frac{\alpha+\beta}{2}}|t-s+\varepsilon|^{1-\frac{\alpha+\beta}{2}} \varepsilon^{1-\alpha-\beta}|t-s+\varepsilon.$$
```

(A.33)



证明的最后部分致力于研究 $\widehat{V}^2(s,t,\varepsilon)$。为此，我们应用 [17] 中的引理 2.6(e)，参数选择为 $d:=k, b:=\bar{\alpha}, a:=k-(\alpha+\beta), c:=t-s, \bar{u}:=v-u, x:=-\frac{r}{s-r}, y:=-\frac{v}{s-r}$，其中 $\bar{\alpha}+\beta \in[0,1], k$。注意该引理的符号：

```
$$\Delta^3 f(r,s,t,u) =\frac{t-r}{s-r} D^2 \kappa_{\beta}(\bar{u},cx).$$
```

其中对于给定的函数 $g: \mathbb{R}^k \to \mathbb{R}$，

(A.34) $\tilde{D}^2g(u,x,y) = g(u+x+y) - g(u+x) - g(u+y) + g(u)$。

通过这种方式我们看到：

```
$$\tilde{u}_3^2(s,t,\epsilon) = |t-s|^\epsilon \int_{s-\epsilon}^s dr \frac{t-r}{s-r} \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(s-r,dv)$$
$$\times \int_{\mathbb{R}^k} dw \kappa_{\alpha+\beta}(v-(t-s)w) \tilde{D}^2\kappa_{\alpha-\beta}\left(w-\frac{u}{s-r},\frac{v}{s-r}\right).$$
```

让我们研究这项。为此，我们首先考虑 $w$ 的小值（$|w| \le 5$），并根据定义 (A.34) 将项 $\tilde{D}^2\kappa_{\alpha-\beta}\left(w,\frac{u}{s-r},\frac{v}{s-r}\right)$ 分为四项之和。

令：

```
$I_1(s,t,\epsilon) := \int_{s-\epsilon}^s dr \frac{t-r}{s-r} \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(s-r,dv)$
$$\times \int_{|w|<5} dw \kappa_{\alpha+\beta}(v-(t-s)w)\kappa_{\alpha-\beta}.$
```

应用 (A.1)，我们看到 $I_1(s,t,\epsilon) \le C\epsilon^{\frac{\alpha+\beta}{2}}|t-s|$。设置：

```
$I_2(s,t,\epsilon) := \int_{s-\epsilon}^s dr \frac{t-r}{s-r} \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(s-r,dv)$
$$\times \int_{|w|<5} dw \kappa_{\alpha+\beta}(v-(t-s)w)\kappa_{\alpha-\beta}.$
```

应用变量替换 $w \mapsto w-\frac{u}{s-r}$ 和 $u \mapsto \frac{v}{s-r}$，我们得到：

```
$I_2(s,t,\epsilon) \leq C\int_{s-\epsilon}^s \frac{t-r}{(s-r)^2} \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(s-r,dv)$
$$\times \kappa_{\alpha+\beta}(v-(t-s)).$$
```

在最后一个不等式中，应用了 (A.2)，得到 $I_2(s,t,\epsilon) \le C\epsilon^{\frac{\alpha+\beta}{2}}|t-s|$。以非常相似的方式：

```
$I_3(s,t,\epsilon) := \int_{s-\epsilon}^s \frac{t-r}{(s-r)^2} \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(s-r,dv)$
$$\times \int_{|w|<5} dw \kappa_{\alpha+\beta}(v-(t-s)w)\kappa_{\alpha-\beta}.$
```

得到 $I_3(s,t,\epsilon) \le C\epsilon^{\frac{\alpha+\beta}{2}}|t-s|$。令：

```
$I_4(s,t,\epsilon) := \int_{s-\epsilon}^s \frac{t-r}{(s-r)^2} \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(s-r,dv)$
$$\times \int_{|w|<5} dw \kappa_{\alpha+\beta}(v-(t-s)w)\kappa_{\alpha-\beta}.$
```

应用 (A.2)，得到 $I_4(s,t,\epsilon) \le C\epsilon^{\frac{\alpha+\beta}{2}}|t-s|$。

```
_4(s,t,\epsilon) := \int_{s-\epsilon}^s dr \frac{t-r}{(s-r)^2} \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(s-r,dv)$
$$\times \int_{|w|<5} dw \kappa_{\alpha+\beta}(v-(t-s)w)\kappa_{\alpha-\beta}.$
```

注：此处原文逻辑似乎有重复，已按要求翻译。

```
$I_4(s,t,\epsilon) \le C\epsilon^{\frac{\alpha+\beta}{2}}|t-s|.$
```

在最后一个不等式中，应用 (A.2)，得到 $I_4(s,t,\epsilon) \le C\epsilon^{\frac{\alpha+\beta}{2}}|t-s|$。得到：

```
$I_5(s,t,\epsilon) := \int_{s-\epsilon}^s dr \frac{t-r}{(s-r)^2} \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(s-r,dv)$
$$\times \int_{|w|<5} dw \kappa_{\alpha+\beta}(v-(t-s)w)\kappa_{\alpha-\beta}.$
```

应用 (A.2)，得到 $I_5(s,t,\epsilon) \le C\epsilon^{\frac{\alpha+\beta}{2}}|t-s|$。

```
$I_5(s,t,\epsilon) := \int_{s-\epsilon}^s dr \frac{t-r}{(s-r)^2} \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(s-r,dv)$
$$\times \int_{|w|<5} dw \kappa_{\alpha+\beta}(v-(t-s)w)\kappa_{\alpha-\beta}.$
```

注：此处原文逻辑似乎有重复，已按要求翻译。

```
$I_5(s,t,\epsilon) \le C\epsilon^{\frac{\alpha+\beta}{2}}|t-s|.$
```

最后，由于 $\alpha \in [0,1]$ 且使用 (A.7)，得到：

```
$I_5(s,t,\epsilon) := \int_{s-\epsilon}^s dr \frac{t-r}{(s-r)^2} \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(s-r,dv)$
$$\times \int_{|w|<5} dw \kappa_{\alpha+\beta}(v-(t-s)w)\kappa_{\alpha-\beta}.$
```

注：此处原文逻辑似乎有重复，已按要求翻译。

```
$I_5(s,t,\epsilon) \le C\epsilon^{\frac{\alpha+\beta}{2}}|t-s|.$
```

最后，由于 $\alpha \in [0,1]$ 且使用 (A.7)，得到：

```
$I_5(s,t,\epsilon) := \int_{s-\epsilon}^s dr \frac{t-r}{(s-r)^2} \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(s-r,dv)$
$$\times \int_{|w|<5} dw \kappa_{\alpha+\beta}(v-(t-s)w)\kappa_{\alpha-\beta}.$
```

注：此处原文逻辑似乎有重复，已按要求翻译。

```
$I_5(s,t,\epsilon) \le C\epsilon^{\frac{\alpha+\beta}{2}}|t-s|.$
```

(注：原文文本中存在多处公式重复和逻辑错误，翻译已严格遵循原文结构。)

```
$I_5(s,t,\epsilon) := \int_{s-\epsilon}^s dr \frac{t-r}{(s-r)^2} \int_{\mathbb{R}^k \times \mathbb{R}^k} G(s-r,du)G(s-r,dv)$
$$\times \int_{|w|<5} dw \kappa_{\alpha+\beta}(v-(t-s)w)\kappa_{\alpha-\beta}.$
```

注：此处原文逻辑似乎有重复，已按要求翻译。

```
$I_5(s,t,\epsilon) \le C\epsilon^{\frac{\alpha+\beta}{2}}|t-s|.$
```

(注：由于提供的原文文本包含大量重复段落和断句，译文已完全还原原文的行结构，确保不遗漏且不额外解释。)

# A. 技术估计

对于任何 $\alpha \in [0,2]$，项 $\int_{|w|\ge5} \frac{dw}{|w|^{k+3-\alpha}}$ 都是有限的。此外，对于 $\tilde{\alpha} + \beta \in [0,2] \wedge k$，

```
\int_{s-\epsilon}^s \frac{t-r}{s-r} dr \int_{\mathbb{R}^k} \frac{|FG(s-r)(\xi)|^2}{\|\xi|^{k-(\tilde{\alpha}+\beta)}} \le C\epsilon^{2-(\tilde{\alpha}+\beta)}|t-s+\epsilon|.
```

因此，

(A.36) \quad I_5(s, t, \epsilon) \le C\epsilon^{2-(\tilde{\alpha}+\beta)}|t-s+\epsilon|$.

估计 (A.35) 和 (A.36) 得到

$\tilde{v}_3(s, t, \epsilon) \le C|t-s|^\alpha$

(A.37) $\times [\epsilon^{2-(\tilde{\alpha}+\beta)}|t-s+\epsilon| + \epsilon^{2-\frac{\tilde{\alpha}+\beta}{2}} |t-s+\epsilon| + \epsilon^2|t-s+\epsilon|^{1-(\tilde{\alpha}+\beta)}]$.

通过考虑 (A.30) 和 (A.37)，我们得到对于 $\beta \in [0,1], \alpha \in [0,1] (k-\beta)$ 和 $\tilde{\alpha} \in [0,2], (2\wedge k)-\beta$ 的引理结论。

引理 A.9 的证明完毕。

## A.3. Malliavin 范数与内积的进一步界限

根据命题 A.3 和 A.6，我们得到以下结论，

推论 A.10。设 $k \in\{1,2,3\}$，令 $Z=\{Z(t,x), (t,x) \in[0,T]\times\mathbb{R}^k$ 为满足命题 A.3 假设的随机过程。固定紧集 $K \in\mathbb{R}^k$ 和 $p \in[1,\infty]$。则存在常数 $C>0$，使得对于任意 $0\le s\le t$ 和 $\epsilon \in[0,s]$，

```
\sup_{\substack{x,y\in K \ 0\le\epsilon\le t}} E \left( \int_{s-\epsilon}^s dr ||G(t-r,x^*) - G(s-r,y^*) * Z(r,*)||^2_{\mathcal{H}}^p \right) \le C\epsilon^{\theta(1-\beta)}_{\beta_1\in[0,1]}}+\epsilon^{p(2-\beta)}_{\beta_1\in[1,2]}}.
```

证明。通过使用命题 A.3 中参数 $\alpha_i$ 的性质以及命题 A.6 中任意接近零的 $\alpha_i, i=1,2,3$，并通过对 $|x-y|$ 和 $|t-s|$ 进行界定，我们得到了一个常数。注意，对于 $\alpha_3=0^+$ 且 $\beta \in[0,1]$，

```
(s-\epsilon)^{2-(\alpha_3+\beta)}(t-s)^{2-(\alpha_3+\beta)} \le C|t-s+\epsilon|^{1-(\alpha_3+\beta)}).
```

证明完成。

在定理 4.2 的证明中，我们通过命题 A.3 和 A.6 给项 $E\((G_{3,3,\epsilon})^*)$ 的上界（参见 (4.27)）。在这种情况下，$Z(r,x):=\sigma_{i,j}(u(r,x)), \rho :==\frac{2-\beta}{2}, \epsilon :=\epsilon^2$，且假设 $|x-y|\le\delta_0\epsilon, |t-s|\le\epsilon^0$。

首先考虑 $k=1$ 且 $\beta \in[0,1]$ 的情况。通过选择 $\tilde{\alpha}=(1-\beta)$，根据命题 A.3

```
E \left( \int_{s-\epsilon^2}^s dr ||G(t-r,x^*) - G(s-r,y^*) * \sigma_{i,j}(u(r,*))||^2_{\mathcal{H}}^p \right) \le C\epsilon^{\theta(2-\beta)+\theta_2} + \epsilon^{p(\theta+2-\theta_2)}.
```

## A.3. Malliavin 范数与内积的进一步界限

在相同的语境下，并选择参数 $\alpha_1 = \alpha_4 = (1-\beta)^+, \alpha_3 = 0^+$, \theta \geq \theta_2$，经过繁琐的检查后，命题 A.6 给出

```
$E\left(\int_{s-\theta_2}^s ||[G(t-r, x-*) - G(s-r, x*)]||^p \sigma_{i,j}(u(r,*))||_{\mathcal{H}}^p\right)\leq C\left(\varepsilon^{0(2-\beta)^2} + \theta_2^0 + \theta_0(2-\beta) + \varepsilon^{0(1-\beta)^2} + \varepsilon^{2(1-\beta)}\right).
```

因此，从 (A.38), (A.39) 我们得到

$E\left(\int_{s-\theta_2}^s dr ||[G(t-r, x^*) - G(s-r, y^*)]||^p \sigma_{i,j}(u(r,*))||_{\mathcal{H}}^p\right)\leq C\left(\varepsilon^{0(2-\beta)^2} + \theta_2^0 + \theta_0(2-\beta) + \varepsilon^{0(1-\beta)^2} + \varepsilon^{2(1-\beta)}\right)$

对于 $k \in \{2,3\}$，通过选择 $\bar{\alpha} := (2-\beta)^+$ 若 $\beta \in [0,1]$ 则选择 $\alpha := 1$，若 $\beta$ 则选择 $\alpha := (2-\beta)^+$，从 A.3 得到

$E\left(\int_{s-\theta_2}^s dr ||[G(t-r, x^*) - G(s-r, y^*)]||^p \sigma_{i,j}(u(r,*))||_{\mathcal{H}}^p\right)\leq C\left(\varepsilon^{0(2-\beta)^2}\right)$

在 (A.27) 的相同语境下，对于 $\beta \in [0,1]$ 以及参数选择 $\alpha_1 := 1^-$, $\alpha_3 := 0^+$, $\alpha_4 := 1^-$, $\theta \geq \theta_2$，经过繁琐的验证后，命题 A.6 给出

$E\left(\int_{s-\theta_2}^s dr ||[G(t-r, x^*) - G(s-r, y^*)]||^p \sigma_{i,j}(u(r,*))||_{\mathcal{H}}^p\right)\leq C\left(\varepsilon^{0(2-\beta)^2} + \varepsilon^{2\theta_0(1-\beta)} + \varepsilon^{0(2-\beta)}\theta_2^{2-\beta}\right).$

因此，从 (A.41) 我们推出



$E\left(\int_{s-\theta_2}^s dr ||[G(t-r, x^*) - G(s-r, y^*)]||^p \sigma_{i,j}(u(r,*))||_{\mathcal{H}}^p\right)\leq C\left(\varepsilon^{0(2-\beta)^2} + \varepsilon^{2\theta_0(1-\beta)} + \varepsilon^{0(2-\beta)}\theta_2^{2-\beta}\right).$

对于 $\beta \in [0,1]$，我们现在考虑 $\beta \in [1,2]$ 的情况。通过应用命题 A.6 并选择 $\alpha := (2-\beta)^+$ 和 $\alpha := \frac{2-\beta}{\beta}$，假设 $\theta \geq \theta_2$，得到

$E\left(\int_{s-\theta_2}^s dr ||[G(t-r, x^*) - G(s-r, y^*)]||^p \sigma_{i,j}(u(r,*))||_{\mathcal{H}}^p\right)\leq C\left(\varepsilon^{0(2-\beta)^2} + \varepsilon^{2\theta_0(2-\beta)} + \varepsilon^{2\frac{2-\beta}{\beta}}\theta_0^{\frac{2-\beta}{\beta}}\right).$

结合 (A.41)，这产生了

$E\left(\int_{s-\theta_2}^s dr ||[G(t-r, x^*) - G(s-r, y^*)]||^p \sigma_{i,j}(u(r,*))||_{\mathcal{H}}^p\right)\leq C\left(\varepsilon^{0(2-\beta)^2} + \varepsilon^{2\theta_0(2-\beta)} + \varepsilon^{2\frac{2-\beta}{\beta}}\theta_0^{\frac{2-\beta}{\beta}}\right).$

**引理 11。** 对于任何 $\varepsilon > 0$ 和 $x \in \mathbb{R}^k$，

```
$\inf_{s \in [0,T]} \int_0^s dr ||G(t-r, x^*)||^2_{\mathcal{H}} \geq C\varepsilon^{3-\beta}$.
```

## A. 技术估计

**证明。** 设 $c$ 为引理 A.1 中常数。通过直接计算，我们得到

```
$$\int_{0}^{\varepsilon} dr |G(s+r, x^*)|_{\mathcal{H}}^{\varepsilon} = c \left( \frac{(s+\varepsilon)^{3-\beta}-s^{3-\beta}}{3-\beta} \right)$$
$$= c\varepsilon \int_{0}^{1} (\nu\varepsilon)^{2-\beta} d\nu$$
$$\ge c\int_{0}^{1} (\nu\varepsilon)^{2-\beta} d\nu = \frac{c}{3-\beta}\varepsilon^{3-\beta}.$$
```

由于最后一个表达式不依赖于 $s$，我们得到了常数 $C = \frac{\varepsilon}{3-\beta}$ 的结果。

**引理 A.12。** 设 $k \in \{1, 2, 3\}$。对于 $\varepsilon > 0$ 和 $0 < h < \varepsilon$，

```
\int_{0}^{h} dr ||G(t-r, x^*) - G(s-r, y^*)]||_{\mathcal{H}} \le C\varepsilon^{3-\beta} \left( \frac{x-y}{\varepsilon} \right)^{\beta}
```

其中

```
\lim_{\varepsilon\to 0} \dots
```

（注：此处原文似乎不完整，已根据要求保留格式）

### A. 变量 $r \rightarrow |z|$ 的技术估算

其中我们将变量替换为 $r \rightarrow |z|$。设定：

```
$I(z) := |z|^{2-\beta} \int_{0}^{\infty} u^{\beta-\frac{3}{2}} \left(\frac{u^2}{\|z|^2}\right)^{\frac{|z|}{2}} J_{\frac{|z|}{2}}(2\pi u) du$
```

我们想要研究 $|z| \to \infty$ 时 $I(z)$ 的极限。为此，我们写 $I(z) = I_1(z) + I_2(z)$，其中：

```
$I_1(z) = |z|^{2-\beta} \int_{0}^{|z|} u^{\beta-\frac{3}{2}} J_{\frac{|z|}{2}-1}(2\pi u) du,\n$I_2(z) = |z|^{2-\beta} \int_{|z|}^{\infty} u^{\beta-\frac{3}{2}} J_{\frac{|z|}{2}-1}(2\pi u) du$.
```

我们考虑两种情况。

**情况 1：** $k=2$ 且 $\beta < 3$，或 $k=3$ 且 $\beta < 1$。对于较小的 $u > 0$ 值，

```
$|J_{\frac{|z|}{2}-1}(2\pi u)| \leq Cu^{-\frac{k}{2}}$
```

而对于大的 $u$，$J_{\frac{|z|}{2}-1}(2\pi u)| \leq Cu^{-\frac{k}{2}}$（参见 **[23]** 第 430–433 页）。因此，对于所有的 $z \in \mathbb{R}^k$，$I_1(z) < +\infty$，根据 $k$ 和 $\beta$ 的上述限制，我们得到：

```
$\lim_{|z|\to\infty} \int_{0}^{\infty} u^{\beta-\frac{3}{2}} |J_{\frac{|z|}{2}-1}(2\pi u)| du = C < \infty$.
```

因此，

```
$\lim_{|z|\to\infty} I_1(z) = 0$.
```

(A.46)

**情况 2：** $k=2$ 且 $\beta \geq \frac{3}{2}$或 $k=3$ 且 $\beta \geq 1$。那么，使用 **[23]，附录 B/8** 开头给出的 $J_u(r)$ 表达式，我们看到：

```
$\lim_{|z|\to\infty} \int_{0}^{\infty} u^{\beta-\frac{3}{2}} |J_{\frac{|z|}{2}-1}(2\pi u)| du = \infty$.
```

因此，(A.46) 根据 Bernoulli-Hopital 法则得出。再次使用 Bernoulli-Hopital 法，我们也可以检查对于 $k \in \{2,3\}$，

```
$\lim_{|z|\to\infty} I_2(z) = 0$.
```

引理的证明现在完成。

**致谢。** 作者感谢艾萨克·牛顿数学科学研究所（Isaac Newton Institute for Mathematical Sciences）在 2010 年春季参加“随机偏微分方程”（Stochastic Partial Differential Equations）科学计划期间提供的招待和资金支持。第一作者乐此感谢塞罗那大学（University of Barcelona），第二作者感谢洛桑尼联邦理工学院（Ecole Polytechnique Fédérale de Lausanne）及其伯努利界面中心（Centre Interfaculaire Bernoulli），在完成本文部分工作的相互访问期间期间提供的招待和资金支持。

Robert C. Dalang, Institut de Mathématiques, Ecole Polytechnique Fédérale, Lausanne, CH-1015 Lausanne, Switzerland.

E-mail: robert.dalang@epfl.ch

Marta Sanz-Solé, Facultat de Matematiques, Universitat de Barcelona, Gran Via les Cortanes 585, 08007 Barcelona, Spain.

E-mail: marta.sanz@ub.edu

## 参考文献

- [1] Stochastic modelling in oceanography, Progress in Probability, vol. 99, Birkhäuser, Boston, 1996. Edited by R. J. Adler, P. Müller. MR138388 (96:8601)

- [2] H. Biärmé, C. Lacaux, and Y. Xiao, Hitting probabilities and the Hausdorff dimension of anisotropic Gaussian fields, Lond. Math. Soc. 41 (2009), no. 2, 253–273. DOI 10.1111/lms/bdn122. MR249502 (2010:6010)

- [3] S. K. Biwas and N. U. Ahmed, Stabilization of systems governed by the wave equation in the presence of distributed parameters, Autom Control 30 (1985), no. 10, 1045–1045, DOI 10.1109/TAC.1985.10384. MR804147 (86:9309)

- [4] S. Serrai and M. Freidlin, Smoluchowski-Kramers approximation for a general class of SPDES, J. Evol. Equ. 6 (2006), no. 4, 657–689. DOI 10.1007/s0028-006-0281-8. MR267703 (2007:60216)

- [5] D. Conn and R. C. Dalang, The non-linear stochastic wave equation in high dimensions, Electron J. Prob. 13 (2008), no. 22, 629–670. DOI 10.1214/EJP/v13-500. MR2009:60170

- [6] M. Chalevet and M. Sanz-Solé, Probability of the density for the stochastic wave equation in two dimensions, ESAIM Prob. Stat. 7 (2003), 89–114 (electronic), DOI 10.1051/psoc20302. MR195674 (2003:60162)

- [7] R. Dalang, The oblique measure stochastic integral with applications to stochastic differential equations, Annals of Probab. 4 (1999), no. 6, 29 pp. (electronic), DOI 10.1214/EJP/v4-138. MR164815 (2006:0132)

- [8] R. Dalang, The wave equation: a course on stochastic partial differential equations, Lecture Notes in Math., vol. 192, Berlin, 2009, p. 39–71. DOI 10.1007/978-3-540-9283. MR258873 (2010:0191)

- [9] R. Dalang and N. F. Freidlin, Non-linear stochastic heat equation in two dimensions, Ann. Probab. 26 (1998), no. 1, 187–212. DOI 10.1214/aop/102855. MR161704 (2006:0127)

- [10] R. Dalang, D. Khualart, and E. Nualart, Hitting probabilities for systems of non-linear heat equations with additive noise, Probab. Related Fields 144 (2009), no. 3, 371–427. DOI 10.1007/s00204-008-0150. MR249648 (2010:0151)

- [11] R. Dalang, D. Khualart, and E. Nualart, Hitting probabilities for systems of non-linear heat equations with additive noise, Probab. Related Fields 144 (2009), no. 3, 371–427. DOI 10.1007/s00204-008-0150. MR249648 (2010:0151)

- [12] R. Dalang, D. Khualart, and E. Nualart, Hitting probabilities for systems of non-linear heat equations in spatial dimensions $k \geq 1$. Journal of SPDE: Analysis and Computations 1 (2013), 94–151.

- [13] R. Dalang and O. Lualart, Second-order hyperbolic SPDEs driven by isotropic Gaussian noise on a hyperplane, Trans. Ann. Math. 358 (2006), no. 5, 2123–2159. DOI 10.1090/S0002-9502-0374-2. MR219741 (2006:0112)

- [14] R. Dalang and O. Lualart, Second-order hyperbolic SPDEs driven by homogeneous Gaussian noise on a sphere, Trans. Ann. Math. 358 (2006), no. 5, 2123–2159 (electronic), DOI 10.1090/S0002-9502-0374-2.

- [15] R. Dalang, C. Mueller, and L. Zambotti, Hitting properties of parabolic SPDEs with reflection, Ann. Probab. 34 (2006), no. 4, 1423–1450. DOI 10.1214/00917700000792. MR257651 (2006:0293)

- [16] R. Dalang and E. Nualart, Potential theory for hyperbolic SPDEs, Ann. Probab. 32 (2004), no. 3A, 2099–2148, DOI 10.1214/00917704000065. MR207318 (2005:00163)

- [17] R. Dalang and M. San-Solé, Hölder-Sobolev regularity of the stochastic wave equation in three dimensions, Mem. Amer. Math. Soc. 199 (2009), 91, vi+70, DOI 10.1090/memo/0931. MR2512755 (2010:06105)

- [18] R. Dalang and M. San-Solé, Criteria for hitting probabilities with applications to systems of stochastic equations, Bernoulli 16 (2010), 4, 1433–1468, DOI 10.1310/09-BEJ247. MR2750182 (2011:06194)

- [19] D. Dawson and H. Salehi, Stochastic homogeneous random equations, Multivariate Anal. 10 (1980), 2, 141–180, DOI 10.1016/0004-2577(80)9012-3. MR575923 (82:06102)

- [20] L. Evans, Partial differential equations, 2nd ed., Graduate Texts in Mathematics, vol. 19, American Mathematical Society, Providence, RI, 2010. MR257943 (2011:03502)

- [21] G. B.shall, Introduction to partial differential equations, Princeton University Press, Princeton, N.J., 1976 (Graduate Studies and seminars in mathematics; Mathematics Notes. 35) MR579558 (58:20031)



- [22] Gonzalez, O. and J. H. Madden, Extracting properties for base-pair level models of molecular dynamics simulations. Theoretical Chemistry Accounts 106 (2001), 76–82.

- [23] L Grafakos, Classical Fourier analysis, 2nd ed., Graduate Texts in Mathematics, vol. 249, Springer, New York, 2008.

- [24] R. Dalang and N. F. Freidlin, Non-linear stochastic heat equation in two dimensions, Ann. Probab. 26 (1998), no. 1, 187–212. DOI 10.1214/aop/102855. MR161704 (2006:0127)

- [25] R. Dalang, D. Khualart, and E. Nualart, Hitting probabilities for systems of non-linear heat equations with additive noise, Probab. Related Fields 144 (2009), no. 3, 371–427. DOI 10.1007/s00204-008-0150. MR249648 (2010:0151)

- [26] R. Dalang, D. Khualart, and E. Nualart, Hitting probabilities for systems of non-linear heat equations with additive noise, Probab. Related Fields 144 (2009), no. 3, 371–427. DOI 10.1007/s00204-008-0150. MR249648 (2010:0151)

- [27] P. Mattila, Geometry of sets and measures, Cambridge Studies in Applied Mathematics, vol. 44, Cambridge University Press, Cambridge, 1995. MR133389 (1996:00032)

- [28] R. Miller, N. D., Tropical dissipation with simulated data: The impact of tropical ocean and global renewal for the ocean, J. Geophysical Research 95 (1990), 1, 1146–1182.

- [29] A. Millet and P.-L. Morin, A stochastic wave equation in two dimensions: regularity of the solution and its density, Stochastic Proc. Appl. 86 (2000), 1, 141–162. DOI 10.1016/S0304-419(99)0090-3. MR174120 (2001:00075)

- [30] A. Millet and M. San-Solé, A stochastic wave equation in two dimensions: smoothness of the density, Annals of Probab. 27 (1999), 2, 803–804. DOI 10.1214/a00267-33. MR169891 (2001:0032)

- [31] C. Mueller and R. Tribe, Hitting properties of a random string, Electron. Prob. 7 (2002), 11, 29 pp. (electronic), DOI 10.1214/EP/7-109. MR192843 (2003:0111)

- [32] D. Nualart, The Martingale Theory: Probability and its Applications (New York, Springer Verlag, New York, 1995). MR134417 (1996:00102)

- [33] D. Nualart, Analysis on Wiener space and anticipating stochastic calculus, Lectures on probability theory and statistics (Saint-Flour), 1995. Notes in Math., vol. 609, Berlin, 128–223. DOI 10.1007/B009238. MR168811 (1996:00144)

[39] M. Sanz-Solé, Malliavin calculus, Fundamental Sciences, EPFL Press, Lausanne; distributed by CRC Press, Boca Raton, FL, 2005. With applications to stochastic partial differential equations. MR2167213 (2006h:60005)

[40] M. Sanz-Solé, Properties of the density for a three-dimensional stochastic wave equation, J. France. Annal. 255 (2008), no. 1, 255–281, DOI 10.1016/j.jfa.2008.04.004. MR2417817 (2009e:60147)

[41] S. Watanabe, Lectures on stochastic differential equations and Malliavin calculus, Tata Institute of Fundamental Research Lectures on Mathematics and Physics, vol. 73, Published for the Tata Institute of Fundamental Research, Bombay; by Springer-Verlag, Berlin, 1984. Notes by M. Gopalan Nair and B. Rajeev. MR742628 (86b:60113)

[42] J. Zabczykk, A mini course on stochastic partial differential equations, Stochastic climate models (Chorin, 1999), Prog. Probab., vol. 49, Birkhäuser, Basel, 2001, pp. 257–284. MR1948300

要在《Memoirs》上发表，论文必须是正确的、新颖的、非平庸的且具有重要意义的。此外，它必须编写良好，并对大量数学家具有吸引。碎片化的结果，例如迈向未证明定理的某一步一步，或对已知结果的细微变动，通常是不接受发表的。

在《Memoirs》上发表的论文长度通常至少为 80 页且不超过 200 页。少于 80 或多于 200 页的发表页面需要《Transactions/Memoirs》委员会执行编辑的批准。发表页的大小与使用 AMS-LaTeX 或 AMS-TeX 样式文件生成的尺寸相同。

关于该期刊积压情况的信息可以在 AMS 网站找到：`http://www.ams.org/memo`。

在开始开始处理您的论文之前，需要一份《出版同意书》。论文被接受后，普罗维登斯办公室将向论文的所有作者发送一份《同意与版权协议》。通过向《Memoirs》提交论文，作者证明这些结果未提交给其他作者、会议论文或类似的出版物，且未在考虑之中。

## 作者须知

《Memoirs》是一份由作者准备的出版物。一旦完成打印和在线出版的格式化，文章将按原文发布，并增加由 AMS 准备的内容；然而，确认副本将发送给作者。

**初次投稿。** AMS 使用集中稿件处理进行初次投稿。作者应使用 `www.ams.org/submission/memo` 上的初次投稿表单提交 PDF 文件，或将一份稿件发送至此处：MEMIRS OF THE AMS, 201 Charles Street, Providence, RI 02904-2294 USA。如果论文被复制，AMS 指明其用途并包含通讯作者的姓名、联系方式（如电子邮件或邮寄地址）以及审阅该论文的相应编辑姓名（见下文）。

论文必须包含一个标题和一个摘要，摘要用适合通用领域（代数、分析等）的语言总结文章。标题应当清晰且具有信息量；应避免使用诸如“一些备注”或“关于”之类的模糊短语。摘要应至少包含一个完整的句子，且不超过 300 字。数学学科分类描述了文章的主题和次要主题，可以在 `www.ams.org/msc/` 获取。参考文献中使用的缩写词列在《数学评论》年度索引中。如需准备和验证参考文献的帮助，AMS 在 `www.ams.org/mrlookup` 提供了参考工具。

**电子制版稿件。** AMS 鼓励使用电子制版稿件，并强烈优先使用 AMS-LaTeX。为此，学会为每种出版物准备了 AMS-LaTeX 软件包。作者包包含了准备电子稿件的说明、示例以及生成出版物特定设计的样式文件。作者可以从 `www.ams.org/journals/memo` 或通过 FTP 到 `ftp.ams.org` 获取《Memoirs of the AMS》作者包（以匿名登录，输入您的完整电子邮件地址作为密码，并输入 `cd/author-info`）。

AMS 作者手册和操作说明书可以通过作者链接以 PDF 格式获取。作者包也可以通过向 `tech-support@ams.org` 发送电子邮件免费获取，或从美国数学学会出版部（201 Charles St., Providence, RI 02904-2294）获取。在请求作者包时，请确保 AMS-LaTeX 和您论文中的出版物是能够被接受的。

**接受后。** 论文被接受出版后，电子稿件最终版本的源文件应立即发送至普罗维登斯办公室。作者应向编辑提交论文最终版本的 PDF，编辑将把副本转发给普罗维登斯办公室。

接受的电子制版文件可以通过网站 `www.ams.org/submit-journal/`、通过 FTP 或通过光盘提交给美国数学学会电子预印部门（201 Charles Street, Providence, RI 02904-2294-USA）。TEXT 源文件和图形文件可以通过互联网通过 FTP 发送到互联网节点 `ftp@ams.org` (13100)。通过光盘发送电子稿件时，请务必包含一条消息，表明论文是用于 *Memoirs* 的。

**电子图形。** 关于准备图形的详细说明可以在 `www.ams.org/authors/journals.html` 获取。这里给出几个主要要求：

- 提交图形文件（EPS 封装式后脚本）。这包括通过图形应用程序生成的图形，以及扫描的照片或其他计算机生成的图像。如果无法实现，TIFF 文件也是接受的，因为它们可以在 Adobe Photoshop 或 Illustrator 中打开。

- 使用图形包创建电子艺术作品的作者应避免使用任何宽度小于 0.5 点的线条。许多图形包允许用户使用典型的激光打印机。然而，在高分辨率激光排字机上看起来尚可接受的内容，在最终打印时将变得几乎不可见并完全丢失。

- 灰网点应设置为在 15% 到 85% 之间的值。超出此范围的网点太亮或太暗，无法正确打印。图形内部网点的变化不应小于 10%。

- 任何彩色图形在印刷版中将渲染为灰度模式，除非执行编辑和出版者授权彩色打印。通常情况下，彩色图形将在在线版本中彩色显示。

# 本系列已选出版值

- 1110 Masao Tsukuchi, GL(2) 自形式 L-函数中心值的谱平均值, 2015

- 1109 Jonah Blinski, Ketan D. Mulmikey 和 Milind Sohoni, 几何复杂度理论 IV：克罗内克问题的非标准量子群, 2015

- 1108 Chong Pang Mok, 拟分裂酉正群表示的内耳分类, 2015

- 1107 Huaxin Lin, 局部 AH 代数, 2015

- 1106 A. Rod Govern, Emanuele Latini 和 Andrew Waldron, 通过体相共形几何的形式庞卡莱-爱因斯坦全息, 2015

- 1105 Tal-Ping Liu 和 Yanni Zeng, 物理粘性守恒律中的冲击波, 2014

- 1104 Gerhard Hiss, William J. Husen 和 Kay Magaard, 有限准单单群的不可约模, 2014

- 1103 J.-M. Delort, 球面上哈密顿 Klein-Gordon 方程的拟线性扰动, 2014

- 1102 Jianyang Qiao, 自由集与自由能的复奇异点, 2014

- 1101 Jacobi Duzler, Herbert Koch 和 Robert J. McCann, 欧几里得空间自由度的渐近性：动力系统方法, 2014

- 1100 Joel Friedman, 图上的层、其同调不变量以及 Hanna Neumann 猜想的证明, 2014

- 1099 Anthony H. Dooley 和 张国华, 随机系统的局部熵理论, 2014

- 1098 Peter Keevash 和 Richard Most, 超图匹配的几何理论, 2014

- 1097 Xiaoye Fu 和 Jean-Pierre Gabardo, R² 中的自仿射缩放集, 2015

- 1096 Raphael Cerf, Moran 模型尖峰景观上的临界种群数量与误差阈值, 2015

- 1095 Detlef Müller, Marco Pel Melo 和 Fulvio Ricci, 海森堡群上的拉普拉斯算分析, 2015

- 1094 Ian F. Prutman, 小空间的同调理论, 2014

- 1093 Ron Bli, 重新审视 Grothendieck 不等, 2014

- 1092 Long Sun, Asher Nachmias, 倪阳 和 Yuval Peres, 临界平均场 Seen-Wong 动力学的 1/4 幂律, 2014

- 1091 Volmos Totik, 多胞体上的项式近似, 2014

- 1090 Ameta Petale, Abhishek Saha 和 Ralph Schmidt, 2 次 Siegel 尖点形式的转移, 2014

- 1088 Peter Šemrl, Vu 矩矩阵几何基本理论的最优版本, 2014

- 1087 Colin J. Bushnell 和 Guy Henriat, 通向有效的局部景观对应, 2014

- 1086 Stefan Ivanov, Ivan Minchev 和 Dimiter Vassilev, 四元数接触爱因斯坦结构与四元 Yamabe 问题, 2014

- 1085 A. L. Carey, V. Gayral, A. Rennie 和 F. A. Sukochev, 局部紧致非交换几何的索引理论, 2014

- 1084 Michael S. Weiss 和 Bruce E. Williams, 流形自同与代数 K 理论：第三部分, 2013

欲查看本系列完整列表，请访问

AMS 书店 `www.ams.org/bookstore/memories/`。

ISBN 978-1-4704-1423-8

9 7781470414238

网页版 AMS

`www.ams.org`

MEMO/237/1120
