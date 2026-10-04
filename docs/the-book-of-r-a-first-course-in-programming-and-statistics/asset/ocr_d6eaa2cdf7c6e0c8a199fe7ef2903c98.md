This informal result indicates that it’s reasonable to make the assumption.

Next, consider the assumption of normality of the raw observations. This can be difficult to determine in many real-data examples. At the least, though, it’s worthwhile to inspect histograms and QQ plots for signs of non-normality. You already inspected histograms and QQ plots for all 71 weights in Section 16.2.2, but for an ANOVA, you need to do this with respect to the grouping of the observations (that is, not just “overall” for the whole set of weights regardless of groups).

To achieve this for the chickwts data, you need to first mean-center each weight by its respective sample mean. You can do this by taking the original vector of weights and subtracting from it the chick.means vector, but first you must rearrange and replicate the latter elements to correspond to the elements in the former. This is done by using as.numeric on the factor vector that represents feed type, giving the numeric value of the levels of chickwts$feed for each record in the original data frame. When that numeric vector is passed via the square brackets to chick.means, you get the correct group mean matched to each observation. As an exercise, you can inspect all the ingredients that go into creating the following chick.meancen object to satisfy yourself of what’s going on:

```
R> chick.meancen <- chickwts$weight-chick.means[as.numeric(chickwts$feed)]
```

In the context of the current analysis, these group-wise, mean-centered values are also referred to as residuals, a term you’ll come across frequently when you study regression methods in the next few chapters.

You can now assess normality of the observations as a whole using the residuals. To inspect a normal QQ plot, the relevant functions are qqnorm and qqline, which you first met in Section 16.2.2. The following two lines produce the image on the right of Figure 19-1.

```
R> qqnorm(chick.meancen,main="Normal QQ plot of residuals")
R> qqline(chick.meancen)
```

Based on this plot (the proximity of the plotted points to the perfect straight line), it doesn’t seem unreasonable to assume normality for these data, particularly when compared to QQ plots of generated normal data of the same sample size (an example was given on the left of Figure 16-9 on page 355).

Investigating the validity of any required assumptions is referred to as diagnostic checking. If you wanted to perform a more rigorous diagnostic check for an ANOVA, other visual diagnostics could involve inspecting QQ plots split by group (you’ll do this in an example in Section 19.3) or plotting the sample standard deviation for each group against the corresponding sample means. Indeed, there are also general hypothesis tests for normality (such as the Shapiro-Wilk test or Anderson-Darling test—you’ll see the former used in Section 22.3.2), as well as tests for equality of variances (such as