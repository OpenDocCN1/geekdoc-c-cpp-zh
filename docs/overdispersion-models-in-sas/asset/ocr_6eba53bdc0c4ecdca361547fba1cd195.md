# Chapter 7 Likelihood Models for Overdispersed Multinomial Responses 219

| z2 | = z2 || z[2,1]; |
|---||
| end; | |
| scale | = scale / d / (n-k); |
| phi | = phi / df; |

```
print n d k ,, scale[format=8.4],, phi[format=8.4];;

--- Part 2) Compute Generalized Multinomial Variance

uu = j(d+k,1,0);
h = j(d+k,d,0);
inv_diag = inv( diag ( phi ) );

do j=1 to n;
p = t(pred_probs[j]);
nt = t(obs_ts[j,1:d]);
flf = cumsum(p);
flf = flf # (1 - flf);
f2f = flf;

temp = diag( phi );
if d > 1 then;
oi = 1 to d-1;
il = i+1;
temp[il,i] = -flf[il,i];
f2f[il,1] = f2f[il,1] - flf[il,i];
end;
end;

der = temp || f2f @ x_matrix[j,];
call inv_cp(p,a,d);
aux = der* a* inv_diag phi * a;
u = u + aux * ( t - m[j,1] * p);
h = h + m[j,1] aux * der;
```

covb = inv(h);

StdErr = diag(covb) ## 0.5 * j(d+k,1,1);
create StdErr var (StdErr);
append;

create Residuals var (z1 z2);
append;

quit;

data beta;
format Variance $29;
Variance = "Scale Multinomial";nset beta;

run;

data beta2;
format Variance $29;

Morel, Jorge, and Nagaraj Neeraraj. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.