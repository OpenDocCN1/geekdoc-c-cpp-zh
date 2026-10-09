
# 结论

在本章中，我们展示了 $x_\tau$ 的单变量特征函数和对于 $(x_\tau, v_\tau)$ 的二元特征函数在形式上是相同的，系数除外。这些系数的区别仅在于 Riccati 方程的初始条件。我们还展示了单变量特征函数是二元特征函数的一个特例。接下来，我们介绍了 Mikhailov 和 Elices (2009) 的时间依赖模型。这两个模型都依赖 Sahbi 和 Lord (2010) 出的二元特征函数的递归关系。最后，我们介绍了 Bahadorzadeh 等 (2010) 的模型，该模型依赖解析展开来获取期权价格。因此，它的计算速度比其他两个时间依赖模型快得多。然而，我们检查的所有时间依赖参数模型的拟合效果都优于此前涵盖的常数参数模型。

在第 8 章中，我们引入了显式法，并解释了它是用有限差法近似 Heston 偏微分方程 (PDE) 的示例。我们在该章中也看到，这些方法在股票价格和波动率的二维网格上产生一组期权价格，而不仅仅是单一的股票价格和波动率值。

# 第 10 章

## 有限差分方法

### 摘要

在本章中，我们将介绍通过求解代表股票价格和波动率的二维网格 Heston PDE 来获取欧式看涨价格的方法。我们首先展示了如何构建用于价格和波动率离散化的均匀和非均匀网格，并给出 Heston PDE 中导数的有限差分近似公式。然后，我们介绍了加权法，这是一种流行的方法，包含隐式方案、显式方案和 Crank-Nicolson 方案作为特例。我们在第 8 章将该方法应用于美式期权定价时，曾简要遇到过显式方案。接下来，我们解释了欧式看涨 PDE 的边界条件。最后，我们解释了交替方向隐式法（ADI），该方法可以用较少的时间点产生准确的结果。

这些方法可以很容易修改以允许欧式看跌的定价，这需要对边界条件进行重新制定。然而，在许多情况下，使用看跌看涨平等式来获取看跌价格更为简单。

### 算子形式的 PDE

回顾第 1 章中支付分红股票期权的价值 $U(S,v,t)$ 的 Heston PDE，当现货价格为 $S$，波动率为 $v$，到期时间为 $t$ 且 $\lambda = 0$ 时：

$$\frac{\partial U}{\partial t} = \frac{1}{2}vS^2\frac{\partial^2 U}{\partial S^2} + \rho vS\frac{\partial^2 U}{\partial S\partial v} + \frac{1}{2}\sigma^2 v^2\frac{\partial^2 U}{\partial v^2} \quad (10.1)$$
$$-rU + (r-q)S\frac{\partial U}{\partial S} + \kappa(\theta - v)\frac{\partial U}{\partial v}$$

由于我们使用的 $t$ 代表到期时间，导数 $\partial U/\partial t$ 的符号与 $t$ 代表时间时相反。使用 $U(t)=U(S,v,t)$ 作为紧凑符号，可以将 PDE 表示为：

$$\frac{\partial U}{\partial t} = LU(t) \quad (10.2)$$

其中算子 $L$ 定义为：

$$L = \frac{1}{2}vS^2\frac{\partial^2}{\partial S^2}+\frac{1}{2}\sigma^2v\frac{\partial^2}{\partial v^2}+\rho vS\frac{\partial^2}{\partial S\partial v} + (r-q)S\frac{\partial}{\partial S}+\kappa(\theta-v)\frac{\partial}{\partial v}-r.$$

有限差分法是实现 PDE 数值近似的技术。为了实现有限差分，我们首先需要一个两个状态变量（股票价格和方差）的离散网格，以及一个到期时间的离散网格。这些网格可以具有相等或等间距的增量。其次，我们需要对 PDE 中出现的连续导数进行离散近似。最后，我们需要有限差分方法论来求解 PDE。

### 构建网格

