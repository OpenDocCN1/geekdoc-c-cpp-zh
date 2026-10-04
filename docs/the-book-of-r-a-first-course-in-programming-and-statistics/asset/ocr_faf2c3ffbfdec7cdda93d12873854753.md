# 13.2.3 Quantiles, Percentiles, and the Five-Number Summary

Let’s return, once more, to thinking about raw numeric observations. An understanding of how observations are distributed is an important statistical concept, and this will form a key feature of discussions in Chapter 15 onward.

You can gain more insight into the distribution of a set of observations by examining quantiles. A quantile is a value computed from a collection of numeric measurements that indicates an observation’s rank when compared to all the other present observations. For example, the median (Section 13.2.1) is itself a quantile—it gives you a value below which half of the measurements lie—it’s the 0.5th quantile. Alternatively, quantiles can be expressed as a percentile—this is identical but on a “percent scale” of 0 to 100. In other words, the pth quantile is equivalent to the 100 × pth percentile. The median, therefore, is the 50th percentile.

There are a number of different algorithms that can be used to compute quantiles and percentiles. They all work by sorting the observations from smallest to largest and using some form of weighted average to find the numeric value that corresponds to p, but results may vary slightly in other statistical software.

Obtaining quantiles and percentiles in R is done with the quantile function. Using the eight observations stored as the vector xdata, the 0.8th quantile (or 80th percentile) is confirmed as 3.6:

```
R> xdata <- c(2,4.4,3,3,2,2.2,2,4)
R> quantile(xdata,prob=0.8)
  80%
 3.6
```

As you can see, quantile takes the data vector of interest as its first argument, followed by a numeric value supplied to prob, giving the quantile of interest. In fact, prob can take a numeric vector of quantile values. This is convenient when multiple quantiles are desired.

```
R> quantile(xdata,prob=c(0,0.25,0.5,0.75,1))
   0%  25%  50%  75% 100%
 2.00 2.00 2.60 3.25 4.40
```

Here, you’ve used quantile to obtain what’s called the five-number summary of xdata, comprised of the 0th percentile (the minimum), the 25th percentile, the 50th percentile, the 75th percentile, and the 100th percentile (the maximum). The 0.25th quantile is referred to as the first or lower quartile, and the 0.75th quantile is referred to as the third or upper quartile. Also note that the 0.5th quantile of xdata is equivalent to the median (2.6, calculated in Section 13.2.1 using median). The median is the second quartile, with the maximum value being the fourth quartile.