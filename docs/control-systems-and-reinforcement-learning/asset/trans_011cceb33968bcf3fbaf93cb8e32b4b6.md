
## 8.4 算法设计示例

本节的目的是通过一个简单的非线性示例来说明算法设计。我们最终将基于 PJR 平均法为此这种情况得到一个非常高效的算法。

SA 递归 (8.2) 中的函数定义为 $f_{n+1}(\theta) = f(\theta, \Phi(n+1))$，其中：

```
$f(\theta, \Phi) = -(\theta + 3\sin(\theta)) + 10\cos(\theta)\Phi$,
```

其中 $\theta$ 和 $\Phi$ 是清晰的，使得 $f: \mathbb{R}^2 \to \mathbb{R}$。当 $\Phi$ 均值为时，我们有：

```
$f(\theta) = E[f(\theta, \Phi)] = -(\theta + 3\sin(\theta))$.
```

图 8.4 中 $f$ 的轨迹显示 $\theta^* = 0$ 是唯一根。我们可以积分得到表示 $f = -\nabla\Gamma$。函数 $\Gamma(\theta) = \frac{1}{2}\theta^2-3\cos(\theta)$ 也显示在图 8.4 中，我们看到它是拟凸且强制的。SA 算法是用于获取 $\Gamma$ 最小值的随机梯度下降实例。

### 8.4.1 增益选择

对于步长选择 $\alpha_n = g/n$，这是该标量示例中最小化渐近方差的增益 $g=-1/A(\theta^*)$。我们有 $A(\theta) = \partial\theta f(\theta) = -(1+3\cos(\theta))$，给出 $A(\theta^*)=-4$ 和 $g^*=4$。在考虑 SA 算法的瞬态性能时，我们将发现这是一个糟糕的选择。

瞬态界 (8.33) 基于形式 (8.33) 的全局指数渐近稳定，该形式通过李雅普诺夫函数获得。对于 $V(\theta) = \frac{1}{2}\theta^2$：

```
$$\frac{d}{dt}V(\theta_t) = -\partial\theta(\theta_t+3\sin(\theta_t)).$$
```

当 $\partial\theta\neq0$ 时，右侧为负。为了获得 $V$ 的界，考虑最坏情况：

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
