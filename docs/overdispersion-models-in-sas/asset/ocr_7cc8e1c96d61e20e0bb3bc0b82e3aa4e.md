# 362 Overdispersion Models in SAS

# Program 10.5: Generation and Analysis of Data under a Random-clumped Binomial GLOMM

```
/*
Random-clumped Binomial GLOMM
Random-clumped Binomial Model with Logit Link and Random Effects
Random effects due to Cross-over Design

t given u --- Random-clumped Binomial(pi,rho,n)
logit( pi ) = beta0 + betal * X + u
u --- Normal(0,sigma*sigma);
*/
data GLOMM
n = 200;
pi_1 = 0.12;
pi_2 = 20;
rho_2 = 0.15; --- Overdispersion Parameter;
sigma = 1.2; --- Seed;
seed = 1983;
beta0 = log(pi_1/(1-pi_1));
betal = log(pi_2/(1-pi_2)) = beta0;
rho = sqrt(rho2);
--- Sequence AB;
-----------------
doo Subj_id=1 to n;
Sequence = 'AB';
u = sigma * normal(seed);
--- Period 1;-
Period = 1;
Product = 1;
X = 1;
pi = 1 / ( 1 + exp(- beta0 - u ))
yy = ranbin(seed,1,pi);
mm = ranbin(seed,m,rho);
t = yy * mm;
if m > mm then t = t + ranbin(seed,m-mm,pi);
output;
--- Period 2;
Period = 2;
Product = 2;
X = 0;
pi = 1 / ( 1 + exp(- betal - u ))
yy = ranbin(seed,1,pi);
mm = ranbin(seed,m,rho);
t = yy * mm;
if m > mm then t = t + ranbin(seed,m-mm,pi);
output;
---
end;
n--- Sequence BA;
-----------------
doo Subj_id=n+1 to n+n;
Sequence = 'BA';
u = sigma * normal(seed);
--- Period 1;-
Period = 1;
```