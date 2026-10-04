

# 402 应用时间序列分析与 R

2. $\Gamma(0) = E[(X_i - \mu)(X_i - \mu)']$ 存在且在时间 $t$ 上保持不变
3. $\Gamma(t_1, t_2)$ 仅是 $t_2 - t_1$ 的函数，即 $\text{cov}(X_{t_i}, X_{t_j})$ 仅是 $t_2 - t_1$ 的函数，对每个 $i$ 和 $j$。对于平稳多元时间序列，我们使用记号

$$\Gamma(k) = \begin{pmatrix} \Gamma_{11}(k) & \dots & \Gamma_{1m}(k) \\ \vdots & : & \vdots \\ \Gamma_{m1}(k) & \dots & \Gamma_{mm}(k) \end{pmatrix} \quad (10.1)$$

其中

$$\gamma_{ij}(k) = E[(X_i - \mu_i)(X_{i+k} - \mu_j)], k=0,\pm1,\dots \quad (10.2)$$

注意如果 $i \neq j$，则 $\gamma_{ij}(k)$ 称为滞后 $k$ 处的交叉协方差。还需关键注意 $\gamma_{ij}(k) = \gamma_{ji}(-k)$ 且 $\Gamma(-k)' = \Gamma(k)$，其中 $\mathbf{A}'$ 是矩阵 $\mathbf{A}$ 的转置。见注 4 以下。$\Gamma(0)$ 的第 $j$ 个对角元素是 $\text{Var}[X_j]$。交叉相关，$\rho_{ij}(k)$，定义为

$$\rho_{ij}(k) = \frac{\gamma_{ij}(k)}{\sqrt{\gamma_{ii}(0)\gamma_{jj}(0)}}$$

相应地，相关矩阵 $\boldsymbol{\rho}(k)$，$k=0, 1, \dots$ 由

$$\boldsymbol{\rho}(k) = \begin{pmatrix} \rho_{11}(k) & \dots & \rho_{1m}(k) \\ \vdots & : & \vdots \\ \rho_{m1}(k) & \dots & \rho_{mm}(k) \end{pmatrix} \quad (10.3)$$

给出

NOTES:

+ 1. 变量 $X_j$ 的自相关是矩阵 $\boldsymbol{\rho}(k)$ 的第 $j$ 个对角元素，$k=0, \pm 1, \dots$
2. 值 $\rho_{ij}(0)$ 衡量的是 $X_i$ 与 $X_j$ 之间所称的同期或同时线性关系。注意 $\rho(0)$ 在对角线上为 1。
3. $\rho(k)$ 的一个有用表达式为

$$\boldsymbol{\rho}(k) = \begin{pmatrix} \gamma_{11}^{-1/2} & 0 & \dots & 0 & \dots & 0 \\ 0 & \gamma_{22}^{-1/2} & \dots & 0 & \dots & 0 \\ \vdots & \vdots & \ddots & \vdots & \ddots & \vdots \\ 0 & 0 & \dots & \Gamma(k) & \dots & 0 \\ \vdots & \vdots & \ddots & \vdots & \ddots & \vdots \\ 0 & 0 & \dots & 0 & \dots & \gamma_{mm}^{-1/2} \end{pmatrix} \quad (10.4)$$

## 向量值（多元）时间序列

+ 4. 注意对于自相关，定义 $\gamma(k) = E[(X_i - \mu)(X_{i+k} - \mu)]$ 和 $\gamma(k) = E[(X_{i+k} - \mu)(X_i - \mu)]$ 是等价的，且 $\gamma(k) = \gamma(-k)$。这些性质不适用于交叉相关。我们上面提到 $\gamma_i(k) = \gamma_j(-k)$（注意下标顺序的变化）。

*Caution:* 我们强调协方差有两种常用定义

+ a. $\gamma_{ij}(k) = E[(X_i - \mu_i)(X_{i+k} - \mu_j)]$（方程 10.2 中给出的定义）这里使用，在 Box, et al. (2008) 中使用，以及其他文献

+ b. $\gamma_{ij}^{(k)} = E[(X_{i+k} - \mu_j)(X_i - \mu_j)]$，由 Shumway 和 Stoffer (2010)、Tsay (2002)、Blackwell 和 Davis (1991, 2002) 等使用。

当然，这两种交叉协方差定义导致两种交叉相关定义。必须注意这两种定义并不等价，我们要求读者在解释交叉协方差或交叉相关结果之前务必核查交叉协方差的定义！

**使用 R：** Base R 函数 `ccf(xi,xj,type='covariance')` 计算 $\gamma_{ij}^{(a)}(k)$（其中 $xi$ 和 $xj$ 分别表示第 $i$ 和第 $j$ 个时间序列）。为了按方程 10.2 的定义计算 $ccf$，你可以使用调用语句 `ccf(xj,xi)`。在任何情况下，使用 `type='correlation'` 计算相应的交叉相关。

定义 10.3 将白噪声的概念扩展到多元情形。

### Definition 10.3

多元时间序列 $\{\mathbf{a}_t; t \in T\}$ 被称为多元白噪声，如果

+ 1. $E(\mathbf{a}_t) = \mathbf{0}$ 其中 $\mathbf{0}$ 是 $m$ 个分量的 $0$ 向量。
2. $\boldsymbol{\rho}(k) = \mathbf{0}, k \neq 0$，其中在这种情况下 $\mathbf{0}$ 表示 $m \times m$ 的 $0$ 矩阵。

应注意定义 10.3 对 $\boldsymbol{\rho}(0)$ 没有任何限制。即 $a_i$ 和 $a_j$ 可能同期相关，且可能存在 $\rho_{ij}(0) \neq 0$ 对至少一个 $i, j$ 且 $i \neq j$。我们使用记号 $\mathbf{a} \sim \text{MWN}(0, \mathbf{\Gamma})$ 来指定 $\mathbf{a}$ 是均值为零、协方差为 $\mathbf{\Gamma}(0) = \mathbf{\Gamma}$ 的多元白噪声过程。乍一看，多元白噪声过程同期相关似乎矛盾。然而，在图 10.2 中，我们展示了来自二元白噪声时间序列 $\mathbf{a}_t = (a_{it})$ 的长度 $n=75$ 的实现，可以看出每个实现似乎沿时间轴不相关

# 404 应用时间序列分析与 R

![](img/41dcbfb9af56fa48895afde322197b0b_420_0.png)

![](img/41dcbfb9af56fa48895afde322197b0b_420_1.png)

**Figure 10.2**
来自两个白噪声过程的实现，其中两个白噪声过程之间存在正的同期相关，即 $\rho_{ij}(0) \neq 0$。

沿时间轴向下，但仔细检查显示两个实现呈正相关。在这种情况下，$\mathbf{\Gamma}_0 = \mathbf{\Gamma}_a$ 由

$$\mathbf{\Gamma}_a = \begin{pmatrix} 1 & 1.78 \\ 1.78 & 4 \end{pmatrix},$$

给出，且

$$\rho_a(0) = \begin{pmatrix} 1 & 0.89 \\ 0.89 & 1 \end{pmatrix}. \quad (10.5)$$

定义 10.4 将定义 2.1 中定义的一般线性过程的概念扩展到多元情形，且定义 10.5 定义了多元时间序列的谱。

### Definition 10.4

多元时间序列 $\{X_{it}; t=0, \pm1, \pm2, ...\}$ 被称为因果且平稳的多元一般线性过程，如果它由

## 向量值（多元）时间序列

$$\mathbf{x}_t - \mu = \sum_{j=0}^{\infty} \mathbf{\Psi}_j \mathbf{a}_{t-j},$$

给出，其中 $a$ 是多元白噪声且 $\Psi$ 是 $m \times m$ 矩阵，使得 $\Psi_0 = \mathbf{I}$（$m \times m$ 单位矩阵）且其分量绝对可和。注意，令 $\psi_j(k, l)$ 表示 $\Psi_j$ 的第 $k$ 行第 $l$ 列元素，则 $\sum_{j=0}^{\infty} |\psi_j(k, l)| < \infty$ 对 $1 \leq k, l \leq m$。

### Definition 10

设 $[X_t; t=0, \pm1, \pm2, \dots]$ 为因果平稳多元过程，其协方差矩阵 $\Gamma(k)$ 如方程 10.1 给出且 $\sum_{k=-\infty}^{\infty} |\gamma_{jh}(k)| < \infty$ 对 $1 \leq j, h \leq m$。对于 $0 \leq f \leq 0.5$，$X_j$ 的功率谱由

$$\mathbf{P}_x(f) = \sum_{k=-\infty}^{\infty} e^{-2\pi if} \Gamma(k).$$

给出。注意在多元情形下，方程 10.7 中的 $\mathbf{P}_x(f)$ 通常称为谱密度。为与单变量情形的记号保持一致，我们称其为谱。还要注意 $\mathbf{P}_x(f)$ 对每个 $f$ 都是 $m \times m$ 矩阵。类似于单变量情形方程 10.28，可以证明

$$\Gamma(f) = \int_{-0.5}^{0.5} e^{2\pi if} \mathbf{P}_x(f) df.$$

其中 $i = \sqrt{-1}$。$\mathbf{P}_x(f)$ 的 $jh$ 元素由

$$\mathbf{P}_{jh}(f) = \sum_{k=-\infty}^{\infty} e^{-2\pi if} \gamma_{jh}(k),$$

给出，其中 $|f| \leq 0.5$，且 $\gamma_{jk}(k)$ 在方程 10.1 之后定义。注意 $P_{jj}^0(f)$ 是单变量序列 $X_j$ 的通常谱，而如果 $j \neq h$ $P_{jh}^0(f)$ 称为 $X_j$ 和 $X_{lh}$ 的交叉谱，其可以是复值且具有性质 $P_{jh}(f)$ 是 $P_{hj}(f)$ 的复共轭。记 $P_{jh}(f) = c_{jh}(f) - iq_{jh}(f)$，则 $q_{jh}(f)$ 称为正交谱。将 $P_{jh}(f)$ 表示为极坐标形式，我们有 $P_{jh}(f) = \alpha_{jh}(f)e^{i\varphi_{jh}(f)}$，其中 $\alpha_{jh}(f) = \sqrt{c_{jh}^2(f) + q_{jh}^2(f)}$ 称为振幅谱且 $\varphi_{jh}(f) = \tan^{-1}(-q_{jh}(f)/c_{jh}(f))$ 是相位谱。两个单变量序列 $X_j$ 和 $X_h$ 的平方相干，$\kappa_{jh}(f)$，定义为

