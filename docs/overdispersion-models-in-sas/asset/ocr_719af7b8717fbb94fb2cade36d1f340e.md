```
append tm;
quit;
ods output ParameterEstimates=Parms_Estimates
AdditionalEstimates=Estimates;
proc nlmixed a=0 data=new;
parms a=0, b0=0, b02=0;
rho = -1 / (1 + exp(-a0));
etal = exp(b01);
eta2 = exp(b02);
p1 = etal/(1+etal+eta2);
p2 = eta2/(1+etal+eta2);
p3 = 1-p1-p2;
t3 = t1+t2;
c = (1-rho**2)/(1+rho**2);
const = lgamma(m+1)-lgamma(t1+1)-lgamma(t2+1)-lgamma(t3+1);
  loglik = lgamma(c)-lgamma(m+c)+lgamma(t1+c+1)+lgamma(t2+c*p2)
  +lgamma(t3*c+p3)-lgamma(c*p1)+lgamma(c*p2)-lgamma(c*p3);
model t1 ~ general(loglik);
estimate 'Kappa' / 1 / (1 + exp(-a0)) / (1 + exp(-a0));
run;
```

```
data Estimates;
set Estimates;
rename Estimate = Kappa;
keep Estimate Lower Upper;
run;
```

```
data Parm_Estimates;
set Parm_Estimates;
if Parameter = 'a0';
Estimate = 1 / (1 + exp(-Estimate)) / (1 + exp(-Lower));
Lower = 1 / (1 + exp(-Lower)) / (1 + exp(-Lower));
Upper = 1 / (1 + exp(-Upper)) / (1 + exp(-Upper));
rename Estimate = Kappa;
keep Estimate Lower Upper;
run;
```

```
title2 "Kappa Results using the Estimate Statement in NLMIXED";
proc print data=Estimates noobs;
run;
```

```
title2 "Kappa Results using the Inverse Method in NLMIXED";
proc print data=Parms_Estimates noobs;
run;
```

Note that in NLMIXED $\kappa$ is reparameterized as $\frac{\exp(\hat{\alpha}_0)}{1+\exp(\hat{\alpha}_0)}$, which appears in the statement. The estimated variance of $\hat{\kappa}$, $\hat{v}(\hat{\kappa})$, is calculated using Taylor's linearization. Thus, an approximate 95% confidence interval for $\kappa$ is computed as $\hat{\kappa}\pm 1.96\sqrt{\hat{v}(\hat{\kappa})}$. To guarantee that