
# Wavelets

# 521

![](img/41dcbfb9af56fa48895afde322197b0b_537_0.png)

FIGURE 12.10
(a) Left panel: MRA for bumps signal using Haar wavelet. (b) Right panel: MRA for bumps signal using the Daubechies(4) wavelet.

for j > 1. The panels on the left of Figure 12.9 illustrate an MRD while the right panel shows an MRA. See Ogden (1997).
The MRA in the right panel of Figure 12.9 provides a visualization of the fact that the wavelet approximations, $S_j$, can be seen as output of lowpass filters applied to the original data. The quality of the associated filter can depend on the wavelet selected. The MRD and MRA in Figure 12.9 are based on the relatively smooth bumps signal using Symlet(8) wavelet. In Figure 12.10 (left panel) we show the MRA of the bumps signal using the Haar wavelet, and Figure 12.10 (right panel) shows the MRA on the Daubechies(4) wavelet. While each of these wavelets eventually reproduces the data (in $S_j$), the preceding 'filtered versions' show the behavior of the underlying wavelets. For example, the Haar version is 'blocky' and the Daubechies(4) version shows vestiges of the fine shift. For the purpose of approximation, a relatively smooth wavelet (such as the Symlet(8)) is best applied to a signal that is relatively smooth (as is the bumps signal). However, Donoho and Johnstone (1994) show a 'blocks' signal for which the Haar wavelet is preferable. See also Bruce and Gao (1996).

**Using R:** The computations to generate Figures 12.6 through 12.9 were performed using dwt and mra functions in the wavethresh package in R that is available on CRAN. The actual plots were created using tswge functions plotts.dwt.wge. See Appendix 12B for more details.

## 12.3.7 Wavelet Shrinkage

Smoothing techniques have been widely used for extracting the underlying signal from a data set containing a signal buried in noise. The low-pass filters

discussed in Section 2.4 are often used for this purpose. Nonparametric statistical methods such as regression and smoothing splines, kernel smoothers, and generalized additive models become quite popular for signal extraction. For example, Wahba (1990), Hastie and Tibshirani (1990), Eubank (1999), Green and Silverman (1993), and Hart (1997).

To illustrate wavelet-based smoothing, refer back to the discussion in Example 12.4 concerning the DWT representations of the bumps and noisy signal. Starting with the noisy bumps signal (bumps signal plus noise) shown in the upper right panel of Figure 12.8, it seems reasonable that the true bumps signal would be well approximated by eliminating nearly zero wavelet coefficients in the DWT in the right panel of Figure 12.8 and reconstructing the signal. This foundation of smoothing techniques based on the DWT, for example, Donoho (1993) and Donoho and Johnstone (1994, 1995). The basic model in the wavelet domain

```
$d_{j,k} = \hat{\theta}_{j,k} + z_{j,k},$
```

where
$d_{j,k}$ is the detail coefficient calculated from the data
$\hat{\theta}_{j,k}$ is the unknown "true" detail coefficient associated with the underlying signal
$z_{j,k}$ is the zero-mean white noise with variance $\sigma_z^2$

The key idea for extracting "smooth" signals from noisy data such as the upper right frame of Figure 12.8 is that most of the $\hat{\theta}_{j,k}$ will be zero or approximately zero. Although many of the wavelet coefficients, $d_{j,k}$, of the noisy signal are nonzero, a relatively few of these nonzero $d_{j,k}$ are actually true to the true signal. The goal is to reconstruct the "signal" based on the estimates $\hat{\theta}_{j,k}$. This is typically accomplished by selecting a threshold and "zeroing-out" coefficients less than the threshold. Two thresholding techniques suggested by Donoho and Johnstone (1994) based on a positive threshold $\lambda$ are as:

Hard threshold ("Keep or Kill")

```
$$\hat{\theta}_{j,k} = 0, \quad \text{if } |d_{j,k}| \le \lambda$$
$$= d_{j,k}, \quad \text{otherwise}.$$
```

Soft threshold

```
$$\hat{\theta}_{j,k} = 0, \quad \text{if } |d_{j,k}| \le \lambda$$
$$= d_{j,k} - \lambda, \quad \text{if } d_{j,k} > \lambda$$
$$= d_{j,k} + \lambda, \quad \text{if } d_{j,k} < -\lambda.$$
```

