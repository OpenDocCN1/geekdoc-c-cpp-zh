
# 306

# Stochastic Approximation

![](img/0790f102da4ffa7564329bf76c7d0815_323_0.png)

Figure 8.9 Histograms of the first three parameter estimates. For the Zap SA routine, the estimates are Gaussian with distribution $N(0,\Sigma(i,t))$ for each $t=1, 2, 3$.

## 8.6.2 Curve of Markovian Memory

The preceding example is special because the "noise" is i.i.d. rather than the Markovian noise that is typical in RL. To illustrate how noise can present challenges, we consider once more a linear algorithm, but with "multiplicative noise":

```
$$\theta_{n+1} = \theta_n + \alpha_n[A_n + \Delta_n\theta_n], \quad \theta_0 \in \mathbb{R},$$
```

in which $A_{n+1} = X(n+1) - \eta$, where $X$ is a sample of the M/M/1 queue (transition matrix given in (6.14)) and $\Delta$ is i.i.d. $N(0,1)$ and independent of $X$. Recall from Section 6.7.4 that the Markov chain $X$ has many desirable properties, provided $\mu > \alpha$ (the load condition for the single server queue). In particular, it is reversible and ergodic, with geometric invariant $\pi$ and $\eta = E_\pi[X(n)] = \alpha/(\mu - \alpha)$.

The ODE approximation for (8.59) linear vector field $f(\theta) = -\theta$, so we expect convergence to zero, where we might attempt to obtain a CLT and moment bounds through the following representation:

```
$$\theta_{n+1} = \theta_n + \alpha_n[1 - \Delta_n\theta_n], \quad \theta_0 \in \mathbb{R},$$
```

where $\Delta_{n+1} = \Delta_{n+1}(X(n+1) - \eta)\theta_n$. Since $\theta_n$ converges to zero, this suggests we might attempt to treat this as a linear version of the Saul algorithm ($A=-1$), for which the CLT holds with asymptotic variance of.

However, the difficulties in Section 6.7.4 estimation of the steady-state mean have a flaw. If the load satisfies $\rho = \alpha/\mu \geq 1/2$, $E[\theta_n^2] \to \infty$ as $n \to \infty$ using $\alpha_n = 1/n$, which corresponds to Zap SA for this simple example (see the "Notes" for references). It is likely the second moment is also unbounded for estimates using PJR averaging.

Figure 8.10 shows positive news: Histograms of the normalized error $Z_n = \sqrt{n}\theta_n$ appear to be nearly $N(0,1)$ for high load. What is missing from these plots is outliers that were removed before plotting the histograms. For load $\alpha/\mu = 3/7$, out of the samples labeled were few and not large. For outliers for Zap, in this case the outliers were massive: Values exceeding $10^{20}$ were observed in about 1/5 of runs.

![](img/0790f102da4ffa7564329bf76c7d0815_324_0.png)

## 8.7 Some Theory*

This chapter is technical, then incomplete. The main challenge is space – theory of stochastic approximation takes a sizable book of its own, as pros will tell. The details of stability and convergence theory are skipped because these results follow the same steps in the theory of quasistochastic approximation from Section 4.5.

The purpose of this section is to highlight the parallels between QSA and SA theory, and point out some differences (especially for analysis of PJR averaging, which takes most of the space in this section).

To streamline discussion, we will impose some assumptions:

- (SA1) $\tilde{f}$ is Lipschitz continuous.
- (SA2) The sequence $\{\Delta_n : n \geq 1\}$ is a martingale difference sequence:

```
$E[\Delta_{n+1} | \mathcal{F}_n] = 0, \quad n \geq 0, \quad (8.60a)
```

```
with $\mathcal{F}_n = \sigma(\Phi(k) : k \leq n)$. Moreover, for some $\sigma_\alpha^2 < \infty,
E\|\Delta_{n+1} | \mathcal{F}_n\|^2 \leq \sigma_\alpha^2(1 + \|\theta_n\|^2), \quad n \geq 0. \quad (8.60b)
```

- (SA3) The sequence $\{\alpha_n : n \geq 1\}$ is deterministic, satisfies $0 < \alpha_n \leq 1$, and

```
$\sum_{n=1}^{\infty} \alpha_n = \infty, \quad \sum_{n=1}^{\infty} \alpha_n^2 < \infty. \quad (8.61)
```

The “Notes” section to find much stronger conclusions under weaker assumptions. Much of this theory is very recent.

In particular, Assumption (SA2) is imposed here for simplicity: It is not essential for the convergence theory for SA [39, 65, 66, 204]. This condition holds when $\Phi$ is i.i.d., and also for TD-learning and Q-learning in special cases (for example, Proposition 9.16).

### 8.7.1 Stability and Convergence

If you read Section 4.9, then you know that convergence of SA is not difficult to establish, once you have demonstrated that the estimates $\{\theta_n : n \geq 0\}$ are bounded.

# 308 Stochastic Approximation

Conditions for boundedness follow the stability theory for QSA based on a Lyapunov, or via the ODE$\infty$ called here:

```
$\frac{d\theta_t}{dt} = f_{\infty}(\theta_t), \quad (8.62)$
```

with $f_{\infty}$ defined in (4.138): $f_{\infty}(\theta) = \coloneq{=} \lim_{r\to\infty} r^{-1}f(r\theta)$ for any $\theta \in \mathbb{R}^d$.

