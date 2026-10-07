
# Program 6.3: Score Test for Testing Poisson model Zero-inflated Poisson model-UTI in Men Infected with HIV

* Urinary Tract Infections (UTI) in Men Infected with HIV Example
Data kindly provided by Prof Jan den Broek, Utrecht University
Reference: Van den Broek (1995), Biometrics

```sas
/*
nurinary_tract_infection;
    input_episode follow_up cd04;
    label_episode = "Number of UTI";
    follow_up = "Time to Follow Up (Months)"
    cd04 = "CD4 Cell Count";
    offs = "Logarithm of Time to Follow Up (Offset)";
    offs = log(follow_up);
datalines;
0 24 125 0 10 11 290
1 50 0 12 5 0 380
0 30 0 6 5 0 420
0 80 0 11 5 9 240
3 170 0 11 5 9 470
0 95 0 11 80 0 310
3 35 0 9 140 0 360
3 50 0 5 2 0 245
2 25 0 5 5 0 670
1 15 0 22 5 0 1280
0 85 0 5 30 0 780
2 130 0 5 110 0 1985
3 40 1 3 104 15 880
2 70 0 6 410 0 640
1 36 0 10 28 13 560
1 63 5 5 480 0 710
0 20 7 7 300 13 640
3 55 0 8 230 12 115
1 26 5 3 210 11 530
0 70 0 23 380 10 620
1 15 0 1 31 1 22 980
22 2 0 77 000
1 105 0 5 390 7 12240
1 60 0 8 440 7 530
1 85 0 18 30 0 590
0 17 0 12 300 0 1375
1 10 0 5 2 3 1 1 0 0 0 12 5 0 0 520
0 10 0 11 275 3 540
0 175 0 11 290 0 860
0 20 1 1 11 1;
;

/* Computation Jan van den Broek (1995) Score Test;
ods data;
title "Poisson Model -- UTI in Men Infected with HIV";
ods output ParameterEstimates= best;
proc genmood data=urinary_tract_infection;
    model episode = cd04 / dist=poisson;
    output out=predicted_mis;
run;

data best;
    set best;
    if Parameter = "Intercept" then call syst('DP',trim(left(DP)));
    if DF ne 0;
        keep Estimate;
run;
```
```

```sas
proc iml;

  -- Read parameter estimates and data;
use betas;
read all into betas;
use outl;
read all var(mu) into lambdas;
use outl;
read all var(cd4) into x;
use outl;
read all var(episode) into y;

  -- Compute Jan van der Broek (1995) Score Test;