均匀网格是指两个状态变量具有等间距增量的网格。这些网格有两个优点：第一，易于构建；第二，由于增量相等，PDE 中导数的有限差分近似形式简单。非均匀网格的构建更为复杂，但它们可以在某些点周围变得更精细，特别是在通常需要期权价格 $(S,v)=(K,0)$ 区域。因此，非均匀网格可以用更少的网格点提供更准确的近似，从而减少计算时间。

我们将 $S$、$v$ 和 $t$ 的最大值标记为 `S_max`、`v_max` 和 `t_max=tau`（到期时间），最小值标记为 `S_min`、`v_min` 和 `t_min=0`。我们定义 `U_{ij}^k=U(S,v,t)` 为时间 `t`，股票价格为 `S`，波动率为 `v` 时欧式看涨期权的价值。股票价格使用 `N_S+1` 个点，波动率使用 `N_v+1` 个点，到期时间使用 `N_t+1` 个点。为了简洁起见，有时我们将 `U(S,v)` 写为 `U_{ij}^k`。

使用最小值 `S_min=v_min=0` 作为 $(S,v,t)$ 的均匀网格，可以构建为：

$$S_i=i\times ds, \quad i=0,\dots,N_S$$
$$v_j=j\times dv, \quad j=0,\dots,N_v$$
$$t_n=n\times dt, \quad n=0,\dots,N_t$$

其中增量为 `ds=(S_max-S_min)/N_S`，`dv=(v_max-v_min)/N_v`，且 `dt=(t_max-t_min)/N_t`。因此，最大值为 `S_max=N_S ds` 和 `v_max=N_v d`。在 Clarke 和 Pratt (1999) 以及 Kluge (2002) 工作的基础上，Hout 和 Foulon (2010) 描述了一种在执行价 `K` 和现货波动率 `v=0` 周围更精细的非均匀网格。其大小为 `N_S+1` 的价格网格为：

$$S_i = K + c \sinh(\xi_i), \quad i = 0, \dots, N_S$$

其中他们选择 `c = K`，且 `\xi_i = \sinh^{-1}(-K/c) + i\Delta\xi`，其中

$$\Delta\xi = \frac{1}{N_S} \left[ \sinh^{-1}\left(\frac{S_{max}-K}{c}\right) - \sinh^{-1}\left(-\frac{K}{c}\right) \right].$$

大小为 `N_v+1` 的波动率网格为：

$$v_j = d \sinh(j\eta), \quad j = 0, \dots, N_v$$

带有

$$\Delta\eta = \frac{1}{N_v} \sinh^{-1}\left(\frac{v_{max}}{d}\right).$$

Hout 和 Foulon (2010) 使用 `d = v_max/50`，并对 `t` 使用均匀网格。图10.1展示了使用他们设置的非均匀网格，其中 `N_S=70`，`N_v=50` 且 `K=10`。价格网格由蓝线表示，波动率由红线表示。注意在价格维度上，网格在执行价周围最精细，而在波动率维度上，网格向零推进变得更精细。

### 导数的有限差分近似

回顾我们使用符号 `U_{ij}^n, U(S,v,t_n)` 表示时间 `t_n`，价格为 `S`，波动率为 `v` 时欧式看涨的价值。当网格是均匀时，导数的有限差分近似是简单的。推广到非均匀网格是直接的，但近似要复杂一些。在本书任何地方，我们都对 PDE (10.1) 中 `S` 和 `v` 方向的一阶和二阶导数使用中心差分近似。通常，$(S,v)$ 处的一阶和二阶导数可以用 $(S,v)$ 相邻点的 `U` 值表示。接下来的段落中，我们假设使用非均匀网格并将导数的中心差分近似简化为更简单的形式。本节的剩余部分，我们分别处理 PDE 内部点和边界点的近似。![](img/bc3df3b6c26227307f56b75ef87311_0.png) 图 10.1 非均匀网格

内部点位于网格内部，因此它们远离边界。一阶导数对于内部点 $(S_i, v_j)$ 由 `2ds` 近似：

