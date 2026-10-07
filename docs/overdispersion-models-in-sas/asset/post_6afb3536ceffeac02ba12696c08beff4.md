
# Chapter 5 Goodness-of-fit Tests for Overdispersed Binomial Models

Then, proceed to compute the GOF test in equation (5.4) with observed frequencies (5.5) and expected frequencies (5.7).

The issue of degrees of freedom of the GOF warrants some discussion. Note that GOF test statistic is computed based on the maximum likelihood estimates, which are obtained from the raw data. On the other hand, the distributional result that the degrees of freedom of the GOF is $\nu=R-3$ is based on the assumption that the statistic is computed using the estimates from the grouped data. As illustrated in Chernoff and Lehmann (1954) and as discussed in Chapter 30 of Kendall, Stuart, and Ord (1991) and in Satradhar et al. (2008), there seems to be a recovery of degrees of freedom due to using the more efficient maximum likelihood estimator. Recommended degrees of freedom of our proposed GOF test lies between $\nu_l=(R-1)-(k+h)$ and $\nu_u=(R-1)$. The lower bound $\nu_l$ corresponds to the case where the parameters are estimated, whereas the upper $\nu_u$ corresponds to the case when all the parameters are known. The results of the Simulation 5.4 support the use of $\nu=(R-1)-2$ degrees of freedom when the probability of success $\pi$ and the overdispersion parameter $\rho$ are common among the clusters.

We illustrate the use of GOF test when using the present data from the epidemiological study conducted by Awa et al. (1971, 1978) on chromosome aberrations in survivors of the atomic bombs exploded in Hiroshima and Nagasaki. The study was conducted from January 1968 to November 1969 in Hiroshima and from January 1968 to March 1971 in Nagasaki. The cases were selected from the A-bomb survivors who were resident in Hiroshima and Nagasaki for whom tentative radiation dose estimates were available. The controls consisted of two groups: those who were not in the cities at the time of bombing and those who were exposed to the bombs but estimated doses were less than 1 rad. Blood samples were taken and cytogenetic examinations were made on n=668 subjects from Hiroshima and n=403 from Nagasaki. We will focus on the Hiroshima data only; we would like to thank Prof. D. Moore for providing the data for this example. A total of 30 to 100 lymphocytes were examined from each subject and the number of chromosome aberrations (j-th subject) were recorded. Let $d$, denote, in rad, the radiation dose received by the unit of exposure in this study is believed to require more than one hit to cause an aberration, whereas a single hit is sufficiently to detect it. The total radiation dose considered here is the sum of the gamma and neutron components. Dose estimates exceeding 600 rad were reduced to 600. Prentice (1986) analyzed the chromosome aberrations data using an extended Beta-binomial model that allows for some degree of overdispersion. Moore (1987) extended the maximum likelihood estimation method for the Beta-binomial and a method based on the mean and variance to allow the modeling of the extra-binomial component as a function of the mean. In Prentice's estimates of the radiation dose received were grouped, whereas in Moore's estimates were used without doing any grouping of the data. We will fill both the Beta-binomial and Random-clumped Binomial models using the Moore (1987) data set. As in the Effort (1986) example of Toxoplasmosis in El Salvador conducted in Section 3.4, we will standardize the radiation dose $d_j$

```
$Z_j = \frac{\sqrt{648}(d_j - \tilde{d})}{\sqrt{\sum_{i=1}^{}(d_i - \tilde{d})^2}}$
```

The two overdispersed models to be fit will have linear predictors

```
logit(\pi_i) = \beta_0 + \beta_1 z_i + \beta_2 z_i^2$ (5.8)
```

and

```
logit(\pi_j) = \alpha_0 + \alpha_1 z_j + \alpha_2 z_j^2$ (5.9)
```

Therefore, the logit of the probability of success $\pi$ and the logit of the overdispersion $\rho$ are quadratic functions of the standardized dose $z$. We refer the reader to Section 4.8 where we introduced the concept of link functions in the context of Generalized Linear Overdispersion Models. The underlying models we fit are the Beta-binomial and the Random-clamped Binomial. The programming statements can be found in Program 5.4. We first compute the MLEs using the NMIXED procedure. The estimated frequencies of $\pi_i^*$ and $\rho_i^*$ are then output into the data sets $\pi_{bb}$, $\rho_{bb}$, $\pi_{rcb}$ and $\rho_{rcb}$. These data sets are needed in order to compute the expected (5.7) and GOF test (5.4) using the macro GOF_RCB_Distribution. This macro is provided in Appendix 5.3.

