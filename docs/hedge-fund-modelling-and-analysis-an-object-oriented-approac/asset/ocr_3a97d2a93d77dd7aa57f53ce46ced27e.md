Negative Skew

Positive Skew

![](bbox=[0.104, 0.116, 0.879, 0.203])

FIGURE 4.12 Positive and negative skew

given (future) return or price will be larger or smaller than the mean value. That is, if a particular return distribution is skewed, which is generally the case, there is a greater probability that the returns will be higher or lower than that of a normal distribution. Unlike mean and standard deviation, skew has no units but is a pure number, like a z-score.
Mathematically, the sample skew, s is given by:

```
$s = \frac{n}{(n-1)(n-2)} \sum_{i=1}^{n} \left(\frac{x_i - \bar{X}}{s}\right)^3 \quad (4.14)$
```

Box 4.2 shows how to calculate the annualised skew based on a square root rule applied to the standard deviation.

BOX 4.2: SQUARE ROOT RULE – SKEW
To get the annualised figure, the original skew is divided by the square root of the frequency representing the original time period e.g. 12 for monthly and 4 for quarterly. More formally:
$s_{annual} = s_{monthly}/\sqrt{12}$
$s_{annual} = s_{quarterly}/\sqrt{4}$

# 4.10.3 Kurtosis

Kurtosis (m4), the fourth moment of a probability distribution, measures the degree of peakedness or flatness of a distribution compared to the normal distribution. When calculating kurtosis, it is generally assumed that excess kurtosis is being considered. Positive kurtosis (or leptokurtic) indicates a relatively peaked distribution and heavy tails with more extreme values whilst negative kurtosis (platykuric) refers to a flatter distribution with thinner tails and relatively fewer extreme values. A distribution with