# TABLE 9.17 Tests for Location from PROC UNIVARIATE

| Tests for Location: Mu=0 | |
| Test | Statistic | p Value |
| Student's t | t | 30.48611 Pr > |t| <.0001 |
| Sign | M | 25 Pr >= |M| <.0001 |
| Signed Rank | S | 637.5 Pr >= |S| <.0001 |

**Tests for Location:** The tests for location given in Table 9.17 are used to determine whether the mean (or central tendency) of the data is significantly different from 0 (or another hypothesized value). These tests are discussed thoroughly in upcoming chapters and are only briefly described here.

**Student's t-test** is a single sample t-test of the null hypothesis that the mean of the data is equal to the hypothesized value (in this case 0 by default). When $p < 0.05$, you would typically reject this hypothesis.

**Signed Rank Test** is a nonparametric test often instead of the Student's t-test when the data are not normally distributed and the sample sizes are small.

**Quantiles:** Table 9.18 provides a listing of commonly used quantiles of the data including the median (listed as the 50th quantile). To interpret the values in the quantile table, note that the $k$th quantile is the value below which $k$% of the values in the data fall. ("Definition 5" in the table refers to the specific method used to calculate the quantiles using an empirical distribution with averaging; see Frigge, Hoaglin, and Igglewicz, 1989).

# TABLE 9.18 Quantiles from PROC UNIVARIATE

| Quantiles (Definition 5) | |
| Quantile | Estimate |
| 100% Max | 15 |
| 99% | 15 |
| 95% | 14 |
| 90% | 13 |
| 75% Q3 | 12 |
| 50% Median | 11 |
| 25% Q1 | 9 |
| 10% | 7 |
| 5% | 6 |
| 1% | 4 |
| 0% Min | 4 |

**Extreme Observations:** The Extreme Observations table (Table 9.19) provides a listing of the largest and smallest values in the data set. This is useful for locating outliers