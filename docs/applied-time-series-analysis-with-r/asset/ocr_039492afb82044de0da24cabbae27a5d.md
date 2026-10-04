# Forecasting

+   ii. Discuss the quality of the forecasts. That is, how close were the forecasts to the actual values, and how well did the forecasts stay in phase with the actual cycles?

+   iii. On the basis of this comparison, which model do you prefer? Which seems to be the poorest model?

6.8 a. Generate a realization of length $n=50$ from the signal-plus-noise model $X_i = 5+0.3+Z_i$, where $Z_i = (1+0.2B+0.6B^2)a_i$ and $\sigma_Z^2=0.5$. Plot the realization, forecasts, and forecast limits for the next 20 time periods.

b. Generate a realization of length $n=100$ from the signal-plus-noise model $X_i=50+5\cos(2\pi f_0 t+2.5)+Z_i$, where $f_0=0.1$ and $Z_i=(1+0.7B)a_i$ and $\sigma_Z^2=1$. Plot the realization, forecasts, and forecast limits for the next 20 time periods.

# Theoretical Problems

6.9 Prove Theorem 6.3, show that if $X_t$ is a stationary process with autocovariance $\gamma_0$ then the quantities $a_1, \dots, a_n$ in the definition of $\hat{X}_t(\ell)$ in Equation 6.2 are the solutions to the system

![](bbox=[0.248, 0.497, 0.752, 0.597])

6.10 Verify the following properties associated with the $\hat{X}_t(\ell)$:

+   a. the one-step forecast errors are the $a_s$, that is, $e_t(1)=a_{t+1}$.
b. the forecast errors have expectation zero, that is, $E[e_t(\ell)]=0, \ell \ge 1$.
c. the variance of the forecast errors is given by $Var[e_t(\ell)]=\sigma_a^2\sigma_w^2$.
d. covariance between forecast errors

$Cov[e_t(\ell), e_{t-j}(\ell)]=0, j \ge \ell$.

Thus, whenever $j=0, 1, \dots, \ell-1$, the forecast errors may be correlated.
e. $e_t(\ell_1)$ and $e_t(\ell_2)$ are correlated. Specifically, find an expression for $Cov[e_t(\ell_1), e_t(\ell_2)]$ where $\ell_2 > \ell_1$.
f. the "best MSE forecast" for $\sum_{k=1}^m \alpha_k X_{t+k}$ from origin $t_0$ is given by $\sum_{k=1}^m \alpha_k \hat{X}_t(k)$.

# 271