
```
estimate 'Pi Control' 1/(1+exp(-b0));
estimate 'Pi TCCO' 1/(1+exp(-b0-b1));
estimate 'Pi PHT' 1/(1+exp(-b0-b2));
estimate 'Pi PHT+TCCO' 1/(1+exp(-b0-b1-b2));
estimate 'Logarithm Odds-Ratio PHT Vs TCCO Control when TCCO Present ' b2+b3;
estimate 'Logarithm Odds-Ratio PHT Vs Binomial ' 1/(1+exp(-a0))/(1+exp(-ad0));
estimate 'Rho TCCO' 1/(1+exp(-a0-a1))/(1+exp(-ad1));
estimate 'Rho PHT' 1/(1+exp(-a2));
estimate 'Rho PHT+TCCO' 1/(1+exp(-a0-a1-a2));
run;
```

Output 4.5 provides the AIC, AICC, and BIC for model (4.37) under the Beta-binomial and the Random-clumped Binomial distributions. These statistics are clearly smaller for the Random-clumped Binomial model. One might argue that in this example the Random-clumped Binomial distribution provides a better fit. Perhaps the clustering mechanism given in (4.10) gives a reasonable explanation for how the mother's genetic trait is passed onto offspring. 4.9 shows the estimated probability of ossification and the estimated overdispersion parameter for each of the treatment groups.

# Table 4.5: Information Criteria for Full Model on Both the "Betas" and the "Alphas" under the Beta-binomial and Random-clumped Binomial Distributions

| Full Model on the Betas, Full Model on the Alphas | The NLMIXED Procedure |
| :--- | :--- |
| Fit Statistics | |
| -2 Log Likelihood | 295.8 |
| AIC (smaller is better) | 311.8 |
| AICC (smaller is better) | 313.8 |
| BIC (smaller is better) | 331.0 |

| Random-clumped Binomial, Full Model on the Betas, Full Model on the Alphas | The NLMIXED Procedure |
| :--- | :--- |
| Fit Statistics | |
| -2 Log Likelihood | 287.8 |
| AIC (smaller is better) | 303.8 |
| AICC (smaller is better) | 305.8 |
| BIC (smaller is better) | 323.0 |

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

# Table 4.9: Beta Estimates and Standard Errors of the Ossification Data for the Full Factorial Logistic Regression Model with Common $\rho$

| Parameter Group | Beta-binomial Estimate | Standard Error | Random-clumped Binomial Estimate | Standard Error |
| :--- | :--- | :--- | :--- | :--- |
| Probability of Ossification $\pi_{op}$ | Control | 0.6642 | 0.05407 | 0.6381 | 0.05669 |
| | TCPO | | 0.4802 | 0.08279 | 0.4245 | 0.07478 |
| | PHT | | 0.2188 | 0.04154 | 0.2186 | 0.04050 |
| | TCPO + PHT | | 0.3149 | 0.1155 | 0.3231 | 0.1180 |
| Overdispersion $\rho_{ip}^2$ | Control | 0.3642 | 0.08003 | 0.3921 | 0.07631 |
| | TCPO | | 0.3568 | 0.1114 | 0.3370 | 0.08610 |
| | PHT | | 0.2257 | 0.1475 | 0.2040 | 0.1559 |
| | TCPO + PHT | | 0.6268 | 0.1535 | 0.7408 | 0.1215 |
| - 2 * Log Likelihood | | 295.8 | | | 287.8 | -- |

# 4.10 Generating Data under the Beta-binomial and Random-clumped Binomial Distributions

In this section, we provide the readers with codes for the algorithms for generating data under the Beta-binomial and Random-clumped Binomial distributions with parameters $(\pi, \rho;m)$. The programming statements are found in Program 4.6. An example based on $n=2000$ clusters with $\pi=0.4, \rho=0.7$ and $m=12$ is given. The underlying true mean and variance are $m\pi = 4.8$ and $m\pi(1-\pi)\{1+(m-1)\rho^2\}=18.4032$. The estimated mean and variance based on the specific "seed" turned out as follows: PHT; TCPO.

# Chapter 4 Likelihood Models for Overdispersed Binomial Responses

| Estimated Mean and Variance Data generated from Beta-binomial and Random-clumped Binomial distributions with parameters $\pi=0.4, \rho=0.7$ and $m=12$ | The MEANS Procedure |
| :--- | :--- |
| Analysis Variable: t | |
| Dist | Obs | Mean | Variance |
| BB | 20000 | 4.8602 | 18.3861 |
| RCB | 20000 | 4.7947 | 18.3707 |

# Program 4.6: Generating Data under the Beta-binomial and Random-clumped Binomial Distributions

