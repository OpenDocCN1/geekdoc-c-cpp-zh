# Figure 5.4 Interaction Plot for Part by Operator

![](bbox=[0.15, 0.105, 0.85, 0.42])

# Table 5.14 Comparison of Method of Moments and REML Estimates on Gage R&R Study after Eliminating Parts 6 and 10

| Component | Method of Moments Estimator | REML Estimator |
|---|---|---|
| part (\(\sigma_p^2\)) | 0.03191 | 0.02808 |
| oper (\(\sigma_o^2\)) | 0.0008601 | 0.0008089 |
| part*oper (\(\sigma_{po}^2\)) | 0.0020045 | 0.0020082 |
| Error (\(\sigma^2\)) | 0.0004062 | 0.0004063 |

as it is in this case, it might be wise to question the results. Table 5.14 shows the variance component estimates from the data from the gage R&R study after eliminating parts 6 and 10. With these parts eliminated, the method of moments does not produce a negative variance component estimate, and the results obtained from the method of moments and REML are quite similar. In a situation like this, if the parts are still available, it might be wise to have the operators remeasure parts 6 and 10 to see if there were mistakes.

# 5.9.2 Gamma and Half-Normal Plots to Check Constant Variance Assumption

Wilk et al. (1962) proposed gamma probability plots as effective tools for investigating homogeneity of groups of variances. Sample of variances, with \(\nu\) degrees of freedom, follow the gamma distribution with shape parameter \(\nu/2\),