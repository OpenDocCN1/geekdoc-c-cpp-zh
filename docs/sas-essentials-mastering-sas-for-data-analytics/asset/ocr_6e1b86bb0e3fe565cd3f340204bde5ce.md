# ANALYZING TWO-WAY TABLES

| TABLE 10.9 Goodness-of-Fit Test Using PROC FREQ |
| COLORTYPE | Frequency | Percent | Test Percent |
|---|---|---|--|
| YELLOWSMOOTH | 315 | 56.65 | 56.25 |
| YELLOWWRINKLE | 108 | 19.42 | 18.75 |
| GREENSMOOTH | 101 | 18.17 | 18.75 |
| GREENWRINKLE | 32 | 5.76 | 6.25 |

| Chi-Square Test for Specified Proportions |
|---|--|
| Chi-Square | 0.4700 |
| DF | 3 |
| Pr > ChiSq | 0.9254 |

# 10.4 ANALYZING TWO-WAY TABLES

To create a cross-tabulation table using PROC FREQ for relating two variables, use the TABLES statement with both variables listed and separated by an asterisk (*), (e.g., A*B). A cross-tabulation table is formed by counting the number of occurrences in a sample across two grouping variables. The number of columns in a table is usually denoted by $c$ and the number of rows by $r$. Thus, a table is said to be an $r \times c$ table, that is, it has $r \times c$ cells. In a dominant-hand (left-right) by hair color (with five hair colors used), the table would be referred to as a $2 \times 5$ table.

The hypotheses associated with a test of independence are as follows:

+   $H_0$: The variables are independent (no association between them).
-$H_a$: The variables are not independent.

Thus, in the "dominant-hand/hair color" example, the null hypothesis is that there is no association between dominant hand and hair color (each hand-domain category has the same distribution of hair color). The alternative hypothesis is that left- and right-handed people have different distributions of hair color—perhaps left-handed people are more likely to be brown-haired.

Another test can be performed on a cross-tabulation table is a test of homogeneity. In this case, the table is built of independent samples from two or more populations, and the null hypothesis is that the populations have the same distribution (they are homogeneous). In this case, the hypotheses are as follows:

+   $H_0$: The populations are homogeneous.
-$H_a$: The populations are not homogeneous.