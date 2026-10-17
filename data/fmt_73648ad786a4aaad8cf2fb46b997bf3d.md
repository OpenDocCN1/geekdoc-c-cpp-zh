
将指数合并为 `2 cos(k h_x)` 并使用恒等式 `1 − cos x = 2 sin²(x/2)` 导致放大因子的所求表达式：

```
ξ = 1 − 4λ sin²(k h_x / 2).  (13.60)
```

鉴于 `0 ≤ sin²(k h_x / 2) ≤ 1`，von Neumann 的稳定性判据（13.58）只能在离散化参数 `λ` 满足条件时成立：

```
0 < λ < 1/2.  (13.61)
```

考虑到 `λ` 的表达式 13.47，稳定性条件转化为

```
h_t < (1/2) h_x² / D.  (13.62)
```

因此，保证 FTCS 算法稳定的时间步长 `h_t` 上限为距离 `h_x` 上的特征扩散时间的一半（`τ_D = h_x² / D`）。因此，基于 FTCS 前向时间离散格式的显式方法（13.46）–（13.48）是条件稳定的，其中临界值 `λ = 1/2` 将稳定和不稳定区域分开。

## 13.3.3 隐式有限差分法

相对于上面发展的显式 FTCS 方法，关于时间步长 `t_n` 与 `t_{n+1}` 的一个看似微小的改变，在离散化时空导数时进行等同，会导致时间传播解的稳定性发生定性变化，即导致一个

无条件稳定的方法。事实上，以 `t_{n+1}` 为参考点，时间导数的同一离散近似（式13.43）现在变成了后向差分格式：

```
\left(\frac{\partial u}{\partial t}\right)_{i,n+1} = \frac{u_i^{n+1} - u_i^{n}}{h_t} + O(h_t). \tag{13.63}
```

相应地，空间导数也需要基于时间层 `t_{n+1}` 上的值来构造：

```
\left(\frac{\partial^2 u}{\partial x^2}\right)_{i,n+1} = \frac{u_{i+1}^{n+1} - 2u_i^{n+1} + u_{i-1}^{n+1}}{h_x^2} + O(h_x^2). \tag{13.64}
```

对于时空点 `(x_i, t_{n+1})` 导出的差分方程，

```
\frac{u_i^{n+1} - u_i^{n}}{h_t} = D \frac{u_{i+1}^{n+1} - 2u_i^{n+1} + u_{i-1}^{n+1}}{h_x^2}, \tag{13.65}
```

代表了所谓的后向时间中心空间（BTCS）方法，并且与FTCS方法类似，它是扩散方程的一个 `O(h_x^2 + h_t)` 阶近似。重新组合各项，并如前所述记 `λ = D h_t / h_x^2`，则对于内部网格点上的传播解分量 `u_i^{n+1}`，可得到如下线性方程组：

```
-\lambda u_{i-1}^{n+1} + (1 + 2\lambda) u_i^{n+1} - \lambda u_{i+1}^{n+1} = u_i^{n}, \quad i = 2,3,\dots,N_x - 1. \tag{13.66}
```

该方程组需结合适当的初始条件和边界条件一起求解。特别地，Dirichlet条件

```
u_1^{n+1} = u_1^{n} = u_0^0, \quad u_{N_x}^{n+1} = u_{N_x}^{n} = u_L^0, \tag{13.67}
```

使边界上的解值保持不变。

由于与FTCS方法不同，传播解的各分量无法独立地表示出来，而是在每个时间步通过求解线性方程组 `(13.66)–(13.67)` 得到，因此BTCS格式被称为隐式方法。时间层 `t_n` 与 `t_{n+1}` 之间的特征信息流动情况也可以从图13.7中看出。

采用矩阵记号，BTCS方法的线性方程组具有如下形式：

```
\mathbf{A} \cdot \mathbf{u}^{n+1} = \mathbf{u}^{n}, \quad n = 0,1,2,\dots, \tag{13.68}
```

其中，前一时刻的解 `u^n` 充当常数向量，系统矩阵为三对角矩阵：

```
\mathbf{A} = \begin{bmatrix} 1 & 0 & & \\ -\lambda & 1 + 2\lambda & -\lambda & \\ & \ddots & \ddots & \ddots \\ & & -\lambda & 1 + 2\lambda & -\lambda \\ & & & 0 & 1 \end{bmatrix}. \tag{13.69}
```

由于按定义有 `λ > 0`，矩阵 `A` 是对角占优且正定的。因此，求解方程组 `(13.68)–(13.69)` 可以借助第7.7节发展的LU分解方法最有效地完成，该方法在库 `linsys.py` 和 `linsys.h` 中实现为例程 `TriDiagSys`。

为了考察隐式BTCS方法的稳定性，将一般本征模 `ε_i^n = ξ(k)^n\exp(ikhx)` 代入差分方程 `(13.66)`，得到：

