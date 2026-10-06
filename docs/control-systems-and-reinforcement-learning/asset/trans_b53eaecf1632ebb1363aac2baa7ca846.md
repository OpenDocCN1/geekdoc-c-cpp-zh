

# 值函数近似

(5.23) 中的第一个等式是通过取值 $h(\xi^0(k)) = g(\sin(2\pi\xi^0(k))) = g(\xi(k))$ 得到的。第二个等式是一个微积分练习题。

在 Lipschitz 连续函数上施加极限 (5.22) 的一致性，将简化某些分析。对于任何 $L > 0$，令：

$$\mathcal{G}_L = \{g : |g(z') - g(z)| \le L|z - z'|, \text{对于任意 } z, z' \in \mathbb{Z}\}.$$$$

**假设 ($A\ell$)** 状态空间和动作空间 $X$ 和 $U$ 是欧几里得空间的闭子集；(3.1) 中定义的 $F$、5.20) 中定义的 $\phi$ 以及 (5.21) 中的 $H$ 在它们的定义域上是连续的。存在一个大状态过程 $\Phi$，具有以下性质：

- (i) $\phi$ 演化在欧几里得空间的闭子集 $Z$ 上，且对于每个 $k$，$(x(k), u(k), \hat{\ell}(k)) = w(\Phi(k))$，其中 $w: Z \to X \times \Omega$ 是 Lipschitz 连续的。
- (ii) 存在概率测 $\mu$，使得对于任意连续函数 $g: Z \to \mathbb{R}$，每个初始条件 $\Phi(0)$ 的遍历平均 (5.22) 都存在。
- (iii) (5.22) 中的极限在 $\mathcal{G}_L$ 上是无偏的，对于 $L < \infty$：

$$\lim_{N \to \infty} \sup_{\Phi \in \mathcal{G}_L} |\hat{g}_N - \mathbb{E}_{\Phi}[g(\Phi)]| = 0. $$

实施由 (5.20) 和 (5.21) 定义的“拟随机”策略结构是为了能够期望得到遍历极限 (5.22)。请记住，这些假设对于算法的成功实现**并非本质的**。引入它们仅是为了简化分析。

# ODE 近似

与上一章一样，遍历性允许通过更简单的 ODE 近似对算法进行近似。特别是，考虑形式如下的递归：

$$\theta_{n+1} = \theta_n + \alpha_n f_{n+1}(\theta_n), \quad n \ge 0. $$

其中 $\{f_n\}$ 是接近遍历极限的函数序列：

$$f(\theta) = \lim_{N \to \infty} \frac{1}{N} \sum f_k(\theta), \quad \theta \in \mathbb{R}^d. $$

相关的 ODE 使用该向量场定义：

$$\frac{d}{dt}\theta_t = f(\theta_t). $$

ODE 近似由朴素的欧拉构造定义：时间尺度由非递减的时间点 $\tau_0=0$ 和 $\tau_n = \sum_0^n \alpha_k$（对于 $n \ge 1$）定义。对于每个 $n$，定义连续过程 $\Theta_{\tau_n} = \theta_n$，并通过分段线性插值扩展到所有 $t$。令 $[\theta_t^* : t \ge \tau_n]$ 表示 ODE (5.25) 的解，初始条件为 $\theta_{\tau_0}^* = \theta_0$。我们将证明，对于每个初始条件 $\theta_0$ 和 $N > 0$，算法 (5.25) 是一个 **ODE 近似**：

$$\lim_{n \to \infty} \sup_{\tau_n \le \tau \le \tau_{n+N}} ||\Theta_\tau - \theta_\tau^*|| = 0. $$

# 5.3 TD 学习与线性回归

![](img/0790f102da4ffa7564329bf76c7d0815_188_0.png)

图 5.4 用于求根的 ODE 近似。

如果参数序列 $\{\theta_n\}$ 是界的，那么通常通过命题 4.28 的步骤很容易建立 (5.26)。我们随后遵循定理 4.15 的证明，在当 (5.25) 全局渐近稳定时建立参数序列的收敛性。

图 5.4 来源于图 8.5，展示了 (5.24) 的一个版本，其中 $f_{n+1}(0)$ 对于每个 $n$ 都是随机的，均值等于 $f(0)$。在这种随机近似设置下，ODE 近似 (5.26) 的定义保持不变。

这三张图比较了 $\theta_t \equiv \theta_k$ 以及 $n=0$ 的 $\hat{\theta}_n$，并根据步长的选择进行区分：$\alpha_n = 1/n^p$，其中 $\rho = 1.0, 0.9, 0.8$。在每情况下，算法 (5.24) 都是针对共同的 $\{f_n\}$ 和共同的时间跨度 $1 \leq n \leq N=10^5$ 运行的。这些图之间的显著差异在于 $\rho$ 如何影响 $\tau_n$ 的范围；对于 $\rho=1$，值 $N=10^5$ 对应于 $\tau_N < 3$，而对于 $\rho=0.8$，$\tau_N > 10$。

在这个例子中，近似 $\theta_k \approx \tau_n$ 通常是紧密的。解释是初始条件：纵轴的收敛掩盖了参数估计的波动。

较大的 $\rho$ 带来的更激进收益会导致 $\{\theta_\tau\}$ 更快收敛，但在某些情况下会导致参数估计 $\{\theta_n\}$ 不可接受的波动。这些言论反映了 4.5 节概述的 QSA 理论。

# 5.3 TD 学习与线性回归

TD学习指的是近似固定策略 $\phi$ 值函数的方法。这可能是 3.2 节引入的策略改进算法的一步，该算法要求在策略改进步 (14) 中估计 $J^n$。

# 5.3.1 固定策略时间差

3.7 节的后续讨论包含了对近似策略改进改进的非正式介绍。这种方法需要估计固定策略 Q 函数以获得更新：

$$\Phi^{n+1}(x) = \arg\min_u Q_n(x),$$

4.5.3 节包含一个说明这种方法的示例。

# 值函数近似

对于任意策略 $\phi$ 及其相关的值函数 $J^\phi$，固定策略 Q 函数表示为：

$$Q^\phi(x,u) = c(x,u) + J^\phi(x)$$

在这种记法下，固定点方程 (45) 为：

$$Q^\phi(x,u) = c(x,u) + Q^\phi(x^+), \quad x^+ = F(x), \quad u^+ = \phi(x^+). \quad (27)$$

对于任意输入 $Q$，我们在固定点方程中观察到的另一个时间差：对于任意输入序列 $(x,u)$：

$$\mathcal{D}_{k+1}(Q) = -Q(x,k) + c(x,k) + Q(k+1), \quad (28a)$$
$$Q^\phi(x) = Q(x,\phi), \quad x \in X. \quad (28b)$$

如果用 $Q^\phi$ 替换 $Q$，时间差 (28a) 为零。基于时间差 (28a) 近似 $Q^\phi$ 的算法被称为 SARSA。全书中，TD 学习有两种不同的类型：策略内和离策略。定义 (28a) 中的策略内版本 $u(k) = \phi(x)$。离策略算法的困难应通过 5.3 节的后续讨论来解决：如果 $\phi$ 是好的策略，且当 $k \to \infty$ 时 $x(k) \to x^*, u(k) \to x^*$，对于任意函数 $Q$：

$$\lim_{k \to \infty} \mathcal{D}_{k+1}(Q) = \lim_{k \to \infty} \{-Q(x,k) + c(x,k) + Q(k+1)\}, \quad u = \phi(x) \text{ 对于每个 } k. \quad (29)$$

因此，根据约定 $c(x^*,u^*) = 0$，时间差趋于零。

在书的这部分，我们主要关注离策略算法以允许探索。随机控制中策略内算法的优雅理论将在第二部分探讨。

# 5.3.2 最小二乘与线性回归

考虑之前在 (43) 中引入的线性化：

$$Q(x,u) = \theta^T \psi(x), \quad \theta \in \mathbb{R}^d. \quad (30)$$

给定假设 $Q(x^*,u^*) = 0$，考虑函数类是重要的：

$$\psi_i(x^*,u^*) = 0 \quad 1 \le i \le d. \quad (31)$$

根据定义 (28a)，我们得到：

$$\mathcal{D}_{k+1}(Q) = -Q(x,k) + c(x,k) + Q(k+1).$$

# 5.3 TD 学习与线性回归

这可以用一种启发统计学家的形式表示。通过定义：

$$\Gamma_k = c(x(k), u(k)),$$
$$\Gamma_{k+1} = \psi(x(k), u(k)) - \psi(k+1), \phi(k+1))$$

