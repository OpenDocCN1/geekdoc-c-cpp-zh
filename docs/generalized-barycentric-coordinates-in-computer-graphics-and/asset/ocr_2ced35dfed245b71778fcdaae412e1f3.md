into their Fourier modes has a plethora of applications in geometry processing; see [242] and references therein.

As in the smooth setting, it is natural to ask the inverse question of how much geometric information can be inferred from information about the Laplacian. Recall that in the smooth case, knowing the full Laplacian allows for recovering the Riemannian metric. Similarly, in the discrete case it can be shown that for simplicial surfaces the knowledge of the cotan weights for discrete Laplacians (covered below) allows for reconstructing edge lengths (i.e., the discrete metric) of the underlying mesh up to a global scale factor [432]. If, however, only the spectrum of the Laplacian is known, then there exist isospectral but non-isomorphic graphs [76]. In fact, for the case of the cotan Laplacian (see below), the exact same isospectral domains considered in [169] that were originally proposed for showing that “One cannot hear the shape of a drum” for smooth Laplacians work in the discrete setup.

A curious fact concerning the connection between discrete Laplacian and the underlying geometry is *Rippa’s theorem* [326]: The Delaunay triangulation of a fixed point set in $\mathbb{R}^n$ minimizes the Dirichlet energy of any piecewise linear function over this point set. In [96], this result is taken a step further, where the authors show that the spectrum of the cotan Laplacian obtains its minimum on a Delaunay triangulation in the sense that the $i$-th eigenvalue of the cotan Laplacian of any triangulation of a fixed point set in the plane is bounded below by the $i$-th eigenvalue resulting from the cotan Laplacian associated with the Delaunay triangulation of the given point set.

# 5.3.3 Laplacians on simplicial manifolds

Recall that in the smooth case, Laplacians acting on $k$-forms take the form

```
$\Delta = dd^* + d^*d.$
```

In order to mimic this construction in the discrete setting, one requires a bit more structure than just an arbitrary graph. To this end, consider a simplicial manifold, such as a triangulated surface. We keep referring to this manifold as $M$. As in the smooth case, for simplicity, suppose that $M$ is orientable and has no boundary.

Simplicial manifolds allow for a natural definition of discrete $k$-forms as duals of $k$-cells. Indeed, every 0-form is a function defined on vertices, a 1-form $\alpha$ is dual to edges, that is, $\alpha(e)$ is a real number for any oriented 1-cell (oriented edge), a 2-form is dual to oriented 2-cells, and so forth. In the sequel, let the linear space of discrete $k$-forms (better known as simplicial cochains) be denoted by $\mathcal{C}^k$.

As in the smooth case, the discrete differential $\delta$ (better known as the coboundary operator) maps discrete $k$-forms to discrete $(k+1)$-forms, $\delta: \mathcal{C}^k \to \mathcal{C}^{k+1}$. Again as in the smooth case, the discrete differential can be defined by *postulating* Stokes’s formula: Let $\alpha$ be a discrete $k$-form. Then one requires that

```
$\delta \alpha(\sigma) = \alpha(\partial \sigma)$
```

for all $(k+1)$-cells $\sigma$, where $\partial$ denotes the simplicial boundary operator. The simplicial boundary operator, when applied to a vertex returns zero (since vertices do