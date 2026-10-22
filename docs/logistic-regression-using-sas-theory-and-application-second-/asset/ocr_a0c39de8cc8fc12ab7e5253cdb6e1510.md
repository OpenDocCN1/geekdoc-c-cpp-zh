```
```sas
PROC GENMOD DATA=postdoc;
    MODEL arts = age mar doc ag und / DIST=POISSON;
PROC GENMOD DATA=postdoc;
    MODEL cits = age mar doc ag und / D=P;
RUN;
```
```

To fit a Poisson regression, we use the DIST=POISSON option, which can be abbreviated D=P. When a Poisson regression is requested, the loglinear model in equation (9.3) is the default. Results appear in Output 9.3 and Output 9.4.

# Output 9.3 Poisson Regression for Article Counts

| Model Information | |
|---|---|
| Data Set | POSTDOC |
| Distribution | Poisson |
| Link Function | Log |
| Dependent Variable | ARTS |

| Number of Observations Read | 554 |
| Number of Observations Used | 554 |

| Criteria For Assessing Goodness Of Fit | DF | Value | Value/DF |
|---|---:|---:|---:|
| Deviance | 548 | 1072.2986 | 1.9567 |
| Scaled Deviance | 548 | 1072.2986 | 1.9567 |
| Pearson Chi-Square | 548 | 1474.6054 | 2.6909 |
| Scaled Pearson X2 | 548 | 1474.6054 | 2.6909 |
| Log Likelihood |  | -541.0603 |  |
| Full Log Likelihood |  | -813.1613 |  |
| AIC (smaller is better) |  | 1638.3226 |  |
| AICC (smaller is better) |  | 1638.4762 |  |
| BIC (smaller is better) |  | 1664.2256 |  |

| Analysis Of Maximum Likelihood Parameter Estimates |  |  |  |  |  |  |
|---|---:|---:|---:|---|---:|---:|
| Parameter | DF | Estimate | Standard Error | Wald 95% Confidence Limits | Wald Chi-Square | Pr > ChiSq |
| Intercept | 1 | 0.4241 | 0.4645 | -0.4862, 1.3344 | 0.83 | 0.3612 |
| age | 1 | -0.0312 | 0.0131 | -0.0569, -0.0056 | 5.70 | 0.0170 |
| mar | 1 | 0.0087 | 0.1306 | -0.2474, 0.2648 | 0.00 | 0.9470 |
| doc | 1 | -0.0001 | 0.0005 | -0.0010, 0.0008 | 0.07 | 0.7861 |