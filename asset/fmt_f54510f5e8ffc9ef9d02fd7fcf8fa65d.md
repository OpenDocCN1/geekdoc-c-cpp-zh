
```
$dS_t = rS_t dt + \sqrt{v_t}d\widetilde{W}_{1,t}$
$dv_t = \kappa^*(\theta^* - v_t) + \sigma\sqrt{v_t}d\widetilde{W}_{2,t}$
```

其中 $\mathbb{E}[d\widetilde{W}_{1,t}d\widetilde{W}_{2,t}] = \rho dt$ 是风险中性测度。注意，当 $\lambda=0$ 时，$\kappa^* = \kappa$ 且 $\theta^* = \theta$，因为这些参数在物理风险中性测度下相等。在书中我们将 $\lambda=0$，但这并非必须。事实上，$\lambda$ 嵌入在风险中性参数 $\kappa^*$ 和 $\theta^*$ 中。因此，估计风险中性参数进行定价是一项研究课题，例如 Bollers 等 (2011)。为了符号简单，当显然处理的是风险中性测度时，我们在书中省略参数上的星号和布朗运动上的波浪号。

`v_t` 的性质由 Cox, Ingersoll 和 Ross (1985) 以及 Brigo 和 Mercurio (2006) 等人描述。众周知，在 `v_s` 的实现值条件下，过程 `v_t` 服从非中心卡方分布，自由度为 `d=4\kappa\theta/\sigma^2`，非中心参数为 `2c_se^{-\kappa(t-s)}`，其中：

```
$c = \frac{2\kappa}{1 - e^{-\kappa(t-s)}}$
```

且 `t > s`。给定值 `v_s` 时，`v_t` 的均值和方差分别为：

```
$m = E[v_t|v_s] = \theta + (v_s - \theta)e^{-\kappa(t-s)}$,
$S^2 = Var[v_t|v_s] = \frac{\sigma^2 e^{-\kappa(t-s)}}{\kappa}(1 - e^{-\kappa(t-s)}) + \frac{\theta\sigma^2}{2\kappa}(1 - e^{-2\kappa(t-s)})^2$.
```

均回归 `kappa` 对矩的影响是直观的，并在 Cox, Ingersoll 和 Ross (1985) 中进行了解释。当 `kappa -> infinity` 时，均值 `m` 趋于均回归率 `theta`，方差 `S_t^2` 趋于零。当 `kappa -> 0` 时，均值趋于当前方差水平 `v_t`，方差趋于 `sigma^2 v_t (t-s)`。

如果条件 `2 kappa theta > sigma^2` 成立，则漂移足够大，保证方差过程为为零。这一条件被称为 Feller 条件。

在本节中，我们展示了 Heston 模型中的看涨价格可以以类似于 Black-Scholes 模型中看涨价格的方式表示，我们在方程 (1.76) 中给出了。作者有时将这种看涨价格表征称为“类 Black-Scholes”或“Black-Scholes 风格”。对于现价为 `S_t` 的不付股息股票，行权价为 `K`，到期时间为 `tau` 的欧洲看涨期权的 `t` 时刻价格为风险中性测度下收益的折现期望值：

```
$C(K) = e^{-r\tau}E^Q[(S_\tau - K)^+$
$= e^{-r\tau}E^Q[S_\tau1_{S_\tau>K} - Ke1_{S_\tau>K}]$
$= S_nP_1 - Ke^{-r\tau}P_2 \quad (1.12)$
```

其中 1 是指示函数。(1.12) 的最后一行是“类 Black-Scholes”看涨价格公式，其中 `P_1` 替换了 `Phi(d_1)`，`P_2` 替换 Black-Scholes 看涨价格 (1.76) 中的 `Phi(d_2)`。在本节中，我们解释如何从第三行推导出最后一行。`P_1` 和 `P_2` 分别代表在给定值 `S_t` 和 `t` 时刻方差 `v_t` 条件下的期权实值概率：

```
$P_j = Pr(\ln S_t > \ln K) \quad (1.13)$
```

对于 `j=1, 2`。这些概率是在不同的概率测度下获得的。在方程 (1.12) 中，期望 `E^Q[1_{S_\tau>K}]` 是在使 `W_t` 和 `W_t^*` 为方程 (1.11) 中风险中性测度布朗运动的测度 `Q` 下的实值概率。我们可以写为：

```
$E^Q[1_{S_\tau>K}] = Q(S_t > K) = Q(\ln S_t > \ln K) = P_2.$
```

计算 (1.12) 中的 `e^{-r\tau}E^Q[1_{S_\tau>K}]` 需要将原始测度变为另一个测度 `Q^S`。考虑拉东-尼科姆导数：

```
$\frac{dQ}{dQ^S} = \frac{B_t/B_0}{S_t/S_0} = \frac{E^Q[e^{rt}]}{e^{rt}} \quad (1.14)$
```

其中：

```
$B_t = \exp(\left(\int_0^t rdu\right) = e^{rt}.$
```

在 (1.14) 中，我们写下 `S_te^{r(T-t)} = E^Q[S_T]`，因为资产以无风险利率 `r` 增长。因此，(1.12)第三行的第一个期望可以写为

