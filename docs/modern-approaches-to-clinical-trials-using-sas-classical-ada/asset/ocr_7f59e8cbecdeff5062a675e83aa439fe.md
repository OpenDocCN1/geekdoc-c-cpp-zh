```
eSize=abs(delta.)/((pc.*(1-pc)+ptrt.*(1-ptrt))/2)**0.5);
nFixedFixed=2*(ceil((prob(1-alpha)+prob(1-beta))*eSize)**2);
/* Total Sample Size at the Interim Analysis */
n1=ceil(nFixed);
n2=nFixed;
c_seed1=1736; t_seed2=6241;
c_seed2=7869;

doi=1 To &Samp
nn1=round((1-r.)*n1);
nn2=round(r.)*n1;
cont1=randbin(c_seed1,N11,cont.)/n11;
trt1=randbin(t_seed1,N12,trt.)/n12;
deltah1=trt1-cont1;
pbar1=(cont1*ntrl1+trt1*n12)/(n1 + n2);
se1=sqrt(pbar1*(1-pbar1)*(1/n1+1/n2));
z1=deltah1/se1;
improve=(trtr1-cont1)/cont1*100;
reject=0=stop;fstop=power=0;
if z1 > cl. then do
reject=1;
ESTOP=1;
pfinal=n1;
end;
if z1 < &bl1. then do
reject=0;
FSTOP=1;
pfinal=n1;
end;
if &bl1.<= z1 < &cl. then do
eRatio=abs(delta/(abs(deltah1)+0.0000001));
n_adj=(eRatio**2)*fixed;
finalMin=Min(nMax, Max(nfixed, n_adj));
finalMin=Min(nMax, Max(nfixed, n_adj));
end;
w1=sqrt(n1/(n1+n2));
nw2=sqrt(n2/(n1+n2));

***** Simulate Data for Stage II ******/
cont2=;
trt2=;
z2=;
zchw=z1;
if final > n1 then do
n21=round((1-r.)*(final-n1);
n22=round(r.)*(final-n1);
n=n21+n22;
cont2=randbin(c_seed1,N21,cont.)/n21;
trt2=randbin(t_seed1,N22,trt.)/n22;
deltah2=trt2-cont2;
pbar2=(cont2*ntrl1+trt2*n22)/(n21 + n2);
se2=sqrt(pbar2*(1-pbar2)*(1/n21+1/n2));
z2=deltah2/se2;
zCHW=w1*Z1*Z2;
end;
if ZCH > &2. then reject=1;
elelse reject=reject;
output=;
end;
run;

title="&title1"
proc means data=SSR_EFF;
var reject nfinal estop fstop;
run;
%end SSR_EFF;
```