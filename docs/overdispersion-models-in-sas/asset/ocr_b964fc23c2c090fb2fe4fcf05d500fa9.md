| n | f | 34 | 3 | 4 | 3 | 3 | 2 |
|---|---|---|---|---|---|---|---|n| n | m | 56 | 3 | 3 | 4 | 4 | 3 |
| n | f | 82 | 1 | 1 | 1 | 1 | 1 |
| n | m | 52 | 1 | 5 | 5 | 4 | 3 |
| n | f | 65 | 1 | 3 | 2 | 2 | 1 |
| n | m | 53 | 2 | 2 | 3 | 4 | 2 |
| n | f | 40 | 2 | 2 | 1 | 3 | 3 |
| n | m | 58 | 1 | 1 | 1 | 1 | 1 |
| n | f | 63 | 1 | 1 | 1 | 1 | 1 |
| n | m | 41 | 5 | 5 | 4 | 3 | 3 |
| n | m | 72 | 3 | 3 | 3 | 1 | 1 |
| n | f | 60 | 5 | 4 | 4 | 2 | 2 |
| n | m | 61 | 1 | 3 | 3 | 2 | 1 |

```
proc format;
    value abc $y' = 'Active';
                   'n' = 'Placebo';
    value xyz 'f' = 'Female';
                   'm' = 'Male';
run;

ods html;
proc surveylogistic data=Shoulder_tip_pin;
    class trt gender;
    model y = trt gender age time / link=cllogit;
    format trt $abc. xyz $xyz;
    title1*** Results from fitting a GES Cumulative Logit Model ***;
    title2** to the Shoulder Tip Pain Data in Lumley (1996) ****;
run;
ods html;
```

Selected results are shown in logarithm of the odds-ratios 9.6. Note that the Wald Chi-square for testing the significance of results from comparing the active (abdominal section) versus the placebo (no abdominal suction) is 14.52. This statistic is highly significant (P-value=0.0001). The corresponding odds-ratio is 6.7 with an associated 95% percent confidence interval of (2.53,18.09). These results strongly support the observation that subjects in the active group experience less pain after surgery. This corresponds to an approximate six-fold reduction in pain. Observe also that the beta estimate related to the variable time is highly significant (P<0.01). The odds-ratio corresponding to a unit increase in time turned out to be 1.22 with an associated 95% percent confidence interval of (1.05,1.44). By default,

SURVEYLOGISTIC models the probability of the lower end of the pain scale. Therefore, time odds ratio being greater than one indicates a lessening of pain with time. These results support the fact that there is an expected reduction in pain during the three-day post operative.

Morel, Jorge, and Nagaraj Neerchar. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.