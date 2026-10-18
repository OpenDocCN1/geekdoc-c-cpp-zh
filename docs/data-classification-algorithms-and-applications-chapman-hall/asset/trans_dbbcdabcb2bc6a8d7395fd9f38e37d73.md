
假设我们想得到的投影矩阵在特征空间中为 $\mathbf{W}^{\phi}$，那么根据表示定理

$$\mathbf{W}^{\phi}=\Phi\alpha \tag{18.10}$$

其中 $\Phi=[\phi(\mathbf{x}_1),\phi(\mathbf{x}_2),\cdots,\phi(\mathbf{x}_n)]$，$\alpha$ 是对所有 $\phi(\mathbf{x}_i)$（$1\leq i\leq n$）的系数向量。我们将 $\mathbf{K}=\Phi^\mathrm{T}\Phi$ 定义为核矩阵。

于是

$$\begin{aligned}
(\mathbf{W}^{\phi})^\mathrm{T}\Sigma_C^{\phi}\mathbf{W}^{\phi}
&=\alpha^\mathrm{T}\left[\frac{1}{C}\sum_{c=1}^{C}\frac{1}{n_c}\sum_{\mathbf{x}_i\in c}\Phi^\mathrm{T}(\phi(\mathbf{x}_i)-\bar{\phi}_c)(\phi(\mathbf{x}_i)-\bar{\phi}_c)^\mathrm{T}\Phi\right]\alpha \\
&=\alpha^\mathrm{T}\left[\frac{1}{C}\sum_{c=1}^{C}\frac{1}{n_c}\sum_{\mathbf{x}_i\in c}(\mathbf{K}_{\cdot i}-\bar{\mathbf{K}}_{\cdot c})(\mathbf{K}_{\cdot i}-\bar{\mathbf{K}}_{\cdot c})^\mathrm{T}\right]\alpha \\
&=\alpha^\mathrm{T}\mathbf{M}_C\alpha
\end{aligned} \tag{18.11}$$

其中 $\mathbf{K}_{\cdot i}=\Phi^{\mathrm{T}}\phi(\mathbf{x}_i)$，$\bar{\mathbf{K}}_{\cdot c}=\frac{1}{n_c}\sum_{\mathbf{x}_i\in c}\mathbf{K}_{\cdot i}$。

$$\begin{aligned}
(\mathbf{W}^{\phi})^\mathrm{T}\Sigma_S^{\phi}\mathbf{W}^{\phi}
=\alpha^\mathrm{T}\left[\frac{1}{C}\sum_c(\bar{\mathbf{K}}_{\cdot c}-\bar{\mathbf{K}}_{\cdot *})(\bar{\mathbf{K}}_{\cdot c}-\bar{\mathbf{K}}_{\cdot *})^\mathrm{T}\right]\alpha
=\alpha^\mathrm{T}\mathbf{M}_S\alpha
\end{aligned} \tag{18.12}$$

其中 $\mathbf{K}_{\cdot *}=\frac{1}{n}\sum_{i=1}^{n}\mathbf{K}_{\cdot i}$。因此，我们可以通过求解下面的问题来得到 $\alpha$：

$$\min_{\alpha^\mathrm{T}\alpha=1}\frac{\operatorname{tr}(\alpha^\mathrm{T}\mathbf{M}_C\alpha)}{\operatorname{tr}(\alpha^\mathrm{T}\mathbf{M}_S\alpha)}. \tag{18.13}$$

### 18.3.2 边际最大化判别分析（MMDA）

MMDA 可以看作是*支持向量机*（SVM）算法 [21] 的一种扩展。假设数据点 $\mathbf{X}=[\mathbf{x}_1,\mathbf{x}_2,\cdots,\mathbf{x}_n]$ 来自两个类别，$\mathbf{x}_i$ 的标签为 $l_i\in\{-1,+1\}$。回顾一下，SVM 的目标是找到将 $l_i=1$ 的点与 $l_i=-1$ 的点分开的最大间隔超平面（因此它是一种有监督方法）。任何超平面都可以写成满足下式的点集 $\mathbf{x}$：

$$\mathbf{w}^{\mathrm{T}}\mathbf{x}-b=0 \tag{18.14}$$

其中 $b/\|\mathbf{w}\|$ 对应超平面到原点的距离。SVM 旨在选择 $\mathbf{w}$ 和 $b$，使得在仍能区分数据的前提下，尽可能远地分开两个平行超平面之间的距离，这通常被称为两个类别的间隔。这些超平面可以用以下方程描述：

$$\mathbf{w}^{\mathrm{T}}\mathbf{x}-b=1\quad\text{或}\quad\mathbf{w}^{\mathrm{T}}\mathbf{x}-b=-1. \tag{18.15}$$

