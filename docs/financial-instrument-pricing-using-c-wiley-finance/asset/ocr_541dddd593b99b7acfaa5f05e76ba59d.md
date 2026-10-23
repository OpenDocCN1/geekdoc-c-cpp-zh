**c)** In Section A1.5 we computed Fresnel integrals as the numerical solution of two real ODEs. It is possible to write such integrals as a single integral with complex-valued integrand:

$$\psi(x)=\int_0^x e^{\frac{i\pi}{2}t^2}\,dt.$$

This formula is found in diffraction applications. We can now differentiate this integral to produce the complex ODE:

$$\frac{d\psi}{dx}=e^{\frac{i\pi}{2}x^2},\quad x>0$$

$$\psi(0)=0.$$

Implement this ODE using the same code as in the above introductory code.

# 3. (Quadratic Equations)

Consider computing the roots of the quadratic equation:

$$94906265.625x^2-189812534x+94906268.375=0.$$

Its roots are:

$x_1=1.00000002897958$

$x_2=1.00000000000000$

while using IEEE 754 double-precision arithmetic corresponding to 15 and 17 significant digits of accuracy the computed roots are:

$x_1=1.000000014487979$

$x_2=1.000000014487979$

Compute the roots of this quadratic equation using Boost multiprecision data types.

# 4. (Heat Equation and Separation of Variables)

Consider the heat equation on a bounded domain with Dirichlet boundary conditions:

$$\frac{\partial u}{\partial x}=\frac{\partial^2u}{\partial x^2},\quad 0<x<1,\ t>0$$

$$u(0,t)=u(1,t)=0$$

$$u(x,0)=2x,\quad 0\le x\le \frac{1}{2}$$

$$u(x,0)=2(1-x),\quad \frac{1}{2}\le x\le 1.$$