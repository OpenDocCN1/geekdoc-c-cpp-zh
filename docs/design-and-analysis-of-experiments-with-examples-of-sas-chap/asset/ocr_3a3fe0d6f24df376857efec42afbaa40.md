**REML Iterations**

| Iteration | Objective | Var(batch) | Var(Error) |
|---|---|---|---|
| 0 | 3.7798354425 | 0 | 1.4100446970 |
| 1 | 3.7798354425 | 0 | 1.4100446970 |

Convergence criteria met.

**REML Estimates**

| Variance Component | Estimate |
|---|---|
| Var(batch) | 0 |
| Var(Error) | 1.41004 |

on factors that can be varied in the second step of the process where the interim is added and mixed with the batch. These further experiments were performed and will be shown in the next chapter.

In processes that contain more than two steps, Leitnaker and Cooper (2005) show that multistage sampling experiments, to be described in Section 5.6, are very useful for identifying process steps and factors within those steps that would be good candidates for further study with factorial type experiments.

When using the option method=reml or method=ml, SAS proc varcomp gives the asymptotic variances of the estimates in addition to the maximum likelihood or REML estimates of the variance components. For example, using the data from dyestuff color yields in Table 5.2, the output table shown at the top of the next page was produced by proc varcomp.

The asymptotic variances on the diagonal of the covariance matrix shown in proc varcomp output can be used to get an asymptotic confidence interval on the variance components. For example, an asymptotic 95% confidence interval for \(\sigma^2\) can be constructed using the estimates on the next page as shown below.

\(\hat{\sigma}^2 \pm 1.96 \sqrt{Var(\hat{\sigma}^2)} = 2451.3 \pm 1.96 \sqrt{500,718.9} = (1064.37, 3838.225)\)

A similar interval estimate can be obtained for \(\sigma^2\). The asymptotic confidence intervals will be reasonably close to the exact confidence intervals produced using the formulas in Table 5.3, when the degrees of freedom for the term corresponding to the variance component being estimated is greater than 45.