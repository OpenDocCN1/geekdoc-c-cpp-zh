# Output 8.21 Regression of PUBHOUSE with Matched-Pair Data Using GEE Adjustment for Matching

| Exchangeable Working Correlation |
|---|
| Correlation | 0.070850115 |

**Analysis Of GEE Parameter Estimates**

**Empirical Standard Error Estimates**

| Parameter | Estimate | Standard Error | 95% Confidence Limits | Z | Pr > \|Z\| |
|---|---:|---:|---:|---:|---:|
| Intercept | -0.0124 | 0.3487 | -0.6959, 0.6710 | -0.04 | 0.9716 |
| STAYBABY | -0.3100 | 0.1074 | -0.5206, -0.0995 | -2.89 | 0.0039 |
| BLACK | -0.1462 | 0.1197 | -0.3809, 0.0884 | -1.22 | 0.2218 |
| KIDS | 0.1790 | 0.0469 | 0.0871, 0.2709 | 3.82 | 0.0001 |
| DOUBLEUP | -0.1138 | 0.1168 | -0.3427, 0.1151 | -0.97 | 0.3298 |
| AGE | -0.0188 | 0.0108 | -0.0400, 0.0024 | -1.74 | 0.0819 |
| DAYS | 0.0043 | 0.0007 | 0.0030, 0.0056 | 6.52 | <.0001 |

Results in Output 8.21 differ only slightly from those in Output 8.20, which were not adjusted for matching. In particular, the coefficient for STAYBABY is about the same, while its estimated standard error is slightly reduced, from .1167 to .1074. Consistent with the small change is the estimated “residual” correlation between within-pair observations of only .07. One reason why the results don’t differ more is that the inclusion of DAYS in Output 8.20 is itself a partial adjustment for matching. When DAYS is omitted from the model, the residual correlation is .20.

In my opinion, GEE is usually the best method for adjusting for treatment-control matching. Although the example consisted of matched pairs, the method is identical for one-to-many matching or many-to-many matching. One alternative to GEE is the mixed model discussed in Section 8.5, but this is likely to give very similar results in most applications. Another widely recommended alternative is the conditional logit (fixed effects) model of Section 8.6. Unfortunately, this method often involves a substantial loss of data with concomitant increases in standard errors. The shelter stay data provides a good example of this loss. The LOGISTIC program for the fixed-effects model with matched-pair data is