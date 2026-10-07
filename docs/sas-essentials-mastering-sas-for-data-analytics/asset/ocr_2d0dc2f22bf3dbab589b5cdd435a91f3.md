(continued)

2. Run the program and observe the output in Table 15.3. The first table provides summary information for the mean scores based on the ranks. The KW test reports p < 0.0001, indicating that there is a significant difference in the distribution of the groups. (Note that in this case there are four groups, NPAR1WAY does not produce output for the two-group Wilcoxon Rank Sum tests as in Table 15.1.) Moreover, you can request p-values using an EXACT statement, and the computing time will be extensive in the current case of four groups.

Unlike the PROCANOVA procedure, there are no multiple comparison tests provided with NPAR1WAY. However, in the Going Deep section later in this chapter, a method is provided to perform this follow-up procedure.

If you prefer not to use the method for multiple comparisons in the Going Deep section, and the test for k-samples is significant, an acceptable procedure is to perform pairwise comparisons across the groups and adjust the significance level from 0.05 using the Bonferroni technique of dividing the significance level by the total number of comparisons. For example, in the case with four groups, there are six pairwise comparisons, so you would perform six Wilcoxon–Mann–Whitney comparisons. For each test, you would use the significance level adjusted to (0.05/6=0.0083) for your criterion for rejecting the null hypothesis.

# TABLE 15.3 Output from NPAR1WAY for a Four-Sample Group Comparison

| Wilcoxon Scores (Rank Sums) for Variable WEIGHT Classified by Variable GROUP |
| GROUP | N | Sum of Scores | Expected Under H0 | Std Dev Under H0 | Mean Score |
|---|---|---|---|---||
| 1 | 7 | 28.00 | 101.50 | 18.845498 | 4.000000 |
| 2 | 7 | 77.50 | 101.50 | 18.845498 | 11.071429 |
| 3 | 7 | 171.00 | 101.50 | 18.845498 | 24.428571 |
| 4 | 7 | 129.50 | 101.50 | 18.845498 | 18.500000 |

Average scores were used for ties.

| Kruskal-Wallis Test |
|---||
| Chi-Square | 24.4807 |
| DF | 3 |
| Pr > Chi-Square | <0001 |

SAS displays comparative box plots in the output that provides a visual comparison of the groups (see Figure 15.1). Results of multiple comparison tests for these data will be given in the Hands-on Example in Section 15.5.