$$\frac{\partial U}{\partial S}(S_i, v_j) = \frac{U_{i+1,j} - U_{i-1,j}}{S_{i+1} - S_{i-1}}, \quad \frac{\partial U}{\partial v}(S_i, v_j) = \frac{U_{i,j+1} - U_{i,j-1}}{v_{j+1} - v_{j-1}} \quad (10.5)$$

当使用均匀网格时，中心差分分别被 `2ds` 和 `2dv` 替换。二阶中心差分位于 Kluge (2002) 的表 4 以及 Hout 和 Foulon (2010) 中。这些是：

$$\frac{\partial^2 U}{\partial S^2}(S_i, v_j) = \frac{\frac{U_{i+1,j} - U_{i,j}}{S_{i+1} - S_i} - \frac{U_{i,j} - U_{i-1,j}}{S_i - S_{i-1}}}{ds}$$
$$\frac{\partial^2 U}{\partial v^2}(S_i, v_j) = \frac{\frac{U_{i,j+1} - U_{i,j}}{v_{j+1} - v_j} - \frac{U_{i,j} - U_{i,j-1}}{v_j - v_{j-1}}}{dv}$$
$$\frac{\partial^2 U}{\partial S \partial v}(S_i, v_j) = \frac{\frac{U_{i+1,j+1} - U_{i+1,j}}{v_{j+1} - v_j} - \frac{U_{i,j+1} - U_{i,j}}{v_j - v_{j-1}}}{ds} - \frac{\frac{U_{i+1,j-1} - U_{i+1,j}}{v_j - v_{j-1}} - \frac{U_{i,j-1} - U_{i,j}}{v_{j-1} - v_j}}{ds}$$

当使用均匀网格时，分母分别被 $(ds)^2$ 和 $(dv)^2$ 替换，得到的表达式简单得多。最后，内部点的混合导数出现在 Kluge (2002) 的表 4 中：

$$\frac{\partial^2 U}{\partial S \partial v}(S_i, v_j) = a_{1,1}U_{i+1,j+1} + a_{1,-1}U_{i+1,j-1} + a_{-1,1}U_{i-1,j+1} + a_{-1,-1}U_{i-1,j-1} + a_{1,0}U_{i+1,j} + a_{-1,0}U_{i-1,j} + a_{0,1}U_{i,j+1} + a_{0,-1}U_{i,j-1}$$

其中系数为：

$$a_{1,1} = \frac{1}{4ds dv}, \quad a_{1,-1} = -\frac{1}{4ds dv}, \quad a_{-1,1} = -\frac{1}{4ds dv}, \quad a_{-1,-1} = \frac{1}{4ds dv},$$
$$a_{1,0} = -\frac{1}{4dv}, \quad a_{-1,0} = \frac{1}{4dv}, \quad a_{0,1} = -\frac{1}{4ds}, \quad a_{0,-1} = \frac{1}{4ds}.$$

在这些系数中，增量为 `\Delta S_i = S_i - S_{i-1}` 和 `\Delta v_j = v_j - v_{j-1}`。这些二阶导数简化的表达方式也有效，但准确性不够。

$$\frac{\partial^2 U}{\partial S^2}(S_i, v_j) = \left(\frac{U_{i+1,j}^n - U_{i,j}^n}{S_{i+1} - S_i} - \frac{U_{i,j}^n - U_{i-1,j}^n}{S_i - S_{i-1}}\right) \frac{1}{S_{i+1} - S_{i-1}}$$

$$\frac{\partial^2 U}{\partial v^2}(S_i, v_j)) = \left(\frac{U_{i,j+1}^n - U_{i,j}^n}{v_{j+1} - v_j} - \frac{U_{i,j}^n - U_{i,j-1}^n}{v_j - v_{j-1}}\right) \frac{1}{v_{j+1} - v_{j-1}}$$

$$\frac{\partial^2 U}{\partial S\partial v}(S_i, v_j) = \frac{U_{i+1,j+1}^n - U_{i,j+1}^n - U_{i+1,j}^n + U_{i,j}^n}{(S_{i+1} - S_i)(v_{j+1} - v_j)}$$

当使用网格时，方程 (10.6) 中的混合导数简化为：

