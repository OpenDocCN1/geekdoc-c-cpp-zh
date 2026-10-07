# COMPARING TWO DEPENDENT (PAIRED) SAMPLES 353

![](bbox=[0.147, 0.096, 0.853, 0.43])

# 15.3 COMPARING TWO DEPENDENT (PAIRED) SAMPLES

Non nonparametric tests for paired data are available in the PROC UNIVARIATE procedure: the sign test and the signed-rank test. These tests are nonparametric counterparts to the paired t-test. The sign test is simple. It counts the number of positive and negative differences and calculates a p-value based on this information. The (Wilcoxon) signed-rank test bases its decision on the magnitude of the ranked differences. The hypotheses for these tests are as follows:

$H_0$: The probability of a positive difference is the same as that of a negative difference.
H_a$: The probability of a positive difference is different from that of a negative difference.

The following Hands-on Example illustrates how to perform these tests in SAS.

> HANDS-ON EXAMPLE
This example illustrates how to compare paired observations using nonparametric techniques.
1. In the Editor window, open the program AUNIPAIRED.SAS.

DATA WEIGHT;
INPUT WBEFORE WAFTER;

(continued)