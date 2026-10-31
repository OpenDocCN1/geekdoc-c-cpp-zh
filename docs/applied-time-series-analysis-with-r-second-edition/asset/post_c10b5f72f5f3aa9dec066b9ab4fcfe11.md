
$$
\ell(\phi_1,\ldots,\phi_p,\theta_1,\ldots,\theta_p,\sigma_a^2)\approx -\frac{n}{2}\ln(2\pi\sigma_a^2)-\frac{S_u}{2\sigma_a^2}. \tag{7.37}
$$

Approximations to the unconditional ML estimates can be obtained by maximizing \(\ell(\phi_1,\ldots,\phi_p,\theta_1,\ldots,\theta_p,\sigma_a^2)\) in Equation 7.37. This maximization can be accomplished by minimizing the unconditional sum of squares \(S_u\) for finite, nonzero \(\sigma_a^2\), and, consequently, these estimates are sometimes referred to as *unconditional least squares* estimates.

Box et al. (2008) suggest a practical method for approximating the unconditional sum of squares, \(S_u\), based on a back-forecasting (or *backcasting*) technique. They express the unconditional sum of squares as

$$
S_u=\sum_{t=-\infty}^{n}\{E[a_t\mid X]\}^2. \tag{7.38}
$$

where \(E[a_t\mid X]\) denotes the conditional expectation of \(a_t\) given \(X_1,\ldots,X_n\). The unconditional sum of squares in Equation 7.38 can be approximated by the sum

$$
\hat{S}_u=\sum_{t=-K}^{n}\hat{a}_t^2. \tag{7.39}
$$

for some positive integer \(K\). This approach essentially involves “backcasting” \(X_0, X_{-1},\ldots\), and using these backcasts and Equation 7.31 to estimate \(a_{-K},a_{-K+1},\ldots,a_n\). Backcasting will be discussed in Section 7.4. The estimates obtained by choosing the parameters that minimize Equation 7.39 are sometimes called the *unconditional least squares* estimates, whereas the *unconditional* or *exact ML* estimates are obtained by minimizing the log-likelihood in Equation 7.35, where \(S_u\) is computed using Equation 7.38. For additional discussion of conditional and unconditional ML estimation, see Priestley (1981).

2. Another simplification is to use \(f(x_{p+1}, \dots, x_n \mid x_1, \dots, x_p)\) as the likelihood function and maximize

$$
l(\phi_1, \dots, \phi_p, \theta_1, \dots, \theta_p, \sigma_a^2) \approx -\frac{n-p}{2}\ln(2\pi\sigma_a^2) - \frac{S_c}{2\sigma_a^2}. \tag{7.40}
$$

The estimates obtained by maximizing Equation 7.40 are called the conditional ML estimates.

**Estimation of \(\sigma_a^2\):** The ML estimate of \(\sigma_a^2\) (based on maximizing either Equation 7.35 or Equation 7.37) can be obtained by differentiating \(l(\phi, \theta, \sigma_a^2)\) with respect to \(\sigma_a^2\), which yields (in either case)

$$
\frac{\partial l}{\partial \sigma_a^2} = -\frac{n}{2}\left(\frac{1}{\sigma_a^2}\right) + \frac{S}{2\sigma_a^4}
$$

where \(S = S_u\) or \(S_c\). Setting this partial derivative equal to zero and solving for \(\sigma_a^2\) gives the estimate

$$
\hat\sigma_a^2 = \frac{1}{n}\sum_{t=1}^{n}\hat a_t^2, \tag{7.41}
$$

where the \(\hat a_t\)'s in Equation 7.41 denote the estimates obtained via backcasting.

If backcasting is not used and the conditional sum of squares \(\hat S_c = \sum_{t=p+1}^{n}\hat a_t^2\) is obtained (based on \(a_1^* = a_2^* = \dots = a_p^* = 0\)), then, in this case, the conditional ML estimate of \(\sigma_a^2\) is

$$
\hat\sigma_a^2 = \frac{\hat S_c}{\,n-p\,}. \tag{7.42}
$$

