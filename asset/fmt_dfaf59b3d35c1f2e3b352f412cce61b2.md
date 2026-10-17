
`numY(t) = numY(t-1) + 2*maxK(t);`

`numV(t) = 2*t - 1;`

`numRows(t) = numV(t)*numY(t);`

end

`NR = max(numRows);`

```
该函数的下部分寻找每个节点的九个分支索引，并将它们存储在 Matlab 代码中。这些索引取决于 $Y_i$ 和 $k_i$ 的当前值。例如，在 Beliaeva 和 Nalwalkha (2010) 的表11 中，第一步的顶部节点（在图中标记为 $V_{11}, Y_{11}$）的跳跃大小 $k_{11}=2$。该节点分支到 $V_{21}$ 的节点 1, 3, 5，$V_{22}$ 的节点 8, 10, 12，以及 $V_{23}$ 的节点 15, 17, 19。这些节点间隔两个时间步。第一步的最后一个节点（标记为 $V_{13}, Y_{13}$）的跳跃大小 $k_{11}=1$。该节点分支到节点 17, 18, 19，节点 25, 26, 27 以及节点 32, 33, 34。这些节点间隔一个时间步。
```

```matlab
Branch = cell(numRows(NT-1),NT-1);

Branch(1,1) = {[1:9]};

B = zeros(numV(NT-1)*numY(NT-1), 9);

% To Branches

for t=2:NT

nY = numY(t);

First = max(K(t-1));

for n=1:numRows(t)

    a = cell(n-1,nY);

    b = mod(n-1,nY);

    % Find the-to-middle branches

    B(n,2) = First + (a-1)*numY(t) + b;

    B(n,5) = B(n,2) + numY(t);

    B(n,8) = B(n,2) + 2*numY(t);

    % Find the rest of branches

    B(n,1) = B(n,2) - a;

    B(n,4) = B(n,5) - a;

    B(n,6) = B(n,5) + a;

    B(n,7) = B(n,8) - a;

    B(n,9) = B(n,8) + a;

    Branch(n,t) = {B(n,:)};

end
```

```matlab
clear B;

% Adjust the last branch upward

for t=ColChange:NT-1

for j=7:9

 Branch(numRows(t),j) = Branch(t-1,j);
```

该函数的后续部分根据之前的分支创建 $Y_t$ 树，并根据方程 (32) 创建联合概率。在由时间（t循环）、方差（v循环）和变换后的价格（r循环）定义的每个节点处，需要若干数量：$Y_t$ 的当前值、$X_t$、$k_t$ 以及 $Y$ 演化到 $Y_{rd}$ 的分支索引。这些索引位于 MATLAB 数组中。在每个节点处，当 $Y_t > 0$ 时创建未来的 $Y_{rd}$；如果 $Y_t = 0$，则节点没有分支，并为每个联合概率分配零。在 Beliaeva 和 Nalwalkha (2010) 的表11 中，在第二步，没有分支源于节点 $(V_{24}, Y_{21})$$(V_{24}, Y_{27})$$(V_{25}, Y_{21})$ 或 $(V_{25}, Y_{27})$。在我们的符号中，这些是 $Y_t$ 矩阵的第22、28、29和35行。最后，存储联合概率。

```matlab
% Log stock tree (Yt), (St), and (Prob)

Yt = zeros(NR, NT);

Y0 = log(S0) - rho*V0/sigma;

Yt(1,1) = Y0;

Prob = cell(numRows(NT-1),NT-1);

X0 = X(M,1);

for t=1:NT-1

 j = 0;

 j=(t-1):(t-1);

 for j=1:numV(t)

 for r=1:numY

 n = r*Y;

 Vt = V(M,t);

 Xt = X(M-j), t);

 Kt = k*M(j,t);

NewBranch = cell2mat(n,t);

muy = (rho*kappa/sigma - 0.5)*Vt;

 I = round(muy/K/sigym0*sqrt(dt));

 if Yt(n,t) > 0

 for s=1:9

 iff s=5 || s=8 || Middle node

 Yt(NewBranch(s),t+1) = Yt(n,t) + (I+0)...

 elseif s=1 || s=4 || s=7 % Up node

 Yt(NewBranch(s),t+1) = Yt(n,t) + (I+1)...

 elseif s=3 || s=6 || s=9 % Down node

 Yt(NewBranch(s),t+1) = Yt(n,t) + (I-1)...

 end

end

end
```