```
$e^{-r(T-t)}E^Q[S_T\mathbb{1}_{S_T>K}] = S_tE^Q[\frac{S_T}{S_t}\mathbb{1}_{S_T>K}] = S_tE^Q[\frac{S_T/S_t}{B_T/B_t}\mathbb{1}_{S_T>K}\frac{dQ}{dQ^S}]$$\n= S_tE^Q[\mathbb{1}_{S_T>K}] = S_tQ^S(S_T > K) = S_tP_1$.
```

这意味着欧式看涨期权可以用两种测度写成：

```
$C(K) = S_tQ^S(S_T > K) - Ke^{-rt}Q(S_T > K)$.
```

测度 `Q` 使用债券 `B_t` 作为计性货币，而测度 `Q^S` 使用股票价格 `S`。Bakshi 和 Madan (2000) 给出了以 (1.16) 形式表示的看涨价格推导，但是在通用设定下的。正如他们的论文所示，导致 (1.16) 的测度变换适用于许多模型，包括 Black-Scholes 模型和 Heston 模型。我们将在本章后面的部分看到，`S_t` 遵循 Black-Scholes 模型指定的对数正分布，则 `Q^S(S_T > K) = Phi(d_1)` 且 `Q(S_T > K) = Phi(d_2)`。因此，由 Heston (1993) 开创的期权定价特征函数方法适用于

在本节中，我们将解释如何推导出 Heston 模型的偏微分方程（PDE）。该推导是通用随机波动模型 PDE 的特例，这些模型在 Gatheral (2006)、Lewis (2000)、Musiela 和 Rutkowski (2011)、Joshi (2008) 等人的著作中有所描述。该逻辑与使用单一衍生品推导出 Black-Scholes PDE 的对冲逻辑相似。在 Black-Scholes 模型中，投资组合由标的股票和一个用于对冲股票的单一衍生品组成，使组合无风险。然而，在 Heston 模型中，组合中需要一个额外的衍生品来对冲波动。在这里，我们构建了一个由一个期权 `V(S,v,t)`、 `Delta` 份股票和用于波动对冲的 `varphi` 单位另一个单位 `U(S,v,t)` 组成的组合。组合价值为

```
$\Pi = V + \Delta S + \varphi U$
```

```
$d\Pi = dV + \Delta dS + \varphi dU$.
```

该策略类似于 Black-Scholes 情况。我们应用 Ito 引理得到 `U` 和 `V` 的过程，从而允许我们找到 `Pi` 的过程。然后我们找到使组合无风险的 `Delta` 和 `varphi` 值，并利用该结果推导出 Heston PDE。

为了形成对冲投资组合，首先对第一个衍生品的价值 `V(S,v,t)` 应用 Ito 引理。我们必须对变量 `t, S, v` 对 `V` 求导，并进行二阶泰勒级数展开。结果是 `dV` 遵循过程

```
$dV = \frac{\partial V}{\partial t}dt+\frac{\partial V}{\partial S}dS+\frac{\partial V}{\partial v}dv+\frac{1}{2}\frac{\partial^2 V}{\partial S^2}dS^2+\frac{1}{2}\frac{\partial^2 V}{\partial v^2}dv^2+\rho sv\frac{\partial^2 V}{\partial S\partial v}dt$.
```

我们使用了 `(dS)^2 = (dW_t)^2 = S^2dt`，且 `langle dS, dv rangle = sigma^2dt`，以及 `dsv = sigma v dW_t, dW_2 = rho svdt`。我们还有 `(dt)^2 = 0` 且 `dW_t^2 = dt`。对第二个衍生品 `U(S,v,t)` 应用 Ito 引理产生与 (1.18) 相同的表达式。通过将这些表达式代入 (1.17)，投资组合价值可以为

```
$d\pi = dV + \Delta S + \varphi U$
$$\left[\frac{\partial V}{\partial t} + \frac{1}{2}\frac{\partial^2 V}{\partial S^2} + \rho sv\frac{\partial^2 V}{\partial S\partial v} + \frac{1}{2}\sigma^2\frac{\partial^2 V}{\partial v^2}\right]dt$
+\varphi\left[\frac{\partial U}{\partial t} + \frac{1}{2}\frac{\partial^2 U}{\partial S^2} + \rho sv\frac{\partial^2 U}{\partial S\partial v} + \frac{1}{2}\sigma^2\frac{\partial^2 U}{\partial v^2}\right]dt$
+\Delta\left[\frac{\partial V}{\partial S} + \varphi\frac{\partial U}{\partial S}\right]dS + \varphi\left[\frac{\partial V}{\partial v} + \varphi\frac{\partial U}{\partial v}\right]dv$.
```

为了对股票和波动都进行组合对冲，(1.19) 中的两项必须为零。这意味着对冲参数为

```
$\varphi = -\frac{\partial V}{\partial v}\frac{\partial U}{\partial v}, \quad \Delta = -\varphi\frac{\partial V}{\partial S}\frac{\partial U}{\partial S}$.
```

将这些 `varphi` 和 `Delta` 值代入 (1.19)，得到

