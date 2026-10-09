
`C = BSC(S,K,rf,q,T);`

`CV = BSV(S,K,rf,q,T);`

`y = c + sigma/sqrt(T*T)*R11 + sigma^2*(J3*R20/T^2 + ...);`

```
函数 SeriesIIcall.m 返回 (4.43) 中的隐含波动率和 (4.44) 中的级数 II 价格。
```

```
function y = SeriesCall(...);
```

`BSC = @S,K,rf,q,T) (S*exp(-q*T)*normcdf(...))`

`J1 = J(rho,theta,kappa,v0,1);`

`J3 = J(rho,theta,kappa,v0,3);`

`J4 = J(rho,theta,kappa,v0,4);`

`v = theta + (v0-theta)*(1-exp(-kappa*T))/(kappa*T);`

`X = log(S*exp((rf-q)*T)/K);`

`v = vT;`

`R20 = R(2,0,X,T);`

`R11 = R(1,1,X,T);`

`R12 = R(1,2,X,T);`

`R22 = R(2,2,X,T);`

`y = BSC(S,K,rf,q,T);`

`iv = sqrt(iv);`
```

生成 (4.42) 中的级数 I 期权、(4.43) 中的隐含方差和 (4.44) 中的级数 II 期权的 C 代码与之类似，不同在于我们使用 `CCDF()` 来计算标准正态分布。请参考第 2 章有关该函数的详细信息。

为了说明，我们计算了到期时间为 3 个月的虚外期权价格，$S_0 = 100, K = 105, r=0.05, q=0.01$。对于 Heston 参数，我们使用 $\kappa = 10, \theta = 0.07, v_0 = 0.06, \sigma = 0.9$ 以及 $\rho = 0.9$。通过这些设置，方程 (4.6) 中的期望平均方差 $v$ 为 $\bar{v}=0.06633$，将其用于 (4.35) 产生 Black-Scholes 价格 $C_{BS}(S_0, \bar{v}, T)=3.48426$。使用梯形法则的精确 Heston 价格为 $C(K)=3.65090$。方程 (4.42) 和 (4.44) 中的级数 I 和级数 II 价格分别为 $C_I(S_0, v_0, T)=3.65218$ 和 $C_{II}(S_0, v_0, T)=3.66106$，它们非常接近解析解价格。(4.43) 中的级数 II 隐含方差为 $\bar{v}=0.26674$。

![](img/bc3df3b6c26c2272307f56bcf75ef87_122_0.png)

图 4.4 Lewis (2000) 图 3.3.1 的

使用 Lewis (2000) 表 3.3.1 中使用的参数值，即 $\rho = -0.5, v_0 = 0.0225, \kappa = 4, \theta = 0.09/4, \sigma = 0.1$，以及 $T = 0.25$ 和 $S = K = 100$，我们从 (3.6) 得到平均方差 $\overline{v} = 0.0225$。Mat 程序 `Lewis_Table.m` 重现了 Lewis (2000) 第 81 页表 3.3.1 中的条目。

# 结论

在本章中，我们介绍了 Lewis (2000, 2001) 开发的用于波动率定价的几种强大且新颖的方法。一旦获得了波动率模型的基本变换，期权价格就可以很容易地获得。此外，根据 Lewis (2000)，该基本变换适用于多种模型，而不限于 Heston 模型。我们还研究了 Lewis (2001) 使用 Parseval 等等式定价的方法。

# 第 5 章 数值积分方案

## 摘要

Heston 模型中期权价格的计算通常需要评估积分。对于我们遇到的大多数公式都是如此，在 Heston 模型中无法找到反函数，必须进行数值估计。

数值积分将 $[a, b]$ 上的积分近似为离散点的函数值与其权重乘积的和：

```
$$\int_{a}^{b} f(x)dx \approx \sum_{l=1}^{N} w_l f(x_l).$$
```

点 $(x_1, \dots, x_N)$ 称为节点或横坐标，而点 $(w_1, \dots, w_N)$ 称为权重或系数。在本章中，我们介绍了数值积分的大类、牛顿公式和高斯积分。牛顿公式很容易实现，但它们假设横坐标等距。为了使 (5.1) 准确，需要许多横坐标，特别是当积分范围内函数剧烈或震荡时。这将评估 (5.1) 的计算时间大幅增加。

Heston (1993) 中的概率 $P_i$ 需要积分域 $(0, \infty)$，因此 $a=0$ 和 $b=\infty$ 是积分 (5.1) 所需边界。当我们使用牛顿公式时，必须截断上限。本章展示了如何通过 Zhu (2010) 描述的多区域积分合理地进行截断。另一种，Kahl 和 Jäck (2005) 将积分域转换为 $[0,1]$，从而消除了截断的需求。

(FFT) 由 Carr 和 Madan (1999) 开创，Chourdakis (2005) 提出了分数傅里叶变换，它是 FFT 的一种改进，比其前身更具活性。这些方法都非常快，因为它们能够在单次计算中产生行权网格上的上的期权价格。

### 数值积分中的被积函数

作者通常用 $x_0$ 表示方程 (5.1) 数值近似中的第一个节点。为了使我们的符号与高斯求积保持一致，我们有时将第一个节点记为 $x_i$。此外，由于 Matlab 中的数组索引从 1 开始，让节点从 1 开始可能会很方便。关于数值积分方法的文献非常丰富且详尽，该领域有许多优秀的教科书，例如 Burden 和 Faires (2010) 以及 Cohen (2011) 的著作。

在 (5.1) 中，节点表示为 $x$，但在 Heston 模型的积分公式中，积分变量表示为 $\phi$，因此节点应表示为 $\phi_i$。被积函数的形式取决于我们使用哪个公式来获取 Heston 看涨期权价格。如果我们使用原始的 Heston (1993) 公式，则 (5.1) 中 $P_i$ 的被积函数为：

```
$f(\phi_i) = \text{Re} \left[ \frac{e^{-i\phi_i} \ln K_f(\phi_i; X, v)}{\phi_i} \right] \quad \text{for } k=1, 2. \quad (5.2)$
```

如果我们使用第 4 章涵盖的 Lewis (2000) 变换，则被积函数为：

```
$f(\phi_i) = \text{Re} \left[ \frac{e^{-i\phi_i X}}{\phi_i^2 - i\phi_i} \hat{H}(\phi_i, v, \tau) \right] \quad (5.3)$
```

最后，如果我们使用第 3 章涵盖的 Carr 和 Madan (1999) 公式，则 (5.1) 中的被积函数变为：

```
$f(\phi_i) = \text{Re}[e^{-i\phi_i} \ln K(\phi_i)] \quad (5.4)$
```

其中

```
$$\psi(\phi_i) = \frac{e^{-rT} f_2(\phi_i) - (\alpha + i; x, v)}{\alpha^2 + \alpha - \phi_i^2 + i(2\alpha + 1)\phi_i}$$
```

其中 $f_2$ 是 Heston 模型的特征函数。

### 牛顿-Cotes 公式

牛顿-Cotes 是最简单的积分规则，但对计算能力的要求也最高。闭式牛顿-Cotes 公式使用节点 $x_1, x_2, \dots, x_N$ 将积分区域 $[a, b]$ 分为等间距的子区间。

## 数值积分方案

节点的定义取决于所使用的公式。我们考虑了四类牛顿-Cotes 公式：中点法则、梯形法则、辛普森法则和辛普森三八法。我们之所以考虑这些，是因为端点 $a$ 和 $b$ 被用作节点，因此这些规则被称为闭式版本。

在 Heston 模型中，我们通常要求在区域 $(0, \infty)$ 上进行积分计算。这意味着当我们使用牛顿-Cotes 公式时，必须选择区域 $[\phi_{\min}, \phi_{\max}]$，其中 $\phi_{\min}$ 是一个小数，$\phi_{\max}$ 是一个很大的数。我们在第 1 章中看到 Heston 的被积函数可能是高度振荡的。当我们选择 $\phi_{\max}$ 时，要确保足够大，使得积分有足够的衰减，以防止 (2.1) 中近似的损失。

积分区域 $(0, \infty)$ 要求的一个例外源于 Kahl 和 Jackel (2005)。他们将区域 $(0, \infty)$ 转换为闭区间 $[0, 1]$。在他们的方法中，我们不需要担心选择 $\phi_{\min}$ 或 $\phi_{\max}$。我们在本章中看到，他们的变换特别适用于 Gauss-Lobatto 求积，而不是牛顿-Cotes 公式。

### 中点法则

这是我们介绍的 Newton-Cotes 公式中最简单的一种。它将 (5.1) 中的积分近似为矩形和，每个矩形的宽度相等为 $x_{j+1}-x_j$，高度由被积函数 $f(x)$ 在区间 $(x_j, x_{j+1})$ 中点的值给出。定义节点 $x_j = a+(j-1)h$，对于 $j=1, \dots, N$，其中 $h=(b-a)/(N-1)$，使得 $x_1=a$ 且 $x_N=b$。由于有 $N-1$ 个子区间，近似涉及：

$$\int_a^b f(x)dx \approx \sum_{j=1}^{N-1} \frac{x_j+x_{j+1}}{2}$$

中点法则使用的权重 $w_j=h$ 对于 $j=1, \dots, N-1$，且 $w_0=0$。以下代码在 `HestonPriceCotes` 中实现了该规则：

```matlab
h = (b-a)/(N-1);
phi = [a:h:b];
wt = h*ones(1,N);
for k=1:N-1
  mid = phi(k);
  int1(k) = wt(k)*HestonProb(mid,1);
  int2(k) = wt(k)*HestonProb(mid,2);