The underlying signal is then reconstructed using the $\hat{d}_{j,k}$ as the detail coefficients.
A variety of techniques have been used for obtaining the threshold $\lambda$. One popular method is to use a single (universal) threshold, $\lambda_u$, across all levels of $j$ given by

```
$$\lambda_u = \hat{\sigma}_u \sqrt{2 \log n}, \quad (12.36)$$
```

where $\hat{\sigma}_u^2$ is an estimate of the noise variance $\sigma_n^2$. Note that $d_j$ coefficients of the DWT of the noisy signal in Figure 12.8 are almost all due to noise. This is typical for smooth signals, and consequently $\hat{\sigma}_j^2$ is often estimated using only the $d_j$ level coefficients. Donoho and Johnstone (1994) set $\hat{\sigma}_j$ to be the median of the absolute deviation (MAD) of the $d_j$ level coefficients. (The MAD of a list of numbers is the median of the absolute differences between the values in the list and the median of the list). Alternatively, separate thresholds can be calculated for each row of detail coefficients, which might be a preferable approach in the case of correlated noise.

### EXAMPLE 12.5: SMOOTHING THE NOISY BUMPS SIGNAL

The left panel of Figure 12.11 shows the noisy bumps and the DWT that was previously shown in the right panel of Figure 12.8. A universal hard threshold is applied to the first three levels of wavelet

![](img/41dcbfb9af56fa48895afde322197b0b_539_0.png)

**FIGURE 12.11**
(a) Left panel: Noisy bumps signal and DWT from right panel of Figure 12.8. (b) Right panel: Wavelet coefficients after universal hard threshold along with reconstructed smoothed noisy bumps signal (top right).

coefficients $d_l$ level coefficients to estimate $\sigma$. The DWT after thresholding is shown in the right panel of Figure 12.11 where it can be seen that only of the 128 + 64 + 32 = 224 coefficients in these three rows are retained. Note that the DWT after thresholding is quite similar to the DWT of the underlying smooth bumps signal shown in the right panel of Figure 12.8. The smoothed signal is reconstructed from the thresholded DWT using Equation 12.24 and is shown at the top right of Figure 12.11.

**Using R:** The wavelet smoothing in Figure 12.11 was done using universal.thresh in the waveslim CRAN package. See Appendix 12B for more details.

## 12.3.8 Scalogram: Time-Scale Plot

Considering the data vector $x$ as a time realization, the wavelet representation at time $t$ assigns "large" values of $d_{j,k}$ when the corresponding $\psi_{j,k}$ has "frequency" behavior similar to that of the realization in the vicinity of time $t$. The discrete scalogram or time-scale plot is a time–frequency plot similar to those in Figures 12.3 and 12.4 where the horizontal axis represents time, $t$, and the vertical axis represents the "frequency" measure in the discussion Example 12.1 it was noted that we use 1/scale as measure of "frequency". In the DWT $d_{j,k}$ are coefficients that correspond to $\psi_{j,k}$ for $j=1, \dots, J$ where $j \leq J_0$ and $n = 2^J$. The support of $\psi_{j,k}$ is of width $2^j$, the Haar mother wavelet is of length 1 and thus it follows that in the DWT setting, 1/scale reaches an upper limit of 1 instead of 0.5 as is the case for standard frequency measure. In general it is useful to associate a 1/scale value of $u$ with a frequency of $u/2$.

The third dimension in the scalogram is a gray scale where the value of $d_{j,k}$ is plotted on the rectangle

![](img/41dcbfb9af56fa48895afde322197b0b_540_0.png)

and $\hat{s}_{j,k}$ is plotted on the rectangle.

![](img/41dcbfb9af56fa48895afde322197b0b_540_1.png)

Figure 12.12a shows a template for the time-scale plot for the case $n=16$ and $J_0=4$. The value $\hat{s}_{2,1}$ is plotted on the rectangle of height $2^{-4}=0.0625$ and width 16 at bottom of the time-scale plot. This rectangle is shown at the bottom of Figure 12.12a. Sitting on top of this rectangle is a rectangle of the same dimensions in which the value $\hat{d}_{4,1}$ is plotted. The gray scale of this rectangle (darker indicates larger $\hat{d}_{4,1}$) is a measure of the detail in the data of duration about $2^4=16$ time points. The value of $\hat{d}_{4,1}$ is plotted on
