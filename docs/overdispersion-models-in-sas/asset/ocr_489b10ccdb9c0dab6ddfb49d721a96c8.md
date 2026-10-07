# Chapter 7 Likelihood Models for Overdispersed Multinomial Responses 217

| 8 0 1 0 0 0 0 |
| 0 0 13 0 0 0 0 |
| 1 0 17 0 0 0 0 |
| 0 0 13 0 0 0 0 |
| 0 0 15 0 0 0 0 |
| 0 0 14 0 0 0 0 |
| 0 0 11 0 0 0 0 |
| 0 0 14 0 0 0 0 |
| UC |
| 0 0 13 0 0 0 0 |
| 5 1 7 0 0 0 0 |
| 0 0 13 0 0 0 0 |
| 1 0 11 0 0 0 0 |
| 0 0 13 0 0 0 0 |
| 0 0 11 0 0 0 0 |
| 0 0 11 0 0 0 0 |
| 1 2 10 0 0 0 0 |
| 0 1 12 0 0 0 0 |

```
data new_birth_defects;
set birth_defects;
litter_id = _n;
y = 1; count = t1; output;
y = 2; count = t2; output;
y = 3; count = t3; output;
keep litter_id zn2 cd2 zn3_zn2 zn2_cd2 count;
```

```
run;
*** Fits Cumulative Logits -- Full Model;
ods output ParameterEstimates=beta;
proc logistic data=new_birth_defects;
model y = zn2 cd2 zn3_cd2 zn2_cd2 / link=clogit
scale=pearson
```

```
aggregate=(litter_id);
output outl1 predprobs=individual;
freq count;
```

```
run;
data outl;
set outl;
y = 1;
keep litter_id IP_1 IP_2;
```

```
run;
ods html;
title1 "Birth Defects Example";
title2 "Cumulative Logits Model -- Full Model";
```

```
proc iml;
use birth_defects;
read all Var(t1, t2, t3) into obs_ts;
use outl;
```

Morel, Jorge, and Nagar Neeraj. Overdispersion Models in SAS.\. © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.