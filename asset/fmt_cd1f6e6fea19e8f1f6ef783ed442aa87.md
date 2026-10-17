
```
$a_{2,T} = \int_0^T e^{t} \rho_{\sigma}v_{0,j} \left(\int_0^t \rho_{\sigma} \left(e^{-u} du\right)\right) ds, \quad (9.52)$
```

```
$b_{0,T} = \int_0^T e^{2t}\sigma_s^2v_{0,j} \left(\int_0^t e^{-k_s} \left(e^{-u} du\right)\right) ds, \quad (9.53)$
```

```
$b_{2,T} = \frac{a_{1,T}^2}{2}. \quad (9.54)$
```

注意所有参数 `$\theta$`、`$\sigma$` 和 `$\rho$` 允许变化；`$\kappa$` 假设为常数，而 `$v_0$` 是一个未观测的状态变量。

### 常数参数

如果假设参数为常数，则 `$\theta=\theta$`，`$\sigma=\sigma$` 且 `$\rho=\rho$`。将这些参数移出积分之外并计算 `(9.51)` 到 `(9.53)` 中的积分，得到以下表达式，它们出现在 Benhamou 等人 (2010) 的命题 2.4 中：

```
$a_{1,T} = \frac{\rho\sigma e^{-\kappa T}}{\kappa^2} [V_0 (\kappa T + e^{\kappa T} - 1) + (\kappa T + e^{\kappa T})(\kappa T - 2)]\
a_{2,T} = \frac{\rho^2\sigma e^{-\kappa T}}{\kappa^3} V_0 (-4\kappa T e^{\kappa T} + 2e^{\kappa T} - 2)\
b_{0,T} = \frac{\sigma^2 e^{-\kappa T}}{4\kappa^3} [V_0 (-4\kappa T e^{\kappa T} + 2e^{\kappa T} - 2) + \theta (2e^{\kappa T}(\kappa T - 3) + \kappa T (\kappa T + 4)))\
b_{2,T} = \frac{a_{1,T}^2}{2}. \quad (9.55)$
```

注意在常数参数下我们有：

```
$v_{0,T} = \theta + (\theta - v_0)e^{-\kappa T}, \quad \hat{w}_T = (v_0 - \theta) \frac{1 - e^{-\kappa T}}{\kappa} + \theta T. \quad (9.56)$
```

使得 `$\hat{w}_T$` 简化为第 2 章中遇到的形式。为了获得认权价格，将方程 `(9.55)` 中的系数代入 `(9.48)`，并使用本章末尾出的 Black-Scholes 衍生品。看权价格通过看跌期权平价获得。

正如 Benhamou 等人 (2010) 所述，常数参数下的价格展开等同于 Lewis (2000) 在第 4 章中涵盖的波动率展开。事实上，很容易验证：

# MATLAB 和 C# 中的 Heston 模型及其扩展

`$a_{1,T}=\sigma_1^2(v, T), a_{2,T}=\sigma_2^2(v, T),$` 且 `$b_{0,T}=\sigma^2J_1(v, T)$`，并产生了相同的价格。

Matlab 函数 `BGMAproxPrice.m` 实现了假设常数参数的 Heston 认权 `(94)` 近似。为了节省空间，省略了函数的某些内容。该函数还通过看跌期权平价返回看权价格。

```matlab
function y = BGMAproxPrice(params,S,K,rf,q,T,trap,PutCall)
y = y^(1/2) - (-x + log(K)) (-rf*q*T) - (1/2)*sqrt(y);
f = y^(1/2) - (-x + log(K)) (-rf*T) + (1/2)*sqrt(y);
BSPut = K*exp(-rf*T)*normcdf(f) - S*exp(-q*T)*normcdf(d);
a1T = (sigma*sqrt(kt*T)/2)^2 - (v*(-kt+kET-1)); ...
a2T = (sigma*sqrt(kt*T)/2)^2 - (v*(-kt*(kT+2)+2*kET)); ...
b2T = (sigma^2*(-2kt+4/3)) - (v*(-4kt+kKT+)); ...
dpdxy = K*exp(-rf*T)*Phixfy - exp(-q*T)*S;
dpd2xy = K*exp(-rf*T)*Phify2 - exp(-q*T)*S;
dpdy2 = K*exp(-rf*T)*Phify2;
dpdy2y = K*exp(-rf*T)*Phify2 - exp(-q*T)*S;
Put = BSPut + a1T*dpdxy + a2T*dpdy2 + b0T*dpdy2;
if strcmp(PutCall,'1')
ny = Put;
else
ny = Put - K*exp(-rf*T) + S*exp(-q*T);
end
```

