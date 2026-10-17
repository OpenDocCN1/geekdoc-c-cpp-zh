
```python
a = 0e0; b = pi                               # integration domain

I = cos(a) - cos(b)                           # exact result

print("Exact result = ",I)

print("   n        IT        errT    facT        IS        errS    facS")

n = 1

errT0 = 1e0; errS0 = 1e0

for i in range(1,11):

    n = 2*n                                   # number of intervals

    IT = qTrapz(Func,a,b,n+1)                 # trapezoidal rule

    errT = fabs(1e0 - IT/I)                   # relative error

    facT = errT0/errT                         # error reduction

    IS = qSimpson(Func,a,b,n+1)               # Simpson's rule

    errS = fabs(1e0 - IS/I)                   # relative error

    facS = errS0/errS                         # error reduction

    print(("{0:5d}{1:11.6f}{2:10.1e}{3:6.1f}{4:11.6f}{5:10.1e}{6:6.1f}").

          format(n,IT,errT,facT,IS,errS,facS))

    errT0 = errT; errS0 = errS
```

## 列表 10.27 问题 10.2 的输出

精确结果 = 0.2222222222222222

| n | IT | errT | facT | IS | errS | facS |
|---:|---:|---:|---:|---:|---:|---:|
| 2 | 1.140625 | 4.1e+00 | 0.2 | 0.854167 | 2.8e+00 | 0.4 |
| 4 | 0.653870 | 1.9e+00 | 2.1 | 0.491618 | 1.2e+00 | 2.3 |
| 8 | 0.400656 | 8.0e-01 | 2.4 | 0.316251 | 4.2e-01 | 2.9 |
| 16 | 0.272359 | 2.3e-01 | 3.6 | 0.229593 | 3.3e-02 | 12.8 |
| 32 | 0.235120 | 5.8e-02 | 3.9 | 0.222707 | 2.2e-03 | 15.2 |
| 64 | 0.225470 | 1.5e-02 | 4.0 | 0.222253 | 1.4e-04 | 15.8 |
| 128 | 0.223036 | 3.7e-03 | 4.0 | 0.222224 | 8.7e-06 | 15.9 |
| 256 | 0.222426 | 9.2e-04 | 4.0 | 0.222222 | 5.4e-07 | 16.0 |
| 512 | 0.222273 | 2.3e-04 | 4.0 | 0.222222 | 3.4e-08 | 16.0 |
| 1024 | 0.222235 | 5.7e-05 | 4.0 | 0.222222 | 2.1e-09 | 16.0 |

## 解

Python 实现见列表 10.26，C/C++ 版本作为补充材料提供（`P10-qTrapSimpConv.cpp`）。

## 问题 10.2

求解前一问题的要求，针对勒让德多项式的范数（定义和数值方法见第 6.4 节）：

\[
\int_{-1}^{+1} [P_N(x)]^2 dx = \frac{2}{2N+1},
\]

使用函数 `Legendre`（来自 `specfunc.py` 或 `specfunc.h`）来计算特定阶数 N = 4 的多项式。

### 解

Python 和 C/C++ 实现作为补充材料提供（文件 `P10-qTrapSimpConv1.py` 和 `P10-qTrapSimpConv1.cpp`），输出显示在列表 10.27 中。

## 问题 10.3

Fresnel 积分（见 Guenther 1990），

\[
C(w) = \int_0^w \cos\left(\frac{\pi u^2}{2}\right) du, \qquad
S(w) = \int_0^w \sin\left(\frac{\pi u^2}{2}\right) du,
\]

是光学衍射理论的核心。利用 `qRomberg` 积分器计算它们，范围为 −3.5 ≤ w ≤ 3.5，相对精度 ε = 10⁻⁶，并绘制曲线 S(w) 随 C(w) 的变化，称为 Cornu 螺旋。

### 解

实现分别给出在列表 10.28 和 10.29 中，图形输出显示在图 10.8 中。

