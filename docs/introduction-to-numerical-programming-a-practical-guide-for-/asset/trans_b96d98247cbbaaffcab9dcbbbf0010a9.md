

特定的积分限 a_y(x_i) 和 b_y(x_i)。相应的数值积分可表述为

```
∫_{a_x}^{b_x} ∫_{a_y(x)}^{b_y(x)} f(x,y) dx dy ≈ Σ_{i=1}^{n_x} w_i^{(x)} F_x(x_i), (10.89)
F_x(x_i) ≈ Σ_{j=1}^{n_y(x_i)} w_j^{(y)}(x_i) f(x_i, y_j),
```

并且强调了内层积分点 y_j（就数量、位置和相关权重而言）对外部参数 x_i 的依赖性。

通过将分解为嵌入式一维积分推广到三维，我们可以用

```
∫_{a_x}^{b_x} ∫_{a_y(x)}^{b_y(x)} ∫_{a_z(x,y)}^{b_z(x,y)} f(x,y,z) dx dy dz ≈ Σ_{i=1}^{n_x} w_i^{(x)} F_x(x_i), (10.90)
F_x(x_i) ≈ Σ_{j=1}^{n_y(x_i)} w_j^{(y)}(x_i) F_y(x_i, y_j),
F_y(x_i, y_j) ≈ Σ_{k=1}^{n_z(x_i,y_j)} w_k^{(z)}(x_i, y_j) f(x_i, y_j, z_k).
```

这三个求和在形式上是一维的，但并非相互独立。原则上，它们可以通过利用内置的递归性，使用同一一维自适应积分器来求值。然而，还有一个额外的复杂性：虽然 F_x(x_i) 符合一维积分器处理的单参数被积函数原型，但 F_y(x_i, y_j) 和 f(x_i, y_j, z_k) 显然不符合。

一种可行的解决方案，尽管背离了模块化编程的精神（该精神要求程序单元仅通过明确定义的接口进行通信——带有参数列表的头文件），是定义两个单参数接口函数，\tilde{F}_y(y_j) ≡ F_y(x_i, y_j) 和 \tilde{F}_z(z_k) ≡ f(x_i, y_j, z_k)，它们通过具体实现中的不同机制接收其他参数 x_i 和分别 (x_i, y_j)，例如通过全局变量的方式。

为了说明上述思想，我们考虑积分

```
I = ∫_0^1 dx ∫_0^{√(1−x²)} dy ∫_0^{√(1−x²−y²)} dz = π/6 ≈ 0.5235987… ,
```

其结果是半径为 1 的球体第一卦限的体积。Listing 10.24 中的实现对三个笛卡尔坐标都使用相同的<|message|> 一维积分器 qRomberg，假定其包含在模块 integral.py 中。虽然不是直接的，积分器通过接口函数递归调用自身，产生对应于 x、y 和 z 方向的三个从属层级。

## Listing 10.24 Adaptive 3D Integration on Spherical Domain (Python Coding)

```
# 3D adaptive quadrature over 1st octant of unity sphere
from math import *
from integral import *

#------------------------------------------------------------------------------- integrand
def Func(x, y, z): return 1e0

#------------------------------------------------------------------------------- integration limits
def ay(x): return 0e0
def by(x): return sqrt(1e0 - x*x)
def az(x, y): return 0.0
def bz(x, y): return sqrt(fabs(1e0 - x*x - y*y))

#------------------------------------------------------------------------------- interfaces
def Fz(z):
    global xvar, yvar                # z-integrand
    return Func(xvar,yvar,z)         # (x,y) as global (xvar,yvar)
def Fy(y):
    global xvar, yvar                # y-integrand
    yvar = y                         # stores y in yvar
    return qRomberg(Fz,az(xvar,y),bz(xvar,y),eps)  # x as global xvar
def Fx(x):
    global xvar                      # x-integrand
    xvar = x                         # stores x in xvar
    return qRomberg(Fy,ay(x),by(x),eps)

# main

ax = 0e0; bx = 1e0; eps = 1e-7

I = qRomberg(Fx,ax,bx,eps)           # outer integral
print("Integral = ",I)               # result 0.5235987...
```

所有与特定积分相关的特定方面都限制在用户函数 Func（返回被积函数 f(x,y,z)）以及函数 ay, by, az, bz 和标量 ax 和 by（描述积分限）中。总体相对精度在主程序中设置，并通过全局变量 eps 可用。

关于 x 的外层积分在主程序中直接通过调用积分器 qRomberg 对被积函数 Fx 和固定的积分限 ax 和 bx 来计算。被积函数 Fx 实际上由 qRomberg 对各种 x 值调用，这些 x 值存储在全局变量 xvar 中以供后续在函数 Fy 和 Fz 中使用。此外，Fx 通过递归调用 qRomberg 对单参数接口 Fy 和当前限 ay(x) 和 by(x) 来启动 y 积分的求值。函数 Fy 由 qRomberg 对各种 y 值调用，这些 y 值存储在全局变量 yvar 中以供 Fz 使用。继续，Fy 启动最内层的 z 积分，然而，不是针对“真实”被积函数 Func（它不符合所需的单参数原型），而是针对单参数接口 Fz，后者接收 z 值作为参数并通过全局变量 xvar 和 yvar 接收 x 和 y 值。部分积分按其递归层级的逆序完成。

