(continued)

+   - There is a lot of output, so you have to be careful about what you are reading. Note that there are actually four tables. The first table gives you the sample mean, standard deviation, standard error of the mean, and the minimum and maximum for each value of BRAND (A and B). The last line has similar information for the mean difference.

+   - The second table gives the mean and standard deviations along with 95%% confidence intervals for the means and standard deviations in each group along with 95% confidence intervals for the difference in the group means using a pooled estimate of the variance (if you believe the variances are equal) and based on the Satterwaite method that does not make an assumption of equals.

+   - The third table gives the results of the two t-tests. The t-test based on a pooled estimate of the variance has a p-value of 0.0005 for the Satterwaite version, p=0.0008. Note that the Satterwaite version generally reports fractional DF. In this case, that the value is 9.4. Also note that the decision regarding which t-test to use is not crucial because both rejecting the null hypothesis. This agreement will often be because the situation.

+   - The fourth table gives the results of the F-test for deciding whether the variances can be considered equal. The p-value for this test is 0.0388, so at the 0.05 level we would conclude that the variances are not equal, and it appears that the variance for BRAND B is larger than that for BRAND A. Thus, the classical approach would lead us to use the Satterwaite t-test.

Observe the graphical information shown in Figure 11.2. This figure is similar to Figure 11.1, but it shows histograms, normal curves, kernel density estimators, and boxplots for HEIGHT separately for BRAND A and BRAND B. In both cases,

![](bbox=[0.166, 0.563, 0.833, 0.913])