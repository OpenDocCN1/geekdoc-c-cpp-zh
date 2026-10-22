
Although it’s usually desirable to adjust for matching in the analysis, the appropriate adjustment methods are quite different for treatment-control and case-control matching. In brief, there are several ways to do it for treatment-control matching, but there is only one way for case-control matching. Let’s begin with a treatment-control example. Metraux and Culhane (1999) constructed a data set of 8,402 women who stayed in family shelters in New York City for at least one 7-day period during 1992. The data contained information on several pre-stay characteristics, events that occurred during the stay, and housing type subsequent to the stay. As our dependent variable, we’ll focus on whether or not the woman exited to public housing (PUBHOUSE), which was the destination for 48% of the sample. Our principal independent variable is STAYBABY, equal to 1 if a woman gave birth during her stay at the shelter, and 0 otherwise. Nine percent of the sample had a birth during the stay. Other independent variables are

- BLACK — 1=black race, 0=nonblack
- KIDS — Number of children in the household
- DOUBLEUP — 1=living with another family prior to shelter stay, 0 otherwise
- AGE — Age of woman at beginning of shelter stay
- DAYS — Number of days in shelter stay

The conventional approach to analysis would be to estimate a logistic regression model for the entire sample of 8,402 women. Results for doing that with PROC LOGISTIC are shown in Output 8.19. We see that although the odds of exiting to public housing increase with the number of children in the household, a birth during the stay reduces the odds by about 33 percent. Both of these effects are overshadowed by the enormous impact of the length of stay. Each additional day increases the odds of exiting to public housing by about 1%. (Not surprisingly, DAYS also has a correlation of .25 with STAYBABY—the longer a woman’s stay, the more likely it is that she gave birth during the stay.)

## Output 8.19 Logistic Regression of Exit to Public Housing

| Analysis of Maximum Likelihood Estimates |
| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
| Intercept | 1 | -1.7441 | 0.1543 | 127.7887 | <.0001 |
| STAYBABY | 1 | -0.4030 | 0.0990 | 16.5780 | <.0001 |
| BLACK | 1 | -0.1606 | 0.0586 | 7.5134 | 0.0061 |
| KIDS | 1 | 0.1835 | 0.0219 | 70.0082 | <.0001 |
| DOUBLEUP | 1 | -0.1903 | 0.0601 | 10.0145 | 0.0016 |
| AGE | 1 | -0.0227 | 0.00523 | 18.8239 | <.0001 |
| DAYS | 1 | 0.0114 | 0.000257 | 1973.0471 | <.0001 |

| Odds Ratio Estimates |
| Effect | Point Estimate | 95% Wald Confidence Limits |
| STAYBABY | 0.668 | 0.550 | 0.811 |
| BLACK | 0.852 | 0.759 | 0.955 |
| KIDS | 1.201 | 1.151 | 1.254 |
| DOUBLEUP | 0.827 | 0.735 | 0.930 |
| AGE | 0.978 | 0.968 | 0.988 |
| DAYS | 1.011 | 1.011 | 1.012 |

Now let’s estimate the effect of STAYBABY in a matched sample. I compared all 791 women who had a baby during the stay with an equal number of women who did not. To control for the effect of DAYS, I matched each woman who had a baby with a random draw from among those women whose length of stay was identical (or as close as possible). In this subsample, then, the correlation between STAYBABY and DAYS is necessarily .00.

Rosenbaum and Rubin (1983) argue that adjustment by matching is “usually more robust to departures from the assumed form of the underlying model than model-based adjustment on random samples . . . primarily because of reduced reliance on the model’s extrapolations.”

Despite the fact that 6,820 cases are discarded in the matched analysis, we’ll see that very little precision is lost in the estimation of the STAYBABY coefficient. I could have used the propensity score method to control for all the variables in Output 8.19, but I wanted to keep things simple, and the adjustment for DAYS would have dominated anyway.

Next, I estimated a logistic model for this matched-pair subsample without adjusting for the matching (see Output 8.20). Although the standard errors increase greatly for most of the variables (compared with those in Output 8.19), the loss of precision is quite small for the STAYBABY coefficient; its standard error only increases by about 18% relative to that in Output 8.19. The coefficient for STAYBABY declines somewhat in magnitude, but the matched subsample may be less prone to bias in this estimate than that in the full sample. Note that if we deleted DAYS from this model, the results for STAYBABY would hardly change at all because the two variables are uncorrelated, by design.

## Output 8.20 Regression of PUBHOUSE with Matched-Pair Data without Adjustment for Matching

| Analysis of Maximum Likelihood Estimates |
| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
| Intercept | 1 | -0.0317 | 0.3357 | 0.0089 | 0.9248 |
| STAYBABY | 1 | -0.3107 | 0.1167 | 7.0914 | 0.0077 |
| BLACK | 1 | -0.1322 | 0.1253 | 1.1139 | 0.2912 |
| KIDS | 1 | 0.1789 | 0.0465 | 14.8089 | 0.0001 |
| DOUBLEUP | 1 | -0.1046 | 0.1216 | 0.7397 | 0.3898 |
| AGE | 1 | -0.0188 | 0.0110 | 2.9045 | 0.0883 |
| DAYS | 1 | 0.00432 | 0.000443 | 95.4934 | <.0001 |

