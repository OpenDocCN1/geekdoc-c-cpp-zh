(lower right figure) has a frequency f = 0.15 (period = 6.67). The autocorrelations (see Exercise 1.11) and spectrum for X(t) in Equation 1.35 are given in Figure 1.15. It is crystal clear from the spectrum in Figure 1.15b that the frequency content is entirely concentrated at the frequencies 0.025, 0.1, and 0.15. Certainly, the spectrum does a much better job of displaying the underlying frequency content of the data than can be obtained by simple examination of the autocorrelations in Figure 1.15a or the realization in the top left of Figure 1.10. We usually plot the spectrum or the spectral density as a function of f in order to examine their characteristics. A peak in the spectrum or spectral density is indicative of the presence of cyclic behavior in the data at the associated frequency. In discrete parameter data, which we will typically analyze in this book, the peaks will not be of the “spiked” nature of Figures 1.14 and 1.15, but will be broader, indicating additional frequency content near the peak. This is illustrated in the following example.

![](bbox=[0.22, 0.48, 0.75, 0.68])

# FIGURE 1.15

(a) Autocorrelations and (b) spectrum for X(t) in Equation 1.35.

# EXAMPLE 1.8: A SIGNAL CONTAINING TWO DOMINANT FREQUENCY COMPONENTS

In Figure 1.16a (data set fig1.16a in tswge), we show a realization of length 250 where it is clear that the data have a pseudo-periodic behavior with a period of about 25 (there are about 10 cycles in the realization of 250 time points). Also apparent is a higher frequency component indicated by the “jagged” behavior. Figure 1.16a is a realization from an AR model of order 4 (we will discuss these in