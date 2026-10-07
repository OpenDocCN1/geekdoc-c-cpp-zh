# Chapter 5 Goodness-of-fit for Overdispersed Binomial Models 129

at m = 15; randomly choosing the size of a cluster from a set {10, 15, 20} with Prob(b of cluster size 10) = 0.40, Prob(a cluster size 15) = 0.20, Prob(a cluster size 20) = 0.40; and finally, generating the cluster sizes from a Poissoned model where m = Y + 1, Y ~ Poisson(14). For each combination of $\pi$ and $ho$, and for each scheme of selecting the cluster, a total of 2000 data sets were generated; each data set of size n = 400. In Table 5 we report the results associated with the Beta-binomial and Random-clumped Binomial distributions. The estimated Type I error rates are given for $\alpha=0.10$ when the cluster sizes are randomly generated. We also estimated the power for testing 1) $H_0:T ~$ Beta-binomial versus

$H_1:T ~$ Random-clumped Binomial, and $H_2:T ~$ Random-clumped Binomial versus $H_1:T ~$ Beta-binomial. The degrees of freedom for the Pearson's Chi-square statistic was $
u=R-3$, where R was the number of non-overlapping intervals covering the [0, 1] interval.

The values of $ho$ were $ho=0.1

**Table 5.5: Empirical Type I and Power (%) for the GOF Test When $\alpha=0.10$ and Cluster Size $m=Y+1$ where $Y ~$ Poisson(14)**

| Hypotheses Tested | $\pi$ | $ho$ | Type I Error | Power |
|---|---|---|---|--|
| $H_0:T ~$ Beta-binomial | 0.1 | 0.1 | 11.0 | 13.8 |
| Versus | | 0.3 | 10.9 | 99.2 |
| $H_1:T ~$ Random-clumped Binomial | | 0.5 | 11.0 | 100.0 |
| | 0.3 | 0.1 | 9.9 | 10.2 |
| | | 0.3 | 10.2 | 89.0 |
| | | 0.5 | 10.5 | 100.0 |
| | | 0.1 | 8.4 | 9.9 |
| | | 0.3 | 9.4 | 73.6 |
| | | 0.5 | 11.1 | 100.0 |
| | | | | (continued) |

More, Jorge, and Nagaraj Neerajal. Overdispersion Models in SAS. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.