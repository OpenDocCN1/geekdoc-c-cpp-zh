
```
// Real roots of a real function by the bisection method

#include <stdio.h>

#include <math.h>

#include "roots.h"

double func(double x)

{

    return (x*x*x*x - 5e0*x*x + 4e0) * sin(2e0*x);

}

int main()

{

    double a, b, h, x, xmin, xmax;

    int ierr;

    xmin = -3.5e0;                         // limits of root search domain

    xmax =  3.5e0;

    h = 0.1e0;                            // width of root separation intervals

    a = xmin;

    while (a < xmax) {                    // root separation loop

        b = a + h;                         // search interval [a,b]

        ierr = Bisect(func,a,b,x);

        if ((ierr == 0) && (x != b))

            printf("x = %8.5f in (%6.2f,%6.2f)  f(x) = %7.0e\n",x,a,b,func(x));

        a = b;                             // shift left boundary

    }

}
```

## 问题 6.2

修改例程 `Bisect` 和 `Secant`，使其返回它们达到收敛所需的迭代次数，即迭代计数器 `it` 的最终值。例如，可以将其设为全局变量，通过参数列表返回，或简单地在例程中打印其值。

使用修改后的例程比较求解方程

$$x - \sin x - 0.25 = 0,$$

并评估两种方法的收敛速度，二分法使用搜索区间 $[-30, 30]$，割线法使用初始近似值 $x_0 = -30$。

### 解

Python 和 C/C++ 示例程序作为补充材料提供在文件 `P06-CompareZeros.py` 和 `P06-CompareZeros.cpp` 中。

## 问题 6.3

*开普勒方程*（由约翰内斯·开普勒于 1609 年推导）是经典天体力学中的核心，因为它能够计算轨道物体的角位置。对于椭圆轨道，它关联*平近点角* $M$、*偏近点角* $E$，以及偏心率 $e = \sqrt{1 - b^2/a^2}$（$a > b$ 为半轴）：

$$M = E - e \sin E. \tag{6.58}$$

“近点角”由天文学家定义为角位置：平近点角 `M` 是物体在假想圆轨道上的角位置，假设角速度恒定，它可以与近日点通过以来的时间流逝相关联：

`M = 2π/T (t − t0)`,  (6.59)

其中 `T` 是轨道周期，`t0` 是物体位于近日点的时间。

对于哈雷彗星（Mottmann 1986），相关参数取值为：`e = 0.9672671`，`T = 75.9600` 年，且 `t0 = 1986.1113` 年（1986 年 2 月 9 日）。

- a. 求哈雷彗星在 1986 年 4 月 1 日 `t = 1986.2491` 时的偏近点角 `E`。为此，绘制函数
  `f(E) = E − e sin E − M`,  (6.60)
  对于 `E ∈ [0,1]`，以确保区间包含单个零点并用牛顿法确定它。
- b. 绘制 `E = E(t)` 整个公转周期，使用牛顿法求解
  `E − e sin E − M(t) = 0`,  (6.61)
  时间步长为 `Δt = T/100`。以每个新时刻 `ti = t0 + (i − 1)Δt` 的前一个值 `E(ti−1)` 作为初始近似，起始于 `E(t0) = 0`。

### 解

Python 实现给出在清单 6.17 中，C/C++ 版本作为补充材料提供（`P06-Kepler.cpp`），图形输出如图 6.8 所示。

#### 清单 6.17 开普勒方程的求解（Python 编码）

