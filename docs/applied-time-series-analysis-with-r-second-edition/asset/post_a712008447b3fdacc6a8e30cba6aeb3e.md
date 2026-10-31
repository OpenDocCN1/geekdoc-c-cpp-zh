
estimates, and R function ar.ols computes the OLS estimates of an AR(p) model. The residuals can also be calculated and retained, and in the tswge routine est.ar.wge they are based on a backcasting procedure discussed in Section 7.4. The white noise variance is estimated using these residuals. See Appendix for more details. Analysis of residuals related to a model fit is discussed in Section 9.1.

## 7.2.2 Preliminary Estimates for MA(q) Models

Estimation of the parameters of the MA(q) model

$$X_t = a_t - \theta_1 a_{t-1} - \cdots - \theta_q a_{t-q}\tag{7.19}$$

is more difficult than the AR estimation discussed earlier. Notice that, as before, we assume $\mu = 0$, and the estimation procedures discussed here are to be applied to the mean-corrected series $X_t - \bar{X}$. In this section, we consider invertible MA(q) models, that is, models for which the roots of $\theta(B) = 0$ are all outside the unit circle.

### 7.2.2.1 MM Estimation for an MA(q)

MM estimation of the parameters $\theta_j$, $j = 1, \dots, q$ is based on the relationship between the autocorrelation function and parameters of an MA(q) model given in Equation 3.4. Specifically, these estimates are found by solving the nonlinear equations

$$\hat{\rho}_k = \frac{-\hat{\theta}_k + \hat{\theta}_1 \hat{\theta}_{k+1} + \hat{\theta}_2 \hat{\theta}_{k+2} + \cdots + \hat{\theta}_{q-k} \hat{\theta}_q}{1 + \hat{\theta}_1^2 + \cdots + \hat{\theta}_q^2},\tag{7.20}$$

where $k = 1, 2, \dots, q$ for $\hat{\theta}_1, \dots, \hat{\theta}_q$. An MM estimate of $\sigma_a^2$ can be obtained from Equation 3.2 as

$$\hat{\sigma}_a^2 = \frac{\hat{\gamma}_0}{1 + \hat{\theta}_1^2 + \cdots + \hat{\theta}_q^2}.\tag{7.21}$$

### Example 7.1: MM Estimation for an MA(1)

For an MA(1) model, Equation 7.20 becomes

### 7.2.2.2 MA(q) Estimation Using the Innovations Algorithm

Another approach to obtaining preliminary estimates of the MA parameters involves use of the innovations algorithm (see Brockwell and Davis, 1991). For a stationary process, $X_t$, let $\hat{X}_m(1)$ denote the best one-step ahead predictor of $X_{m+1}$ given data $X_1$, ..., $X_m$. These predictors can be shown to follow the relationship

$$
\hat{X}_n(1)=\begin{cases}
0 & \text{if } n=0,\\
\sum_{j=1}^{n}\theta_{n|j}\bigl(X_{n+1-j}-\hat{X}_{n-j}(1)\bigr) & \text{if } n=1,2,\dots
\end{cases}\tag{7.25}
$$

for some constants $\theta_{n|j}$, $j=1,2,\dots,n$. (see Brockwell and Davis, 1991, 2002). That is, the one-step ahead predictor is expressed as a linear combination of the prediction errors (innovations) $\hat{a}_{k+1}=X_{k+1}-\hat{X}_k(1)$. The estimated coefficients $\hat{\theta}_{m1},\dots,\hat{\theta}_{mm}$ and white noise variance $\hat{v}_m$, $m=1,2,\dots$ are calculated recursively as follows:

$$
\hat{v}_0=\hat{\gamma}_0
$$

$$
\hat{\theta}_{m,m-k}=\hat{v}_{k}^{-1}\left\{\sum_{j=0}^{k-1}\hat{\theta}_{m,m-j}\hat{\theta}_{k,k-j}\hat{v}_j-\hat{\gamma}_{m-k}\right\},
$$

for $k=0,1,\dots,m-1$ and

$$
\hat{v}_m=\hat{\gamma}_0-\sum_{j=0}^{m-1}\hat{\theta}_{m,m-j}^2\hat{v}_j.
$$

The innovations algorithm can be used to fit MA models such as

$$
X_t = a_t - \hat{\theta}_{m1}a_{t-1} - \cdots - \hat{\theta}_{mm}a_{t-m},
$$

