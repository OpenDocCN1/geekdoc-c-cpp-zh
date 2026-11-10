

```text
sage: q = vector(RDF,[1,-1,2,3,5,-1,10,11])
sage: comp = polycompanion(q); comp
[  0.0   0.0   0.0   0.0   0.0   0.0   0.0  -1.0]
[  1.0   0.0   0.0   0.0   0.0   0.0   0.0   1.0]
[  0.0   1.0   0.0   0.0   0.0   0.0   0.0  -2.0]
[  0.0   0.0   1.0   0.0   0.0   0.0   0.0  -3.0]
[  0.0   0.0   0.0   1.0   0.0   0.0   0.0  -5.0]
[  0.0   0.0   0.0   0.0   1.0   0.0   0.0   1.0]
[  0.0   0.0   0.0   0.0   0.0   1.0   0.0 -10.0]
[  0.0   0.0   0.0   0.0   0.0   0.0   1.0 -11.0]
sage: roots = comp.eigenvalues(); roots
[0.3475215101190289 + 0.5665505533984981*I, 0.3475215101190289 -
  0.5665505533984981*I,
 0.34502377696179265 + 0.43990870238588275*I, 0.34502377696179265 -
  0.43990870238588275*I,
 -0.5172576143252197 + 0.5129582067889322*I, -0.5172576143252197 -
  0.5129582067889322*I,
 -1.3669971645459291, -9.983578180965276]
```

在此示例中，多项式由其系数列表 `q` 表示，系数从 0 到 $n-1$。因此，多项式 $x^2 - 3x + 2$ 将表示为 `q=[2,-3,1]`。

### 13.2.9 多项式曲线拟合：魔鬼又回来了

**连续版本。** 我们希望用次数 $\le n$ 的多项式 $P(x)$ 在区间 $[\alpha, \beta]$ 上逼近函数 $f(x)$。我们建立如下最小二乘问题：

$$\min_{a_0,\ldots,a_n\in\mathbb{R}} J(a_0,\ldots,a_n) = \int_\alpha^\beta \left(f(x)-\sum_{i=0}^n a_i x^i\right)^2\,dx.$$

将 $J(a_0,\ldots,a_n)$ 对系数 $a_i$ 求导，我们发现 $a_0,\ldots,a_n$ 是线性方程组 $Ma = F$ 的解，其中 $M_{i,j}=\int_\alpha^\beta x^{i+j}\,dx$，$F_j=\int_\alpha^\beta x^j f(x)\,dx$。观察 $\alpha=0$、$\beta=1$ 的情形，我们立刻可以看出 $M$ 是一个希尔伯特矩阵！不过存在补救办法：只需使用正交多项式基（例如，对于 $\alpha=-1$ 和 $\beta=1$，我们得到勒让德多项式）；于是 $M$ 变为单位矩阵。

**离散版本。** 我们考虑在点 $x_1,\ldots,x_m$ 处对某一现象的 $m$ 个观测值 $y_1,\ldots,y_m$。我们想在这些值之间拟合一个次数（至多）为 $n-1$ 的多项式 $\sum_{i=0}^{n-1} a_i x^i$，其中 $n\le m$。因此我们最小化泛函：

$$J(a_0,\ldots,a_{n-1}) = \sum_{j=1}^m \left(\sum_{i=0}^{n-1} a_i x_j^i-y_j\right)^2.$$

这样写出来，该问题会产生一个接近希尔伯特矩阵的矩阵，方程组将难以精确求解。然而，我们注意到 $\langle P,Q\rangle = \sum_{j=1}^m P(x_j)\cdot Q(x_j)$ 定义了次数至多为 $n-1$ 的多项式上的一个内积。因此，我们可以先构造 $n$ 个次数递增且关于该内积标准正交的多项式，然后对线性方程组进行对角化。记住⁵，Gram-Schmidt 过程在计算正交多项式时归结为三项递推，我们寻找形如 $P_{n+1}(x)= xP_n(x) - \alpha_n P_{n-1}(x) - \beta_n P_{n-2}(x)$ 的多项式 $P_{n+1}(x)$；下面的 `orthopoly` 过程执行该计算（这里我们用系数列表表示多项式：例如 `[1,-2,3]` 对应多项式 $1-2x+3x^2$）。用于计算多项式值的 Horner 方案给出以下程序：