### 列表 10.28 Fresnel 积分（Python 编码）

```python
# Fresnel integrals and Cornu spiral

from math import *

from integral import *

from graphlib import *

def CosF(u): return cos(0.5*pi*u*u)             # integrands of Fresnel integrals

def SinF(u): return sin(0.5*pi*u*u)

#### main

eps = 1e-6                                      # relative integration precision

xmin = -3.5; xmax = 3.5                         # interval upper limits

h = 0.05;                                       # plotting mesh spacing

n = int((xmax-xmin)/h + 1)                      # number of upper limits

x = [0]*(2*n+1); c = [0]*(2*n+1); s = [0]*(n+1)

for i in range(1,n+1):

    x[i] = xmin + (i-1)*h; x[i+n] = x[i]                    # upper limit

    c[i] = qRomberg(CosF,0e0,x[i],eps);                     # Fresnel integrals

    s[i] = qRomberg(SinF,0e0,x[i],eps); c[i+n] = s[i]

GraphInit(1200,600)

nn = [0, n, 2*n]; col = ["", "red", "blue"]; sty = [0, 1, -1]

MultiPlot(x,c,c,nn,col,sty,2,10,

          0e0,0e0,0e0,0.10,0.10,0.45,0.15,0.85,

          "x","C, S","Fresnel integrals")

Plot(c,s,n,"green",1,0.60,0.95,0.15,0.85,"C(x)","S(x)","Cornu Spiral")

MainLoop()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_406_0.png)

**图 10.8** Fresnel 积分 C(w) 和 S(w)（虚线）以及 Cornu 螺旋，由程序 10.28 和 10.29 计算得出。

### 列表 10.29 Fresnel 积分（C/C++ 编码）

```cpp
// Fresnel integrals and Cornu spiral

#include <math.h>

#include "memalloc.h"

#include "integral.h"

#include "graphlib.h"

#define pi 3.141592653589793

double CosF(double u) { return cos(0.5e0*pi*u*u); }    // integrands of

double SinF(double u) { return sin(0.5e0*pi*u*u); }    // Fresnel integrals

int main(int argc, wchar_t** argv)

{

    int i, n;

    double eps, h, xmin, xmax;

    double *c, *s, *x;

    int sty[3], nn[3];

    const char* col[3];

    eps = 1e-6;                         // relative integration precision

    xmin = -3.5e0; xmax = 3.5e0;                // interval of upper limits

    h = 0.05e0;                         // plotting mesh spacing

    n = int((xmax-xmin)/h + 0.5) + 1;           // number of upper limits

    x = Vector(1,2*n); c = Vector(1,2*n); s = Vector(1,n);

    for (i=1; i<=n; i++) {

        x[i] = xmin + (i-1)*h; x[i+n] = x[i];           // upper limit

        c[i] = qRomberg(CosF,0e0,x[i],eps);            // Fresnel integrals

        s[i] = qRomberg(SinF,0e0,x[i],eps); c[i+n] = s[i];

    }

    PyGraph w(argc, argv);

    w.GraphInit(1200,600);

    nn[1] = n ; col[1] = "red" ; sty[1] = 1;

    nn[2] = 2*n; col[2] = "blue"; sty[2] = -1;          // dashed line

    w.MultiPlot(x,c,nn,col,sty,2,10,

        0e0,0e0,0,0e0,0e0,0,0.10,0.45,0.15,0.85,

        "x","C, S","Fresnel integrals");

    w.Plot(c,s,n,"green",1,0.60,0.95,0.15,0.85,"C(x)","S(x)","Cornu Spiral");

    w.MainLoop();

}
```

## 问题 10.4

氢原子中 2s 态（n = 2, l = 0, m = 0）电子的波函数在无量纲径向单位下可定义为（Fitts 2002）：

\[
\psi_{200}(r,\theta,\phi) = \frac{1}{4\sqrt{2\pi}} (2 - r) e^{-r/2}.
\]

电子被局域在径向位置 r = 0 到 R 之间的概率为

\[
\int_0^R \int_0^\pi \int_0^{2\pi} |\psi_{200}(r,\theta,\phi)|^2 r^2 dr \sin\theta\, d\theta\, d\phi = \frac{1}{8} \int_0^R r^2 (2 - r)^2 e^{-r} dr,
\]

其中角积分贡献因子为 \(4\pi\)。

- a. 利用 Romberg 方法（例程 `qRomberg`）计算电子在径向位置 r = 0 到 R ∈ [10, 25] 之间、步长为 1 的概率，相对精度 ε = 10⁻⁸。
- b. 利用例程 `qImprop1` 和 `qGaussLag` 分别计算从 r = 0 到 +∞ 的径向积分，并检验电子在空间中任意位置的总概率确实等于 1。注意 Gauss-Laguerre 数值积分所需的积分点数非常少。

### 解

Python 实现见列表 10.30，C/C++ 版本作为补充材料提供（`P10-ElecProbRad.cpp`）。

### 列表 10.30 氢原子中电子的径向局域概率（Python 编码）

```python
# Radial localization probability of an electron within the H atom

