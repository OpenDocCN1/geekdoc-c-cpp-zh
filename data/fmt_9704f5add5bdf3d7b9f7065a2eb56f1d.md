
```csharp
static double[] findroot(double[] C, double a, double b, int n, double Tol, int MaxIter) {
    // Find Sturm 序列
    double[][] Sturm = sturm(C);
    int nS = C.Length;
    // Find区间内的 Sturm 符号
    var sr = findintervals(a, b, n, Sturm, nS);
    // 根的数量和区间的起始/结束
    int NRoots = sr.NRoots;
    double[] StartInt = sr.StartInt;
    double[] EndInt = sr.EndInt;
    // 应用二分法寻找根
    double[] root = new double[NRoots];
    for (int i = 0; i < NRoots - 1; i++) {
        a = StartInt[i];
        b = EndInt[i];
        root[i] = Bisection(C, a, b, Tol, MaxIter);
    }
    return root;
}
```

为了说明，假设 `$N=5$`，则公式 (5.6) 中的 Laguerre 多项式为：

$L_5(x) = 1 - 5x + 5x^2 - \frac{5}{3}x^3 + \frac{5}{24}x^4 - \frac{1}{120}x^5. \quad (5.1)$

该多项式绘制于图 5.1。图中识别了根并用左右端点列出。

**图 5.1 Laguerre 多项式**

| 编号 | 左端点 | 右端点 | 根 | 权重 |
|---|---|---|---|---|
| 1 | 0.2500 | 0.3300 | 0.2836 | 0.6791 |
| 2 | 1.3699 | 1.4497 | 1.4134 | 1.6385 |
| 3 | 3.5297 | 3.5997 | 3.5664 | 2.7694 |
| 4 | 7.0494 | 7.1294 | 7.0858 | 4.3157 |
| 5 | 12.5690 | 12.6489 | 12.6408 | 7.2192 |

**表 5.1 Laguerre 的根和权重**

以下代码段为 `$N = 32$` 个点生成 Laguerre 横坐标和权重。

```matlab
n = 32;
% 二分算法设置
Tol = 1e-10;
MaxIter = 500;
% 区间的起始和结束值
a = 0.0;
b = 120.0;
ni = 500;
% Laguerre 横坐标和权重
Xw = GaussLaguerre(n,a,b,ni,Tol,MaxIter);
```

## 积分极限与 KAHL AND JACKEL 变换

当我们实现 Gauss-Laguerre 积分时，横坐标是提供的，因此我们不需要担心积分的下限和上限。当我们实现 Newton-Cotes 公式以及 Gauss-Legendre 或 Gauss-Lobatto 积分时，我们需要提供极限。公式 (5.1) 要求的下限是 `a=0`，但如果我们使用公式 (5.2) 中的原始 Heston 被积函数公式，我们不能使用零，因为函数在那里未定义。因此我们必须使用一个较小数 `phi_min` 作为 `a`。(5.1) 要求的上限是 `b=∞`，所以我们必须截断积分区域并选择一个大数 `b = phi_max` 作为

## 数值积分方案

上限。数值的大小取决于被积函数（通常是震荡的）衰减到零的速度。通常情况下，震荡和衰减速度随期限的增长而发生巨大变化，因此短期限会产生剧烈震荡，需要较大的上限。图 5.2 展示了典型 Heston 参数和期权设置下的这一情况。

通常而言，不应对积分上限使用随意的选择，而是应该采用考虑了被积函数衰减速度的选择，如图 5.2 所示。例如，在他的 Mathematica 中，Lewis (2000) 使用了 `w_max=[1000, 10/sqrt(T)]`。

我们还可以在该方法中使用 Zhu (2010) 描述的多域积分法，积分区域被划分为多个子域 `[a_0, a_1], [a_1, a_2], [a_2, a_3]` 等，其中 `a_0 = 0` 且 `a_0 < a_1 < a_2 < …`。概率 `hat{P}` 的积分通过累加每个子域的积分来构建：

$$\sum_{k=0}^{a_{k+1}} Re \left[ \frac{e^{-i\phi} \ln f_{l}(\phi; x, v)}{i\phi} \right] d\phi$$

当子域积分不再对和产生贡献时，求和停止。换句话说，当

$$\int_{a_M}^{a_{M+1}} Re \left[ \frac{e^{-i\phi} \ln K_{l}(\phi; x, v)}{i\phi} \right] d\phi < \varepsilon \quad (5.13)$$

![](img/bc3df3b6c26c2272307f56b6cf75ef87_140_0.png)

**图 5.2** 被积函数的衰减与期限

对于某个整数 `M`，`ε` 是容差水平。积分域为 `(0,a_M]`，因此 `phi_max=a_M`。Zhu (2010) 解释道，这种方法的优点能够优化地分配上限，并能够适应不同的行权价和期限值。该方法会自动为短期限期权分配更宽的区域（此时被积函数倾向于震荡），并为长期限期权分配更窄的区域（此时被积函数性质较好）。该方法通过避免不需要的区域来缩短计算时间，同时通过为需要的区域分配较宽区域来提高准确性。

