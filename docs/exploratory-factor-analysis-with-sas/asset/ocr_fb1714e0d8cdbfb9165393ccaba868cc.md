# Figure 11.3 Updated output with recoded items

| Variables | Alpha |
|---|---|
| Raw | 0.834427 |
| Standardized | 0.838161 |

| Deleted Variable | Raw Variables Correlation with Total | Raw Variables Alpha | Standardized Variables Correlation with Total | Standardized Variables Alpha |
|---|---|---|---|---|
| Par1 | 0.643062 | 0.800653 | 0.644466 | 0.804390 |
| Par2_recode | 0.595988 | 0.811647 | 0.597524 | 0.817244 |
| Par3 | 0.732967 | 0.775705 | 0.733190 | 0.779291 |
| Par4_recode | 0.568660 | 0.820491 | 0.568433 | 0.825066 |
| Par5 | 0.658999 | 0.796445 | 0.661981 | 0.799518 |

Let's think of this as our gold standard "population" statistic and see what small samples can do to the estimation of alpha. Using PROC SURVEYSELECT, we drew 1000 subsamples of N=50, 1000 subsamples of N=100, and 1000 subsamples of N=250 from the data set using simple random sampling with replacement. The syntax to do this is provided below.

```
```
/*Take 1000 subsamples of N=50;
proc surveysselect data=sasdqta method=SRS n=50 out=sasdqta_sub50
seed=5092 reps=1000;
run;
/*Take 1000 subsamples of N=100;
proc surveysselect data=sasdqta method=SRS n=100 out=sasdqta_sub100
seed=821 reps=1000;
run;
/*Take 1000 subsamples of N=250;
proc surveysselect data=sasdqta method=SRS n=250 out=sasdqta_sub250
seed=291 reps=1000;
run;
```
```

We then computed alphas for the parent scale in each subsample and plotted the distribution of alphas by sample size to get an idea of the range of the estimates. Syntax to do this step for the 1000 subsamples of N=50 is presented below. The syntax for the other two sets of subsamples is identical to this, except that the names of the input (and generally the output