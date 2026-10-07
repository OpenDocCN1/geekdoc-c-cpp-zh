
# Overdispersion Models in SAS

| GLM with Binomial Distribution and Probit Link using PROC PROBIT |
| Analysis of Maximum Likelihood Parameter Estimates |

| Parameter | DF | Estimate | Standard Error | 95% Confidence Limits | Chi-Square | Pr > ChiSq |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Intercept | 1 | -5.9139 | 0.1875 | -6.2815 | -5.5464 | 994.63 | <0001 |
| Ln(dose) | 1 | 1.4090 | 0.0402 | 1.3303 | 1.4877 | 1230.23 | <0001 |

| Probit Analysis on Ln(dose) |

| Probability | Ln(dose) | 95% Fiducial Limits |
| :--- | :--- | :--- | :--- |
| 0.50 | 4.1973 | 4.1574 | 4.2344 |

| Probit Analysis on dose |

| Probability | dose | 95% Fiducial Limits |
| :--- | :--- | :--- | :--- |
| 0.50 | 66.5040 | 63.90220 | 69.0298 |

There seems to be no clear-cut criteria for choosing between these two analyses (Probit versus Logit). They may be thought of as modeling the event triggered by a latent variable distributed as to Normal or Logistic distribution, respectively. Cox and Snell (1989, pp. 21-22) point out that for most purposes the Logistic and the Normal distributions agree closely, except when interest is in extreme values, where the probability of success is either very small or very close. The cumulative normal curve approaches its limit more rapidly than the cumulative logistic curve, indicating that the latter has longer tails than the former. The programming statements in Program 2.4 provide the plots of the estimated probability functions versus the observed proportions. (More than 70 years ago, Bliss and Berkinson much had to make these plots by hand!) The observed proportions $\hat{P}_j = \frac{t_j}{m}, j=1,2,...,11$ are m., overlaid with the estimated functions. We first generate the data set "temp," dosage values in the 38-to-301 range, by increments of ten. The variable "$x" is the natural log of dose. This data is concatenated with the data "pyrethrins." Then, two GLM's are fit: one with Probit link and the other one with Logit. The data set "temp" is not used in any of the computation of the MLE for the variables "$t" and "$m" are missing. However, like many other procedures, GLIMMIX provides probability estimates for the missing data. They are used to construct the smooth cumulative probability functions.

More, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

## Chapter 2 Generalized Linear Models

## Program 2.4: Estimation of the Normal and Logistic Cumulative Distribution Functions—nDosage-Mortality Data of Pyrethrins

```
-- Plotting
1)Estimated Logistic Curve and Observed Proportions
2)Estimated Probit Curve and Observed Proportions
temp:
    do dose=38 to 301 by 0.1; -- Dose range in increments of 0.1;
    x = log(dose);
    output;
end;
drop dose;
run;
data new;
    set pyrethrins temp;
run;
proc glimmix data=new;
    model t/m = x / link=probit;
    output=pred_out1(xlink)=pi_hat;
run;
proc glimmix data=new;
    model t/m = x;
    output=pred_out2(xlink)=pi_hat;
run;
data pred_out1;
    set pred_out1;
    label pi_hat = 'Predicted Probability'
    obs_pi = ;
    obs_pi = 'Observed Probability';
    if t > 0 then
        obs_pi = t/m;
        pi_hat = ;
end;
drop t;
run;
data pred_out2;
    set pred_out2;
    label pi_hat = 'Predicted Probability'
    obs_pi = ;
    obs_pi = 'Observed Probability';
    if t > 0 then
        obs_pi = t/m;
        pi_hat = ;
end;
drop t;
run;
html;
ods graphics data=pred_out1;
proc sgplot;
    title "Estimated Probit Curve"
    title2 "Dosage-Mortality of Pyrethrins on Male Flies, Murray (1938)";
    scatter x=x y=pi_hat;
    series x=x y=pi_hat / y2axis;
run;
proc sgplot data=pred_out2;
    title "Estimated Logistic Curve";
```

More, Jorge, and Nagaraj Neelchal. Overdispersion Models in SAS. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

```
title2 "Dosage-Mortality of Pyrethrins on Male Flies, Murray (1938)";
scatter x=x y=obs_pi;
series x=x y=pi_hat / y2axis;
run;
ods graphics off;
ods close;
```

The SGPLOT procedure is implemented for creating the final plots (SAS 9 or later is needed). Plots 2.4 and 2.5 provide the plots under discussion. The difference between the two plots might be subtle. The reader can see that the cumulative normal curve approaches its limit more rapidly than the logistic curve. The logistic curve fits better in this example, as can be seen from the plots.

