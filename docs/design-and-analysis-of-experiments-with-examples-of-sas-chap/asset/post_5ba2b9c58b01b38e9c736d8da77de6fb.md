
can result in an estimated variance component that is too large, too small, or even negative. Graphical techniques, like those described in Section 5.9, can often reveal atypical values and increase the chance of a useful interpretation of the data.

| Source | DF | Sum of Squares | Mean Square |
|---|---|---|---|
| part | 9 | 1.448915 | 0.160991 |
| oper | 2 | 0.029703 | 0.014852 |
| part*oper | 18 | 0.000430 | 0.028885 |
| Error | 30 | 0.022550 | 0.000752 |
| Corrected Total | 59 | 1.985098 | |

| Source | Expected Mean Square |
|---|---|
| part | Var(Error) + 2 Var(part*oper) + 6 Var(part) |
| oper | Var(Error) + 2 Var(part*oper) + 20 Var(oper) |
| part*oper | Var(Error) + 2 Var(part*oper) |
| Error | Var(Error) |
| Corrected Total | |

| Variance Component | Estimate |
|---|---|
| Var(part) | 0.02285 |
| Var(oper) | -0.000617 |
| Var(part*oper) | 0.01307 |
| Var(Error) | 0.0007517 |

In cases where atypical values are not cause of negative variance component estimates, the REML estimators avoid the negative values shown in the output containing the REML estimates on the next page. From these results it can be seen that most 94.3% = 100 x [0.01247/(0.01247 + 0.0007517)] of the measurement error is due to reproducibility. Therefore to reduce measurement error, efforts should be concentrated on better training of operator inspectors rather than investing in more precise gages.

REML Estimates

| Variance Component | Estimate |
|---|---|
| Var(part) | 0.02255 |
| Var(oper) | 0 |
| Var(part*oper) | 0.01247 |
| Var(Error) | 0.0007517 |

## 5.5.2 Confidence Intervals on Variance Components in Two-Factor Designs

When there is an equal number of replicates per subclass, and the normality assumptions hold, the ANOVA mean squares are independently distributed as multiples of chi-square random variables. Therefore confidence intervals on any expected mean square can be obtained similar to line 1 in Table 5.3. However, except for E(msE) = σ², the expected value of all other mean squares are linear combinations of two or more variance components as shown in the SAS output above. Although exact confidence intervals can be obtained on individual variance components in the balanced two-factor design following the formula on line 2 of Table 5.3, they are not applicable to all designs or unbalanced data. Burdick and Graybill (1992) show a method of computing approximate confidence intervals that is more generally applicable.

Whenever a variance component can be expressed in the form \(\delta = c_1 E(ms1) - c_2 E(ms2)\) where \(ms1\) and \(ms2\) are mean squares in the ANOVA table and \(c_1\) and \(c_2\) are positive, the approximate confidence interval shown by Burdick and Graybill is applicable. For example in the ANOVA table shown above for the gage R&R study,

```
E(msPartOperator) = \sigma^2 + 2\sigma_{ab}^2
```

and

```
E(msOperator) = \sigma^2 + 2\sigma_{ab}^2 + 20\sigma_b^2
```

therefore

```
\delta = 0.05 \times E(msOperator) - 0.05 \times E(msPartOperator) = \sigma_b^2
```

An approximate \(1 - \alpha\) confidence interval on \(\delta\) is given by:

```
(\delta - \sqrt{V_L}, \delta + \sqrt{V_U}), \quad (5.11)
```

where \(\delta = c_1 ms1 - c_2 ms2\), \(\nu_1\) is the degrees of freedom for \(ms1\), \(\nu_2\) is the degrees of freedom for \(ms2\).

```
V_L = G_0^2 c_1^2 ms1^2 + G_3^2 c_2^2 ms2^2 + G_{12} c_1 c_2 (ms1)(ms2)
```

```
V_U = H_1^2 c_1^2 ms1^2 + G_3^2 c_2^2 ms2^2 + H_{12} c_1 c_2 (ms1)(ms2)
```

```
G_1 = 1 - \frac{1}{F_{\alpha, \nu_1, \infty}}
```

```
H_2 = \frac{1}{F_{1-\alpha, \nu_2, \infty}} - 1
```

```
\( G_{12} = \frac{(F_{\alpha,\nu_1,\nu_2}-1)^2 - G_1^2 F_{\alpha,\nu_1,\nu_2}^2 - H_1^2}{F_{\alpha,\nu_1,\nu_2}} \\
H_1 = \frac{1}{F_{1-\alpha,\nu_1,\infty}} - 1 \\
G_2 = 1 - \frac{1}{F_{\alpha,\nu_2,\infty}} \\
and \\
H_{12} = \frac{(1-F_{1-\alpha,\nu_1,\nu_2})^2 - H_1^2 F_{1-\alpha,\nu_1,\nu_2}^2 - G_2^2}{F_{1-\alpha,\nu_1,\nu_2}} \)
```

