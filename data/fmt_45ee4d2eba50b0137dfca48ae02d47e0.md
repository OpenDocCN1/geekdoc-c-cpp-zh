
且 $\mathcal{D}_{n+1}$ 定义如 (5.48)。![](img/0790f102da4ffa7564329bf76c7d0815_198_0.png) 图 5.5 Baird 的问题。

## 价值函数近似

这是 (5.48) 的推广，如果 $\mathcal{H}$ 是 $d$ 维函数类 $\zeta_n^0 = \psi(n)$。

### 完美探索下的不稳定动态

图 5.5 展示了 Baird 的反例，这是一个使用 TD($\lambda$) 的不稳定示例。有六个状态且没有控制，对于所有 $k \ge 1$，状态保持 $x(k)=7$。对于每个 $x$，$Q^*(x,u)=h^*(x)=0$。注意 $\theta'$ 表示 $\theta$ 的第 $i$ 个索引。该例子违反了本章两个约定：

- (i) $\psi(x) = (0, \dots, 2)^T = 0$ 在 $x^*=7$ 时被违反。
- (ii) 如果只有状态，则基是至关重要的。这意味着对于任何值 $N$，样本矩阵 (5.19) 都不是满秩。

退化矩阵不是问题，因为 $h^0 = h^*$ 且对于所有 $\theta^0=0$ 的 $n$，$\mathcal{D}_{n+1}^0 = 0$。秩缺陷意味着 $\theta'$ 不是唯一的。

该例子是在折扣设置下引入的，折扣因子 $\gamma \le 1$。在这里保持，并且由于没有控制，我们使用价值函数定义时间差：

```
$\mathcal{D}_{n+1}^0 = -h^0(n) + \gamma h(n+1) = -h^0(n) + \gamma h(7),$
```

后者等式由于平凡定义而成立。在折扣设置下，资格方法的定义略微修改：

```
$\zeta_{n+1} = \lambda\zeta_n + \psi(n+1).$$
```

完美探索基于重启的版本，每个回合允许一次转移，并均匀采样七个状态。周期性实现描述如下：对于 $n=0, 1, \dots, 6$，选择 $x(n)=n+1$ 并得到

```
$\mathcal{D}_{n+1} = -h(n+1) + \gamma h(n).$
```

其中 $\{\theta_n\}$ 使用 TD($\lambda$) 更新；$\theta_{n+1} = \theta_n + \alpha_n\mathcal{D}_{n+1}\zeta_n$。此过程重复使得 $x(n)-1 \equiv n \pmod 7$，对于所有 $n \ge 1$。

该算法在 $\gamma \le 1$ 足够大且某些初始条件下收敛（在假设 $\sum \alpha_n = \infty$ 下）。为了看到这一点，仔细看差异：

```
$\mathcal{D}_{n+1} = \begin{cases} -[\theta_n^0 + 2\theta_n^1] + \gamma[2\theta_n^0 + \theta_n^1] & x(n)=k \le 6 \\ -[\theta_n^0 + \theta_n^1] + \gamma[2\theta_n^0 + \theta_n^1] & x(n)=7 \end{cases}$
```

通过观察六个参数的最后一个揭示了不稳定性源：

```
$\theta_{n+1}^0 = \theta_n^0 + \begin{cases} \alpha_{n+1}\{(2-1)\theta_n^0 + \gamma\theta_n^0 - 2\theta_n^1\}\zeta_n^0 & x(n)=k \le 6 \\ \alpha_{n+1}\{(1-\gamma)[2\theta_n^0 + \theta_n^1]\}\zeta_n^0 & x(n)=7 \end{cases}$
```

假设 $\gamma > \frac{1}{2}$ 且 $\theta_0^0 > 0$ 相对其他参数较大。每当 $x(n)\le 6$ 时，由于正系数 $(2\gamma-1)$，估计 $\theta_{n+1}^0$ 倾向于增加。

## 5.4 投影贝尔曼方程与 TD 算法

