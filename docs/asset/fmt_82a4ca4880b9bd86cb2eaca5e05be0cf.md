
```python
# Angular motion of a nonlinear pendulum by the Runge–Kutta method
#     u'' = -g/l * sin(u) - k * u',    u(0) = u0, u'(0) = u0'
from math import *
from ode import *

g = 9.81e0                         # gravitational acceleration

def Func(t, u, f):                 # RHS of 1st order ODEs
    f[1] = u[2]                    # u[1] = u, u[2] = u'
    f[2] = -g/l * sin(u[1]) - k * u[2]

#### main

l = 1e0                            # pendulum length
k = 0e0                            # velocity coefficient
u0 = 0.5e0*pi                      # initial displacement
du0 = 0e0                          # initial derivative
tmax = 20e0                        # time span
ht = 0.001e0                       # time step size

n = 2                              # number of 1st order ODEs
u = [0] * (n+1)                    # solution components

out = open("pendulum.txt","w")     # open output file
out.write("        t           u       du\\n")

t = 0e0
u[1] = u0; u[2] = du0              # initial values
out.write("{0:10.5f}{1:10.5f}{2:10.5f}\\n".format(t,u[1],u[2]))

nT = 0                             # number of half-periods
t1 = t2 = 0e0                      # bounding solution zeros
us = u[1]                          # save solution
while (t+ht <= tmax):              # propagation loop
    RungeKutta(t,ht,u,n,Func)
    t += ht

    if (u[1]*us < 0e0):            # count solution passages through zero
        if (t1 == 0): t1 = t       # initial zero
        else: t2 = t; nT += 1      # final zero
    us = u[1]                      # save solution

    out.write("{0:10.5f}{1:10.5f}{2:10.5f}\\n".format(t,u[1],u[2]))

T = 2e0*(t2-t1) / nT               # calculated period
T0 = 2e0*pi*sqrt(l/g)              # harmonic period
print("u0 = {0:7.5f}   T/T0 = {1:7.5f}".format(u0,T/T0))

out.close()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_460_0.png)

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_460_1.png)

FIGURE 12.3 Solution `u(t)` of the Cauchy problem of the nonlinear pendulum yielded by the fourth-order Runge–Kutta method for a step size `h = 0.001` and initial angular displacements `u0` = 0.1, π/2, and 3.1 (left panel). Relative period `T/T0` as a function of the initial angular displacement `u0`, and comparison with the theoretical dependence `(2/π)K(sin²(u0/2))` (right panel).

为用 Runge–Kutta 方法之一数值求解问题 12.39–12.40，首先需要将其化为一阶常微分方程组的问题：

```
u₁' = u₂,
u₂' = −(g/l) sin(u₁) − k u₂,
u₁(0) = u₀,
u₂(0) = 0.
```

除了初始模型之外，这里还考虑了速度相关的阻尼项（`u₂ = u'`），其速度系数为 `k`。

在程序 12.4 中，上述常微分方程的右端项在用户函数 `Func` 中编码。由于 `Func` 必须符合 `RungeKutta` 例程期望的参数列表，它通过全局参数 `l` 和 `k` 访问特定于问题的量，而这些参数在主程序中被赋予值。

主程序通过一种简单而可靠的方法确定振荡周期。具体而言，传播循环通过符号变化识别解 `u₁(t)` 的第一个和最后一个零点，并计数所包含的半周期。周期随后通过将极值零点之间的时间跨度除以半周期数得到。

图 12.3 左面板显示了在无摩擦力（`k = 0`）的情况下，对初始角位移 `u₀` = 0.01、π/2 和 3.1 运行代码所得到的时变解之间的巨大差异。右面板显示了随初始角位移 `u₀` 增大而显著上升的相对周期 `T/T₀`，并与精确的解析结果 (12.41) 完美吻合。

## 12.5 Adaptive Step Size Control

在数值求解初值问题时，选择合适的传播步长 `h` 至关重要。使用常数且高估的 `h` 值会在大多数应用中恶化稳定性，并由于截断误差的异常传播导致解的发散。另一方面，过小的步长虽然能够成功克服解剧烈变化的区域，但在变化减小的区域可能会导致计算量过高。求解常微分方程柯西问题的有效算法实际上预期会对步长进行自适应控制，以实现解的整体目标精度。

