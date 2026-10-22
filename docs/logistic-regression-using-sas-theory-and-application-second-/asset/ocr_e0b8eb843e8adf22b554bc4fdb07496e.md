# Output 8.3  PROC SURVEYLOGISTIC Output with Robust Standard Errors

| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
|---|---:|---:|---:|---:|---:|
| **Analysis of Maximum Likelihood Estimates** |  |  |  |  |  |
| **Intercept** | 1 | 1.4246 | 0.9065 | 2.4695 | 0.1161 |
| **control** | 1 | -0.9594 | 0.2281 | 17.6846 | <.0001 |
| **problems** | 1 | 0.2956 | 0.0517 | 32.6886 | <.0001 |
| **sevent** | 1 | 0.3557 | 0.0904 | 15.4726 | <.0001 |
| **cohes** | 1 | -0.1782 | 0.0469 | 14.4646 | 0.0001 |
| **time** 1 | 1 | 0.3566 | 0.1847 | 3.7278 | 0.0535 |
| **time** 2 | 1 | 0.2499 | 0.1728 | 2.0906 | 0.1482 |
| **time** 3 | 0 | 0 | . | . | . |

Comparing Output 8.2 with Output 8.3, we see that the coefficients are identical.

What *has* changed are the standard errors, which are somewhat larger in Output 8.3 for the first four variables. And since the chi-squares are calculated by dividing the parameter estimates by their standard errors, the chi-squares are somewhat lower than they were before. This doesn’t make a noticeable difference in the *p*-values, however, because they were so low to begin with.

The exceptions to this pattern are the robust standard errors for the two indicator variables for TIME, which are smaller than the conventional standard errors. But that’s consistent with a more general pattern: with robust standard errors, you tend to see the biggest percentage increase for variables that don’t change over time (like COHES) and somewhat smaller increases for variables that do change over time (like CONTROL, PROBLEMS, and SEVENT). For variables that change over time but do not vary across persons (like TIME itself), the robust standard errors are often smaller than conventional standard errors.

Now let’s see how to get the same results with PROC GENMOD, which is designed to estimate generalized linear models. These include linear models, logistic models, and the models for count data that we will examine in the next chapter. Here’s the GENMOD code for the PTSD data: