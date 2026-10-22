
so that we only get a single set of coefficients. That’s the essential idea of the continuation ratio model.

Let’s formalize the model for $J$ categories on the dependent variable. As usual we assume that the categories are ordered in the sequence $j=1,\ldots,J$. Let $y_i$ be the dependent variable that can take on one of these $J$ values. Define $A_{ij}$ as the probability that individual $i$ advances to stage $j+1$, given that he made it to stage $j$. More formally,

$$A_{ij}=\Pr(y_i>j\mid y_i\ge j).$$

We then specify $J-1$ logit equations,

$$\log\left(\frac{A_{ij}}{1-A_{ij}}\right)=\alpha_j+\boldsymbol{\beta}\mathbf{x}_i\qquad j=1,\ldots,J-1 \tag{6.8}$$

where $\boldsymbol{\beta}\mathbf{x}_i=\beta_1x_{i1}+\ldots+\beta_kx_{ik}$. Again, the right-hand side of equation (6.8) is just like the cumulative logit model and the adjacent categories model, with a separate intercept for each stage but a single set of coefficients. The left-hand side can also be rewritten in terms of the original probabilities, $p_{ij}$:

$$\log\left(\frac{A_{ij}}{1-A_{ij}}\right)=\log\left[\frac{\displaystyle\sum_{m=j+1}^{J}p_{im}}{p_{ij}}\right]$$

How can this model be estimated? Surprisingly, we can do it with an ordinary binary logit procedure. The trick is in the construction of the data set. Again, imagine doing a sequence of binary logit analyses. For each stage, you construct a data set that excludes all individuals who didn’t make it to that stage, with a dummy dependent variable indicating whether or not the individual advanced to the next stage. Now, instead of doing separate analyses, we combine these data sets into a single set, including a variable indicating which stage the data came from. Finally, we estimate a single binary logit model on the combined data.

Here’s how to do it for the data in Table 6.2. First, we read in the data as a contingency table, with each record corresponding to one of the cells. (To save space, two records are placed on each data line, which is accommodated by the @@ on the INPUT statement).

```sas
DATA afqt;
    INPUT white old faed ed count @@;
    DATALINES;
1 0 1 1 39    0 0 1 1 19
1 0 1 2 29    0 0 1 2 40
1 0 1 3 8     0 0 1 3 19
1 0 2 1 4     0 0 2 1 5
1 0 2 2 8     0 0 2 2 17
1 0 2 3 1     0 0 2 3 7
1 0 3 1 11    0 0 3 1 2
1 0 3 2 9     0 0 3 2 14
1 0 3 3 6     0 0 3 3 3
1 0 4 1 48    0 0 4 1 49
1 0 4 2 17    0 0 4 2 79
1 0 4 3 8     0 0 4 3 24
1 1 1 1 231   0 1 1 1 110
1 1 1 2 115   0 1 1 2 133
1 1 1 3 51    0 1 1 3 103
1 1 2 1 17    0 1 2 1 18
1 1 2 2 21    0 1 2 2 38
1 1 2 3 13    0 1 2 3 25
1 1 3 1 18    0 1 3 1 11
1 1 3 2 28    0 1 3 2 25
1 1 3 3 45    0 1 3 3 18
1 1 4 1 197   0 1 4 1 178
1 1 4 2 111   0 1 4 2 206
1 1 4 3 35    0 1 4 3 81
;
```

The data set for the first stage is then constructed as follows:

```sas
DATA first;
    SET afqt;
    stage=1;
    advance = ed GE 2;
RUN;
```

For the second stage, we have the following:

```sas
DATA second;
    SET afqt;
    stage=2;
    IF ed=1 THEN DELETE;
    advance = ed EQ 3;
RUN;
```

The two data sets are concatenated into a single set as follows:

```sas
DATA concat;
    SET first second;
RUN;
```

Alternatively, we can create the combined data set in a single DATA step:

```sas
DATA combined;
    SET afqt;
    stage=1;
    advance = ed GE 2;
OUTPUT;
    stage=2;
    IF ed=1 THEN DELETE;
    advance = ed EQ 3;
OUTPUT;
RUN;
```

Now we’re ready to estimate the model with PROC LOGISTIC:

```sas
PROC LOGISTIC DATA=combined;
    FREQ count;
    CLASS faed / PARAM=REF;
    MODEL advance(EVENT='1')=stage white old faed / AGGREGATE SCALE=NONE;
RUN;
```

The results in Output 6.12 show strong effects of race, father’s education, and stage, but little or no effect of age (at the time of the AFQT examination). White men are only about half as likely to advance to the next stage as black men. As you might expect, with increasing education of the father, the odds of advancing go up substantially, with the lowest probability of advancement among men whose father’s education was “unavailable.”

## Output 6.12 PROC LOGISTIC Results for Continuation Ratio Model

**Deviance and Pearson Goodness-of-Fit Statistics**

| Criterion | Value | DF | Value/DF | Pr > ChiSq |
|---|---:|---:|---:|---:|
| Deviance | 85.1090 | 25 | 3.4044 | <.0001 |
| Pearson | 84.6686 | 25 | 3.3867 | <.0001 |

**Analysis of Maximum Likelihood Estimates**

| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
|---|---:|---:|---:|---:|---:|
| Intercept | 1 | 1.5268 | 0.1352 | 127.4323 | <.0001 |
| stage | 1 | -1.1785 | 0.0753 | 244.9951 | <.0001 |
| white | 1 | -0.6918 | 0.0731 | 89.5732 | <.0001 |
| old | 1 | 0.0919 | 0.0867 | 1.1228 | 0.2893 |
| faed 1 | 1 | 0.2678 | 0.0776 | 11.9123 | 0.0006 |
| faed 2 | 1 | 0.6771 | 0.1336 | 25.7059 | <.0001 |
| faed 3 | 1 | 1.2031 | 0.1339 | 80.7279 | <.0001 |

**Odds Ratio Estimates**

| Effect | Point Estimate | 95% Wald Confidence Limits |
|---|---:|---:|---:|
| stage | 0.308 | 0.266 | 0.357 |
| white | 0.501 | 0.434 | 0.578 |
| old | 1.096 | 0.925 | 1.299 |
| faed 1 vs 4 | 1.307 | 1.123 | 1.522 |
| faed 2 vs 4 | 1.968 | 1.515 | 2.557 |
| faed 3 vs 4 | 3.330 | 2.562 | 4.330 |

The highly significant deviance and Pearson chi-square statistics suggest that something about this model is not right. Like the other ordinal models, this one imposes some restrictions, namely that the effects of the explanatory variables are the same at each stage. We can test this by including interactions between STAGE and the other three variables:

```sas
MODEL advance(EVENT='1')=stage white old faed stage*white stage*old stage*faed;
```

This produces the Type 3 statistics shown in Output 6.13. Clearly there are interactions with all three variables, which means that each variable has different effects on advancement into high school and advancement to high school graduation.

## Output 6.14 Separate Logit Models for Two Levels of Advancement

### Advancement from Grammar School to High School

**Analysis of Maximum Likelihood Estimates**

| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
|---|---:|---:|---:|---:|---:|
| Intercept | 1 | 0.6424 | 0.1129 | 32.3763 | <.0001 |
| white | 1 | -0.9388 | 0.0897 | 109.5316 | <.0001 |
| old | 1 | -0.1092 | 0.1110 | 0.9680 | 0.3252 |
| faed 1 | 1 | 0.1781 | 0.0952 | 3.4960 | 0.0615 |
| faed 2 | 1 | 0.9198 | 0.1895 | 23.5634 | <.0001 |
| faed 3 | 1 | 1.3376 | 0.1910 | 49.0229 | <.0001 |
| faed 4 | 0 | 0 | . | . | . |

### Advancement from High School Entrance to High School Graduation

**Analysis of Maximum Likelihood Estimates**

| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
|---|---:|---:|---:|---:|---:|
| Intercept | 1 | -1.3217 | 0.1570 | 70.8575 | <.0001 |
| white | 1 | -0.1811 | 0.1245 | 2.1166 | 0.1457 |
| old | 1 | 0.4427 | 0.1508 | 8.6214 | 0.0033 |
| faed 1 | 1 | 0.4721 | 0.1348 | 12.2748 | 0.0005 |
| faed 2 | 1 | 0.4425 | 0.2079 | 4.5303 | 0.0333 |
| faed 3 | 1 | 1.0273 | 0.1949 | 27.7924 | <.0001 |
| faed 4 | 0 | 0 | . | . | . |

For these data, then, the constrained continuation ratio model is a failure, its attractive parsimony apparently spurious. Nevertheless, even when a single equation model is inappropriate, there can be conceptual advantages in viewing the process in terms of stages. Output 6.14 is probably more meaningfully interpreted than a multinomial logit model with an equal number of coefficients. Another potential advantage of the continuation ratio approach—one not applicable to the data in Table 6.2—is the possibility of stage-dependent explanatory variables. Variables like parental income, number of persons in the household, and presence of the father are likely to vary over time, and this variation can be easily incorporated into the modeling process. In constructing the working data set, you simply redefine the variables to have different values at each of the stages.

There are several other points worth noting about the continuation ratio method. First, you may have observed that in the combined data set, the same people may appear more than once. For the education example, everyone who had some high school contributed two observations to the combined data set. Usually this raises red flags because of possible dependence among the multiple observations. While there isn’t space here to go into the details, there is absolutely no problem of dependence. For each individual, the probability of a particular outcome is factored into a set of conditional probabilities that have the same structure as independent observations.

Second, the continuation ratio approach is closely related to discrete-time methods for survival analysis. In that setting, the aim is to model the length of time until some event occurs, and time is measured in discrete units like years. Each year is treated as a stage and “advancement” means getting to the next year without experiencing the event. For further details, see Chapter 7 of my book, *Survival Analysis Using SAS: A Practical Guide, Second Edition* (2010).

Third, just as there are cumulative probit and cumulative complementary log-log models, one can easily estimate continuation ratio models using the probit or complementary log-log functions. The complementary log-log model is particularly attractive for event history applications because it is the discrete-time equivalent of the proportional hazards model used in Cox regression. I’ll close this chapter with a statistical curiosity: the complementary log-log continuation ratio model is mathematically equivalent to the cumulative complementary log-log model (McCullagh 1980).