这两个平行超平面之间的距离为 $2/\|\mathbf{w}\|$。那么，如果来自两个类别的数据被清晰分开，SVM 的目标是求解以下优化问题，以找到使两个类别之间间隔最大的超平面：

$$\begin{aligned}
\min_{\mathbf{w},b}\quad & \frac{1}{2}\|\mathbf{w}\|^2 \\
\text{s.t.}\quad & l_i(\mathbf{w}^{\mathrm{T}}\mathbf{x}_i-b)\geq 1\quad(\forall i=1,2,\cdots,n).
\end{aligned} \tag{18.16}$$

然而在现实中，两个类别可能不是完全可分的，即它们之间可能存在一些重叠。这时我们需要*软间隔*SVM，其目标是求解：

$$\begin{aligned}
\min_{\mathbf{w},b,\boldsymbol{\xi}}\quad & \frac{1}{2}\|\mathbf{w}\|^2+C\sum_{i=1}^{n}\xi_i \\
\text{s.t.}\quad & l_i(\mathbf{w}^{\mathrm T}\mathbf{x}_i-b)\ge 1-\xi_i,\quad (\forall i=1,2,\ldots,n)
\end{aligned} \tag{18.17}$$

其中 $\{\xi_i\}\ge 0$ 是松弛变量，用于惩罚重叠区域上的间隔。

MMDA 旨在求解多个投影方向，并且它旨在求解以下优化问题：

$$\begin{aligned}
\min_{\mathbf{W},b,\boldsymbol{\xi}_r\ge 0}\quad & \frac{1}{2}\sum_{r=1}^{d}\|\mathbf{w}_r\|^2+\frac{C}{n}\sum_{r=1}^{d}\sum_{i=1}^{n}\xi_{ri} \\
\text{s.t.}\quad & \forall i=1,\ldots,n,\quad r=1,\ldots,d \\
& l_i\left((\mathbf{w}_r)^{\mathrm T}\mathbf{x}_i+b\right)\ge 1-\xi_{ri}, \\
& \mathbf{W}^{\mathrm T}\mathbf{W}=\mathbf{I}.
\end{aligned} \tag{18.18}$$

因此，MMDA 是一种全局且线性的方法。我们也可以应用核技巧使其非线性化；具体细节可参见 [11]。学习到的 $\mathbf{x}_i$ 与 $\mathbf{x}_j$ 之间的距离就是 $\mathbf{W}^{\mathrm T}\mathbf{x}_i$ 与 $\mathbf{W}^{\mathrm T}\mathbf{x}_j$ 之间的欧氏距离。

### 18.3.3 利用辅助信息学习（LSI）

LDA 和 MMDA 都使用数据标签作为监督信息。正如我们在 18.3 节开头所介绍的，我们考虑的另一类监督信息是成对约束。数据标签信息更严格，因为我们可以将数据标签转换为成对约束，但反之则不行。

最早利用成对约束来学习合适距离度量的研究之一是*利用辅助信息学习（LSI）*方法 [28]。我们将*必须链接*约束集记为 $\mathcal{M}$，将*不能链接*约束集记为 $\mathcal{C}$；那么 LSI 的目标是求解以下优化问题：

$$\begin{aligned}
\max_{\mathbf{M}}\quad & \sum_{(\mathbf{x}_i,\mathbf{x}_j)\in\mathcal{C}}(\mathbf{x}_i-\mathbf{x}_j)^{\mathrm T}\mathbf{M}(\mathbf{x}_i-\mathbf{x}_j) \\
\text{s.t.}\quad & \sum_{(\mathbf{x}_u,\mathbf{x}_v)\in\mathcal{M}}(\mathbf{x}_u-\mathbf{x}_v)^{\mathrm T}\mathbf{M}(\mathbf{x}_u-\mathbf{x}_v)\le 1 \\
& \mathbf{M}\succeq 0.
\end{aligned} \tag{18.19}$$

这是一个二次优化问题，[28] 提出了一种迭代投影梯度上升法来求解它。由于 $\mathbf{M}$ 是半正定的，我们总是可以将其分解为 $\mathbf{M}=\mathbf{W}\mathbf{W}^{\mathrm T}$。因此，LSI 是一种全局且线性的方法。学习到的距离形式正是以 $\mathbf{M}$ 为精度矩阵的广义马氏距离。

### 18.3.4 相关成分分析（RCA）

