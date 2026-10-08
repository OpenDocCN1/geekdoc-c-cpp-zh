

## 7.2 几何圆拟合的 Cramer-Rao 界

照例，$\mathbf{I}_{n}$ 表示 $n$ 阶单位矩阵。接下来我们应用标准的分块矩阵求逆引理（参见 [128] 第 26 页），得到

$$
\left[\begin{array}{cc}\mathbf{K} & \mathbf{L}^{T} \\ \mathbf{L} & R^{2} \mathbf{I}_{n}\end{array}\right]^{-1}=\left[\begin{array}{cc}\left(\mathbf{K}-R^{-2} \mathbf{L}^{T} \mathbf{L}\right)^{-1} & -\left(R^{2} \mathbf{K}-\mathbf{L}^{T} \mathbf{L}\right)^{-1} \mathbf{L}^{T} \\ -\mathbf{L}\left(R^{2} \mathbf{K}-\mathbf{L}^{T} \mathbf{L}\right)^{-1} & \left(R^{2} \mathbf{I}_{n}-\mathbf{L K}^{-1} \mathbf{L}^{T}\right)^{-1}\end{array}\right].
$$

通过直接相乘可以轻松验证该公式。最后一个矩阵左上角的 $3 \times 3$ 分块对我们来说最感兴趣，因为它对应于主要参数 $a,b,R$。用之前公式 (7.4) 中引入的矩阵 $\mathbf{W}$ 来表示，我们有 $\hat{u}_{i}=\cos \varphi_{i}$ 和 $\hat{v}_{i}=\sin \varphi_{i}$，因此

$$
\mathbf{K}-R^{-2} \mathbf{L}^{T} \mathbf{L}=\mathbf{W}^{T} \mathbf{W},
$$

从而 Cramer-Rao 界表示为

$$
\mathbb{E}\left[\left(\Delta \hat{\boldsymbol{\theta}}\right)\left(\Delta \hat{\boldsymbol{\theta}}\right)^{T}\right] \geq \sigma^{2}\left(\mathbf{W}^{T} \mathbf{W}\right)^{-1}.\tag{7.13}
$$

统计学界熟知这一结果，尽管不清楚是谁最先推导出了它。显然 Chan 在 1965 年就知道这一点，参见 [31] 第 53 页，尽管他没有明确陈述。以显式形式发表这一结果的是 1995 年的 Chan 和 Thomas [35]，但他们的论证存在些许缺陷。正确的论证由 Kanatani [96] 在 1998 年给出，并且 Zelniker 和 Clarkson [196] 在 2006 年也独立给出了相同论证。

**无偏性限制。** 关于上述结果的实用相关性，有几条评论是必要的。Cramer-Rao 定理仅确立了*无偏*估计量的最小方差。在将非线性曲线拟合到数据的情况下，不存在无偏估计量这种奢侈；特别是*所有*圆拟合算法都在某种程度上是有偏的（有时偏倚严重）；参见第 6.10 节。因此，界 (7.13) 是否具有实用价值并不立即清晰，即它是否适用于任何圆拟合。

实际上它是适用的，正如我们在第 6.9 节中解释的那样，如果将分析限制在主项（$\sigma^{2}$ 阶）上。公式 (7.13) 的右侧给出了协方差矩阵*主项*的下界，即

$$
\mathbf{V} \geq\left(\mathbf{W}^{T} \mathbf{W}\right)^{-1}.\tag{7.14}
$$

这对于任何几何一致的圆拟合都是成立的，即任何满足 (6.19) 的拟合。因此 (7.14) 适用于几何圆拟合以及所有已知的代数圆拟合。

**总结。** 比较 (7.6) 和 (7.14) 表明，几何圆拟合在主项上具有最小可能的方差。稍后将确立代数圆拟合具有类似的事实；届时我们将看到，所有已知的圆拟合都具有最小可能的方差 $\mathbf{V}$，即 $\mathbf{V}_{\text {min }}=(\mathbf{W}^{T} \mathbf{W})^{-1}$。

另一方面，几何圆拟合的本质偏倚并不消失，它由 (7.9) 给出。那么一个自然的问题是：本质偏倚 (7.9) 是否也达到了其自然最小值，或者它可以被减少？我们将在接下来的几节中看到，本质偏倚*可以*被减少，并且实际上可以*消除*。

