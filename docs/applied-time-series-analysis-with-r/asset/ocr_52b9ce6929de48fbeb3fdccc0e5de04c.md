# 420

# Applied Time Series Analysis with R

multivariate time series $Z$, is multivariate white noise. Here, $Z$, may simply be an observed time series or it may be the residual series based on a VAR(p) fit to a set of data. A portanteau test of the hypotheses $H_0$: $ho(k) = 0, k=1, \dots,$ against $H_a$: $ho(k) 
eq 0$ for some $k$ between 1 and $K$ is based on the test statistic

```
$L = \sum_{k=1}^{K} \frac{k}{n-k} \text{tr}(\hat{\Gamma}(k)\hat{\Gamma}^{-1}(0)\hat{\Gamma}^{-1}(k)), \quad (10.42)$
```

$\hat{\Gamma}(k)$ is defined in Equation 10.11, and $\text{tr}[\mathbf{M}]$ denotes the trace of the matrix $\mathbf{M}$ (i.e., the sum of its diagonal elements). The statistic $L$ in Equation 10.42 is approximately distributed as $\chi^2$ with $m'K$ degrees of freedom when the data are multivariate white noise, and we reject $H_0$: $\rho(k)=0$, if the calculated $L$ is sufficiently large. When the data to be residuals from a fitted VAR($K-p$) process, then the test statistic is approximately $\chi^2$ with $m^2(K-p)$ degrees of freedom under $H_0$.

# EXAMPLE 10.4: AIC AND PARAMETER ESTIMATION FOR THE DATA IN EXAMPLE 10.2

In this example we use R AIC to fit a VAR(p) model to the bivariate VAR(1) data. Letting AIC select the order of the model (allowing $1 \le p \le 8$), AIC correctly selected $p=1$. In this example we will estimate the parameters of the VAR(1) process in Example 10.2 using the bivariate realization plotted in Figure 10.3. The base R function runif calculates the Yule-Walker and least squares estimates of either $\Phi_i$ and $\Gamma_a$. The resulting Yule-Walker estimates of $\Phi_1^{(YW)}$ and $\Gamma_a^{(YW)}$ are given

```
$$\Phi_1^{(YW)} = \begin{pmatrix} 0.89 & 0.58 \ -0.27 & 0.62 \end{pmatrix}$
```

and

```
$$\Gamma_a^{(YW)} = \begin{pmatrix} 0.97 & 1.45 \ 1.45 & 3.83 \endend{pmatrix}$
```

The corresponding least squares estimates are

```
$$\Phi_1^{(LS)} = \begin{pmatrix} 0.90 & 0.57 \ -0.27 & 0.63 \endend{pmatrix}$
```

and

```
$$\Gamma_a^{(LS)} = \begin{pmatrix} 0.78 & 1.47 \ 1.47 & 3.63 \endend{pmatrix}$
```