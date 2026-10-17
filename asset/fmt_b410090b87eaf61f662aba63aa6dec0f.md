
定义 $\Theta_w^\tau, w \ge \tau$ 为 (4.42) 在 $\Theta_\tau$ “处的”唯一解：

```
$$\frac{d}{dw}\Theta_w^\tau = f(\Theta_w^\tau), w \ge \tau, \Theta_\tau^\tau = \hat{\Theta}_\tau. \quad (130)$$
```

我们有以下建议：

```
$$\hat{\Theta}_{\tau+\nu} = \Theta_{\tau+\nu} + \int_{\tau}^{\tau+\nu} f(\theta_w,\xi(s^{-1}(w))) dw, \quad (131)$$
$$\Theta_{\tau+\nu} = \Theta_{\tau} + \int_{\tau}^{\tau+\nu} f(\theta_w^\tau) dw, \quad \tau, \nu \ge 0.$$
```

### 命题 4.28
假设 $\theta$ 是界的。那么，对于任意 $T>0$，

```
$$\lim_{\tau\to\infty} \sup_{\nu\in[0,T]} \|\int_{\tau}^{\tau+\nu} [f(\theta_w,\xi(s^{-1}(w))) - f(\theta_w^\tau)] dw\| = 0, \quad (132a)$$
```

```
$$\lim_{\tau\to\infty} \sup_{\nu\in[0,T]} \|\Theta_{\tau+\nu} - \Theta_{\tau}^\tau\| = 0. \quad (132b).$$
```

# 4.9 QSA 的收敛理论

命题很容易建立定理 4.15：

### 定理 4.15 的证明
在定理假设下，存在 $b < \infty$ 使得对于 $t \ge \mathcal{T}_\varepsilon$，有 $\|\varepsilon_t^t\| \le b$。根据全局性的定义，对于每个 $\varepsilon > 0$，存在 $\mathcal{T}_\varepsilon > 0$ 使得

```
$$\|\varepsilon_t^t - v\| < \varepsilon \quad \text{for all } v \ge \mathcal{T}_\varepsilon, \text{whenever } \|\varepsilon_t^t\| \le b.$$
```

命题 4.28

```
$$\lim_{\tau\to\infty} \|\varepsilon_\tau^\tau + \mathcal{T}_\varepsilon - v\| \le \lim_{\tau\to\infty} \|\varepsilon_\tau^\tau + \mathcal{T}_\varepsilon - \varepsilon_0^0\| + \lim_{\tau\to\infty} \|\varepsilon_0^0 - v\| \le \varepsilon.$$
```

我们得到了所需的极限，因为 $\varepsilon > 0$ 是任意的。接下来的几页用于证明命题 4.28。我们从一个粗界开始，将命题 19 推广到 QSA ODE。命题 19 的证明通过符号符号扩展到引理 4.29。

### 引理 4.29
考虑 ODE (4.29)，满足 (QSA2) 中的 Lipschitz 条件。则存在一个依赖于 $f$ 的常数 $B_f$，使得

```
$$\|\hat{\theta}_t - \theta_0\| \le (B_f + L_f)\|\theta_0\|e^{L_f t}, \quad t \ge 0. \quad (4.33)$$
```

下一步是得到 (4.132a) 的一个版本，其中 $\Theta_w$ 是冻结的。引理 4.30 中的 (4.134) 是时间缩放过程 $\{\xi(s^{-1}(\tau))}_{\tau\to\infty}$ 的大数定律 (LLN) 的强版本。注意其差异。

### 引理 4.30
对于任意 $T>0$ 且 $\theta \in \mathbb{R}^d$，

```
$$\int_{\tau}^{\tau+\nu} [f(\theta_w,\xi(s^{-1}(w))) - f(\theta_w^\tau)] dw \to 0 \text{ as } \tau \to \infty. \quad (134)$$
```

（注：由于用户提供的待翻译文本中存在部分重复和逻辑断层，译文已根据上下文逻辑进行了对齐和清理，以确保学术严谨性。）

