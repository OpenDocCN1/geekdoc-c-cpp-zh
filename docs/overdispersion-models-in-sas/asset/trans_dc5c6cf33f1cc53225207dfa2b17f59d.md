

## 程序 10.4：Beta-二项分布 GLOMM 的生成与分析

```
/*
Beta-binomial分布 GLOMM

带有 Logit 链接和随机效应的 Beta-二项模型
由于交叉设计产生的随机效应

t given u ~ Beta-binomial(pi,rho,n)
logit(pi) ~ beta0 + betal * X + u
u ~ Normal(0,sigma=sigma)
*/
data GLOMM, bn;
n = 200;
pi_1 = 0.12;
pi_2 = 0.08;
m = 20;
rho_2 = 0.15;
sigma = 1.2;
seed = 1983;
beta0 = log(pi_1/(1-pi_1));
betal = log(pi_2/(1-pi_2)) - beta0;
c = 1 / rho_2 / rho_2 - 1;

--- 过离散参数;
----------------------
--- u ~ Normal(0,sigma=sigma);
----------------------
--- 种子;
----------------------
--- 序列 AB;
n----------------------
do Subj_id=1 to n;
----------------------
Sequence = 'AB';
u = sigma * normal(seed);
--- 第1期;-
Period = 1;
Product = 1;
X = 1 / (1 + exp(- beta0 - u));
pi = c * pi;
a = c - a;
y1 = rangam(seed, a);
y2 = rangam(seed, b);
y = y1 / (y1 + y2);
t = ranbin(seed,m,p);
output:
--- 第2期;-
Period = 2;
Product = 0;
X = 1 / (1 + exp(- beta0 - betal - u));
pi = c * pi;
a = c - a;
y1 = rangam(seed, a);
y2 = rangam(seed, b);
y = y1 / (y1 + y2);
t = ranbin(seed,m,p);
output:
---*-
end;
----------------------
--- 序列 BA;
----------------------
do Subj_id=n+1 to n+n;
----------------------
Sequence = 'BA';
u = sigma * normal(seed);
-- 第1期;
Period = 1;
Product = 0;
pi = 1 / ( 1 + exp( beta0 - betal - u ) );
c = c * pi;
b = c - a;
y1 = rangam(seed, a);
y2 = rangam(seed, b);
p = y1 / ( y1 + y2);
t = ranbin(seed,m,p);
output:
-- 第2期;
Period = 2;
Product = 1;
pi = 1 / ( 1 + exp( beta0 - u ) );
c = c - a;
b = 
y1 = rangam(seed, a);
y2 = rangam(seed, b);
p = y1 / ( y1 + y2);
t = ranbin(seed,m,p);
output:
--;
end;
--;
```

run; Subj_id Sequence Product X t m

```
ods html;
proc glimmix data=glm_BB method=quad;
class Subj_id Sequence Product;
model t/m = Product / link=logit dist=binomial s;
random int = subject+subj_id;
run;
proc nlmed data=glm_BB;
parms beta0=-2.7, -2.6, -2.5, betal=0.4, 0.5, 0.3 a0=-0.5 0, sigma=1;
linr = a0;
rho_2 = 1/(1+exp(-linr));
c = 1 / rho_2 - 1;
linp = beta0+betal*x + u;
pi = 1/(1+exp(-linp));
c = 1*pi;
z = gamma(m+1) - gamma(t+1) + gamma(t*c*pi) + gamma(m-t*c*pi) - ngamma(m*c) - gamma(c*c*pi) - gamma(c*pi);
model t = general(1);
random u = normal(0, sigma*sigma) subject=Subj_id;
estimate 'Pi_1' = 1/(1+exp(-beta0-betal));
estimate 'Pi_2' = 1/(1+exp(-beta0));
estimate 'var' = exp(betal);
estimate 'Sigma*Sigma' = Sigma*Sigma;
estimate 'Rho*' = 1/(1+exp(-a0));
run;
```

Morel, Jorge and Nagaraj Neeraj. Overdispersion Models in SAS. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多资源请访问 support.sas.com/publishing。

## 输出 10.4：程序 104 Beta-二项分布 GLOMM 分析的选定结果

| 协方差参数 |  | 估计 | 标准误 |
|---|---|---|---|
| 截距 | Subj_id | 1.6131 | 0.1576 |

| 效应 | 估计 | 标准误 | DF | t 值 | Pr >t |
|---|---|---|---|---|---|
| 截距 | -2.6056 | 0.0796 | 399 | -32.70 | <0001 | |
| Product 1 | 0.4801 | 0.0510 | 399 | 9.41 | <0001 | |
| Product 2 | 0 | | | | | |

| -2 对数似然 | 3229.6 | | | | | |
| AIC (越小越好) | 3237.6 | | | | | |
| AICC (越小越好) | 3237.6 | | | | | |
| BIC (越小越好) | 3253.6 | | | | | |

