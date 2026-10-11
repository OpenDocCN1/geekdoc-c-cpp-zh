
对于 $\theta \in \mathbb{R}^d$，记 $f_r(\theta) = r^{-1}f(r\theta)$，则方程变为：

```
$\frac{d}{dt}\theta_i^r = f_r(\theta^r).\quad\quad (4.112)$
```

假设存在极限向量场：

```
$f_{\infty}(\theta) = \lim_{r\to\infty} f_r(\theta) = \lim_{r\to\infty} r^{-1}f(r\theta),\quad\quad\theta \in \mathbb{R}^d.\quad\quad (4.113)$
```

并将 $\infty$ 处的 ODE 定义为 (4.112) 的极限情况：

```
$\frac{d}{dt}\theta_i^{\infty} = f_{\infty}(\theta^{\infty}),\quad\quad\theta^{\infty} \in \mathbb{R}^d.\quad\quad (4.114)$
```

根据 (4.113)，我们有 $f_{\infty}(0)=0$，因此原点是 (4.114) 的平衡点。

### 命题 4.2
假设 $f$ 是全局 Lipschitz 连续的，Lips 常数为 $L$。假设极限 (4.113) 对于所有 $\theta$ 均存在，并定义连续函数 $f_{\infty}: \mathbb{R}^d \to \mathbb{R}^d$。那么，如果原点对于 (4.114) 是渐稳定的，则 ODE (4.2) 是最终界的（ultimately bounded）。

为了证明该命题，我们需要更好地理解 (4.114) 解的特殊性质：

### 引理 4.23
假设命题 4.2 的假设成立，特别是原点对于 (4.114) 是渐稳定的。那么满足以下结论：

- (i) 对于每个 $\theta \in \mathbb{R}^d$ 和 $s \ge 0$，$f_{\infty}(s\theta) = sf_{\infty}(\theta).$

- (ii) 如果 $\{\theta_i^{\infty} : t \ge 0\}$ 是 ODE (4.114) 的任意解，且 $s>0$，则 $\{y_i = s\theta_i^{\infty} : t \ge 0\}$ 也是一个解，起始于 $y_0 = s\theta_0^{\infty} \in \mathbb{R}^d$。

- (iii) 原点对于 (4.114) 是全局渐稳定的，且向原点的收敛是指数级的：对于某些 $R < \infty$ 和 $\rho > 0$，

```
$\|\theta^{\infty}\| \le Re^{-\rho t}\|\theta_0^{\infty}\|,\quad\quad\theta_0^{\infty} \in \mathbb{R}^d$.
```

证明考虑部分 (i) 中的第一个缩放结果：根据 (4.113) 的定义，对于 $s>0$，

```
$f_{\infty}(s\theta) = \lim_{r\to\infty} r^{-1}f(r\theta) = s\lim_{r\to\infty} r^{-1}f(r\theta) = sf_{\infty}(\theta).$.
```

$s=0$ 的情况是显而易见的，显然 $f_{\infty}(0)=0$。这证明了 (i)。

接下来，写下

```
$\theta^{\infty} = \theta_0^{\infty} + \int_0^t f_{\infty}(\theta^\tau^{\infty})d\tau$.
```

两边乘以 $s$ 并应用 (i) 得到 (ii)。

原点的渐近稳定性意味着：：存在 $\varepsilon > 0$，使得当 $\|\theta_0^{\infty}\| \le \varepsilon$ 时，$\lim_{t\to\infty}\|\theta_i^{\infty}\|=0$，且收敛对于初始条件是均匀的。因此，存在 $T_0$ 使得当 $t \ge T_0$ 时

```
$\|\theta^{\infty}\| \le \varepsilon$.
```

