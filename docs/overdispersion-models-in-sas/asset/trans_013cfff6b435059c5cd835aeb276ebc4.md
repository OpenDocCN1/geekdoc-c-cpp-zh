

# SAS 中的 150 种过度离散模型

```sas
pt = (pi*pr1+pic*pr2);
end;
else do
  pr1_l = PROBBNML(p1,m[j],t[j]-1);
  pr2_l = PROBBNML(p2,m[j],t[j]-1);
  pt = (pi*(pr1 - pr1_l)+pic*(pr2 - pr2_l));
end;
if pt < 1e-10 then pt = 1e-10;
logcb = logcb + log(pt);
************************************************************************************
* 在新 beta 估计下计算 logcb 的结束;
************************************************************************************
if (logcb > old_old | split > 5) then stop2=1;
split = split+1;
************************************************************************************
* stop2 while 循环结束;
************************************************************************************
  if split>6 then else beta = betan;
  criteria = abs(logcb - old_old)/abs(old_old + eps1);
  if (criteria < eps2 | iterate > 20) then stop1=1;
  iterate = iterate + 1;
************************************************************************************
* stop1 while 循环结束;
************************************************************************************
```

```sas
pi = beta[1];
rho = beta[2];
pl = 1-prpl;
rhoc = 1-rho;
p2 = rhoc*pi;
p1 = p2*rho;
if pl >= 1 then pl = 0.99;
plc = 1-pl;
p2c = 1-p2;
c1 = pi/plc;
c2 = pic/pi;
c3 = pi/pl;
c4 = plc/p2c;
```

> *************************************************************************************
* RCB 分布下 Fisher 信息的最终计算;
************************************************************************************

```sas
FIMCRB = j(2,2,0);
run FISHERCB;
INVERCB = inv(FIMCRB);
se_pi = sqrt(INVERCB[1,1]);
se_rho = sqrt(INVERCB[2,2]);

nest = j(2,5,0);
est[1,1:2] = round(pi, 0.00001)//round(se_pi, 0.00001);
nest[2,1:2] = round(rho, 0.00001)//round(se_rho, 0.00001);
nest[3,1:2] = round(est[1]/est[2], 0.00001);
nest[1,4] = n-2;
nest[2,4] = n-2;
est[5] = 2*-1PROBT(est[3],est[4]);
if est[5] < 0.0001 then est[5] = 0.00001;
```

More, Jorge, and Nagaraj Neerajal. Overdispersion Models in SAS. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL rights reserved. For additional resources, visit.sas.com/publishing.

# 第 5 章 过度离散二项分布模型的拟合度检验 151

```sas
vvv = 2;
fitStat[1,1] = -2*logrlik;
fitStat[2,1] = fitStat[1,1] + 2*vvv;               --- AIC;
fitStat[3,1] = fitStat[1,1] + 2*vvv*n / (n-vvv-1);   --- AICC;
fitStat[4,1] = fitStat[1,1] + vvv*log(n);             --- BIC
```

********************************************************************************
从 RCB 计算期望频率并检查频率 = 5;
并此确定 r;
********************************************************************************

```sas
k = max(mj) + 1;
pic = 1-pi;
rho = 1-rho;
p2 = rho*pi;
pl = p2 + rho*p1;
if pl >= 1 then pl = 0.99;

*   初始化;
lowerb = j(k,1,-0.000001);
upper = j(k,1,0.000001);
P = j(k,1,0);

*   定义区间的下限和上限;
do s = 2 to k;
lowerb[s] = (s-1)/k;
upper[s] = (s-1)/k;
end;

*   计算随机聚类二项分布下的期望计数;
do s = 1 to k;
```