| 参数 | 估计 | 标准误 | DF | t 值 | Pr >t | Alpha | 下限 | 上限 |
|---|---|---|---|---|---|---|---|---|
| beta0 | -2.5563 | 0.08290 | 399 | -30.84 | <0001 | 0.05 | -2.7193 | -2.3933 |
| beta1 | 0.4740 | 0.06018 | 399 | 7.88 | <0001 | 0.05 | 0.3557 | 0.5924 |
| a0 | -1.7578 | 0.14633 | 399 | -12.02 | <0001 | 0.05 | -2.0454 | -1.4702 |
| sigma | 1.2131 | 0.06537 | 399 | 18.56 | <0001 | 0.05 | 1.0845 | 1.3416 |

| 标签 | 估计 | 标准误 | DF | t 值 | Pr >t | Alpha | 下限 | 上限 |
|---|---|---|---|---|---|---|---|---|
| PI_1 | 0.1108 | 0.007683 | 399 | 14.43 | <0001 | 0.05 | 0.09573 | 0.1259 |
| PI_2 | 0.0720 | 0.005539 | 399 | 13.00 | <0001 | 0.05 | 0.06111 | 0.08289 |
| OR | 1.6065 | 0.09668 | 399 | 16.62 | <0001 | 0.05 | 1.4164 | 1.7966 |
| Rho*Rho | 0.1471 | 0.01835 | 399 | 8.01 | <0001 | 0.05 | 0.1110 | 0.1831 |
| Sigma*Sigma | 1.4715 | 0.01586 | 399 | 9.28 | <0001 | 0.05 | 1.1597 | 1.7883 |

表 10.5 显示了从 NLMIXED 程序获得的 Beta-二项分布 GLOMM 方程 10.5 的估计和标准误。读者可以验证参数估计（“-2 对数似然”）非常接近底层参数。

#### 表 10:5：Beta-二项分布 GLOMM 的参数估计和标准误

| 参数 | 估计 | 标准误 |
|---|---|---|
| -2 对数似然 | 3229.6 | -- |
| $\pi_1$ | 0.1108 | 0.0077 |
| $\pi_2$ | 0.0720 | 0.0055 |
| 优势比 (Odds-ratio) | 1.6065 | 0.0967 |
| $\rho^2$ | 0.1471 | 0.0184 |
| $\sigma^2$ | 1.4715 | 0.1586 |

现在我们来处理随机 GLOMM：

```
$t_{ij} \text{ given } (x_{ij}; u_{ij}) \sim \text{Random-ed Binomial}(\pi_i; \rho; m_{ij}),\log (\pi_{ij}) = \beta_0 + \beta_1,x_{ij} + u_{ij}$ (10.16)
```

使用了之前 GLOMM 中的参数：$\pi_i = 0.12$, $\pi_2 = 0.08$, $\rho^2 = 0.15$, $\sigma = 1.2$ 以及 $m_{ij} = 20$。分析数据的编程语句位于程序 10.5。之前，我们使用将受试视为随机的 GLMIX 获取 beta 参数和方差分量的初始估计。然后通过由初始值定义的 NLMIXED 程序拟合随机 GLOMM。程序 10.5 的选定结果显示在输出 10.4。

## 程序 10.5：Beta-二项分布 GLOMM 下的数据生成与分析

```
/*
带有 Logit 链接和随机效应的 Beta-二项模型
由于交叉设计产生的随机效应

t given u ~ Beta-binomial(pi,rho,n)
logit(pi) ~ beta0 + betal * X + u
u ~ Normal(0,sigma=sigma)
*/
data GLOMM
n = 200;
pi_1 = 0.12;
pi_2 = 0.08;
rho_2 = 0.15; --- 过离散参数;
sigma = 1.2; --- 种子;
seed = 1983;
beta0 = log(pi_1/(1-pi_1));
betal = log(pi_2/(1-pi_2)) - beta0;
rho = sqrt(rho_2);
--- 序列 AB;
do Subj_id=1 to n;
Sequence = 'AB';
u = sigma * normal(seed);
--- 第1期;-
Period = 1;
Product = 1;
X = 1;
pi = 1 / (1 + exp(- beta0 - u));
yy = ranbin(seed,1,pi);
mm = ranbin(seed,m,rho);
t = yy * mm;
if m > mm then t = t + ranbin(seed,m,pi);
output;
--- 第2期;
Period = 2;
Product = 2;
X = 0;
pi = 1 / (1 + exp(- betal - u));
yy = ranbin(seed,1,pi);
mm = ranbin(seed,m,rho);
t = yy * mm;
if m > mm then t = t + ranbin(seed,m,pi);
output;
---
end;
--- 序列 BA;
do Subj_id=n+1 to n+n;
Sequence = 'BA';
u = sigma * normal(seed);
--- 第1期;-
Period = 1;
Product = 0;
pi = 1 / ( 1 + exp( beta0 - betal - u ) );
c = c * pi;
b = c - a;
y1 = rangam(seed, a);
y2 = rangam(seed, b);
p = y1 / ( y1 + y2);
t = ranbin(seed,m,p);
output:
-- 第2期;
Period = 2;
Product = 1;
pi = 1 / ( 1 + exp( beta0 - u ) );
c = c - a;
b = 
y1 = rangam(seed, a);
y2 = rangam(seed, b);
p = y1 / ( y1 + y2);
t = ranbin(seed,m,p);
output:
--;
end;
--;
```

