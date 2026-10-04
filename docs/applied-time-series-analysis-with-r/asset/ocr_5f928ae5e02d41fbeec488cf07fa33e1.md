# G-Stationary Processes

# 579

![](bbox=[0.118, 0.121, 0.468, 0.296])

![](bbox=[0.498, 0.121, 0.848, 0.296])

![](bbox=[0.118, 0.313, 0.468, 0.473])

![](bbox=[0.498, 0.313, 0.875, 0.473])

FIGURE 13.17
(a) GLC(2) data with $a=1, b=0$, (b) dual data based on a fitted GLC(5) model to the data in (a), (c) instantaneous spectrum based on GLC(5) fit, and (d) Wigner-Ville plot for data in (a).

used for estimating $a$ and $b$ in Equation 13.21 based on the fact that the instantaneous frequencies change linearly on each side of the reflection point, and in fact change like $g'(t)=2\pi+b$. See Robertson et al. (2010). Interpolation is used to approximate the values of the time series at the $t_i$'s defined in Equation 13.26. The resulting dual is found by indexing on $k$ to yield $X(t)=Y_k$. A plot of $Y_k$ is shown in Figure 13.17b, which clearly looks stationary, especially compared to the data in Figure 13.17a. AIC selects an AR(5) model for the dual data. See Robertson et al. (2010). The instantaneous spectrum is shown in Figure 13.17c where it is seen that the linear frequency on each side of the reflection point is similar to that in the Wigner-Ville plot in Figure 13 See Appendix 13A.3 for details concerning the generalized IF and instantaneous spectrum in the linear chirp case.

# 13.5 G-Filtering

Standard filtering techniques, for example, using the Butterworth filter as discussed in Chapter 2, can produce unacceptable results when dealing with