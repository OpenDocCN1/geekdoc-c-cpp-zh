
Discuss the effect of changes in $\alpha_i$ and $\beta_i$ (see gen.garch.wge tswge).

4.6 Use gen.arch.wge to create ARCH(1) errors and write an R program for generating realizations of length 1000 from AR(2) models with ARCH(1) errors. In each case, let $\varepsilon_i$ be zero mean, unit variance white noise and scale the ARCH(1) noise to have unit variance. Generate from each of the following scenarios:

- a. $\phi_1 = 1.6, \phi_2 = -0.9, \alpha_i = 0$
b. $\phi_1 = 1.6, \phi_2 = -0.9, \alpha_i = 0.5$
c. $\phi_1 = 1.6, \phi_2 = -0.9, \alpha_i = 0.95$
d. $\phi_1 = 0.95, \phi_2 = 0, \alpha_i = 0$
e. $\phi_1 = 0.95, \phi_2 = 0, \alpha_i = 0.5$
f. $\phi_1 = 0.95, \phi_2 = 0, \alpha_i = 0.98$

Discuss and explain the behavior observed.

## 5
Nonstationary Time Series Models

In Chapters 3 and 4, we considered stationary processes. However, many or even more processes of interest tend to have some type of nonstationary or near-nonstationary behavior. Referring to the definition of stationarity in Definition 1.5, a process can be nonstationary by having (1) a nonconstant mean, (2) a nonconstant variance or infinite variance, or (3) an autocorrelation function that depends on time. The processes we discuss in this chapter will have one or more of these properties. In Chapters 12 and 13, we discuss techniques for analyzing time series having property (3). In this chapter, we will discuss the following:

- deterministic-plus-noise models
- ARIMA, ARUMA, and nonstationary multiplicative seasonal models
- Random walk models with and without drift
- Time-varying frequency (TVF) models (or time-varying autocorrelation (TVA) models)

### 5.1 Deterministic Signal-Plus-Noise Models

In this section, we consider models of the form

$X_t = s_t + Z_t,$

where $s_t$ is a deterministic signal and $Z_t$ is a zero-mean stationary noise component that may or not be uncorrelated.

In this book, we model $Z_t$ in such models using an AR(p) model although other models (e.g. ARMA(p,q)) could be used. We consider two types of signals: (a) "trend" signals, such as $s_t = a + bt$ or $s_t = a + bt + bt^2$, and and (b) harmonic signals, such as $s_t = C \cos(2\pi ft + U)$. We emphasize that signal-plus-noise models are quite restrictive, and they should only be considered if there are physical reasons to believe that a deterministic signal is present.

### 5.1.1 Trend-Component Models

In this section, we consider the model

$X_i = a + bt + Z_i, \quad (5.2)$

where $a$ and $b$ are real constants and $Z_i$ is a zero-mean AR(p) process.

Clearly, $X_i$ is nonstationary if $b \neq 0$, since the mean of $X_i$ is $\mu_i = a + bt$, which depends on $t$ whenever $b \neq 0$. It can be easily shown that $Var(X_i) = \sigma_z^2$, which is constant and finite, because the autocovariance $\gamma(t_i, t_j)$ only depends on $t_i - t_j$, because $Z_i$ is stationary. A model, such as the one in Equation 5.2, is often fit to data by first estimating $a$ and $b$ and then analyzing the residuals $\hat{Z}_i = X_i - \hat{a}-\hat{b}t$ as a stationary process. Of course, polynomial trends or other types of trends could be considered, but these will not be discussed here (Woodward and Gray, 1995).

If the goal of the analysis of a particular time series is to determine whether there is a deterministic trend, a common practice is to fit a model such as Equation 5.2 and test the null hypothesis $H_0: b=0$. As an example, for the global temperature data (see Figure 1.2a), we might ask the question whether the observed increase in temperatures over the past 160 years could be predicted to continue. If $Z_i$ is uncorrelated white noise, then the testing of $H_0: b=0$ is routinely accomplished using the results of simple linear regression. However, the uncorrelated errors are a key assumption for this type of regression analysis and, as consequence, standard regression methods should not be used in the presence of correlated errors. We will discuss the topic of trend testing in time series data in Section 9.3. This is a difficult problem, and as Example 5.1 shows, certain stationary time series models without a trend component can produce realizations with trending behavior.

### EXAMPLE 5.1: GLOBAL TEMPERATURE DATA

