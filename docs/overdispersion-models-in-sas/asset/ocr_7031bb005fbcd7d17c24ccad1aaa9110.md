# Chapter 7 Likelihood Models for Overdispersed Multinomial Responses 255

```
****************************************************************
Start ProbMultinomial1(m, p, t);

k = nrow(p+1);
temp = mj;
g = 1;
If (t[1]=0) Then Prob = PROBNML(p[1], mtemp, t[1]);
Else Prob = (PROBNML(p[1], mtemp, t[1])-PROBNML(p[1], mtemp, t[1]);

Do i = 2 to (k-1) While (mtemp > 0)
  mtemp = t([i-1]);
  If (mtemp*=0) Then Do:
    ti = t([i-1]);
    g = g-p([i-1]);
    newp = p[i]/g;
    If (t[i]=0) Then Prob = Prob*PROBNML(newp, mtemp, t[i]);
    Else Prob = Prob*PROBNML(newp, mtemp, t[i])-PROBNML(newp, mtemp, t[i-1]);
  End;
End;

If Prob < 1e-50 Then Prob = 1e-50
Return(Prob);
```

```
Finish;
Store Module=ProbMultinomial;

Start ProbMultinomial2(m, p, t);

k = nrow(p+1);
Prob = 1;

Do i = 1 to (k-1)
  Prob = Prob*((p[i])**t[i])/gamma(t[i]);
End;
```

```
pk = 1-sum(p);
tk = m-sum(t);

Prob = Prob*gamma(m+1)*(pk**tk)/gamma(tk+1);
Return(Prob);
```

```
Finish;
Store Module=ProbMultinomial2;

Start ProbMultinomial3(m, p, t);

k = nrow(p+1);
Prob = 0;

Do i = 1 to (k-1)
  Prob = Prob + t[i]*log(p[i]) - lgamma(t[i]+1);
End;
```

```
pk = 1-sum(p);
tk = m-sum(t);

Prob = Prob + lgamma(m+1)+ tk*log(pk) - lgamma(tk+1);
Return(Prob);
```

More, Jorge, and Nagaraj Neerchal. Overdisped Models in SAS.. Copyright © 2011, SAS Institute, Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.