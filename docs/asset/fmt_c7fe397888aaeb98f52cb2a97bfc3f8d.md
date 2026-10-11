
```
$$\Sigma_0^G A^{-1}\Sigma_\Delta(A^{-1})^\top \quad (8.30)$$
```

这是最优的，因为差值 `$\Sigma_0^G - \Sigma_0^*$` 是正定的。

特殊情况见命题 8.10，资源请参见“注释”部分。当今强化学习文献的重点完全不同：计算形式如下的有限时间误差界

```
$$P\{\|\theta_n - \theta^*\| > \varepsilon\} \leq \exp(-nI(\varepsilon)), \quad n \geq 1, \quad (8.31)$$
```

其中 `$\bar{b}$` 是常数，且对于 `$\varepsilon > 0$` 有 `I(\varepsilon) > 0`。该界通常是反过来的：对于给定的 `$\delta > 0$`，定义：

```
$$\pi(\varepsilon, \delta) = \frac{1}{I(\varepsilon)}[\log(\delta) + \log(\delta^{-1})]. \quad (8.32)$$
```

(8.31) 样本复杂度界：对于所有 `n \geq \pi(\varepsilon, \delta)`，`P\{\|\theta_n - \theta^*\| > \varepsilon\}`。

有限 `n` 界的值价值连城：只要我们等待算法迭代 `n \geq \pi(\varepsilon, \delta)` 次，就能确保误差概率低于期望值。但也存在重重挑战：

- (1) 复杂的界通常是保守的。如果界非常松，那么我们不愿意等待 `n` 超过高估值 `\tilde{n}`。

- (2) `\tilde{n}` 可能无法提供改进算法的指导。

参数估计收敛的对应项并不是挑战：

关于误差指标 `\|\theta_n\|` 的任何界（基于 (8.31) 或误差方差界）还有第三点批评：这可能不是我们所关心的！在强化学习语境下，最有价值的指标应该是与参数估计相关的策略性能的衡量，正如在 7.8 节综述的多老虎机理论中提到的。幸运的是，参数估计的中心极限定理（CLT）可能意味着更相关统计量的近似，例如平均成本。在这种情况下，我们可以借鉴仿真理论中的技术来获得时间的近似界。

## 8.2.6 渐近性能与瞬态性能

与第 4.9 节中的 QSA 问题一样，步长的选择存在权衡：至关重要的是：虽然 `$\alpha_n = g/n$` 通常会产生最优收敛率 (8.8)（最关键的是选择了足够大的 `g > 0`），但可能导致导致糟糕的瞬态行为。

请回顾第 8.2.2 节和第 4.5.4 节的摘要，以想起 SA 和 QSA 的收敛理论与 `$\theta_t$` 的比较等同于 ODE (8.4a) 的时间缩放，回想 (8.16) 和 (8.17)。该时间缩放界很容易获得：

```
$\tau_n^- \le \tau_n \le \tau_n^+$
```

其中当 `$\rho < 1$` 时，`$\tau_n = \frac{\log(n+1)}{\frac{1}{\rho}[(n+1)^{1-\rho}-1]}$`；当 `$\rho < 1$` 时，`$\tau_n^+=\frac{1+\log(n)}{\frac{1}{1-\rho}[n^{1-\rho}-1]}$`。

证明：对于任何 `t \ge 0`，以下不等式均成立：

```
$t+1 \le \frac{1}{t} \le \frac{1}{[t+1]} \le \frac{1}{\max(1,t)}$
```

其中 `[t+1]` 是 `t+1` 的整数部分；特别是，当 `0 \le t < 1` 时，`t+1] = 1`。该引理源于这些不等式，结合积分表示：

```
$\tau_n = \int_0^n (\frac{1}{[t+1]})^\rho dt.$
```

让我们回顾 (8.19) 中得到的一致收敛性，这是引理的动机。假设 ODE 指数级快速收敛到最优参数：存在 `$\theta_0 > 0$`

```
$\|\theta_{t_0+t} - \theta^*\| \le B_0 \|\theta_0 - \theta^*\| \exp(-\rho t). (8.33)$
```

