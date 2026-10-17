
$$
u_{ij}^{(r)} = \left[ k_x \left( u_{i-1,j}^{(r)} + u_{i+1,j}^{(r-1)} \right) + k_y \left( u_{i,j-1}^{(r)} + u_{i,j+1}^{(r-1)} \right) - f_{ij} \right] / k_{xy},
$$

$$
i = i_{\min} + 1, \dots, i_{\max} + 1, \quad j = 2, \dots, N_y - 1. \tag{13.33}
$$

图 13.5 通过嵌入笛卡尔网格的类圆盘区域，以及离散化边界和相应的边界线索引，举例说明了非矩形积分域。

实现所述迭代过程的例程是`Poisson2D`（清单 13.4），其输入由通过数组`u`接收的解的初始近似组成，包括适当的边界值，离散化网格的坐标`x`和`y`，边界索引的数组`imin`和`imax`，两个笛卡尔方向的网格点数`nx`和`ny`，解分量的所需相对精度`eps`，以及计算泊松方程右端项的用户函数名称。与`PoissonXY`类似，`Poisson2D`执行 Gauss-Seidel 迭代以使解`u`收敛到所需精度。当解分量在两次连续迭代之间的最大相对变化降至容差`eps`以下时，解的迭代细化终止。

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_542_0.png)

FIGURE 13.5 Integration grid and bounding line indexes, `i_min` and `i_max`, for a disk-like integration domain. Filled circles represent boundary values and empty circles indicate values that need to be calculated.

### Listing 13.4 Solver for the 2D Poisson Equation on an Irregular Domain (Python Coding)

```python
# ============================================================================
# def Poisson2D(u, x, y, imin, imax, nx, ny, eps, Func):
# ----------------------------------------------------------------------------
# Solves the 2D Poisson equation in Cartesian coordinates on a regular grid
# with (nx x ny) nodes (x[],y[]), with limiting indexes along x specified by
# imin[j] and imax[j] (j=1,ny), using the Gauss-Seidel method. The solution
# u[][] is converged with relative precision eps.
# An error index is returned: 0 - normal execution.
# Calls: Func(x,y) - RHS of Poisson equation
# ----------------------------------------------------------------------------
    itmax = 10000                                      # max no. of iterations

    f = [[0]*(ny+1) for i in range(nx+1)]

    hx = (x[nx]-x[1])/(nx-1); kx = 1e0/(hx*hx)          # mesh spacings
    hy = (y[ny]-y[1])/(ny-1); ky = 1e0/(hy*hy)
    kxy = 2e0*(kx + ky)

    for j in range(2,ny):                              # RHS of PDE for interior points
        for i in range(2,nx): f[i][j] = Func(x[i],y[j])

    for it in range(1,itmax+1):                        # Gauss-Seidel iteration loop
        err = 0e0
        for j in range(2,ny):
            for i in range(imin[j]+1,imax[j]):         # interior mesh points
                uij = (kx*(u[i-1][j] + u[i+1][j]) - f[i][j]) / kxy
                if (i >= imin[j-1] and i <= imax[j-1]): uij += ky*u[i][j-1] / kxy
                if (i >= imin[j+1] and i <= imax[j+1]): uij += ky*u[i][j+1] / kxy

                eij = 1e0 - u[i][j]/uij if uij else uij - u[i][j]
                if (fabs(eij) > err): err = fabs(eij)      # max. component error
                u[i][j] = uij

        if (err <= eps): break                         # convergence test

    if (it >= itmax):
        print("Poisson2D: max. number of iterations exceeded!"); return 1
    return 0
```

作为静态热方程的应用，我们确定圆形导电盘上的温度分布，边界温度从左半圆的 100°C 递减到右半圆的 0°C。具体而言，我们求解拉普拉斯方程，

$$
\frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} = 0, \tag{13.34}
$$

在由正方形域 $D = [-a, a] \times [-a, a]$ 包围的圆盘上，其中 $a = 5$，受边界条件约束：

$$
u_{i,1}^{0} = 0, \quad i = i_{\min}^{1}, \dots, i_{\max}^{1}, \quad j = 1,
$$

$$
u_{i_{\min},j}^{0} = 100, \quad u_{i_{\max},j}^{(r)} = 0, \quad j = 2, \dots, N_{y} - 1, \tag{13.35}
$$

$$
u_{i,N_{y}}^{0} = 0, \quad i = i_{\min}^{N_{y}}, \dots, i_{\max}^{N_{y}}, \quad j = N_{y}.
$$

在清单 13.5 的实现中，用户函数`BoundCondEllipse`实际上可以处理更一般的椭圆域的情况，该域由 $N_x \times N_y$ 正则笛卡尔网格包围。该例程确定所有 $N_y$ 条水平网格线上的边界索引 $i_{\min}^{j}$ 和 $i_{\max}^{j}$，并将解的边界值分配给数组`u[][]`的适当分量。

函数`BoundCondEllipse`实际上并不接收积分域的几何范围，而是仅使用无量纲节点索引，将所有位置相对于无量纲椭圆中心坐标`x0`和`y0`关联。在每条网格线`j`上，该例程根据相对`y`坐标`yj`确定与椭圆边界的正`x`相交点`xi`，从而确定边界索引`imin[j]`和`imax[j]`。然后根据方程 13.35 基于这些索引初始化解的边界值。

主程序与清单 13.3 中的程序非常相似，它基本上初始化网格坐标，用有区别的值标记外部节点，使用例程`BoundCondEllipse`设置边界值，调用求解器`Poisson2D`计算内部解值，最后将解打印到文件中。

通过运行程序 13.5 得到温度分布的等高线图如图 13.6 所示。

### Listing 13.5 Solution of the Static Heat Problem of a Conducting Disk (Python Coding)

