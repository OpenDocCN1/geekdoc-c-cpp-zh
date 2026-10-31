
other models should be considered. This will be discussed in Example 8A.2.

## EXAMPLE 8.1: A WHITE NOISE PROCESS

[Figure 8.1a](#) displays the white noise realization of length $n = 200$ from [Figure 1.3b](#), and [Figure 8.1b](#) shows the sample autocorrelations, $\hat{\rho}_k$, $k = 0, \ldots, 44$, from [Figure 1.9b](#), along with horizontal lines at $\pm 2(1/\sqrt{n}) = \pm 0.14$. The sample autocorrelations at lags 10 and 36 marginally exceed the 95% limits with all others being within the lines. This behavior is typical of sample autocorrelations from white noise data. To draw the conclusion that there is some pertinent information for modeling purposes due to the fact that the lag 10 and lag 36 sample autocorrelation exceed the 95% limits would be a mistake. As mentioned earlier, one should expect about 5% of the $\hat{\rho}_k$ values to exceed the 95% limits if the data are white noise.

![](img/a0e0259119deb8c7b41dfd4f664e541d_394_0.png)

**FIGURE 8.1**  
(a) Realization from a white noise process. (b) Sample autocorrelations from (a) along with 95% limits.

**Using R:** The 95% limit lines can be included on sample autocorrelation plot produced by `plots.sample.wge` by specifying `arlimits = TRUE`.

## EXAMPLE 8.2: CHECKING FOR WHITE NOISE

In [Figure 8.2a](#), we show sample autocorrelations (with 95% limits) based on the realization of length $n = 190$ in [Figure 8.2b](#). As in [Figure 8.1b](#), more than 95% of the sample autocorrelations stay within the 95% limit lines. Consequently, examination of the sample autocorrelation suggests white noise. However, examination of [Figure 8.2b](#) shows that the realization has characteristics inconsistent with white noise. For example, the variability of the data seems larger early in the series, and there appears to be a certain amount of piecewise trending behavior after *t* = 100. While local irregularities can occur in white noise data, the total picture of this realization is that, although the sample autocorrelations are small, the realization does not appear to be white noise. The realization in Figure 8.2b consists of the residuals from an AR(10) fit to the data set in Figure 8.2c. Note that this realization displays frequency behavior that decreases with time similar to the bat echolocation signal in Figure 1.26a. An ARMA(*p,q*) model cannot appropriately be fit to such data because of its nonstationary behavior, and it is not surprising that the residuals from such a fit are not white.

In Chapters 12 and 13, we will discuss the analysis of time-varying frequency data sets such as the one shown in Figure 8.2c. In Section 9.1, we return to the topic of white noise testing when we discuss portmanteau tests.

![](img/a0e0259119deb8c7b41dfd4f664e541d_395_0.png)

**FIGURE 8.2**  
(a) Sample autocorrelations along with 95% limit lines for the realization in (b).

case, identifying p and q in an ARMA(p,q) model). ML estimation is a common tool that applies to a model or class of distributions with a fixed set of parameters, say α1, ..., αk. In this setting, the ML estimators are the estimators α̂1, ..., α̂k that maximize the likelihood function. However, simply maximizing the likelihood is not an appropriate strategy when parameters are being added to an existing model. For example, suppose ML methods are used to choose between a model with k parameters (e.g., an AR(k)) and a model from the same class with k + 1 parameters, for example, an AR(k + 1). Consider the strategy of maximizing the likelihood under each scenario and selecting the model with the maximized likelihood. This strategy would always select the AR(k + 1) model, since

$L_{MAX}(\hat{α}_{k1}, ..., \hat{α}_{kk}) ≤ L_{MAX}(\hat{α}_{k+1,1}, ..., \hat{α}_{k+1,k+1}), \quad (8.2)$ where $\hat{α}_{mj}$ denotes the ML estimator of αj for a model with m parameters. To see why Equation 8.2 is true, note that when there are k + 1 parameters, one choice for $\hat{α}_{k+1,k+1}$ is $\hat{α}_{k+1,k+1}=0$. The maximized likelihood on the left-hand side of Equation 8.2 is thus based on the constraint that $\hat{α}_{k+1,k+1}=0$ while the right-hand side is maximized without this constraint. AIC addresses this problem in the ARMA case by imposing a penalty for adding parameters. The method is based on selecting the p and q that minimize the expected Kullback–Leibler distance between the true underlying model of the data and an ARMA(p,q) model fit to the data where 0 ≤ p ≤ P and 0 ≤ q ≤ Q. See Akaike (1976). Essentially, AIC imposes a penalty for adding terms to a model, and the resulting procedure is to select the model that minimizes

$\text{AIC} = -2[\ln(\text{maximized likelihood})] + 2(\#\ \text{of free parameters}). \quad (8.3)$ In the setting of ARMA(p,q) modeling, the AIC criterion becomes $\text{AIC} = -2[\ln(\text{maximized likelihood})] + 2(p + q + 1), \quad (8.4)$

since there are p + q + 1 parameters including the constant term. It can be shown that AIC in Equation 8.4 is approximately equal to $\text{AIC} = \ln(\hat{σ}_a^2) + 2\frac{p+q+1}{n}, \quad (8.5)$ where $\hat{σ}_a^2$ is the estimated white noise variance associated with the ML fit of an ARMA(p,q) model (see Box et al., 2008; Shumway and Stoffer, 2010).

We will subsequently apply AIC by finding the p and q (0 ≤ p ≤ P and 0 ≤ q ≤ Q) that minimize AIC as defined in Equation 8.5.

A problem with the use of AIC is that as the realization length increases, AIC tends to overestimate the model orders (i.e., select models with too many parameters). Several authors have considered modifications to AIC to adjust for this problem. Two of the popular alternatives are AICC (Hurvich and Tsai, 1989) and BIC (sometimes called the Schwarz Information Criterion [SIC]) (Schwarz, 1978). These are given by

AICC = ln(σ̂_a²) + (n + p + q + 1)/(n - p - q - 3) , (8.6)

and

BIC = ln(σ̂_a²) + (p + q + 1) ln(n)/n . (8.7)

Simulation studies have shown BIC to perform best for large realization lengths, n, while AICC generally performs better for smaller n when the number of parameters is relatively large (see McQuarrie and Tsai, 1998). If computing time related to the use of ML estimation is an issue, then the quantities in Equations 8.5 through 8.7 can be approximated using alternative estimation techniques. For example, if the decision has been made to restrict attention to AR models, then Equations 8.5 through 8.7 can be calculated using σ̂_a² obtained based on Burg estimates of the model parameters.

Other automated model identification techniques have been proposed in the literature. For example, Akaike (1969) suggested the use of final prediction error (FPE) for identifying the order of an AR model. Another early technique for identifying the order of an AR model is the criterion AR transfer (CAT) function proposed by Parzen (1974).

## Using R:

Use aic.wge to find the best fitting ARMA(p,q) model for specified ranges of p and q and the model identification criterion you choose. For example, the command aic.wge(x, p = 0:8, q = 0:4, type = "aicc") finds the best fitting (based on AICC) ARMA(p,q) model for the data in vector x for model orders p = 0 through 8 and q = 0 through 4. You may specify type = "aic","bic", or "aicc". (default is "aic"). Function aic.wge also outputs the ML parameter estimates among other output. The function aic5.wge is similar to aic.wge but it finds the top five candidate models among the model order ranges using the specified selection criterion. See Appendix 8B.

NOTE: In this book, we use AIC as the model identification criterion. This is not meant as an endorsement of this criterion over the others, but is simply done for consistency of presentation.

## EXAMPLE 8.3: MODEL IDENTIFICATION USING AIC

### A: Simulated Data from Known Models

In this section, we reconsider some of the simulated data sets (for which we know the true model orders) discussed in earlier chapters and illustrate the use of AIC.

- In Example 3.12, we considered the AR(4) model

  $X_t - 1.15X_{t-1} + 0.19X_{t-2} + 0.64X_{t-3} - 0.61X_{t-4} = a_t,$ (8.8)

  and, in Figure 3.18a, we showed a realization of length $n = 200$ from this model with $\mu = 0$ and $\sigma_a^2 = 1$ (data set `fig3.18a` in tswge). The factor table is shown in Table 3.3. `aic.wge` with $P = 8$ and $Q = 4$ correctly selects $p = 4$ and $q = 0$ for this realization. The ML estimates for an AR(4) fit are shown in Table 7.5 (along with Yule–Walker and Burg estimates).

- In Example 3.17, we discussed the features of the ARMA(2,1) model

  $X_t - 1.6X_{t-1} + 0.9X_{t-2} = a_t - 0.8a_{t-1}.$ (8.9)

  Figure 3.24a shows a realization of length $n = 200$ from this model, and Table 7.10 shows ML estimates that are reasonably close to the true values. `aic5.wge` with $P = 5$ and $Q = 3$ correctly selects $p = 2$ and $q = 1$ for this realization. It should be noted that if we allow $P = 8$ and $Q = 4$, then AIC selects an ARMA(6,1) model whose factor table shows a factor very near to $1 - 1.6B + 0.9B^2$. However, using $P = 8$ and $Q = 4$ using AICC or BIC correctly results in an ARMA(2,1) model selection.

- Figure 5.3c shows a realization of length $n = 200$ (`fig5.3c` in
