# SIMPLE LINEAR REGRESSION 293

```
PROC REG;
MODEL TASK=CREATE;
TITLE "Example simple linear regression using PROC REG";
RUN;
QUIT;
```

2. Examine the code for PROC REG. The MODEL statement indicates that you want to predict the TASK score (the old test) from the CREATE score (the new test). Run the program and observe the output, some of which is given in Table 12.5.

| TABLE 12.5 Output from PROG REG for a Simple Linear Regression |
|---|---|---|---||
| Root MSE | 1.60348 | R-Square | 0.3075 |
| Dependent Mean | 5.05000 | Adj R-Sq | 0.2498 |
| Coeff Var | 31.75213 | | |

| Parameter Estimates |
| Variable DF Parameter Estimate Standard Error t Value Pr > |t| |
|---|---|---|---|---|---||
| Intercept | 1 | 2.16452 | 1.32141 | 1.64 | 0.1273 |
| CREATE | 1 | 0.06253 | 0.02709 | 2.31 | 0.0396 |

Information of particular interest in these two tables the following:

+   - **R-Square**: This value is indicated in the first table. It is a measure of the strength of the association between the dependent and independent variables. (It is the square of the Pearson correlation coefficient.) The closer this value is to 1, the stronger the association. In this case, R-Square = 0.31 indicates that 31% of the variability in TASK is explained by the regression with CREATE.
- **Slope**: In the Parameter Estimates, the statistical test on the "CREATE" row is for a test of H₀β=0, and p=0.0396 provides evidence to reject the null hypothesis and conclude that the slope is not zero. (The statistical test on the intercept is generally of little importance).
- **Estimates**: The column labeled “Parameter Estimate” gives the least squares estimates of the slope and intercept (A and B) of the regression equation

```
TASK = A + B * CREATE;
```

which in this case, is

```
TASK = 2.16452 + 0.06235 * CREATE;
```

Thus, from this equation you can gain some information from the CREATE score for predicting the TASK score.

(continued)