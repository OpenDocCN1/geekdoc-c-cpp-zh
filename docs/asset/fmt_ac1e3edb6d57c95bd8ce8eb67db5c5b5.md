
存在数据中非常短的周期。然而，这种行为可以归因于序列中相继值之间的负相关性 $\rho_1 = -0.497$。然而，有趣的是，自相关性对于 $k \ge 2$ 为零。此外，这种高频行为在谱密度中通过 $f = 0.5$ 处的最大值得以说明。另一方面，模型 (b) 的数据显然没有那么高振荡，这进一步通过谱密度在 $f = 0$ 处的最大值及其随着 $f$ 接近 0.5 而稳步下降得以说明。

### 3.1.2 MA(2) Model

设 $X_i$ 表示由下式给出的 MA(2) 模型

```
$X_i = a_i - \theta_1a_{i-1} - \theta_2a_{i-2}$.
```

对于该模型，有

```
$$\gamma_0 = \sigma_a^2(1 + \theta_1^2 + \theta_2^2) = \sigma_x^2$$
$\rho_1 = \frac{\theta_1 + \theta_1\theta_2}{1 + \theta_1^2 + \theta_2^2}$
```

$$\rho_2 = \frac{-\theta_2}{1+\theta_1^2+\theta_2^2}, \ \rho_k=0, k \ge 3.$

使用方程 3.6，MA(2) 过程的谱密度由下式给出

$S_X(f)=\frac{\sigma_2^2}{[1+\theta_1^2+\theta_2^2-2\theta_1(1-\theta_2)\cos 2\pi-2\theta_2\cos 4\pi]}.$

**Using R:** The twsg function `arma.wge` can be used to generate and plot a realization from an MA model, `true.arma.aut` `true.arma.spec.wge` calculate and plot the true autocorrelations and spectral densities for an MA model, respectively. Additionally, the twsg function `plots.true.wge` can be used to generate a realization, calculate the true autocorrelations and spectral density, and create a plot Figure 3.11 in this text. Be careful with the coefficients. That is, for the MA(2) model $X_t = a_t-1.1a_{t-1}+0.6a_{t-2}$ the coefficients $\theta_1$ and $\theta_2$ are 1.1, and $-0.6$, respectively. These twsg functions can also be used for AR and ARMA models which will be discussed in the future. See Appendix 3B for more details.

## 3.2 AR Processes

设 $a_t$ 为白噪声过程且如果 $X_t$, $t=0, \pm1,\dots$, $\phi_p$ 为实常数且 $\phi_p \neq 0$。那么，宽松地说，由下式指定

$X_t-\mu-\phi_1(X_{t-1}-\mu)-\phi_2(X_{t-2}-\mu)-\dots-\phi_p(X_{t-p}-\mu)=a_t, \quad (3.13)$

则 $X$ 被称为阶为 $p$ 的 AR 过程，通常缩写为 AR(p)。我们将方程 3.13 写成算子形式

$$\phi(B)(X_t-\mu)=a_t, \quad (3.14)$$

其中

AR(p) 模型在方程 3.14 中可以重写为形式 $\phi(B)X_t=\phi(B)\mu+a_t$，通过注意到

$$\phi(B)\mu=(1-\phi_1B-\dots-\phi_pB^p)\mu \neq(1-\phi_1-\dots-\phi_p)\mu \neq\phi(1)\mu,$$

可以写成

$\phi(B)X_t = \phi(1)\mu + a_t. \quad (3.15)$

量 $\phi(1)\mu$ 被称为 $MA constant$。方程 3.13 中的模型通常通过令 $\tilde{X}_t = X_t - \mu$ 来简化，这导致

$\tilde{X}_t - \phi_1\tilde{X}_{t-1} - \phi_2\tilde{X}_{t-2} - \cdots - \phi_p\tilde{X}_{t-p} = a_t, \quad (3.16)$

对应于方程 3.13。此后，除非另有说明，我们将不失一般性地假设 $\mu = 0$ 使得 $\tilde{X}_t = X_t$，并且我们将 AR(p) 模型指定为

