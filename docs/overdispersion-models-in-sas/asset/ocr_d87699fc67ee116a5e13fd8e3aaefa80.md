```
bounds 1>rho0;
etal = al1*zn2*b12*cd2*cd13*b14*zn2_cd2*b15*zn2_cd3;
eta2 = eta2*b21*zn2*b22*cd2*cd23*b23*b24*zn2_cd2*b25*zn2_cd3;
gamma1 = 1/(1+exp(-eta1))
gamma2 = 1/(1+exp(-eta2))
pl1 = gamma1
pl2 = gamma2
p = pl1 - pl2
m = t1+t2+t3
c = (1-rho2)/(rho2);
loglik = lgamma(m+1)-lgamma(t1+1)-lgamma(t2+1)-lgamma(t3+1)
lgamma(c)-lgamma(m+c)-lgamma(t1+c)*lgamma(t2+c)+lgamma(t2*c)
lgamma(t3+c)-lgamma(t3+c)-lgamma(p1)*lgamma(c*p2)-lgamma(c*p3)
+ const;
todel tl = general(loglik);
contrast = "Proportionality Assumption Test -- DM Distribution"
b11-b21, b12-b22, b13-b23, b14-b24, b15-b25;
```

Title Testing Proportionality — Random-coupled Multinomial Distribution;

ods Outputs Contrast-Assump_Rho RCM FitStatistics-Fit_Rcm_full Full_Dimensions=Dimensions_1
ParameterEstimates=Betas_RCM CoVarMapEstimate=Cov_RCM;

```
Proc nlmix data=defects cov;
params al=3.7, a2=2.4, b11=0.2, b21=0.2, b31=3.1, b22=3.1,
b13=3.5, b23=3.5, b14=-1.8, b24=-1.8, b15=-1.7, b25=-1.7,
rho=0.5;
bounds 1>rho0;
etal = al1*zn2*b12*cd2*cd13*b14*zn2_cd2*b15*zn2_cd3;
eta2 = eta2*b21*zn2*b22*cd2*cd23*b23*b24*zn2_cd2*b25*zn2_cd3;
gamma1 = 1/(1+exp(-eta1))
gamma2 = 1/(1+exp(-eta2))
pl1 = gamma1;
pl2 = gamma2;
p = pl1 - pl2
m = t1+t2+t3;
hoc = 1-rho2;
loglik = log (lgamma(m+1)-lgamma(t1+1)-lgamma(t2+1)-lgamma(t3+1))
+ (p***(rhoc*rho1**t1)*(rhoc*rho2**t2)*(rhoc*rho3**t3))
+ (p***(rhoc*rho1**t1)*(rhoc*rho2**t2)*(rhoc*rho3**t3))
+ (p***(rhoc*rho1**t1)*(rhoc*rho2+p3)**3))
+ const2;
todel tl = general(loglik);
contrast = "Proportionality Assumption Test -- RCM Distribution"
b11-b21, b12-b22, b13-b23, b14-b24, b15-b25;
```

ods html close;

Table 7.6 the MLEs obtained by running Program 7.5.