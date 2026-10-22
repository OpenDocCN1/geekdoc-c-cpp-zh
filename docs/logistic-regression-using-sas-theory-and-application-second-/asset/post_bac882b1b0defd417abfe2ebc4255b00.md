
Similarly, if we reverse the independent and dependent variables, we obtain:

log(m_{i1} / m_{i2}) = β₂ + β₃ R_i.

These results show that the loglinear model for the 2 × 2 table implies two logit models, one for the row variable as dependent on the column variable and the other for the column variable as dependent on the row variable.

## 10.3 Loglinear Models for a Four-Way Table

Now let’s look at a much more complicated table, the 2 × 2 × 4 × 4 table that we previously analyzed by way of a logit model in Section 4.5. Our main goal will be to duplicate the results of the logit model with a loglinear model. To refresh your memory, the sample consisted of 4,991 high school seniors in Wisconsin. The dependent variable was whether or not they planned to attend college in the following year. The three independent variables were coded as follows:

- IQ        1=low, 2=lower middle, 3=upper middle, 4=high
- SES       1=low, 2=lower middle, 3=upper middle, 4=high
- PARENT    1=low parental encouragement, 2= high encouragement

In Section 4.5, the data were read in as 32 records, each record containing a unique combination of values of the independent variables, along with the number of seniors who had those values and the number of those seniors who planned to attend college. Unfortunately, that’s not the format we need for a loglinear analysis. Instead, we need 64 records, one for each cell in the four-way table, with values for all the variables and the frequency count in that cell. Here’s a DATA step that inputs the previous data set (WISC) and outputs the new data set in the appropriate format (WISCTAB).

```
DATA wisctab;
  SET wisc;
  college=1;
  freq=coll;
  OUTPUT;
  college=0;
  freq=total-coll;
  OUTPUT;
  DROP total coll;
PROC PRINT;
RUN;
```

### Output 10.4 Data for a Four-Way Contingency Table

| Obs | iq | parent | ses | college | freq |
| --- | --- | --- | --- | --- | --- |
| 1 | 1 | 1 | 1 | 1 | 4 |
| 2 | 1 | 1 | 1 | 0 | 349 |
| 3 | 1 | 1 | 2 | 1 | 2 |
| 4 | 1 | 1 | 2 | 0 | 232 |
| 5 | 1 | 1 | 3 | 1 | 8 |
| 6 | 1 | 1 | 3 | 0 | 166 |
| 7 | 1 | 1 | 4 | 1 | 4 |
| 8 | 1 | 1 | 4 | 0 | 48 |
| 9 | 1 | 2 | 1 | 1 | 13 |
| 10 | 1 | 2 | 1 | 0 | 64 |
| 11 | 1 | 2 | 2 | 1 | 27 |
| 12 | 1 | 2 | 2 | 0 | 84 |
| 13 | 1 | 2 | 3 | 1 | 47 |
| 14 | 1 | 2 | 3 | 0 | 91 |
| 15 | 1 | 2 | 4 | 1 | 39 |
| 16 | 1 | 2 | 4 | 0 | 57 |
| 17 | 2 | 1 | 1 | 1 | 9 |
| 18 | 2 | 1 | 1 | 0 | 207 |
| 19 | 2 | 1 | 2 | 1 | 7 |
| 20 | 2 | 1 | 2 | 0 | 201 |
| 21 | 2 | 1 | 3 | 1 | 6 |
| 22 | 2 | 1 | 3 | 0 | 120 |
| 23 | 2 | 1 | 4 | 1 | 5 |
| 24 | 2 | 1 | 4 | 0 | 47 |
| 25 | 2 | 2 | 1 | 1 | 33 |
| 26 | 2 | 2 | 1 | 0 | 72 |
| 27 | 2 | 2 | 2 | 1 | 64 |
| 28 | 2 | 2 | 2 | 0 | 95 |
| 29 | 2 | 2 | 3 | 1 | 74 |
| 30 | 2 | 2 | 3 | 0 | 110 |
| 31 | 2 | 2 | 4 | 1 | 123 |
| 32 | 2 | 2 | 4 | 0 | 90 |
| 33 | 3 | 1 | 1 | 1 | 12 |
| 34 | 3 | 1 | 1 | 0 | 126 |
| 35 | 3 | 1 | 2 | 1 | 12 |

