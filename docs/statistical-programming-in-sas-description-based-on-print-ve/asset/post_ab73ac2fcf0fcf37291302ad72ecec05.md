
# **Display 5.20** ANOVA table results from comparing mean log-bacterial growth for different packaging

| Source | DF | Sum of Squares | Mean Square | F Value | Pr > F |
|---|---|---:|---:|---:|---:|
| Model | 3 | 32.87280000 | 10.95760000 | 94.58 | <.0001 |
| Error | 8 | 0.92680000 | 0.11585000 |  |  |
| Corrected Total | 11 | 33.79960000 |  |  |  |

| R-Square | Coeff Var | Root MSE | logcount Mean |
|---:|---:|---:|---:|
| 0.972580 | 5.768940 | 0.340367 | 5.900000 |

| Source | DF | Type I SS | Mean Square | F Value | Pr > F |
|---|---:|---:|---:|---:|---:|
| Condition | 3 | 32.87280000 | 10.95760000 | 94.58 | <.0001 |

| Source | DF | Type III SS | Mean Square | F Value | Pr > F |
|---|---:|---:|---:|---:|---:|
| Condition | 3 | 32.87280000 | 10.95760000 | 94.58 | <.0001 |

The statement immediately following the MODEL statement (`means condition / bon tukey scheffe cldiff lines`) requests a pairwise comparison between the packaging conditions. While SAS offers many multiple comparison procedures, only three procedures—Bonferroni (bon), Tukey (tukey) and Scheffe (scheffe)—are invoked in this example. `cldiff` requests confidence intervals for the pairwise differences between packaging conditions. `lines` requests a graphical display of the results of comparing all mean differences. For `tukey`, `cldiff` generates Display 5.21.

# Display 5.21 Tukey ANOVA table results with CLDIFF specified

| NOTE: This test controls the Type I experimentwise error rate. |
| Alpha | 0.05 |
| Error Degrees of Freedom | 8 |
| Error Mean Square | 0.11585 |
| Critical Value of Studentized Range | 4.52880 |
| Minimum Significant Difference | 0.89 |

| Comparisons significant at the 0.05 level are indicated by *** |
| condition Comparison | Difference Between Means | Simultaneous 95% Confidence Limits |  |
| Plastic - Mixed | 0.2200 | -0.6700 | 1.1100 |  |
| Plastic - Vacuum | 1.9800 | 1.0900 | 2.8700 | *** |
| Plastic - Co2 | 4.1200 | 3.2300 | 5.0100 | *** |
| Mixed - Plastic | -0.2200 | -1.1100 | 0.6700 |  |
| Mixed - Vacuum | 1.7600 | 0.8700 | 2.6500 | *** |
| Mixed - Co2 | 3.9000 | 3.0100 | 4.7900 | *** |
| Vacuum - Plastic | -1.9800 | -2.8700 | -1.0900 | *** |
| Vacuum - Mixed | -1.7600 | -2.6500 | -0.8700 | *** |
| Vacuum - Co2 | 2.1400 | 1.2500 | 3.0300 | *** |
| Co2 - Plastic | -4.1200 | -5.0100 | -3.2300 | *** |
| Co2 - Mixed | -3.9000 | -4.7900 | -3.0100 | *** |
| Co2 - Vacuum | -2.1400 | -3.0300 | -1.2500 | *** |

The LINES statement for the Tukey multiple comparison procedure produces the output shown in Display 5.22.

# Display 5.22 Tukey ANOVA table results with LINES specified

| Means with the same letter are not significantly different |
|---|---|---|---|
| Tukey Grouping | Mean | N | condition |
| A | 7.4800 | 3 | Plastic |
| A |  |  |  |
| A | 7.2600 | 3 | Mixed |
|  |  |  |  |
| B | 5.5000 | 3 | Vacuum |
|  |  |  |  |
| C | 3.3600 | 3 | Co2 |

Both Display 5.21 and 5.22 show that the mean log-bacterial growth for the CO₂ packaging condition is significantly lower than vacuum, which is significantly lower than plastic or mixed. This fact is shown in Display 5.21 because the mean comparisons yielding confidence intervals for the pairwise differences do not contain zero. In Display 5.22, this fact is shown because the lines have different letters (A, B, and C) associated with the different groups.

Following the MEANS statement are two statements, lsmeans condition / cl pdiff and lsmeans condition / cl pdiff adjust=Tukey. These statements request the means for the different groups, request confidence intervals for the mean response in each group (using a pooled variance estimate) and for the mean differences, and request a matrix of p-values for the pairwise tests of mean equality. The second LSMEANS statement applies a Tukey multiple comparison adjustment to the comparisons. The output from these two statements is shown in Display 5.23. Not surprising, the Tukey adjusted p-values are larger, and the simultaneous confidence intervals for the mean differences are wider when compared to their unadjusted counterparts. Other adjustments such as Bonferroni can be specified. When analyzing one treatment, MEANS and LSMEANS lead to identical results. However, differences surface in multi-factor studies if the treatments (combinations of factor levels) are unequally replicated. This is discussed in Section 5.4, “ANOVA Models—PROC GLM for an ANOVA Model with Two or More Factors.”

# Display 5.23 Pairwise comparisons via LSMEANS (Edited)

