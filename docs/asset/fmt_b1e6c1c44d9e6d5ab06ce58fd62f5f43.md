
# Charged particle orbiting about a fixed charge - Verlet method

```python
from math import *
from ode import *
from graphlib import *


def Forces(m, x, y, vx, vy):
    factCoul = 14.3996517e0                 # e**2/(4*pi*eps0) [eV*A]
                                             # charge: e, energy: eV, force: eV/A
    r2 = x*x + y*y                          # mass: u, distance: A, time: ps
    r = sqrt(r2)                            # distance from force center
    fr = factCoul * q * Q / r2              # radial force
    fx = fr * x/r                           # force components
    fy = fr * y/r
    Epot = fr * r                           # potential energy
    return (fx, fy, Epot)

#### main

nn  = [0]*4; sty = [0]*4                   # end-indexes, styles of plots
col = ["w"]*4                             # colors of plots
```

```python
m = 1e0                                                                 # mass of particle
q = -1.e0; Q = 1.e0                                                      # in units of e
x0 = 1e0; y0 = 0e0                                                       # initial position
vx0 = 0e0; vy0 = 4.5e0                                                    # initial velocity
tmax = 20e0                                                              # time span
ht = 0.1e0                                                               # time step size

nt = int(tmax/ht + 0.5) + 1                                              # number of time steps
tt = [0]*(3*nt+1); Et = [0]*(3*nt+1)                                      # plotting arrays
xt = [0]*(nt+1); yt = [0]*(nt+1)

t = 0e0; it = 1
x = x0; vx = vx0                                                         # initial values
y = y0; vy = vy0

(fx, fy, Epot) = Forces(m,x,y,vx,vy)                                     # initial forces and potential energy
ax = fx/m; ay = fy/m                                                      # initial acceleration
Ekin = 0.5e0 * m * (vx*vx + vy*vy)                                        # initial kinetic energy
xt[it] = x; yt[it] = y                                                    # store for plotting
tt[it] = tt[nt+it] = t; tt[2*nt+it] = t
Et[it] = Ekin; Et[nt+it] = Epot; Et[2*nt+it] = Ekin + Epot

while (t < tmax):                                                        # propagation loop
    (x,y,vx,vy,ax,ay,Ekin,Epot) = Verlet2(ht,m,x,y,vx,vy,ax,ay,Forces)
    t += ht; it += 1

    xt[it] = x; yt[it] = y                                                # store for plotting
    tt[it] = tt[nt+it] = t; tt[2*nt+it] = t
    Et[it] = Ekin; Et[nt+it] = Epot; Et[2*nt+it] = Ekin + Epot

GraphInit(1200,600)

nn[1] = nt; col[1] = "blue"; sty[1] = 1                                   # Ekin
nn[2] = 2*nt; col[2] = "green"; sty[2] = 1                               # Epot
nn[3] = 3*nt; col[3] = "red"; sty[3] = 1                                 # Etot
MultiPlot(tt,Et,nn,col,sty,3,10,0e0,0e0,0,0e0,0e0,0,
          0.10,0.45,0.15,0.85,"t","Ek,Ep,Et","Energies of charged particle")
Plot(xt,yt,nt,"blue",1,0.60,0.95,0.15,0.85,
     "x","y","Trajectory of charged particle")

MainLoop()
```

## 问题 12.6

考虑非线性刚性摆角位移 $u$ 的运动方程，摆长为 $l$（$g$ 为重力加速度）：

$$u'' = -\frac{g}{l} \sin u, \tag{12.112}$$

初始条件为：

$$u(0) = u_0, \quad u'(0) = 0. \tag{12.113}$$

任意振幅振荡的周期显式依赖于初始位移 $u_0 \in [-\pi, \pi]$（Beléndez et al. 2007）：

$$T = T_0 \frac{2}{\pi} K\left(\sin^2 \frac{u_0}{2}\right). \tag{12.114}$$

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_510_0.png)

图 12.14 使用 Verlet 方法时，绕固定电荷运动的带电粒子的动能、势能和总能量的时间依赖性以及轨迹（对应问题 12.5）。

这里

```
$T_0 = 2\pi \sqrt{\frac{l}{g}}$
```

为谐振周期，特定于振幅趋于零的极限，而 $K(m)$ 为第一类完全椭圆积分，定义为（Abramowitz and Stegun 1972）

```
$K(m) = \int_{0}^{1} \frac{dz}{\sqrt{(1 - z^2)(1 - m z^2)}}.$
(12.115)
```

- a. 编写一个基于其定义的椭圆积分 $K(m)$ 的计算例程，并使用函数 `Improp2`（定义在 `integral.py` 或 `integral.h` 中）来求值所涉及的第二类 improper 积分（在边界之一处具有奇异被积函数；参见第 10.8 节）。
- b. 考虑长度 $l = 1$ m 的摆，初始角位移 $u_0 = \pi/2$。使用 Runge–Kutta 方法以时间步长 $h = 0.001$ s 传播动力学状态至 $t_{max} = 20$ s。通过计数解的零点（符号变化）确定传播所覆盖的半周期数，并由第一个和最后一个零点之间的时间跨度计算振荡周期并与精确值进行比较。
- c. 绘制位移的时间依赖性以定性验证所确定的周期。绘制摆在相空间中的轨迹，$u' = u'(u)$，以直观检查解的稳定性。

