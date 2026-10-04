This indicates that 10,000 × 0.0489 = 489 of the samples taken yielded a corresponding test statistic that provided a $p$-value, which would incorrectly result in rejection of $H_0$. This simulated Type error rate lies close to the preset $\alpha=0.05$.

Here's another example, this time for nonstandard normal data samples with $\alpha = 0.01:

```
R type.tester(mu0=-4,sigma=0.3,n=60,alpha=0.01)
[1] 0.0108
```

Note that, the numerically simulated rate of Type I error reflects the significance level.

These results are not difficult to understand theoretically—if the distribution does indeed have a mean equal to the null value, you'll naturally observe those "extreme" test values in practice at a rate equal to $\alpha$. The catch, is that in practice the distribution is unknown, highlighting once more the fact that a rejection of any $H_0$ can never be interpreted as proof of the truth of $H_A$. It might be that the sample you observed followed the null hypothesis but produced an extreme test value by chance, however small chance might be.

# Bonferroni Correction

The fact that Type I errors naturally occur because of random variation is particularly important and leads us to consider the multiple testing problem. If you're conducting many hypothesis tests, you should be cautious in simply reporting the "number of statistically significant outcomes”—as you increase the number of hypothesis tests, you increase the chance of receiving an erroneous result. In, say, 20 tests conducted under $\alpha=0.05$, on average one will be a so-called false positive; if you conduct 40 or 60 tests, you are inevitably more likely to find more false positives.

When several hypothesis tests are conducted, you can curb the testing problem with respect to committing a Type I error by using the Bonferroni correction. The Bonferroni correction suggests that when performing a total of $N$ independent hypothesis tests, each under a significance level of $\alpha$, you should use $\alpha_B=\alpha/N$ for any interpretation of statistical significance. Be aware, however, that this correction to the level of significance represents the simplest solution to the multiple testing problem and can be criticized for its conservative nature, which is potentially problematic when $N$ is large.

The Bonferroni and other corrective measures were developed in an attempt to making a Type I error in multiple tests. In general, though, it suffices to be aware of the possibility that $H_0$ might be true, even if the $p$-value is considered small.