
Using PROC LOGISTIC, I first estimated a conventional logit model. The results are shown in Output 8.15. Except for article and citation counts, all variables are statistically significant at the .05 level. Older, married PhDs with degrees from agricultural departments were less likely to receive postdoctoral training. Those from high prestige institutions or who were undergraduates at selective institutions were more likely to receive postdoctoral training.

### Output 8.15 PROC LOGISTIC Estimates for Conventional Logit Model

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

```sas
PROC GENMOD DATA=postdoc DESC;
    CLASS docid;
    MODEL pdoc = age mar doc ag und arts cits / D=B;
    REPEATED SUBJECT=docid / TYPE=EXCH;
RUN;
```

### Output 8.17 PROC GLIMMIX Results for Postdoctoral Data

| Cov Parm | Subject | Estimate | Standard Error |
|---|---|---:|---:|
| Intercept | DOCID | 0.4036 | 0.3285 |

| Effect | Estimate | Standard Error | DF | t Value | Pr > \|t\| |
|---|---:|---:|---:|---:|---:|
| Intercept | 2.6653 | 1.0305 | 104 | 2.59 | 0.0111 |
| AGE | -0.1101 | 0.02753 | 442 | -4.00 | <.0001 |
| MAR | -0.5870 | 0.2914 | 442 | -2.01 | 0.0446 |
| DOC | 0.002958 | 0.001311 | 442 | 2.26 | 0.0245 |
| AG | -1.0215 | 0.2834 | 442 | -3.60 | 0.0003 |
| UND | 0.1278 | 0.05349 | 442 | 2.39 | 0.0173 |
| ARTS | -0.07744 | 0.08917 | 442 | -0.87 | 0.3857 |
| CITS | -0.00429 | 0.01868 | 442 | -0.23 | 0.8186 |

| Label | DF | -2 Log Like | ChiSq | Pr > ChiSq | Note |
|---|---:|---:|---:|---:|---|
| Parameter list | 1 | 688.65 | 5.25 | 0.0109 | MI |

Next, we apply the fixed effects method using PROC LOGISTIC. The attraction of the fixed effects approach is that we control for *all* characteristics of universities, not just prestige. Failure to control for these characteristics could bias some or all of the coefficients in the model.

We implement the method with the program

```sas
PROC LOGISTIC DATA=postdoc;
    MODEL pdoc(EVENT='1') = age mar ag und arts cits;
    STRATA docid;
RUN;
```

I excluded DOC from the model because it has the same value for all students within each university. If I had put it in, LOGISTIC wouldn’t have reported any results for it.

The results in Output 8.18 show little difference in the coefficients as compared with the GEE and mixed model results. Apparently, other characteristics of universities either have little effect on who gets postdoctoral training or are uncorrelated with the measured variables in the model. Nevertheless, the standard errors are higher and the chi-squares are lower than those we got with GEE or the mixed model. That’s due in part to the fact that 47 universities with 110 students were excluded from the analysis because either everyone or no one at those universities got postdoctoral training (see the “Model Information” table). Of these universities, 20 were necessarily excluded because the university had only one student in the sample. In any case, the decline in chi-squares is enough to move the p-values above the .05 level for two of the variables, MAR and UND. Again, it seems that fixed-effects is not the best method for these data because it produces little reduction in bias but a big increase in standard errors.

### Output 8.18 Fixed-Effects Results for Postdoctoral Data

**Model Information**

| | |
|---|---|
| Data Set | WORK.POSTDOC |
| Response Variable | PDOC |
| Number of Response Levels | 2 |
| Number of Strata | 106 |
| Number of Uninformative Strata | 47 |
| Frequency Uninformative | 110 |
| Model | binary logit |
| Optimization Technique | Newton-Raphson ridge |

**Analysis of Maximum Likelihood Estimates**

| Parameter | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
|---|---:|---:|---:|---:|---:|
| AGE | 1 | -0.1076 | 0.0311 | 11.9972 | 0.0005 |
| MAR | 1 | -0.5314 | 0.3138 | 2.8681 | 0.0903 |
| AG | 1 | -0.9355 | 0.3827 | 5.9757 | 0.0145 |
| UND | 1 | 0.1352 | 0.0725 | 3.4825 | 0.0620 |
| ARTS | 1 | -0.0868 | 0.0976 | 0.7910 | 0.3738 |
| CITS | 1 | -0.0107 | 0.0228 | 0.2197 | 0.6393 |

## 8.8 Matching

In the postdoctoral example, the data were clustered into naturally occurring groups. Matching is another form of clustering in which individuals are grouped together by design. Matching was once commonly used in the social sciences to control for potentially confounding variables. Now, most researchers use some kind of regression procedure, primarily because of the difficulty of matching on several variables. However, with the development of the *propensity score* method, that objection to matching is largely obsolete (Rosenbaum and Rubin 1983, Smith 1997).

Here’s a typical application of the propensity score method. Imagine that your goal is to compare academic achievement of students in public and private schools, controlling for several measures of family background. You have measures on all the relevant variables for a large sample of eighth grade students, 10% of whom are in private schools. The first step in a propensity score analysis is to do a logistic regression in which the dependent variable is the type of school and the independent variables are the family background characteristics. Based on that regression, the propensity score is the predicted probability of being in a private school. Each private school student is then matched to one or more public school students according to their closeness on the propensity score. In most cases, this method produces two groups that have nearly equal means on all the variables in the propensity score regression. One can then do a simple bivariate analysis of achievement versus school type. Alternatively, other variables not in the propensity score regression could be included in some kind of regression analysis. In many situations, this method could have important advantages over conventional regression analysis in reducing both bias and sampling variability (Smith 1997).

The propensity score method is an example of *treatment-control* matching. In this kind of matching, the individuals within each match group necessarily differ on the explanatory variable of central interest. Another sort of matching is *case-control* matching in which individuals within each match group necessarily differ on the *dependent* variable. Case-control studies have long been popular in the biomedical sciences for reasons I explained in Section 3.13. In a case-control study, the aim is to model the determinants of some dichotomous outcome, for instance, a disease condition. People who have the condition are called cases; people who do not have the condition are called controls. In Section 3.13, we saw that it’s legitimate to take all the available cases and a random subsample of the controls, pool the two groups into a single sample, and do a conventional logit analysis for the dichotomous outcome. Although not an essential feature of the method, each case is often matched to one or more controls on variables—such as age—that are known to affect the outcome but are not of direct interest.