接下来，应用缩放：对于任意初始条件 $\theta_0^{\infty}$，考虑 $s = \varepsilon/\|\theta_0^{\infty}\|$ 对应的 $y_t$，使得 $\|y_0\| = \varepsilon$，则对于 $t \ge T_0$，$\|y_t\| \le \frac{\varepsilon}{2} = \frac{\varepsilon}{2}\|y_0\|$，意味着

$\|\partial_t^\infty\| \le \frac{1}{2}\|\partial_0^\infty\| \quad t \ge T_0$

这很容易推导出 (iii)。对于任意 $t$，我们可以写为 $t = nT_0 + t_0$，其中 $0 \le t_0 < T_0$，使得

$\|\partial_t^\infty\| \le \frac{1}{2}^n\|\partial_0^\infty\|$

Proposition 4.19 给出 $\|\partial_{t_0}^\infty\| \le e^l\|\partial_0^\infty\|$，因此

$\|\partial_t^\infty\| \le 2e^{l^{-(n+1)}}\partial_0^\infty$

其中右侧已安排以使用界 $t \le (n+1)T_0$，给出 $2^{-(n+1)} \le \exp(-\log(2)t/T_0)$。在 $R = 2^l$ 和 $\rho = \log(2)/T_0$ 时得到 (iii) 中的界。

命题 4.22 的证明：

$$\mathcal{E}(\theta) = \|f(\theta) - f_{\infty}(\theta)\|$$

因此根据引理 4.23，对于 $s = \|\theta\|$

$$\mathcal{E}(\theta) = \|f_s(\theta/s) - f_{\infty}(\theta/s)\|$$

由于函数 $\{f_s : s \ge 1\}$ 是均匀连续的，且当 $\|\theta/s\| \to 0$ 时，右侧趋于零。即 $\mathcal{E}(\theta) = o(\|\theta\|)$。考虑这意味着：对于任意 $\varepsilon > 0$，存在 $\mathcal{N}(\varepsilon) < \infty$，使得当 $\|\theta\| \ge \mathcal{N}(\varepsilon)$ 时，$\mathcal{E}(\theta) \le \varepsilon\|\theta\|$。从这里得到更简单的界：

$$\mathcal{E}(\theta) \le B_{\varepsilon} + \varepsilon\|\theta\|, \quad B_{\varepsilon} = \max\{\mathcal{E}(\theta) : \|\theta\| \ge \mathcal{N}(\varepsilon)\}. \quad (4.15)$$

对于任意初始条件 $\partial_0^\infty$，基于此界比较两个解：

$$\partial_t = \partial_0 + \int_0^t f(\partial^\tau)d\tau,$$

$$\partial_t = \partial_0 + \int_0^t f_{\infty}(\partial^\infty)d\tau.$$

写 $z_t = \|\partial_t - \partial_t^\infty\|$ 并使用前面的定义得到：

$$z_t \le \int_0^t \|f(\partial^\tau) - f_{\infty}(\partial^\tau)\|d\tau + \int_0^t \mathcal{E}(\partial^\tau)d\tau \le L \int_0^t z_\tau d\tau + \int_0^t \mathcal{E}(\partial^\tau)d\tau.$$

Grönwall 不等式的第二形式 (4.6c) 成立，其中 $\beta_t \equiv L$，$\alpha_t$ 为第二个积分，给出

## 4.9 QSA 的收敛理论

$z_t \le e^{Lt} \int_0^t \mathcal{E}(\partial^\tau)d\tau \le e^{Lt} \int_0^t \{B_\varepsilon + \|\partial^\tau\|\}d\tau,$

其中第二个不等式使用了 (4.15)，并选择 $\varepsilon > 0$。Proposition 4.19 给出 $\|\partial_t\| \le \{B_f + \|\partial_0\|\}e^{Lt}$，因此

```
|\partial_t - \partial_0^\infty\| = z_t \le z_t e^{Lt} + \varepsilon e^{Lt}\{B_f + \|\partial_0\|\} \{L^{-1}e^{Lt}.
```

再次应用三角不等式：

