

# 应用 R 进行时间序列分析

由公式 3.129 可知，为了启动模拟，需要白噪声值 $a_1$ 以及值 $x_0$ 和 $x_{-1}$。回想一下，随机变量 $X_0$ 和 $X_{-1}$ 与 $a_1$ 不相关但彼此相关。假设噪声服从正态分布，$x_0$ 和 $x_{-1}$ 是均值为 $\mu$ 且方差-协方差矩阵为

$$\Sigma = \begin{pmatrix} \sigma_a^2 & 1-\phi_1\rho_1-\phi_2\rho_2 \\ 1-\phi_1\rho_1-\phi_2\rho_2 & 1-\phi_2 \end{pmatrix}$$

的双变量正态随机变量 $(X_i, X_j)$ 的取值

（参见公式 3.43 和 3.56）。

## 3.6.3 一般程序

从前面的 AR(2) 示例可以看出，对于高阶模型，找到合适的起始值可能很困难。因此，我们通常使用旨在对起始值相对不敏感的适当技术。由于平稳 ARMA(p,q) 过程中 $\rho_k \rightarrow 0$ 当 $k \rightarrow \infty$，因此 $X_t$ 与起始值在足够大的 $t$ 时不相关。也就是说，对于 $\varepsilon > 0$，存在一个 $K$ 使得 $|rho_k| < \varepsilon$ 对于 $k > K$。一种保守的技术是选择 $K$ 使得 $|r_{max}| < K$，其中 $|r_{max}|$ 是特征方程 $\phi(z) = 0$ 的根 $r_v$ 的最大绝对倒数。在表 3.9 中，我们给出了“预热”长度 $K$，有时称为诱导期，对于各种 $\varepsilon$ 和 $|r_{max}|$ 的值。

从 ARMA(p,q) 模型生成长度为 $n$ 的实现的一种程序是使用任意选择的起始值，生成这些起始值的实现，并仅保留最后 $n$ 个值作为实现 $x_t, t=1,...,n$。根据前面的讨论，这些最后的 n 个值与起始值“几乎不相关”。该程序在 gen.arma.wge 程序中使用，其中起始值 $a_i$ 和 $x_i$ 分别设为其无条件期望值零和 $\mu$。

### TABLE 3.9
Warm-Up Length, $K$, for Various
Values of $\varepsilon$ and $|r_{max}|$

| $\varepsilon$ | $|r_{max}|$ | $K$ |
|---|---|---|
| 0.01 | 0.90 | 44 |
| 0.05 | 0.90 | 29 |
| 0.01 | 0.95 | 90 |
| 0.05 | 0.95 | 59 |
| 0.01 | 0.99 | 459 |
| 0.05 | 0.99 | 299 |
| 0.01 | 0.999 | 4603 |
| 0.05 | 0.999 | 2995 |

# ARMA 时间序列模型

values as the realization $x_t, t=1,...,n$. According to the preceding discussion, these last n values are “nearly uncorrelated” with the starting values. This procedure is used in the gen.arma.wge program where the starting values $a_i$, and $x_i$, are set equal to their unconditional expectations of zero and $\mu$, respectively.

## 3.7 变换

有时将变换应用于时间序列数据会很有用。本节介绍关于无记忆性和 AR 变换的基本问题。

### 3.7.1 无记忆变换

有时，为了产生更接近满足基本假设的数据，有助于对每个观测值进行变换。在图 1.25a 中，我们展示了经典航空数据中航空乘客数的对数。图 3.31a 显示了“原始航空数据”（airline in tswe）未应用对数变换的情况，而在图 3.31b 中，我们展示了对数航空数据，如图 1.27a 中之前所示。图 3.31a 中的“原始”航空数据似乎不是平稳过程的实现，因为方差似乎随时间增加。在这种情况下，可以应用方差稳定变换，例如对数变换，以产生序列 $Y_t=\log(X)$，例如图 3.31b 中的序列（airlog in tswe），该序列更接近满足平稳性的方差条件。将在后续章节中给出的航空数据的参数估计、模型识别和预测技术，更适合应用于 $Y_t$。对数变换是无记忆变换的一个例子（1964）

![](img/41dcbfb9af56fa48895afde322197b0b_173_0.png)

FIGURE 3.31

(a) Airline data before and (b) after making a logarithmic transformation.

引入了一类已用于时间序列数据的无记忆变换的一般类。对于给定的 $\lambda$，使得 $0 < \lambda \le 1$，变换由

$Y = \frac{X_t^2 - 1}{\lambda}$.

指定。应用于航空数据的对数 $\lambda$ 变换是该类在 $\lambda \to 0$ 时的极限情况，以及平方根（当 $\lambda=1/2$ 时方程 1.310 的缩放版本）是此类变换中较为流行的变换之一。应注意，为了应用对数、平方根或任何其他 Box-Cox 变换，需要 $x_t > 0, t=1, n$。

**使用 R：** 如果 $x$ 是包含时间序列实现（正值）的向量，则基础 R 函数如 $y = \log(x)$、$y = \log10(x)$ 或 $y = \sqrt(x)$ 可用于对实现执行无记忆变换。

