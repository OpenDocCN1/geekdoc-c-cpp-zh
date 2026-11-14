tests for whole-plot effects are less sensitive. The REML estimated whole-plot and subplot error variances are shown at the bottom on the right side of the table. Letsinger et al. (1996) showed that when \(\sigma^2_\delta/\sigma^2 < 0.25\) the least squares estimates will be reasonably close to the REML estimates and can be used in practice. However, since \(\sigma^2_\delta/\sigma^2\) is usually not known, the REML method should be used first.

Table 10.10 Comparison of Least Squares and REML Estimates for Split-Plot Response Surface Experiment

| Factor | Least Squares (proc rsreg) \(\hat{\beta}\) | \(s_{\hat{\beta}}\) | P-value | REML (proc mixed) \(\hat{\beta}\) | \(s_{\hat{\beta}}\) | P-value |
|---|---|---|---|---|---|---|
| intercept | 2.979 | 0.1000 | <.001 | 3.1312 | 0.2667 | 0.054 |
| \(x_1\) | -0.2500 | 0.0795 | 0.026 | -0.2500 | 0.2656 | 0.399 |
| \(x_2\) | -0.4333 | 0.0795 | 0.003 | -0.4333 | 0.0204 | <.001 |
| \(x_1^2\) | -0.6974 | 0.1223 | 0.002 | -0.6835 | 0.3758 | 0.143 |
| \(x_2^2\) | 0.1526 | 0.1223 | 0.016 | -0.0965 | 0.0432 | 0.089 |
| \(x_1x_2\) | -0.3500 | 0.0973 | 0.268 | -0.3500 | 0.0250 | <.001 |

\(\hat{\sigma}^2_\delta = 0.1402, \hat{\sigma}^2 = 0.0025\)

From a practical point of view, it would be advantageous to be able to use the least squares estimates, since proc rsreg that uses the least squares method, can also automatically compute the canonical analysis, the ridge analysis, or produce predicted values over a grid for use in contour plotting. Vining et al. (2005) proved an equivalence theorem that shows the least squares estimates of all of the regression coefficients in a split-plot response surface design will be the same as the REML estimates if (1) the design is balanced (in that each whole plot contains the same number of subplots), (2) the subplot designs are orthogonal (although not necessarily the same), and (3) the axial runs for the subplots are run in a single whole plot. In addition, to get separate estimates of the variances of whole-plot and subplot experimental units at least two whole plots of center points on all factors should be included. Designs that have these properties will be referred to here as estimation equivalent split-plot response surface designs or EESPRS. No EESPRS is possible when there is only one subplot factor because property (2) cannot be satisfied.

When there are two or more subplot factors, EESPRS designs can be easily obtained by modifying standard response surface designs. For example, consider the two central composite designs run in a split-plot arrangement shown in Figure 10.23. If there is one whole-plot factor, A, and two subplot factors, P and Q, the standard central composite design with three center points shown on the left can be grouped into five whole plots by sorting on the whole-plot factor A as exhibited in the figure. Since the number of runs in each whole-plot are not equal for the design on the left, it is not balanced, and it is not