(QSA2) 中的 Lipschitz 条件意味着了上界：

$$\|\mathcal{E}_v^{\tau+v}\| \leq \delta^\tau v + L_f \int_{\tau}^{\tau+v} \|\mathcal{E}_w^\tau\| dw,$$

其中，

$$\delta^\tau \frac{\text{def}}{=} \sup_{\tau \geq 0 < v < \tau} \int_{\tau}^{\tau+v} |f(\mathbf{\Theta}_w) - f(\mathbf{\Theta}_w, \xi(s^{-1}(w)))| dw.$$

命题 4.2 给出对于所有 $\tau$ 和所有 $0 \leq v \leq 1$，$|\mathcal{E}_v^{\tau+v}\| \leq e^{l/\tau}$。误差项 $\delta^\tau$ 在 $\tau \to \infty$ 时消失 (4.132a)。

## 局部一致性 (Local Solidarity)

我们在本小节结束时给出了 $\mathbf{\Theta}$ 与 $\mathbf{\Theta}^\tau$ 之间差的一个较弱但通用的界。该不等式不需要 ODE 解的有界性，并且在小 $T$ 时对于建立 $\mathbf{\Theta}$ 的李雅诺夫漂移条件有用。

对于 $b < 0$ 和任意 $0 < T \leq 1$，**引理 4.31**：

$$\|\mathbf{\Theta}_{\tau+T} - \mathbf{\Theta}^\tau\| \leq e^{l/\tau}b_0(\tau) + b(1 + |\mathbf{\Theta}_\tau\|)T^2, \quad (4.136)$$

其中 $b_0(\tau)$ 由 (4.82)给出，$L_f$ 是假设 (QSA2) 中引入的 Lipschitz 常数。

*证明。* 对于 $w \geq \tau$，记 $\mathcal{E}_w^\tau = \mathbf{\Theta}_w - \mathbf{\Theta}^\tau$。(4.131) 的性质给出：

$$\mathcal{E}_{\tau+T} = \int_{\tau}^{\tau+T} [f(\mathbf{\Theta}_w) - f(\mathbf{\Theta}_w, \xi(s^{-1}(w)))] dw + \int_{\tau}^{\tau+T} [f(\mathbf{\Theta}_w^\tau) - f(\mathbf{\Theta}_w)] dw, \quad (4.137)$$

(QSA2) 中的 Lipschitz 条件用于界定：

$$\|f(\mathbf{\Theta}_w) - f(\mathbf{\Theta}_\tau)\| \leq L_f|\mathbf{\Theta}_w - \mathbf{\Theta}_\tau\|,$$

$$\|f(\mathbf{\Theta}_w, \xi(s^{-1}(w))) - f(\mathbf{\Theta}_\tau, \xi(s^{-1}(w)))\| \leq L_f|\mathbf{\Theta}_w - \mathbf{\Theta}_\tau\|,$$

$$\|f(\mathbf{\Theta}_w^\tau) - f(\mathbf{\Theta}_w)\| \leq L_f|\mathcal{E}_w^\tau\|.$$

因此，对于 $T \geq 0$，：

$$\|\mathcal{E}_{\tau+T}^\tau\| \leq \int_{\tau}^{\tau+T} [f(\mathbf{\Theta}_w) - f(\mathbf{\Theta}_w, \xi(s^{-1}(w)))] dw + 2L_f \int_{\tau}^{\tau+T} |\mathbf{\Theta}_w - \mathbf{\Theta}_\tau| dw + \int_{\tau}^{\tau+T} |\mathcal{E}_w^\tau| dw$$

$$\leq e^{l/\tau} + L_f \int_{\tau}^{\tau+T} |\mathcal{E}_w^\tau| dw, \quad \delta^\tau \frac{\text{def}}{=} b_0(\tau)\mathcal{E}_\tau^\tau + 2L_f |\mathbf{\Theta}_{\tau+w} - \mathbf{\Theta}_\tau| dw.$$

