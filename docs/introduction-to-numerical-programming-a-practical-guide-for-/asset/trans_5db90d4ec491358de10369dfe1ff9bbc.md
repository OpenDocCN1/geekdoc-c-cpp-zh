

用 \(O(h_t^3)\) 幂级数近似两个指数算符得到

\[
\left[1+i\frac{h_t}{2}\hat{H}-\frac{1}{2}\left(\frac{h_t}{2}\hat{H}\right)^2\right]\Psi^{n+1}
=
\left[1-i\frac{h_t}{2}\hat{H}-\frac{1}{2}\left(\frac{h_t}{2}\hat{H}\right)^2\right]\Psi^n+O(h_t^3).
\]

此外，联系 \(\Psi^{n+1}\) 和 \(\Psi^n\) 可知，抛物项 \(h_t^2\hat{H}^2\Psi^{n+1}\) 和 \(h_t^2\hat{H}^2\Psi^n\) 实际上在 \(h_t^2\) 项本身的精度下相互抵消。因此，我们最终得到所需的二阶精度传播公式：

\[
\left(1+i\frac{h_t}{2}\hat{H}\right)\Psi^{n+1}
=
\left(1-i\frac{h_t}{2}\hat{H}\right)\Psi^n,
\qquad (13.104)
\]

或等价地，

\[
\Psi^{n+1}
=
\left(1+i\frac{h_t}{2}\hat{H}\right)^{-1}
\left(1-i\frac{h_t}{2}\hat{H}\right)\Psi^n.
\qquad (13.105)
\]

第二种变体引入了演化算符的所谓 Cayley 形式，

\[
e^{-ih_t\hat{H}}
\cong
\left(1+i\frac{h_t}{2}\hat{H}\right)^{-1}
\left(1-i\frac{h_t}{2}\hat{H}\right).
\qquad (13.106)
\]

根据上述论证，其精度达到 \(h_t^2\) 阶。

在等式 13.105 的两边构建范数并利用算符的厄米特性可证明波包的范数守恒，即

\[
\int |\Psi^{n+1}|^2\,dx=\int |\Psi^n|^2\,dx,
\]

并且演化算符的 Cayley 形式 (13.106) 确实是幺正的。

传播关系 (等式 13.104 和 13.105) 的两种形式在实践中都被使用。无论如何，其一或其二的适用性很大程度上取决于波包在空间上的表示方式。例如，如果基于波包的空间网格表示，等式 13.104 通常更为合适，因为由于所得到的系数形式简单且规则，它可以避免存储大型矩阵。另一方面，如果波包更适合由基函数的线性组合来表示（如在 *ab initio* 分子计算中），则采用 Cayley 算符矩阵表示的传播公式 13.105 更有可能有用。

现在我们考虑质量为 \(m\) 的量子粒子在一维定态势 \(V(x)\) 中的运动。系统的哈密顿量为

\[
\hat{H}
=
-\frac{\hbar^2}{2m}\frac{\partial^2}{\partial x^2}+V(x),
\qquad (13.107)
\]

并且为简化取 \(\hbar=1\) 且 \(m=1\)，相应的薛定谔方程形式为：

\[
i\frac{\partial\Psi}{\partial t}
=
\left[-\frac{1}{2}\frac{\partial^2}{\partial x^2}+V(x)\right]\Psi.
\qquad (13.108)
\]

我们将所有函数近似在由节点定义的规则空间网格上：

\[
x_j=(j-1)h_x,\qquad j=1,2,\dots,N_x.
\qquad (13.109)
\]

在等式 13.104 中使用哈密顿量 (13.107) 的中心差分表示，\(V_j=V(x_j)\)，得到以下传播公式：

\[
\begin{aligned}
\Psi_j^{n+1}
+i\frac{h_t}{2}\left[
-\frac{\Psi_{j+1}^{n+1}-2\Psi_j^{n+1}+\Psi_{j-1}^{n+1}}{4h_x^2}
+V_j\Psi_j^{n+1}
\right]
={}&\Psi_j^n\\
-i\frac{h_t}{2}\left[
-\frac{\Psi_{j+1}^{n}-2\Psi_j^{n}+\Psi_{j-1}^{n}}{4h_x^2}
+V_j\Psi_j^n
\right].
\end{aligned}
\tag{13.110}
\]

值得注意的是，这正是通过直接将一般 Crank–Nicholson 方法（参见第 13.3.4 节）应用于薛定谔方程 (13.108) 所得到的有限差分表示：

\[
\begin{aligned}
i\frac{\Psi_j^{n+1}-\Psi_j^n}{h_t}
={}&-\frac{\Psi_{j+1}^{n+1}-2\Psi_j^{n+1}+\Psi_{j-1}^{n+1}}{4h_x^2}
+\frac{1}{2}V_j\Psi_j^{n+1}\\
&-\frac{\Psi_{j+1}^{n}-2\Psi_j^{n}+\Psi_{j-1}^{n}}{4h_x^2}
+\frac{1}{2}V_j\Psi_j^n.
\end{aligned}
\tag{13.111}
\]

