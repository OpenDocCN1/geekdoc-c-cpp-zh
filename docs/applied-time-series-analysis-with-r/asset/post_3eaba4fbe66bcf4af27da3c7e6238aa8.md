
# Forecasting

$E[(X_{t_0+\ell} - Z_{t_0}^*)X_j] = 0, \ j = 1, 2, \dots, t_0$.

Proof: See Appendix 6A.

Let $\tilde{X}_{t_0}(\ell)$ denote the linear predictor, $Z_{t_0}^*$, in Theorem 6.2. Theorem 6.3 shows how to compute the coefficients $a_1, \dots, a_{t_0}$ of $\tilde{X}_{t_0}(\ell)$, where

$$\tilde{X}_{t_0}(\ell) = a_1^*X_{t_0} + a_2^*X_{t_0-1} + \dots + a_{t_0}^*X_1$$
$= \sum_{k=1}^{t_0} a_k^*X_{t_0-k+1}. \quad (6.2)$

## Theorem 6.3

If $X_t$ is a stationary process with autocovariance function $\gamma_k, a_1^*, \dots, a_t^*$ in Equation 6.2 are the solutions to the system of equations

$$\mathbf{g}_\ell = \Gamma\mathbf{a}^*, \quad (6.3)$$

where $\mathbf{g}_\ell = (\gamma_\ell, \gamma_{\ell+1}, \dots, \gamma_{\ell+t_0-1}), \ a^* = (a_1^*, a_2^*, \dots, a_{t_0}^*),$ and

$$\Gamma = \begin{pmatrix} \gamma_0 & \gamma_1 & \dots & \gamma_{t_0-1} \\ \gamma_1 & \gamma_0 & \dots & \gamma_{t_0-2} \\ \vdots & \vdots & \ddots & \vdots \\ \gamma_{t_0-1} & \gamma_{t_0-2} & \dots & \gamma_0 \end{pmatrix}$$

Proof: See Problem 6.8.

The typical application of these results is the case $t_0 = n$ (i.e., the realization length). In this case, Equation 6.3 can be an extremely large system of equations, and these forecasts can be difficult to obtain. Consequently, in the section, we will discuss the so-called Box–Jenkins forecasts. The Box–Jenkins forecasts are based on an ARMA model and are linear predictors based on the (unattainable) assumption that the random variables $X_t, t=t_0,...$ (i.e., the infinite past) are available. Nevertheless, forecasts based on the assumption of availability are widely used in practice because they are easy to compute and intuitively attractive, and for a moderately large $t_0$, the results are close to those obtained by solving Equation 6.3. In this chapter, we focus on the Box–Jenkins style forecasts.

## 6.2 Box–Jenkins Forecasting for ARMA(p,q) Models

We return to the problem of finding the best predictor of $X_{t+h}$, but now we assume that we are given the infinite past $X_t, X_{t-1}, ...$, and that the data are from a known ARMA$(p,q)$ model. That is, we assume that the model orders and parameters are known. In a practical situation, the model orders and parameters will be estimated, and thus, the forecast errors will differ somewhat from those we present here. However, in most cases, this difference is small. As discussed in Section 6.1, "best" will to be in the mean-square sense, and the best predictor is the conditional expectation $E[X_{t+h} | X_t, X_{t-1}, ...]$. As mentioned earlier, the conditional expectation is often difficult to obtain, but it turns out it can be readily computed in the current setting.

Since $X_t$, is an ARMA$(p,q)$ process, because of its stationarity and invertibility we can write

$X_t - \mu = \sum_{j=0}^{\infty} \Psi_j a_{t-j}, \quad (6.4)$

and

$a_t = \sum_{j=0}^{\infty} \pi_j(X_{t-j} - \mu), \quad (6.5)$

respectively. Based on Equations 6.4 and 6.5, it follows that "knowing" $X_k, X_{k-v}$ is equivalent to obtaining $a_k, a_{k-1}, ...$. Thus,

$E[X_t | X_k, X_{k-1}, ...] = E[X_t | a_k, a_{k-1}, ...]. \quad (6.6)$

For notational convenience, we denote the conditional expectation in Equation 6.6 as $E_k[X]$. Similarly,

$E[a_t | a_k, a_{k-1}, ...] = E[a_t | X_k, X_{k-1}, ...]. \quad (6.7)$

which will be denoted $E_k[a_t]$. Since $E[a_t] = 0$ and $a_t$ are uncorrelated for $t_1 \neq t_2$, it follows that