Gauss-Legendre 或 Gauss-Lobatto 特别适用于这种方法，因为它们都可以通过使用方程 (5.8) 中的变换来适应任意区域的积分。然而，为了应用 Zhu (2010) 的多域积分法，我们可以生成一次横坐标和权重以获得子域上的积分，每次应用变换。当满足 (5.13) 中的条件时。Matlab 函数 `HPriceGaussLegendreMD.m` 实现了多域积分。

```matlab
function [Price D N] = HPriceGaussLegendreMD(xLE,wLE)
for j=2:length(A)
  for k=1:length(xGE)
    % Lower and upper limits
    a = A(j);
    b = B(j);
    X = (a+b)/2 + (b-a)/2*xGE(k);
    % The integrals
    int1(j,k) = wLE(k)*HestonProb(X,...,1)*(b-a)/2;
    int2(j,k) = wLE(k)*HestonProb(X,...,2)*(b-a)/2;
    % Sum the integrals over each subdomain
    sum1(j) = sum(int1(j));
    sum2(j) = sum(int2(j));
    % Stopping criterion
    if abs(sum1(j))<tol && abs(sum2(j))<tol
      break;
    end
  end
nP1 = 1/2 + 1/pi*sum(sum1);
nP2 = 1/2 + 1/pi*sum(sum2);
Hestonc = S*exp(-q*T)*P1 - K*exp(-r*T)*P2;
% Integration domain and points
D = [A(1); A(j)];
N = length(A(1:j));
```

该函数接受一组一组定义子域的点作为输入。它返回看涨价格，或通过看跌期权平价公式返回看跌价格。它还会输出生成的积分域和使用的点数。实现此方法的 C# 函数与 Matlab 代码非常相似，此处未给出。

为了说明 Zhu (2010) 的多域积分，我们使用了本章贯穿始终的高斯积分示例中的设置。

## 数值积分方案

回想此示例中的期限为 `τ = 1.5`。以下代码实现了多域积分。我们将积分域 `(0, 150]` 划分为 10 个子域。

```matlab
[xGle wGle] = GenerateGaussLegendre(32);
% The domain of integration and the tolerance
lo = 1e-20; hi = 150;
N = 10;
dA = (hi - lo)/N;
A = [lo:dA:hi];
tol = 1e-6;
% Calculate the "true" option price using Newton-Cotes
N = 10000;
method = 3;
ab = 150;
Price = HestonPriceCoates(method,b,N);
% Calculate the price using multi-domain integration
[PriceMD Domain N] = HPriceGaussLegendreMD(xGle,wGle);
```

使用 `ε = 10^{-6}` 的容差进行多域积分得到的价格为 3.2561，这与使用 10000 个点的辛森法非常接近。在该容差水平下，算法返回 `hat{phi}_max=25`，但积分区域显著变窄。如果我们将期限缩短到 `τ = 0.5`，价格下降到 7.1026，这同样是准确的。算法返回 `hat{phi}_max=35`，对于 `τ=1.5`，计算时间增加了。另一种寻找合适积分域的方法是将 `phi ∈ [0, ∞)` 转换为更容易处理的区间 `x ∈ [0, 1]`，如 Kahl 和 Jäck (2005) 所建议。在他们的方法中，Heston 被积函数 `Re [ e^{-i\phi} ln f_{phi}; x, v) / i\phi ]` 中的 `phi` 被替换为 `-ln x/C_∞`，其中 `C_∞ = sqrt(theta/sigma^2)`，`tau` 是期限，且积分除以 `xC_∞`。价格变为：

$$C(K) = e^{-rT} \int_0^1 y(x)dx$$

其中

$$y(x) = \frac{1}{2}(F-K) + \frac{\lim_{u\to 0} f_1(u) - K\lim_{u\to 0} f_2(u)}{\pi C_{\infty}}$$

在形式 (5.15) 中，积分 `y(x)` 在 `x=0` 和 `x=1` 处未定义，这意味着积分只能在 `(0, 1)` 范围内进行。然而，Kahl 和 Jäck (2005) 解析导出了被积函数的极限：

$$\lim y(0) = \frac{1}{2}(F-K)$$

$$\lim y(1) = \frac{F-K}{2\pi C_{\infty}}$$

`lim_{u\to 0} f_i(u)` 的表达式在他们的方程 (44) 和 (50) 中。因此：

$$\lim_{u\to 0} f_1(u) = \ln(F/K) + C(0) \quad (16)$$

以及

$$\lim_{u\to 0} f_2(u) = \ln(F/K) + D'(0) \quad (17)$$

在最后一个实例中，我们有

$$C(0) = -\frac{e^{-\kappa\tau} + \theta(\tau - 1)}{2\kappa}, \quad D'(0) = -\frac{e^{-\kappa\tau}}{2\kappa}$$

在方程 (5.14) 中，当 `κρ ≠ 0` 时，

$$C(0) = -\frac{e^{\rho\tau^2} + \theta(\rho\tau - 1)}{2(\kappa - \rho)^2}, \quad D'(0) = -\frac{e^{-(\kappa - \rho)\tau}}{2(\kappa - \rho)}$$

