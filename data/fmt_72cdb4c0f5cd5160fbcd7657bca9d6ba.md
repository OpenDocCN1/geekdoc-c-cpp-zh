
收敛判定条件（即辛普森公式（而非梯形公式！）的相邻两次逼近之间的相对差值）可以方便地写成

$$|S_k-S_{k-1}|\leq \varepsilon |S_k|.$$

函数 `qSimpsonCtrl` 在清单 10.4 中实现了上述思想，其参数、变量和常数的含义与函数 `qTrapzCtrl` 中赋予的含义保持一致。尽管与梯形法则有着内在联系，但由于辛普森法则提供了更优的逼近（$O(h^4)$ 相比 $O(h^2)$），该过程的收敛速度得以提升，在相同的精度下，通常需要显著更少的对分迭代次数。下一节将给出一个关于自适应梯形法、辛普森法和龙贝格法的比较示例。

## 10.7 龙贝格法

龙贝格法（Romberg 1955）可以看作是 10.6 节中基于辛普森公式的自适应算法向高阶牛顿–柯特斯公式的推广。在龙贝格法中，积分步长对分伴随有基本积分器阶数的额外递归提升，这带来了任何其他基于牛顿–柯特斯公式的求积方案都无法比拟的收敛速度。

在 10.6 节中，我们建立了如下简单关系：

$$S_k=\frac{4T_k-T_{k-1}}{3},$$

其中 $T_k$ 是梯形法则在对分积分网格后得到的逼近（公式 10.28），$S_k$ 是辛普森公式给出的相应逼近（公式 10.32）。为了将此结果推广到高阶牛顿–柯特斯公式，我们将梯形逼近重新标记为 `R_{k,0}`：

$$\begin{aligned}
R_{0,0}&=h_0\left[\frac{f(a)}{2}+\frac{f(b)}{2}\right],\qquad h_0=b-a,\\
R_{1,0}&=h_1\left[\frac{f(a)}{2}+f(a+h_1)+\frac{f(b)}{2}\right],\qquad h_1=\frac{h_0}{2},\\
R_{2,0}&=h_2\left[\frac{f(a)}{2}+f(a+h_2)+f(a+2h_2)+f(a+3h_2)+\frac{f(b)}{2}\right],\qquad h_2=\frac{h_1}{2}.
\end{aligned}$$

对于给定的逼近 `R_{k,0}`，其子区间数以及第 k 次迭代时的相应网格间距分别为

$$n_k=2^k,\qquad h_k=(b-a)/n_k.$$

通过隐式复用先前计算过的被积函数值（避免冗余计算）来实现 `R_{k,0}` 最优计算的递推关系为：

$R_{k,0} = \frac{1}{2} \left[ R_{k-1,0} + h_{k-1} \sum_{i=1}^{n_{k-1}} f\left(a + (i - 1/2)h_{k-1}\right) \right], \quad k = 1,2,\dots,k_{\max}, \qquad (10.40)$

它正是公式 10.30 的直接改写。相应地，辛普森公式给出的前两个逼近为：

$R_{1,1} = \frac{h_1}{3} \left[ f(a) + 4f(a + h_1) + f(b) \right] = \frac{4R_{1,0} - R_{0,0}}{3},$

$R_{2,1} = \frac{h_2}{3} \left[ f(a) + 4f(a + h_2) + 2f(a + 2h_2) + 4f(a + 3h_2) + f(b) \right]$

$= \frac{4R_{2,0} - R_{1,0}}{3}.$

于是，辛普森公式逼近与梯形法则逼近之间的一般关系式 10.33 具有如下形式：

$R_{k,1} = \frac{4R_{k,0} - R_{k-1,0}}{3} = \frac{4R_{k,0} - R_{k-1,0}}{4 - 1}, \quad k = 1,2,\dots,k_{\max}. \qquad (10.41)$

沿着递归提升基本牛顿–柯特斯公式阶数的思路，下一个求积方案的第一个逼近预计将依赖于辛普森公式第一个逼近 `R_{1,1}` 的特征子区间对分后得到的节点，或者说，依赖于第二个逼近 `R_{2,1}` 的节点。这一要求由五点布尔公式*（Boole and Moulton 2003）内在地满足，该公式本质上是利用四阶拉格朗日插值多项式来逼近被积函数：

$\int_{x_1}^{x_5} f(x) dx = \frac{2h}{45} \left[ 7f_1 + 32f_2 + 12f_3 + 32f_4 + 7f_5 \right] - \frac{8h^7 f^{(6)}(\xi)}{945}. \qquad (10.42)$

这个基于布尔公式的第一个逼近可以用积分步长 `h_2` 来表示，`h_2` 对应于整个积分区间 `[a, b]` 经过连续两次对分迭代后的步长：

$R_{2,2} = \frac{2h_2}{45} \left[ 7f(a) + 32f(a + h_2) + 12f(a + 2h_2) + 32f(a + 3h_2) + 7f(b) \right], \qquad (10.43)$

