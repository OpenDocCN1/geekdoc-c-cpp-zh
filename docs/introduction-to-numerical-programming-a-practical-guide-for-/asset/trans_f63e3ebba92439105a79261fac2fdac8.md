

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_483_0.png)

图 12.8 量子谐振子问题的解：用连续线表示精确的未归一化解 ψ₀(x) = exp(−x²/2)，用虚线表示由试探能量 E₀^{(1)}, E₀^{(2)}, E₀^{(3)}, E₀^{(4)} 的射击法得到的解，两两夹住真实本征值 E₀ = 0.5。

## Listing 12.16 使用射击法求解一维薛定谔方程的求解器（Python 编码）

```
def ShootQM(E1, E2, V, x, y, nx, nc, y0, dy0, eps):
# ----------------------------------------------------------------------------
# Solves the two-point eigenvalue problem for the 1D Schrodinger equation
# y'' = (2m/h^2) [V(x) - E] y, y(0) = y0, y(+inf) = 0
# on a regular mesh x[] with nx points, using the shooting method with the
# trial energies E in [E1,E2] and the tabulated potential in V[]. Returns
# the solution y[] vanishing at the checkpoint x[nc] within tolerance eps,
# and the existence flag exist.
# Calls: Numerov(V, x, y, nx, y0, dy0, E)
# ----------------------------------------------------------------------------
    itmax = 100                                 # max. number of bisections

    inf = Numerov(E1,V,x,y,nx,y0,dy0)           # propagate y for E1
    f1 = y[inf]                                 # asymptotic y
    inf = Numerov(E2,V,x,y,nx,y0,dy0)           # propagate y for E2
    f2 = y[inf]                                 # asymptotic y

    if (f1*f2 < 0):                             # check if exists E in [E1,E2]
        exist = 1
        for it in range(1,itmax+1):             # refine E by bisection
            E = 0.5e0*(E1 + E2)                 # new approximation
            inf = Numerov(E,V,x,y,nx,y0,dy0)    # propagate y
            f = y[inf]                          # asymptotic y
            if (f1*f > 0): E1 = E               # new semi interval
            else:           E2 = E
            if (fabs(y[nc]) <= eps): break      # check if y vanishes at x[nc] ?

        if (it >= itmax): print("ShootQM: max. no. of bisections exceeded !")
    else:
        E = 1e10; exist = 0

    return (E, exist)
```

如果存在，则返回被输入能量 E1 和 E2 夹住的本征能量 E。同样，例程返回相应的本征函数 y[]，该函数被确定为在容差 eps 内在检查点 x[nc] 处消失。

ShootQM 在 E1 和 E2 之间的区间仅分离一个本征能量 E 或无本征能量时工作正确。因此，它应在一个外部能量“窗口”循环中被调用，该窗口足够窄以保证本征值的分离，并且依次扫描感兴趣的整个能量域（可能包含多个本征能量）。

例程 ShootQM 调用的全局 ODE 积分器是第 12.7 节中开发的 Numerov 函数。从初始值 y0 和 dy0 开始，Numerov 传播对应于输入能量 E 和存储在 V[] 中的势的解 y[]，遍及 x[] 中指定的 nx 个等距网格点整个域。此外，Numerov 返回解发散（超过 10^10）的网格点索引，默认为 nx，如果未发生发散。

ShootQM 最初对极限输入能量 E1 和 E2 执行两次完整传播，并按顺序在 inf 中接收各自发散点的索引。如果相应的发散 y[inf]，分别存储在 f1 和 f2 中，具有相同符号，则 E1 和 E2 之间的区间肯定不包含所求本征值，例程返回一个虚假的 E 并将标志 exist 设置为 0。相反，如果两个试探解以相反符号发散（f1*f2 < 0），例程启动对 E1 和 E2 之间区间通过二分法的迭代细化。在每次二分步骤中，对当前能量子区间的中间值进行传播，同时保留其极限的解以相反符号发散的半区间。

再次，能够不断夹住精确本征能量并与外部多本征能量分离序列协同工作，如上所述，是二分法被优选的期望特性。

