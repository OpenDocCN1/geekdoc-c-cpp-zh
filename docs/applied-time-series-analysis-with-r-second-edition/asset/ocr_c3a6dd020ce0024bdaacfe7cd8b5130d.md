factor $1 - 0.8B$ weakened the behavior of the AR factor $1 - 0.95B$ in the ARMA(1,1) model in [Equation 3.90]. We use the term “system frequencies” to indicate the frequencies displayed in the factor table whether the factor is an AR or MA factor. Examples 3.17 and 3.18 further illustrate the use of factor tables to aid the understanding of ARMA$(p,q)$ models.

# EXAMPLE 3.17: AN ARMA(2,1) MODEL

Consider the ARMA(2,1) model given by

$$(1 - 1.6B + 0.9B^2)X_t = (1 - 0.8B)a_t. \tag{3.93}$$

Recall that autocorrelations, a realization (based on $\sigma_a^2 = 1$) and the spectral density for the AR(2) model $(1 - 1.6B + 0.9B^2)X_t = a_t$ were given in [Figures 3.12b, 3.13b, and 3.14b]. In [Table 3.6], we show the factor table for the model in [Equation 3.93], which is an ARMA(2,1) model, since all roots associated with AR and MA factors are outside the unit circle. As discussed, the effect of the MA factor $1 - 0.8B$ is to reduce frequency content at $f = 0$.

In [Figure 3.24], we show a realization (fig3.24a in tswge), autocorrelations, and spectral density for the ARMA(2,1) model in [Equation 3.93] where $\sigma_a^2 = 1$. In comparing [Figure 3.24] with [Figures 3.12b through 3.14b], we note similar behavior in the realization and autocorrelations. Both spectral densities have a peak at about $f = 0.1$, but it should be noted the spectral densities differ at and around $f = 0$. Specifically, the spectral density in [Figure 3.24c] for the ARMA(2,1) model is much lower at $f = 0$ than is the corresponding spectral density for the AR(2) model $(1 - 1.6B + 0.9B^2)X_t = a_t$. Thus, the effect of the MA factor $1 - 0.8B$ is to reduce the spectral content at $f = 0$ and cause the frequency content to be more focused about $f = 0.1$. Thus, the effect of the MA factor $1 - 0.8B$ in Examples 3.13 and 3.14 is to remove or reduce frequency behavior at $f = 0$.

# EXAMPLE 3.18: AN ARMA(4,3) MODEL

Consider the ARMA(4,3) model

$$X_t - 0.3X_{t-1} - 0.9X_{t-2} - 0.1X_{t-3} + 0.8X_{t-4} = a_t + 0.9a_{t-1} + 0.8a_{t-2} + 0.72a_{t-3}. \tag{3.94}$$