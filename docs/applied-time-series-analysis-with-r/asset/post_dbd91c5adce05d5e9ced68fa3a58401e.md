
## Other Stationary Time Series Models

![](img/41dcbfb9af56fa48895afde322197b0b_203_0.png)

**FIGURE 4.3** (a) Theoretical autocorrelations and (b) spectrum for the model $Y_t = 4.4\cos(2\pi t/12) + U_t + N_t$.

## 4.1.3 ARMA Approximation to the Harmonic Signal-Plus-Noise Model

We have seen that realizations from the harmonic signal-plus-noise model and ARMA($p,q$) models can be similar in nature. However, as we discussed, there are differences between the two models (4.1) and (4.2). Nevertheless, in many cases, the ARMA($p,q$) or high-order AR can serve as a very good approximation to the signal-plus-noise model. The primary differences between an ARMA model and a harmonic signal-plus-noise are the random phase and amplitude nature of ARMA realizations. However, since phase information is "Lost" in the power spectrum (and the amplitude information, random or nonrandom, is "captured" by the variance), it is not surprising that the ARMA model can serve as a good model for estimating the spectrum of harmonic signals.

### FIGURE 4.1: APPROXIMATING A HARMONIC SIGNAL-PLUS-NOISE MODEL WITH AN ARMA(2,2) MODEL

A harmonic signal-plus-noise model such as Equation 4.12 can often be well approximated by an ARMA(2, 2) model as the following development shows. Let $Y_t$ be given by Equation 4.10 with $m=1$ with $N_t = a_t$ and consider $\phi(B)Y_t$

```
$$\phi(B) = 1 - 2\cos(2\pi f_1)B + B^2.$$
```

It follows that

```
$$\phi(B)Y_t = \phi(B)(H_t + a_t)$$
$$= \phi(B)H_t + \phi(B)a_t, \quad\quad\quad (4.14)$$
```

where $H_t$ is given in Equation 4.10. But $\phi(B)H_t = 0$ (Problem 4.2) from which it follows that $\phi(B)Y_t = \phi(B)a_t$. In practice, $\phi(B)$ must be estimated, and, in place of Equation 4.14, we have

$\hat{\phi}(B)Y_i = \varepsilon_i + \hat{\phi}(B)a_i, \quad (4.15)$

where

$\varepsilon_i = \hat{\phi}(B)A_1 \cos(2\pi f_1 t + U_i).$

If $\varepsilon_i$ is sufficiently small, which it often is, then it produces only a small perturbation to $\hat{\phi}(B)a_i$ and Equation 4.14 is well approximated by

$\hat{\phi}(B)Y_i = \hat{\phi}(B)Z_i,$

where $Z_i$ is white noise, $\hat{\phi}(B) = \hat{\theta}(B)$ (but $\hat{\phi}(B) \neq \hat{\theta}(B)$), and the roots of $\hat{\phi}(z)=0$ are very near the unit circle.

Figure 4.4 shows realizations of length $n=200$ from the ARMA(2, 2) process

$(1-1.72B + 0.99B^2)Y_i = (1-1.37B + 0.72B^2)a_i, \quad (4.16)$

and of the harmonic-signal-plus-noise model

$Y_i = 3.57 \cos(\frac{2\pi}{12} + U) + Z_i, \quad (4.17)$

where $a_i$ and $Z_i$ are both $N(0,1)$ white noise and $\sigma_a^2=\sigma_v^2=7.4$. The two realizations are similar, but the amplitudes associated with the ARMA(2, 2) realization are more variable than those for the signal-plus-noise model. In Table 4.1, we see the factor table for the ARMA(2, 2) model

![](img/41dcbfb9af56fa48895afde322197b0b_204_0.png)

FIGURE 4.4

(a) Realizations from the ARMA(2, 2) in Equation 4.16 and (b) the harmonic signal-plus-noise model in Equation 4.17.

## Other Stationary Time Series Models

### TABLE 4.1
Factor Table for the ARMA(2, 2) Model in Equation 4.16

| AR factors | $r_j^{-1}$ | $f_{oj}$ |
|---|---|---|
| $1 - 1.72B + 0.99B^2$ | $0.87 \pm 0.51i$ | 0.995 | 0.08 |
| MA factors | | | |
| $1 - 1.37B + 0.72B^2$ | $0.95 \pm 0.70i$ | 0.85 | 0.10 |

In Equation 4.16 it can be seen that the AR and moving factors have very similar spectral frequencies (0.08 and 0.10). The spectral density for the signal-plus-noise model in Equation 4.17 is a single spike at $f=0.083$ along with a flat spectrum at other frequencies associated with the white noise. In Figure 4.5a, we show the spectral density for the ARMA(2, 2) model in Equation 4.16, and it can be seen that there is a sharp peak at about $f=0.08$. In Figure 4.5b, we show the spectral density associated with the AR(2) model ($1 - 1.72B + 0.99B^2)X_t = a_t$. This spectral density also has a peak at about $f=0.08$, but the difference

