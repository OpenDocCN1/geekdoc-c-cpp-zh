![](bbox=[0.38, 0.13, 0.62, 0.27])

Figure 10.5 A function z(x, y) and its polar dual. Tangent planes map to points.

# 10.2.2 Airy stress potential

We can again decompose the equilibrium equation (10.4) into horizontal and vertical components,

```
0 = \nabla \cdot S
```

```
F \sqrt{\det g} = \nabla \cdot [S \nabla z].
```

The first set of equations, together with symmetry of S, are precisely the local integrability conditions required for existence of a scalar function, the Airy stress potential s, with

```
S = \begin{bmatrix} s_{yy} & -s_{xy} \\ -s_{xy} & s_{xx} \end{bmatrix} = J^T[\mathbf{H}_s]J,
```

where H_s is the Hessian of s and J is the ninety-degree rotation matrix.

In direct analogy to the discussion above on reciprocal diagrams, if M is simply connected, s exists globally, and we have the following theorem.

**Theorem 10.2.** The surface M with simply connected top view \bar{M} is in compressive static equilibrium if there exists a convex function s: M \rightarrow \mathbb{R} with

```
F \sqrt{\det g} = \nabla \cdot J^T[\mathbf{H}_s]J \nabla z
```

at every point on the interior of \bar{M}, and

```
[\mathbf{H}_s]J\hat{\mathbf{n}} = \mathbf{0}
```

on the free boundary, where \hat{\mathbf{n}} is the normal to \partial \bar{M}.

# 10.2.3 Relative curvatures

The standard Gauss map \xi maps every point on a surface z(x, y) to the corresponding point on the unit sphere with matching tangent plane. This idea can be generalized: given a second, convex surface s(x, y), we define the relative Gauss