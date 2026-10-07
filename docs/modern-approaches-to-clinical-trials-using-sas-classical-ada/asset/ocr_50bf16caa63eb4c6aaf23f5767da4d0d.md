# Appendix C

Example Code 7.6 Code to Produce Plot for Example 1

```
********************************************************************************
Create a plot showing the results
********************************************************************************
/* data set containing where to predict dose-response curves */
data biompredict;
do i=1 to 100;
    dosepred=(i-1)/99;
    output;
end;
drop i;
run;
data biompredict;
    merge biompredict;
run;

/* model fit */
%let deltadiff=0.4;

/* fit emax and predict at specified grid of dose values */
proc nmlixed data=biompredict;
    ods output FitStatistics;
    parms emax=0.3 ed50=1 sigma=1;
    bounds 0.001 * ed50 * 1.5;
    mn=0+ emax*dose/(dose + ed50);
    model resp normal(mn, sigma=2);
    predict emax*dosepred/(dosepred + ed50) out=preout;
    estimate 'TD' &deltadiff* ed50/(emax &deltadiff);
run;

/* create adjusted raw means for plot */
proc sql;
    create table adj_means as
    select distinct(dose), mean(resp) as mean_resp
    from biom
    group by dose;
run;
data adj_means;
    set adj_means;
    if dose=0 then mean0=mean_resp;
    retain mean0;
    if dose ne 0 then diff=mean_resp-mean0;
run;
data preout;
    set preout adj_means;
    recline=0.4;
run;

/* plot dose-response curve confidence intervals and adjusted raw means */
proc sgplot data=preout;
    xaxis grid label="Dose";
    yaxis grid label="Response (difference to placebo)";
    band x=dosepred lower=upper upper= /transparency=0.5
```