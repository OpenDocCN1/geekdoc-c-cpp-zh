+   There is a statement on the second line of the t-test report that says “Assuming unequal variances”. This test is also known as the unpooled t-test. If you want the pooled version (where the variances are assumed to be equal), select the Means/Anova/Pooled t command.

Select the Means/Anova/Pooled t command from the report’s drop-down menu.

+   The plot gets embellished with means diamonds, and other text tables. All of these are discussed later in this tutorial in “Analysis of Variance (anova),” p. 50. Here, note that the p-value for the unpooled t-test is listed beside Prob>|t| in the original t test report. Notice that this is the same value as listed in the new Analysis of Variance report in the column labeled Prob>F. In essence, JMP Student Edition has tested the same hypothesis twice, with two different methods, and both methods agree (as they always should!). In fact, the square of the t statistic (listed under t-Test) is equal to the value of the F statistic (listed in the ANOVA table as F Ratio).

![](bbox=[0.26, 0.29, 0.8, 0.68])

From the drop-down menu in the Oneway Analysis title bar, select Means/Anova/t test to remove the pooled t report.

+   This is a two sample t-test, not a matched pairs t-test. If the data from the two groups have a natural pairing (for example, the before-and-after measurements of a patient taking an experimental medication), use the Matched Pairs platform. Details on matched pairs are found in “The Matched Pairs Platform,” p. 71 in the “The Matched Pairs Platform” chapter.

# Pooled t test

Now, examine the plot on the left side in the report in Figure 3.2, of Starch Content (%) vs. Method. Denim washed with Alpha Amalyze appears to have a lower starch content than denim washed with