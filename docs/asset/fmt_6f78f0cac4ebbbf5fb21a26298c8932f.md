
![](img/5c6c126e3d8cf2b3029f4242e9ad2887_442_0.png)

FIGURE 11.8 Monte Carlo estimates of integral (11.44) (left panel) and associated standard deviations (right panel) using uniform, Gaussian, and exponential sampling (lowest log–log dependence).

## PROBLEM 11.3

构建 10⁶ 个随机偏差的直方图，这些随机偏差在范围 [0,1) 内均匀生成，由例程 `random`（基于内置随机数生成器）、`randLCG1`（使用 Press et al. 2007 中的规范的线性同余生成器）、`randLCG2`（基于 Rapaport 2004 中的规范的线性同余生成器）以及分别 `randMCG`（George Marsaglia 的乘法-进位生成器）生成，这些例程包含在库 `random1.py` 和分别 `random.h` 中。

对于直方图数据的初始化、累积和归一化，使用例程 `HistoBin`，对于绘制直方图，使用样式参数 `sty` 设置为 4 的函数 `Plot`。两个例程都是图形模块 `graphlib.py` 和分别 `graphlib.h` 的一部分。

通过相应直方图的均匀性评估随机数生成器的质量。

## Solution

Python 实现见第 11.13 节列表，C/C++ 版本作为补充材料提供（`P11-RandUni.cpp`）。生成的随机分布的直方图见图 11.9。

## PROBLEM 11.4

构建 10⁶ 个具有正态（高斯）分布的随机偏差的直方图，由例程 `randNrm`（基于中心极限定理）、`randNrm2`（基于极坐标变量变换）和 `randMet`（基于 Metropolis 算法）生成。对于 `randMet` 考虑大小为 δ = 0.1 和 δ = 0.5 的超立方体采样。

### Listing 11.13 Generation of Random Variables with Uniform Distribution (Python Coding)

```
# Generation of random numbers with uniform distribution

from random1 import *

from graphlib import *

#### main

n = 21                                         # number of bin boundaries

nrnd = 1000000                                 # number of random numbers

x = [0]*(n+1); y = [0]*(n+1)                   # plotting points

seed()

GraphInit(1200,800)

a = 0e0; b = 1e0

HistoBin(0e0,a,b,x,y,n,0)                      # initialize histogram

for irnd in range(1,nrnd+1): HistoBin(random(),a,b,x,y,n,1)

HistoBin(0e0,a,b,x,y,n,2)                      # normalize histogram

Plot(x,y,n,"blue",4,0.10,0.45,0.60,0.90,"x","n",

     "Built-in RNG")

                                         # Linear Congruential Generator 1

HistoBin(0e0,a,b,x,y,n,0)                      # initialize histogram

randLCG1(0)                                    # initialize RNG

for irnd in range(1,nrnd+1): HistoBin(randLCG1(1),a,b,x,y,n,1)

HistoBin(0e0,a,b,x,y,n,2)                      # normalize histogram

Plot(x,y,n,"blue",4,0.60,0.95,0.60,0.90,"x","n",

     "Linear Congruential Generator 1")

                                         # Linear Congruential Generator 2

HistoBin(0e0,a,b,x,y,n,0)                      # initialize histogram

randLCG2(0)                                    # initialize RNG

for irnd in range(1,nrnd+1): HistoBin(randLCG2(1),a,b,x,y,n,1)

HistoBin(0e0,a,b,x,y,n,2)                      # normalize histogram

Plot(x,y,n,"blue",4,0.10,0.45,0.10,0.40,"x","n",

     "Linear Congruential Generator 2")

                                         # Multiply-with-Carry Generator

HistoBin(0e0,a,b,x,y,n,0)                      # initialize histogram

randMCG(0)                                     # initialize RNG

for irnd in range(1,nrnd+1): HistoBin(randMCG(),a,b,x,y,n,1)

HistoBin(0e0,a,b,x,y,n,2)                      # normalize histogram

Plot(x,y,n,"blue",4,0.60,0.95,0.10,0.40,"x","n",

     "Multiply-with-Carry Generator")

MainLoop()
```

对于直方图数据的初始化、累积和归一化，使用例程 `HistoBin`，对于绘制直方图，使用样式参数 `sty` 设置为 4 的函数 `Plot`。两个例程都包含在 `graphlib.py` 和分别 `graphlib.h` 中。

## Solution

Python 实现见第 11.14 节列表，C/C++ 版本作为补充材料提供（`P11-RandNrm.cpp`）。生成的随机分布的直方图见图 11.10。

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_444_0.png)

图 11.9 由例程 `random`、`randLCG1`、`randLCG2` 和 `randMCG` 生成的 10⁶ 个均匀随机偏差的直方图。

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_444_1.png)

图 11.10 由例程 `randNrm`、`randNrm2` 和 `randmet` 生成的具有高斯分布的 10⁶ 个随机偏差的直方图。

