which is closer to the ideal circle (5.71) but still slightly worse than circles found by simpler and faster algebraic fits (Section 5.12).

# 8.10 Numerical tests and conclusions

We have tested all the algorithms described in this chapter in a set of numerical experiments with simulated data. Our goal was to “try them on” under various conditions and compare them to the geometric and algebraic circle fits described in the previous chapters.

**Numerical tests.** First, we generated $N = 10^7$ random samples of $n = 20$ points located (equally spaced) on the entire circle $x^2 + y^2 = 1$ and corrupted by Gaussian noise at level $\sigma = 0.05$. For each circle fit we have empirically determined the mean squared error of the parameter vector, i.e.,

```
MSE = 1/N \sum_{i=1}^{N} [ (\hat{a}_i - a)^2 + (\hat{b}_i - b)^2 + (\hat{R}_i - R)^2 ],
```

where $\hat{a}_i, \hat{b}_i, \hat{R}_i$ denote the estimates of the circle parameters computed from the $i$th sample, and $a = b = 0, R = 1$ are their true values. The resulting MSE's are given in the first column of Table 8.1.

We note that the inversion-based fit and Karimäki fit require a pole (i.e., a point presumably lying on the circle) to be supplied. We did not give them such a luxury as a point on the true circle, but we used a randomly selected data point as a pole (which is a standard strategy; see Section 8.5).

The first column of Table 8.1 shows that the exotic circle fits described in this chapter are generally less accurate than the standard geometric and algebraic fits. The plain RTKD inversion-based fit (the second line) is especially poor; apparently, it heavily depends on the choice of the pole, and a randomly selected data point is just not good enough. The subsequent iterations improve the performance of the inversion-based fit, making it similar to that of the Pratt fit.

The plain Karimäki fit is not very accurate either, but after the subsequent corrective step it performs similarly to the Pratt fit. This fact confirms our theoretical predictions that the iterative RTKD fit and the corrected Karimäki fit would produce nothing but good approximations to the Pratt fit.

The SWFL Riemann fit was implemented with data centering and rescaling, as described in Section 8.4, to enforce its invariance under translations and similarities. These steps were added to the original version published in [175, 173], as without such steps the performance of the Riemann fit was unreliable. Surprisingly, with these additional steps, the Riemann fit becomes very stable, it even slightly outperforms the Pratt fit! But the best fitting schemes are still our “old friends”—Taubin, Hyper, and geometric fits.

Next we simulated more a difficult situation, where the $n = 20$ data points