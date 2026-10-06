# Markov Chains

```
$$\hat{L}_N = \frac{1}{N} \sum_{k=0}^{N-1} L(X^1(k), X^2(k+1)). \quad (6.47)$
```

Consider Exercise 6.15 for instructions on how to obtain an expression for the asymptotic variance of this estimate, and compare it to the standard estimator. You can expect significant variance reduction when $\sigma_{LR}^2 \gg \sigma^2$.

# Control Variates

Suppose that there is a d-dimensional stochastic process $\{c(k)\}$, that is correlated with the sequence $\{c(X(k))\}$, and for which we know the steady-state mean is zero. That is, the following limit hold with probability one, for each $1 \le i \le d$:

```
$$\lim_{n\to\infty} \frac{1}{n} \sum_{k=0}^{n-1} \Delta_i(k) = 0.$
```

For each $v \in \mathbb{R}^d$, define $\Delta_v(k) = \sum v_i \Delta_i(k)$, and define new sequences of:

```
$$\eta_n = \frac{1}{n} \sum_{k=0}^{n-1} [c(X(k)) + \Delta_v(k)]. \quad (6.48)$
```

Significant variance reduction is possible in some cases -- see the "Notes" section for examples and resources.

# State Weighting and Likelihood Ratios

Consider the mean-square error (6.22) defined with respect to the invariant probability measure $\pi$. Algorithms to minimize this loss may suffer from very high variance. One way to reduce variance is to introduce a weighting function $w: \mathbf{X} \to \mathbb{R}_+$ (it might also be interpreted as an unnormalized likelihood ratio). The weighted mean-square error is denoted

```
$$\|\hat{h} - h||_{\omega}^2 = \mathbb{E}[|\hat{h}(X(k)) - h(X(k))|^2 w(X(k))] \quad \text{when } X(k) \sim \pi. \quad (6.49)$
```

For example, in the M/M/1 example where $\pi$ is geometric, and $h$ is a quadratic function of $x$, we choose $w(x) = 1/(1+x^4)$, so that the product within the expectation is bounded.

# 6.8 Sensitivity and Actor-Only Methods

Let's turn to a control problem. Rather than the feedback formulations developed in Part I, we are presented with a parameterized family $\{P_{\theta}, \pi_{\theta}, c_{\theta}, \eta_{\theta} : \theta \in \mathbb{R}^d\}$, subject to the following assumptions:

Assumptions for a Markov Family There is a common state space $X$, and for each $\theta$:

+   - $\pi_{\theta}$ is invariant for $P_{\theta}$.
- $c_{\theta}: X \to \mathbb{R}$, and $\eta_{\theta} = \pi_{	heta}(c_{\theta})$.