### Plot 2.4: Estimated Cumulative Normal Function for the Dosage-Mortality Data of Pyrethrins
img/fa69b48c17ad45ebeb4d92ffb_50.png

More, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

### Plot 2.5: Estimated Cumulative Logistic Function for the Dosage-Mortality Data of Pyrethrins
img/fa69b48c17ad45ebeb4d92ffb_51.png

## 2.8 Odds-ratios and Logistic Regression

One of the main advantages of logistic regression is the clear interpretation of its parameters in terms of odds-ratios, and the ability to implement it with a variety of studies that are different in nature. Consider a hypothetical example where subjects are cross-classified according to the presence or absence of a risk factor, and the presence or absence of a certain disease. The true and unknown joint probabilities of exposure/disease can be represented in a 2x2 contingency table

| Exposure Factor | Yes | No | Total |
| :--- | :--- | :--- | :--- |
| Present | $\pi_{11}$ | $\pi_{12}$ | $\pi_{+}$ |
| Absent | $\pi_{21}$ | $\pi_{22}$ | $\pi_{++}$ |
| Total | $\pi_{+1}$ | $\pi_{+2}$ | 1 |

More, Jorge, and Nagaraj Neerchal. *Overdispersion Models in SAS*. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

where $\pi_i = \sum_{j=1}^{2} \pi_{ij}, i=1,2$ and $\pi_{\cdot j} = \sum_{i=1}^{2} \pi_{ij}, j=1,2$. In **prospective studies** two independent groups are selected. Subjects from one group being exposed to the risk factor, and subjects in the other group are not. Subjects from both groups are then followed, and at the end of the study they are classified according to whether or not they developed a disease. The true and unknown conditional probabilities of disease giving the status of a subject with respect to exposure for a prospective study are given

| Exposure Factor | Yes | No | Total |
| :--- | :--- | :--- | :--- |
| Present | $\pi_{11} / \pi_{++}$ | $\pi_{12} / \pi_{++}$ | 1 |
| Absent | $\pi_{21} / \pi_{++}$ | $\pi_{22} / \pi_{++}$ | 1 |

A common risk measure is the **Odds-ratio (OR)**, which is based on the ratio of two odds, namely, the odds of having the disease when the exposure factor is present, and the odds of having the disease when the exposure factor is absent. These odds are defined as

> $\text{Odds(Having the disease when the Exposure Factor is Present)} = \frac{\pi_{11} / \pi_{12}}{\pi_{21} / \pi_{22}}$

and

> $\text{Odds(Having the disease when the Exposure Factor is Absent)} = \frac{\pi_{21} / \pi_{22}}{\pi_{11} / \pi_{12}}$

Thus, the odds-ratio is

> $OR = \frac{\text{Odds(Having the disease when the Exposure Factor is Present)}}{\text{Odds(Having the disease when the Exposure Factor is Absent)}} = \frac{\pi_{11} / \pi_{12}}{\pi_{21} / \pi_{22}}$

Consider now a classification variable X that takes the value 1 if the exposure factor is present, but takes 0 otherwise. Let $\pi(X)$ represent the probability of having the disease, given the exposure factor X. Now, we posit a logistic regression model for $\pi(X)$ as follows:

```
logit(\pi(X)) = \ln\left(\frac{\pi(X)}{1-\pi(X)}\right) = \beta_0 + \beta_1 X .
```

When the exposure factor is present, the probability of having the disease is

```
\pi(X=1) = \frac{e^{\beta_0+\beta_1}}{1+e^{\beta_0+\beta_1}} .
```

Similarly, the probability of having the disease when the exposure factor is absent

```
\pi(X=0) = \frac{e^{\beta_0}}{1+e^{\beta_0}} .
```

Therefore, it can be shown that the odds-ratio is

```
OR = \frac{\pi(X=1)}{1-\pi(X=1)}}{\frac{\pi(X=0)}{1-\pi(X=0)}} = e^{\beta_1} .
```

The result is fundamental: the slope parameter of a logistic regression model can be interpreted in terms of the logarithm of odds-ratios. In the previous setup, $\beta_1=\ln(OR)$. The topic of logistic regression has been covered by many authors. We refer the reader to Hosner and Lemhow (2000) for an all-inclusive text on logistic regression.

In general, if the exposure factor is present, the classification variables take $X=x_1$, and $X=x_2$ if the exposure factor is absent. The odds-ratio is given by $OR=e^{(x_1-x_2)\beta_1}$. In particular, if a $\pm1$ coding is used $OR=e^{\pm\beta_1}$. The coding provides flexibility to the analysts to directly estimate the quantity of impact in a given study.
