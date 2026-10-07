```
/* t - number of success
 *******************************************************/
Start ProbBBB(m, pi, rho, t);

 c = (1-rho**2)/rho**2;
N1 = 0;
N2 = 0;
D = 0;

 Do k = 1 to t1;
  N1 = N1+log(c*pi + k - 1);
End;
  Do k = 1 to (m-t2);
  N2 = N2+log(c*(1-pi) + k - 1);
End;
  Do k = 1 to m;
  D = D+log(c + k - 1);
End;

  Prob = comb(m,t)*exp(N1+N2-D);
  Return(Prob);

Finish;
Store::Module=ProbBBB;
```

```
/*******************************************************/
/* This Module returns P(T>t)from a Beta-Binomial
/* Distribution
/* m - cluster size
/* pi - probability of success
/* rho - correlation
/* t - number of success
/******************************************************/
StartProbGTRBB(m, pi, rho, t);

 Prob = 0;
 If t/m >= 0.5 Then;
  Do i = t to m;
    Prob = Prob + ProbBB(m, pi, rho, i);
  End;
 Else Do;
  Do i = 0 to (t-1);
    Prob = Prob + ProbBB(m, pi, rho, i);
  End;
 Prob = 1 - Prob;
 End;

Finish;
Store::Module=ProbGTRBB;
```

```
/*******************************************************/
/* This Module returns P(T1, T2=t2, ...Tk=tk) from */
/* Multinomial Distribution. There are several ways to
/* implement this function. Three versions are provided. */
/* m - cluster size
/* p - vector of probabilities [p1,p2...,p(k-1)]`
/* t - vector of counts [t1,t2,...,tk(k)]`
```