![](/0790f102da4ffa7564329bf76c7d0815_198_0.png)

![](img/0790f102da4ffa7564329bf76c7d0815_198_1.png)

![](img/0790f102da4ffa7564329bf76c7d0815_198_2.png)

![](img/0790f102da4ffa7564329bf76c7d0815_198_3.png)

![](img/0790f102da4ffa7564329bf76c7d0815_198_4.png)

在本节的剩余部分中，我们转向 $Q^*$ 的近似，即与最优控制问题相关的 Q 函数。

### 5.4.3 投影 Bellman 算子与 Q-Learning

总最优控制问题的 Q 函数满足固定点方程 (3.7d)，为了方便起见，复制如下：

```
$Q^*(x,u) = c(x,u) + Q^*(F(x,u)),$
```

其中对于任意 $Q$，有 $Q(x) = \min_u Q(x,u)$。对于参数化近似族 $\{Q^\theta : \theta \in \mathbb{R}^d\}$，记得对于每个 $\theta$，我们根据 (3.44) 定义了一个策略：

```
$\phi^\theta(x) = \arg \min_u Q^\theta(x,u), \quad x \in X.$
```

我们通过 (5.48) 的“模式匹配”获得了一种近似算法。这里给出了带有线性函数近似的算法：

## Q($\lambda$) 学习

对于给定的 $\lambda \in [0,1]$、非负步长序列 $\{\alpha_n\}$、初始条件 $\theta_0, \zeta_0$ 以及观测样本 $u(k,x) : 0 \leq k \leq N$，估计序列由以下方程定义：

```
$$\theta_{n+1} = \theta_n + \alpha_n \mathcal{D}_n \zeta_n, \quad (5.52a)$$
$$\zeta_{n+1} = \lambda \zeta_n + \psi_{(n+1)}, \quad (5.52b)$$
```

```
$$\mathcal{D}_n = -Q^\theta(x(n),u(n)) + c_n + Q^\theta(x(n+1),\phi^\theta(x(n+1))), \quad (5.52c)$$
```

其中 $\psi(n+1) = \psi(x(n+1),u(n+1))$，$c_n = c(x(n),u(n))$。

该算法与 TD 学习有显著的相似与不同之处：

- 变化在 (5.52c) 中：它使用了当前策略估计 $\phi^\theta$，而不是 TD($\lambda$) 中的固定策略 $\phi$。注意在 (5.52c) 中我们可以替换为

```
$Q^\theta(x(n+1)),\phi^\theta(x(n+1)) \overset{def}{=} Q^\theta(x(n+1))$
```

- QSA 理论预测 Q($\lambda$) 学习中的目标 $\theta^*$ 将满足 $f(\theta^*) = 0$，其中：

```
$f(\theta) = E_\theta [f_{n+1}(\theta)], \quad f_{n+1}(\theta) = \mathcal{D}_n Q^\theta \zeta_n. \quad (5.53)$
```

这看起来像 TD($\lambda$)，直到你意识到从 (5.52c) 得到的 $\mathcal{D}_n(Q^{\theta^*})$ 有不同的定义：

```
$$\mathcal{D}_n(Q^{\theta^*}) = -Q^{\theta^*}(x(n),u(n)) + c_n + Q^{\theta^*}(x(n+1),u).$$
```

- 对于 $\lambda = 0$ 的特殊情况，我们可以应用命题 5.6 得出 $Q^{\theta^*}$ 解决了投影 Bellman 方程：

```
$Q^{\theta^*} = P_h\{T(Q^{\theta^*})\}$
```

其中 Bellman 算子被重新定义为：$T(Q)|_{(x,u)} = c(x,u) + Q(F(x,u))$。

## 5.4 投影 Bellman 方程与 TD 算法

遗憾的是，这些观察让我们陷入了死胡同。Q($\lambda$)-learning 的 ODE 分析要求我们考虑由 (5.53) 定义的 ODE 的全局渐近稳定性。首先，我们必须找到寻根问题允许解的条件！不幸的是，即使在 $\lambda=0$ 的情况下，关于存在性也知之甚少。而且，如果存在平衡点，稳定性几乎是无效的。