为了应用 (8.19)，我们设置 `t_0 = \tau_n`，从而使得 `$\theta^{(\tau_n)} = \theta_n$`，并在 `$\alpha_n = g/n$` 时选择 `t_0+t = n+k`。如果 (8.19) 对于很大范围的 `k \ge 1`：

```
$\|\theta_{n+k} - \theta^*\| \ge \|\theta_{\tau_n+k}^* - \theta^*\| \le B_0 \|\theta_0 - \theta^*\| \exp(-\rho \rho_0 g) (\log(n+k) - 1 - \log(n)) = B_0 \|\theta_0 - \theta^*\| \exp(-\rho \rho_0 g) (\frac{n}{n+k}) (8.34)$
```

如果 `$\rho_0 g$` 不足够大，`$\theta^{(\tau_n)}_{n+k}$` 收敛到 `$\theta^*$` 的速度非常慢。在这种情况下，担心参数估计的方差没有意义：我们应该担心的是瞬态行为。

# 随机近似

引理 8.4 告诉我们 `$\rho < 1$` 会导致更快的收敛：

```
$$\theta_{n+1} = \theta_n + \frac{g}{n+1}[c(\Phi(n+1)) - \theta_n] \quad (8.35)$$
```

这种 `S_n/n` 表示为蒙特卡洛平均 (8.37) 的方式表明，由于 `S_0 = 0`。`$\square$`

# 294 随机近似

![](img/0790f102da4ffa7564329bf76c7d0815_311_0.png)

**图 8.3** 尺度递归的蒙特卡洛估计 (8.36) 的渐近收敛。

## 8.3.2 随机梯度下降

假设最小化问题为 `$\theta^* = \arg \min_{\theta} \Gamma(\theta)$`，其中 `$\Gamma(\theta) = E[\tilde{\Gamma}(\theta, \Phi)]$``$\theta \in \mathbb{R}^d$`。梯度下降 ODE 定义为：

```
$\dot{\theta} = -\nabla\Gamma(\theta).$ (8.38)
```

梯度下降的近似可以通过以下方式实现：

```
$$\tilde{\theta} = -\nabla E[\tilde{\Gamma}(\theta, \Phi)] = -E[\nabla\tilde{\Gamma}(\theta, \Phi)].$$
```

在较弱条件下，导数与期望的交换是合理的。假设我们给定样本 `$\Phi = \{\Phi_n, n \geq 1\}$`，当 `n \to \infty` 时 `$\Phi_n$` 的分布收敛于 `$\Phi$`，并对于任意 `n` 和 `$\theta$`，记 `$\Gamma_n(\theta) = \tilde{\Gamma}(\theta, \Phi_n)$`。基本算法 (8.2) 产生随机梯度下降 (SGD)：

```
$$\theta_{n+1} = \theta_n - \alpha_n\nabla\Gamma_{n+1}(\theta_n).$ (8.39)
```

### 算法的稳定性

只要 `$\Gamma$` 是强凸的（回顾 4.22），命题 4.7 告诉我们 (8.38) 是指数渐近稳定的。在证明中，显示 `V(\theta) = \frac{1}{2}|\theta - \theta^*\|^2` 是 Lyapunov 函数。

```
$$\dot{V}(\theta_t) \leq -2\delta_0V(\theta_t) \leq -\delta_0|\theta - \theta^*\|^2\exp(-\delta_0t).$ (8.40)
```

因此，界界 (8.33) 在 `$\beta_0=1$` 且 `$\alpha_0=\delta_0$` 时成立。无凸性的指数渐近稳定条件可以从定理 4.9 中获得。

SA 算法的稳定性如何？一个充分条件基于 ODE@$\infty$，就像第 4.4.4 节中的确定性情况一样：对于 `$\theta \in \mathbb{R}^d$` 定义：

```
$$\Gamma^{\infty}(\theta) = \lim_{r\to\infty}\frac{1}{r}\Gamma(r\theta), \quad\nabla\Gamma^{\infty}(\theta) = \lim_{r\to\infty}\frac{1}{r}\nabla\Gamma(r\theta).$$
```

假设这些函数是有有限值的，且第一个是径向二次的，第二个是径向线性的：

