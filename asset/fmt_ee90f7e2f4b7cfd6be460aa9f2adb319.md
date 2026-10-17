
```
from random import *

def ranSqrt():

#--------------------------------------------------------------------------

# Returns a random number x in the range [0,1) with the distribution

# w(x) = 3/2 x^(1/2), and the corresponding value w(x)

#--------------------------------------------------------------------------

    x = pow(random(),2e0/3e0)

    w = 1.5e0 * sqrt(x)

    return (x, w)

def func(x): return x * exp(-x)          # integrand

#### main

n = eval(input("n = "))                 # number of sampling points

seed()

f1 = f2 = 0e0                            # quadrature with importance sampling

for i in range(1,n+1):

    (x, w) = ranSqrt()                   # RNG with distribution w(x)

    if (w):

        f = func(x) / w                  # integrand

        f1 += f; f2 += f * f             # sums

f1 /= n; f2 /= n                         # averages

s = f1                                   # integral

sigma = sqrt((f2-f1*f1)/n)               # standard deviation

print("s = ",s," +/- ",sigma)
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_421_0.png)

FIGURE 11.1 Monte Carlo estimates of the integral ∫₀¹ x e⁻ˣ dx (left panel) and associated standard deviations σ (right panel) using uniform sampling and, respectively, importance sampling with the distribution w(x) = (3/2)x¹/², for numbers of integration points ranging between n = 100 and 30,000.

其中域 𝒟 外的点可以通过使用 Heaviside 函数来区分

```
H(x) = { 0 if x < 0, 1 if x ≥ 0. } (11.19)
```

相应的蒙特卡洛求积公式因此为

```
I ≈ 4/n Σ_{i=1}^n H[1 - (x_i^2 + y_i^2)] = 4 n_i / n, (11.20)
```

它意味着 `n` 个随机采样点 `(x_i, y_i)`，均匀分布在正方形 $\tilde{D}$ 内。在这种情况下，和显然具有位于圆形扇区 `D` 内部的点数 `n_i` 的意义，其面积如所见与 `n_i` 与总采样点数 `n` 之间的比率成正比。换句话说，圆形扇区的面积与生成内部采样点的概率成正比。简单的计算表明，在这种情况下，平均被积函数和平均平方被积函数相等，即 `⟨H⟩ = ⟨H²⟩ = n_i / n`。

程序 11.3 精确实现了所讨论的思想。单位圆面积的估计值列在表 11.2 中，对应于若干采样点数。对于 `n = 50,000`，期望的 π 值以四位精确小数被重现，尽管相关的标准误差 σ 表明估计较差。

继续这一思想，即对于扩展域 $\tilde{D}$ 的均匀采样，体积 `V` 和 $\tilde{V}$ 的比率近似于相应采样点数 `n_i / n` 的比率；上述

## Listing 11.3 Monte Carlo Evaluation of the Area of the Unit Circle (Python Coding)

```
# Monte Carlo calculation of the unit circle area

from math import *

from random import *

#### main

n = eval(input("n = "))                     # number of sampling points

seed()

ni = 0                                       # number of interior points

for i in range(1,n+1):

    x = random(); y = random()

    if (x*x + y*y <= 1e0): ni += 1           # add interior point

fi = ni/n                                    # fraction of interior points

s = 4e0 * fi                                 # integral

sigma = 4e0 * sqrt((fi - fi*fi)/n)           # standard deviation

