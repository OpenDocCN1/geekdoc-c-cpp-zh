
% Boundary condition for Vmin.

```
for s=2:NS-1

derV = (u(s,2) - u(s,1)) / (V(2)-V(1));

derS = (u(s+1,1) - u(s-1,1)) / (S(s+1)-S(s-1));

LHS = r*u(s,1) + (r-q)*S(s)*derS + ...

U(s,1) = LHS*dt + u(s,1);

end

u = U;
```

% Interest points of the grid

```
for s=2:NS-1

 for v=2:NV-1

  derS = (u(s+1,v) - u(s-1,v)) / (S(s+1)-S(s-1));

  derV = (u(s,v+1) - u(s,v-1)) / (V(v+1)-V(v-1));

  derSS = ((u(s+1,v) - u(s,v)) / ...;

  derVV = ((u(s,v+1) - u(s,v)) / ...) / ...;

  derSV = (u(s+1,v+1) - u(s-1,v-1)) / ...;

  L = 0.5*V(v)*S(s)^2*derSS + rho*sigma*V(v)*S(s);

  U(s,v) = L*dt + u(s,v);

end

end
```

最后，函数的最后一部分在每个时间步应用方程 (8.11) 中的条件，以确定提前行权是否是最优的。

```
if strcmp(BeroAmer,'A')

for s=1:NS

  if strcmp(PutCall,'C')

    U(s,:) = max(U(s,:), S(s));

  elseif strcmp(PutCall,'P')

    U(s,:) = max(U(s,:), K-S(s));

end
```

该函数进入网格矩阵，对于 $i=0, \dots, N_s$ 和 $j=0, \dots, N_v$，即 $N_{ij}^t$。Matlab 函数 `interp2m` 采用二维插值来获取位于网格点之间的 $(S, v)$ 值的的期权价格。
实现显式法的 C# 代码非常相似，此处未给出。然而，我们需要一个用于二维线性插值的函数。这通过 C# 函数 `interp2()` 完成。

```
static double interp2(double[] X, double[] Y, double[] Z, Z... ) {

  // Find the index for x

if(xi == X[0]) {xi = 0; xflag = 1};

else if (xi == X[NX-1]) {xi = NX-1; xflag = 1};

else

  for(int i=1;i<=NX-1;i++)

    if(X[i-1] <= xi && (xi < X[i])) {x1 = i-1; x2 = i};

  // Find the index for y

if(yi == Y[0]) {yi = 0; yflag = 1};

else if (yi == Y[NY-1]) {yi = NY-1; yflag = 1};

else

  for(int i=1;i<=NY-1;i++)

    if(Y[i-1] <= yi && (yi < Y[i])) {y1 = i-1; y2 = i};

// Interpolation

if (xflag == 1 && yflag == 1) {

  result = Z[x1,y1];

} else if (xflag == 1 && yflag == 0) {

  result = Z[x1,y1] + (Z[x1,y2] - Z[x1,y1]) * (yi - Y[y1]) / (Y[y2] - Y[y1]);

} else if (xflag == 0 && yflag == 1) {

  result = Z[x1,y1] + (Z[x2,y1] - Z[x1,y1]) * (xi - X[x1]) / (X[x2] - X[x1]);

} else {

  result = Z[x1,y1] + (Z[x2,y1] - Z[x1,y1]) * (xi - X[x1]) / (X[x2] - X[x1]) +

                 (Z[x1,y2] - Z[x1,y1]) * (yi - Y[y1]) / (Y[y2] - Y[y1]) +

                 (Z[x2,y2] - Z[x1,y2] - Z[x2,y1] + Z[x1,y1]) * (xi - X[x1]) / (X[x2] - X[x1]) * (yi - Y[y1]) / (Y[y2] - Y[y1]);

}

return result;

}
```

为了说明，我们使用了上一节描述的 Clarke (1999) 和 Toivanen (2008) 的数值示例。显式法通过以下代码实现：

