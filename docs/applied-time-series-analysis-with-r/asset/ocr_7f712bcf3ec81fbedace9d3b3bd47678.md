# Model Building

# 391

![](bbox=[0.121, 0.121, 0.483, 0.296])

![](bbox=[0.517, 0.121, 0.879, 0.296])

![](bbox=[0.121, 0.317, 0.483, 0.492])

![](bbox=[0.517, 0.317, 0.879, 0.492])

Figure 9.8
Realizations (a–d) from the AR(2) model in Equation 9.16 fit to the sunspot data.

do not satisfy the physical constraint that sunspot numbers are nonnegative. For reason, you might conclude that neither model is adequate. Refer to Tong (1990) for nonlinear models for the sunspot data.

Regardless of the issue regarding the need for a nonlinear model, suppose that we want to fit an ARMA model to the sunspot data and have decided to choose between the AR(2) and AR(9) models given above. It appears that the realizations in Figure 9.9 from the AR(9) model tend to have more consistent 10-11 year cycles (similar to the sunspot series), but only the realization in Figure 9.9b is reasonably close in appearance to the sunspot data. In Figure 9.10a, we see sample autocorrelations for the sunspot data (bold) and for the four realizations in Figure 9.8. It can be seen that the sample autocorrelations for the generated realizations decay out more quickly than for the sunspot data, and the first damped cycle differs from 10 to 11 lags. Figure 9.9b, we show sample autocorrelations for the realizations from the AR(9) model in Equation 9.17, and there can be seen that autocorrelations from these realizations are very similar in appearance to those of the sunspot data. Figure 9.11 shows spectral density estimates using a Parzen window with M=32 for the sunspot data (bold) and for the realizations in Figures 9.8 and 9.9 from models in Equations 9.16 and 9.17, respectively. The peaks in spectral densities in Figure 9.10a for the realizations from the AR (2) model tend to not be as sharp as the peaks for the sunspot data. Also, there is no consistency there for the spectral