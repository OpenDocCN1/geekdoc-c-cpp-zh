# Value Function Approximations

188 While this is required for convergence theory, any of the algorithms to come can be applied using a nonlinear function approximation architecture.

An approximation of the inequality in (5.63) is given by $\Gamma^\zeta(\theta) \leq 0$, where

```
$$\Gamma^\zeta(\theta) \overset{\text{lim}}{N\to\infty} \frac{1}{N} \sum_{k=0}^{N-1} [D_{k+1}(\theta)]_-, (5.66a)$
```

```
$$\tilde{D}_{k+1}(	heta) = -Q^	heta(x,u(k)) + c_k + Q^	heta(x(k+1)), \quad (5.66b)$
```

and $[z]_- = \max(0, -z)$ for any $z \in \mathbb{R}$, and $c_k = c(x,u(k))$. Subject to (5.64), the function $\Gamma^\zeta$ is convex, so that $\{\theta : \Gamma^\zeta(\theta) \leq 0\}$ is a convex subset of $\\mathbb{R}^D$.

This motivates the first algorithm:

# Convex Q-Learning

Choose a $\mu$ on $X \times U$, a convex regularizer $\mathcal{R}_N(\theta)$, tolerance $Tol \geq 0$, and solve

```
$$\theta^* = \arg\min_{\theta} \langle\mu, Q^	heta\rangle + \mathcal{R}_N(\theta) (5.66a)$
```

```
$s.t. \Gamma_N^zeta(\theta) \overset{\text{def}}{=}} \frac{1}{N} \sum_{k=0}^{N-1} [D_{k+1}(\theta)]_- \leq Tol. (5.66b)$
```

The choice of regularizer might be biased on computational efficiency. The introduction of the tolerance "Tol" is in anticipation of computational challenges to be discussed shortly.

The next algorithm is inspired by the architecture of DQN: Choose intermediate times $T_0 = 0 < T_1 < T_2 < ... < T_{B-1} < T_B = N$, and a sequence of regularizers: $\mathcal{R}_n(Q, \theta)$ is a convex functional of $Q, \theta$, which may depend on $\theta_n$. Examples follow.

# Batch Q-Learning #1

With $\theta_0 \in \mathbb{R}^d$ given, defined recursively

```
$$\theta_{n+1} = \arg\min_{\theta} \{-\langle\mu, Q^	heta\rangle + \mathcal{R}_n(Q^	heta)\} (5.67a)$
```

```
$s.t. \Gamma_n^zeta(\theta) \leq Tol. (5.67b)$
```

where $0 \leq n \leq B - 1$, with $r_n = T_{n+1}-T_n$,

```
$$\Gamma_n^zeta(\theta) = \frac{1}{r_n} \sum_{k=T_n}^{T_{n+1}-1} [D_{k+1}(\theta)]_-. (5.67c)$
```

It is expected that $\mathcal{R}_n$ is designed to avoid discarding previous data, as

```
$$\mathcal{R}_n^0(Q, \theta) = \mathcal{R}_n^0(\theta) + \frac{1}{2\beta_n+1} ||\theta - \theta_n||^2, (5.68)$
```

in which $\mathcal{R}_n^0$ is convex and $\{\beta_n\}$ are positive scalars.