```python
# Steady-state temperature distribution in a thin conducting disk
from math import *
from pde import *

def Func(x, y):                     # RHS function for Poisson2D
    return 0e0
#==============================================================================
def BoundCondEllipse(u, imin, imax, nx, ny):
#------------------------------------------------------------------------------
# Determines the boundary indexes imin[j] and imax[j] (j=1,ny) for an
# elliptical domain, determined by the number of mesh points nx and ny, and
# sets values on the boundaries for the function u
#-------------------------------------------------------------------------------
    x0 = 0.5e0*(nx + 1e0)                    # center of dimensionless ellipse
    y0 = 0.5e0*(ny + 1e0)
    a = x0 - 1e0                             # semi-axes
    b = y0 - 1e0

    for j in range(1,ny+1):                  # boundary indexes
        yj = j - y0                          # relative y-coordinate
        xi = a * sqrt(1e0 - yj*yj/(b*b))     # x-coordinate on ellipse
        if (xi == 0e0): xi = 0.75e0          # correction for 1-point boundary

        imin[j] = int(x0 - xi + 0.5e0)       # left boundary index
        imax[j] = int(x0 + xi + 0.5e0)       # right boundary index

    # boundary values
    for i in range(imin[1],imax[1]+1): u[i][1] = 0e0   # bottom
    for j in range(2,ny):
        u[imin[j]][j] = 100e0                # left
        u[imax[j]][j] = 0e0                  # right
    for i in range(imin[ny],imax[ny]+1): u[i][ny] = 0e0   # top

#### main

a = 5                                    # disk radius
xmin = -a; xmax = a; ymin = -a; ymax = a  # domain boundaries
nx = 51; ny = 51                         # number of mesh points
eps = 1e-5                               # relative solution tolerance

u = [[0]*(ny+1) for i in range(nx+1)]   # solution
x = [0]*(nx+1); y = [0]*(ny+1)           # mesh point coordinates
imin = [0]*(ny+1)                        # indexes of y-line boundaries
imax = [0]*(ny+1)

hx = (xmax-xmin)/(nx-1)
for i in range(1,nx+1): x[i] = xmin + (i-1)*hx   # x-mesh points
hy = (ymax-ymin)/(ny-1)
for j in range(1,ny+1): y[j] = ymin + (j-1)*hy;   # y-mesh points

for j in range(1,ny+1):                  # initialize solution
    for i in range(1,nx+1): u[i][j] = -1e99

BoundCondEllipse(u,imin,imax,nx,ny)      # boundary values

for j in range(2,ny):                    # initial approximation of the solution
    for i in range(imin[j]+1,imax[j]): u[i][j] = 0e0   # interior nodes

Poisson2D(u,x,y,imin,imax,nx,ny,eps,Func)

out = open("Poisson.txt","w")          # open output file
out.write("      x            y            u\n")
for j in range(1,ny+1):
    for i in range(1,nx+1):
        out.write(("{0:10.5f}{1:10.5f}{2:14.5e}\n").format(x[i],y[j],u[i][j]))
out.close()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_545_0.png)

**图 13.6** 通过程序 13.3 求解静态热问题 (13.34)–(13.35) 得到的一块导电盘的温度分布。

## 13.3 抛物型微分方程的初值问题

科学与工程提供了大量抛物型偏微分方程问题的例子。作为抛物型偏微分方程的原型，我们下面讨论的是 1D 扩散方程，或形式上相似的热方程。尽管如此，所应用的离散化技术以及相关的稳定性分析具有普遍的适用性，也可应用于其他抛物型方程。

尽管扩散方程存在相当数量的解析解，但这些解仅限于简单的几何形状和分段常数的扩散系数。解析上可处理的边界条件同样简单；然而，解通常表示为无穷级数，其求值绝非微不足道。另一方面，存在大量实际问题，对于这些问题，为实现精确可解而所需的简化假设在不可接受的程度上影响了物理模型的本质。

为了获得能够真实模拟实际状况的扩散方程解，通常需要求助于数值算法。基本上，这些算法将解限制在离散的网格点集合上，并用相对于这些点的有限差分格式近似导数。随后，数值方法归结为求解由此得到的线性系统，其未知量是网格点处的解值。

1D 扩散和热方程，

$$
\frac{\partial u}{\partial t} - D\frac{\partial^2 u}{\partial x^2} = 0, \tag{13.36}
$$

$$
\frac{\partial u}{\partial t} - K\frac{\partial^2 u}{\partial x^2} = f(x,t), \tag{13.37}
$$

分别描述了扩散物质浓度 $u(x,t) \equiv c(x,t)$ 的时间演化与空间分布，以及系统的温度 $u(x,t) \equiv T(x,t)$。扩散系数 $D$ 根据菲克定律将扩散通量 $J_{\text{diff}}$ 与浓度梯度联系起来，而热扩散率 $K$ 根据傅里叶定律将热通量 $J_{\text{heat}}$ 与温度梯度联系起来：

$$
J_{\text{diff}} = -D \frac{\partial c}{\partial x}, \quad J_{\text{heat}} = -K \frac{\partial T}{\partial x}.
$$

上述热方程的形式也考虑了热源 $f(x,t)$。

尽管这两个方程看起来是空间 1D 的，但作为替代，它们也可以被假定为模拟 3D 平面“平板”几何，其中仅显式依赖于垂直于平板的笛卡尔坐标 $x$，而对另外两个坐标 $y$ 和 $z$ 无依赖，沿这两个坐标系统的延伸被隐式地认为是无限的。

对特定物理情况的建模，除了实际的偏微分方程外，还需要提供 *初始* 和 *边界条件*。*初始条件* 指定在某个初始时刻 $t_0$ 时整个空间域上的解：