$E_k[a_t] = 0, \quad t > k$
$= a_t, \quad t \leq k.$

Thus, whenever $t > k$,

$E_k[X_i] = E_k \left[ \mu + \sum_{j=0}^{\infty} \psi_j a_{i-j} \right]$
$= \mu + \sum_{j=1}^{\infty} \psi_j a_{i-j},$

Our interest is in $E_{t_0}[X_{t_0+\ell}]$ when $\ell > 0$, which is given by

$E_{t_0}[X_{t_0+\ell}] = E_{t_0} \left[ \mu + \sum_{j=0}^{\infty} \psi_j a_{t_0+\ell-j} \right]$
$= \mu + \sum_{j=1}^{\infty} \psi_j a_{t_0+\ell-j}, (6.8)$

and the desired forecast $\hat{X}_{t_0}(\ell) \equiv E_{t_0}[X_{t_0+\ell}]$ is given in Equation 6.9 below.

### 6.2.1 General Linear Process Form of the Best Forecast Equation

$\hat{X}_{t_0}(\ell) = \mu + \sum_{j=1}^{\infty} \psi_j a_{t_0+\ell-j}. (6.9)$

Note that the forecast equation in Equation 6.9 is not attainable in practice, but is given here because of its usefulness in deriving the properties of the best forecasts. Several properties of $\hat{X}_{t_0}(\ell)$ are given in the next section.

## 6.3 Properties of the Best Forecast $\hat{X}_{t_0}(\ell)$

In this section, we give several properties of the “best” predictor, $\hat{X}_{t_0}(\ell)$, when $X_i$ is a stationary, invertible ARMA(p,q) process. We provide derivations of property (b) in the following, and leave the others as exercises.

Properties of $\hat{X}_{t_0}(\ell)$

- 1. In the current setting, the best predictor, given by the conditional expectation, is a linear function of $X_{t_0}, X_{t_0-1}, \dots$

2. $\hat{X}_{t_0}(\ell) = X_{t_0+\ell}$ when $\ell \le 0$.
This useful (but not surprising) result follows from the fact that

$$\begin{aligned} \hat{X}_{t_0}(\ell) &= E_{t_0}[X_{t_0+\ell}] \\ &= E_{t_0} \left[ \mu + \sum_{j=0}^{\infty} \Psi_j a_{t_0+\ell-j} \right] \\ &= \mu + \sum_{j=0}^{\infty} \Psi_j a_{t_0+\ell-j}, \end{aligned} $$ (6.10)

whenever $\ell \le 0$

3. The $\ell$-step ahead forecast errors, $e_{t_0}(\ell) = X_{t_0+\ell} - \hat{X}_{t_0}(\ell)$, are given by

$$\begin{aligned} e_{t_0}(\ell) &= X_{t_0+\ell} + \Psi_1 a_{t_0+\ell-1} + \cdots + \Psi_{\ell-1} a_{t_0+1} \\ &= \sum_{j=1}^{\ell} \Psi_j a_{t_0+\ell-j}. \end{aligned} $$ (6.11)

4. The $\ell$-step ahead forecast errors have expectation zero, that is,

$E[e_{t_0}(\ell)] = 0, \quad \ell \ge 1. (6.12)$

Because of Equation 6.12, we say that the forecasts are unbiased.
5. The one-step ahead forecast errors are the $a_i$'s (sometimes called the residuals), that is,

$e_{t_0}(1) = a_{t_0+1}. (6.13)$

6. The variance of the forecast errors is given by

$Var[e_{t_0}(\ell)] = \sigma_a^2 \sum_{j=0}^{\ell-1} \Psi_j^2. (6.14)$

7. The covariance between forecast errors satisfies

$Cov[e_{t_0}(\ell), e_{t_0}(j)] = 0, \quad j \ge \ell.$

Whenever $j = 0, \dots, \ell - 1$, the forecast errors may be correlated.

- $e_{t_0}(\ell_1)$ and $e_{t_0}(\ell_2)$ are correlated, that is, forecast errors from the same origin are correlated.

- The “best” mean squared error (MSE) forecast” for $\sum_{k=1}^m \alpha_k \hat{X}_{t_0+k}$ from origin $t_0$ is given by $\sum_{k=1}^m \alpha_k \hat{X}_t(k)$. As an example, if $X_t$ represents monthly sales, then (i) states that from forecast origin $t_0$, the “best” forecast for next quarter’s sales, that is, for $X_{t_0+1} + X_{t_0+2} + X_{t_0+3}$ is $X_{t_0}(1) + X_{t_0}(2) + X_{t_0}(3)$.