end
I1 = sum(int1);
I2 = sum(int2);
P1 = 1/2 + 1/pi*I1;
P2 = 1/2 + 1/pi*I2;
```

### 梯形法则

该规则稍微复杂，因为它将 (5.1) 中的积分近似为梯形和，每个梯形的宽度相等为 $x_{j+1}-x_j$，但高度由端点 $f(x)$ 的值定义。梯形通过连接 $f(x_i)$ 和 $f(x_{i+1})$ 构建。节点的定义见前一节的中点法则。梯形法则使用 $w_i = w_N = b/2$，且对于 $j=2 \dots N-1，$w_j = h$。因此 (5.1) 的近似为：

$$\int_a^b f(x)dx = \frac{b}{2}f(i) + \sum_{j=2}^{N-1} f(x_j) + \frac{b}{2}f(N)$$

实现梯形法的 Matlab 代码非常直接。它出现在 `HestonPriceCotes.m` 函数中：

```matlab
wt = h.*[1/2 ones(1,N-2) 1/2];
for k=1:N
  int1(k) = wt(k)*HestonProb(phi(k),1);
  int2(k) = wt(k),2;
```

### 双重积分的梯形法则

在第 8 章中，我们将遇到 Chiara 和 Zogas (2006) 用于 Heston (1993) 模型美式看涨期权定价的模型。他们的方法需要双重积分的数值计算。双重积分最简单的方法之一是 Burden 和 Faires (2010) 描述的复合梯形法则。我们希望在区域 $[a,b] \times [c,d]$ 上评估双重积分。复合梯形法则将积分近似为：

$$\int_a^b\int_c^d f(x,y)dy = \frac{(b-a)(d-c)}{16} \times [f(a,c)+f(a,d)+f(b,d) + 2\left(f(\frac{a+b}{2},c) + f(\frac{a+b}{2},d)\right) + 2\left(f(a,\frac{c+d}{2}) + f(b,\frac{c+d}{2})\right) + 4f(\frac{a+b}{2},\frac{c+d}{2})]$$

Matlab 函数 `DoubleTrap.m` 根据方程 (5.5) 实现了复合梯形法则。

```matlab
function y = DoubleTrap(f,X,Y)
Nx = length(X);
Ny = length(Y);
for y=2:Ny
a = Y(y-1);
b = Y(y);
for x=2:Nx
 c = X(x-1);