| Obs | iq | parent | ses | college | freq |
|---:|---:|---:|---:|---:|---:|
| 36 | 3 | 1 | 2 | 0 | 115 |
| 37 | 3 | 1 | 3 | 1 | 17 |
| 38 | 3 | 1 | 3 | 0 | 92 |
| 39 | 3 | 1 | 4 | 1 | 9 |
| 40 | 3 | 1 | 4 | 0 | 41 |
| 41 | 3 | 2 | 1 | 1 | 38 |
| 42 | 3 | 2 | 1 | 0 | 54 |
| 43 | 3 | 2 | 2 | 1 | 93 |
| 44 | 3 | 2 | 2 | 0 | 92 |
| 45 | 3 | 2 | 3 | 1 | 148 |
| 46 | 3 | 2 | 3 | 0 | 100 |
| 47 | 3 | 2 | 4 | 1 | 224 |
| 48 | 3 | 2 | 4 | 0 | 65 |
| 49 | 4 | 1 | 1 | 1 | 10 |
| 50 | 4 | 1 | 1 | 0 | 67 |
| 51 | 4 | 1 | 2 | 1 | 17 |
| 52 | 4 | 1 | 2 | 0 | 79 |
| 53 | 4 | 1 | 3 | 1 | 6 |
| 54 | 4 | 1 | 3 | 0 | 42 |
| 55 | 4 | 1 | 4 | 1 | 8 |
| 56 | 4 | 1 | 4 | 0 | 17 |
| 57 | 4 | 2 | 1 | 1 | 49 |
| 58 | 4 | 2 | 1 | 0 | 43 |
| 59 | 4 | 2 | 2 | 1 | 119 |
| 60 | 4 | 2 | 2 | 0 | 59 |
| 61 | 4 | 2 | 3 | 1 | 198 |
| 62 | 4 | 2 | 3 | 0 | 73 |
| 63 | 4 | 2 | 4 | 1 | 414 |
| 64 | 4 | 2 | 4 | 0 | 54 |

Here is the SAS code for estimating a loglinear model that is equivalent to the first logit model of Section 4.5:

```
PROC GENMOD DATA=wisc tab;
  CLASS iq ses;
  MODEL freq=iq|ses|parent college iq*college ses*college
        parent*college / D=P TYPE3;
RUN;
```

As before, we are fitting a Poisson regression model for the frequency counts, with the default logarithmic link. The first term on the right-hand side of the MODEL equation—IQ|SES|PARENT—is shorthand for IQ*SES*PARENT IQ*SES IQ*PARENT SES*PARENT IQ SES PARENT. In other words, we fit the 3-way interaction, the three 2-way interactions, and the main effects of each of the independent variables. These parameters pertain only to the relationships among the independent variables in the logit model, not to the effects of the independent variables on the dependent variable (college choice). We include them in the model because to do otherwise would assert that they are 0. Because we cannot force these parameters to be 0 in a logit model, neither do we do it in the corresponding loglinear model. The general principle is this: *Whenever you want a loglinear model to be equivalent to some logit model, you must include all possible interactions among the predictor variables in the logit model.* Even though we include these interactions, they rarely have any substantive interest because they describe relationships among the predictor variables *conditional on the values of the dependent variable*. Ordinarily, these parameters have no useful causal interpretation.

The parameters that do have a useful interpretation are specified in the MODEL statement as COLLEGE IQ*COLLEGE SES*COLLEGE PARENT*COLLEGE. These correspond to the intercept and the three main effects of the independent variables on the dependent variable in the logit model. So, all the parameters in the corresponding logit model involve the dependent variable when specified in the loglinear model. Notice that IQ and SES are listed as CLASS variables so that, for each variable, three dummy variables will be constructed to represent the four categories. This is unnecessary for COLLEGE and PARENT because they are dichotomous.

Results are shown in Output 10.5. Values that are the same as those in Output 4.10, obtained by direct fitting of the logit model, are shown in italics. The numbers to the right of the parameter names correspond to the values of the CLASS variables. Apparently, the loglinear model contains many more parameters than the logit model, but the parameters that matter are identical in the two models. Notice also that the deviance and Pearson chi-squares are identical for the logit and loglinear models. The Type 3 chi-squares are not identical in the two outputs because PROC LOGISTIC reports Wald chi-squares while PROC GENMOD reports likelihood ratio chi-squares. But the values are similar.

