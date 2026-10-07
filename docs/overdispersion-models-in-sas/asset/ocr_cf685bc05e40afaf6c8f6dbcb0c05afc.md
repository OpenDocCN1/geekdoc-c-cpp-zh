# 250 Overdispersion Models in SAS

```
*** Fisher Scoring Method -- Dirichlet-Multinomial Distribution ***;

pi0 = QLEpi(m,T);
rho0 = QLErho(m,T,pi0);
k = ncol(T);
n = nrow(T);
theta = = j(k,1,0);
theta[1:k-1] = pi0;
theta[k] = rho0;

eps = 1E-8;
conv = 1;
iter = 0;
Do Until(conv<eps);

    iter = iter + 1;
    pi = theta[1:k-1];
    rho = theta[k];
    INVNFIM = Inv(n*FIMDM(m, pi, rho));
    Old = 0;
    Scores = j(k,1,0);
    Do j = 1 to n;
        tj = T[j,1:k-1];
        Scores = Scores + gradDM(m, pi, rho, tj);
    Old = Old + log(ProbDM(m, pi, rho, tj));
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
        Lnew = Lnew + log(ProbDM(m, pi, rho, tj));
    End;

    si = si + 1;
    if si > 20 then;
        print "NOTE: Step size halved twenty times, convergence assumed";
        Lnew = Old + 0.000001;
    end;
End;

theta = thetaNew;
conv = abs(Lnew)/(abs(Lnew)+1E-6);
conv_0 = conv;

if si > 20 then conv = eps - 0.000001;
if iter > 100 then;
    print "NOTE: After 100 iterations, convergence not met yet";
    conv = eps - 0.000001;
end;

End;

if conv_0 < eps then;
    print "NOTE: Convergence criterion (EPSILON-1E-8) satisfied";
end;
```

Morel, Jorge, and Nagaraj Nechel. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.