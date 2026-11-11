$$\mathbf{V}'=\frac{1}{16}\begin{bmatrix}9&\frac32&\frac32&\frac32&\frac32&\frac14&\frac14&\frac14&\frac14\\6&6&2&2&1&1&0&0&1\\6&1&6&1&0&1&1&0&0\\6&0&1&6&1&0&1&1&0\\6&1&0&1&6&0&0&1&1\\4&4&4&0&0&4&0&0&0\\4&0&4&4&0&0&4&0&0\\4&0&0&4&4&0&0&4&0\\4&4&0&0&4&0&0&0&4\end{bmatrix}\mathbf{V}. \qquad (23.16)$$

More generally, for a vertex of degree $n$, there are $2n+1$ rows in $\mathbf{V}$ and the subdivision matrix is a $(2n+1)\times(2n+1)$ matrix. Letting $\mathbf{V}_n$ denote the neighborhood coordinates for a vertex of degree $n$, we can write

$$\mathbf{V}'_n=\mathbf{S}_n\mathbf{V}_n, \qquad (23.17)$$

where the matrix $\mathbf{S}_n$ is of the appropriate size. Everything about Catmull-Clark subdivision can be determined by studying the matrix $\mathbf{S}$. Halstead et al. [HKD93] carry this out in some detail.

As an example of what one can derive, if we look at some vertex $\mathbf{v}$ in a mesh, during repeated subdivision $\mathbf{v}$ will approach some point $\mathbf{v}^{\infty}$. (This can be proved by looking at powers of $\mathbf{S}$; the web materials for this chapter do so explicitly.) The limit point $\mathbf{v}^{\infty}$ for $\mathbf{v}$ under repeated subdivision is

$$\mathbf{v}^{\infty}=\frac{n^2\mathbf{v}'+4\sum_i\mathbf{e}'_i+\sum_i\mathbf{f}'_i}{n(n+5)}, \qquad (23.18)$$

where the primes indicate one level of subdivision. (This is determined by looking at eigenvectors of $\mathbf{S}$.) Notice that $\mathbf{v}$ need not be a vertex of the original mesh. If, after three levels of subdivision, we insert a new face point, we can call this point $\mathbf{v}$, find its neighboring face and edge points, and apply the limit formula above.

We can now make three observations.

First, the formula for computing the limit point does exactly the same computation with the $x$-, $y$-, and $z$-coordinates. In fact, it works in any dimension at all, and we can think about subdivision surfaces one coordinate at a time.

Second, if the initial mesh consists of the integer lattice in the $xy$-plane (i.e., all integer points are vertices), and the unit-length vertical and horizontal segments joining them are the edges, then a single subdivision operation produces the half-integer lattice, two subdivisions produce the quarter-integer lattice etc.

Third, if we alter the integer lattice by replacing $(0,0,0)$ with $(0,0,1)$, the limit surface shown in Figure 23.6 is very simple. In fact, just as for subdivision curves, it turns out that this limit surface is actually identical to the cubic B-spline basis function. In particular, if $(x,y,z)$ is on the limit surface, then $B(x,y)=z$, where $B$ is the basis function.

This means that, at least in areas where the mesh has standard lattice connectivity, the limit subdivision surface is the same as the B-spline surface defined by those control points. Since code for computing and rendering such surfaces is widely available, this is very convenient. In any neighborhood of an exceptional vertex (i.e., one whose degree is different from four), the limit surface is not similar to a B-spline, and we have to compute the surface by repeated subdivision. Stam [Sta98] discusses the limit shape both at and away from exceptional points.

![](bbox=[0.7, 0.5, 0.94, 0.92])