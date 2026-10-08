

![](img/2d1ac831a270b8b08f8b8ec2205913dc_282_0.png)

**图 7.9** 假设对冲基金在 100 天内的亏损情况

通过母分布以及母分布内的子分布来解释主分布，可以让我们对极值理论（EVT）的运用方式产生一些定性的理解。

考虑图 7.9，它展示了某个特定对冲基金在 100 天内损失的假设图表。根据此类信息，下一步是尝试用某种数学方法对这段期间的损失进行表征。EVT 为此类表征提供了两种基本方法，即块极大值（block maxima）法和阈值（point over threshold）方法¹¹²

块极大值（BM）方法基于将时间段划分为一组等大小的桶（或块）。例如，图 7.10 重现了图 7.9 中给出的假设对冲基金在 100 天内的损失数据，但将时间分成了 10 个块，每个块是一个 10 天的时期，其中包含一定数量的损失。取每个 10 天块中的最大值，我们得到了 10 个局部块极大值，即 10 个数据点，这些点可以用于表征（或拟合）概率分布。这通常被称为广极值分布（GED）。

在对冲基金领域，块极大值法是使用 EVT 估计 VaR（风险风险价值）时较不受青睐的方法。

阈值（POT）方法是一种更现代且被广泛接受的 VaR 估计方法，尽管在数学上具有一定要求。其的基本

![](img/2d1ac831a270b8b08f8b8ec2205913dc_283_0.png)

**图 7.10** 每个 10 天块中的最大损失

![](img/2d1ac831a270b8b08f8b8ec2205913dc_283_1.png)

**图 7.11** 超过阈值的损失

POT 方法背后的思想是选择一个数值阈值，任何超过该阈值的损失都被视为极端损失。超过阈值的数据点数量可用于表征（或拟合）概率分布，即在在这种情况下，它被称为广义帕累托分布（GPD）¹¹³。图 7.11 显示了一个典型阈值的示例，其中只有超过 $90,000 的损失会被认为相对于投资组合价值是极端的。

我们已经在第 4 章看到过如何从累积分布函数（CDF）的角度考虑概率分布，即：

$F(x) = P(X \le x)$ (7.10)

![](img/2d1ac831a270b8b08f8b8ec2205913dc_284_0.png)

即对于给定值 $x$，$F(x)$ 是随机变量 $X$ 的观测值至多或等于 $x$ 的概率。对于 EVT，需要考虑一个基于条件概率的后续函数（类似于条件期望模型 ES 的方式）。也就是说，对于收益变量 $X$ 超过某一阈值 $u$ 的超额分布，使得 $X > u$ 时 $y = X - u$ 的条件概率分布可以写为：

$F_u(y) = P(X - u \le y|X > u)$ (7.11)

现在 CDF 是在 $X$ 超过阈值 $u$ 的条件下，$y = X - u$（即阈值的超额或超过部分）小于或等于概率（见图 7.12）。Pickards (1975) 开发的 EVT 主要定理之一指出，对于足够高的阈值 $u$，$F_u(y)$ 可以由 GPD 近似，其可以写为：

```
$G(X) = \begin{cases} 1 - (1 + \frac{\xi y}{\beta})^{-1/\xi} & \text{if } \xi \neq 0 \\ 1 - \exp(-\frac{y}{\beta}) & \text{if } \xi = 0 \end{cases} \quad (7.12)$
```

其中 $y = X - u, \xi = 1/\alpha$ 是形状参数，$\alpha$ 是尾部指数，$\beta$ 是一个缩放参数。有几种方法可以估计 (7.12) 中的参数，例如 Hosking 和 Wallis (1987)、Grimshaw (1993) 以及 Castillo 和 Hadi (1997) 在研究中的*极大似然法、元素分位数法和矩估计法*。

使用上述 GPD 方法对 VaR 的估计可以写为：

```
$VaR_{1-\alpha} = u + \frac{\beta}{\xi} \left( \left( \frac{N}{n_u} \right)^{-\xi} - 1 \right) \quad (7.13)$
```

