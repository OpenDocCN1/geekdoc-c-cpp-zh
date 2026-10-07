# 192 Overdispersion Models in SAS

# Program 6.7: Goodness-of-fit Tests for the Hurdle Models—Daily Milk Consumption Data

```
/*
   Milk Consumption Example -- Mullahy (1986)
*/
%macro gof_test(File,Distribution,DF);
proc iml;
/* Input:    File = File Containing Observed and Expected Frequencies
               Distribution = Distribution being fitted
               DF = Degrees of Freedom for GOF Test
   Output:   Pearson's GOF and Associated P-value */
--- Get observed and expected frequencies;
use &File var (freq);
read all into obs;
use &File var (pred);
read all into exp_f;
sum1       = obs[,1];
sum2       = exp_f[,1];
exp_f[7,1] = exp_f[7,1] + sum1 - sum2;
sum2       = exp_f[,1];
--- Compute Chi-square GOF statistics and P-values;
chi = 0;
do j = 1 to 7;
  chi = chi + obs[j] * obs[j] / exp_f[j];
end;
chi = round(chi &n, 0.01);
df = &DF;
npval = 1 - probchi(chi,df,0);
--- Print results;
x0 = ('0', '1', '2', '3', '4', '5');
distribution = ({&Distribution};};
x1 = obs / sum;
x2 = exp / sum;
mattrib x0   label=Value of Y';      format=8.0;
mattrib x1   label='Observed Frequencies'; format=10.4;
mattrib x2   label='Expected Frequencies'; format=10.4;
mattrib chi label='Chi-square';        format=8.2;
mattrib df   label='DF';                format=8.0;
mattrib pval label='P-Value';          format=pvalue6;

print 'Goodness-of-fit Tests Results';
print x0 x1 x2;
print Distribution chi df pval;
quit;
%end gof_test;\ods html;
title1 "Milk Consumption Example -- Mullahy (1986)"
title2 "Poisson Hurdle Model";
```

Morel, Jorge, and Nagaraj Neel. Overdispersion Models in SAS®. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.