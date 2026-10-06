
## 6.7 Simulation: Confidence Bounds and Control Variates

![](img/0790f102da4ffa7564329bf76c7d0815_244_0.png)

**Figure 6.6** Histogram of the mean in the M/M/1 queue.

- (iii) It is geometrically ergodic: The limit in (6.6) holds geometrically for all $x, S$.
- (iv) It is reversible: This means that reversing the direction of time does not change the statistics of $X$ in steady state. Equivalently, the balance equations hold:

```
$\pi(x)P(x,y) = \pi(y)P(y,x), \quad x,y \in X \equiv \{0,1,2,\dots\}.$
```

These desirable properties should have positive implications for simulation.
In fact, the M/M/1 queue and other skip-free Markov chains pose challenges, as illustrated here for the sample of estimating the steady-state mean $\eta = \pi(c)$ with $c(x) = x$. We don't need to simulate, since

```
$\eta = (1-\rho) \sum_{n=0}^{\infty} n\rho^n = \frac{\rho}{1-\rho}.$
```

The experiments will illustrate what can go wrong in the simplest examples when the state space is not finite.

### Challenges

- 1 The asymptotic variance is massive.
- 2 The CLT holds, but the empirical distribution appears finite-$n$.
- 3 There is no known sample complexity bound.

The ordinary variance is $\sigma^2 = \pi(\pi^2)-\eta^2 = \rho/(1-\rho)^2$. The asymptotic variance, as stated in math 1, **massive:**

```
$\sigma_{clt}^2 = \frac{1+o(1)}{(1-\rho)^2} = (8+o(1))\sigma^4,$
```

where $o(1) = O(1-\rho)$. This approximation holds for $\rho = 9/10$. The histogram results from $2 \times 10^4$ runs, with initial condition drawn independently from $\pi$. The asymptotic variance estimate $\sigma_{clt}^2 \approx 8(1-\rho)^{-4}$ results in the standard deviation approximation $\sigma_{clt} \approx 28$ indicated by the figure.

Despite the skew observed in the histogram, the CLT remains a reliable predictor of algorithm performance in this example. In particular, we find that the time horizon is too long. Consider the approximation

```
$P[|\eta_n - \eta| > 2\sigma_{clt}/\sqrt{n}] \approx P[|W| > 2] \approx 0.045, \quad W \sim N(0,1).
```

With $n=10^5$, we have $2\sigma_{clt}/\sqrt{n} \approx 1.8\eta$. That is, in 5% of our experiments, the error is over 20%. If we increase the time horizon to $n=10^7$, the error reduces to 2% with the same frequency.

### Markov Chains

![](img/0790f102da4ffa7564329bf76c7d0815_245_0.png)

**Figure 6.7** Sample paths of the M/1 queue; two large excursions.

A finite-$n$ bound of the form (6.43) is not available, but we can establish the (highly asymmetric) one-sided asymptotic bounds: For functions $I_-, I_+ : \mathbb{R}_+ \to \mathbb{R}_+$, and all $\varepsilon > 0$,

```
$$\lim_{n\to\infty} \log P{\{\eta_n - \eta \le -\varepsilon\} = -L_-(\varepsilon) < 0, \quad (6.44a)$$
```

```
$$\lim_{n\to\infty} \log P{\{\eta_n - \eta \ge n\varepsilon\} = -I_+(\varepsilon) < 0. \quad (6.44b)$$
```

The first limit is exact for a finite state space Markov chain. The probability in the second limit (6.44b) is not a typo: It is possible that the error exceeds **n times** $\varepsilon$. See the "Notes" section for history and resources.

It's difficult to explain the source of asymmetry: If $\eta_n$ is nonnegative for all $n_0$, so that $P{\eta_n - \eta \le -n\varepsilon} = 0$ for all large $n$: with (6.44a). To understand the upper tail (6.44b), write $\eta_n = n^{-1}S_n$ with $S_n = \sum_{k=0}^n X(k)$, so that

```
$P{\eta_n - \eta \ge n\varepsilon} = P{\eta_n \ge n + n^2\varepsilon}$.
```

