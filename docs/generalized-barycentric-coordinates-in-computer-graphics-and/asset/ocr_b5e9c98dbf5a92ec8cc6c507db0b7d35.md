As an example, consider diagonal inner products on 0-forms and 1-forms,

$(u, v)_0 = \sum_{i \in V} m_i u_i v_i \quad \text{and} \quad (\alpha, \beta)_1 = \sum_{e \in E} \omega_e \alpha(e) \beta(e),$

with positive vertex weights $m_i > 0$ and positive edge weights $\omega_e > 0$. The resulting strongly defined Laplacian acting on 0-forms (functions) takes the form

$((\mathbb{L}u)_i = \frac{1}{m_i} \sum_{j \sim i} \omega_{ij} (u_i - u_j)$

and its associated weakly defined cousin is the Laplacian on graphs defined in (5.1).

# 5.3.5 Hodge decomposition

Given a choice of inner products for $k$-forms on simplicial manifolds, one always obtains a discrete Hodge decomposition. Indeed, for every discrete $k$-form $\alpha$ one has

$\alpha = \delta \mu + \delta^* \nu + h,$

where $\mu$ is a $(k-1)$-form, $\nu$ is a $(k+1)$-form and $h$ is a harmonic $k$-form ($\mathbb{L}h = 0$). As in the smooth case, not only is this decomposition unique, it is also orthogonal with respect to the inner products on $k$-forms,

$0 = (\delta \mu, \delta^* \nu)_k = (h, \delta \mu)_k = (h, \delta^* \nu)_k,$

which immediately follows from $\delta \circ \delta = 0$ and the fact that harmonic forms satisfy $\delta h = \delta^* h = 0$.

Akin to the smooth case, the Hodge decomposition establishes relations to global properties of simplicial manifolds, since the linear space of harmonic $k$-forms is isomorphic to the $k$-th simplicial cohomology of the simplicial manifold $M$. Again, as an application of this fact, consider a compact simplicial surface without a boundary. Then the dimension of the space of harmonic 1-forms is equal to twice the genus of the surface—independent of the concrete choice of inner products on $k$-forms.

# 5.3.6 The cotan Laplacian and beyond

We conclude the discussion of Laplacians on simplicial manifolds by providing an important example of inner products. In [426], Whitney constructs a map from simplicial $k$-forms ($k$-cochains) to piecewise linear differential $k$-forms. In a nutshell, the idea is to linearly interpolate simplicial $k$-forms across full-dimensional cells. As the simplest example, consider linear interpolation of 0-forms (functions) on vertices. This kind of interpolation can be extended to arbitrary $k$-forms. The resulting map

$W : C^k \to L^2 \Lambda^k$