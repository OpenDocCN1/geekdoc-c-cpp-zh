

传播步数，开始主导解，解不再因 h 进一步减小而改善，低于某一值时不再改善。

克服欧拉方法精度低的一种实用方法是提高近似的阶数，通过应用其变体称为预测-校正欧拉方法，该方法在每个传播步中操作两个解估计：

ỹ_{m+1} = y_m + h f(t_m, y_m),  m = 0,1,2,…, (12.17)
y_{m+1} = y_m + h/2 [f(t_m, y_m) + f(t_m + h, ỹ_{m+1})]. (12.18)

预测解 ỹ_{m+1} 按基本欧拉方法计算，由预测公式 12.17 得到，并用于预测传播导数 f(t_m + h, ỹ_{m+1})。校正解 y_{m+1} 然后基于校正公式 12.18 得到，该公式采用区间 [t_m, t_{m+1}] 上的预测平均导数，即 [f(t_m, y_m) + f(t_m + h, ỹ_{m+1})]/2。

在第 12.4 节中，基本欧拉方法和预测-校正欧拉方法都被证明是已知为 Runge–Kutta 方法的整个算法族的特例。基本欧拉方法等价于一阶 Runge–Kutta 方法，而预测-校正欧拉算法为 O(h²)，等价于二阶 Runge–Kutta 方法。预测-校正欧拉算法的优越精度显然以双倍的 ODE 右端函数 f(x,y) 的求值次数为代价。

欧拉方法在其基本和预测-校正变体中已在函数 Euler 和分别 EulerPC 中实现，如清单 12.1 所示。

## 清单 12.1 Euler 和 Euler 预测-校正 ODE 求解器（Python 编码）

```
# =================================================================================
def Euler(t, ht, y, n, Func):
# --------------------------------------------------------------------------------
#   Propagates the solution y of a system of 1st order ODEs
#     y'[i] = f[i](t,y[]), i = 1..n
#   from t to t+ht using Euler's method
#   Calls: Func(t, y, f) - RHS of ODEs
# --------------------------------------------------------------------------------
    f = [0]*(n+1)                                   # RHS of ODEs
    Func(t,y,f)                                     # get RHS of ODEs
    for i in range(1,n+1): y[i] += ht * f[i]        # propagate solution
# =================================================================================
def EulerPC(t, ht, y, n, Func):
# --------------------------------------------------------------------------------
#   Propagates the solution y of a system of 1st order ODEs
#     y'[i] = f[i](t,y[]), i = 1..n
#   from t to t+ht using Euler's predictor-corrector method
#   Calls: Func(t, y, f) - RHS of ODEs
# --------------------------------------------------------------------------------
    f1 = [0]*(n+1); f2 = [0]*(n+1)                   # RHS of ODEs
    yt = [0]*(n+1)                                  # predicted solution
    Func(t,y,f1)                                    # RHS of ODEs at t
    for i in range(1,n+1): yt[i] = y[i] + ht * f1[i] # predictor
    Func(t+ht,yt,f2)                                # RHS of ODEs at t+ht
    ht2 = ht/2e0
    for i in range(1,n+1): y[i] += ht2 * (f1[i] + f2[i]) # corrector
```

为了说明所讨论的欧拉方法的精度和稳定性，让我们考虑线性二阶 ODE 的柯西问题：

y'' + y = 0,  (12.19)
y(0) = y0,    y'(0) = y0'.  (12.20)

该问题的通解为 y(t) = A sin t + B cos t 并且特定常数取决于特定初始值 y0 和 y0'。根据本章引言中描述的方法，通过记号

y1 ≡ y,    y2 ≡ y',

所考虑的柯西问题可以写成形式：