$$\xi\left[-\lambda\exp(-ikh_x)+(1+2\lambda)-\lambda\exp(ikh_x)\right]=1.$$

将指数项合并为 `2\cos(kh_x)`，并利用恒等式 `1-\cos x=2\sin^2(x/2)`，即可得到放大因子的表达式：

$$\xi=\frac{1}{1+4\lambda\sin^2(kh_x/2)}. \tag{13.70}$$

由于 `0\leq\sin^2(kh_x/2)\leq1` 且 `λ>0`，分母始终大于1，因此 `ξ` 始终是次幺正的（即模小于1），这正是von Neumann稳定性准则（`|\xi(k)|<1`）所要求的。所以，与FTCS方法不同，隐式BTCS方法对任意时间步长 `h_t` 都是*无条件稳定的*。

然而，应当指出，BTCS格式的无条件稳定性并不能同时保证预定的精度。由于在时间方向上的精度阶较低（`O(h_t)`），BTCS方法需要相当小的时间步长才能达到可接受的精度水平，这仍然是该方法的一个显著缺点。

清单13.8中给出的例程 `PropagBTCS` 通过上述隐式BTCS方法，将扩散方程的初始解 `u0[]` 在一个基本时间间隔 `ht` 上向前传播。为此，该例程构造系统矩阵三条相关对角线上的元素，并在数组 `a[]`、`b[]`、`c[]` 以及 `u[]` 中构造相应的常数项。然后通过调用例程 `TriDiagSys` 求解离散化得到的三对角方程组，解通过数组 `u[]` 返回。该例程可以替代程序13.7中的函数 `PropagFTCS` 使用，无需任何更改。

```python
#================================================================================

def PropagBTCS(u0, u, nx, D, hx, ht):

#--------------------------------------------------------------------------------

#  Propagates the solution u0[] of the diffusion equation

#      du/dt = D d2u/dx2, D - diffusion coefficient (constant)

#  over the time interval ht, using an implicit BTCS difference scheme on

#  a spatial grid with nx nodes and spacing hx. Returns the solution in u[].

#--------------------------------------------------------------------------------

    a = [0]*(nx+1); b = [0]*(nx+1); c = [0]*(nx+1)

    lam = D * ht/(hx*hx)

    lam1 = 1e0 + 2e0*lam

    b[1] = 1e0; c[1] = 0e0       # build coefficients of discretized system

    u[1] = u0[1]

    for i in range(2,nx):

        a[i] = -lam; b[i] = lam1; c[i] = -lam

        u[i] = u0[i]

    a[nx] = 0e0; b[nx] = 1e0

    u[nx] = u0[nx]

    TriDiagSys(a,b,c,u,nx)       # solve tridiagonal discretized system
```

## 13.3.4 Crank–Nicolson方法

前面提到的隐式BTCS方法在时间上仅有一阶精度的缺点，可以通过在离散化扩散方程时以中间时间层 `t_{n+1/2} ≡ t_n + h_t/2` 为参考点来消除。由此得到的差分格式在空间和时间上均具有二阶精度。为此，我们以 `t_{n+1/2}` 为参考点，考察解在 `t_n` 和 `t_{n+1}` 处的泰勒展开：

`u_i^n = u_i^{n+1/2} - (h_t/2)(∂u/∂t)_{i,n+1/2} + 1/2(h_t/2)^2(∂²u/∂t²)_{i,n+1/2} + O(h_t^3)`, `u_i^{n+1} = u_i^{n+1/2} + (h_t/2)(∂u/∂t)_{i,n+1/2} + 1/2(h_t/2)^2(∂²u/∂t²)_{i,n+1/2} + O(h_t^3).`

将这两个展开式相减后，`t_{n+1/2}` 处的解 `u_i^{n+1/2}` 与时间二阶导数 `(∂²u/∂t²)_{i,n+1/2}` 恰好完全抵消，从而得到时间一阶导数的*二阶中心差分格式*：

` (∂u/∂t)_{i,n+1/2} = (u_i^{n+1} - u_i^n)/h_t + O(h_t^2).  (13.71)`

时刻 `t_{n+1/2}` 处的空间二阶导数可以简单地用时间层 `t_n` 和 `t_{n+1}` 的差分格式的平均值来近似：

` (∂²u/∂x²)_{i,n+1/2} = 1/2[ (u_{i+1}^{n+1} - 2u_i^{n+1} + u_{i-1}^{n+1})/h_x^2 + (u_{i+1}^n - 2u_i^n + u_{i-1}^n)/h_x^2 ] + O(h_x^2).  (13.72)`

于是，扩散方程可以写成如下离散形式：

