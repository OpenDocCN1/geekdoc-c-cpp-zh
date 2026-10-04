
# ARMA Time Series Models

```
$f_0 = \frac{1}{2\pi} \cos^{-1} \left(\frac{1.6}{2\sqrt{-\phi_2}}\right) \quad (3.71)$
```

Therefore, if $\phi_2 = -1$, the associated frequency is $f_0 = 0.1024$.
Notice that changing $\phi_1$ in Equation 3.71 while keeping $\phi_2 = 1.6$ fixed, changes the associated system frequency. For the AR(2) models in Equation 3.70, we obtain $f_0 = 0.05, 0.09$, and $0.10$ for $\phi_0 = -0.7, -0.9$, and $-0.98$. The strong periodic nature of the autocorrelations is clear when $\phi_2$ is close to $-1$, and in this example, it diminishes as $\phi_2 \to -0.7$. Realizations of length $n = 200$ from Equation 3.70 are shown in Figure 3.13, where the effects of the differing autocorrelation structures can be seen. Specifically, as $\phi_2 \to -1$ the periodicity becomes more apparent in the realizations, the period becomes shorter, and the process variance increases. In Figure 3.14, the corresponding spectral densities are displayed where it is seen as $\phi_2 \to -1$, the peak of the spectral density becomes sharper.

As discussed previously, the AR(2) process $(1 - \phi_1 B - \phi_2 B^2)X_t = a$, has complex roots if only $\phi_1^2 + 4\phi_2 < 0$. Therefore, it is necessary that

![](img/41dcbfb9af56fa48895afde322197b0b_131_0.png)

![](img/41dcbfb9af56fa48895afde322197b0b_131_1.png)

FIGURE 3.13
Realizations from the AR(2) models $X_t - 1.6X_{t-1} - \phi_2 X_{t-2} = a_t$, (a-c) $\phi_2 = -0.7, -0.9, -0.98$.

# Applied Time Series Analysis with R

![](img/41dcbfb9af56fa48895afde322197b0b_132_0.png)

FIGURE 3.14
Spectral densities of the AR(2) models $X_t - 1.6X_{t-1} - \phi_2X_{t-2} = a_t (a - c) \phi_2 = -0.7, -0.9, -0.98$.

$\phi_2 < 0$ in order for the process to have a characteristic equation with complex roots. However, for negative $\phi_2$, $\phi_2 = -(a^2 + b^2)^{-1}$, the process is nonstationary with roots on the unit circle and if $\phi_2 = -1$. The behavior shown in this example as roots approach the unit circle is cyclical.

One final comment about AR(2) models associated with complex roots of the characteristic equation is that if the system frequency is sufficiently removed from 0 or 0.5, the spectral density will have a peak at $f_0 = \frac{1}{2\pi}\cos^{-1}\left(\frac{\phi_1}{2\sqrt{-\phi_2}}\right)$
(see Example 3.20). It is interesting to note that $f^* \neq f_0$ as $\phi_2 \to -1$, then $f^* \to f_0$. That is, the peak in the spectral density occurs at a frequency close to but not equal to the system frequency $f_0$.

## EXAMPLE 3.7

Figure 3.15a (set lynx in tswge) shows the annual number of the Canadian lynx trapped in the Mackenzie River District of North Canada for the period 1821–1934. Figure 3.15b shows the log data (base 10) of the annual numbers trapped, and this log data is a classical data set that has been analyzed by many authors. These data interested researchers because of the pseudo-periodic behavior with cycle lengths about 10 years. For example Tong (1977), Bhansali (1979), and Woodward and Gray (1983). Also shown in Figure 3.15b and c is the

# ARMA Time Series Models

![](img/41dcbfb9af56fa48895afde322197b0b_133_0.png)

![](img/41dcbfb9af56fa48895afde322197b0b_133_1.png)

![](img/41dcbfb9af56fa48895afde322197b0b_133_2.png)

FIGURE 3.15
(a) Number of lynx, (b) natural log of the data in (a), (c) sample autocorrelations of the data in (b), and (d) Parzen spectral density estimate of the data in (b).

sample autocorrelations and the Parzen spectral density estimate of the log lynx data. This shows the 10-year cycle of the data. The log of the lynx data is usually used for analysis because it makes the peaks and troughs of the cycles behave in similar manners, and is more AR-like. If an AR(2) model is fitted to the data (we will discuss alternative models in later chapters) then the fitted model is $X_t - \phi_1X_{t-1} + 0.75X_{t-2} = a_t$, which has system frequency $f_0 = 0.10$. Also, the sample autocorrelations have the appearance of a damped sinusoid with period of about 10, and the spectral density estimate of Figure 3.15 has a peak at about $f=0.10$.

## 3.2.8 Summary of AR(1) and AR(2) Behavior

Before proceeding to further examination of general AR(p) models, we summarize the information about AR(1) and AR(2) models

- 1. Facts about the stationary AR(1) model $X_t - \phi_1X_{t-1} = a_t$. In this case, the characteristic equation is given by $1 - \phi_1z = 0$, so that the root, $r_1$, of the characteristic equation is given by $r_1 = \phi_1^{-1}$. As a consequence, an AR(1) process is stationary if and only if $|\phi_1| < 1$. It is instructive to

# Applied Time Series Analysis with R

note that since $|\eta_1^{-1}|=\phi_1$, the proximity of the root to the unit circle be determined by simple examination of $\phi_1$.

