The dual complex $K$ can be seen as the generalized Voronoi diagram of the $\boldsymbol{x}_i$'s for the distance $d(\boldsymbol{x}, \boldsymbol{x}_i) = \|\boldsymbol{x} - \boldsymbol{x}_i\|^2 - \omega_i$. If the vectors $\boldsymbol{v}_i$ are all zero, then the parameterized primal-dual triangulation $\mathcal{T}$ is regular, thus perpendicular to its dual $K$, and the pair $(\mathcal{T}, K)$ forms an orthogonal primal-dual triangulation. This proves that weighted Delaunay triangulations are sufficient to parameterize the set of all orthogonal primal-dual triangulations of a simply connected domain (see also [166]). The displacement vectors extend the type of triangulations and duals we can parameterize.

Characterizing the classes of equivalent triplets parameterizing the same PDT and completed with constraints for the parameters in order to avoid redundancy between equivalent triplets, the following theorem was proved in [274].

**Theorem 9.10** (PDT parameterization). There is a bijection between all primal-dual triangulations in $\mathbb{R}^d$ and sets of triplets $(\boldsymbol{x}_i, \omega_i, \boldsymbol{v}_i)$, $1 \le i \le n$, where $\boldsymbol{x}_i, \boldsymbol{v}_i \in \mathbb{R}^d$, $\omega_i \in \mathbb{R}$ with $\sum_i \omega_i = 0$, $\sum_i \boldsymbol{v}_i = 0$, and $\sum_i \|\boldsymbol{x}_i + \boldsymbol{v}_i\|^2 = \sum_i \|\boldsymbol{x}_i\|^2$.

Using this parameterization, the particular case of Delaunay and Voronoi PDT of a set of points $\{\boldsymbol{x}_i\}_{i=1, \dots, n}$ is naturally parameterized by the triplets $(\boldsymbol{x}_i, 0, \boldsymbol{0})$.

We now employ this parameterization to derive a novel discretization of calculus that verifies structural geometric properties, such as the linear accuracy for the gradient and Laplacian operators that are useful in geometry processing and graphics applications (see also [115]).

# 9.4 DISCRETE REPRESENTATION USING GENERALIZED TRIANGULATIONS

# 9.4.1 Discrete exterior calculus framework

The theory of discrete exterior calculus (see Section 5.2.1) provides one possible discretization of differential geometry, which has proven to be highly successful in improving and analyzing finite element methods.

The geometric principles on which these methods of computations are built are very intuitive. In this framework, discrete differential forms are considered as continuous forms integrated over each discrete element (simplices and cells). Once discrete forms and vector fields are defined, a calculus can be developed by defining discrete operators.

For example, the classical operations of gradient, divergence, and curl, as well as the theorems of Green, Gauss, and Stokes can all be expressed concisely in terms of two differential forms: the discrete exterior derivative (d) and the Hodge star (*). More details on the discrete exterior calculus framework can be found in a variety of sources [118, 192], as well as in a recent Siggraph course [109].

Here, we are particularly interested in the discrete Hodge star *, which takes geometry into account by encoding how integrated measures over primal elements are transferred to their associated dual elements. More concretely, the discrete diagonal Hodge star for discrete $p$-forms is defined as a diagonal matrix with entries