```python
# Generation of random numbers with normal distribution
from math import *
from random1 import *
from graphlib import *

def wMet(x): return exp(-0.5*x*x)                 # distribution for randMet

#### main

n = 21                                             # number of bin boundaries
nrnd = 1000000                                     # number of random numbers
x = [0]*(n+1); y = [0]*(n+1)                       # plotting points

seed()

GraphInit(1200,800)

a = -3.5e0; b = 3.5e0

                                                     # Central limit theorem
HistoBin(0e0,a,b,x,y,n,0)                           # initialize histogram
for irnd in range(1,nrnd+1):
    (w, rnd) = randNrm()
    HistoBin(rnd,a,b,x,y,n,1)
HistoBin(0e0,a,b,x,y,n,2)                            # normalize histogram
Plot(x,y,n,"blue",4,0.10,0.45,0.60,0.90,"x","n",
     "Mean value of uniform random numbers")        # 2D Gaussian distribution

HistoBin(0e0,a,b,x,y,n,0)                            # initialize histogram
for irnd in range(1,nrnd+1):
    (w,rnd) = randNrm2()
    HistoBin(rnd,a,b,x,y,n,1)
HistoBin(0e0,a,b,x,y,n,2)                            # normalize histogram
Plot(x,y,n,"blue",4,0.60,0.95,0.60,0.90,"x","n",
     "2D Gaussian distribution")

                                                     # Metropolis method
HistoBin(0e0,a,b,x,y,n,0)                            # initialize histogram
randMet(wMet,0.1e0,0)                                # initialize RNG
for irnd in range(1,nrnd+1): HistoBin(randMet(wMet,0.1e0,1),a,b,x,y,n,1)
HistoBin(0e0,a,b,x,y,n,2)                            # normalize histogram
Plot(x,y,n,"blue",4,0.10,0.45,0.10,0.40,"x","n",
     "Metropolis delta = 0.1")

                                                     # Metropolis method
HistoBin(0e0,a,b,x,y,n,0)                            # initialize histogram
randMet(wMet,0.1e0,0)                                # initialize RNG
for irnd in range(1,nrnd+1): HistoBin(randMet(wMet,0.5e0,1),a,b,x,y,n,1)
HistoBin(0e0,a,b,x,y,n,2)                            # normalize histogram
Plot(x,y,n,"blue",4,0.60,0.95,0.10,0.40,"x","n",
     "Metropolis delta = 0.5")

MainLoop()
```

## 参考文献和建议进一步阅读

- Beichl, I. and F. Sullivan. 2000. The Metropolis algorithm. *Computing in Science and Engineering* 2(5), 65–69.
- Beu, T. A. 2004. *Numerical Calculus in C* (3rd ed., in Romanian). Cluj-Napoca: MicroInformatica.
- Box, G. E. P. and M. E. Muller. 1958. A note on the generation of random normal deviates. *Annals of Mathematical Statistics* 29, 610–611.
- Gould, H., J. Tobochnik, and W. Christian. 2007. *An Introduction to Computer Simulation Methods: Applications to Physical Systems* (3rd ed.). San Francisco, CA: Pearson Addison-Wesley.
- Koonin, S. E. and D. C. Meredith. 1990. *Computational Physics: Fortran Version*. Redwood City, CA: Addison-Wesley.
- Landau, R. H., M. J. Páez, and C. C. Bordeianu. 2007. *Computational Physics: Problem Solving with Computers* (2nd ed.). Weinheim: Wiley-VCH.
- Metropolis, N., A. W. Rosenbluth, M. N. Rosenbluth, A. H. Teller, and E. Teller. 1953. Equation of state calculations by fast computing machines. *Journal of Chemical Physics* 21(6), 1087–1092.
- Press, W. H., S. A. Teukolsky, W. T. Vetterling, and B. P. Flannery. 2007. *Numerical Recipes: The Art of Scientific Computing* (3rd ed.). Cambridge: Cambridge University Press.
- Rapaport, D. C. 2004. *The Art of Molecular Dynamics Simulation* (2nd ed.). Cambridge: Cambridge University Press.

## 12

## 常微分方程

### 12.1 引言

求解常微分方程（ODE）或其系统的数值方法之所以特别重要，是由于许多自然规律都方便地以微分形式表达。粒子运动的经典方程、质量扩散或热传输方程，或薛定谔波动方程只是几个例子，说明了由微分方程建模的本质上截然不同的物理现象的非凡多样性。

大量现象由偏微分方程（PDEs）描述，涉及未知函数关于若干自变量的各阶导数。同样，在许多情况下，人们必须处理关于单一自变量的未知函数各阶导数的 ODE。

ODE 可以本质上是普通的，即它们可以直接从所研究现象的建模中产生，或者它们可能通过从初始 PDE 进行变量分离的过程产生，通常利用所建模系统所具有的某些对称性。在更复杂的情况下，解可能包含多个未知函数，满足一组耦合的 ODE。

为了说明高阶 ODE 与 ODE 系统之间的密切联系，让我们以经典的 1D 牛顿粒子运动方程作为典型例子，该粒子质量为 `m`，经历力场 `F(x)`：

```
m d²x/dt² = F(x).  (12.1)
```

定义粒子动量 `p = m (dx/dt)`，该二阶方程可分解为两个一阶方程的集合：

```
dx/dt = p/m,  dp/dt = F(x),  (12.2)
```

它们就是所谓的哈密顿正则运动方程。更强调粒子的速度 `v = p/m` 而非其动量，上式变为

```
dx/dt = v,  dv/dt = 1/m F(x).  (12.3)
```

由于构成该耦合系统的第一阶微分方程的等价函数形式，两个未知函数 `x` 和 `v` 被置于同等地位。此外，将初始运动方程 (12.1) 转化为系统 (12.3) 的方法揭示了原则上只需开发求解一阶微分方程或此类方程系统的数值方法即可。尽管如此，由于二阶运动方程在实践中具有特殊的重要性（例如在量子或经典分子动力学中），在本章中还将开发求解二阶 ODE 或此类方程系统的特定数值方法。

为了推广上述技术，让我们现在考虑未知函数 `y(t)` 的一般 `n` 阶微分方程：

```
y^{(n)} = f(t, y, y', ..., y^{(n-1)}).  (12.4)
```

可以很容易地证明该方程等价于 `n` 个一阶微分方程的系统

```
y'_i(t) = f_i(t, y_1(t), y_2(t), ..., y_n(t)),  i = 1, 2, ..., n,  (12.5)
```

方法是除了 `y` 之外，还将它的前 `(n − 1)` 个导数作为未知函数考虑，