Here, \(\hat{S}_c\) denotes the sum of squares function with conditional ML estimates inserted for \(\phi_1\), ..., \(\phi_p\), \(\theta_1\), ..., \(\theta_q\).

**Using R:** The tswge function `est.arma.wge` calculates ML estimates of the ARMA(p,q) parameters based on base R function `arima`. The default option in `arima` is to obtain ML estimates but conditional sums-of-squares estimates can also be obtained. See the R documentation but realize that the signs of the MA parameter estimates should be changed to match the model used in this book for the MA parameters.

## 7.3.2 ML Estimation Using the Innovations Algorithm

The exact likelihood function in the ARMA(p,q) case can be expressed in terms of the innovations algorithm (see Brockwell and Davis, 1991) for calculating one-step ahead forecasts. The log-likelihood function can be written as

$$
l(\phi, \theta, \sigma_a^2) = -\frac{n}{2}\ln(2\pi\sigma_a^2) - \frac{1}{2}\sum_{t=0}^{n-1}\ln(r_t) - \frac{\sigma_a^{-2}}{2}\sum_{t=1}^{n}\frac{(X_t - \hat{X}_{t-1}(1))^2}{r_{t-1}}, \tag{7.43}
$$

where, using the notation of Chapter 6, \(\hat{X}_{t-1}(1)\) is the one-step ahead forecast for \(X_t\) (using the \(\phi'_j\)s and \(\theta'_j\)s) and

$$
r_t = \frac{E[(X_{t+1} - \hat{X}_t(1))^2]}{\sigma_a^2}.
$$

Taking the partial derivative of \(l(\phi, \theta, \sigma_a^2)\) with respect to \(\sigma_a^2\) results in

$$
\hat{\sigma}_a^2 = \frac{1}{n}S_u(\hat{\phi}, \hat{\theta}), \tag{7.44}
$$

where

$$
S_u(\hat{\phi}, \hat{\theta}) = \sum_{t=1}^{n}\frac{(X_t - \hat{X}_{t-1}(1))^2}{r_{t-1}},
$$

$$
\hat{X}_1^B(l) = 1.2\hat{X}_1^B(l + 1) - 0.6\hat{X}_1^B(l + 2) + 50.04(0.4),
$$

where \(\hat{X}_1^B(l)\) is the backcast of \(X_{1-l}\) given data from \(X_1, X_2, \ldots\); the default value for \(K\) in `backcast.wge` is \(K = 50\), but in Table 7.2, we only show the backcasts for \(X_0, X_{-1}, \ldots, X_{-12}\).

3. Set \(\hat{a}_{-50} = \hat{a}_{-49} = 0\) and calculate the residuals

$$
\hat{a}_t = \hat{X}_t^B - 1.2\hat{X}_{t-1}^B + 0.6\hat{X}_{t-2}^B + 0.5\hat{a}_{t-1} - 50.04(0.4),
$$

where \(\hat{X}_t^B\) is defined in Step 2. These values are shown for \(t = -12, -11, \ldots, 25\) in Table 7.2, where it can be seen that for \(t \le 11\) the residuals thus obtained agree with those shown in Table 6.1 obtained using the conditional approach.

4. Estimate \(\sigma_a^2\) using \(\hat{\sigma}_a^2 = \frac{1}{25}\sum_{t=1}^{n}\hat{a}_t^2 = 0.68\).

**Using R:** Residuals are calculated (using backcasting) and retained each time parameter estimates are obtained in `est.ar.wge` and `est.arma.wge`.

**TABLE 7.2** Realization of Length 25 and Associated Estimates of \(a_t\) Obtained Using Backcasting from the Model \((1 - 1.2B + 0.6B^2)(X_t - 50) = (1 - 0.5B)a_t\)

$$
\mathbf{\Gamma}=\begin{pmatrix}\gamma_0 & \gamma_1 & \cdots & \gamma_{p-1}\\\gamma_1 & \gamma_0 & \cdots & \gamma_{p-2}\\\vdots & \vdots & \ddots & \vdots\\\gamma_{p-1} & \gamma_{p-2} & \cdots & \gamma_0\end{pmatrix}.
$$

(see Brockwell and Davis, 1991.)

