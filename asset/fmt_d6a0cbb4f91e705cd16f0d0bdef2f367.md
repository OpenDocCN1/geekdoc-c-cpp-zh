
y'ₘ 的高阶近似可由泰勒展开式 (12.97) 和 (12.98) 相减得到，其中显式忽略三阶项 (h³/6) yₘ⁽³⁾，而二阶项 (h²/2) y''ₘ 则完全抵消：

y'ₘ = (yₘ₊₁ − yₘ₋₁)/(2h) + O(h²).  (12.100)

该中心差分公式利用关于求导点 xₘ 对称分布的网格点信息。同样，最终除以 h 会使格式的阶数降低 1。

将泰勒展开式 (12.97) 和 (12.98) 相加，一阶项 h y'ₘ 和三阶项 (h³/6) yₘ⁽³⁾ 恰好抵消，得到如下二阶导数的中心差分格式：

$$y''_m = \frac{y_{m+1} - 2y_m + y_{m-1}}{h^2} + O(h^2), \tag{12.101}$$

由于最终除以 $h^2$，其精度为 $O(h^2)$。

将中心差分格式应用于离散化的线性两点问题，会得到具有对称带状矩阵的线性方程组，这对后续求解方法的稳定性产生积极影响。利用 $O(h^2)$ 中心差分公式 12.100 和 12.101 对常微分方程 12.93 进行离散化，并使用公式 12.99 来近似边界条件 12.94，我们得到以下线性方程组：

```
\begin{cases}
\displaystyle \frac{y_{m+1} - 2y_m + y_{m-1}}{h^2} = p_m \frac{y_{m+1} - y_{m-1}}{2h} + q_m y_m + r_m, \\
m = 2,3,\dots,M-1, \\
\alpha_1 y_1 + \beta_1 \frac{y_2 - y_1}{h} = 1, \\
\alpha_2 y_M + \beta_2 \frac{y_M - y_{M-1}}{h} = 1.
\end{cases}
```

对未知解值 $y_m$ 重新组合后，与两点边值问题 12.93–12.94 对应的离散化线性方程组具有如下形式：

```
\begin{cases}
(h\alpha_1 - \beta_1) y_1 + \beta_1 y_2 = h, \\
-\left(2 + h p_m\right) y_{m-1} + \left(4 + 2h^2 q_m\right) y_m - \left(2 - h p_m\right) y_{m+1} = -2h^2 r_m, \\
m = 2,3,\dots,M-1, \\
-\beta_2 y_{M-1} + (h\alpha_2 + \beta_2) y_M = h.
\end{cases} \tag{12.102}
```

值得注意的是，该方程组具有三对角矩阵，最终可表示为

```
\begin{bmatrix}
b_1 & c_1 & & & \\
a_2 & b_2 & c_2 & & 0 \\
 & \ddots & \ddots & \ddots & \\
 & & a_m & b_m & c_m \\
 & & & \ddots & \ddots & \ddots \\
0 & & & a_{M-1} & b_{M-1} & c_{M-1} \\
 & & & & a_M & b_M
\end{bmatrix}
\begin{bmatrix} y_1 \\ y_2 \\ \vdots \\ y_m \\ \vdots \\ y_{M-1} \\ y_M \end{bmatrix}
= \begin{bmatrix} d_1 \\ d_2 \\ \vdots \\ d_m \\ \vdots \\ d_{M-1} \\ d_M \end{bmatrix}, \tag{12.103}
```

其非零元素的表达式为：

```
\begin{aligned}
b_1 = h\alpha_1 - \beta_1, \quad c_1 = \beta_1, \quad d_1 = h, \\
\begin{cases}
a_m = -\left(2 + h p_m\right), & m = 2,3,\dots,M-1, \\
b_m = 4 + 2h^2 q_m, \\
c_m = -\left(2 - h p_m\right), \\
d_m = -2h^2 r_m,
\end{cases} \tag{12.104} \\
a_M = -\beta_2, \quad b_M = h\alpha_2 + \beta_2, \quad d_M = h.
\end{aligned}
```

清单 12.18 中的 `Bilocal` 例程演示了上述有限差分算法的实现。该函数接收以下输入数据：解的定义域边界 `xa` 和 `xb`、空间网格点数量 `nx`，以及定义边界条件的四个系数 `alf1`、`bet1`、`alf2` 和 `bet2`。定义常微分方程的函数 `p(x)`、`q(x)` 和 `r(x)` 的值由用户函数 `Func` 通过参数 `p`、`q` 和 `r` 分别返回。

## 清单12.18 基于有限差分法的线性双点问题求解器（Python 编码）