但当 `κρ=0` 时，这些简化为：

$$C(0) = \frac{\tau^2}{4}, \quad D'(0) = \frac{\tau}{2}.$$

Kahl 和 Jäck (2005) 建议对方程 (5.14) 中的积分使用 Gauss-Lobatto 积分。这是合理的，因为这种积分包含了积分域 `[-1, 1]` 的横坐标。当应用 (5.8) 的变换时，结果是 Kahl 和 Jäck 方法所需的变换域 `[0, 1]` 的端点包含在了横坐标中。Matlab 函数 `HestonPriceKahlJäck` 实现了 (5.14) 中的看涨价格，并通过看跌期权平价返回看涨或看跌价格。

```matlab
function y = HestonPriceKahlJäck(...)
for u = 1:length(X)
    % Transformation of the abscissa
    x = 0.5*X(u) + 0.5;
    if x == 0
        % Integrand at left abscissa 0
        y(u) = 0.5*(F-K);
    elseif x == 1
        % Integrand at right abscissa 1
        f1 = log(F/K) + C1 + D1*v0;
        f2 = log(F/K) + C2 + D2*v0;
        y(u) = 0.5*(F-K) + (P*f1 - K*f2)/(pi*Cinf);
    else
        % Integrand at remaining abscissas
        f1 = HestonPro(-log(x)/Cinf,...,1);
        f2 = HestonPro(-log(x)/Cinf,...,2);
        y(u) = 0.5*(F-K) + (P*f1)/(pi*Cinf);
    end
    % Multiply by the weights
    z(u) = W(u)*y(u);
end
% The call price
JCAll = exp(-rf*T)*(1/2)*sum(z);
```

为了说明，我们使用了以下设置：`S=10, K=7, r=0.06, q=0.04`，期限为1 个月，以及参数 `κ=1, θ=0.06, σ=0.5, v0=0.06` 和 `ρ=-0.8`。使用 Heston 和 32 个横点的 Gauss-Laguerre 和 Gauss-Lobatto 积分得到的看涨价格分别为 3.0006 和 3.0017。相同的 Gauss-Lobatto 权重配合 Kahl 和 Jäck (2005) 公式得到的价格为 2.9992。

Kahl 和 Jäck 的被积函数如图 5.3 所示，图中包含了 32 个 Gauss-Lobatto 横坐标处的被积函数值。

# 136

## MATLAB 和 C# 中的 HESTON 模型及其扩展

震荡的，但由于它衰减很快，这种震荡只会导致微不足道的精度损失。

## 数值积分演示

Matlab 函数 `HestonPriceNewtonCotes.m` 包含了实现本章中四种 Newton-Cotes 公式所需的所有代码，而函数 `HestonPriceGaussLaguerre.m` 和 `HestonPriceGaussLegendre.m` 则用于高斯求积。在这个示例中，我们计算了当现货 `S=100、r=0.03、q=0.02` 时，1 个月欧式看涨和看跌期权的价格。对于 Newton-Cotes 公式我们使用了 100 个节点，而对于高斯求积仅使用了 5 个节点。行权价从 `K=98` 到 `K=102` 的价格分别位于表 5.2（看涨）和表 5.3（看跌）中，最后一列为平均绝对误差。

结果表明，四种 Newton-Cotes 公式产生的价格相当准确。高斯-Legendre（Gauss-Legendre）和高斯-Lobatto（Gauss-Lobatto）求积也非常准确，特别是考虑到它们仅使用了 5 个节点。高斯-Laguerre（Gauss-Laguerre）求积是所有方法中精度最低的。

## 表 5.2 看涨期权的求积比较

| 方法 | K = 98 | K = 99 | K = 100 | K = 101 | K = 102 | 误差 |
| --- | --- | --- | --- | --- | --- | --- |
| 真实价格 | 2.70 | 1.97 | 1.37 | 0.86 | 0.43 | 0.0369 |
| 100 点中点法 | 2.71 | 2.04 | 1.41 | 0.84 | 0.39 | 0.0369 |
| 100 点梯形法 | 2.71 | 2.04 | 1.41 | 0.84 | 0.39 | 0.0369 |
| 100 点辛普法 | 2.71 | 2.04 | 1.41 | 0.84 | 0.39 | 0.0375 |
| 100 点辛普森 3/8 法 | 2.71 | 2.04 | 1.41 | 0.84 | 0.39 | 0.0369 |
| 5 点高斯-Laguerre | 1.80 | 1.16 | 0.61 | -0.16 | -0.23 | 0.7634 |
| 5 点高斯-Legendre | 2.71 | 2.04 | 1.41 | 0.83 | 0.38 | 0.0376 |
| 5 点高斯-Lobatto | 2.71 | 2.04 | 1.41 | 0.84 | 0.39 | 0.0372 |

## 表 5.3 看跌期权的求积比较

| 方法 | K = 98 | K = 99 | K = 100 | K = 101 | K = 102 | 误差 |
| --- | --- | --- | --- | --- | --- | --- |