```
|\partial_t\| \le \|\partial_0^\infty\| + \varepsilon L^{-1}e^{2Lt}\|\partial_0\| + B_{\varepsilon,t},
```

其中值 $B_{\varepsilon,t}$ 可以通过整理项确定。然后使用引理 4.23，它意味着存在 $T_0$ 使得当 $t \ge T_0$ 时 $\|\partial_t^\infty\| \le \frac{1}{2}\|\partial_0^\infty\| = \frac{1}{2}\|\partial_0\|$。因此，

```
|\partial_{T_0}\| \le (\frac{1}{2} + \varepsilon L^{-1}e^{2LT_0})\|\partial_0\| + B_{\varepsilon,T_0}.
```

选择 $\varepsilon > 0$ 使得括号中的项不超过 3/4：

```
|\partial_{T_0}\| \le \rho\|\partial_0\| + B_{\varepsilon,T_0}, \quad \rho = 3/4.
```

正如引理 4.23 的证明中所述的，我们可以迭代对于每个整数 $n$ 和 $t_0 \le T_0$，得到：

```
|\partial_{nt_0+t_0}\| \le \rho^n\|\partial_0\| + \frac{1}{1-\rho}B_{\varepsilon,t_0} \le \rho^n\{B_f + \|\partial_0\|\}e^{Lt_0} + \frac{1}{1-\rho}B_{\varepsilon,T_0}.
```

这建立了最终界性，我们可以选择 $S=\{\theta : \|\theta\| \le \frac{1}{1-\rho}B_{\varepsilon,T_0} + 1\}$。

## 4.9 QSA* 收敛理论

在这种场景下，我们考虑一般的非线性 ODE (4.44)，满足假设 (QSA1)-(QSA3)（在 4.5 节引入）。定理 4.15 的证明主要是 Gronwall 不等式的直接应用，如命题 4.12 所示。QSA 的稳定性理论紧随 4.8 中综述的 ODE 稳定性理论。只有当我们考虑收敛速率时才会遇到数学挑战。这些结果还需要额外的假设，是对 (QSA2) 的微加强：

(QSA4) 向量场 $f$ 是可微的，其导数命名为

```
$A(\theta) = \partial_\theta f(\theta).$ (4.116)
```

# 132 用于算法设计的 ODE 方法

最后一个假设是对遍历性极限 (4.82) 的大幅加强：

(QSA5) 探测信号是 (4.79) 的解，其中 $\Omega$ 是欧几里得空间的一个紧集。它在 $\Omega$ 上有一个唯一的不变测度 $\mu$，并且对于每个初始条件 $\Xi_0 \in \Omega$，满足以下条件：

- * 对于每个 $\theta$，都存在一个函数 $\hat{f}(\theta)$ 满足

$$\hat{f}(\theta, \Xi_{t_0}) = \int_{t_0}^{t_1} [f(\theta, \Xi_t) - \hat{f}(\theta)] \, dt + \hat{f}(\theta, \Xi_{t_1}), \quad \text{对于所有 } 0 \le t_0 \le t_1 \quad (4.117)$$

其中 $\hat{f}(\theta) = \int_{\Omega} f(\theta, x) \mu(dx) \quad \text{且} \quad 0 = \int_{\Omega} \hat{f}(\theta, x) \mu(dx)$。

- * (ii) 函数 $f$ 及其导数 $\partial_\theta f$ 和 $\partial_\Xi f$ 在 $\theta$ 上是 $C^1$ 且满足 Lipschitz 连续的。特别地，$f$ 允许存在导数 $A$ 满足

$$\hat{A}(\theta, \Xi_{t_0}) = \int_{t_0}^{t_1} [A(\theta, \Xi_t) - A(\theta)] \, dt + \hat{A}(\theta, \Xi_{t_1}), \quad 0 \le t_0 \le t_1,$$

