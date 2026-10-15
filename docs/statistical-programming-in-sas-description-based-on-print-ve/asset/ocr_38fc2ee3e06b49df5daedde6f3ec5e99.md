# **Display 5.20** ANOVA table results from comparing mean log-bacterial growth for different packaging

| Source | DF | Sum of Squares | Mean Square | F Value | Pr > F |
|---|---:|---:|---:|---:|---:|
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