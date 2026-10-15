

**表 8.3:** 控制 $R$ 允许取值个数对收敛的影响，$\tau = 0.1$

| Number of random points $R$ | Performance index $I$ |
|---:|---:|
| 15 | 0.023241 |
| 25 | 0.023170 |
| 50 | 0.023171 |
| 100 | 0.023171 |
| 200 | 0.023170 |

**表 8.4:** 两级 CSTR 系统分段线性控制 $P = 10$ 时的最小性能指标

| Time delay $\tau$ | Performance index $I$ |
|---:|---:|
| 0.1 | 0.023166 |
| 0.2 | 0.023731 |
| 0.3 | 0.024213 |
| 0.4 | 0.024615 |
| 0.5 | 0.024940 |
| 0.6 | 0.025192 |
| 0.7 | 0.025376 |
| 0.8 | 0.025499 |

![](img/06ae75163df4fdf5e1eec243d497d393_162_0.png)

**图 8.4:** 两级 CSTR 系统的分段线性连续控制策略，显示了时滞 $\tau$ 的影响

## 8.4 参考文献

- [1] ARIS, R. AND AMUNDSON, N.R.: “An analysis of chemical reactor stability and control”, Chem. Eng. Sci. 7 (1958), 121-147.
- [2] CHAN, H.C. AND PERKINS, W.R.: “Optimization of time delay systems using parameter imbedding”, Automatica 9 (1973), 257-261.
- [3] DADEBO, S. AND LUUS, R.: “Optimal control of time-delay systems by dynamic programming”, Optimal Contr. Applic. Methods 13 (1992), 29-41.
- [4] HAIRER, E., NORSETT, S.P., AND WANNER, G.: Solving ordinary differential equations 1, Springer Series in Computational Mathematics, Vol. 8; Springer, Berlin (1987).
- [5] LAPIDUS, L. AND LUUS, R.: Optimal Control of Engineering Processes, Blaisdell, Waltham, Mass. (1967).
- [6] LUUS, R.: “Iterative dynamic programming: From curiosity to a practical optimization procedure”, Control and Intelligent Systems 26 (1998), 1-8.
- [7] LUUS, R., ZHANG, X., HARTIG, F., AND KEIL, F.J.: “Use of piecewise linear continuous control for time-delay systems”, Ind. Eng. Chem. Res. 34 (1995), 4136-4139.
- [8] OH, S.H. AND LUUS, R.: “Optimal feedback control of time-delay systems”, AIChE J. 22 (1976), 140-147.
- [9] PALANISAMY, K.R., BALACHANDRAN, K., AND RAMASAMY, R.S.: “Optimal control of linear time-varying delay systems via single-term Walsh series”, Proc. IEE 135 pt. D (1988), 332.

## 第 9 章：可变阶段长度

### 9.1 引言

我们在第 7 章中看到，使用分段常值控制时，增加时间阶段数总是会提高对线性系统二次性能指标的控制策略的逼近精度。然而，存在非线性最优控制问题，其中阶段数的增加并不一定会改善性能指标。例如，当最优控制策略涉及从一个极值突然改变到另一个极值时，该切换的时间非常重要。在时间最优控制问题中，我们预期这种类型的“bang-bang”控制。还有其他情况下，我们最不期望最优控制策略出现这种变化，而这可能会令人惊讶。然后，对最优控制策略的良好逼近取决于的不是使用的时间阶段数，而是切换时间能够被多好地逼近。让我们用一个简单的例子来说明。

让我们考虑 Ko 和 Stevens [6] 中的最优控制问题，涉及一阶、可逆、放热化学反应 $A \rightleftharpoons B$ 在化学反应器中。反应器的物料和能量平衡由下式给出：

$$
\frac{dx_1}{dt}=(1-x_1)k_1-x_1k_2 \tag{9.1}
$$

$$
\frac{dx_2}{dt}=300[(1-x_1)k_1-x_1k_2]-u(x_2-290) \tag{9.2}
$$

初始条件为

$$
x^T(0)=[\ 0\quad 410\ ] \tag{9.3}
$$

