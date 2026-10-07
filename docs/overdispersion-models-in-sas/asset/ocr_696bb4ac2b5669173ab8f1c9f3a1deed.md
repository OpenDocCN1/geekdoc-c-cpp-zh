# 10 Overdispersion Models in SAS

```
ods html;

proc means data=out mean var maxdec=2;
    var t;

run;
ods html close;
```

Recall that one of the consequences of overdispersion in the data is inflated Type Errors. Program 1.1 can be easily extended to a simulation to demonstrate this undesirable effect. To this end, consider a sample of n=20 clusters each size m=5. The elemental units within the clusters are treated as independent, then we will have a total of 120 Bernoulli trials with the same probability of success π. We need to test the null H₀:π=0.6 versus the alternative hypothesis H₁π>0.6. For the binomial distribution, the Z-test at α=0.05 is to reject the null when

$Z = \frac{\pi-0.6}{\sqrt{\pi(1-\pi)}}} > 1.644$. An estimate of the true Type I Error can be obtained by

performing this on a series of overdispersed data sets generated to be 0.160, and then by computing the number of rejections. Program 1.2 provides the necessary statements to perform this simulation.

# Program 1.2: Estimating Type I Error Rate for Data Created in Program 1.1

```
* Estimating actual Type I Error rate for overdispersed data;
data correlated_bernoulli; --- This data was created in Program 1.1;
    set correlated_bernoulli;
    reps = ceil(id / 20); --- Creates 1000 reps of n=20 clusters of size m=5 each;
run;
proc means data=correlated_bernoulli mean noprint;
    class reps;
    var yr;
    output=test mean=Pi_hat;
run;
data test;
set test;
    if _type_ = 1;
    z = (Pi_hat - 0.6) / sqrt(Pi_hat*(1-Pi_hat) / 100);
    p Val = 0;
    if z > 1.644 then p Val = 1;
run;
title "Monte Carlo Estimate of Type I Error Rate";
proc means data=test mean maxdec=3;
    var P_val;
run;
```

$\rho^2=0.3$, the estimated Type I Error runs out 0.160, about three times the nominal level of 0.05. We can now rerun Programs 1.1 and Program 1.2, appropriately concatenated for other values of $\rho^2$. The following table provides a summary for three runs using the same seed above convenience.