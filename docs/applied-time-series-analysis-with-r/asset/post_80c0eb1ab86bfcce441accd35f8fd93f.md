
# Applied Time Series Analysis with R

the sample autocorrelations in Figure 11.9d (based on the 200-point realization) primarily pick up the oscillatory behavior. However, the sample autocorrelations for the full realization of $n = 500$ are a close approximation to the theoretical autocorrelations in Figure 11.8c, which shows a mixture of oscillatory and 4-period cycle behavior for early lags with the persistent autocorrelation from the Gegenbauer factor showing up to $k \ge 20$. In general, the natural damping associated with $\hat{\rho}_k$ (based on division by $n$ instead of $n-k$) in Section 1.4 causes it to be different for persistent autocorrelations to be well estimated for moderate realization-lengths.

# EXAMPLE 11.6: LYN DATA

Figure 5.2b and c shows the log-lynx data for which AR(1) or signal-plus-noise models were considered in Example 5.2. Upon examination of the data and the sample autocorrelations it can be seen that Gegenbauer or GARMA model with G-frequency approximately $f_G = 0.10$ might be appropriate. We return to this data set in Example 11.9 where we will fit a GARMA model to the data.

# 11.4 k-Factor Gegenbauer and GARMA Processes

As we introduced the Gegenbauer process in Section 11.3, we noted that the long-memory fractional difference $(1-B)^d$ can only model "first-order" long-memory behavior associated with $f=0$. It was noted that the restriction of this to first-order long-memory behavior is analogous in the setting of AR(p) models being restricted to first-order AR models with $\phi_p = 0$. The Gegenbauer factor $(1-2B+B^2)$ provides a model in Section 11.3 for "second order" or cyclic memory when $|\mu| < 1$. Continuing with the AR(p) analysis, this corresponds to an irreducible second-order factor. In Section 3.2, we noted that a p-th AR operator, $\phi(B)=1-\phi_1B-\dots-\phi_pB^p$, can be written as $\phi(B)=\sum_{j=0}^p (-1)^j\alpha_j^j$ where $\alpha_0=1$ for first-order factors. Thus, the first- and second-order factors are viewed as building blocks of the AR(p) process represent a combination of the behaviors induced by the first- and second-order factors of $\phi(B)$. In this section, we discuss the k-factor Gegenbauer process that allows for long-memory behavior to be associated with each of $m (\le k)$ frequencies in $[0, 0.5]$. This model includes the fractional and Gegenbauer as special cases. We also consider the k-factor GARMA model that similarly generalizes the GARMA and FARMA models.

# Long-Memory Processes

In Definition 11.7, we define the $k$-factor Gegenbauer process which was considered in the $k=2$ case by Cheng (1993) and in general by Woodward et al. (1998) and Giraitis and Leips (1995).

# Definition 11.7
If $X_t$ is a causal, stationary, and invertible process satisfying

$$\prod_{j=1}^{k}(1-2u_jB+B^2)^{\lambda_j}(X_t-\mu)=a_t; \quad (11.18)$$

where $a_t$ is white noise, then it is called a $k$-factor Gegenbauer process. Theorem 11.6 gives the stationarity, long memory, and invertibility conditions for a $k$-factor Gegenbauer process.

# Theorem 11.6
Let $X$, be a $k$-factor Gegenbauer process of the form Equation 11.18.

- 1. If the $u_i$ are distinct, $|\lambda_i| < 1/2$ when $|u_i| \neq 1$ and $|\lambda_i| < 1/4$ when $|u_i|=1$, then $X$ is causal, stationary, and invertible.
- 2. The spectrum of a causal, stationary, and invertible Gegenbauer process is given by

$$P(f)=\sigma_0^2\prod_{j=1}^{k}(1-2u_je^{-2\pi f}+e^{-4\pi f})^2)^{\lambda_j} = \sigma_0^2\prod_{j=1}^{k}[4(\cos 2\pi f-u_j)^2]^{\lambda_j}. \quad (11.19)$$

The frequencies $f_G=(\cos^{-1}u_j)/(2\pi)$ are all Gegenbauer frequencies or G-frequencies.

- 3. If the conditions of (1) are satisfied along with $\lambda_j > 0$ for any $j=1, \dots$, then $X$, is long memory.

Proof: See Giraitis and Leips (1995) and Woodward et al. (1998). Note that (3) follows from the spectrum in Equation 11.19 becomes unbounded at the G-frequencies $f_G$.

In the same manner that fractional and Gegenbauer processes have been extended to include ARMA factors, the $k$-factor Gegenbauer process can be extended to the $k$-factor GARMA process which is defined in Definition 11.8.