Although these formulas look formidable, they can easily be evaluated in a SAS data step. A SAS macro `%vci`, listed in the appendix of this chapter, will compute confidence intervals using these formulas. The input to the macro is a SAS data set called `meansq` that contains the variables `conf1`=1 - \(\alpha\), `c1`=`c1`, `ms1`=`ms1`, `nu1`=\(\nu_1\), `c2`=`c2`, `ms2`=`ms2`, and `nu2`=\(\nu_2\). To see how to use this macro consider making confidence intervals on the variance component for operator, and the variance component for the part by operator interaction in the gage R&R study data.

To get a confidence interval on the variance component for operator, \(\sigma_b^2\), ms1=0.014852 with 2 degrees of freedom, ms2=0.026885 with 18 degrees of freedom. These are read into a SAS data set as follows:

```
data meansq;
   input conf1 c1 ms1 nu1 c2 ms2 nu2;
   datalines;
   .90 .05 .014852 2 .05 .026885 18
;
run;
```

The %vci statement calls the macro and produces the following results:

| Obs | delta | L | U |
|---|---|---|---|
| 1 | -.00060165 | -.001579783 | .005717457 |

This shows that even though the method of moments estimator for \(\sigma_b^2\) is negative, the upper 90% confidence bound is positive.

The 90% confidence interval for \(\sigma_{ab}^2\) is found to be (0.008936 - 0.021895) using the same approximation formula.

## 5.5.3 Determining Sample Sizes for Two-Factor Sampling Experiments

In a two-factor sampling experiment, there are three sample sizes to be considered. First the number of levels of factor A, a, second the number of levels of factor B, b, and finally the number of replicates within each cell, r. The degrees of freedom for the replicate mean square is ab(r - 1), by replacing t(r - 1) by ab(r - 1) in formula (5.8), it can be used to determine the value of ab(r - 1) that will result in the desired width of the confidence interval for σ². Next using a rule of thumb like that expressed in Section 5.4.4 the levels of factor A and Factor B can be determined.

## 5.5.4 Two-Factor Studies with Unequal Replication

When there are unequal numbers of replicates in each subclass, the method of moments or analysis of variance estimators of the variance components for the two-factor sampling experiment are not unique. Their values will depend on whether the type I or type III sums of squares are used to get the estimates. On the other hand, the maximum likelihood estimators and REML estimators are unique and may be preferred in this situation.

Table 5.6 Calcium in Blood Serum Solutions with Unknown Concentrations Standard Solution

| Laboratory | 1 | 2 | 3 | 4 |
| :--- | :--- | :--- | :--- | :--- |
| A | 87 | 92 | 179 | 177 |
| | 84 | 83 | 173 | |
| | 80 | 76 | 166 | |
| B | 80 | 69 | 138 | 151 |
| | 70 | 46 | 138 | |
| | | | 132 | |
| C | 70 | 67 | 173 | 176 |
| | 60 | 63 | 166 | |
| | 44 | 48 | | |

To illustrate the calculations, consider the data in Table 5.6 taken from a sampling study to estimate the sources of variability in an inter-laboratory assay of calcium in blood serum that was shown by Rao and Rao (1997). The commands to read the data and compute the variance components using proc varcomp are similar to those shown in the last section for balanced data. Using the method of moments-analysis of variance estimators proc varcomp only gives the option to use the type I sums of squares. The results of this analysis are shown on the next page.

Type I Analysis of Variance

| Source | DF | Sum of Squares | Mean Square |
| :--- | :--- | :--- | :--- |
| lab | 2 | 2919.974074 | 1459.987037 |
| sol | 3 | 54869 | 18289.61623 |
| lab*sol | 6 | 1384.326453 | 230.721075 |
| Error | 15 | 20787 | 1385.811111 |
| Corrected Total | 26 | 59960 | |

Type I Analysis of Variance

| Source | Expected Mean Square |
| :--- | :--- |
| lab | Var(Error) +2.525 Var(lab*sol) +0.0806 Var(sol) |
| sol | +8.963 Var(lab) |
| lab*sol | +2.1979 Var(lab*sol) +6.4648 Var(sol) |
| Error | Var(Error) +2.1935 Var(lab*sol) |
| Corrected Total | |

Type I Estimates

| Variance Component | Estimate |
| :--- | :--- |
| Var(lab) | 144.91348 |
| Var(sol) | 1767.6 |
| Var(lab*sol) | -541.41218 |
| Var(Error) | 1385.8 |

There it can be seen that the unequal replication in the cells causes the coefficients in the expected mean squares to be non-integer values. In addition, the mean square for the lab by solution interaction is smaller than the error mean square, so the estimated variance component is negative.

The REML estimates avoid the problem of negative estimates and the results of proc varcomp with the option method=reml is shown on the page. There it can be seen that the majority of the variability in the assay for calcium in blood serum is due to differences among the standard solutions and among the repeat analyses using the same solution in the same lab.

Notice that while the variance component, \(\sigma^2_\alpha\), for lab is positive, its asymptotic variance, 23212.8, is quite large. However, since there are only three labs, an asymptotic confidence interval for \(\sigma^2_\alpha\) would not be accurate. With unequal replication the ANOVA mean squares are no longer distributed as multiples of chi-square random variables, so the confidence intervals using line 2 in Table 5.3 are also not appropriate.

Approximate confidence intervals can still be obtained if unweighted mean squares are substituted for the mean squares in Formula (5.11). The unweighted mean squares for factor A, B and the interaction can be obtained
