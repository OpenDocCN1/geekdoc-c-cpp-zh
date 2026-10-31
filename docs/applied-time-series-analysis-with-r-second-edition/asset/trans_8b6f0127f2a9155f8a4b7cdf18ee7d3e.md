
需要注意的是 $\gamma_{ij}(k)=\gamma_{ji}(-k)$ 且 $\Gamma(-k)=\Gamma'(k)$，其中 $\mathbf{A}'$ 是矩阵 $\mathbf{A}$ 的转置。见下文注 4。$\Gamma(0)$ 的第 $j$ 个对角元素为 $\operatorname{Var}[X_{tj}]$。

*交叉相关*，$\rho_{ij}(k)$，定义为

$$\rho_{ij}(k)=\frac{\gamma_{ij}(k)}{\sqrt{\gamma_{ii}(0)\gamma_{jj}(0)}}.$$

相应地，相关矩阵 $\boldsymbol{\rho}(k)$，$k=0,1,\ldots$，由下式给出

$$\boldsymbol{\rho}(k)=\begin{pmatrix}\rho_{11}(k)&\cdots&\rho_{1m}(k)\\ \vdots&\ddots&\vdots\\ \rho_{m1}(k)&\cdots&\rho_{mm}(k)\end{pmatrix}. \tag{10.3}$$

## NOTES:

- 1. 变量 $X_{tj}$ 的自相关是矩阵 $\boldsymbol{\rho}(k)$，$k=0,\ \pm1,\ldots$ 的第 $j$ 个对角元素。
- 2. $\boldsymbol{\rho}(0)$ 的值 $\rho_{ij}(0)$ 衡量的是 $X_{ti}$ 与 $X_{tj}$ 之间所称的同期或同时线性关系。请注意 $\boldsymbol{\rho}(0)$ 沿对角线有 1。
- 3. $\boldsymbol{\rho}(k)$ 的一个有用表达式为

$$\boldsymbol{\rho}(k)=\begin{pmatrix}\gamma_{11}^{-1/2}&0&\cdots&0\\0&\gamma_{22}^{-1/2}&0&\vdots\\\vdots&0&\ddots&0\\0&\cdots&0&\gamma_{mm}^{-1/2}\end{pmatrix}\Gamma(k)\begin{pmatrix}\gamma_{11}^{-1/2}&0&\cdots&0\\0&\gamma_{22}^{-1/2}&0&\vdots\\\vdots&0&\ddots&0\\0&\cdots&0&\gamma_{mm}^{-1/2}\end{pmatrix}. \tag{10.4}$$
- 4. 请注意，对于自相关，定义 $\gamma(k)=E[(X_t-\mu)(X_{t+k}-\mu)]$ 和 $\gamma(k)=E[(X_{t+k}-\mu)(X_t-\mu)]$ 是等价的，且 $\gamma(k)=\gamma(-k)$。这些性质在交叉相关中并不成立。我们上面提到 $\gamma_{ij}(k)=\gamma_{ji}(-k)$（注意下标顺序的变化）。

*Caution:* 我们在此强调，对于

交叉协方差

通常使用两种定义

