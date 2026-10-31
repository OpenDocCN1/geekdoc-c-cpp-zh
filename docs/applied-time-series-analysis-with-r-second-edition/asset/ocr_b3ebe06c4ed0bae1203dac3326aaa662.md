\hat{\phi}(B)Y_t = \hat{\theta}(B)Z_t,

where Z_t is white noise, \hat{\phi}(B) \approx \hat{\theta}(B) (but \hat{\phi}(B) \neq \hat{\theta}(B)), and the roots of \hat{\phi}(z) = 0 are very near the unit circle.

Figure 4.4 shows realizations of length n = 200 from the ARMA(2, 2) process

(1 − 1.72B + 0.99B²)X_t = (1 − 1.37B + 0.72B²)a_t, (4.16)

and of the harmonic signal-plus-noise model

Y'_t = 3.57cos(2πt/12 + ν) + Z_t, (4.17)

where a_t and Z_t are both N(0, 1) white noise and σ_X² = σ_Y² = 7.4. The two realizations are similar, but the amplitudes associated with the ARMA(2, 2) realization are more variable than those for the signal-plus-noise model. In Table 4.1, we see the factor table for the ARMA(2, 2) model in Equation 4.16 where it can be seen that the AR and moving average factors have very similar system frequencies (0.08 and 0.10). The spectral density for the signal-plus-noise model in Equation 4.17 is a single spike at f = 0.083 along with a flat spectrum at other frequencies associated with the white nose. In Figure 4.5a, we show the spectral density for the ARMA(2, 2) model in Equation 4.16, and it can be seen that there is a sharp peak at about f = 0.08. In Figure 4.5b, we show the spectral density associated with the AR(2) model (1 − 1.72B + 0.99B²)X_t = a_t. This spectral density also has a peak at about f = 0.08, but the difference between Figure 4.5a and b is that the peak in Figure 4.5a is sharper with less frequency content near the peak frequency. In Figure 4.5c, we show the spectral density for the MA(2) model X_t = (1 − 1.37B + 0.72B²)a_t. This spectral density has a dip at about f = 0.1. The effect of the moving average component of the ARMA(2, 2) model in Equation 4.16 is to reduce the frequency content in a neighborhood just to the right of f = 0.08 causing the sharp, nearly spike-like peak in the ARMA(2, 2) spectral density in Figure 4.5a. In Figure 4.5d, we fit a high-order AR(p) model with p = 7 to model the data in Figure 4.4a. It can be seen that the peak is quite