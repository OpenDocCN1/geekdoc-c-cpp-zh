# 256 Overdispersion Models in SAS

Store Module=ProbMultinomial;

```
StartProbRCM(m, pi, rho, t);

  k = nrow(pi)+1;
  e = diag((j(k-1), rho));
  Prob = 0;

  Do i = 1 to (k-1);
    pi = (1-rho)*pi + e[i];
    Prob = Prob + pi[i]*ProbMultinomial(m, pi, t);
End;
```

```
piK = (1-rho)*pi
pk = -sum(pi)
Prob = Prob + pk*ProbMultinomial(m, piK, t);
Return(Prob);
```

Finish;
Store Module=ProbRCM;

```
StartProbDM(m, pi, rho, t);

  k = nrow(pi)+1;
  c = (1-rho)*2/rho+2;
  Prob = lgamma(m+1)+lgamma(c)-lgamma(m+c);

  Do i = 1 to (k-1);
    Prob = Prob+lgamma(t[i]+c*pi[i])-lgamma(t[i]+1)-lgamma(c*pi[i]);
End;
```

```
piK = -sum(pi);
tK = m-sum(t);
Prob = Exp(lgamma(tK+c*piK)-lgamma(c*piK));
Return(Prob);
```

Finish;
Store Module=ProbDM;

Morel, Jorge, and Nagaraj Neel. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc. Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.