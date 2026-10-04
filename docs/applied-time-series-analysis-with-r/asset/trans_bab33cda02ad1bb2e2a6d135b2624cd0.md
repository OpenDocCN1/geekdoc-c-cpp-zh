

# 406 应用时间序列分析与 R

$$\kappa_{jh}^2(f) = \frac{|P_{jh}(f)|^2}{P_j(f)P_h(f)} \quad (10.9)$$

应注意 $\kappa_{jh}^2(f)\le1$ 且可解释为频率 $f$ 下 $X_{ij}$ 与 $X_{ih}$ 的随机分量之间线性关系的平方相关度量。

## 10.2.1 平稳多元过程均值与协方差的估计

我们简要讨论基于平稳多元过程 $[X_{ij}; t=0, \pm 1, \pm 2, \dots]$ 的长度为 $n$ 的实现，对均值 $\mu$ 和协方差矩阵 $\Gamma(k)$ 的估计。这些估计程序与单变量过程的相应程序完全类似。

### 10.2.1.1 估计 $\mu$

$m$ 分量向量 $\mu$ 的自然无偏估计量是 $m$ 分量向量 $\mathbf{X}$，其定义为

$$\mathbf{X} = \begin{pmatrix}\tilde{X}_1 \\ \tilde{X}_2 \\ \vdots \\ \tilde{X}_m \end{pmatrix}, \quad (10.10)$$

