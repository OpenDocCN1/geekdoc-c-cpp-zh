
# Applied Time Series Analysis with R

![](img/41dcbfb9af56fa48895afde322197b0b_32_0.png)

# FIGURE 1.6

Three realizations of $X(t)$ of Example 1.3. (a) $Y=1.5$. (b) $Y=0.5$. (c) $Y=4.5$.

from the ensemble of possible realizations. Note that for these three realizations, $X(10)$ equals $0.35, 0.98$, and $-0.48$, respectively, which is consistent with our finding that $E[X(t)]$ does not depend on $t$.

The important point is that the property of stationarity cannot be determined by simple inspection of the data. Instead, it must be inferred from physical considerations, knowledge of the correlation structure, or more sophisticated techniques that we will consider in future chapters. Since Theorem 1.2 and its corollary only relate to discrete parameter processes, they do not apply to $X(t)$ in the current example. However, results analogous to both Theorem 1.2 and Corollary 1.1 do hold for continuous parameter processes (see Parzen, 1962). Notice that, in this example, $Y(t)$ does not go to zero as $h \to \infty$, $\tilde{X}_t$, defined in this continuous parameter example as

$$\tilde{X}_t = \frac{1}{t} \int_0^t X(s)ds, \quad (1.15)$$

# Stationary Time Series

can be shown to be ergodic for $\mu$ using the continuous analog to Theorem 1.2. The ergodicity of $\tilde{X}_t$ seems reasonable in this example as $t$ in Equation 1.15 increases, it seems intuitive that $\tilde{X}_t \to 0(\mu)$.

## EXAMPLE 1.4: A NON-ERGODIC PROCESS

As a hypothetical example of a non-ergodic process, consider a thread manufacturing process that produces spools of thread. The machine is cleaned and adjusted at the end of each day after the diameter remains unchanged until the end of the next day at which time it is re-cleaned. The diameter setting could be thought of as a stochastic process with each day being a realization. In Figure 1.7, we show three realizations from this hypothetical process $X(t)$.

$\mu$ is the average diameter across days, then is also clear that $\gamma(t, t+h)$ does not depend on $t$ within a day. It is also clear that $\gamma(t, h) = \gamma(0) < \infty$, for all $h$. Thus, the process is stationary. However, it obviously makes no sense to try to estimate $\mu$ by $\bar{X}_t$, that is, by averaging down the time axis for a single realization. Heuristically, we see that $\mu$ can be estimated by averaging over several realizations, but using one realization in essence provides only one piece of information. Clearly, in this case $X_t$ is not ergodic for $\mu$.

### 1.4.1.2 Variance of $\bar{X}$

Before leaving the topic of estimating $\mu$ from a realization from a stationary process, in Theorem 1.3, we give a useful formula for $\text{Var}(\bar{X})$. We leave the proof of the theorem as an exercise.

## Theorem 1.3

If $X_t$ is a discrete stationary time series, then the variance of $\bar{X}$ based on a realization of length $n$ is given by

![](img/41dcbfb9af56fa48895afde322197b0b_33_0.png)

FIGURE 1.7 Three realizations from the process in Example 1.4.

# Applied Time Series Analysis with R

$Var(\bar{X}) = \frac{\sigma^2}{n} \sum_{k=(n-1)}^{n-1} \left(1 - \frac{|k|}{n}\right) \rho_k. \quad (1.16)$

The result in Equation 1.16 shows the effect of autocorrelation on the variance of $\bar{X}$, and if $X$ is white noise, then $\gamma_k=0$ if $k \neq 0$, then Equation 1.16 becomes the well-known result $Var(\bar{X})=\sigma^2/n$. In the following section, we discuss the estimation of $\hat{\gamma}_k$ and $\hat{\rho}_k$ for a discrete stationary time series. Using the notation $\hat{\rho}_k$ to denote the estimated (sample) autocorrelations (discussed in Section 1.4.2) and $\hat{\sigma}^2=\hat{\gamma}_0$ to denote the sample variance, it is common practice to obtain approximate 95% intervals for $\mu$ using

$\bar{X}-1.96 \sum_{k=(n-1)}^{n-1} \left(1 - \frac{|k|}{n}\right) \hat{\rho}_k, \bar{X}+1.96 \sum_{k=(n-1)}^{n-1} \left(1 - \frac{|k|}{n}\right) \hat{\rho}_k. \quad (1.17)$

## 1.4.2 Estimation of $\gamma_k$

Because of stationarity, $E[(X_t-\mu)(X_{t+k}-\mu)]=\gamma_k$ does not depend on $t$. As a consequence, it seems reasonable to estimate $\gamma_k$ from a single realization, by

$\hat{\gamma}_k = \frac{1}{n-|k|} \sum_{t=1}^{n-|k|} (X_t-\bar{X})(X_{t+|k|}-\bar{X}), \quad k=0, \pm1, \pm2,\dots\pm(n-1) n=0, |k|\geq n. \quad (1.18)$

that is, by moving the time axis and finding the average of all products in the realization separated by $k$ time units. Notice that if we replace $\bar{X}$ by $\mu$ in Equation 1.18, then the resulting estimator is unbiased. However, the estimator $\hat{\gamma}_k$ in Equation 1.18 is only asymptotically unbiased.

Despite the intuitive appeal of $\hat{\gamma}_k$, most series analysts use an alternative estimator, $\tilde{\gamma}_k$, defined by

$\tilde{\gamma}_k = \frac{1}{n-|k|} \sum_{t=1}^{n-|k|} (X_t-\bar{X})(X_{t+|k|}-\bar{X}), \quad k=0, \pm1, \pm2,\dots\pm(n-1) n=0, |k|\geq n. \quad (1.19)$