而且，它可以与辛普森公式给出的前两个逼近建立联系：

$R_{2,2} = \frac{16R_{2,1} - R_{1,1}}{15} = \frac{4^2 R_{2,1} - R_{1,1}}{4^2 - 1}. \qquad (10.44)$

可以很容易地预期，基本求积方案阶数的提升意味着特征子区间数量从 $2^k$（辛普森公式为 2）翻倍到 $2^{k+1}$（布尔公式为 4），并且内在地，用于逼近被积函数的拉格朗日插值多项式的阶数也翻倍。因此，除了初始逼近 `R_{0,0}` 外，所有更高阶的逼近都基于具有奇数个节点 $(2^k + 1)$ 的积分网格。

* 曾被误称为“博德公式”（Bode's formula）。

一种替代策略是按*列向左到右*的方式填充数组 (10.46)。然而，这需要预先确定最大二分迭代次数 `k_max`，并在每一列上对*所有*近似值进行评估，直到对某个对角估计 `R_{k,k}` 达到收敛为止。此时，如果 `k < k_max`，则位于第 `k` 行下方已计算的估计值将变得不再需要，从而使算法效率低下。

Romberg 方法 (10.47)–(10.50) 在函数 `qRomberg` 中实现（代码清单 10.5），其参数与例程 `qTrapzCtrl` 和 `qSimpsonCtrl` 相同。代替近似值 `R_{k,j}` 的三角数组，实现仅使用两个一维数组 `r1` 和 `r2` 来保存最近的两个连续行，并在每次子区间二分迭代结束时进行移动。与函数 `qTrapzCtrl` 和 `qSimpsonCtrl` 的情况类似，二分迭代次数限制为 30，这对应于最多 $2^{30}$ 个积分点（标准 C 中 long 类型变量可表示的最大 2 的幂）。

每次积分步长的二分迭代都从基于梯形公式的积分求值开始。然后递归地提高基本求积的阶数并检查过程的收敛性。如果在遍历当前网格点数适用的所有 Newton–Cotes 公式后仍未达到要求的精度 `eps`，则通过加倍子区间数（减半网格间距）准备下一次二分步骤。如果在允许的 `k_max` 次二分迭代内未达到收敛，则发出警告信息。

```
#===============================================================

def qRomberg(Func, a, b, eps = 1e-6):

#  Integrates function Func on interval [a,b] with relative precision eps

#  using the adaptive Romberg method

#===============================================================

    kmax = 30                              # max. no. of step halving iterations

    r1 = [0]*(kmax+1)                       # two consecutive lines

    r2 = [0]*(kmax+1)                       # from the method table

    h = b-a; n = 1

    r1[0] = 0.5*h*(Func(a) + Func(b))       # initial approximation

    for k in range(1,kmax+1):               # step halving loop

        sumf = 0e0

        for i in range(1,n+1): sumf += Func(a+(i-0.5)*h)

        r2[0] = 0.5*(r1[0] + h*sumf)        # trapezoid formula

        f = 1e0

        for j in range(1,k+1):               # increase quadrature order

            f *= 4

            r2[j] = (f*r2[j-1] - r1[j-1])/(f-1)  # new approximation

        if (k > 1):                          # convergence check

            if (fabs(r2[k]-r1[k-1]) <= eps*fabs(r2[k])): break

            if (fabs(r2[k]) <= eps and fabs(r2[k]) <= fabs(r2[k]-r1[k-1])): break

        h *= 0.5; n *= 2                    # halve integration step

        for j in range(0,k+1): r1[j] = r2[j] # shift table lines

    if (k >= kmax):

        print("qRomberg: max. no. of iterations exceeded !")

        k -= 1

    return r2[k]
```

## 代码清单 10.6 自适应求积的应用（Python 编程）

```
# Evaluates an integral using adaptive classical quadratures

from math import *

from integral import *

def Func(x): return (x*x*x) * exp(-x)

#### main

a = 0e0; b = 1e0; eps = 1e-10

print("I TrapzCtrl   = ",qTrapzCtrl(Func,a,b,eps))

print("I SimpsonCtrl = ",qSimpsonCtrl(Func,a,b,eps))

print("I Romberg     = ",qRomberg(Func,a,b,eps))
```

为了评估迄今为止所介绍的自适应求积方法的效率，我们考虑积分

∫₀¹ x³ exp(−x) dx = 6 − 16e⁻¹ = 0.11392894125692...

一个调用自适应积分器（假定为 integral.py 模块的一部分）来求值上述积分的简单程序在代码清单 10.6 中给出。出于数值效率的考虑，在被积函数中不是采用三次方，而更倾向于使用重复乘法。积分由 `qTrapzCtrl`、`qSimpsonCtrl` 和 `qRomberg` 以相对精度 ε = 10⁻¹⁴ 求值，分别在 23、13 和六次二分迭代内完成，这清楚地表明了 Romberg 方法的优越效率。

