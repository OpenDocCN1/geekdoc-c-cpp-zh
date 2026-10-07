# Example Code 3.6Information Based Design – 4-Stage Design

```
proc seqdesign altref=15;
OneSidedErrorSpending: design nstages=4
method(alpha)=errfuncofb
alttype=stop-reject
alpha=0.025
samplesize model=twamplefreq(nullprop=0.15 test=prop);
ods output Boundary=Bound_Count;
```

Figure 3.2 Sample Size and Maximum Information for 4-Stage Design

| | Sample Sizes (N) | | | | |
| | Two-Sample Z Test for Proportion Difference | | | |
| | Fractional N | Null Reference | Information | Ceiling N | | |
| _Stage_ | N(Grp1) | N(Grp2) | Information | N(Grp1) | N(Grp2) | Information |
| 1 | 80.25 | 40.12 | 40.12 | 119.9 | 82 | 41 | 121.5 |
| 2 | 160.49 | 80.25 | 80.25 | 237.6 | 81 | 81 | 240.0 |
| 3 | 240.74 | 120.37 | 120.37 | 358.7 | 121 | 121 | 358.5 |
| 4 | 320.99 | 160.49 | 160.49 | 476.5 | 161 | 161 | 477.0 |

Figure 3.3 Boundary Information for 4-Stage Design

| Boundary Information (Standardized Z Scale) | | |
| Null Reference = 0 | | |
| Information Level | | |
| Reference | Boundary Values | |
| _Stage_ | Proportion | N | Upper | Upper | Alpha |
| 1 | 0.2500 | 118.8935 | 80.2457 | 1.63551 | 4.33263 |
| 2 | 0.5000 | 237.757 | 180.4927 | 2.31295 | 2.96318 |
| 3 | 0.7500 | 356.605 | 240.7391 | 2.83278 | 2.35904 |
| 4 | 1.0000 | 475.534 | 320.685 | 3.21301 | 2.01409 |

Suppose that at interim analysis of 120 subjects (60 subjects per arm) provides an estimated treatment difference of 0.017 (14 responses out of 60 subjects in treatment in control) with a standard error of 0.0781. The information at Stage 1 is 163.9(Figure 3.4 Information at First Interim Analysis for 4-Stage Design). The actual information is 0.34, slightly less than the expected information of 0.37 (120/322). Since the actual information is not very different from the expected information and the efficacy boundary is not crossed, the trial continues without any change.

Figure 3.4 Information at Interim Analysis for 4-Stage Design