From examination of Equation 1.19, it is clear that $|\tilde{\gamma}_k|$ values will tend to be “small” when $|k|$ is large relative to $n$. The estimator, $\hat{\gamma}_k$, as given in Equation 1.19, has a larger bias than, $\tilde{\gamma}_k$, in most cases, smaller mean square error. The difference between the two estimators is, of most dramatic when $|k|$ is large with respect to $n$. The comparison can be made easily

# Stationary Time Series

when $\bar{X}$ is replaced by $\mu$ in Equations 1.18 and 1.19, which we will assume for the discussion in the remainder of the current paragraph. The bias of $\hat{\gamma}_k$ in this case can be seen to be $(|k|/n)\gamma_k$. As $|k|$ increases toward $n$, the factor $|k|/n$ increases toward one, so the bias tends to $\gamma_k$. As $|k|$ increases toward $n-1$, $\text{Var}(\hat{\gamma}_k)$ will increase, and $\hat{\gamma}_k$ values will tend to have a quite erratic behavior for the larger values of $k$. The overall pattern of $\hat{\gamma}_k$ is usually better approximated by $\hat{\gamma}_k$ than by $\tilde{\gamma}_k$, and we will see that it is often the *pattern* of the auto-correlation function that is of importance. The behavior of $\hat{\gamma}_k$ is also better approximated by $\tilde{\gamma}_k$ in which $\tilde{\gamma}_k$ is also positive semidefinite in the sense of property (4) given in Section 1.3, while $\hat{\gamma}_k$ is not necessarily positive. For further discussion of these topics, the reader is referred to Priestley (1981).

## EXAMPLE 1.5: BEHAVIOR OF SAMPLE AUTCOVARIANCES

In Figure 1.8, we display theoretical autocovariances for the AR(1) realization of Example 1.2 along with sample autocovariances $\hat{\gamma}_k$ and $\tilde{\gamma}_k$ based on the realization shown in Figure 1.5 (see fig1.5 in text). There can be seen that, for small $k$ the estimators are similar to each other, but for $k$ near $n$ the damped expectation of $\gamma_k$ is better estimated with $\hat{\gamma}_k$. Ergodic results for $\hat{\gamma}_k$ (and for $\tilde{\gamma}_k$ because of their asymptotic convergence) can also be obtained, but they are in general not of the straightforward nature of Theorem 1.2. Most of the results for $\tilde{\gamma}_k$ are proved for the case in which $\mu$ is assumed to be bounded, and without loss of generality, equal to zero. For a discussion of ergodic theorems for $\tilde{\gamma}_k$ and for some results concerning $Cov(\tilde{\gamma}_j, \tilde{\gamma}_k)$, see Priestley (1981). In the remainder of this book, we assume that the necessary conditions hold for the sample autocovariances to be ergodic for $\hat{\gamma}_k$.

![](img/41dcbfb9af56fa48895afde322197b0b_35_0.png)

**FIGURE 1.8** Theoretical and sample autocovariances based on the realization in Figure 1.5.

## 1.4.3 Estimation of $\rho_k$

The natural estimator of $\rho_k = \gamma_k/\gamma_0$ is $\hat{\rho}_k = \tilde{\gamma}_k/\tilde{\gamma}_0$, which we will refer to as the sample autocorrelation function. The estimator $\hat{\rho}$ has the desirable property that $|\hat{\rho}| \le 1$, a property that $\tilde{\rho}_k = \tilde{\gamma}_k/\tilde{\gamma}_0$ does not possess. This property can be shown by relating $\hat{\rho}$ to the Pearson product-moment correlation between the two sets of $n+k$ observations

$0,0,...,0, X_1-\tilde{X}_1, X_2-\tilde{X}_2, ..., X_n-\tilde{X}_n,$
$X_1-\tilde{X}_1, X_2-\tilde{X}_2, ..., X_n-\tilde{X}_n, 0,0,...,0,$

where, in each case, there are zeros. For notational convenience, we will denote the first row by $V_{\rho}$ $i=1, ..., n+k$ and the second row by $W_{\rho}$ $i=1, ..., n+k$. Thus, $\tilde{V} = \tilde{W} = 0$ and the product-moment correlation between $V$ and $W$ is given by

$r = \frac{\sum_{i=1}^{n+k} V_i W_i}{\sqrt{\sum_{i=1}^{n+k} V_i^2 \sum_{i=1}^{n+k} W_i^2}}$

The denominator can be rewritten as $\sum_{t=1}^n (X_t-\tilde{X}_t)^2$, and the numerator can be written as $\sum_{i=1}^k V_i W_i + \sum_{i=n+1}^n V_i W_i + \sum_{i=n+1}^{n+k} V_i W_i$. The first and last sums are zero, so that the numerator can be written as

$\sum_{i=1}^k V_i W_i + \sum_{i=n+1}^n V_i W_i = \sum_{t=1}^n (X_t-\tilde{X}_t)(X_{t+k}-\tilde{X}_{t+k}).$

Thus $r = \hat{\rho}_k$ and so $|\hat{\rho}_k| \le 1$.

Bartlett (1946) has obtained approximate expressions for $Cov(\hat{\rho}_k, \hat{\rho}_{k+j})$ when $X_t$ is a stationary Gaussian process. In particular, he showed that

$Cov(\hat{\rho}_k, \hat{\rho}_{k+j}) = \frac{1}{n} \sum_{\mu=-\infty}^{\infty} {\rho_\mu\rho_{\mu+j} + \rho_{\mu+k}\rho_\mu - 2\rho_k\rho_{\mu+k-j} - 2\rho_{k+j}\rho_{\mu-k} + 2\rho_k\rho_{k+j}\rho_{\mu}^2},$

from it follows, with $j=0$, that
