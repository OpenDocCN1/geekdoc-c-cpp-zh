# 414 Partial Observations and Belief States

We obtain $eta_n$ through normalization, since we know it is a pmf:

```
$$\beta_n(x_0^n) = \kappa_n \beta_n^*(x_0^n), \quad \kappa_n^{-1} = \sum_{x_0, \dots, x_n} \beta_n^*(x_0, \dots, x_n').$$
```

What about the original problem? We again have Bayes's rule:

```
$b_n(x_n) = P\{X_n = x_n | Y_n^0 = y_n^0, U_{n-1}^{-1} = u_{n-1}^{-1}$$\n$\frac{P\{X_n = x_n, Y_n^0 = y_n^0, U_{n-1}^{-1} = u_{n-1}^{-1}\}}{b_n^*(u_n^1)}.$
```

The numerator, denoted $b_n^*(x_n)$, is obtained from $eta_n^*$ as follows:

```
$$\b_n^*(x_n) = P\{X_n = x_n | Y_n^0 = y_n^0, U_{n-1}^{-1} = u_{n-1}^{-1}\.$
```

Applying (C.13) gives a recursive formula for the unnormalized belief state:

```
$$\beta_n^*(x_n) = \sum_{x_0, \dots, x_{n-1}} \rho_n(x_n | x_{n-1}^{-1}) \beta_{n-1}^*(x_0', \dots, x_{n-1}')$\n$\sum_{x_{n-1}} \rho_n(x_n | x_{n-1}^{-1}) \left[ \sum_{x_0, \dots, x_{n-2}} \beta_{n-1}^*(x_0', \dots, x_{n-1}') \right]..$
```

From this, we obtain the linear dynamics:

```
$$\b_n^*(x') = \sum_{x} \rho_n(x' | x) b_{n-1}^*(x), \quad n \geq 1, x' \in \mathbf{X}..$
```

From Proposition C.3, we obtain the transition matrix for the belief state process given in Proposition C.1.

# Proposition C.3 (Nonlinear Filter) The belief state dynamics are nonlinear:

```
$$\b_n(x') = \kappa_0 \mu(x')q(Y_0 | x')..$
```

```
$$\b_n(x') = M(b_{n-1}, Y_n, U_{n-1}^{-1}) = \kappa_n \sum_{x} \rho_n(x' | x) b_{n-1}(x), \quad x' \in \mathbf{X}, n \geq 1,.$
```

where $ho_n$ is defined in (C.12), and $\kappa_n$ is determined by the constraint $\sum_{x} b_n(x) = 1.$