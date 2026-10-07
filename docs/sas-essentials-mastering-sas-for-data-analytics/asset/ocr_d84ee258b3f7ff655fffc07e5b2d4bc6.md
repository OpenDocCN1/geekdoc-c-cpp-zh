# PERFORMING A ONE-SAMPLE T-TEST 273

of freedom (19 in this case), which should be included when you report these results. The TTEST output also gives you a 95% confidence interval of the mean under the 95% CL mean heading (3.9826, 4.0034). Both the p-value and the fact that the confidence interval contains the hypothesized value 4 indicate that $H_0:\mu=4$ would not be rejected at the 0.05 level of significance.

# TABLE 11.2 T-test results using PROC TTEST

| N | Mean | Std Dev | Std Err | Minimum | Maximum |
|---|---|---|---|---|-|
| 20 | 3.9930 | 0.0223 | 0.00498 | 3.9500 | 4.0300 |

| Mean | 95% CL | Mean | Std Dev | 95% CL | Std Dev |
|---|---|---|---|---|---||
| 3.9930 | 3.9826 | 4.0034 | 0.0223 | 0.0169 | 0.0325 |

| DF | t Value | Pr > |t| |
|---|---|---||
| 19 | -1.41 | 0.1759 |

+   Although the statistical test did not reject the null hypothesis, the researcher should also consider the minimum and maximum values in the table to determine if, in a clinical setting, each of these lengths would present a detrimental clinical issue.

+   Observe the plots in Figure 11.1. The blue (or solid curve in some SAS versions) would be a normal curve based on the mean (3.993) and standard deviation (0.022) estimated from the data. The red (or dashed in some SAS versions) curve is a kernel density

![](bbox=[0.213, 0.532, 0.783, 0.826])

Figure 11.1 Histogram and normal curve output for single same t-test

(continued)