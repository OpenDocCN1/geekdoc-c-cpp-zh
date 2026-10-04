2. In order, for example, to choose the ‘best’ AR model, then use
q=0:0.

3. After model orders are obtained then parameter estimates can
obtained using est.arma.wge if q>0 or est.arma.wge if q=0.
See Appendix 7B.

Example: Referring back to Example 8.3a, in order to find the five
"best" models for fitting the data in fig3.18a and allowing p to
range from 0 to 8 and q to range from 0 to 4 we use the following
commands:

```
data(fig3.18a)
aic5.wge(fig3.18a,p=0:8,q=4,type='aic')
```

the output from aic5.wge is as follows:
Five smallest values of aic

| p | q | aic |
| 4 | 0 | 0.1267913 |
| 4 | 1 | 0.1366794 |
| 5 | 0 | 0.1366926 |
| 5 | 1 | 0.1431634 |
| 6 | 0 | 0.1453974 |

From the output we see that an ARMA(4,0) (that is an AR(4)) is cor-ect chosen as the best fitting model with AIC=0.1267913. The
second best fitting model according to AIC is an ARMA(4,1) with
AIC = 0.1366794 (notice that AIC for the ARMA(4,1) is larger than the
one for the AR(4)). In order to estimate the parameters of the selected
AR(4) model, you could use the command

```
est.ar.wge(fig3.18a,p=4)
```

or

```
est.arma.wge(fig3.18a,p=4,q=0)
```

# 8B.1 Other twge Functions Useful for Model Identification

We briefly review routines as a first step in the analysis

+   1. Plotting the data
2. Assessing sample autocorrelations for white noise
3. Overfitting with high-order AR models to identify nonstationary
components
4. Transforming data to stationarity