- a. The autocorrelation function of a stationary AR(1) process is given by $\rho_k=\phi_1^k$ for $k\ge0$, that is, Equation 3.49, $C_1=1$ and $\eta_1=\phi_1^2$. The autocorrelation function is damped exponential if $\phi_1>0$ and an oscillating exponential if $\phi_1<0$.

- b. As a result of the autocorrelations in (a), realizations from an AR(1) model with $\phi_1>0$ tend to be aperiodic with a general “wandering”. When $\phi_1<0$ the realizations will tend to oscillate back and forth the mean.

- c. The spectral density $S_X(f)$ has a peak at $f=0$ if $\phi_1>0$ and at $f=0.5$ if $\phi_1<0$.

- 2. Facts about a stationary AR(2) model $X_t-\phi_1X_{t-1}-\phi_2X_{t-2}=a_t$. In this case, the characteristic equation is $1-\phi_1z-\phi_2z^2=0$, and the features of the AR(2) process depend on the nature of the roots of this quadratic equation.

Case 1—The roots of the characteristic equation are complex: From Equation 3.61, it follows that $|\eta_1^{-1}|=\sqrt{-2}$ where $r_v, k=1,2$ are conjugate roots of the characteristic equation. This provides a useful measure of how close complex roots are to the unit circle.

- a. In the complex roots case, the general solution in Equation 3.49 is satisfied by $\rho_k$ has two, $C_2=C_1^*$ and $\eta_2=\eta_1^*$, where $z^*$ denotes the complex conjugate of $z$. The autocorrelation function is a damped sinusoidal of

```
$\rho_k=d(\sqrt{-\phi_2})^k\sin(2\pi f_0k+\psi)$
```

where $d$ and $\psi$ are real constants and system frequency $f_0=\frac{1}{2\pi}\cos^{-1}(\frac{\phi_1}{\sqrt{-\phi_2}})$,

- b. As a result of (a), if the roots of the characteristic equation are close to the unit circle, then realizations from an AR(2) model in this case are pseudo-cyclic with frequency $f_0$ given in (a), that is, with period $1/f_0$

- c. If the system frequency is sufficiently removed from 0 or 0.5, spectral density will have a peak near $f_0$ given in (a).

Case 2—The roots of the characteristic equation are real: In this case roots, $r_1$ and $r_2$, of the characteristic equation are real, and the characteristic equation factors as $(1-r_1^{-1}z)(1-r_2^{-1}z)=0$. Plots of $\rho_k$ will have the appearance of a damped exponential, damped oscillating exponentials, or a mixture of damped exponentials and oscillating exponentials. Realizations from these models will have a mixture of the

# ARMA Time Series Models

behaviors induced by their autocorrelations. Depending on the signs of $r_i$ and $r_j$, the spectral density will have peaks at $f=0$, at $f=0.5$, or at both $f=0$ and $f=0.5$.

## 3.2.9 AR(p) Model

The general behavior of the autocorrelation function (and to a large degree the time series itself) of an AR(p) model can be understood by examining the roots of the characteristic equation. The information summarized earlier for the AR(1) and AR(2) models provide valuable information concerning the characteristics of higher-order AR(p) models. We begin our discussion of AR(p) models by considering two examples.

### EXAMPLE 3.8: AN AR(3) MODEL WITH A POSITIVE REAL AND COMPLEX CONJUGATE ROOTS

Consider the AR(3) model

```
$X_t - 2.55X_{t-1} + 2.42X_{t-2} - 0.855X_{t-3} = a_t.$
```

For this model, the characteristic polynomial $1-2.55z+2.42z^2-0.855z^3$ can be factored as $(1-0.95z)(1-1.6z+0.9z^2)$, that is, as the product of a linear and an quadratic factor. It follows that the roots of the characteristic equation are $r_1=1/0.95=1.05$ along with the pair of complex conjugate roots $0.89\pm 0.57$. For each of the three roots of the characteristic equation, we have $|r^{-1}|=sqrt{0.9}$. Based on the factorization of the characteristic equation, it is often useful to write the model in Equation 3.73 in the factored form

```
$(1-0.95z)(1-1.6z+0.9z^2)X_t = a_t.$
```

From our discussion of AR(1) and AR(2) models, we know that an AR(1) model based on the first factor in Equation 3.74, that is, the model $(1-0.95B)y_t=a_t$, has (a) realizations displaying a wandering or piecewise behavior as seen in Figure 3.5a, (b) autocorrelations that are damped exponentials as seen in Figure 3.4a, and (c) a peak in the spectral density at $f=0$ since the roots of $1-1.6z+0.9z^2$ are complex, it follows from Equation 3.63 that an AR(2) model based on the second-order factor, $1-1.6B+0.9B^2$, will have: (a) realizations that are pseudo-periodic with period of about 11 (1/0.9), (b) autocorrelations with a damped sinusoidal behavior, and behavior. These behaviors are seen in Figures 3.12b, and 3.14b, respectively.

In Figure 3.16, we show a realization of length $n=200$, where $\sigma_a^2=1$, true autocorrelations, and the spectral density for the AR(3) model given in Equation 3.73. The data in Figure 3.16 is stored in dataset fig3.16a in tswge. The AR(1) and AR(2) behaviors are evident in the factored form in Equation 3.74 in the realization we see