| condition | logcount LSMEANS | LSMEANS Number | 95% Confidence Limits |  |
|---|---|---|---|---|
| Plastic | 7.48000000 | 1 | 7.026844 | 7.933156 |
| Vacuum | 5.50000000 | 2 | 5.046844 | 5.953156 |
| Mixed | 7.26000000 | 3 | 6.806844 | 7.713156 |
| Co2 | 3.36000000 | 4 | 2.906844 | 3.813156 |

Least Squares Means for Effect Condition
Pr > |t| for H0: LSMeans(i)=LSMeans(j)
Dependent Variable: logcount
| i/j | 1 | 2 | 3 | 4 |
| 1 |  | <.0001 | 0.4514 | <.0001 |
| 2 | <.0001 |  | 0.0002 | <.0001 |
| 3 | 0.4514 | 0.0002 |  | <.0001 |
| 4 | <.0001 | <.0001 | <.0001 |  |

Least Squares Means for Effect Condition
| i | j | Difference Between Means | 95% Confidence Limits for LSMeans(i)-LSMeans(j) |  |
| 1 | 2 | 1.980000 | 1.339141 | 2.620859 |
| 1 | 3 | 0.220000 | -0.420859 | 0.860859 |
| 1 | 4 | 4.120000 | 3.479141 | 4.760859 |
| 2 | 3 | -1.760000 | -2.400859 | -1.119141 |
| 2 | 4 | 2.140000 | 1.499141 | 2.780859 |
| 3 | 4 | 3.900000 | 3.259141 | 4.540859 |

NOTE: To ensure overall protection level, only probabilities associated with preplanned comparisons should be used.

# Display 5.23 (continued)

| Adjustment for Multiple Comparisons: Tukey |
| condition | logcount LSMEANS | LSMEANS Number |
| Plastic | 7.48000000 | 1 |
| Vacuum | 5.50000000 | 2 |
| Mixed | 7.26000000 | 3 |
| Co2 | 3.36000000 | 4 |

Least Squares Means for Effect Condition
Pr > |t| for H0: LSMeans(i)=LSMeans(j)
Dependent Variable: logcount
| i/j | 1 | 2 | 3 | 4 |
| 1 |  | 0.0005 | 0.8564 | <.0001 |
| 2 | 0.0005 |  | 0.0010 | 0.0003 |
| 3 | 0.8564 | 0.0010 |  | <.0001 |
| 4 | <.0001 | 0.0003 | <.0001 |  |

The confidence limits for the differences in the mean log-bacterial counts between two packaging conclusions are similar to confidence intervals based on a pooled variance t-test. The mean squared error is used as an estimate of the pooled variance, and the degrees of freedom are adjusted accordingly. Try This at Home: Use PROC TTEST to compare two of the packaging conditions. How different are the confidence intervals for the mean difference from the (unadjusted) LSMEANS comparison when compared to PROC TTEST?

The qualitative conclusions from comparing the packaging conditions are similar. The LSMEANS statement becomes more interesting for multifactor analyses. The CONTRAST statement allows for tests of specific contrasts (i.e., linear combinations whose coefficients sum to zero—H0: Σ ci μi = 0 for Σ ci = 0). To test whether the mean response in the plastic condition is equal to the average of the mean response in the other three conditions, test H0: μplastic = 1/3 (μvacuum + μmixed + μCo2) or H0: 3 μplastic - 1 μvacuum - 1 μmixed - 1 μCo2 =0. This is specified using the following statement:

```
contrast 'plastic vs. rest' condition 3 -1 -1 -1;
```

This statement specifies the coefficients of the contrast and provides a label for output. The ORDER=DATA option in the GLM statement guarantees that the first coefficient, 3, corresponds to plastic (the first condition in the data set). The second coefficient, −1, corresponds to vacuum, and so on. The results of this contrast test are the following:

| Contrast | DF | Contrast SS | Mean Square | F Value | Pr > F |
|---|---|---|---|---|---|
| plastic vs. rest | 1 | 9.98560000 | 9.98560000 | 86.19 | <.0001 |

These results suggest that the plastic mean log-bacterial count differs from the average of the other three conditions. The final statement constructs a data set (new) with residuals that can be analyzed for checking model assumptions (e.g., homogeneity of variance):

```
output out=new p=yhat r=resid stdr=eresid;
```

The procedures following the GLM analysis—PROC SGPLOT and PROC UNIVARIATE—produce graphical displays that can be used for checking the model. (The output of these procedures is not included. Some of it isn’t very interesting when you have a total of only 12 observations.)

## 5.4 ANOVA Models—PROC GLM for an ANOVA Model with Two or More Factors

Multiple factors in a designed experiment are commonly analyzed using a factorial treatment structure. Suppose a three-factor study was conducted with each factor set at one of two levels (a 2x2x2 or 2³ design). These three factors in combination define eight treatments. Thus, the one-way ANOVA model from the previous section could be applied. It is more interesting to study the factor effects and their possible interactions. In a display of minimal imagination, label these factors A, B, and C. A model for the response of the lth replicate at the ith level of factor A, jth level of factor B, and kth level of factor C is Y_ijkl = μ + α_i + β_j + γ_k + αβ_ij + αγ_ik + βγ_jk + αβγ_ijk + ε_ijkl. To request the analysis of this model in PROC GLM, the following partial code can be used:

```
proc glm data=DSN;
class A B C;
model Y = A B C A*B A*C B*C A*B*C;
run;
```
