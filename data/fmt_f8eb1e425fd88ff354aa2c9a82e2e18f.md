
Mixed boundary conditions, prescribing linear combinations of solution and derivative values on the boundary,

```
α(x, y) u(x, y) + β(x, y) ∂u/∂n (x, y) = γ(x, y),   for (x, y) ∈ S.
```

A special category of boundary-value problems is the one of the eigenproblems, which admit stationary solutions only for particular values of a parameter, called eigenvalues.

Initial-value (Cauchy) problems are naturally associated with parabolic or hyperbolic equations and typically model propagation phenomena. Specifically, based on the known spatial behavior of the solution (and possibly also of its time derivative) at some initial moment t₀, the differential equation governs the propagation of the solution u(x, t) in space and time.

From a numerical perspective, the classification according to the type of problem tends to prevail over the equation type, since the character of the boundary conditions is one of the determining aspects in adopting the numerical strategy. The conceptual differences between the boundary-value and initial-value problems are also suggested by Figure 13.1. Even though the main goal of both types of problems is the calculation of the solution on a spatial grid, the steady-state solution for boundary-value problems is determined by a numerical process simultaneously converging in the entire domain D, whereas, in the

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_531_0.png)

**FIGURE 13.1** Integration grids for (a) boundary-value problems and (b) initial-value problems. Full circles stand for the input data, while empty circles represent the solution values that need to be calculated.

case of initial-value problems, the solution values from all the points of the spatial domain are recursively propagated in time, starting from the solution at the initial moment t0.

## 13.2 Boundary-Value Problems for Elliptic Differential Equations

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

By their addition, we get the following finite-difference scheme for the second derivative:

$$\left(\frac{\partial^2 u}{\partial x^2}\right)_{i,j}=\frac{u_{i+1,j}-2u_{i,j}+u_{i-1,j}}{h_x^2}+O(h_x^2). \tag{13.3}$$

The $O(h_x^2)$ error term results by the exact cancellation of the third-order terms in the above $O(h_x^4)$ expansions and the subsequent division by $h_x^2$ for expressing the second derivative. The formula is said to be a *central-difference scheme*, since it uses information from nodes distributed symmetrically about the point where the derivative is being evaluated.

Analogously, for the second derivative along the $y$-direction, we have the scheme:

$$\left(\frac{\partial^2 u}{\partial y^2}\right)_{i,j}=\frac{u_{i,j+1}-2u_{i,j}+u_{i,j-1}}{h_y^2}+O(h_y^2). \tag{13.4}$$

Thus, for the Laplacian of function $u$ at the node $(x_i,y_j)$, there results a five-point difference scheme, which may be correlated with the graphical representation in Figure 13.2:

$$\nabla^2u(x,y)\big|_{i,j}=\frac{1}{h_y^2}u_{i,j-1}+\frac{1}{h_x^2}u_{i-1,j}-2\left(\frac{1}{h_x^2}+\frac{1}{h_y^2}\right)u_{i,j}+\frac{1}{h_x^2}u_{i+1,j}+\frac{1}{h_y^2}u_{i,j+1}+O(h_x^2+h_y^2). \tag{13.5}$$

Therewith, one obtains the following finite-difference representation of the Poisson equation (13.1) at the interior points of the domain $\mathcal{D}$:

$$\frac{1}{h_y^2}u_{i,j-1}+\frac{1}{h_x^2}u_{i-1,j}-2\left(\frac{1}{h_x^2}+\frac{1}{h_y^2}\right)u_{i,j}+\frac{1}{h_x^2}u_{i+1,j}+\frac{1}{h_y^2}u_{i,j+1}=f_{i,j},$$

$$i=2,\ldots,N_x-1,\qquad j=2,\ldots,N_y-1. \tag{13.6}$$

where $f_{i,j}=f(x_i,y_j)$.

The linear system (13.6), having as unknowns the solution values $u_{i,j}$ at the grid nodes, does not actually contain sufficient equations for the solution to be completely determined. On the other hand, the five-point discretization scheme employed for the Laplacian prevents the direct embedding of the boundary conditions, which have thus to be treated separately.

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_532_0.png)

**FIGURE 13.2**  Discretization mesh for the finite-difference solution of the Poisson equation.

Quite often, discretizing the boundary conditions is more intricate than discretizing the PDEs themselves. For the sake of clarity, we use in the following the lowest-order approximations for the mixed boundary conditions. Concretely, considering the normal derivatives to be positive if they are oriented outward from the domain D, the conditions on the left and, respectively, right boundary (i = 1 and i = Nx) can be expressed as

