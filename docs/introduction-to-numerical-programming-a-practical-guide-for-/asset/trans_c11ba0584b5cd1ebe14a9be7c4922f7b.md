

```
ht*(c1*f1[i] + c3*f3[i] + c4*f4[i] + c5*f5[i] + c6*f6[i])       # error estimate
erri = ht*(e1*f1[i] + e3*f3[i] + e4*f4[i] + e5*f5[i] + e6*f6[i])
erri = fabs(erri/yt[i])
if (err < erri): err = erri

f = 1e0                                      # scaling factor for step size
if (err): f = 0.9e0*pow(eps/err,1e0/p)
if (f > 5e0): f = 5e0                       # prevent increase > 5x
ht1 = f * ht                                 # guess for next step size
if (err <= eps): break                       # precision attained: exit
ht = ht1                                     # reduce step size and repeat

if (it > itmax): print("RKFehlberg: max. no. of iterations exceeded !")
for (i in range(1,n+1)): y[i] = yt[i]       # update y with the best solution
return (ht, ht1)
```

与 RungeKutta 例程的情况一样，我们实际上并不直接计算系数 \(k_i\) 本身，而是计算右端函数 \(f\) 的相关值，并将它们存储在局部数组 f1、f2、f3、f4、f5 和 f6 中。其余方面，积分步长的控制机制与 RKadapt 中实现的机制相同。

步长缩放循环的退出条件是解分量的最大相对误差 err 降到期望的相对容差 eps 以下。无论如何，步长增加超过 5 倍的情况都会被阻止。RKFehlberg 中编码的特定 Runge–Kutta–Fehlberg 系数可以方便地替换为其他嵌入式自适应 ODE 求解器特有的系数。

为了说明 RKFehlberg 求解器的运行方式，我们考虑一个具有强不连续系数的二阶 ODE 的柯西问题：

$$y'' = f(t)y,\quad y(0)=0,\quad y'(0)=1,$$  (12.53)

$$f(t)=\begin{cases}1, & 0\le t\le 5,\\-100, & t>5.\end{cases}$$

可以容易地证明，精确解析解由两个在函数形式上不同的片段组成——一个快速增长的双曲正弦函数，以及一组剧烈振荡的谐波函数的组合：

$$y(t)=\begin{cases}\sinh t, & 0\le t\le 5,\\\sinh 5\cos 10(t-5)+\frac{1}{10}\cosh 5\sin 10(t-5), & t>5.\end{cases}$$

显然，固定的积分步长无法在整个定义域上保证均匀的精度。步长既要小到足以应对函数的不连续性并重现振荡行为，又会在双曲部分造成计算浪费。在这种情况下，自适应求解器无疑是首选方法。程序 12.7 在 Func 中实现了等价的一阶 ODE 系统的右端项，并反复调用例程 RKFehlberg 将解推进到 tmax。传播循环用前一次调用 RKFehlberg 返回的猜测值 ht1 更新试探步长 ht。解 \(y(t)\) 显示在图 12.4 的左面板，而所用步长的显著时间依赖性则绘于右面板。对于相同的相对容差 \(\varepsilon=10^{-8}\)，可以看到两种形式的解所需的步长相差一个数量级以上。

## 代码清单 12.7 自适应步长控制的应用（Python 代码）

