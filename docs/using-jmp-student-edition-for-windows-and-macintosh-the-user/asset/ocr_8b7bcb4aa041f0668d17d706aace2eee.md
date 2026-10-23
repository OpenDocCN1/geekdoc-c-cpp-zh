# Figure 3.17 One Way ANOVA Popup Menu

![](bbox=[0.25, 0.12, 0.78, 0.45])

The Quantiles command displays the Quantiles table, which lists the 0% (minimum), 10%, 25%, 50% (median), 75%, 90%, and 100% (maximum) quantiles for each group. It also activates Box Plots from the Display Options menu.

The Means/Anova/t test command fits means for each group and performs a one-way analysis of variance to test if there are differences among the means. Three tables are produced: a summary table, a one-way analysis of variance table, and a table that lists group frequencies, means, and standard errors computed with the pooled estimate of the error variance. If there are only two groups, a t-test also shows. This option automatically activates the Means Diamonds display option. See “Analysis of Variance (anova),” p. 50 for a detailed description of means diamonds.

The Means and Std Dev command fits means for each group, but uses standard deviations computed within each group rather than the pooled estimate of the standard deviation used to calculate the standard errors of the means. This command also displays Means Dots, Error Bars, and Std Dev Lines display options.

Compare Means has a submenu that provides the following four multiple comparison methods for comparing sets of group means. All activate the Comparison Circles display option.

+   - Each Pair, Student's t displays a table with Student's t statistics for all combinations of group means.
+   - All Pairs, Tukey HSD displays a table that shows the Tukey-Kramer HSD (honestly significant difference) comparisons of group means.
+   - With Best, Hsu's MCB displays a table that shows Hsu's MCB (Multiple Comparison with the Best) comparisons of group means to the best (maximum or minimum) group mean.
+   - With Control, Dunnett's displays a table showing Dunnett's comparisons of group means with a control group.