```
$$\Gamma^{\infty}(s\theta) = s^2\Gamma^{\infty}(\theta), \quad\nabla\Gamma^{\infty}(s\theta) = s\nabla\Gamma^{\infty}(\theta), \quad s > 0.$$
```

如果 `$\Gamma$` 是强凸的，(4.25) 意味着下界：

```
$$\theta^T\nabla\Gamma^{\infty}(\theta) \geq \delta_0||\theta||^2, \quad\Gamma^{\infty}(\theta) \geq \frac{1}{2}\delta_0||\theta||^2.$$
```

### 8.3 示例

第一个界直接来自 (4.25) 和 `$\nabla\Gamma^{\infty}$` 的定义。第二个界由第一个以及以下条件得出：

**引理 8.6** 如果 `$\Gamma^{\infty}$` 是连续可微的，则 `$\Gamma^{\infty}(\theta) = \frac{1}{2}\theta^{\top}\nabla\Gamma^{\infty}(\theta)$`，`$\theta \in \mathbb{R}^d$`。

*证明* 可微性证明了链式法则：

```
$\Gamma^{\infty}(\theta) = \int_{0}^{1} \frac{d}{dt}\Gamma^{\infty}(t\theta) dt = \int_{0}^{1} \theta^{\top}\nabla\Gamma^{\infty}(t\theta) dt.$
```

等式遵循微积分基本定理和等式 `$\Gamma^{\infty}(0) = 0$`。ODE^{\infty}$ 定义为 `$\frac{d\theta}{dt} = -\nabla\Gamma^{\infty}(\theta)$`：

- (i) 如果 `$\Gamma^{\infty}$` 是连续的，且对于 `$\theta \neq 0$`，`$\Gamma^{\infty}(\theta) > 0$`，ODE 是全局渐近稳定的。8.7 节的理论意味着 SA 算法 (8.39) 的估计是有界的：

```
$\sup ||\theta_n|| < \infty.$
```

- (ii) 如果假设 (i) 且 ODE 是全局渐近稳定的，则估计收敛于唯一根 `$\Gamma(\theta^*) = 0$`。(8.6) 渐近收敛或其任何变体可以用线性化矩阵 `A` 来表示。对于这类算法，它是用矩阵表示的：

```
$$A_{i,j}(\theta) = \frac{\partial^2}{\partial\theta_i\partial\theta_j}\Gamma(\theta).\quad (8.41)$$
```

确保 `A(\theta^*)` 是 Hurwitz 矩阵 (2a 和 2b)，在这种情况下意味着 `$\Gamma$` 的海森矩阵是正定的：`$\nabla^2\Gamma(\theta^*) > 0$`。

### 渐近与瞬态性能之间的权衡

考虑一种情况：`$\Gamma$` 是二次的，且 `$\Gamma(\theta) = \frac{1}{2}(\theta-\theta^*)^{\top}G(\theta-\theta^*)$`，`$G>0$`（正定）。这是强凸的，`$\delta_0 = \lambda_1$` 是 `G` 的最小特征值。考虑步长 `$\alpha_n = g/n$`：

- **瞬态界**：当使用 `$\alpha_n = g/n$` 且 `g=1/\lambda_1` 时，界 (34) 的右侧随 `1/n` 衰减。

- **渐近收敛**：用于计算渐近方差的线性化矩阵为 `A=G`。增益 `g=1/\lambda_1` 将导致由于 `gA` 的所有特征值满足 `$\lambda(gA) < -1/2$`。

- **小 n 时的 ODE 保真**：我们需要 `n_0 \gg n` 以避免小 n 时的瞬态（或采用重启将参数保持在预定义区域）。

围绕 `G` 的理论促使使用 `$\alpha_n = g/n$` 并取较小的 `g` 值（例如，如果有良好的选择，`g<1`）。这种方法对参数的“调优”要求较少。我们留下了 `$\theta, g$` 和 `N_0`，通过 (10b) 获取最终估计 `$\hat{\theta}_{N_0}$`。理论和实践建议 `$\rho \leq 0.9$` 且 `g` 不大，在观察了不同初始条件的样本路径后，`N_0` 应该是明确的。或者，我们完全放弃 SA。接下来考虑 SGD 的替代方案。

