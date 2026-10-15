

从实际角度看，根分离过程意味着确定函数 f(x) 在一个足够精细的划分 {x_m} 各点上的符号，其选择在很大程度上取决于函数本身的特殊性。如果子区间 [x_m, x_{m+1}] 足够小，根据上述定理，每个子区间至多包含方程 f(x) = 0 的一个实根。因此，满足 f(x_m)f(x_{m+1}) > 0 的区间不包含任何根，而满足 f(x_m)f(x_{m+1}) ≤ 0 的区间包含一个根。

## 6.2 二分法

考虑方程

```
f(x) = 0,
```

其中实函数 f(x) 在区间 [a, b] 上连续。我们假设通过先前的根分离过程，方程 6.2 在 [a, b] 内至多有一个根。用 ξ 表示该根，可能出现以下情况：

- a. 如果 f(a) = 0，则根为 ξ = a；
- b. 如果 f(b) = 0，则根为 ξ = b；
- c. 如果 f(a)f(b) < 0，则根为内部点之一，ξ ∈ (a, b)；
- d. 如果 f(a)f(b) > 0，则在 [a, b] 中不存在根 ξ。

考虑到情况 (c)，它是唯一需要实际计算的非平凡情况，为了找到所包含的根，我们将区间 [a, b] 通过中点 x0 = (a + b)/2 分成两个相等子区间，如图 6.3 所示。特别地，如果 f(x0) = 0，则 ξ = x0 为所求根。在相反情况下，我们选择函数在其端点处符号相反的子区间 [a1, b1]，该区间显然仍限制根，并保存其边界。可能出现以下情况之一

```
a1 = a0,  b1 = x0,   if f(a)f(x0) < 0,
a1 = x0,  b1 = b0,   if f(a)f(x0) > 0.
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_149_0.png)

图 6.3 二分法搜索区间的减半过程。

新的区间 [a₁, b₁] 再次被对半分割，执行与上述类似的符号测试。通过继续此过程，经过 i 次迭代后，通过点 xᵢ₋₁ = (aᵢ₋₁ + bᵢ₋₁)/2 对区间 [aᵢ₋₁, bᵢ₋₁] 进行二分，可得到边界区间 [aᵢ, bᵢ]。因此，新的边界为：

```
aᵢ = aᵢ₋₁,   bᵢ = xᵢ₋₁,   if f(aᵢ₋₁)f(xᵢ₋₁) < 0,
 aᵢ = xᵢ₋₁,   bᵢ = bᵢ₋₁,   if f(aᵢ₋₁)f(xᵢ₋₁) > 0.  (6.3)
```

对于所有先前的边界区间，显然函数 f(x) 在最近一个区间的两端变号，

```
f(aᵢ)f(bᵢ) < 0,  (6.4)
```

其长度与初始区间之比为

```
bᵢ − aᵢ = (b − a)/2ⁱ.  (6.5)
```

通过其中点对最近区间进行二分，

```
xᵢ = ½(aᵢ + bᵢ),  (6.6)
```

可得到数值根 ξ = xᵢ，或新的边界区间 [aᵢ₊₁, bᵢ₊₁]。

由于连续区间的左边界 a₀, a₁, …, aᵢ 形成有界非递减序列，右边界 b₀, b₁, …, bᵢ 形成有界非递增序列，由方程 6.5 取极限可知，序列 {aᵢ} 和 {bᵢ} 有共同极限

```
ξ = limᵢ→∞ aᵢ = limᵢ→∞ bᵢ.
```

此外，根据函数 f(x) 的连续性，由不等式 (6.4) 取极限 i → ∞ 可得 [f(ξ)]² ≤ 0，由此 f(ξ) = 0，意味着 ξ 是方程 6.2 的根。

显然，实际中只能执行有限次迭代，因此只能确定根的近似值。迭代过程可在满足以下一个或两个条件时以根 ξ = xᵢ 终止：

```
|f(xᵢ)| ≤ ε,      bᵢ − aᵢ ≤ ε,  (6.7)
```

其中 ε > 0 为预定义容差。对于实际实现，更有用的停止准则可直接与计算根的预期有效数字位数相关，由边界区间宽度给出的相对误差估计提供：

```
|(bᵢ − aᵢ)/xᵢ| ≤ ε.
```

该准则的更方便形式仍基于相对误差，但避免了偶然的除零，即

```
|bᵢ − aᵢ| ≤ ε |xᵢ|.  (6.8)
```

所公开算法的直接实现由第 6.1 节中的函数 Bisect 表示，其输入参数为用户函数 Func 的实际名称，以及搜索区间 [a, b] 的极限，在该区间内假定分离的根存在。Bisect 返回计算得到的根 x，以及错误索引，等于 0——表示正常

## 6.2 二分法求函数的实根（Python 编码）

```
# Real roots of a real function by the bisection method
from math import *
from roots import *

