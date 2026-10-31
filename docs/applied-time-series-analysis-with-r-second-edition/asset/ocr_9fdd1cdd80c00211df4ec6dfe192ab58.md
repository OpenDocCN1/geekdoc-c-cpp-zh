are more discernible in such a plot, and 10 log₁₀ Sₓ(f) puts the ordinate axis in units of decibels (dB), which is the standard unit for measuring acoustical energy and is thus widely used in engineering.

# 1.6 Estimating the Power Spectrum and Spectral Density for Discrete Time Series

Estimation of the power spectrum and spectral density from data can be a challenging problem, and there are a variety of estimation techniques in the literature. We will briefly introduce the topic here but will come back to it in later chapters. Given the spectrum in Equation 1.29 for a discrete parameter time series, it seems that a natural estimator for the spectrum could be obtained by simply substituting the sample autocovariances discussed in Section 1.4 into Equation 1.29. The resulting estimator is called the *sample spectrum* and is defined in Definition 1.14.

# Definition 1.14

Let Xₜ be a discrete stationary time series defined on the integers. The sample spectrum based on a realization of length n from this time series is given by

$$\hat{P}_X(f) = \hat{\sigma}_X^2 + 2 \sum_{k=1}^{n-1} \hat{\gamma}_k \cos(2\pi f k),$$ (1.36)

for |f| ≤ 0.5. The sample spectral density is given by

$$\hat{S}_X(f) = 1 + 2 \sum_{k=1}^{n-1} \hat{\rho}_k \cos(2\pi f k),$$ (1.37)

The limit, n − 1, on the sum is reasonable, since sample autocovariances and autocorrelations for k ≥ n are defined to be zero.

A related estimator is the *periodogram* that is simply the sample spectrum evaluated at the harmonics of the *fundamental frequency* f₁ = 1/n. Specifically,