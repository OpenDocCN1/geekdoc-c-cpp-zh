Call:
lm(formula = cost ~ date, data = nuclear)

Residuals:

| Min 1Q Median 3Q Max |
| -176.00 -105.27 -25.24 58.63 359.46 |

Coefficients:

Signif. codes: 0 *** 0.001 ** 0.01 * 0.05 ' ' 0.1 ' ' 1

Residual standard error: 137 on 30 degrees of freedom
Multiple R-squared: 0.3727, Adjusted R-squared: 0.3517
F-statistic: 17.82 on 1 and 30 DF, p-value: 0.000201

In you provide the model you want to update as the first argument, and the second argument, formula, tells how to update the model. Using the . notation, the instruction is to update muc. by adding date as a predictor, in a fitted model object of the class of the first argument. A summary of the new model, muc.1, to see this.
So, let's keep going! Call again, but pass muc.1 as your first argument.

```
R> add(muc.1,scope=".+date+t1+t2+cap+pr+ne+ct+bw+cum.n+pt,test="F")
Single term additions
```

| DF of Sq RSS AIC value Pr(F> |
| <1> 56287 316.80 |
| t1 15322 54715 317.92 0.8115 0.350843 |
| t2 66816 49476 314.67 3.9959 0.050606 |
| cap 189732 371305 305.64 14.7471 0.000163 *** |
| pr 40278 558180 318.57 0.0200 0.650968 |
| ne 92256 470583 313.07 5.6854 0.023861 * |
| ct 54794 508043 318.52 3.1277 0.0874906 |
| bw 1240 561597 318.73 0.0640 0.820147 |
| cum.n 4658 558179 318.53 0.2420 0.626454 |
| pt 90587 472250 313.18 5.5628 0.025997 * |

Signif. codes: 0 *** 0.001 ** 0.01 * 0.05 ' ' 0.1 ' ' 1