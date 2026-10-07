# 220 Overdispersion Models in SAS

![](bbox=[0.11, 0.08, 0.889, 0.343])

```
Variance = "Generalized Scale Multinomial";
merge beta stderr2;
WaldChiSq = Estimate * Estimate / StdErr / StdErr;
ProbChiSq = 1 - probchi(WaldChiSq, DF);
run;
data betal2;
set betal2;
format ProbChiSq value6.4;
run;
proc print data=betal2 noobs;
run;
ods html close;
```

The results are produced in Output 7.2.

# Output 7.2: Scale Multinomial and Generalized Scale Multinomial Results–Prenatal Exposure to Cadmium and Zinc Data with Cumulative Logits

![](bbox=[0.093, 0.437, 0.906, 0.727])

| n | d | k |
|---|---|---|n| 70 | 2 | 5 |
| Scale | | |
| 4.8323 | | |
| Phi | | |
| 7.9296 | | |
| 2.0419 | | |

| Variance | Variable | ClassVal0 | DF | Estimate | StdErr | WaldChiSq | ProbChiSq |
|---|---|---|---|---|---|---|---|

| Scale Multinomial | Intercept | 1 | 1 | -3.6525 | 0.5335 | 46.8777 | <0.001 |

| Scale Multinomial | Intercept | 2 | 1 | -2.3679 | 0.4850 | 23.8357 | <0.001 |

| Scale Multinomial | zn2 | | 1 | -0.2357 | 0.8832 | 0.0712 | 0.7896 |

| Scale Multinomial | cd2 | | 1 | 3.0886 | 0.6091 | 25.7130 | <0.001 |

Morel, Jorge, and Nagaraj Neel. Overdispersion Models in SAS*. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.