# Forecasting

the persistent trending behavior in realizations of Equation 6.45, forecasts predict that near future trending behavior is likely to reflect the immediate past, but forecasts of $X_{t+l}$ for $l$ reasonably large are very unreliable. The forecast limits in Figure 6.7 reflect the lack of certainty that the trending behavior will continue as predicted.

It should be noted that the more general ARIMA(p,2,q) model

```
$\phi(B)(1-B)^2(X_t, \mu) = \theta(B)_a,$
```

will forecasts for this case, the eventual forecast function is a straight line. In this case, the stationary AR and MA components in the model will have a bearing on the forecasts for small times and the slope of the eventual forecast function.

**Using R**: To obtain forecasts from a nonstationary ARUMA model, you can use the tswage function `for.arima.wge`. The nonstationary components can be obtained by factors $(1-B)^d$ where $d$ is a positive integer, seasonal factors, specified by $s$ (discussed in Section 6.9), and other nonstationary components entered using the vector $\lambda$. See Appendix 6B.

# 6.9 Forecasts Using Multiplicative Seasonal ARUMA Models

In this section, we briefly explain the forecasting technique for ARUMA models discussed in Section 6.8 to the more general case of the nonstationary multiplicative seasonal model

```
$\phi(B)\lambda(B^s)\Lambda(B^s)(X_t - \mu) = \theta(B)\Theta(B^s)_{a_t}, \quad (6.47)$
```

where the roots of $\phi(z) = 0, \Phi(z) = 0, \theta(z) = 0$, and $\Theta(z) = 0$ all lie outside the unit circle, while the roots of $\lambda(z) = 0$ and $\Lambda(z) = 0$ lie on the unit circle. We let

```
$\phi^{(s)}(B) = \phi(B)\lambda(B^s)\Lambda(B^s)$
```

so that $\phi^{(n)}(B)$ is a $(p+d+P_s+D)$-th order operator with coefficients, $\phi_1^{(n)}, \phi_2^{(n)}, \dots, \phi_{p+d+P_s+D}^{(n)}$. Viewing Equation 6.47 as a list of stationary models whose roots of the characteristic equation approach the roots associated with the nonstationary components of Equation 6.47, we obtain a forecast equation analogous to Equation 6.36.

EXAMPLE 6.6: FORECASTS FROM A BASIC SEASONAL MODEL

Consider the simple nonstationary seasonal model

```
$(1-B^s)(X_t - \mu) = a_t, \quad (6.48)$
```