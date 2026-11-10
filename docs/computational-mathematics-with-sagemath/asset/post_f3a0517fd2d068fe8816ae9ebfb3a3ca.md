
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

In this example, the polynomial is represented by the list `q` of its coefficients, from 0 to $n-1$. The polynomial $x^2 - 3x + 2$ would thus be represented by `q=[2,-3,1]`.

### 13.2.9 Polynomial Curve Fitting: the Devil is Back

**Continuous Version.** We would like to approximate the function $f(x)$ by a polynomial $P(x)$ of degree $\le n$, on the interval $[\alpha, \beta]$. We formulate the least squares problem:

$$\min_{a_0,\ldots,a_n\in\mathbb{R}} J(a_0,\ldots,a_n) = \int_\alpha^\beta \left(f(x)-\sum_{i=0}^n a_i x^i\right)^2\,dx.$$

By differentiating $J(a_0,\ldots,a_n)$ with respect to the coefficients $a_i$, we find that $a_0,\ldots,a_n$ are solutions of the linear system $Ma = F$ where $M_{i,j}=\int_\alpha^\beta x^{i+j}\,dx$ and $F_j=\int_\alpha^\beta x^j f(x)\,dx$. We immediately see by looking at the case $\alpha=0$, $\beta=1$ that $M$ is a Hilbert matrix! However a remedy exists: it suffices to use a basis of orthogonal polynomials (for example, for $\alpha=-1$ and $\beta=1$ we obtain Legendre polynomials); then $M$ becomes the identity matrix.

**Discrete Version.** We consider $m$ observations $y_1,\ldots,y_m$ of a phenomenon at points $x_1,\ldots,x_m$. We want to fit a polynomial $\sum_{i=0}^{n-1} a_i x^i$ of degree (at most) $n-1$ among those values, with $n\le m$. We thus minimize the functional:

$$J(a_0,\ldots,a_{n-1}) = \sum_{j=1}^m \left(\sum_{i=0}^{n-1} a_i x_j^i-y_j\right)^2.$$

Written like this, the problem will produce a matrix close to a Hilbert matrix and the system will be hard to solve accurately. Yet, we notice that $\langle P,Q\rangle = \sum_{j=1}^m P(x_j)\cdot Q(x_j)$ defines a scalar product on polynomials of degree at most $n-1$. We can thus first construct $n$ polynomials of increasing degrees, orthonormal for this scalar product, and then diagonalise the linear system. Remembering⁵ that the Gram-Schmidt process reduces to a 3-term recurrence for the computation of orthogonal polynomials, we are looking for the polynomial $P_{n+1}(x)$ under the form $P_{n+1}(x)= xP_n(x) - \alpha_n P_{n-1}(x) - \beta_n P_{n-2}(x)$; the `orthopoly` procedure below performs this computation (we represent here polynomials by the list of their coefficients: for example `[1,-2,3]` corresponds to the polynomial $1-2x+3x^2$). Horner’s scheme to evaluate a polynomial yields the following program:

```text
sage: def eval(P,x):
....:     if len(P) == 0:
....:         return 0
....:     else:
....:         return P[0] + x*eval(P[1:],x)
```

We can then encode the scalar product of two polynomials:

```text
sage: def pscal(P,Q,lx):
....:     return float(sum(eval(P,s)*eval(Q,s) for s in lx))
```

and the operation $P \leftarrow P + aQ$ for two polynomials $P$ and $Q$:

```text
sage: def padd(P,a,Q):
....:     for i in range(0,len(Q)):
....:         P[i] += a*Q[i]
```

A more careful program should raise an exception when wrongly used; in our case, we use the following exception when $n > m$:

```text
sage: class BadParamsForOrthop(Exception):
....:     def __init__(self, degreplusone, npoints):
....:         self.deg = degreplusone - 1
....:         self.np = npoints
....:     def __str__(self):
....:         return "degree: " + str(self.deg) + \
....:                " nb. points: " + repr(self.np)
```

The following procedure computes the $n$ orthogonal polynomials:

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

⁵ Proving it is not very difficult!

Once the orthogonal polynomials $P_0(x), \ldots, P_{n-1}(x)$ are computed, the solution is given by $P(x) = \sum_{i=0}^{n-1} \gamma_i P_i(x)$, with:

$$\gamma_i = \sum_{j=1}^{m} P_i(x_j)y_j,$$

which can be clearly expressed in turn in the monomial basis $1, x, \ldots, x^{n-1}$.

**Example ($n=15$):**

