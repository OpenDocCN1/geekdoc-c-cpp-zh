0 10/46 21.7

1 21/52 40.4

3 25/51 49.0

9 24/49 49.0

# Example Code 8.5 Analysis of SLE Trial

```
proc mcmc data = sum dt outpost = emax_out nmc = 150000 nbi = 10000 seed = 12
monitor = (parms_ed50 predose1 predose3 predose9 pipred0 pipred1 pipre
piped9) = stats(percent = 2.5 5.0 10.0 95 97.5)=(interval summary);
ods output PostIntervals = intervals;
ods output PostSummaries = summaries;
par e0 max ed50;
prior e0 = ~normal(mean=-0.45,var=4);
prior emax = ~normal(mean=0,var=4);
prior ed50 = ~uniform(0,15);
beginindata;
predose1 = exp(e0+(emax*1)/(ed50+1))/(1+e0+(emax*1)/(ed50+0)));
      = exp(e0+(emax*0)/(ed50+0))/(1+e0+(emax*0)/(ed50+0)));
predose3 = exp(e0+(emax*3)/(ed50+3))/(1+e0+(emax*3)/(ed50+3)));
      = exp(e0+(emax*0)/(ed50+0))/(1+e0+(emax*0)/(ed50+0)));
predose9 = exp(e0+(emax*9)/(ed50+9))/(1+e0+(emax*9)/(ed50+0)));
      = exp(e0+(emax*0)/(ed50+0))/(1+e0+(emax*0)/(ed50+0)));

pipred0 = exp(e0+(emax*0)/(ed50+0))/(1+e0+(emax*0)/(ed50+0)));
pipred1 = exp(e0+(emax*1)/(ed50+1))/(1+e0+(emax*1)/(ed50+0)));
pipred3 = exp(e0+(emax*3)/(ed50+3))/(1+e0+(emax*3)/(ed50+3)));
pipred9 = exp(e0+(emax*9)/(ed50+9))/(1+e0+(emax*9)/(ed50+9)));
endindata;

eta = e0 + ((emax*dose)/(ed50+dose));
expeta = exp(eta);
p = expeta/(1+expeta);
model count ~ binomial(total, p);
run;
```

Figure 8.8 Diagnostic Plots for e0