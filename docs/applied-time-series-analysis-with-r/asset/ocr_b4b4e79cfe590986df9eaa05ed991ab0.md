# 524

# Applied Time Series Analysis with R

coefficients $d_l$ level coefficients to estimate $\sigma$. The DWT after thresholding is shown in the right panel of Figure 12.11 where it can be seen that only of the 128 + 64 + 32 = 224 coefficients in these three rows are retained. Note that the DWT after thresholding is quite similar to the DWT of the underlying smooth bumps signal shown in the right panel of Figure 12.8. The smoothed signal is reconstructed from the thresholded DWT using Equation 12.24 and is shown at the top right of Figure 12.11.

**Using R:** The wavelet smoothing in Figure 12.11 was done using universal.tmooth in the waveslim CRAN package. See Appendix 12B for more details.

# 12.3.8 Scalogram: Time-Scale Plot

Considering the data vector $x$ as a time realization, the wavelet representation at time $t$ assigns "large" values of $d_{j,k}$ when the corresponding $\psi_{j,k}$ has "frequency" behavior similar to that of the realization in the vicinity of time $t$. The discrete scalogram or time-scale plot is a time–frequency plot similar to those in Figures 12.3 and 12.4 where the horizontal axis represents time, $t$, and the vertical axis represents the "frequency" measure in the discussion Example 12.1 it was noted that we use 1/scale as measure of "frequency". In the DWT $d_{j,k}$ are coefficients that correspond to $\psi_{j,k}$ for $j=1, \dots, J$ where $j \leq J_0$ and $n = 2^J$. The support of $\psi_{j,k}$ is of width $2^j$, the Haar mother wavelet is of length 1 and thus it follows that in the DWT setting, 1/scale reaches an upper limit of 1 instead of 0.5 as is the case for standard frequency measure. In general it is useful to associate a 1/scale value of $u$ with a frequency of $u/2$.

The third dimension in the scalogram is a gray scale where the value of $d_{j,k}$ is plotted on the rectangle

![](bbox=[0.398, 0.646, 0.602, 0.693])

and $\hat{s}_{j,k}$ is plotted on the rectangle.

![](bbox=[0.428, 0.732, 0.572, 0.78])

Figure 12.12a shows a template for the time-scale plot for the case $n=16$ and $J_0=4$. The value $\hat{s}_{2,1}$ is plotted on the rectangle of height $2^{-4}=0.0625$ and width 16 at bottom of the time-scale plot. This rectangle is shown at the bottom of Figure 12.12a. Sitting on top of this rectangle is a rectangle of the same dimensions in which the value $\hat{d}_{4,1}$ is plotted. The gray scale of this rectangle (darker indicates larger $\hat{d}_{4,1}$) is a measure of the detail in the data of duration about $2_4=16$ time points. The value of $\hat{d}_{4,1}$ is plotted on