## 解

为应用 Runge–Kutta 方法，摆的方程被转化为一阶常微分方程组：

```
$\begin{cases} u'_1 = u_2, \\ u'_2 = -(g/l)\sin(u_1) - k u_2, \end{cases}\qquad \begin{cases} u_1(0) = u_0, \\ u_2(0) = 0. \end{cases}$
```

Python 代码见清单 12.26，C/C++ 版本作为补充材料提供（P12-PendulumRKg.cpp）。摆角位移的时间依赖性和相空间中的轨迹如图 12.15 所示。所得周期 $T/T_0 = 1.18036$ 与精确值在五位有效数字上一致。程序还为考虑摆的阻尼提供了相应设置。

**清单 12.26**　Runge-Kutta 方法下的非线性摆振荡（Python 编码）

```python
# Angular motion of a nonlinear pendulum by the Runge-Kutta method

#     u'' = -g/l * sin(u) - k * u',   u(0) = u0, u'(0) = u0'

from math import *

from ode import *

from integral import *

from graphlib import *

g = 9.81e0                                      # gravitational acceleration

def Func(t, u, f):                              # RHS of 1st order ODEs

    f[1] = u[2]                                 # u[1] = u, u[2] = u'

    f[2] = -g/l * sin(u[1]) - k * u[2]

#==========================================================================

def Kel(m):

#--------------------------------------------------------------------------

# Returns the complete elliptic integral of the 1st kind

# Calls: qImprop2 (integral.py)

#--------------------------------------------------------------------------

    eps = 1e-7                                   # relative precision

    def fKel(z): return 1e0 / sqrt((1e0-z*z)*(1e0-m*z*z))   # integrand

    return qImprop2(fKel,0e0,1e0,eps)

#### main

l = 1e0                                         # pendulum length

k = 0e0                                         # velocity coefficient

u0 = 0.5e0*pi                                   # initial displacement

du0 = 0e0                                       # initial derivative

tmax = 20e0                                     # time span

ht = 0.001e0                                    # time step size

n = 2                                           # number of 1st order ODEs

nt = int(tmax/ht + 0.5) + 1                    # number of time steps

u = [0]*(n+1)                                   # solution components

tt = [0]*(nt+1); ut = [0]*(nt+1); vt = [0]*(nt+1)  # arrays for plotting

t = 0e0; it = 1

u[1] = u0; u[2] = du0                           # initial values

tt[1] = t; ut[1] = u[1]; vt[1] = u[2]           # store for plotting

nT = 0                                          # number of half-periods

t1 = t2 = 0e0                                   # bounding solution zeros

us = u[1]                                       # save solution

while (t+ht <= tmax):                            # propagation loop

    RungeKutta(t,ht,u,n,Func)

    t += ht; it += 1

    if (u[1]*us < 0e0):                          # count solution passages through zero

        if (t1 == 0): t1 = t                     # initial zero

        else: t2 = t; nT += 1                   # final zero

    us = u[1]                                      # save solution

    tt[it] = t; ut[it] = u[1]; vt[it] = u[2]              # store for plotting

    T = 2e0 * (t2-t1) / nT                              # calculated period
    T0 = 2e0*pi*sqrt(1/g)                               # harmonic period
    Tex = 2/pi * T0 * K(el(pow(sin(0.5e0*u0),2))       # exact period
    print("u0 = {0:7.5f}  T/T0 = {1:7.5f} + ({2:7.1e})". \
          format(u0,T/T0,(Tex-T)/T0))

    GraphInit(1200,600)

    Plot(tt,ut,it,"blue",1,0.10,0.45,0.15,0.85, \
         "t (s)","u (rad)","Displacement of nonlinear pendulum")
    Plot(ut,vt,it,"blue",1,0.60,0.95,0.15,0.85, \
         "u (rad)","u' (rad/s)","Trajectory of pendulum in phase space")

    MainLoop()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_512_0.png)

**FIGURE 12.15** 非线性摆角位移随时间的变化及其在相空间中的轨迹，初始位移等于 $\pi/2$ 时的情况（第 12.6 题）。

## PROBLEM 12.7

考虑前一题的非线性摆问题，从初始角位移 $u_0 \in [0.1, 3.1]$ 且间隔为 0.1 的初始条件出发传播轨迹。绘制最低和最大初始位移的位移随时间变化 $u = u(t)$，并注意周期和函数形式上的显著差异。绘制振荡周期随初始位移的变化 $T = T(u_0)$，并将该依赖关系与精确结果（公式 12.114）进行比较。
