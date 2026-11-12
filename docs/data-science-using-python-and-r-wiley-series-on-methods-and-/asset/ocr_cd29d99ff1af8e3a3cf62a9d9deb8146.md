+   - For symmetric data, the mean and the median are approximately equal.

+   - For right-skewed data, the mean is greater than the median.

+   - For left-skewed data, the median is greater than the mean.

+   - **Measures of variability** quantify the amount of variation, spread, or dispersion present in the data. The measures of variability we will learn are the range, the variance, the standard deviation, and, later, the interquartile range (IQR).

+   - The **range** of a variable equals the difference between the maximum and minimum values. The range of income is: range = max(income) - min(income) = 48,000 - 24,000 = 24,000.

+   - A **deviation** is the signed difference between a data value and the mean value. For Applicant 1, the deviation in income equals x - x̄ = 38,000 - 32,540 = 5460. For any conceivable data set, the mean deviation always equals zero, because the sum of the deviations equals zero.

+   - The **population variance** is the mean of the squared deviations, denoted as σ² ("sigma-squared"):

```
\sigma^2 = \frac{\sum(x-\mu)^2}{N}
```

+   - The **population standard deviation** is the square root of the population variance: \sigma = \sqrt{\sigma^2}.

+   - The **sample variance** is approximately the mean of the squared deviations, with n replaced by n - 1 in the denominator in order to make it an unbiased estimator of \sigma^2. (An **unbiased estimator** is a statistic whose expected value equals its target parameter.)

```
s^2 = \frac{\sum(x-\bar{x})^2}{n-1}
```

+   - The **sample standard deviation** is the square root of the sample variance: s = \sqrt{s^2}.

+   - The variance is expressed in **units squared**, an interpretation that may be opaque to nonspecialists. For this reason, the standard deviation, which is expressed in the original units, is preferred when reporting results. For example, the sample variance of income is s^2 = 51,860,444 dollars squared, the meaning of which may be unclear to clients. Better to report the sample standard deviation s = $7201.

+   - The sample standard deviation s is interpreted as the size of the **typical deviation**, that is, the size of the typical difference between data values and