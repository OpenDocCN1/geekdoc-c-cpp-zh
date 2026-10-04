respectively. The first arguments, x, p, and n, respectively, provide the relevant value (or values) of interest to these functions; the second argument in all of these is df, to which you must specify the degrees of freedom v.
The best way to get an impression of the t family is through a visualization. Figure 16-10 plots the standard normal distribution, curve with $\nu=1$, $\nu=6$, and $\nu=20$.

![](bbox=[0.238, 0.193, 0.658, 0.477])

Figure 16-10: Comparing the standard normal distribution with three instances of the t-distribution. Note that the higher the degrees of freedom, the closer the t-distribution approximation becomes to the normal.

The one important note to take away from Figure 16-10, and indeed from this section, is the way in which the t density function changes with respect to the N(0,1) distribution as you increase the $
u$. For small values of $\nu$ close 1, the t-distribution is shorter, in terms of its mode, with more probability occurring in noticeably heavier tails. The t density approaches the standard normal density as $\nu \to \infty$. As a case in point, note that the upper 5 percent tail of the standard normal distribution is delineated by the following value:

```
R qnorm(1-0.05)
[1] 1.644854
```

The same upper of the t-distribution is provided with df values of $\nu=1$, $\nu=6$, and $\nu=20$, respectively.

```
R qt(1-0.05,df=1)
[1] 6.313752
R qt(1-0.05,df=6)
[1] 1.943188
```