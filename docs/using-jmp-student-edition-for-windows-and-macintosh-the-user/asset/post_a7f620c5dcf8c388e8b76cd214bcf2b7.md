
The red bracket along the edge of the box identifies the shortest half, the smallest length that contains 50% of the data. This is useful when determining the shape of underlying distributions.

## Quantile Box Plots

The Quantile Box Plot command shows additional quantiles (sometimes called percentiles) on the axis of the histogram. If a distribution is normal, the quantiles are approximately equidistant from each other. Like the Normal Quantile Plot, the Quantile Box Plot is useful for seeing normality in a graphical way. For example, if the quantile marks are grouped closely at one end, but have greater spacing at the other end (as in this picture), the distribution is skewed toward the end with more spacing.

Note that the quantile box plot is not the same as the outlier box plot from page 31. Quantiles are values that divide a distribution into two groups — where the pth quantile is larger than p% of the values. For example, half the data are below the 50th percentile (median).

![](img/a858f3b35ed4923af65c22e8829ee5a8_32_0.png)

## Stem and Leaf Plots

The Stem and Leaf command constructs a plot that is essentially a variation on the histogram. It was developed for tallying data in the days when computer printouts were neither graphical nor easy to produce. They remain useful because they show the actual data at the same time as the shape of the data. Each line of the plot has a stem value that is the leading digit of a range of column values. The leaf values are made from the remaining digits of the values. The data values can be reconstructed by joining the stem and leaf (and multiplying by the scale factor, if one exists).

In the example pictured in Figure 2.11, the third line of the table reveals that there are data points with values 40 and 41. Values are reconstructed by using the legend at the bottom of the plot.

Figure 2.11 Stem and Leaf Plot

![](img/a858f3b35ed4923af65c22e8829ee5a8_32_1.png)

Stem and leaf plots have similar interactive capabilities to JMP Student Edition’s graphics plots, in that they highlight corresponding data points in the data table when they are selected in the plot.

## CDF Plot

The CDF Plot command plots a cumulative distribution function step plot using the observed data (with weights or frequencies if specified). Consult a statistics text for a definition of a density function. A CDF plot (Figure 2.12) estimates the area under the density curve up to each data point.

Figure 2.12 CDF Plot for Size of Load

![](img/a858f3b35ed4923af65c22e8829ee5a8_33_0.png)

## Fit Distribution

The Fit Distribution menu allows you to fit certain distributions (Normal, Lognormal, Weibull) to the data. After fitting, you can select among several options, including a Goodness of Fit test.

![](img/a858f3b35ed4923af65c22e8829ee5a8_33_1.png)

## Categorical Variable Graphs and Reports

The only text report that appears by default in categorical distribution reports is a frequencies table (Figure 2.13).

Figure 2.13 Frequencies Table

![](img/a858f3b35ed4923af65c22e8829ee5a8_34_0.png)

This table lists the levels of a categorical variable, the count (sometimes called the frequency) of each level, and the probability associated with each variable. This probability is simply the ratio of each level's count to the total count.

The standard error of these probabilities (StdErr Prob) and the cumulative probabilities (Cum Prob) for the data are also computed, but are not initially shown in the results table. To see them,

- Right-click on the table to bring up a popup menu (Figure 2.14)
- Select Columns to reveal a popup menu of all possible columns for the table.

Tables that are currently shown have a check mark beside them.

- Select the column to be shown or hidden.

Figure 2.14 Table Popup Menu

![](img/a858f3b35ed4923af65c22e8829ee5a8_34_1.png)

The options listed in the drop-down menu for categorical variables (Figure 2.15) work the same as those for continuous variables (see “Continuous Variable Graphs and Reports,” p. 30.)

Figure 2.15 Drop-down Menu for Categorical Variables

![](img/a858f3b35ed4923af65c22e8829ee5a8_34_2.png)

## Statistical Tests

JMP Student Edition contains numerous statistical tests for single variables, including:

- **Prob>|ChiSq|** is the probability of obtaining a greater absolute Chi Square value by chance alone when the sample standard deviation is not different from the hypothesized value. This is the *p*-value for observed significance of the two-tailed *t*-test.
- **Prob>ChiSq** is the probability of obtaining a Chi Square value greater than the computed sample Chi Square by chance alone when the sample standard deviation is not the hypothesized value. This is the *p*-value for observed significance of a one-tailed *t*-test.
- **Prob<ChiSq** is the probability of obtaining a Chi Square value less than the computed sample Chi Square by chance alone when the sample standard deviation is not the hypothesized value. This is the *p*-value for observed significance of a one-tailed *t*-test.

## Testing Categorical Probabilities

The **Test Probabilities** option displays the dialog shown in Figure 2.16, where hypothesized probabilities are entered. The Likelihood Ratio and Pearson Chi Square tests are calculated for those probabilities.

