
```
$$\min_{\theta\neq 0}\frac{1}{V(\theta)}|(\theta+3\sin(\theta))| = 2\min_{\theta\neq 0}\frac{1}{\theta}(\theta+3\sin(\theta)) = 2+6[\min\sin(\theta)]\geq 0.68,$$
```

其中最终界来自于所有 $\theta$ 的 $\sin(\theta)\geq-0.22$。记 $\varrho_0=0.68/2=0.34$，我们得到李雅普诺夫漂移条件 $\frac{d}{dt}V(\theta_t)\leq-2\varrho_tV(\theta_t)$，导致 $V(\theta_t)\leq\exp(-2\varrho_0t)$，根据 $V$ 的定义：

```
$|\theta-\theta^*|\leq|\theta-\theta^*|\exp(-\varrho_0t)$. (8.46)
```

因此 (8.33) 在 $B_0=1$ 时成立。图 8.4 表明 $\varrho_0=0.34$ 大约等于最大值，使得对于 $\theta\leq0$ 有 $\varrho\geq-0.34\theta$，且对于 $\theta\geq0$ 有 $f(\theta)\leq-0.34\theta$。

界 (8.33) 变为：

```
$|\partial\tau_{\tau_{n+k}}-\theta^*|\leq|\theta_n-\theta^*|\exp(0.334g)\frac{n}{n+k}.$
```

当 $g=1/0.34\approx3$ 时，右侧以 $1/k$ 的速度收于零。

随机近似

![](img/0790f102da4ffa7564329bf76c7d0815_315_0.png)

值 $g=1/4$ 可能导致非常缓慢的瞬态性能，即使均方误差以最优速率收于零。这在图 8.5 中所示。在讨论该图之前，我们重新回顾渐近方差的主题。

### 8.4.2 方差公式

如果我们增加步长规则 $\alpha_n = g/n$ 中的增益，会预期什么？对于 $g > g^*/2$ 的方差公式来自 (8.28a)，并且与蒙特卡洛的方差公式相似：

$$\sigma_{\Delta}^2 = \left(\frac{g^2}{g/g^*}\right)\sigma_{\Delta}^2. (8.47)$$

值 $g=1/0.34$ 比使用渐近理论得出的值 $g^*=1/4$ 大 12 倍。公式 (8.47) 可以证明在较大的增益下，$\sigma_{\Delta}^2$ 增加了六倍以上。

如果我们选择 $\alpha_n = g/n^2$，则 (8.6) 结果为：

$$\sigma_{\Delta}^2 = \lim_{n\to\infty} n\mathbb{E}[(\theta_n - g^*)^2]. (8.48)$$

在这种情况下，公式更简单，并且对于任何 $g>0$ 和任何 $\rho \in (0.5,1)$ 均有效：

$$\sigma_{\Delta}^2 = gg^*\sigma_{\Delta}^2. (8.49)$$

详情见第 8.7.2 节。

### 8.4.3 仿真

到为止，我们还没有提到过均值为零的扰动 $\Phi$。随后的图是一个独立同分布的高斯过程，$\Phi_n \sim N(0,1)$。对于独立同分布扰动，(8.47) 右侧出现的方差项定义为：

