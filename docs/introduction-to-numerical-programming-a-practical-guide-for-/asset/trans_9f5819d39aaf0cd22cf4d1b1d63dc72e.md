

## 清单 6.6 Newton–Raphson 法（Python 编码）

```
#================================================================================
def Newton(Func, a, b, x):
#--------------------------------------------------------------------------------
# Determines a real root x of function Func isolated in interval [a,b] by
# the Newton–Raphson method using the analytical derivative. x contains on
# input an initial approximation.
# Error code: 0 - normal execution
#             1 - interval does not contain a root
#             2 - max. number of iterations exceeded
#--------------------------------------------------------------------------------
    eps = 1e-10                     # relative precision of root
    itmax = 100                     # max. no. of iterations

    for it in range(1,itmax+1):
        (f,df) = Func(x)            # function and derivative
        dx = -f/df if fabs(df) > eps else -f   # root correction
        x += dx                     # new approximation
        if ((x < a) or (x > b)): return (x,1)  # [a,b] does not contain a root
        if (fabs(dx) <= eps*fabs(x)): return (x,0)   # check convergence

print("Newton: max. no. of iterations exceeded !"); return (x,2)
```

## 清单 6.7 用于牛顿法的带导数用户函数（Python 编码）

```
def func(x):
    df = 1e0 + exp(-x)
    return (x - exp(-x), df)
```

清单 6.7 以方程 x − e^{−x} = 0 的特殊情况为例，演示了例程 Newton 的用户函数的构造。

在许多实际情况下，直接以可编程形式表示导数 f′(x) 是困难甚至不可能的。在这种情况下，可以求助于数值计算。清单 6.8 中给出的例程 NewtonNumDrv 使用导数的有限前向差分表示，分别基于当前 x 以及该值增加一个小的 dx。除了导数的计算方式不同，以及不再期望用户函数返回导数之外，例程 Newton 和 NewtonNumDrv 是相同的。

与逐次逼近法不同，牛顿法的收敛性对函数 f(x) 的写法不敏感，因为修正项 −f(x_i)/f′(x_i) 中额外除以导数，会在根附近调整迭代函数，以满足定理 6.2 的要求。

具体考虑方程

x − e^{−x} = 0，

与逐次逼近法相反，牛顿法收敛到根 x = 0.567143，无论函数定义为 f(x) = x − e^{−x} 还是 f(x) = e^{−x} − x。事实上，在两种情况下，迭代函数的导数具有相同的表达式 φ′(x) = e^{−x}(x − e^{−x})/(1 + e^{−x})^2，并且对于任何正 x，它都是小于 1 的，如定理所要求。

## 清单 6.8 具有数值导数的牛顿法（Python 编码）

```
# =================================================================================
def NewtonNumDrv(Func, a, b, x):
# ---------------------------------------------------------------------------------
# Determines a real root x of function Func isolated in interval [a,b] by
# the Newton-Raphson method using the numerical derivative. x contains on
# input an initial approximation.
# Error code: 0 - normal execution
#             1 - interval does not contain a root
#             2 - max. number of iterations exceeded
# ---------------------------------------------------------------------------------
    eps = 1e-10                     # relative precision of root
    itmax = 100                     # max. no. of iterations

    for it in range(1,itmax+1):
        f = Func(x)
        dx = eps*fabs(x) if x else eps          # derivation step
        df = (Func(x+dx)-f)/dx                  # numerical derivative
        dx = -f/df if fabs(df) > eps else -f    # root correction
        x += dx                                 # new approximation
        if ((x < a) or (x > b)): return (x,1)   # [a,b] does not contain a root
        if (fabs(dx) <= eps*fabs(x)): return (x,0)   # check convergence

    print("NewtonNumDrv: max. no. of iterations exceeded !"); return (x,2)
```

一般来说，牛顿法比逐次逼近法收敛得快得多。例如，对于方程

x − sin x − 0.25 = 0，

从相同的初始近似 x₀ = 0 出发，牛顿法需要 10 次迭代即可得到具有 10 位精确小数（相对精度 ε = 10⁻¹⁰）的解 x = 1.171229653，而逐次逼近法需要 28 次迭代才能以相同的精度完成计算。为了更全面地了解情况，请参见习题 7.2 中对二分法和割线法的进一步比较。

## 6.6 割线法