状态变量 $x_1$ 是期望组分 $B$ 的浓度，$x_2$ 表示绝对温度。控制 $u$ 是取决于冷却剂流量的归一化传热项，且受限于

$$
0\leq u\leq 0.5. \tag{9.4}
$$

反应速率常数随温度的变化方式如下：

$$
k_1 = 1.7536 \times 10^5 \exp\left(\frac{-1.1374 \times 10^4}{1.9872 x_2}\right) \tag{9.5}
$$

和

$$
k_2 = 2.4885 \times 10^{10} \exp\left(\frac{-2.2748 \times 10^4}{1.9872 x_2}\right). \tag{9.6}
$$

问题是在时间区间 $0 \le t < t_f$ 内寻找 $u$，使得性能指标

$$
I = x_1(t_f), \quad t_f = 5 \tag{9.7}
$$

最大化。该问题对应于 Reddy 和 Husain [15] 的案例 II，他们研究了使用基于梯度的方法求解该最优控制问题的困难。案例 I 已由 Luus [9] 详细讨论过。

通过 IDP 获得分段常值最优控制策略并无困难。然而，造成困难的是选择求解该问题的阶段数，因为当阶段数增加时，性能指标的改善并不十分规律，如图 9.1 所示。然而存在明显的规律，因为三个峰值出现在 $P = 17$、$P = 26$ 和 $P = 35$。

![](img/06ae75163df4fdf5e1eec243d497d393_164_0.png)

**图 9.1:** 时间阶段数 $P$ 对性能指标最大值的影响

可以很容易地观察到，使用 17 个时间阶段得到的性能指标值比使用 40 个时间阶段更好。为了理解其背后的原因，让我们检查 $P = 16$、$17$ 和 $18$ 时得到的最优控制曲线。在图 9.2 中，$P = 16$ 时，可以看到在两个时间间隔 $t = 0.625$ 之后，我们切换到允许的最大值有点晚。因此，第二时间步的控制值很小。

在图 9.3 中，$P = 17$ 时，在第二个时间步 $t = 0.588$ 之后，切换大致正确，因此在第三个时间步我们将控制置于允许的最大值。这使得性能指标 $I = 0.72387$ 得到。

在图 9.4 中，$P = 18$ 时，在两个时间步 $t = 0.555$ 之后，切换过早，且切换到小于最大值的值，性能指标 $I = 0.72378$ 不如 $P = 17$ 时得到的值好。

![](img/06ae75163df4fdf5e1eec243d497d393_165_0.png)

**图 9.2:** 使用 $P = 16$ 个时间阶段得到的最优控制策略

因此，我们看到了使用灵活阶段长度而非等长阶段的必要性。本章的目标是展示如何将灵活阶段长度用于 IDP 以及可以获得的改进。仅为完成此示例，让我们看看使用灵活阶段长度时得到的控制策略类型。通过使用 7 个长度不等的阶段，我们得到了图 9.5 中的 6 阶段最优控制策略。这里阶段 2 和 3 都给出了控制的上界。性能指标 $I = 0.723886$ 略好于使用 17 个等长阶段得到的值。

![](img/06ae75163df4fdf5e1eec243d497d393_166_0.png)

**图 9.3:** 使用 $P = 17$ 个时间阶段得到的最优控制策略

图 9.6 和 9.7 显示，通过增加阶段数，性能指标可以得到改善，但改善非常轻微。控制策略在超过上界之后的<|message|> 部分并不很重要。该控制策略部分的这种极低灵敏度使得准确确定最优控制变得困难。策略中最重要的部分是切换时间，必须尽可能准确地获得从 0 到 0.5 的切换时间 $t = 0.5796$。

因此，我们可以看到使用长度不等的阶段来建立最优控制策略的好处。在本章中，我们将概述将阶段长度优化纳入 IDP 的算法，并考虑最终时间指定的问题，正如我们刚刚考虑的示例一样。

![](img/06ae75163df4fdf5e1eec243d497d393_167_0.png)

**图 9.4:** 使用 $P = 18$ 个时间阶段得到的最优控制策略

![](img/06ae75163df4fdf5e1eec243d497d393_167_1.png)

**图 9.5:** 使用 $P = 7$ 个长度不等的阶段得到的最优控制策略