$X_t - \phi_1X_{t-1} - \phi_2X_{t-2} - \cdots - \phi_pX_{t-p} = a_t, \quad (3.17)$

或

$\phi(B)X_t = a_t. \quad (3.18)$

同样，方程 3.1 中的 $MA(q)$ 模型通常假设 $\mu = 0$ 来书写。

NOTE: When using the AR(p) or $MA(q)$ to model a given set of stationary time series data, it will be the standard procedure to first estimate $\mu$ by $\bar{X}$, subtract $\tilde{X}$ from each observation, and model the remaining data using the "zero mean" model.

如所指出的，$MA(q)$ 过程是一般线性过程的特例，其中只有有限数量的 $\psi$-权重非零。检查方程 3.17 并不能立即揭示 AR(p) 过程与一般线性过程之间的关系。实际上，方程 3.17 给出的 AR(p) 过程的指定是不充分的，因为方程 3.17 有许多不同的解，到目前为止，我们还没有指定我们希望考虑的解。例如，如果 $X_t$ 是方程 3.17 的解且 $\phi(B)y_t=0$，则 $X_t + cy_t$ 也是方程 3.17 的解对于任意常数 $c$。因此，方程 3.17 有不可数多个解。然而，如果 $c \neq 0$，所有这些解都是不存在的，现在我们的兴趣在于平稳解。这导致以下定义：

### 3.2

假设 $\{X_t; t=0, \pm1, \pm2, \dots\}$ 是满足差分方程的因果、平稳过程

$$\phi(B)(X_t - \mu) = a_t.$

则 $X_t$ 将被称为阶为 $p$ 的 AR 过程并记为 AR(p)。再次，我们将取 $\mu=0$ 除非另有说明。

为澄清定义 3.2，考虑 AR(1) 模型

$$\phi(B)X_t = (1-\alpha B)X_t = a_t,$$

其中 $|\alpha| < 1$。注意到 $B\alpha^{-t} = \alpha^{-(t-1)}$，则

$$(1-\alpha B)X_t = \alpha'(1-B)\alpha^{-t}X_t,$$

可通过展开每一侧得到 $X_t - \alpha X_{t-1}$ 来证明。两个算子 $1-\alpha B$ 和 $\alpha'(1-B)\alpha^{-t}$ 是等价的，即

$$1-\alpha B = \alpha'(1-B)\alpha^{-t}.$

因此，

$$\alpha'(1-B)\alpha^{-t}X_t = a_t.$

所以

$$(1-B)\alpha^{-t}X_t = \alpha^{-t}X_t,$$

和

$$\sum_{k=-\infty}^{t}(1-B)\alpha^{-k}X_k = \sum_{k=-\infty}^{t}\alpha^{-k}a_k,$$

这给出

$$\alpha^{-t}X_t - \lim_{j=-\infty}^{t}\alpha^{-j}X_j = \sum_{k=-\infty}^{t}\alpha^{-k}a_k.$

由于 $|\alpha| < 1$，可知 $\alpha^{-t}X_j = 0$ 以概率 1。因此，

$$X_t = \sum_{k=-\infty}^{t}\alpha^{t-k}a_k,$$

$= \sum_{h=0}^{t}\alpha^h a_{t-h}.$

## Applied Time Series Analysis with R

显然，X，方程 3.23 满足 (3.20)，是因果的，并且由定理 2.3 是平稳的，因为 $|\alpha| < 1$ 意味着 $\sum_{p=0}^\infty |\alpha|^p < \infty$。因此，X，是因果且平稳的 AR(1) 过程。因为多项式算子 $\phi(B)$ 总是可以分解为

```
$X_t - \phi_1 X_{t-1} - \cdots - \phi_p X_{t-p} = \phi(B)X_t$\n= (1-\alpha_1 B)(1-\alpha_2 B)\cdots(1-\alpha_p B)X_t$
= \prod_{k=1}^p \alpha_k^{-1}(1-B)^{\alpha_k^{-1}}X_t$(3.24)
```