## 5.4.4 GQ-学习

如果我们担心 $f({\theta^*}) = 0$ 不存在解，我们可能会转向次优方案：对于给定的 $d \times d$ 矩阵 $M > 0$，

```
$$\min \Gamma(\theta) = \min_{\theta} \frac{1}{2}f(\theta)^\top M f(\theta).$$
```

我们可以使用 ODE 方法来设计算法。一种方法是梯度下降：

```
$$\frac{d}{dt}\theta_t = -[\partial_{\theta} f(\theta_t)]^\top M f(\theta_t).$$
```

[234] 中的 GQ-learning 算法可以视为此 ODE 的离散时间翻译，使用 $M = E[\zeta_n\zeta_n^\top]$。通过双尺度算法避免了矩阵求逆：使用“高增益” ODE 的解获得 $Mf(\theta_t)$ 的 ODE 近似，

```
$$\frac{d}{dt}\omega_t = b_t[f(\theta_t) - R\omega_t],$$
```

其中 $R = M^{-1}$。只要 $\{b_t\}$ 取得很大且 $\{\theta_t\}$ 有界，那么要建立近似 $\omega_t \approx Mf(\theta_t)$ 在过渡期后成立并不困难。

这些 ODE 是双尺度 GQ 算法原生的，这里给出线性函数近似的形式：

## GQ($\lambda$) 学习

与 Q($\lambda$) 学习具有相同的起点，并增加了一个初始化 $\omega_0 \in \mathbb{R}^d$。

```
$$\theta_{n+1} = \theta_n - \alpha_{n+1}\Lambda_n^\top \omega_n, \quad (5.56a)$$
$$\omega_{n+1} = \omega_n + \beta_{n+1}\{f_{n+1}(\theta_n) - \zeta_n + \zeta_{n+1}^\top \omega_n\}, \quad (5.56b)$$
```

```
$$\zeta_{n+1} = \lambda\zeta_n + \psi_{(n+1)},$$
$$\mathcal{D}_{n+1} = -Q^{\theta_n}(x(n), u(n)) + c_n + Q^{\theta_n}(x(n+1)),$$
$$f_{n+1}(\theta_n) = D_{n+1}\zeta_n, \quad A_{n+1} = \partial_{\theta_n}f(\theta_1) = \zeta_n\{\psi_{(n)} + \psi_{(n+1)}^\top\}^\top \quad (5.56c)$$
```

其中 $\psi_{(n+1)} = \psi(x(n+1), u(n+1))$，而 $\psi_{(n+1)} = \psi(x(n+1), \phi^{\theta n}(x(n+1)))$

## 值函数近似

始终，算法的输出定义了最终近似 $Q^{\theta^*}$。只要第二步序列尺寸足够大，ODE 近似就是成功的：

```
$$\lim_{n\to\infty} \frac{\beta_n}{\alpha_n} = \infty.$$
```

存在几个挑战和问题：

- 我们可能很难获得 (5.54) 的全局最小值，目标函数 $\Gamma$ 不是凸的。
- 假设 $\hat{f}(\theta^*)=0$ 不存在解。Nesterov 警告说这可能导致不稳定。

## 价值函数近似

$\theta_{n+1} = \theta_n + \alpha_{n+1} \frac{1}{r_n} \sum_{k=T_n}^{T_{n+1}-1} [-Q^{\theta_n}(x, u(k)) + \gamma_n(k) + \mathcal{E}_{n+1}] \nabla_\theta Q^{\theta_n}(x, u(k)),$

其中 $|\mathcal{E}_{n+1}\| \leq O(\alpha_{n+1})$。这促使了相对于 DQN 的 Batch QSA 近似：

## Batch Q(0) 学习

给定 $\theta_0 \in \mathbb{R}^d$，以及一组正标量序列 $\{\alpha_n\}$，递归定义。