$$\frac{\partial^2 U}{\partial S\partial v}(S_i, v_j) = \frac{U_{i+1,j+1}^n - U_{i,j+1}^n - U_{i+1,j}^n + U_{i,j}^n}{4 \Delta ds \Delta dv}} \quad (10.6)$$

无论使用均匀网格还是非均匀网格，点 $(S, v)$ 处的所有导数都可以用涉及在 $(S, v)$ 相邻点求值的 `U` 及其系数的和来表示，如：

$$\sum_{k,l} a_{k,l} U_{k,l}^n$$

详情见 Kluge (2002) 或 Burden and Ferreira (2010)。微分方程 (PDE) 的边界点（在本章稍后定义）需要使用不涉及网格外点的近似。因此，我们可以使用前向或后向差分。例如，对于第一个 S 导数，差分值为：

$$\frac{\partial U}{\partial S}(S_i, v_j) = \frac{U_{i+1,j}^n - U_{i,j}^n}{S_{i+1} - S_i}, \frac{\partial U}{\partial v}(S_i, v_j) = \frac{U_{i,j+1}^n - U_{i,j}^n}{v_{j+1} - v_j}} \quad (10.8)$$

Duffy (2006) 的教材也是期权定价背景下 PDE 有限差分近似的极佳参考。

## 加权方法

这是一种将其他有限差分方案纳入特例例方法。记得 `U_{i,j}^n` 表示欧式看涨在网格点 $(S, v)$ 和到期日 `t_n` 处的值。由于 $(S, v)$ 的二维网格大小为 `N=(N_S+1)(N_v+1)`，在每个 `t_n` 时，`U_{i,j}^n` 有 `N` 种可能的值。

为了应用加权方法，必须构造一个大小为 `N` 的向量 `U^n`，这些值可以任意排列。我们选择将图 10.2 中的 `N_v` 个列向量 `u_0, u_1, \dots, u_{N_v}` 堆叠，使得 `U^0 = (u_0^0, u_1^0, \dots, u_{N_v}^0)` 为其向量。因此，`U^n` 的项对应于以下 $(S_i, v_j)$ 点：

$$(S_0, v_0), (S_1, v_0), \dots, (S_{N_s}, v_0), (S_0, v_1), (S_1, v_1), \dots, (S_{N_s}, v_1), \dots, (S_0, v_{N_v}-1), (S_1, v_{N_v}-1), \dots, (S_{N_s}, v_{N_v}-1), (S_0, v_{N_v}), (S_1, v_{N_v}), \dots, (S_{N_s}, v_{N_v}). \quad (10.9)$$

| | `v_0` | `v_1` | ... | `v_{N_v}` |
|---|---|---|---|---|
| `S_0` | `U^0_{0,0}` | `U^0_{0,1}` | | `U^0_{0,N_v}` |
| `S_1` | `U^0_{1,0}` | `U^0_{1,1}` | | `U^0_{1,N_v}` |
| : | : | : | : |
| `S_{N_s}` | `U^0_{N_s,0}` | `U^0_{N_s,1}` | | `U^0_{N_s,N_v}` |

**图 10.2** 股票价格和波动率网格上的欧式看涨价值

加权方法也称为 `\theta` 方法，通过以下关系定义：

$$\frac{U^{n+1} - U^n}{dt} = L U^{n+1} + (1 - \theta)U^n \quad (10.10)$$

其中 `L` 是基于 (10.3) 定义算子的 `N \times N` 稀疏矩阵。初始条件 `U^0` 是已知的，因为它代表到期时的价值。在这里，我们可以从到期开始，从初始值 `U^0` 开始使用 `L` 获取 `U^1, U^2`，直到达到 `U^{N_v}`。这是通过每步求解方程实现的：

$$(I - \theta dtL)U^{n+1} = (I + \theta dt)U^n \quad (10.11)$$

其中 `I` 是大小为 `N` 的单位矩阵。该方程可以通过取左侧矩阵的逆来求解，使得：

$$U^{n+1} = (I - \theta dtL)^{-1}(I + \theta dt)U^n. \quad (10.12)$$