现在参考量子谐振子的具体例子，我们在无量纲单位下有简单的抛物势：

V(x) = 1/2 x^2.

精确的无量纲本征能量（以 ħω 为单位）和相应的本征函数为（Fitts 2002）

E_n = n + 1/2,   n = 0, 1, 2, ...,
ψ_n(x) = (√π 2^n n!)^(-1/2) e^(-x^2/2) H_n(x),

其中 H_n(x) 是厄米多项式（见第 5.4 节了解性质和例程）。特别地，基态本征函数是高斯函数 ψ_0(x) = π^(-1/4) e^(-x^2/2)。

程序 12.17 设计用于通过射击法确定量子谐振子的单个束缚态。要计算的特定本征态由本征函数的宇称 par（0 或 1）和本征能量 E 的搜索区间下限 Emin 决定。xx 指定 x 网格的极限，xc 是“检查点”的位置，在该处解预期在容差 eps 内消失，Emax 是搜索 E 的上限，dE 是 E 的连续搜索窗口的宽度，hx 是空间积分步长。关于 dE 的可用值，它们应足够低以分离不同的本征能量；然而，过低的值不会有害，因为它们只会增加不包含任何本征值的能量窗口的数量。

程序首先确定最终网格点和检查点的索引 nx 和 nc。然后初始化空间网格 x[] 并在 V[] 中列表势。

## Listing 12.17 通过射击法求量子振子本征态（Python 编码）

```
# Eigenstates of the 1D Schroedinger equation for the harmonic oscillator
# y'' = 2 [V(x) - E] y, y(0) = y0, y'(0) = y'0, y(+inf) = 0
# V(x) = 0.5*x*x
# using a shooting algorithm based on the Numerov method
#---------------------------------------------------------------------
from math import *
from ode import *
from specfunc import *

def Pot(x): return 0.5e0*x*x                 # Potential for harmonic oscillator

# main

xx = 10e0                                   # limit of x-mesh
xc = 6e0                                    # checkpoint for vanishing solution (xc < xx)
par = 0                                     # parity of eigenstate (0/1)
Emin = 0e0                                  # lower limit for eigenvalues
Emax = 1e2                                  # upper limit for eigenvalues
dE = 0.1e0                                  # minimum separation of eigenvalues
eps = 1e-4                                  # tolerance for solution at xc
hx = 1e-4                                   # x-mesh step size

nx = int(xx/hx + 0.5) + 1                   # number of x-mesh points
nc = int(xc/hx + 0.5) + 1                   # index of checkpoint for vanishing y
x = [0]*(nx+1); y = [0]*(nx+1)              # x-mesh, solution
V = [0]*(nx+1)                              # tabulated potential

for m in range(1,nx+1):
    x[m] = (m-1)*hx                        # integration mesh
    V[m] = Pot(x[m])                       # tabulate potential

Ew = Emin                                   # lower limit of search window for E, [Ew,Ew+dE]
while (Ew < Emax):                          # loop over eigenvalue windows
    # initial values at x = 0
    if (par == 0): y0 = 1e0; dy0 = 0e0      # even y
    else:           y0 = 0e0; dy0 = 1e0     # odd y

    (E, exist) = ShootQM(Ew,Ew+dE,V,x,y,nx,nc,y0,dy0,eps)

    if (exist): break

    Ew += dE                                # shift [Ew,Ew+dE] for next shoot

if (exist):
    n = int(E)                              # quantum number

    f = 0e0                                 # normalize y by trapezoidal rule
    for m in range(1,nc+1): f += y[m]*y[m]*hx   # norm for [0,+inf]
    f = sqrt(2e0*f)
    if (int(n/2) % 2): f = -f               # sign correction
    for m in range(1,nx+1): y[m] /= f

    f = sqrt(pi)                            # norm of Hermite polynomials
    for i in range(1,n+1): f *= 2e0 * i
    f = 1e0/sqrt(f)

    out = open("shoot.txt","w")
    out.write("E{0:1d} = {1:8.5f}\n".format(n,E))
```

