estimates, and R function ar.ols computes the OLS estimates of an AR(p) model. The residuals can also be calculated and retained, and in the tswge routine est.ar.wge they are based on a backcasting procedure discussed in Section 7.4. The white noise variance is estimated using these residuals. See Appendix for more details. Analysis of residuals related to a model fit is discussed in Section 9.1.

# 7.2.2 Preliminary Estimates for MA(q) Models

Estimation of the parameters of the MA(q) model

$$X_t = a_t - \theta_1 a_{t-1} - \cdots - \theta_q a_{t-q}\tag{7.19}$$

is more difficult than the AR estimation discussed earlier. Notice that, as before, we assume $\mu = 0$, and the estimation procedures discussed here are to be applied to the mean-corrected series $X_t - \bar{X}$. In this section, we consider invertible MA(q) models, that is, models for which the roots of $\theta(B) = 0$ are all outside the unit circle.

# 7.2.2.1 MM Estimation for an MA(q)

MM estimation of the parameters $\theta_j$, $j = 1, \dots, q$ is based on the relationship between the autocorrelation function and parameters of an MA(q) model given in Equation 3.4. Specifically, these estimates are found by solving the nonlinear equations

$$\hat{\rho}_k = \frac{-\hat{\theta}_k + \hat{\theta}_1 \hat{\theta}_{k+1} + \hat{\theta}_2 \hat{\theta}_{k+2} + \cdots + \hat{\theta}_{q-k} \hat{\theta}_q}{1 + \hat{\theta}_1^2 + \cdots + \hat{\theta}_q^2},\tag{7.20}$$

where $k = 1, 2, \dots, q$ for $\hat{\theta}_1, \dots, \hat{\theta}_q$. An MM estimate of $\sigma_a^2$ can be obtained from Equation 3.2 as

$$\hat{\sigma}_a^2 = \frac{\hat{\gamma}_0}{1 + \hat{\theta}_1^2 + \cdots + \hat{\theta}_q^2}.\tag{7.21}$$

# EXAMPLE 7.1: MMS ESTIMATION FOR AN MA(1)

For an MA(1) model, Equation 7.20 becomes