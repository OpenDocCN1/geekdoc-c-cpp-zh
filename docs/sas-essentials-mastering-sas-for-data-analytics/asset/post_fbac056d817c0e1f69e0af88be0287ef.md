
laboratories for his experiment. In this case, LAB would be a random effect. Two-way ANOVA models are classified with the following scheme:

- Both factors fixed: Model I ANOVA
- Both factors random: Model II ANOVA
- One random, fixed: Model III ANOVA

In this section, we will assume that both factors (A and B) are fixed, and we illustrate an analysis for a Model I ANOVA, but we will not provide an example of a Model III ANOVA which will be described in the following section.

When gathering data for this fixed-factor ANOVA design, the p×q possible combinations of factors (cells), subjects should be randomly assigned to a treatment in such a way to balance the number of subjects per cell. However, if the data are not balanced, an analysis can still be performed with PROC GLM (but not with PROC ANOVA).

There are some additional calculation issues involving the unbalanced case that are not discussed here. Generally, in the unbalanced case, the Type III sums-of-squares are returned. Moreover, the dependent variable should be a quantitative variable whose distribution within each level of the p×q (p by q) combinations is approximately normal with equal variances among combinations. (Some of these issues are relaxed when using PROC MIXED.)

There are two types of hypotheses used in a two-factor Model I design: hypotheses about interaction effects and main effects. The interaction effect should be examined first as follows:

$H_0$: There is no interaction effect.
$H_a$: There is an interaction effect.

Interaction implies that the pattern of means across groups is inconsistent (as illustrated in Figure 14.4a). If there is an interaction effect, main effects cannot be examined directly because the interaction effect shows that differences across one main effect are not consistent across all levels of the other factor.

Thus, if there is no interaction effect, it makes sense to test hypotheses about main effects. The “main effects” for factor A are as follows:

$H_0$: Means are equal across levels of A summed over B.
$H_a$: Means are not equal across levels of A summed over B.

Similarly, for factor B:

$H_0$: Means are equal across levels of B summed over A.
$H_a$: Means are not equal across levels of B summed over A.

The results of these three tests (interaction and two main effects) are given in an analysis of variance table as F-tests. A low p-value (usually <0.05) for a test indicates evidence to reject the null hypothesis in favor of the alternative.

# HANDS-ON EXAMPLE

This example (adapted from data 404 in Hand, Doly, McConway, Lunn, and Ostrowski [1994]) concerns a study on weight loss for those meeting about dieting. A variable called CONDITION indicates whether the patient received a weight loss (CONDITION=1) or not (CONDITION=2). The STATUS variable indicates whether the patient had already been trying to lose weight before the series of meetings (STATUS=1) or not (STATUS=2).

Both factors are assumed to be fixed effects for this example, and there are an unequal number of subjects in each category. For this case, PROC GLM can be used.

Open the program file AGLM_2FACTOR.SAS.

```
DATA SLIM;
INPUT CONDITION STATUS RESPONSE;
DATALINES;
1 -13.67 1 -12.85 1 1 -9.55 5 1 -17.03 1 13.61
2 -9.91 2 2.48 1 2.84 1 2.6 1 2 20.2 2 -73
2 -30.05 1 -5.68 1 -3.44 1 -7.18 2 -3.40 1 -74
1 -23.29 1 -4 2 -2.31 1 -3.42 1 -7.49 1 -13.62
1 -73.54 1 -1.91 2 -4.2 2 -12.01 2 1 -8.35
2 5.94 2 -1.91 2 -4.0 2 -5.19 2 0 2 -2.8

RUN;
TITLE "Two-Way ANOVA Example";
PROC GLM;
CLASS CONDITION STATUS;
MODEL RESPONSE=CONDITION STATUS CONDITION*;
MEANS CONDITION STATUS CONDITION*;

RUN;
QUIT;
```

Recall that in the MODEL statement, the dependent variable (RESPONSE) appears to the left of the equal sign and the independent variables (CONDITION and STATUS) appear to the right. The CONDITION*STATUS component of the model statement is the interaction term. The two factors, CONDITION and STATUS, are listed in the CLASS statement because they are categorical variables.

2. Run this program and observe the output, partially illustrated in Table 14.5. This is output from the first PROC GLM statement in the code. Note that the overall model is significant (p=0.04), indicating the presence of some differences in means. Note also that because of the unequal number of observations per cell, the Type III sums-of-squares (SS) give different results. It is recommended that Type III SS be used, and only that SS table is given in Table 14.5.

3. For this analysis, first examine the interaction effect (the CONDITION*STATUS row) in the Type III ANOVA table. Because p=0.7872, there is no evidence of interaction. As mentioned previously:

- If there is no interaction, examine the main effects.

### 347: ANALYSIS OF VARIANCE (PART II)

Because there is no interaction, examine the main effects by comparing means.

# TABLE 14.5 Results from a Two-Factor ANOVA

| Source | DF | Sum of Squares | Mean Square | F Value | Pr > F |
|---|---|---|---|---|---|
| Model | 3 | 309.004 | 103.003 | 3.13 | 0.0402 |
| Error | 30 | 967.604 | 32.920 | | |
| Corrected Total | 33 | 1276.616 | | | |
| CONDITION | 1 | 61.547 | 61.547 | 1.87 | 0.1686 |
| STATUS | 1 | 293.105 | 293.105 | 8.90 | 0.0056 |
| CONDITION*STATUS | 1 | 2.443 | 2.443 | 0.07 | 0.7872 |

- If there is no interaction, examine the main effects.

### 348: MARGINAL MEANS

# TABLE 14.6 Marginal Means for Levels of STATUS

| Level of STATUS | N | Mean | Std Dev |
|---|---|---|---|
| 1 | 16 | -5.87562500 | 7.17206058 |
| 2 | 18 | -0.91500000 | 3.63062829 |

![](img/6113440fee6085d6edba5f406f541c2_348_0.png)

Figure 14.5 Interaction plot for the two-factor ANOVA example

Also included in the output are boxplots by STATUS and CONDITION (not shown here) that provide a visual look at the distribution and location for those.

# 14.2 GOING DEEPER: TWO-FACTOR ANOVA USING PROC MIXED

PROC MIXED performs mixed-model analysis of variance and repeated measures analysis of variance with covariance structure modeling. PROC MIXED has features not available in PROC GLM. Briefly, here are some of the major differences between PROC GLM and PROC MIXED in relation to two-factor ANOVA analysis:

# PROC GLM

- Is designed primarily for fixed effects models.
- Calculates based on ordinary least squares and method of moments.
- Defines all effects as fixed and adjusts for random effects after estimation.
- Can perform mixed model analysis, but some results are not optimally calculated.
