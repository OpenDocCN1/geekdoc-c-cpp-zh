# ## 10.4 The Discretization

The terms in the above PDE that contain spatial derivatives are symmetric in the sense to be described in Chapter 11, Section 2. Thus, the discretization method must be defined so that the matrix that contains the discrete spatial derivatives is also symmetric. Furthermore, in Chapter 12, Section 4, we'll see that it is also desirable that this matrix be diagonally dominant. Thus, we already have rather clear guidelines toward the definition of a discretization method.

In fact, we already have a discretization method that enjoys the above properties. This discretization method is defined in the exercises at the end of Chapter 8 for linear diffusion problems. It is based on the observation that if the diffusion coefficient $P$ is evaluated at midpoints of the form $(j+1/2,i)$ and $(j,i+1/2)$ in the grid, then the resulting matrices that contain the discrete spatial derivatives at a particular time step are symmetric and diagonally dominant [78]. In the exercises at the end of Chapter 8, it is shown that these properties are attractive because they guarantee that the implicit and semi-implicit schemes are stable and accurate with respect to the usual norm.

The finite-difference discretization is based on the approximation

$$(P u_x)_{(j+1/2)h_x,ih_y}=P_{j+1/2,i}h_x^{-1}\bigl(u((j+1)h_x,ih_y)-u(jh_x,ih_y)\bigr),$$

where $P_{j+1/2,i}$ is an approximation of $P$ at the corresponding midpoint:

$$P_{j+1/2,i}=\frac{1}{1+\eta^{-1}(u_{x,j+1/2,i}^{2}+u_{y,j+1/2,i}^{2})}.$$

where $u_x{}_{j+1/2,i}$ and $u_y{}_{j+1/2,i}$ are approximations to $u_x$ and $u_y$, respectively, at the corresponding midpoint:

$$u_{x,j+1/2,i}=h_x^{-1}\bigl(u((j+1)h_x,ih_y)-u(jh_x,ih_y)\bigr),$$

$$u_{y,j+1/2,i}=(4h_y)^{-1}\bigl(u((j+1)h_x,(i+1)h_y)+u(jh_x,(i+1)h_y)$$
$$\qquad-u((j+1)h_x,(i-1)h_y)-u(jh_x,(i-1)h_y)\bigr).$$

Actually, it turns out that, in noncolor (grayscale) images, this latter term can be dropped or replaced by the simpler term

$$u_{y,j+1/2,i}=h_y^{-1}\bigl(u(jh_x,(i+1)h_y)-u(jh_x,ih_y)\bigr)$$

to increase efficiency.

Note that the above definitions may use points that lie outside the grid and, hence, are not well defined. For example, when $i$ indicates the top line in the grid, $i+1$ is not well defined. Fortunately, using the homogeneous Neumann boundary conditions, $i+1$ can be replaced by $i$ in this case. Similarly, when $i$ indicates the bottom line in the grid, $i-1$ should be replaced by $i$ in the above formulas. A similar approach is used when $j=N_x$, $(j+1\leftarrow j)$ and $j=0$ $(j-1\leftarrow j)$.

The above definition of $P$ at the midpoints is now used to discretize the term $(P u_x)_x$ at the grid points themselves, as in Chapter 7, Section 13. This completes the discretization of the first spatial term in the PDE.

The discretization of the second spatial term, $(P u_y)_y$, is done in a similar way, by inverting the roles of $x$ and $y$ (and $i$ and $j$) in the above formulas. The time derivative is