其中 $N$ 是数据点的总数，$n_u$ 是超过阈值 $u$ 的数据点数量。此外，该方法可以扩展，使得期望缺口 $ES_{1-\alpha}$ 可以如下式表示：

```
$ES_{1-\alpha} = \frac{VaR_{1-\alpha} - \beta - \xi u}{1 - \xi} \quad (7.14)$
```

对于对冲基金而言，收益分布尾部的数据量通常很小，导致较宽的置信区间和弱的显著性估计。BM 和 POT 方法都受到数据有限问题的影响，尽管可以通过减小 BM 中的时间划分或降低 POT 技术的阈值，以产生更多数据点来拟合理想的分布。

在本章中，我们介绍了从传统的 VaR 方法到一些更先进、更具挑战性的理论对冲基金市场模型的主要量化风险指标。在整本书中，我们看到对冲基金的收益通常具有更肥的尾部和非对称收益分布，这严重违背了传统衡量方法所依据的正态分布假设。为了解决这些局限性，研究人员已经开发了传统 VaR 方法的许多扩展，作为对冲基金市场风险的更好估计。这些方法显式地将偏度和峰度纳入模型，或者主要关注收益分布的左尾部（即大多数大部分损失发生的地方）。尽管有了更稳健且可能更准确的市场模型，但必须指出，该分析仅涵盖了与对冲基金相关的风险的一个部分。更全面的处理将涉及同等重要的风险纳入分析。例如，在稳健且有效的对冲基金管理过程中，还应与市场风险一起考虑信用风险、流动性和操作风险的监测、管理和报告。

## 参考文献

Amenc, N. and Martellini, L. (2003). Desperately seeking pure style indices. Working Paper,
HEDC Risk and Asset Management Research Centre.
Amenc, N., Feir, D. and Martellini, L. (2003), An integrated framework for style analysis and
performance measurement, Journal of Performance Measurement,
Anson, M. (2008). The beta continuum: from classic to bulk, Journal of Portfolio
Management, 34.
Artzner, P. Delbaen, E. Faber, J. and Heath, (1999), Coherent measures of risk, Mathe-
Finance, 3(9),
Castillo, E and Hadi, A. (1997), Fitting the Generalised Pareto
Distribution, Journal of the American Statistical Association, 92(4),
Cornish, E. and Fisher, R. (1937), Moments and cumulants in the specification of distributions,
Review of International Statistical Association, 5,
Embrecht, P. Klppelberg, C. and Mikosch, T. (1999), Modelling Extremal Events, Springer-
Berlin.
Favre, L. and Ronaldo, A. (2005), Hedge fund performance and high-
The Journal of Alternative Investments, 8(3),
Fisher, R.A. and Tippett, L.H. (1928). Limiting forms of the frequency distributions of largest
or smallest member of a sample. Proceedings of the Cambridge Philosophical
Society, 24,
Fang, W. and Hsieh, D.A. (2000a), Performance characteristics of hedge funds and commodity
funds: Natural spurious biases, Journal of Financial and Quantitative Analysis,
35,
Fang, W. and Hsieh, D.A. (2000b), The risk in hedge fund strategies: Theory and evidence
from followers, Review of Financial Statistics, 14,
Fang, W. and Hsieh, D.A. (2004). Hedge fund benchmarks: A risk-based approach, Financial
Analysts Journal, 60(5),
Goodwin, T.H. (1998), The Information Ratio, Financial Analysts Journal, 54(4),
Grimshaw, S.D. (1993), Computing maximum likelihood estimates for the Generalised Pareto
Distribution, Technometrics, 35,
Hosking, J.R.M and Wallis, J.R. (1987), Parameter and quantile estimation for the Generalised
Pareto Distribution, Technometrics, 29(3),
Jensen, M.C. (1968), The performance of mutual funds in the period 1945–1964, Journal of
Finance, 23(2),
Gupta, R.H., Kazemi, A. and Schneewe, T. (2003), Omega as a performance measure.
CISDM Research Paper, June.

