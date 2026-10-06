# 5.6 Q-Learning in Continuous Time

# Kernel Batch Convex Q-Learning

With $	heta_0 \in \mathbb{R}^d$ and $\lambda_0 \ge 0$, define recursively

```
$Q^{n+1} = \arg\min_{Q \in \mathcal{H}} \{-\{\mu(Q) + \lambda_n \Gamma_n^n(Q) - Tol\{\}, \quad (5.71a)$
```

```
$\lambda_{n+1} = |\lambda_n + \beta_n(\Gamma_n^n(Q_{n+1}) - Tol)\|_+, \quad (5.71b)$
```

A candidate regularizer to match (5.68) is the quadratic

```
$R_n(Q) = \frac{1}{\alpha_{n+1}} ||Q - Q^n||_{\mathcal{H}}^2$
```

However, this choice presents a challenge: To apply the Representer Theorem, we must make a change of variables $h = Q - Q^n$, and our BCQL algorithm will prefer the optimizer $h^{n+1} \in \mathcal{H}$. The Representer Theorem tells us that the function $h^{n+1}(\cdot,\cdot)$ is a linear combination of the functions $\{\mathbf{k}[(x(k),u(k)),(\cdot, \cdot))\}$, where $k$ ranges over the $n$th batch (size $r_n$). The Q-function approximation is the sum $Q^{n+1} = Q^n + h^{n+1}$, and so by induction.

```
$Q^{n+1} = Q^n + h^1 + \dots + h^{n+1}$.
```

This estimate is too complex: A regularizer that avoids this complexity is defined by the sum of two quadratics:

```
$R_n(Q) = \frac{1}{\alpha_{n+1}} ||Q - Q^n||_{\mathcal{H}}^2 + \delta ||Q^n||_{\mathcal{H}}^2, \quad (5.72)$
```

where $Q^n \in \mathcal{H}$ is the estimate at stage $n$, and

```
$||Q - Q^n||_{r_n}^2 = \frac{1}{r_n} \sum_{k=T_n}^{T_{n+1}} (Q(x(k),u(k)) - Q^n(x(k),u(k)))^2$.
```

With this regularizer, the Representer Theorem tells us that for each $n$, the optimizer takes the following form: For some $\theta^* \in \mathbb{R}^{r_n}$

```
$Q^n(x,u) = \sum_{i=1}^{r_n} \theta_n^i \mathbf{k}(z_i, z), \quad z = (x,u)$.
```

where $z_i = (x_i, u_i)$ are the state-input pairs observed over the time interval $\{T_{n-1} \le k < T_n\}$.

Recall from Section 3.8 the HJB equation $\min_u \{c(x,u) + \nabla J(x) \cdot f(x,u)\}$. The term in brackets could lead to a useful definition of the Q-function. Instead, we fix a $\sigma > 0$ and denote

```
$H^*(x,u) \coloneqq \{c(x,u) + \nabla J^*(x) \cdot f(x,u)\} + \sigma J^*(x)$.
```