` (u_i^{n+1} - u_i^n)/h_t = D/2 * [ (u_{i+1}^{n+1} - 2u_i^{n+1} + u_{i-1}^{n+1}) + (u_{i+1}^n - 2u_i^n + u_{i-1}^n) ] / h_x^2.  (13.73)`

这种中心时间中心空间格式被称为Crank–Nicolson方法。尽管它在形式上代表FTCS格式与BTCS格式的平均，但Crank–Nicolson方法具有更高的精度阶 `O(h_t^2 + h_x^2)`。将时间层 `t_n` 和 `t_{n+1}` 的各项分离，可得到以下以传播解分量为未知量的线性方程组：

` -λ u_{i-1}^{n+1} + (1 + 2λ) u_i^{n+1} - λ u_{i+1}^{n+1} = λ u_{i-1}^n + (1 - 2λ) u_i^n + λ u_{i+1}^n,  (13.74)` `i = 2,3,…,N_x - 1,`

其中

` λ = 1/2 * D h_t / h_x^2.  (13.75)`

离散化方程组 `(13.74)` 连同所附的边界条件可以表示为矩阵形式：

` A·u^{n+1} = B·u^n,  n = 0,1,2,…,  (13.76)`

其中矩阵 `A` 和 `B` 均为三对角矩阵，在Dirichlet边界条件情形下，它们分别由式13.50和式13.69给出。矩阵 `A` 是对角占优且正定的，因此是非奇异的。因此，与隐式方法的情形一样，传播解 `u^{n+1}` 可以借助三对角系统的LU分解算法来确定，该算法在

第 7.7 节。与隐式方法相比，显然由于常数项所隐含的额外矩阵乘法，存在操作开销。

遵循 von Neumann 稳定性分析的一般方法，通过将通用特征模态 `e_i^n=ξ(k)^n\exp(ikhx)` 代入差分方程 `(13.74)`，可得：

` ξ[-λ\exp(-ikh_x)+(1+2λ)-λ\exp(ikh_x)] = λ\exp(-ikh_x)+(1-2λ)+λ\exp(ikh_x).`

将两边的指数合并为 `2\cos(kh_x)`，并利用恒等式 `1-\cos x=2\sin^2(x/2)`，可得增幅因子：

$$\xi=\frac{1-4\lambda\sin^2(kh_x/2)}{1+4\lambda\sin^2(kh_x/2)}. \tag{13.77}$$

由于在任何情况下都有 `|1-4λ\sin^2(kh_x/2)| ≤ |1+4λ\sin^2(kh_x/2)|`，根据 von Neumann 稳定性判据 (`|ξ(k)|<1`)，Crank–Nicolson 方法对任意时间步长 `h_t` 都是无条件稳定的。此外，由于相对于时间具有更高的阶数，Crank–Nicolson 格式是求解抛物型 PDE 的首选方法。

扩散方程的 Crank–Nicolson 方法已在例程 `PropagCN`（清单 13.9）中实现，其参数列表和功能与前几节中介绍的函数 `PropagFTCS` 和 `PropagBTCS` 相同。

为了说明相对于时间的高阶精度对稳定传播的有益效果，让我们再次考虑扩散方程的初值问题 13.51–13.53，我们通过调用程序 13.7 中的例程 `PropagBTCS` 和 `PropagCN`，分别使用隐式 BTCS 和 Crank–Nicolson 方法进行比较求解。

## **清单 13.9**  扩散方程的 Crank–Nicolson 传播子（Python 编码）

```python
#====================================================================

def PropagCN(u0, u, nx, D, hx, ht):

#--------------------------------------------------------------------

#  Propagates the solution u0[] of the diffusion equation

#      du/dt = D d2u/dx2,  D - diffusion coefficient (constant)

#  over the time interval ht, using the Crank-Nicolson difference scheme on

#  a spatial grid with nx nodes and spacing hx. Returns the solution in u[].

#--------------------------------------------------------------------

    a = [0]*(nx+1); b = [0]*(nx+1); c = [0]*(nx+1)

    lam = 0.5e0 * D * ht/(hx*hx)

    lam1 = 1e0 + 2e0*lam; lam2 = 1e0 - 2e0*lam

    b[1] = 1e0; c[1] = 0e0          # build coefficients of discretized system

    u[1] = u0[1]

    for i in range(2,nx):

        a[i] = -lam; b[i] = lam1; c[i] = -lam

        u[i] = lam*u0[i-1] + lam2*u0[i] + lam*u0[i+1]

    a[nx] = 0e0; b[nx] = 1e0

    u[nx] = u0[nx]

    TriDiagSys(a,b,c,u,nx)         # solve tridiagonal discretized system
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_557_0.png)

图 13.10 使用空间间距 `hₓ = 0.05` 和时间步长 `hₜ = 0.25`，由隐式方法和 Crank–Nicolson 方法得到的扩散问题 13.51–13.53 在 `t = 6.0` 时的数值解。