```
$d\pi = \left[\frac{\partial V}{\partial t} + \frac{1}{2}\frac{\partial^2 V}{\partial S^2} + \rho sv\frac{\partial^2 V}{\partial S\partial v} + \frac{1}{2}\sigma^2\frac{\partial^2 V}{\partial v^2}\right]dt$
+\varphi\left[\frac{\partial U}{\partial t} + \frac{1}{2}\frac{\partial^2 U}{\partial S^2} + \rho sv\frac{\partial^2 U}{\partial S\partial v} + \frac{1}{2}\sigma^2\frac{\partial^2 U}{\partial v^2}\right]dt$.
```

组合获得无风险利率 `r` 的条件意味着组合价值的变化为 `d\pi = rdt`。方程 (1.17) 变为

```
$d\pi = r(V + \Delta S + \varphi U)dt$.
```

现在将方程 (1.22) 与 (21) 相等，代入 `varphi` 和 `Delta`，去掉 `dt` 项并重新整理。得到欧式期权的 Heston 模型

$$\frac{\partial V}{\partial t} + \frac{1}{2}v^2\frac{\partial^2 V}{\partial S^2} + \rho sv\frac{\partial^2 V}{\partial S\partial v} + \frac{1}{2}\sigma^2\frac{\partial^2 V}{\partial v^2} - rV + rS\frac{\partial V}{\partial S} \quad (1.23)$$

$$\frac{\partial U}{\partial t} + \frac{1}{2}v^2\frac{\partial^2 U}{\partial S^2} + \rho sv\frac{\partial^2 U}{\partial S\partial v} + \frac{1}{2}\sigma^2\frac{\partial^2 U}{\partial v^2} - rU + rS\frac{\partial U}{\partial S}$$

我们在下一节中利用这一点。

方程 (1.23) 的左侧是 `v` 的函数，右侧是 `U` 的函数。这意味着两边都可以写成函数 `f(S, v, t)`。遵循 Heston (1993)，指定此函数为

```
$f(S, v, t) = -\kappa(\theta - v) + \lambda(S, v)$
```

其中 `lambda(S, v, t)` 是波动率。Breeden (1979) 的应用产生关于波动率的线性函数，`lambda` 是一个常数。在方程 (1.23) 的左侧代入 `f(S, v, t)`

```
$-\kappa(\theta - v) + \lambda(S, v)$
```

重新整理得到关于 `S` 的 Heston PDE

```
$$\frac{\partial U}{\partial t} + \frac{1}{2}v^2\frac{\partial^2 U}{\partial S^2} + \rho sv\frac{\partial^2 U}{\partial S\partial v} + \frac{1}{2}\sigma^2\frac{\partial^2 U}{\partial v^2} - rU + rS\frac{\partial U}{\partial S} + [\kappa(\theta - v) - \lambda(S, v)]\frac{\partial U}{\partial v} = 0.$$
```

这是 Heston (1993) 的方程 (6)。方程 (1.24) 中的以下边界条件适用于到期日为 `T`、执行价为 `K` 的欧式看涨期权。在到期日，期权价值等于其内在价值

```
$U(S, v, t) = \max(0, S - K)$.
```

当股票价格为零时，期权毫无价值。随着股票价格上涨，`delta` 趋于一，当波动率增加时，看涨期权等于股票价格。这意味着以下边界条件

```
$U(0, v, t) = 0, \frac{\partial U}{\partial S}(\infty, t) = 1, U(S, \infty, t) = S.$
```

最后，注意 PDE (1.24) 可以写成

```
$$\frac{\partial U}{\partial t} + \mathcal{A}U - rU \quad (1.27)$$
```

其中 `mathcal{A}` 是生成子。(1.27) 中的行是 Lewis (2000) 解释的 Black-Scholes 模型生成子。我们可以定义对数价格 `x = \ln S`，用 `(x,t)` 代替 `(S,t)` 表示 PDE。这导致了一个不出现现价 `S` 的更简单形式的 PDE。这需要

```
$\frac{\partial U}{\partial x} = \frac{1}{S}\frac{\partial U}{\partial S}, \quad \frac{\partial^2 U}{\partial x^2} = \frac{1}{S^2}\frac{\partial^2 U}{\partial S^2} - \frac{1}{S^2}\frac{\partial U}{\partial S} \text{ (no, it is } \frac{\partial^2 U}{\partial x^2} = \frac{1}{S^2}\frac{\partial^2 U}{\partial S^2} + \frac{1}{S^2}\frac{\partial U}{\partial S})$
```

使用乘法法则，我们得到

```
$\frac{\partial^2 U}{\partial x^2} = \frac{1}{S^2}\frac{\partial^2 U}{\partial S^2} + \frac{1}{S}\frac{\partial U}{\partial S}$
```

等等，正确的变换是 $\frac{\partial^2 U}{\partial x^2} = \frac{1}{S^2}\frac{\partial^2 U}{\partial S^2} + \frac{1}{S}\frac{\partial U}{\partial S}$。让我们重新评估。

将这些表达式代入 Heston PDE (1.29)。所有的 `S` 项都抵消了，我们得到 Heston PDE
