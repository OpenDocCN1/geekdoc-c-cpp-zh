
# Chapter 9 Generalized Estimating Equations Techniques for Marginal Models 323

**Output 9.6:** Selected Results from Fitting a GEE Cumulative Logit Model using PROC SURVEYLOGISTIC

*** Results from fitting a GEE Cumulative Logit Model ***
*** to the Shoulder Tip Pain Data in Lumley (1996) ***

The SURVEYLOGISTIC Procedure

| Type 3 Analysis of Effects | | | |
| Effect | DF | Wald Chi-Square | Pr > ChiSq |
| --- | --- | --- | --- |
| trt | 1 | 14.5228 | 0.0001 |
| gender | 1 | 0.0575 | 0.8105 |
| age | 1 | 3.5987 | 0.0578 |
| time | 1 | 6.6168 | 0.0101 |

| Odds Ratio Estimates | | | |
| Effect | Point Estimate | 95% Wald Confidence Limits |
| --- | --- | --- | --- |
| trt Active vs Placebo | 6.766 | 2.531 | 18.086 |
| gender Female vs Male | 1.130 | 0.415 | 3.079 |
| age | 1.027 | 0.999 | 1.055 |
| time | 1.217 | 1.048 | 1.414 |

The same cumulative logit model can be fit in GENMOD using the following codes:

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

## 9.10 Small Sample Bias Corrections for Sandwich Estimators

It is well-known that in small samples, the GEE estimator of the variance-covariance matrix of the parameter estimates leads to inflated Type I error rates. To cope with this problem, resampling methods such as the jackknife and the bootstrap have been suggested to estimate robust covariance matrix. As pointed out by Mancel and DeRouten (2001), these methods fail for binary responses and for small numbers of subjects (clusters). If $\hat{H}^{-1}\hat{G}\hat{H}^{-1}$ denotes the “sandwich” estimator using GEE with $\hat{H}^{-1}$ as the “model-based” covariance matrix, Mancel and DeRouten argue that the residuals used to estimate $\hat{H}$ tend to be too small. Thus, the “sandwich” covariance matrix would be expected to underestimate the covariance matrix of the parameters, and its bias towards underestimation when the bias of the residuals is large (i.e., when the number of clusters is small). Thus, to reduce the small sample bias by using a first-order Taylor series approximation on the residuals in the computation of $\hat{G}$, Fay and Graraud (2001) propose two sample corrections. The first of these corrections is similar to that of Mancel and DeRouten (2001) but has the advantage that it may be applied to more general frameworks than GEE, such as the Cox proportional hazard and logistic regression. The second correction by Fay and Graraud (2001) consists of using f (or t) distribution instead of Chi-square (or normal) distribution, with an adjustment on the degrees of freedom. Kaumarni and Karoll (2001) propose an adjustment to ensure the use of the sandwich estimates combined with the distribution quantities provides coverage with probability below the nominal value. Pan and Wall (2002) propose an estimator and allows for f-test (or t test) that takes into account the bias of the “sandwich” estimator and allows for testing more one parameter simultaneously. Morel (1989), inspired by similar work in the survey sampling literature, propose a small sample correction to the GEE estimator and implemented it with the generalized link function with nominal-type data. The correction not only reduces the small sample bias in the Type I error rates but also guarantees that the estimated variance-covariance matrix is positive. It can be applied for testing one or more parameters, but differs from other corrections in the adjustment to the residuals of $\hat{G}$. That is, the correction is additive and not multiplicative, with the added term varying as the number of clusters (primary sampling units) increases. Morel, Bokossa and Neerhaal (2003) consider this additive correction to the GLM and GLMM frameworks, which are applicable to univariate and multivariate-type responses. The GLIMMIX procedure provides a variety of multiplicative small sample bias corrections, which are de-facto found in their documentation under the heading “Residual-based Estimators.” The de-facto by Morel, Bokossa and Neerhaal (2003) correction, MBN for short, is under the heading “Design-adjusted MBN Estimator.” THE SURVEYLOGISTIC procedure provides the option of adjusting the sandwich variance estimator with the Morel (1989) correction.

Following the documentation of PROC GLIMMIX, the general form of the empirical covariance estimator with the current multiplicative small sample bias corrections can be written as:

```
$Var(\hat{\beta}) = c \times \Omega \sum_{i=1}^{n} A_{i}' \hat{D}_{i}' \Sigma_{i}^{-1} e_{i} e_{i}' \hat{D}_{i} A_{i}, \quad (9.26)
```

Morel, Jorge, and Nagaraj Neerhaal. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA.

## 9 Generalized Estimating Equations for Marginal Models 325

where $e_i = y_i - \mu_i$, and $m$ is the number of clusters (often referred to as primary sampling units). Note that $\Omega$ in (9.26) is the inverse of $D'VD$, where $D$ is the matrix of design. The general form of the empirical covariance estimator with the current multiplicative small sample bias corrections can be written as:

### Table 9.6: Multiplicative Small Sample Corrections

| | | | | |
|---|---|---|---|---|
| CLASSICAL | 1 | I | |
| | | | | |
| | | | | (9.27)

The formula for $\delta_m$ given above is a generalization of the corresponding formula from Morel (1989); it allows the user to bound $\delta_m$ from above by $d$. The default value is 2, which corresponds to an upper bound of 0.5. The choice $d=1$ implies $\delta_m=1$ whenever $m \leq 2k$. In this case the classical sandwich is "inflated" additively by $\phi$.

The quantity

```
\text{trace} \left[ \Omega \left[ \sum_{i=1}^m D_i^T \Sigma_i^{-1} e_i D_i \right] \right] / k
```

is the average of the "Generalized Designs" (see Rao and Scott, 1981). In quasi-likelihood theory this is an estimator of the stable constant needed to inflate or deflate the "naïve" covariance estimate. Note

```
\text{trace} \left[ \Omega \left[ \sum_{i=1}^m D_i^T \Sigma_i^{-1} e_i D_i \right] \right] > 0.
```

User might choose $r$ such that $0 \leq r \leq 1$. Default value is $r=1$, which is a natural lower bound of $\phi$ assuring always inflation of the sandwich. This corresponds to the common case of overdispersion where the design effect is greater than one. In case the user suspects underdispersion, $r$ should be smaller than 1 so that the inflation is less pronounced. By taking $r$ positive, the user enforces a minimum amount of correction. The choice $r=0$ implies that no restriction on the lower bound of $\phi$ has been imposed.