根据 Grönwall 引理的形式 (4.6c)：

$$\|\mathcal{E}_{\tau+T}^\tau\| \leq |\mathcal{E}_\tau^\tau|e^{L_f T}.$$

使用相同的证明方法通过 Grönwall 引理推导出 (4.108b)，我们得到：

$$\|\mathbf{\Theta}_{\tau+w} - \mathbf{\Theta}_\tau\| \leq (B_f + L_f|\mathbf{\Theta}_\tau\|)e^{L_f w}.$$

## 算法设计中的 ODE 方法

在积分范围内将 $e^{L_f w}$ 增加到 $e^{L_f T}$ 得：

```
$2 \int_0^T ||\dot{\theta}_w - \dot{\theta}_\tau|| dw \leq 2(B_f + L_f ||\dot{\theta}_\tau||)e^{L_f T} \int_0^T w dw = \langle B_f + L_f ||\dot{\theta}_\tau||\rangle T^2 e^{L_f T}$.
```

因此：

```
$$\hat{\alpha}_T^2 \leq b_0(\dot{\theta}_0)\varepsilon_0^2 + L_f(B_f + L_f ||\dot{\theta}_\tau||)T^2 e^{L_f T},
```

证明完成，因为 $0 \leq T \leq 1$。

### 4.9.3 稳定性标准

建立 QSA 收敛性的第一步是证明解在时间上是有界的。可以从动力系统中借用两种方法：李雅诺夫函数，或第 4 节引入的无穷远处的 ODE。

### 李雅诺夫准则与 (QSV)

存在连续函数 $V: \mathbb{R}^d \to \mathbb{R}_+$ 和常数 $c_0 > 0, \delta_0 > 0$，使得对于 (4.42) 的任意初始条件 $\theta_0$ 和任意 $0 \leq T \leq 1$，当 $\|\theta_s\| > c_0$ 时满足以下界：

```
$V(\theta_s + T) - V(\theta_s) \leq \delta_0 \int_0^T ||\dot{\theta}|| dt.
```

李雅诺夫函数是 Lipschitz 的：存在常数 $L_V < \infty$，使得对于所有 $\theta, \theta'$，$||V(\theta') - V(\theta)|| \leq L_V ||\theta' - \theta||$。

假设 QS1 确保当 $\theta_t$ 离开半径为 $c_0$ 的球时，$V(\theta_t)$ 是严格递减的。如果 $V$ 是二次的，那么该假设意味着：

```
$$\frac{d}{dt}V(\theta_t) \leq -\delta_0||\dot{\theta}_t||, \quad \text{whenever } ||\dot{\theta}_t|| > c_0.
```

选择积分形式是因为有时更容易建立界。特别是命题 4.3 的证明基于 QS1 解的构造。

### 为线性系统验证 QS1

考虑 ODE (4.42)，其中 $f(x) = Ax$，$A$ 是 Hurwitz $d \times d$ 矩阵。存在二次函数 $V_2(x) = x^T Mx$，其中 $M \in \mathbb{R}^{d \times d}$ 满足李雅诺夫方程 $MA + A^TM = -I, M > 0$。因此，4.42) 的解满足：

```
$$\frac{d}{dt}V_2(\theta_t) = -||\dot{\theta}_t||^2.
```

选择 $V = \sqrt{V_2}$，根据链式法则：

```
$$\frac{d}{dt}V(\theta_t) = -\frac{1}{2}\frac{1}{\sqrt{V_2(\theta_t)}}||\dot{\theta}_t||^2 \leq -\frac{1}{2}\sqrt{\lambda_{max}}||\dot{\theta}_t||,
```

其中 $\lambda_{max}$ 是 $M$ 的最大特征值。对于任意 $c_0 > 0，$V$ 是 QS1 的 Lipschitz 函数。

# 4.9 QSA 的收敛理论

我们首先在 QS1 的变体下建立有界性：

