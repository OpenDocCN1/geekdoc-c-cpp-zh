# Output 2.6: GLIMMIX Results for Analysis of Number of Failures of Electronic Equipment

*** Fisher Scoring optimization technique up to iteration 10 ***
*** Identity Link ***

The GLIMMIX Procedure
| Optimization Information | | |
| Optimization Technique | Newton-Raphson |
| Fisher Scoring | to iteration 10 |

Scoring did not stop.
| Fit Statistics | | |
| Pearson Chi-Square | 8.90 |
| Pearson Chi-Square / DF | 1.27 |

Parameter Estimates | | |
| Effect | Estimate | Standard Error | DF | t Value | Pr > |t| |
| x1 | 0.1666 | 0.03486 | 7 | 4.78 | 0.0020 |
| x2 | 0.09040 | 0.06301 | 7 | 1.43 | 0.1945 |

| Covariance Matrix for Fixed Effects | | |
| Effect | Row | Col1 | Col2 |
| x1 | 1 | 0.001216 | -0.00196 |
| x2 | 2 | -0.00196 | 0.003970 |

Note that the optimization technique is Newton-Raphson by default. We requested to use the Fisher scoring method for the first 10 iterations. Since the algorithm converged in four iterations, the output results correspond to the Fisher scoring method. The message "Scoring did not stop" indicates convergence was achieved using the Fisher scoring method within the first 10 iterations. The value of the Pearson X2 is 8.90, which is divided by degrees of freedom to