$r_1,r_2$ are the partial derivatives of $\mathbf r$ with respect to $u_1$ and $u_2$, respectively. The *Riemannian metric* or the *first fundamental form* is

$$\langle d\mathbf r,d\mathbf r\rangle=\sum\langle r_i,r_j\rangle\,du_i\,du_j,\quad i,j=1,2.$$ (4.1)

The Gauss map $G:S\to S^2$ from the surface $S$ to the unit sphere $S^2$ maps each point $p$ on the surface to its normal $\mathbf n(p)$ on the sphere. The *Gaussian curvature* $K(p)$ is defined as the *Jacobian of the Gauss map*. Intuitively, it is the ratio between the infinitesimal area of the Gauss image on the Gaussian sphere and the infinitesimal area on the surface.

Let $\partial S$ be the boundary of the surface $S$, $k_g$ the geodesic curvature, $dA$ the area element, $ds$ the line element, and $\chi(S)$ the Euler characteristic number of $S$. The total curvature is determined by the topology, which satisfies the following Gauss–Bonnet Theorem:

$$\int_S K\,dA+\int_{\partial S}k_g\,ds=2\pi\chi(S).$$ (4.2)

# Conformal Deformation

Let $S$ be a surface embedded in $\mathbb R^3$. $S$ has a Riemannian metric induced from the Euclidean metric of $\mathbb R^3$, denoted by $\mathbf g$. Suppose $u:S\to\mathbb R$ is a scalar function defined on $S$. It can be verified that $\bar{\mathbf g}=e^{2u}\mathbf g$ is also a Riemannian metric on $S$. Furthermore, angles measured by $\mathbf g$ are equal to those measured by $\bar{\mathbf g}$. Therefore, we say $\bar{\mathbf g}$ is a conformal deformation from $\mathbf g$.

A conformal deformation maps infinitesimal circles to infinitesimal circles and preserves the intersection angles among the infinitesimal circles. In Figure 4.1, we illustrate this property by approximating infinitesimal circles by finite circles. We put a regular circle packing pattern on the texture and map the texture to the surface using a conformal parameterization, where all the circles on the texture still look like circles on the surface, and all the tangency relations among the circles are preserved.

When the Riemannian metric is conformally deformed, curvatures will also be changed accordingly. Suppose $\mathbf g$ is changed to $\bar{\mathbf g}=e^{2u}\mathbf g$. Then, the Gaussian curvature will become

$$\bar K=e^{-2u}(-\Delta_{\mathbf g}u+K).$$ (4.3)