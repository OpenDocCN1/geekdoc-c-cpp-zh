
进入`/path/to/xxx`目录，找到`xxx.json`。

*边界条件* 定义了解在所有时间 `t>t_0` 时在边界上的行为。为了简化，我们暂时考虑狄利克雷型边界条件，意味着边界上解值为常数：

\[
u(0,t)=u_0^0, \quad u(L,t)=u_L^0. \tag{13.39}
\]

抛物型方程的离散化方法有多种，其中一些已在前面的章节中使用。尽管如此，对离散化格式的看似微小的修改对解的时间演化的稳定性和精度有巨大影响。下面，我们讨论三种有限差分方法：显式、隐式和 Crank–Nicolson 方法。

### 13.3.1 显式有限差分法

我们首先通过建立规则的时空网格来离散化扩散方程 `(13.36)` 结合初始条件 `(13.38)` 和边界条件 `(13.39)`，该网格由节点组成（见图 13.7）：

\[
x_i = (i-1)h_x, \quad i=1,2,\dots,N_x, \tag{13.40}
\]

\[
t_n = n h_t, \quad n=0,1,2,\dots \tag{13.41}
\]

这里 `h_t` 为时间步长，`h_x` 表示 `N_x` 个空间节点之间的间距，由下式定义

\[
h_x = \frac{L}{N_x - 1}. \tag{13.42}
\]

在时空节点 `(x_i,t_n)` 处的第一个时间导数 `\partial u/\partial t` 可以通过对 `t` 关于常数 `x=x_i` 的泰勒级数的线性近似以直接方式获得：

\[
u_i^{n+1}=u_i^{n}+h_t\left(\frac{\partial u}{\partial t}\right)_{i,n}+O(h_t^2)
\]

其中使用记号 `u_i^n \equiv u(x_i,t_n)`。事实上，表示时间导数，可得到简单的 *向前差分格式*：

\[
\left(\frac{\partial u}{\partial t}\right)_{i,n}=\frac{u_i^{n+1}-u_i^{n}}{h_t}+O(h_t). \tag{13.43}
\]

“向前”特性由导数在 `t^n` 处的表达式中存在 `t^{n+1}` 处的传播解给出，而该格式在 `h_t` 方面仅保持一阶精度是由于隐含的除以 `h_t`。

对于时空节点 `(x_i, t_n)` 处的二阶空间导数，可以使用与第 13.2 节中椭圆方程所使用的类似的中心差分格式，即

\[
\left(\frac{\partial^2 u}{\partial x^2}\right)_{i,n} = \frac{u_{i+1}^n - 2u_i^n + u_{i-1}^n}{h_x^2} + O(h_x^2), \tag{13.44}
\]

该格式仅涉及来自 `t_n` 的信息以及位于所表达导数节点对称位置的空间点。

将有限差分格式 `(13.43)` 和 `(13.44)` 代入扩散方程 `(13.36)`，我们得到向前时间中心空间 `(FTCS)` 方法：

\[
\frac{u_i^{n+1} - u_i^n}{h_t} = D \frac{u_{i+1}^n - 2u_i^n + u_{i-1}^n}{h_x^2}, \tag{13.45}
\]

它在时空节点 `(x_i, t_n)` 处以 `O(h_x^2 + h_t)` 近似扩散方程。由此，我们可以仅用来自前一时间步 `t_n` 的值来表示每个内部空间网格点 `x_i` 在时间步 `t_{n+1}` 处的传播解：

\[
u_i^{n+1} = \lambda u_{i-1}^n + (1 - 2\lambda) u_i^n + \lambda u_{i+1}^n, \quad i = 2, 3, \dots, N_x - 1, \tag{13.46}
\]

其中

\[
\lambda = \frac{D h_t}{h_x^2}. \tag{13.47}
\]

至于边界上的解值，它们在整个传播过程中由狄利克雷条件 `(13.39)` 固定，不需要任何特殊处理：

\[
u_1^{n+1} = u_1^n = u_0^0, \quad u_{N_x}^{n+1} = u_{N_x}^n = u_L^0. \tag{13.48}
\]

由于在每个时间步，传播的解分量可以根据公式 `13.46` 独立地表示，仅基于前一时间步的数据，建立在 FTCS 格式上的方法被称为显式，其本质也在图 13.7 中显现。

传播过程的显式性质也可以通过将方程 `13.46` 至 `13.48` 用矩阵形式重写而显现：

\[
\mathbf{u}^{n+1} = \mathbf{B} \cdot \mathbf{u}^{n}, \quad n = 0,1,2,\ldots \tag{13.49}
\]

传播矩阵 `\mathbf{B}` 是三对角的，矢量 `\mathbf{u}^{n}` 收集了在时间步 `t_n` 时所有空间网格点的解值：

