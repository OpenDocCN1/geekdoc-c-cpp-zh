wavelet packet coefficients “hone in” on 1/scale = 0.5 (i.e., system frequency f = 0.25) and provide best frequency localization in this region of the 1/scale axis. This is similar to the manner in which DWT coefficients focus in on lower frequencies.

![](bbox=[0.18, 0.22, 0.52, 0.48])

![](bbox=[0.58, 0.22, 0.85, 0.48])

![](bbox=[0.35, 0.51, 0.62, 0.78])

# FIGURE 12.19

(a) Realization of length n = 256 from the AR(2) model in Equation 12.37, (b) the time-scale plot based on the DWT, and (c) the time-scale plot based on the best basis algorithm for selecting the wavelet packet basis.

Computational notes: The time-scale plot based on wavelet packets that are shown here were plotted using the S-Plus Wavelets module.

# EXAMPLE 12.10: WAVELET ANALYSIS OF WHALE CHIRP DATA

Figure 12.20a (data set wha1e in tsweve) shows a plot of 256 points of a whale click echolocation signal sampled at 4.8 kHz (see Robertson et al. 2010). From the figure it can be seen that initially the data are high frequency, toward the middle of the series the data become more low frequency, while toward the end of the realization, the data become