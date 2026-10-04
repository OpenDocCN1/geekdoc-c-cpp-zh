
pt 1 627 144692 289.33 0.0914 0.7654015

Signif. codes: 0 '***' 0.001 '**' 0.01 '*' 0.05 '.' .1 ' 1

One handy feature of drop1 is that its scope argument is optional. If you don't include code, it defaults to the intercept-only model which is the "most-reduced" model, which is usually a reasonable choice.

Before diving into the deletion process, remind yourself of the interpretation of what you're doing. Just as adding any term will improve the goodness-of-fit in forward selection, deleting any term in backward selection will always worsen the goodness-of-fit. The real question is the perceived significance of these changes in fit. In the same way as earlier, when you wanted to add only those that offer a statistically significant improvement in goodness-of-fit, when dropping terms, you only want to remove those that do not result in a statistically significant detriment to goodness-of-fit. As such, backward selection is the complete reverse of forward selection in the way it's carried out.

So, from the output of drop1, you want to choose the term to remove from the model that has the least significant effect of reducing the goodness of fit. In your words, you're looking for the term with the largest, nonsignificant p-value for its partial F-test—because dropping a term with a significantly small p-value would significantly worsen the predictive capacity of the regression model.

In the current example, it seems the predictor bs has the least significant effect on reducing the goodness-of-fit, so let's start the update by removing that term from nuc.

```R
nuc.1 <- update(nuc.0,"-bw")
```

Use of drop1 in this selection algorithm is the same as before; though, you use -a to signify the deletion of a term following the standard "what's already there". The process is then repeated using the latest model nuc:1.

```R
drop1(nuc.1,test="F")
Single deletions
```

Model:
| cost ~ date + t1 + t2 + cap + pr + ne + ct + cum.n + pt |
| Df | Sum of Sq | RSS | AIC | F value | Pr(F) |
|---|---|---|---|---|---|
| <none> | | | | 144238 | 289.23 |
| date | 1 | 55942 | 203180 | 297.72 | 8.5326 | 0.0079*** |
| t1 | 1 | 3124 | 147632 | 287.92 | 0.4765 | 0.49745 |
| t2 | 1 | 30717 | 174985 | 293.41 | 6.6852 | 0.04156 |
| cap | 1 | 159976 | 304214 | 311.11 | 24.4005 | 0.698e-05 *** |
| pr | 1 | 27140 | 173177 | 297.25 | 4.1395 | 0.05422 |
| ne | 1 | 86408 | 230646 | 302.25 | 13.1795 | 0.00147 ** |
| ct | 1 | 11815 | 165003 | 289.75 | 1.8021 | 0.19353 |
| cum.n | 1 | 24048 | 168286 | 292.17 | 3.6680 | 0.068557 |
| pt | 1 | 930 | 145168 | 287.44 | 0.1419 | 0.710039 |

Linear Model Selection and Diagnostics 539

---
Signif. codes: 0 *** 0.001 *** 0.01 '*' 0.05 '*' '.' ' ' ' 1

It would seem that pt is the most sensible effect to drop. Drop so and name the resulting object nuc.2.

```R
nuc.2 <- update(nuc.1,~-pt)
```

Now keep going, rechecking with a call to drop1 (not shown), and you'll find that the predictor t1 reveals itself as another viable deletion. Update your model with the predictor deleted; name the model object nuc.3.

```R
nuc.3 <- update(nuc.2,~-.t1)
```

Recheck the new nuc.3 with drop1. You should find the effect of ct remains nonsignificant, so delete and update again, giving you a new nuc.4.

```R
nuc.4 <- update(nuc.3,~-.ct)
```

Perform yet another check with drop1, this time on nuc.4. At this point, you might hesitate removing any more predictors, with significance varying strengths being associated with the effect of their deletion. Note, however, that for at least three of the remaining predictors, t2, pr, and cum.n, the statistical significance should probably be considered borderline at all—all of the cutoff levels of α = 0.01 and α = 0.05. This again emphasizes the active role researcher must play in model selection algorithms as forward or backward elimination; whether you should delete any variables from here is a difficult question to answer and is left up to your judgment.

Let's remain with nuc.4 as the final model. Summarizing, you're able to see the estimated regression parameters and the usual post-fit statistics.

```R
summary(nuc.4)
```

Call:
lm(formula = ~ + t2 + cap + pr + ne + cum.n, data = nuclear)

Residuals:

Min 1Q Median 3Q Max
-152.851 -53.929 -8.827 53.382 155.581

Coefficients:

Estimate Std. Error t value Pr(|t|)
(Intercept) -9.702e+03 1.294e+03 -7.495 7.55e-08 ***

Linear Model Selection and Diagnostics 539
