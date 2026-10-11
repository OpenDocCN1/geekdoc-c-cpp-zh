
$\Lambda^\theta(x,u) = \nabla_\theta \log^\Phi(u \mid \theta). \quad (10.38)$

特别，我们有

$\nabla_\theta c_\theta(x) = \sum_u \Phi^\theta(u \mid x) \Lambda^\theta(x,u)c(x,u), \quad (10.39)$

$\nabla_\theta P_\theta(x,x') = \sum_u \Phi^\theta(u \mid x) \Lambda^\theta(x,x'), \quad x,x' \in X, \theta \in \mathbb{R}^d$。

或许是 $\Lambda^0$ 是 $Z$ 上转移矩阵的得分函数（score function）：

$\Lambda^0(z,z') = \nabla_z T_\theta(z,z'), \quad z,z' \in Z. \quad (10.40)$

演员-评论（actor-critic）方法之所以出现在这里平均成本的 TD(1) 学习之后，是因为定理 6.8 中的敏感性公式可以用固定的 Q 函数来表示。对于任意 $\theta$，

$Q_\theta(x,u) \overset{\text{def}}{=} c(x) + P_\theta h_\theta(x) = c(x,u) + \sum_{x' \in X} P_\theta(x,x')h_\theta(x'), \quad x \in X, u \in U, \quad (10.41)$

其中 $h_\theta$ 遵循泊松方程，即 $P_\theta h_\theta = h_\theta + \Gamma(\theta)$。

**定理 10.16** *在本节的假设下，对于每个 $\theta \in \mathbb{R}^d$，*

$\Gamma(\theta) = E_{\Phi}[\Lambda^\theta(\Phi(k))Q_\theta(\Phi(k))]. \quad (10.42)$

$E[Q_\theta(\Phi(k+1)) \mid \Phi(k)] = \sum_{x'} \sum_{u'} P_\theta(x,x') \Phi^\theta(u \mid x') \{c(x',u) + P_\theta h_\theta(x')\}$

$= \sum_{x'} P_\theta(x,x') \{c_\theta(x') + P_\theta h_\theta(x')\}$

$= \sum_{x'} P_\theta(x,x')[b_\theta(x') + \Gamma(\theta)] = Q_\theta(x,u) - c(x,u) - \Gamma(\theta)$。

用矩阵符号表示，这是 $T_\theta Q_\theta = Q_\theta - c + \Gamma(\theta)$。

这结合 (10.40) 和定理 6.8 完成了证明。

该定理引发了许多问题：

- (i) 如何将其用于优化？随机逼近是一个选项：

$\theta_{n+1} = \theta_n - \alpha_{n+1}\Gamma(\theta_n), \quad \hat{\Gamma}_n = \Lambda^\theta(\Phi(n))Q_{\theta_n}(\Phi(n))$。

这是随机梯度下降 (SGD) 的版本。由于我们构建了策略，$\Lambda^0$ 是已知的。Q 函数是未知的，糟糕的估计意味着对 $\theta^0$ 的近似很差。

- (ii) 即使 $Q_\theta$ 是已知的，随机逼近算法预计会有很大的方差。如何减少方差？

这些问题得到了逐一解答，并证明了新的结论和算法。每个算法需要两个函数类：一个定义随机策略族 $\{\phi : 0 \in \mathbb{R}^d\}$，第二个函数类 $\{\mathcal{H}^\theta : 0 \in \mathbb{R}^d\}$ 用于定义 Q 函数的近似。施加以下假设使得本节的 $L_2$ 理论成立：

### 演员-评论基础 (Actor-Critic Basis)

假设 $\{\mathcal{H}^\theta : 0 \in \mathbb{R}^d\}$ 采用线性参数化，维度固定为 $d'$。基函数可能依赖于 $\theta$，因此 $\mathcal{H}^\theta$ 中的通用函数可以为：

$H_\theta^\omega = \omega^\top \psi_\theta, \quad \omega \in \mathbb{R}^d, \quad \theta \in \mathbb{R}^d. \quad (10.43)$

假设 $\psi_\theta$ 在 $\theta$ 上是连续可微且 Lipschitz 连续的。

我们很快会看到 $d' \geq d$ 通常是理想。

### 演员-评论算法 (Actor-Critic Algorithm)

对于初始化 $\theta_0 \in \mathbb{R}^d$ 和 $\omega_0, \zeta_0 \in \mathbb{R}^d$，

$\theta_{n+1} = \theta_n - \alpha_n + \frac{1}{\sqrt{r(n)}}, \quad \tilde{R}(n) = \Lambda^{\theta_n}(\Phi(n))H^{\omega_n}_{\theta_n}(\Phi(n)), \quad (10.44a)$

$\Phi(n+1) \sim T_{\theta_n}(z, \cdot), \quad z = \Phi(n), \quad (10.44b)$

$\mathcal{D}_{n+1} = \{-H^{\omega_n}_{\theta_n}(\Phi(n)) + \tilde{C}_n + \mathbb{I}_{\{\Phi(n+1) \neq z'\}}H^{\omega_n}_{\theta_n}(z') \mid \theta = \theta_n\}$

$\omega_{n+1} = \omega_n + \beta_n \zeta_n$

$\zeta_{n+1} = \lambda \mathbb{I}_{\{\Phi(n+1) \neq z'\}}\zeta_n + \psi_{n+1}(\Phi(n+1))$

$\eta_{n+1} = \eta_n + \beta_n + \tilde{c}_n - \eta_n, \quad (10.44c)$

(10.44) 中的方程组基于 TD(1) 算法 (10.28)(设置 $\lambda=1$）。这种版本的 TD(1) 相比 (10.32) 具有更好的稳定性。该算法有两个步长，满足：

$\sum_{n=1}^\infty \alpha_n = \infty, \quad \sum_{n=1}^\infty \beta_n = \infty, \quad \sum_{n=1}^\infty (\alpha_n^2 + \beta_n^2) < \infty$。

认为后者远大于前者，因此 $H^{\omega_n}_{\theta_n}$ 可以跟踪固定策略 Q 函数 $Q_\theta$（对应策略 $\phi^*_\theta$）。

双尺度 SA 理论预期将得出：

**命题 10.17** 假设 $\lambda =1$ 且步长序列满足假设 (8.22)。

$\lim_{n\to\infty} \frac{\beta_n}{\alpha_n} = \infty.$

### 收集演员 (Gather the Actors)

假设参数估计是有界的，并且满足以下一致性条件：对于每个 $\theta \in \mathbb{R}^d$，存在 $w \in \mathbb{R}^d$ 满足 $\Lambda^w = Q$ (10.45)。

那么 (10.44) 的 ODE 近似是梯度下降 $\dot{\theta} = -\Gamma(\theta)$。$\square$

一致性假设 (10.45) 在表格环境下是不现实的。通过应用定理 10.14 可以移除该假设——详见第 10.6 节。

### 10.5.2 若干警告与补救 (A Few Warnings and Remedies)

是时候谈谈随机化了，这在第 4.6 和 4.7 节中是未要求的。如果我们想应用马尔可夫链的敏感性理论，就需要随机化，这引入了函数 $S^\theta$ 和 $\Lambda^\theta$。特别是对于确定性策略（如 4.1 节中的山路车），$\Lambda^\theta$ 没有意义的定义。$^1$ 在大多数应用中，在策略设计的最后放弃随机化是合理的：一旦我们有了参数估计 $\theta \approx \theta^*$，构造一个确定性策略：

$\Phi^{\tilde{\theta}}(x) = \arg\max_u \tilde{\theta}(u|x), x \in X.$。我们预期如果是最优，它是近确定性的，在这种情况下 $\Phi^{\text{final}}$ 是 $\Phi$ 的某种扰扰。

**示例 10.5.1（最佳参数可能是 $\infty$）** 考虑 $d=1$ 的完全理想设置，$\theta$ 在 Gibbs 策略 (9.66a) 中扮演“反温度”的角色：

$\Phi(u|x) = \frac{\exp(-\theta H(x,u))}{\kappa(x,\theta)}$

其中 $H: X \times X \to \mathbb{R}$，$\kappa(x,\theta)$ 是归一化常数。假设我们很幸运从 $H$ 可以得到最优策略：

$\Phi^*(x) = \arg\max_u H(x,u), x \in X.$ 且 $\Phi^*$ 是唯一的（只有一个最优策略）。结论如下：

- (i) $\Phi$ 不是任何 $\theta$ 的最优策略，且 (ii) $\lim_{\theta \to \infty} \Phi = \Phi^*$。这个示例似乎是人为设计的，但 Gibbs 策略将在后续章节出现，我们将在第 10.6 节看到，在 Gibbs 策略中包含 Q 函数近似是有充分理由的。示例表明良好的算法必须允许 $\theta_n$ 收敛到 $\infty$。这可能不实际，因此引入正则化：选择一个凸正则项。

$^1$ 见 [323]确定性策略演员-评论方法的另一种公式。

### 舞台搭建，演员的返回 (Setting the Stage, Return of the Actors)

$\theta_{n+1} = \theta_n - \alpha_n + \frac{1}{\sqrt{r(n)}}, \quad \tilde{R}(n) = \Lambda^{\theta_n}(\Phi(n))H^{\omega_n}_{\theta_n}(\Phi(n)), \quad (10.44a)$

$\Phi(n+1) \sim T_{\theta_n}(z, \cdot), \quad z = \Phi(n), \quad (10.44b)$

$\mathcal{D}_{n+1} = \{-H^{\omega_n}_{\theta_n}(\Phi(n)) + \tilde{C}_n + \mathbb{I}_{\{\Phi(n+1) \neq z'\}}H^{\omega_n}_{\theta_n}(z') \mid \theta = \theta_n\}$

$\omega_{n+1} = \omega_n + \beta_n \zeta_n$

$\zeta_{n+1} = \lambda \mathbb{I}_{\{\Phi(n+1) \neq z'\}}\zeta_n + \psi_{n+1}(\Phi(n+1))$

$\eta_{n+1} = \eta_n + \beta_n + \tilde{c}_n - \eta_n, \quad (10.44c)$

(10.44) 中的方程组基于 TD(1) 算法 (10.28)(设置 $\lambda=1$）。这种版本的 TD(1) 相比 (10.32) 具有更好的稳定性。该算法有两个步长，满足标准假设：

$\sum_{n=1}^\infty \alpha_n = \infty, \quad \sum_{n=1}^\infty \beta_n = \infty, \quad \sum_{n=1}^\infty (\alpha_n^2 + \beta_n^2) < \infty$。认为后者远大于前者，因此 $H^{\omega_n}_{\theta_n}$ 可以跟踪固定策略 Q 函数 $Q_\theta$（对应策略 $\phi^*_\theta$）。双尺度 SA 理论预期将得出：

**命题 10.17** 假设 $\lambda =1$ 且步长序列满足假设 (8.22)。

$\lim_{n\to\infty} \frac{\beta_n}{\alpha_n} = \infty.$

## 10.6 无偏 SGD (SGD without Bias)

命题 10.17 中的 ODE 近似可以在比 (10.45) 更弱的假设下获得。如果 Q 函数候选函数类 $\{\mathcal{H}^\theta:\theta \in \mathbb{R}^d\}$ 满足兼容特征属性（CFP），则

$\Lambda_i^\theta = \theta \quad$ 对于每个 $\theta \in \mathbb{R}^d$ 且 $1 \le i \le d. \quad (10.47)$

**命题 10.18** 假设 $\{\mathcal{H}^\theta : \theta \in \mathbb{R}^d\}$ 满足 CFP (10.47)。给定 $\theta \in \mathbb{R}^d$，令 $Q$ 为最小范数解：

$\tilde{Q} = \arg\min ||H - Q_0\|_\theta^2 : H \in \mathcal{H}^\theta.$。

那么，

$\Gamma(\theta) = E_{\theta}[\Lambda^\theta(\Phi(k))Q(\Phi(k))] = E_{\theta}[\Lambda^\theta(\Phi(k))\Phi(k))]. \quad (10.48)$

证明 $L_2$ 局部性等价于正交性：

$0 = E_{\theta}[[Q(\Phi(k)) - \tilde{Q}(\Phi(k))]H(\Phi(k))], \quad$ 对于所有 $H \in \mathcal{H}^\theta$。等式 (10.48) 是通过对每个 $i$ 设置 $\theta = \Lambda^\theta$ 得到的。该假设并没有限制性。在实践中，我们可能从一个函数类 $\mathcal{H}^\theta$ 开始，并对每个 $\theta$ 定义

$\mathcal{H}^\theta = \{h = h^0 + \sum_{i=1}^d \omega_i\Lambda_i^\theta : h^0 \in \mathcal{H}^\theta, \omega \in \mathbb{R}^d\}. \quad (10.49)$

## 10.6 无偏置的 SGD

我们忽略 $\Lambda^\theta_-$ 中任何不依赖于 $u$ 的部分。令 $\mathcal{F}_k^-$ 表示到时间 $k$ 之前的部分历史：

```
$$\mathcal{F}_k=\{X(k), \Phi(i) : 0 \leq i \leq k-1\}$$
```

这是到 $k$ 为止的历史，只是丢除了 $U(k)$。

**引理 10.20** *对于 $X(0)$ 的任何初始分布，$E[\Lambda^\theta(\Phi(k)) | \mathcal{F}_k] = 0$。因此，*

- (i) $\Lambda^\theta(\Phi(k)) : k \geq 0$ 是一个鞅差分序列。

- (ii) 对于任何函数 $g: X \to \mathbb{R}$，

```
$0 = E[g(X(k))\Lambda^\theta(\Phi(k))].$
```

*证明* 根据定义，对于 $X$ 中的任意 $k$ 和 $x$，有：

```
$E[\Lambda^\theta(\Phi(k)) | \mathcal{F}_k : X(k) = x] = \sum_{u} \Lambda^\theta(x,u)\phi^\theta(u | x).$
```

给定定义 $\Lambda^\theta(x,u) = \nabla_\theta\phi^\theta (u | x)/\phi^\theta (u | x)$，得：

```
$E[\Lambda^\theta(\Phi(k)) | \mathcal{F}_k : X(k) = x] = \sum_{u} \nabla_\theta\phi^\theta (u | x) = \nabla_\theta\sum_{u} \phi^\theta (u | x) = 0,$
```

最后一个等式成立是因为对于每个 $x$，$\phi^\theta(\cdot | x)$ 都是 $U$ 的概率质量函数。条件期望的平滑性质给出：

```
$E[g(X(k))\Lambda^\theta(\Phi(k))] = E[g(X(k))\Lambda^\theta(X(k),U(k)) | \mathcal{F}_k] = 0.$
```

引理 10.20 意味着我们可以放宽条件特征的定义如下：对于每个 $\theta \in \mathbb{R}^d$ 和 $1 \leq i \leq d$，存在函数 $G^\theta: X \to \mathbb{R}$ 使得：

```
$$\Lambda^\theta - G^\theta \in \mathcal{H}^\theta.$$
```

Gibbs 策略考虑每个策略 $\theta$ 

给定一个 $d$ 维向量 $\psi^\theta$，对于每个策略 $\theta$ 考虑：

```
$$\phi^\theta (u | x) = \frac{1}{\kappa(\theta,x)} \exp(\theta^T\psi^\theta(x,u)).$$
```
