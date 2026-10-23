each response category. The probabilities are measured as the vertical distance between the curves, with the total across all Y category probabilities sum to 1.

# Figure 3.25 Interpreting the Logistic Plot

![](bbox=[0.15, 0.145, 0.85, 0.4])

# Whole Model Test

| Model | -LogLikelihood | DF | ChiSquare | Prob>ChiSq |
| Difference | 1.693202 | 1 | 3.386404 | 0.0657 |
| Full | 95.195141 |  |  |  |
| Reduced | 96.888343 |  |  |  |
| RSquare (U) | 0.0175 |  |  |  |
| Observations (or Sum Wgts) | 98 |  |  |  |
| Converged by Gradient |  |  |  |  |

# Parameter Estimates

| Term | Estimate | Std Error | ChiSquare | Prob>ChiSq |
| Intercept[Low] | -2.0414108 | 0.6932111 | 8.67 | 0.0032* |
| Intercept[Moderate] | 0.52799389 | 0.6607462 | 0.64 | 0.4242 |
| Size of Load (lbs) | 0.00630744 | 0.0034849 | 3.28 | 0.0703 |

Markers for the data are drawn at their x-coordinate, with the y position jittered randomly within the range corresponding to the response category for that row. You can see that the points tend to push the lines apart and make vertical space where they occur in numbers, and allow the curves to get close together where there is no data. The data pushes the curves because the criterion that is maximized is the product of the probabilities fitted by the model. The fit tries to avoid points attributed to have a small probability, which are points crowded by the curves of fit.

There are only a couple of options in the Logistic drop-down menu (see Figure 3.26)—turning the plot on and off through the Logistic Plot command, and Script options. (See “Script Submenu,” p. 66 for details on scripting options.)

# The Whole Model Test Table

The Whole Model Test table shows if the model fits better than constant response probabilities. This table is analogous to the Analysis of Variance table for a continuous response model. It is a specific likelihood-ratio Chi-square test that evaluates how well the categorical model fits the data. The negative sum of logs of the observed probabilities is called the negative log-likelihood (−LogLikelihood). The