```
U = HestonPDENonUniformGrid(...);

for k=1:length(Spot)

S0 = Spot(k);

AmerPrice(k) = interp2(V,U,S0);
```

使用 140 和 90 分别作为价格和波动率的网格，带有 1000 个时间步。

### BELIAEVA-NAWALHA TREE

Beliaeva 和 Nawalkha (2010) 为 Heston 模型开发了路径无关的二元树。在他们的方法中，价格和方差树是独立构造的，然后重新合并。这需要对 $S_t$ 进行变换，使得 $Y_t$ 和 $v_t$ 独立。回想 Heston 模型由随机微分方程 (SDEs) 定义：

```
$dS_t = rS_td + \sqrt{v_t}dW_{t,1},dv_t = \kappa(\theta - v_t)dt + \sigma\sqrt{v_t}dW_{t,2}. (12)$
```

$E^Q[dW_{t,1}dW_{t,2}] = \rho$ 是方程之间的相关性。$S_t$ 的变换定义为：

```
$Y_t = \ln S_t - \frac{\rho}{\sigma}v_t$ (13)$
```

其中

```
$h_t = (r - \frac{\rho\theta}{\sigma})t.$ (14)$
```

应用 Ito 引理产生 $Y_t$ 的 SDE：

```
$dY_t = \mu_y(t)dt + \sigma_y(t)dW_{t,1}^* (15)$
```

其中漂移和波动率给出：

```
$\mu_y(t) = (\frac{\rho}{\sigma} - \frac{1}{2})v_t$, $\sigma_y(t) = \sqrt{1-\rho^2}\sqrt{v_t}.$ (16)$
```

方程 (15) 中的随机项是：

```
$dW_{t,1}^* = \frac{dW_{t,1}-dW_{t,2}}{\sqrt{1-\rho^2}}$ (17)$
```

由于 $E^Q[dW_{t,1}dW_{t,2}] = 0$，二元过程 $(Y_t)$ 是不相关的。这意味着 $Y_t$ 的概率可以使用三叉树近似。给定值 $Y_t$，可以通过反推 (13) 恢复股票价格：

```
$S_t = \exp(Y_t + h_t).$
```

# MATLAB 和 C# 中的 Heston 模型及其扩展

Beliaeva 和 Nawalkha (2010) 为变换后的方差 $x_t$ 构建了三叉树，定义为：

```
$x_t = \frac{2v_t}{\sigma} (19)$
```

他们通过变换恢复方差 $v_t$：

```
$v_t = \frac{1}{4}x_t^2. (20)$
```

首先构造变换后的方差 $x_t$ 的三叉树，并转换为方差 $v_t$ 的树。接下来，构造变换后的价格 $Y_t$ 的树，并转换为股票价格 $S_t$ 的树。最后，组合这些树形成一个可以对美式期权定价的树。在以下章节中，我们将解释如何这样做。

### 方差的三叉树

根据 Ito 引理，变换后的方差 $x_t$ 遵循带有漂移的 SDE：

```
$$\mu(x_t, t) = \frac{1}{2}(\frac{2\kappa\theta}{\sigma^2} - \frac{\kappa x_t^2}{2}). (21)$$
```

$x_t$ 三叉树的时间零点为 $x_0$，它通过将初始方差参数 $v_0$ 代入 (19) 得到。在时间 $t > 0$，给定过程处于 $x_t$，有组移动，取决于 $x_t > 0$ 还是 $x_t = 0$。

情况 1。如果 $x_t > 0$，时间 $t+dt$ 时的向上、中间和向下的移动为：

```
$x_{t+dt}^+ = x_t + b(j+1)\sqrt{dt},\nx_{t+dt}^m = x_t + bj\sqrt{dt},\nx_{t+dt}^- = x_t + b(j-1)\sqrt{dt} (8.22)$
```

其中 $j$ 和 $b$ 在后的方程 (8.25) 和 (8.26) 中定义。每次移动的概率为：