## 7.3 代数圆拟合的误差分析

在此，我们分析第 5 章中描述的代数圆拟合，包括 Kasa 拟合、Pratt 拟合和 Taubin 拟合。

**代数圆拟合回顾（第 5.11 节）。** 让我们再次用代数方程描述圆

$$
A\left(x^{2}+y^{2}\right)+B x+C y+D=0,
$$

其中 $\mathbf{A}=(A, B, C, D)^{T}$ 是 4 参数向量。回顾一下，每个代数拟合都等价于最小化

$$
\begin{gathered} \mathscr{F}(A, B, C, D)=\frac{1}{n} \sum_{i=1}^{n}\left(A z_{i}+B x_{i}+C y_{i}+D\right)^{2} \\ =n^{-1} \mathbf{A}^{T}\left(\mathbf{X}^{T} \mathbf{X}\right) \mathbf{A}=\mathbf{A}^{T} \mathbf{M A}, \end{gathered}
$$

受限于约束

$$
\mathbf{A}^{T} \mathbf{N A}=1
$$

其中 $\mathbf{N}$ 是某个矩阵。这里我们使用简写符号 $z_{i}=x_{i}^{2}+y_{i}^{2}$ 以及

$$
\mathbf{M}=\frac{1}{n} \mathbf{X}^{T} \mathbf{X}=\left[\begin{array}{cccc} \overline{z z} & \overline{z x} & \overline{z y} & \bar{z} \\ \overline{x z} & \overline{x x} & \overline{x y} & \bar{x} \\ \overline{y z} & \overline{y x} & \overline{y y} & \bar{y} \\ \overline{z} & \bar{x} & \bar{y} & 1 \end{array}\right],
$$

其中

$$
\mathbf{X}=\left[\begin{array}{cccc} z_{1} & x_{1} & y_{1} & 1 \\ \vdots & \vdots & \vdots & \vdots \\ z_{n} & x_{n} & y_{n} & 1 \end{array}\right].
$$

约束矩阵 $\mathbf{N}$ 在 (7.17) 中决定了特定的代数拟合。对于 Kasa 拟合，它是

$$
\mathbf{N}=\mathbf{K}=\left[\begin{array}{cccc} 1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{array}\right]
$$

参见 (5.39)，

$$
\mathbf{N}=\mathbf{P}=\left[\begin{array}{cccc} 0 & 0 & 0 & -2 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ -2 & 0 & 0 & 0 \end{array}\right] \quad (7.20)
$$

对于 Pratt 拟合，参见 (5.27)，以及

$$
\mathbf{N}=\mathbf{T}=\left[\begin{array}{cccc} 4\bar{z} & 2\bar{x} & 2\bar{y} & 0 \\ 2\bar{x} & 1 & 0 & 0 \\ 2\bar{y} & 0 & 1 & 0 \\ 0 & 0 & 0 & 0 \end{array}\right], \quad (7.21)
$$

对于 Taubin 拟合，参见 (5.48)；这里我们再次使用标准的“样本均值”符号 $\bar{z} = \frac{1}{n}\sum z_i$ 等。

带约束的最优化问题 (7.16)–(7.17) 简化为广义特征值问题

$$
\mathbf{M}\mathbf{A} = \eta \mathbf{N}\mathbf{A}, \quad (7.22)
$$

因此 $\mathbf{A}$ 必须是矩阵对 $(\mathbf{M}, \mathbf{N})$ 的广义特征向量。为了找到最优化问题 (7.16)–(7.17) 的解，我们必须选择具有最小非负特征值 $\eta$ 的特征向量 $\mathbf{A}$。这一事实将 $\mathbf{A}$ 确定到一个标量倍数；由于将 $\mathbf{A}$ 乘以标量不改变它所代表的圆，我们可以设 $\|\mathbf{A}\| = 1$。

**矩阵摄动方法。** 由于代数拟合可以方便地用矩阵形式表达，我们按照 Kanatani [104] 的方法对矩阵进行误差分析。对于每一个随机变量、矩阵或向量 $\mathbf{Z}$，我们写为

$$
\mathbf{Z} = \tilde{\mathbf{Z}} + \Delta_1\mathbf{Z} + \Delta_2\mathbf{Z} + \mathscr{O}_P(\sigma^3), \quad (7.23)
$$