```matlab
Branch(n,t) = {{['No branch from ('...)]};

end

if Yt(n,t) == 0;

    Prob(n,t) = {zeros(1,9)};

else

    [pvm pvmd] = probV(Vt,X0,...);

    [pyu pymd] = probY(Vt,V0,...);

    Prob(n,t) = {pvm*pvmd, pyu*pymd};

end
```

## Medvedev-Scaillet 展开

Medvedev 和 Scaillet (2010) 开发了一种方法，可以将美式看跌价格作为渐近展开进行解析表示。他们的方法适用于这类随机波动模型。在本节中，我们首先介绍了 Black-Scholes 模型下美式看跌期权的方法，然后给出了 Heston 模型的展开。他们方法的优点是美式看跌价格可以通过仅解析项的展开获得。因此，该方法能够快速地生成 Black-Scholes 和 Heston 期权价格。

为了说明，我们重现了 Clarke 和 Parrot (1999) 以及 Ikonen 和 Toivaren (2008) 的美式价格。使用 50 个时间步和控制变量技术，我们获得了 1.96724、1.105853、0.519488、0.213408 和 0.081948，其中精度小于一个美分。

### 美式期权

## Medvedev-Scaillet 的 Black-Scholes 方法

在 Black-Scholes 模型的假设下，到期时间为 $\tau = T - t$ 的美式看跌期权在时间 $t$ 的价格 $P(S(t), t)$ 遵循偏微分方程 (PDE)：

```
$P_t + (r - q)SP_S + \frac{1}{2}\sigma^2S^2P_{SS} - rP = 0 \quad (8.35)$
```

其边界条件为：

```
$P(\infty, t) = 0$
$P(S(T), T) = \max(K - S(T), 0)$
$P(\tilde{S}(t), t) = \max(K - \tilde{S}(t), 0)$
$P_S(\tilde{S}(t), t) = -1 \quad (8.36)$
```

其中 $\tilde{S}(t)$ 是提前行权价格，例如 Albanese 和 Compoletti (2006)。在方程 (8.35) 和 (8.36) 中，下标表示求导，$r$ 和 $q$ 分别为无风险利率和股息率，sigma$ 是股票波动率。

Medvedev 和 Scaillet (2010) 通过修改后的价格 $P(\theta, \tau) = P(Ke^{-\theta\sqrt{\tau}}, \tau)$ 构建了方程 (8.35) 的一个修改版本，其中 $\theta$ 是归一化深度值值（moneyness）：

```
$$\theta = \frac{\ln(K/S)}{\sigma\sqrt{\tau}} \quad (8.37)$$
```

修改后的 PDE 版本仍然遵循方程 (8.35)，但将 (8.36) 中的最后一个条件替换为提前行权价格 $\tilde{S}(\tau) = Ke^{-\theta\sqrt{\tau}}$。该修改后问题的唯一解是障碍期权的价格，该期权在 $\theta$ 达到障碍水平 $y$ 时被即刻执行，其中 $y \approx 2$。

通过应用链式法则并使用 PDE (8.35)，可以直接得到用 $P(\theta, \tau)$ 表示的修改后 PDE (8.35)：

```
$$\theta P_\theta + P_{\theta\theta} + \frac{1}{\sigma}[a^2 + 2(q - r)]P_\theta\sqrt{\tau} - 2(P + rP)\tau_\tau = 0 \quad (8.38)$$
```