![](img/41dcbfb9af56fa48895afde322197b0b_205_0.png)

FIGURE 4.5
True spectral plots for (a) ARMA(2, 2) model, (b) AR(2) model, (c) MA(2) model, and (d) AR(7) model.

## Applied Time Series Analysis with R

These ideas can be extended to higher order models, and the general harmonic signal-plus-noise model of Equation 4.10 where $N_t$ is white noise can be approximated by an ARMA($2m, 2m$) process.

### EXAMPLE 4.2: TWO DATA SET WITH CYCLIC BEHAVIOR

In Figure 4.6a, we show the plot previously shown in Figure 1.1b of the Pennsylvania monthly average temperatures from January 1990 to December 2004 (partemp in tsw). Figure 4.6b is a plot of the logs of the monthly lynx trapping data previously shown in Figure 3.15b and discussed in Example 3.7.

Both plots show a cyclic behavior that could possibly be described by either a signal-plus-noise model or an ARMA(2,2), or other AR or ARMA models. We discuss models for these data in later chapters using techniques discussed in Chapters 6 through 9. Another possible model is a Gegenbauer or GARMA long-memory model which is discussed in Chapter 11.

![](img/41dcbfb9af56fa48895afde322197b0b_206_0.png)

FIGURE 4.6
(a) Pennsylvania monthly average temperatures from January 1990 to December 2004, (b) natural logs of the monthly lynx trapping data.

## Other Stationary Time Series Models

## 4.2 ARCH and GARCH Processes

In Definition 1.6 we defined white noise to be zero mean, uncorrelated, and identically distributed random variables. We have often used examples in which these random variables are also normally distributed, although this is not a requirement for white noise. However, it is not uncommon to have data for which the noise appears more variable or volatile over certain sections of the time axis than others. For example, consider the data in Figure 4.7 that shows the DOW daily rate of return from October 1, 1928 to December 31, 2010 (data set dow.rate in tswge). Clearly, the data look much more variable in some regions than others. Isolated extremes are also evident, the 1930s were a period of continuing volatility. Isolated notably on the 1929 stock market crash on October 29, 1929 and Black Monday, October 19, 1987. However, as we will see in Example 4.4 these data seem to be a type of noise, $a_t$ which the observations are uncorrelated.

For the rate of returns ($a_t, t=1, \dots, 2065$) in Figure 4.7 it appears that the conditional variance, $\sigma_{t-1}^2$ of $a_t$, given $a_{t-k}, a_{t-j}, \dots$, that is,

```
$$\sigma_{t-1}^2 = E[a_t^2 | a_{t-k}, k=1, 2, \dots], \quad (4.18)$$
```

depends on $t$. Thus, as we will see in Example 4.4, the $a_t^2$ in Figure 4.7 appear to be uncorrelated and not independent. The time series for which the conditional variance of the noise, $\sigma_{t-1}^2$, depends on $t$ is said to be *volatile*, and the conditional variance is often referred to as the *conditional volatility*.

![](img/41dcbfb9af56fa48895afde322197b0b_207_0.png)

**FIGURE 4.7** DOW Jones daily rate of return from October 1, 1928 to December 31, 2010.

## Applied Time Series Analysis with R

### EXAMPLE 4.3

If the white noise $a_t \sim N(0,\sigma_a^2)$, then both the $a_t$'s and $a_t^2$ are uncorrelated and independent. Recall that functions of independent random variables are also independent. See Casella and Berger (2001), Theorem 4.3.2. Thus, we emphasize that if the $a_t$'s are uncorrelated while the $a_t^2$ are correlated, then the $a_t$ cannot be normally distributed. Also note that it is often stressed in statistics courses that correlation is only a measure of linear correlation. This setting provides a good example of the impact of data being uncorrelated but not independent.

To illustrate this, Figure 4.8a (data set $fig4.8a$ in $tswe$) shows a realization of Gaussian (normally distributed) white noise with $\sigma_a^2=1$, and Figure 4.8b shows the sample autocorrelations for the data in (a) lags up to 50. It can be seen that, as expected, the sample autocorrelations are small and fall within 95% limit lines (which are discussed in Section 8.1). Figure 4.8c plots the squares of the data in (a). While the data in Figure 4.8c do not "look like" white noise, the original observations are independent, the squares are also independent and thus uncorrelated. The sample autocorrelations in Figure 4.8d have a similar behavior to those in Figure 4.8b and suggest that in the data in Figure 4.8c white noise.

![](img/41dcbfb9af56fa48895afde322197b0b_208_0.png)

**Figure 4.8**
(a) Normally distributed white noise, (b) sample autocorrelations for the data in (a), (c) squares of the data in (a), and (d) sample autocorrelations of the data in (c).
