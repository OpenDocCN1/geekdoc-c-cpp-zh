observations closer to a measure of centrality. In that sense, transforming to a logarithmic scale can help reduce the severity of heavily skewed data (Section 15.2.4). In the context of regression modeling, log transformations can be used to capture trends where apparent curves “flatten off”, with the same kind of instability outside the range of observed data that you saw with the polynomials.

If you need to refresh your memory on logarithms, turn back to Section 2.1.2; it suffices to note that the logarithm is the power to which you must raise a base value in order to obtain an value. For example, in $3^5 = 243$, the logarithm 5 and 3 is the base, expressed as $\log_3 243 = 5$. Because of the ubiquity of the exponential function in common probability distributions, statisticians almost exclusively work with the natural log (logarithm) to the base e. From, assume all mentions of the log transformation refer to the natural log.

To briefly illustrate the typical behavior of the log transformation, take a look at Figure 21-5, achieved with the following:

```
R plot(1:1000,log(1:1000),type="n",xlab="x",ylab="",ylim=c(-8,8))
R lines(1:1000,-log(1:1000),lty=2)
R legend("topleft",legend=c("log(x)",-log(x*)),lty=c(1,2))
```

This plots the log of the integers 1 to 1000 against the raw values, as well as plotting the negative log. You can see in the way the transformed values taper off and flatten out as the raw values increase.

![](bbox=[0.238, 0.521, 0.523, 0.715])

Figure 21-5: The log function applied to integers 1 to 1000

# Fitting the Log Transformation

As noted, use one of the log transformation in regression is is to allow this kind of curvature in situations when a perfectly straight line doesn’t suit the observed relationship. For an illustration, return to the mtcars examples and consider mileage as a function of both horsepower and transmission