如果积分相对于其某些变量是不适当的，则积分域可以被划分以将奇异区域置于新的边界上，并且可以使用开放型数值积分例程（如例如函数 qMidPoint）来计算部分积分。

## 10.13 Implementations in C/C++

Listing 10.25 显示了文件 integral.h 的内容，其中包含与正文中开发的 Python 函数等价的 C/C++ 实现，并包含在模块 integral.py 中。相应的例程具有相同的名称、参数和功能。

高斯积分器调用包含在头文件 specfunc.h 中的特殊函数 Legendre 和 Laguerre，因此出于这个原因，integral.h 也需要与 specfunc.h 一起可访问。

## Listing 10.25 Integrators for Real Functions (integral.h)

```
//--------------------- integral.h -----------------------------
// Contains 1D and 3D integrators for real functions with real variables.
// Part of the numxlib numerics library. Author: Titus Beu, 2013
//----------------------------------------------------------------
#ifndef _INTEGRAL_
#define _INTEGRAL_

#include <stdio.h>
#include <math.h>
#include "memalloc.h"
#include "specfunc.h"

//================================================================
double qTrapz(double Func(double), double a, double b, int n)
//----------------------------------------------------------------
// Integrates function Func on interval [a,b] using the trapezoidal rule
// with n integration points
//----------------------------------------------------------------
{
    double h, s;
    int i;

    h = (b-a)/(n-1);
    s = 0.5*(Func(a) + Func(b));
    for (i=1; i<=(n-2); i++) s += Func(a+i*h);

    return h*s;
}

//================================================================
double qSimpson(double Func(double), double a, double b, int n)
//----------------------------------------------------------------
// Integrates function Func on interval [a,b] using Simpson’s rule with n
// (odd) integration points
//----------------------------------------------------------------
{
    double h, s1, s2;
    int i;

    if (n % 2 == 0) n++;                     // increment n if even

    h = (b-a)/(n-1);
    s1 = s2 = 0e0;
    for (i=2; i<=n-3; i+=2) { s1 += Func(a + i*h); }   // odd-index sum
    for (i=1; i<=n-2; i+=2) { s2 += Func(a + i*h); }   // even-index sum

    return (h/3)*(Func(a) + 4*s2 + 2*s1 + Func(b));
}
```

```
//==============================================================================
double qTrapzCtrl(double Func(double), double a, double b, double eps)
//--------------------------------------------------------------------------------
// Integrates function Func on interval [a,b] with relative precision eps
// using the adaptive Trapezoidal Rule
//--------------------------------------------------------------------------------
{
    const int kmax = 30;                    // max. no. of step halving iterations
    double h, sum, t, t0;
    long i, n;
    int k;

    h = b-a; n = 1;
    t0 = 0.5*h*(Func(a) + Func(b));         // initial approximation

    for (k=1; k<=kmax; k++) {               // step halving loop
        sum = 0e0;
        for (i=1; i<=n; i++) sum += Func(a+(i-0.5)*h);
        t = 0.5*(t0 + h*sum);               // new approximation
        if (k > 1) {                        // convergence check
            if (fabs(t-t0) <= eps*fabs(t)) break;
            if (fabs(t) <= eps && fabs(t) <= fabs(t-t0)) break; // integral ~= 0
        }
        h *= 0.5; n *= 2;                   // halve integration step
        t0 = t;
    }
    if (k > kmax) printf("qTrapzCtrl: max. no. of iterations exceeded !\n");

    return t;
}
```

```
//==============================================================================
double qSimpsonCtrl(double Func(double), double a, double b, double eps)
//--------------------------------------------------------------------------------
// Integrates function Func on interval [a,b] with relative precision eps
// using the adaptive Simpson Rule
//--------------------------------------------------------------------------------
{
    const int kmax = 30;                    // max. no. of step halving iterations
    double h, s, s0, sum, t, t0;
    long i, n;
    int k;

    h = b-a; n = 1;
    s0 = t0 = 0.5*h*(Func(a) + Func(b));     // initial approximation

    for (k=1; k<=kmax; k++) {               // step halving loop
        sum = 0e0;
        for (i=1; i<=n; i++) sum += Func(a+(i-0.5)*h);
        t = 0.5*(t0 + h*sum);
        s = (4*t - t0)/3;                   // new approximation
        if (k > 1) {                        // convergence check
            if (fabs(s-s0) <= eps*fabs(s)) break;
            if (fabs(s) <= eps && fabs(s) <= fabs(s-s0)) break; // integral ~= 0
        }
        h *= 0.5; n *= 2;                   // halve integration step
        s0 = s; t0 = t;
    }
    if (k > kmax) printf("qSimpsonCtrl: max. no. of iterations exceeded!\n");
