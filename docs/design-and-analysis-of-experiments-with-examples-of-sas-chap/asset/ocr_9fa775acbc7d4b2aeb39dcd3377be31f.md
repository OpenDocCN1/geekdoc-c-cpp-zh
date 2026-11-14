# 2.6.1 Box-Cox Power Transformations

One way to recognize the need for a variance stabilizing transformation is to examine the plot of residuals versus cell means described in the last section. If the spread in the residuals tends to increase proportionally as a function of the cell means, as illustrated in Figure 2.4, a transformation, Y = f(y) can usually be found that will result in a more sensitive analysis, Box and Cox (1964) proposed a series of power transformations Y = y^λ that normally work well. If the variance tends to increase as the mean increases, choose a value of λ less than one, and if the variance tends to decrease as the mean increases, choose a value of λ greater than one. Table 2.3 summarizes some common Box-Cox Power transformations. A common situation where the σ ∝ μ is when the response is actually a measure of variability, like the sample variance s^2.

Table 2.3 Box-Cox Power Transformations

| Relation Between σ and μ | λ | Transformation |
| :--- | :--- | :--- |
| σ ∝ μ^2 | -1 | Reciprocal |
| σ ∝ μ^1/2 | -1/2 | Square root of Reciprocal |
| σ ∝ μ | 0 | Log |
| σ ∝ μ^1/2 | 1/2 | Square Root |

In a CRD design with replicate experiments in each level of the treatment factor, one way to determine the most appropriate value of λ to use in the Box-Cox transformation is to fit a least squares regression line

log(s_i) = a + b log(ȳ_i.)

to the summary statistics. If the straight line provides a reasonable fit to the data, use λ = 1 - b. For example, for the bread rise experiment the SAS commands below use proc sort and proc means to calculate and store the cell means and standard deviations in the SAS file, means.

```
proc sort data=bread; by time;
proc means data=bread; var height; by time;
output out=means mean=meanheight stddev=s;
data logs; set means;
logsmean=log(mean);
logs=log(s);
```

Logarithms of both the cell means and standard deviations are computed in the data step and stored in the file logs. In the commands shown at the top of the next page proc reg is used to calculate the slope and intercept of the regression line and proc sgplot is used to plot the log standard deviations by log means with the fitted regression line as shown in Figure 2.7.