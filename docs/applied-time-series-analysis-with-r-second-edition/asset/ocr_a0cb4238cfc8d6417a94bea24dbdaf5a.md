the five best ARMA(p,q) models within the p and q ranges in the call statement using the selection criterion specified by type.

x is a vector containing the realization to be analyzed

p = pmin:pmax specifies the range of values for the AR order p to be used in the search for the best model. (default is p = 0:5)

q = qmin:qmax specifies the range of values for MA order q to be used in the search for the best model. (default is q = 0:2)

type specifies the criterion used to select the model. Choices are type = "aic", "bic", or "aicc". (default is "aic")

The program outputs the model orders of the top five models (and associated criterion values) within the range of p and q specified in the function statement.

# NOTES:

+   1. ML parameter estimation is performed using base R function arima and tswge function aic.wge.
+   2. In order, for example, to choose the ‘best’ AR model, then use q = 0:0.
+   3. After model orders are obtained then parameter estimates can be obtained using est.arma.wge if q > 0 or est.ar.wge if q = 0. See Appendix 7B.

Example: Referring back to Example 8.3a, in order to find the five “best” models for fitting the data in fig3.18a and allowing p to range from 0 to 8 and q to range from 0 to 4 we use the following commands:

```
data(fig3.18a)
aic5.wge(fig3.18a,p = 0:8,q = 0:4,type = "aic")
```

the output from aic5.wge is as follows:

Five smallest values of aic

```
p q aic
4 0 0.1267913
4 1 0.1366794
5 0 0.1366926
```