# Applied Time Series Analysis with R

then $P_V(f) = P_W(f)$. Using this fact, we see that $\gamma_X(k) = \int_{-0.5}^{0.5} e^{2\pi itk} P_X(f)$ by defi-nnition, and $\gamma_X(k) = \int_{-0.5}^{0.5} e^{2\pi itk} \sum_{j=-\infty}^{\infty} h_j e^{-2\pi ijf} P_Z(f) df$ from the preceding calcula-ns. So, it follows that

```
$P_X(f) = \sum_{j=0}^{\infty} h_j e^{-2\pi ijf} P_Z(f).
```

# Appendix 2B: R Commands

# 2B.1 R Commands

butterworth.wge(x,order,type,cutoff) is a tswge R function that requires functions in the CRAN package signal which should be installed on your machine before calling butterworth.wge.

x is a vector containing the time series realization $x_t, t=1, \dots, n$ order is the order of the Butterworth filter you want to use (default = 4) type should be either "low", "high", "pass", or "stop" for a low-pass, high-pass, band-pass, or stop-band (notch) filter, respectively.

cutoff

+   - if type = "high" or "low" then cutoff is the scalar cutoff frequency
- if type = "stop" or "band" then cutoff is a 2-component vector containing the lower and upper cutoff frequencies

Example: The data sets wages is contained in 'tswge'. The tswge R com-m to perform the lowpass filter described in Example 2.4 are

```
wages05 = butterworth.wge(wages,order=4,type="low",
cutoff=0.05)
```

The filtered data is wages05$x.filt.

# EXERCISES

The following data sets include the use of the butterworth.wge function along with commands given in Appendix 1B for generating realizations from a signal-plus-noise model and for plotting spectral estimates.

# Applied Problems

2.1 Generate a realization of length $n=100$ from the signal-plus-noise model in Problem 1.6.