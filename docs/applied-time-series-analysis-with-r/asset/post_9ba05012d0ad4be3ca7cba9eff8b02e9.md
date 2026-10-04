
## Vector-Valued (Multivariate) Time Series

first method, we discuss multivariate Yule-Walker estimation based on the multivariate Yule-Walker equations given in Equation 10.18. Replacing $\Gamma(k)$ in the Yule-Walker equations with $\tilde{\Gamma}(k)$ defined in Equation 10.11 yields the sample multivariate Yule-Walker equations

```
$\tilde{\Gamma}(k) = \hat{\Gamma}(k-1)\hat{\Phi}_1^* + \dots + \tilde{\Gamma}(k-p)\hat{\Phi}_p^*, k=1, 2, \dots, p.$
```

As with the univariate case, the multivariate Yule-Walker estimates always produce a stationary process.

## 10.3.3.2 Least Squares and Conditional ML Estimation

Least squares estimates of the parameters of a VAR($p$) process can be obtained by expressing the VAR($p$) model as

```
$X_t = \alpha + \sum_{i=1}^p \hat{\Phi}_i X_{t-i} + a_t$
= \alpha + \hat{\Phi}_p^* X_t(p), \ t=p+1, \dots, n,$
```

where, $X_t(p)$ is the $mp \times 1$ matrix given

```
$X_t(p) = (X_{t-1}, \dots, X_{t-p})^*.$
```

The equations in Equation 10.34 are analogous to those in Equation 7.12 in the univariate case. We estimate $\mu$ with $X$ as given in Equation 10.10 and analyze the zero-mean process $X_t-X$. In this section, we for convenience refer to this mean adjusted process $X_t^*$. Thus, the model in Equation 10.35 does not have a constant term, that is $\alpha=0$, and the least squares estimates of the AR parameters are in the $mp \times m$ matrix

```
$\hat{\mathbf{\Phi}}_{p)} = [\hat{\Phi}_1, \dots, \hat{\Phi}_p]$
= (X')^{-1}X'X_t^*,$
```

where $X_{(ip)}$ is an $(n-p) \times m$ matrix with rows $(X_{t_1}, \dots, X_{t_m}), t=p+1, \dots, n,$ and $X$ is the $(n-p) \times p$ matrix with rows

```
$(X_{t-1}, \dots, X_{t-p}), t=p+1, \dots, n,$
```

where $X_{t-j} = (X_{t-j,1}, \dots, X_{t-j,m})$.

## 10.3.3.3 Burg-Type Estimation

Nuttall (1976a,b) and Strand (1977) obtained Burg-type estimates of the AR parameters by considering the multivariate backward model analogous to Equation 7.16 as well the forward model. See also Jones (1978). As with the univariate Burg estimates, the Burg-type AR estimates always produce a stationary solution. Marple and Nuttall (1983) have shown through simulation results that the Burg-type (Nuttall-Strand) estimator has better properties than the Yule-Walker estimator.

## 10.3.4 Calculating the Residuals and Estimating $\Gamma_a$

Analogous to Equation 9.2, the residuals associated with an estimated VAR(p) model are given by

```
$$\hat{\mathbf{a}}_t = \mathbf{X}_t - \sum_{j=1}^{p} \mathbf{\hat{\Phi}}_{t-j} - \hat{\mathbf{\alpha}}, \quad t=p+1,\dots,n.$$
```

The least squares estimator of $\hat{\Gamma}_a$ is given by

```
$$\hat{\Gamma}_a = \frac{1}{n-2p-1} \sum_{t=p+1}^{n} \hat{\mathbf{a}}_t \hat{\mathbf{a}}'_t.$$
```

and the conditional ML estimator is

```
$$\hat{\Gamma}_a = \frac{1}{n} \sum_{t=p+1}^{n} \hat{\mathbf{a}}_t \hat{\mathbf{a}}'_t.$$
```

