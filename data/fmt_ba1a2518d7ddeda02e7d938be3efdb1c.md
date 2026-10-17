
# 调用：`Numerov(V, x, y, nx, y0, dy0, E)`

```
//-------------------------------------------------------------

{

    const int itmax = 100;                         // max. no. of bisections

    double E, f, f1, f2;

    int inf, it;

    inf = Numerov(E1,V,x,y,nx,y0,dy0);             // propagate y for E1

    f1 = y[inf];                                   // asymptotic y

    inf = Numerov(E2,V,x,y,nx,y0,dy0);             // propagate y for E2

    f2 = y[inf];                                   // asymptotic y

    if (f1*f2 < 0) {                               //check if exists E in [E1,E2]

        exist = 1;

        for (it=1; it<=itmax; it++) {              //refine E by bisection

            E = 0.5e0*(E1 + E2);                   //new approximation

            inf = Numerov(E,V,x,y,nx,y0,dy0);      //propagate y

            f = y[inf];                            // asymptotic y

            if (f1*f > 0) E1 = E; else E2 = E;      //new semi interval

            if (fabs(y[nc]) <= eps) break;         //check if y vanishes at x[nc] ?

        }

        if (it >= itmax) printf("ShootQM: max. no. of bisections exceeded!\n");

    } else

    { E = 1e10; exist = 0; }

    return E;

}

//================================================================================

void Bilocal(double xa, double xb, double y[], int nx,

             double alf1, double bet1, double alf2, double bet2,

             void Func(double, double&, double&, double&))

//--------------------------------------------------------------------------------

// Solves a linear two-point boundary-value problem for a 2nd order ODE

//     y'' = p(x) y' + q(x) y + r(x),   xa <= x <= xb

//     alf1 y(xa) + bet1 y'(xa) = 1

//     alf2 y(xb) + bet2 y'(xb) = 1

// on a regular mesh with nx points, using central finite-differences.

// Returns the solution in y[].

// Calls: Func(x, p, q, r) - returns values of p(x), q(x), r(x)

//        TriDiagSys (linsys.h) - solves discretized tridiagonal system

//--------------------------------------------------------------------------------

{

    double *a, *b, *c;

    double hx, h2, p, q, r, x;

    int m;

    a = Vector(1,nx); b = Vector(1,nx); c = Vector(1,nx);   // matrix elements

    hx = (xb-xa)/(nx-1); h2 = 2e0*hx*hx;

    b[1] = hx*alf1 - bet1; c[1] = bet1; y[1] = hx;            // build system coefficients

    for (m=2; m<=nx-1; m++) {

        x = xa + (m-1)*hx;                                   // mesh point

        Func(x,p,q,r);

        a[m] = -(2e0 + hx*p); b[m] = 4e0 + h2*q; c[m] = -(2e0 - hx*p);

        y[m] = -h2*r;                                        // RHSs of tridiagonal system

    }

    a[nx] = -bet2; b[nx] = hx*alf2 + bet2; y[nx] = hx;

TriDiagSys(a,b,c,y,nx);        // solve discretized system

FreeVector(a,1); FreeVector(b,1); FreeVector(c,1);

}

#endif
```

## 12.11 问题

以下问题的 Python 和 C/C++ 程序可以从本章开发的模块 `ode.py` 和 `ode.h` 中导入函数，这些模块作为补充材料提供。用于创建运行时绘图的图形例程可使用库 `graphlib.py` 和 `graphlib.h`。

### 问题 12.1

考虑柯西问题：

`y'' + y = 0`,    (12.109)

`y(0) = 0`,   `y'(0) = 1`.    (12.110)

先将 ODE 化为一阶 ODE 系统的形式，然后通过比较使用欧拉方法和欧拉预测-校正方法求解等价问题，直至 `t_max = 100`，将步长从 `h = 0.05` 减小到 `h = 0.001`。绘制依赖关系 `y' = y'(y)` 并估计基本欧拉方法开始变得稳定的 `h` 值。

#### 解

Python 实现见列表 12.21，C/C++ 版本作为补充材料提供（`P12-ODEg.cpp`）。应用欧拉和欧拉预测-校正算法时 `h = 0.05` 的结果图如图 12.10 所示。

#### 列表 12.21 用欧拉方法求解二阶 ODE 的柯西问题（Python 编码）

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_501_0.png)

图 12.10 对于柯西问题 (12.109)–(12.110) 步长 `h = 0.05` 时，欧拉（左）和欧拉预测-校正方法（右）所得解。

