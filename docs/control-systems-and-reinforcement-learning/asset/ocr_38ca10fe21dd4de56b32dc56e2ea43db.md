# 8.2 Themes and Roadmaps

# 8.2.3 Choice of Step-Size

The next question is how to choose the step-size appearing in (8.2). A constant step-size is often preferred in applications, although choice of the constant value remains an art form. Also, with a constant step-size we cannot expect convergence, unless the covariance matrix defined in (8.27) is identically zero. This degenerate case is not found in the applications of interest in this book, so we assume a vanishing step-size: $\lim_{n\to\infty} \alpha_n = 0$. Two further assumptions are imposed; the discrete-time version of Assumption (QSA1) of Section 4.5.4:

```
$\sum_{n=1}^{\infty} \alpha_n = \infty.$
```

This is imposed so that it is possible to reach $\theta^*$ from each initial $	heta_0$. The second assumption is more strongly rooted in probability theory:

```
$\sum_{n=1}^{\infty} \alpha_n^2 < \infty.$ (8.21)
```

In particular, it is used to establish (8.18), which is required for convergence of parameter estimates in Theorem 8.1. The proposition that follows makes clear why we require (8.21). The uniform bound on the second moment of $\{\Delta_k\}$ is relaxed in Proposition 8.7 (see (8.60b)).

**Proposition 8.2** Suppose that $\{\Delta_k\}$ is an uncorrelated sequence with bounded covariance: $\sigma_{\Delta}^2 = \sup_k E[|\Delta_k||^2] < \infty$. Then the second moment of $\{M_K^{(n)} : K \ge 1\}$ appearing in (8.16) admits the uniform bound

```
$E[|M_K^{(n)}||^2] \le \sigma_{\Delta}^2 \sum_{j=n+1}^{K} \alpha_j^2.$
```

The right-hand side vanishes as $n\to\infty$, provided (8.21) holds.

Proof If{\Delta_k\}$ is an uncorrelated sequence, then the covariance of $M_K^{(n)}$ satisfies

```
$E[M_K^{(n)}\top M_K^{(n)}] = \sum_{i=1}^{K} \alpha_i^2 + E[\Delta_n + \alpha_i\Delta_n^top]$
```

and consequently

```
$E[|M_K^{(n)}||^2] = \text{trace} E[M_K^{(n)} M_K^{(n)}\top] \le \sigma_{\Delta}^2 \sum_{j=n+1}^{K} \alpha_j^2.$
```

# 8.2.4 Multiple Time Scales

There are many examples in which it is valuable to use different step-sizes for different parameter estimates. Consider the averaging technique (8.10). This is usually presented as a time-scale recursion where with $N_0=0$,

```
$\theta_{n+1}^{pr} = \theta_n^{pr} + \alpha_n[\theta_n^{\theta} - \theta_n^{pr}], \quad n \ge 0$
```