在常数参数下实现模型的 C# 代码非常相似，此处未给出。为了说明，我们在表 9.4 中重现了表 4 和表 3 中的看权价格和隐含波动率（`$\kappa=3, \sigma=0.3,$` 且 `$\rho=0$`）。为了节省空间，表 9.4 仅展示了 `$S=100, \theta=0.06$` 和平值（at-the-money）列。对于每一项，隐含波动率和看权价格都是使用带有 32 点 Gauss-Laguerre 积分的闭式 Heston 模型以及方程 `(9.48)` 中的近似得到的。表 9.4 中的数据与 Benhamou 等人 (2010) 从表 9.3 和 9.4 得到的相同。

# 分段常数参数

假设 `$0 < T_1 < T_2 < \dots < T_N < \infty$`。Benhamou 等人 (2010) 假设 `$\kappa$` 和 `$v_0$` 在 `[0, T_N]` 上常数，`$\theta, \sigma$` 和 `$\rho$` 在区间 `[T_i, T_{i+1}]` 上分别具有分段常数值 `$\theta_i, \sigma_i$` 和 `$\rho_i$`。他们通过分离 `(9.51)` 到 `(9.53)` 的区域，为价格系数 `$a_{1,T}, a_{2,T}$` 和 `$b_{0,T}$` 提供了递归表达式。注意表 3 和 4 中的价格是看权而非看跌。感谢 Emmanuel 指出。

# 与时间相关的 Heston 模型

表 9.4 ATM 看权价格和隐含波动率，闭式与近似

| 期限 | 闭式看权价格 | 近似看权价格 | 闭式隐含波动率 | 近似隐含波动率 |
| :--- | :--- | :--- | :--- | :--- |
| 3M | 4.23 | 4.22 | 0.19 | 0.19 |
| 6M | 6.20 | 9.11 | 0.99 | 0.98 |
| 1Y | 9.12 | 13.26 | 2.90 | 2.89 |
| 2Y | 13.26 | 16.39 | 3.61 | 3.61 |
| 3Y | 16.39 | 16.39 | 3.89 | 3.89 |
| 5Y | 21.26 | 21.26 | 4.12 | 4.12 |
| 7Y | 25.14 | 25.14 | 5.23 | 5.22 |
| 10Y | 29.92 | 29.92 | 0.30 | 0.30 |

`$(T_i, T_{i+1})$` 和 `$(T_j, T_{j+1})$`。因此，对于 `$a_{T_i,T_{i+1}}$`，根据 `(9.51)` 和 Benhamou 等人 (2010) 的命题 2.5：

```
$a_{T_i,T_{i+1}} = \int_{T_i}^{T_{i+1}} e^{t\rho\sigma_{v_{0,t}}} \left(\int_{T_i}^{t} e^{-u} du\right) dt + \int_{T_i}^{T_{i+1}} e^{t\rho\sigma_{v_{0,t}}} \left(\int_{t}^{T_{i+1}} e^{-u} du\right) dt. \quad (9.57)$
```

`(9.57)` 的第二行可以通过将内积分区域 `$(t, T_{i+1})$` 分为 `$(T_i, t)$` 和 `$(t, T_{i+1})$` 来分为两部分：

```
$\int_{T_i}^{t} e^{t\rho\sigma_{v_{0,t}}} \left(\int_{T_i}^{t} e^{-u} du\right) dt + \int_{t}^{T_{i+1}} e^{t\rho\sigma_{v_{0,t}}} \left(\int_{t}^{T_{i+1}} e^{-u} du\right) dt. \quad (9.58)$
```

`(9.58)` 中的第一项是 `$a_{T_i,T_{i+1}}$`。这意味着我们可以将 `$a_{T_i,T_{i+1}}$` 写为：

