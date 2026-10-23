# 13.8 EXERCISES AND PROJECTS

1. (Double Sweep Method)
Generalise the Double Sweep method from one that supports Dirichlet boundary conditions to one that supports Robin boundary conditions:

```
\begin{cases}
a_j U_{j-1} + b_j U_j + c_j U_{j+1} = f_j, \quad 1 \le j \le J-1 \\
U_0 = \alpha U_1 + \varphi \\
U_{J-1} = \beta U_J + \psi
\end{cases}
```

where α, β, φ and ψ are given constants. You should get equations similar to those in Section 13.2.1.

Test the new algorithm by discretising the two-point boundary value problem:

```
\begin{cases}
\dfrac{d^2 u}{dx^2} = f(x), \quad 0 < x < 1 \\
u(0) = \varphi \\
\dfrac{du(1)}{dx} + \beta u(1) = \psi
\end{cases}
```

using the following finite difference scheme:

```
\begin{cases}
U_{j+1} - 2U_j + U_{j-1} = h^2 f_j, \quad 1 \le j \le J-1 \\
U_0 = \varphi \\
\dfrac{U_J - U_{J-1}}{h} + \dfrac{\beta}{2}(U_J + U_{J-1}) = \psi.
\end{cases}
```

We note that the averaged approximation at the boundary x = 1 is second-order accurate (see Morton and Mayers, 1994).

Answer the following questions:

+   a) Modify the Double Sweep algorithm so that it can be applied to problems with Robin boundary conditions.

+   b) Test the new code on the above two-point boundary value problem. Assemble the system of equations and determine the conditions under which the tridiagonal matrix is diagonally dominant, hence ensuring that the system has a unique solution. When is the matrix an M-matrix?

+   c) Solve the two-point boundary value problem using the Thomas algorithm and compare the efficiency and accuracy with the results in part b).

+   d) Consider the first-order approximation at x = 1:

```
\dfrac{U_J - U_{J-1}}{h} + \beta U_J = \psi.
```