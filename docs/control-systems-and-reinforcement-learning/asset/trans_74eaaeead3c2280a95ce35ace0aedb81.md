

## 6.6 Lyapunov 函数

在更紧凑的算子理论表示法中，这变为

```
$$PV \leq V - c + \bar{\eta}. \quad (6.27)
```

与确定性情况一样，函数 $c$ 通常被解释为状态空间上的代价函数。通常假设 $c(x)$ 对于“大” $x$ 来说很大（回想第 2.4 节中*强制性*的定义）。在这种情况下，泊松不等式意味着每当 $X(k)$ 很大时，$V(X(k))$ 就会减少。图 2.5 展示了一个确定性系统，图中说明中所指的集合为 $S=\{x : c(x) \leq \bar{\eta}\}$。

## 6.6.1 平均代价

令 $\eta(x)$ 表示平均代价：

```
$$\eta(x) = \lim_{n \to \infty} \frac{1}{n} \sum_{k=0}^{n-1} E[c(X(k)) \mid X(0) = x].$$
```

使用算子理论表示法 (6.9b) 得到

```
$$\eta(x) = \lim_{n \to \infty} \frac{1}{n} \sum_{k=0}^{n-1} P^k c(x).$$
```

在 $\eta(x)$ 的定义中，对 $x$ 的依赖性以及使用“上上界”而非极限都是必要的，因为我们没有对 $X$ 施加任何特定的结构。平均代价在泊松不等式 (6.27) 下允许稳定的界。这是命题 2.3 在马尔可夫设置下的扩展。

**命题 6.4** *假设 (6.27) 成立且处处 $V \geq 0$。那么对于每个 $n \geq 1$ 和每个 $x \in X$，均满足以下瞬态界：*

```
$$\frac{1}{n} \sum_{k=0}^{n-1} P^k c(x) \leq \bar{\eta} + \frac{1}{n}V(x).
```

因此，平均代价满足界 $\eta(x) \leq \bar{\eta}$。

*证明* 将 $P$ 应用于等式两边得到 $P^2V \leq PV - Pc + P\bar{\eta}$，由于 $\eta$ 是常数，

```
$$P^2V \leq PV - Pc + \bar{\eta} \leq V - Pc + 2\bar{\eta}.$$
```

通过重复乘以 $P$，我们得出对于每个 $n$，

```
$$P^nV \leq V + n\bar{\eta} - \sum_{k=0}^{n-1} P^k c.$$$
```

通过重新排列项并利用 $V \geq 0$ 的假设，我们得到了所需的结论。$\square$

我们已经看到，在定理 6.3 的假设下，命题 6.4 给出的平均代价界对于有限空间马尔可夫链是紧的：我们可以取 $V = h + const.$，其中常数选择足够大使得 $V \geq 0$。

Lyapunov理论的魅力在于不需要知道模型就可以性能界。这在下一个示例中得到了说明。

## 示例：标量线性状态模型

考虑标量模型，

```
X(k+1) = \alpha X(k) + N(k+1), \quad k \geq 0, \quad (6.28)
```

其中 $N$ 是独立同分布的，均值为零且具有有限二阶矩 $\sigma_N^2$（不一定是高斯分布）。代价函数是二次的，$c(x) = \frac{1}{2}x^2$。
令 $V(x) = \frac{1}{2}\kappa x^2$，其中 $\kappa > 0$。我们随后有：

```
$PV(x) = E[V(X(k+1)) \mid X(k)=x]\\= \frac{1}{2}\kappa(\alpha x + N(1))^2\\= V(x) + \frac{1}{2}\kappa(\alpha^2 - 1)^2 + \frac{1}{2}\kappa\sigma_N^2., \quad (6.29)
```

只要 $|\alpha| < 1$，我们可以在 $V$ 的定义中设置 $\kappa = (1-\alpha^2)^{-1}$，以获得强制项 $\eta$ 的泊松方程解：

```
$PV(x) = V(x) + \eta(x), \quad with \ \eta = \frac{1}{2}(1-\alpha^2)^{-1}\sigma_N^2., \quad (6.30)
```

由命题 6.4 可知，对于每个 $x$，$\eta(x) \leq \Gamma$。事实上，前面的步骤表明对于每个初始条件，$E[\eta(X(k))] \to \bar{\eta}$，因此我们有等式：$\eta(x) = \bar{\eta}$。
如果 $N$ 是高斯分布，那么当 $k \to \infty$ 时，$P^k(x, \cdot)$ 收敛于高斯分布 $N(0, \sigma_{\eta}^2)$，其中 $\sigma_{\eta}^2 = (1-\alpha^2)^{-2}\sigma_N^2$。

## 6.6.2 折扣代价

*长期来看，我们都会死掉。* 这句话归于约翰·凯恩斯（John Keynes），通常用于证明在最优控制中使用折扣的合理性。我认为这在大多数应用中是错误的。然而，折扣准则有时便于分析，并且在许多学科（特别是运筹学和经济学）中更受青睐。Lyapunov 界及其后果如 (6.4) 所示，表明稳态行为是良好的。特别是如果平均代价是有限的，通过 (6.27) 得到瞬态界。给定参数 $\gamma \in (0,1)$，初始条件 $x$ 的折扣代价定义为和：

```
$h_{\gamma}(x) = \sum_{k=0}^{\infty} \gamma^k E[c(X(k)) \mid X(0)=x]. \quad (6.31)
```

