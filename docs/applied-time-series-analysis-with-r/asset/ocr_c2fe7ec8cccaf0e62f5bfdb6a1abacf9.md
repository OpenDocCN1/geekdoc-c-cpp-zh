# Applied Time Series Analysis with R

the procedure suggested by Haugh (1976) and find cross-correlations of the residuals based on fitting ARMA(p,q) models to each data set.

Let P=10 and Q=0, AIC selects an AR(9) for the sunspot data between 1850 and 2009, and the fitted model based on Burg estimates

```
(1-0.073B+0.218B^2-0.188B^3+0.071B^5-0.035B^6
-0.027B^7+0.118B^8-0.360B^9)(X_i, -55.04) = a_i.
```

where $\hat{\sigma}_a^2=223.7$. In Example 9.2, we discussed that model might be appropriate for the temperature data. In this example, we consider the temperature data to be stationary and use the AR(4) model, (1-0.646 B+0.026B^2-0.097B^3-0.249B^4)(X+0.7)=a_i$, with $\hat{\sigma}_a^2=0.0107$, previously given in factor form in Example 9.8. Figure 9a. Figure 10.9b shows the estimated correlations, the residuals $\hat{a}_i$ from the AR(9) fit to the sunspot data and the AR(4) fit to the temperature data. Also, in Figure 10.9b, we show the limits $\pm2/\sqrt{16}=\pm0.518$, and we can state that there is no real relationship. So, at least based on this method of analysis, it cannot be concluded that there is an association between sunspot activity and global temperatures.

Clearly, a VAR(p) model allows for a correlation structure among the variables. In order to connect the discussion in this section with the VAR(p) model, in Example 10.6 we consider again the bivariate VAR(1) model in Example 10.2.

# EXAMPLE 10.6: TESTING COMPONENTS OF THE VAR(1)
MODEL IN EXAMPLE 10.2 FOR INDEPENDENCE

Suppose the two realizations in Figure 10.3 (fig10.3x1 and fig10.3x2) were observed with the knowledge that they represented a bivariate VAR(1) realization. Suppose also that the only question of interest is whether there is a relationship between the two stationary time series. One approach for assessing relationships between the two series would be to fit a VAR(p) model to the data as was done in Example 10.4, in this example we simply consider the data to represent realizations as a univariate AR(p) model, find the residuals from the fitted models, and test whether the residuals are independent using the procedure recommended by Haugh (1976). Using AIC with $0\le p\le 8$, we select an AR(3) for $X_1$ and an AR(4) for $X_2$. The sample correlations of the residuals with limit lines $\pm2/\sqrt{75}=\pm0.231$ are shown in Figure 10.10. It can be seen that the residuals are relatively correlated at lag k=0 while the correlations at other lags are within the 95% limit except for a borderline case at k=1. This is consistent with the model used to generate the VAR(1) data where from Equation 10.5, it is that the contemporaneous cross-correlation between the residuals (of the VAR(1) model) is 0.89 while the cross-correlations at nonzero lags are zero by construction.