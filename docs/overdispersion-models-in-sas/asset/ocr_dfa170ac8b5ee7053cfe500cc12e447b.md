# 276 Overdispersion Models in SAS

```
pII = pi[i];
PrI
RI = TriGamma(c*pII);
FIM[i,i] = (c*2)*(PrI + PrK);
Do j = (i+1) to (k-1)
FIM[i,j] = (c*2)*PrK;
FIM[j,i] = (c*2)*PrK;
```

```
End;
FIM[i,k] = c*(piK*PrK - piI*PrI)/(rho*3);
FIM[k,i] = c*(piK*PrK - piI*PrI)/(rho*3);
FIM[k,k] = (piII*2)*PrI;
```

```
End;

FIM[k,k] = (FIM[k,k] + (piK*2)*PrK PrC)*(4/rho*6);
Return (FIM);
```

Finish;
Store Model=AFIMDM;

```
****************************************************************
/* Module: AFIRCM(m, pi, rho) */
/* This module returns the Approximate Fisher Information */
/* Matrix for a Random-clumped Multinomial Distribution */
/* References: Neerchal, CSDA (2004) - Result 2 */
/* Neerchal and Morel, JASA (1998) - Theorem 2 */
/* Model and Nagaraj, Biometrika (1993) - Theorem 1 */
/* m - cluster size */
/* vector of probabilities [pi1, pi2, ..., pi(k-1)] */
/* rho - correlation */
****************************************************************
```

```
Start AFIRCM(m, pi, rho);

k = nrow(pi)+1;
FIM = j(k,k,0);
```

```
piK = 1-sum(pi);
betaK = piK/((1-rho)*piK+rho) + (1-piK)/((1-rho)*piK+rho);
gammaK = piK*((1/((1-rho)*piK+rho))/(1-rho);
Do i = 1 to (k-1)

piII = pi[i];
betaI = piII/((1-rho)*piII+rho) + (1-piII)/((1-rho)*piII+rho);
gammaI = piII*(1/((1-rho)*piII+rho)) + piI/(1-rho);
FIM[i,i] = m*((1-rho)*2)*betaI+betaK + 1/piK;
FIM[i,j] = m*((1-rho)*2)*betaI + 1/piK;
FIM[j,i] = m*((1-rho)*2)*betaK + 1/piK;
```

```
End;
FIM[i,k] = m*(1-rho)*(gammaI-gammaK);
FIM[k,i] = m*(1-rho)*(gammaI-gammaK);
FIM[k,k] = FIM[k,k] + (piII*(1-piII))((1-rho)*piII+rho);
```

```
End;

FIM[k,k] = {FIM[k,k] + (piK*(1-piK))*((1-rho)*piK+rho)*(m/(1-rho));
Return (FIM);
```

Finish;
Store Model=AFIRCM;

Morel, Nagaraj and Neerchal. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary,
North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS support, visit support.sas.com/publishing.