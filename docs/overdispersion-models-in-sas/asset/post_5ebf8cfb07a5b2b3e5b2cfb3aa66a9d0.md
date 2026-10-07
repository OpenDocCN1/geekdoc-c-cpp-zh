
## Chapter 9 Generalized Estimating Equations Techniques for Marginal Models 285

# 1) Binomial Distribution

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_297_0.png)

Binomial Marginal Models GEE type

# 2) Poisson Distribution

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_297_1.png)

Poisson Marginal GEE Type

# 3) Multinomial Distribution

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_297_2.png)

Multinomial Marginal Models GEE Type

## 9.2 Marginal and Conditional Models

GEE can be applied to the so-called Marginal and Conditional Models. Marginal Models or Population-average Models are used to make inferences about population averages. On the other hand, Conditional Models are used when the focus is on subject-specific inference. The procedures MIXED and GLIMMIX distinguish between two different ways in which random effects affect a GLM, G-side and R-side. To distinguish these two types of random effects, consider a parallel study for evaluating the efficacy of a cream for hair growth where subjects were randomized to either apply the cream that supposedly grows hair, or to use a cream lotion placebo with nothing but inert ingredients. Subjects applied the lotions to their heads for a total of eight weeks, and a dermatologist observed hair growth on a weekly basis. Data are collected at weekly intervals to quantify the possible hair growth. Note that a string of measurements are obtained for each subject. We can account for the correlation of each subject by modeling it in different ways. One way is to model hierarchically, with subjects within the subject treated as random, i.e., normally distributed with zero mean and variance². This approach introduces a variance-covariance structure to the string of measurements from the subject. This specification is referred to as "G-side." The model is said to be conditional, perhaps as a reference to the fact that it is specified using a conditional argument. Inferences, previously stated, are subject-specific. On the other hand, the string of measurements associated with each subject can be treated as a multivariate random vector. This explicit specification of a variance-covariance matrix is called "R-side." The model is said to be marginal, as a reference to the fact that the correlation structure is specified directly without considering subjects. Inferences, as previously stated, are at population-average level. R-side effects are also called "residual" effects. Models in practice containing both G-side and R-side effects can be handled by the MIXED procedure. The concept of mixed model can be extended to the exponential family. This extended family is called Generalized Mixed Models (GLMM) and can be handled by the GLIMMIX procedure. Other procedures in SAS, such as NLMIXED, permit the use of GLMMs. For more information on mixed models, GLMMs, and non-linear models with random effects, refer to Littell et al. (2006). We now present a simple example in the same structure as the hair growth application described above, to illustrate the G-side and R-side random effects. programming statements of the data generation as well as the fitted programs are included in Program 9.1.

# Program 9.1 Generating Continuous and Binary Data from a Random Effects Model

```sas
data hair;
  seed = 1999;
  beta = 1.86294; -- P is approximately 0.8;
  do subj_id=1 to 100;
    sl = 2*normal(seed);
    s2 = sqrt(normal(seed));
    do week=1 to 8;
      score = round(sl + normal(seed), 1);
      p = 1/(1+exp(-beta - s2));
      u = uniform(seed);
      if u < p then y = 1;
      output;
    end;
  end;
  keep subj_id score y;
run;

ods html;
title "*** Linear Mixed Model with G-side Random Effects ***";
proc glimmix data=hair;
  class subj_id;
  model score = / s;
  random int / subject_id;
run;

title "*** Linear Mixed Model with R-side Random Effects ***";
proc glimmix data=hair;
  class subj_id;
  model score = / s;
  random _residual / subject_id type=cs;
run;
```

In this example we generate assessment data for 100 subjects. Continuous responses (score) are generated from the Normal distribution. Note the nested loops (weeks within subject) so that all the same subject share a common random effect. The program also generates a binary response (y), corresponding to whether or not the subject had appreciable growth relative to the previous week. Program 9.1 uses the SAS codes for estimating G-side and R-side models for the response variables "score" and "y". In the GLIMMIX procedure, the results are shown in Output 9.1. Note that the results for the linear mixed model are identical, except that the variance components are labeled differently. The estimate for fixed effect (intercept) is given. Since we generated data from a Normal distribution with zero mean, as expected, the estimate is not significantly different from zero.

## 288 Overdispersion Models in SAS

Output 9.1: Results from GLIMMIX Showing G-side and R-side Random Effects Models for a Linear Mixed Model

*** Linear Mixed Model with G-side Random Effects ***

| The GLIMMIX Procedure | |
| :--- | :--- |
| **Covariance Parameter Estimates** | |
| **Cov Parm** | **Subject** | **Estimate** | **Standard Error** |
| Intercept | Subj_id | 4.0004 | 0.1845 |
| Residual | | 0.9876 | 0.01669 |

| **Solutions for Fixed Effects** | | |
| **Effect** | **Estimate** | **Standard Error** | **DF** | **t Value** | **Pr >|t|** |
| Intercept | 0.05564 | 0.06422 | 999 | 0.87 | 0.3865 |

*** Linear Mixed Model with R-side Random Effects ***

| The GLIMMIX Procedure | | |
| :--- | :--- | :--- |
| **Covariance Parameter Estimates** | | |
| **Cov Parm** | **Subject** | **Estimate** | **Standard Error** |
| CS | Subj_id | 4.0004 | 0.1845 |
| Residual | | 0.9876 | 0.01669 |

| **Solutions for Fixed Effects** | | | | | |
| **Effect** | **Estimate** | **Standard Error** | **DF** | **t Value** | **Pr >|t|** |
| Intercept | 0.05564 | 0.06422 | 999 | 0.87 | 0.3865 |

Similarly, Output 9.1 (Continued) shows the results for the G-side and R-side options for the binary data. Due to the nonlinearity of the regression model, the two outputs are identical.

Output 9.1: (Continued) Results from GLIMMIX Showing G-side and R-side Random Effects for a Logistic Model

*** Logistic Model with G-side Random Effects ***

| The GLIMMIX Procedure | | | |
| :--- | :--- | :--- | :--- |
| **Covariance Parameter Estimates** | | | |
| **Cov Parm** | **Subject** | **Estimate** | **Standard Error** |
| Intercept | Subj_id | 1.0604 | 0.08441 |

| **Estimates** | | | | | | | |
| **Label** | **Estimate** | **Standard Error** | **DF** | **t Value** | **Pr >|t|** | **Mean** | **Standard Error Mean** |
| P | 1.2214 | 0.04315 | 999 | 28.31 | <0001 | 0.7723 | 0.00758 |

*** Logistic Model with R-side Random Effects ***

| The GLIMMIX Procedure | | | | |
| :--- | :--- | :--- | :--- |
| **Covariance Parameter Estimates** | | | | |
| **Cov Parm** | **Subject** | **Estimate** | **Standard Error** |
| CS | Subj_id | 0.1990 | 0.01349 |
| Residual | | 0.8013 | 0.01354 |

| **Estimates** | | | | | | | |
| **Label** | **Estimate** | **Standard Error** | **DF** | **t Value** | **Pr >|t|** | **Mean** | **Standard Error Mean** |
| P | 1.0880 | 0.03984 | 999 | 27.31 | <0001 | 0.7480 | 0.00751 |