Extension of the backcasting procedure discussed in Section 74 can be used to obtain residuals for $t=1, \dots, n$ and inevitably improve the ability to estimate $\Gamma_a$.

Recall that under normality, the least squares and conditional ML estimates of $\Phi_1, \dots, \Phi_p$ are the same. If backcasting is used to calculate $\hat{\mathbf{a}}_1, \dots, \hat{\mathbf{a}}_p$, then an unconditional ML estimator is given by

```
$$\hat{\Gamma}_a = \frac{1}{n} \sum_{t=1}^{n} \hat{\mathbf{a}}_t \hat{\mathbf{a}}'_t.$$
```

An estimator of $\Gamma_a$ can be based on residuals obtained from any estimation procedure (e.g., the Burg-type estimators, Yule-Walker, etc.) using Equation 10.39 whenever backcasting is used to calculate $\hat{\mathbf{a}}_1, \dots, \hat{\mathbf{a}}_p$.

## Vector-Valued (Multivariate) Time Series

## 10.3.5 VAR($p$) Spectral Density Estimation

The multivariate spectrum (spectral density) of a VAR($p$) process is given in Equation 10.32. The VAR spectral estimate is simply the spectral density associated with the VAR($p$) model fit to a set of multivariate time series data. That, the VAR spectral estimate is given

```
$$\hat{\Phi}_X(f) = \hat{\Phi}^{-1}(e^{2\pi i f})\hat{\Gamma}_a\hat{\Phi}^{*-1}(e^{-2\pi i f})$$
```

when $\hat{\Phi}$ and $\hat{\Gamma}_a$ are estimated from the data as discussed earlier.

## 10.3.6 Fitting a VAR($p$) Model to Data

In the following, we briefly summarize the steps involved in fitting a VAR($p$) model to a vector time series realization.

### 10.3.6.1 Model Selection

As in the univariate case, the first step in fitting a VAR($p$) model to a set of data is to identify the order $p$. The multivariate extension of AIC (based on ML estimation of the parameters) is given

```
AIC = \ln|\hat{\Gamma}_a| + \frac{2m^2p}{n}$$
```

As in the univariate case, versions of AIC can be found using Equation 10.41 based on other estimation procedures (e.g., Burg-type estimators). The model order is selected as the one for which we obtain the minimum value of AIC calculated using Equation 10.41 for the range of orders $0 \le p \le P$ for some integer $P$. Multivariate versions of alternatives to AIC such as BIC and AICC are also available (see Box of 2008).

### 10.3.6.2 Estimating the Parameters

Once the order $p$ is identified, the estimates of the parameters $\Phi_v, \dots, \Phi_w$ and $\mu$ associated with the selected model are obtained using methods such as those described above. Recall that it is typical to estimate with $\hat{\mathbf{X}}$ and then estimate the remaining parameters using the series $\mathbf{X}_t - \hat{\mathbf{X}}$. We will use this procedure in the following.

### 10.3.6.3 Testing the Residuals for White Noise

The Ljung-Box test discussed in Section 9.1 has been extended to the multivariate setting (see Hosking, 1981). Suppose you want to test whether the

## 420

## Applied Time Series Analysis with R

multivariate time series $Z$, is multivariate white noise. Here, $Z$, may simply be an observed time series or it may be the residual series based on a VAR(p) fit to a set of data. A portanteau test of the hypotheses $H_0$: $\rho(k) = 0, k=1, \dots,$ against $H_a$: $\rho(k) \neq 0$ for some $k$ between 1 and $K$ is based on the test statistic

```
$L = \sum_{k=1}^{K} \frac{k}{n-k} \text{tr}(\hat{\Gamma}(k)\hat{\Gamma}^{-1}(0)\hat{\Gamma}^{-1}(k)), \quad (10.42)$
```