from math import *

from integral import *

def Func(r):                     # probability density for 2s state

    f = r * (2-r)

    return f * f * exp(-r) / 8e0

#### main

eps = 1e-8                       # relative precision of integrals

print("Radial localization probability:")

for R in range(10,31):

    I = qRomberg(Func,0e0,R,eps)

    print("[0,{0:.1f}] = {1:10.8f}".format(R,I))

print("\nTotal localization probability:")

Rinf = 25e0                      # guess for +infinity

(I,Rinf) = qImprop1(Func,0e0,Rinf,eps)

print("I Improp1  = {0:10.8f}  Rinf = {1:.1f}".format(I,Rinf))

n = 3                            # number of radial integration nodes

I = qGaussLag(Func,0e0,n)

print("I GaussLag = {0:10.8f}".format(I))
```

## 问题 10.5

氢原子中 3d₀ 态（n = 3, l = 2, m = 0）电子的波函数在无量纲径向单位下具有以下形式（Fitts 2002）：

\[
\Psi_{320}(r,\theta,\phi) = \frac{1}{81\sqrt{6\pi}} r^2 e^{-r/3} (3\cos^2\theta - 1).
\]

使用函数 `qSimpsonSph` 和 `qGaussSph` 对比验证 Ψ₃₂₀(r,θ,φ) 的范数，即电子的总局域概率，确实为单位：

\[
\int_0^\infty \int_0^\pi \int_0^{2\pi} |\Psi_{320}(r,\theta,\phi)|^2 r^2 dr \sin\theta\, d\theta\, d\phi = 1.
\]

结合例程 `qSimpsonSph`，径向积分上限取 a = 40，使用 n_r = 100, n_θ = 70, n_φ = 3 个节点。对于高斯数值积分，采用 n_r = 10, n_θ = 10, n_φ = 1 个积分点。比较结果中正确有效数字的个数，并确定每种数值积分方案为获得额外一位有效数字所需的网格点数。论证在高斯数值积分情况下 n_φ = 1 是合适的选择。

### 列表 10.31 氢原子中电子的总局域概率（Python 编码）

```python
# Total localization probability of an electron in the H atom

from math import *

from integral import *

def Func(r, theta, phi):                # probability density for 3d_0 state

    c = 1e0/(81e0*sqrt(6e0*pi))

    cost = cos(theta)

    psi = c * r * r * exp(-r/3e0) * (3e0*cost*cost - 1e0)

    return psi * psi

#### main

a = 40e0                                # radial limit

nr = 100; nt = 70; np = 3

I = qSimpsonSph(Func,a,nr,nt,np)

print("I SimpsonSph = ",I)

nr = 10; nt = 10; np = 1

I = qGaussSph(Func,nr,nt,np)

print("I GaussSph   = ",I)
```
