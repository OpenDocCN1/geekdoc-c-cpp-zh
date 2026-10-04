# Other Stationary Time Series Models

![](bbox=[0.148, 0.126, 0.836, 0.287])

**FIGURE 4.15**
ismic data from the Lg wave measured on the Massachusetts Mountain earthquake.

than of the ARCH(1) sequence. Corresponding, the AR(2) realization
in Figure 4.14f shows more subtle response to regions of volatility in the noise.

> **EXAMPLE 4.7: SEISMIC DATA**
Figure 4.15 shows a seismic Lg wave (data mm.eq in tswge) from
an earthquake known as the Massachusetts earthquake
(August 5, 1971) which was recorded at the Mina, Nevada state. See
Gupta et al. (2005). The extended period of higher variability around
t=100 is similar to the behavior in Figure 4.14d around t=700 and
t= 1150 suggesting that an AR with ARCH errors might be an appropri-
ate model for the seismic data in Figure 4.15.

# Appendix 4A: R Commands

# 4A.1 Basic computation and plot routines

+   The following functions were discussed previously
i. signplusnoise.wge (Appendix 1B)
ii. gen.arma.plot (Appendix 3B)
b. gen.arch.wge(n,alpha0,alpha,plot,sn) is a function that gen-
erates a length of n from the ARCH(q0) model given in
Equation 4.23.
n is the realization length ($x_t$ $t = 1, \dots , $n$)
alpha0 is the value for $\alpha_0$
alpha is a vector of length q0 containing $\alpha_i$ $i = 1, \dots , $q_0$
plot = TRUE (default) produces a plot of the realization generated
sn determines the seed used in the simulation (see Note (2) below)
(default = 0).