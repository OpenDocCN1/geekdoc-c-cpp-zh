
# Integrates function `Func(x,y,z)` in the cuboid `[ax,bx] x [ay,by] x [az,bz]` using Gauss-Legendre quadratures with (`nx x ny x nz`) integration points

```
x = [0]*nx; wx = [0]*nx

y = [0]*ny; wy = [0]*ny

z = [0]*nz; wz = [0]*nz

(x,wx) = xGaussLeg(ax,bx,nx)          # generate integration points

(y,wy) = xGaussLeg(ay,by,ny)

(z,wz) = xGaussLeg(az,bz,nz)

s = 0e0

for i in range(0,nx):

    sx = 0e0

    for j in range(0,ny):

        sy = 0e0

        for k in range(0,nz):

            sy += wz[k] * Func(x[i],y[j],z[k])

        sx += wy[j] * sy

    s += wx[i] * sx

return s
```

从特定点 $(x,y,z)$ 到旋转轴 Oz 的径向距离，以及分别到管轴（中心圆）的距离由下式给出

$$R' = \sqrt{x^2 + y^2},\quad r' = \sqrt{(R - R')^2 + z^2},\qquad (10.84)$$

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_384_0.png)

FIGURE 10.6 Toroidal integration domain revealing the radial distances R' and r' from the current point (x,y,z) to the symmetry axis Oz and, respectively, to the tube axis.

而环面内部点满足的条件具有非常简单的形式：

$r' \le r.$ \tag{10.85}

我们考虑数值说明的简单但仍现实的情况，密度函数 $f(x,y,z)$ 仅依赖于到管轴的距离 $r'$，并且在环面外消失：

$f(x,y,z)=\begin{cases}(1-r'/r)^2, & r'\le r,\\0, & r'>r.\end{cases}\tag{10.86}$

具体而言，该函数从管轴上的 1 到表面上的 0 抛物线式递减，其积分为 $\frac{1}{3}\pi^2Rr^2\approx 9.8696044$。

采用笛卡尔坐标，直截了当的方法是用一个长方体包围整个环面。然而，利用旋转对称性和相对于 *Oxy*-平面的额外反射对称性，积分域可以简化为 $[0,R+r]\times[0,R+r]\times[0,r]$，位于第一卦限，最终结果相应地乘以 8。

对于积分函数（10.86）的积分，程序 10.19 比较使用了例程 `qSimpson3D` 和 `qGaussLeg3D`。为了符合所有讨论的三维积分器使用的三参数用户函数列表，环面的几何细节（$R$ 和 $r$）通过全局变量传递给 `Func`。出于效率原因，开方始终被乘法取代。

特别地，函数 `qGaussLeg3D` 使用 $200\times200\times50$ 个积分点（如此选择以确保三个笛卡尔方向上节点密度相同）即可以七位有效数字的精度给出积分。另一方面，使用相同的积分网格，函数 `qSimpson3D` 仅能达到低两个数量级的精度。

## Listing 10.19 Integral Over Toroidal Domain Using Cartesian Coordinates (Python Coding)

```python
# Evaluates a 3D integral on a torus using Cartesian coordinates

from math import *

from integral import *

def Func(x, y, z):

    global R, r

    Rp = sqrt(x*x + y*y)                 # major radial distance

    dR = R - Rp

    rp = sqrt(dR*dR + z*z)               # minor radial distance

    dr = 1e0 - rp/r

    return (dr*dr if rp <= r else 0e0)  # zero-padding

#### main

R = 3e0; r = 1e0                        # major & minor torus radii

ax = ay = az = 0e0                      # bounding box: 1st octant

bx = by = R+r; bz = r                   # multiply results with 8

nx = ny = 200                            # equal density of mesh

nz = int(nx * r/(R+r))                   # points along x, y, z

I = 8e0 * qSimpson3D(Func,ax,bx,nx,ay,by,ny,az,bz,nz)

print("I Simpson = ",I)

I = 8e0 * qGaussLeg3D(Func,ax,bx,nx,ay,by,ny,az,bz,nz)

print("I GaussLeg = ",I)                 # result 9.869603...
```

使 `f(x,y,z) = 1` 在所有内部点成立时，积分显然表示环面体积 $(2\pi^2Rr^2 \approx 59.217626)$，这是一个程序的方便测试用例。

对于球坐标中定义的 3D 积分，可以设计出类似于笛卡尔坐标的求积公式：

∫₀ᵃ ∫₀^π ∫₀^{2π} f(r,θ,φ) r² dr sinθ dθ dφ ≈ Σ_{i=1}^{n_r} w_i^{(r)} Σ_{j=1}^{n_θ} w_j^{(θ)} Σ_{k=1}^{n_φ} w_k^{(φ)} f(r_i,θ_j,φ_k), (10.87)

然而，权重也考虑了来自体积元素的补充 r² 和 sinθ 因子。原则上，与笛卡尔情况一样，可以对各个坐标采用相同的单维格式。基于辛普森法的积分器 `qSimpsonSph`（列表 10.20）期望除了描述被积函数的用户函数 `Func` 之外，还需要一个几何参数，即外径极限 `a`。`r`、`θ` 和 `φ` 的积分点数 (`nr`、`nt` 和 `np`) 也必须提供。

在从例程 `xSimpson` 为所有三个球坐标获取通用节点和权重后，函数 `qSimpsonSph` 将径向权重 `wr` 按 `r²` 缩放，并将 θ 积分的角度权重 `wt` 按 `sinθ` 缩放。重新定义权重后，随后的三重求和与笛卡尔坐标的情况类似。

## Listing 10.20 Integrator in Spherical Coordinates Based on Simpson’s Rule (Python Coding)

```python
#================================================================================
def qSimpsonSph(Func, a, nr, nt, np):
#--------------------------------------------------------------------------------
#  Integrates function Func(r,theta,phi) on [0,a] x [0,pi] x [0,2*pi]
#  in spherical coordinates using Simpson’s rule with (nr x nt x np) points
#--------------------------------------------------------------------------------
    if (nr % 2 == 0): nr += 1                # increment nr if even
    if (nt % 2 == 0): nt += 1                # increment nt if even
    if (np % 2 == 0): np += 1                # increment np if even
    r = [0]*nr; wr = [0]*nr
    t = [0]*nt; wt = [0]*nt
    p = [0]*np; wp = [0]*np
    (r,wr) = xSimpson(0e0,a,nr)              # generate integration points
    (t,wt) = xSimpson(0e0,pi,nt)
    (p,wp) = xSimpson(0e0,2e0*pi,np)
    for i in range(0,nr): wr[i] *= r[i] * r[i]      # factors from
    for j in range(0,nt): wt[j] *= sin(t[j])        # volume element
    s = 0e0
    for i in range(0,nr):
        sr = 0e0
        for j in range(0,nt):
            st = 0e0
            for k in range(0,np):
                st += wp[k] * Func(r[i],t[j],p[k])
            sr += wt[j] * st
        s += wr[i] * sr
    return s
```

对于在整个空间上延伸的球坐标积分，高斯求积比经典公式更合适。特别是，径向积分可以最方便地使用高斯-拉盖尔公式 10.79 来执行，该公式专门为半无限区间 [0, +∞) 设计，而角度贡献则可以使用高斯-勒让德求积有效地求值。保持 `qSimpsonSph` 的整体结构，例程 `qGaussSph`（列表 10.21）调用 `xGaussLag` 和 `xGaussLeg` 生成径向和相应的角度节点和权重。

下面，我们以氢原子中 2p 态电子的波函数为例（量子数 n = 2, l = 1, 和 m = 0）。用无量纲径向单位表示（见 Fitts 2002），该波函数为：

Ψ210(r,θ,φ) = 1/(4√2π) r e^(-r/2) cos θ.

其范数由概率密度 |Ψ210(r,θ,φ)|² 的积分给出，

∫₀^∞ ∫₀^π ∫₀^{2π} |Ψ210(r,θ,φ)|² r² dr sin θ dθ dφ = 1,

并且，由于它表示电子在空间中某处被发现的总概率，因此自然等于 1。程序 10.22 比较使用辛普森法则和

## Listing 10.21 Integrator in Spherical Coordinates Based on Gaussian Quadratures (Python Coding)

```python
def qGaussSph(Func, nr, nt, np):
# Integrates function Func(r,theta,phi) on [0,inf] x [0,pi] x [0,2*pi]
# in spherical coordinates using Gauss-Laguerre and Gauss-Legendre formulas
# with (nr x nt x np) points
r = [0]*nr; wr = [0]*nr
t = [0]*nt; wt = [0]*nt
p = [0]*np; wp = [0]*np
(r,wr) = xGaussLag(0e0,nr)      # Gauss-Laguerre radial quadrature
(t,wt) = xGaussLeg(0e0,pi,nt)   # Gauss-Legendre angular quadratures
(p,wp) = xGaussLeg(0e0,2e0*pi,np)
for i in range(0,nr): wr[i] *= r[i] * r[i]      # factors from
for j in range(0,nt): wt[j] *= sin(t[j])        # volume element
s = 0e0
for i in range(0,nr):
    sr = 0e0
    for j in range(0,nt):
        st = 0e0
        for k in range(0,np):
            st += wp[k] * Func(r[i],t[j],p[k])
        sr += wt[j] * st
    s += wr[i] * sr
return s
```

## Listing 10.22 Integral in Spherical Coordinates (Python Coding)

```python
# Evaluates a 3D integral using spherical coordinates
from math import *
from integral import *
def Func(r, theta, phi):              # probability density for 2p state
    c = 1e0/(32e0*pi)
    rcos = r * cos(theta)
    return c * rcos * rcos * exp(-r)
#### main
a = 35e0                             # radial limit
nr = 150; nt = 60; np = 3
I = qSimpsonSph(Func,a,nr,nt,np)
print("I SimpsonSph = ",I)
nr = 3; nt = 9; np = 1
I = qGaussSph(Func,nr,nt,np)
print("I GaussSph   = ",I)
```

## Listing 10.23 Integrator in Cylindrical Coordinates Based on Simpson's Rule (Python Coding)

```python
# ============================================================================
def qSimpsonCyl(Func, a, az, bz, nr, np, nz):
# ----------------------------------------------------------------------------
#   Integrates function Func(r,phi,z) on domain [0,a] x [0,2*pi] x [az,bz]
#   in cylindrical coordinates using Simpson's rule with (nr x np x nz) points
# ----------------------------------------------------------------------------
    if (nr % 2 == 0): nr += 1                 # increment nr if even
    if (np % 2 == 0): np += 1                 # increment np if even
    if (nz % 2 == 0): nz += 1                 # increment nz if even
    r = [0]*nr; wr = [0]*nr
    p = [0]*np; wp = [0]*np
    z = [0]*nz; wz = [0]*nz
    (r,wr) = xSimpson(0e0,a,nr)               # generate integration points
    (p,wp) = xSimpson(0e0,2e0*pi,np)
    (z,wz) = xSimpson(az,bz,nz)
    for i in range(0,nr): wr[i] *= r[i]       # factor from volume element
    s = 0e0
    for i in range(0,nr):
        sr = 0e0
        for j in range(0,np):
            sp = 0e0
            for k in range(0,nz):
                sp += wz[k] * Func(r[i],p[j],z[k])
            sr += wp[j] * sp
```
