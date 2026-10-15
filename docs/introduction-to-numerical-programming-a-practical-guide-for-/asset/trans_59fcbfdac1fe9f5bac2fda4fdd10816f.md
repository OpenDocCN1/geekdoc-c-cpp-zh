

## 代码清单 13.10 扩散系数可变的 Crank–Nicolson 传播子（Python 编码）

```
# =================================================================================
def PropagDiff(u0, u, D, nx, hx, ht, iopBC1, iopBC2, Jdiff1, Jdiff2):
# --------------------------------------------------------------------------------
#   Propagates the solution u0[] of the diffusion equation
#    du/dt = D d2u/dx2,  D - diffusion coefficient (spatially variable)
# over the time interv at ht, using the Crank-Nicolson difference scheme on
# a spatial grid with nx nodes and spacing hx. Returns the solution in u[].
# iopBC1, iopBC2 - left/right boundary condition: 0 - Dirichlet, 1 - Neumann
# Jdiff1, Jdiff2 - left/right boundary fluxes for Neumann conditions
# --------------------------------------------------------------------------------

a = [0]*(nx+1); b = [0]*(nx+1); c = [0]*(nx+1)

f = 0.5e0 * ht/(hx*hx)

b[1] = 1e0; c[1] = -iopBC1      # build coefficients of discretized system
u[1] = hx*Jdiff1/D[1] if iopBC1 else u0[1]
for i in range(2,nx):
    lam = D[i] * f
    lam1 = 0.5e0 * (D[i] + D[i-1]) * f
    lam2 = 0.5e0 * (D[i] + D[i+1]) * f
    a[i] = -lam1
    b[i] = 1e0 + 2e0*lam
    c[i] = -lam2
    u[i] = lam1*u0[i-1] + (1e0 - 2e0*lam)*u0[i] + lam2*u0[i+1]

a[nx] = -iopBC2; b[nx] = 1e0
u[nx] = -hx*Jdiff2/D[nx] if iopBC2 else u0[nx]

TriDiagSys(a,b,c,u,nx)               # solve tridiagonal discretized system

for i in range(1,nx+1):                     # keep solution >= 0
    if (u[i] < 0e0): u[i] = 0e0

uint0 = 0.5e0*(u0[1] + u0[nx])              # integral of old solution
for i in range(2,nx): uint0 += u0[i]         # trapezoidal rule
uint0 *= hx
if (iopBC1 == 1): uint0 += Jdiff1*ht         # contribution of left flux
if (iopBC2 == 1): uint0 -= Jdiff2*ht         # contribution of right flux

uint = 0.5e0*(u[1] + u[nx])                 # integral of new solution
for i in range(2,nx): uint += u[i]           # trapezoidal rule
uint *= hx

f = uint0/uint                               # normalization factor
if (f < 0e0): f = 0e0
for i in range(1,nx+1): u[i] *= f            # normalize solution
```

初始解被选为阶梯状，整个扩散物质集中在区域的前半部分：

u(x,0) = { 1, 0 ≤ x < L/2,
          0, L/2 ≤ x ≤ L. } (13.96)

所施加的零通量 Neumann 边界条件，

j_diff^(1) = -[ D ∂u/∂x ]_{x=0} = 0,   j_diff^(2) = -[ D ∂u/∂x ]_{x=L} = 0, (13.97)

## 代码清单 13.11 扩散系数空间可变的扩散（Python 编码）

```
```python
# Solves the diffusion equation for spatially variable diffusion coefficient
from math import *
from pde import *
from graphical import *

def Init(u, x, D, nx):
    global L                                      # initialization
    for i in range(1,nx+1):                       # extent of spatial domain
        D[i] = 0.09e0*(x[i]/L) + 0.01e0          # diffusion coefficient
        u[i] = 1.0e0 if x[i] < 0.5e0*L else 0e0   # initial steplike solution

# main

L      = 1e0                                     # [0,L] spatial domain
iopBC1 = 1;  iopBC2 = 1                         # left/right boundary condition type
Jdiff1 = 0e0; Jdiff2 = 0e0                       # left/right boundary fluxes
nx     = 51                                      # number of spatial mesh points
tmax   = 2e0                                     # propagation time
ht     = 1e-3                                   # time step
nout   = 100                                     # output every nout steps

nt = (int)(tmax/ht + 0.5)                        # number of time steps
u0 = [0]*(nx+1); u = [0]*(nx+1)                  # solution
x  = [0]*(nx+1)                                  # spatial mesh
D  = [0]*(nx+1)                                  # diffusion coefficient

hx = L/(nx-1)
for i in range(1,nx+1): x[i] = (i-1)*hx         # spatial mesh

Init(u0,x,D,nx)                                   # initialization: diffusion coefficient, solution

GraphInit(1000,700)
out = open("diffusion.txt","w")
out.write("       x    ")
for i in range (1,nx+1): out.write("{0:10.5f}".format(x[i]))   # print x-mesh
out.write("\\n")
out.write("       t        u\\n")