The problem with the analysis in Output 8.20 is that the matched pairs are not independent, which could lead to bias in the standard error estimates. One way to adjust for the matching is to use the GEE method discussed in Section 8.4. Here’s how:

```
PROC GENMOD DATA=casecont DESC;
    CLASS casenum;
    MODEL pubhouse=staybaby black kids doubleup age days /
        D=B;
    REPEATED SUBJECT=casenum / TYPE=EXCH;
RUN;
```

CASENUM is the unique identifier for each matched pair. Although I specified an exchangeable structure (TYPE=EXCH), all types of correlation structure are equivalent when there are only two observations per cluster.

## Output 8.21 Regression of PUBHOUSE with Matched-Pair Data Using GEE Adjustment for Matching

| Exchangeable Working Correlation |
|---|
| Correlation | 0.070850115 |

**Analysis Of GEE Parameter Estimates**

**Empirical Standard Error Estimates**

| Parameter | Estimate | Standard Error | 95% Confidence Limits | Z | Pr > \|Z\| |
|---|---|---:|---:|---:|---:|---:|
| Intercept | -0.0124 | 0.3487 | -0.6959, 0.6710 | -0.04 | 0.9716 |
| STAYBABY | -0.3100 | 0.1074 | -0.5206, -0.0995 | -2.89 | 0.0039 |
| BLACK | -0.1462 | 0.1197 | -0.3809, 0.0884 | -1.22 | 0.2218 |
| KIDS | 0.1790 | 0.0469 | 0.0871, 0.2709 | 3.82 | 0.0001 |
| DOUBLEUP | -0.1138 | 0.1168 | -0.3427, 0.1151 | -0.97 | 0.3298 |
| AGE | -0.0188 | 0.0108 | -0.0400, 0.0024 | -1.74 | 0.0819 |
| DAYS | 0.0043 | 0.0007 | 0.0030, 0.0056 | 6.52 | <.0001 |

Results in Output 8.21 differ only slightly from those in Output 8.20, which were not adjusted for matching. In particular, the coefficient for STAYBABY is about the same, while its estimated standard error is slightly reduced, from .1167 to .1074. Consistent with the small change is the estimated “residual” correlation between within-pair observations of only .07. One reason why the results don’t differ more is that the inclusion of DAYS in Output 8.20 is itself a partial adjustment for matching. When DAYS is omitted from the model, the residual correlation is .20.

In my opinion, GEE is usually the best method for adjusting for treatment-control matching. Although the example consisted of matched pairs, the method is identical for one-to-many matching or many-to-many matching. One alternative to GEE is the mixed model discussed in Section 8.5, but this is likely to give very similar results in most applications. Another widely recommended alternative is the conditional logit (fixed effects) model of Section 8.6. Unfortunately, this method often involves a substantial loss of data with concomitant increases in standard errors. The shelter stay data provides a good example of this loss. The LOGISTIC program for the fixed-effects model with matched-pair data is

As an example of the case-control design, we again use the data on shelter stays, but now with STAYBABY as the dependent variable rather than as an independent variable. Output 8.23 shows the results from estimating a logistic model (with PROC LOGISTIC) for the full data set of 8,402 women. We see evidence that the probability of having a baby during the shelter stay is higher for blacks, women with more children in the household, younger women, and those with longer shelter stays.

## Output 8.23 Logistic Regression of STAYBABY for Full Sample

| Response Profile |  |  |
| Ordered Value | STAYBABY | Total Frequency |
| 1 | 0 | 7611 |
| 2 | 1 | 791 |

| Analysis of Maximum Likelihood Estimates |  |  |  |  |
| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
| Intercept | 1 | -2.6802 | 0.2204 | 147.8532 | <.0001 |
| BLACK | 1 | 0.2857 | 0.0860 | 11.0466 | 0.0009 |
| KIDS | 1 | 0.1558 | 0.0287 | 29.5256 | <.0001 |
| DOUBLEUP | 1 | 0.1497 | 0.0832 | 3.2351 | 0.0721 |
| AGE | 1 | -0.0467 | 0.00772 | 36.6776 | <.0001 |
| DAYS | 1 | 0.00447 | 0.000224 | 399.7093 | <.0001 |

Now let’s re-estimate the model for the 791 pairs of women who are matched by number of days of shelter stay. The LOGISTIC output without adjustment for matching is shown in Output 8.24.

## Output 8.24 Logistic Regression of STAYBABY for Matched Pairs, No Adjustment for Matching

| Response Profile |  |  |
| Ordered Value | STAYBABY | Total Frequency |
| 1 | 0 | 791 |
| 2 | 1 | 791 |
