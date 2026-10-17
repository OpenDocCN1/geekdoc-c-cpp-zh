Similarly, if we assume that a mesh is embedded in the 3D sphere $S^3$, then each face is a spherical triangle. We say the mesh is with spherical background geometry (see **Figure 4.2a**). The angles and the edge lengths of each face satisfy the spherical cosine law.

Furthermore, if we assume that a mesh is embedded in the 3D hyperbolic space $\mathbb{H}^3$, then all faces are hyperbolic triangles. We say the mesh is with hyperbolic background geometry (see **Figure 4.2c**). The angles and the edge lengths of each face satisfy the hyperbolic cosine law.

In the following discussion, we will explicitly specify the background geometry for a mesh when it is needed. Otherwise, the concept or the algorithm is appropriate for all kinds of background geometries.

# Discrete Riemannian Metric

A discrete Riemannian metric on a mesh $\Sigma$ is a piecewise constant metric with cone singularities. A metric on a mesh with Euclidean metric is a discrete Euclidean metric with cone singularities. Each vertex is a cone singularity. Similarly, a metric on a mesh with spherical background geometry is a discrete spherical metric with cone singularities; a metric on a mesh with hyperbolic background geometry is a discrete hyperbolic metric with cone singularities.

The edge lengths of a mesh $\Sigma$ are sufficient to define a discrete Riemannian metric:

```
$l:E\to\mathbb{R}^{+}$
```

as long as, for each face $f_{ijk}$, the edge lengths satisfy the triangle inequality $l_{ij}+l_{jk}>l_{ki}$ for the three background geometries, and another inequality $l_{ij}+l_{jk}+l_{ki}<2\pi$ for spherical geometry.

# Discrete Gaussian Curvature

The discrete Gaussian curvature $K_i$ on a vertex $v_i\in\Sigma$ can be computed from the angle deficit:

```
$$K_i=\begin{cases} 2\pi-\displaystyle\sum_{f_{ijk}\in F}\theta_i^{jk}, & v_i\notin\partial\Sigma\\[4pt] \pi-\displaystyle\sum_{f_{ijk}\in F}\theta_i^{jk}, & v_i\in\partial\Sigma \end{cases}$$
```

where $\theta_i^{jk}$ represents the corner angle attached to vertex $v_i$ in the face $f_{ijk}$, and $\partial\Sigma$ represents the boundary of the mesh. The discrete Gaussian curvatures are determined by the discrete metrics.