# Definition 11.8
If $X_t$ is a causal, stationary, and invertible process satisfying

$$\phi(B) \prod_{i=1}^{k} (1-2u_iB+B^2)^{\lambda_i}(X_t-\mu)=\theta(B)a_t \quad (11.20)$$

where $\phi(z)$ and $\theta(z)$ share no common factors, then $X_t$ is a $k$-factor GARMA process. In Theorem 11.7 we give the stationary, long memory, and invertibility conditions for a $k$-factor GARMA process.

# Theorem 11.7
- 1. $X_t$, in Equation 11.20 is causal, stationary, and invertible if $u_i$ and $\lambda_i$ ($i=1,...,k$) satisfy the conditions in Theorem 11.5(1) and all roots of the equation $\phi(z)=0$ and $\theta(z)=0$ lie outside the unit circle.
- 2. The spectrum of a causal, stationary, and invertible $k$-factor GARMA process is given by

$$P(f) = \sigma_\eta^2 \frac{|\theta(e^{-i2\pi f})|^2}{|\phi(e^{-i2\pi f})|^2} \prod_{j=1}^{k}[4(\cos 2\pi f - u_j)^2]^{\lambda_j}. \quad (11.21)$$

- 3. A process $X$, satisfying the conditions in (1) is also long memory if $\lambda_j>0$ for any $j=1,...,k$.

Proof: See Woodward et al. (1998) and Giraitis and Leips (1995).

# EXAMPLE 11.7: 2-FACTOR GEBAUER AND 2-FACTOR GARMA PROCESSES

- 1. Figure 11.10a shows a realization of length $n=500$ from 2-factor Gegenbauer model $(1-1.8B+B^2)^{0.45}(1+1.6B+B^2)^{0.3} X_t = a_t, \quad (11.22)$ with $\sigma_\eta^2=1$, and Figure 11.10b shows the first 100 observations to show more detail. The $G$-frequencies associated with $u_1$ and $u_2$ are $f_G=0.07$ and $f_G=0.4$, respectively, and in Figure 11.10b it can be seen that there is low-frequency and high-frequency periodic behavior in the data. Figure 11.10c shows the true autocorrelations which have a slowly damping sinusoidal behavior associated with the low-frequency G-frequency ($f_G=0.07$). Little evidence of the higher G-frequency behavior is seen in the autocorrelations. Figure 11.11d shows the estimated spectral density function (using a Parzen window on the data in Figure 11.1a) which shows two peaks at about 0.0 and 0.4.

- 2. Figure 11.11a shows a realization of length $n=500$ from 2-factor GARCH model $(1-0.9B)(1-1.8B+B^2)^{0.45}(1+1.6B+B^2)^{0.3}X_t=a_t,$ where $\sigma_\eta^2=1$. Figure 11.11b shows the first 100 observations. In both realizations, the wandering behavior induced by the (AR) factor $1-0.9B$ can be seen, Figure 11.11b shows low-frequency and high-frequency periodic behaviors. Figure 11.11c shows the true autocorrelations which display a slowly damping sinusoidal behavior associated with the lower G-frequency ($f_G=0.07$) under a damped exponential path induced by $1-0.9B$. Again, little evidence of the higher G-frequency behavior is seen in the autocorrelations. Figure 11.11d shows the estimated spectral density.

### 11.10
- (a) Realization of length $n=500$ from 2-order Gegenbauer model in Equation 11.22, (b) first 100 points in (a), (c) true autocorrelations for the model in Equation 11.22, and (d) Parzen spectral estimator for data in (a).

### FIGURE 11.11
- (a) Realization of length $n=500$ from 2-factor GARMA model in Equation 11.23, (b) first 100 points in (a), (c) true autocorrelations for the model in Equation 11.22, and (d) Parzen spectral estimator for data in (a).

# 11.4.1 Calculating Autocovariances

The autocorrelation function of a Gegen process with $u=1$ (i.e., a fractional model) is given in Theorem 11.4(5)(a), and the autocorrelation for a Gegen process with $u=-1$ is given in Theorem 11.4(5)(b). No simple closed form expression for the autocovariance or autocorrelation exists for a Gegen process with $|u| < 1$, but from Equation 2.7 it follows that

$$\gamma_k = \sigma_a^2 \sum_{j=0}^{\infty} \Psi_{j+k}$$

$$\sigma_a^2 \sum_{j=0}^{\infty} C_j^{(\lambda)}(u)C_{j+k}^{(\lambda)}(u). \quad (11.24)$$