\[
\mathbf{B}=\begin{pmatrix}
1 & 0 & 0 & 0 & \cdots & 0\\
\lambda & 1-2\lambda & \lambda & 0 & \cdots & 0\\
0 & \lambda & 1-2\lambda & \lambda & \ddots & \vdots\\
\vdots & \ddots & \ddots & \ddots & \ddots & 0\\
0 & \cdots & 0 & \lambda & 1-2\lambda & \lambda\\
0 & \cdots & 0 & 0 & 0 & 1
\end{pmatrix},\quad
\mathbf{u}^{n}=\begin{pmatrix}
u_1^{n}\\
u_2^{n}\\
\vdots\\
u_{N_x-1}^{n}\\
u_{N_x}^{n}
\end{pmatrix}. \tag{13.50}
\]

传播解 `\mathbf{u}^{n+1}` 的每个分量均由矩阵 `\mathbf{B}` 与前一解矢量 `\mathbf{u}^{n}` 的乘法单独得到。

例程 `PropagFTCS`（列表 13.6）求解扩散方程 `(13.36)` 的一个初等柯西问题，根据显式 FTCS 离散化格式得到的公式 `13.46` 至 `13.48` 将初始解 `u0[]` 在时间间隔 `h_t` 上传播。常数扩散系数、空间步长和节点数通过参数 `D`、`hx` 和 `nx` 接收，传播后的解通过数组 `u[]` 返回。主程序中的驱动序列被假定执行任何额外的处理，尤其是通过将 `u[]` 的内容保存到 `u0[]` 来为新的传播步释放数组 `u[]`。

一个典型的 `main` 程序包含在列表 13.7 中。代码首先通过对用户函数 `Init` 的调用初始化解 `u0[]`，然后在时间循环中通过对 `PropagFTCS` 的重复调用控制传播，每次调用后必须紧接着将内容从 `u[]` 向后转移到 `u0[]`。

通过显式 FTCS 方法求解扩散方程 `(13.36)` 容易出现一种特定的数值现象，在某些条件下会遇到严重的数值不稳定性。不稳定性意味着，与平滑、良好的空间剖面相比，传播会产生虚假振荡，这些振荡随时间指数增长，使解不可恢复地失真。这种临界行为是由于舍入误差的不断主导所致，并且只要时间步长超过与所采用的空间步长相关的某个上限，就会始终出现。

**列表 13.6** 扩散方程的显式 FTCS 传播器（Python 编码）

```python
# ============================================================================
def PropagFTCS(u0, u, nx, D, hx, ht):
    # ----------------------------------------------------------------------------
    # Propagates the solution u0[] of the diffusion equation
    #   du/dt = D d2u/dx2,  D - diffusion coefficient (constant)
    # over the time interval ht, using an explicit FTCS difference scheme on
    # a spatial grid with nx nodes and spacing hx. Returns the solution in u[].
    # ----------------------------------------------------------------------------
    lam = D * ht/(hx*hx)
    lam1 = 1e0 - 2e0*lam

    u[1] = u0[1]; u[nx] = u0[nx]
    for i in range(2,nx):
        u[i] = lam*u0[i-1] + lam1*u0[i] + lam*u0[i+1]
```

## 代码清单 13.7 扩散方程的有限差分解法（Python 编程）

```
# Solves the 1D diffusion equation by finite-difference schemes
from math import *
from pde import *
from graphlib import *

def Init(u, x, nx):    # initial solution for the diffusion equation
    global L           # extent of spatial domain
    for i in range(1,nx+1): u[i] = sin(pi*x[i]/L)

#### main

D   = 0.1e0                         # diffusion coefficient
L   = 1e0                           # [0,L] spatial domain
nx  = 21                            # number of spatial mesh points
tmax = 6.0e0                        # propagation time
ht  = 1.25e-2                       # time step

u0 = [0]*(nx+1); u = [0]*(nx+1)     # solution
x = [0]*(nx+1)                      # spatial mesh

hx = L/(nx-1)
for i in range(1,nx+1): x[i] = (i-1)*hx     # spatial mesh

Init(u0,x,nx)                       # initial solution

t = 0e0
while (t < tmax):                   # temporal loop
    t += ht                         # increase time
    PropagFTCS(u0,u,nx,D,hx,ht)     # propagate solution
    for i in range(1,nx): u0[i] = u[i]   # shift solutions

out = open("diffusion.txt","w")    # open output file
out.write("lambda = {0:f} t = {1:f}\n".format(D*ht/(hx*hx),t))
out.write("      x          u        exact\n")
f = exp(-pi*pi*D*t/(L*L))
for i in range(1,nx+1):
    out.write(("{0:10.5f}{1:10.5f}{2:10.5f}\n"). \
              format(x[i],u[i],f*sin(pi*x[i]/L)))
out.close()

GraphInit(800,600)
Plot(x,u,nx,"blue",1,0.15,0.95,0.15,0.85,"x","u","Diffusion")
MainLoop()
```

为说明时间步长与空间步长之间关键关系的，我们求解一维扩散方程：

∂u/∂t = D ∂²u/∂x²,  x ∈ [0,L],  t > 0,  (13.51)

扩散系数为常数，受狄利克雷边界条件约束

