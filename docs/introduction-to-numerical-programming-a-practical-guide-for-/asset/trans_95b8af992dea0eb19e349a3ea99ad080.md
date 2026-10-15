

P_i^{(m)}(x) = (x - x_{m+i}) P_i^{(m-1)}(x) + (x_i - x) P_{i+1}^{(m-1)}(x) / (x_i - x_{m+i}),
 m = 1,2,...,n-1,   i = 1,2,...,n - m.  (9.24)

在依次推进的每一列 m 中，行索引 i 取 n − m 个值，比前一列少一个。每一对 P_i^{(m-1)}(x) 和 P_{i+1}^{(m-1)}(x) 产生一个新值 P_i^{(m)}(x)，此后 P_i^{(m-1)}(x) 不再需要。因此，在具体实现中，不需要二维数组，只需一个向量来存储当前列的插值多项式值 P_i^{(m)}(x)，用 P_i^{(m)}(x) 替换 P_i^{(m-1)}(x)。

最终插值 P_{n-1}(x) ≡ P_1^{(n-1)}(x) 与其两个前驱值之一（例如 P_2^{(n-2)}(x)）之差，为用拉格朗日多项式逼近列表函数关系时的绝对误差提供了一个有用且易于实现的估计：

Δ = | P_1^{(n-1)}(x) − P_2^{(n-2)}(x) | .

清单 9.4 中给出的 Neville 方法实现，其参数含义与上一节讨论的 Lagrange 例程相同。x 和 y 是输入时包含 n 个数据点坐标的数组，xi 是要求计算插值的自变量。除了通过函数名返回插值结果外，参数 err 用于返回相关的误差估计。

在清单 9.5 所示的 Neville 函数使用示例中，被插值的数据集与上一节程序 9.3 所用的数据集相同。从图 9.3 可以看出，被建模的函数 f(x) = 1/x 恰好穿过与插值值相关联的误差条。但值得注意的是，在插值出现虚假振荡的区域，估计误差相当大。

## 清单 9.4 基于 Neville 算法的插值（Python 代码）

```
#============================================================
def Neville(x, y, n, xi):
#------------------------------------------------------------
# Evaluates the Lagrange interpolating polynomial of n data points at xi by
# Neville’s method and returns an estimate of the absolute error
# x[] - x-coordinates of data points
# y[] - y-coordinates of data points
# n  - number of data points
# xi - interpolation argument
# err - estimate of the absolute error (output)
#------------------------------------------------------------
    p = [[0]*(n+1) for i in range(n+1)]      # values of successive interpolants

    for i in range(1,n+1): p[i] = y[i]       # initialize with 0-order polynomial

    for m in range(1,n):                     # loop over columns of scheme array
        for i in range(1,n-m+1):             # increase polynomial order
            p[i] = ((xi-x[m+i])*p[i] + (x[i]-xi)*p[i+1]) / (x[i]-x[m+i])

    yi = p[1]                                # polynomial value
    err = fabs(p[1] - p[2])                  # error estimate

    return (yi, err)
```

## 清单 9.5 使用 Neville 方法进行插值（Python 代码）

```
# Interpolation by Neville’s algorithm
from modfunc import *

# main

n = 8                                         # number of data points
ni = 50                                       # number of interpolation points

x = [0]*(n+1)                                 # data points
y = [0]*(n+1)

x[1] = 0.15; x[2] = 0.2; x[3] = 0.3; x[4] = 0.5       # data points:
x[5] = 0.8 ; x[6] = 1.1; x[7] = 1.4; x[8] = 1.7       # f(x) = 1/x
for i in range(1,n+1): y[i] = 1e0/x[i]

out = open("interpol.txt","w")                     # open output file
out.write("      x            y            xi            yi            err\n")
h = (x[n]-x[1])/(ni-1)
for i in range(1,ni+1):
    xi = x[1] + (i-1)*h                             # interpolation argument
    (yi,err) = Neville(x,y,n,xi)                    # interpolant value
    if (i <= n):
        out.write("{0:12.3e}{1:12.3e}{2:12.3e}{3:12.3e}{4:12.3e}\n".format(x[i],y[i],xi,yi,err))
    else:
        out.write("{0:36.3e}{1:12.3e}{2:12.3e}\n".format(xi,yi,err))
out.close()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_296_0.png)

图 9.3 在虚假振荡情形下 Neville 插值及其相关误差条的图示。插值数据采样自函数 f(x) = 1/x。

## 9.4 三次样条插值

前两节中的应用表明，拉格朗日多项式作为覆盖整个列表数据范围的单一插值多项式时，其主要缺点是可能出现虚假振荡。这一现象可归因于插值多项式通常具有较高的次数，以及相应的大量零点，而这些零点直接由被插值的数据点个数决定。显然，若要理想地将多项式次数降到合理的光滑度，可以在总区间的相邻子区间（数据点子集）上分别考虑较低次数的插值多项式。这种方法称为分段多项式插值。

插值多项式在不同子区间上的各段限制原则上可以是相互独立的。然而在这种情况下，无法保证插值在子区间端点处的可微性。如果整体光滑度（用连续导数的最高阶数表示）很重要，则必须对这些限制施加额外约束，以确保它们在子区间边界处直到某一阶的导数连续。这种带有耦合插值限制的分段多项式逼近称为样条插值，而这些限制本身称为样条。

“样条”函数最初受到“绘图员样条”的启发。在计算机时代之前，绘图员样条是技术制图中用来通过给定点塑造平滑平面曲线的工具。这种工具由一条柔性条带组成，放置在水平绘图板上，有时通过固定两端使其张紧，并通过销钉固定或在某些点悬挂重物产生的摩擦阻力，使其保持所需的弯曲形状。样条会呈现与最小应变能相对应的形状，也就隐式地对应最小曲率（曲率与应变能成正比）。样条函数旨在模仿绘图员样条，具有最小曲率的显著特性，从而减少了在插值节点之间出现振荡的不利现象，而这种振荡正是高次插值多项式所特有的。

设 Δ 为区间 [α, β] 的一个分割，

Δ : α = x₁ < x₂ < ⋯ < xₙ = β,

且 f: [α, β] → ℝ 是一个列表函数关系：

yᵢ = f(xᵢ), i = 1, 2, …, n.

为了对与分割点不同的自变量处的 f(x) 进行建模，我们构造分段样条插值函数。我们称相对于分割 Δ 的 m 阶样条插值为函数 S : [α, β] → ℝ，其在子区间 [xᵢ, xᵢ₊₁] 上的限制 Sᵢ(x) 是 m 次多项式（样条）。这样定义的分段插值函数属于 C^{m−1}[α, β] 类，即其前 (m − 1) 阶导数在整个区间 [α, β] 上连续，而第 m 阶导数在节点 xᵢ 处不连续。

最广泛使用的样条限制是三次多项式，称为三次样条：

Sᵢ(x) = Aᵢx³ + Bᵢx² + Cᵢx + Dᵢ, (9.25)
x ∈ [xᵢ, xᵢ₊₁], i = 1, 2, …, n − 1.

具有这些限制的插值函数 S 显然属于 C²[α, β] 类，即它二次连续可微。三次样条一方面为大多数实际应用保证了足够的整体光滑性，另一方面由于其低阶性而不易引发振荡。此外，由于其函数形式简单，它们为多种积分和微分格式提供了基础。

原则上，样条系数 Aᵢ、Bᵢ、Cᵢ 和 Dᵢ 可由插值节点 xᵢ 处的连续性和插值条件确定：

S(xᵢ) = yᵢ, i = 1, 2, …, n. (9.26)

