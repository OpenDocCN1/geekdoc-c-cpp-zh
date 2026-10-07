
# 492

# AN INTRODUCTION TO R

Dist with Dist the name for the distribution and d, p, q and r indicating the density/mass function, cumulative distribution function, quantile function and random number generation. The choices for Dist include

- beta for the beta distribution,
- binom for the binomial distribution,
- qchisq for the chi-square distribution,
- exp for the exponential distribution,
- f for the F distribution,
- hypergeometric for the hypergeometric distribution,
- nbinom for the negative binomial distribution,
- norm for the normal distribution,
- pois for the Poisson distribution,
- t for the Student's t distribution and
- unif for the uniform distribution.

The random number generator for the uniform distribution was used earlier to create the matrices A and B that were used in the examples. The commands below illustrate the use of functions for some of the other distributions.

```
> qchisq(.95, df = 9)
[1] 16.91898
> qchisq(qchisq(.95, df = 9), df = 9)
[1] 0.95
> set.seed(123)
> rpois(3, lambda = 5)
[1] 4 7
> dbinom(4, size = 4, p = .25)
[1] 0.0390625
> qnorm(.9, mean = ., sd = 1.); qnorm(.9); qnorm(.95); qnorm(.975)
[1] 1.281852
[1] 1.281852
[1] 1.644854
[1] 1.959964
```

Notice that if this choice is not specified for the mean and standard deviation of the normal distribution the dnorm, pnorm, qnorm and rnorm functions will provide all values for the standard normal distribution.

## B.2 R as a graphics engine

Undoubtedly one of the most useful features of the R package is the collection of functions it provides for generating graphics. The plot function is a key component of the available graphic utilities. It has the prototype

```
plot(x, y, ... )
```

with x and y variables for the x and y axes and the ellipse ... indicating further possible arguments that can be used to add enhancements to a figure. When in its simplest commands like

```
set.seed(123)
x <- 1:100/101
y <- x + runif(100, -.25, .25)
plot(x, y)
```

produce a plot such as Figure B.1. Here random numbers have been generated from a uniform distribution on [.25,.25] then added to the value of a line with unit slope that was evaluated at uniformly spaced points over the unit interval. The plot is satisfactory but lacks standard features such as a title.

![](img/b50973a0535e1d41c799ab78355b19f6_509_0.png)

Figure B.1 Uniform random numbers added to a line with unit slope

The ellipsis argument for plot is R standard that indicates there are other arguments that may be supplied defining the classes for the objects x and y. For our purposes x and y can be assumed to be numeric arrays which can case the additional arguments of most interest

- type for the type of plot with 1 and p producing lines and points (with points being the default option),
- lty, 1xd for values that specify the line type and width,
- pch for an integer or specified symbol for plots using points,
- main for a quoted phrase to be used for the plot title and
- xlab, ylab for text, in quotes, to be placed on the horizontal and vertical axes.

There are six line type by the integers from 1 to 6. A solid line corresponding to lty = 1 is the default. It is also possible to create custom lines as described in Merkel (2006). There are twenty-six symbol options with the selection of a specific symbol being achieved by setting pch to one of the integers between 0 and 25. Open circles, for which pch = 1, are the default. Any character can also be set as the symbol; for example pch = "A" produces a plot with points represented by

Once a plot has been drawn, additional points or lines can also be added using the points and lines. A legend can also be added to the plot using the legend function. Figure B.2 was produced by Listing B.1 below. It illustrates a number of R’s graphical capabilities that will be the focus of the remainder of this section.

# 494

# AN INTRODUCTION TO R

# Listing B.1 graphEx.r
```
par0d <- par()
pdf("graphEx.pdf")
set.seed(123)
x <- 1:100/101
y <- x + rnorm(100, sd = .25)
par(mfrow = c(2, 2))
hist(y, main = "Histogram of y data", xlab = "frequency")
boxplot(y, main = "Boxplot of y data", xlab = "")
plot(x, y, main = "Scatter plot", xlab = "x", pch = 4)
lines(x, lty = 6, lwd = 2)
legend(.15, legend=c("data y", "mean"), pch = c(4, -1), lty = c(1, 6), lwd = 2)
qnorm(lm(y, x)), xlab = expression(Q_{tilde}(u)))
lines(x=seq(-3, 3, by = .1))
dev.off()
par(par0d)
```

First, Listing B.1 creates multiple figure using the graphics mfrow = c(2, 2) that states we have a 2 x 2 array of figures and that the rows of the array are to be filled first as new columns. List of the R parameters can be obtained by using par() on the command line. By using par way the mfrow parameter is set globally and will remain that it is explicitly changed. In particular, parmfrow = c(1, 1) has the effect of changing mfrow back to its original value.

In general global parameter changes may be made in creating a figure. A simple way to return to the original settings is to save the current parameters (e.g., par=par0d) and then restore them using the function (e.g., par(par0d)) after a plotting has been completed. That is what was done in Listing B.1.

The data that is used in Figure B.2 is created by generating a response vector y from a regression model with slope and zero intercept. The random error of the data is generated from a normal distribution with mean zero and standard deviation .25. The independent variable (or x) values are uniformly spaced over the unit interval. The left-hand plot in Figure is a histogram of the y values that was created using the function hist. The second plot on the first row is a boxplot for the same data created using the function boxplot.

# 495

# R AS A GRAPHICS ENGINE

Appropriate titles and axis labels have been added to both figures using the main, xlab and ylab arguments. The first one on the second row is a scatter plot of the x and y vectors where the selected symbol (pch = 4) is x rather than the open circle. The lines has been used to overlay a dashed line with the default width to indicate the true mean for the responses. A legend has been placed on the plot using the legend function with its first arguments specifying the location of the upper-hand corner of the legend. The legend function gives the text to be used to provide information about the symbols and lines that appear in the graph. Without, symbols and the responses were not connected by lines. Nonetheless, R expects both a symbol and line type to be specified for each component of the value that is assigned to the legend argument. The problem is easily resolved by providing values (e.g., -1) that do not correspond to valid symbols or line types. Note that the line width must also be given if that to be a feature of the legend.

# Histogram of y data

# Boxplot of y data

![](img/b50973a0535e1d41c799ab78355b19f6_511_0.png)

![](img/b50973a0535e1d41c799ab78355b19f6_511_1.png)

# Scatter plot

# Normal Q–Q Plot

![](img/b50973a0535e1d41c799ab78355b19f6_511_2.png)
![](img/b50973a0535e1d41c799ab78355b19f6_511_3.png)

Figure B.2 A figure array

The final figure is a normal distribution Q-Q plot of the standardized residuals obtained from fitting a linear model to our simulated data using the lm function that will be described more fully in the next section. A line with unit slope is overlaid on the Q-Q plot using the lines function. The labels for both axes (Qy for normal quantiles and Q for the sample quantiles) are created using a LaTeX type feature of R that allows mathematical symbols and nomenclature to be included in axis labels, legends and titles. The R help page describes this feature.