# Program 5.4: MLE Analysis and GOF Test of Hiroshima Chromosome Aberration Example

```
/*
Hiroshima Chromosome Aberration Example
*/
data hiroshima;
input m t d65_gamma t65_neutron;
label m = "Number of cells examined"
      t = "Total aberrations"
      d65_gamma = "T-65-D gamma"
      t65_neutron = "T-65-D neutron";
z = d65_gamma + t65_neutron;
datalines;
100 0 0
100 0 0
100 0 0
100 32 84
100 8 82
100 0 0
100 96 18
100 0 0
100 79 41
100 0 0
100 0 0
;

```proc stdize data=hiroshima;
  var z;
run;

data hiroshima;
  set hiroshima;
  zz = z * z;
run;

ods html;
ods graphics;

title "***Beta-binomial fit";
ods output Dimensions=Dimensions;
proc nlmixed data=hiroshima;
  parms b0=1 b1=0 b2=0 a0=0 a1=0 a2=0;
  rho = -1 / (1 + exp(-a1*z-a2));
  xbeta = b0 + b1*z + b2*zz;
  pi = 1 / (1 + exp(xbeta));
  theta = 1 / rho - 1;
  c = lgamma(m-1) * lgamma(m-theta) + lgamma(theta*pi) + lgamma(m-theta*(1-pi)) - lgamma(m-theta*pi) - lgamma(theta*(1-pi));
  model t = general( );
  predict pi out=pi_bb;
  predict rho out=rho_bb;
run;

data Dimensions;
  set Dimensions;
  if Descr = "Parameters" then call symput("params_bb",trim(left(Value)), "-nparams is number of parameters");
run;

data pi_bb;
  set pi_bb;
  keep Pred;
run;

data rho_bb;
  set rho_bb;
  keep Pred;
run;

title "***Random-clumped Binomial fit";
ods output Dimensions=Dimensions;
proc nlmixed data=hiroshima;
  parms b0=1 b1=0 b2=0 a0=0 a1=0 a2=0;
  rho = -1 / (1 + exp(-a1*z-a2));
  xbeta = b0 + b1*z + b2*zz;
  pi = 1 / (1 + exp(xbeta));
  plc = (1 - rho)*pi + rho;
  p2 = rho;
  p2c = 1 - p2;
  c = lgamma(m+1) - lgamma(t+1) - lgamma(m-t+1);
  ll = c + log(pi**t*plc**(m-t)) + p2**t*p2c**(m-t));
  model t = general( );
  predict pi out=pi_rcb;
  predict rho out=rho_rcb;
run;

data Dimensions;
  set Dimensions;
  if Descr = "Parameters" then call symput("nparams_rcb",trim(left(Value)), "-nparams is number of parameters");
run;

data pi_rcb;
  set pi_rcb;
  keep Pred;
run;

data rho_rcb;
  set rho_rcb;
  keep Pred;
run;

title;
%GOF_BB_RCB_Distributions(hiroshima,"Hiroshima Chromosome Aberration Example");
ods graphics off;
ods close;
```

Table 5.6 provides the MLEs under the Beta-binomial and Random-clumped Binomial models. All the terms in each are highly significant (P-value < 0.0001). We found (not reported here) that cubic of the beta estimates were not statistically significant. The corresponding P-values were 0.17 under the Beta-binomial model and 0.8 under the Random-clumped Binomial. This seems reasonable to assume that the probability of observing a chromosome aberration is a quadratic function (through the logistic mean) of the standardized dose received, and the degree of overdispersion varies (via the logistic function) as a linear function of the standardized dose received. Higher order combinations can be tried by simple modification in Program 5.4.

# Table 5.6: Maximum Likelihood Results under the Beta-binomial and Random-clumped Binomial Models—Hiroshima Chromosome Aberration Example

| Parameter | Estimate | Standard Error | Random-clumped Binomial Estimate | Random-clumped Binomial Standard Error |
|---|---|---|---|---|
| $\beta_0$ | -3.0145 | 0.04450 | -3.0699 | 0.03378 |
| $\beta_1$ | 1.3594 | 0.05643 | 1.3011 | 0.04441 |
| $\beta_2$ | -0.3449 | 0.03324 | -0.3705 | 0.02445 |
| $\alpha_0$ | -1.8661 | 0.07375 | -2.3525 | 0.09650 |
| $\alpha_1$ | 0.7993 | 0.11090 | 0.9331 | 0.15690 |
| $\alpha_2$ | -0.1610 | 0.05251 | -0.2365 | 0.05646 |
| -2 Log Likelihood | 2859.2 | | 3093.2 | |

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.