where $m=1,2,\dots$. This technique is closely related to the use of the Durbin–Levinson algorithm given in Equation 7.9 which produces YW estimates of the AR parameters by recursively solving the YW equations. However, unlike the

$\hat{e}_{pt}^{(0)} = X_t - \sum_{j=1}^{p} \hat{\phi}_{jp}^{(0)} X_{t-j}$ are obtained. Note that if $q > 0$, then $\hat{e}_{pt}^{(0)}$ is not an estimator of white noise and will contain information about the model.

The first iterated regression model

$$
X_t = \sum_{j=1}^{p} \phi_{jp}^{(1)} X_{t-j} + \beta_{1p}^{(1)} e_{p,t-1}^{(0)} + e_{pt}^{(1)}
$$

for $t = p + 2, ..., n$ is then formed. Let $\hat{\phi}_{jp}^{(1)}$ and $\hat{\beta}_{1p}^{(1)}$ denote the corresponding least squares estimates. If $q = 1$, then $\hat{\phi}_{jp}^{(1)}$ is consistent for $\phi_j$, $j = 1, ..., p$. If $q > 1$, the procedure is continued, by calculating residuals

$$
\hat{e}_{pt}^{(1)} = X_t - \sum_{j=1}^{p} \hat{\phi}_{jp}^{(1)} X_{t-j} - \hat{\beta}_{1p}^{(1)} \hat{e}_{p,t-1}^{(0)}
$$

and forming a second iterated regression model. Tsay and Tiao (TT) estimates $\hat{\phi}_j$, $j = 1, ..., p$ for an ARMA$(p,q)$ model are given by $\hat{\phi}_{jp}^{(q)}$, $j = 1, ..., p$.

Tsay and Tiao (1984) showed that it is not necessary to go through this entire procedure, but note that the TT estimates $\hat{\phi}_{jp}^{(q)}$ can be obtained using the recursion

$$
\hat{\phi}_{jk}^{(m)} = \hat{\phi}_{jk+1}^{(m-1)} - \frac{\hat{\phi}_{j-1,k}^{(m-1)} \hat{\phi}_{k+1,k+1}^{(m-1)}}{\hat{\phi}_{kk}^{(m-1)}}
$$

where $j = 1, ..., k$ with $k \ge 1$. The recursion is initialized with $\hat{\phi}_{0k}^{(m-1)} = -1$ and with estimates $\hat{\phi}_{jk}^{(0)}$ for the case $q = 0$ obtained using a method for estimating the parameters of an AR process. Tsay and Tiao (1984) used least squares estimates to initialize this recursion. The TT estimates are asymptotically equivalent to the

## 7.3.1 Conditional and Unconditional ML Estimation

Letting $\sigma_a^2 M_n^{-1}=\Sigma_n$, the joint probability density function of $\mathbf{X}=(X_1,\ldots,X_n)$ is given by

$$f(x_1,\ldots,x_n)=\frac{1}{(2\pi\sigma_a^2)^{n/2}}|M_n|^{1/2}\exp\left\{-\frac{\mathbf{x}^{\prime}M_n\mathbf{x}}{2\sigma_a^2}\right\}.\tag{7.29}$$

The joint density function in Equation 7.29 can be written

$$f(x_1,\ldots,x_n)=f(x_{p+1},\ldots,x_n\mid x_1,\ldots,x_p)f(x_1,\ldots,x_p).\tag{7.30}$$

where $f(\,\cdot\mid\cdot\,)$ is the conditional probability density function. Since the $a_t$ are uncorrelated $N(0,\sigma_a^2)$ random variables, it follows that

$$f(a_{p+1},\ldots,a_n)=\frac{1}{(2\pi\sigma_a^2)^{(n-p)/2}}\exp\left\{-\frac{1}{2\sigma_a^2}\sum_{t=p+1}^{n}a_t^2\right\}.$$

Reordering the terms in Equation 7.27, we obtain

$$a_t=X_t-\phi_1X_{t-1}-\cdots-\phi_pX_{t-p}+\theta_1a_{t-1}+\cdots+\theta_qa_{t-q}.\tag{7.31}$$

