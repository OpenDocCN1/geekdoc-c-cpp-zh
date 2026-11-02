A measure of quality of the fit is the probability Q that the value of the mean-squared difference is equal or larger compared to the value from the current fit, given the assumption that the data points are distributed as in Eq. (8.97) [Press et al. (1995)]. The larger the value of Q, the better is the quality of the fit. As mentioned above, Q can be evaluated from a chi-squared distribution with n − n_p degrees of freedom. Since the cumulative chi-squared distribution is related to the normalized incomplete gamma function, which is available in gnuplot, one can evaluate Q directly in gnuplot:

```
gnuplot> Q = 1 - igamma(0.5 * FIT_NDF, 0.5 * FIT_NDF*FIT_STDFIT**2)
```

Note that in this case we obtain Q = 1, which is so large, because σ_r = 1 was used, see below.

To watch the result of the fit along with the original data, just enter

```
gnuplot> plot "sg_e0_L.dat" w e, f(x)
```

![](bbox=[0.15, 0.62, 0.85, 0.88])

Fig. 8.48 Gnuplot window showing the result of a fit command along with the input data.

The result is displayed in Fig. 8.48. Please note that the convergence depends on the initial choice of the parameters. The algorithm may be trapped into a local minimum in case the parameters are too far away from the best values. Try the initial values e=1, a=-3 and b=1! Furthermore, not