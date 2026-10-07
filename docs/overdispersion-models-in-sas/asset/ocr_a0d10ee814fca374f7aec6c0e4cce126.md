# Chapter 5 Goodness-of-fit Tests for Overdispersed Binomial Models 153

```
mattrib obs label='Observed Frequency' format=8.0;
mattrib expected label='Expected Frequency' format=8.4;
```

```
mattrib n label='No of Clusters' format=8.0;
mattrib obs_sum label='Observed Frequencies' format=8.0;
mattrib exp_sum label='Expected Frequencies' format=12.4;
```

```
mattrib chisq label='Chi-square' format=8.4;
mattrib df='DF' format=8.0;
mattrib pvalue label='P-value' format=8.4;
```

```
mattrib est colname=('Estimate' 'St-Error' 't-Value' 'DF' 'p-Value'
mattrib fit rowname='-2 Log Likelihood, AIC (smaller is better)'
AICC (smaller is better) (smaller is better)'
mattrib GOF create='Fit Statistics' format=20.2;
mattrib GOFstat colname=('GOF-Stat' 'DP' 'p-Value'
GOF='GOF Test Statistic;'
```

```
Label = {
  'Parameter Pi', 'Parameter Rho';
}
print fitStat;
print est[rowname];
print 'Goodness-of-fit Test under Random-clumped Binomial Distribution';
print 'Total Counts';
  print n Obs_sum exp_sum;
  print 'Null Hypothesis: Data are distributed according to a Random-clumped
Binomial Distribution';
print GOFStat;
```

```
********************************************************************
end;
  End of group loop do;
********************************************************************
```

* Output Results (Observed - Expected) into data set Resid_RCB needed later
for QO-Plots;

```
Distribution = jnow(obs,1,'Random-clumped');
Resid = obs - expected;
create Resid_RCB var=(Distribution Resid);
```

```
append;
quit;
title;
title2;
end GOF_RCB;
End of Macro;
```

```
* Usage;
*%GOF_RCB(inds=group2,t=t,m=m, title2=Group Haseman and Soares (1976));
```

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary,
North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.