### 11.1.2a Naming the OUTPUT Data Set

| Obs | Var Name | Low | lname_ Low | fname_ Low | LowObs | High | lname_ High | fname_ High | High Obs |
|---:|---|---:|---|---|---:|---:|---|---|---:|
| 1 | ht | 62 | Moon | Rachel | 51 | 74 | Lawless | Henry | 38 |
| 2 | ht | 62 | Karson | Shawn | 36 | 74 | Mercy | Ronald | 50 |
| 3 | ht | 62 | Cranston | Rhonda | 18 | 74 | Rhodes | David | 53 |
| 4 | ht | 62 | Carlile | Patsy | 11 | 74 | Panda | Merv | 56 |
| 5 | ht | 63 | Temple | Linda | 72 | 74 | Taber | Lee | 70 |
| 6 | wt | 98 | Karson | Shawn | 36 | 215 | Mann | Steven | 43 |
| 7 | wt | 98 | Carlile | Patsy | 11 | 215 | Marks | Gerald | 44 |
| 8 | wt | 105 | Stubs | Mark | 69 | 215 | Rose | Mary | 63 |
| 9 | wt | 105 | Maxwell | Linda | 49 | 240 | Antler | Peter | 4 |
| 10 | wt | 105 | Leader | Zac | 39 | 240 | King | Doug | 37 |

# Using CLASS and BY Variables

When CLASS or BY variables are added to the PROC step, the resulting data set is expanded to include them.

```
title1 '11.1.2b CLASS Variable Present';
ods output extremeobs=maxclass(keep=sex varname high_obs lname_high fname_high);
ods listing close;
proc univariate data=advrpt.demog;
    class sex;
    id lname fname;
    var ht wt;
run;
```

⑥ Data set options (see Section 2.1) can be included when naming the new data set.

⑦ When one or more classification variables are used, they are added to the new data set for each combination of levels. The BY statement yields a similar result; however, the order of both the observations and the variables will be different.

### 11.1.2b CLASS Variable Present

| Obs | Var Name | sex | High | lname_ High | fname_ High |
|---:|---|---|---:|---|---|
| 1 | ht | F | 68 | East | Jody |
| 2 | ht | F | 68 | Rose | Mary |
| 3 | ht | F | 68 | Wills | Norma |
| 4 | ht | F | 72 | Adamson | Joan |
| 5 | ht | F | 72 | Olsen | June |
| 6 | ht | M | 74 | Lawless | Henry |
| 7 | ht | M | 74 | Mercy | Ronald |

*... portions of this listing are not shown...*

# Using the Object’s Label

The object’s label can be used instead of the object name on the ODS OUTPUT statement. Here the example from 11.1.2a is repeated using the quoted label (extreme observations) ⑧ instead of the object name.

```
ods output 'extreme observations'=extobs;
```