

## 第 10 章 广义线性过离散混合模型 369

| AIC (越小越好) | 18974 |
| AICC (越小越好) | 18974 |
| BIC (越小越好) | 18990 |

| 参数 | 估计值 | 标准误 | DF | t 值 | Pr > |t| | Alpha | 下限 | 上限 | 梯度 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| b0 | 0.7988 | 0.07797 | 399 | 10.25 | <0001 | 0.05 | 0.6455 | 0.9521 | 0.000269 |
| b1 | 0.3090 | 0.1092 | 399 | 3.58 | 0.0004 | 0.05 | 0.1761 | 0.6057 | 0.000567 |
| w | 0.1984 | 0.007531 | 399 | 26.35 | <0001 | 0.05 | 0.1836 | 0.2132 | 0.00056 |
| sigma | 1.0594 | 0.04170 | 399 | 25.41 | <0001 | 0.05 | 0.9774 | 1.1414 | 0.000215 |

| 标签 | 估计值 | 标准误 | DF | t 值 | Pr > |t| | Alpha | 下限 | 上限 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 组 1 期望计数 | 2.6340 | 0.2032 | 399 | 12.96 | <0001 | 0.05 | 2.2346 | 3.0335 |
| 组 0 期望计数 | 1.7818 | 0.1389 | 399 | 12.83 | <0001 | 0.05 | 1.5088 | 2.0548 |
| 组 1 对组 0 期望计数之比 | 1.4783 | 0.1615 | 399 | 9.15 | <0001 | 0.05 | 1.1608 | 1.7958 |
| Sigma**2 | 1.1223 | 0.08835 | 399 | 12.70 | <0001 | 0.05 | 0.9486 | 1.2960 |

我们考虑 ZINB GLOMM

```sas
$y_{ij} \text{ given } (x_{ij}; u_{ij}) \sim \text{Zero-inflated Negative-binomial}(\lambda_{ij}, \kappa, \omega),$
\log(\lambda_{ij}) = \beta_0 + \beta_1 x_{ij} + u_{ij}$
```

其中 $\kappa$ 是过离散参数，$\omega$ 是相对于负二项分布的额外零值比例，$u_{ij}$ 是独立同分布的正态分布 $(0, \sigma^2)$，且

```sas
$x_{ij} = \begin{cases} 1 & \text{如果受试者在组 1 中} \\ 0 & \text{否则。}\end{cases}$
```

与 ZIP GLOMM 一样，我们假设 n=200, m=12, $\beta_0=0.70, \beta_1=0.40, \omega=0.20$ 且 $\sigma^2=1.20$。额外的过离散参数假设为 $\kappa=0.15$。与之前，第一组的期望计数为 $(1-\omega)e^{\beta_0+\beta_1}=0.80(e^{1.10})\approx2.4033$。
第二组的期望计数为 $(1-\omega)e^{\beta_0}=0.80(e^{0.70})\approx1.6110$。因此，期望计数的比值如下

##  程序 10.7: 零膨胀负二项分布 GLOMM

```sas
/*
在零膨胀负二项分布 GLOMM 下生成数据，
参数为 Beta0, Betal, Kappa, W, 和 Sigma**2
*/
data zbind_glomm;
    beta0 = 0.70;
    betal = 0.40;
    kappa = 0.15;
    w = 0.20;
    sigma2 = 1.2;
    m = 12;
    n = 200;
    seed = 1917;
    nl = n+1;
    n2 = n+n;
    alpha = 1 / kappa;
    sigma = sqrt(sigma2);
    do i=1 to n;
        u = uniform(seed);
        if u > w then do;
            Group = 1;
            mu = exp(Beta0+Betal+u); /* 注意：原始 OCR 可能将 'u' 误写为 'z' */
            kappa = kappa * mu;
            beta = rang(seed,alpha);
            Y = ranpoi(seed,u);
            output;
        end else do;
            Group = 2;
            Y = 0;
            output;
        end;
    end;
    do i=n+1 to n2;
        z = Sigma*(seed);
        do t=1 to m;
            u = uniform(seed);
            if u > w then do;
                Group = 0;
                mu = exp(Beta0 +z);
                kappa = kappa * mu;
                beta = rang(seed, alpha);
                Y = ranpoi(seed, u);
                output;
            end else do;
                Group = 1;
                Y = 0;
                output;
            end;
        end;
    end;
    keep t group y;
run;
```

