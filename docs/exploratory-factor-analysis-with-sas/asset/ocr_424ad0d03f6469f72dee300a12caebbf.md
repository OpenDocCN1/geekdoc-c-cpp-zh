```
run;
proc sort data=boot_itemss; by Variable replicate; run;
proc univariate data=boot_itemss.;
by Variable;
var RawCorr;
output out=ci_itemss pctlpts=2.5, 97.5 mean=RawCorr_mean
std=RawCorr_std pctlpre=RawCorr_ci ;
run;
%NEND;
%subNBoot(50,3); *Run analysis with subsample of N=50;
%subNBoot(100,8321); *Run analysis with subsample of N=100;
%subNBoot(250,26); *Run analysis with subsample of N=250;
```

The estimates and corresponding confidence intervals for each sample are presented in Table 11.2 on page 200 and Table 11.3 on page 201. Ideally, bootstrap analyses of small samples would include the population parameter in the 95% confidence interval, and they would provide information about the precision of the estimate (and thus the potential replicability of the statistic). In the tables below, we can see this pattern is generally true. The 95% CI for the alphas in each subsample contains the “population” alpha. Furthermore, as the sample size increased, the CI became more narrow and precise. This same general pattern is seen in the 95% CI for the item-total correlations. There were only a few instances (highlighted) where the bootstrapped CI did not contain the “population” parameter.

Let’s focus on this idea of CI range and precision for a moment. As we mentioned above, the CI became narrower and more precise as the sample size increased. We can see that the CIs are narrower, but how do we know they are more precise? In the smallest sample of N=50, the range of the CI tended to be rather large, and the sample estimates varied by .12, on average, from the “population” estimates. Some estimates varied substantially more (e.g., GDS06, GDS10). As the subsamples got larger, the estimates came closer to our “population” estimates and the corresponding CIs became narrower.

# Table 11.2 Alphas and 95% CI for three subsamples

| Subsample | Alpha | 95% CI |
|---|---|---|
| N=50 | 0.84 | (0.74, 0.89) |
| N=100 | 0.88 | (0.82, 0.91) |
| N=250 | 0.90 | (0.87, 0.92) |