## 10.8 improper 积分：开型公式

Improper 积分是指积分区间为无穷（第一类），或被积函数在某些点上未定义（第二类）的积分。数学上，两类 improper 积分都意味着在无穷极限或奇异点处取积分的极限，对于第二类积分，首先在奇异点处将积分域分割。下面示例说明了两类 improper 积分的典型特征：

∫₀⁺∞ x exp(−x²) dx = 1/2,  (10.51)
∫₀^∞ sin x / x dx = π/2,  (10.52)
∫₀¹ x⁻¹/² dx = 2.  (10.53)

在前两种情况下，上限 (+∞) 无法在具体的数值求值中实现。此外，第二种被积函数在 0 处不能按原样求值，需要用其已知极限（limₓ→0 sin x / x = 1）来代替。第三种被积函数在 0 处具有可积奇点，但不能在该处实际求值。

对于第一类 improper 积分的具体实现，必须通过逐步扩展积分域来在无穷边界处取数值极限，这由代码清单 10.7 中给出的例程 `qImpropl` 举例说明。参数 `a` 表示有限积分极限，`xinf` 的符号选择积分区间（[a, +∞) 或 (−∞, a]），`eps` 是要求的相对精度。

## 代码清单 10.7 第一类 improper 积分的自适应积分器（Python 编程）

```
# =================================================================================

def qImpropl(Func, a, xinf, eps = 1e-6):

# --------------------------------------------------------------------------------

# Integrates function Func on interval [a,+inf) (for xinf >= 0) or (-inf,a]

# (for xinf < 0) with relative precision eps. On output, xinf contains the

# integration domain limit for which convergence was achieved.

# Calls: qRomberg

# --------------------------------------------------------------------------------

    h = 1e0; x = a      # subinterval length and initial left limit for [a,+inf)

    if (xinf < 0e0): h = -h; x = a + h                     # for (-inf,a]

    s1 = 1e0

    s = 0e0

    while (fabs(s1) > eps*fabs(s) or fabs(Func(x)) > eps):

        s1 = qRomberg(Func,x,x+fabs(h),eps)               # integral for [x,x+h]

        s += s1                                           # update total integral

        x += h                                            # shift interval [x,x+h]

    xinf = x                                            # final "infinite" boundary

    return (s, xinf)
```

从技术上讲，部分积分 `s1` 被加到积分估计 `s` 中，用于迭代移动的子区间，同时监测相对误差的减小和被积函数的渐近消失。原则上，可以采用迄今为止描述的任何自适应求积方法来求值部分积分，并且在达到所需精度之前继续该过程。积分子区间的大小（实现中的 `h`）并不重要，因为过高的估计值最多只会在积分区间最后一次扩展时造成浪费的计算。在输出时，`xinf` 包含积分已收敛的实际极限。

我们现在转向第二类 improper 积分的求值。特别是，在内部可积奇点的情况下，域可以分解为奇点成为部分积分边界的区域，在这些区域内被积函数在所有内部点上连续。然而，考虑到具体的计算，迄今为止讨论的闭式算法由于显式涉及积分边界而被证明是不够的。相反，可以开发所谓的开型求积算法，它们仅使用奇异边界周围的内部点。显然，即使是这些算法对于发散积分，如 ∫₀¹ x⁻ᵖ dx，其中 p > 1 也是无用的。

基本思想是 (1) 创建一个排除奇点的受限“核心”区间，在该区间内可以成功应用闭式积分算法之一，以及 (2) 通过不断添加奇异边界点附近的贡献来迭代修正总积分，直到达到要求的精度。

假设一般情况下 `a` 和 `b` 都是奇异点，积分区间 `[a,b]` 实际上被划分为三个区域：“左”区间 `[a, a + h₀]`、“核心”区间 `[a + h₀, b − h₀]` 和“右”区间 `[b − h₀, b]`，其中 `h₀` 等于整个区间的某个分数。特别地，假设 `a` 为奇异点，在其邻域 `[a, a + h₀]` 内，通过从核心区间向 `a` 逐渐扩展的连续减半子区间来添加对积分的贡献（图 10.4）。

子区间 `[xₖ⁽ᵃ⁾, xₖ⁽ᵃ⁾ + hₖ]` 的左边界 `xₖ⁽ᵃ⁾` 的序列由下式给出

h₀ = (b − a)/10,
 hₖ = hₖ₋₁/2,   xₖ⁽ᵃ⁾ = a + hₖ,   k = 1,2,…

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_370_0.png)

图 10.4 第二类广义积分：奇异边界 a 附近 [a, a + h0] 内对部分积分有贡献的递归二分区间序列。

### 代码清单 10.8 第二类广义积分的自适应积分器（Python 编码）

```
#================================================================================
```
