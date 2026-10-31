

其中 χ²(p) 表示自由度为 p 的卡方分布，σ̂ₐ² 和 Γ̂ 分别表示基于数据的 σₐ² 和 Γ 估计值（参见 Brockwell and Davis, 1991）。由式 7.57 可得，φ 的近似 (1 − α) × 100% 置信椭球为

(\hat{φ} - φ)' \hat{Γ} (\hat{φ} - φ) ≤ \frac{\hat{σ}_a^2}{n} χ²_{1-α}(p),  (7.58)

其中 χ²_β 表示自由度为 p 的卡方分布的 β × 100 百分位数。若需要对单个参数 φ_j 构造置信区间，则可将式 7.58 修改为

\hat{φ}_j ± z_{(1-α)/2} \frac{\hat{σ}_a^2 \hat{Γ}_{jj}^{1/2}}{√n},  (7.59)

其中 z_β 表示标准正态分布的 β × 100 百分位数，\hat{Γ}_{jj} 表示 \hat{Γ}^{-1} 的第 j 个对角元素。

在继续讨论 ARMA(p,q) 情形之前，关于 σₐ² 和 Γ 的估计可作几点说明。首先，对于 AR(1) 和 AR(2) 情形，σₐ² \hat{Γ}^{-1} 可分别通过将参数估计值直接代入式 7.53 和 7.56 来估计。对于高阶模型，σₐ² 可用 \hat{σ}_a² 来估计，即采用第 7.4 节讨论的回测（backcasting）方法时，与特定估计过程相关联的估计白噪声方差。然后，矩阵 \hat{Γ} 可通过用式 7.5 中的 \hat{γ}_k 估计元素 γ_k 来获得。

在例 7.9d 中，我们基于已知 AR 模型生成的实现，根据 YW、Burg 和 ML 估计计算模型参数的置信区间。

## 7.5.2 ARMA(p,q) 情形

在本节中，我们简要讨论更一般的 ARMA(p,q) 过程 \hat{ρ} = (\hat{φ}_1, ..., \hat{φ}_p, \hat{θ}_1, ..., \hat{θ}_q) 的渐近分布，φ(B)X_t = θ(B)a_t,  (7.60) 其中参数估计值通过 ML 或最小二乘法（条件或非条件）获得。该渐近分布为

$n^{1/2}(\hat{\boldsymbol{\beta}}-\boldsymbol{\beta}) \Rightarrow N(0,\sigma_a^2\boldsymbol{\Gamma}^{-1})$， (7.61)

其中 $\boldsymbol{\beta}$ 表示真实参数值向量。为获得此情形下的矩阵 $\boldsymbol{\Gamma}$，我们考虑由下式定义的两个 AR 过程 $\mathcal{U}$ 和 $V_t$：

$\phi(B)\mathcal{U}_t = a_t$, (7.62)

$\theta(B)V_t = a_t$, (7.63)

其中 $\phi(B)$ 和 $\theta(B)$ 与式 7.60 中相同。我们使用记号 $\gamma_U(k)=E[U_t U_{t+k}]$、$\gamma_V(k)=E[V_t V_{t+k}]$ 和 $\gamma_{UV}(k)=E[U_t V_{t+k}]$。则 $\boldsymbol{\Gamma}$ 是 $(p+q)\times(p+q)$ 矩阵，定义为

$\boldsymbol{\Gamma}=\begin{bmatrix}\boldsymbol{\Gamma}_{pp}&\boldsymbol{\Gamma}_{pq}\\ \boldsymbol{\Gamma}_{qp}&\boldsymbol{\Gamma}_{qq}\end{bmatrix}$, (7.64)

其中

- $\boldsymbol{\Gamma}_{pp}$ 是 $p\times p$ 矩阵，其第 $ij$ 个元素为 $\gamma_U(i-j)$
- $\boldsymbol{\Gamma}_{qq}$ 是 $q\times q$ 矩阵，其第 $ij$ 个元素为 $\gamma_V(i-j)$

