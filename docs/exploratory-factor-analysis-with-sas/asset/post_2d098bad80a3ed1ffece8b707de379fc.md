
procedure, and getting into the intricacies of the analysis is beyond the scope of this chapter, for our purposes all you need to understand is that SEM can be used to estimate relationships between variables as though they were measured perfectly. The estimate, therefore, of the correlation under perfect correlation was r = 0.90 (coefficient of determination of 0.81), very close to the calculated corrected correlation effect size. Unfortunately, although alphas in the 0.80 range are common, published research based on data with much lower reliabilities is also not difficult to find. In fact, it is not difficult to find alphas under 0.70, despite the fact that means that a substantial portion of the effect size is lost! This should be considered an undesirable state of affairs in the 21st century, particularly when it is relatively simple to improve measurement in scales by increasing item numbers or through analysis by using modern methods like structural equation modeling.

## Application

## Sample Size and the Precision of Alpha

As we mentioned before, alpha is sample dependent. Thus it might be expected that sample size can affect the precision of our alpha estimate. When a smaller sample is used to estimate alpha, each observation contributes a lot of information to the estimate. An outlier or deviation from expectation in a small sample can have a profound effect on the results and can cause them to vary from the population mean. However, in a larger sample, the outlier or deviation will likely be averaged out by the other observations.

Let's explore this issue of sample size and precision with the Marsh SDQ data that we've been using throughout the book. Let us start by examining the reliability of the parent subscale in the complete data set. The parent subscale is composed of five items:

- (Par1) My parents treat me fairly.
- (Par2) I do not like my parents very much.
- (Par3) I get along well with my parents.
- (Par4) My parents are usually unhappy or disappointed with what I do.
- (Par5) My parents understand me.

Obviously Par2 and Par4 are reversed in direction. If you calculate alpha using these five items as is (see Figure 11.2 on page 192), you will get a negative alpha (which is impossible) as well as some negative item-total correlations (another sign of trouble).

### Figure 11.2 Output with reverse coded items

### Cronbach Coefficient Alpha

| Variables | Alpha |
|---|---|
| Raw | -.338304 |
| Standardized | -.316077 |

### Cronbach Coefficient Alpha with Deleted Variable

| Deleted Variable | Raw Variables Correlation with Total | Raw Variables Alpha | Standardized Variables Correlation with Total | Standardized Variables Alpha |
|---|---|---|---|---|
| Par1 | 0.193681 | -.834220 | 0.180020 | -.861766 |
| Par2 | -.417175 | 0.194553 | -.431354 | 0.245049 |
| Par3 | 0.174914 | -.828698 | 0.163839 | -.821268 |
| Par4 | -.406022 | 0.220399 | -.402013 | 0.208550 |
| Par5 | 0.115035 | -.872559 | 0.181588 | -.865728 |

We must therefore recode our two variables and rerun. Since we likely want to retain a copy of our original data, we will create a new variable with the recoded values in it, Par2_recode and Par4_recode. The syntax for our initial run (summarized above), the recoding, and the revised run are presented below along with comments. Please note we provide two options for recoding—a long way with individual value recoding for each variable and a shorter way using arrays.

```
/*Try to compute alpha for parenting items;
proc corr data=sqdata alpha;
Par;

run;

/*Recode and re-run;
*Recode option 1 - the long way;
data sqdata;
set sqdata;

recode Par2;
if Par2=1 then Par2_recode=6;
if Par2=2 then Par2_recode=5;
if Par2=3 then Par2_recode=4;
if Par2=4 then Par2_recode=3;
if Par2=5 then Par2_recode=2;
if Par2=6 then Par2_recode=1;
*recode Par4;
if Par4=1 then Par4_recode=6;
if Par4=2 then Par4_recode=5;
if Par4=3 then Par4_recode=4;
if Par4=4 then Par4_recode=3;
if Par4=5 then Par4_recode=2;
if Par4=6 then Par4_recode=1;
run;
```

```
*Recode option 2 - arrays;
data sqddata (drop=i);
set sqddata;
array old(*) Par2 Par4; *old variables to recode;
array recode(*) Par2_recode Par4_recode; *new versions;
do i=1 to dim(old);
  if old(i)=1 then recode(i)=6;
  if old(i)=2 then recode(i)=5;
  if old(i)=3 then recode(i)=4;
  if old(i)=4 then recode(i)=3;
  if old(i)=5 then recode(i)=2;
  if old(i)=6 then recode(i)=1;
end;
run;
```

```
**Re-run;
proc corr data=sqddata alpha;
var Par1 Par2_recode Par3 Par4_recode Par5;
run;
```

The updated results from our run with the recoded Par2 and Par4 are displayed in Figure 11.3 on page 194. Since we input the raw data and not standardized versions of our variables, we interpret the raw coefficients presented. We now have a normal (and quite decent) looking alpha of 0.834, with an N = 15661. Further, the item-total correlations all range from 0.569 to 0.733, which is reasonable.

### Figure 11.3 Updated output with recoded items

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

We then computed alphas for the parent scale in each subsample and plotted the distribution of alphas by sample size to get an idea of the range of the estimates. Syntax to do this step for the 1000 subsamples of N=50 is presented below. The syntax for the other two sets of subsamples is identical to this, except that the names of the input (and generally the output data sets if you are following best practice and changing names of important output data sets) differ. In this syntax, we use ODS to output a data set containing the alphas, and then we use ODS graphics and the SGPLOT procedure to plot our histograms.

```
*Estimate alpha in each subsample;
ods output CronbachAlpha=alphaS50;
*noprint option used to suppress printing and outp used to output data set
with alphas;
proc corr data=sqdata_sub50 alpha nosimple nocorr noprob;
by Replicate;
var Par1 Par2_recode Par3 Par4_recode Par5;
run;
ods output close;

**Print histogram of alphas;
ods graphics on /height=3in width=3in;
proc sgplot data = alpha50 nautolegend;
title "Sample Size = 50";
where Variables="Raw";
histogram Alpha / binwidth=.025 FILLATTRS=(COLOR=cx5E5EAF2) ;
xaxis label = 'Alpha' grid values = (.55 to 1 by .1);
run;

ods graphics off;
```

In general, subsampled alphas that are closer to our “population” alpha of 0.83 can be considered more precise. However, those farther away are less precise. As you can see in Figure 11.4 on page 196, alpha became somewhat volatile in the smaller samples. The observed alphas ranged from a low of α = 0.56 to a high of α = 0.94 in the smallest samples with N=50. The range narrowed a little further in the samples of N=100, with a low of α = 0.70 and a high of α = 0.92. Finally, the samples of N=250 had the narrowest alpha range, with a low of α = 0.74 and a high of α = 0.89. Thus, the precision of the alpha improved as sample size increased. This serves to demonstrate that even in a scale with reasonable strong psychometric properties (such as this), small samples tend to have a good deal of volatility.
