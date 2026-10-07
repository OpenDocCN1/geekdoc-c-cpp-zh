# Chapter 7 Likelihood Models for Overdispersed Multinomial Responses 257

```
/ pi vector of probabilities {pi,p2,...,p(k-1)}    */
/* rho - correlation                                */
/* vector of counts {t1,t2,...,t(k-1)}                               */
********************************************************************
Start gradRCM(m, pi, rho, t);
k = nrow(pi);
PrT = ProbRCM(m, pi, rho, t);
e = diag((k-1),rho);
piK = (1-rho)*pi;
prk = ProbMultinomial(m, pi, TK);
pk = 1-sum(pi);
tk = m-sum(t);
A = (tk/pk) + (prXK/PrTK)*(1-(rho*tk)/((1-rho)*pk));
grad = j(k,1,0);
```

```
Do i = 1 to (k-1);
piI = (1-rho)*pi
prXI = ProbMultinomial(m, pi, t);
ai = (t[i]/pi[i]) + (PrXI/PrTI)*(1-(rho*t[i])/pi[i]);
grad[i,] = ai;
grad[k,] = grad[k,] + pi*prXI*(t[i]);
```

```
End;
grad[k,] = (1/((1-rho)*prTK))*(grad[k,]+prXK*((tk-m)*pk+rho))/((1-rho)*pk+rho));
Return(grad);
```

Finish;
Store Module=gradRCM;

```
Start gradRCM(m, pi, rho, t);
k = nrow(pi)+1;
piK = 1-sum(pi);
tK = m-sum(t);
c = (1-rho^2)/rho^2;
grad = j(k,0,1);
fM = 0;
fTK = 0;
```

```
fM = sum(1/(c:(c-m)));
If (TK > 0) Then fTK = sum(1/(c*piK+c*TK-1));
sumTI = piK*fTK;
```

```
Do i = 1 to (k-1);
fTI = 0;
If (t[i], > 0) Then fTI = sum(1/(c*pi[i]:(c*pi[i]+t[i]-1));
grad[i,] = c*(fTI);
sumTI = sumTI + pi[i]*fTI;
```

Morel, Jorge, and Nagaraj Neharjee. Overdispersed Models in SAS. © 2011, SAS Institute Inc., Cary,
North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.