```
$P_v^u = \frac{1}{2b^2} - \frac{j}{2} + \frac{1}{2b}\mu(x_t, t)\sqrt{dt},\nP_v^m = 1 - \frac{1}{b^2},\nP_v^d = \frac{1}{2b^2} + \frac{j}{2b}\mu(x_t, t)\sqrt{dt}. (8.23)$
```

# 案例 2. 如果 $x_i = 0$，则 $x_i^{v+dt}$ 的定义与方程 (8.22) 相同，向下移动为 $x_{i+dt}^d = 0$，中间移动 $x_{i+dt}^m$ 不被使用。
在这种情况下，概率为：

```
$p_v^u = \frac{k\theta dt}{v_{i+dt}^u}, \quad p_v^m = 0, \quad p_v^d = 1 - p_v^u \quad (8.24)$
```

其中 $v_{i+dt}^u$ 通过代入方程 (8.20) 中的 $x_{i+dt}^u$ 得到。

上述方程 $j$ 和 $b$ 定义为

```
$j = \text{floor} \left( \frac{\mu (x_i, t)}{b} + \frac{\sqrt{dt}}{b^2} \right) \quad (8.25)$
```

以及

```
$b = \begin{cases} b_c & \text{if } |b_c - \sqrt{1.5}| < |b_e - \sqrt{1.5}| \\ b_e & \text{otherwise} \end{cases} \quad (8.26)$
```

其中

```
$b_e = \frac{x_0\sqrt{dt}}{\text{floor}(x_0/\sqrt{1.5})}, \quad b_c = \frac{x_0\sqrt{dt}}{\text{floor}(x_0/\sqrt{1.5} + 1)} \quad (8.27)$
```

$x_i$ 和 $v_i$ 的三项叉树均在零以下被截断（也可以在任意值以上进行截断，以减少计算时间）。$b$ 参数定义在 $1 \le b \le \sqrt{2}$ 范围内，其作用是收缩或扩展树，以确保 $x_i$ 树的最后一行正好为零。$v_i$ 的三项叉树通过将每个节点处 $x_i$ 的值代入方程 (8.20) 得到的。

# 股票价格的三项叉树

在方程 (8.13) 定义的变换后股票价格 $Y_i$ 的三项叉树中，允许跨越多个节点的跳转。$v_i$ 的高值会导致 $Y_i$ 跳跨越多个节点向上或向下，而 $v_i$ 的低值仅允许跨越单个节点。Beliaeva 和 Nawalka (2010) 将节点跨度定义为 $k\sigma_v(0)\sqrt{dt}$，它代表了当过程处于节点 $Y_i$ 时，$Y_{i+dt}$ 取值的节点之间的距离。$k_i = 1$ 代表跨越单个节点的跳转，而 $k_i > 1$ 代表跨越多个节点的跳转。该参数定义为

```
$k_i = \begin{cases} \text{Ceiling}(\sqrt{v_i/v_0}) & \text{if } v_i > 0 \\ 1 & \text{otherwise.} \end{cases} \quad (8.28)$
```

$Y_i$ 的多次跳跃如图 8.2 所示，该图重现了 Beliaeva 和 Nawalka (2010) 的表 3。左面板对应 $k_i = 1$ 的情况，类似于

![](img/bc3df3b6c26c2272307f56b6cf75ef87_228_0.png)

# 图 8.2 变换后股票价格的跳转

一个普通的三项叉树。右面板说明了 $k_t = 2$ 的情况。请注意，在两种情况下，树在每个时间步都会合并。
初始节点处树的时间零值由 $Y_0$ 给出，通过在方程 (8.13) 和 (8.14) 中设置 $t = 0$ 得到。在给定 $Y_t$ 的条件下，$Y_{i+dt}$ 的向上、中间和向下值为

