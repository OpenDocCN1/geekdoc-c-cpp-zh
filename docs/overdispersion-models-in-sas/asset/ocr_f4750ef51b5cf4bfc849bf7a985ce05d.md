# Chapter 10 Generalized Linear Overdispersion Mixed Models 367

# Program 10.6: A Zero-inflated Poisson GLOMM

```
/*
Generation of data under a Zero-inflated Poisson GLOMM
with parameters Beta0, Betal, W, and Sigma**
*/
data zip_glomm;
  beta0 = 0.70;
  betal = 0.40;
  w = 0.20;
  sigma2 = 1.2;
  m = 200;
  seed = 1917;
  nl = n+1;
  n2 = n+n;
  sigma = sqrt(sigma2);
do id=1 to m;
  u = uniform(seed);
  if u > w then
    Group = 1;
    mu = exp(Beta0+Betal+z);
    Y = ranpoi(seed,mu);
    output;
  else do
    Group = 0;
    Y = 0;
    output;
  end;
end;
do id=nl to n2;
  z = Sigma*normal(seed);
  do id=1 to m;
    u = uniform(seed);
    if u > w then
      Group = 0;
      mu = exp(Beta0 + +z);
      Y = ranpoi(seed,mu);
      output;
    else do
      Group = 0;
      Y = 0;
      output;
    end;
end;
keep it t group;
run;
ods html;
title "Initial estimates of Beta0, Betal and Sigma**2 using PROC GLIMMIX";
proc glimmix data=zip_glomm method=quad-order=data;
  class group;
  model Y = group / link=dist=poisson;
  random int / subject=id;
run;
```