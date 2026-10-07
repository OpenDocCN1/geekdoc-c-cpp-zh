
# Chapter 5 Goodness-of-fit Tests for Overdispersed Binomial Models 145

```sas
chisq = sum(obs-expected)**2/expected);
chisq = round(chisq, 0.0001);
pvalue = round(1- PROBCHI (chisq, df), 0.0001);
GOF_fit = chisq|pvalue:

mattrib lower format=8.4;
mattrib upper format=8.4;
mattrib obs label=Observed Frequency format=8.0;
mattrib expected label=Expected Frequency format=8.4;

mattrib n label=No, of Clusters format=8.0;
mattrib obs_sum label=Observed Frequencies format=8.0;
mattrib exp_sum label=Expected Frequencies format=12.4;

mattrib chisq label='Chi-square' format=8.4;
mattrib df label='DF' format=8.0;
mattrib pvalue label='P-value' format=8.4;

mattrib est colname=('Estimate' 'St-Error' 't-Value' 'DF' 'p-Value'
label=Maximum Likelihood Estimates;
mattrib fit rowspan=('1-2 Log Likelihood', '(smaller is better)', 'AIC (smaller is better)', 'BIC (smaller is better)', 'BIC (smaller is better)')
label=Fit Statistics format=20.2;
mattrib GOFstat label=('GOF-Stat' 'DF' 'p-Value'
label='GOF Test Statistic; }
```

```sas
Label = { 'Parameter Pi ', 'Parameter Rho ' };
print fitStat;
print est[rowname=label];
print "Goodness-of-fit Test under Beta-binomial Distribution";
print lower obs expected;
print "Total Counts";
print n obs_sum exp_sum;
print "Null Hypothesis: Data are distributed according to a Beta-binomial Distribution";
print GOFStat;

******************************************************
end;                                     End of group loop;
******************************************************
```

Output Residuals (Observed - Expected) into data Resid_BB needed later for QQ-Plots:

