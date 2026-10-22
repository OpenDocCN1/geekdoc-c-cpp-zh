have little effect on who gets postdoctoral training or are uncorrelated with the measured variables in the model. Nevertheless, the standard errors are higher and the chi-squares are lower than those we got with GEE or the mixed model. That’s due in part to the fact that 47 universities with 110 students were excluded from the analysis because either everyone or no one at those universities got postdoctoral training (see the “Model Information” table). Of these universities, 20 were necessarily excluded because the university had only one student in the sample. In any case, the decline in chi-squares is enough to move the p-values above the .05 level for two of the variables, MAR and UND. Again, it seems that fixed-effects is not the best method for these data because it produces little reduction in bias but a big increase in standard errors.

# Output 8.18 Fixed-Effects Results for Postdoctoral Data

| Model Information |  |
|---|---| 
| Data Set | WORK.POSTDOC |
| Response Variable | PDOC |
| Number of Response Levels | 2 |
| Number of Strata | 106 |
| Number of Uninformative Strata | 47 |
| Frequency Uninformative | 110 |
| Model | binary logit |
| Optimization Technique | Newton-Raphson ridge |

| Analysis of Maximum Likelihood Estimates |  |  |  |  |  |
|---|---|---|---|---|---|
| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
| AGE | 1 | -0.1076 | 0.0311 | 11.9972 | 0.0005 |
| MAR | 1 | -0.5314 | 0.3138 | 2.8681 | 0.0903 |
| AG | 1 | -0.9355 | 0.3827 | 5.9757 | 0.0145 |
| UND | 1 | 0.1352 | 0.0725 | 3.4825 | 0.0620 |
| ARTS | 1 | -0.0868 | 0.0976 | 0.7910 | 0.3738 |
| CITS | 1 | -0.0107 | 0.0228 | 0.2197 | 0.6393 |

# 8.8 Matching

In the postdoctoral example, the data were clustered into naturally occurring groups. Matching is another form of clustering in which individuals are grouped together by design. Matching was once commonly used in the social sciences to control for potentially