
```matlab
function [CallFFT, lambda] = HestonCallFFreek(..., Greek)
  if fast
    % 实现 FFT 算法
    U = [0:N-1];
    J = [0:N-1];
    psi = HestonCFreeks(v-(alpha+1)).i;
    phi = exp(-r*tau).*psi ./ (alpha^2 + v.^2);
    x = exp(i*(b-s0).*phi;
    e = exp(-i*2*pi/N).*x;
    CallFFT = sta.*exp(-alpha./pi) * real(e);
```

`HestonCallFRGT.m` 用于实现分数希腊字母和 Carr and Madan (1999) 公式。它还使用了早些章节定义的 `CarrGreeks.m` 函数来比较这种方法获得的希腊字母的准确性。

```matlab
rule = 'S';
Greek = {'Price', 'Delta', 'Gamma', 'Rho', 'Vanna', 'Volga'};
% FFT 或 FRT
for j=1:8
  if strcmp(method,'FFT')
    [Greeks(:,j)] = HestonCallFRGT(...,j);
  else
    [Greeks(i,j)] = HestonCallGMT(...,j);
  end
% 闭式希腊字母和误差
GreeksCM = zeros(length(ATM), 8);
for k=1:8
  GreeksCM(k,j) = CarrGreeks(...,j);
end
for j=1:8
  error(j) = sum(GreeksCM(:) - Greeks(:,j));
```

使用 FFT 和 FRT 实现希腊字母的代码在此未给出。为了说明，我们使用现价 `$S_0=100$` 和 6 个月的期限运行 FRT。结果在表 11.4 中，包含了来自 Carr and Madan (1999) 公式的真实值误差。表格表明通过分数 FFT 获得的希腊字母是准确的。虽然 FFT 本身没有给出，但它们也非常准确。

### 使用模拟的美式希腊字母

记得第 8 章中使用了 Longstaff 和 Schwartz (2001) 的最小二乘蒙特卡洛 (LSM) 算法在 Heston 模型中为美式期权定价。

## 表 14 分数傅里叶变换的希腊字母

| 执行权 (Strike) | 价格 (Price) | Delta | Gamma | Rho | Vega | Vanna |

|---|---|---|---|---|---|---|---|

| 98.02 | 9.21 | 0.649 | 0.021 | -9.25 | 27.85 | 16.63 | -0.188 | 27.77 |

| 98.51 | 8.93 | 0.638 | 0.021 | -9.27 | 27.46 | 16.60 | -0.163 | 27.44 |

| 99.00 | 8.66 | 0.628 | 0.022 | -9.28 | 27.06 | 16.96 | -0.137 | 27.14 |

| 99.50 | 8.39 | 0.617 | 0.022 | -9.29 | 26.64 | 17.11 | -0.111 | 26.88 |

| 100.00 | 8.12 | 0.606 | 0.022 | -9.29 | 26.23 | 17.25 | -0.084 | 26.66 |

| 100.50 | 7.86 | 0.595 | 0.022 | -9.29 | 25.80 | 17.37 | -0.056 | 26.49 |

| 101.01 | 7.61 | 0.573 | 0.023 | -9.28 | 25.36 | 17.48 | -0.028 | 26.36 |

| 误差 (Error) | $4.5 \times 10^{-6}$ | $5.2 \times 10^{-6}$ | $5.2 \times 10^{-7}$ | $1.8 \times 10^{-4}$ | $4.5 \times 10^{-6}$ | $5.2 \times 10^{-6}$ | $1.8 \times 10^{-4}$ |

该算法可以修改以计算美式希腊字母。此外，为了确保希腊字母准确，我们必须存储生成股票价格和波动率路径的角随机变量值，并在对输入偏移值生成路径时应用相同的随机变量。这确保了原始路径与偏移路径之间的任何差异都是由偏移本身引起的，而不是模拟噪声。

修改第 7 章的函数以使用 LSM 算法获取美式希腊字母是简单的。第一个任务是在函数外部创建相关随机变量矩阵，并将这些矩阵作为函数参数。`MMSim.m` 函数是第 7 章中 Andersen 和 Brotherton-Ratcliffe (2005) 矩匹配模拟的简单修改版本。唯一的区别是相关随机变量 `$Z_s$` 和 `$Z_v$` 在函数外部，并作为参数传递给函数。

```matlab
function [S V] = MMSim(params,...,Zv, Zs)
% 生成股票和波动率路径
for i=1:N
  for t=2:T
      dw = sqrt(dt)*V(t,i);
      num = .5*sigma^2V(t-1,i)*(1-exp(-2*kappa*dt));
      den = (exp(-kappa*dt)*V(t-1,i) + (1-exp ...
% ... (code truncated in original)
      Gam = log(1 + num/den);
      V(t,i) = (exp(-kappa*dt)*V(t-1,i) + (1-exp ...
      % Euler/Milstein离散化对数股票价格
      S(t,i) = S(t-1,i)*exp((r-q-V(t-1,i)/2 + ...
  end
end
end
```