print("Unit circle area = ",s,"+/- ",sigma)
```

## TABLE 11.2 Monte Carlo Estimates of the Integral I = ∫∫_{x²+y²≤1} dx dy and Associated Standard Deviations σ

| n | I | σ | n | I | σ |
|---|---|---|---|---|---|
| 100 | 3.20000 | 0.16000 | 5,000 | 3.14400 | 0.02320 |
| 500 | 3.22400 | 0.07074 | 10,000 | 3.15520 | 0.01633 |
| 1000 | 3.12800 | 0.05223 | 50,000 | 3.14128 | 0.00734 |

该技术可基于关系式推广用于复杂多维体积的求值：

$$V = \lim_{n \to \infty} \frac{n_i}{n} \tilde{V}.$$

从技术上讲，计算相当于在整个扩展域内生成的总点数中登记位于原始积分域内部的点。

第二个二维示例考虑积分：

$$\frac{1}{4\pi} \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} (x^2 + y^2) e^{-(x^2 + y^2)/2} dy dx = 1. \qquad (11.21)$$

显然，它可以用均匀采样的通用蒙特卡洛方法求值。然而，可以利用高斯因子并使用由高斯分布生成的积分点进行更有意义的采样：

$$w(x,y) = \frac{1}{2\pi} e^{-(x^2 + y^2)/2}. \qquad (11.22)$$

由于该概率分布归一化为 1，$\int_{-\infty}^{\infty} \int_{-\infty}^{\infty} w(x,y) dy dx = 1$，蒙特卡洛求积相当于计算平均值

$$\langle \tilde{f} \rangle = \frac{1}{n} \sum_{i=1}^{n} \frac{\tilde{f}(x_i, y_i)}{w(x_i, y_i)} = \frac{1}{2n} \sum_{i=1}^{n} (x_i^2 + y_i^2), \qquad (11.23)$$

其中自变量根据正态概率分布 $w(x,y)$ 采样。生成具有此类分布的随机数的技术在第 11.5 节中介绍。其中一个开发的例程是`randNrm2`，它实际上返回随机变量`x`和`y`的配对，以及分布函数的相应值`w`。

程序 11.4 比较了均匀采样和高斯采样。图 11.2 描绘了所讨论积分的方差减小结果。左面板中可以看到，使用重要性采样获得的积分估计值比均匀采样具有显著更低的离散度。

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_424_0.png)

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_424_1.png)

图 11.2 蒙特卡洛估计积分 $(1/4\pi) \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} (x^2 + y^2) e^{-(x^2 + y^2)/2} dy dx = 1$（左面板）和相关标准偏差 $\sigma$（右面板）使用均匀采样和分别使用高斯采样，积分点数在 $n = 250$ 到 100,000 之间。

## Listing 11.4  2D Monte Carlo Integration with Importance Sampling (Python Coding)

```
# Two-dimensional Monte Carlo quadrature with variance reduction

from math import *

from random import *

from randoml import *

def func(x,y):                                      # integrand

    return (x*x + y*y)*exp(-0.5e0*(x*x + y*y))/(4e0*pi)

#### main

L = 8e0                                             # integration domain [-L,L] x [-L,L]

L2 = L * L                                          # area of sampling domain

n = 100000                                          # number of sampling points

seed()

f1 = f2 = 0e0                                       # quadrature with uniform sampling

for i in range(1,n+1):

    x = L * random(); y = L * random()

    f = func(x,y)                                   # integrand

    f1 += f; f2 += f * f                            # sums

f1 /= n; f2 /= n                                    # averages

s = 4e0 * L2 * f1                                   # integral

sigma = 4e0 * L2 * sqrt((f2-f1*f1)/n)               # standard deviation

print("Uniform sampling : s = ",s," +/- ",sigma)

f1 = f2 = 0e0                                       # quadrature with importance sampling

for i in range(1,n+1):

    (w, x, y) = randNrm2()                          # random numbers with normal distribution

    f = func(x,y) / w                              # integrand

    f1 += f; f2 += f * f                           # sums

f1 /= n; f2 /= n                                    # averages

s = f1                                              # integral

sigma = sqrt((f2-f1*f1)/n)                          # standard deviation

