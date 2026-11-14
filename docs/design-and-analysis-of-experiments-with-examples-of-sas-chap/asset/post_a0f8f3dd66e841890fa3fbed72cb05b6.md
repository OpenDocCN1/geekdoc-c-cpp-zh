
Figure 2.4 Plot Residuals versus Cell Means for Bread Rise Experiment

![](img/878b651cdbe9da3d6d22e64d64b8a54f_43_0.png)

Figure 2.5 Normal Plot of Residuals for Bread Rise Experiment

![](img/878b651cdbe9da3d6d22e64d64b8a54f_43_1.png)

In a normal probability plot, if the points fall along a straight line, the normal distribution would be justified. The more data, and more points on the plot, the closer the points must lie to a straight line to justify the normality assumption. In Figure 2.5, the points lie reasonably close to a straight line, and the normality assumption would appear justified. The equal variance assumption is more critical than the normality assumption, but they sometimes go hand in hand. When the equal variance assumption is violated, the normality assumption is often violated as well, and the corrective measures used for modifying the analysis when there is heterogeneity of variance will often correct both problems.

## 2.6 Analysis Strategies When Assumptions Are Violated

One common cause of heterogeneity of variances between levels of the treatment factor is a non-linear relationship between the response and stimulus or treatment. For example, in the upper half of Figure 2.6, it can be seen that the response increases non-linearly in response to the treatment. The density functions, drawn on their sides at three treatment levels, represent how non-linearity often affects the distribution of the response. As the mean or center of the distribution increases, the variance or spread in the distribution also increases, and the distributions have long tails on the right. One way of correcting this situation is to transform the response data prior to analysis.

Figure 2.6 Representation of Effect of Non-linearities on Distribution of Response

![](img/878b651cdbe9da3d6d22e64d64b8a54f_44_0.png)

The bottom half of Figure 2.6 shows the potential result of a variance stabilizing transformation. On the transformed scale, the variance appears constant at different factor levels and the distribution appears more normal.

### 2.6.1 Box-Cox Power Transformations

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

```
proc reg data=logs;
model logs=logmean;
run;
proc sgplot data=logs;
reg y=logs x=logmean/curvelabel="Slope=1.29487";
xaxis label="log mean";
yaxis label="log standard deviation";
run;
```

Figure 2.7 Plot of log(s_i) versus log(y_bar_j) for Bread Rise Experiment

![](img/878b651cdbe9da3d6d22e64d64b8a54f_46_0.png)

In this plot it can be seen that log(s_i) increases as log(y_bar_j) increases, and that the linear fit provides a good representation of that relationship. Therefore, the appropriate lambda to use for transforming the dough heights is lambda = 1 - 1.294869. The SAS data step commands shown earlier to read in the data from the bread rise experiment can be modified to incorporate the transformation as follows:

```
data bread2;
input time h1-h4;
height=h1*(1-1.294869); output;
height=h2*(1-1.294869); output;
height=h3*(1-1.294869); output;
height=h4*(1-1.294869); output;
drop h1-h4;
run;
datalines;
```

After incorporating this transformation, the plot of residuals versus cell means is shown in Figure 2.8. It can be seen in this figure that the spread or variability of the residuals is nearly the same for each value of the predicted value or log cell mean.

Figure 2.8 Plot of Residuals versus Cell means after \( y^\lambda \) Transformation for Bread Rise Experiment

![](img/878b651cdbe9da3d6d22e64d64b8a54f_47_0.png)

This transformation also makes the F-test more sensitive. The ANOVA table for the transformed response is shown below, where it can be seen that the P-value has decreased from 0.042 (before transformation) to 0.0227 (after transformation).

The GLM Procedure

Dependent Variable: height

| Source | DF | Sum of Squares | Mean Square | F Value | Pr > F |
|---|---|---|---|---|---|
| Model | 2 | 0.01305604 | 0.00652802 | 5.94 | 0.0227 |
| Error | 9 | 0.00989833 | 0.00109981 | | |
| Corrected Total | 11 | 0.02295437 | | | |

Even when transformations are used to justify the assumptions of the analysis and make the F-test more sensitive, the results are normally reported on the original scale. For example, it would be confusing to talk about the (dough height)^-0.294869 in a report.

### 2.6.2 Distribution-Based Transformations

The distribution assumption for the effects for the CRD described in Section 2.3, was $Y_{ij} \sim N(\mu + \tau_i, \sigma^2_\epsilon)$. However, if it is known that the data follow some distribution other than the normal distribution, such as the Binomial, Poisson or Lognormal, then it would also be known that the standard deviation would not be constant. For example, if the response, $Y$, was a binomial count of the number of successes in $n$ trials, then due to the central limit theorem, $Y$ would be approximately normal, but $\mu_Y = np$ and $\sigma_Y = \sqrt{np(1-p)}$, where $p$ is the probability of success. In situations like this where the distribution of the response is known to follow some specific form, then an appropriate transformation can be found to stabilize the variance. Table 2.4 shows the transformation for common situations often encountered.

Table 2.4 Response Distribution-Based Transformations

| Response Distribution | Variance in Terms of Mean $\mu$ | Transformation $f(y)$ |
|---|---|---|
| Binomial | $\frac{\mu(1-\mu)}{n}$ | $\sin^{-1}\sqrt{y/n}$ (radians) |
| Poisson | $\mu$ | $\sqrt{y}$ or $\sqrt{y + \frac{1}{2}}$ |
| Lognormal | $c\mu^2$ | $\log(y)$ |

### 2.6.3 Alternatives to Least Squares Analysis

When the variance of the experimental error is not constant for all levels of the treatment factor, but it is not related to the cell means, a transformation will not be an appropriate way of equalizing or stabilizing the variances. A more general solution to the problem is to use weighted least squares. Using weighted least squares, $\hat{\beta}$, is the solution to the normal equations $\mathbf{X'WX}\hat{\beta} = \mathbf{X'Wy}$, where $\mathbf{W}$ is a diagonal matrix whose diagonal elements are the reciprocals of the standard deviation within each treatment level. As an illustration of this method, consider the SAS commands, at the top of the next page, for analyzing the data from the bread rise experiment.

As in the previous examples, the data is read in the same way. The sort and means procedures calculate the cell standard deviations and the next data step merges these with the original data and computes the weights, $\mathbf{w}$, that are the reciprocals of the standard deviations. The weight statement, in the proc glm call, solves the weighted least squares normal equations. The results appear below the commands.
