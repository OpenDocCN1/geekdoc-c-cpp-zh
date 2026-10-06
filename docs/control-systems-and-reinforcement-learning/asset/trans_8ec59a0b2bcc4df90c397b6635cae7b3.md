

# 算法设计的 ODE 方法

通用 Runge-Kutta 方法 [79, 168, 384]。更新方程更为复杂，但这种复杂性通常会被更紧密的近似所抵消。然而，请记住在本章中，我们的目标是估计一个驻点，即方程

```
f(\theta^*) = 0,
```
解 $\theta^* \in \mathbb{R}^d$，而不是精确地跟踪 ODE (4.2) 的解。对于这个相对有限的目标，执行 ODE 近似的最佳方法仍是一个开放的研究领域。

# 4.3 牛顿-Raph森 流

本节涉及 ODE 设计近似，其目标是求解求根问题 (4.10)。参数 $\theta^*$ 被视为 ODE (4.2) 的平衡条件。我们在这里面临的问题是，ODE 在任何意义上可能都是稳定的。在本节中，我们描述了一种修改动力学并确保稳定性的通用方法。

第 4.4 节涉及特殊情况下的求根问题，其中 $f = -\nabla_\Gamma f$，$\Gamma: \mathbb{R}^d \to \mathbb{R}^s$ 是某个优化问题中的损失函数。此时求根问题等同于最优的一阶条件 $\nabla_\Gamma f(\theta^*) = 0$。如果 $f$ 具有良好的性质（如凸性），使用李雅诺夫函数技术确保 (4.2) 的稳定性并不（此类结果在第 4.4 节中综述）。本节的技术可能为 (4.2) 失效的情况提供有用的应用。

我们的起点是将 $f(\theta_t)$ 视为“状态变量”，下一步是定义动力学，使得对于每个初始条件都有 $\lim_{t \to \infty} f(\theta_t) = 0$。在对 $f$ 的适和假设下，将得出 $\lim_{t \to \infty} \theta_t = \theta^*$，这是我们的设计目标。

如果 $f(\theta_t)$ 是状态变量，这意味着存在一个相关的向量场 $\mathcal{V}: \mathbb{R}^s \to \mathbb{R}^d$，

```
\frac{d}{dt}f(\theta_t) = \mathcal{V}(f(\theta_t)).
```

确保 $f(\theta_t)$ 收敛的一种方法是选择 $\mathcal{V}(f) = -f$，得到：

```
\frac{d}{dt}f(\theta_t) = -f(\theta_t).
```

解为 $f(\theta_t) = e^{-t}f(\theta_0)$，它指数级收于零。实现这些动力学将是一项了不起的成就！

其实这并不难。应用链式法则：

```
\frac{d}{dt}f(\theta_t) = A(\theta_t)\frac{d}{dt}\theta_t, \quad A(\theta_t) = \partial_\theta f(\theta_t), \quad \theta \in \mathbb{R}^d,
```

其中 $\partial_\theta f$ 表示 $d \times d$ 雅可比矩阵，其元素为

```
A_{i,j}(\theta) = \frac{\partial^2}{\partial\theta_j}f_i(\theta).
```

这意味着实现动力学 (4.11) 等价于

```
\frac{d}{dt}\theta_t = [A(\theta_t)]^{-1}\mathcal{V}(f(\theta_t)).
```

将该等式应用于特殊情况 $\mathcal{V}(f) = -f$，得到一个著名的 ODE：

# 牛顿-Raph森 流

```
$$\frac{d}{dt}\partial_t = -[A(\partial_t)]^{-1}\mathbf{f}(\partial_t). \quad (4.14a)$$
```

右侧的函数是牛顿-Raph森向量场

```
$$\mathbf{f}^{rn}(\theta) = -[A(\theta)]^{-1}\mathbf{f}(\theta). \quad (4.14b)$$
```

在大多数应用中，无法先验判断矩阵 $A(\theta) = \partial_\theta\mathbf{f}(\theta)$ 是否满秩，这促成了正则化的牛顿-Raph森流：对于固定的 $\varepsilon > 0$，

```
$$\frac{d}{dt}\partial_t = G(\partial_t)\mathbf{f}(\partial_t). \quad (4.15)$$
```

$G(\theta) \stackrel{\text{def}}{=} -[I + A(\theta)^T A(\theta^*)]^{-1}A(\theta^*)$ 是 $-A(\theta)$ 伪逆的近似。命题 4.4 证明，如果 $V = ||\mathbf{f}||^2$ 是 $\mathbb{R}^d$ 上的强制函数，则 (4.15) 的解在时间内是有界的。适的条件意味着 $V$ 作为 (4.15) 的李雅诺夫函数，

```
$$\lim_{t\to\infty} \partial_t = 0. \quad (4.16)$$
```

**命题 4.4** 考虑关于函数 $\mathbf{f}$ 的以下条件：

- (a) f 是 Lipschitz连续且连续可微的。因此 $A(\cdot)$ 是有界且连续的矩阵值函数。
- (b) $||\mathbf{f}||$ 是强制的。即对于每个 $n$，集合 $\{|\mathbf{f}|| \le n\}$ 都是界的。
- (c) 函数 $\mathbf{f}$ 有一个唯一的根 $\theta^*$，且当 $\theta \neq \theta^*$ 时，$A^T(\theta)\mathbf{f}(\theta) \neq 0$。此外矩阵 $A(\theta^*)$ 非奇异。

