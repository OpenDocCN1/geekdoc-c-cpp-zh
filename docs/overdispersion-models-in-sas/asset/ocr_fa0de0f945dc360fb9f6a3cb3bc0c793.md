# 274 Overdispersion Models in SAS

```
if si > 20 then conv = eps - 0.000001;
if iter > 100 then do;
    print "NOTE: After 100 iterations, convergence not met yet";
    conv = eps - 0.000001;
end;
```

```
End;
if conv_0 < eps then do;
    print "NOTE: Convergence criterion (EPSILON=1E-8) satisfied";
end;
Return(theta);
```

Finish;
Store Module=AMLEDM);
/****************************************************************/
/* Module: AMLERCM(m,T)
/* This Module computes the MLE from a Random-clumped Multinomial
Distribution using the approximate Fisher Information
Matrix and Fisher Scoring Algorithm

```
/* m cluster size
/ T nx matrix of counts (t1,t2,...,tk) where ti is a
/ nxl vector of observed counts in category
/****************************************************************/
```

Start AMLERCM(m,T);
print "Fisher Scoring Method using approximate RCM - Random-clumped
Multinomial Distribution ****";

```
pi0 = OLepi(m,T);
rho0 = LERho(m,T,pi0);
k = ncol(T);
row = row(T);
theta = j(k,1,0);
theta(1:(k-1)) = pi0;
theta[k,] = rho0;
```

```
eps = 1E-8;
conv = 1;
iter = 0;
Do Until(conv<eps);
    iter = iter + 1;
    pi = theta[1:(k-1)];
    rho = theta[k];
    INVFAMIM = Inv(AFIRCM(m, pi, rho));
    Lold = 0;
    Scores = j(k,1,0);
    Do j = 1 to nj;
        tj = T[j,1:(k-1)];
        Scores = Scores + gradRCM(m, pi, rho, tj);
        Lold = Lold + log(ProbRCM(m, pi, rho, tj));
```

```
End;
s = 0;
Lnew = Lold - 1;
Do Until(Lnew > Lold);
```

More, Jorge, and Nogaraj Neeraj. Overdispersion Models in SAS.. Copyright ©2011, SAS Institute Inc. Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.