# Output 8.2 PROC LOGISTIC Output for PTSD Data

| Analysis of Maximum Likelihood Estimates |
| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
| Intercept | 1 | 1.4246 | 0.8287 | 2.9554 | 0.0856 |
| control | 1 | -0.9594 | 0.2047 | 21.9760 | <.0001 |
| problems | 1 | 0.2956 | 0.0505 | 34.3081 | <.0001 |
| sevent | 1 | 0.3557 | 0.0804 | 19.5912 | <.0001 |
| cohe s | 1 | -0.1782 | 0.0373 | 22.8583 | <.0001 |
| time 1 | 1 | 0.3566 | 0.2055 | 3.0116 | 0.0827 |
| time 2 | 1 | 0.2499 | 0.2041 | 1.4993 | 0.2208 |
| time 3 | 0 | 0 | . | . | . |

The problem with this analysis is that it assumes that the three observations for each person are independent. That’s unlikely at face value and contradicted by the data. As Table 8.1 shows, the association between PTSD at time 1 and time 2 is quite strong, and even stronger between time 2 and time 3.

# Table 8.1 Association between Symptoms of PTSD at Adjacent Time Points

| PTSD at Time 1 | %With PTSD at Time 2 | | PTSD at Time 2 | %With PTSD at Time 3 |
| Yes | 47% | | Yes | 51% |
| No | 18% | | No | 10% |

Of course, the real question is whether this association persists after controlling for the explanatory variables in the model. To answer that question, I included PTSD at time 1 in a logistic model predicting PTSD at time 2, along with the other explanatory variables that are in Output 8.2. The coefficient for PTSD at time 1 was highly significant, indicating dependence over time (output not shown).

What are the consequences? Even with dependence among the observations, the coefficients in Output 8.2 should be consistent estimates of the true coefficients, and, therefore, approximately unbiased. They are not efficient, however. That means that there are other ways of estimating the coefficients that make better use of the data, thereby producing