*相关成分分析（RCA）* [18] 是另一种利用成对数据约束的代表性距离度量学习算法。RCA 的目标是找到一个变换，放大*相关变异性*并抑制*不相关变异性*。我们认为，如果从数据中去除这种变异性会（平均地）降低聚类或检索的结果，那么数据变异性与特定任务相关。如果变异性在数据中保持但与特定任务不相关，则它是无关的 [18]。我们还定义了称为 *chunklet* 的小簇，它们是由所有必须链接导出的连通分量。RCA 的具体步骤包括：

- 根据等价（必须链接）约束构造 *chunklet*，使得每个 chunklet 中的数据通过必须链接约束成对连接。
- 假设 $k$ 个 chunklet 中共有 $p$ 个点，其中第 $j$ 个 chunklet 由点 $\{\mathbf{x}_{ji}\}_{i=1}^{n_j}$ 组成，其均值为 $\bar{\mathbf{m}}_j$。RCA 计算以下加权 chunklet 内协方差矩阵：

$$\mathbf{C}=\frac{1}{p}\sum_{j=1}^{k}\sum_{i=1}^{n_j}(\mathbf{x}_{ji}-\bar{\mathbf{m}}_j)(\mathbf{x}_{ji}-\bar{\mathbf{m}}_j)^\top. \tag{18.20}$$

- 计算白化变换 $\mathbf{W}=\mathbf{C}^{-1/2}$，并将其应用于原始数据点：$\tilde{\mathbf{x}}=\mathbf{W}\mathbf{x}$。或者，使用 $\mathbf{C}$ 的逆矩阵作为广义马氏距离的精度矩阵。

因此，RCA 是一种全局、线性的方法。

### 18.3.5 信息论度量学习（ITML）

信息论目标是一种发展有监督距离度量的机制。*信息论度量学习（ITML）* [3] 就是这样一个代表性算法。假设我们有一个由精度矩阵 $\mathbf{M}_0$ 参数化的初始广义马氏距离，一个必须链接约束集 $\mathcal{M}$，以及一个不能链接约束集 $\mathcal{C}$。ITML 求解以下优化问题：

$$\begin{aligned}
\min_{\mathbf{M}\succeq 0}\quad & d_{\log\det}(\mathbf{M},\mathbf{M}_0) \\
\text{s.t.}\quad & (\mathbf{x}_i-\mathbf{x}_j)^\top\mathbf{M}(\mathbf{x}_i-\mathbf{x}_j)\ge l,\quad (\mathbf{x}_i,\mathbf{x}_j)\in\mathcal{C} \\
\phantom{\text{s.t.}}\quad & (\mathbf{x}_u-\mathbf{x}_v)^\top\mathbf{M}(\mathbf{x}_u-\mathbf{x}_v)\le u,\quad (\mathbf{x}_u,\mathbf{x}_v)\in\mathcal{M}
\end{aligned} \tag{18.21}$$

其中

$$d_{\log\det}(\mathbf{M},\mathbf{M}_0)=\operatorname{tr}(\mathbf{M}\mathbf{M}_0^{-1})-\log\det(\mathbf{M}\mathbf{M}_0^{-1})-n \tag{18.22}$$

其中 $d_{\log\det}$ 是 LogDet 散度，也称为 Stein 损失。可以证明，Stein 损失是唯一满足均匀最小方差无偏估计同时也是最小风险等变估计的尺度不变损失函数 [3]。文献 [3] 的作者还提出了一种有效的 *Bregman 投影* 方法来求解问题 (18.21)。ITML 是一种全局且线性的方法。学习到的距离度量是以 $\mathbf{M}$ 为精度矩阵的马氏距离。

### 18.3.6 邻域成分分析（NCA）

我们上面介绍的所有有监督方法都是全局方法。接下来我们还将介绍几种有代表性的局部有监督度量学习算法。首先，我们将概述*邻域成分分析（NCA）* [7]。与无监督度量学习中描述的 SNE 类似，每个点 $\mathbf{x}_i$ 以某个概率 $p_{ij}$ 选择另一个点 $\mathbf{x}_j$ 作为其邻居，并从其选择的点继承类别标签。NCA 定义点 $i$ 选择点 $j$ 作为邻居的概率：

$$p_{ij}=\frac{\exp(-\|\mathbf{W}^{\top}\mathbf{x}_i-\mathbf{W}^{\top}\mathbf{x}_j\|^2)}{\sum_{k\ne i}\exp(-\|\mathbf{W}^{\top}\mathbf{x}_i-\mathbf{W}^{\top}\mathbf{x}_k\|^2)}. \tag{18.23}$$

在这种随机选择规则下，NCA 计算点 $i$ 被正确分类的概率

$$p_i=\sum_{j\in\mathcal{L}_i}p_{ij} \tag{18.24}$$