其中 $\tilde{\mathbf{Z}}$ 是其“真实”的非随机值（在 $\sigma$ = 0 时达到），$\Delta_1\mathbf{Z}$ 是 $\delta_i$ 和 $\varepsilon_i$ 的线性组合，而 $\Delta_2\mathbf{Z}$ 是 $\delta_i$ 和 $\varepsilon_i$ 的二次型；所有更高阶项（三次等）由 $\mathscr{O}_P(\sigma^3)$ 表示。为了简洁，我们在随后的公式中省略了 $\mathscr{O}_P(\sigma^3)$ 项。

还要注意 $\tilde{\mathbf{M}}\tilde{\mathbf{A}}$ = $\mathbf{0}$，以及 $\tilde{\mathbf{X}}\tilde{\mathbf{A}}$ = $\mathbf{0}$，因为真实点位于真实圆上。这意味着

$$
\tilde{\mathbf{A}}^T \Delta_1\mathbf{M}\tilde{\mathbf{A}} = n^{-1} \tilde{\mathbf{A}}^T(\tilde{\mathbf{X}}^T\Delta_1\mathbf{X} + \Delta_1\mathbf{X}^T\tilde{\mathbf{X}})\tilde{\mathbf{A}} = \mathbf{0},
$$

因此 $\mathbf{A}^T\mathbf{M}\mathbf{A}$ = $\mathscr{O}_P(\sigma^2)$，并且左乘 (7.22) 以 $\mathbf{A}^T$ 得到 $\eta$ = $\mathscr{O}_P(\sigma^2)$。

接下来我们将 (7.22) 展开到二阶项，根据一般规则 (7.23)，并省略 $\mathscr{O}_P(\sigma^3)$ 项，得到

$$
(\tilde{\mathbf{M}} + \Delta_1\mathbf{M} + \Delta_2\mathbf{M})(\tilde{\mathbf{A}} + \Delta_1\mathbf{A} + \Delta_2\mathbf{A}) = \eta\tilde{\mathbf{N}}\tilde{\mathbf{A}} \quad (7.24)
$$

（回想一下，对于 Taubin 方法 $\mathbf{N}$ 依赖于数据，但只有其“真实”值 $\widetilde{\mathbf{N}}$ 重要，因为 $\eta = \overline{\sigma}_{P}(\sigma^{2})$）。

公式 (7.24) 的左边由线性部分（$\widetilde{\mathbf{M}}\boldsymbol{\Delta_{1}}\mathbf{A}+\boldsymbol{\Delta_{1}}\mathbf{M}\widetilde{\mathbf{A}}$）和二次部分（$\widetilde{\mathbf{M}}\boldsymbol{\Delta_{2}}\mathbf{A}+\boldsymbol{\Delta_{1}}\mathbf{M}\boldsymbol{\Delta_{1}}\mathbf{A}+\boldsymbol{\Delta_{2}}\mathbf{M}\widetilde{\mathbf{A}}$）组成。右边是二次的。分离线性和二次项得到

$$
\widetilde{\mathbf{M}}\boldsymbol{\Delta_{1}}\mathbf{A}+n^{-1}\widetilde{\mathbf{X}^{T}}\boldsymbol{\Delta_{1}\mathbf{X}\widetilde{\mathbf{A}}}=\mathbf{0} \quad (7.25)
$$

并再次省略 $\mathcal{O}_{P}(\sigma^{3})$ 项，

$$
\widetilde{\mathbf{M}}\boldsymbol{\Delta_{2}}\mathbf{A}+\boldsymbol{\Delta_{1}}\mathbf{M}\boldsymbol{\Delta_{1}}\mathbf{A}+\boldsymbol{\Delta_{2}}\mathbf{M}\widetilde{\mathbf{A}}=\eta\widetilde{\mathbf{N}\widetilde{\mathbf{A}}}.\quad (7.26)
$$

注意 $\widetilde{\mathbf{M}}$ 是一个奇异矩阵（因为 $\widetilde{\mathbf{M}}\widetilde{\mathbf{A}}=\mathbf{0}$），但只要至少有三个不同的真实点，它们就确定唯一的真实圆，因此 $\widetilde{\mathbf{M}}$ 的核是一维的，并且与一维向量空间 $\mathrm{span}(\widetilde{\mathbf{A}})$ 重合。此外，由于我们设 $\|\widetilde{\mathbf{A}}\|=1$，我们看到