```
$a_{T_i,T_{i+1}} = a_{1,T} + \sum_{j=T_i}^{T_{i+1}} \rho_j \sigma_j v_{0,j} \left(\int_{T_j}^t e^{-u} du\right) dt. \quad (9.59)$
```

由于参数在 `$(T_i, T_{i+1})$` 上是分段常数的，我们需要划分区域 `$(T_i, T_{i+1})$`。因此 `(9.59)` 变为：

```
$a_{T_i,T_{i+1}} = a_{1,T} + \sum_{j=T_i}^{T_{i+1}} \rho_j \sigma_j v_{0,j} \left(\int_{T_j}^t e^{-u} du\right) dt. \quad (9.60)$
```

由于参数在 `$(T_i, T_{i+1})$` 上是分段常数的，我们需要划分区域 `$(T_i, T_{i+1})$`。因此 `(9.60)` 变为：

```
$a_{T_i,T_{i+1}} = a_{1,T} + \sum_{j=T_i}^{T_{i+1}} \rho_j \sigma_j v_{0,j} \left(\int_{T_j}^t e^{-u} du\right) dt. \quad (9.61)$
```

由于参数在 `$(T_i, T_{i+1})$` 上是分段常数的，我们需要划分区域 `$(T_i, T_{i+1})$`。因此 `(9.61)` 变为：

```
$a_{T_i,T_{i+1}} = a_{1,T} + \sum_{j=T_i}^{T_{i+1}} \rho_j \sigma_j v_{0,j} \left(\int_{T_j}^t e^{-u} du\right) dt. \quad (9.62)$
```

## 时间依赖型 Heston 模型

```matlab
% Coefficients for a2T(T+1)
% 第一个求和中的第一个元素
f10 = int(exp(-kappa*t)*v0)
* int(exp(-kappa*u),u,s,Ti1,s,Ti1,t,0,Tj);
% 第一个求和中的剩余元素
f11 = int(exp(-kappa*t)*v0)
* int(exp(-kappa*u),u,s,Ti1,s,Ti1,t,Tmj,Tj);
% 第二求和中的第一个元素
f20 = int(exp(kappa*t)*v0)
% 第二求和中的剩余元素
f21 = int(exp(kappa*t)*v0)
* int(exp(-kappa*u),u,Ti,Tj,s,Tj,t,Tmj,Tj);
% 最后一项
f3 = int(exp(kappa*t)*v0)
* int(exp(-kappa*u),u,Ti,Tj,s,Tj,t,Tj);
```

代码运行后，必须使用文字处理器的查找和替换功能将符号项在适用的情况下转换为 Matlab 数组。例如，`$T_j$` 必须更改为 `$T(j)$`，`$T_{i1}$` 更改为 `$T(i+1)$`。获取剩余系数的代码也类似。

为了计算分段参数下的看跌期价格，我们首先使用方程 `(9.55)` 和参数 `$\kappa, v_0, \theta_i, \sigma_i, \rho_i$` 来计算 `$a_{1,T_i}, a_{2,T_i}, b_{0,T_i}$` 和 `$b_{2,T_i}$`。然后我们使用方程 `(9.60)` 和参数 `$\kappa, v_0, \theta_i, \sigma_i, \rho_i$` 计算 `$a_{1,T_{i+1}}, a_{2,T_{i+1}}, b_{0,T_{i+1}}$` 和 `$b_{2,T_{i+1}}$`，并继续应用方程 `(9.60)` 到 `(9.64)`，直到达到最后一个矩阵 `$T_N$`，并将 `$a_{1,T_N}, a_{2,T_N}, b_{0,T_N}$` 和 `$b_{2,T_N}$` 代入方程 `(9.48)` 以得到看跌期价格。

回想起参数 `$\kappa$` 和 `$\omega$` 对于所有矩阵都是固定的，但 `$\theta_i, \sigma_i$` 和 `$\rho$` 允许变化。因此，如果有 `$N$` 个矩阵，则有 `$2+3N$` 个参数。将这些参数堆叠在向量中是方便的。我们在前两个位置使用 `$\kappa$` 和 `$v_0$`，在剩余位置使用 `$\theta_i, \sigma_i$` 和 `$\rho_i$`（按此顺序）。例如，对于三个矩阵，该向量为：

