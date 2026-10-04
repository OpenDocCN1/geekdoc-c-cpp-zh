3. Figure 5.3c shows a realization of length $n = 200$ (fig5.3cwge) generated from the AR(3) model

```
$X_t - 2.195X_{t-1} + 1.994X_{t-2} - 0.796X_{t-3} = a_t; \quad (8.10)$
```

which can be written as $(1 - 0.995B)(1 - 1.2B + 0.8B^2) X_t = a_t$. In Table 7.7, we show the factor table for the ML, Burg, and YW estimates of the parameters. The ML and Burg estimates are similar to each other and reasonably close to the true values while the YW estimates are poor. aic.wge aic5.wge with $P=8$ and $Q=3$ correctly selects $p=3$ and $q=0$. Again, the message is to avoid using YW estimates.

# B: Real Data Sets

We use aic.wge (aic5.wge) to find ARMA(p,q) models selected for real data sets (which we do not know the correct model, and more accurately, for which an ARMA(p,q) only an approximating model.

+   1. In Chapter 7 we used an AR(9) to estimate the parameters of the sunset data in file ss08. Using aic.wge and letting $P=12$ and $Q=4$, the function selects AR(9) as the best model using AIC, BIC, and BIC. The sample autocorrelations appear to be consistent with white noise. Further examination of model appropriateness will be discussed in Chapter 9.

+   2. The (base10) log data in tswage file llynx is modeled by Tong (1977) as an AR(1) and by Campbell and Walker as a harmonic signal-plus-noise for the log-lynx data letting $P=12$ and $Q=4$. AIC selected AR(12), ARMA(1,1), and AR(11) as the top three while AIC picked AR(12), AR(11), and ARMA(11,1) as the top three. These models are consistent with the AR used by Tong (1977). Interestingly, BIC selected AR(2,3), ARMA(3,3), and AR(2) as the top three models. In Example 7.1b we discussed the ARMA(2,3) model fit to the log-lynx data and its relationship to the ARMA(2,2) approximation of harmonic signal-plus-noise models discussed in Example 4.1.

# 8.3 Model Identification for Nonstationary ARUMA(p,d,q) Models

In the previous section, we considered a variety of methods for identifying the orders of ARMA(p,q) processes. However, if it becomes necessary to fit a nonstationary model to a given set of data. In this section, we discuss