Examples of excursions of the queue length are illustrated in Figure 6.7. In each of the two paths shown, the maximum height of $X$ is roughly proportional to the length of the time duration. The partial sum $S_n$ may be regarded as the area under the trajectory formed by $\{X(k) : 0 \le k \le n-1\}$, which is of order $n^2$ over much of the run in these two plots. This is consistent with (6.44b). The performance criterion (6.43) is focused exclusively on rare events, that we know $P{\{\eta_n - \eta| \ge \varepsilon}$ will go to zero quickly. The asymptotic variance is guaranteed, which helps to explain why the CLT holds under very general conditions.

### 6.7.5 Combating Variance

Here are a few techniques to cope with high variance:

#### Common Random Numbers

Suppose we have a family of Markov chains indexed by a parameter $\theta \in \mathbb{R}^d$,

```
$X(k+1) = F(X(k), N(k); \theta). \quad (6.45)$
```

The goal is to estimate $\eta$ for a function $c: X \to \mathbb{R}$. Using (6.37) to estimate $\eta$ for different values of $\theta$, be sure to reuse the sample path $\{N(k): 1 \le k \le n\}$ for each $\theta$. Consider, for example, a linear system:

```
$X(k+1) = (1-\theta)X(k) + N(k+1),$
```

with an i.i.d. sequence $c(x)$, and our interest is minimizing over $\theta \in \mathbb{R}$ the objective function $\Gamma(\theta) = (\theta^2 + 1)$. This is easily computed for this simple example:

```
$\Gamma(\theta) = \frac{(\theta^2+1)}{(1-\theta)^2}\eta^2.$
```

The upper plots in Figure 6.8 compare estimates obtained with common random numbers and those with independent random numbers (meaning that the samples of disturbance $N(k)$ are chosen independently for each value of $\theta$). The plot obtained using common random numbers is smooth as a function of $\theta$. Independent trials were performed, where in each of 500 experiments the minimizer was computed for each approach. The histograms shown in Figure 6.8 confirm that the estimate of $\theta^* \approx 0.6$ is far more reliable using common random numbers.

#### Splitting Sampling

Consider estimation of $E[L(X(k), X(k+1))]$ where $X$ is a finite state Markov chain with unique invariant measure $\pi$. The standard estimator is

```
$$\hat{L}_N = \frac{1}{N}\sum_{k=0}^{N-1} L(X(k),X(k+1)).$$
```

If the second eigenvalue of the transition matrix $P$ is close to unity, then the mixing time of the Markov chain $X$ will be slow, and this will adversely affect the convergence rate. In this case, the following variant, known as splitting sampling, can be used. $X^1$ denotes an i.i.d. sequence with marginal $\pi$. For each $k=1,2,\dots$, the random variable $X^2(k)$ is chosen in two stages. First, the value $x=X^1(k-1)$ is observed. Then the value of $X^2(k)$ is chosen according to the distribution $P(x,\cdot)$, independent of $\{X^1(j),X^2(j) : j \le k-1\}$. Based on this part of stochastic process, the estimate at iteration $N$ is defined

```
$$\hat{L}_N = \frac{1}{N} \sum_{k=0}^{N-1} L(X^1(k), X^2(k+1)). \quad (6.47)$$
```

Consider Exercise 6.15 for instructions on how to obtain an expression for the asymptotic variance of this estimate, and compare it to the standard estimator. You can expect significant variance reduction when $\sigma_{LR}^2 \gg \sigma^2$.

#### Control Variates

Suppose that there is a d-dimensional stochastic process $\{c(k)\}$, that is correlated with the sequence $\{c(X(k))\}$, and for which we know the steady-state mean is zero. That is, the following limit hold with probability one, for each $1 \le i \le d$:

```
$$\lim_{n\to\infty} \frac{1}{n} \sum_{k=0}^{n-1} \Delta_i(k) = 0.$$
```

For each $v \in \mathbb{R}^d$, define $\Delta_v(k) = \sum v_i \Delta_i(k)$, and define new sequences of:

```
$$\eta_n = \frac{1}{n} \sum_{k=0}^{n-1} [c(X(k)) + \Delta_v(k)]. \quad (6.48)$$
```

Significant variance reduction is possible in some cases -- see the "Notes" section for examples and resources.

#### State Weighting and Likelihood Ratios

Consider the mean-square error (6.22) defined with respect to the invariant probability measure $\pi$. Algorithms to minimize this loss may suffer from very high variance. One way to reduce variance is to introduce a weighting function $w: \mathbf{X} \to \mathbb{R}_+$ (it might also be interpreted as an unnormalized likelihood ratio). The weighted mean-square error is denoted

```
\|\hat{h} - h||_{\omega}^2 = \mathbb{E}[|\hat{h}(X(k)) - h(X(k))|^2 w(X(k))] \quad \text{when } X(k) \sim \pi. \quad (6.49)$$
```

For example, in the M/M/1 example where $\pi$ is geometric, and $h$ is a quadratic function of $x$, we choose $w(x) = 1/(1+x^4)$, so that the product within the expectation is bounded.

## 6.8 Sensitivity and Actor-Only Methods

Let's turn to a control problem. Rather than the feedback formulations developed in Part I, we are presented with a parameterized family $\{P_{\theta}, \pi_{\theta}, c_{\theta}, \eta_{\theta} : \theta \in \mathbb{R}^d\}$, subject to the following assumptions:

Assumptions for a Markov Family There is a common state space $X$, and for each $\theta$:

- $\pi_{\theta}$ is invariant for $P_{\theta}$.
- $c_{\theta}: X \to \mathbb{R}$, and $\eta_{\theta} = \pi_{\theta}(c_{\theta})$.
