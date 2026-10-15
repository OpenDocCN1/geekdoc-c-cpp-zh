
用有限差分法，使用 Bilocal 程序（程序清单 12.18），步长 $h = 10^{-4}$。计算并绘制第一类勒让德多项式和切比雪夫多项式，最高阶数 $n_{\max} = 5$。

## 解

将这两个两点边值问题改写成标准形式：

$$y'' = p(x) y' + q(x) y + r(x), \tag{12.126}$$
$$\left\{ \begin{array}{l} \alpha_1 y(x_a) + \beta_1 y'(x_a) = 1, \\ \alpha_2 y(x_b) + \beta_2 y'(x_b) = 1, \end{array} \right. \tag{12.127}$$

其特征函数为

$$p(x) = x/(1 - x^2), \quad q(x) = -n(n+1)/(1 - x^2), \quad r(x) = 0,$$

对于勒让德多项式，以及

$$p(x) = x/(1 - x^2), \quad q(x) = -n^2/(1 - x^2), \quad r(x) = 0,$$

对于切比雪夫多项式。两种情况下，边界条件都由以下系数定义：

$$\alpha_1 = (-1)^n, \quad \beta_1 = 0,$$
$$\alpha_2 = 1, \quad \beta_2 = 0.$$

Python 程序见程序清单 12.32，C/C++ 版本以补充材料形式提供（P12-LegChebBL.py）。用有限差分法计算得到的勒让德多项式和切比雪夫多项式绘制于图 12.22 中。

### 程序清单 12.32 用有限差分法计算勒让德多项式和切比雪夫多项式（Python 代码）

```python
# Legendre and Chebyshev polynomials by the finite-difference method
from math import *
from ode import *
from graphlib import *

def Func(x):                                    # RHS of Legendre ODE
    p = 2e0*x/(1e0-x*x); q = -n*(n+1)/(1e0-x*x); r = 0e0
    return (p, q, r)

def Func1(x):                                   # RHS of Chebyshev ODE
    p = x/(1e0-x*x); q =-n*n/(1e0-x*x); r = 0e0
    return (p, q, r)

# main

nmax = 5                                        # max. order of polynomial
xa = -1e0;  xb = 1e0                            # domain boundaries
hx = 1e-3                                       # x-mesh step size

nx = int((xb-xa)/hx + 0.5) + 1                  # number of x-mesh points

x = [0]*(nx+1); y = [0]*(nx+1)                  # x-mesh, solution
xp = [0]*(nx*nmax+1); yp = [0]*(nx*nmax+1)      # plotting arrays
nn  = [0]*(nmax+1)                              # ending indexes of plots
sty = [0]*(nmax+1)                              # styles of plots

col = [""]*(nmax+1)
color = ["blue", "cyan", "green", "orange", "red"]

# colors of plots

for m in range(1,nx+1): x[m] = xa + (m-1)*hx
# generate x-mesh

GraphInit(1200,600)

for n in range(1,nmax+1):
    # Legendre polynomials
    # loop over polynomial order
    alf1 = -1e0 if n % 2 else 1e0; bet1 = 0e0
    # Dirichlet conditions
    alf2 = 1e0; bet2 = 0e0
    Bilocal(xa,xb,y,nx,alf1,bet1,alf2,bet2,Func)

    nn[n] = n*nx; col[n] = color[(n-1)%5]; sty[n] = 1
    m0 = (n-1)*nx
    for m in range(1,nx+1): xp[m0+m] = x[m]; yp[m0+m] = y[m]

MultiPlot(xp,yp,yp,nn,col,sty,nmax,10,0e0,0e0,0,-1e0,1e0,1, \
    0.10,0.45,0.15,0.85,"x","Pn", \
    "Legendre polynomials - finite-differences")

for n in range(1,nmax+1):
    # Chebyshev polynomials
    # loop over polynomial order
    alf1 = -1e0 if n % 2 else 1e0; bet1 = 0e0
    # Dirichlet conditions
    alf2 = 1e0; bet2 = 0e0
    Bilocal(xa,xb,y,nx,alf1,bet1,alf2,bet2,Func1)

    nn[n] = n*nx; col[n] = color[(n-1)%5]; sty[n] = 1
    m0 = (n-1)*nx
    for m in range(1,nx+1): xp[m0+m] = x[m]; yp[m0+m] = y[m]

MultiPlot(xp,yp,yp,nn,col,sty,nmax,10,0e0,0e0,0,-1e0,1e0,1, \
    0.60,0.95,0.15,0.85,"x","Tn", \
    "Chebyshev polynomials - finite-differences")

MainLoop()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_526_0.png)

图 12.22 用有限差分法计算得到的 n = 1–5 的勒让德多项式 P_n(x)（左）和第一类切比雪夫多项式 T_n(x)（右）（针对问题 12.14）。

## 参考文献与进一步阅读建议

- Abramowitz, M. 和 I. A. Stegun（编）1972.《数学函数手册：含公式、图形和数学用表》。纽约：Dover Publications。
- Beléndez, A., C. Pascual, D. I. Méndez, T. Beléndez, 和 C. Neipp. 2007. 非线性摆的精确解. *Revista Brasileira de Ensino de Física* 29(4), 645–648.
- Beu, T. A. 2004.《C 语言数值计算》（第 3 版，罗马尼亚文）。Cluj-Napoca: MicroInformatica.
- Burden, R. 和 J. Faires. 2010.《数值分析》（第 9 版）。Boston: Brooks/Cole, Cengage Learning.
- Butcher, J. C. 1996. Runge–Kutta 方法的历史. *Applied Numerical Mathematics* 20, 247–260.
- Cromer, A. 1981. 利用欧拉近似得到的稳定解. *American Journal of Physics* 49(5), 455–459.
- Fehlberg, E. 1966. 具有任意小截断误差的新型高阶 Runge–Kutta 公式. *Zeitschrift für Angewandte Mathematik und Mechanik* 46(1), 1–16.
- Fehlberg, E. 1970. Klassische Runge–Kutta-Formeln vierter und niedrigerer Ordnung mit Schrittweiten-Kontrolle und ihre Anwendung auf Wärmeleitungsprobleme.（经典的四阶及更低阶 Runge–Kutta 公式，带步长控制及其在热传导问题中的应用（德文））. *Computing* 6, 61–71.
- Fitts, D. 2002.《量子力学原理：在化学与化学物理中的应用》。Cambridge: Cambridge University Press.
- Gear, C. W. 1971.《常微分方程数值初值问题》。Englewood Cliffs, NJ: Prentice-Hall.
- Giannozzi, P. 2013. 量子力学中的数值方法. http://www.fisica.uniud.it/~giannozz/Corsi/MQ/mq.html.
- Hockney, R. W. 和 J. W. Eastwood. 1988.《使用粒子进行计算机模拟》。Bristol: Adam Hilger.
- Ixaru, L. G. 1979.《微分方程数值方法及其应用》（罗马尼亚文）。Bucharest: Editura Academiei.
- Kutta, W. 1901. Beitrag zur näherungsweisen Integration totaler Differentialgleichungen（关于全微分方程近似积分的贡献（德文））. *Zeitschrift für Mathematik und Physik* 46, 435.
- Landau, R. H., M. J. Páez, 和 C. C. Bordeianu. 2007.《计算物理：用计算机解决问题》（第 2 版）。Weinheim: Wiley-VCH.
- Numerov, B. 1923. Méthode nouvelle de la détermination des orbites et le calcul des éphémérides en tenant compte des perturbations（考虑摄动确定轨道和计算星历表的新方法（法文））. *Publications de l’Observatoire Astrophysique Central de Russie* II, 188–288.
- Press, W. H., S. A. Teukolsky, W. T. Vetterling, 和 B. P. Flannery. 2007.《数值方法》（第 3 版）。《科学计算的艺术》。Cambridge: Cambridge University Press.
- Rapaport, D. C. 2004.《分子动力学模拟的艺术》（第 2 版）。Cambridge: Cambridge University Press.
- Runge, C. 1895. Über die numerische Auflösung von Differentialgleichungen（关于微分方程的数值求解（德文））. *Mathematische Annalen* 46, 167.
- Stoer, J. 和 R. Bulirsch. 1980.《数值分析导论》。New York: Springer-Verlag.
- Swope, W. C., H. C. Andersen, P. H. Berens, 和 K. R. Wilson. 1982. 计算分子物理团簇形成平衡常数的计算机模拟方法：对小水团簇的应用. *Journal of Chemical Physics* 76(1), 637–649.
- Verlet, L. 1967. 经典流体的计算机“实验”。I. Lennard-Jones 分子的热力学性质. *Physical Review* 159(1), 98–103.

## 13 偏微分方程

### 13.1 引言

偏微分方程（PDE）通常出现在连续系统所发生的现象中，在这些系统中，物理量随空间和时间变化。所涉及的过程种类繁多——热与质量输运、机械波、电磁波或量子力学波的传播等等。除了少数简单情形（其解可以用闭式形式表示）外，通常需要借助数值方法来求解这些方程。

通常，通过使用某种*离散格式*，微分方程被转化为矩阵方程，其未知量是时空网格节点上的解值。尽管所得的矩阵方程原则上可以用任何一种通用方法（高斯消去法、LU 分解等）求解，但对于实际问题而言，系统的规模相当大（数千阶），通常使这种方法不可行。幸运的是，所考虑的偏微分方程的*局部性*（只包含低阶导数），以及应用于微分算子的离散格式的局部性（只涉及相邻网格点），通常使得离散化方程组具有所谓的*稀疏矩阵*，即只有少数几条对角线上有非零元素。对于这类矩阵，存在特殊的求逆技术，本章将应用其中最重要的几种。

科学与工程中许多具有实际重要性的偏微分方程是*二阶方程*，包含未知函数最高到二阶的偏导数，其自变量通常只包含空间坐标，或同时包含空间与时间坐标。为简单起见，将讨论限制在两个变量的线性问题上，这些偏微分方程可以写成如下一般形式：

$$a(x,y) \frac{\partial^2 u}{\partial x^2} + b(x,y) \frac{\partial^2 u}{\partial x \partial y} + c(x,y) \frac{\partial^2 u}{\partial y^2} + d(x,y) \frac{\partial u}{\partial x} + e(x,y) \frac{\partial u}{\partial y} + g(x,y) u = f(x,y),$$

其中 $(x,y) \in \mathcal{D}$（xy 平面中的区域），且条件 $a^2(x,y) + b^2(x,y) + c^2(x,y) > 0$ 必须在 $\mathcal{D}$ 中处处成立。与圆锥曲线（其中包含的是 $x$ 和 $y$ 的幂而不是导数）类似，偏微分方程可根据其信息传播曲线分为：

- *椭圆方程*：若对所有 $(x,y) \in \mathcal{D}$，$b^2 - 4ac < 0$；
- *抛物方程*：若对所有 $(x,y) \in \mathcal{D}$，$b^2 - 4ac = 0$；
- *双曲方程*：若对所有 $(x,y) \in \mathcal{D}$，$b^2 - 4ac > 0$。

*椭圆型偏微分方程*的典型代表是泊松方程：

$$\frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} = f(x,y),$$
