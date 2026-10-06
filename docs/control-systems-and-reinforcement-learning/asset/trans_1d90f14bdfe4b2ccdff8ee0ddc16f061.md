

## 4.9 QSA 的收敛理论

命题 4.34 的证明：选取 $T > 0$，使得当 $t \ge T$ 时，对于 (4.139) 的任意解以及任意初始条件 $\partial_0 \theta = \theta$，均有 $|\partial_t \theta| \le \frac{1}{2}\|\theta\|$。我们随后定义

```
$V(\theta) = \int_0^T |\partial_t \theta| dt, \quad \partial_0 \theta = \theta$，
$V(\theta) = \int_0^T V^{\infty}(\theta_t)dt, \quad \theta_0 = \theta$.
```

Gronwall 不等式表明它是 $\theta$ 的利普希茨连续函数。此外，应用引理 4.35 可以证明第一个是径向齐性的，即对于每个 $\theta$ 和 $s > 0$，有 $V^{\infty}(s\theta) = sV^{\infty}(\theta)$，并且对于某些 $\delta > 0$ 满足下界：

```
$V^{\infty}(\theta) \ge \delta|\theta|$
```

因此，这是 ODE=$\infty$ 的李雅诺夫函数：对于每个初始条件 $\partial_0^{\infty} = \theta$，

```
$V^{\infty}(\partial_T^{\infty}) = \int_0^T |\partial_{t+T}^{\infty}| dt \le \frac{1}{2}V^{\infty}(\theta) \le V^{\infty}(\theta) - \frac{1}{2}\delta|\theta|$.
```

下一步是证明当 $\partial_T^{\infty}$ 替换为 $\partial_T$ 时，类似的边界仍然。令 $L_V$ 表示 $V^{\infty}$ 的利普希茨常数。上述边界结合引理 4.36 得到

```
$V^{\infty}(\partial_T) \le V^{\infty}(\theta) - \frac{1}{8}\delta|\theta| + L_V(B_T(\varepsilon)) + K_T[1 + |\theta|]$.
```

固定 $\varepsilon \in (0,1)$ 使得

```
$L_V K_T \varepsilon \le \delta/A$,
```

得到

```
$V^{\infty}(\partial_T) \le V^{\infty}(\theta) - \frac{1}{8}\delta|\theta| + K'_V$
```

其中 $K'_V = L_V(B_T(\varepsilon)) + K_T$。为了完成证明，写下

```
$V(\theta_s) = \int_s^T V^{\infty}(\theta_t)dt + \int_0^s V^{\infty}(\theta_{T+t}) dt$.
```

上述边界给出

```
$V^{\infty}(\partial_T+t) \le V^{\infty}(\theta_t) - \frac{1}{8}\delta|\theta_t| + K'_V$
```

使得

```
$V(\theta_s) \le V(\theta_0) - \frac{1}{8}\delta \int_0^s |\theta_t| dt + sK'_V$.
```

该边界意味着 (QSVI)。

### 4.9.4 确定马尔可夫模型

这里的目标是在简单的设置下理解假设 QSA5。为此，我们在 (4.117) 的函数 $f(\theta, \xi)$ 中抑制变量 $\theta$，并采用新的符号：

```
$$\hat{g}(\mathcal{E}_{t_0}) = \int_{t_0}^{t_1} |g(\mathcal{E}_t) - g| dt + \hat{g}(\mathcal{E}_{t_1}), \quad 0 \leq t_0 \leq t_1.
```

我们本质上固定了单个索引 $i$ 和参数 $\theta$，并设置 $\hat{g}(\mathcal{E}_t) \overset{def}{=} f(\theta, \mathcal{E}_t)$。这是泊松方程的一种——进一步讨论见第 4.9 节。函数 $\hat{g}$ 是解（在某些应用中称为相对值），$g$ 是激励函数，$\hat{g}$ 是它的稳态均值。引理 4.37 涉及特殊情况 (4.80)，其中 $H$ 具有 $z \in \mathcal{C}^K$。

**引理 4.37** 假设 $g: \mathcal{C}^K \to \mathbb{R}$ 允许泰勒表示，

```
$g(z) = \sum_{n_1,...,n_K} a_{n_1,...,n_K} z_1^{n_1}...z_K^{n_K}, \quad z \in \Omega.$
```

其中求和涵盖了 $\mathbb{Z}_+^K$ 中所有长度为 $K$ 的序列，且系数 $(a_{n_1,...,n_K}) \subset \mathcal{C}^K$ 是绝对可和的：

```
$\sum_{n_1,...,n_K} |a_{n_1,...,n_K}| < \infty.$
```

那么，根据 (4.80) 定义的 $\xi$，

- (i) 遍历学极限成立：

```
$$\hat{g} = \lim_{T \to \infty} \frac{1}{T} \int_{0}^{T} \hat{g}(\mathcal{E}_t) dt = \int_{0}^{1}\int_{0}^{1} g(e^{2\pi t_1}...e^{2\pi t_K}) dt_1dt_K,$$
```

其中 $g = 0$（当每个 $i$ 的 $n_i = 0$ 时）。

- (ii) 在 (4.10) 中存在解 $\hat{g}: \mathcal{C}^K \to \mathbb{R}$。它的形式为 (4.11)：

```
$$\hat{g}(x) = \sum_{n_1,...,n_K} a_{n_1,...,n_K} x_1^{n_1}...x_K^{n_K},
```

