
Historically, this led researchers to create “factor scores,” which weighted each item by the factor loading to more closely approximate what a latent variable score might be. As we discussed in Chapter 9, we do not believe this is a good idea. However, there is not currently a good way to deal with this theoretical issue when using alpha (in our opinion). Those interested in estimating internal consistency via alpha must simply be aware of its violation of the assumption of unique item contribution and live with it.

## Estimation of Alpha in SAS

Estimation of Cronbach’s alpha is extremely easy in SAS. It is done using the CORR procedure. The ALPHA option must be included on the CORR statement to request SAS to output estimates of alpha, and all the variables to be included in the alpha estimate should be listed on the VAR statement (or they can be referenced by a prefix, e.g., EngProb: ). An example of the syntax to produce estimates for the engineering problem-solving items in the engineering data is presented below. It is followed by a screenshot of the output produced by the ALPHA option.

```
proc corr data=engdata alpha;
var EngProb:;
run;
```

### Figure 11.1 PROC CORR output requested by the ALPHA option

### Cronbach Coefficient Alpha

| Variables | Alpha |
|---|---|
| Raw | 0.958800 |
| Standardized | 0.959151 |

### Cronbach Coefficient Alpha with Deleted Variable

| Deleted Variable | Raw Variables - Correlation with Total | Raw Variables - Alpha | Standardized Variables - Correlation with Total | Standardized Variables - Alpha |
|---|---|---|---|---|
| EngProbSolv1 | 0.835290 | 0.953610 | 0.834642 | 0.954113 |
| EngProbSolv2 | 0.795291 | 0.956088 | 0.795975 | 0.956439 |
| EngProbSolv3 | 0.855386 | 0.952396 | 0.855698 | 0.952837 |
| EngProbSolv4 | 0.877468 | 0.951141 | 0.877592 | 0.951502 |
| EngProbSolv5 | 0.871148 | 0.951451 | 0.871712 | 0.951862 |
| EngProbSolv6 | 0.855193 | 0.952449 | 0.855418 | 0.952854 |
| EngProbSolv7 | 0.858709 | 0.952188 | 0.858970 | 0.952638 |
| EngProbSolv8 | 0.797570 | 0.956172 | 0.797903 | 0.956323 |

As you can see in Figure 11.1 on page 188, the ALPHA option produces a lot more than a single alpha estimate! The first table provides a raw and standardized estimate of Cronbach’s alpha. You should use the raw alpha if you are inputting your original data into the CORR procedure, and you should use the standardized alpha if you are inputting standardized versions of your variables (e.g., z-scores) into the CORR procedure. You would use standardized versions of your variables if some of the items in the scale contained different numbers of response options (e.g., three dichotomous items and five Likert-type 5-point items). In the current example, we input the unstandardized engineering items into the scale. Thus, we will interpret the raw alpha.

The second table provides item-total correlations and revised estimates of alpha based on removal of items. The item-total correlations are the correlations between each individual item and the total composite score computed as the average or sum of the items. We expect items to be highly correlated with the total score as it represents the construct the item is intended to measure. Items with low item-total correlations can be scrutinized for potential removal. The revised alpha estimates represent the Cronbach’s alpha if a particular item was removed from the scale. A revised alpha estimate that is larger than our alpha indicates that an item contributes unique variance that reduces our overall reliability. This unique variance can in fact be unwanted error associated with an item. In that case you might consider removing the item, or it could be construct-relevant variance that is not captured by the other items, in which case you would want to keep the item. Knowledge of the construct must be used to guide decisions about item removal. Finally, similar to our interpretation of the first table, we would interpret the raw or standardized versions of these estimates based on the format of our data.

The engineering problem-solving scale demonstrates good internal consistency. It has a strong alpha of .95. The item-total correlations range from .80 to .88, and none of the revised alphas exceeds the original estimate. Unless we had a content-based reason for removing an item (e.g., an item is related but does not directly reflect problem solving), we would recommend making no changes to this scale.

## Would Error-Free Measurement Make a Real Difference?

### A Demonstration with Effect Sizes

To give a concrete example of how important good measurement is, we can use an example from the first author's survey of the educational psychology literature (Osborne, 2008). This survey consisted of recording all effects from all quantitative studies published in the Journal of Educational Psychology (usually considered one of our top empirical journals) during the years 1998 to 1999.

The mean effect size and the reliability coefficient (Cronbach's α), if reported, were used to identify nine potential measurement scenarios. First, a small, average, and large observed effect size were determined as the effect size one standard deviation below the mean (Cohen's d = .31), the mean effect size (Cohen's d = .68), and the effect size one standard deviation above the mean (Cohen's d = 1.05). We transformed the Cohen's d effect sizes into simple correlation coefficients (formulas and conversions derived from information in Cohen, 1988) to aid in interpretation of the results. This left us with a “small” observed effect of r = .16, an “average” observed effect of r = .32, and a “large” observed effect of r = .46. Next, we identified indicators of poor, average, and good reliability based on the reliability estimates one standard deviation below the mean reliability (α = .70), the mean reliability (α=.80), and one standard deviation above the mean reliability (α = .90). Finally, we created a cross tabulation of the three effect size conditions (small, average, large) by the three reliability conditions (poor, average, good) and examined what the true effect could be in the nine different scenarios that result. Table 11.1 on page 190 summarizes the results.

As we can see in the table below, the observed effects substantially underestimated the true effects. For example, looking at an average observed effect (r = 0.32), we can see that even if reliability was “good” (α = .90), the true effect (r = .36) is underestimated by 30%. With "average" reliability (α = 0.80) we can see this effect is underestimated by 60%, and by over 100% if alphas were 0.70 (which is often considered acceptable in top journals).

### Table 11.1 True effect by instrument reliability and observed effect

| Reliability | Small (r = .16, r² = .025) | Average (r = .32, r² = .10) | Large (r = .46, r² = .21) |
|---|---|---|---|
| Poor (α = .70) | r = .23 r² = .05 | r = .46 r² = .21 | r = .66 r² = .43 |
| Average (α = .80) | r = .20 r² = .04 | r = .40 r² = .16 | r = .58 r² = .33 |
| Good (α = .90) | r = .18 r² = .03 | r = .36 r² = .13 | r = .51 r² = .26 |

Note: This data is adapted from that originally published in Osborne (2008).

## An Example with the Coefficient of Determination

We now review an example from the first author's personal research on identification with academics (self-concept vis-a-vis school). In one study a long while ago, he administered two closely related scales (the School Perceptions Questionnaire and the Identification with School questionnaire, Osborne, 1997; Voelkl, 1997) to high school students. Alphas were calculated to be α = 0.88 and 0.81, respectively. These levels are widely considered "good." After averaging the items to create composite scores and testing assumptions, the simple correlation was calculated to be r = 0.75, which translates to a coefficient of determination (% variance accounted for) of 0.56. This is generally a pretty strong correlation for the social sciences, and is reasonable considering these are two measures of similar constructs. The corrected correlation (formulas available in many places including Cohen, Cohen, West, & Aiken, 2003) is calculated to be r = 0.89, which would represent a coefficient of determination of 0.79. If we assume that this corrected effect size of 0.79 is the correct population estimate, the original correlation between two measures with "good" reliability lost almost 30% of the effect size.

Although we cannot directly know the population correlation for this example, we can simulate what perfect measurement might yield as a correlation between these two variables using AMOS structural equation modeling software to construct latent variables representing each of these scales. Although structural equation modeling (SEM) is a relatively advanced
