# Using IIf functions to create crosstab analyses

Many seasoned analysts use the IIf function to create custom crosstab analyses in lieu of using a crosstab query. Among the many advantages of creating crosstab analyses without a crosstab query is the ability to categorize and group otherwise unrelated data items.

In the example shown in Figure 13.16, you're returning the number of account managers hired before and after 2014. Categorizations this specific would not be possible with a crosstab query.

# FIGURE 13.16

This query demonstrates how to create a crosstab analysis without using a crosstab query.

![](bbox=[0.17, 0.435, 0.88, 0.7])

The result, shown in Figure 13.17, is every bit as clean and user-friendly as the results would be from a crosstab query.

# FIGURE 13.17

The resulting data set gives you a clean crosstab-style view of your data.

![](bbox=[0.17, 0.865, 0.47, 0.965])

Another advantage of creating crosstab analyses without a crosstab query is the ability to include more than one calculation in your crosstab report. For example, Figure 13.18 illustrates a query where the sum of units and revenue will be returned in crosstab format.