在逐渐增强的假设下，ODE (4.15) 解满足：

- (i) 如果 (a) 成立，对于每个 $t$ 和每个初始条件，
```
$$\frac{d}{dt}\partial_t = -A(\partial_t)[I + A(\partial_t)^T]^{-1}A^T(\partial_t). \quad (17)$$
```
- (ii) 如果额外满足 (b)
```
$$\lim_{t\to\infty} \partial_t^T\mathbf{f}(\partial_t) = 0. \quad (18)$$
```
- (iii) 如果 (a)-(c) 成立，(4.15) 是全局稳定的。

证明：(ii) 的结论源于链式法则和定义。(iii) 的结论源于李雅诺夫函数 $V(\partial_t) = \frac{1}{2}||\mathbf{f}(\partial_t)||^2$，并结合：

```
$$\frac{d}{dt}V(\partial_t) = -\mathbf{f}(\partial_t)^T A(\partial_t)[I + A(\partial_t)^T]^{-1}A^T(\partial_t)\mathbf{f}(\partial_t).$$
```

当 $\partial_t \neq \theta^*$ 时，右侧非负。对于任何 $T > 0$ 积分每一步：

```
$$V(\partial_T) = V(\partial_0) - \int_0^T \mathbf{f}(\partial_t)^T A(\partial_t)[I + A(\partial_t)^T]^{-1}A^T(\partial_t)\mathbf{f}(\partial_t)dt, \quad (19)$$
```

使得对于所有 $T$，$V(\partial_T) \le V(\partial_0)$。在强制假设下(4.15) 的解也是界的。令 $T \to \infty$，从 (19) 得到界：

```
$$\int_0^{\infty} f(\partial_t)^T A(\partial_t) (I + A(\partial_t)^T)^{-1} A^T(\partial_t)f(\partial_t) dt \le V(\partial_0).$$
```

$\partial_t$ 的有界性和 $A$ 的连续性意味着存在 $B(\partial_0) < \infty$，使得 $\int_0^{\infty} \gamma_t dt \le B(\partial_0) < \infty, \quad \gamma_t \stackrel{\text{def}}{=} \|A(\partial_t)f(\partial_t)\|_2^2$。

函数 $f$ 和 $A$ 是 Lipschitz 连续的，有界性意味着 $\gamma_t$ 满足引理 4.3 中的条件。因此 $\lim_{t\to\infty} =0$ 如所示。

接下来我们证明 (iii)。虽然根据命题 2.5，我们提供了另一个短证明的素材。(4.15) 的全局渐近稳定性要求解从每个初始条件收敛到 $\theta^*$，且 $\theta_t$ 在李雅诺夫意义上是稳定的。假设 (c) 结合 (ii) 得出 $\lim_{t\to\infty} \theta_t = \theta^*$。后者的充分条件通过考虑 $A_\theta = \nabla_\theta \Gamma(\theta)|_{\theta=\theta^*}$ 得到。如果其特征值位于 $\mathbb{C}$ 中的严格左半平面，则在李雅诺夫意义上稳定 [1, 2]。

应用定义，得到 $A_\theta = -[I+M]^{-1}M$，其中 $M = A(\theta^*)^T A(\theta^*) > 0$（记得假设 $A(\theta^*)$是非奇异的）。$A_\theta$ 的特征值与 $M$ 的特征值重合，对于每个特征值-特征向量对，我们有：

```
$A_\theta v = \lambda_A v, \quad \lambda_A = -\frac{\lambda}{\varepsilon+\lambda} < 0.$
```

这建立了 $A_\theta$ 是 Hurwitz 的。

# 4.4 优化

我们转向损失函数 $\Gamma: \mathbb{R}^d \to \mathbb{R}_+$ 的最小化，我们想要计算全局最小值：

```
$$\theta^* \in \arg\min \Gamma(\theta).$$
```

本节包含了估计 $\theta^*$ 的优化和 ODE 技术的简要综述。特别是，我们建立了最陡 ODE 收敛的条件：

```
$\frac{d\theta}{dt} = -\nabla\Gamma(\theta). \quad (4.20)$
```

这也被称为*梯度流*（gradient flow）。

记得向量 $\theta_0 \in \mathbb{R}^d$ 处的梯度 $\nabla\Gamma$ 正交于等值集 $\{\theta \in \mathbb{R}^d : \Gamma(\theta) = \Gamma(\theta_0)\}$，如图 4.1 所示。对于给定的时间 $t_0$，记 $\theta_0 = \theta_{t_0}, r_0 = \Gamma(\theta_0)$，并根据 (2.28) 回想等值集的定义为

```
$S_\Gamma(r_0) = \{\theta \in \mathbb{R}^d : \Gamma(\theta) \le r_0\}.
```

如果 $\theta_0$ 处的梯度不零，在所示所示，梯度流驱动解进入该集合内部：$\Gamma(\theta_t) < r_0$ 对于所有 $t > t_0$。特别是，每个下值集都是**吸收的**（absorbing）；一旦梯度流的解进入集合 $S_\Gamma(r_0)$，它永远不会离开。