我们得出结论，当应用于薛定谔方程时，Crank–Nicolson 方法和 Cayley 方法是等价的。

我们引入记号

\[
\lambda=\frac{h_t}{4h_x^2},
\qquad (13.112)
\]

并在等式 13.110 或 13.111 的任一式中分离对应于时间步 \(t_n\) 和 \(t_{n+1}\) 的项：

\[
\begin{aligned}
-\lambda\Psi_{j+1}^{n+1}
+\left(2\lambda+\frac{1}{2}h_tV_j-i\right)\Psi_j^{n+1}
-\lambda\Psi_{j-1}^{n+1}\\
=\lambda\Psi_{j+1}^n
-\left(2\lambda+\frac{1}{2}h_tV_j+i\right)\Psi_j^n
+\lambda\Psi_{j-1}^n.
\end{aligned}
\]

最后，通过仍定义与势值相关的量

\[
W_j=2\lambda+\frac{1}{2}h_tV_j,
\qquad (13.113)
\]

对应于薛定谔方程 (13.108) 的离散化系统获得简单的三对角形式：

\[
-\lambda\Psi_{j-1}^{n+1}
+(W_j-i)\Psi_j^{n+1}
-\lambda\Psi_{j+1}^{n+1}
=
\lambda\Psi_{j-1}^n
-(W_j+i)\Psi_j^n
+\lambda\Psi_{j+1}^n,
\qquad (13.114)
\]

\[
j=2,\dots,N_x-1.
\]

该系统通过施加波包的渐近消失来完成，对于足够大的空间网格，这转化为边界条件：

\[
\Psi_1^{n+1}=\Psi_{N_x}^{n+1}=0.
\qquad (13.115)
\]

有多种方法可以求解差分系统 (13.114)–(13.115) 以将波包的状态从 \(t_n\) 推进到 \(t_{n+1}\)。鉴于系统的三对角结构，最直接的方法似乎是使用第 7.7 节中描述的基于 LU 分解的三对角求解器。相应地，三个非零对角线的复元素 \(a=[a_i]\)、\(b=[b_i]\) 和 \(c=[c_i]\)，以及常数项 \(d=[d_i]\) 为

\[
\begin{aligned}
&b_1=1,\qquad c_1=0,\qquad d_1=0,\\
&a_j=-\lambda,\qquad j=2,3,\ldots,N_x-1,\\
&b_j=W_j-i,\\
&c_j=-\lambda,\\
&d_j=\lambda\Psi_{j-1}^n-(W_j+i)\Psi_j^n+\lambda\Psi_{j+1}^n,\\
&a_{N_x}=0,\qquad b_{N_x}=1,\qquad d_{N_x}=0.
\end{aligned}
\tag{13.116}
\]

处理复元素的额外复杂性在实现函数重载机制的现代编程语言中被优雅地规避（其中包括 C++ 和 Python）。函数重载是一种允许创建具有相同名称但参数不同的多个函数的特性。事实上，C++ 库 `linsys.h` 提供了例程 `TriDiagSys` 的两个版本——一个使用 double 变量，另一个使用复数变量。编译器根据实际参数的类型将调用定向到其中之一。由于内置的动态类型能力，在 Python 中不需要多个变体，因为同一例程的实现可以用不同类型的参数调用。确实，库 `linsys.py` 包含 `TriDiagSys` 的单一版本，可以同时使用实数和复数参数调用。

## Listing 13.12 Propagator for the Schrödinger Equation Based on Tridiagonal Solver (Python Coding)

```python
#================================================================================
def PropagQTD(Psi, V, nx, hx, ht):
#--------------------------------------------------------------------------------
#   Propagates the solution PSI = Psi + i Chi of the 1D Schrodinger equation
#     i d/dt PSI(x,t) = [-(1/2) d2/dx2 - V(x)] PSI(x,t),
#   over the time interval ht. Uses the Crank-Nicolson scheme on a grid with
#   nx nodes and spacing hx and solves the tridiagonal discretized system by
#   LU factorization. Uses complex arithmetic.
#--------------------------------------------------------------------------------
a = [complex(0,0)]*(nx+1)                     # diagonals of discretized system
b = [complex(0,0)]*(nx+1)
c = [complex(0,0)]*(nx+1)

lam = ht/(4e0*hx*hx)

b[1] = 1e0; c[1] = 0e0                         # build coefficients of discretized system
Psii = Psi[1]
for i in range(2,nx):
    Psil = Psii; Psii = Psi[i]                # save initial wave packet values
    W = 2e0*lam + 0.5e0*ht*V[i]
    a[i] = -lam
    b[i] = complex(W,-1e0)
    c[i] = -lam
    Psi[i] = lam*Psil - complex(W,1e0)*Psii + lam*Psi[i+1]  # constant term

a[nx] = 0e0; b[nx] = 1e0
                                            # solve tridiagonal discretized system
TriDiagSys(a,b,c,Psi,nx)                    # solution Psi: propagated wave packet
```

