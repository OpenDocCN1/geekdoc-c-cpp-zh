# Output 8.10 GEE Results for an Exchangeable Odds Ratio Model

|  | Analysis Of GEE Parameter Estimates |  |  |  |  |  |
|---|---|---|---|---|---|---|
|  | Empirical Standard Error Estimates |  |  |  |  |  |
| Parameter |  | Estimate | Standard Error | 95% Confidence Limits |  | Z | Pr > |Z| |
| Intercept |  | 1.7035 | 0.8703 | -0.0022 | 3.4093 | 1.96 | 0.0503 |
| control |  | -0.9728 | 0.2165 | -1.3972 | -0.5484 | -4.49 | <.0001 |
| problems |  | 0.2642 | 0.0495 | 0.1672 | 0.3613 | 5.33 | <.0001 |
| sevent |  | 0.2922 | 0.0868 | 0.1221 | 0.4622 | 3.37 | 0.0008 |
| cohe s |  | -0.1825 | 0.0460 | -0.2727 | -0.0923 | -3.97 | <.0001 |
| time | 1 | 0.4079 | 0.1810 | 0.0532 | 0.7626 | 2.25 | 0.0242 |
| time | 2 | 0.2679 | 0.1703 | -0.0659 | 0.6017 | 1.57 | 0.1157 |
| time | 3 | 0.0000 | 0.0000 | 0.0000 | 0.0000 | . | . |
| Alpha1 |  | 1.2060 | 0.2314 | 0.7524 | 1.6596 | 5.21 | <.0001 |

# 8.5 Mixed Models with PROC GLIMMIX

As we have seen, the principal attraction of GEE is the fact that it produces efficient coefficient estimates that have minimum sampling variability. Mixed modeling has the same attraction, but also offers a number of additional features. In this approach, clustering is treated as a random effect in a mixed model—so named because it includes both fixed and random effects. Although mixed models are quite similar to GEE, they have two potential advantages. First, much more complex models are possible, with multiple levels of clustering, overlapping clusters, and random coefficients. Second, estimation of mixed models can correct for heterogeneity shrinkage discussed in Section 3.12. In other words, mixed models are subject specific rather than population averaged like the models estimated by GEE (McCulloch 1997, Rodriguez and Goldman 1995).

Mixed models differ from GEE models in that dependence between repeated measurements is directly built into the model. In its simplest form, the mixed logit model can be written as follows:

```
log( p_it / (1 - p_it) ) = α_i + β x_it .   (8.2)
```