Figure 2.16 Test Probabilities

![](img/a858f3b35ed4923af65c22e8829ee5a8_36_0.png)

**Test Probabilities** can scale the hypothesized values so that the probabilities sum to one. Therefore, the easiest way to test that all the probabilities are equal is to enter a one in each field. To test a subset of the probabilities, leave the levels that are not involved blank. JMP Student Edition substitutes estimated probabilities for those left blank.

The radio buttons on the dialog allow a choice between rescaling hypothesized values to sum to one or using the entered value without rescaling.

## Confidence Intervals

For continuous variables, confidence intervals for a mean are automatically displayed in the Moments table (Figure 2.17).

## Figure 2.17 The Moments Table for Continuous Variables

![](img/a858f3b35ed4923af65c22e8829ee5a8_37_0.png)

To calculate confidence intervals for a specific value of α,

- Select Confidence Interval from the popup menu next to the variable name in the title bar.

A dialog box appears that lets you specify which confidence interval to display.

![](img/a858f3b35ed4923af65c22e8829ee5a8_37_1.png)

- Select the desired level to see, for example, 0.95.

## Figure 2.18 Confidence Intervals for Continuous Variables

Confidence Intervals
| Parameter | Estimate | Lower CI | Upper CI | 1-Alpha |
|---|---|---|---|---|
| Mean | 25.51663 | 23.58055 | 27.45272 | 0.950 |
| Std Dev | 9.656888 | 8.468259 | 11.23675 |  |

To obtain the equivalent table for categorical variables, select Confidence Interval > 0.95. To obtain a confidence interval alpha that is not listed on the Confidence Interval menu, select Confidence Interval > Other and enter the desired level. An example is shown in Figure 2.19.

## Figure 2.19 Confidence Intervals for Categorical Variables

Confidence Intervals
| Level | Count | Prob | Lower CI | Upper CI | 1-Alpha |
|---|---|---|---|---|---|
| Alpha Analyze | 32 | 0.32653 | 0.241763 | 0.424385 | 0.950 |
| Caustic Soda | 33 | 0.33673 | 0.250901 | 0.434885 |  |
| Pumice Stone | 33 | 0.33673 | 0.250901 | 0.434885 |  |
| Total | 98 |  |  |  |  |
Note: Computed using score confidence intervals.

## Saving Information

To save information computed from continuous response variables, use the Save menu commands. Each command generates a new column in the current data table named by appending the response column name (denoted colname in the following definitions) to the saved statistic's name.

The Save commands can be used repeatedly. This enables the same statistic to be saved multiple times under different circumstances, such as before and after combining histogram bars. If the Save command is used multiple times, the column name for the statistic is named colname1, colname2, and so forth, to create unique column names.

The Save menu contains the following commands:

- **Level Numbers** creates a new column, called Level colname. The level number of each observation corresponds to the histogram bar that contains the observation. The histogram bars are numbered from low to high, beginning with 1.
- **Level Midpoints** creates a new column, called Midpoint colname. The midpoint value for each observation is computed by adding half its level width to its lower level bound.
- **Ranks** creates a new column called Ranked colname that contains a ranking for each of the corresponding column’s values, starting at 1. If there are duplicates in the column, they are assigned consecutive ranks in order of their occurrence in the spreadsheet.
- **Ranks averaged** creates a new column, called RankAvgd colname. If a value is unique, its averaged rank is the same as the rank. If a value occurs k times, its average rank is computed as the sum of its value’s ranks divided by k.
- **Prob Scores** creates a new column, called Prob colname. For N non-missing scores, the probability score of a value is computed as the averaged rank of that value divided by N+1. This column is similar to the empirical cumulative distribution function.
- **Normal Quantiles** creates a new column, called N-Quantile colname. These normal scores are Van Der Waerden approximations to the expected order statistics for the normal distribution.
- **Standardized** creates a new column, called Std colname. This contains the original column’s standardized values (each value in the column has had the column mean subtracted, which is then divided by the column standard deviation).

## Whole-Platform Options

Each statistical platform has a popup menu in the outermost outline level next to the platform name. Options and commands in this menu affect all text reports and graphs on the platform.

![](img/a858f3b35ed4923af65c22e8829ee5a8_38_0.png)

The whole-platform options for the Distribution platform include the following:

- **Uniform Scaling** scales all axes with the same minimum, maximum, and intervals so that the distributions are easily compared. This option applies to reports for all response variables when selected.
- **Stack** lets you orient all the output in the report window as either portrait or landscape.
- **Script** lets you rerun or save the JSL script that produced the platform results. If the script is saved to a file, you can edit it; if it is saved with the current data table, it is available to run the next time you open the table. The JSL generated by **Save Script for All Objects** is the same as **Save Script to Script Window** if there are no By-Groups. When there are By-Groups the script includes JSL Where clauses that identify the By-Group levels.