```sas
ods html;
title "Beta0, Kappa 和 Sigma**2 的零膨胀估计值";
proc glimm data=zib_glomm method=quad;
  class id group;
  model y = group / link=log dist=negbin;
  random / subject=id;
run;

proc nlixed data=zib_glomm;
  parms b0=0.49 b1=0.3 kappa=0.8 w=0.1 0.2 sigma=1.13;
  bounds kappa > 0 and kappa < 1;
  mu = exp(b0+b1*group);
  a = 1/kappa;
  p = lgamma(kappa*a);
  z = lgamma(y+a) - lgamma(y+1);
  if y<=0 then
    ll = log((1-w)*p);
  else ll = log(w) + a * log(p) + y * log(1-p);
  model y = ll;
  random u-normal(0,sigma) subject=id;
  estimate "Expected Counts Group 1" (1-w)*exp(b0+b1);
  estimate "Expected Counts Group 0" (1-w)*exp(b0);
  estimate "Ratio Expected Counts Group 1 Va 0" exp(b1);
  estimate "Sigma*2" sigma*sigma;
run;
ods close;
```

## 372 SAS 中的过离散模型

输出 10.7: 程序 10.7 节选——一个零膨胀负二项分布 GLOMM。使用 PROC GLIMMIX 对 Beta0, Beta1, Kappa 和 Sigma**2 进行初始估计

| GLIMMIX 过程 | | |
| :--- | :--- |
| |方差参数估计值 | | |
| 协方差参数 | 受试者 | 估计值 | 标准误 |
| :--- | :--- | :--- | :--- |
| 截距 | id | 1.2735 | 0.1033 |
| 尺度 | | 0.7787 | 0.0330 |
| 固定效应解 | | | |
| 效应 | 估计值 | 标准误 | DF | t 值 | Pr > |t| |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 截距 | 0.4904 | 0.0845 | 398 | 5.80 | <0001 |
| 组 | 0.3525 | 0.1189 | 399 | 2.97 | 0.033 |
| 组 | 0 | | | | |
| NLMIXED 过程 | | |
| 参数 | 估计值 | 标准误 | DF | t 值 | Pr > |t| | Alpha | 上限 | 梯度 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| b0 | 0.7072 | 0.0096 | 399 | 13.19 | <0001 | 0.05 | 0.6486 | 0.7941 |
| b1 | 0.3513 | 0.1189 | 399 | 2.96 | 0.0033 | 0.05 | 0.1176 | 0.5850 |
| kappa | 0.1269 | 0.00924 | 399 | 13.77 | <0001 | 0.05 | 0.1080 | 0.1458 |
| w | 0.2061 | 0.00832 | 399 | 24.77 | <0001 | 0.05 | 0.1898 | 0.2325 |
| sigma | 1.0594 | 0.04170 | 399 | 25.41 | <0001 | 0.05 | 0.9774 | 1.1414 | 0.000215 |

## 第 10 章 广义线性过离散混合模型 373

| 额外估计 | | | | |
| 标签 | 估计值 | 标准误 | DF | t 值 | Pr > |t| | Alpha | 下限 | 上限 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 组 1 期望计数 | 2.2881 | 0.2020 | 399 | 11.92 | <0001 | 0.05 | 1.9106 | 2.6656 |
| 组 0 期望计数 | 1.6103 | 0.1364 | 399 | 11.81 | <0001 | 0.05 | 1.3421 | 1.8781 |
| 组 1 对组 0 期望计数之比 | 1.4209 | 0.1689 | 399 | 8.41 | <0001 | 0.05 | 1.0889 | 1.7530 |
| Sigma**2 | 1.3144 | 0.1035 | 399 | 12.70 | <0001 | 0.05 | 1.1109 | 1.5179 |

表 10.7 汇总了 NLMIXED 过程报告的两种 GLOMM 主要结果。

10.7 结语

在本章中，我们介绍了关于广义线性混合模型 (GLMM)的一些基本概念。我们强调了被称为极大似然的估计方法，该方法基于自适应高斯-赫特积分，是本章所有示例使用的估计方法。这是 GLIMMIX 过程使用的方法之一。另一种方法，基于线化的伪似然方法已在第 9 章中讨论。第 10.2 节的多个中心随机试验和第 10.3 节的压水反应堆核电泵可靠性示例用于说明二项分布和泊松分布 GLMM 的拟合。第三个示例第 9.9 节讨论的肩部研究在 GLMM 的背景下被重新讨论。GLMM 的基本概念可以扩展到更广泛的模型族，即广义线性过离散混合模型 (GLOMM) 族；这一特定特征是