```
/*
Generation of data under Beta-binomial and Random-clumped Binomial distributions with parameters $\pi, \rho$ and $m$
*/
#macro bb_rcb_data(pi,rho,m,n,seed);
Generation of data under the Beta-binomial distribution;
data bb;
  format Dist;
  Dist = "BB";
  seed = &seed;
  c = 1/rho - 1;
  a = c * pi;
  b = c - a;
  do cluster=1 to n;
    y1 = rangam(seed, a);
    y2 = rangam(seed, b);
    p = y1/(y1+y2);
    t = ranbin(seed,m,p);
    output;
  end;
keep Dist;
run;

Generation of data under the Random-clumped Binomial distribution;
data rcb;
  Dist = "RCB";
  seed = &seed;
  do cluster=1 to n;
    y = ranbin(seed,1);
    nn = ranbin(seed,rho);
    t = y * nn; /* Random clumping of the data;
    if nn < m then t = t + ranbin(seed,nn,pi);
    output;
  end;
keep Dist;
run;

data bb_rcb;
  set rcb;
run;

ods html;
title1 "Estimated Mean and Variance";
title2 "Data generated from Beta-binomial and Random-clumped Binomial distributions";
title3 "with parameters $\pi, \rho$ and $m=m";
proc means data=bb_rcb mean var=4;
  class Dist;
  var t;
run;
ods close;

%end bb_rcb;
%bb_rcb_data(0.4,0.7,12,20000);
```

# Goodness-of-fit Tests for Overdispersed Binomial Models

- 5.1 Introduction ................................................................115
- 5.2 Testing “No Overdispersion” against an Overdispersed Binomial Alternative .................................................116
- 5.3 An Omnibus Goodness-of-fit ...................................................121
- 5.4 Extension of the GOF Test When Covariates Are Present: The Chromosome Aberration................................................................130
- Appendix 5.1: Module “GOF_RCB” ..........................................138
- Appendix 5.2: Module “GOF_RCB” .........................................................146
- Appendix 5.3: GOF Test under Both the Beta-binomial and Random-clumped Binomial Distributions When Covariates Are Present ................154

# 5.1 Introduction

In this chapter we will consider two types of Goodness-of-fit (GOF) tests. Both types are usually referred to GOF in general, we will see that the two types have crucial differences regarding the null and alternative hypotheses. In the first type of, the null hypothesis that there is overdispersion is tested against specific alternatives, such as the Beta-binomial or Random-clumped Binomial models. An illustration of these for overdispersion was given in Section 4.6, when we tested the hypothesis $H_0 : \rho=0$ versus the alternative hypothesis $H_1 : \rho>0$ under the Beta-binomial, Random-clumped Binomial, Zero-inflated Binomial (ZIB), and the Generalized Binomial with Additive Interaction models for the chromosome data of Table 4.1. An example of the second type of GOF testing the adequacy of a specific model was also illustrated with the chromosome data of Table 4.1. The results provided in Table 4.3 indicate that the Beta-binomial, the Random-clumped Binomial, and the Generalized-Binomial with Additive distribution fit the number of associations fairly well, whereas Binomial and the ZIB distributions do not. In this chapter, we will describe both types of GOF tests and provide illustrative examples.

# 5.2 Testing “No Overdispersion” against an Overdispersed Binomial Alternative

In this section we consider the tests for the null hypothesis of “No Overdispersion” under several specific Overdispersed Binomial Distributions. One such was tested by Tarone (1979) under the Beta-binomial model. Suppose that $t_1, t_2, \dots, t_n$ are realizations of $T_1, T_2, \dots, T_n$, where the $T_j$ are independent random variables such that each $j$, $j=1, 2, \dots, n$, $T_j \sim \text{Binomial}(\pi, \rho; m_j)$. Under the Beta-binomial model, for $H_0: \rho = 0$ versus the one-sided alternative $H_1: \rho > 0$ is obtained as follows. If $\hat{\pi}$ is the maximum likelihood estimator of $\pi$ when $T_j$ are assumed to be distributed Binomial, then Tarone’s GOF one-sided statistic

```
$Z = \sqrt{\sum_{j=1}^n \frac{(t_j - \hat{m}_j)^2}{\hat{\pi}(1 - \hat{\pi}) - \sum_{j=1}^n m_j(m_j - 1)}}$ (5.1)
```

which under the null hypothesis is asymptotically distributed as a standard Normal distribution. Tarone also drew a two-sided GOF test of the Binomial distribution against the Generalized Binomial with Additive element of Altham (1978). This model was simultaneously proposed by Kupper and Hasek (1978) and is termed “Correlated Binomial Model.” The GOF test is

```
$X^2 = \frac{\sum_{j=1}^n \frac{(t_j - \hat{m}_j)^2}{\hat{\pi}(1 - \hat{\pi})}{\sum_{j=1}^n m_j(m_j - 1)}}$ (5.2)
```

which under the null hypothesis is asymptotically distributed as a Chi-square distribution with one degree of freedom. Prentice (1986) extended the Beta-binomial distribution to allow for some degree of negative correlations among the binary variables within experimental units. In the context of the extended Beta-binomial model Prentice provided a two-sided Z-statistic by (5,1), allowing tests for either overdispersion or underdispersion. These tests are locally most powerful with specific attributes.