### Output 10.5 PROC GENMOD Output for Loglinear Analysis of a Four-Way Table

| Criteria For Assessing Goodness Of Fit |  |  |  |
|---|---:|---:|---:|
| **Criterion** | **DF** | **Value** | **Value/DF** |
| Deviance | 24 | 25.2358 | 1.0515 |
| Scaled Deviance | 24 | 25.2358 | 1.0515 |
| Pearson Chi-Square | 24 | 24.4398 | 1.0183 |
| Scaled Pearson X2 | 24 | 24.4398 | 1.0183 |
| Log Likelihood |  | 18912.8805 |  |
| Full Log Likelihood |  | -192.6604 |  |
| AIC (smaller is better) |  | 465.3207 |  |
| AICC (smaller is better) |  | 607.9294 |  |
| BIC (smaller is better) |  | 551.6760 |  |

| Analysis Of Maximum Likelihood Parameter Estimates |  |  |  |  |  |  |  |  |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| **Parameter** | **DF** | **Estimate** | **Standard Error** | **Wald 95% Confidence Limits** |  | **Wald Chi-Square** | **Pr > ChiSq** |
| Intercept | 1 | 1.4076 | 0.4093 | 0.6055 | 2.2098 | 11.83 | 0.0006 |
| iq | 1 | 1 | 2.4070 | 0.5036 | 1.4200 | 3.3939 | 22.85 | <.0001 |
| iq | 2 | 1 | 1.8198 | 0.4967 | 0.8462 | 2.7934 | 13.42 | 0.0002 |
| iq | 3 | 1 | 1.7044 | 0.4969 | 0.7305 | 2.6782 | 11.77 | 0.0006 |
| iq | 4 | 0 | 0.0000 | 0.0000 | 0.0000 | 0.0000 | . |
| ses | 1 | 1 | 3.4289 | 0.4775 | 2.4929 | 4.3648 | 51.55 | <.0001 |
| ses | 2 | 1 | 3.3431 | 0.4600 | 2.4416 | 4.2446 | 52.83 | <.0001 |
| ses | 3 | 1 | 1.6470 | 0.5007 | 0.6657 | 2.6283 | 10.82 | 0.0010 |
| ses | 4 | 0 | 0.0000 | 0.0000 | 0.0000 | 0.0000 | . |
| iq*ses | 1 1 | 1 | 0.2993 | 0.5817 | -0.8408 | 1.4393 | 0.26 | 0.6069 |
| iq*ses | 1 2 | 1 | -0.7469 | 0.5692 | -1.8625 | 0.3687 | 1.72 | 0.1895 |
| iq*ses | 1 3 | 1 | 0.2001 | 0.6061 | -0.9879 | 1.3881 | 0.11 | 0.7413 |
| iq*ses | 1 4 | 0 | 0.0000 | 0.0000 | 0.0000 | 0.0000 | . |
| iq*ses | 2 1 | 1 | -0.3036 | 0.5794 | -1.4392 | 0.8321 | 0.27 | 0.6004 |
| iq*ses | 2 2 | 1 | -0.6241 | 0.5633 | -1.7282 | 0.4799 | 1.23 | 0.2679 |
| iq*ses | 2 3 | 1 | 0.0101 | 0.6070 | -1.1796 | 1.1999 | 0.00 | 0.9867 |
| iq*ses | 2 4 | 0 | 0.0000 | 0.0000 | 0.0000 | 0.0000 | . |
| iq*ses | 3 1 | 1 | -0.7575 | 0.5905 | -1.9148 | 0.3999 | 1.65 | 0.1996 |
| iq*ses | 3 2 | 1 | -1.4171 | 0.5746 | -2.5433 | -0.2910 | 6.08 | 0.0137 |
| iq*ses | 3 3 | 1 | -0.2082 | 0.6113 | -1.4063 | 0.9899 | 0.12 | 0.7334 |
| iq*ses | 3 4 | 0 | 0.0000 | 0.0000 | 0.0000 | 0.0000 | . |
| iq*ses | 4 1 | 0 | 0.0000 | 0.0000 | 0.0000 | 0.0000 | . |