```
#================================================================================
def Bilocal(xa, xb, y, nx, alf1, bet1, alf2, bet2, Func):
#--------------------------------------------------------------------------------
#   Solves a linear two-point boundary-value problem for a 2nd order ODE
#       y'' = p(x) y' + q(x) y + r(x),   xa <= x <= xb
#       alf1 y(xa) + bet1 y'(xa) = 1
#       alf2 y(xa) + bet2 y'(xa) = 1
#   on a regular mesh with nx points, using central finite-differences.
#   Returns the solution in y[].
#   Calls: Func(x, p, q, r) - returns values of p(x), q(x), r(x)
#          TriDiagSys (linsys.py) - solves discretized tridiagonal system
#--------------------------------------------------------------------------------
a = [0]*(nx+1); b = [0]*(nx+1); c = [0]*(nx+1)               # matrix elements

hx = (xb-xa)/(nx-1); h2 = 2e0*hx*hx

b[1] = hx*alf1 - bet1; c[1] = bet1; y[1] = hx                 # build system coefficients
for m in range (2,nx):
    x = xa + (m-1)*hx                                        # mesh point
    (p,q,r) = Func(x)
    a[m] = -(2e0 + hx*p); b[m] = 4e0 + h2*q; c[m] = -(2e0 - hx*p)
    y[m] = -h2*r                                            # RHSs of tridiagonal system
a[nx] = -bet2; b[nx] = hx*alf2 + bet2; y[nx] = hx

TriDiagSys(a,b,c,y,nx)                                       # solve discretized system
```

r. 解决系统(12.103)–(12.104)最有效的方法是采用LU分解法，该方法适用于三对角矩阵系统，已在7.7节中介绍，并以`TriDiagSys`例程（包含在`linsys.py`和`linsys.h`库中）编码实现。基于输入，`Bilocal`计算离散化系统的系数，将其传递给`TriDiagSys`例程以实际求解离散化系统，并将解`y[]`返回给调用程序。

为了说明问题，我们考虑勒让德多项式的相同双点问题，这一问题在打靶法的背景下也已讨论过：

d²Pₙ/dx² = 1/(1−x²) [ 2x dPₙ/dx − n(n+1)Pₙ ] ,  (12.105)

Pₙ(−1) = (−1)ⁿ,   Pₙ(1) = 1.  (12.106)

定义该常微分方程右端函数在此情况下为：

p(x) = x/(1−x²),   q(x) = −n(n+1)/(1−x²),   r(x) = 0,   (12.107)

并且狄利克雷边界条件由以下系数表征：

α₁ = (−1)ⁿ,   β₁ = 0,

α₂ = 1,       β₂ = 0.   (12.108)

程序12.19针对n = 5求解此问题，实现了用户函数`Func`，用于返回函数`p(x)`、`q(x)`和`r(x)`的值。通过使用（相当大的）空间网格间距h = 0.1和h = 0.01运行代码所获得的解，在图12.9中与打靶法（程序12.15）所得的解进行了比较。对于h = 0.1，打靶法明显失败

## 清单12.19 用有限差分法计算勒让德多项式（Python 编码）

```
# Legendre polynomials by the finite-difference method
from math import *
from ode import *
from specfunc import *

global n                                    # polynomial order
def Func(x):                                # RHS of Legendre ODE
    p = 2e0*x/(1e0-x*x); q = -n*(n+1)/(1e0-x*x); r = 0e0
    return (p, q, r)

#### main

n = 5                                       # order of Legendre polynomial
xa = -1e0; xb = 1e0                         # domain boundaries
hx = 1e-3                                   # x-mesh step size

nx = int((xb-xa)/hx + 0.5) + 1              # number of x-mesh points

x = [0]*(nx+1); y = [0]*(nx+1)              # x-mesh, solution

for m in range(1,nx+1): x[m] = xa + (m-1)*hx    # generate x-mesh

alf1 = -1e0 if n % 2 else 1e0; bet1 = 0e0       # Dirichlet conditions
alf2 = 1e0; bet2 = 0e0

Bilocal(xa,xb,y,nx,alf1,bet1,alf2,bet2,Func)

out = open("bilocal.txt","w")
out.write("    x          P{0:1d}          err\n".format(n))
for m in range(1,nx+1):
    (P, d) = Legendre(n,x[m])
    out.write("{0:10.5f}{1:10.5f}{2:10.5f}\n".format(x[m],y[m],P-y[m]))
out.close()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_490_0.png)

图12.9 对于n = 5阶勒让德多项式的两点问题，分别采用有限差分法（虚线）和打靶法（点划线）所得的解，对应于空间网格间距h = 0.1（左图）和h = 0.01（右图）。作为参考，精确勒让德多项式P5(x)用实线绘出。

无法遵循解析依赖关系（P₅(x)），尽管解满足边界条件。对于h = 0.01，有限差分法提供的解与精确解变得不可区分，而打靶法的吻合度则显著改善。

## 12.10 C/C++ 实现

清单12.20显示了文件`ode.h`的内容，其中包含了正文中开发的Python函数（收录在模块`ode.py`中）的等效C/C++实现。相应的例程具有相同的名称、参数和功能。

### 清单12.20 常微分方程组柯西问题和两点问题的求解器（ode.h）