for it in range(1,nt+1):                         # time loop
    t = it*ht                                    # propagate solution
    PropagDiff(u0,u,D,nx,hx,ht,iopBC1,iopBC2,Jdiff1,Jdiff2)
    for i in range(1,nx+1): u0[i] = u[i]        # shift solutions

    if (it % nout == 0 or it == nt):             # output every nout steps
        out.write("{0:10.5f}".format(t))
        for i in range (1,nx+1): out.write("{0:10.5f}".format(u[i]))
        out.write("\\n")

        GraphClear()
        title = "Diffusion  t = {0:4.2f}".format(t)
        Plot(x,u,nx,"blue",1,0.15,0.95,0.50,0.90,"None","u",title)
        Plot(x,D,nx,"red",1,0.15,0.95,0.08,0.48,"x","D","")
        GraphUpdate()
out.close

MainLoop()
```
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_562_0.png)

图 13.11 扩散系数空间可变的扩散问题 13.94–13.97 的时分辨浓度剖面。

防止物质在整个传播过程中泄漏到区域之外，并在无限长时间极限下使平衡解成为常数剖面：

```
u(x, t → ∞) = 0.5.
```

具体而言，程序 13.11 使用 L = 1 和 N_x = 51（由此得到 h_x = 0.02），以及 h_t = 10^{-3}。它将解传播到 t_max = 2，并每 n_out = 100 个时间步产生打印和图形输出。图 13.11 显示了时间增量为 0.1 的浓度剖面。可以看到解从初始阶梯状剖面向预期的均匀分布演化。如果程序运行到 t_max > 20 的时间，平衡解确实能以相当好的精度得到恢复。

## 13.4 时间依赖的薛定谔方程

非相对论量子系统的空间和时间演化由薛定谔方程描述：

```
iℏ ∂Ψ/∂t = ĤΨ, (13.98)
```

其中 Ĥ 是哈密顿量，ℏ = h/2π——约化普朗克常数，i = √−1——虚数单位。波函数 Ψ 作为方程的解，一般是位置和时间的复函数。特别地，对于一维系统，Ψ = Ψ(x, t)。从形式上看，量子波动方程等价于两个耦合的抛物型偏微分方程，耦合波函数的实部和虚部。

在量子形式体系中起核心作用的是概率密度，|Ψ(x, t)|² = Ψ*(x, t)Ψ(x, t)，其中 |Ψ(x, t)|² dx 表示系统在时间 t 位于区间 (x, x + dx) 内的概率。在求解时间相关问题时，波函数通常被建模

为波包，具有局域化和波动行为。波包的初始形状，Ψ(x, t = 0)，必须被指定，其局域化要求它在渐近时消失，即 Ψ → 0 当 x → ±∞。归一化波包的范数按定义为

∫₋∞^∞ |Ψ|² dx = 1,

它表示系统在空间某处被局域化的总概率。无论如何，范数不仅必须具有特定的有限值，而且必须随时间保持不变。

薛定谔方程 (13.98) 对一维系统的解可以形式上表示为

Ψ(x, t) = e^{-i(t−t₀)Ĥ} Ψ(x, t₀),   (13.99)

其中 e^{-i(t−t₀)Ĥ} 是所谓的演化算符。演化算符被称为幺正，因为乘以其伴随算符，[e^{-i(t−t₀)Ĥ}]^* = e^{i(t−t₀)Ĥ}，它会得到恒等算符。事实上，幺正性是演化算符的一个基本特征，因为它保证了波包范数在时间上的守恒。

考虑两个连续的时间步，tₙ 和 tₙ₊₁ = tₙ + hₜ，波包按如下演化

Ψ^{n+1} = e^{-i hₜ Ĥ} Ψ^{n}.   (13.100)

指数算符的具体作用由 Ĥ 的幂级数定义，由此，保留一阶近似，我们得到传播公式：

Ψ^{n+1} = (1 − i hₜ Ĥ) Ψ^{n}.   (13.101)

当哈密顿量由有限差分表示时，这是一个显式传播格式，允许解 Ψ^{n+1} 直接由前一解 Ψ^{n} 确定。不幸的是，该方法仅为条件稳定，因此容易迅速发散。在量子形式体系的层面上，可能的不稳定性可能与线性化传播子 (1 − i hₜ Ĥ) 对有限 hₜ 不是幺正的事实有关，因此不守恒波包的范数。非幺正性可通过对等式 13.101 两边取范数立即得到。

显式格式的条件稳定性可通过将逆演化算符 e^{i(t−t₀)Ĥ} 应用于等式 13.100 的两边并再次保留一阶近似来消除：

(1 + i hₜ Ĥ) Ψ^{n+1} = Ψ^{n}.   (13.102)

无论如何，除了隐式且因此需要额外计算来表达传播解之外，该格式同样是非幺正的。

对等式 13.100 中演化算符的离散化适当方式，导致一个既幺正又二阶精度的近似，是基于将波函数 Ψ^{n+1/2} 在中间时间步 t_{n+1/2} = t_n + h_t/2 处表示，既由 Ψ^{n+1} 向后传播，也由 Ψ^{n} 向前传播：

Ψ^{n+1/2} ≡ e^{i(h_t/2)Ĥ} Ψ^{n+1} = e^{-i(h_t/2)Ĥ} Ψ^{n}.   (13.103)