n = nrow(x);
if (df = 1) then x = j(n,1,1) || x;
aux1 = y;
aux2 = exp(-lambdas);
aux3 = x*inv(x'*diag(lambdas)*x)*x*lambdas;
chisq = (sum(aux1/aux2) - n)*2 / (sum(1/aux2) - n) - aux3;
pval = 1 - probchisq(chisq,df,0);

  -- Print result
chisq("Chi-Square Statistic", format=8.2);
matrib df_label="Degree of Freedom";
matrib pval_label="P-Value", format=value.6;
distribution;
print "Jan van der Broek (1995) Score Test for Zero Inflation in a Poisson Distribution";
print "Urinary Tract Infections on HIV Infected Men Example";
print chisq df pval;

quit;
ods html close;
```

# Output 6.3: Poisson Model and Score Test Results--UTI in Men Infected with HIV

| Criterion | DF | Value/DF |
| --- | --- | --- |
| Log Likelihood | | -50.9849 |
| Full Log Likelihood | | -57.6287 |
| AIC (smaller is better) | | 119.2574 |
| AICC (smaller is better) | | 119.3837 |
| BIC (smaller is better) | | 124.4274 |

# 180 Overdispersion Models in SAS

| Parameter | DF | Estimate | Standard Error | Wald 95% Confidence Limits | Wald Chi-Square | Pr > ChiSq |
|---|---|---|---|---|---|---|
| Intercept | 1 | -0.4990 | 0.2466 | -0.9823 | 4.09 | 0.0430 |
| cd4 | 1 | -0.0048 | 0.0016 | -0.0079 | 9.55 | 0.0020 |
| Scale | 0 | 1.0000 | 0.0000 | 1.0000 | | |

Note: The scale parameter was held. The score test statistic turned out to be 5.96, which the null hypothesis is approximated by a Chi-square with one degree of freedom. Its associated P-value was 0.0146, providing evidence that too many zeros were observed for the Poisson distribution to fit the data. As indicated in Section 6.5, other GLMs could be fit by properly changing the link functions. For instance, one might consider a model where ln(μ) and log(σ) are both linear functions. The accompanying statements for fitting a model in GENMOD are given below.

```sas
title "ZIP Model - UTI in Men Infected with HIV";
proc genmod data=urinary_tract_infection;
model episode = cd4 / dist=zip;
zero link=logit;
```
Another model of interest is the one with ln(μ) = β₀ and log(σ) = α₀ + α₁, with xj representing CD4+ cell counts. Although this model and the previous two models mentioned before would provide essentially the same fit, where μⱼ are constant and the zero-inflated parameter is a linear function of CD4+ cell counts, in this model, the probability of being at risk for a UTI can be established for different values of xj.

# 6 Likelihood Models for Overdispersed Count Responses

```sas
Prob(At Risk of UTI given $x_j$) = $(1-\omega_j) \frac{\exp(-\alpha_0-\alpha_j)}{1+\exp(-\alpha_0-\alpha_j)}$
```
Furthermore, the estimated increase of risk for a UTI, measured by odds-ratio, and for any decrease of 100 cell counts on CD4+ is exp(β₀). We estimate the three quartiles of the distribution of CD4+ cells to estimate the probability of being at risk for a UTI given quartile value. Results are shown in Output 6.4. In the estimates, the GENMOD procedure uses @zero to indicate the portion related to Zero-inflation Probability parameters. In Program 6.4, we use ESTIMATE statements "@zero intercept -1 cd4 -q1" to obtain the estimates and standard errors of the risk probabilities.

# Program 6.4: ZIP Model with In(μⱼ) = β₀ and log(ωⱼ) = α₀+αⱼ—UTI in Men Infected with HIV

```sas
ods html;
proc univariate data=urinary_tract_infection
var cd4;
output out=out2 q1= median=q2 q3=
run;
data _null;
set out2;
call output('q1',trim(left(q1)));
call output('q2',trim(left(q2)));
call output('q3',trim(left(q3)));
run;
```
```sas
title "Zero-Inflated Poisson Model using GENMOD"
ods output=Est;
proc genmod data=urinary_tract_infection;
model episode /dist=zip;
zero cd4 /link=logit;
estimate "Prob at Risk at UTI when CD4<=q1" @zero intercept -1 cd4 -q1;
estimate "Prob at Risk at UTI when CD4<=q2" @zero intercept -1 cd4 -q2;
estimate "Prob at Risk at UTI when CD4<=q3" @zero intercept -1 cd4 -q3;
estimate "Log(OR)" @zero cd4 100 / exp;
run;
```
```sas
title "Estimated Probabilities of Risk of UTI at Different Values of CD4;"
proc print data=ests
where label contains "Prob" and label contains "Zero Inflation"
var label;
run;
```
```sas
title "Estimated Odds-Ratio for CD4 decrease of 100 units"
proc print data=ests
where label contains "Exp"
var label Beta;
run;
ods html close;
```

# Output 6.4: Selected Results Model with In(μⱼ) = β₀ and logit(ωⱼ) = αₙ + α₁xⱼ—UTI in Men Infected with HIV

Estimate Probabilities of Risk of UTI at Different Values of CD4

| Label | MeanEstimate | MeanLowerCL | MeanUpperCL |
|---|---|---|---|
| Prob at risk UTI when CD4=50 (Zero Inflation) | 0.5327 | 0.2516 | 0.7945 |
| Prob at risk UTI when CD4=235 (Zero Inflation) | 0.2340 | 0.0943 | 0.4725 |
| Prob at risk UTI when CD4=480 (Zero Inflation) | 0.0507 | 0.0077 | 0.2694 |

Estimated Odds-Ratio for CD4 decrease of 100 units

| Label | LBetaEstimate | LBetaLowerCL | LBetaUpperCL |
|---|---|---|---|
| Exp(OR) (Zero Inflation) | 2.0378 | 1.1931 | 3.4804 |