$A(\theta, \Xi_t) = \int_{t_0}^{t_1} \partial_\theta f(\theta, \Xi_t) \, dt = \partial_\theta f(\theta)$ 在 (4.116) 中定义。

假设 Lipschitz 连续性关于探索过程是均匀的：对于 $L_f < \infty$，

$$\begin{aligned} \|f(\theta, \Xi) - f(\theta', \Xi)\| &\le L_f \|\theta - \theta'\| \\ \|A(\theta, \Xi) - A(\theta', \Xi)\| &\le L_f \|\theta - \theta'\| \\ \|A(\theta, \Xi) - A(\theta', \Xi')\| &\le L_f \|\theta - \theta'\| \end{aligned} \quad \theta, \theta' \in \mathbb{R}^d, \Xi, \Xi' \in \Omega.$$

- * (iii) 令 $\hat{\Upsilon}_t = \int_0^t \hat{A}(\theta^*, \Xi_s) f(\theta^*, \Xi_s)$。以下极限存在：

$$\bar{\Upsilon} = \lim_{T \to \infty} \frac{1}{T} \int_0^T \hat{\Upsilon}_t \, dt = -\int_0^\infty \hat{A}(\theta^*, \Xi_t) f(\theta^*, \Xi_t) \mu(dx)$$

且部分积分是有有界的：

$$\hat{\Upsilon}_t = \int_0^t [\hat{\Upsilon}_r - \bar{\Upsilon}] \, dr, \quad \text{其中} \quad \hat{\Upsilon}_t = \Upsilon_t - \bar{\Upsilon}. \quad (4.118)$$

引入假设 (QSA5) (iii) 是因为向量 $\Upsilon$ 出现在缩放误差 $\Xi_t$ 的近似中。这与其他项相比并不大多少。特别地，如果存在有界解 $\{\hat{\Upsilon}_t\}$ 满足，则 (4.118) 中的部分积分是有界的：

$$\hat{\Upsilon}_{t_0} = \int_{t_0}^{t_1} [\hat{\Upsilon}_t - \bar{\Upsilon}] \, dt + \hat{\Upsilon}_{t_1}, \quad \text{对于所有 } 0 \le t_0 \le t_1.$$

本节的剩余部分分为五个小节：

* 第一小节总结了 QSA 收敛速率的界——见定理 4.24 和 4.25。

* 4.9.2 节涉及 (4.42) 与 QSA ODE (4.44) 之间的界，这是本节其余部分的基础。

* QSA 最终有界的标准包含在 4.9.3 节。

# 4.9 QSA 收敛理论

- 4.9.4 节包含证明假设 (QSA5) 的理论。

* 4.9.5 节包含关于收敛速率的主要证明。

### 4.9.1 主要结果与启示

(4.117) 中的符号 $\hat{f}$ 用于强调与马尔可夫过程的相似性：这是泊松方程（强制函数 $f(\cdot) = f(\cdot) - \hat{f}(\cdot)$）的解，它出现在马尔可夫过程模拟、平均控制和随机近似 [12, 39, 144]。对于由锯齿函数 $\xi_t = t \pmod 1, t \ge 1$ 定义的一维信号，泊松方程的解形式简单：

$$\tilde{g}(z) = -\int_{0}^{z} g(x) \, dx + \hat{g}(0) \quad z \in [0,1), \quad \tilde{g} = \int_{0}^{\infty} g(x) \, dx.$$

引入新符号将是有用的：对于 $\theta \in \mathbb{R}^d$ 和 $T \ge 0$，

$$\Xi_T(\theta) = \int_{0}^{T} [f(\theta, \xi_t) - \hat{f}(\theta)] \, dt = \hat{f}(\theta), \quad (4.119)$$

第二个等式遵循 (4.117)。特殊情况 $\theta = \theta^*$ 用于：

$$\Xi_T(\theta^*) = \int_{0}^{T} f(\theta^*, \xi_t) \, dt,$$
