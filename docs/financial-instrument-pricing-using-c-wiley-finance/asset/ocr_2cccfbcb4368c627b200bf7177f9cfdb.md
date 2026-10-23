Our aim in this exercise is to use the Saul’yev method in combination with upwinding for the convection term. We first concentrate on the constant-coefficient convection–diffusion equation:

\[\frac{\partial u}{\partial t} + c \frac{\partial u}{\partial x} = v \frac{\partial^2 u}{\partial x^2}\;(c, v > 0)\]

in addition to Dirichlet boundary conditions and an initial condition. Answer the following questions:

a) Verify that the Saul’yev scheme with upwinding leads to the following sweeps for odd and even time levels:

\[(1 + \rho) u_j^{n+1} = (1 - \rho) u_j^n + \rho\left(u_{j-1}^{n+1} + u_{j+1}^n\right) - \tau\left(u_j^n - u_{j-1}^n\right)\]

and

\[(1 + \rho) u_j^{n+1} = (1 - \rho) u_j^n + \rho\left(u_{j+1}^{n+1} + u_{j-1}^n\right) - \tau\left(u_j^n - u_{j-1}^n\right)\]

where:

\[\tau = \frac{c \Delta t}{h}, \rho = \frac{v \Delta t}{h^2}.\]

b) Implement this scheme for the linear convection–diffusion equation:

\[\frac{\partial u}{\partial t} + c \frac{\partial u}{\partial x} = v \frac{\partial^2 u}{\partial x^2},\; 0 \le x \le 20,\; t \ge 0\]

with initial condition:

\[u(x,0) = \exp\left(-\alpha (1 - x_1)^2\right),\; \alpha = 6, x_1 = 2.\]

The exact solution is given by:

\[u(x,t) = (1 + 4\alpha v t)^{-1/2} \exp\left\{-\frac{\alpha (x - x_1 - c t)^2}{1 + 4\alpha v t}\right\}.\]

c) Implement this scheme for the viscous Burgers' equation:

\[\frac{\partial u}{\partial t} + u \frac{\partial u}{\partial x} = v \frac{\partial^2 u}{\partial x^2},\; 0 \le x \le 10,\; t \ge 0\]

with initial condition:

\[u(x,0) = \begin{cases} 1, & 0 \le x < 1 \\ 0, & 1 < x \le 10. \end{cases}\]