Distribution = j(nrow(obs),1,'Beta-binomial ' ');
Resid = obs - expected;
create Resid_BB var= { Distribution Resid };
append;

```sas
quit;
title;
title2;
#end GOF_fBB;

End of Macro GOF_fBB;

Usage:
%GOF BB (inds=group2,t=t,m, title2=Group III Haseman and Soares (1976)
```

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

# 146 Overdispersion Models in SAS

# Appendix 5.2: Module _GOF_RCB_

*************************************************\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
Author: Santosh C Sutradhar
Associate Director
Fisher Inc.
235 East 42nd St
New York, NY 10017
Phone: (212) 733-0496
Email: Santosh.Sutradhar@pfizer.com
Last Modified: Sep 16, 2009

Purpose: To write a SAS MACRO in order to compute MLE and perform GOF-test under Random-clumped Binomial distribution. This GOF() SAS Macro computes the MLE iteratively using the Fisher-Scoring method based on Direct Likelihood

Required: To call other module in file fishermf.sas

+   List of MACRO variables:
inds = input SAS data (MUST contains three variables t, m, group name may be different)
t = cluster count
m = cluster size
group = group variable

Usage: _GOF_RCB(inds=HS,t=t,m,title2=HS data set)
Comment: Clustering sizes (m) were assumed
Initial number of classes to form GOF = MAX(m's) + 1

> *************************************************\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

```sas
;macro GOF_RCB(inds= t, m, title2 = "Data: ");

title="Goodness-of-fit test under Random-clumped Binomial distribution"
title2="&title2";
```

> *************************************************\*\*
*
* Starting IML procedure;
*************************************************\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

```sas
proc iml;
file print;

* Print input information;
```

> *************************************************\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
* Module: FISHERRCB: This module can be called to
Compute Fisher information under RCB
*************************************************\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

```sas
start FISHERRCB;
doj j = 1 to size_j;
mpl = mj[j]*p1;
mmp2 = mj[j]*p2;
derrcb = j(mj[j])+1, 1, 0;
derrcb2 = j(mj[j])+1, 1, 0;
```

Morel, Jorge and Nagaraj Neerchel. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For all SAS resources, visit support.sas.com/publishing.

# Chapter 5 Goodness-of-fit Tests for Overdispersed Binomial Models 147

| AH | = j(2,0) |
|---|---|
| xl | = (0:mj[j]) |
| m2 | = mj[j]+1 |
| pr1 | = PROBNML(p1,mj[j]) |
| pr2 | = PROBNML(p2,mj[j]) |
| pr1[2:m2] = pr1[1:m2-1] |
| pr2[2:m2] = pr2[1:m2-1] |

```sas
do i = 1 to mj[j]+1
  u = i-1
  pi = pi*pr1[i] + pic*pr2[i];
  if pi < 1e-10 then pi = 1e-10;
  b1 = u-mj;
  b2 = u-mj;
  a1 = c1*b1+p1;
  a2 = c2*b2-p2;
```

```sas
derrcb1 = (pr1[i]) / p1 + pr2[i]*a2/p2;
derrcb2 = (pr1[i]) / b1-c3 + pr2[i]*b4;
```

> * Compute Fisher information for each mj;
HAH[1,1] = AH[1,1] + derrcb1[i]/pt;
HAH[1,2] = AH[1,2] + derrcb1[i]/pt;
H[2,2] = AH[2,2] + derrcb2[i]/pt;

end i = 1 to loop;
FIMCBC = FIMCBC + f[j]*AH;
AH[2,1] = AH[2,1];
end j = 1 to size_mj;
finish FIMCBC;
End Module;

> * Read the input set with variables: t, m, and group;
uses &inds;
read all into y
close &inds;

```sas
n = nrow(y);
t = y[1];
y = y[2];
m = unique(y);
size_mj = nrow(m);
fj = repeat(0,size_mj,1);
j = 1 to size_mj;
fj[j] = sum(m);

> * Distribution of mj;
print 'Distribution of Cluster Size (m*)';
print mj[label='Cluster Size (m*)'] fj[label='Frequency'];

> * ML of parameters using ungrouped likelihood.
* Sum of the likelihood (-2) for Random-clustered Binomial;

> * Moment estimate of pi and rho used as initial estimates;
pi = sum(t[*])/sum(m[*]);

if (pi = 0 | pi = 1) then pi = (sum(t[*]) + 1)/(sum(m[*]) + 2);

num = n*(t[*]-m[*]);
```

Morel, Jorge and Nagaraj. Overdispersed Models in SAS.. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional resources, visit support.sas.com/publishing.

```sas
denum = ((n-1)*pi*(1-pi));
mm = (m-j)(n,1);
if ((n/denum - sum(mm))/sum(mm)) > 0 then
  rho = sqrt(n/denum - sum(mm))/sum(mm)); else rho = 0.01;
rho2 = rho*rho;
stopl = 0;
beta = j(2,1);
beta[1] = pi;
beta[2] = 10*(-6);
eps1 = 10*(-8);
eps2 = 1;
iterate = 0;
while (stopl) /* Continue until precision is achieved*/
pi = beta[1];
rho = beta[2];
pic = 1-pi;
rhoc = 1-rho;
pip1 = pi*pic;
pic2 = rho*pi;
pl = p2 + rho;
if pl = 1 then pl = 0.99;
p1c = 1-pl;
p2c = 1-p2;
c1 = pi/pic;
c2 = pic/p1;
c3 = pi/pl;
c4 = pic/p2;

logcrb = 0;
grad = j(2,1,0);
do j = 1 to n; /* Looping for all observations */
if (t[j] = 0) then do
  pr1 = PROBBNML(p1,m[j],t[j]);
  pr2 = PROBBNML(p2,m[j],t[j]);
  pt = pr1+pi*pr2;
else do
  pr1 = PROBBNML(p1,m[j],t[j]-1);
  pr2 = PROBBNML(p2,m[j],t[j]-1);
  pt = pr1+pi*pr2;
end;
if pt < 1e-10 then pt = 1e-10;
logcrb = logcrb + log(pt);
log = -2*logcrb;

Compute gradient under Random-clamped Binomial distribution;
b1 = t[j] m[j]*pi;
b2 = t[j] m[j]*p2;
a1 = c1*b1 + a2*c2;
grad[1] = grad[1] + (pr1*a1 + (pr2*a2*2*a2/c2)/pt);
grad[2] = grad[2] + (pr1*b1*c3 - pr2*b2*c4)/rhoc/pt);

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. All rights reserved. For additional resources, visit support.sas.com/publishing.

# Chapter 5 Goodness-of-fit Tests for Overdispersed Binomial Models 149

```sas
************************************************************************************
* Of looping for observations;
************************************************************************************
n
************************************************************************************
* Compute Fisher information under Random-clumped Binomial distribution;
************************************************************************************
FIMRCB = j(2,2,0);
run FISHERCB;
INVRCB = inv(FIMRCB);
logl_old = logrcb;
add = INVRCB*grad;

stop2 = 0;
split = 1;

************************************************************************************
*To check if the loglikelihood is improved with the new estimates
Otherwise modify the estimates by adding only part (splitting) for improved
estimate;
  do while (stop2 <1)
    ****************************************************************************
    div = 2**(split-1);
    beta = beta + add/div;
  end;
* Checking for the estimates we are in the range of parameter space;

  if beta[1] < 0.0001 then beta[1] = 0.01;
  else if beta[1] > 0.9999 then beta[1] = 0.99;

  if beta[2] < 0.0001 then beta[2] = 0.01;
  else if beta[2] > 0.9999 then beta[2] = 0.99;
************************************************************************************
* Compute logrcb under new beta estimate and see whether an
improvement;
************************************************************************************

pi = beta[1];
rho = beta[2];
pic = 1-pi;
rhoc = 1-rho;
pip1 = pi*pic;
pic2 = rho*pi;
pl = p2 + rho;
  if pl = 1 then pl = 0.99;
p1c = 1-pl;
p2c = 1-p2;
c1 = pi/pic;
c2 = pic/p1;
c3 = pi/pl;
c4 = pic/p2;

end do;
```
