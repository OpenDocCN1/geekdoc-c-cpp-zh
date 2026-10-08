function is altered to include the next lobe zero-crossings. This produces a residual for correcting four samples on each window size but keeping the same length, the zero crossings are now on two-internal boundaries). Figure 5.13 (a) shows a rectangularly windowed sinc() pulse, while Figure 5.13 (b) shows the resulting BLEP edge, and Figure 5.13 (c) shows the resulting residual.

Figure 5.12: (a) The trivial sawtooth spectrum reveals massive aliasing (b) the two-point BLEP corrected suppresses most of the aliasing, pushing the components below -60 dB and off the plot; $f_0=440$ Hz.

Figure 5.13: (a) a wider rectangular window extracts the central pulse and next pair of lobes (b the resulting BLEP edge after integrating) and (c) the BLEP residual.

![](bbox=[0.375, 0.035, 0.905, 0.55])

We can now experiment with widened window and generate a set of BLEP tables with varying applied to see how the windowing affects the aliasing as well as distorts the desired sawtooth spectrum. Figures 5(a)-(e) shows the resulting spectra when a variety of window functions are applied. If you are not using RackAFX, then you will need to use a third party FFT analyzer to test the implementation in this chapter. In Figure 5.14 (a) the rectangular shaped windowing introduces aliasing components that are wider but lower in amplitude than the two-point version in Figure 5.12; aliasing components near are much more suppressed.

![](bbox=[0.375, 0.56, 0.905, 0.68])

These widened versions of the BLEP residuals are also prepackaged for use in synth.h as the following arrays (all 4096 points):

+   - dBLEPTable_8_RECT
- dBLEPTable_8_TRI
- dBLEPTable_8_HANN
- dBLEPTable_8_HAMM
- dBLEPTable_8_BLHKAR
- dBLEPTable_8_WELCH

Our oscillators will default to the original two-point version without interpolation between lookup tables. You may easily alter this in the BLEP function described later; you may also generate and then test your own BLEP tables using the BLEP function. In the rest of the chapter, "two-point" refers to the one-point-side BLEP correction from the last section. "Eight-point BLEP" refers to the widened transition region version with four points per