def func(x):
    return (x*x*x*x - 5e0*x*x + 4e0) * sin(2e0*x)

# main

xmin = -3.5e0                     # limits of root search domain
xmax =  3.5e0
 h = 0.1e0                        # width of root separation intervals

a = xmin
while (a < xmax):                # root separation loop
    b = a + h                     # search interval [a,b]
    (x,iierr) = Bisect(func,a,b)
    if ((iierr == 0) and (x != b)):
        print('x = {0:8.5f} in ({1:6.2f},{2:6.2f})   f(x) = {3:7.0e}'.format(x,a,b,func(x)))
    a = b                         # shift left boundary
```

## 6.3 假位法

与二分法类似，假位法（或称正割法）旨在寻找方程 f(x) = 0 的实根 ξ，该根已隔离在区间 [a, b] 中，其两端函数取相反符号（f(a)f(b) < 0）。主要区别在于选择后续边界区间 [a₁, b₁], [a₂, b₂], …, [aᵢ, bᵢ] 的方式，在假位法中，这些区间并非通过二分得到，而是通过按函数值之比 f(aᵢ)/f(bᵢ) 将当前区间 [aᵢ, bᵢ] 分割得到。此过程在试错步骤序列中重复，用“假”试验值代替未知量以逐步改进解的近似。

从几何上看，如图 6.4 所示，假位法意味着用点 (aᵢ, f(aᵢ)) 和 (bᵢ, f(bᵢ)) 定义的弦代替函数 f(x)。由弦方程，

(xᵢ − aᵢ)/(bᵢ − aᵢ) = −f(aᵢ)/(f(bᵢ) − f(aᵢ))

可 readily 得到与 x 轴交点的坐标：

xᵢ = aᵢ f(bᵢ) − bᵢ f(aᵢ) / (f(bᵢ) − f(aᵢ)).   (6.9)

经过一定次数的迭代，可得到数值精确根 ξ = xᵢ，使得 f(xᵢ) ≤ ε，或得到由下式定义的区间序列 [a₀, b₀], [a₁, b₁], …, [aᵢ, bᵢ], …

aᵢ₊₁ = aᵢ,   bᵢ₊₁ = xᵢ,   if f(aᵢ)f(xᵢ) < 0,
aᵢ₊₁ = xᵢ,   bᵢ₊₁ = bᵢ,   if f(aᵢ)f(xᵢ) > 0,   (6.10)

并满足

f(aᵢ₊₁)f(bᵢ₊₁) < 0.   (6.11)

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_153_0.png)

图 6.4 假位法中通过连接点 (a_i, f(a_i))，și (b_i, f(b_i)) 的弦对搜索区间进行分割。

假位法被编码为第 6.3 节中的例程 FalsPos。其总体构造原则、输入/输出参数和功能与前一节描述的函数 Bisect 相同，因此在应用中两者可互换。

## 第 6.3 节 假位法（Python 编码）

```
================================================================================
def FalsPos(Func, a, b):
#--------------------------------------------------------------------------------
# Determines a real root x of function Func isolated in interval [a,b] by
# the false position method
# Error code: 0 - normal execution
#             1 - [a,b] does not isolate one root or contains several roots
#             2 - max. number of iterations exceeded
#--------------------------------------------------------------------------------
    eps = 1e-10                         # relative precision of root
    itmax = 100                         # max. no. of iterations

    x = a; fa = Func(x)                 # is a the root?
    if (fabs(fa) == 0e0): return (x,0)
    x = b; fb = Func(x)                 # is b the root?
    if (fabs(fb) == 0e0): return (x,0)

    if (fa*fb > 0): return (x,1)        # [a,b] does not contain a root
                                    # or contains several roots
    for it in range(1,itmax+1):
        x = (a*fb - b*fa)/(fb - fa)     # new approximation
        fx = Func(x)
        if (fa*fx > 0):
            dx = x - a; a = x; fa = fx  # choose new bounding interval
        else:
            dx = b - x; b = x; fb = fx
        if ((fabs(dx) <= eps*fabs(x)) or (fabs(fx) <= eps)): return (x,0)

    printf("FalsPos: max. no. of iterations exceeded !"); return (x,2)
```

