
# 252 SAS 中的过度离散模型

```sas
********************************************************************
/* Module: MLERCM(m, T)                                               *
/* 此模块使用费舍信息                 *
/* Matrix和费舍评分算法从随机聚类多项 *                             *
/* 分布中计算 MLE                             *
/* m - 聚类大小                                                  *
/* T - nxk 计数矩阵 (t1,t2,...,tk)，其中 ti 是 *                          *
/* nxl 向量，表示类别 i 中的观测计数                    /
/****************************************************
Start MLERCM(m, T);
print "**费舍评分法 -- 随机聚类多项分布 ***";
pi0 = QLEpi(m,T);
rho0 = QLErho(m,T,pi0);
k = ncol(T);
n = nrow(T);
theta[1:k-1] = j(k,1,0);
theta[k] = rho0;

eps = 1E-8;
conv = 1;
iter = 0;
Do Until(conv<eps);

  iter = iter + 1;
  pi = theta[1:k-1];
  rho = theta[k];
  INFIM = Inv(n*FIMCM(m, pi, rho));
  Old = 0;
  Scores = j(k,1,0);
  Do j = 1 to n;
    tj = T[j,1:k-1];
    Scores = Scores + gradRCM(m, pi, rho, tj);
    Old = Old + log(ProbRCM(m, pi, rho, tj));
  End;

  si = 0;
  Lnew = Old - 1;
  Do Until (Lnew > Old);
    thetaNew = theta + {0.5*si}INVNFIM*Scores;
    pi = thetaNew[1:k-1];
    rho = thetaNew[k];
    Lnew = 0;
        Do j = 1 to n;
            tj = T[j,1:k-1];
            Lnew = Lnew + log(ProbRCM(m, pi, rho, tj));
        End;

        si = si + 1;
        if si > 20 then;
            print "NOTE: 步长减了二十次，假设收敛";
            Lnew = Old + 0.000001;
        end;
    End;

    theta = thetaNew;
    conv = abs(Lnew)/(abs(Lnew)+1E-6);
    conv_0 = conv;

    if si > 20 then conv = eps - 0.000001;
    if iter > 100 then;
        print "NOTE: 迭代 100 次后，尚未满足收敛";
        conv = eps - 0.000001;
    end;

End;

if conv_0 < eps then;
    print "NOTE: 收敛标准 (EPSILON-1E-8) 已满足";
end;

Return(theta);

Finish;
Store=MLERCM
```

## 费舍信息矩阵

```sas
******************************************************

/* 费舍信息矩阵                                */

******************************************************

******************************************************

/* Module: FIMDM(m,pi)                                */

/* 此模块返回狄利克特 *                                

/* 多项分布的费舍信息矩阵                                */

/* m = 聚类大小                                                    

/* pi = 概率向量 [pi1, pi2, ..., pk]               */

/* rho - 相关系数                                                    */

******************************************************

Start FIMDM(m, pi);

k = nrow(pi);

c = (1-rho)/rho;

FIM = j(k, c, 0);

PrK = 0;

PrC = 0;

pik = 1-sum(pi);

Do s = 1 to m;

    PrK = PrK + ProbDM(m, pi, rho, s)/(c*pi[s]-s)**2;

    PrC = PrC + (c+s-1)**-2;

end;

Do i = 1 to (k-1);

    PrI = 0;

    Do s = 1 to m;

        PrI = PrI + ProbDM(m, pi[i], rho, s)/(c*pi[i]+s-1)**2;

    end;

    FIM[i,j] = (c**2)*(PrI + PrK);

    Do j = (i+1) to (k-1);

        FIM[j,i] = (c**2)*(PrI + PrK);

    End;

    FIM[i,k] = c*(pi*PrK - pi[i]*PrI) * (2/rho**3);

    FIM[k,i] = c*(pi*PrK - pi[i]*PrI) * (2/rho**3);

    End;

    FIM[k,k] = (FIM[k,k] + (pi**2)*PrK - PrC) * (4/rho**6);

End;

Return (FIM);

Finish;

Store Module=FIMDM;
```

```sas
/* t - 成功次数

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

```sas
/*******************************************************/
/* 该模块根据 Beta-二项分布返回 P(T>t) 

 */
/* m - 聚类大小
/* pi - 成功概率
/* rho - 相关性
/* t - 成功次数
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

```sas
/*******************************************************/
/* 该模块根据多项分布返回 P(T1, T2=t2, ...Tk=tk)  */
/* 实现此函数有多种方法。这里提供了三个 */
/* 版本。 */
/* m - 聚类大小
/* p - 概率向量 [p1,p2...,p(k-1)]`
/* t - 计数向量 [t1,t2,...,tk(k)]`
```

# 第 7 章 针对过度离散多项响应的似然模型 255

```sas
****************************************************************

Start ProbMultinomial1(m, p, t);

k = nrow(p+1);

mtemp = mj;

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

```sas
Finish;

Store Module=ProbMultinomial;

Start ProbMultinomial2(m, p, t);

k = nrow(p+1);

Prob = 1;

Do i = 1 to (k-1)

  Prob = Prob*((p[i])**t[i])/gamma(t[i]);

End;
```

```sas
pk = 1-sum(p);

tk = m-sum(t);

Prob = Prob*gamma(m+1)*(pk**tk)/gamma(tk+1);

Return(Prob);
```

```sas
Finish;

Store Module=ProbMultinomial2;

Start ProbMultinomial3(m, p, t);

k = nrow(p+1);

Prob = 0;

Do i = 1 to (k-1)

  Prob = Prob + t[i]*log(p[i]) - lgamma(t[i]+1);

End;
```

```sas
pk = 1-sum(p);

tk = m-sum(t);

Prob = Prob + lgamma(m+1)+ tk*log(pk) - lgamma(tk+1);

Return(Prob);
```

More, Jorge, and Nagaraj Neerchal. Overdispersed Models in SAS.. Copyright © 2011, SAS Institute, Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/publishing。

# 256 SAS 中的过度离散模型

```sas
Store Module=ProbMultinomial;
```

```sas
StartProbRCM(m, pi, rho, t);

  k = nrow(pi)+1;

  e = diag((j(k-1), rho));

  Prob = 0;

  Do i = 1 to (k-1);

    pi = (1-rho)*pi + e[i];

    Prob = Prob + pi[i]*ProbMultinomial(m, pi, t);

End;
```

```sas
piK = (1-rho)*pi

pk = -sum(pi)

Prob = Prob + pk

Return(Prob);

Finish;

Store Module=ProbRCM;
```

```sas
StartProbDM(m, pi, t);

  k = nrow(pi)+1;

  c = (1-rho)/rho**2;

  Prob = 0;

  Do i = 1 to (k-1);

    pi = (1-rho)*pi + e[i];

    Prob = Prob + pi[i]*ProbMultinomial(m, pi, t);

End;
```

```sas
piK = (1-rho)*pi

pk = -sum(pi)

Prob = Prob + pk*

Return(Prob);

Finish;

Store Module=ProbDM;
```

```sas
StartProbG(m, pi, t);

  k = nrow(pi)+1;

  g = 1;

  e = j(k-1), rho);

  Prob = 0;

  Do i = 1 to (k-1);

    pi = (1-rho)*pi + e[i];

    Prob = Prob + pi[i]*ProbMultinomial(m, pi, t);

End;
```

```sas
piK = (1-rho)*pi

pk = -sum(pi)

Prob = Prob + pk*

Return(Prob);

Finish;

Store Module=ProbG;
```