```text
sage: L = 40
sage: X = [100*float(i)/L for i in range(40)]
sage: Y = [float(1/(1+25*X[i]**2)+0.25*random()) for i in range(40)]
sage: n = 15; orth = orthopoly(n, X)
```

Let us compute the solution coefficients on the basis of orthogonal polynomials:

```text
sage: coeff = [sum(Y[j]*eval(orth[i],X[j]) for j in
....:           range(0,len(X))) for i in range(0,n)]
```

We can then translate this result into the monomial basis $1, x, \ldots, x^{n-1}$, for example to draw the graph:

```text
sage: polmin = [0 for i in range(0,n)]
sage: for i in range(0,n):
....:     padd(polmin, coeff[i], orth[i])
sage: p = lambda x: eval(polmin, x)
sage: plot(p(x), x, 0, X[len(X)-1])
```

We do not detail here the computation of the naive fitting on the monomial basis $x^i$, and its graphical representation. We obtain Figure 13.1.

![](img/99840d73c45ee58b635c4eedc727fd9a_310_0.png)

FIGURE 13.1 – Dotted line: naive fitting. Continuous line: orthogonal polynomials fitting.

The two curves, which correspond to the fitting with a basis of orthogonal polynomials and to the monomial basis, are close; however, if we compute their residue (the value of the functional $J$) we find 0.1202 for the orthogonal polynomial basis, and 0.1363 for the naive fitting.

### 13.2.10 Implementation and Efficiency

The computations with matrices having RDF coefficients are performed with the processor floating-point unit, those having RR coefficients with the GNU MPFR library. Moreover, in the first case, Sage uses NumPy/SciPy, which in turn calls the Lapack library (written in Fortran), which uses the BLAS⁶, which are optimised for each processor. We then get for the product of two matrices of size 1000:

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

⁶ Basic Linear Algebra Subroutines (matrix-vector products, matrix-matrix products, etc.).

Whence a ratio of more than 10000 between the multiplication times! (Recall that we compute with the same precision in both cases.)

We can also notice the efficiency of computations with matrices having RDF coefficients: since the product of two square matrices of size $n$ costs $n^3$ multiplications (and as many additions), we perform here $10^9$ multiplications and as many additions in 0.045 second; this is about $44\cdot 10^9$ floating-point operations per second, which corresponds to 44 gigaflops. The processor clock having a frequency of 3.3 GHz, we thus perform more than one operation by clock cycle: this is possible thanks to the almost direct call to the corresponding BLAS routine (which uses the different possibilities to compute in parallel in modern processor cores). There exists an algorithm of cost lower than $n^3$ to compute the product of two matrices, namely Strassen's algorithm. It is not often used in practice for floating-point computations, as it is more sensitive to roundoff errors than the naive method [Hig93].

## 13.3 Sparse Matrices

Sparse matrices arise quite often in scientific computing: the sparsity is indeed a wanted property which enables us to solve problems of large size, out of reach with dense matrices.

*An approximate definition: we will say that a sequence $M_n$ of matrices, with $M_n$ of size $n$, is a family of sparse matrices if the number of non-zero coefficients of $M_n$ is $O(n)$.*

Clearly, those matrices are encoded in the computer using data structures where only the non-zero elements are stored. By taking into account the sparsity of the matrices, we want of course to save memory to be able to represent large matrices, but also heavily reduce the computation cost.

### 13.3.1 Where do Sparse Systems Come From?

**Boundary Problems.** The most common source of sparse linear systems is the discretisation of partial differential equations. Let us consider for example the Poisson equation (stationary heat equation):

$$-\Delta u = f$$

where $u = u(x,y)$, $f = f(x,y)$,

$$\Delta u := \frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2}.$$

The equation is considered in the square $[0,1]^2$, with boundary conditions $u = 0$ on the square border. The one-dimensional analogue is the problem

$$-\frac{\partial^2 u}{\partial x^2} = f, \qquad (13.1)$$

with $u(0)=u(1)=0$.

To approximate the solution of this equation, one of the simplest methods consists in using the finite difference method: we divide the range $[0,1]$ into a finite number $N$ of intervals of constant width $h$. We denote by $u_i$ the approximation of $u$ at the point $x_i = ih$. We approximate the derivative of $u$ by $(u_{i+1} - u_i)/h$, and its second derivative by

$$\frac{(u_{i+1} - u_i)/h - (u_i - u_{i-1})/h}{h} = \frac{u_{i+1} - 2u_i + u_{i-1}}{h^2}.$$
