
\(\phi(B)=1-2\cos(2\pi f_1)B+B^2\)

then \(\phi(B)H_t=0\).

- 4.3 Generate realizations of length 1000 similar to those shown in [Figure 4.10](#) for the cases: \(\alpha_1=0, 0.6, 0.8,\) and \(0.9\). In each case, let \(\epsilon_t\) be zero mean, unit variance white noise. Also, choose \(\alpha_0\), so that in each case, the unconditional process variance is 1. Discuss the effect of different \(\alpha_1\) values. Explain why \(\alpha_1\) is constrained to be less than 1 for an ARCH(1) model (see `gen.arch.wge` in `tswge`).

- 4.4 Generate realizations of length 1000 from ARCH(2) processes with \((\alpha_1,\alpha_2)\) values: (0.4, 0.4), (0.1, 0.8), and (0.8, 0.1). Discuss the effect of changes in \(\alpha_1\) and \(\alpha_2\). Select \(\alpha_0\) for unit unconditional variance.

- 4.5 Generate realizations of length 1000 from GARCH(1, 1) processes with \((\alpha_1,\beta_1)\) values: (0.4, 0.4), (0.1, 0.8), and (0.8, 0.1). Also, choose \(\alpha_0\) so that in each case, the unconditional process variance is 1. Discuss the effect of changes in \(\alpha_1\) and \(\beta_1\) (see `gen.garch.wge` in `tswge`).

- 4.6 Use `gen.arch.wge` to create ARCH(1) errors and write an R program for generating realizations of length 1000 from AR(2) models with ARCH(1) errors. In each case, let \(\epsilon_t\) be zero mean, unit variance white noise and scale the ARCH(1) noise to have unit variance. Generate from each of the following scenarios:

  - a. \(\phi_1=1.6, \phi_2=-0.9, \alpha_1=0\)
  - b. \(\phi_1=1.6, \phi_2=-0.9, \alpha_1=0.5\)
  - c. \(\phi_1=1.6, \phi_2=-0.9, \alpha_1=0.95\)
  - d. \(\phi_1=0.95, \phi_2=0, \alpha_1=0\)
  - e. \(\phi_1=0.95, \phi_2=0, \alpha_1=0.5\)
  - f. \(\phi_1=0.95, \phi_2=0, \alpha_1=0.98\)

  Discuss and explain the behavior observed.

## 5 Nonstationary Time Series Models

In Chapters 3 and 4, we considered stationary processes. However, many or even most processes of interest tend to have some type of nonstationary or near-nonstationary behavior. Referring to the definition of stationarity in Definition 1.5, a process can be nonstationary by having (1) a nonconstant mean, (2) a nonconstant or infinite variance, or (3) an autocorrelation function that depends on time. The processes we discuss in this chapter will have one or more of these properties. In Chapters 12 and 13, we discuss techniques for analyzing time series having property (3). In this chapter, we will discuss the following:

- Deterministic signal-plus-noise models
- ARIMA, ARUMA, and nonstationary multiplicative seasonal models
- Random walk models with and without drift
- Time-varying frequency (TVF) models (or time-varying autocorrelation [TVA] models)

### 5.1 Deterministic Signal-Plus-Noise Models

In this section, we consider models of the form

$X_t = s_t + Z_t$

where $s_t$ is a deterministic signal and $Z_t$ is a zero-mean stationary noise component that may or may not be uncorrelated.

In this book, we will model $Z_t$ in such models using an AR($p$) model although other models (e.g. ARMA($p,q$)) could be used. We consider two types of signals: (a) “trend” signals, such as $s_t = a + b t$ or $s_t = a + b_1 t + b_2 t^2$, ..., and (b) harmonic signals, such as $s_t = C\cos(2\pi f t + U)$. We emphasize that signal-plus-noise models are quite restrictive, and they should only be considered if there are physical reasons to believe that a deterministic signal is present.

#### 5.1.1 Trend-Component Models

In this section, we consider the model

$X_t = a + b t + Z_t$ (5.2)

where $a$ and $b$ are real constants and $Z_t$ is a zero-mean AR($p$) process.

Clearly, $X_t$ is nonstationary if $b \neq 0$, since the mean of $X_t$ is $\mu_t = a + b t$, which depends on $t$ whenever $b \neq 0$. It can be easily shown that Var$(X_t) = \sigma_Z^2$, which is constant and finite, and that the autocovariance $\gamma(t_1, t_2)$ only depends on $t_2 - t_1$ because $Z_t$ is stationary. A model, such as the one in Equation 5.2, is often fit to data by first estimating $a$ and $b$ and then analyzing the residuals $\hat Z_t = X_t - \hat a - \hat b t$ as a stationary process. Of course, polynomial trends or other types of trends could be considered, but these will not be discussed here (see Woodward and Gray, 1995).

If the goal of the analysis of a particular time series is to determine whether there is a deterministic linear trend, a common practice is to fit a model such as Equation 5.2 and test the null hypothesis $H_0 : b = 0$. As an example, for the global temperature data (see Figure 1.24a), we might ask the question whether the observed increase in temperatures over the past 160 years should be predicted to continue. If $Z_t$ is uncorrelated white noise, then the testing of $H_0 : b = 0$ is routinely accomplished using the results of simple linear regression. However, the uncorrelated errors are a key assumption for this type of regression analysis and, as a consequence, standard regression methods should not be used in the presence of correlated errors. We will discuss the topic of trend testing in time series data in Section 9.3. This is a difficult problem, and as Example 5.1 shows, certain stationary time series models without a trend component can produce realizations with trending behavior.

**Example 5.1: Global Temperature Data**

To emphasize the issues involved in testing for trend, we consider modeling the global temperature data shown previously in Figure 1.24a. An AR(4) model fit to the global temperature series is

$X_t - 0.66 X_{t-1} + 0.02 X_{t-2} - 0.10 X_{t-3} - 0.24 X_{t-4} = a_t, \quad (5.3)$

where, for convenience, we use $\mu = 0$ and $\sigma_a^2 = 1$ in the following discussion rather than the corresponding estimates from the temperature data. The factor table for the model in Equation 5.3 is given in Table 5.1. It is important to note that this model does not contain a deterministic component and thus accounts for the trending behavior via the correlation structure in the model. From the factor table, it is clear that the model is stationary since all the roots are greater than one in absolute value (i.e. all the $|r_j^{-1}|$ values are less than one). Table 5.1 shows that the dominant feature of the model is a first-order factor associated with a positive real root quite close to the unit circle. As discussed previously, such a factor is related to aimless wandering behavior in realizations. The other factors contribute less pronounced higher frequency behavior, so we expect the wandering behavior associated with the positive real root to dominate realizations. In Figure 5.1, we show four realizations of length n = 150 from the AR(4) model in Equation 5.3. The wandering/random trending behavior is visible in all realizations as is the presence of more modest high frequency behavior. Figure 5.1a and c shows realizations that trend up and down, respectively, in a manner similar to that of the temperature series. Figure 5.1b and d shows random “trends” that change direction, twice in Figure 5.1b, and several times in Figure 5.1d. Figure 5.1a and c shows that the model in Equation 5.3 is capable of generating realizations that have the appearance of the temperature data, but Figure 5.1b and d shows that these “trends” may turn around abruptly.

**Table 5.1** Factor Table for the AR(4) Model in Equation 5.3

| AR Factors | Roots ($r_j$) | $\lvert r_j^{-1}\rvert$ | $f_{0j}$ |
|---|---|---|---|
| $1 - 0.99B$ | $1.01$ | $0.99$ | $0$ |
| $1 - 0.2B + 0.455B^2$ | $0.22 \pm 1.47i$ | $0.67$ | $0.23$ |
| $1 + 0.53B$ | $-1.88$ | $0.53$ | $0.5$ |

![](img/a0e0259119deb8c7b41dfd4f664e541d_258_0.png)

![](img/a0e0259119deb8c7b41dfd4f664e541d_258_1.png)

![](img/a0e0259119deb8c7b41dfd4f664e541d_258_2.png)

![](img/a0e0259119deb8c7b41dfd4f664e541d_258_3.png)

**Figure 5.1** Four realizations from the AR(4) model in Equation 5.3 fit to the global temperature data. (a) Realization 1, (b) Realization 2, (c) Realization 3, and (d) Realization 4.

The point of this example is to illustrate the fact that trending behavior can be produced by the autocorrelation structure alone, and as a consequence, the problem of testing for the existence of a real or deterministic trend of the form in Equation 5.2 is quite difficult. See, for example, Woodward and Gray (1993, 1995) and Woodward et al. (1997). We return to this problem in Chapter 9. Another important point is that forecasts (to be studied in Chapter 6) from the stationary model in Equation 5.3 do not predict the increasing trend to continue because subsequent observations are just as likely to begin going down as they are to continue going up as Figure 5.1b and d illustrates. However, forecasts using the model in Equation 5.2 with nonzero b will forecast an existing trend to continue. We will refer to trends produced by models of type in Equation 5.2 as deterministic trends while those produced by stationary models, such as Equation 5.3, will be called random trends.

#### 5.1.2 Harmonic Component Models