### 3.7.2 AR 变换

这里称为 AR *变换* 的第二种变换也很有用。考虑 AR(1) 模型

$$(1-0.95B)X_t = a_t,$$

并令 $Y_t$ 由

```
$Y_t = X_t - 0.95X_{t-1}$\
= (1-0.95B)X_t.$
```

定义。可以得出 $Y_t$ 是白噪声

```
$Y_t = (1-0.95B)X_{t-1}$\
= a_t.$
```

因此，AR 模型本身可以被视为变换为白噪声或“白化滤波器”。事实上，这是 AR 模型的主要应用之一。请注意，对长度为 $n$ 的实现应用方程 3.311 中的变换会产生长度为 $n-1$ 的“新”实现

```
$Y_1 = X_2 - 0.95X_1$\
$Y_2 = X_3 - 0.95X_2\
$\vdots$
$Y_{n-1} = X_n - 0.95X_{n-1}.$
```

# ARMA 时间序列

![](img/41dcbfb9af56fa48895afde322197b0b_175_0.png)

**FIGURE 3.32**
Effect of transforming realization from an AR(1) model. (a) $X_i - 0.95X_{i-1} = a_i$, (b) $Y_i = X_i - 0.95X_{i-1}$.

在图 3.32a 中，给出了长度 $n = 100$ 的实现，该实现来自方程 3.131 中给出的 AR(1) 过程 $X_i$。该实现之前已在图 3.5a 中显示。在图 3.32b 中，我们显示了 $Y_i$ 的长度 $n = 99$ 的相应实现。$X_i$ 的实现显示了第 3.2 节中讨论的 AR(1) 过程的行为，其特征方程具有正根。图 3.32b 中 $Y_i$ 的实现具有白噪声的外观。更一般地，对于 ARMA$(p,q)$ 模型

> $\phi(B)X_t = \theta(B)a_t,$  (3.132)

我们考虑确定 $Y_t$ 所满足的模型的问题，其中

> $Y_t = \alpha(B)X_t$

$\alpha(B)$ 为 $k$ 阶，即 $\alpha(B) = 1 - \alpha_1B - \dots - \alpha_kB^k$。因此，$X_i = \alpha^{-1}(B)Y_t$ 且方程 3.132 可以重写为

> $\phi(B)\alpha^{-1}(B)Y_t = \theta(B)a_t$.

有两个主要感兴趣的情况。

情况 (1) $\alpha(B)$ 是 $\phi(B)$ 的因子。在这种情况下，$k \leq p$ 且 $\phi(B)$ 可以分解为 $\phi_t(B)\alpha(B)$，因此形式上

> $\phi(B)\alpha^{-1}(B) = \phi_t(B)\alpha(B)\alpha^{-1}(B)$
$= \phi_t(B),$

即 $\phi_t(B)Y_t = \theta(B)a_t$，且 $Y_t$ 满足 ARMA$(p - k, q)$ 模型。

情况 (2) $\alpha(B)$ 不是 $\phi(B)$ 的因子且没有共同子因子：在这种情况下

> $\phi(B)\alpha^{-1}(B)Y_t = \theta(B)a_t$,

或

$\phi(B)Y_t = \alpha(B)\theta(B)a_t$,

即 $Y_t$ 为 ARMA $(p, q + k)$。

# 160 应用 R 进行时间序列分析

## **EXAMPLE 3.25: AN AR TRANSFORMATION IN WHICH $\alpha(B)$ IS A FACTOR OF $\phi(B)$**

考虑示例 3.12 中之前讨论的 AR(4) 模型。事实上，该模型由 $(1-0.95B)(1+0.8B^2)X_t = a_t$ 给出。在图 $3.33a$ 和 $b$ 中，我们显示了该 AR(4) 模型的实现和理论谱密度。这些图也分别在图 $3.18a$ 和 $3.33b$ 中显示。在表 $3.3$ 给出的因子表中，可以看出因子按顺序与系统频率 $f_0=0, 0.16$ 和 $0.5$ 相关联，这与谱密度一致。我们现在变换为 $Y_t = \alpha(B)X_t = (1+0.8B^2)X_t$。在这种情况下，可以看出 $Y_t$ 满足模型 $(1-0.95B)(1+0.8B^2)Y_t = a_t$，即模型为 AR (2)。在图 $3.33c$ 中，我们显示了变换后的 $y_t = (1-B+0.8B^2)x_t$，而在图 $3.33d$ 中，我们显示了变换后数据的 Parzen 谱密度估计。在这些图中，

![](img/41dcbfb9af56fa48895afde322197b0b_176_0.png)

**Figure 3.33**

(a) Realization of the AR(4) model $(1-0.95B)(1+0.8B^2)X_t = a_t$, (b) spectral density of the AR(4) model, (c) data in (a) transformed by $Y_t = (1-B+0.8B^2)X_t$, and (d) Parzen spectral density estimator of the data in (c).

