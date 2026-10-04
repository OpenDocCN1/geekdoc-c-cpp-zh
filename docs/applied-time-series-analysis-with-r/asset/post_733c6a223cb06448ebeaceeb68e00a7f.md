
# Stationary Time Series

# 11

![](img/41dcbfb9af56fa48895afde322197b0b_27_0.png)

![](img/41dcbfb9af56fa48895afde322197b0b_27_1.png)

**FIGURE 1.4**
True autocorrelations from models associated with realizations in Figure 1.3. (a) Realization 1. (b) Realization 2. (c) Realization 3. (d) Realization 4.

Also note that due to the fact that there is only a pseudo-cyclic behavior in the realization, with some cycles a little longer than others, lag 28 (i.e., two cycles), the autocorrelations are quite small.

Finally, relation 4 in Figure 1.3d shows a highly oscillatory behavior. In fact, if $x_i$ is above average, then $x_{i+1}$ tends to be below average, $x_{i+2}$ tends to be above average, etc. Again, the autocorrelations in Figure 1.4 describe this behavior where we see that $\rho_1 = -0.8$ while $\rho_2 = 0.6$. Note also that the up-and-down pattern is sufficiently imperfect that the autocorrelations damp to near zero by about lag 15.

# 1.4 Estimation of the Mean, Autocovariance, and Autocorrelation for Stationary Time Series

As discussed previously, a common goal in time series analysis is that of obtaining information concerning a time series on the basis of a single realization. In this section, we discuss the estimation of $\gamma(h)$, and $\rho(h)$ from a

single realization. Our focus will be discrete parameter time series where $T = \{..., -2, -1, 0, 1, 2, ...\}$, in which case a finite length realization $t = 1, 2, ...$, $n$ is typically observed. Analogous to the ones given here are available for continuous parameter time series will only be briefly mentioned in examples. The reader is referred to Parzen (1962) for the more general results.

# 12 Applied Time Series Analysis with R

# 1.4.1 Estimation of $\mu$

Given the realization $[x_t, t = 1, 2, ... , n]$ from a stationary time series, the natural estimate of the common $\mu$ is the sample mean

```
$$\bar{X} = \frac{1}{n} \sum_{t=1}^{n} X_t. \quad (1.4)$$
```

It is obvious that the estimator $\bar{X}$ is unbiased for $\mu$.

# 1.4.1.1 Ergodicity of $\bar{X}$

We will say that $\bar{X}$ is ergodic for $\mu$ if $\bar{X}$ converges in the mean square sense to $\mu$ as $n$ increases, that is, $\lim_{n\to\infty} E[( \bar{X}-\mu)^2] = 0$.

# Theorem 1.2

Suppose $\{X_t; t = 0, \pm1, \pm2, ...\}$ is a stationary time series. Then, $\bar{X} = \frac{1}{n} \sum_{t=1}^{n} X_t,$ is ergodic for $\mu$ if and only if

```
$$\lim_{k\to\infty} \frac{1}{k} \sum_{t=0}^{k-1} \gamma_t = 0. \quad (1.5)$$
```

See Yaglom (1962) for a proof of Theorem 1.2. We also have the following corollary.

# Corollary 1.1

Let $X_t$ be a discrete parameter stationary time series as in Theorem 1.2. Then, $X$ is ergodic for $\mu$ if

```
$$\lim_{k\to\infty} \gamma_k = 0, \quad (1.6)$$
```

or equivalently if

$$\lim_{k\to\infty} \rho_k = 0. \quad (1.7)$$

The sufficient condition for the ergodicity of $\tilde{X}$ given in Corollary 1.1 is quite useful and one that holds for the broad class of stationary autoregressive-moving average, ARMA($p,q$) time series that we will discuss in Chapter 3. Even though $X_i$’s close to each other in time may have substantial correlation, the condition in Corollary 1.1 assures that “large” separation, are nearly uncorrelated.

# EXAMPLE 1.2: AN ERGODIC PROCESS

Consider the process $X_t, t=0, \pm1, \pm2,$ ... defined by

$X_t = 0.8X_{t-1} + a_t. \quad (1.8)$

$a_t$, is discrete white noise with zero mean and variance $\sigma_a^2$. In other words, Equation 1.8 is a “regression-type” model in which $X$ (the dependent variable) is 0.8 times $X_t$ (the independent variable) plus a uncorrelated “noise”. Notice that $X_t$ and $a_k$ are uncorrelated for $k>0$. The process in Equation 1.8 is an example of a first-order autoregressive process, denoted AR(1), which will be examined in detail in Chapter 3. We will show in that chapter that $X_t$ as defined in Equation 1.8 is a stationary process. By taking expectations of both sides of Equation 1.8 and recalling that $a_t$ has zero mean, it follows

$E[X_t] = 0.8E[X_{t-1}]. \quad (1.9)$

Since $X$ is stationary, it follows that $E[X_t] = E[X_{t-1}] = \mu$. Now, Equation 1.9 implies that $\mu = 0.8\mu$, that is, $\mu = 0$. Letting $k>0$, we obtain an expression by pre-multiplying each term in $E[X_t, a_k] = E[X_t a_k]$ from Equation 1.8 by $X_{t-k}$ and taking these expectations. This yields

