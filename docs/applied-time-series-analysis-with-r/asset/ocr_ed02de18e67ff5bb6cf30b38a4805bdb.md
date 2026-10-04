# ARMA Time Series Models

Using R: For a given AR(p) model, you can obtain a factor table using the tswge factor.wge. This function will factor an m order polynomial into its first order and irreducible second order factors. Again, be-ful with the signs. See Appendix 3B for more details.

# EXAMPLE 3.12: AN AR(4) MODEL

Consider the AR(4) process given by

```
$X_i - 1.15X_{i-1} + 0.19X_{i-2} + 0.64X_{i-3} - 0.61X_{i-4} = a_i.$
```

Although inspecting the coefficients in Equation 3.81 tells us nothing about the nature of the model, much can be learned by examining the factors. The characteristic polynomial can be factored

```
$\phi(z) = 1 - 1.15z + 0.19z^2 + 0.64z^3 - 0.61z^4$
$= (1-0.95z)(1-z+0.8z^2)$
```

Information concerning the factors of $\phi(z)$ is given in the factor table Table 3.3. Since $|r_1|<1$ for all roots, the model is causal and stationary. The factor table shows a complex pair of roots. The positive root is associated with damped exponential autocorrelations, wandering behavior in the realizations, and a peak in the spectral density at $f=0$. The negative root produces oscillating damped autocorrelations, oscillating behavior in realizations, and a peak in the spectral density at $f=0.5$. The complex conjugate roots are related to damped sinusoidal behavior in the autocorrelations with a system frequency (using Equation 3.63) of $f=0.16$, pseudo-periodic behavior in the data with periods of about 6 (i.e., 1/06), and a peak in the spectral density at $f=0.16$.

In Figure 3.18, we show a realization of length $n=200$ where $\sigma_\epsilon^2=1$, autocorrelations, and the spectral density for the AR(4) model in Equation 3.8. The realization in Figure 3.18a is stored in data set

# TABLE 3.3
Factor Table for the AR(4) Model in Example 3.12

| AR Factors | $|r_1|$ | $f_{sj}$ |
|---|---|--|
| $1 - 0.95B$ | 0.95 | 0 |
| $1 - 0.8B^2$ | $0.62 \pm 0.93i$ | 0.90 | 0.16 |
| $1 + 0.8B$ | $-1.25$ | 0.80 | 0.5 |