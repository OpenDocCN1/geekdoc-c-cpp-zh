# 308 Stochastic Approximation

Conditions for boundedness follow the stability theory for QSA based on a Lyapunov, or via the ODE$\infty$ called here:

```
$\frac{d	heta_t}{dt} = f_{\infty}(	heta_t), \quad (8.62)$
```

with $f_{\infty}$ defined in (4.138): $f_{\infty}(\theta) = \coloneq}{=} \lim_{r\to\infty} r^{-1}f(r\theta)$ for any $	heta \in \mathbb{R}^d$.

The first row of Figure 8.5 might be viewed as illustration of approximation of SA by the solution to the ODE $\frac{d\theta_t}{dt} = f(\theta_t)$, with $\theta_0=100$.

The Lyapunov criterion is (QSV1): For a differentiable Lyapunov function, this is Equivalently expressed

```
$V'(\theta_t) \le -||\theta_t||, \quad \quad \quad \quad \text{whenever} \||\theta_t|| > c_0.$
```

**Theorem 8.9** *Suppose that (SA1)-(SA3) hold, with one of the following conditions:*

+   (i) (QSV1) holds with V Lipschitz continuous.

+   (ii) The origin is asymptotically stable for the ODE$\infty$.

The SA recursion is ultimately bounded in the following sense: There exists $\sigma_0 < \infty$ such that for any initial condition,

```
$$\limsup_{n\to\infty} \|\theta_n|| \le \sigma_0 \quad \text{a.s.} \quad \quad \quad \limsup_{n\to\infty} E[\|\theta_n||^2] \le \sigma_0^2., \quad (8.63)$
```

The proof of the sure bound in (8.63) is identical to the proofs obtained for QSA. The mean-square error bound requires more work.

# 8.7.2 Linearization and Convergence Rates

Section 8.7.3 contains a complete analysis of the asymptotic covariance when using PJR averaging, begins with the following approximation:

```
$f_{n+1}(\theta_n) = A(\theta_n - \theta^*) + \Delta_{n+1} + \mathcal{E}_f(\theta_n), \quad (8.64)$
```

where

```
$$\mathcal{E}_f(\theta) = f(\theta) - A(\theta - \theta^*) \quad \text{error in a first - order Taylor series approximation for } \text{f}. \quad \quad (8.65)$
```

The difficult work involves mean-square bounds on the two terms $[\Delta_{n+1} - \Delta_{n+1}^infty]$ and $\mathcal{E}_f(\theta_n)$.

To expose the most interesting concerns, we consider a special model of the linear SA recursion (8.53a) for which $\mathcal{E}_f$ is eliminated. Under the simplest setting:

```
$f_{n+1}(\theta_n) = A\theta_n + \Delta_{n+1}, \quad (8.66)$
```

with $A$ Hurwitz, and $\bar{	heta}_n = \theta_n - \theta^*$. For analysis, it is convenient to express the linear recursion in terms of the error:

```
$$\bar{	heta}_{n+1} = \bar{	heta}_n + \alpha_n\{A\bar{	heta}_n + \Delta_{n+1}\}. \quad (8.67)$
```