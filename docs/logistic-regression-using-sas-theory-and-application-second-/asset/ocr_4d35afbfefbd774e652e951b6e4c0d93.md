# Output 7.4 Travel Model with MODE as a CLASS Variable

| Type 3 Analysis of Effects |
| Effect | DF | Wald Chi-Square | Pr > ChiSq |
| MODE | 3 | 12.6107 | 0.0056 |

| Analysis of Maximum Likelihood Estimates |
| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
| MODE 1 | 1 | -0.0171 | 0.1849 | 0.0085 | 0.9263 |
| MODE 2 | 1 | 0.0656 | 0.1812 | 0.1311 | 0.7173 |
| MODE 3 | 1 | -0.6763 | 0.2242 | 9.0973 | 0.0026 |
| MODE 4 | 0 | 0 | . | . | . |

| Odds Ratio Estimates |
| Effect | Point Estimate | 95% Wald Confidence Limits |
| MODE 1 vs 4 | 0.983 | 0.684 | 1.412 |
| MODE 2 vs 4 | 1.068 | 0.749 | 1.523 |
| MODE 3 vs 4 | 0.508 | 0.328 | 0.789 |

In Output 7.5, we see the results of combining these two models. The COST coefficient is now in the expected direction with a p-value below .05. The terminal time coefficient has increased markedly so that now each additional minute results in a 9% reduction in the odds of choice. The coefficients for the mode dummies are all much larger and highly significant. People overwhelmingly prefer not to go by car.

What’s going on here? The coefficients for the mode dummies in Output 7.5 represent relative preferences for these modes after differences in the other variables are taken into account. Because terminal time is 0 for car travel, there’s a strong correlation between terminal time and the mode dummies. It appears that the main reason people like to travel by car is the absence of terminal waiting. After terminal time is taken into account, car travel seems to be unappealing. The coefficients for the time and cost variables can be interpreted as representing the effects of these variables after taking account of the overall preference for each mode compared with the others.