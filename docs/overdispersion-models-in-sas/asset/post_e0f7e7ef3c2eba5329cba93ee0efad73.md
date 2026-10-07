
# 150 Overdispersion Models in SAS

```
pt = (pi*pr1+pic*pr2);
end;
else do
  pr1_l = PROBBNML(p1,m[j],t[j]-1);
  pr2_l = PROBBNML(p2,m[j],t[j]-1);
  pt = (pi*(pr1 - pr1_l)+pic*(pr2 - pr2_l));
end;
if pt < 1e-10 then pt = 1e-10;
logcb = logcb + log(pt);
************************************************************************************
* End of computation of logcb under new beta estimate;
************************************************************************************
if (logcb > old_old | split > 5) then stop2=1;
split = split+1;
************************************************************************************
* End of stop2 while loop;
************************************************************************************
  if split>6 then else beta = betan;
  criteria = abs(logcb - old_old)/abs(old_old + eps1);
  if (criteria < eps2 | iterate > 20) then stop1=1;
  iterate = iterate + 1;
************************************************************************************
* End of stop1 while loop;
************************************************************************************
```

```
pi = beta[1];
rho = beta[2];
pl = 1-prpl;
rhoc = 1-rho;
p2 = rhoc*pi;
p1 = p2*rho;
if pl >= 1 then pl = 0.99;
plc = 1-pl;
p2c = 1-p2;
c1 = pi/plc;
c2 = pic/pi;
c3 = pi/pl;
c4 = plc/p2c;
```

> *************************************************************************************
* Final computation of Fisher information under RCB distribution;
************************************************************************************

```
FIMCRB = j(2,2,0);
run FISHERCB;
INVERCB = inv(FIMCRB);
se_pi = sqrt(INVERCB[1,1]);
se_rho = sqrt(INVERCB[2,2]);

nest = j(2,5,0);
est[1,1:2] = round(pi, 0.00001)//round(se_pi, 0.00001);
nest[2,1:2] = round(rho, 0.00001)//round(se_rho, 0.00001);
nest[3,1:2] = round(est[1]/est[2], 0.00001);
nest[1,4] = n-2;
nest[2,4] = n-2;
est[5] = 2*-1*PROBT(est[3],est[4]);
if est[5] < 0.0001 then est[5] = 0.00001;
```

More, Jorge, and Nagaraj Neerajal. Overdispersion Models in SAS. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL rights reserved. For additional resources, visit.sas.com/publishing.

# Chapter 5 Goodness-of-fit Tests for Overdispersed Binomial Models 151

```
vvv = 2;
fitStat[1,1] = -2*logrlik;
fitStat[2,1] = fitStat[1,1] + 2*vvv;               --- AIC;
fitStat[3,1] = fitStat[1,1] + 2*vvv*n / (n-vvv-1);   --- AICC;
fitStat[4,1] = fitStat[1,1] + vvv*log(n);             --- BIC
```

********************************************************************************
Compute expected frequency from RCB and check for frequency =5;
and hence determine r;
********************************************************************************

```
k = max(mj) + 1;
pic = 1-pi;
rho = 1-rho;
p2 = rho*pi;
pl = p2 + rho*p1
if pl >= 1 then pl = 0.99;
```

+   * Initialization;
lowerb = j(k,1,-0.00000001);
upper = j(k,1,1.00000001);

P = j(k,1, 0);

+   * Define lower and upper bound for the intervals;
do s = 2 to k;
lowerb[s] = (s-1)/k;
upper[s] = (s-1)/k;
end;

+   * Compute Expected Counts under FRandom-clumped Binomial Distribution;
do s = 1 to k-1;
P[s] = 0;
probmf = 0;
xlm = (0:mj[j]);
mj = mj[j]+1;
pr1 = PROBNML(p1,mj[j],xl);
pr2 = PROBNML(p2,mj[j],xl);
pr1[2:m2] = pr1[2:m2] - pr1[1:m2-1];
pr2[2:m2] = pr2[2:m2] - pr2[1:m2-1];
do it = 0 to mj[j];
i = it+1;
ratio = it/mj;
 if (ratio > lowerb[s]) & (ratio < upper[s]) then
probmf = probmf + pi*pr1[i] + (1-pi)*pr2[i];
end;
P[s] = P[s] + fj[j]*probmf;
probmf = 0;
end;
P[k] = n-sum(P(1:k-1));

exp = P;

********************************************************************************
CATEGORIES WITH EXPECTED FREQUENCIES SMALLER THAN 5 ARE;
COLLAPSED WITH PRIOR CATEGORY;
********************************************************************************

```
do false = 1 to; necessary for GOTO statement;
class = k;
index = 1;
```

Morel, Jorge, and Nagar Neeraj. Overdispersion Models in SAS*. Copyright © 2011, SAS Institute Inc., Cary,
North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

```
s = 1;
aux2 = j(k,1,0);
aux4 = j(i,1,0);
begin:
aux2[index] = exp[s];
aux4[index] = upperb[s];
while (s < k) do
  if (aux2[index] < 5) then
    s = s+1;
    class = class-1;
    aux2[index] = aux2[index] + exp[s];
    aux4[index] = upperb[s];
  end
  else
    index = index +1;
    s = s+1;
    goto begin2;
end;
if (class[index] < 5) then do
class = class-1;
aux2[index-1] = aux2[index] + aux2[index-1];
end;
```

```
Lower = j(class,1,0);
Upper = j(class,1,0);
upper = aux4[class];nlower[2:class] = aux4[class-1];nlower[1] = -0.00001;0.00001;
upper[class] = class;
expected = aux2[1:class];
```

> Goodness of fit test under Random-clumped Binomial distribution;

+   * Compute observed count;
obs = j(r,1,0);

```
ratio = t/m;
do s = 1 to r-1 do
obs[s] = sum(ratio > lower[s]) & (ratio <= upper[s]);
end;
```

```
obs[r] = n - sum(obs[1:r-1]);
lower[1] = 0;
upper[r] = 1.0000;
sum_obs = sum(obs);
exp_sum = sum(expected);
```

+   * Compute the corresponding chi-square under Random-clumped Binomial distribution;

```
chisq = 0;
df = r-3;
chisq = sum(obs-expected)##2/expected;
chisq = round(chisq, 0.00001);
pvalue = round(1-PROCHBI(chisq, df), 0.00001);
GOStat = chisq ||df||pvalue;
```

```
mattrib lower=8.4;
mattrib upper=8.4;
```

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

# Appendix 5.3: GOF Test under Both the Beta-binomial and Random-clumped Binomial Distributions When Covariates Are Present

```
/*
Macro GOF_BB_RCB_Distributions

Arguments:
 mydata -- name of the data set containing the variables "t" and "m"
title -- description of the data being analyzed

User needs to provide the estimated Pi's and Rho's for both the Beta-binomial and Random-clumped Binomial models
 These files are denoted in this macro as "pi_bb" "rho_bb" "pi_rcb" and "rho_rcb"\ and were obtained in the Hiroshima Chromosome Aberration Example using PROC NLMIXED
*/

%macro GOF_BB_RCB_Distributions(mydata,title);
title &title;
proc iml;
 read input data set with variables: &t and &m;
 read all into y;

n = now(y);
t = y[1];
y = y[2];
mj = unique(m);
size_mj = length(mj);
fj = repeat(0,size_mj,1);

do j = 1 to size_mj;
f[j] = sum(m[m==mj[j]]);
end;

 print "Distribution of Cluster Size (m)";
 print mj[label="Cluster Size (m)"] fj[label="Frequency"];
Matrix attributes for matrices to be printed:
matrib Lower format=8.4;
matrib Upper format=8.4;
matrib obs label="Observed Frequency" format=8.0;
matrib expected label="Expected Frequency" format=8.2;
matrib n label="No. of Clusters";
matrib obs sum label="Observed Frequency" format=8.0;
matrib exp sum label="Expected Frequency" format=12.4;
matrib chiq label="Chi-square" format=8.4;
matrib df label="DF" format=8.0;
matrib pvalue label="P-value" format=8.4;
matrib GOStat colname="GOF-Stat" "p-Value"
rowname="Lower Bound Dfs Results" "Upper Bound Dfs Results"
label="GOF Test Statistic";
matrib BoundsDof="Results based on";";

 define subsets "collapse" and "goof";
%mend;
```
