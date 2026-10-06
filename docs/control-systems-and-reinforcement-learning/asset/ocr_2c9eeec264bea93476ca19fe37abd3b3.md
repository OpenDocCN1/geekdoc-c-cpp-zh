# 5.4 Projected Bellman Equations and TD Algorithms

# TD(λ) Learning

For a given $\lambda \in [0,1]$, nonnegative step-size sequence $\{\alpha_n\}$, initial conditions $	heta_0, \zeta_0$, and observed samples $\{u(k),x(k) : 0 \leq k \leq N\}$, the sequence of estimates is defined by the coupled equations:

```
$$\theta_{n+1} = \theta_n + \alpha_n\mathcal{D}_n\zeta_n$,$
\mathcal{D}_{n+1}(Q) = -Q^{\theta_n}(\psi(n),u(n)) + c_n + Q^*(x(n+1)),$
\zeta_{n+1} = \zeta_n + \psi(n+1)).$$
```

This defines the approximation of the Q-function $Q^{	heta^N} = \sum_i \theta_N(i)\psi_i$.

For the purposes of analysis, we require an extension of the state process:

```
$$\Phi(k) = \langle x(k),u(k),\zeta(k)\rangle.$$
```

so that $f_{\lambda}(\theta)$ is a linear function of $\Phi(k)$.\nDenote $f_{\lambda}(\theta) = E_{\theta}[\zeta(k)\mathcal{D}_k+1(Q^{\theta})]$. TD($\lambda$) is an approximation of the ODE

```
$$\frac{d\theta}{dt} = f_{\lambda}(	heta).$$
```

The right-hand side is linear: $f_{\lambda}(\theta) = A(\theta-\theta^*)$, in which

```
$A = E_{\theta}[\zeta(k)]-\\psi(k)+\psi(x(k+1))\Phi(x(k+1))].$$
```

Convergence of TD($\lambda$) learning is not guaranteed in the policy-offset setting, with $\lambda=0$.\nA famous example is described after Figure 5.5.\nWhat about neural networks? If $\Phi$ is not a linear function class, then we lose much of the convergence theory, but the algorithm can be designed

# TD(λ) Learning (with Nonlinear Function Approximation)

For a given $\lambda \in [0,1]$, nonnegative step-size sequence $\{\alpha_n\}$, initial conditions $\theta_0, \zeta_0$, and observed samples $\{u(k),x(k) : 0 \leq k \leq N\}$, the sequence of estimates is defined by the coupled equations:

```
$$\theta_{n+1} = \theta_n + \alpha_n\mathcal{D}_n\zeta_n$,$\n\zeta_{n+1} = \lambda\zeta_n + c_n^0$,$\n\zeta_n = \nabla_{\theta}Q^*(x(n),u(n))|_{\theta=\theta_n}.$$
```

and $\mathcal{D}_{n+1}$ defined as in (5.48b).

![](bbox=[0.198, 0.833, 0.798, 0.883])

Figure 5.5 Baird's star problem.