基于等式 13.112 至 13.116 构建的初等传播子实现为 Listing 13.12 中的例程 `PropagQTD`。该例程接收初始波包的表格值 `Psi[]` 和势的 `V[]`。`PropagQTD` 在具有 `nx` 个节点、规则间距为 `hx` 的空间网格上操作，并将解在时间间隔 `ht` 上推进。`PropagQTD` 的 Python 版本使用内置类型 `complex`。该例程的 C/C++ 版本（参见 Listing 13.18）采用库 `memalloc.h` 中定义的双复数类型 `dcmplx`，该库还包括复数向量的动态分配例程 `CVector`。该例程为离散化系统的三个相关对角线分配数组 `a[]`、`b[]` 和 `c[]`，并临时使用数组 `Psi[]` 存储常数项。组成其元素后，`PropagQTD` 将这些数组传递给例程 `TriDiagSys`，该例程在求解三对角系统后通过 `Psi[]` 返回传播的波包。

求解差分系统 (13.114)–(13.115) 的另一种策略是显式处理波函数的实部和虚部：

\[
\Psi^n=\psi^n+i\chi^n.
\tag{13.117}
\]

我们首先将此表达式代入差分方程 (13.114)，进行一些代数运算，并分离实部和虚部得到

\[
\chi_j^{n+1}
-\lambda\psi_{j-1}^{n+1}
+W_j\psi_j^{n+1}
-\lambda\psi_{j+1}^{n+1}
=
\chi_j^n
+\lambda\psi_{j-1}^n
-W_j\psi_j^n
+\lambda\psi_{j+1}^n,
\]

\[
\psi_j^{n+1}
+\lambda\chi_{j-1}^{n+1}
-W_j\chi_j^{n+1}
+\lambda\chi_{j+1}^{n+1}
=
\psi_j^n
-\lambda\chi_{j-1}^n
+W_j\chi_j^n
-\lambda\chi_{j+1}^n.
\]

在每个方程中将来自时间步 \(t_n\) 的项收集为不同的量，

\[
\psi_{j,0}^{n+1}
=
\psi_j^n
-\lambda\left(\chi_{j-1}^n+\chi_{j+1}^n\right)
+W_j\chi_j^n,
\]

\[
\chi_{j,0}^{n+1}
=
\chi_j^n
+\lambda\left(\psi_{j-1}^n+\psi_{j+1}^n\right)
-W_j\psi_j^n,
\qquad j=2,3,\dots,N_x-1,
\tag{13.118}
\]

我们实际上得到了传播解分量的显式零阶近似。采用 \(\psi_{j,0}^{n+1}\) 和 \(\chi_{j,0}^{n+1}\) 作为常数项，传播波包的分量 \(\psi_j^{n+1}\) 和 \(\chi_j^{n+1}\) 表示为

\[
\psi_j^{n+1}
=
\psi_{j,0}^{n+1}
-\lambda\left(\chi_{j-1}^{n+1}+\chi_{j+1}^{n+1}\right)
+W_j\chi_j^{n+1},
\qquad j=2,3,\dots,N_x-1,
\]

\[
\chi_j^{n+1}
=
\chi_{j,0}^{n+1}
+\lambda\left(\psi_{j-1}^{n+1}+\psi_{j+1}^{n+1}\right)
-W_j\psi_j^{n+1}.
\tag{13.119}
\]

鉴于整个集合的隐式依赖性，这些分量可通过 Gauss–Seidel 迭代数值确定，其中更新后的分量递归地成为右端项，直至达到自洽。

这种基于 Gauss–Seidel 方法的方法的主要优点是避免了复数运算，并显著减少了存储需求，因为三对角差分系统的元素无需同时存储以传递给求解例程。此外，整体编码也得以简化，并适用于多维推广。尽管如此，对于相同的输入（本质上相同的步长 \(h_t\)），由于涉及的 Gauss–Seidel 迭代，该方法比前一种方法慢。

上述算法的一对一实现，基于实数运算和离散化系统的 Gauss–Seidel 求解，是例程 `PropagQGS`（Listing 13.13）。每次调用时，例程首先根据等式 13.118 构建传播解的显式零阶分量 `Psi0[]` 和 `Chi0[]`（\(\psi_{j,0}^{n+1}\) 和 \(\chi_{j,0}^{n+1}\)）。这些随后作为常数项在