用于自动步长控制的基本信息包含在截断误差中。下面我们讨论估计截断误差的最简单方法，即步长减半法。为此，我们比较两种解的估计值 `\tilde{y}_{m+1}` 和 `y_{m+1}`，它们分别通过以步长 `h` 进行单步传播初始解 `y_m ≡ y(t_m)`，以及分别以步长 `h/2` 进行两步传播得到，同时也产生 `t_m + h/2` 的中间值 `y_{m+1/2}`。两种近似值之间的差异（其中 `y_{m+1}` 自然更精确）提供了绝对截断误差的有用估计：

```
\Delta_{m+1} = |y_{m+1} - \tilde{y}_{m+1}|, \tag{12.43}
```

以及相应的相对误差：

```
\delta_{m+1} = \frac{\Delta_{m+1}}{|y_{m+1}|} = \left| 1 - \frac{\tilde{y}_{m+1}}{y_{m+1}} \right|. \tag{12.44}
```

积分步长的调整机制主要依赖于截断误差的具体阶数。从这个角度来看，实际上主要有两种实用选择：以局部截断误差或全局截断误差为参考。如第 12.3 节所述，阶数为 `p` 的常微分方程求解器提供的解等价于包含至 `O(h^p)` 项的泰勒级数，因此显示出局部截断误差 `O(h^{p+1})` 和低一阶的全局截断误差 `O(h^p)`。由于在应用中控制全局误差通常更有意义，我们在下面将相对误差 `δ_{m+1}` 与全局截断误差联系起来，并假设其随积分步长按如下方式缩放：

```
\delta_{m+1} \approx K h^{p}. \tag{12.45}
```

设定最大允许误差 `ε`，可以假设对于小于最大值 `h_1` 的步长不会超过它，该值预期与 `ε` 之间存在类似的依赖关系：

```
\varepsilon \approx K_1 h_1^{p}. \tag{12.46}
```

从这两个依赖关系的比值中，可以预测最大可用步长 `h_1`，用实际使用的步长 `h` 和由此产生的误差 `δ_{m+1}` 表示：

```
h_1 \approx \left( \frac{\varepsilon}{\delta_{m+1}} \right)^{1/p} h. \tag{12.47}
```

如果出现的误差 `δ_{m+1}` 超过允许值（`δ_{m+1} > ε`），该公式规定采用减小的步长，以重复传播步。相反，如果 `δ_{m+1} < ε`，该公式指定可增加的步长，可在不超出 `ε` 的情况下传播解。在后一种情况下，实际上无需重复该步，因为所需精度已经达到，步长猜测值 `h_1` 可用于下一步传播。

然而需要注意的是，公式 12.47 并非精确结果，它仅提供步长使用的预测。此外，对于快速变化的解，误差估计 `δ_{m+1}` 本身可能与其实值显著偏离。综合考虑，还可以通过一个小于 1 的特设因子进一步微调预测值 `h_1`（参见 Burden and Faires 2010 和 Press et al. 2007 的变体），旨在总体上减少所使用的步长。

我们实际在以下实现中用来调整积分步长的方案是：

```
h₁ = 0.9 ( ε / δ_{m+1} )^{1/p} h,   h₁/h ≤ 5,   (12.48)
```

该方案倾向于通过因子 0.9 减小步长，并防止步长增加超过 5 倍。

例程 `RKadapt`（清单 12.5）实现了所描述的算法，并采用四阶龙格-库塔方法（`p = 4`）作为基本常微分方程求解器。对 `RungeKutta` 求解器的三次调用（在第 12.4 节中开发）在 `yt` 中返回从 `t` 到 `t + h` 的单步传播的初始解，分别在 `yt2` 中返回初始解先传播到 `t + h/2`，再传播到 `t + h`。入口时接收的参数 `ht` 仅代表当前传播过程的试验步长 `h`。

### 清单 12.5 使用步长减半和龙格-库塔方法的自适应常微分方程求解器（Python 编码）

