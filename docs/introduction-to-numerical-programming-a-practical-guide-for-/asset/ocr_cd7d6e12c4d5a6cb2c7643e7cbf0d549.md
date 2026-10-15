![](bbox=[0.22, 0.12, 0.78, 0.32])

FIGURE 13.1 Integration grids for (a) boundary-value problems and (b) initial-value problems. Full circles stand for the input data, while empty circles represent the solution values that need to be calculated.

case of initial-value problems, the solution values from all the points of the spatial domain are recursively propagated in time, starting from the solution at the initial moment t0.

# 13.2 Boundary-Value Problems for Elliptic Differential Equations

With a view to expounding the discretization principles for boundary-value problems, we consider in the following the 2D Poisson equation in Cartesian coordinates:

```
∇² u(x,y) ≡ ∂²u/∂x² + ∂²u/∂y² = f(x,y).  (13.1)
```

We choose the rectangular integration domain D ≡ [x_min, x_max] × [y_min, y_max] and impose mixed boundary conditions:

```
[α u + β ∂u/∂n]_(x,y)∈S = γ,  (13.2)
```

where α(x,y), β(x,y), and γ(x,y) are functions defined on the domain boundary S. In particular, we have Dirichlet conditions for β = 0 (fixed solution values), Neumann conditions for α = 0 (fixed normal derivatives), and the so-called uniform conditions for γ = 0.

Following the basic approach of the finite-difference methods, we restrict the solution to the N_x × N_y values u_ij ≡ u(x_i, y_j) at the nodes of a uniform spatial grid, defined by

```
x_i = x_min + (i - 1)h_x,   i = 1,2,...,N_x,
 y_j = y_min + (j - 1)h_y,   j = 1,2,...,N_y,
```