```text
sage: def eval(P,x):
....:     if len(P) == 0:
....:         return 0
....:     else:
....:         return P[0] + x*eval(P[1:],x)
```

然后我们可以编码两个多项式的内积：

```text
sage: def pscal(P,Q,lx):
....:     return float(sum(eval(P,s)*eval(Q,s) for s in lx))
```

以及两个多项式 $P$ 和 $Q$ 的运算 $P \leftarrow P + aQ$：

```text
sage: def padd(P,a,Q):
....:     for i in range(0,len(Q)):
....:         P[i] += a*Q[i]
```

更谨慎的程序应在使用错误时抛出异常；在我们的情形中，当 $n > m$ 时使用以下异常：

```text
sage: class BadParamsForOrthop(Exception):
....:     def __init__(self, degreplusone, npoints):
....:         self.deg = degreplusone - 1
....:         self.np = npoints
....:     def __str__(self):
....:         return "degree: " + str(self.deg) + \
....:                " nb. points: " + repr(self.np)
```

以下过程计算 $n$ 个正交多项式：

```text
sage: def orthopoly(n,x):
....:     if n > len(x):
....:         raise BadParamsForOrthop(n, len(x))
....:     orth = [[1./sqrt(float(len(x)))]]
....:     for p in range(1,n):
....:         nextp = copy(orth[p-1])
....:         nextp.insert(0,0)
....:         s = []
....:         for i in range(p-1,max(p-3,-1),-1):
....:             s.append(pscal(nextp, orth[i], x))
....:         j = 0
....:         for i in range(p-1,max(p-3,-1),-1):
....:             padd(nextp, -s[j], orth[i])
....:             j += 1
....:         norm = sqrt(pscal(nextp, nextp, x))
....:         nextp = [nextp[i]/norm for i in range(len(nextp))]
....:         orth.append(nextp)
....:     return orth
```

⁵ 证明它并不很难！

一旦计算出正交多项式 $P_0(x), \ldots, P_{n-1}(x)$，解由 $P(x) = \sum_{i=0}^{n-1} \gamma_i P_i(x)$ 给出，其中：

$$\gamma_i = \sum_{j=1}^{m} P_i(x_j)y_j,$$

这显然又可以依次在单项式基 $1, x, \ldots, x^{n-1}$ 中表示出来。

**示例（$n=15$）：**

```text
sage: L = 40
sage: X = [100*float(i)/L for i in range(40)]
sage: Y = [float(1/(1+25*X[i]**2)+0.25*random()) for i in range(40)]
sage: n = 15; orth = orthopoly(n, X)
```

让我们在正交多项式基上计算解的系数：

```text
sage: coeff = [sum(Y[j]*eval(orth[i],X[j]) for j in
....:           range(0,len(X))) for i in range(0,n)]
```

然后我们可以将该结果转换到单项式基 $1, x, \ldots, x^{n-1}$，例如为了绘制图形：

```text
sage: polmin = [0 for i in range(0,n)]
sage: for i in range(0,n):
....:     padd(polmin, coeff[i], orth[i])
sage: p = lambda x: eval(polmin, x)
sage: plot(p(x), x, 0, X[len(X)-1])
```

这里我们不再详述在单项式基 $x^i$ 上进行朴素拟合的计算及其图形表示。我们得到图 13.1。

![](img/99840d73c45ee58b635c4eedc727fd9a_310_0.png)

图 13.1 – 虚线：朴素拟合。实线：正交多项式拟合。

两条曲线，即对应于用正交多项式基进行的拟合和用单项式基进行的拟合，很接近；然而，如果我们计算它们的残差（泛函 $J$ 的值），我们会发现正交多项式基为 0.1202，而朴素拟合为 0.1363。

