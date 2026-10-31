shown in Figure 3.15b where it can be seen that the asymmetry is largely removed. Figure 3.15c and d shows the sample autocorrelations and the Parzen spectral density estimate of the log-lynx data where the cyclic behavior of about 10 years is apparent in both plots. A feature to note about the sample autocorrelations is their slowly damping behavior.

We used a simple AR(2) model for the log-lynx data in Example 3.7, but the AR model typically used to model the log-lynx data is the AR(11) model

$(1 - 1.138 B + 0.51 B^2 - 0.238 B^3 + 0.29 B^4 - 0.148 B^5 + 0.14 B^6 + 0.148 B^7 - 0.08 B^8 + 0.04 B^9 - 0.13 B^{10} - 0.19 B^{10} + 0.31 B^{11}) X_t$

proposed by Tong (1977). Also, Campbell and Walker (1977) obtained the harmonic component model

$X_t = 2.9036 + 0.3649 \cos\left(\frac{2\pi t}{9.5}\right) - 0.4866 \sin\left(\frac{2\pi t}{9.5}\right) + u_t,$

where $u_t = 1.0302 u_{t-1} - 0.3228 u_{t-2} + a_t$, and $a_t$ has zero mean and variance 0.044. Bhansali (1979) compared the models and concluded, using Priestley's (1962) $P(\lambda)$ test designed to detect harmonic behavior, that the data contained a harmonic component. However, Woodward and Gray (1983) pointed out that the factored form of the Tong model has a factor of $1 - 1.562 B + 0.967 B^2$ which has roots very close to the unit circle (the absolute reciprocal is $|r^{-1}| = 0.98$) associated with frequency $f_0 = 0.104$ (=1/9.6). Additionally they generated realizations from the AR(11) model, which does not have harmonic components, and found that the Priestley $P(\lambda)$ test usually detected “harmonic components.” The lynx data will be re-examined in Chapter 11 when we discuss cyclic long-memory behavior.

# 5.2 ARIMA(p,d,q) and ARUMA(p,d,q) Processes

The ARIMA(p,d,q) and ARUMA(p,d,q) models defined in Definition 5.1 are useful nonstationary extensions of the ARMA(p,q) model.