```
$\theta_{n+1} = \theta_n + \alpha_{n+1} \frac{1}{r_n} \sum_{k=T_n}^{T_{n+1}-1} \mathcal{D}_{k+1}(\theta_n) \nabla_\theta Q^{\theta_n}(x, u(k)), \quad (5.61)$
$\mathcal{D}_{k+1}(\theta_n) = -Q^{\theta_n}(x, u(k)) + c_k + Q^{\theta_n}(x(k+1)).$
```

虽然 DQN 易于实现，但它并没有解决围绕 Q($\lambda$)-学习的这些：

**命题 5.10** 考虑可能带有非线性函数近似的 DQN 算法。假设 $Q$ 是连续可微的，其梯度 $\nabla_\theta Q^{\theta}(x,u)$ 是全局 Lipschitz 连续的，且 Lipschitz 常数独立于 $(x,u)$。假设 $B = \infty$，非负步长序列满足：

- $\sum \alpha_n = \infty$ （等待，可能可能是 $\sum \alpha_n = \infty$）
- $\sum \alpha_n^2 < \infty$

并且假设由 DQN 算法定义的序列 $\{\theta_n\}$ 收敛于 $\theta_{\infty} \in \mathbb{R}^d$。那么

- (i) $\dot{(\theta_n)} = 0$，其中 $f$ 通过 (5.53) 定义，使用 $\zeta_n = (\nabla_\theta Q^{\theta}(x,u))_{\theta=\theta_n}$
- (ii) 该算法允许 ODE 近似 $\frac{d\theta}{dt} = f(\theta)$。

这些结论可能会引起警示，因为我们不知道 (5.53) 中定义的 $f$ 是否有根。如果我们设法建立 $f(\theta_*)=0$ 解的存在，我们仍然不知道 ODE 是否稳定，或者 $\theta_{\infty}$ 是否具有良好的性质。

另一方面，DQN 每天都被成功使用，因此不应被忽视。

# 5.5 凸 Q 学习

我们调查了“TD 分类法”中的三类算法：

- (i) 使用 LSTD 或 TD 的近似 PIA。在两个条件下我们可以确保成功：(a) 函数类是线性的，(b) 函数类在意义上是完备的，即我们可以确保对于每个 $n$，$Q^{\phi n} = Q^{\phi}$。
- (ii) GQ 学习以最小均方 Bellman 误差。如果 $Q^*$ 位于我们的函数类中，且梯度下降满足目标条件（如第 4.4.2 节引入的 PL 条件），我们确保成功。
- (iii) 使用 Q($\lambda$) 学习、DQN 或 Batch Q(0) 学习保留 ODE 方程的松弛。这里的理论几乎不存在。

# 5.5 凸 Q 学习

本节调查的 RL 算法均受 DPLP(3.36) 的启发。我们从一种基于联合参数化的直接方法开始：在 5.1 节的符号中，$\mathcal{H} = \{h^\theta = (J^\theta, Q^\theta): \theta \in \mathbb{R}^d\}$。值 $\theta_i$ 可能代表神经函数近似架构中的第 $i$ 个权重，但为了证明“凸”这个形容词，我们需要线性参数化的族：

```
$J^\theta(x) = \theta^T \psi^j(x), \quad Q^\theta(x, u) = \theta^T \psi(x, u).$
```

函数类经过归一化，使得对于每个 $\theta$，$J^\theta(x) = 0$。对于线性架构，这要求对于每个 $1 \leq i \leq d$，$\psi^i(x) = 0$；对于神经架构，归一化通过网络的输出施加。基于 RKHS 的凸 Q 学习算法在 5.5.2 节中描述。考虑基于参数化族的 (3.36) 翻译：

```
\max_{\theta} \langle \mu, Q^\theta \rangle \text{s.t.} \quad Q^\theta(x, u) \leq c(x, u) + J^\theta(x, u),
Q^\theta(x, u) \geq J^\theta(x), \quad x \in X, u \in U. (5.62)
```