### 13.2.10 实现与效率

具有 RDF 系数的矩阵计算由处理器浮点单元执行，而具有 RR 系数的矩阵计算由 GNU MPFR 库执行。此外，在第一种情况下，Sage 使用 NumPy/SciPy，而后者又调用 Lapack 库（用 Fortran 编写），Lapack 库使用 BLAS⁶，这些 BLAS 针对每个处理器进行了优化。于是对于两个大小为 1000 的矩阵的乘积，我们得到：

```text
sage: a = random_matrix(RR, 1000)
sage: b = random_matrix(RR, 1000)
sage: %time _ = a*b
CPU times: user 7min 50s, sys: 508 ms, total: 7min 50s
Wall time: 7min 51s
```

```text
sage: c = random_matrix(RDF, 1000)
sage: d = random_matrix(RDF, 1000)
sage: %time _ = c*d
CPU times: user 40 ms, sys: 4 ms, total: 44 ms
Wall time: 45.2 ms
```

⁶ 基础线性代数子程序（矩阵-向量乘积、矩阵-矩阵乘积等）。

因此，乘法时间之比超过 10000！（回想一下，两种情况下的计算精度相同。）

我们还可以注意到具有 RDF 系数的矩阵计算的效率：由于两个大小为 $n$ 的方阵的乘积需要 $n^3$ 次乘法（以及同样多次加法），我们在这里用 0.045 秒执行了 $10^9$ 次乘法和同样多次加法；这大约是每秒 $44\cdot 10^9$ 次浮点运算，相当于 44 gigaflops。处理器时钟频率为 3.3 GHz，因此我们每个时钟周期执行超过一次运算：这之所以可能，要归功于对相应 BLAS 例程的几乎直接调用（该例程利用了现代处理器核心中并行计算的不同可能性）。存在一种计算两个矩阵乘积的代价低于 $n^3$ 的算法，即 Strassen 算法。它在浮点计算中并不经常使用，因为它比朴素方法对舍入误差更敏感 [Hig93]。

## 13.3 稀疏矩阵

稀疏矩阵在科学计算中经常出现：稀疏性确实是一种人们所期望的性质，它使我们能够求解大规模问题，而这些问题用稠密矩阵是无法处理的。

*一个近似定义：我们将称一个矩阵序列 $M_n$（其中 $M_n$ 的大小为 $n$）为稀疏矩阵族，如果 $M_n$ 的非零系数个数为 $O(n)$。*

显然，这些矩阵在计算机中使用只存储非零元素的数据结构进行编码。通过考虑矩阵的稀疏性，我们当然希望节省内存以能够表示大型矩阵，同时也大幅降低计算成本。

### 13.3.1 稀疏系统从何而来？

**边值问题。** 稀疏线性系统最常见的来源是偏微分方程的离散化。例如，让我们考虑泊松方程（稳态热方程）：

$$-\Delta u = f$$

其中 $u = u(x,y)$，$f = f(x,y)$，

$$\Delta u := \frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2}.$$

该方程在正方形 $[0,1]^2$ 中考虑，边界条件为在正方形边界上 $u = 0$。一维类似问题是

$$-\frac{\partial^2 u}{\partial x^2} = f, \qquad (13.1)$$

其中 $u(0)=u(1)=0$。

为了近似该方程的解，最简单的方法之一是使用有限差分法：我们将区间 $[0,1]$ 划分为有限个数 $N$ 的等宽 $h$ 区间。我们用 $u_i$ 表示 $u$ 在点 $x_i = ih$ 处的近似值。我们用 $(u_{i+1} - u_i)/h$ 近似 $u$ 的导数，并用

$$\frac{(u_{i+1} - u_i)/h - (u_i - u_{i-1})/h}{h} = \frac{u_{i+1} - 2u_i + u_{i-1}}{h^2}.$$

近似其二阶导数。