$\tilde{X}_j = \frac{1}{n}\sum_{t=1}^{n}X_{ij}$。我们说 $\mathbf{X}$ 对 $\mu$ 是遍历的，如果当 $n \to \infty$ 时 $\mathbf{X}$ 在均方意义下收敛，即 $E[(\mathbf{X}-\mu)(\mathbf{X}-\mu)']\to 0$。推论 1.1 给出了单变量情形下遍历性的充分条件，并将其应用于 $\mathbf{X}$ 的每个分量，可得 $\mathbf{X}$ 对 $\mu$ 遍历的条件为 $\lim_{k\to\infty}\gamma_{jh}^2(k)=0$ 对每个 $j$，$1 \le j \le m$。

### 10.2.1.2 估计 $\Gamma(k)$

通常用 $m \times m$ 矩阵来估计协方差矩阵 $\Gamma(k)$，其定义为

$$\mathbf{\hat{\Gamma}}(k) = \begin{pmatrix}\hat{\gamma}_{11}(k) & \cdots & \hat{\gamma}_{1m}(k) \\ \vdots & & \vdots \\ \hat{\gamma}_{m1}(k) & \cdots & \hat{\gamma}_{mm}(k) \end{pmatrix}, \quad (10.11)$$

$\hat{\gamma}_{ij}(k)=(1/n)\sum_{t=1}^{n-k}(X_{it}-\tilde{X}_i)(X_{jt+k}-\tilde{X}_j)$。注意，式 10.11 中的估计量对应于

## 向量值（多元）时间序列

中交叉相关性的定义。

式 10.2 与使用式 1.19 估计 $\gamma_j$ 的用法类似。关于估计量的性质的讨论，参见 Blackwell 和 Davis (1991, 2002)。$X_{it}$ 与 $X_{jt}$ 在滞后 $k$ 处的交叉相关 $\rho_{ij}(k)$ 估计为

$$\hat{\rho}_{ij}(k) = \frac{\hat{\gamma}_{ij}(k)}{\sqrt{\hat{\gamma}_{ii}(0)\hat{\gamma}_{jj}(0)}} \quad (10.12)$$

注意 $\hat{\rho}_{ij}(0)$ 是基于 $X_{it}$ 和 $X_{jt}$ 的 $n$ 个观测值计算的通常的 Pearson 乘积矩相关。

## 10.3 多元（向量）ARMA 过程

AR(p)、MA(q)、ARMA(p,q)、ARUMA(p,d,q) 以及相应的季节模型都可以推广到多元情形。我们将重点完全放在多元 AR(p) 过程上。我们从例 10.1 开始讨论。

## 例 10.1：一个双变量过程

考虑双变量过程

$$X_t = \begin{pmatrix} X_{t1} \\ X_{t2} \end{pmatrix}, t=0, \pm1, \pm2, \dots$$

由下式指定

$$X_{t1} = \phi_{11}X_{t-1,1} + \phi_{12}X_{t-1,2} + a_{t1},$$
$$X_{t2} = \phi_{21}X_{t-1,1} + \phi_{22}X_{t-1,2} + a_{t2}, \quad (10.13)$$

其中 $\mathbf{a}_t = (a_{t1}, a_{t2})'$ 是一个双变量白噪声过程。式 10.13 中的方程可以写成矩阵形式

$$X_t = \mathbf{\Phi}X_{t-1} + \mathbf{a}_t, \quad (10.14)$$

其中

$$\Phi_1 = \begin{pmatrix} \phi_{11} & \phi_{12} \\ \phi_{21} & \phi_{22} \end{pmatrix}.$$

式 10.13 中的双变量过程是多元（或向量）AR(1) 过程的一个例子。向量 AR(p) 过程在随后给出的定义 10.6 中定义。

## 定义 10.6

设 $X_t$ 为满足

$$X_t = \alpha + \Phi_1 X_{t-1} - \dots - \Phi_p X_{t-p} + a_t, \quad (10.15)$$

的因果、平稳多元过程，其中

- $X_t = (X_{t1}, \dots, X_{tm})'$ 是一个 $m \times 1$ 向量
- $\Phi_k$ 是每个 $k = 1, \dots, p$ 的实值 $m \times m$ 矩阵
- $a_t$ 是协方差矩阵为 $E[a_t a_t'] = \Gamma_a$ 的多元白噪声；
- $\alpha = (\Phi_1 - \dots - \Phi_p)\mu$，其中 $\mu = E(X_t)$

则 $X_t$ 是 VAR($p$) 过程，即 $p$ 阶多元 AR 过程。

注意式 10.1 可以写成多元算子记号 $\Phi(B)(X_t - \mu) = a_t$，

$$\Phi(B) = \mathbf{I} - \Phi_1 B - \dots - \Phi_p B^p, \quad (10.16)$$

且 $B^k X_t = X_{t-k}$。定理 10.1 给出了 VAR($p$) 模型的平稳性条件，其与定理 3.2 中单变量 AR($p$) 模型的条件类似。

## 定理 10.1

满足式 10.15 中差分方程的多元过程 $X_t$ 当且仅当行列式方程的根

$$|\Phi(z)| = |\mathbf{I} - \Phi_1 z - \dots - \Phi_p z^p| = 0,$$

位于单位圆之外时，才是平稳且因果的 VAR($p$) 过程。

证明：参见 Brockwell 和 Davis (1991) 以及 Reinsel (1997)。

注意满足定理 10.1 的 VAR($p$) 模型 $\Phi(B)(X_t - \mu) = a_t$ 可以写成多元广义线性过程形式

$$X_t - \mu = \Psi(B)a_t;$$
$$= \sum_{j=0}^{\infty} \Psi_j a_{t-j}, \quad (10.17)$$

其中 $\Psi(B) = \Phi^{-1}(B)$。

多元 Yule-Walker 方程为

$$\Gamma(k) = \Gamma(k-1)\Phi_k' + \dots + \Gamma(k-p)\Phi_p, \quad k=1, \dots, p, \quad (10.18)$$

## 向量值（多元）时间序列

其中

$$\Gamma(0) = \Phi_1\Gamma(-1) + \dots + \Phi_p\Gamma(-p) + \Gamma_a, \quad (10.19)$$

这与单变量情形下的式 3.42 类似。

$$\Gamma(0) = \Gamma(-1)\Phi_1 + \dots + \Gamma(-p)\Phi_p + \Gamma_a, \quad (10.20)$$

这与单变量情形下的式 3.42 类似。

在 VAR(1) 情形下，式 10.18 和 10.19 简化为 $\Gamma(k) = \Gamma(k-1)\Phi_1$，$k > 0$ 且 $\Gamma(0) = \Gamma(-1)\Phi_1 + \Gamma_a$。由于任何平稳多元过程，若对 VAR(1) 有 $\Gamma(1) = \Gamma(0)\Phi_1^*$ 且 $\Gamma(-k) = \Gamma(k)\Phi_k^*$，则 $\Gamma(0) = \Gamma(0)\Phi_1 + \Gamma_a$。这些表达式说明了对于 VAR(1)，已知 $\Phi_1$（和 $\Gamma_a$）可以方便地计算协方差矩阵 $\Gamma(k)$，$k=0, \dots$。由于 $\Phi_1^* = \Gamma^{-1}\Gamma(1)$，因此若已知 $\Gamma(0)$ 和 $\Gamma(1)$，则可计算 $\Phi_1$。这些关系与单变量 AR(1) 情形下先前观察到的性质类似。参见例如 3.34 和 3.35。

## 例 10.2：一个双变量 VAR(1) 过程

考虑零均值 VAR(1) 过程 $\Phi(B)X_t = (I - \Phi_B)X_t = a_t$，其中

$$\Phi_1 = \begin{pmatrix} 0.9 & 0.6 \\ -0.3 & 0.7 \end{pmatrix}, \quad (10.21)$$

且

$$\Gamma_a = \begin{pmatrix} 1 & 1.78 \\ 1.78 & 4 \end{pmatrix}, \quad (10.22)$$

在此例中 $a_t$ 具有与图 10.2 中双变量白噪声实现相同的 $\Sigma_a$。本例中式 10.13 为

$$X_{t,1} = 0.9X_{t-1,1} + 0.6X_{t-1,2} + a_{t1},$$
$$X_{t,2} = -0.3X_{t-1,1} + 0.7X_{t-1,2} + a_{t2}, \quad (10.23)$$

且方程

$$|I - \Phi_1z| = \begin{pmatrix} 1-\phi_{11}z & -\phi_{12}z \\ -\phi_{21}z & 1-\phi_{22}z \end{pmatrix}| = 0$$

由 $(\phi_{11}\phi_{22} - \phi_{12}\phi_{21})z^2 - (\phi_{11} + \phi_{22})z + 1 = 0$ 给出。对于本例，该方程为 $1 - 1.6z + 0.81z^2 = 0$，其根 $r$ 和 $r^*$ 为 $0.99 + 0.51i$ 且 $|r| = 0.90$。因此根位于单位圆之外。

# 410 应用时间序列分析与 R

注意：方程 $1 - 1.6z + 0.81z^2 = 0$ 与单变量 ARMA(p,q) 模型的特征方程形式相同。因此与平稳性相关的根（评估）可使用 tswge 中的 factor.wge 得到，并输入 1.6、-0.81 作为系数。

长度为 $n=75$ 的实现，其中式 10.23 中的 VAR(1) 过程如图 10.3 所示，可以看出在双变量情形下 VAR(1) 模型可以表现出伪循环行为。利用 $\Gamma(0) - \Phi\Gamma(0)\Phi^* = \Gamma_z$ 这一事实，并求解 $\Gamma(0)$，可得

$$\Gamma(0) = \begin{pmatrix} 27.74 & -0.40 \\ -0.40 & 13.07 \end{pmatrix}$$

这与图 10.3 一致，其中可以看出 $X_{i1}$（上图）的方差大于 $X_{i2}$（下图）。利用性质 $\Gamma(k) = \Gamma(k-1)\Phi^k, k>0$，可以证明

$$\Gamma(1) = \begin{pmatrix} 24.73 & -8.60 \\ 7.48 & 9.27 \end{pmatrix}, \Gamma(2) = \begin{pmatrix} 17.09 & -13.34 \\ 12.30 & 4.24 \end{pmatrix}, \dotsdots$$

![](img/41dcbfb9af56fa48895afde322197b0b_426_0.png)

**图 10.3** 例 10.2 中双变量 VAR(1) 过程的实现。(a) $X_{i1}$ 的实现。(b) $X_{i2}$ 的实现。