- a. $\gamma_{ij}(k)=E[(X_{t,i}-\mu_i)(X_{t+k,j}-\mu_j)]$（[方程 10.2](#] 中给出的定义，这里使用，Box 等（2008）及其他文献中使用）
- b. $\gamma_{ij}^{(a)}(k)=E[(X_{t+k,i}-\mu_i)(X_{t,j}-\mu_j)]$ 由 Shumway 和 Stoffer（2010）、Tsay（2002）、Brockwell 和 Davis（1991, 2002）等人使用。

当然，这两种交叉协方差的定义导致了两种相应的交叉相关定义。需要特别注意的是这两种定义*不等价*，我们提醒读者在解释交叉协方差或交叉相关结果之前，务必检查所使用的交叉协方差定义！

**Using R:** Base R 函数 `ccf(xi,xj,type = 'covariance')` 计算 $\gamma_{ij}^{(a)}(k)$（其中 xi 和 xj 分别表示第 i 个和第 j 个时间序列）。为了计算如 [方程 10.2](#] 中定义的 $\gamma_{ij}(k)$，则可以使用调用语句 `ccf(xj,xi)`。在任何一种情况下，使用 `type = 'correlation'` 计算相应的交叉相关。

Definition 10.3 将白噪声的概念扩展到多元情形。

## Definition 10.3

多元时间序列 $\{a_t; t\in T\}$ 被称为多元白噪声，如果

- 1. $E(a_t)=0$ 其中 $0$ 是 $m$ 个分量的 0 向量。
- 2. $\rho_a(k)=0,\ k\ne 0$，其中在这种情况下 $0$ 表示 $m\times m$ 的零矩阵。

应注意 Definition 10.3 对 $\rho_a(0)$ 没有限制。也就是说，$a_{ti}$ 和 $a_{tj}$ 可能同期相关，并且可能存在至少某些 $i,j$ 且 $i\ne j$ 使得 $\rho_{ij}(0)\ne 0$。我们使用记号 $a_t\sim\operatorname{MVN}(0,\Gamma_a)$ 来指定 $a_t$ 是一个多元白噪声过程且 $\Gamma(0)=\Gamma_a$。乍一看，多元白噪声过程同期相关似乎矛盾。然而，在 [图 10.2](#] 中，我们展示了来自二元白噪声时间序列 $a_t=(a_{t1},a_{t2})'$ 的长度 $n=75$ 的实现，其中可以看出每个实现沿时间轴似乎不相关，

但仔细检查表明这两个实现是正相关的。在这种情况下，Γ(0) = Γ_a 由下式给出

![](img/a0e0259119deb8c7b41dfd4f664e541d_493_0.png)

![](img/a0e0259119deb8c7b41dfd4f664e541d_493_1.png)

## FIGURE 10.2

来自二元白噪声过程的实现，其中两个白噪声过程之间存在正的同时相关，即 ρ12(0) ≠ 0。

Γ_a = ( 1 1.78 ; 1.78 4 )

and

ρ_a(0) = ( 1 0.89 ; 0.89 1 ). (10.5)

Definition 10.4 将 Definition 2.1 中定义的一般线性过程的概念扩展到多元情形，Definition 10.5 定义了多元时间序列的谱。

## Definition 10.4

多元时间序列 { X_t ; t = 0, ± 1, ± 2, ... } 被称为因果且平稳的多元一般线性过程，如果它由下式给出

$$X_t - \boldsymbol{\mu} = \sum_{j=0}^{\infty} \boldsymbol{\Psi}_j \mathbf{a}_{t-j},$$ (10.6)

其中 $\mathbf{a}_t$ 是多元白噪声且 $\Psi'_j$s 是 $m \times m$ 矩阵，使得 $\boldsymbol{\Psi}_0 = \mathbf{I}$（$m \times m$ 单位矩阵）并且其分量绝对可和。也就是说，令 $\psi_j(k,l)$ 表示 $\Psi_j$ 的第 $k$ 行第 $l$ 列的元素，则 $\sum_{j=0}^{\infty} |\psi_j(k,l)| < \infty$ 对于 $1 \le k, l \le m.$

## Definition 10.5

设 $\{X_t; t = 0, \pm 1, \pm 2, \dots\}$ 为因果平稳多元过程，其协方差矩阵 $\boldsymbol{\Gamma}(k)$ 给出于 Equation 10.1 且其中 $\sum_{k=-\infty}^{\infty} |\gamma_{jh}(k)| < \infty$ 对于 $1 \le j, h \le m$。对于 $0 \le f \le 0.5$，$\mathbf{X}_t$ 的功率谱由下式给出

$$\boldsymbol{P}_X(f) = \sum_{k=-\infty}^{\infty} e^{-2\pi i f k} \boldsymbol{\Gamma}(k).$$ (10.7)

请注意，在多元情形下，Equation 10.7 中的 $\boldsymbol{P}_X(f)$ 通常称为谱密度。为了与单变量情形的记号保持一致，我们将其称为谱。还请注意，对于每个 $f$，$\boldsymbol{P}_X(f)$ 是一个 $m \times m$ 矩阵。类似于单变量情形的 Equation 1.28，可以证明

$$\boldsymbol{\Gamma}(k) = \int_{-0.5}^{0.5} e^{2\pi i f k} \boldsymbol{P}_X(f) df,$$ (10.8)

其中 $i = \sqrt{-1}$。$\boldsymbol{P}_X(f)$ 的 $jh$ 个元素由下式给出

$$P_{jh}(f) = \sum_{k=-\infty}^{\infty} e^{-2\pi i f k} \gamma_{jh}(k),$$ 其中 $|f| \le 0.5$，且 $\gamma_{jh}(k)$ 的定义见 Equation 10.1 之后。请注意 $P_{jj}(f)$ 是单变量时间序列 $X_{tj}$ 的通常谱，而如果 $j \ne h$ 则

Then **X**_t is called a VAR(p) process, that is, a vector AR process of order p.

请注意 Equation 10.15 可以写成多元算子记号 **Φ**(B)(**X**_t − **μ**) = **a**_t，其中

**Φ**(B) = **I** − **Φ**₁B − ⋯ − **Φ**_p B^p,   (10.16)

且 B^k **X**_t = **X**_{t−k}。下面的 Theorem 10.1 给出了 VAR(p) 模型平稳性条件，其类似于单变量 AR(p) 模型中 Theorem 3.2 的条件。

## Theorem 10.1

满足 Equation 10.15 中差分方程的多元过程 **X**_t 当且仅当行列式方程的根

| **Φ**(z) | = | **I** − **Φ**₁z − ⋯ − **Φ**_p z^p | = 0,

位于单位圆之外时，才是平稳且因果的 VAR(p) 过程。

Proof: See Brockwell and Davis (1991) and Reinsel (1997).

请注意，满足 Theorem 10.1 的 VAR(p) 模型 **Φ**(B)(**X**_t − **μ**) = **a**_t 可以写成多元一般线性过程形式

**X**_t − **μ** = **Ψ**(B)**a**_t   (10.17)
= Σ_{j=0}^{∞} **Ψ**_j **a**_{t−j},

其中 **Ψ**(B) = **Φ**^{-1}(B)。

多元 Yule–Walker 方程由下式给出

**Γ**(k) = **Γ**(k−1)**Φ**₁' + ⋯ + **Γ**(k−p)**Φ**_p',   k = 1, …, p,   (10.18)

其中

**Γ**(0) = **Φ**₁**Γ**(−1) + ⋯ + **Φ**_p**Γ**(−p) + **Γ**_a,   (10.19)

这类似于单变量情形中的 [方程 3.42](#]。

$$\Gamma(0)=\Gamma(-1)\Phi_1' + \cdots + \Gamma(-p)\Phi_p' + \Gamma_a,$$  
(10.20)

这类似于单变量情形中的 [方程 3.42](#]。

在 VAR(1) 情形下，[方程 10.18](#] 和 [方程 10.19](#] 简化为 $\Gamma(k)=\Gamma(k-1)\Phi_1'$, $k>0$，和 $\Gamma(0)=\Gamma(-1)\Phi_1'+\Gamma_a$，分别。由于对于 VAR(1) 有 $\Gamma(1)=\Gamma(0)\Phi_1'$ 且对于任何因果平稳多元过程有 $\Gamma(-k)=\Gamma'(k)$，可得 $\Gamma(0)=\Phi_1\Gamma(0)\Phi_1'+\Gamma_a$。这些表达式说明了对于 VAR(1)，知道 $\Phi_1$（和 $\Gamma_a$）可以方便地计算协方差矩阵 $\Gamma(k)$，$k=0,\ \pm1,\ \ldots$。由于 $\Phi_1'=\Gamma^{-1}(0)\Gamma(1)$，因此如果已知 $\Gamma(0)$ 和 $\Gamma(1)$，也可以计算 $\Phi_1$。这些关系类似于单变量 AR(1) 情形中先前观察到的性质。参见例如 [方程 3.34](#] 和 [3.35](#]。

## EXAMPLE 10.2: A BIVARIATE VAR(1) PROCESS

考虑零均值 VAR(1) 过程

$\Phi(B)X_t=(I-\Phi_1B)X_t=a_t,$ 其中

$$\Phi_1=\begin{pmatrix}0.9 & 0.6\\-0.3 & 0.7\end{pmatrix},$$  
(10.21)

and

$$\Gamma_a=\begin{pmatrix}1 & 1.78\\1.78 & 4\end{pmatrix}.$$  
(10.22)

在此示例中 $a_t$ 具有与 [图 10.2](#] 中所示的二元白噪声实现相同的 $\Sigma_a$。在此情况下 [方程 10.13](#] 为

$$X_{t1}=0.9X_{t-1,1}+0.6X_{t-1,2}+a_{t1},$$  
(10.23)

$$X_{t2}=-0.3X_{t-1,1}+0.7X_{t-1,2}+a_{t2},$$

and the equation