矩阵 $\boldsymbol{\Gamma}_{pq}$ 是 $p\times q$ 矩阵，其第 $ij$ 个元素为 $\gamma_{UV}(i-j)$，而 $\boldsymbol{\Gamma}_{qp}$ 是 $q\times p$ 矩阵，其第 $ij$ 个元素为 $\gamma_{UV}(j-i)$。由式 7.64 可知，MA$(q)$ 模型 $X_t=\theta(B)a_t$ 的 $\boldsymbol{\Gamma}$ 矩阵与 AR$(q)$ 模型 $\theta(B)X_t=a_t$ 的 $\boldsymbol{\Gamma}$ 矩阵相同。利用这一事实，在例 7.6 中我们求出了 MA(1) 和 MA(2) 模型相关的渐近分布，在例 7.7 中我们求出了 ARMA(1,1) 的渐近分布。关于 ARMA$(p,q)$ 情形下渐近分布的推导，参见 Box et al. (2008) 和 Brockwell and Davis (1991)。

### 例 7.6：MA(1) 和 MA(2) 模型的渐近分布

1. MA(1)：由前述讨论可知，对于 MA(1) 模型，$\boldsymbol{\Gamma}$ 是 $1\times1$ 矩阵，其元素为 $\gamma_0=\sigma_a^2/(1-\theta_1^2)$。因此 $\sigma_a^2\boldsymbol{\Gamma}^{-1}=1-\theta_1^2$，且 $\hat{\theta}_1$ 渐近服从正态分布，均值为 $\theta_1$，方差为 $(1-\theta_1^2)/n$。

2. MA(2)：由式 7.56 可得

$$\sigma_a^2\mathbf{\Gamma}^{-1}=\begin{bmatrix}1-\theta_2^2 & -\theta_1(1+\theta_2)\\ -\theta_1(1+\theta_2) & 1-\theta_2^2\end{bmatrix}.\tag{7.65}$$

与 AR(2) 情形一样，从式 7.65 的对角元素可以看出，渐近地，$\hat{\theta}_1$ 服从均值为 $\theta_1$、方差为 $(1-\theta_2^2)/n$ 的正态随机变量，而 $\hat{\theta}_2$ 的均值为 $\theta_2$，且与 $\hat{\theta}_1$ 具有相同的渐近方差。

### 例 7.7：ARMA(1,1) 模型的渐近分布

考虑 ARMA(1,1) 模型

$$(1-\phi_1 B)X_t=(1-\theta_1 B)a_t.\tag{7.66}$$

在这种情况下，式 7.64 中的每个子矩阵都是 $1\times1$ 的，且 $\mathbf{\Gamma}$ 为

$$\mathbf{\Gamma}=\begin{bmatrix}\gamma_{\mathcal{U}}(0) & \gamma_{\mathcal{U}V}(0)\\ \gamma_{\mathcal{U}V}(0) & \gamma_{V}(0)\end{bmatrix}$$

其中 $\gamma_{\mathcal{U}}(0)=\sigma_a^2/(1-\phi_1^2)$，$\gamma_V(0)=\sigma_a^2/(1-\theta_1^2)$。现在，

$$\gamma_{\mathcal{U}V}(0)=E[\mathcal{U}_t V_t]=E[(\phi_1\mathcal{U}_{t-1}+a_t)(\theta_1 V_{t-1}+a_t)]=\phi_1\theta_1E[\mathcal{U}_{t-1}V_{t-1}]+\theta_1E[V_{t-1}a_t]+\phi_1E[\mathcal{U}_{t-1}a_t]+\sigma_a^2,$$

因此 $$\gamma_{\mathcal{U}V}(0)=\phi_1\theta_1\gamma_{\mathcal{U}V}(0)+\sigma_a^2,$$ 且 $\gamma_{\mathcal{U}V}(0)$ 为 $$\gamma_{\mathcal{U}V}(0)=\frac{\sigma_a^2}{1-\phi_1\theta_1}.$$