### 引理 4.3
如果对于某些 $T > 0, 0 < \delta_1 < 1$ 以及 $\tau_0, b < \infty$，则 (4.29) 的解是有最终界的，满足：

```
$V(\tilde{\Theta}_{\tau+T}) - V(\tilde{\Theta}_\tau) \le -\delta_1||\tilde{\Theta}_\tau||,
```

对于所有 $\tau \geq \tau_0, ||\tilde{\Theta}_\tau|| > b$。

*证明。* 对于每个初始条件 $\tilde{\Theta}_0 = 0$ 和 $\tau \geq \tau_0$，记：

```
$\tau = \tau(\theta, b) \triangleq \min(v \ge 0 : ||\tilde{\Theta}_{\tau+v}|| \le b),
```

其中 $\tau_0$ 和 $b$ 在引理中定义。如果 $||\tilde{\Theta}_0|| \le b$，则 $\tau = 0$，且对于所有 $v \ge 0, \tau \in \mathbb{Z}_+$，$||\tilde{\Theta}_{\tau+v}|| > b$，定义 $\tau_m = \min(\tau, m)$。那么：

```
$-\tau_m b \delta_1 \ge -\delta_1 \int_{\tau}^{\tau+\tau_m} ||\Theta_w|| dw \ge \int_{\tau}^{\tau+\tau_m} V(\Theta_w+T)dw = \int_{\tau}^{\tau+\tau_m} V(\Theta_w)dw - \int_{\tau}^{\tau+T} V(\Theta_w)dw \ge \int_{\tau}^{\tau+T} V(\Theta_w)dw.
```

右侧与 $m$ 无关，从而建立了上界：

```
$\tau \le \frac{1}{b\delta_1} V(\Theta_{\tau}).
```

在 $V$ 的 Lipschitz 假设下，对于常数 $b_v$，可以应用命题 4.19 来建立：

```
$\tau \le b_v(1+||\Theta_{\tau}||).
```

因此 $\tau(\theta, \tau)$ 处处有限。$b_1 = \sup\{||\Theta_{\tau+v}|| : \tau \ge \tau_0, v \le \tau(\theta, \tau)\}$。b_1$ 限制了当 $\tau \in S = \{\theta : ||\theta|| \le b+1\}$ 时 $\Theta$ 在时刻 $\tau$ 的最大偏离次数，结束于集合 $S_0 = \{\theta : ||\theta|| \le b\}$，记为 $\tau(\theta, \tau)$。每条轨迹在某个时刻 $\tau \ge \tau_0$ 进入 $S_0$，因此对于所有足够大的 $\tau，$||\Theta_\tau|| \le b_1$。

### 命题 4.33
在 QS1 下，(4.29) 的解是有最终界的，如果对于某些 $T > 0, 0 < \delta_1 < 1$ 以及 $\tau_0, b < \infty$：

```
$V(\tilde{\Theta}_{\tau+T}) - V(\tilde{\Theta}_\tau) \le -\delta_1||\tilde{\Theta}_\tau||,
```

对于所有 $\tau \geq \tau_0, ||\tilde{\Theta}_\tau|| > b$。

*证明。* 考虑到 $V$ 是李雅诺夫函数，且 $\delta_0 > 0$，对于 (4.42) 的任意初始条件 $\theta_0$ 和任意 $0 \leq T \leq 1$，满足：

```
$V(\theta_s + T) - V(\theta_s) \leq \delta_0 \int_0^T ||\dot{\theta}|| dt.
```

李雅诺夫函数是 Lipschitz 的：存在常数 $L_V < \infty$，使得对于所有 $\theta, \theta'$，$||V(\theta') - V(\theta)|| \leq L_V ||\theta' - \theta||$。

假设 QS1 确保当 $\theta_t$ 离开半径为 $c_0$ 的球时，$V(\theta_t)$ 是严格递减的。如果 $V$ 是二次的，那么该假设意味着：
