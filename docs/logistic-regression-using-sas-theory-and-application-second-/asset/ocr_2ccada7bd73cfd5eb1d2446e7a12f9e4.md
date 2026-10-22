| Parameter | DF | Estimate | Standard Error | Wald 95% Confidence Limits | Wald Chi-Square | Pr > ChiSq |
|---|---:|---:|---:|---|---:|---:|
| *happyq*year | 2 | 1 | -0.0900 | 0.0526; -0.1932 to 0.0131 | 2.93 | 0.0870 |
| *happyq*year | 3 | 0 | 0.0000 | 0.0000; 0.0000 to 0.0000 | . | . |
| *married*happyq | 1 | -0.8020 | 0.0453 | -0.8908 to -0.7131 | 312.97 | <.0001 |
| Scale | 0 | 1.0000 | 0.0000 | 1.0000 to 1.0000 |  |  |

**Analysis Of Maximum Likelihood Parameter Estimates**

Looking first at the deviance (and Pearson chi-square), we see strong evidence that the fitted model is unsatisfactory: the deviance is more than five times the degrees of freedom. This is similar to what we found in Output 6.10 when we estimated the equivalent logit model by weighted least squares. Although there is little evidence for an effect of YEAR, the chi-square for MARRIED is quite large. The parameter estimate for the marital status effect (MARRIED*HAPPYQ) is −.8020. Again this is quite close to the WLS estimate of −.8035 in Output 6.7. Because higher values of HAPPYQ indicate lower happiness and MARRIED=1 for married, otherwise 0, the negative sign of the coefficient tells us that married people are happier. To be more specific, if we contrast the categories “very happy” and “pretty happy,” the odds of a married person being in the latter category are exp(−.8020)=.45 times the odds of an unmarried person. To put it another way, married people are about twice as likely (on the odds scale) as unmarried people to be in the happier category. Because of the constraints on the model, the same statement can be made about the contrast between “pretty happy” and “not too happy”—married people are about twice as likely as unmarried people to be in the happier category.

Given the poor fit of the model, we must be wary of these interpretations. But how can the model be improved? There are two possibilities. We can allow an interaction between year and marital status in their effects on happiness, which corresponds to a three-way interaction in the loglinear model. Or, we can relax the adjacent-categories constraint and fit a regular multinomial logit model. To fit the interaction model, we use the following statement:

```
MODEL count=year|married happy year*happyq married*happyq
      married*year*happyq / D=P ;
```