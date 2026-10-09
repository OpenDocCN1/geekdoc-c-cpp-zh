
我们还可以将局部波动率的三种估计值（解析和有限差分）应用于方程 `(2.24)`，并对 `(2.44)` 中的近似值应用于 SPX 期权数据。这在图 2.11 中所示。

## MATLAB 和 C# 中的 HESTON 模型及其扩展

到期 7 天

到期 15 天

![](img/bc3df3b6c26c2272307f56b6cf75ef87_65_0.png)

![](img/bc3df3b6c26c2272307f56b6cf75ef87_65_1.png)

到期 43 天

到期 71 天

![](img/bc3df3b6c26c2272307f56b6cf75ef87_65_2.png)

![](img/bc3df3b6c26c2272307f56b6cf75ef87_65_3.png)

图 2.11 市场隐含波动率与 Heston 波动率，标普 500 指数

正如预期，且与图 2.10 一致，局部波动率通常比隐含波动率更陡峭且波动更大。对局部波动率的近似保留了更陡的斜率，但没有保留这种波动行为。解析和有限差分的局部波动率非常接近，71 天到期的除外，有限差分近似略有失效。

### 隐含波动率

我们在本章较早提到，使用 Heston 模型获得的期权价格具有内置的隐含波动率，从意义上说，从这些价格中提取的隐含波动率将表现出隐含波动率特征。此外，从从中提取的参数 `$\rho$` 和 `$\sigma$` 对模型的陡峭度和光滑度有影响。在实践中，从 Heston 模型中提取的波动率在匹配短期隐含波动率时有时拟合效果较差。对于长期期权，拟合效果更好。我们通过对道琼斯工业平均指数 ETF（代码 DIA）的四种到期日（37、72、135 和 226 天）的看跌期权来说明。DIA 的收盘价为 `$129.14`。我们列出了参数估计值 `$\kappa = 0.8799, \sigma = 3.6706, v_{0} = 0.0435,$` 和 `$\rho = -0.4171$`。Heston 模型参数估计方法在第 6 章中有详细讨论。为了简单，我们设置 `r=0`。图 2.12 展示了来自 DIA 的市场隐含波动率，以及使用二分算法根据之前生成的 Heston 价格得到的隐含波动率。

图 2.12 清楚地表明，在短期，Heston 隐含波动率与市场隐含波动率的拟合效果很差。对于长期，Heston 模型提供了非常好的拟合。

使用二分算法来获取市场和 Heston 隐含波动率。本章之前介绍了用于该算法的 Matlab 函数 `BiscBIV.m` 和 C 函数 `BiscBIV()`。该算法通过寻找市场价格与 Black-Scholes 价格之间差值的零点来确定隐含波动率。使用该算法的优点是，只要函数是连续的，且选择的区间两个初始端点使得一个值产生负差，另一个值产生正差——即区间内存在根——就能始终找到解。由于期权价格随波动率单调递增，我们始终可以使用小值作为第一个端点（例如 0.1%），并在第二个端点使用非常大的值（例如 500%）。

我们使用了以下 Matlab 代码生成了图 2.12。我们硬编码了参数值，这些值是从第 6 章的 Matlab 代码中获得的。

![](img/bc3df3b6c26c2272307f56b6cf75ef87_66_0.png)

图 2.12 DIA 看跌期权的市场与 Heston 隐含波动率

```matlab
param = [8.8799, 0.0674, 3.6706, 0.0435, -0.4171];

for k=1:NK
  t=1:NT
    CallPrice = HestonCallGaussLaguerre(K(k),T(t),...)
    ModelPrice(k,t) = CallPrice - S0 + exp(-rf*T(t))*K(k);
for k=1:NK
  t=1:NT
    IVm(k,t) = BisecBSIV(K(k),T(t),ModelPrice(k,t),...);
for t=1:NT
  subplot(2,2,t);
  plot(K,IV(:,t),KIVm(:,t));
```

### 矩量爆炸

Andersen 和 Piterburg (2007) 推导了终端股票价格矩量 `$E[S_T^\omega]$` 在有限时间内发生爆炸（变为无穷大）的条件。他们论文的结果可以用于寻找 `$\omega > 1$` 的值，使得 `$E[S_T^\omega]$` 对于所有 `T` 保持有限。使用他们关于时间的解析表达式来寻找 `$E[S_T^\omega]$` 对于所有 `T` 保持有限的 `$\omega > 1$` 的值。

```matlab
UpperAP = W(j);
% 矩下界
W = [LoLimit:0];
for k=1:n
  j = 1;
  T(j) = 0;
  while (T(j) < inf)
    j = j+1;
    T(j) = MomentExplode(W(j), lambda, sigma, kappa, rho);
  end
  e = 1/10^k;
  W = [W(j-1):e:W(j+1)];
  clear T
end
LowerAP = W(j);
```

为了使用特征函数寻找矩边界，我们循环遍历 omega 的值，直到特征函数返回一个复值。这是通过 `FindLeeBounds.m` 函数的中间部分实现的。

```matlab
% 上部矩。循环直到遇到虚部imag(CF)
CF = 0;
e = 1e-5;
W = 0.9*UpperAP;
while isreal(CF)
  phi = -i*W;
  CF = HestonCF(phi, kappa, theta, 0, rho, sigma, tau, S, r, q, v0, trap);
  W = We;
end
UpperAP = W;
% 下部矩。循环直到遇到虚部imag(CF)
CF = 0;
e = -1e-5;
W = 0.9*LowerAP;
while isreal(CF)
  phi = -1*W;
  CF = HestonCF(phi, kappa, theta, rho, sigma, tau, 0, S, r, q, v0, trap);
  W = We;
end
LowerAP = W;
```

最后，该函数的最后部分返回了波动率斜的 Lee (2004b) 边界。

```matlab
p = UpperAP - 1;
q = -LowerAP;
BR = 2 - 4*(sqrt(p^2 + p) - p);
BL = 2 - 4*(sqrt(q^2 + q) - q);
```

## MATLAB 和 C# 中的 HESTON 模型及其扩展