于是我们有

$$\boldsymbol{\Gamma}=\sigma_a^2\begin{bmatrix}\frac{1}{1-\phi_1^2} & \frac{1}{1-\phi_1\theta_1}\\\frac{1}{1-\phi_1\theta_1} & \frac{1}{1-\theta_1^2}\end{bmatrix},$$

从而

$$\sigma_a^2\Gamma^{-1}=\frac{1-\phi_1\theta_1}{(\phi_1-\theta_1)^2}\begin{pmatrix}(1-\phi_1^2)(1-\phi_1\theta_1) & -(1-\phi_1^2)(1-\theta_1^2)\\-(1-\phi_1^2)(1-\theta_1^2) & (1-\theta_1^2)(1-\phi_1\theta_1)\end{pmatrix}.\tag{7.67}$$

渐近地，$\hat{\phi}_1$ 服从均值为 $\phi_1$、方差为

$$\operatorname{var}(\hat{\phi}_1)=\frac{(1-\phi_1^2)(1-\phi_1\theta_1)^2}{n(\phi_1-\theta_1)^2},$$

的正态分布，而 $\hat{\theta}_1$ 服从均值为 $\theta_1$、方差为

$$\operatorname{var}(\hat{\theta}_1)=\frac{(1-\theta_1^2)(1-\phi_1\theta_1)^2}{n(\phi_1-\theta_1)^2}.$$

的正态分布。

### 7.5.2.1 ARMA(p,q) 参数的置信区间

式 7.61 的结果为 ARMA(p,q) 模型的参数提供了大样本置信区间。对应于式 7.57 的置信椭球和对应于式 7.58 的单个置信区间分别为

$$\left(\hat{\beta}-\beta\right)'\hat{\Gamma}\left(\hat{\beta}-\beta\right)\le \frac{\hat{\sigma}_a^2}{n}\chi_{1-\alpha}^2(p+q),\tag{7.68}$$

和

$$\hat{\beta}_j\pm z_{1-\alpha/2}\frac{\hat{\sigma}_a\hat{\gamma}_{jj}^{1/2}}{\sqrt{n}}.\tag{7.69}$$

可使用式 7.70 和 7.71 中估计的 AR 模型进行估计，为每个模型找出适当的权重，并近似式 7.72 中相应的无穷级数。

## 7.5.3 MA(1) 估计量的渐近比较

虽然本章讨论的用于估计 AR 过程参数的几种估计技术产生的估计量渐近等价，但对于 MA 过程参数的估计量而言，情况并非如此。为了说明这一点，我们考察 MA(1) 过程 X_t = a_t - θ₁ a_{t-1}。在例 7.6 中，我们发现 \hatθ₁ 的 MLE 渐近服从正态分布，其渐近方差为 (1 - θ₁²)/n。创新估计量和矩估计量也渐近服从正态分布，矩估计量、创新估计量和 ML 估计量的渐近方差见表 7.3（参见 Brockwell and Davis, 1991）。从表中可以看出，对于 MA(1)，

Asyvar{\hatθ₁^{MM}} > Asyvar{\hatθ₁^{(I)}} > Asyvar{\hatθ₁^{ML}}.

在表 7.4 中，给出了不同 θ₁ 取值下这些渐近方差（乘以 n）的值。

## 表 7.3

θ₁ 估计量的渐近方差

| 估计量 | 渐近方差 |
|---|---|
| 矩估计：$\hatθ₁^{MM}$ | $\frac{(1+θ₁²+θ₁⁴+θ₁⁶+θ₁⁸)}{n(1-θ₁²)}$ |
| 创新估计：$\hatθ₁^{(I)}$ | $\frac{1}{n}$ |
| 最大似然：$\hatθ₁^{ML}$ | $\frac{(1-θ₁²)}{n}$ |

## 表 7.4

不同 |θ₁| 取值下 θ₁ 估计量的渐近方差和效率比

