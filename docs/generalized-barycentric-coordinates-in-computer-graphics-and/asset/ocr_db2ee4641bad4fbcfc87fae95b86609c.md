which is known as the *Dirichlet energy* of $u$. In the discrete setup, one may discretize the gradient $\nabla u$ along an edge $e = (i, j)$ as the finite difference $(u_i - u_j)$. Accordingly, one defines discrete Dirichlet energy as

```
$E_D[u] = \frac{1}{2} \sum_{e \in E} \omega_{ij} (u_i - u_j)^2,$
```

where the sum ranges over all edges. Then one has

```
(discrete) $E_D[u] = \frac{1}{2} u^T L u$ vs. (smooth) $E_D[u] = \frac{1}{2} (u, \Delta u)_0,$
```

which justifies calling $L$ a Laplace matrix. Due to this representation (and using the language of partial differential equations [140]) we call discrete Laplacians of the form (5.1) *weakly defined* instead of *strongly defined*. We return to this distinction below.

Weakly defined discrete Laplacians of the form (5.1) are always symmetric— they satisfy (SYM) due to the assumption that $\omega_{ij} = \omega_{ji}$. However, whether or not a discrete Laplacian satisfies (at least some of) the other properties of the smooth setting heavily depends on the choice of weights.

The simplest choice of weights is to set $\omega_{ij} = 1$ whenever there is an edge between vertices $i$ and $j$. This results in the so-called *graph Laplacian*. The diagonal entries of the graph Laplacian are equal to the degree of the respective vertex, that is, the number of edges adjacent to that vertex. The graph Laplacian is just a special case of what we call a *Laplacian on graphs* here.

Positive edge weights are a natural choice if weights resemble transition probabilities of a random walker. Discrete Laplacians with positive weights are always positive semidefinite (PSD) and, just like in the smooth setting, they only have the constant functions in their kernel provided that the graph is connected. As a word of caution we remark that positivity of weights is *not* necessary to guarantee (PSD). Below we discuss Laplacians that allow for (some) negative edge weights but still satisfy (PSD).

Laplacians with positive edge weights always satisfy the mean value property since every harmonic function $u$ (a function for which $Lu = 0$) satisfies

```
$u_i = \sum_{j \sim i} l_{ij} u_j \quad \text{with} \quad l_{ij} = \frac{\omega_{ij}}{L_{ii}} > 0.$
```

Therefore, discrete Laplacians with positive weights also satisfy the maximum principle (Max) since $\sum_{j \sim i} l_{ij} = 1$ and thus $u_i$ is a convex combination of its neighbors $u_j$ for discrete harmonic functions. This convex combination property establishes a connection between Laplacians and barycentric coordinates via the partition of unity property (1.8).

# 5.3.2 The spectrum

As in the smooth case, one cannot discuss discrete Laplacians without mentioning their spectrum and their eigenfunctions, which provide a fingerprint of the structure of the underlying graph.