再次，这具有算子形式：

```
$h_{\gamma} = \sum_{k=0}^{\infty} \gamma^k P^k c., \quad (32)
```

如果 $c$ 是负值的，界 $h_{\gamma}(x) \geq c$，使得折扣代价无偏的。再次得到 $h_{\gamma}$ 的界：

```
$h_{\gamma} = c + \gamma Ph_{\gamma}. \quad (33)
```

**命题 6.5** 若 (6.27) 成立且处处 $V \geq 0$，则对于每个 $x$ 和 $\gamma \in (0,1)$，$h_{\gamma}(x) \leq V + \bar{\eta}(1-\gamma)^{-1}$。

*证明* 界 (6.27) 得到

```
$\gamma PV \leq V - g + \eta.$ (34)
```

其中 $g = (1-\gamma)V + \gamma c$ 是 Lyapunov 函数和代价函数的组合。对两边应用 $\gamma P$ 得到：

```
$(\gamma P)^2V \leq \gamma PV - \gamma g + \gamma\bar{\eta}.$
```

然后使用 (34)，

```
$(\gamma P)^nV \leq V - \sum_{k=0}^{n-1} \gamma^k g + \sum_{k=0}^{n-1} \gamma^k \bar{\eta}.$
```

对于平均代价问题，通过 $g = (1-\gamma)V + \gamma c$ 的归纳法得到：

```
$\sum_{k=0}^{\infty} \gamma^k P^k c(x) + (1-\gamma)V(x) \leq V(x) + \frac{\bar{\eta}}{1-\gamma}.$ (35)
```

利用 $V \geq 0$ 的事实，我们可以去掉 (35) 左侧所有涉及 $V$ 的项，得到：

```
$\sum_{k=0}^{\infty} \gamma^k P^k c(x) \leq V(x) + \frac{\bar{\eta}}{1-\gamma}.$
```（此处此处原文逻辑应为推导）通过从两边减去 $(1-\gamma)V(x)$ 并将不等式除以 $\gamma$，得到界 $h_{\gamma} \leq V + \bar{\eta}(1-\gamma)^{-1}$。

**示例 6.4.1** 代价 $c(x) = \frac{1}{2}x^2$ 的线性状态模型折扣代价，泊松方程的解在 (30) 中得到。命题 6.5 给界 $h_{\gamma} \leq V + \bar{\eta}(1-\gamma)^{-1}$，在这种情况下变为

```
$h_{\gamma}(x) \leq \frac{1}{1-\alpha^2}[x^2 + \frac{\sigma^2}{1-\gamma}]. (36)
```

我们接下来计算 $h_{\gamma}$ 以查看该界是否准确。为此，我们从动态规划方程 (33) 开始。令 $V(x) = A_{\gamma} + \frac{1}{2}\kappa x^2$，其中 $A_{\gamma}, \kappa_{\gamma}$ 是待选的常数。从 (29) 得到：

```
$PV \leq \alpha^2 V + (1-\alpha^2)A_{\gamma} + \frac{1}{2}\kappa\sigma^2.$
```

乘以 $\gamma$ 并向每边加上 $c$ 得到：

```
$c+\gamma PV=c+\gamma(\alpha^2 V+(1-\alpha^2) A_{\gamma}+\kappa_{\gamma}),
```

或者重新引入二次表达式：

```
$c(x)+\gamma PV(x)=\frac{1}{2}(1+\gamma^2\kappa_{\gamma})x^2+\frac{1}{2}(\kappa_{\gamma}\sigma_{N}^2+A_{\gamma}).$
```

为了求解动态规划方程，我们需要右侧与 $V$ 匹配。这需要匹配系数：$1+\gamma^2\kappa_{\gamma}=\kappa_{\gamma}$ 以及 $\gamma(\frac{1}{2}\kappa_{\gamma}\sigma_{N}^2+A_{\gamma})=A_{\gamma}$，得到

```
$h_{\gamma}(x)=A_{\gamma}+\frac{1}{2}\kappa_{\gamma}x^{2}=\frac{1}{1-\gamma \alpha^{2}}[x^{2}-\frac{\gamma}{1-\gamma}\sigma_{N}^{2}].$
```

特别是，界 (36) 成立。

## 6.7 仿真：最优控制，面临置信界和控制变量

在平均代价最优控制中，我们面对的不是单一马尔可夫链，而是整个族：族中的每个策略对应一个马尔可夫链。我们想要估计许多策略的平均代价 $\eta=\pi(c)$，以便选择最好的。Lyapunov 函数提供了界，但很难获得足够紧的界来确定哪个策略是最优的。在没有其他选择的情况下，大多数情况下依靠仿真。

## 6.7.1 渐近统计使其有限

只要存在不变概率测度 $\pi$，大数定律 (LLN) 就是成立的。基于 $n$ 个样本的蒙特卡洛估计记为

```
$$\eta_{n}=\frac{1}{n}\sum_{k=0}^{n}c(X(k)).$$ (6.37)
```

LLN 告诉我们它是渐近一致的：

```
$$\lim_{n\to\infty}\eta_{n}=\eta.$$ (6.38)
```

其中极限对于几乎每个（关于 $\pi$）初始条件以概率1 成立。在大多数情况下，极限对于每个初始条件都成立。