# 348 MATLAB 和 C# 中的 Heston 模型及其扩展

```matlab
function [Euro, Amer] = LSMGreeks(...,NT,NS,Zs,Greek)
ds = 0.01*S; //
dv = 0.01*V0;
if strcmp(Greek,'delta') % strcmp(Greek,'gamma')
  [Pathup V] = MMSGreeks(params,S+ds,...);
  [Pathsm V] = MMSGreeks(params,S-ds,...);
  [EuroPrice AmerPrice] = LSM(Pathsp',...);
  [EuroPriceAmerism] = LSM(Pathsm',...);
  if strcmp(Greek,'delta')
    Euro = (EuroPrice - EuroPrice) /2/ds;
    Amer = (AmerPrice - AmerPrice) /2/ds;
  else
    [Pathup V] = MMSGreeks(params,S,...);
    [EuroPrice AmerPrice] = LSM(Pathsp',...);
    Amer = (AmerPrice + AmerPrice) /ds^2;
    Euro = (EuroPrice - 2*AmerPrice + EuroPrice)/ds^2;
  end
if strcmp(Greek,'vega')
  paramsp = [kappa theta sigma v0+dv rho lambda];
  paramsp = [kappa theta sigma v0-dv rho lambda];
  [Pathup V] = MMSGreeks(paramsp,S,...);
  [Pathsm V] = MMSGreeks(paramsp,S,...);
  [EuroPrice AmerPrice] = LSM(Pathsp',...);
  [EuroPriceAmerism] = LSM(Pathsm',...);
  Euro = (EuroPrice - EuroPrice)/2/dv*sqrt(v0);
  Amer = (AmerPrice - AmerPrice)/2/dv*sqrt(v0);
end
```

`LSMGreeks.m` 函数用于以下代码，它仅生成 delta 和 gamma。

- * 相关 N(0,1) 随机变量矩阵

`Zv = randn(NT,NS);`

`Zs = rho*Zv + sqrt(1-rho^2).*randn(NT,NS);`

`[EuroDelta Amer] = LSMGreeks(...,,'delta');`

`[EuroGammaGamma] = LSMGreeks(...,,'gamma');`

使用 Longstaff 和 Schwartz (2001) 的 LSM 算法获取美式看跌期权 Greeks 的 C 代码非常相似，此处不再给出。区别在于我们需要为回归参数估计和生成随机数创建 C 函数。这些函数与第 8 章中的函数相同，它们在 LSM 算法中被用于生成美式期权的价格。

为了说明，我们使用 Clarke 和 Parrott (1999) 的设置对美式看跌期权运行 LSM 算法，并使用 Ikonen 和 Toivan (2008) 计算的价格，即 K=100, τ=0.25, r=0.1, κ=5, θ=0.16, ρ=0.9，现价从 8 到 12。我们使用 NT=1,000 个时间步和 NS=50,000 个股票价格步长。结果见表 11.5。

### Heston Greeks

**表 11.5** 美式看跌期权的价格和 Greeks，LSM 算法

| 现价 (Spot) | 价格 (Price) | Delta | Gamma | Theta | Rho | Vega1 | Vanna |

|---|---|---|---|---|---|---|---|

| 8 | 2.000 | -0.999 | 0.006 | 0.006 | 0.005 | -0.005 | -0.480 |

| 9 | 1.111 | -0.731 | 0.056 | -0.835 | -1.094 | 0.848 | 1.227 |

| 10 | 0.537 | -0.431 | 0.255 | -1.255 | -0.726 | 0.983 | -0.465 |

| 11 | 0.225 | -0.211 | 0.168 | -1.026 | -0.427 | 0.675 | -0.481 |

| 12 | 0.080 | -0.086 | 0.089 | -0.575 | -0.240 | 0.317 | -0.462 |

**表 11.6** 欧式看跌期权的价格和 Greeks，LSM 算法

| 现价 (Spot) | 闭式价格 (Closed Price) | LSM 价格 | 闭式 Delta (Closed Delta) | LSM Delta | 闭式 Gamma (Closed Gamma) | LSM Gamma | 闭式 Vega1 (Closed Vega1) | LSM Vega1 |

|---|---|---|---|---|---|---|---|---|

| 8 | 1.839 | 1.834 | -0.880 | -0.875 | 0.139 | 0.174 | 0.358 | 0.367 |

| 9 | 1.048 | 1.057 | -0.681 | -0.663 | 0.253 | 0.252 | 0.857 | 0.729 |

| 10 | 0.502 | 0.522 | -0.411 | -0.409 | 0.264 | 0.241 | 0.857 | 0.859 |

| 11 | 0.225 | 0.221 | -0.193 | -0.206 | 0.164 | 0.165 | 0.662 | 0.693 |

| 12 | 0.080 | 0.078 | -0.083 | -0.085 | 0.074 | 0.085 | 0.383 | 0.415 |

