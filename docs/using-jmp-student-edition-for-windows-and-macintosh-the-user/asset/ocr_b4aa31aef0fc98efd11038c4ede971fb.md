The red bracket along the edge of the box identifies the shortest half, the smallest length that contains 50% of the data. This is useful when determining the shape of underlying distributions.

# Quantile Box Plots

The Quantile Box Plot command shows additional quantiles (sometimes called percentiles) on the axis of the histogram. If a distribution is normal, the quantiles are approximately equidistant from each other. Like the Normal Quantile Plot, the Quantile Box Plot is useful for seeing normality in a graphical way. For example, if the quantile marks are grouped closely at one end, but have greater spacing at the other end (as in this picture), the distribution is skewed toward the end with more spacing.

Note that the quantile box plot is not the same as the outlier box plot from page 31. Quantiles are values that divide a distribution into two groups — where the pth quantile is larger than p% of the values. For example, half the data are below the 50th percentile (median).

![](bbox=[0.77, 0.2, 0.9, 0.35])

# Stem and Leaf Plots

The Stem and Leaf command constructs a plot that is essentially a variation on the histogram. It was developed for tallying data in the days when computer printouts were neither graphical nor easy to produce. They remain useful because they show the actual data at the same time as the shape of the data. Each line of the plot has a stem value that is the leading digit of a range of column values. The leaf values are made from the remaining digits of the values. The data values can be reconstructed by joining the stem and leaf (and multiplying by the scale factor, if one exists).

In the example pictured in Figure 2.11, the third line of the table reveals that there are data points with values 40 and 41. Values are reconstructed by using the legend at the bottom of the plot.

Figure 2.11 Stem and Leaf Plot

![](bbox=[0.38, 0.71, 0.63, 0.87])

Stem and leaf plots have similar interactive capabilities to JMP Student Edition’s graphics plots, in that they highlight corresponding data points in the data table when they are selected in the plot.