Conditional on $X_1=x_1,\ldots,X_p=x_p$ and starting values $a_1=a_1^*,\ldots,a_p=a_p^*$, it follows from Equation 7.31 (assuming for convenience that $q\leq p$) that for a choice of the $\phi_i$'s and $\theta_i$'s, the random variables $a_{p+1},\ldots,a_n$ and $X_{p+1},\ldots,X_n$ are related by the system of equations

$$
\begin{aligned}
a_{p+1}&=X_{p+1}-\phi_1X_p-\cdots-\phi_pX_1+\theta_1a_p+\cdots+\theta_qa_{p+1-q},\\
a_{p+2}&=X_{p+2}-\phi_1X_{p+1}-\cdots-\phi_pX_2+\theta_1a_{p+1}+\cdots+\theta_qa_{p+2-q},\\
&\vdots\\
a_n&=X_n-\phi_1X_{n-1}-\cdots-\phi_pX_{n-p}+\theta_1a_{n-1}+\cdots+\theta_qa_{n-q}.
\end{aligned}
$$

The values for $a_1,\ldots,a_p$ given earlier are often taken to be 0, their unconditional mean. Since the absolute value of the Jacobian of this transformation is one, it follows that

$$
\begin{aligned}
f(x_{p+1},\ldots,x_n\mid x_1,\ldots,x_p)
&=\frac{1}{(2\pi\sigma_a^2)^{(n-p)/2}}\exp\left\{-\frac{1}{2\sigma_a^2}\sum_{t=p+1}^{n}(x_t-\phi_1x_{t-1}-\cdots-\phi_px_{t-p}+\theta_1a_{t-1}+\cdots+\theta_qa_{t-q})^2\right\}\\
&=\frac{1}{(2\pi\sigma_a^2)^{(n-p)/2}}\exp\left\{-\frac{S_c}{2\sigma_a^2}\right\}.\tag{7.32}
\end{aligned}
$$

where $S_c$ is given by

$$S_c=\sum_{t=p+1}^{n}(x_t-\phi_1x_{t-1}-\cdots-\phi_px_{t-p}+\theta_1a_{t-1}+\cdots+\theta_qa_{t-q})^2.$$

Calculating $f(x_1,\ldots,x_n)$ using Equation 7.30 involves $f(x_1,\ldots,x_p)$, which is given by

$$f(x_1,\ldots,x_p)=\frac{1}{(2\pi\sigma_a^2)^{p/2}}|M_p|^{1/2}\exp\left\{-\frac{x_p'M_px_p}{2\sigma_a^2}\right\},\tag{7.33}$$

where $x_p=(x_1,\ldots,x_p)'$. Multiplying $f(x_{p+1},\ldots,x_n\mid x_1,\ldots,x_p)$ in Equation 7.32 by $f(x_1,\ldots,x_p)$ in Equation 7.33 yields

$$\begin{aligned}f(x_1,\ldots,x_n)&=f(x_{p+1},\ldots,x_n\mid x_1,\ldots,x_p)f(x_1,\ldots,x_p)\\&=\frac{1}{(2\pi\sigma_a^2)^{(n-p)/2}}\exp\left\{-\frac{S_c}{2\sigma_a^2}\right\}\frac{1}{(2\pi\sigma_a^2)^{p/2}}|M_p|^{1/2}\exp\left\{-\frac{x_p'M_px_p}{2\sigma_a^2}\right\}\\&=\frac{1}{(2\pi\sigma_a^2)^{n/2}}|M_p|^{1/2}\exp\left\{-\frac{S_u}{2\sigma_a^2}\right\}.\end{aligned}$$

where

$$S_u=S_c+x_p'M_px_p.\tag{7.34}$$

It is common terminology to refer to $S_u$ as the *unconditional sum of squares* and to $S_c$ as the *conditional sum of squares*. The log-likelihood function is given by

$$l(\phi_1,\ldots,\phi_p,\theta_1,\ldots,\theta_q,\sigma_a^2)=-\frac{n}{2}\ln(2\pi\sigma_a^2)+\frac{1}{2}\ln|M_p|-\frac{S_u}{2\sigma_a^2}.\tag{7.35}$$

The ML estimators are found by maximizing Equation 7.35 with respect to the parameters $\phi_1,\ldots,\phi_p$, $\theta_1,\ldots,\theta_q$, and $\sigma_a^2$. The estimators so obtained are the *unconditional* or *exact ML* estimates.
