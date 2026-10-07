# Chapter 3 Quasi-likelihood Functions 57

```
/*
pH Oral Care Example from Schulte et al., 1998
*/
data pH;
  input t f;
  m = 4;
  datalines;
0 4
1 4
2 6
3 2
4 1n;
proc genmodel data=pH;
  model t/m = dist/binomial link=identity scale=deviance;
  freq f;
run;
```

# 3.4 Toxoplasmosis in El Salvador

We shall now consider a logistic regression example where covariates are available to model the results. Efron (1978, 1986) examined data from 34 cities in El Salvador where the outcome "number of cases testing positive for Toxoplasmosis (tⱼ) out of the number of subjects (mⱼ)" was analyzed as a function of some covariates based on annual rainfall (inches). All subjects were adolescents between 10 and 15 years old.

Table 3.2: Number of Subjects Testing Positive for Toxoplasmosis (tⱼ) Out of (mⱼ) Sampled Subjects in 34 Cities of El Salvador
| City (j) | Number Positive Cases (tⱼ) | Number Sampler (mⱼ) | Annual Rainfall (in) (xⱼ) |
| 1 | 2 | 4 | 1735 |
| 2 | 3 | 10 | 1936 |
| 3 | 1 | 5 | 2000 |
| 4 | 3 | 10 | 1973 |
| 5 | 2 | 5 | 1750 |
| 6 | 3 | 5 | 1800 |
| 7 | 2 | 8 | 1750 |
| 8 | 7 | 19 | 2077 |
| 9 | 3 | 6 | 1920 |
| 10 | 8 | 10 | 1800 |
| 11 | 7 | 24 | 2050 |
| 12 | 0 | 1 | 1830 |
| 13 | 15 | 30 | 1650 |
| 14 | 4 | 22 | 2200 |

(continued)

Morel, Jorge, and Nagaraj Neeraraj. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.