To emphasize the issues in testing for trend, we consider the global temperature data shown previously in Figure 1.2a. An AR(4) model fit to the global time series is

$X_i - 0.66X_{i-1} + 0.02X_{i-2} - 0.10X_{i-3} - 0.24X_{i-4} = a_i, \quad (5.3)$

where, for convenience we use $\mu=0$ and $\sigma^2=1$ for the first discussion with the corresponding estimates from the temperature data. The factor table for the model in Equation 5.3 is given in Table 5.1. It is important to note that this model does not contain a deterministic component and accounts for the trending behavior by the correlation in the model. From the factor table, it is clear that the model is stationary since all the roots are greater than one (i.e. all the $|r_j|$ values are less than one). Table 5.1 shows that the dominant feature of the model is a first-order factor associated with a

positive root quite close to the unit circle. As discussed previously, such a factor is related to aimless wandering behavior. The other factors contribute less pronounced high frequency behavior, so we expect the wandering behavior associated with the positive real root to dominate realizations. In Figure 5.1, we show four realizations of length $n = 150$ from the AR(4) model in Equation 5.3. The wandering behavior is visible in all realizations as the presence of most indeed high frequency behavior. Figure 5.1a and c shows realizations that trend up and down, respectively, in a manner similar to that of the temperature series. Figure 5.1b and d show random "trends" that change direction, twice, and several times in Figure 5.1d. Figure 5.1a and c shows that the model in Equation 5.3 is capable

# Nonstationary Time Series Models

# 207

# TABLE 5.1
Factor Table for the AR(4) Model in Equation 5.3

| AR Factors | Roots ($r_j$) | $|r_j|^{-1}$ | $f_{ij}$ |
|---|---|---|---|
| 1 - 0.99B | 1.01 | 0.99 | 0 |
| 1 - 0.2B + 0.455B^2$ | $0.22 \pm 1.47i$ | 0.67 | 0.23 |
| 1 + 0.53B | $\sim1.88$ | 0.53 | 0.5 |

![](img/41dcbfb9af56fa48895afde322197b0b_223_0.png)

![](img/41dcbfb9af56fa48895afde322197b0b_223_1.png)

![](img/41dcbfb9af56fa48895afde322197b0b_223_2.png)

![](img/41dcbfb9af56fa48895afde322197b0b_223_3.png)

FIGURE 5.1
Four realizations of the AR(4) model in Equation 5.3 fit to the global temperature data.
(a) Realization 1, (b) Realization 2, (c) Realization 3, and (d) Realization 4.

# Applied Time Series Analysis with R

of generating realizations that have the appearance of the temperature data, by Figure 5.1b and d shows that these “trends” may turn around abruptly.

The point of this example is to illustrate the fact that trending behavior can be produced by the autocorrelation alone, and as a consequence, the problem of testing for the existence of a real or deterministic trend in the form of Equation 5.2 is quite difficult, for example, Woodward and Gray (1993, 1995) and Woodward et al. (1997). We return to this problem in Chapter 9. Another important point is that forecasts (to be studied in Chapter 6) from the model predicting the increasing trend to continue because subsequent observations are just as likely to going down as they are going up as Figure 5.1b and d. However, forecasts using the model in Equation 5.2 with nonzero b will forecast an existing trend to continue. We will refer to trends produced by models of type in Equation 5.2 as deterministic trends while those produced by stationary models, such as Equation 5.3, will be called random trends.

### 5.1.2 Harmonic Component Models

In this section, we consider the case where s is a function of the form s= C (2πft + U). In Chapters 1 and 4, we have discussed models with harmonic components and studied them as a type of stationary process. The stationarity requires that the phase, U, is a random variable. However, in physical situations in which one realization is available, the phase is constant throughout the only realization observed. For this reason, it is often the case that signal-plus-noise models with harmonic components, the harmonic component, such as s= C (2πft + U) is considered to be a deterministic signal in the case of the trend-plus-noise examples.

Consider the case of the signal-plus-noise model with one harmonic component

```
X_i = C cos(2πft + U) + Z_i,
```

which is written as

```
X_i = A cos(2πft) + B sin(2πft) + Z_i,
```

where A=C cos U and B=-C sin U using trigonometric identities. In practice, if X satisfies Equation 5.5, then it is analyzed as if it a nonstationary process, in which the parameters A, B, and f fare often estimated as a first step, and then the process

```
Z_i = X_i - A cos(2πft) - B sin(2πft),
```