为了评估通过这种方法计算的 Greeks 的准确性，我们使用 LSM 算法为欧式看跌期权定价，使用与表 11.5 相同的设置，并将 LSM 算法得到的 Greeks 与闭式解 Greeks 进行比较。表 11.6 显示的结果表明，在 LSM 算法下计算的 Greeks 相当接近。

# 使用显式法计算美式 GREE

回想第 10 章，当用有限差法求解 Heston PDE 时，股票价格和波动率维度的矩阵包含一组完整的期权价格。因此，可以通过双维插值函数 `interp2` 很容易获得矩阵的偏移值以获得 Greeks。通过这种方式，可以获得对 S 和 v 的所有敏感度，即 delta、gamma、vega 和 vol。以下代码展示了如何在 Matlab 中对非均匀网格使用显式法处理欧式期权。该代码使用了第 10 章中提供的 `HestonUniformGrid` 来在二维网格上近似 Heston PDE。

```matlab
PutCall = 'P';
EuroAmer = 'E';
[u] = HestonUniformGrid(...,PutCall,EuroAmer);
PDEPrice = interp2(V,S,U0,S0);
% Delta and Gamma
dS = 1;
```

### MATLAB 和 C 中的 Heston 模型及其扩展

```matlab
D1 = interp2(V,S,U0,S0+dS);
D2 = interp2(V,S,U0,S0-dS);
DeltaPDE = (D1-D2)/2/dS;
GammaPDE = (D1 - 2*PDEPrice + D2)/dS^2;
% Vega
dV = 1e-2;
V1 = interp2(V,S,U0,V0+dV);
V2 = interp2(V,S,U0,V0-dV);
VegaPDE = (V1-V2)/2/dV*sqrt(V0);
C1 = interp2(V,S,U0,S0+dS);
C2 = interp2(V,S,U0,S0-dS);
C3 = interp2(V,S,U0,V0+dS);
C4 = interp2(V,S,U0,V0-dS);
% Vanna and Volga
VannaPDE = (C1 - C2 + C3 - C4)/4/dV/dS*sqrt(V0);
dc2 = (V1 - 2*PDEPrice + D2)/dV^2*sqrt(V0);
VolgaPDE = 4*sqrt(V0) * (dc2 + VegaPDE);
```

Theta 的获取可以通过识别 `HestonUniformGrid` 函数返回上一步的 `$U(S,v,t)$` 和 `$U(S,v,t-dt)$` 直到到期值，这提供了有限差法所需的 theta 时间偏移值。

```matlab
[U] = HestonUniformGrid(...);
% Theta
T1 = interp2(V,S,U0,S0); // 获取 U(S,v,T)
T2 = interp2(V,S,U0,S0); // 获取 U(S,v,T-dt)
ThetaPDE = -(T1 - T2)/dt;
```

注意，在第一行中，函数被修改为返回 `$U(S,v,r)$` 和 `$U(S,v,r-dt)$`，而不仅仅是 `$U(S,v,t)$`。在 C# 中，区别在于我们创建了用于二维插值的 `interp2()` 函数。

```csharp
public struct Uu
{
    public double[,] bigU;
    public double[,] smallU;
}
```

```csharp
for(int k=0; k<=N-1; k++)
{
    // 求解 PDE 并返回 U(S,v,T) 和 U(S,v,T-dt)
    Uu output = HestonExplicitUniformGrid(...);
    double[,] u = output.bigU; // output.smallU;
    // 价格, Delta, Gamma
    PDEPrice[k] = interp2(V,S,U0,S0[k]);
    D1 = interp2(V,S,U0,S0[k]+dS);
    D2 = interp2(V,S,U0,S0[k]-dS);
    DeltaPrice[k] = (D1-D2)/2/dS;
    GammaPrice[k] = (D1 - 2*PDEPrice[k] + D2)/dS^2;
    // Vega
    V1 = interp2(V,S,U0,S0[k]);
    V2 = interp2(V,S,U0,S0[k]-dv);
    VegaPrice[k] = (V1 - V2) * 2/dv * sqrt(V0);
    // Theta
    T1 = interp2(V,S,U0,S0[k]); // U(S,v,T)
    T2 = interp2(V,S,U0,S0[k]); // U(S,v,T-dt)
    ThetaPrice[k] = -(T1 - T2)/dt;
}
```

使用显式法生成美式期权 Greeks 的 C 代码非常相似，并使用了第 10 章引入的 `HestonExplicitUniformGrid()` 函数来近似 PDE。该函数必须修改为返回 `$U(S,v,\tau)$` 和 `$U(S,v,\tau-dt)$`。显式法也可以用于获取 Clarke 和 Parrott (1999) 的美式看跌期权价格和 Greeks。为每个现价构建了一个独立的非均匀网格，并围绕现价中心。

```matlab
S0 = [8 9 10 11 12];
for s=1:length(S0)
% 现价网格
c = S0(s)/s; % 代替 K/5
dz = 1/ns*(asinh((Smax-S0(s))/c - asinh(-S0(s))/c); % 代替 K/c
```
