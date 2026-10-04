# Vector-Valued (Multivariate) Time Series

+   4. A finite realization, $x_i t = 1, ..., n$, of a multivariate time series is a collection of the univariate realizations $x_{ij} t = 1, ..., n$, of the component time series, where $i = 1, ..., m$. For the interest rate data in Figure 10.1, we let $X_{it}$ denote rates on 6-month CDs, $X_{it2}$ stands for Moody’s seasoned Aaa corporate bonds, and $X_{i3}$ is the 30-year mortgage rate. These univariate realizations can be considered as a single realization, $x_i = (x_{i1}, x_{i2}, x_{i3})$, from a trivariate time series, $X_i = (X_{it1}, X_{it2}, X_{it3})$.

+   5. The mean of a multivariate time series is given by

```
$$\mu_i = E[X_i] = \begin{pmatrix} \mu_1 \ \mu_2 \ \vdots \ \mu_m \end{pmatrix}$$
```

where $\mu_{it} = E[X_{it}], i = 1, ..., m$.

+   6. The covariance matrix is given by

```
$$\Gamma(t_1, t_2) = E[(X_{t_1} - \mu_{t_1})(X_{t_2} - \mu_{t_2})^T] = \begin{pmatrix} \gamma_{11}(t_1, t_2) & ... & \gamma_{1m}(t_1, t_2) \ \vdots & \ddots & \vdots \ \gamma_{m1}(t_1, t_2) & ... & \gamma_{mm}(t_1, t_2) \end{pmatrix}$$
```

where $\gamma_{ij}(t_1, t_2)$ is the covariance between the univariate random variables $X_{t_i}$ and $X_{t_j}$ that is, $\gamma_{ij}(t_1, t_2) = E[(X_{t_i} - \mu_{t_i})(X_{t_j} - \mu_{t_j})]$, where $t_1 \in T$ and $t_2 \in T$.

# 10.2 Stationary Multivariate Time Series

In this section, we discuss the concept of covariance stationarity for multivariate time series. The basic definition is given in Definition 10.2.

# Definition 10.2

The multivariate time series $\{X_t, t \in T\}$ is said to be covariance stationary if

```
$$\mu = \begin{pmatrix} \mu_1 \ \mu_2 \ \vdots \ \mu_m \end{pmatrix}$$
```