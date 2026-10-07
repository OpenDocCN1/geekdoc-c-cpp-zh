# Chapter 10 Generalized Linear Overdispersion Mixed Models 373

| Additional Estimates | | | | | | |
| Label | Estimate | Standard Error | DF | t Value | Pr > |t| | Alpha | Lower | Upper |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Expected Counts Group 1 | 2.2881 | 0.1920 | 399 | 11.92 | <0001 | 0.05 | 1.9106 | 2.6656 |
| Expected Counts Group 0 | 1.6103 | 0.1364 | 399 | 11.81 | <0001 | 0.05 | 1.3421 | 1.8784 |
| Ratio Expected Counts Group 1 Vs 0 | 1.4209 | 0.1689 | 399 | 8.41 | <0001 | 0.05 | 1.0889 | 1.7530 |
| Sigma**2 | 1.3144 | 0.1035 | 399 | 12.70 | <0001 | 0.05 | 1.1109 | 1.5179 |

Table 10.7 summarizes the main results as reported by the NLMIXED procedure of the two GLOMMs discussed in this section.

Table 10.7: Parameters Estimates and Standard Errors of the Zero-inflated Poisson and Zero-centered Negative-binomial GLOMMs

| ZIP GLOMM | | ZINB GLOMM | | |
| Parameter | Estimate | Standard Error | Estimate | Standard Error |
| --- | --- | --- | --- | --- |
| $eta_0$ (=0.70)$ | 0.7988 | 0.0780 | 0.7072 | 0.0849 |
| $eta_1$ (=0.40)$ | 0.3909 | 0.1092 | 0.3513 | 0.1189 |
| $\kappa$ (=0.15)$ | | | 0.1269 | 0.0097 |
| $\omega$ (=0.20)$ | 0.1984 | 0.0075 | 0.2061 | 0.0084 |
| $\sigma^2$ (=1.20)$ | 1.1223 | 0.0883 | 1.3144 | 0.1035 |

# 10.7 Concluding Remarks

In this chapter, we presented some fundamental concepts regarding Generalized Linear Mixed Models (GLMM). We highlighted the estimation method known as Maximum Likelihood, based on adaptive Gauss-Hermite quadrature, which is the estimation method used in all the examples discussed in this chapter. This is one of the methods used in the GLIMMIX procedure. The other method, the Pseudo-likelihood method based on linearization, was discussed in Chapter 9. Examples, the Multicenter Randomized Trial of Section 10.2 and the Pump Reliability at a Pressured Water Reactor Nuclear Power Plant of Section 10.3, were used to illustrate the fitting of a Binomial and a Poisson GLMM. A third example, the Shoulder Study discussed in Section 9.9, was revisited in the context of a Multinomial GLMM. The fundamental concepts of GLMM can be extended to wider family of models, the family of Generalized Linear Overdispersion Mixed Models (GLOMM); this particular feature is

More, and Nagaraj Neeraraj, Overdispersion Models in SAS*. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional resources, visit support.sas.com/publishing.