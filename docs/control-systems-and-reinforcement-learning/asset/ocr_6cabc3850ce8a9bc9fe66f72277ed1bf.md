# 9.6 Watkins's Q-Learning

# TD(\lambda) Algorithm (On-Policy for Advantage)

For initialization $\omega_0 \in \mathbb{R}^m$, the sequence of estimates are defined recursively:

```
$$\omega_{n+1} = \omega_n + \alpha_n \zeta_n \mathcal{D}_{n+1},$
$\mathcal{D}_{n+1} = (-H^w(\Phi(n)) + c_n + yH^w(\Phi(n+1)))|w=\omega_n,$$
$\zeta_{n+1} = \lambda\zeta_n + \hat{\psi}(\Phi(n)), \quad H^w(\Phi(n)) = \omega^T\hat{\psi}(\Phi(n)).$$ (9.68)
```

Is it a problem if $d=10^4$ and $m=7$ just? Complexity is reduced, and for $\lambda=1$ the optimal estimate $\omega^* \in \mathbb{R}^m$ defines the optimal $L_2$ approximation of $V$. See Section 10.2 for details. The only remaining challenge be computation of $\psi$. See the discussion surrounding (9.54) for a solution using split sampling.

In the following sections, we exit the fixed-policy setting, returning to (9.1).

# 9.6 Watkins's Q-Learning

# 9.6.1 Optimal Control Essentials

Two values of interest are there to have:

```
$h^*(x) = \min_{U(0),U(1),...} \sum_{k=0}^{\infty} \gamma^k E[c(\Phi(k)) | X(0)=x],$\nQ^*(x,u) = \min_{U(0),U(1),...} \sum_{k=0}^{\infty} \gamma^k E[c(\Phi(k)) | X(0)=x, U(0)=u].$ (9.69)
```

Where $\Phi(k)=(X(k),U(k))$, and in the optimal control setting we denote $Q^*(x)$ as $\min_u Q^*(x,u)$, with the convergence (9.5c). Given one value, we have the other: for each $x$ and $u$,

```
$h^*(x) = Q^*(x) \quad and \quad Q^*(x,u) = c(x,u) + \gamma P_u(x',x)h^*(x').$ (9.70)
```

The advantage is defined as the difference $V^* = Q^* - h^*$, which is a function on $X \times U$ taking non-negative values; $V^*(x)=0$ for each $x$.\nQ-learning algorithms are often based on a Gakelman relaxation that mirrors TD(\lambda$): Given a parameterized function $H(\theta: \theta \in \mathbb{R}^d)$, and a sequence of $d$-dimensional elements $\{\zeta_n\}$, we get to find a solution $\theta^*$ to

```
$f(\theta^*) = E[{-H^\theta(\Phi(n)) + c_n + \gamma H^\theta(X(n+1))\zeta_n]_{	heta=\theta^*}.$ (9.71)
```

The ODE method (8.4) leads quickly to an algorithm:

+   (1) Formulate the goal $f$ as a root-finding problem $f(\theta^*)=0$, with $f$ defined in (9.71).\n(2) Refine the design of $f$ to ensure the associated ODE is globally asymptotically stable
(3) Is an Euler approximation appropriate? Is $f$ Lipschitz continuous?