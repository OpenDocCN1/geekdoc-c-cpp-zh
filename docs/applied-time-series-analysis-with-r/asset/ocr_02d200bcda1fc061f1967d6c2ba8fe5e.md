# Other Stationary Time Series Models

![](bbox=[0.313, 0.118, 0.686, 0.266])

**FIGURE 4.2**
True spectral density for the harmonic model in Equation 4.5 with $m = 1$.

and

$S_{\gamma}(f) = \frac{1/2 \sum_{j=1}^m A_j^2(\Delta(f-f_j) + \Delta(f+f_j))}{\sum_{j=1}^m A_j^2},

respectively. Realizations from models such as Equation 4.5 will be sinusoids and will display multiple periodicities. Similarly, a plot of the true spectral density (positive $f$) will be zero for $m$ spikes at $f_j$ $j=1,...,$. Spectra such as these are said to be discrete or line spectra as contrasted with the smooth or continuous spectra associated with ARMA($p,q$) models.

# 4.1.2 Harmonic Signal-Plus-Noise Models

We consider the signal-plus-noise model

$Y_t = \sum_{j=1}^m A_j \cos(2\pi f_j t + U_j) + N_t \n= H_t + N_t,$

for $t=0, \pm1, ...$, where $H_t$ is referred to as the harmonic component or signal and $N_t$ is a stationary noise process. In Equation 4.5, the $A_j$ and $f_j$ are constants, and the $U_j$ are uncorrelated random variables which are distributed as uniform $[0, 2\pi]$. Additionally, $H_t$ and $N_t$ are uncorrelated processes. It follows that once $Y_t$ in Equation 4.10 is a stationary process, it is the sum of uncorrelated stationary processes (see Problem 1.10).

For our purpose, we consider the case $m=1$, for which it can be shown (Problem 1.12) when $N_t$ is discrete white noise, $\gamma_h$ is given by