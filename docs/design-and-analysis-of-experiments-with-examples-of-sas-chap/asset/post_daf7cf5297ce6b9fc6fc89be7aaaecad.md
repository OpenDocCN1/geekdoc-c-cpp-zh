
Table 10.9, the general quadratic model can be written in the form

y = X\beta + \omega + \epsilon (10.17)

where \(\beta\) is the vector of regression coefficients for the whole-plot effects, \(\omega\) is a vector of random whole-plot errors, and \(\epsilon\) is a vector of random subplot errors. It is assumed that \(\omega + \epsilon\) has zero mean and variance covariance matrix given by \(\Sigma = \sigma^2_\omega I + \sigma^2_\epsilon J\), where \(\sigma^2_\omega\) and \(\sigma^2_\epsilon\) are the variances of the whole-plot and subplot experimental units and

J = \begin{pmatrix} 1_1 1'_1 & 0 & \dots & 0 \\ 0 & 1_2 1'_2 & \dots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \dots & 1_m 1'_m \end{pmatrix}

The length of 1_i is n_i, the number of subplot runs within the ith whole plot. The least squares estimates of \(\beta\) is \((X'X)^{-1}X'y\), while the best linear unbiased estimate of \(\beta\)

\(\hat{\beta} = (X'\Sigma^{-1}X)^{-1}X'\Sigma^{-1}y\) (10.18)

and its variance covariance matrix is given by

\(Var(\hat{\beta}) = (X'\Sigma^{-1}X)^{-1}\) (10.19)

\(\sigma^2_\omega, \sigma^2_\epsilon\) must be known in order to compute the best linear unbiased estimate of \(\beta\). However, estimates of \(\sigma^2_\omega, \sigma^2_\epsilon\), and the large sample best linear unbiased estimates that is found by substituting \(\hat{\sigma}^2_\omega\) and \(\hat{\sigma}^2_\epsilon\) into Equation (10.18) can be obtained using the REML method that was described in Chapter 10.5 and is available in proc mixed. The commands to fit the general quadratic model to the data in Table 10.9 using proc mixed are shown below.

```
data CakeBake;
   input sp x1 x2 y;
   datalines;
   1 -1 -1 2.7
   .
   .
   .
   proc mixed;
      class sp;
      model y=x1 x2 x1*x1 x2*x2 x1*x2 /
      solution;
      random sp;
   run;
```

A comparison of the parameter estimates obtained by the least squares method and REML is shown in Table 10.10. Here it can be seen that the estimated linear main effects are the same of both methods, but the standard errors are much smaller for the subplot effect and larger for the whole-plot effect using the more correct REML method. The other estimates differ and again the tests for the subplot effects are more sensitive using REML and the tests for whole-plot effects are less sensitive. The REML estimated whole-plot and subplot error variances are shown at the bottom on the right side of the table. Letsinger et al. (1996) showed that when \(\sigma^2_\delta/\sigma^2 < 0.25\) the least squares estimates will be reasonably close to the REML estimates and can be used in practice. However, since \(\sigma^2_\delta/\sigma^2\) is usually not known, the REML method should be used first.

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

### Figure 10.23 Comparison of Split-plot CCDs

![](img/878b651cdbe9da3d6d22e64d64b8a54f_442_0.png)

### Standard CCD in SP

| Whole Plot | A | P | Q |
|---|---|---|---|
| 1 | -α | 0 | 0 |
| 2 | - | - | - |
| 2 | - | + | - |
| 2 | - | - | + |
| 2 | - | + | + |
| 3 | 0 | -α | 0 |
| 3 | 0 | α | 0 |
| 3 | 0 | 0 | -α |
| 3 | 0 | 0 | α |
| 3 | 0 | 0 | 0 |
| 3 | 0 | 0 | 0 |
| 3 | 0 | 0 | 0 |
| 4 | + | - | - |
| 4 | + | + | - |
| 4 | + | - | + |
| 4 | + | + | + |
| 5 | α | 0 | 0 |

### EESPRS CCD

| Whole Plot | A | P | Q |
|---|---|---|---|
| 1 | -α | 0 | 0 |
| 1 | -α | 0 | 0 |
| 1 | -α | 0 | 0 |
| 1 | -α | 0 | 0 |
| 2 | - | - | - |
| 2 | - | + | - |
| 2 | - | - | + |
| 2 | - | + | + |
| 3 | - | + | + |
| 3 | - | + | + |
| 3 | 0 | 0 | 0 |
| 3 | 0 | 0 | 0 |
| 3 | 0 | 0 | 0 |
| 3 | 0 | 0 | 0 |
| 4 | 0 | -α | 0 |
| 4 | 0 | α | 0 |
| 4 | 0 | 0 | -α |
| 4 | 0 | 0 | α |
| 5 | 0 | 0 | 0 |
| 5 | 0 | 0 | 0 |
| 5 | 0 | 0 | 0 |
| 5 | 0 | 0 | 0 |
| 6 | + | - | - |
| 6 | + | + | - |
| 6 | + | - | + |
| 6 | + | + | + |
| 7 | α | 0 | 0 |
| 7 | α | 0 | 0 |
| 7 | α | 0 | 0 |
| 7 | α | 0 | 0 |

an EESPRS design. By removing the center point from the whole plot that has the axial points for the subplot factors P and Q, adding replicates to the whole plots that contain the axial points for the whole-plot factor A, and adding replicates in the whole plots that contain center points, the design on the right becomes balanced. Since the columns for the two subplot factors P and Q are orthogonal (i.e., \(\sum p_i q_i = 0\)) within each whole plot, and all the axial points for the subplot factors are in the same whole plot, this is an EESPRS design. Duplicate whole plots (3 & 5) containing all center points make it possible to estimate \(\sigma_w^2\) and \(\sigma^2\) using the REML method in proc mixed.

While the least squares and REML estimates of the regression coefficients are the same when an EESPRS design is used, the standard errors of the coefficients will not be the same, because the covariance matrix of the least squares estimates, \(\sigma^2(\mathbf{X}'\mathbf{X})^{-1}\), is not the same as the covariance of the REML estimates \((\mathbf{X}'\hat{\Sigma}^{-1}\mathbf{X})^{-1}\). Therefore, if an EESPRS design is used, proc mixed should be used to make hypothesis tests about the parameters (in order to determine if the model can be simplified), but proc reg can be used for doing a canonical analysis, ridge analysis or contour plots.

In a balanced EESPRS design, the number of whole plots is m and the number of subplots within each whole plot is n, making the total number of runs N = nm. The number of factors is k = k1 + k2, where k1 is the number of whole-plot factors and k2 is the number of subplot factors. In an estimation equivalence central composite design, the number of runs in each whole plot will be 2 x k2, since one whole plot must contain all the axial runs for the subplot factors. Table 10.11 on the next page shows some EESPRS designs that can be constructed by modifying standard central composite designs. The designation k1(k2) in the first column refers to the number of whole and subplot factors.

The design in the first row of Table 10.11 is the design in the right side of Figure 10.22 that has one whole-plot factor and two subplot factors. In this design, the factorial portion (whole plots 2 and 6) has the four treatment combinations of a full 2^2 factorial in the subplot factors, randomized to the four subplots. In other designs shown in Table 10.11, the subplots in the factorial portion of the design may contain fractional factorial in the subplot factors, or a fractional factorial in the subplot factors augmented by two center points as indicated in the last column in the table.

Using Table 10.11 as a guide, these designs can be created easily in the SAS data step. The example code below Table 10.11 on the next page creates the design in row four of the table which has two whole-plot factors and two subplot factors in a non-random order. In this code each whole plot is created in a separate data step, and all the whole plots are combined in the last data step.