Even though the estimators are asymptotically equivalent in the AR(p) case, it is worth noting that the YW estimates can be quite poor in practice when some roots of the characteristic equation are very near the unit circle or when there are repeated roots. Consider, for example, the AR(3) model

$$
(1 - 0.995B)(1 - 1.2B + 0.8B^2)X_t = a_t, \tag{7.52}
$$

in Equation 5.12 which has a positive real root very close to the unit circle (\(\left| r_1^{-1} \right| = 0.995\)) and complex conjugate roots that are further from the unit circle \(\left| r_i^{-1} \right| = \sqrt{0.8}=0.89\). Figure 5.2c shows that the autocorrelation function for this model approximates the damped exponential behavior of a first-order process, and, in Section 5.2, we discussed the fact that the (limiting) autocorrelations satisfy a first-order difference equation. As a consequence, the third-order theoretical YW equations associated with Equation 7.52 are a near singular system, and the use of sample autocorrelations in these equations will tend to reflect the weakened effect of the second-order behavior. In Tables 7.6 and 7.7, we will see that the YW estimates based on a realization from this model are quite poor while the Burg estimates are much more stable. This is a common pattern for such models, and, for this reason, it is preferable to use the ML or Burg estimates. In Example 7.5, we use Equation 7.50 to find the asymptotic distributions for estimators of an AR(1) and an AR(2) process.

### EXAMPLE 7.5: ASYMPTOTIC DISTRIBUTIONS FOR AR(1) AND AR(2) MODELS

1. AR(1): In the case of an AR(1) model, \(\mathbf{\Gamma}\) is the \(1 \times 1\) matrix whose element is \(\gamma_0\), which from Equation 3.37 is given by \(\gamma_0 = \sigma_a^2 / (1 - \phi_1^2)\). Thus, it follows that

$$
\sigma_a^2 \Gamma^{-1} = 1 - \phi_1^2, \tag{7.53}
$$

so that \(\hat{\phi}_1\) is asymptotically normal with mean \(\phi_1\) and variance \(\left(1 - \phi_1^2\right)/n\).

2. AR(2): The matrix \(\mathbf{\Gamma}\), for an AR(2), is given by

$$
\mathbf{\Gamma} = \begin{bmatrix} \gamma_0 & \gamma_1 \\ \gamma_1 & \gamma_0 \end{bmatrix}, \tag{7.54}
$$

where \(\gamma_0\) and \(\gamma_1\) are given by Equations 3.113 and 3.114 (with \(\theta_1 = 0\)) as

$$
\gamma_0 = \frac{(1 - \phi_2)\sigma_a^2}{(1 + \phi_2)\left((1 - \phi_2)^2 - \phi_1^2\right)}. \tag{7.55}
$$

$$
\gamma_1 = \frac{\phi_1\sigma_a^2}{(1 + \phi_2)\left((1 - \phi_2)^2 - \phi_1^2\right)}.
$$

After some algebra, it follows that

$$
\sigma_a^2 \mathbf{\Gamma}^{-1} = \begin{bmatrix} 1 - \phi_2^2 & -\phi_1(1 + \phi_2) \\ -\phi_1(1 + \phi_2) & 1 - \phi_2^2 \end{bmatrix}. \tag{7.56}
$$

From Equation 7.50 and the diagonal elements of Equation 7.56, it can be seen that, asymptotically, \(\hat{\phi}_1\) is distributed as a normal random variable with mean \(\phi_1\) and variance \(\left(1 - \phi_2^2\right)/n\), while \(\hat{\phi}_2\) is asymptotically normal with mean \(\phi_2\) and the same asymptotic variance as \(\hat{\phi}_1\).

### 7.5.1.1 Confidence Intervals: AR Case

A common use for the result in Equation 7.50 is to compute approximate large sample confidence intervals for the parameters. From Equation 7.50, it follows that

$$
\left(\hat{\phi} - \phi\right)' \frac{n\hat{\mathbf{\Gamma}}}{\hat{\sigma}_a^2} \left(\hat{\phi} - \phi\right) \Rightarrow \chi^2(p), \tag{7.57}
$$