## 8.3 经验风险最小化

回顾 5.1 节对经验风险最小化 (ERM) 的简要介绍。这种方法可以应用，经验风险等于经验均值：

```
$$\Gamma_N(\theta) = \frac{1}{N} \sum_{i=1}^N \Gamma_i(\theta).\quad (42)$$
```

应用 ERM 意味着我们倾向于递归算法，并通过最小化来获得 `$\hat{\theta}_N^M$`。这种方法近年来在高维优化中变得流行。

为了说明，考虑二次损失的特例 `$\Gamma_i(\theta) = \frac{1}{2}\|M_i\theta-\xi_i\|^2$`，其中矩阵 `M_i` 和向量 `$\xi_i$` 是随机的。我们定义 `$\Gamma_i(\theta) = M_i^T(M_i\theta-\xi_i)$`，因此 SA 算法定义为：

```
$$\theta_{n+1} = \theta_n - \alpha_n M_{n+1}^T(M_{n+1}\theta_n - \xi_{n+1})\quad (43)$$
```

通过应用一阶最优条件 `$\bar{\Gamma}_N(\theta) = 0$`，可以以闭形式获得 ERM 解，其中：

```
$$\bar{\Gamma}_N(\theta) = \frac{1}{N} \sum_{i=1}^N M_i^T(M_i\theta - \xi_i)$$
```

相反，证明了：

```
$$\hat{\theta}_N^M = (\sum_{i=1}^N M_i^T M_i)^{-1} \sum_{i=1}^N M_i^T \xi_i.\quad (44)$$
```

命题 8.8 显示 `$\hat{\theta}_N^M$` 与一种使用精心构造的矩阵增益的特定 SA 算法一致：

```
$$\theta_{n+1} = \theta_n - \alpha_n G_{n+1} M_{n+1}^T(M_{n+1}\theta_n - \xi_{n+1})\quad (45)$$
```

其中：

```
$$G_{n+1} = \frac{1}{n+1} \sum_{i=1}^n M_i^T M_i, \quad n \geq 0.$$
```

## 8.4 算法设计示例

本节的目的是通过一个简单的非线性示例来说明算法设计。我们最终将基于 PJR 平均法为此这种情况得到一个非常高效的算法。

SA 递归 (8.2) 中的函数定义为 `f_{n+1}(\theta) = f(\theta, \Phi(n+1))`，其中：

```
$f(\theta, \Phi) = -(\theta + 3\sin(\theta)) + 10\cos(\theta)\Phi$,
```

其中 `$\theta$` 和 `$\Phi$` 是清晰的，使得 `f: \mathbb{R}^2 \to \mathbb{R}$`。当 `$\Phi$` 均值为时，我们有：

```
$f(\theta) = E[f(\theta, \Phi)] = -(\theta + 3\sin(\theta))$.
```

图 8.4 中 `f` 的轨迹显示 `$\theta^* = 0$` 是唯一根。我们可以积分得到表示 `f = -\nabla\Gamma`。函数 `$\Gamma(\theta) = \frac{1}{2}\theta^2-3\cos(\theta)$` 也显示在图 8.4 中，我们看到它是拟凸且强制的。SA 算法是用于获取 `$\Gamma$` 最小值的随机梯度下降实例。

### 8.4.1 增益选择

对于步长选择 `$\alpha_n = g/n$`，这是该标量示例中最小化渐近方差的增益 `g=-1/A(\theta^*)`。我们有 `A(\theta) = \partial\theta f(\theta) = -(1+3\cos(\theta))`，给出 `A(\theta^*)=-4` 和 `g^*=4`。在考虑 SA 算法的瞬态性能时，我们将发现这是一个糟糕的选择。

瞬态界 (8.33) 基于形式 (8.33) 的全局指数渐近稳定，该形式通过李雅普诺夫函数获得。对于 `V(\theta) = \frac{1}{2}\theta^2`：

```
$$\frac{d}{dt}V(\theta_t) = -\partial\theta(\theta_t+3\sin(\theta_t)).$$
```

当 `$\partial\theta\neq0$` 时，右侧为负。为了获得 `V` 的界，考虑最坏情况：