d = X(x);
term1 = f(a,c) + f(a,d) + f(b,c) + f(b,d);
term2 = f((a+b)/2, c) + f((a+b)/2, d) + ...;
term3 = f((a+b)/2, (c+d)/2);
Int(x,y) = (b-a)*(d-c)/16*(...);
end
end
y = sum(sum(Int));
```

调用该函数时，为 $[a, b] \times [c, d]$ 创建积分网格，为 $f(x,y)$ 创建函数，然后将该函数作为第一个参数传递给 `DoubleTrap`。为了说明这一点，我们运行以下代码来评估正态分布。

```matlab
f = @(x,y) (0.5/pi*exp(-(x^2+y^2)/2));
for j=1:Nx
X(j) = LoX + j*dx;
end
for j=1:Ny
Y(j) = LoY + j*dy;
end
TrapValue = DoubleTrap(f, X, Y);
```

`DoubleTrap.m` 函数返回 $(x,y) = (-0.515, 0.243)$ 处的正态分布函数值为 0.18075，这与使用 Matlab 函数 `mvnncdf.m` 得到的值非常接近。此处没有代码。

### 辛普森法则

辛普森法则比中点法则或梯形法则都复杂，因为它在 (5.1) 的近似中使用二次多项式而非直线。然而，因此它精确得多。辛普森法则使用与中点和梯形法则相同的节点，但将权重定义为 $w_1 = w_n = h/3$，当 $j$ 为偶数时，$w_i = 4h/3$，当 $j$ 为奇数时，$w_i = 2h/3$。

$$\int_a^b f(x)dx \approx \frac{h}{3}f(a) + \frac{4h}{3}\sum_{j=1}^{N/2}f(x_{2j-1}) + \frac{2h}{3}\sum_{j=1}^{N/2}f(x_{2j}) + \frac{h}{3}f(x_N)$$

在 Matlab 中实现辛普森法则并不比实现中点或梯形法则更复杂。我们需要注意交替的

依赖于 $j$ 的权重性质是偶数还是奇。以下代码取自 Matlab 函数 `HestonPriceNewtonCotes.m`，用于实现此规则。

```
wt = (h/3).*1 [(3+(-1)).^[2:N-1]];
for k=1:N;
int1(k) = wt(k)*HestonProb(phi(k), ..., 1);
int2(k) = wt(k)*HestonProb(phi(k), ..., 2);
```

### 辛普森三八法

辛普森三八法是辛普森法的改进。它在方程 (5.1) 的近似中使用三次多项式，而不是二次多项式。为了实现辛普森三八法，更方便的方法是从 $x_0$ 开始定义横坐标，定义为 $x_i = x_0 + ih$，其中 $i=0, \dots, N$，$N$ 是三的倍数且 $h = (b-a)/N$。辛普森三八法的权重 $w_j$ 取决于 $j$ 是否能被 3 整除。

$w_j = \begin{cases} 3h/8 & \text{if } j=0 \text{ or } j=N \\ 6h/8 & \text{if } j=3, 6, 9, \dots \\ 9h/8 & \text{otherwise.} \end{cases}$

例如，当 $N=12$ 时，权重为：

$$\begin{array}{c|ccccccccccccccc} j & 0 & 1 & 2 & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10 & 11 & 12 \\ \hline w_j & 3h & 9h & 9h & 6h & 9h & 9h & 6h & 9h & 9h & 6h & 9h & 9h & 3h \\ & & 8 & 8 & 8 & 8 & 8 & 8 & 8 & 8 & 8 & 8 & 8 \end{array}$$

因此，辛普森三八法为：

> $$\int_a^b f(x)dx = \frac{3b}{8}f(x_0) + \frac{6b}{8}\sum_{j=3,6,\dots}^{N-1}f(x_j) + \frac{9b}{8}\sum_{j\neq3,6,\dots}^{N-1}f(x_j) + \frac{3b}{8}f(x_N).$$$$

下面的代码段实现了辛普森三八法。取自 Matlab 函数 `HestonPriceNewtonCotes.m`。

```
N = N-mod(N,3)+1;
h = (b-a)/(N-1);
wt = (3*h/8).*[1 3 3] repmat([2 3 3],1,(N-1)/3-1);
phi = [a:h:b];
for k=1:N
int1(k) = wt(k)*HestonProb(phi(k),..., 1);
int2(k) = wt(k)*HestonProb(phi(k),..., 2);
```