```python
# =================================================================================
def RKadapt(t, ht, eps, y, n, Func):
# ---------------------------------------------------------------------------------
# Propagates the solution y of a system of 1st order ODEs
#     y'[i] = f[i](t,y[]), i = 1..n
# from t to t+ht using 4th order Runge-Kutta and adaptive step size control
#
# ht  - initial step size (input); final step size (output):
#         ht is unchanged if err <= eps; ht is reduced if err > eps
# ht1 - step size guess for next propagation (output)
# eps - max. relative error of solution components
# Calls: Func(t, y, f) - RHS of ODEs
# ---------------------------------------------------------------------------------
    p = 4                                 # order of basic ODE solver
    itmax = 10                            # max. no. of step size reductions

    yt = [0]*(n+1); yt2 = [0]*(n+1)

    for it in range(1,itmax+1):           # loop of step size scaling
        ht2 = ht/2e0
        for i in range(1,n+1): yt2[i] = yt[i] = y[i]   # initialize trial sol.
        RungeKutta(t,ht,yt,n,Func)                      # t -> t+ht
        RungeKutta(t,ht2,yt2,n,Func)                    # t -> t+ht/2
        RungeKutta(t+ht2,ht2,yt2,n,Func)                # t+ht/2 -> t+ht

        err = 0e0                         # max. error of solution components
        for i in range(1,n+1):
            erri = abs(1e0 - yt[i]/yt2[i]) if yt2[i] else abs(yt2[i] - yt[i])
            if (err < erri): err = erri

        f = 1e0                           # scaling factor for step size
        if (err): f = 0.9e0*pow(eps/err,1e0/p)
        if (f > 5e0): f = 5e0             # prevent increase > 5x
        ht1 = f * ht                      # guess for next step size
        if (err <= eps): break            # precision attained: exit
        ht = ht1                          # reduce step size and repeat

    if (it > itmax): print("RKadapt: max. no. of iterations exceeded !")
    for i in range(1,n+1): y[i] = yt2[i]   # update y with the best solution
    return (ht, ht1)
```

如果估计的截断误差 `err` 超过目标值 `eps`，例程会根据公式 12.48 迭代减小 `ht`，并从相同的初始条件重复进行传播步骤，直到满足精度准则。相对截断误差 `err` 评估为解 `yt` 和 `yt2` 的分量之间的最大相对差。一旦 `err` 降到 `eps` 以下，试验传播被接受，过程退出步长缩放循环。除了实际使用的步长 `ht` 之外，例程还通过 `ht1` 返回对下一次传播步骤步长的猜测。在任何情况下，步长增加超过 5 倍都被明确禁止。

实践中，通过使用两个共享相同定义系数的连续阶 `p` 和 `p + 1` 的嵌入求解器，而不是对单个常微分方程求解器进行步长减半，可以实现显著提高的效率。这种方案是龙格-库塔-费尔伯格方法（Fehlberg 1966, 1970），其中联合使用两个特定的 `O(h⁵)` 和 `O(h⁶)` 龙格-库塔方法：

```
ỹₘ₊₁ = yₘ + 25/216 k₁ + 1408/2565 k₃ + 2197/4104 k₄ − 1/5 k₅,   (12.49)

yₘ₊₁ = yₘ + 16/135 k₁ + 6656/12,825 k₃ + 28,561/56,430 k₄ − 9/50 k₅ + 2/55 k₆.   (12.50)
```

共同的定义系数为

```
k₁ = h f(tₘ, yₘ),   (12.51)

k₂ = h f( tₘ + 1/4 h, yₘ + 1/4 k₁ ),

k₃ = h f( tₘ + 3/8 h, yₘ + 3/32 k₁ + 9/32 k₂ ),

k₄ = h f( tₘ + 12/13 h, yₘ + 1932/2197 k₁ − 7200/2197 k₂ + 7296/2197 k₃ ),

k₅ = h f( tₘ + h, yₘ + 439/216 k₁ − 8 k₂ + 3680/513 k₃ − 845/4104 k₄ ),

k₆ = h f( tₘ + 1/2 h, yₘ − 8/27 k₁ + 2 k₂ − 3544/2565 k₃ + 1859/4104 k₄ − 11/40 k₅ ).
```

通过从公式 12.50 中减去公式 12.49 得到截断误差的估计：

```
Δₘ₊₁ = yₘ₊₁ − ỹₘ₊₁ = 1/360 k₁ − 128/4275 k₃ − 2197/75,240 k₄ + 1/50 k₅ + 2/55 k₆ + O(h⁶),   (12.52)
```
