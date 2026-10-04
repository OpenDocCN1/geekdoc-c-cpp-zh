# 396 Applied Time Series Analysis with R

The function outputs the value of $K$, the test statistic (called chi square), degrees of freedom for the chi-square approximation, and the p-value of the test $H_0$: the data in vector $x$ to be analyzed for white noise. A small p-value suggests rejection of the null hypothesis of white noise.

As an example, to reproduce the results in Example 9.1(a)(i) for the AR(4) data in Figure 3.18a, we can use the following commands:

```
data(fig3.18a)
example=est.ar.wge(fig3.18a,p=4)
ljunge.wge(example$res, p=4, K=24)
ljunge.wge(example$res, p=4, K=48)
```

# 9A.1 Other functions and CRAN packages related to this chapter

+   1. Base R functions
   a. qnorm(x) plots a Q–Q plot for the data in vector x
   b. shapiro.test(x) will perform a Shapiro–Wilk test of the null hypothesis that the data in x are normal.
2. CRAN package nortest provides other tests for normality, including the Anderson–Darling test, Cramer–von Mises, and Lilliefors (Kolmogorov-Smirnov) tests. See Stephens (1974).
3. CO tests can be found in the CRAN package ocutt.

# EXERCISES

# Applied Problems

+   1. For each of the realizations in Problem 8.2, examine the appropriateness of the fitted models
   a. Check the whiteness of the residuals.
   b. Plot the associated ARMA spectral density estimator and compare it with a window-based estimator.
   c. Examine the appropriateness of the model in terms of forecasting performance by determining how well the model forecasts the last $l$ steps for whatever value or value you decide $l$ be.
   d. Generate realizations from the fitted model to determine whether realizations have a similar appearance and characteristics as the original realization.
2. For each of the fitted models found in Problem 8.3, examine the model appropriateness using the outline in Problem 9.1
3. For the fitted model found in Problem 8.5, examine the model appropriateness using the outline in Problem 9.1