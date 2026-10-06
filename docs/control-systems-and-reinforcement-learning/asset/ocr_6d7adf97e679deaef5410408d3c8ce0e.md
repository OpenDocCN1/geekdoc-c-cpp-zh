# 10.4 Average Cost and Every Other Criterion

# Regenerative TD($\lambda$) Algorithm for Average Cost (On-Policy)

For initialization $\theta_0, \zeta_0 \in \mathbb{R}^d$, the sequence of estimates is defined recursively:

```
$$\theta_{n+1} = \theta_n + \alpha_n\zeta_n, \mathcal{D}_{n+1}.$\n$\mathcal{D}_{n+1} = (-H^{\theta}(\Phi(n)) - \delta\langle\mu, H^{\theta}\rangle + c_n + H^{\theta}(\Phi(n+1)))|_{	heta=\theta_n},$\n$\zeta_{n+1} = \lambda\mathbb{1}[\Phi(n+1) \neq z^*]\zeta_n + \psi(n+1).\$$
```

We have $\theta_{n+1} = \theta_n + \alpha_n[\mathcal{A}_{n+1} - b_n - b_1]$ with

```
$$\mathcal{A}_{n+1} = \zeta_n[-\psi_n - \delta\psi^{\mu} + \psi(n+1)]^T, \quad b_{n+1} = -\zeta_nc_n.,$$
```

where $\psi^\mu = (\mu, \psi_i)$ for each $i$. We have the following companion to Theorem 10.14:

**Theorem 10.15 (Optimality of TD(1) for Average Cost)** *Consider the algorithm (10.32) with linear function approximation $H^	heta = \theta^T\psi$. Assume that $\Phi$ is uni-chain, that $\varrho(z^*) > 0$, and for some parameter $z^* \in \mathbb{R}^d$.*

```
$$\sum \theta_i\psi_i(z) = \mathbb{1}[z = z^*], \quad z \in X \times U.\$$$
```

Then, in the case $\lambda = 1$, for any solution to $\tilde{f}(\theta) =0$,

+   (i) $\delta = \delta\langle\mu, H^{	heta}\rangle$,

+   (ii) The “projected Poisson’s equation” has: $Y = \psi(\Phi(n)),$

```
$$\H^{\theta}(\Phi(n)) = \mathbb{E}[H^{\theta}(\Phi(n)) + H^{\theta}(\Phi(n+1)) | Y].\$$
```

+   (iii) Suppose in addition that 1 is in the span of the Basis: For some $\theta^1 \in \mathbb{R}^d$,

```
$$\sum \theta_i^1\psi_i(z)=1, \quad z \in X \times U.\$$$
```

Then, $H^{	heta}(\Phi(n)) = \mathbb{E}[H_3(\Phi(n)) + H^*(z^*) | Y]$, and the minimum norm problem is solved in the following span semiminorm: with $r^* = H^*(z^*)$.

```
$$\(\theta^*, r^*) = \arg\min \mathbb{E}_{\omega}[(H^{\theta}(\Phi(n)) - r - H_3(\Phi(n)))^2].\$$
```

Unfortunately we lose the elegant expression $A = R(\theta)$ for this algorithm. A glance at the proof reveals that,

```
$$\A = \mathbb{E}[\zeta_n[-\psi_n - \delta\psi^{\mu} + \psi(n+1)]^T].$\n$-=\delta\mathbb{E}_{\omega}[{\zeta_n\psi^{\mu}\}^T + \mathbb{E}_{\omega}[\psi(n)\{-\psi(n) + \psi(z)\}^T].\$$
```

It can be shown that $A$ is invertible for sufficiently small $\delta > 0$ provided $\psi^*R(0)^{-1}\psi^*(z) < 1$. Moreover,

```
$$\hat{\psi}^T R(0)^{-1}\psi(z) < \sqrt{\psi(z)^T R(0)^{-1}\psi(z)}.\$$$
```

which might lead to choices for basis selection to ensure the right-hand side is no greater than one. One approach to ensure $A$ is Hurwitz is not yet available, so this approach