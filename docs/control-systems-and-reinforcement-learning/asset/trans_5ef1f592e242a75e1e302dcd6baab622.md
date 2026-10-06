

# 算法设计的 ODE 方法

![](img/0790f102da4ffa7564329bf76c7d0815_131_0.png)

**图 4.8** 用于无梯度优化的极值搜索控制。

控制 (ESC)，在纯确定性设置下公式化。当将其转化为 QSA 时，SPSA 与 ESC 之间的相似性变得更加清晰。
在机器学习社区中，形式如 (4.94) 的算法被称为随机梯度下降 (SGD)。这使用了本书中的一些术语，如*拟随机梯度下降* (qSGD)。本章稍后展示的算法 #1 是 [329] 中引入的单次测量形式 SPSA 的 QSA 解释，而 qSGD #2 是 ESC 的一个非常特殊的特例——它将基于图 4.8 所示的通用架构进行解释。

## 4.6.1 模拟退火算法

SPSA 和 ESC 算法的主要动力是它们可以完全基于对损失函数的观测来运行。次要动力是探测设计旨在模拟用于非凸函数优化的“模拟退火”算法：探测可以帮助避免局部极值。此处描述的示例已说明到此。

![](img/0790f102da4ffa7564329bf76c7d0815_131_1.png)

图 4.9 显示了一个高度非凸函数的图表，该函数定义为凸二次函数的“软最小”（soft min）：