The first row of Figure 8.5 might be viewed as illustration of approximation of SA by the solution to the ODE $\frac{d\theta_t}{dt} = f(\theta_t)$, with $\theta_0=0$.

The Lyapunov criterion is (QSV1): For a differentiable function, this is equivalently expressed

```
$V'(\theta_t) \le -\|\theta_t\|, \quad \text{whenever} \|\theta_t\| > c_0.
```

**Theorem 8.9** *Suppose that (SA1)-(SA3) hold, with one of the following conditions:*

- (i) (QSVI) holds with $V$ Lipschitz continuous.
- (ii) The origin is asymptotically stable for the ODE$\infty$.

The SA recursion is ultimately bounded in the following sense: There exists $\sigma_0 < \infty$ such that for any initial condition

```
$$\limsup_{n\to\infty} \|\theta_n\| \le \sigma_0 \quad \text{a.s.} \quad \limsup_{n\to\infty} E[\|\theta_n\|^2] \le \sigma_0^2. \quad (8.63)
```

The proof of the sure bound in (8.63) is identical to proofs obtained for QSA. The mean-square error bound requires more work.

## 8.7.2 Linearization and Convergence Rates

Section 8.7.3 contains a complete analysis of asymptotic covariance using PJR averaging, begins with the following approximation:

```
$f_{n+1}(\theta_n) = A(\theta_n - \theta^*) + \Delta_{n+1} + \mathcal{E}_f(\theta_n), \quad (8.64)$
```

where

```
$$\mathcal{E}_f(\theta) = f(\theta) - A(\theta - \theta^*) \quad \text{error in first-order Taylor series approximation for f}. \quad (8.65)
```

The work involves mean-square bounds on the two terms $\Delta_{n+1}$ and $\mathcal{E}_f(\theta_n)$. To expose the most interesting concerns, we consider a special model of linear SA recursion (8.53) for which $\mathcal{E}_f$ is eliminated. Under the simplest setting:

```
$f_{n+1}(\theta_n) = A\theta_n + \Delta_{n+1}, \quad (8.66)$
```

with $A$ Hurwitz, and $\bar{\theta}_n = \theta_n - \theta^*$. For analysis, it is convenient to express the linear recursion in terms of the error:

```
$$\bar{\theta}_{n+1} = \bar{\theta}_n + \alpha_n\{A\bar{\theta}_n + \Delta_{n+1}\}. \quad (8.67)
```

# 8.7 Some Theory

The scaled error is denoted

```
$Z_n \triangleq \frac{1}{\sqrt{\alpha_n}}\bar{\theta}_n, \quad \text{and,} \quad \Sigma_n \triangleq \mathbb{E}[Z_n Z_n^\top] = \frac{1}{\alpha_n}\mathbb{E}[\bar{\theta}_n\bar{\theta}_n^\top]. \quad (8.68)
```

**Proposition 8.10** Suppose that $\{\Delta_n\}$ satisfies (SA2), and that the covariance is independent of $n$. Then the following approximations hold:

- (i) With $\alpha_n = 1/(n+n_0)$,

```
$\Sigma_{n+1}^Z = \Sigma_n^Z + \frac{1}{n+n_0}\{(A + I + \mathcal{E}_n)\Sigma_n^Z + \Sigma_n^Z(A + I + \mathcal{E}_n)^\top + \Sigma_{\Delta}\}, \quad (8.69a)
```

with $\|\mathcal{E}_n\| = O(1/n)$. If in addition the matrix $A+\frac{1}{2}I$ is Hurwitz, then $\Sigma_n^Z$ converges to $\sigma_0$, and this limit is the solution to the Lyapunov equation (8.28a).

- (ii) With $\alpha_n = 1/(n+n_0)^\rho$, using $\frac{1}{2}<\rho < 1$,

```
$\Sigma_{n+1}^Z = \Sigma_n^Z + \frac{1}{n+n_0}\{(A + I)\Sigma_n^Z + \Sigma_n^Z(A + I)^\top + \Sigma_{\Delta}\}, \quad (8.69b)
```

with $\|\Delta_n\| = O(1/n)$. If in addition the matrix $A$ is Hurwitz, then $\Sigma_n^Z$ converges to $\sigma_0$, and this limit is the solution to the Lyapunov equation (8.28b).

Proof. In both parts, we simplify the calculations by setting $n_0 = 0$. This is justified if $\rho \in (\frac{1}{2},1]$ and $n_0 > 0$, we have the following for any $n \geq 1$:

```
$\frac{1}{(n+n_0)^\rho} = \frac{1}{n^\rho} + O(\frac{1}{n^{1+\rho}}).
```

- (i) The approximation (8.69a) begins with the Taylor series approximation

```
$\sqrt{n+1} = \sqrt{n} + \frac{1}{2\sqrt{n}} + O(\frac{1}{n^{3/2}}).
```

Multiplying both sides of the recursion (8.67) results in a result for $Z$:

```
$Z_{n+1} = Z_n + \frac{1}{n+1}\{(A + I + \mathcal{\varepsilon}_n)Z_n + \sqrt{n}\Delta_{n+1}\}, \quad (8.70)
```

with $\varepsilon_n = O(n^{-1})$. Taking products on both sides of the recursion, and then taking expectations, we obtain the recursion of (8.69a) after simplifications. It is in this step that we use the fact that $\Delta$ is a martingale difference sequence, in particular,

```
$\mathbb{E}[Z_n\Delta_{n+1}^\top] = \mathbb{E}[\Delta_{n+1}Z_n^\top] = 0.
```