## 6.4 $\pi$-Weight Form of the Forecast Function

A stationary and invertible process can be written in the $\pi$-weight form

$$\sum_{j=0}^{\infty} \pi_j(X_{t-j} - \mu) = a_t,$$

which was previously given in Equation 3.83. Therefore, since $\pi_0 = 1$, Equation 6.15 can be written as

$X_t = \mu - \sum_{j=1}^{\infty} \pi_j(X_{t-j} - \mu) + a_t,$

which leads to the forecasting formula

$$\hat{X}_{t_0}(\ell) = \mu - \sum_{j=1}^{\infty} \pi_j(\hat{X}_{t_0}(\ell-j) - \mu),$$

where, as before, $\hat{X}_{t_0}(\ell) = X_{t_0+\ell}$, for $\ell \le 0$. The form in Equation 6.16 is similar to the $\psi$-weight form in Equation 6.9 in it involves an infinite summation and is based on the unrealistic assumption that $X_{t_0}, X_{t_0-1}, \dots, X_1, X_0, X_{-1} \dots$ are known. Then, the following truncated version of the forecast function is used in practice.

Truncated Version of the Forecast Equation

$$\hat{X}_{t_0}^{(T)}(\ell) = \bar{X} - \sum_{j=1}^{t_0-1+\ell} \pi_j(\hat{X}_{t_0}^{(T)}(\ell-j) - \bar{X}),$$

For example, if $t_0 = n$, then using Equation 6.17, it follows that

$\hat{X}_n^{(T)}(1) = \bar{X} - \pi_1(X(n)-\bar{X}) - \pi_2(X(n-1)-\bar{X}) - \cdots - \pi_n(X(1)-\bar{X})$
$\hat{X}_n^{(T)}(2) = \bar{X} - \pi_1(\hat{X}_{t_0}^{(T)}(1)-\bar{X}) - \pi_2(X(n)-\bar{X}) - \cdots - \pi_{n+1}(X(1)-\bar{X}),$

NOTES: the $\pi$-weight version of the forecast function is appropriately used when the $\pi$-weights damp quickly so that $\pi$'s are essentially zero for $j>\ell$, which should generally hold for stationary and invertible ARMA processes when $t_0$ is sufficiently large. This form of the forecast function is useful for forecasting based on long memory models (see Section 11.6).

## 6.5 Forecasting Based on the Difference Equation

If $X$, is a stationary, invertible ARMA$(p,q)$ process, then Equation 6.9 is an expression for the best predictor of $X_{t_0+\ell}$ given $X_{t_0,t_0+\ell-1}$ in terms of the general linear process or “infinite moving average” representation of the process. $\hat{X}_t(\ell)$, can also be written in terms of the difference equation satisfied by $\phi(B)X_t = \theta(B)a_t$, and hence is more useful in practice. Suppose $X$ satisfies $\phi(B)X_t = \theta(B)a_t$, and hence

$X_{t_0+\ell} - \phi_1 X_{t_0+\ell-1} - \cdots - \phi_p X_{t_0+\ell-p} = a_{t_0+\ell} - \theta_1 a_{t_0+\ell-1} - \cdots - \theta_p a_{t_0+\ell-p}$.

Taking conditional expectations, we obtain

$E_{t_0}[X_{t_0+\ell} - \phi_1 X_{t_0+\ell-1} - \cdots - \phi_p X_{t_0+\ell-p}] = E_{t_0}[a_{t_0+\ell} - \theta_1 a_{t_0+\ell-1} - \cdots - \theta_p a_{t_0+\ell-p}].$

(6.18)

This can be written as

$\hat{X}_{t_0}(\ell) = \phi_1 \hat{X}_{t_0}(\ell-1) + \phi_2 \hat{X}_{t_0}(\ell-2) + \cdots + \phi_p \hat{X}_{t_0}(\ell-p)$
$+ E_{t_0}[a_{t_0+\ell} - \theta_1 E_{t_0}[a_{t_0+\ell-1}] - \cdots - \theta_p E_{t_0}[a_{t_0+\ell-p}]],$

(6.19)

where

$\hat{X}_{t_0}(k) = X_{t_0+k}, \quad k \le 0$,
