# **Output 3.21  Association Statistics for Three Different Models**

| ROC Model | Area | Standard Error | 95% Wald Confidence Limits | Somers' D (Gini) | Gamma | Tau-a |
|---|---:|---:|---:|---:|---:|---:|
| Model | 0.8998 | 0.0264 | 0.8481–0.9515 | 0.7996 | 0.8272 | 0.3614 |
| omit culpl | 0.5652 | 0.0469 | 0.4732–0.6571 | 0.1303 | 0.1847 | 0.0589 |
| omit blackd | 0.8713 | 0.0331 | 0.8065–0.9362 | 0.7427 | 0.7934 | 0.3357 |
| omit whitvic | 0.8918 | 0.0269 | 0.8390–0.9445 | 0.7835 | 0.8363 | 0.3541 |

The ROCCONTRAST statement enables us to test for differences in the area under the curve (*c*-statistic) for the different models, as shown in Output 3.22. We first get an overall test of the null hypothesis that the *c*-statistic is the same across all four models (the main model with all three covariates and the three submodels that omit one covariate each). Clearly that hypothesis must be rejected. Then, because I included the ESTIMATE=ALLPAIRS option, we get the difference in the *c*-statistics for each pair of models, along with its standard error, 95 percent confidence interval, and *p*-value for testing the null hypothesis that the true difference is 0. The only significant differences are between models that include CULP and models that exclude it.

# **Output 3.22  Tables Produced by ROCCONTRAST Statement**

| Contrast | DF | Chi-Square | Pr > ChiSq |
|---|---:|---:|---:|
| Reference = Model | 3 | 95.6616 | <.0001 |

| Contrast | Estimate | Standard Error | 95% Wald Confidence Limits | Chi-Square | Pr > ChiSq |
|---|---:|---:|---:|---:|---:|
| Model - omit culpl | 0.3346 | 0.0513 | 0.2341–0.4352 | 42.5659 | <.0001 |
| Model - omit blackd | 0.0285 | 0.0179 | -0.00656–0.0635 | 2.5366 | 0.1112 |
| Model - omit whitvic | 0.00804 | 0.00921 | -0.0100–0.0261 | 0.7625 | 0.3826 |
| omit culpl - omit blackd | -0.3062 | 0.0637 | -0.4310–-0.1813 | 23.1091 | <.0001 |
| omit culpl - omit whitvic | -0.3266 | 0.0510 | -0.4265–-0.2267 | 41.0821 | <.0001 |
| omit blackd - omit whitvic | -0.0204 | 0.0225 | -0.0645–0.0237 | 0.8228 | 0.3644 |