割线法代表了牛顿法的高效性与因需要额外计算所求解函数的一阶导数而带来的不便之间的折衷。一个重要的简化为：导数不再出现在逐步修正中，这些修正改为通过一个涉及根的三（而不是两个）个连续近似的递推关系来获得。

假设函数 f(x) 在根附近近似线性，由对应最近近似的点 (xᵢ₋₁, f(xᵢ₋₁)) 和 (xᵢ, f(xᵢ)) 确定的弦（见图 6.7）代替切线，通过其 x 截距提供新的近似 xᵢ₊₁。或者，割线法的递推关系可以通过简单地在牛顿-拉夫森公式中近似导数来获得，

xᵢ₊₁ = xᵢ − f(xᵢ)/f′(xᵢ),

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_163_0.png)

### 图 6.7 割线法中近似根的序列。

使用涉及最近近似的有限（前向）差分表达式：

```
f'(x_i) ≈ [f(x_i) - f(x_{i-1})] / [x_i - x_{i-1}]  (6.28)
```

由此得到的递推关系，

```
x_{i+1} = x_i - f(x_i) * [x_i - x_{i-1}] / [f(x_i) - f(x_{i-1})],  (6.29)
```

能够在先前近似 x_i 和 x_{i-1} 的基础上计算根的近似 x_{i+1}。与本章描述的所有其他方法一样，当根的相对修正减小到低于预定义容差 ε 时，迭代过程终止：

```
|x_{i+1} - x_i| ≤ ε |x_{i+1}|.  (6.30)
```

为了启动递推，原则上可以取任意初始近似 x_0 和 x_1。然而，从单个初始近似 x_0 出发，可以通过应用逐次逼近法的单步步骤获得第二个近似：

```
x_1 = x_0 - f(x_0).  (6.31)
```

割线法与试位法之间的主要区别在于：割线法总是使用两个最近近似，然而它们不一定包围根；而试位法保留两个不一定连续的近似，但它们对应函数值异号，从而隐式地包围根。尽管割线法通常收敛更快，但由于不一定包围根，对于不够光滑的函数，割线法不能保证收敛。

上述算法原理在清单 6.9 中编码为函数 Secant，可以看出，如上所述，它执行一次初始迭代，按照逐次逼近法产生第二个根近似。

## 清单 6.9 割线法（Python 编码）

```
# =================================================================================
def Secant(Func, a, b, x):
# --------------------------------------------------------------------------------
# Determines a real root x of function Func isolated in interval [a,b] by
# the secant method. x contains on entry an initial approximation.
# Error code: 0 - normal execution
#             1 - interval does not contain a root
#             2 - max. number of iterations exceeded
# --------------------------------------------------------------------------------
    eps = 1e-10                     # relative precision of root
    itmax = 1000                    # max. no. of iterations

    x0 = x; f0 = Func(x0)
    x = x0 - f0                     # first approximation
    for it in range(1,itmax+1):
        f = Func(x)
        df = (f-f0)/(x-x0)           # approximate derivative
        x0 = x; f0 = f               # store abscissa and function value
        dx = -f/df if fabs(df) > eps else -f   # root correction
        x += dx                      # new approximation
        if ((x < a) or (x > b)): return (x,1)  # [a,b] does not contain a root
        if (fabs(dx) <= eps*fabs(x)): return (x,0)   # check convergence

print("Secant: max. no. of iterations exceeded !"); return (x,2)
```

对于测试方程

x − sin x − 0.25 = 0,  (6.32)

割线法的表现几乎与牛顿法一样好，从初始近似 x₀ = 0 出发，需要 12 次而不是 10 次迭代即可得到具有 10 位精确小数的解 x = 1.171229653。

## 6.7 Birge–Vieta 法

Birge–Vieta 法代表了牛顿-拉夫森法的一种应用，特别用于求实多项式的零点。具体来说，我们考虑代数方程

Pₙ(x) = 0,  (6.33)

其中 Pₙ(x) 是一个实系数的 n 次多项式：

Pₙ(x) ≡ a₀xⁿ + a₁xⁿ⁻¹ + ⋯ + aₙ₋₁x + aₙ.  (6.34)

在这种情况下，特定根 ξ 的近似序列由递推关系给出

xᵢ₊₁ = xᵢ − Pₙ(xᵢ)/Pₙ′(xᵢ),  i = 0, 1, 2, …  (6.35)

并且需要针对参数序列 xᵢ 计算多项式及其导数。原则上，从各种初始近似出发，该关系可用于确定所有