$$
1 = \|\widetilde{\mathbf{A}} + \boldsymbol{\Delta_{1}}\mathbf{A}\|^{2} = \|\widetilde{\mathbf{A}}\|^{2} + 2\widetilde{\mathbf{A}}^{T}\boldsymbol{\Delta_{1}}\mathbf{A} + \mathcal{O}_{P}(\sigma^{2}),
$$

因此 $\widetilde{\mathbf{A}}^{T}\boldsymbol{\Delta_{1}}\mathbf{A} = 0$，即 $\boldsymbol{\Delta_{1}}\mathbf{A}$ 正交于 $\widetilde{\mathbf{A}}$。因此我们可以写为

$$
\boldsymbol{\Delta_{1}}\mathbf{A}=-n^{-1}\widetilde{\mathbf{M}^{-}}\widetilde{\mathbf{X}^{T}}\boldsymbol{\Delta_{1}\mathbf{X}\widetilde{\mathbf{A}}}, \quad (7.27)
$$

其中 $\widetilde{\mathbf{M}^{-}}$ 表示 Moore-Penrose 伪逆。注意 $\mathbb{E}(\boldsymbol{\Delta_{1}}\mathbf{A}) = 0$。

## 7.4 代数圆拟合的方差和偏倚

在此，我们使用之前的误差分析来推导代数圆拟合在参数 $A, B, C, D$ 中的方差和偏倚的显式公式。自然的几何参数 $a, b, R$ 将在第 7.6 节中处理。

**代数圆拟合的方差。** 主项的方差为

$$
\begin{aligned} \mathbb{E}\left[\left(\boldsymbol{\Delta_{1}}\mathbf{A}\right)\left(\boldsymbol{\Delta_{1}}\mathbf{A}\right)^{T}\right]= & n^{-2}\widetilde{\mathbf{M}^{-}}\widetilde{\mathbf{X}^{T}}\mathbb{E}\left[\boldsymbol{\Delta_{1}\mathbf{X}\widetilde{\mathbf{A}}\widetilde{\mathbf{A}}^{T}\boldsymbol{\Delta_{1}\mathbf{X}^{T}\widetilde{\mathbf{X}}^{T}}\right]\widetilde{\mathbf{M}^{-}} \text{ } & =n^{-2}\widetilde{\mathbf{M}^{-}}\mathbb{E}\left[\left(\sum_{i}\widetilde{\mathbf{X}_{i}}\boldsymbol{\Delta_{1}\mathbf{X}_{i}^{T}}\right)\widetilde{\mathbf{A}}\widetilde{\mathbf{A}}^{T}\left(\sum_{j}\boldsymbol{\Delta_{1}\mathbf{X}_{j}^{T}\widetilde{\mathbf{X}_{j}}^{T}}\right)\right]\widetilde{\mathbf{M}^{-}}, \end{aligned} \quad (7.28)
$$

其中

$$
\widetilde{\mathbf{X}_{i}}=\left[\begin{array}{c} \widetilde{z_{i}} \\ \widetilde{x_{i}} \\ \widetilde{y_{i}} \\ 1 \end{array}\right] \quad \text { 且 } \quad \boldsymbol{\Delta_{1}\mathbf{X}_{i}}=\left[\begin{array}{c} 2\widetilde{x_{i}\delta_{i}}+2\widetilde{y_{i}\varepsilon_{i}} \\ \delta_{i} \\ \varepsilon_{i} \\ 0 \end{array}\right]
$$

分别表示矩阵 $\widetilde{\mathbf{X}^{T}}$ 和 $\boldsymbol{\Delta_{1}\mathbf{X}^{T}}$ 的列。观察到

$$
\mathbb{E}\left[\left(\boldsymbol{\Delta_{1}\mathbf{X}_{i}}\right)\left(\boldsymbol{\Delta_{1}\mathbf{X}_{j}}\right)^{T}\right]=\left\{\begin{array}{ccc} 0 & \text { 当 } & i \neq j \\ \sigma^{2}\widetilde{\mathbf{T}_{i}} & \text { 当 } & i=j \end{array}\right.
$$

