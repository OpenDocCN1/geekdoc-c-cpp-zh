# Chapter 8 A Two-stage Maximum Likelihood Estimation Procedure 273

```
/*
* m - cluster size */
/* T - nxk matrix of counts (t1,t2,...,tk) where ti is a */
/* ni vector of observed counts in category i */
********************************************************************
```

StartMLEM(m,T);
print "**** Fisher Scoring Method using approximate FIM -- Dirichlet-Multinomial Distribution **";

```
pi0 = QLEpi(m,T);
rho0 = QLRho(m,T,pi0);
k = ncol(T);
n = row(T);
theta = j(k,1,0);
theta[1:k-1] = pi0;
theta[k] = rho;
```

```
eps = 1E-8;
conv = 1;
iter = 0;
Do Until(conv<eps);
```

```
iter = iter + 1;
pi = theta[1:k-1];
rho = theta[k];
INFADMIM = Inv*(nAFIDM(m, pi, rho);
Old = 0;
Scores = j(k,1,0);
Do j = 1 to n;
tj = T[j,1:(k-1)];
Scores = Scores + gradDM(m, pi, rho, tj);
Old = Old + log(ProbDM(m, pi, rho, tj));
```

```
End;
s = 0;
Lnew = Old - 1;
Do Until (Lnew > Old);
```

```
thetaNew = theta + (0.5*si)*INFADMIM*Scores;
thetaNew = thetaNew[1:(k-1)];
rho = thetaNew[k];
Lnew = 0;
Do j = 1 to n;
tj = T[j,1:(k-1)];
Lnew = Lnew + log(ProbDM(m, pi, rho, tj));
```

```
End;
s = si + 1;
if si > 20 then;
print "* Step size halved twenty times, convergence assumed*";
Lnew = Old + 0.0000001;
```

```
end;
theta = thetaNew;
conv = abs(Lnew-Lold) / abs(Lnew+1E-6);
conv_0 = conv;
```

Morel, Jane, and Nagaraj Neeraj. Overdispersion Models in SAS*. Copyright © 2011, SAS Institute Inc. Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.