# 342

# Applied Time Series Analysis with R

and $\beta_i=-\phi_{vi} + \dots + \phi_{ij})$, for $j=1, \dots, p-1$. The form in Equation 8.23 is the lagged error correction form. (See Problem 8.10) Note that there are $p-1$ terms involving $VX_{t-j}$ in Equation 8.23. These are sometimes called the augmenting terms. Note that if $1-\\phi_1-\dots-\\phi_p z=0$ has a unit root, then $1-\\phi_1-\\dots-\\phi_p=0$, and also $	au=0$. As a consequence, for unit roots have been developed that the test hypothesis $H_0: \tau=0$ versus $H_1: \tau\neq0$ in Equation 8.23. The augmented Dickey-Fuller (tau) test (see Dickey and Fuller, 1979) is based on considering Equation 8.23 to be a regression equation with dependent variable $X_t$, and independent variables $X_{t-j}$. Using OLS regression (including an intercept term), $t_{DF}=	au/\sigma$ is calculated, and $H_0: \tau=0$ is rejected if $t_{DF}<C$ for a critical value $C$. Dickey and Fuller (1979) show that under the null hypothesis $H_0: \tau=0$, the sampling distribution of the test statistic, $t_{DF}$ does not follow the usual $t$-distribution and its limiting distribution is skewed to the left. The $\alpha$-level critical values, $t_{DF}(\alpha)$, based on the limiting distribution are $-2.57, -2.86, -3.43$ for $\alpha=0.1, 0.05$, and $0.01$, respectively (Dickey, 1976). It should be noted that in practice, the value of $ho$ is chosen sufficiently large, so that the residuals, $\hat{a}_t$, appear unaltered.

Testing for a factor $(1-B)Y_t$, that is, unit roots, requires application of the procedure $d$ times. For example, if the null hypothesis is not rejected, a second unit root test could be performed by letting $Y_t=(1-B)X_t$ considering the model

> $Y_t = \alpha_0 + \tau Y_{t-1} + \beta_1 Y_{t-1} + \dots + \beta_{p-1} Y_{t-p+1} + a_t$,

and $H_0: \tau=0$ in this new model.

# EXAMPLE 8.7

+   1. Testing the data in Figure 8.6 for unit roots: We apply the augmented Dickey-Fuller (tau) test to the realization from Equation 8.21 shown in Figure 8.6a. Note that this model has two unit roots and a second-order stationary component. We use the function `addTest` in the R package `fUnit` to apply the augmented Dickey-Fuller test using $p=4$ and allowing a constant term, we use the command `addTest t(fig86a, lags=4,type="c")` and obtain $t_{DF}=-2.03$, for which a p-value 0.03 is reported. Thus, the null hypothesis is not rejected, and we consider that the model has a unit root. Based on Figure 8.6c, it is reasonable to consider a second unit root. The augmented Dickey-Fuller test can be performed on the differenced data (this time using $p=3$) with the commands:

```
dl=artrans.wge(fig86a, phi.tr=1)
ADFTEST(d1, lags=3, type="c")
```