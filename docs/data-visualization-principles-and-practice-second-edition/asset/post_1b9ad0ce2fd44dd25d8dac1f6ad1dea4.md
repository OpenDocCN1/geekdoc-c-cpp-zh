
sampled dataset \(\{p_i, f_i\}\) consisting of a set of \(N\) sample points \(p_i \in D\) and sample values \(f_i \in C\), we want to produce a continuous function \(\bar{f} : D \to C\) that approximates the original \(\bar{f}\). The reconstructed function should equal the original one at all sample points, i.e., \(\bar{f}(p_i) = f(p_i) = f_i\). One way to define the reconstructed function that satisfies this property is to set

```
\(\bar{f} = \sum_{i=1}^N f_i \phi_i,\) (3.2)
```

where \(\phi_i : D \to C\) are called *basis functions* or *interpolation functions*. In other words, we have defined the reconstruction operation using a weighted sum of a given set of basis functions \(\phi_j\), where the weights are exactly our sample values \(f_i\). Since we want that \(\bar{f}(p_j) = f_j\) for all sample points \(p_j\), we get

```
\(\sum_{i=1}^N f_i \phi_i(p_j) = f_j, \forall j.\) (3.3)
```

Equation (3.3) must hold for any function \(f\). Let us consider a function \(g\) that is overall zero, except at \(p_j\), where \(g(p_j) = 1\). Replacing the expression for \(g\) in Equation (3.3) we obtain that

```
\(\phi_i(p_j) = \begin{cases} 1, & i=j, \\ 0, & i \neq j. \end{cases}\) (3.4)
```

Equation (3.4) is sometimes referred to as the *orthogonality of basis functions*. Let us now consider the constant function \(g(x) = 1\) for any \(x \in D\). Replacing \(g\) in Equation (3.3), we obtain that \(\sum_{i=1}^N \phi_i(p_j) = 1\) for all \(p_j\), i.e., the sum of all basis functions is 1 at all sample points. However, if we enforce that this sum is 1 at all points \(x \in D\), i.e.,

```
\(\sum_{i=1}^N \phi_i(x) = 1, \forall x \in D,\) (3.5)
```

then we can exactly reconstruct \(g\) everywhere in D. The property described in Equation (3.5) is called the *normality* of basis functions or, in some other texts, the *partition of unity*. Most basis functions used in practice in data approximation are both orthogonal and normal.

Grids and cells. To reconstruct a sampled function, we can use different basis functions. These offer different trade-offs between the continuity order of the reconstruction, on the one hand, and complexity of the functions, thus the evaluation efficiency of Equation (3.3), on the other hand. To be able to explain the different choices one has for basis functions, we must now introduce the notions of sample grids and grid cells.

A grid, sometimes also called a mesh, is a subdivision of a given domain D $\subset \mathbb{R}^d$ into a collection of cells, sometimes also called elements, denoted $c_i$. The most commonly used cells are sets of connected lines in $\mathbb{R}$ (also called polylines), polygons in $\mathbb{R}^2$, polyhedra in $\mathbb{R}^3$, and so on. Moreover, the union of the cells completely covers the sample domain, i.e., $\bigcup_i c_i = D$, and the cells are nonoverlapping, i.e., $c_i \cap c_j = \emptyset, \forall i \neq j$. In other words, a grid is a tiling of the domain D with cells. The vertices of these cells are usually the sample points $p_i \in \mathbb{R}^d$, though this is not required, as we shall see.

We can now define the simplest set of basis functions, the *constant basis functions*. For a grid with $N$ cells, we define the basis functions $\phi_i^0$ as follows:

$\phi_i^0(x) = \begin{cases} 1, & x \in c_i, \\ 0, & x \notin c_i. \end{cases} \quad (3.6)$

In Equation (3.6), the superscript 0 denotes that our basis functions are constant, i.e., of zero-order continuity. Clearly, these basis functions are orthogonal and normal. If we now imagine our sample points are inside the grid cells, e.g., at the cell centers, then these basis functions approximate a given function $\tilde{f} = \sum_i f_i \phi_i^0$ by the piecewise, per-cell, constant sample values $f_i$. For a simple grid with equal cells, such as one created by the uniform sampling discussed in Chapter 2, this interpolation is equivalent to assigning to every point $x \in D$ the sample value of the nearest cell center. For this reason, the piecewise constant interpolation is also called *nearest-neighbor interpolation*. As an example, Figure 3.2 shows the reconstruction of the Gaussian function discussed in Chapter 2 with constant basis functions.

Constant basis functions are simple to implement and have virtually no computational cost. Also, they work with any cell shape and in any dimension. However, constant basis functions provide a poor, staircase-like approximation $\tilde{f}$ of the original $f$. Over every cell $i$, $\tilde{f}$ is piecewise constant, equal to the sample value $f_i$ in that cell, but has discontinuities at the cell borders, as visible in our example (see Figure 3.2).

We can provide a better, more continuous reconstruction of the original function by using higher-order basis functions. The next-simplest basis functions beyond the constant ones are the *linear basis functions*. To use these, however, we need to make some assumptions about the cell types used in the grid. Let us consider a single quadrilateral cell $c$ having the vertices $(v_1, v_2, v_3, v_4)$, where

![](img/1274306e378c42ed8a0ad5669902d2a1_73_0.png)

Figure 3.2. Gaussian function reconstructed with constant basis functions.

$v_1 = (0, 0), v_2 = (1, 0), v_3 = (1, 1), \text{and } v_4 = (0, 1).$ i.e., an axis-aligned square of edge size 1, with the origin as first vertex. We call this the *reference cell* in $\mathbb{R}^d$. In the following, to distinguish coordinates given in the reference cell $[0, 1]^d$ from coordinates given in the function domain $\mathrm{D} \subset \mathbb{R}^d$, we denote the former by $r_1, \dots, r_d$ (or $r, s, t$ for $d=3$) and the latter by $x_1, \dots, x_d$ (or $x, y, z$ for $d=3$). Coordinates in the reference cell are also called *reference coordinates*. For our reference cell, we define now four local basis functions $\Phi_1^1, \Phi_2^1, \Phi_3^1$, and $\Phi_4^1 : [0, 1]^2 \to \mathbb{R}$ as follows (see also Figure 3.3):$^2$

```
\(\begin{aligned} \Phi_1^1(r,s) &= (1-r)(1-s), \\ \Phi_2^1(r,s) &= r(1-s), \\ \Phi_3^1(r,s) &= rs, \\ \Phi_4^1(r,s) &= (1-r)s; \end{aligned}\)
(3.7)
```

We denoted these local basis functions using capital letters (e.g., \(\Phi\)) to distinguish them from global, gridwise ones, which are denoted with lowercase letters (e.g., \(\phi\)). These basis functions are indeed orthogonal and normal. For any point \((r, s)\) in the reference cell, we can now use these basis functions to define

$^2$In the following, for a basis function \(\Phi_i^j\), the superscript \(j\) denotes the order of the function (0 = constant, 1 = linear, etc.), and the subscript $i$ denotes the index of the cell vertex to which this function corresponds.

![](img/1274306e378c42ed8a0ad5669902d2a1_74_0.png)

![](img/1274306e378c42ed8a0ad5669902d2a1_74_1.png)

Figure 3.3. Basis functions, interpolation, and coordinate transformations for the quad cell.