其中 $\alpha_k$ 可以是实数或复数，以下定理可以被证明。

### Theorem 3.1

设 X，为因果且原因假设

```
$\phi(B)X_t = (1-\alpha_1 B)(1-\alpha_2 B)\cdots(1-\alpha_p B)X_t = a_t,$(3.25)
```

其中 $\alpha_k$ 为实数或复数，$\alpha_k \neq \alpha_j, k \neq j$，$|\alpha_k| < 1, k=1, \dots, p$，且 $a_t$ 为零均值白噪声。则 X，为 AR(p) 过程且

```
$X_t = \sum_{\ell=0}^p \psi_{\ell}(p)a_{t-\ell},(3.26)
```

其中

- a. $\psi_1(p) = \alpha_1^{p-1}$ for $p=1$

- b. $\psi_k(p) = \frac{\alpha_k^{-p-k}(\alpha_k^{p+1}-\alpha_j^{p+1})}{\alpha_k-\alpha_j} \prod_{h \neq k}^{p-k} (\alpha_{p-k}-\alpha_h)$, for $p \geq 2$.$(3.27)

Proof: See Appendix 3A.

我们注意到定理 3.1 给出了无重根情况下的 $\psi$-权重。问题 3.33 显示了如何在使用重根的情况下使用方程 3.27。常数 $\psi(p)$ 将被称为 AR(p) 过程的“$\psi$-权重”。定义 3.3 引入了特征方程，它是 AR(p) 模型分析中的一个有用工具。

## ARMA 时间序列模型

### 定义 3.3

若 X 是由方程 3.17 定义的 AR(p) 过程，则代数方程 $\phi(z)=0$ 称为相应的特征方程，其中

$$\phi(z) = 1 - \phi_1 z - \dots - \phi_p z^p,$$

且 $z$ 为实数或复数。多项式 $\phi(z)$ 称为特征多项式。

定理 3.2 是判断给定一组 AR(p) 系数是否产生因果、平稳 AR(p) 过程的重要结果。

### 定理 3.2

过程 X，其 $\psi$ 权重如定理 3.1 中定义，当且仅当特征方程 $\phi(z)=0$ 的根全部位于单位圆之外时，才是平稳且因果的 AR(p) 过程。

证明：见附录 3A。

因此，在方程 3.25 中是 AR(p) 过程当且仅当 $|\alpha_k| < 1, k=1, \dots, p$，因为 $\alpha_k$ 是特征方程第 $k$ 个根的倒数。从方程 3.26 可明显看出 $X_t$ 是一个广义线性过程。

### 3.2.1 逆转算子

值得注意的是，$\phi(B)$ 的性质可以通过考察代数对应物 $\phi(z)$ 来找到，其中 $z$ 为实数或复数。即可以证明（见 Blackwell and Davis, 1991）对于

$$\phi(z) = 1 - \phi_1 z - \dots - \phi_p z^p,$$

$$\prod_{k=1}^p (1 - \alpha_k z),$$

其中 $|\alpha_k| < 1, k=1, \dots, p$，有 $\phi^{-1}(B) = \phi^{-1}(z)|_B$。因此，例如，若 $(1-\phi_1 B)X_t = a_t$ 且 $|\phi_1| < 1$，则由于 $(1-\phi_1 B)^{-1} = \sum_{k=0}^\infty \phi_1^k B^k$，可得

$$X_t = (1-\phi_1 B)^{-1} a_t,$$

$$\sum_{k=0}^\infty \phi_1^k B^k a_t,$$

$$\sum_{k=0}^\infty \phi_1^k a_{t-k}.$$

## 应用 R 进行时间序列分析

在本书中，由于其易用性，我们经常使用这种形式化程序来逆转算子。请注意，定理 3.1 的证明实际上是基于将 $\phi(B)$ 作为算子使用。

### 3.2.2 AR(1) 模型

我们首先考虑由下式给出的 AR(1) 模型的性质

$X_t - \phi_1 X_{t-1} = a_t, \quad (3.28)$

其中 $|\phi_1| < 1$。

