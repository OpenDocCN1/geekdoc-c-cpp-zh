# Stationary Time Series

![](bbox=[0.206, 0.122, 0.792, 0.273])

![](bbox=[0.206, 0.287, 0.792, 0.439])

+   1. The data set fig1.21a in the R package twge contains the realization of length n=250 shown in Figure 1.21a. Notice that the data and the spectral density (but not the autocorrelations) show evidence of two frequencies, a lower one at about f=0.05 and a higher frequency of about f=0.33. Find the Parzen spectral density estimate for this realization with M=31. Plot this spectral density estimate in dB (10 log10) and again without taking the logarithms. Comment on the information visible in the spectral density estimates concerning the two dominant frequencies. What impact has the logarithm (as dB) have?

+   2. Generate a realization of length n=100 from the signal-plus-noise model

$X_t = 3\cos(2\pi(0.05)t) + 1.5\cos(2\pi(0.35)t) + a(t),$

where $a$ is $N(0,1)$ white noise. For these data, plot the

Discuss cyclic features of the data that can be seen from each of the plots. Which of these plots provide the best indication of the two dominant frequencies (i.e., 0.05 and 0.35) in the data?