$$\sigma_{\Delta}^2 = \mathbb{E}[(f'(\theta^*),\Phi_n)^2] = \mathbb{E}[[(10\cos(\theta^*))\Phi_n]^2] = 100.$$

对于步长 $\alpha_n = g/n$，公式 (8.47) 给出：

$$\sigma_{\Delta}^2 = (5/2)^2,\quad g=g^*=1/4,$$

（注：提供的文本在 OCR 页面之间存在大量的重复和重叠。我已经根据提示源按时间顺序合并了唯一内容。）

## 8.5 Zap 随机近似 (Stochastic Approximation)

(ii) 瞬态行为是理想：根据 (4.12) 我们得到 $f(\theta_t) = f(\theta_0)e^{-t}$，这表明 SA 算法具有良好的数值特性。

(iii) 在书的第一部分无法预测的是，$A_n$ 的渐近协方差也是最优的（在 $f$ 和 $\{f_n\}$ 满足松和假设的情况下）。

### 8.5.1 近似牛顿-拉夫森流

该算法的设计旨在近似 (4.15) 中引入的正则化牛顿-拉夫森流：

$$\frac{d}{dt}\theta_t = -[I + A(\theta_t)^\top A(\theta_t)]^{-1} A(\theta_t)^\top f(\theta_t)$$

## Zap 随机近似

初始化 $\theta_0 \in \mathbb{R}^d, A_0 \in \mathbb{R}^{d \times d}, \epsilon > 0$。对于 $n \geq 0$ 更新：

$$\bar{A}_{n+1} = \bar{A}_n + \beta_n[\bar{A}_{n+1} - \bar{A}_n], \quad \bar{\theta}_{n+1} = \bar{\theta}_n + \alpha_n \partial f_n(\bar{\theta}_n), \quad \theta_{n+1} = \theta_n + \alpha_n G_n f_n(\theta_n), \quad G_{n+1} = -[I + \bar{A}_{n+1}^\top \bar{A}_{n+1}]^{-1} \bar{A}_{n+1}^\top. \quad (8.51a) (8.51b)$$

两个步长序列 $\{\alpha_n\}$ 和 $\{\beta_n\}$ 满足 (8.22)：

$$\lim_{n \to \infty} \frac{\beta_n}{\alpha_n} = \infty.$$

在“高增益”假设 (8.22) 下，我们期望当 $n$ 较大时 $\bar{A}_{n+1}$ 是 $A(\theta_n)$ 的合理估计，其中 $A(\theta_n)$ 定义在 (8.13) 中。这种直觉得到了第 8.2.4 节总结的双尺度 SA 通用理论的支持。特别是，(8.51a) 的高增益假设告诉我们，在瞬态期后可以预期 $A_n \approx A(\theta_n)$。对于 $\{\theta_n\}$ 的 ODE 近似正是正则化的牛顿-拉夫森流。

### 8.5.2 Zap Zero Zero

在后续章节考虑的大多数算法中，出现在 (8.51a) 中的矩阵 $A_{n+1}$ 是低秩的。对于 $\epsilon=0$ 的特殊情况，使用矩阵逆引理 (A.1) 可以高效计算 $G_n$ 的矩阵更新。当 $A_{n+1}$ 的秩等于一时，这尤为简单，且分解形式定义 $A_{n+1} = W_{n+1}V_{n+1}$，其中 $W_{n+1}$ 和 $V_{n+1}$ 为列向量。那么，(A.1) 给出了以下更新方程：

$$G_{n+1} = [G_n^{-1} - A_{n+1}] = G_n - \frac{1}{1-V_{n+1}^\top G_nW_{n+1}}G_nW_{n+1}V_{n+1}^\top G_n.$$

右侧涉及两个矩阵-向量乘积，$G_nW_{n+1}$ 和 $V_{n+1}^\top G_n$，这引入了 $O(d^2)$ 复杂度。

在更强条件下，复杂度为 $O(d)$（甚至 $O(1)$）的更新是可能的。

那么，$\lim_{n\to\infty} f(\theta_n) = 0$。

$$\theta_{n+1} = \theta_n + \alpha_{n+1}[A_{n+1}\theta_n - b_{n+1}]. \quad (8.53b)$$

## 8.5 Zap 随机近似

这是一个非常特殊的情况，因为 $A(\theta) = E[A_n]$ 不依赖于 $\theta$。这是可以容易证明放宽假设 (8.22) 的唯一情况。

接下来的命题考虑使用 $\alpha_n = \beta_n = 1/n$ 的 SNR，因此 (8.51a) 变为：

$$\bar{A}_{n+1} = \bar{A}_n + \frac{1}{n+1}[A_{n+1} - \bar{A}_n].$$

回想第 8.3.1 节，该递归的解可以表示为平均值：

$$\bar{A}_{n+1} = \frac{1}{n+1} \sum_{k=1}^{n+1} A_k.$$

**命题 8.8** 考虑线性模型 (8.53a) 的 SNR 算法形式如下：

$$\theta_{n+1} = \theta_n - \frac{1}{n+1}[A_{n+1}\theta_n - b_n],$$

$$\bar{A}_{n+1} = \frac{1}{n+1}\{\bar{A}_0 + \sum_{k=1}^{n} A_k\}. \quad (8.54)$$

假设 $d \times d$ 矩阵 $A_n$ 的选择使得 $A_n$ 对每个 $n$ 均可逆。对于每个 $n$，无论初始条件 $\theta_0$ 如何：

$$\theta_n = \bar{A}_n^{-1}b_n, \quad \text{其中} \bar{b}_n = \frac{1}{n} \sum_{k=1}^n b_k.$$

一个例子是第 8.3.3 节中带有噪声观测的二次损失函数最小化。这是使用 $\alpha_n = \beta_n = 1/n$ 的线性 SA 算法 (8.53b)，其中 $A_n = M_n^T M_n，$b_n = M_n^T \xi_n$，且根据假设 $A(\theta) = -E[M_n^T M_n] < 0$。对于所有 $n$，任何初始化 $\bar{A}_0 < 0$ 均满足该假设。命题 8.8 意味着 SNR 本质上等同于 ERM。

对于更通用的（非二次）优化问题 (8.42)，不能声称将使用 SNR 进行随机梯度下降。可以通过 SA 或 PJR 平均获得与 ERM 相同的渐近协方差。

**命题 8.8 的证明** 将 (8.54) 中 $\{\theta_n\}$ 的递归每一步乘以 $(n+1)A_{n+1}$，得到：

$$(n+1)\bar{A}_{n+1}\theta_{n+1} = (n+1)\bar{A}_n\theta_n - [A_{n+1}\theta_n - b_n].$$

根据定义，$(n+1)\bar{A}_{n+1} = n\bar{A}_n + A_{n+1}$，给出：

$$\bar{A}_{n+1}\theta_{n+1} = \bar{A}_n\theta_n + \frac{b_n}{n+1}.$$迭代该递归得到对于每个 $n \ge 0$，$(n+1)\bar{A}_{n+1}\theta_{n+1} = \sum_{k=1}^{n+1} b_k$。

## 8.6 注意事项 (Buyer Beware)

由于非线性动力学，随机近似很难应用。这通常使用 SA 解决，而 PJR 平均可能会失败。

### 8.6.1 条件数的诅咒

线性化矩阵 $A = \partial f(\theta^*)$ 的条件数是最大奇异值与最小奇异值的比：

$$\kappa(A) = \frac{\sigma_{\max}(A)}{\sigma_{\min}(A)} \quad (8.55)$$

其中奇异值 $\sigma_i(A)$ 通过取 $AA^\top$ 的特征值得到。如果条件数很大，直到运行很久才能观察到 Polyak-Ruppert 平均的效果。该例子是强化学习中可能出现问题的预警。标准 Q-learning 算法具有巨大条件数的线性化矩阵 $A$，第 9 节的例子揭示了 PJR 平均可能没有益处。使用 SA 递归说明：

$$\theta_{n+1} = \theta_n + n^{-1}[A\theta_n + \Delta_n] \quad (8.56)$$

其中 $\Delta$ 是高斯分布且独立同分布，边缘分布为 $N(0,1)$。矩阵形式为简单形式 $A = -I + (\kappa-1)vv^\top$，其中 $\|v\| = 1$ 且 $\kappa > 1$。$A$ 的条件数为 $\kappa$。让我们考虑两个最优收敛算法：

- (i) 随机牛顿-拉夫森：$\theta_{n+1} = \theta_n + n^{-1}(A_n)^{-1}\Delta_n \quad (8.57)$

- (ii) 仔细选择步长的 PJR 估计。大条件数的挑战之一是缩小步长以避免参数估计爆炸。即使没有噪声这也是需要的，因此产生了修正 $\alpha_n = \min(\alpha_0, n^{-\rho})$ (8.58)。

值 $\alpha_0 = 1/\kappa$ 在实验中是可靠的，$\rho \in (1/2,1)$。两种算法都实现了每个参数分量的最优方差：

$$\Sigma_{\theta} = G\Sigma_A G^\top = (I + rv^\top)^{-1} = I - \frac{r}{1+r}vv^\top,$$

其中 $r = \kappa-1$。特别是，每种方法达到了最优方差：

$$\lim_{n\to\infty} E[\theta_n(i)^2] = \lim_{n\to\infty} E[\theta^*(i)^2] = \Sigma_{\theta^*}(i).$$

## 8.6 注意事项 (Buyer Beware)

事实上，SA 递归不需要极限。这通过命题 8.8 的改进变看出：首先注意当 $n=0$ 时 (8.57) 中，初始条件被抵消了：

$$\theta_1 = \theta_0 + \theta_0 - A^{-1}\Delta_1 = -A^{-1}\Delta_1.$$

可以通过归纳法证明对于每个 $n \geq 1$，

$$\theta_n = -A^{-1}\frac{1}{n}\sum_{k=1}^n \Delta_k.$$

这里 $\sqrt{n}\theta_n \sim N(0, \Sigma^*)$ 对于每个 $n$。在描述的实验中，向量 $v$ 选择为 $z/\|z\|$，$z$ 选取自 $N(0,d)$，$d=50$。发现 $\hat{\Sigma}(i)$ 对于每个 $\kappa$ 的值接近单位。Polyak-Ruppert 平均的指数取为 $0.75$，对最近 70% 的样本进行平均：

$$\theta_n = \frac{1}{0.7n}\sum_{0.3n \leq k \leq n} \theta_k.$$

得到了 $Z_n^i = \sqrt{n}\theta_n^i : 1 \leq i \leq 500$（500 次独立运行），初始化 $\theta_0^i \sim N(0,\sigma^2)$ 使用 $\sigma^2 = 25$。

对于 $\kappa = 100$，Polyak-Ruppert 估计的行为在 $10^3$ 次迭代后非常相似。将值增加到 $\kappa = 500$ 揭示了差异。问题的源头见图8.8：使用了 $\alpha_n \leq 1/n$ 以避免参数估计爆炸。该图仅显示了三个参数估计的前三个参数估计。在这些情况下，估计 $\theta_n(1)$ 和 $\theta_n(1)$ 是不可见的，因为 $\theta_0(1)$ 超出了范围且步长太小。

图 9，$n=10^3$，显示使用 Polyak-Ruppert 平均时方差显著增大。当 $n=10^4$ 时，情况有所改善，PJR 平均的结果结果与 SNR 更相似。

然而，如果条件 $\kappa$ 从 500 增加到 1,000，$n=10^4$ 个样本不再足够。

![](img/0790f102da4ffa7564329bf76c7d0815_322_0.png)

**图 8.8** 前三个参数估计的比较。(8.56) 使用步长 $\alpha_n = \min(1/\kappa,1/n)$。右侧比较了 Zap SA 和 PJR 平均。

# 306

# 随机逼近

![](img/0790f102da4ffa7564329bf76c7d0815_323_0.png)

图 8.9 前三个参数估计值的直方图。对于 Zap SA 算法，对于每个 $t=1, 2, 3$，估计值服从分布为 $N(0,\Sigma(i,t))$ 的高斯分布。

## 8.6.2 马尔可夫记忆曲线

上一个例子是特殊的，因为“噪声”是独立同分布的（i.i.d），而不是强化学习（RL）典型的马尔可夫噪声。为了说明噪声如何带来挑战，我们再次考虑一个线性算法，但带有“乘性噪声”：

```
$$\theta_{n+1} = \theta_n + \alpha_n[A_n + \Delta_n\theta_n], \quad \theta_0 \in \mathbb{R},$$
```

其中 $A_{n+1} = X(n+1) - \eta$，其中 $X$ 是 M/M/1 队列的样本（转移矩阵见 (6.14)），而 $\Delta$ 是独立同分布的 $N(0,1)$ 且与 $X$ 独立。回顾第 6.7.4 节，只要 $\mu > \alpha$（单服务队列的负载条件），马尔可夫链 $X$ 就具有许多良好的性质。特别是，它是可逆且遍历的，具有几何不变性 $\pi$ 和 $\eta = E_\pi[X(n)] = \alpha/(\mu - \alpha)$。

对于 (8.59) 线性向量场 $f(\theta) = -\theta$ 的 ODE 近似，我们期望其收敛到零，其中我们可以尝试通过以下表示获得中心极限定理（CLT）和矩界：

```
$$\theta_{n+1} = \theta_n + \alpha_n[1 - \Delta_n\theta_n], \quad \theta_0 \in \mathbb{R},$$
```

其中 $\Delta_{n+1} = \Delta_{n+1}(X(n+1) - \eta)\theta_n$。由于 $\theta_n$ 收敛于零，这表明我们可能将其视为 Saul 算法（$A=-1$）的线性版本，该算法满足 CLT 且渐近方差为。