$\hat{\Gamma}(k)$ is defined in Equation 10.11, and $\text{tr}[\mathbf{M}]$ denotes the trace of the matrix $\mathbf{M}$ (i.e., the sum of its diagonal elements). The statistic $L$ in Equation 10.42 is approximately distributed as $\chi^2$ with $m'K$ degrees of freedom when the data are multivariate white noise, and we reject $H_0$: $\rho(k)=0$, if the calculated $L$ is sufficiently large. When the data to be residuals from a fitted VAR($K-p$) process, then the test statistic is approximately $\chi^2$ with $m^2(K-p)$ degrees of freedom under $H_0$.

## EXAMPLE 10.4: AIC AND PARAMETER ESTIMATION FOR THE DATA IN EXAMPLE 10.2

In this example we use R AIC to fit a VAR(p) model to the bivariate VAR(1) data. Letting AIC select the order of the model (allowing $1 \le p \le 8$), AIC correctly selected $p=1$. In this example we will estimate the parameters of the VAR(1) process in Example 10.2 using the bivariate realization plotted in Figure 10.3. The base R function runif calculates the Yule-Walker and least squares estimates of either $\Phi_i$ and $\Gamma_a$. The resulting Yule-Walker estimates of $\Phi_1^{(YW)}$ and $\Gamma_a^{(YW)}$ are given

```
$$\Phi_1^{(YW)} = \begin{pmatrix} 0.89 & 0.58 \ -0.27 & 0.62 \end{pmatrix}$$
```

and

```
$$\Gamma_a^{(YW)} = \begin{pmatrix} 0.97 & 1.45 \ 1.45 & 3.83 \end{pmatrix}$$
```

The corresponding least squares estimates are

```
$$\Phi_1^{(LS)} = \begin{pmatrix} 0.90 & 0.57 \ -0.27 & 0.63 \end{pmatrix}$$
```

and

```
$$\Gamma_a^{(LS)} = \begin{pmatrix} 0.78 & 1.47 \ 1.47 & 3.63 \end{pmatrix}$$
```

## Vector-Valued (Multivariate) Time Series 421

In both cases, the estimates can be seen to be quite close to the true model parameters given in Equations 10.21 and 10.22.

**Using R:** As mentioned, the base R function calculates the Yule-Walker and least squares estimates for VAR models. The mle and burg methods are available in are for the univariate case only. In the following R code we create a bivariate time series [Figure 10.3](#) using cbind on the univariate code in [Figure 10.3a](#) and [b](#).

```
data(fig10.3.x1)
data(fig10.3.x2)
fig10.3 = cbind(fig10.3x1,fig10.3x2)
```

The call statements used in this example to identify the model order using AIC and to obtain the Yule-Walker and least squares estimates are

```
ar(fig10.3,order.max=8,aic=TRUE,method='wyw')
```

and

```
ar(fig10.3,order.max=8,aic=TRUE,method='ols')
```

respectively.

A useful CRAN package for VAR models is the package vars. The following vars commands, applied to the bivariate data [fig10.3](#) created above, will produce the least squares estimates (which match those above) and the corresponding Ljung-Box test with K= 24:

```
lsfit=VAR(fig10.3,p=1,type=c("const"),ic=c("AIC")
serial.test(lsfit,ags.pt=24,type=c("PT.asymptotic"))
```

The Ljung-Box test has a p-value greater than 0.9, and thus $H_0:\rho(k)=0, k=1,..., 24$ is not rejected. Similar results were obtained for other values of K tested.
Forecasts shown in [Figure 10.6](#) are based on the true model. Forecasts can be obtained using the package vars by adding the following line below the two command lines:

```
predict(lsfit,n.ahead=25)
```

By default you are also given the 95% confidence limits.

## 10.4 Nonstationary VARMA Processes

The ARUMA(p,d,q) processes discussed in [Section 5.2](#) can be generalized to the multivariate case. Specifically, we consider the model

> $$\Phi(B)\lambda(B)(X, \mu) = \Theta(B)a_1,$$
