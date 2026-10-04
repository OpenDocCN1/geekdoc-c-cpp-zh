```
R> xvals.sub <- xvals[xvals>=mu.minus.1isig & xvals<=mu.plus.1isig]
R> fx.sub <- fx[xvals>=mu.minus.1isig & xvals<=mu.plus.1isig]
```

You can sandwich these two corners at the bottom of the shaded polygon using the matrix structure that the polygon function expects.

```
R> polygon(rbind(c(mu.minus.1isig,0), cbind(xvals.sub,fx.sub),c(mu.plus.1isig,0))
border=NA,col="gray")
```

Finally, arrows text indicates the areas discussed in the test.

```
R> arrows(c(-4.2,-2.7,-2.9),c(0.5,0.5,1.2),c(-3.7,-3.15,-3.4),c(0.2,0.2,1.1))
R> text(c(-4.2,-2.7,-2.9),c(0.5,0.5,1.2))=0.05,
labels=c("0.159", "0.159", "0.682")
```

# The quantile Function

Let's turn to quantile. To find the quantile value that will give you a lower-tail probability of 0.159, use the following:

```
R> qnorm(0.159,mean=mu,sd=sigma)
```

+   [1] -3.619175

Given the earlier results and what you already know about previous q-functions, it should be clear why the result is a value of approximately -3.62. You find the upper quartile (the value above which you'd found a probability of 0.25) with this:

```
R> qnorm(1-0.25,mean=mu,sd=sigma)
```

+   [1] -3.285102

Remember that the q-function will operate on the (left) lower-tail probability, to find a quantile based on an upper-tail probability, you must first subtract it from the total probability of 1.

In some methods and models used in frequentist statistics, it's common to assume that your observed data are normal. Using your knowledge of the theoretical quantiles of the normal distribution, found in the results of: calculate a range of sample quantile values for your observed data and plot these against the same quantiles for a correspondingly standardized normal distribution. This visual tool is referred to as a normal quantile-quantile or QQ plot and is useful when viewed alongside a histogram. If the plotted points don't lie on a straight line, the quantiles from your data do not match the appearance of those from a normal curve, and the assumption that your data are normal may not be valid.