```
#  Solves a Cauchy problem for a 2nd order ODE by Euler's method
#      y'' + y = 0,   y(0) = y0, y'(0) = y0'
from math import *
from ode import *
from graphlib import *

def Func(t, y, f):                         # RHSs of 1st order ODEs
    f[1] = y[2]                            # y[1] = y, y[2] = y'
    f[2] = -y[1]

#### main

y0 = 0e0; dy0 = 1e0                        # initial values => y(t) = sin(t)
tmax = 100e0                               # time span
ht = 0.05e0                                # step size

n = 2                                      # number of 1st order ODEs
nt = int(tmax/ht + 0.5) + 1                # number of time steps
y = [0]*(n+1)                              # solution components
y1 = [0]*(nt+1); y2 = [0]*(nt+1)           # plotting arrays

GraphInit(1200,600)

t = 0e0; it = 1                            # Euler method
y[1] = y0; y[2] = dy0                      # initial values
y1[1] = y[1]; y2[1] = y[2]                 # store for plotting
while (t+ht <= tmax):                      # propagation loop
    Euler(t,ht,y,n,Func)
    t += ht; it += 1
    y1[it] = y[1]; y2[it] = y[2]            # store for plotting

Plot(y1,y2,nt,"red",2,0.10,0.45,0.15,0.85,"y","y'","Euler method")

t = 0e0; it = 1                            # Predictor-Corrector Euler method
y[1] = y0; y[2] = dy0                      # initial values
y1[1] = y[1]; y2[1] = y[2]                 # store for plotting
while (t+ht <= tmax):                      # propagation loop
    EulerPC(t,ht,y,n,Func)
    t += ht; it += 1
    y1[it] = y[1]; y2[it] = y[2]            # store for plotting

Plot(y1,y2,nt,"blue",2,0.60,0.95,0.15,0.85,
    "y","y'","Euler Predictor-Corrector method")

MainLoop()
```

### 问题 12.2

男子铁饼世界纪录为 86.74 m，自 1986 年以来由 Yuriy Sedykh 保持。* 男子铁饼重 7.26 kg，为球形，典型半径 `R = 6 cm`。铁饼所受阻力可视为与铁饼相对于空气的平方速度成正比：

`F_D = 1/2 ρ A C_D v²`

* http://hammerthrow.org

其中 `ρ` 为空气密度（1.2 kg/m³）且 `A = πR²` 为铁饼的横截面积。铁饼在原则上可能经历“层流分离”流动，典型阻力系数 `C_d = 0.5`，或“非定常振荡”流动，`C_d = 0.75`。*

+   a. 使用步长 `h = 0.01` 的欧拉预测-校正方法求解铁饼斜抛运动的牛顿运动方程，先将 `x` 和 `y` 运动的 ODE 转化为四个一阶 ODE 的系统。考虑从初始位置 `x₀ = 0`、`y₀ = 2 m` 在理想角度 `φ = 45°` 下的投掷，并求出产生世界纪录投掷距离的初速度。

+   b. 计算并绘制铁饼高度随时间的变化及其轨迹 `y = y(x)` 在三种流动状态下：（a）无摩擦，（b）层流分离流动，以及（c）非定常振荡流动。评估阻力对投掷距离的影响程度。

+   c. 采用欧拉-克罗默和 Verlet 方法求解同一问题。使用步长减半技术估计影响投掷距离的误差，并就其已知的精度阶数讨论结果。

#### 解

使用记号 `y₁ = x`、`y₂ = y`、`y₃ = vₓ` 和 `y₄ = v_y` 的一阶方程等价柯西问题为：

```
⎧ y₁′ = y₃,          y₁(0) = x₀,
  y₂′ = y₄,          y₂(0) = y₀,
  y₃′ = −(k/m) y₃ |y₃| ,   y₃(0) = vₓ₀,
  y₄′ = −(k/m) y₄ |y₄| − g,   y₄(0) = v_y₀.    (12.111)
```

基于欧拉预测-校正方法的 Python 程序见列表 12.22。相应的 C/C++ 实现作为补充材料提供（`P12–ThrowPCg.cpp`），以及使用欧拉-克罗默方法的变体

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_503_0.png)

图 12.11 由欧拉预测-校正方法得到的在 45° 下投掷并经历二次阻力的铁饼随时间变化的高度和轨迹（问题 12.2）。

* https://www.grc.nasa.gov/www/k-12/airplane/dragsphere.html

（`P12-ThrowECg.py` 和 `P12-ThrowECg.cpp`），以及基于 Verlet 方法的程序（`P12-ThrowVg.py` 和 `P12-ThrowVg.cpp`）。层流分离流的典型图形输出如图 12.11 所示。

## 清单 12.22 使用欧拉预测-校正法进行链球投掷（Python 编码）
