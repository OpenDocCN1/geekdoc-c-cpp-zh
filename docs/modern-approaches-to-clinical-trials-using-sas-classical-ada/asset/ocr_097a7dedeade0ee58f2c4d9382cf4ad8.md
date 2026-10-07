```
read all;
use &skeleton;
read all;
phat={};
dose=dosecurse[nrow(doselevel)];
stop=0;
/* posterior-likelihood prior */\nstart posterior(alpha) global (DLT,doselevel,p,cohortsize);
sigma=2;
lik=1;
nn=nrow(j);
 k=1 to nn
pi=(p[doselevel[k]])##exp(alpha);
lik=lik*(pi##(DLT))##(1-pi)##(cohortsize[k]-DLT[k]);
end;
lik=exp(-0.5*alpha*alpha/sigma2);
return(lik);
finish;
```

```
/* used to calculate the posterior mean of pi */\nstart posttox(alpha) global (j,DLT,doselevel,cohortsize);
post-pi=j##exp(alpha)posterior(alpha);
return(post);
finish;
```

```
call quad(marginal,"posterior",{.M P})eps=1E-4 peak=0.1;
pi={};
do j=1 to ndose
 call quad(j,"posttox",{.M P});
pij=pij/marginal;
pi=pi//pij;
end;
```

```
lb1=log(log(target)/log(p[1]));
call quad(postover,"posterior",-35|lb) eps=1E-4 peak=0.5;
postover=postover/marginal;
```

```
if postover>toxstop then stop=1;
```

```
diff=abs(pi-target)
dosebest=diff[:]<1;
dosenet=dosecurse;

if dosebest<dosecurse then
 if dosecurse<ndose then do
dosenet=dosecurse+1;
end;

if dosebest>1 then
 if dosecurse>1 then do
dosenet=dosecurse-1;
end;

if stop=1 then dosenet="The trial should be terminated early";\nprint dosenet;
doselevel=1::ndose;
doselevel-1=doselevel;
create doselevel from doselevel[colname="doselevel"];\nappend from dosenet;
```

```
create pi from pi[colname="pi"]
append from pi;
quit;
```