```
# Solution of Kepler's equation

from math import *

from roots import *

from graphlib import *

pi2 = 2e0 * pi

def Func(E):

    global e, M                 # eccentricity, mean anomaly

    f = E - e * sin(E) - M

    df = 1e0 - e * cos(E)

    return (f, df)

#### main

n = 101

x = [0]*(n+1); y = [0]*(n+1)

GraphInit(1200,600)

e = 0.9672671e0                # Halley comet (Mottmann 1986):

                               # eccentricity

T = 75.96e0                    # period

t0 = 1986.1113e0               # time at perihelion

#------------------------------------------------------------

t = 1986.2491e0

M = pi2 / T * (t - t0)         # mean anomaly

Emax = 1e0

# eccentric anomaly vs. Kepler's function

h = Emax / (n-1)

for i in range(1,n+1):

    E = (i-1)*h

    x[i] = E; (y[i],df) = Func(E)

Plot(x,y,n,"blue",1,0.10,0.45,0.15,0.85,

    "E (rad)","f(E)","Kepler's function")

(E,ierr) = Newton(Func,0e0,Emax,E)            # solve Kepler's equation

print("E = ",E," rad at t = ",t," years")

#--------------------------------------------------------------------

h = T / (n-1)                                 # time dependence of eccentric anomaly

x[1] = t0; y[1] = E = 0e0

for i in range(2,n+1):

    t = t0 + (i-1)*h

    M = pi2 / T * (t - t0)

    (E,ierr) = Newton(Func,0e0,pi2,E)         # solve Kepler's equation

    x[i] = t; y[i] = E

Plot(x,y,n,"red",1,0.60,0.95,0.15,0.85,

    "t (years)","E (rad)","Eccentric anomaly")

MainLoop()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_180_0.png)

图 6.8 哈雷彗星开普勒方程的解：开普勒函数 `f(E)` 随偏心近点角 `E` 的变化，`t = 1986.2491` 时的情况（左图）以及一个周期内偏心近点角的演化（右图）。

## 问题 6.4

当用波长为 `λ` 的单色光照射宽度为 `W` 且高度无限的狭缝时，夫琅禾费衍射产生的强度分布为（Hecht 2002）：

`I(θ) = I₀ [ sin(π W sin θ / λ) / (π W sin θ / λ) ]²`,  (6.62)

其中 `θ` 是相对于入射光观察衍射波的角度。引入

`x = π W sin θ / λ`,  (6.63)

强度及其对 `x` 的一阶导数可写为

`I(x) = I₀ ( sin x / x )² ,   I(0) = I₀`,  (6.64)

`I′(x) = (2I₀ / x) ( cos x − sin x / x ) sin x / x ,   I′(0) = 0`,  (6.65)

中央强度最大值的一半宽度表示使强度下降到最大值 `I₀` 的一半的正值 `x₁/₂`，显然它是方程的解

`I(x) − I₀/2 = 0`,  (6.66)

强度最大值的位置 `xᵢ` 可以通过一阶导数（6.65）的零点得到，这相当于求解：

`I′(x) = 0`,  (6.67)

- a. 使用图形库 `graphlib` 中的例程 `MultiPlot` 绘制 `x ∈ [−10, 10]` 范围内的分布 `I(x)` 和 `I′(x)`。
- b. 通过割线法求解方程 6.66 来求主衍射最大值的半宽度 `x₁/₂`，并以 `x₀ = π`（`I(x)` 的第一个零点）作为初始近似。
- c. 通过求解方程 6.67 求 `x ∈ [−10, 10]` 中的强度最大值 `xᵢ`；以步长 `h = 0.5` 分离根（该步长小于 `sin x` 零点之间的距离），并用假位法计算它们以保持根被限定。

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_181_0.png)

图 6.9 矩形狭缝夫琅禾费衍射的强度分布 `I(x)`（实线）和导数 `I′(x)`（虚线），狭缝宽度有限且高度无限。

### 解

Python 实现见第 6.18 节，C/C++ 版本作为补充材料提供（`P06-Fraunhofer.cpp`），图形输出如图 6.9 所示。

#### 列表 6.18 夫琅禾费衍射（Python 编码）

```
# Intensity distribution for Fraunhofer diffraction

from math import *

from roots import *

from graphlib import *

def Intens(x):

    global I0                     # intensity

    sinc = sin(x)/x if x else 1e0 # maximum intensity

    return I0 * sinc * sinc

def dIntens(x):                   # derivative of Intens

    global I0                     # maximum intensity

    if (x):

        sinc = sin(x)/x

        return 2e0 * I0 * (cos(x) - sinc) * sinc / x

    else: return 0e0

def func(x):                      # function for half-width calculation

    global I0                     # maximum intensity

    return Intens(x) - 0.5e0 * I0

#### main

GraphInit(800,600)

I0 = 1e0                          # maximum intensity

xmin = -10e0; xmax = 10e0

#--------------------------------------------------

n = 101