$E[X_t, a_k] = 0.8E[X_{t-1}, X_{t-k}] + E[X_{t-k}, a_t]. \quad (1.10)$

and since $E[X_{t-1}, a_k] = 0$, Equation 1.1 simplifies to $\gamma_k = 0.8\gamma_{k-1}$, which implies $\gamma_k = \gamma_0(0.8)^k$ and $\rho_k = 0.8^k$. Thus, according to Corollary 1.1, $\tilde{X}$ is ergodic for model $\mu$ (1.8). See Section 3.2.4.

In order to see the impact of condition (1.7) on the estimate using $\mu$ based on a single realization, that $\rho_1 = 0.8$, so that $X_t$ and $X_{t+1}$ are providing correlated (and somewhat redundant) information about $\mu$, but for example, $\rho_{20} = 0.01$, so that $X_t$ and $X_{t+20}$ are providing nearly uncorrelated information about $\mu$. Figure 1.5 (data set fig1.5 in tswge) shows a realization of

# Applied Time Series Analysis with R

![](img/41dcbfb9af56fa48895afde322197b0b_30_0.png)

FIGURE 1.5
Realization from X, in Example 1.2.

length 100 from the model in Equation 1.8. Notice that the realization seems to “wander” back and forth around the mean $\mu = 0$ suggesting the possibility of a stationary process.

# EXAMPLE 1.3: A STATIONARY COSINE PROCESS
Define $X(t)$ for $t \in (-\infty, \infty)$ by

```
$X(t) = C\cos(\lambda t + Y)$
```

where
C and $\lambda$ are real-valued constants
Y is a random variable

Then, as we will show in the following, $X(t)$ is stationary if and only if $\varphi(1) = \varphi(2) = 0$, where $\varphi(u)$ is the characteristic function of $Y$, that is,

```
$\varphi(u) = E[e^{iuY}] \quad \text{for } i = \sqrt{-1}$.
```

Before verifying this result we first note that $\varphi(u)$ can be written as

```
$\varphi(u) = E[cos(uY) + iE[sin(uY)]. \quad (1.12)$
```

We also make use of the trigonometric identities

+   1. $\coscosA + B) = \cos A \cos B - \sin A \sin B$
2. $\cos A \cos B = \frac{1}{2}\cos(A + B) + \frac{1}{2}\cos(A - B)$.

Using identity (1), we know that $X(t)$ in Equation 1.11 can be expressed as

```
$X(t) = C[cos\lambda t \cos Y - \sin \lambda t \sin Y], \quad (1.13)$
```

# Stationary Time Series

while the product X(t)X(t+h) can be rewritten using first (2) and then as (1) as

```
X(t)X(t+h) = C\cos(\lambda t+Y)\cos(\lambda(t + h) + Y)\n= \frac{C^2}{2}\cos(2\lambda t+\lambda h+2Y) + \frac{C^2}{2}\cos(\lambda h)\n= \frac{C^2}{2}\cos(2\lambda t+\lambda h)\cos(2Y)\n- \sin(\lambda t+\lambda h)\sin(2Y)+\cos(\lambda h). (1.14)
```

(= Suppose) $\varphi(1) = \varphi(2) = 0$. Then, it is clear from Equation 1.12 that

+   a. E[cos Y] = E[sin Y] = 0
b. E[cos 2Y] = E[sin 2Y] = 0

From Equation 1.13, we see that (a) implies E[X(t)] = 0. Also, upon taking
the expectation of X(t)X(t+h) in Equation 1.14, it is seen that (b) implies

```
\gamma(h) = E[X(t)X(t+h)] = \frac{C^2}{2}\cos(\lambda h),
```

which depends on h but not on t. Moreover, $\sigma_X^2 = \gamma(0) = (C^2/2) < \infty$.
Thus, X(t) is covariance stationary.
(= Suppose) X(t) is covariance stationary. Then, since E[X(t)] does
depend on t, it follows from Equation 1.13 that E[cos Y] = E[sin Y] = 0, and
so $\varphi(1) = 0$. Likewise, E[X(t)X(t+h)] depends on h but not on t,
it follows from the last equation of Equation 1.14 that E[cos 2Y] = E[sin
2Y] = 0, that is, that $\varphi(2) = 0$-Uniform[0, 2π], then

```
\varphi(u) = \int_0^{2\pi} e^{iu} \frac{1}{2\pi} dy
= \frac{e^{2\pi iu}-1}{2\pi iu},
```

so that $\varphi(1) = \varphi(2) = 0$, and thus, the uniform [0, 2π] satisfies the
condition on Y, and the resulting process X(t) = C cos(\lambda t+Y) is stationary.
Figure 1.6 shows three realizations of the process described in
Equation 1.11 with $\lambda=0.6$ and Y ~ [0, 2π]. The realization in Figure 1.6a
is for the case where Y = 1.5. The realizations in Figures 1.3 and
1.5, the behavior in Figure 1.6 is very deterministic. In, of
the plot would lead to believe that the mean of this process depends
t. However, it is not the case where Y is random. Figure
1.6b and c shows two other realizations for different values for the ran-
domain variable Y. Note that the effect of the random variable Y is to ran-\domly shift the "starting point" of the cosine wave in each realization. Y
is called the phase shift. These realizations are simply three realizations
