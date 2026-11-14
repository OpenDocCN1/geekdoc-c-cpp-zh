| Control Factor | Feasible Range ($\mu m$) | Low-Cost Tolerance Range ($\mu m$) |
| :--- | :--- | :--- |
| A: Insulator thickness | 20-30 | $\pm 1.0$ |
| B: Linewidth | 12.5-17.5 | $\pm 0.67$ |
| C: Line height | 4-6 | $\pm 0.33$ |

+   (a) Construct a control-factor array using a $2^3$ factorial design.
+   (b) Construct a noise-factor array (in deviations from the nominal settings in the control-factor array) using the table of Wang, Fang and Lin.
+   (c) Evaluate Equation (12.10) for each combination of values in the product array, and calculate the mean and log variance impedance across the noise-factor array for each of the eight points in the control-factor array.
+   (d) Fit a model to the mean and log variance and identify the control factor settings that will make the impedance equal to 85$\Omega$ with minimum variability.
+   (e) Approximate the variance of $Z$, using the formula $\sigma_Z^2 \approx \left(\frac{\partial Z}{\partial A}\right)^2 \sigma_A^2 + \left(\frac{\partial Z}{\partial B}\right)^2 \sigma_B^2 + \left(\frac{\partial Z}{\partial C}\right)^2 \sigma_C^2$ (where $\sigma_A^2$ = tolerance range/6, etc.), and use non-linear programming (proc nlp as described in Chapter 10) to minimize $\sigma_Z^2$ as a function of $A, B$, and $C$ subject to the constraint that $Z = 85\Omega$. Do the results differ substantially from the answer you got in (d)?

+   8. Consider the data for the product array design for the elastomeric connector shown in Figure 12.4.
+   (a) Calculate the mean pull-off force and log variance of the pull-off force across the noise array for each run in the control-factor array.
+   (b) Analyze the data using the location-dispersion modeling method.
+   (c) Do you find the same optimal levels of the control factors as identified in Section 12.4.2?
+   (d) Is any information lost when analyzing this data using location-dispersion modeling?

+   9. Reconsider the data from the injection molding experiment in Table 12.12.
+   (a) Fit the model $y = \beta_0 + \beta_A X_A + \beta_B X_B + \beta_{A \times B} X_A X_B$ in the adjustment factors using the method of least squares.
+   (b) Simultaneously estimate the variance of the residuals at each level of the dispersion factor, C, and compute the weighted least squares estimates of the coefficients in the model in (a) using proc mixed as shown in Section 12.6.1.