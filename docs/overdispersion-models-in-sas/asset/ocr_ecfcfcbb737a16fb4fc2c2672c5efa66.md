# Chapter 8 A Two-stage Maximum Likelihood Estimation Procedure 279

```
%Macro DM_RCM_Exact_Approximate(data, label);
title &label;

Proc IML;

use &data;
read all into T;

n = nrow(T);
k = ncol(T);
m = sum(T(1));

Parameter = shape(('PI1') ('PI2') ('PI3') ('PI4') ('PI5')
('PI6') ('PI8') ('PI9'),k-1,1) // ('Rho) // ('Log Likelihood);
FVALUE = j(k,1,0);

mattrib Estimate format=12.5;
mattrib StdErr format=12.6;
mattrib AppStdErr format=12.6;
mattrib Pic_Rel_Error format=12.5;

**************************************/
/* MLE from DM Distribution */
**************************************/
Load Module=MLEM;

thetaMLE = MLEM(m, T);
pIMLE1 = thetaMLE[1:(k-1)];
rhoMLE1 = thetaMLE[k];

INVIM = Inv(*nFIDM(m, pIMLE1, rhoMLE1));
SE1 = j(k,1,0);
Do i 1 to k;
SE1[i] = sqrt(INVIM[i,i]);
End;

ll = 0;
Do j 1 to n;
tj = T[j:(k-1)];
l11 = ll + log(ProbDM(m, pIMLE1, rhoMLE1, tj));
End;

Estimate = pIMLE1 // rhoMLE1 // ll11
StdErr = SE1;
Pct_Rel_Error = StdErr;

**************************************/
/* MLE from DM Distribution using approximate FIM */
**************************************/\nLoad Module=Stage2DM;

thetaMLE = Stage2DM(m, T);
pIMLE1 = thetaMLE[1:(k-1)];
rhoMLE1 = thetaMLE[k];

INVIM = Inv(*nFIDM(m, pIMLE1, rhoMLE1)); // ---- Updates FIM;
SE1 = j(k,1,0);
Do i 1 to k;
```

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS. Copyright © 2011, SAS Institute, Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.