u(0,t) = u(L,t) = 0,  t > 0,  (13.52)

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_550_0.png)

图 13.8 用显式 FTCS 方法对扩散问题 (13.51)–(13.53) 的数值解，空间步长 hₓ = 0.05，时间步长 hₜ = 0.00125。

以及初始解剖面

```
u(x, 0) = sin(π x / L),    x ∈ [0, L].
(13.53)
```

满足此问题的精确解可很容易验证为

```
u(x, t) = exp(−π² D t / L²) sin(π x / L) .
(13.54)
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_550_1.png)

图 13.9 用显式 FTCS 方法对扩散问题 (13.51)–(13.53) 的数值解，空间步长 hₓ = 0.05，时间步长 hₜ = 0.0013。

具体而言，我们考虑 D = 0.1 且 L = 1，并将解传播至 t_max = 6.0。我们比较使用两个时间步长，h_t = 1.25·10^−2 和 1.30·10^−2，同时保持相同的空间间距 h_x = 0.05。相应地，离散化参数（式 13.47）取值为 λ = 0.5 和分别为 0.52，而两者之间的微小差异被证明是至关重要的。

对于 h_t = 1.25·10^−2（λ = 0.5）所得的空间剖面如图 13.8 所示，并附有三个所考虑时刻的解析解。除了由于采用的空间间距较大而造成的轻微系统性低估外，数值剖面（虚线）相当好地再现了解析解。

类似的剖面，但采用 h_t = 1.30·10^−2（λ = 0.52）得到，显示在图 13.9 中。虽然在 t = 5.0 时，用两种时间步长得到的解几乎无法区分，但不稳定性在 t = 5.5 时开始发展，并在 t = 6.0 时完全主导了解。由此可见，时间步长 h_t 似乎很小的增加会导致解的行为发生巨大的定性变化。λ = 1/2 看起来是一个临界值，将稳定（λ ≤ 1/2）和不稳定传播（λ > 1/2）两个不同的区域分开。

### 13.3.2 von Neumann 稳定性分析

评估应用于线性（通常是时变）偏微分方程的有限差分格式稳定性的标准技术是所谓的 von Neumann 稳定性分析（von Neumann 1950）。数值格式的稳定性本质上涉及误差在解的递归传播过程中如何演化。如果相关误差通过连续累积而增长超出可控限度，最终产生无界解，则认为该方法不稳定。

von Neumann 分析基于以下假设：（1）PDE 的系数为常数（或变化缓慢到可视为常数），以及（2）PDE 在周期性边界条件下求解（意味着对边上的值相互关联）。尽管如此，即使边界条件实际上是非周期的，该分析也证明是有用的。该分析使用局部舍入误差，定义为有限精度解 ũ_i^n 与精确离散解 u_i^n（在无舍入误差情况下得到）之差：

ε_i^n ≡ ũ_i^n − u_i^n. (13.55)

由此，误差必须满足与精确解本身相同的差分方程。

对于在域 [0, L] 上的周期性边界条件，误差可表示为离散傅里叶级数：

ε(x, t) = Σ_m ξ_m(t) e^{i k_m x}, (13.56)

其中实波数 k_m = 2π m / L 定义为整数 m = 1, 2, …, N_x（N_x = [L / h_x + 1]）。特别地，与空间节点 x_i = (i − 1) h_x 和时间 t_n = n h_t 相关的误差为

ε_i^n ≡ Σ_m ξ_m(n h_t) exp[ i k_m i h_x ],

其中 i = √−1 为虚数单位（不要与下标 i 混淆），每个系数 ξ_m 还包含一个位置无关因子 exp(−i k_m / h_x)，源于节点定义的定义。系数 ξ 显然仅取决于时间（下标 n）和波矢（下标 m），而指数则取决于位置（下标 i）和波矢（下标 m）。

差分方程的一个通用本征模（独立解）可写成一般形式：

```
ε_i^n = ξ(k)^n exp(i k i h_x),  (13.57)
```

其中放大因子 ξ 通常是 k 的复函数。von Neumann 分析的一个基本特征是本征模对时间的幂律依赖，即经过 n 个时间步后为放大因子的 n 次幂。时间传播显然只有在放大因子的绝对值小于 1 时才稳定，

```
|ξ(k)| < 1,  (13.58)
```

因为这样就不存在误差项的指数增长本征模。

为了确定稳定性判据（13.58）是否满足，或在何种条件下满足的一般程序，是将通用本征模（13.57）代入通过离散化 PDE 得到差分方程，并由此表达 ξ(k)。具体而言，在用显式 FCTS 格式离散化扩散方程的情况下，本征模必须满足（见式 13.46）

```
ε_i^{n+1} = λ ε_{i-1}^n + (1 − 2λ) ε_i^n + λ ε_{i+1}^n,  (13.59)
```

并通过代入通用本征模 13.57 的表达式，可得：

```
ξ = λ exp(−i k h_x) + (1 − 2λ) + λ exp(i k h_x).
```