> $$\Gamma(\theta) = -\log\left(\sum_{i=1}^{4} \exp(-\{\|z_i - \theta^*\|^2/\sigma^2\)\right)$$

其中 $\sigma = 1/10$，且

${[\theta, z_i\]} = \{\{\left(\binom{1}{0}\right), -1\], [\left(\binom{1}{1}\right), -2\], [\left(\binom{0}{1}\right), -3\]\{\}.$

**图 4.9** 一个高度非凸的函数。

算法 qSGD #1 在单位中定义。它在这个特殊情况下经过了测试：最小化点为 $\Gamma(\theta^*) \approx -300$。

```
$$\frac{d}{dt}\Theta_t = -a_t\varepsilon_d\Gamma(\Theta_t + \varepsilon_d)$$
```

使用 $\varepsilon = 0.15$，$a_t = \min{\{\bar{z}, (1+t)^{-\rho}\}}$，其中 $\rho = 0.9$ 且 $\bar{z} = 10^{-3}$。探测信号满足 (4:48)。

```
$$\varepsilon_d = \sqrt{2}[\sin(t\omega_1), \sin(t\omega_2)]^T$$
```

其中 $\omega_1 = 1/4$且 $\omega_2 = 1/e^2$，以获得吸引力的图表——更高的频率会导致更快的收敛。

## 4.6 无梯度优化

![](img/0790f102da4ffa7564329bf76c7d0815_132_0.png)

(a) PGR 估计：接近最优

**图 4.10** 最小化具有多个局部极值的损失函数：虽然 $\Gamma(\Theta_t)$ 剧烈震荡，但估计值 $\hat{\Theta}_T^\Gamma$ 接近最优（通过对最后20%的估计取平均值）。

这些超参数是通过试错得到的：如果 $\bar{a}$ 或 $\varepsilon$ 太小，我们有时会被困在局部极值中。

使用带有1次采样的标准欧拉方案对 ODE 进行近似：粗略的 ODE 近似要求 $\omega_1/\omega_2$ 为无理数。图 4.10 右侧的两个幅图显示了 $\mathbb{R}^2$ 中 $\Theta_t$ 的演化，其中 $0 \leq t \leq 5 \times 10^4$，$\Theta_0 = (-2, 2)$。图显示估计在运行过程中存在显著变化，但在图 (c) 中，显然它们被困在了吸引范围内。

此外，平均化非常成功：估计值 $\hat{\Theta}_T^\Gamma$ 是通过对最后20%的运行取平均得到的。发现 $\Gamma(\hat{\Theta}_T^\Gamma)$ 只比 $\Gamma(\theta)$ 大一小部分。

## 4.6.2 算法列表

在定义的每个算法中，假设过程 $\Psi$ 是两项之和：$\Psi_t = \Theta_0 + \varepsilon\Xi_t, t \geq 0$，其中 $\varepsilon > 0$，且 $\Xi_t$ 是 $d$ 维探测信号。除非另有说明，否则我们强制归一化条件：

```
$$\lim_{T\to\infty} \frac{1}{T} \int \Xi_t dt = 0, \quad \frac{1}{T} \int \Xi_t\Xi_t^T dt = I \quad (95)$$
```

使用正弦波混合很容易安排。最简单的：

### SGD #1

对于给定的 $d \times d$ 正定矩阵 $G$ 和 $\Theta_0 \in \mathbb{R}^d$：

```
$$\dot{\Theta}_t = -a_t\frac{1}{\varepsilon}G\Gamma(\Theta_t), \quad (96a)
```

```
$$\Psi_t = \Theta_t + \varepsilon\Xi_t. \quad (96b)$$
```

# 算法设计的 ODE 方法

该算法形式为 (4.44)：

```
f(0, \varepsilon_d) = -\frac{1}{\varepsilon}G\varepsilon_d\Gamma(\theta).
```

如果 $\Gamma: \mathbb{R}^d \to \mathbb{R}$ 是连续可微的，目标函数的二阶泰勒展开给出：

```
\Gamma(0 + \varepsilon_d) = \Gamma(0) + \varepsilon_d\nabla\Gamma(0) + \frac{1}{2}\varepsilon_d^2\nabla^2\Gamma(0)
```

以及 $f(0, \varepsilon_d) = -\frac{1}{\varepsilon}G\Gamma(0)\varepsilon_d - G\varepsilon_d^2\nabla(0) + O(\varepsilon),$其中误差符号 $o(\cdot)$ 和 $O(\cdot)$ 在附录 A 中回顾。根据 (4.95)，这意味着平均场的如下近似：

```
f_{\varepsilon}(\theta) = \lim_{T\to\infty}\frac{1}{T}\int_0^T f(\theta_t)dt = -G\Gamma(\theta) + O(\varepsilon).
```

QSA 理论预测 qSGD #1 在选择 $G = I$ 时将近似梯度下降算法。下一个算法需要对测量值求导。其动力是：

```
$$\frac{d}{dt}(\Psi_t) = \nabla\Gamma(\Psi_t)^\top\varepsilon_t,$$
```

其中撇号表示 $\varepsilon'_t = \frac{d}{dt}\varepsilon_t$。

### qSGD #2

对于给定的 $d \times d$ 正定矩阵 $G$ 和初始条件 $\Theta_0$：

```
$$\frac{d}{dt}\Theta_t = -\frac{1}{\varepsilon}G\varepsilon_d\Gamma(\Psi_t).
```

```
$$\Psi_t = \Theta_t + \varepsilon\Xi_t.
```

该算法完美契合图 4.8 中的 ESC 架构，其中高通（HP）滤波器被选择为纯求导：

```
$$\dot{\Gamma}(t) = \frac{d}{dt}\varepsilon_t \frac{d}{dt}\Gamma(\Psi_t). \in \mathbb{R}^{2m}$$
```

算法 (4.99) 也可以被转化为 QSA ODE，其中我们将 $\varepsilon_t = (\varepsilon_t, \frac{d}{dt}\varepsilon_t) \in \mathbb{R}^{2m}$ 视为探索方程。(4.99) 给出：

```
f(0, \varepsilon'_0) = -\frac{1}{\varepsilon}G\{\varepsilon'_0\}^\top\nabla\Gamma(\theta + \varepsilon_d).
```

分析这两个算法每一个都面临挑战。qSGD #2 的挑战是对观测值 $\{\Gamma(\Psi_t)\}$ 求导。这是用高通滤波器代替求导的动力。

对于 qSGD #1，挑战来自于 (4.97) 中 $f$ 的形式。在许多问题中，我们知道 $\nabla\Gamma$ 是全局 Lipschitz 连续的，但 $\Gamma$ *不是*。在这种情况下，$f$ 在 $\theta$ 上不是 Lipschitz 连续，这将是理论中的一个长期假设。这不是巨大的挑战，因为我们可以修改算法以获得收敛（例如，将参数估计投影到有界集合上）。

下一个算法很容易建立 Lipschitz 连续性。

### qSGD #3

对于给定的 $d \times d$ 正矩阵 $G$ 和初始条件 $\Theta_0$：

```
$$\frac{d}{dt}\Theta_t = -a_t\frac{1}{\varepsilon}G\xi_t\{\Gamma(\Theta_t + \varepsilon\xi_t) - \Gamma(\Theta_t - \varepsilon\xi_t)\}. \quad (4.100)$$
```

用 $a_t(\Theta_t, \xi_t)$ 表示 (4.100) 的右侧，我们发现只要 $\nabla\Gamma$ 是 Lipschitz 的，$f$ 在其第一个变量上就是 Lipschitz 的，在这种情况下 $f(\theta, \xi) = -G\xi^T\nabla\Gamma(\theta) + O(\varepsilon)$。

(4.100) 的均值向量 $f_t$ 在探测信号稍微宽松的条件下允许相同的近似 (4.98)，此时零均值近似 (4.48a) 被舍。此外，以下全局一致性结果成立：

**命题 4.18** *假设对于函数 $\Gamma$ 和 qSGD #3 算法满足以下条件：*

- (i) 假设 QSA1。
- (ii) 探测信号满足 (48b)。
- (iii) $\Gamma$ 是强凸的，且具有唯一的最小化点 $\theta^* \in \mathbb{R}^d$。

存在 $\varepsilon > 0$，使得对于每个 $\varepsilon \in (0, \varepsilon)$，$f_\varepsilon$ 有唯一的根 $\theta_\varepsilon^*$，满足 $||\theta_\varepsilon^* - \theta^*|| \le O(\varepsilon)$。此外，对于每个初始条件都成立：$\lim_{t\to\infty}\theta_t = \theta^*$。

证明 该命题的假设意味着节 4.5 中的假设 QSA1-QSA2 适用于 $f(\theta, \xi) = -G\xi^T\nabla\Gamma(\theta) + O(\varepsilon)$ 和根据 (4.98) 定义的 $f_t$。根据 (495)，由于 $\Gamma$ 是强凸的，存在 $\varepsilon_0 > 0$，使得对于 $||z|| \le \varepsilon_0$，方程 $G\Gamma(\theta) = z$ 有唯一的解，从而对于足够小的 $\varepsilon$ 可以建立假设 QSA3。定理 4.15 意味着对于每个 $\varepsilon > 0$，$\Theta_t$ 都收敛到 $f_\varepsilon$ 的唯一根 $\theta_\varepsilon^*$，满足 $||\Gamma(\theta_\varepsilon^*)|| = O(\varepsilon)$。