{ y1' = y2,    { y1(0) = y0,
  y2' = -y1,     y2(0) = y0'.  (12.21)

设计用于求解问题 12.21 的程序（清单 12.2）在用户函数 Func 中定义 ODE 的右端。所采用的求解器 Euler 和 EulerPC 从

## 清单 12.2  用欧拉方法求解 ODE 系统的柯西问题（Python 编码）

```
# Solves a Cauchy problem for a 2nd order ODE by Euler's method
# y'' + y = 0,  y(0) = y0, y'(0) = y0'
# Equivalent problem: y[1] = y, y[2] = y'
#     y[1]' = y[2],    y[1](0) = y0
#     y[2]' = -y[1],   y[2](0) = y0'
#-----------------------------------------------------------------
from math import *
from ode import *

def Func(t, y, f):                     # Right-hand sides of ODEs
    f[1] = y[2]
    f[2] = -y[1]

# main

y0 = 0e0; dy0 = 1e0                     # initial values => y(t) = sin(t)
tmax = 100e0                           # time span
ht = 0.05e0                            # step size

n = 2                                  # number of 1st order ODEs
y = [0]*(n+1)                          # solution components

out = open("ode.txt","w")            # open output file
out.write("      t        y1        y2      check\n")

t = 0e0
y[1] = y0; y[2] = dy0                   # initial values
out.write(("{0:10.5f}{1:10.5f}{2:10.5f}{3:10.5f}\n"). \
          format(t,y[1],y[2],y[1]*y[1]+y[2]*y[2]))

while (t+ht <= tmax):                  # propagation loop
    Euler(t,ht,y,n,Func)
    t += ht

    out.write(("{0:10.5f}{1:10.5f}{2:10.5f}{3:10.5f}\n"). \
              format(t,y[1],y[2],y[1]*y[1]+y[2]*y[2]))
out.close()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_454_0.png)

**图 12.2** 欧拉方法（左图）和预测-校正欧拉方法（右图）对柯西问题 12.21–12.22 在传播步长 $h = 0.05$ 下得到的数值解。

库 ode.py（分别为 C/C++ 编码的 ode.h）导入。程序实现了一个特征的 while-do 传播循环，该循环反复调用求解器以在基本时间间隔 ht 上传播解，同时负责推进当前时间。

问题 12.21 在初始值特定情况下的精确解

$y_1(0)=0,\quad y_2(0)=1,$  (12.22)

是

$y_1(t)=\sin t,\quad y_2(t)=\cos t,$

并且可以很容易地与程序产生的数值输出进行比较。关于数值稳定性的更具说服力的指示由一个解分量对另一个解分量的依赖提供，具体而言，由 $y_1$ 对 $y_2$ 的作图提供。在稳定传播的情况下，曲线 $y_1=y_1(y_2)$ 预期为半径为 1 的闭合圆。

正如图 12.2 所示，该图描绘了在时间跨度 $t_{\max}=100$ 上、传播步长 $h=0.05$ 下得到的轮廓演化，基本欧拉方法（左图）产生的解逐渐偏离预期的圆形行为，而根据接近 1 的半径的闭合曲线判断，预测-校正欧拉方法（右图）表现出合理的稳定性和精度。基本欧拉方法仅在步长小 50 倍时，即 $h=0.001$ 时，才能达到与预测-校正算法相当的稳定程度。

## 12.4 Runge–Kutta 方法

Runge–Kutta 方法代表了一整族用于数值求解一阶 ODE 或其系统初值问题的算法。它们最初由 C. Runge 开发，他在 1895 年的开创性论文中发表了该类型的前几个格式（Runge 1895），而 W. Kutta 将该类方法扩展到 5 阶（Kutta 1901）。由于其可靠性和鲁棒性，Runge–Kutta 方法已获得数值积分 ODE 的标准、通用方法的地位。

Runge–Kutta 算法是自启动单步方法，仅需要求值 ODE 的右端，而不需要其导数。根据通用约定，

p 阶方法提供与对应 Taylor 级数的 O(h^p) 近似相吻合的解。阶数的增加自然伴随着更高的精度，但也伴随着实现复杂性的增加。

让我们考虑一阶 ODE 或 ODE 系统的一般柯西问题：

$$y' = f(t,y), \qquad y(t_0)=y_0.$$  (12.23)

解 y(t) 从 t_m 到 t_{m+1} 的传播可以如第 12.2 节所述通过应用 Taylor 展开来完成

$$y_{m+1}=y_m+hf(t_m,y_m)+\frac{h^2}{2}\left[\frac{\partial f}{\partial t}+f\frac{\partial f}{\partial y}\right]_{t_m,y_m}+\cdots$$  (12.24)

为了提高精度而在该级数中保留大量项是不切实际的，因为右端函数 f(t,y) 所涉及的导数的复杂性迅速增加。Runge–Kutta 方法遵循另一种主导思想：构造仅依赖于 f(t,y) 的值而非其导数的求解器，并且其在 h 中的幂级数表示应与精确展开式 (12.24) 在最高可能项上等价，而与特定的函数 f(t,y) 无关。

我们将 y_{m+1} 表示为线性组合：

$$y_{m+1}=y_m+\sum_{i=1}^{p}w_i k_i.$$  (12.25)

其中 w_i 为权重且 k_i 取值与 f(t,y) 成比例，

$$k_i=hf(\xi_i,\eta_i),$$

对于 p 个来自 t_m 和 y_m 附近的特定参数对：

$$\begin{cases}
\xi_i=t_m+\alpha_i h,\\
\eta_i=y_m+\displaystyle\sum_{j=1}^{i-1}\beta_{ij}k_j.
\end{cases}$$  (12.26)

α_i、β_ij 和 w_i 是可调参数，需要确定以最大化线性组合 (12.25) 与 Taylor 级数 (12.24) 之间的吻合度。在不失一般性的情况下，可以在所有情况下考虑：

$$\alpha_1=0,\qquad \beta_{11}=0,\qquad \xi_1=t_m,\qquad \eta_1=y_m.$$  (12.27)

这保证了 hf(t_m,y_m) 总是任何 Runge–Kutta 传播子 (12.25) 中的第一项。我们则有：

$$\begin{cases}
k_1=hf(t_m,y_m),\\
k_2=hf(t_m+\alpha_2h,y_m+\beta_{21}k_1),\\
k_3=hf(t_m+\alpha_3h,y_m+\beta_{31}k_1+\beta_{32}k_2),\\
\cdots
\end{cases}$$  (12.28)

上述关系揭示了 Runge–Kutta 方法的显式算法特性，意味着各种量仅基于已可用的量以直接方式计算。