`$$\kappa,v_0,\theta_1,\sigma_1,\rho_1,\theta_2,\sigma_2,\rho_2,\theta_3,\sigma_3,\rho_3$$`

在 Matlab 中实现定价时，将 `$a_{1,T_{i+1}}$` 和 `$b_{0,T_{i+1}}$` 表达式中的求和拆分为求和的第一项和剩余项是比较方便的。例如，方程 `(9.61)` 中的 `$a_{1,T_{i+1}}$` 写为：

`$$a_{1,T_{i+1}} = a_{1,T_i} + \rho_i \int_{T_i}^{T_{i+1}} e^{v_0\sigma_i t} (e^{-\sigma_i t}) dt + \sum_{j=2}^{i} \rho_j \sigma_j \int_{T_{j-1}}^{T_j} e^{v_0\sigma_j t} dt + \rho_{i+1} \int_{T_i}^{T_{i+1}} e^{v_0\sigma_{i+1} t} (e^{-\sigma_{i+1} t}) dt.$$`

`BGMAApproxTD` 函数计算分段到期日的近似看跌价值。我们通过方程 `(9.66)` 中的系数 `$a_{i,T}$` 代码来说明该函数。其他系数的代码与 `(9.65)` 指定的顺序相同，并计算对应于第一个时间步的系数的第一部分。该第一部分是使用 `(9.55)` 得到的。

```matlab
function y = BGMAApproxPriceTD(param,T,S,rf,q)
NT = length(T);
Nparam = 2 + 3*NT;
kappa = param(1);
v0 = param(2);
for i=1:3:Nparam
j = floor(i/3);
theta(j) = param(i);
sigma(j) = param(i+1);
rho(j) = param(i+2);
end
% 第一组系数
al1(1) = -rho(1)*sigma(1)*(2*theta(1)*exp(kappa*T(1))) + ...
a2T(1) = -1/2*rho(1)^2*sigma(1)^2*(kappa^2*v0*T(1)) + ...;
b0T(1) = -1/4*sigma(1)^2*(5+theta(1)*exp(kappa*T(1))) + ...;
b2T(1) = al1(1)^2;
```

第二部分计算系数的剩余部分。项 `$A_1$` 对应于 `(9.66)` 中的积分，顺序相同。

```matlab
% 剩余系数组
Al = 0;
if NT>=2
for t=1:NT-1
  % alT(T+1) 的系数
  for j=1
    Al = Al + rho(j)*sigma(j)*(-exp(-kappa*T(t))) + ...;
  for j=2:t
    Al = Al - rho(j)*sigma(j)*(-exp(-kappa*T(t))) + ...;
  for j=t+1
    Al = Al - rho(j)*sigma(j)*(-v0*exp(kappa*T(t))) + ...;
  alT(t+1) = alT(t) + Al;
end
```

第三也是最后一部分保留系数数组的最后一个元素，计算所需的导数，并计算 `(9.48)` 中的看跌期价格。该函数通过期权平价关系返回看涨期价格。

```matlab
% 展开式的系数是最后几个
A1T = a1(end);
A2T = a2T(end);
b0T = b0T(end);
b2T = b2T(end);
% 积分方差
W = (v0-theta(end))*(1-exp(-kappa*T(end)))/kappa + ...
% Black-Scholes 导数
ddx = K*exp(-rf*T(end));
ddy = K*exp(-rf*T(end));
dPdy2 = K*exp(-rf*T(end));
dPdx2 = K*exp(-rf*T(end));
% Benamou 展开
Put = A1T*ddx + A2T*ddy + B0T*dPdy2 + dPdx2;
```

C 代码类似且此处未给出。为了说明在 Benamou 等人 (2010) 模型中使用时间依赖参数进行定价，我们重现了表 8 中的平值价格（K=100）。这是通过以下代码实现的。

```matlab
% 构建随时间变化的参数
for i=1:40;
T(i) = i/4;
theta(i) = 0.04 + (i-1)*0.05;
sigma(i) = 0.30 + (i-1)*0.50;
rho(i) = -0.20 + (i-1)*0.35;
end
```

第二段代码构建 Benamou 等人 (2010) 的价格，在每一步将参数向量与分段参数拼接。
