# 3.9 Examples

a stochastic model in which average arrival and service rates match those of the fluid model; details can be found in Section 7.6. Solidarity of the two models is clear in this simulation.

# 3.9.4 Solving the HJB Equation

These examples illustrate optimal control solutions for models in continuous time.

Example 3.9.1 (LQR) The formulation of the linear quadratic regulator problem is as expected:

```
$$\frac{d}{dt}x = Fx + Gu, \quad x(0) = x_0,\$\nc(x,u) = x^T S x + u^T Ru, \quad (3.60)$
```

where $S$ is a positive semidefinite matrix, and $R > 0$. Provided the value function $J^*$ is finite valued, it follows that it is a quadratic function of $x$, and an optimal policy is obtained via linear state feedback. The proof of these statements is exactly the same as in Section 3.6. In particular, we know that $J^*(x) = x^T M^*$ for $x$, then the HJB equation gives

```
$$\phi^*(x) = \argmin_u \{x^T S x + u^T Ru + [2M^*]^T[Fx + Gu]\}, \$\quad = \argmin_u \{u^T Ru + 2x^T M^*\},$
```

where in this second equation we is obtained by imposing symmetry of $M^*$, $[M^*]^T = x^T M^*$. The minimum of this quadratic function of $u$ is obtained by solving the linear equation:

```
$$\nabla_u(u^T Ru + 2x^T M^* Gu)|_{u=\phi^*(x)} = 0,$
```

which gives $\phi^*(x) = -R^{-1}G^T M^*x$.

The closed-loop dynamics are given by

```
$$\frac{d}{dt}x^* = |F - GR^{-1}G^T M^*|,$
```

The HJB equation (3.50) is also obtained from (3.50):

```
$$\frac{d}{dt}J^*(x^*) = -c_{\phi^*}(x^*), \$\nc_{\phi^*}(x) = c(x, \phi^*(x)) = x^{*T}\{S + M^*GR^{-1}G^TM^*\}x, \quad x \in X.$
```

A fixed point for $M^*$ is also obtained from (3.50):

```
$$\0 = x^{*T}\{Sx + u^T Ru + [2M^*]^T[Fx + Gu]\}_{u=\phi^*(x)} \$\quad = x^{*T}\{S + M^*GR^{-1}G^TM^*\}x + x^{*T}\{2M^*F - 2M^*GR^{-1}G^TM^*\}x,$
```

Substitute $2x^*TM^*F = x^{*T}[2M^*F - F^TM^*]$, and after canceling terms this results results in

```
$$\0 = x^{*T}\{S + M^*F + F^TM^* - M^*GR^{-1}G^TM^*\},$
```

Since this holds for any $x$, and since the matrix within the brackets is symmetric, it follows that $M^*$ is a positive semidefinite solution to the ARE:

```
$$\0 = S + M^*F + F^TM^* - M^*GR^{-1}G^TM^*., \quad (3,61)$
```