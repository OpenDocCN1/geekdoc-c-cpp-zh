```
covariance matrix */
%optcont(models=models, doses=doses, sigma=omega, direction=incr,
dosevarname=dose*time);
%put &modcontr;

data _null_;
  call execute(
proc glmix data=neurodeg;
class dose id;
  model resp=dose*time /solution COVB ;
  random intercept time / type=UN subject=id;
  estimate
  / adjust=simulate(&modcontr; (nsample=1000000 seed=1) uppertialed
run);\nrun;

/* Bootstrap simulations to get estimates and CI for dose-response
estimates*/
proc iml;
  /initiation step*/
call randseed(1);
nsime=1000;

  / read-in data */
use omega;
read all var (col2 col3 col4 col5 col6) into cv;
use beta;
read all var (Estimate) into mn;
read all var (dose) into dose;

  / model fitting */
  /* additional variables needed after */
invs=inv(cv);
nd-row(dose);
predmn=mn;
resp=mn;

  /* define functions to optimize for different models */
  start fnglsemax(par) global (dose, resp, predmn, nd);

  do i=1 to nd;
    predmn[i]=par[1]+par[2]*dose[i]/(dose[i] + par[3]);
  end;
  dif=(predmn-resp);
  return(dif*invs*dif);
  finish fnglsemax;
start fnglsexpo(par) global (dose, resp, predmn, nd);

  do i=1 to nd;
    predmn[i]=par[1]+par[2]*(exp(dose[i]/par[3]))-1);
  end;
  dif=(predmn-resp);
  return(dif*invs*dif);
  finish fnglsexpo;
start fngslin(par) global (dose, resp, predmn, nd);

  do i=1 to nd;
    predmn[i]=par[1]+par[2]*dose[i];
  end;
  dif=(predmn-resp);
  return(dif*invs*dif);
  finish fngslin;
start fngslquad(par) global (dose, resp, invs, predmn, nd);

  do i=1 to nd;
    predmn[i]=par[1]+par[2]*dose[i]+par[3]*dose[i]*2;
```

# 386