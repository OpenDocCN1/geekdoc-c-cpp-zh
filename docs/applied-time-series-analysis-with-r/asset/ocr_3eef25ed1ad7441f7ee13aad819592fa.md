# 362

# Applied Time Series Analysis with R

![](bbox=[0.125, 0.123, 0.004797, 0.303])

![](bbox=[0.005103, 0.123, 0.008664999999999999, 0.303])

![](bbox=[0.125, 0.316, 0.004797, 0.496])

![](bbox=[0.005103, 0.316, 0.008664999999999999, 0.496])

**FIGURE 8A.5**
(a) True autocorrelations. (b) Sample autocorrelations. (c) True partial autocorrelations.
d) Sample partial autocorrelations. Plots (a) and (c) are based on the ARMA(4,3) model in Equation 8A.11.

autocorrelations, true partial autocorrelations, and sample partial autocorrelations for this ARMA(4,3) model. In the figure it can be seen that the true and sample autocorrelations have a damped sinusoidal behavior. There is some suggestion in the partial autocorrelations that a pattern appears at k=2 but this is not absolutely clear. Based on these observations one might conclude that p-q=1, but due to the fact that the autocorrelations appear to have second-order behavior, ARMA(2,1) selection is a possible choice. If you examine a sample density estimator and conclude that there are two peaks in the spectrum between f=0 and f=0.5, then the correct ARMA(4,3) identification is plausible.

# 8A.4 Generalized Partial Autocorrelations

One major concern with the Box-Jenkins approach in the case of an ARMA(p,q) with p>0 and q>0 is that there is concerning concerning model selection even when examining the true autocorrelations and partial autocorrelations. The failure of the true autocorrelation and partial autocorrelation functions to uniquely identify p and q in a mixed ARMA(p,q) model as discussed above led Woodward and Gray (1981) to define the generalized