同样，下标表示求导。修改后 PDE 的边界条件为：

```
$P(-\infty, \tau) = 0,$
$P(y, \tau) = K(1 - e^{-y\sqrt{\tau}}) \quad (8.39)$
```

Medvedev 和 Scaillet (2010) 的主要结果是修改后 PDE (8.38) 的解为级数：

```
$P(\theta, \tau) = \sum_{n=1}^{\infty} P_n(\theta)\tau^{n/2} \quad (8.40)$
```

对于 $i = 0, 1, 2, \dots$。$x_{n,j+1}^0$ 对 $\pi_{n,j}^0$ 的依赖关系。获取 $p_n^\theta$ 和 $q_n^\theta$ 通过直接应用 (8.45) 完成。这些多项式在 $n \leq 7$ 时的系数出现在表 8.1 和 8.2。

### 美式期权

**表 8.1** 多项式 $p_n^0$ 的系数

| N | $\theta^7$ | $\theta^6$ | $\theta^5$ | $\theta^4$ | $\theta^3$ | $\theta^2$ | $\theta^1$ | $\theta^0$ |
|---|---|---|---|---|---|---|---|---|
| 1 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 |
| 2 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 1 |
| 3 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 3 |
| 4 | 0 | 0 | 0 | 1 | 0 | 6 | 0 | 3 |
| 5 | 0 | 0 | 0 | 1 | 10 | 0 | 15 | 0 |
| 6 | 0 | 1 | 0 | 15 | 0 | 45 | 0 | 15 |
| 7 | 1 | 0 | 21 | 0 | 105 | 0 | 105 | 0 |

**表 8.2** 多项式 $q_n^0$ 的系数

| N | $\theta^7$ | $\theta^6$ | $\theta^5$ | $\theta^4$ | $\theta^3$ | $\theta^2$ | $\theta^1$ | $\theta^0$ |
|---|---|---|---|---|---|---|---|---|
| 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 |
| 2 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 2 |
| 3 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 5 |
| 4 | 0 | 0 | 0 | 0 | 1 | 0 | 9 | 8 |
| 5 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 8 |
| 6 | 0 | 0 | 1 | 0 | 14 | 0 | 33 | 0 |
| 7 | 0 | 0 | 1 | 0 | 20 | 0 | 87 | 48 |

多项式 $p_n^k$ 和 $q_n^k$ 的形式为：

```
$p_n^0(\theta) = \pi_{n0}^0\theta^n + \pi_{n1}^1\theta^{n-2} + \pi_{n2}^2\theta^{n-4} + \dots$
$q_n^0(\theta) = \chi_{n0}^0\theta^{n-1} + \chi_{n1}^1\theta^{n-3} + \chi_{n2}^2\theta^{n-5} + \dots \quad (8.46)$
```

其中 $\pi_{n0}^0 = x_{n0}^0$ 和 $q_{n0}^0$ 较为复杂，通过将单独方程代入 PDE (8.35) 完成。将级数 (8.40) 以 $\tau^{n/2}$ 的项代入 (8.38)，得到 Medvedev 和 Scaillet 的方程 (29)：

```
$-nt_{n0} + \theta P_{n-1} - 2rP_{n-2} = 0 \quad (8.47)$
```

其中 $\tilde{\sigma} = \sigma$。(8.47) 的解通过将 PDE 分为齐次和非齐次部分得到：

1. (8.47) 的齐次部分为 $P_n^0(\theta)$。
2. (8.47) 的非齐次部分为 $P_n(\theta) = P_n^0(\theta) + P_n^1(\theta)$。

(8.47) 的齐次部分涉及 $P_n$ 及其导数。在非齐次部分中，代入 (8.41) 中的 $P_n^1(\theta)$ 并使用 (8.43) 中的导数得到：