- AR(1) 的 $\psi$-权重和平稳性条件：从方程 3.27 可见，AR(1) 过程的广义线性过程为

$X_t = \sum_{k=0}^\infty \phi_1^k a_{t-k}$.

即，$\psi$-权重为 $\psi_k = \phi_1^k$。特征方程由 $1 - \phi_1 z=0$ 给出，其根为 $\eta_1 = \phi_1^{-1}$，其中 $|\eta_1|=|\phi_1^{-1}|>1$ 因为 $|\phi_1| < 1$，由此可知方程 3.28 中的模型是平稳且因果的。我们也在关于逆转算子的前述讨论中注意到 AR(1) 模型的 $\psi$-权重。

- AR(1) 过程的自相关：为了求 AR(1) 过程的 $\gamma_0$ 和 $\rho_k$，需要计算期望 $E[X_tX_{t-k}] = E[X_{t-k}X_t]$。为得到 $\gamma_k$，将方程 3.28 等式两边乘以 $X_{t-k}$ $k>0$，得到

$X_{t-k}[X_t = \phi_1 X_{t-1} + a_t]$.

对两边取期望得到

$E[X_{t}X_{t-k}] = \phi_1 E[X_{t-k}X_{t-1}] + E[X_{t-k}a_t]. \quad (3.29)$

现在，$X_{t-k} = \sum_{j=0}^k \phi_1^j a_{t-k-j}$ 且因此 $X_{t-k}$ 仅依赖于 $a_{t-k-j}$ $0, 1, \dots$。由此可知 $X_{t-k}$ 与 $a_t$ 不相关，即 $E[X_{t-k}a_t]=0$ 对 $k>0$ 成立。因此，由方程 3.29，$\gamma_k = \phi_1\gamma_{k-1}$ 对 $k>0$ 成立，且

$\gamma_1 = \phi_1\gamma_0$ 且 $\gamma_2 = \phi_1\gamma_1 = \phi_1^2\gamma_0$,

从而一般地

$\gamma_k = \phi_1^k \gamma_0$, (3.30)

且

$\rho_k = \phi_1^k$, (3.31)

由于 $\gamma_k = \gamma_{|k|}$ 且 $\rho_k = \rho_{|k|}$，则对 $k=0, \pm1, \pm2, ...$，方程 3.30 和 3.31 分别变为

$\gamma_k = \phi_1^{|k|} \gamma_0$,

且

$\rho_k = \phi_1^{|k|}$, (3.32)

此外，$\gamma_0$ 可以通过用 $X_t$ 预乘方程 3.28 两边并取期望而得到，如前所述，得到

$E[X_t^2] = \phi_1 E[X_{t-1}X_t] + E[X_t a_t]$.

因此

$\gamma_0 = \phi_1 \gamma_1 + E[X_t a_t]$. (3.33)

项 $E[X_t a_t]$ 使用类似的程序求得，这次将方程 3.28 两边后乘以 $a_t$ 并取期望，得到

$E[X_t a_t] = \phi_1 E[X_{t-1}a_t] + E[a_t^2]$.

之前已证明 $E[X_{t-1}a_t] = 0$，因此由方程 3.28，$E[X_t a_t] = \sigma_a^2$。代入方程 3.33 得到

$\gamma_0 = \phi_1 \gamma_1 + \sigma_a^2$, (3.34)

从而使用方程 3.30，我们有

$\gamma_0 = \frac{\sigma_a^2}{1 - \phi_1^2}$. (3.35)

3. AR(1) 的谱和谱密度：关于逆转算子的第 3.2.1 节讨论使我们能够应用方程 2.8 得到谱

$P_X(f) = \sigma_a^2 |\psi(e^{-2\pi if})|^2

= \sigma_a^2 |\phi^{-1}(e^{-2\pi if})|^2

= \frac{\sigma_a^2}{|\phi(e^{-2\pi if})|^2}

= \frac{\sigma_a^2}{|1-\phi_1 e^{-2\pi if}|^2}$

使用方程 3.35，AR(1) 过程的谱密度因此由下式给出
