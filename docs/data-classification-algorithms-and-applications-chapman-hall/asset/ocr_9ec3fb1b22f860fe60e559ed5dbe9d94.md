![](bbox=[0.18, 0.12, 0.78, 0.34])

# FIGURE 24.4: Non-parametric statistical tests for multiple comparisons.

where z_{α/2} is the 1 − α/2 percentile of the standard normal distribution. An important practical aspect that should be kept in mind is that the Wilcoxon test uses the continuous evaluation measures, so one should not round the values to one or two decimals, as this would decrease the power of the test in case of a high number of ties.

# 24.4.2.2 Multiple Comparisons

The non-parametric statistical tests that perform multiple comparisons we will discuss in this section are depicted in Figure 24.4. The lower test can be used as a stand-alone method, while the four upper-left tests need a post-hoc procedure to finish the comparison.

Friedman’s test [16, 17] and the Iman Davenport’s test [27] are similar. For each instance, the classifiers are ranked according to the evaluation measure (let r_i^j denote the corresponding rank) and next the average rank R_j for each classifier over the different instances is calculated, R_j = Σ_{i=1}^n r_i^j / n. The best method gets rank 1, the second best method gets rank 2, and so on. Under the null hypothesis, all classifiers are equivalent and hence the average ranks of the different classifiers should be similar. Both the Friedman test and Iman Davenport test aim to detect a deviation from this and can detect if there are significant differences between at least two of the methods. The test statistic of the Friedman test is given by

χ² = (12n)/(k(k+1)) ( Σ_{j=1}^k R_j² - k(k+1)²/4 ).

For a sufficient number of instances and classifiers (as a rule of thumb n > 10 and k > 5), χ² approximately follows a chi-square distribution with k − 1 degrees of freedom. If χ² exceeds the critical value χ²_{k−1,α}, where χ²_{k−1,α} is the 1 − α percentile of the chi-square distribution with k − 1 degrees of freedom, the null hypothesis is rejected. For a small number of data sets and classifiers, exact critical values have been computed [48, 55]. The test statistic for the Iman and Davenport’s