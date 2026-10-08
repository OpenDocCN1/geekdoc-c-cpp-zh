

其中

$$\tilde{\mathbf{T}}_{i}=\left[\begin{array}{cccc} 4 \tilde{z}_{i} & 2 \tilde{x}_{i} & 2 \tilde{y}_{i} & 0 \\ 2 \tilde{x}_{i} & 1 & 0 & 0 \\ 2 \tilde{y}_{i} & 0 & 1 & 0 \\ 0 & 0 & 0 & 0 \end{array}\right] .$$

现在我们将(7.28)重写为

$$\begin{aligned} \mathbb{E}\left[\left(\Delta_{1} \mathbf{A}\right)\left(\Delta_{1} \mathbf{A}\right)^{T}\right] & =n^{-2} \tilde{\mathbf{M}}^{\leftarrow}\left[\sum_{i, j} \tilde{\mathbf{X}}_{i} \tilde{\mathbf{A}}^{T} \mathbb{E}\left[\left(\Delta_{1} \mathbf{X}_{i} \Delta_{1} \mathbf{X}_{j}^{T}\right) \tilde{\mathbf{A}} \tilde{\mathbf{X}}_{j}^{T}\right] \tilde{\mathbf{M}}^{\rightarrow} \\ & =n^{-2} \sigma^{2} \tilde{\mathbf{M}}^{\leftarrow}\left[\sum_{i} \tilde{\mathbf{X}}_{i} \tilde{\mathbf{A}}^{T} \tilde{\mathbf{T}}_{i} \tilde{\mathbf{A}} \tilde{\mathbf{X}}_{i}^{T}\right] \tilde{\mathbf{M}}^{\rightarrow} \end{aligned}$$

注意到

$$\tilde{\mathbf{A}}^{T} \tilde{\mathbf{T}}_{i} \tilde{\mathbf{A}}=\tilde{\mathbf{A}}^{T} \mathbf{P} \tilde{\mathbf{A}}=\tilde{B}^{2}+\tilde{C}^{2}-4 \tilde{A} \tilde{D}$$

对每个 $i$ 都成立，因此

$$\sum_{i} \tilde{\mathbf{X}}_{i} \tilde{\mathbf{A}}^{T} \tilde{\mathbf{T}}_{i} \tilde{\mathbf{A}} \tilde{\mathbf{X}}_{i}^{T}=\sum_{i}\left(\tilde{\mathbf{A}}^{T} \mathbf{P} \tilde{\mathbf{A}}\right) \tilde{\mathbf{X}}_{i} \tilde{\mathbf{X}}_{i}^{T}=n\left(\tilde{\mathbf{A}}^{T} \mathbf{P} \tilde{\mathbf{A}}\right) \tilde{\mathbf{M}} .$$

由此得出

$$\mathbb{E}\left[\left(\Delta_{1} \mathbf{A}\right)\left(\Delta_{1} \mathbf{A}\right)^{T}\right]=n^{-1} \sigma^{2} \tilde{\mathbf{M}}^{\leftarrow}\left(\tilde{\mathbf{A}}^{T} \mathbf{P} \tilde{\mathbf{A}}\right) . \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad (7.29)$$

值得注意的是，代数拟合的方差不依赖于约束矩阵 $\mathbf{N}$，因此所有代数拟合具有相同的方差（在主要项意义下）。在第 7.6 节中，我们将推导自然圆参数 $(a,b, R)$ 下代数拟合的方差，并发现它与几何拟合的方差 (7.6) 相一致。

### 代数圆拟合的偏差

由于 $\mathbb{E}\left(\Delta_{1} \mathbf{A}\right)=0$，我们只需要找到 $\mathbb{E}\left(\Delta_{2} \mathbf{A}\right)$，这将通过(7.26)来完成。首先，根据(7.23)，我们可以写成

$$\eta=\tilde{\eta}+\Delta_{1} \eta+\Delta_{2} \eta+\mathscr{O}_{P}\left(\sigma^{3}\right) .$$

将(7.22)左乘以 $\tilde{\mathbf{A}}^{T}$ 得到

$$\eta=\frac{\tilde{\mathbf{A}}^{T} \mathbf{M} \mathbf{A}}{\tilde{\mathbf{A}}^{T} \mathbf{N} \mathbf{A}}=\frac{\tilde{\mathbf{A}}^{T} \Delta_{2} \mathbf{M} \tilde{\mathbf{A}}+\tilde{\mathbf{A}}^{T} \Delta_{1} \mathbf{M} \Delta_{1} \mathbf{A}}{\tilde{\mathbf{A}}^{T} \tilde{\mathbf{N}} \tilde{\mathbf{A}}}+\mathscr{O}_{P}\left(\sigma^{3}\right) ,$$

特别地，我们看到 $\tilde{\eta}=\Delta_{1} \eta=0$ 且 $\eta=\mathscr{O}_{P}\left(\sigma^{2}\right)$。因此，由(7.26)可得

$$\Delta_{2} \mathbf{A}=\tilde{\mathbf{M}}^{\leftarrow}\left(\frac{\tilde{\mathbf{A}}^{T} \mathbf{L}}{\tilde{\mathbf{A}}^{T} \tilde{\mathbf{N}} \tilde{\mathbf{A}}} \tilde{\mathbf{N} \tilde{\mathbf{A}}-\mathbf{L}}\right)+\mathscr{O}_{P}\left(\sigma^{3}\right), \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad(7.30)$$

其中

$$\mathbf{L}=\Delta_{2} \mathbf{M} \tilde{\mathbf{A}}+\Delta_{1} \mathbf{M} \Delta_{1} \mathbf{A} . \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad (7.31)$$

我们注意到(7.30)实际上给出了 $\Delta_2\mathbf{A}$ 中垂直于 $\tilde{\mathbf{A}}$ 的分量，但这正是我们所需要的，因为我们设定了 $\|\mathbf{A}\| = 1$。我们可以将(7.31)重写为

其中，根据(7.27)，

$$\begin{aligned} \mathbf{R} & = \frac{1}{n}\bigg[\Delta_1\mathbf{X}^T\Delta_1\mathbf{X} + \hat{\mathbf{X}}^T\Delta_2\mathbf{X} + \Delta_2\mathbf{X}^T\hat{\mathbf{X}} \\ & \qquad \qquad - \frac{1}{n}(\hat{\mathbf{X}}^T\Delta_1\mathbf{X} + \Delta_1\mathbf{X}^T\hat{\mathbf{X}})\hat{\mathbf{M}}^{-}\hat{\mathbf{X}}^T\Delta_1\mathbf{X}\bigg]. \end{aligned}$$

因此，偏差的公式变为

$$\mathbb{E}(\Delta_2\mathbf{A}) = \hat{\mathbf{M}}^{-}\begin{bmatrix} \tilde{\mathbf{A}}^T\mathbb{E}(\mathbf{R}\tilde{\mathbf{A}}) & \tilde{\mathbf{N}}\tilde{\mathbf{A}} - \mathbb{E}(\mathbf{R}\tilde{\mathbf{A}}) \\ \tilde{\mathbf{A}}^T\tilde{\mathbf{N}}\tilde{\mathbf{A}} \end{bmatrix} + \mathcal{O}(\sigma^4).$$

接下来我们逐项求(7.32)的均值。首先，

$$\begin{aligned} \frac{1}{n}\mathbb{E}(\Delta_1\mathbf{X}^T\Delta_1\mathbf{X}) & = \frac{1}{n}\mathbb{E}\Big(\sum_i(\Delta_1\mathbf{X}_i)(\Delta_1\mathbf{X}_i)^T\Big) = \frac{\sigma^2}{n}\sum_i\tilde{\mathbf{T}}_i = \boldsymbol{\sigma}^2\tilde{\mathbf{T}}. \end{aligned}$$

其次，由于 $\mathbb{E}(\Delta_2\mathbf{X}_i) = (2\sigma^2, 0, 0, 0)^T$，我们得到

$$\begin{aligned} \frac{1}{n}\mathbb{E}(\hat{\mathbf{X}}^T\Delta_2\mathbf{X} + \Delta_2\mathbf{X}^T\hat{\mathbf{X}}) & = \frac{2\sigma^2}{n}\sum_i \begin{bmatrix} 2\tilde{z}_i & \tilde{x}_i & \tilde{y}_i & 1 \\ \tilde{x}_i & 0 & 0 & 0 \\ \tilde{y}_i & 0 & 0 & 0 \\ 1 & 0 & 0 & 0 \end{bmatrix} = \boldsymbol{\sigma}^2(\tilde{\mathbf{T}} - \mathbf{P}). \end{aligned}$$

上述两项结合构成了本质偏差，即

$$\mathbb{E}(\Delta_2\mathbf{A}) \overset{\mathrm{ess}}{=} \boldsymbol{\sigma}^2\hat{\mathbf{M}}^{-}\begin{bmatrix} \frac{\tilde{\mathbf{A}}^T(2\tilde{\mathbf{T}}-\mathbf{P})\tilde{\mathbf{A}}}{\tilde{\mathbf{A}}^T\tilde{\mathbf{N}}\tilde{\mathbf{A}}} & \tilde{\mathbf{N}}\tilde{\mathbf{A}} - (2\tilde{\mathbf{T}}-\mathbf{P})\tilde{\mathbf{A}} \end{bmatrix}.$$ 

### $\mathcal{O}(\sigma^2)$ 的完整偏差

我们继续计算(7.32)的均值：

$$\begin{aligned} \mathbb{E}(\hat{\mathbf{X}}^T\Delta_1\mathbf{X}\hat{\mathbf{M}}^{-}\hat{\mathbf{X}}^T\Delta_1\mathbf{X}) & = \sum_i\mathbb{E}(\hat{\mathbf{X}}_i\Delta_1\hat{\mathbf{X}}_i^T\hat{\mathbf{M}}^{-}\hat{\mathbf{X}}_i\Delta_1\mathbf{X}_i^T) \ & = \sum_i\mathbb{E}(\hat{\mathbf{X}}_i\hat{\mathbf{X}}_i^T\hat{\mathbf{M}}^{-}\Delta_1\mathbf{X}_i\Delta_1\mathbf{X}_i^T) \ & = \boldsymbol{\sigma}^2\sum_i\hat{\mathbf{X}}_i\hat{\mathbf{X}}_i^T\hat{\mathbf{M}}^{-}\tilde{\mathbf{T}}_i. \end{aligned}$$

类似地，我们有

$$\mathbb{E}(\Delta_1\mathbf{X}^T\hat{\mathbf{X}}\hat{\mathbf{M}}^{-}\hat{\mathbf{X}}^T\Delta_1\mathbf{X}) = \boldsymbol{\sigma}^2\sum_i\hat{\mathbf{X}}_i^T\hat{\mathbf{M}}^{-}\hat{\mathbf{X}}_i\tilde{\mathbf{T}}_i.$$

因此，完整偏差由下式给出

$$\mathbb{E}(\Delta_{2}\mathbf{A}) = \boldsymbol{\sigma}^{2}\mathbf{\widetilde{M}}-\left[\begin{array}{c}\widetilde{\mathbf{A}}^{T}\widetilde{\mathbf{H}}^{*}\widetilde{\mathbf{A}}\\ \widetilde{\mathbf{A}}^{T}\mathbf{N}\widetilde{\mathbf{A}}\end{array}\right. \widetilde{\mathbf{N}}\widetilde{\mathbf{A}}-\widetilde{\mathbf{H}}^{*}\widetilde{\mathbf{A}}\right]+\mathcal{O}\left(\sigma^{4}\right),\tag{7.39}$$

其中

$$\mathbf{H}^{*}=2\mathbf{T}-\mathbf{P}+\frac{1}{n^{2}}\sum_{i}\left[\mathbf{X}_{i}\mathbf{X}_{i}^{T}\mathbf{M}^{-}\mathbf{T}_{i}+\mathbf{T}_{i}\mathbf{M}^{-}\mathbf{X}_{i}\mathbf{X}_{i}^{T}+\mathbf{X}_{i}^{T}\mathbf{M}^{-}\mathbf{X}_{i}\mathbf{T}_{i}\right].\tag{7.40}$$

我们添加了项 $\mathbf{T}_{i}\mathbf{M}^{-}\mathbf{X}_{i}\mathbf{X}_{i}^{T}$，其唯一目的是保持 $\mathbf{H}^{*}$ 为对称矩阵；其对称性在未来将是至关重要的。所添加的项不影响(7.39)，因为对于每个 $i=1,\ldots, n$，都有 $\mathbf{X}_{i}^{T}\widetilde{\mathbf{A}}=0$。

### 本质偏差的更简单公式

接下来我们简化本质偏差的公式(7.36)。注意到

$$\widetilde{\mathbf{T}}_{i}\widetilde{\mathbf{A}}=\mathbf{P}\widetilde{\mathbf{A}}+2\widetilde{\mathbf{A}}\widetilde{\mathbf{X}}_{i}$$

对所有 $i=1,\ldots, n$ 都成立，因此

$$\widetilde{\mathbf{T}}\widetilde{\mathbf{A}}=\mathbf{P}\widetilde{\mathbf{A}}+2\widetilde{\mathbf{A}}n^{-1}\sum_{i}\widetilde{\mathbf{X}}_{i}$$

并且因此 $\widetilde{\mathbf{A}}^{T}\widetilde{\mathbf{T}}\widetilde{\mathbf{A}}=\widetilde{\mathbf{A}}^{T}\mathbf{P}\widetilde{\mathbf{A}}$。我们也有

$$(2\widetilde{\mathbf{T}}-\mathbf{P})\widetilde{\mathbf{A}}=\mathbf{P}\widetilde{\mathbf{A}}+4\widetilde{\mathbf{A}}n^{-1}\sum_{i}\widetilde{\mathbf{X}}_{i}.$$

还要注意，向量 $n^{-1}\sum_{i}\widetilde{\mathbf{X}}_{i}$ 与矩阵 $\widetilde{\mathbf{M}}$ 的最后一列重合，因此

$$n^{-1}\widetilde{\mathbf{M}}-\sum_{i}\widetilde{\mathbf{X}}_{i}=[0,0,0,1]^{T}.$$ 

总结上述事实，我们将(7.36)化简为

$$\mathbb{E}(\Delta_{2}\mathbf{A})^{\mathrm{ess}}=\boldsymbol{\sigma}^{2}\mathbf{\widetilde{M}}-\left[\begin{array}{c}\widetilde{\mathbf{A}}^{T}\mathbf{P}\widetilde{\mathbf{A}}\\ \widetilde{\mathbf{A}}^{T}\widetilde{\mathbf{N}}\widetilde{\mathbf{A}}\end{array}\right. \widetilde{\mathbf{N}}\widetilde{\mathbf{A}}-\mathbf{P}\widetilde{\mathbf{A}}\right]-4\sigma^{2}\widetilde{\mathbf{A}}\left[0,0,0,1\right]^{T}.\tag{7.41}$$

## 7.5 代数圆拟合的比较

**Pratt 和 Taubin 拟合的偏差。** 我们已经看到，所有代数拟合具有相同的渐近方差 (7.29)。我们将在下文看到，它们的渐近方差与几何圆拟合的方差相一致。因此，我们所有圆拟合之间的差异应归结于高阶项，尤其是它们的本质偏差。

