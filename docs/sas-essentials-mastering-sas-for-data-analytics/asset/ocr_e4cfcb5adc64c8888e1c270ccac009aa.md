in your data. Note with each extreme value listed in the table, the observation number is also provided. This helps you to be able to go back to locate these extreme observations in your data set.

# TABLE 9.19 Extreme Values Output from PROC UNIVARIATE

| Extreme Observations | | |
|---|---|---||
| Lowest Value Obs | Highest Value Obs |
| 4 | 20 | 13 | 42 |
| 6 | 24 | 13 | 47 |
| 6 | 17 | 14 | 12 |
| 7 | 46 | 14 | 38 |
| 7 | 26 | 15 | 36 |

# 9.2.2 Using PROC UNIVARIATE to Assess the Normality of the Data

When you select certain options in the PROC UNIVARIATE statement, SAS produces information helpful in assessing the normality of your data. This is important information because a number of statistical tests are based on an assumption of normality. For example, consider the following SAS code that can be used to assess normality:

```
PROC UNIVARIATE NORMAL PLOT DATA=EXAMPLE; VAR AGE;
HISTOGRAM AGE/NORMAL;
```

The NORMAL and PLOT options produce the following output:

+   - Tests for normality
- Stem-and-leaf plot (for some SAS versions)
- Box plot
- Normal probability plot.

The HISTOGRAM statement with the NORMAL option in addition produces a

+   - histogram
- superimposed normal distribution curve.

> HANDS-ON EXAMPLE
In this example, you will learn how to request options to assess normality using PROC UNIVARIATE.