其中每个系数 $|a_{n_1,...,n_K}| \leq |a_{n_1,...,n_K}|/\omega$。

证明使用复指数得到简单公式：

```
$$\hat{g}(\mathcal{E}_{t_0}) = \sum_{n_1,...,n_K} a_{n_1,...,n_K} \exp(\{n_1\omega\}) dt.
```

绝对可和性 (4.12) 证明了 Fubini 定理：

```
$$\int_{t_0}^{t_1} [\hat{g}(\mathcal{E}_{t_0}) - g] dt = \sum_{n_1,...,n_K} a_{n_1,...,n_K} \int_{t_0}^{t_1} \exp(\{n_1\omega+...+n_K\omega\}) dt,
```

```
$$\hat{g}(\mathcal{E}_{t_0}) - \hat{g}(\mathcal{E}_{t_1}).
```

其中 $\hat{g}$ 由 (4.13) 给出，且 $\bar{a}_0 = 0$（对于每个 $k$），对于其他系数，$\hat{a}_{n_1,...,n_K} = a_{n_1,...,n_K}\{n_1\omega+...+n_K\omega\}^{-1}$。

## 4.9 QSA 的收敛理论

引理证明了 (QSA) $f_i(\cdot, \cdot)$ 对于 $i$ 和 $\theta$ 满足泰勒级边界，以及对于导数 $\frac{\partial}{\partial \theta_j}f_i(\cdot, \cdot)$。虽然任何算法都不需要 $f$ 的显式公式，但在 QSA ODE 的精细收敛速率分析中可能有用。特别是，定理 24 中得到的缩放误差 $Z_t = \frac{1}{a_t}(\Theta_t - \overline{\Theta}_t)$ 取决于 $\tilde{f}(\Theta_t, \Xi_t)$。

### 4.9.5 收敛速率

我们从命题 4.27 的证明开始。根据引理 4.14，对于 $t \ge t_0$，恒等式 $\overline{\Theta}_t = \theta_t$ 和 $a^{det}=s_t \ge a_0$。

命题 4.27 的证明：对 (4.72) 两边求导，使用乘积法则，

```
$$\frac{dZ_t}{dt} = \frac{d}{dt}\left(\frac{1}{a_t}(\Theta_t - \overline{\Theta}_t)\right)\\\\left(-\frac{1}{a_t}\frac{d}{dt}a_t\right)(\Theta_t - \overline{\Theta}_t) + f(\Theta_t, \Xi_t) - f(\overline{\Theta}_t)\\= r_t Z_t + f(\Theta_t, \Xi_t) - \tilde{f}(\overline{\Theta}_t)
```

其中在最后一个方程中使用了对数导数的链式法则（记得 $r_t = -\frac{d}{dt}\log(a_t)$ 和 $Z_t$ 的定义）。

加上并减去 $f(\overline{\Theta}_t)$，我们得到一个启发性的分解：

```
$$\frac{dZ_t}{dt} = r_t Z_t + [f(\overline{\Theta}_t) - f(\overline{\Theta}_t)] + [f(\Theta_t, \Xi_t) - f(\overline{\Theta}_t)]
```

$R_t$: Almost数
$\Xi_t$: 有界扰动

也就是说，在命题 4.27 的假设下，

```
$R_t = A(\overline{\Theta}_t)[\Theta_t - \overline{\Theta}_t] + \Xi_t,
```

其中，在 $A = \partial f$ 的利普希茨条件下，

```
$$\|\Xi_t\|^2 \le a_t(\|\Theta_t - \overline{\Theta}_t\|^2) = o(a_t)
```

这完成了 (4.12a) 的证明，其中 $a_t = 1/t$。
如果得到 $r_t = 1/(1+t)$，则方程 (4.12a) 意味着近似 (4.12b)，其中 $\Delta_t$ 的定义被修改以包含将 $A(\overline{\Theta}_t)$ 替换为其极限 $A^*$ 产生的误差。

考虑下一个“增益” $a_t = 1/(1+t)$，$\rho \in (0,1$，使得 $r_t = \rho/(1+t)$。得到简单的近似 (4.12d)，其中 $\Delta_t$ 有一个额外项：一次将 $A(\overline{\Theta}_t)$ 替换为其极限 $A^*$。

记得变量：$\hat{g}(\mathcal{E}_{t_0}) - \hat{g}(\mathcal{E}_{t_1})$ 是为了消除 (4.12) 中的非消失噪声 $\Xi_t$。

## 4.6 设计 ODE 方法

比例 $r_t/a_t$ 在算法中是有界的，对于 $a_t = 1/t$。

**引理 4.38** 在命题 4.27 的假设下，假设对于每个 $i$，$r_t/a_t \le b$，对于常数 $b$。

使用复指数得到以下公式：

```
$$\hat{g}(\mathcal{E}_{t_0}) = \sum_{n_1,...,n_K} a_{n_1,...,n_K} \exp(\{n_1\omega\}) dt.
```

其中 $\hat{g}$ 由 (4.13) 给出，且 $\bar{a}_0 = 0$（对于每个 $k$），对于其他系数，$\hat{a}_{n_1,...,n_K} = a_{n_1,...,n_K}\{n_1\omega+...+n_K\omega\}^{-1}$。

在 (44) 处证明了 $\

```
$$\hat{g}(\mathcal{E}_{t_0}) - \hat{g}(\mathcal{E}_{t_1}).
```

其中 $\xi_t^Y$ 随 $t \to \infty$ 消失。

