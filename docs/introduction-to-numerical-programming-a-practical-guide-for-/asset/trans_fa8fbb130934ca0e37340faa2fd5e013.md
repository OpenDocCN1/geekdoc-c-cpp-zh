

# 列表 10.34 使用笛卡尔坐标对环面域进行积分（Python 编码）

```
# Evaluates a 3D integral on a torus using Cartesian coordinates
from math import *
from integral import *

def Func(x, y, z):
    global R, r
    Rp = sqrt(x*x + y*y)                     # major radial distance
    dR = R - Rp
    rp = sqrt((dR*dR + z*z))                 # minor radial distance
    return (exp(-rp/r) - exp(-1e0) if rp <= r else 0e0)   # zero-padding

# main
R = 3e0; r = 1e0                            # major & minor torus radii
ax = ay = az = 0e0                          # bounding box: 1st octant
bx = by = R+r; bz = r                       # multiply results with 8
nx = ny = 200                               # equal density of mesh
nz = int(nx * r/(R+r))                      # points along x, y, z

I = 8e0 * qTrapz3D(Func, ax, bx, nx, ay, by, ny, az, bz, nz)
print("I Trapeze = ", I)
I = 8e0 * qSimpson3D(Func, ax, bx, nx, ay, by, ny, az, bz, nz)
print("I Simpson = ", I)
I = 8e0 * qGaussLeg3D(Func, ax, bx, nx, ay, by, ny, az, bz, nz)
print("I GaussLeg = ", I)                    # result = 9.510516...
```

为了区分内部点和外部点。考虑到积分的精确值（4π²Rr²(1 − 5/2 e⁻¹) ≈ 9.5105163）并使用相同数量的网格点（200 × 200 × 50），将获得的结果就其精确有效数字而言与函数 qSimpson3D 和 qGaussLeg3D 提供的结果进行比较。

## 解答

Python 积分器可在列表 10.33 中找到，是 integral.py 模块的一部分。其 C/C++ 对应部分包含在头文件 integral.h 中。执行所需积分的 Python 程序在列表 10.34 中给出，C/C++ 版本作为补充材料提供（P10-Integ3D1.py）。

## 问题 10.8

基于第 10.12 节中提出的自适应 3D 技术，编写 Python 和 C/C++ 代码，对半径为 R = 3 和 r = 1 的环面域（见图 10.6）进行积分，被积函数为

f(x, y, z) = { (1 − r′/r)²   r′ ≤ r,  0   r′ > r, }

仅显式依赖于到管轴的距离 r′。施加相对精度 ε = 10⁻⁶。

## 解答

实现分别给出在列表 10.35 和 10.36 中。

# 列表 10.35 环面域上的自适应 3D 积分（Python 编码）

```
# 3D adaptive quadrature over 1st octant of a torus
from math import *
from integral import *

#--------------------------------------------------------------- integrand
def Func(x, y, z):
    global R, r
    Rp = sqrt(x*x + y*y)                         # major radial distance
    dR = R - Rp
    rp = sqrt(dR*dR + z*z)                       # minor radial distance
    dr = 1e0 - rp/r
    return (dr*dr if rp <= r else 0e0)           # zero-padding

#--------------------------------------------------------------- integration limits
def ay(x):
    return (sqrt((R-r)*(R-r) - x*x) if x <= R-r else 0.0)
def by(x):
    return sqrt((R+r)*(R+r) - x*x)
def az(x, y):
    return 0.0
def bz(x, y):
    r0 = R - sqrt(x*x + y*y)
    return sqrt(fabs(r*r - r0*r0))

#--------------------------------------------------------------- interfaces
def Fz(z):
    global xvar, yvar                          # z-integrand
    return Func(xvar,yvar,z)                   # (x,y) as global (xvar,yvar)
def Fy(y):
    global xvar, yvar                          # y-integrand
    yvar = y                                   # stores y in yvar
    return qRomberg(Fz,az(xvar,y),bz(xvar,y),eps)  # x as global xvar
def Fx(x):
    global xvar                                # x-integrand
    xvar = x                                   # stores x in xvar
    return qRomberg(Fy,ay(x),by(x),eps)

# main

R = 3e0; r = 1e0
ax = 0e0; bx = R + r; eps = 1e-6
I = 8e0 * qRomberg(Fx,ax,bx,eps)               # outer integral
print("Integral = ",I)                         # result 9.869605...
```

# 列表 10.36 环面域上的自适应 3D 积分（C/C++ 编码）

```
// 3D adaptive quadrature over 1st octant of a torus
#include <stdio.h>
#include <math.h>
#include "integral.h"

//--------------------------------------------------------------- globals
double eps, r, R, xvar, yvar;
//--------------------------------------------------------------- integrand
```

