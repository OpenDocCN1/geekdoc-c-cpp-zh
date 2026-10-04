# Applied Time Series Analysis with R

![](bbox=[0.313, 0.131, 0.659, 0.305])

![](bbox=[0.116, 0.318, 0.879, 0.497])

**FIGURE 13.16**
(a) Linear chirp signal showing equally spaced time points, (b) same realization as in showing the $t_i$ time points given in Equation 13.26, and (c) realization in (b) indexed on $k$.

The analysis steps for analyzing the GLc(p) processes are very similar to those for the G(p;$\lambda$) processes, the only difference being the specific time transformation. In the Gc(p;$\lambda$) case, the $t'_i$ are not equally spaced and are obtained by interpolation. Wang et al. (2009) gave a Kalman filtering-based approach to avoid the need for interpolation. However, as stated, in most cases, we find the linear interpolation to be satisfactory. See also Haney (2011) and Bao (2014) for a discussion of the use of a Fourier-based interpolation. We will use linear interpolation in the examples through this book.

**EXAMPLE 13.15: GLc(p) ANALYSIS OF SIMULATED CHIRP DATA**
In this example, we consider the GLc(2) process associated with the discrete AR(2) dual process ($1-1.927B+0.999BY^2$). A realization of 400 evenly spaced time points from the GLc(2) process is plotted in Figure 13.17a, in which it is clear that the frequency content is time-varying and in particular it is non-monotonic in nature. The Wigner–Ville plot is shown in Figure 13.17d, where the linearity of the frequency change on each side of the reflection point can be seen. As in other cases, in order to analyze such a time-varying data set, we must find a stationary dual based on a transformation of the time index. The Wigner-Ville plot is