```
$Y_{t+dt}^{u} = Y_t + (I + 1) \cdot k_t\sigma_y(0)\sqrt{dt}$,
$Y_{t+dt}^{m} = Y_t + I \cdot k_t\sigma_y(0)\sqrt{dt}$,
$Y_{t+dt}^{d} = Y_t + (I - 1) \cdot k_t\sigma_y(0)\sqrt{dt} \quad (8.29)$
```

其中 $I$ 是绝对值最接近的整数

```
$\frac{\mu_y(t)\sqrt{dt}}{k_t\sigma_y(0)}$
```

在这些表达式中，$\sigma_y(0)$ 是通过在方程 (8.16) 的 $\sigma_y(t)$ 中设置 $t = 0$ 得到的。向上、中间和向下的概率由给出

```
$P_y^u = \frac{1 \sigma_y^2(t)dt + e_u e_d}{2(k_t\sigma_y(0))^2dt}, P_y^m = \frac{\sigma_y^2(t)dt + e_u e_d}{2(k_t\sigma_y(0))^2dt}$,
$P_y^d = \dots$ (此处原文原文未写全，按逻辑保留)
```

$Y_i$ 的多次跳转如图 8.2 所示...（此处省略重复翻译，遵循不重复原文原则）

## 224
MATLAB 和 C# 中的 Heston 模型及其扩展

$S_t$ 的概率使用 Matlab 函数 `probY.m` 计算，该函数应用了方程 (8.30)。

```matlab
function [pu pm pd] = probY(Vt,V0,Yt,dt,rho,sigma,kappa)
% Equation 11
  if Vt > 0
    k = ceil(sqrt(Vt/V0));
  else
    k = 1;
  end
% Equations 9 and 6
muY = (rho/sigma*kappa - 0.5)*Vt;
sigymat = sqrt((1-rho)^2)*sqrt(Vt);
sigym0 = sqrt((1-rho)^2)*sqrt(V0);
% 根据方程 13 计算 Yu, Ym, Yd
I = (round(muY/k)/sigym0*sqrt(dt));
Y = Yt + (I+1)*k*sigym0(dt);
Ym = Yt + (I-0)*k*sigym0(dt);
Yd = Yt + (I-1)*k*sigym0(dt);
% Equations 17 and 16
eu = k*Vt - muY*dt;
em = Ym - Yt - muY*dt;
ed = Yd - Yt + muY*dt;
pu = 0.5*(sigma^2*dt + eu*ed)/k^2/sigma^2/dt;
pm = 0.5*(sigma^2*dt + eu*em)/k^2/sigma^2/dt;
pd = 0.5*(sigma^2*dt + eu*ed)/k^2/sigma^2/dt;
```

变换后的价格树 $Y_t$、股票价格 $S_t$ 以及美式和欧式价格均使用 `BuildBivariateTree.m` 函数构建。$Y_t$ 的结构是上三角，通过将 $Y_0$ 放置在 $Y_t$ 矩阵的左上角。第一个时间步的值放置在第二列的前九行，第二个时间步的值放在从顶部开始第三列，以此此类推。

该函数的第一部分生成方差树，找到每个 $v_i$ 节点处的 $k_i$ 值，并根据 $k_i$ 的最大值和该步方差节点的数量确定每个时间步所需的行数。每个节点处的 $k_i$ 值从方程 (8.28) 获取。

```matlab
function [EuroAmer Amer... Branch] = BuildBivariateTree(...)
dt = T/NT;
sigym0 = sqrt(1-rho^2)*sqrt(V0);
% Generate the volatility tree
[X RBound M] = BuildVolTree(...);
ColChange = RBound M + 2;
% 来自方程 (11) 的 k(t) 和 (14) 的 I(t)
k = zeros(2*NT-1,NT);
for t=1:NT
  for n=M-(t-1):M+(t-1);
```

### 美式期权

```matlab
if V(n,t) > 0
    k(n,t) = ceil(sqrt(V(n,t)/V0));
else
    k(n,t) = 1;
end
% Find树的维度
maxK = max(k);
numY = [1 3];
umV = [1 3];
umRows = [1 9];
for t=3:NT
```