```
double Func(double x, double y, double z)
{
    double dR, dr, Rp, rp;
    Rp = sqrt(x*x + y*y);                     // major radial distance
    dR = R - Rp;
    rp = sqrt((dR*dR + z*z));                // minor radial distance
    dr = 1e0 - rp/r;
    return (rp <= r ? dr*dr : 0e0);          // zero-padding
}

//--------------------------------------------------------------- integration limits
double ay(double x)
{ return (x <= R-r ? sqrt((R-r)*(R-r) - x*x) : 0.0); }
double by(double x)
{ return sqrt((R+r)*(R+r) - x*x); }
double az(double x, double y)
{ return 0.0; }
double bz(double x, double y)
{ double r0 = R - sqrt(x*x + y*y); return sqrt(fabs(r*r - r0*r0)); }

//--------------------------------------------------------------- interfaces
double Fz(double z)                         // z-integrand
{
    return Func(xvar,yvar,z);               // (x,y) as global (xvar,yvar)
}
double Fy(double y)                         // y-integrand
{
    yvar = y;                               // stores y in yvar
    return qRomberg(Fz,az(xvar,y),bz(xvar,y),eps);  // x as global xvar
}
double Fx(double x)                         // x-integrand
{
    xvar = x;                               // stores x in xvar
    return qRomberg(Fy,ay(x),by(x),eps);
}

//---------------------------------------------------------------
int main()
{
    double ax, bx, I;
    R = 3e0; r = 1e0;
    ax = 0e0; bx = R + r; eps = 1e-6;
    I = 8e0 * qRomberg(Fx,ax,bx,eps);       // outer integral
    printf("Integral = %f\n",I);             // result 9.869605...
}
```

## 参考文献和建议进一步阅读

Abramowitz, M. and I. A. Stegun (Eds.). 1972. Handbook of Mathematical Functions: With Formulas, Graphs, and Mathematical Tables. New York: Dover Publications.

Beu, T. A. 2004. Numerical Calculus in C (3rd ed., in Romanian). Cluj-Napoca: MicroInformatica.

Boole, G. and J. F. Moulton. 2003. A Treatise on the Calculus of Finite Differences (2nd ed.). New York: Dover Publications.

Burden, R. and J. Faires. 2010. Numerical Analysis (9th ed.). Boston: Brooks/Cole, Cengage Learning.

Demidovich, B. and I. Maron. 1987. Computational Mathematics (4th ed.). Moscow: MIR Publishers.

Fitts, D. 2002. *Principles of Quantum Mechanics: As Applied to Chemistry and Chemical Physics.* Cambridge: Cambridge University Press.
Guenther, R. D. 1990. *Modern Optics.* New York: John Wiley & Sons.
Press, W. H., S. A. Teukolsky, W. T. Vetterling, and B. P. Flannery. 2007. *Numerical Recipes: The Art of Scientific Computing* (3rd ed.). Cambridge: Cambridge University Press.
Ralston, A. and P. Rabinowitz. 2001. *A First Course in Numerical Analysis* (2nd ed.). New York: Dover Publications.
Romberg, W. 1955. Vereinfachte numerische Integration (Simplified Numerical Integration (in German)). *Det Kongelige Norske Videnskabers Selskab Forhandlinger (Trondheim)* 28, 30–36.
Stroud, A. 1971. *Approximate Calculation of Multiple Integrals.* Englewood Cliffs: Prentice-Hall.
Stroud, A. and D. Secrest. 1966. *Gaussian Quadrature Formulas.* Englewood Cliffs: Prentice-Hall.

# 11
蒙特卡洛方法

## 11.1 引言

求解数值分析问题的经典方法依赖于严格的算法，该算法对于给定的输入，在预定数量的步骤内提供明确的解。这种方法本质上是确定性的，因为其实现在重复运行、完成相同数量的操作后预期会得到相同的结果。然而，对于应用科学和工程中的众多前沿问题，确定性算法的复杂性使得在合理的时间内进行计算变得不可行。

现代科学的某些领域关注由大量耦合组件组成的系统，这些组件有时还容易受到波动的影响。这种复杂系统可以像自旋集合、生物种群或星系一样不同。它们的表征通常通过高维积分来完成。一个典型例子是 N 个相互作用粒子的经典正则配分函数，

Z = ∫ ⋯ ∫ d³r₁ ⋯ d³r_N exp[ − 1/(k_B T) E(r₁ ⋯ r_N) ] ,

其中 E(r₁ ⋯ r_N) 是系统的总能量，r_i 为粒子 i 的位置，T 是系统温度，k_B 为玻尔兹曼常数。即使对于实际感兴趣的最低粒子数，通过任何经典求积方法对这个 3N 维积分进行求值也是完全不可行的。事实上，考虑到适中的值 N = 20 且每个维度仅有 10 个积分点，所需的基本运算次数将达到 10⁶⁰ 的数量级。即使使用最新的百亿亿次超级计算机，其每秒可执行超过 10¹⁶ 次浮点运算，计算也需要大约 3 · 10³⁶ 年！

对于复杂的高维问题，确定性方法的一种有益替代方案是所谓的随机方法，其基于概率论中的大数定律。在这里，感兴趣的量被定义为随机变量的期望值，或者换句话说，在某些概率假设下，考虑大量随机变量的平均值以获得所求量的概率估计。这些技术通常被称为蒙特卡洛方法，具有内在的非确定性特征，因为它们使用随机实验的结果，并且在统计误差范围内，在不同运行中表现出不同的行为。本质上，与确定性地覆盖所涉及函数的域相比，蒙特卡洛方法随机地采样这些域。一般而言，随机技术不需要真正的随机数，而是使用伪随机序列，但具有高度的均匀性和低的序列相关性。

开创性的蒙特卡洛方法由 Stanislaw Ulam、Nicholas Metropolis 和 John von Neumann 于 1940 年代末在洛斯阿拉莫斯国家实验室开发，并因其赌博般的底层原理而以著名的蒙特卡洛赌场命名。随着高性能计算机的出现，蒙特卡洛方法开始展现其优势，因为获得

