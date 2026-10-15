unconditionally stable method. In fact, taking as reference t_{n+1}, the very same discrete approximation of the time derivative (Equation 13.43) now becomes a backward-difference scheme:

```
\left(\frac{\partial u}{\partial t}\right)_{i,n+1} = \frac{u_i^{n+1} - u_i^{n}}{h_t} + O(h_t). \tag{13.63}
```

The spatial derivative, in turn, needs to be built accordingly, based on values from time step t_{n+1}:

```
\left(\frac{\partial^2 u}{\partial x^2}\right)_{i,n+1} = \frac{u_{i+1}^{n+1} - 2u_i^{n+1} + u_{i-1}^{n+1}}{h_x^2} + O(h_x^2). \tag{13.64}
```

The difference equation resulting for the space–time point (x_i, t_{n+1}),

```
\frac{u_i^{n+1} - u_i^{n}}{h_t} = D \frac{u_{i+1}^{n+1} - 2u_i^{n+1} + u_{i-1}^{n+1}}{h_x^2}, \tag{13.65}
```

represents the so-called backward-time central-space (BTCS) method and is, analogously to the FTCS method, an O(h_x^2 + h_t) approximation of the diffusion equation. Regrouping the terms and noting, as before, λ = D h_t / h_x^2 one obtains for the propagated solution components u_i^{n+1} at the interior mesh points the linear system

```
-\lambda u_{i-1}^{n+1} + (1 + 2\lambda) u_i^{n+1} - \lambda u_{i+1}^{n+1} = u_i^{n}, \quad i = 2,3,\dots,N_x - 1. \tag{13.66}
```

This system is to be solved in conjunction with appropriate initial and boundary conditions. In particular, the Dirichlet conditions,

```
u_1^{n+1} = u_1^{n} = u_0^0, \quad u_{N_x}^{n+1} = u_{N_x}^{n} = u_L^0, \tag{13.67}
```

maintain the solution values constant on the boundaries.

Since, as opposed to the FTCS method, the components of the propagated solution cannot be expressed independently, but result at every time step by solving the linear system (13.66)–(13.67), the BTCS scheme is said to be an implicit method, and the characteristic information flow between the time steps t_n and t_{n+1} can be also learnt from Figure 13.7.

In matrix notation, the linear system of the BTCS method takes the form:

```
\mathbf{A} \cdot \mathbf{u}^{n+1} = \mathbf{u}^{n}, \quad n = 0,1,2,\dots, \tag{13.68}
```

whereby, the preceding solution u^n plays the role of constant vector and the system matrix is tridiagonal:

```
\mathbf{A} = \begin{bmatrix} 1 & 0 & & \\ -\lambda & 1 + 2\lambda & -\lambda & \\ & \ddots & \ddots & \ddots \\ & & -\lambda & 1 + 2\lambda & -\lambda \\ & & & 0 & 1 \end{bmatrix}. \tag{13.69}
```

Since λ > 0 by definition, matrix A is diagonally dominant and positive definite. Therefore, solving system (13.68)–(13.69) can be carried out most efficiently by means of the LU decomposition method developed in Section 7.7 and implemented as routine TriDiagSys in the libraries linsys.py and linsys.h.