我们得到这种表示：

$$\Gamma_k = \Gamma_{k+1}^T\theta + \mathcal{D}_k(Q)$$

这是标准回归问题的形式：

$$\Gamma_k = \Gamma_{k+1}^T\theta^* + \varepsilon_k,$$

其中 $[\varepsilon_k = \mathcal{D}_k(Q); k \geq 0]$ 被视为“噪声”，而 $\theta^*$ 通常定义为最小方差参数：$\theta^* = \arg\min_{\theta} \Gamma(\theta)$

$$\Gamma(\theta) = E_{\theta}[Y_0 - \Upsilon_0\theta]^2 = \lim_{N\to\infty} \frac{1}{N} \sum_{k=0}^{N} |Y_k - \Upsilon_k\theta|^2.$$

这是时间差序列的均方误差：应用 (32c)

$$\Gamma(\theta) = \lim_{N\to\infty} \frac{1}{N} \sum_{k=1}^{N} [\mathcal{D}_k^{\theta}]^2.$$

该极限的收敛需要输入满足条件，还需要其他条件使得该函数有意义。特别是，在策略内方法 (29) 下，$\Gamma(\theta) = 0$。这就是为什么需要解释。练习 5.2 说明了 LQR 特殊情况下的的设计。

# 最小二乘时间差学习 (LSTD)

对于给定的 $d\times d$ 矩阵 $W>0$，整数 $N$ 以及观测样本 $\{u(k), x(k) : 0 \leq k \leq N\}$，优化极值：

$$\Gamma_{\theta}^{LSTD}(\theta) = \arg\min_{\theta} \Gamma(\theta), \quad \Gamma(\theta) = \theta^T W + \sum_{k=1}^{N} |Y_k - \Upsilon_k\theta|^2.$$

这定义了 Q 函数近似：$Q_N^{LSTD} = \sum_{i} \psi_N^i.$

目标函数是正定二次的，因此通过令目标梯度为零得到解：$\nabla_{\theta}\Gamma_N(\theta) = 0$ 对于 $\theta = \theta_N^{LSTD}$。

