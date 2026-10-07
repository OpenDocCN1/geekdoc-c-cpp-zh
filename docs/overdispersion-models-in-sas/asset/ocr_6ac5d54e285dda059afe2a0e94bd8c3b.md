# Chapter 5 Goodness-of-fit Tests for Overdispersed Binomial Models 133

```
proc stdize data=hiroshima out=hiroshima;
  var z;
run;

data hiroshima;
  set hiroshima;
  zz = z * z;
run;

ods html;
ods graphics;

title "***Beta-binomial fit ****";
ods output Dimensions=Dimensions;
proc nlmixed data=hiroshima;
  parms b0=1 b1=0 b2=0 a0=0 a1=0 a2=0;
  rho = -1 / ( 1 / (1 + exp(-a1*z-a2*zz));
  xbeta = b0 + b1*z + b2*zz;
  pi = 1 / ( 1 + exp( xbeta ) );
  theta = 1 / rho - 1;
  c = lgamma(m-1) * lgamma(m-theta) + lgamma(theta*pi) + lgamma(m-t*theta*(1-pi)) - lgamma(m-theta*pi) - lgamma(theta*(1-pi));
  model t = general( l );
  predict pi out=pi_bb;
  predict rho out=rho_bb;
run;

data Dimensions;
  set Dimensions;
  if Descr = "Parameters" then call sympt(
params_bb',trim(left(Value)));
    "-nparams is number of parameters";
run;

data pi_bb;
  set pi_bb;
  keep Pred;
run;

data rho_bb;
  set rho_bb;
  keep Pred;
run;

title "***Random-clumped Binomial fit ****";
ods output Dimensions=Dimensions;
proc nlmixed data=hiroshima;
  parms b0=1 b1=0 b2=0 a0=0 a1=0 a2=0;
  rho = -1 / ( 1 / exp(-a1*z-a2*zz));
  xbeta = b0 + b1*z + b2*zz;
  pi = 1 / ( 1 + exp( xbeta ) );
  pl = (1 - rho)*pi + rho;
  plc = 1 - pi;
  p2 = rho;
  p2c = 1 - p2;
  c = lgamma(m+1) - lgamma(t+1) - lgamma(m-t+1);
  ll = c + log(pi**t*plc**(m-t)) + pic*p2**t*p2c**(m-t));
  model t = general( l );
  predict pi out=pi_rcb;
  predict rho out=rho_rcb;
```

Morel, Jorge and Nagaraj Neeler. Overdispersed Models in SAS^*. Copyright © 2011, SAS Institute Inc., North Carolina, USA. ALL RIGHTS RESERVED. For additional resources, visit support.sas.com/publishing.