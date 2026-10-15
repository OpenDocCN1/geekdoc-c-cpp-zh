

在此，同样引入记号

```
$$\lambda = \left(\frac{c h_t}{h_x}\right)^2, \tag{13.131}$$
```

则可将时间步 $t_{n+1}$ 处所有内部网格点 $x_i$ 的传播解用前两个时间步 $t_n$ 和 $t_{n-1}$ 的值表示为：

```
$$u_i^{n+1} = \lambda u_{i-1}^n + 2\,(1-\lambda)\,u_i^n + \lambda u_{i+1}^n - u_i^{n-1}, \tag{13.132}$$ $$i = 2,3,\dots,N_x-1.$$
```

至于边界值，根据狄利克雷条件，它们在整个传播过程中保持不变，这可以简单地表示为

```
$$u_1^{n+1} = u_1^n,\quad u_{N_x}^{n+1} = u_{N_x}^n. \tag{13.133}$$
```

用矩阵记号，系统13.132–13.133可写成如下形式：

```
$$\mathbf{u}^{n+1} = \mathbf{B}\cdot\mathbf{u}^n - \mathbf{u}^{n-1},\quad n = 0,1,2,\dots, \tag{13.134}$$
```

其中

```
$$\mathbf{B} = \begin{bmatrix}1 & 0 & & & 0 \\ \lambda & 1-2\lambda & \lambda & & \\ & \ddots & \ddots & \ddots & \\ & & \lambda & 1-2\lambda & \lambda \\ 0 & & & 0 & 1\end{bmatrix},\quad \mathbf{u}^n = \begin{bmatrix}u_1^n \\ u_2^n \\ \vdots \\ u_{N_x-1}^n \\ u_{N_x}^n\end{bmatrix}, \tag{13.135}$$
```

且传播矩阵 $\mathbf{B}$ 具有三对角结构。

由于传播解 $\mathbf{u}^{n+1}$ 的各个分量可以独立表达，该方法被称为显式方法，它与第13.3.1节为扩散方程发展的显式FTCS方法本质上是类似的。

尽管形式上相似，但抛物型和双曲型偏微分方程的显式方法之间仍然存在一个不可忽视的差别：后者中除了前一个解 $\mathbf{u}^n$ 之外，还出现了再前一个解 $\mathbf{u}^{n-1}$。一旦传播开始，这一方面可以通过持续存储最近的两个解来轻松处理。

一个较为敏感的方面是传播的启动。事实上，除了初始解 $\mathbf{u}^0$ 之外，还需要提供第一个传播解 $\mathbf{u}^1$，而不是一阶时间导数 $\partial\mathbf{u}^0/\partial t$。一种保持方法整体二阶精度的有效做法是从解分量关于时间的泰勒级数展开开始：

```
$$u_i^{n+1} = u_i^n + h_t\left(\frac{\partial u}{\partial t}\right)_{i,n} + \frac{1}{2}h_t^2\left(\frac{\partial^2 u}{\partial t^2}\right)_{i,n} + O(h_t^3).$$
```

特别地，对于第一个传播步，我们有：

```
$$u_i^1 = u_i^0 + h_t\left(\frac{\partial u}{\partial t}\right)_{i,0} + \frac{1}{2}h_t^2\left(\frac{\partial^2 u}{\partial t^2}\right)_{i,0} + O(h_t^3).$$
```

虽然一阶时间导数可以从初始条件(13.124)直接得到，但二阶导数可以利用波动方程(13.122)替换为二阶空间导数：

```
u_i^1 = u_i^0 + h_t v_i^0 + 1/2 h_t^2 c^2 (∂²u/∂x²)_{i,0} + O(h_t^3),
```

其中 v_i^0 = v^0(x_i)。对于二阶空间导数，我们现在可以采用与前面相同的二阶格式(13.5)：

```
u_i^1 = u_i^0 + h_t v_i^0 + 1/2 h_t^2 c^2 (u_{i+1}^0 - 2u_i^0 + u_{i-1}^0)/h_x^2 + O(h_t^3 + h_x^2).
```

引入参数 λ，我们最终得到第一个传播解 u^1 的分量用初始解 u^0 和初始时间导数 v^0 表示的表达式：

```
u_i^1 = 1/2 λ u_{i-1}^0 + (1 - λ) u_i^0 + 1/2 λ u_{i+1}^0 + h_t v_i^0,  i = 2,3,...,N_x - 1.  (13.136)
```

