```
SE = s / √n
```

Defining an uncertainty interval for mean is further explained in Chapter 25.

# Median

The physical median divides a highway into two, and the statistical median divides data into two halves. One half of the data have values greater than the median. The other half of the data have values smaller than the median. It is a rule of thumb that if data are nonnormal, use median as the central tendency. If data are normally distributed, median is equal to mean in any case. Hence, median is a robust expression of the central tendency, true for all kinds of data. For example, customer satisfaction data—known as CSAT data—are usually obtained in an ordinal scale known as the Likert scale. One should not take the mean value of CSAT data; median is the right choice. (It is a commonly made mistake to take the mean of CSAT data.) In fact, only median is a relevant expression of central tendency for all subjective data. Median is a truer expression of central tendency than mean in engineering data, such as data obtained from measurements of software complexity, productivity, and defect density.

> While the mean is used in the design of normal distribution, the median is used in the design of skewed distributions such as the Weibull distribution. Median value is used to develop the scale parameter that controls width.

# BOX 2.1 HANGING A BEAM

Think of mean as a center of gravity. In Figure 2.1, the center of gravity coincides with the geometric center, which is analogous to the median of the beam, and as a result, the beam achieves equilibrium. In Figure 2.2, the center of gravity shifts because of asymmetrical load distribution; the beam tilts in the direction of center of gravity. The median, however, is still the same old point. The distance between median and center of gravity is like the difference between median and mean. Such a difference makes the beam tilt; in the case of a data array, the difference between median and mean is a signal of data “skew” or asymmetry.