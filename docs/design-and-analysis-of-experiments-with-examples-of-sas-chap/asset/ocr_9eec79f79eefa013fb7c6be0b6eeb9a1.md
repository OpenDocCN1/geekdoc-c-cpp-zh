After incorporating this transformation, the plot of residuals versus cell means is shown in Figure 2.8. It can be seen in this figure that the spread or variability of the residuals is nearly the same for each value of the predicted value or log cell mean.

# Figure 2.8 Plot of Residuals versus Cell means after \( y^\lambda \) Transformation for Bread Rise Experiment

![](bbox=[0.102, 0.225, 0.845, 0.52])

This transformation also makes the F-test more sensitive. The ANOVA table for the transformed response is shown below, where it can be seen that the P-value has decreased from 0.042 (before transformation) to 0.0227 (after transformation).

The GLM Procedure

Dependent Variable: height

| Source | DF | Sum of Squares | Mean Square | F Value | Pr > F |
|---|---|---|---|---|---|
| Model | 2 | 0.01305604 | 0.00652802 | 5.94 | 0.0227 |
| Error | 9 | 0.00989833 | 0.00109981 | | |
| Corrected Total | 11 | 0.02295437 | | | |

Even when transformations are used to justify the assumptions of the analysis and make the F-test more sensitive, the results are normally reported on the original scale. For example, it would be confusing to talk about the (dough height).-294869 in a report.