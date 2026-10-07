# Chapter 2 Generalized Linear Models 35

# Program 2.3: Fitting a Binomial Model with Probit and Logit Links to the Dosage-
Mortality Data of Pyrethins Using PROC PROBIT

```
ods html;
title1 "Dosage-Mortality of Pyrethins on Male Flies, Murray (1938)"
title2 "GLM with Binomial Distribution and Logit Link using PROC PROBIT";nproct probit data=pyrethins log;
model t/m = dose / dlogistic inversecl;
run;
title "Dosage-Mortality of Pyrethins on Male Flies, Murray (1938)"
title2 "GLM with Binomial Distribution and Probit Link using PROC PROBIT";nproct prob data=pyrethins log;
model t/m = dose / inversecl;
run;
ods html;
```

The option "log" in the PROC requests the analysis performed on the natural logarithm of dose. The option "inversecl" provides the Lethal Dose (LD) estimates in increments of 1% that kill from 1% to 99% of the population. These LDs are calculated on the log scale and on the dosage scale. Selected results are produced in output 2.3.

Output 2.3: PROC PROBIT Results for the Dosage-Mortality Data of Pyrethins

| Dosage-Mortality of Pyrethins on Male Flies, Murray (1938) GLM with Binomial Distribution and Logit Link using PROC PROBIT |
| Probit Procedure Analysis of Maximum Likelihood Parameter Estimates |
| Parameter | DF | Standard Error | 95% Confidence Limits | Chi-Square | Pr > ChiSq |
|---|---|---|---|---|-|
| Intercept | 1 | -10.3279 | 0.3429 | -11.0000, -9.6558 | 907.14 | <0001 |
| Ln(dose) | 1 | 2.4582 | 0.0747 | 2.3118, 2.6047 | 1082.89 | <0001 |
| Probit Analysis on Ln(dose) |
| Probability | Ln(dose) | 95% Fiducial Limits |
|---|---|-|
| 0.50 | 4.20133 | 4.16305, 4.23705 |
| Probit Analysis on dose |
| Probability | dose | 95% Fiducial Limits |
|---|---|-|
| 0.50 | 66.77534 | 64.26718, 69.20315 |
| Dosage-Mortality of Pyrethins on Male Flies, Murray (1938) |

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS*. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.