Using PROC LOGISTIC, I first estimated a conventional logit model. The results are shown in Output 8.15. Except for article and citation counts, all variables are statistically significant at the .05 level. Older, married PhDs with degrees from agricultural departments were less likely to receive postdoctoral training. Those from high prestige institutions or who were undergraduates at selective institutions were more likely to receive postdoctoral training.

# **Output 8.15  PROC LOGISTIC Estimates for Conventional Logit Model**

| Parameter | DF | Estimate | Standard Error | Wald 95% Confidence Limits | Wald Chi-Square | Pr > ChiSq |
|---|---:|---:|---:|---:|---:|---:|
| Intercept | 1 | 2.3974 | 0.9092 | 0.6154, 4.1794 | 6.95 | 0.0084 |
| AGE | 1 | -0.0991 | 0.0254 | -0.1490, -0.0493 | 15.19 | <.0001 |
| MAR | 1 | -0.5645 | 0.2684 | -1.0905, -0.0385 | 4.42 | 0.0354 |
| DOC | 1 | 0.0027 | 0.0009 | 0.0009, 0.0044 | 8.40 | 0.0038 |
| AG | 1 | -1.1070 | 0.2030 | -1.5049, -0.7090 | 29.72 | <.0001 |
| UND | 1 | 0.1215 | 0.0600 | 0.0039, 0.2391 | 4.10 | 0.0429 |
| ARTS | 1 | -0.0739 | 0.0809 | -0.2324, 0.0846 | 0.83 | 0.3610 |
| CITS | 1 | -0.0030 | 0.0170 | -0.0363, 0.0303 | 0.03 | 0.8593 |

Because many of the members in the sample got their degrees from the same institutions, it’s reasonable to suspect some dependence among the observations. There are many characteristics of universities besides prestige that are likely to have some impact on the probability of postdoctoral training. The omission of these variables from the model would produce a correlation in postdoctoral training among those men from the same institution. To adjust for this possible correlation, I estimated the model by GEE:

```
PROC GENMOD DATA=postdoc DESC;
    CLASS docid;
    MODEL pdoc = age mar doc ag und arts cits / D=B;
    REPEATED SUBJECT=docid / TYPE=EXCH;
RUN;
```