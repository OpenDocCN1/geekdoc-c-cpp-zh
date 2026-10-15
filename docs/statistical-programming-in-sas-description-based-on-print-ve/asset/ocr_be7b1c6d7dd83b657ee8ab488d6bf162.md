# Display 5.12 Fitting allometric regression models to predict brain weight from body weight assuming different intercept

| Analysis of Variance |
| Source | DF | Sum of Squares | Mean Square | F Value | Pr > F |
| Model | 2 | 26.95668 | 13.47834 | 142.86 | <.0001 |
| Error | 25 | 2.35867 | 0.09435 |  |  |
| Corrected Total | 27 | 29.31535 |  |  |  |

| Root MSE | 0.30716 | R-Square | 0.9195 |
| Dependent Mean | 1.92195 | Adj R-Sq | 0.9131 |
| Coeff Var | 15.98167 |  |  |

| Parameter Estimates |
| Variable | DF | Parameter Estimate | Standard Error | t Value | Pr > |t| |
| Intercept | 1 | 0.93879 | 0.08465 | 11.09 | <.0001 |
| logbody | 1 | 0.74855 | 0.04428 | 16.90 | <.0001 |
| idino | 1 | -2.26674 | 0.23024 | -9.84 | <.0001 |

From these fits, allowing dinosaurs to have a different intercept leads to better fits. In particular, the coefficient associated with this term is significantly different from zero. (See the test of IDINO.) The residual error is reduced from 0.442 to 0.094. The coefficient of determination is increased from 0.61 to 0.92. The model suggests that for all non-dinosaurs, the predicted log10(brain weight)i = 0.93879 + 0.74855 log10(body weight)i. For dinosaurs, the predicted log10(brain weight)i = 0.93879 + 0.74855 log10(body weight)i - 2.26674. Or, for dinosaurs, the predicted log10(brain weight)i = -1.32795 + 0.74855 log10(body weight)i. The predicted log10(brain weight) for the common intercept and different intercept models is generated as part of the data set mreexample2 in Display 5.13. The data are plotted with the predictions from each of the models.