```
α_j^{x min} u_{1j} + β_j^{x min} (u_{1j} - u_{2j})/h_x = γ_j^{x min},   i = 1,
α_j^{x max} u_{Nx,j} + β_j^{x max} (u_{Nx,j} - u_{Nx-1,j})/h_x = γ_j^{x max},   i = N_x,
j = 1, ..., N_y.
```

In a similar manner, the discretized conditions on the lower and, respectively, upper boundary (j = 1 and j = N_y) read:

```
α_i^{y min} u_{i,1} + β_i^{y min} (u_{i,1} - u_{i,2})/h_y = γ_i^{y min},   j = 1,
α_i^{y max} u_{i,N} + β_i^{y max} (u_{i,Ny} - u_{i,Ny-1})/h_y = γ_i^{y max},   j = N_y,
i = 1, ..., N_x.
```

To simplify the discretized equations and the boundary coefficients, we define the quantities:

```
k_x = 1/h_x^2,   k_y = 1/h_y^2,   k_xy = 2(1/h_x^2 + 1/h_y^2),   (13.7)
```

and the boundary coefficients:

```
β̄_i^{y min} = β_i^{y min} / (α_i^{y min} h_y + β_i^{y min}),   γ̄_i^{y min} = γ_i^{y min} / (α_i^{y min} + β_i^{y min}/h_y),
β̄_i^{y max} = β_i^{y max} / (α_i^{y max} h_y + β_i^{y max}),   γ̄_i^{y max} = γ_i^{y max} / (α_i^{y max} + β_i^{y max}/h_y),
β̄_j^{x min} = β_j^{x min} / (α_j^{x min} h_x + β_j^{x min}),   γ̄_j^{x min} = γ_j^{x min} / (α_j^{x min} + β_j^{x min}/h_x),   (13.8)
β̄_j^{x max} = β_j^{x max} / (α_j^{x max} h_x + β_j^{x max}),   γ̄_j^{x max} = γ_j^{x max} / (α_j^{x max} + β_j^{x max}/h_x).
```

Therewith, the complete linear system resulting by discretizing the Poisson equation and the attached mixed boundary conditions takes the form:

```
u_{i,1} - β̄_i^{y min} u_{i,2} = γ̄_i^{y min},   i = 1, ..., N_x,   j = 1,   (bottom)   (13.9)
u_{1j} - β̄_j^{x min} u_{2j} = γ̄_j^{x min},   i = 1,   j = 2, ..., N_y - 1,   (left)   (13.10)
k_y u_{i,j-1} + k_x u_{i-1,j} - k_xy u_{i,j} + k_x u_{i+1,j} + k_y u_{i,j+1} = f_{i,j}
i = 2, ..., N_x - 1,   j = 2, ..., N_y - 1,   j = 1,   (interior)   (13.11)
- β̄_j^{x max} u_{Nx-1,j} + u_{Nx,j} = γ̄_j^{x max},   i = N_x,   j = 2, ..., N_y - 1,   (right)   (13.12)
- β̄_i^{y max} u_{i,Ny-1} + u_{i,Ny} = γ̄_i^{y max},   i = 1, ..., N_x,   j = N_y.   (top)   (13.13)
```

整个离散化系统可以用一般形式正式重写，这有助于揭示其结构：

```
a_i^j u_{i,j-1} + b_{ai}^j u_{i-1,j} + b_{bi}^j u_{i,j} + b_{ci}^j u_{i+1,j} + c_i^j u_{i,j+1} = d_i^j,

 i = 1, ..., N_x,   j = 1, ..., N_y. (13.14)
```

考虑到以网格节点 (i,j) 为中心的离散方程不仅连接五个相邻值 (u_{i,j-1}, u_{i-1,j}, u_{i,j}, u_{i+1,j}, u_{i,j+1})，还连接三个相邻行 j-1、j 和 j+1 上的所有值，该系统可以改写为

```
∑_{i'=1}^{N_x} [A_{ii'}^j u_{i',j-1} + B_{ii'}^j u_{i',j} + C_{ii'}^j u_{i',j+1}] = d_i^j,

 i = 1, ..., N_x,   j = 1, ..., N_y, (13.15)
```

其中 N_x × N_x 块 A^j = [A_{ii'}^j]_{N_x,N_x}、B^j = [B_{ii'}^j]_{N_x,N_x} 和 C^j = [C_{ii'}^j]_{N_x,N_x} 的元素为：

```
A_{ii'}^j = a_i^j δ_{ii'},
```