print("Gaussian sampling: s = ",s," +/- ",sigma)
```

采样。标准偏差作为采样点数的函数的对数-对数图的线性拟合进一步证实了高斯采样的更好性能，这表明使用正态分布而不是均匀分布的随机数时，不确定性大约降低了 2.9 倍。

让我们将蒙特卡洛方法应用于三维求积的一个应用，考虑主半径 `R = 3`、次半径 `r = 1` 的环面质量和质量中心位置的求值（见图 11.3）。环面以原点为中心并关于 `z` 轴对称。类似的问题已在第 10 章中通过确定性求积处理。环面表面的方程为

$$\left(R - \sqrt{x^2 + y^2}\right)^2 + z^2 = r^2. \qquad (11.24)$$

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_426_0.png)

图 11.3 蒙特卡洛计算环面质量及其质量中心位置的积分域和坐标系。

从给定点 `(x, y, z)` 到 `z` 轴的径向距离分别为，以及到管轴的径向距离分别为

```
R' = sqrt(x^2 + y^2),    r' = sqrt((R - R')^2 + z^2).    (11.25)
```

点位于环面内部的条件可以简单地表示为

```
r' ≤ r.    (11.26)
```

作为密度函数，我们考虑

```
f(x, y, z) = { (1 - r'/r)^2   r' ≤ r,  0   r' > r, }    (11.27)
```

它仅依赖于次径向距离 `r'`，并从管轴的 1 抛物线递减到环面表面的 0。密度的积分给出质量，等于 `m = 1/3 π^2 R r^2 ≈ 9.8696044`。至于质量中心，由于对称性，它显然位于原点：`x_c = y_c = z_c = 0`。

作为扩展积分域，我们考虑紧密包围环面的平行六面体，$\tilde{D} = [-R - r, R + r] \times [-R - r, R + r] \times [-r, r]$。质量和质量中心的坐标分别由

```
m = ∫_{tilde D} ρ dx dy dz,
```

```
x_c = (1/m) ∫_{tilde D} ρ x dx dy dz,    y_c = (1/m) ∫_{tilde D} ρ y dx dy dz,    z_c = (1/m) ∫_{tilde D} ρ z dx dy dz.
```

给出。

这些积分的蒙特卡洛求值可根据关系式完成：

```
m ≈ tilde V ⟨ρ⟩ ± tilde V sqrt([⟨ρ^2⟩ - ⟨ρ⟩^2]/n),    (11.28)
```

```
x_c ≈ (tilde V / m) ⟨ρ x⟩ ± (tilde V / m) sqrt([⟨(ρ x)^2⟩ - ⟨ρ x⟩^2]/n),    (11.29)
```

```
y_c ≈ (tilde V / m) ⟨ρ y⟩ ± (tilde V / m) sqrt([⟨(ρ y)^2⟩ - ⟨ρ y⟩^2]/n),    (11.30)
```

```
z_c ≈ (tilde V / m) ⟨ρ z⟩ ± (tilde V / m) sqrt([⟨(ρ z)^2⟩ - ⟨ρ z⟩^2]/n).    (11.31)
```

基于在区间 [0, 1) 上均匀分布的随机变量 `ξi`、`ηi` 和 `ζi`，可以生成在域 $\tilde{D}$ 内均匀分布的随机点 `(xi, yi, zi)` 为

```
xi = (2ξi − 1) (R + r),   yi = (2ηi − 1) (R + r),   zi = (2ζi − 1) r.      (11.32)
```

程序 11.5 实现了关系式 11.28 到 11.32，并且密度的特定函数形式在函数 `Func` 中编码。

## Listing 11.5 Monte Carlo Evaluation of the Mass Center of a Torus (Python Coding)

```
# Monte Carlo calculation of the mass center of a torus of radii R and r,

# centered at the origin and with Oz as symmetry axis

from math import *

from random import *

def Func(x, y, z):

    global R, r

    Rp = sqrt(x*x + y*y)                     # major radial distance

    dR = R - Rp

    rp = sqrt((dR*dR + z*z))                 # minor radial distance

    dr = 1e0 - rp/r

    return (dr*dr if rp <= r else 0e0)       # zero-padding

#### main
```
