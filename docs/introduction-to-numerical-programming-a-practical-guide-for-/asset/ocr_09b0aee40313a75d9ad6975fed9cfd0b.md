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

![](bbox=[0.355, 0.687, 0.64, 0.872])

**FIGURE 13.2**  Discretization mesh for the finite-difference solution of the Poisson equation.