x = [0]*(2*n+1); y = [0]*(2*n+1)

h = (xmax-xmin) / (n-1)

for i in range(1,n+1):

    xi = xmin + (i-1)*h

    x[i ] = xi; y[i ] = Intens(xi)

    x[i+n] = xi; y[i+n] = dIntens(xi)

nn = [0, n, 2*n]; col = ["", "red", "blue"]; sty = [0, 1,-1]

MultiPlot(x,y,y,nn,col,sty,2,10,

          0e0,0e0,0e0,0e0,0.15,0.85,0.15,0.85,

          "x","I, I'","Fraunhofer diffraction")

#--------------------------------------------------

xi = pi/2e0

(xi,iierr) = Secant(func,0e0,pi,xi)   # half-width of major peak

print("Half-width of major peak = {0:8.5f}".format(xi))

#--------------------------------------------------

print("\nPositions of intensity maxima:")

h = 0.5e0

a = xmin

while (a < xmax):                     # root separation loop

    b = a + h                         # new search interval [a,b]

(xi,i err) = FalsPos(dIntens,a,b)

if ((i err == 0) and (xi != b) and (Intens(xi) > 1e-10)):

    print("{0:8.5f}  in  ({1:5.2f},{2:5.2f})".format(xi,a,b))

    a = b                                         # shift left boundary

MainLoop()
```

## 问题 6.5

普朗克定律表达了处于热平衡的黑体发射的电磁辐射的谱能量密度（Toda et al. 1998）：

`u(λ, T) = 8πhc / λ⁵ · 1 / (exp(hc / (λk_B T)) − 1)`,

其中 `T` 是平衡温度，`λ` 是波长，`h = 6.62606957 × 10⁻³⁴ J·s` 是普朗克常数，`k_B = 1.3806488 × 10⁻²³ J·K⁻¹` 是玻尔兹曼常数，`c = 2.99792458 × 10⁸ m·s⁻¹` 是真空中的光速。`u(λ, T)dλ` 表示在谱区间 `(λ, λ + dλ)` 内辐射的能量。

引入无量纲变量

`x = λ / λ₀`,

以及依赖于温度的参数

`λ₀ = hc / (k_B T),    K = 8πk_B T / λ₀⁴`,

普朗克定律变为

`u(λ, T) = K · 1 / [x⁵ (e^(1/x) − 1)]`,    (6.68)

谱能量密度的导数，

`∂/∂λ u(λ, T) = Kλ₀ [5x + (1 − 5x)e^(1/x)] / [x⁷ (e^(1/x) − 1)²]`,    (6.69)

通过其零点给出 `u(λ, T)` 的最大值位置。维恩位移定律指出，对于黑体，对应于 `u(λ, T)` 最大值的波长 `λ_max` 与温度 `T` 成反比，或等价地 `λ_max T = 2.897768 × 10⁻³ m·K`。

- a. 绘制平衡温度 `T = 4000`、`5000` 和 `6000 K` 时的谱能量密度 `u(λ, T)` 及其对应导数 `∂u(λ, T)/∂t`。
- b. 通过求解方程
  `∂/∂λ u(λ, T) = 0`,
  求太阳电磁辐射的 `u(λ, T)` 的最大值，考虑有效光球温度 `T = 5778 K`（Williams 2013）。使用带数值导数的牛顿法，并检验维恩定律的有效性。

### 解

Python 实现见第 6.19 节，C/C++ 版本作为补充材料提供（`P06-Planck.cpp`）。图形输出如图 6.10 所示。

#### 列表 6.19 黑体辐射普朗克定律（Python 编码）

```
# Planck's law of black body radiation

from math import *

from roots import *

from graphlib import *

hP = 6.62606957e-34                     # Planck's constant (J s)

kB = 1.3806488e-23                      # Boltzmann constant (J/K)

c  = 2.99792458e8                       # speed of light (m/s)

def u(lam):                             # spectral energy density u(lam)

    global lam0, K                      # reference wavelength, factor of u(lam)

    if (lam == 0e0): return 0e0

    x = lam / lam0

    return K / (pow(x,5) * (exp(1e0/x) - 1e0))

def du(lam):                            # du/dlam

    global lam0, K                      # reference wavelength, factor of u(lam)
```