根据von Neumann稳定性分析的一般方法，我们将一般的特征模态 ε_i^n = ξ(k)^n exp(i k i h_x) 作为解代入差分方程(13.132)，得到：

```
ξ = [λ exp(-i k h_x) + 2(1 - λ) + λ exp(i k h_x)] ξ - ξ^{-1}.
```

将指数项合并为 2λ cos(k h_x)，并利用恒等式 1 - cos x = 2 sin²(x/2)，放大因子满足：

```
1/2 (ξ + ξ^{-1}) = 1 - 2λ sin²(k h_x / 2).  (13.137)
```

由于右端是实数，ξ + ξ^{-1} 也必须是实数。这要求 |ξ| = |ξ|^{-1}，从而得到

```
1/2 (ξ + ξ^{-1}) = |ξ| cos φ,
```

其中 φ 是任意相位。考虑到稳定性条件 |ξ| < 1，上述关系对方程13.137的右端施加了如下限制：

```
-1 ≤ 1 - 2λ sin²(k h_x / 2) ≤ 1,
```

这只有在以下条件下才能满足：

```
0 ≤ λ ≤ 1.  (13.138)
```

鉴于 λ 的定义(13.131)，基于显式差分格式(13.132)-(13.133)的波函数 u(x,t) 传播的稳定性条件为：

```
h_t ≤ h_x / c.  (13.139)
```

例程 PropagWave（清单13.16）采用算法13.131-13.133来求解波动方程13.122的一个基本柯西问题，在时间间隔 ht 上传播两个初始解 u0[] 和 u1[]。常数相速度 c、空间步长 h_x 和空间节点数 N_x 分别通过参数 c、hx 和 nx 传递给例程。

传播后的解在数组 u[] 中返回。

主程序中的驱动传播循环应向后移动数组 u[]、u1[] 和 u0[] 的内容，以腾出 u[] 为新的传播步骤做准备。

求解一维波动方程的典型主程序如清单13.17所示。程序首先通过调用用户函数 Init 获取两个初始解 u0[] 和 u1[]。

## 清单13.16 经典波动方程的显式传播器（Python代码）

```
#================================================================================
def PropagWave(u0, u1, u, nx, c, hx, ht):
#--------------------------------------------------------------------------------
#   Propagates the solutions u0[] and u1[] of the wave equation
#   d2u/dt2 = c^2 d2u/dx2,  c - phase velocity (constant)
#   over the time interval ht, using the explicit difference scheme on a
#   spatial grid with nx nodes and spacing hx. Returns the solution in u[].
#--------------------------------------------------------------------------------
    lam = c*ht/hx; lam = lam*lam
    lam2 = 2e0*(1e0 - lam)
    u[1] = u0[1]; u[nx] = u0[nx]                     # Dirichlet boundary conditions
    for i in range(2,nx):                           # propagate solution at interior points
        u[i] = lam*u1[i-1] + lam2*u1[i] + lam*u1[i+1] - u0[i]
```

## 清单13.17 经典波动方程的有限差分求解（Python代码）

```
# Solve 1D wave equation by the explicit finite-difference method
from math import *
from pde import *
from graphlib import *

#================================================================================
def Init(u0, u1, x, nx, c, dk, hx, ht):
#--------------------------------------------------------------------------------
#   Returns initial solutions u0 and u1, for the first two time steps
#       u0(x,0) = sin(x*dk) / (x*dk)                         initial solution
#       v0(x,0) = 0                                         initial time derivative
#   x - spatial mesh, nx - number of nodes
#   c - phase velocity of wave, dk - wave number interval
#   hx - x-spacing, ht - time step size
#--------------------------------------------------------------------------------
    for i in range(1,nx+1):                                 # time step 0
        u0[i] = sin(dk*x[i])/(dk*x[i]) if dk*x[i] else 1e0   # initial solution
    lam = c*ht/hx; lam = lam*lam                             # time step 1
    lam2 = 2e0*(1e0 - lam)
    u1[1] = u0[1]; u1[nx] = u0[nx]                           # constant boundary values
    for i in range(2,nx):
        v0 = 0e0                                            # initial time derivative
        u1[i] = 0.5e0*(lam*u0[i-1] + lam2*u0[i] + lam*u0[i+1]) - ht*v0

# main
c    = 10e0                                             # phase speed of wave
dk   = 1e0                                              # wave number interval
xmax = 100e0                                            # maximum x
hx   = 5e-2                                             # spatial step size
```