```
$(p_{n0}^1 + \theta p_{n0}^1)\Phi(\theta) + ((n+1)q_{n0}^1 - \theta q_{n0}^1)\phi(\theta) = 0 \quad (8.48)$
```

在 (8.47) 的非齐次部分（涉及 (8.47) 左侧的最后两项）中，代入 $P_n(\theta) + P_n^1(\theta)$ 并应用链式法则得到：

```
$(C_{n-1}p_{n-1}^{n-1} + \sigma_{n-1}p_{n-1}^{n-1} - 2rp_{n-2}^{n-2})\Phi(\theta) + (C_{n-1}q_{n-1}^{n-1} - \sigma_{n-1}q_{n-1}^{n-1} - 2rq_{n-2}^{n-2})\phi(\theta) = 0$
```

将 (8.48) 和 (8.49) 重新分组为共同项 $\Phi(\theta)$ 和 $\phi(\theta)$，得到方程组：

```
$p_{n-\theta}^n + \theta p_{n-\theta}^{n-1} + \sigma_{n-1}p_{n-\theta}^{n-1} + C_{n-1}p_{n-\theta}^{n-2} - 2r(C_{n-2}^{n-2} + p_{n-2}^{n-2}) = 0,$
$(n+1)q_{n-\theta}^n + q_{n-\theta}^{n-1} + 2p_1^n C_{n-1}(p_{n-\theta}^{n-1} + q_{n-\theta}^{n-2}) - \theta q_{n-1}^{n-1} + (p_{n-1,\theta} - \sigma_{n-1}q_{n-1,\theta}^{n-1} - 2rq_{n-2}^{n-2} + 2rq_{n-2}^{n-2})\phi(\theta) = 0 \quad (8.50)$
```

对于每个 $n$，求解 (8.50) 中的第一个 PDE 得到 $q_n^n$；所有其他量的情况类似，求解 (8.50) 中的第二个 PDE 得到 $p_n^n$。在本节末尾，我们可以使用 Matlab 中的符号方法。

一旦通过 (8.50) 中的两个 PDE 得到多项式 $q_n^n$ 和 $p_n^n$，就可以通过在 $\theta$ 处评估 (8.40)，代入 (8.39) 中 $e^{-\gamma y^2}$ 的泰勒展开，并等两个 $\tau^{n/2}$ 的连续幂次获得系数 $C_n$。消去两边的 $\tau^{n/2}$ 后，产生以下结果，可以很容易求解出 $C_n$：

```
$C_n[p_n^n(\Phi) + q_n^n(\phi) + p_n^n(\tilde{\theta}) + q_n^n(\tilde{\theta})] = (-1)^{n+1}\sigma^ny^n/n! \quad (8.51)$
```

当 $\Phi(\theta) = \Phi(\tilde{\theta})$ 和 $\phi(\theta) = \phi(\tilde{\theta})$ 分别是 $\theta = \tilde{\theta}$ 处的标准正态分布和密度函数时，优化值从 (8.42) 得到。例如，当 $n=1$ 时，我们看到 $p_1^1 = \theta, q_1^1 = 1$ 且 $p_1^1 = 0$。此处得到 $C_1$：

```
$C_1 = \frac{K\sigma}{\Phi(\theta) + \phi(\theta)} \quad (8.52)$
```

## 234 MATLAB 和 C# 中的 HESTON 模型及其扩展

```matlab
for i=1:N

for k=1:N-i+2

    pi(i,k) = 0;

end

j = N-i+3;

k = 1;

while j<=N+1

    pi(i,j) = pis(i,k);

    k = k+1;

    j = j+2;

end

n = dot(pi(n,:),'theta);

% 生成多式 qln

syms qill12 qill13 qill14 qill15 qill16 qill17; % 根据需要添加更多

qis = [qill12 qill13 qill14 qill15 qill16 qill17]; ...

syms qi

for i=1:N

for k=1:N-i+3
```
