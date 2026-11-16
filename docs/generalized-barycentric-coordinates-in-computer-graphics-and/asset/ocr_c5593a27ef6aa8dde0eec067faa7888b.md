where the sums index over the faces circulating around a vertex of $\bar{G}$.

The discrete Airy stress surface is not unique, since the choice of the gradient of the first face of $S$ was chosen arbitrarily. Different stress surfaces of the same diagram will differ by addition of a linear function to $S$. The above constructions also require $\bar{G}$ to be simply connected; otherwise $S$ can only be assembled locally.

# 10.3.4 FEM discretization of Airy stress

By the above construction, lengths on the reciprocal diagram correspond to the magnitude of the jump in the gradient of $S$ when moving between neighboring faces. This relationship has also been observed by Fraternali [156], who derived it in the context of finite element analysis of cracking in masonry vaults. Starting from the smooth setting, both the thrust surface $z(x, y)$ and the Airy stress potential $s(x, y)$ can be discretized using piecewise linear shape functions over the top view $\bar{G}$. Doing so, and discretizing horizontal equilibrium using Galerkin finite elements, yields the orthogonal relationship between gradient jumps of $S$ and edges of $\bar{G}$.

# 10.3.5 Discrete curvature interpretation of equilibrium

Relative curvature of a polyhedral surface at a vertex with respect to a second polyhedral surface has been studied by Bobenko et al. [56] and formulated in terms of mixed areas of vertex neighborhoods. This concept can be extended to dual isotropic relative curvature [311] to yield formulas for the dual relative mean curvature at a vertex $\mathbf{v}_i$ of a discrete surface $G$.

```
$$H_{\bar{G}^*}^{S^*}(\mathbf{v}_i) = \frac{A_i(G^*, S^*)}{A_i(S^*, S^*)},$$\n$$A_i(G^*, S^*) = \frac{1}{4} \sum_j [\det(\vec{v}_j^*, \vec{s}_j^*) + \det(\vec{s}_j^*, \vec{v}_j^*)],$$
```

where the sum in the mixed area term $A_i$ is over the faces in the one-ring of $\mathbf{v}_i$. It can be shown [405] that the mixed area in the numerator is

```
$$2A_i(G^*, S^*) = \sum_{j \sim i} w_{ij}(z_j - z_i),$$
```

where the weights $w_{ij}$ are those corresponding to the reciprocal diagram constructed from $S$. Moreover, the dual Gaussian curvature relative to the Maxwell paraboloid is

```
$$K_{\bar{G}^*}^h(\mathbf{v}_i) = \frac{A_i(S^*, S^*)}{A_i},$$
```

where $A_i$ (with no arguments) is, as before, the Voronoi area of $\bar{\mathbf{v}}_i$ in the top view. Putting together all of the pieces and combining them with (10.3), we have, in direct analogy to (10.6), the following theorem.