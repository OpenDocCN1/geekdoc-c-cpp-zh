Selected parts of the results of Program 6 are given in Output 6. Under both models, the estimated values of $\pi_i = Pr(Y, 0)$ are the same, i.e., $\pi_i = 0.4037$. Once the hurdle is crossed,

the estimated mean of the positive counts is $(1-\hat{\pi}_1) \frac{\hat{\mu}}{(1-\hat{\pi}_2)}$ where $\pi_2 = Pr(Y_2, 0)$. In this

example, both hurdle models provided the value: 1.1095. Not the true Akaike Information Criterion (AIC), the corrected information (AICC), and the Schwarz Bayesian Information Criterion (BIC) are smaller under the Negative-binomial hurdle model, suggesting that this model might be preferred over the Poisson hurdle model. We will corroborate this observation by performing a Pearson's Goodness-of-fit test, similar to the one computed in Program 6.2. The estimated means under the two models (see equations (6.27) and (6.30)) turned out to be 1.1095, which coincides with the arithmetic mean attained from the MEANS procedure. That is not the case for the variance. The estimated variance under the Poisson hurdle model is 2.28, while that obtained under the Negative-Binomial hurdle model (see equation (6.31)) is 1.568. The latter variance is much closer to 1.564—the usual variance reported by the MEANS procedure. Note that the variances of the two hurdle models under discussion are larger than their mean. Thus, these models exhibit overdispersion. Furthermore, the estimated mean of a Poisson model is in this case 1.1095, the two hurdle models also exhibit overdispersion relative to the Poisson distribution.

# Output 6.6: Results from Fitting Two Hurdle Models to the Daily Milk Consumption Data of Table 6.4

| Consumption Example — Mullahly (1986)
Poisson Hurdle Model |
| The NLMIXED Procedure |
| Fit Statistics |
| -2 Log Likelihood | 5470.5 |
| AIC (smaller is better) | 5474.5 |
| AICC (smaller is better) | 5477.5 |
| BIC (smaller is better) | 5474.4 |
| Additional Estimates |
| Label | Estimate | Standard Error | DF | t Value | Pr > [t] | Alpha | Lower | Upper |
| P1 | 0.4037 | 0.01126 | 7 | 35.86 | <0001 | 0.05 | 0.3771 | 0.4303 |
| Mu | 1.4032 | 0.04419 | 7 | 33.82 | <0001 | 0.05 | 1.3051 | 1.5013 |
| Mean | 1.1095 | 0.02749 | 7 | 40.37 | <0001 | 0.05 | 1.0445 | 1.1745 |
| Variance | 1.4354 | 0.04946 | 7 | 29.02 | <0001 | 0.05 | 1.3184 | 1.5523 |

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.