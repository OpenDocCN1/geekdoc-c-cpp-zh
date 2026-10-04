The final steps are easy—the test statistic given by (18.12) is just the grand total of all elements of the matrix that is the third layer of skin.array.

```
R X2 <- sum(skin.array[,3])
R X2
[1] 66.16615
```

The corresponding p-value for this test of independence is as follows:

```
R 1-pchisq(X2,df=(kr-1)*(kc-1))
[1] 2.494251e-12
```

Recall the relevant degrees of freedom are defined as $\nu (k_r - 1) \times (k_c - 1)$.

The extremely small p-value provides strong evidence against the null hypothesis. The appropriate conclusion would be to reject $H_0$ and state that there does appear to be a relationship between the type of treatment for the skin affliction and the level of success in curing it.

# R Function: chisq.test

Once more, no section in this chapter would be complete without showcasing the built-functionality R possesses for these fundamental procedures. The default behavior of chisq.test, when supplied a matrix as x, is to perform a chi-squared test with respect to the row and column frequencies—just as performed manually here for the skin affliction example. The following easily confirms your previous calculations:

```
R chisq.test(x=skin)
Pearson's Chi-squared test
data: skin
X-squared = 66.1662, df = 6, p-value = 2.4902e-12
```

| Exercise 18.4 |
| HairColor is a ready-to-use data set in R that you haven't met across. This $4 \times 4 \times 2$ array provides frequencies of hair and eye color of 592 statistics students, split by sex (Snee, 1974). |
| a. Perform and interpret, at a significance level of $\alpha=0.01$, a chi-squared test of independence for hair against eye color for all students, regardless of their sex. |