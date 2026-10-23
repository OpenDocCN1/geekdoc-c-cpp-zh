$u_{2j}(h/2)$ and $u_j(h)$, $j=0,\ldots,J$ be the finite difference solutions on the meshes $h/2$ and $h$, respectively. Now construct the array:

$$\bar{u}_j=\frac{4}{3}u_{2j}(h/2)-\frac{1}{3}u_j(h)\qquad 0\leq j\leq J.$$

Verify by numerical experiment that it is a fourth-order approximation to the exact solution.

+   **f)** Use first-order upwinding as in equation (20.47). Is the resulting matrix monotone? Can you reproduce the numerical results for this scheme as reported in Section 20.7.1?

+   **g)** Convert system (20.50) to conservative form and approximate it using the finite difference method.

+   **h)** We now return to Chapter 13 by solving the heat equation using Rothe’s method. The *semi-discrete system* of ODEs will be a special case of the following equation that uses implicit Euler in time:

$$-\frac{u^{n+1}-u^n}{\Delta t}+\sigma(x,t_{n+1})\frac{d^2u^{n+1}}{dx^2}+\mu(x,t_{n+1})\frac{du^{n+1}}{dx}+b(x,t_{n+1})u^{n+1}=f(x,t_{n+1}),$$

$$0\leq n\leq N-1.$$

Implement the scheme in C++ using explicit Euler (for convenience) as the approximation to the time derivative. The focus is on creating an algorithm that can easily be mapped to C++. The algorithm will need to implement the time-marching aspect of the problem.