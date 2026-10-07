
下面的程序提供了通过似然比检验检验平行性假设（parallelism assumption）的语句。似然比检验是根据方程 (7.35) 中无限制模型的对数似然函数与方程 (7.34) 中比例优势模型（Proportional-odds Model）的对数似然函数构建的。程序中获得了“缩减模型”（比例优势模型）的拟合。

# 程序 7.5：使用似然比检验检验平行性假设（续）

```sas
ods html;
title "Proportional-Odds Model -- Dirichlet-multinomial Distribution";
ods output FitStatistics;Fit_DM;
Proc nlmixed birth_defects;
params a1=3.7,a2=-2.4,b1=-0.2,b2=3.1,b3=5.5,b4=-1.8,b5=-1.7,rhoc=0.5;
bounds 1-rho=0;
etal=a1+b1*zn2+b2*cd2+b3*cd3+b4*zn2+b5*zn2;
eta2=a2+b1*zn2+b2*cd2+b3*cd3+b4*zn2+b5*zn2;
gamma1=1/(1+exp(-etal));
gamma2=1/(1+exp(-eta2));
p1=gamma1;
p2=gamma2-gamma1;
p3=1-p1-p2;
t=t1+t2+t3;
c=(1-rhoc)*rho;
const=ligma(m+1)-ligma(t1)-ligma(t2+1)-ligma(t3+1);
loglik=ligma((p1+(rhoc)*rho1)*(t1+(rhoc)*rho2)*(t2+(rhoc)*rho3)*(rhoc**t3))
+ (p2+(rhoc)*rho1)*(t1+(rhoc)*rho2)*(t2+(rhoc)*rho3)*(rhoc**t3))
+ (p3+(rhoc)*rho1)*(t1+(rhoc)*rho2)*(t2+(rhoc)*rho3)*(rhoc**t3))
+const;
model t1=general(loglik);
```

```sas
Title "Proportional-Odds Model -- Dirichlet Multinomial Distribution";
ods output FitStatistics;Fit_ROM_Reduced_DM_Dimensions=0;
Proc nlmixed birth_defects;
params a1=3.7,a2=-2.4,b1=-0.2,b2=3.1,b3=5.5,b4=-1.8,b5=-1.7;
bounds 1-rho=0;
etal=a1+b1*zn2+b2*cd2+b3*cd3+b4*zn2+b5*zn2;
eta2=a2+b1*zn2+b2*cd2+b3*cd3+b4*zn2+b5*zn2;
gamma1=1/(1+exp(-etal));
gamma2=1/(1+exp(-eta2));
p1=gamma1;
p2=gamma2-gamma1;
p3=1-p1-p2;
t=t1+t2+t3;
oc=1-rhoc;
const=ligma(m+1)-ligma(t1)-ligma(t2+1)-ligma(t3+1);
loglik=ligma((p1+(rhoc)*rho1)*(t1+(rhoc)*rho2)*(t2+(rhoc)*rho3)*(rhoc**t3))
+ (p2+(rhoc)*rho1)*(t1+(rhoc)*rho2)*(t2+(rhoc)*rho3)*(rhoc**t3))
+ (p3+(rhoc)*rho1)*(t1+(rhoc)*rho2)*(t2+(rhoc)*rho3)*(rhoc**t3))
+const;
model t1=general(loglik);
```

```sas
data Fit_reduced;
  set Fit_DM;
  if n=1;
  rename Value=0;
  descr="LR Test -- DM Distribution";
run;
```

```sas
data DM_full;
    set Fit_DM_full;
    if _n_ = 1;
    rename Value=Value_1;
    keep Value;
run;
data Fit_DM;
    merge Fit_reduced DM_full;
run;
data Fit_RCM_reduced;
    set Fit_RCM_reduced;
    if _n_ = 1;
    rename Value=Value_0;
    descr = "LR Test -- RCM Distribution";
run;
data Fit_RCM_full;
    set Fit_RCM_full;
    if _n_ = 1;
    rename Value=Value_1;
    keep Value;
run;
data Fit_RCM;
    merge Fit_RCM_reduced Fit_RCM_full;
run;
data dimensions_1;
    set Fit_DM;
    if _n_ = 4 then callput('nparms_1=',trim(Value));
run;
data dimensions_0;
    set Fit_DM;
    if _n_ = 4 then callput('nparms_0=',trim(Value));
run;
data LR_Tests;
    set Fit_RCM;
    format Chi_square_Stat Chi_square_Stat;
    output;
run;
```