```
# Solves a Cauchy problem with adaptive step size control
from math import *
from ode import *

def Func(t, y, f):                     # RHSs of ODEs
    f[1] = y[2]
    f[2] = (1e0 if t < 5e0 else -100e0) * y[1]

# main

y0 = 0e0; dy0 = 1e0                     # initial values
tmax = 10e0                             # time span
ht = 0.01e0                             # step size
eps = 1e-8                              # relative solution precision

n = 2                                   # number of 1st order ODEs
y = [0]*(n+1)                           # solution components

out = open("ode.txt","w")             # open output file
out.write("      t           y           h\n")

t = 0e0
y[1] = y0; y[2] = dy0                    # initial values
out.write("{0:10.5f}{1:10.5f}{2:10.5f}\n".format(t,y[1],ht))

ht1 = ht                               # initial step size guess
while (t+ht <= tmax):                   # propagation loop
    ht = ht1                            # update initial step size with guess
    (ht, ht1) = RKFehlberg(t,ht,eps,y,n,Func)
    t += ht

    out.write("{0:10.5f}{1:10.5f}{2:10.5f}\n".format(t,y[1],ht))

out.close()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_466_0.png)

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_466_1.png)

图 12.4 使用基于 Runge–Kutta–Fehlberg 方法的自适应步长控制求解柯西问题 12.53（左面板）。所用积分步长的时间演化（右面板）。

## 12.6 二阶常微分方程的求解方法

二阶常微分方程（ODE）的柯西问题出现在应用科学和工程的许多领域，最常描述所关注连续量的时间或空间依赖性。尽管两个典型的二阶 ODE——牛顿第二定律和一维不含时薛定谔方程——看起来可能截然不同，但适用于求解它们的数值方法共享许多共同特征。

因此，让我们考虑如下一般柯西问题：

d²y/dt² = f(t, y, y')  (12.54)
y(t₀) = y₀,    y'(t₀) = y'₀.  (12.55)

为求解该问题而开发的算法通常源自 Taylor 级数法（见 12.2 节），其中一阶导数 y'（在底层形式体系中通常具有明确的意义）与解一起被显式传播。

考虑自变量的两个相邻值 tₘ 和 tₘ₊₁，它们相隔 h = tₘ₊₁ − tₘ，从已知初值 yₘ ≡ y(tₘ) 和 y'ₘ ≡ y'(tₘ) 出发，可以基于 y 和 y' 的 Taylor 展开将解传播到 tₘ₊₁，其中二阶导数 y'' 直接由 ODE 确定。按算法顺序排列的相关方程为：

y''ₘ = f(tₘ, yₘ, y'ₘ),
yₘ₊₁ = yₘ + h y'ₘ + ½ h² y''ₘ + O(h³),  (12.56)
y'ₘ₊₁ = y'ₘ + h y''ₘ + O(h²).

基于这些方程构建的所有算法的一个典型特征是，每个传播步骤只需对 ODE 右端的二阶导数进行一次求值。实际实现中使用的往往是这些方程的变体，分别针对简单性、精度或存储效率进行了调整。

最简单的变体是 Euler 方法，它相当于 12.3 节所述方法在二阶 ODE 情形下的对应版本。Euler 方法本质上意味着在位置和速度的传播子中都保留线性近似：

y''ₘ = f(tₘ, yₘ, y'ₘ),
yₘ₊₁ = yₘ + h y'ₘ + O(h²),  (12.57)
y'ₘ₊₁ = y'ₘ + h y''ₘ + O(h²).

由于它仅使用来自 tₘ 的信息（而不使用 tₘ₊₁ 的信息），该格式也被称为起点近似，其明显优点是易于实现。

尽管 Euler 方法简单诱人，但由于其不可忽视的缺点，很难被推荐。首先，其全局截断误差为 O(h)，是二阶 ODE 求解器中阶数最低的。其次，由于截断误差的快速传播，它常常产生不稳定的解，尤其是对于振荡系统。第三，由于它仅使用来自 tₘ 的信息，从 tₘ 到 tₘ₊₁ 的传播在时间上是不可逆的（传播子在 t 中不对称）。

所谓 Euler–Cromer 方法（Cromer，1981）使用相同的 Taylor 级数 O(h) 近似，但非常重要的是，它弥补了 Euler 方法的不稳定性。基本关系式可由 y'ₘ₊₁ 和 yₘ₊₁ 的方程简单反演，并在后一式中使用更新后的值 y'_{m+1} 代替初始导数 y'_m 而形式上得到：y''_m = f(t_m, y_m, y'_m), y'_{m+1} = y'_m + h y''_m + O(h^2), y_{m+1} = y_m + h y'_{m+1} + O(h^2). (12.58)

在实现中，先计算 y'_{m+1} 然后在 y_{m+1} 中使用它，使得同一个程序变量可以同时表示 y'_m 和 y'_{m+1}。此外，使用更新后的导数（即同时来自 t_m 和 t_{m+1} 的信息）被证明能大幅改善解的稳定性（Cromer，1981）。不过，就解精度而言，Euler–Cromer 方法保持了与原始 Euler 方法相同的低阶 O(h)。

下文考虑的速度 Verlet 方法（Swope 等，1982）属于一族代数等价的 O(h^2) 算法，其中包括原始 Verlet 方法（Verlet，1967）和蛙跳法（Hockney 和 Eastwood，1988）。一般而言，这些方法用于分子动力学模拟中求解牛顿运动方程（Rapaport，2004），但也可用于求解其他二阶 ODE 的初值问题。Euler/Euler–Cromer 与速度 Verlet 算法的主要区别在于，后者还保留了解 Taylor 展开中的二次项。具体地，被传播的解可依次表示为

y_{m+1} = y_m + h y'_m + 1/2 h^2 y''_m + O(h^3) = y_m + h (y'_m + 1/2 h y''_m) + O(h^3) = y_m + h y'_{m+1/2} + O(h^3).

解 y_{m+1} 看起来是基于区间中点（即 t_{m+1/2} = t_m + h/2）处的导数 y'_{m+1/2} 从 t_m 到 t_{m+1} 线性传播的。从另一个角度看，y'_{m+1/2} 可以视为区间 [t_m, t_{m+1}] 上的平均一阶导数。将传播后的解 y_{m+1} 代入 ODE，可确定区间端点处的二阶导数 y''_{m+1}，这反过来又使一阶导数 y'_{m+1/2} 能够传播到 t_{m+1}。

速度 Verlet 方法的传播公式序列最终具有如下形式：

y'_{m+1/2} = y'_m + 1/2 h y''_m + O(h^2),
y_{m+1} = y_m + h y'_{m+1/2} + O(h^3),
y''_{m+1} = f(t_{m+1}, y_{m+1}, y'_{m+1/2}),
y'_{m+1} = y'_{m+1/2} + 1/2 h y''_{m+1} + O(h^2). (12.59)

除了保证 O(h^2) 精度（比 Euler 和 Euler–Cromer 方法高一阶）之外，速度 Verlet 方法还以其稳定性和低存储需求著称，这得益于算法中所有量在传播过程中都可以覆盖自身的可能性。不过，有一点需要特别强调。某一步确定的二阶导数 y''_{m+1} 不仅用于在第二个半区间（从 t_{m+1/2} 到 t_{m+1}）传播一阶导数 y'_{m+1/2}，还要用于在下一步的前半个区间（从 t_{m+1} 到 t_{m+3/2}）推进 y'_{m+1}。因此，除了 y_{m+1} 和 y'_{m+1} 之外，二阶导数 y''_{m+1} 也需要保存以供下一步使用。

Euler、Euler–Cromer 和速度 Verlet 方法求解单个二阶 ODE 初值问题的实现见代码清单 12.8。

