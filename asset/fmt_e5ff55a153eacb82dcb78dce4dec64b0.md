
已经提出了几种算法来利用 `$L$` 的稀疏性以加速求。参考 `Duffy (2006)`。向量 `U^0` 取于定价。对于看涨期权，它在 `U` 中对应 `S > K` 的部分包含 `S-K`，在对应 `S < K` 的部分包含零。这些项在向量中出现的顺序取决于 `U` 组件的排列。

若干有限差分方案根据 `theta` 的值产生方程 `(10.11)` 的特例。设置 `theta=0` 产生显式方案，`theta=1/2` 产生 `Crank-Nicolson` 方案，`theta=1` 产生隐式方案。见 `Kluge (2002)` 关于加权方法的通用开发以及当 `N` 很大时可能出现的数值问题的讨论。显式方案在数值上最易处理；当我们在 `(10.12)` 中设置 `theta=0` 时，不再需要矩阵逆。`L` 是一个维度为 `N=(N_s+1)(N_v+1)` 的方阵，其行和列取决于向量 `U^v` 如何构造。通过堆叠图 `10.2` 中的 `N_v` 个列向量 `u_0,u_1,...,u_{N_v}`，`L` 的行和列对应于 `(10.9)` 中向量 `U^v` 的项。

我们通过将 `L` 中的 `partial/partial v` 替换为两个部分来修改方程 `(10.3)` 中算子的 `L`：

```
$$L = \frac{1}{2}vS^2\frac{\partial^2}{\partial S^2} + \frac{1}{2}\sigma^2\frac{\partial^2}{\partial v^2} + \rho vS\frac{\partial^2}{\partial S\partial v} + (r-q)S\frac{\partial}{\partial S} + \theta\frac{\partial}{\partial \theta} - \dots$$
```
（注：由于原文文本在此处中断，此处根据提供的文本内容翻译至此）

`U^n` 中的点 `(S_i, v_{j-1})` 和 `(S_i, v_{j+1})` 分别位于 `(S_i, v_j)` 上、下方 `N_V+1` 个位置，如方程 `(10.16)` 所示。

| | `u_0` | 列向量 0 |
|---|---|---|
| | ... | |
| | : | |
| `U^n_{i,j-1}` | 列向量 `j-1` | `r-N_S-1` |
| | : | |
| | : | |
| `U^n` = `U^n_{i,j}` | 列向量 `j` | `r` (10.16) |
| | : | |
| | : | |
| `U^n_{i,j+1}` | 列向量 `j+1` | `r+N_S+1` |
| | : | |
| | : | |
| `u_{NV}` | 列向量 `N_V` | |

因此，`L_{\mu 2}` 的元素如下所示：

`L_{\mu 2}(r-N_S-1, c) = \frac{-1}{2dv} \times v_i`
`L_{\mu 2}(r, c) = 0` (10.17)
`L_{\mu 2}(r+N_S+1, c) = \frac{1}{2dv} \times v_j`。

当使用非均匀网格时，(10.17) 分母中的 `2dv` 被替换为 `(v_{i+1}-v_{j-1})`。
`Matlab` 函数 `BuildDerivatives.m` 是一个创建 `L` 子矩阵的程序。它需要三个网格作为输入：分别对应股价、波动率和到期日。它假设这些网格是使用均匀网格构建的。为了节省空间，我们仅展示最核心部分。
第一部分识别了 `U` 中对应于 `S` 和 `v` 边界点的元素。

```matlab
function [derS ... derS RV] = BuildDerivatives(S,V,T)
N = NS*NV;
Si = repmat(S',NV,1);
Vi = reshape(kron(V,ones(NS,1)),N,1);
```

## 有限差分方法

```matlab
VminB = zeros(N,1); VmaxB = zeros(N,1);
SminB = zeros(N,1); SmaxB = zeros(N,1);
VminB(1:NS-1) = 1;
VmaxB(N-NS+2:N) = 1;
for i = 1:N
  if mod(i,NS)==0 && (i~N)
    SmaxB(i) = 1;
  end
  if mod(i,NS)==1 && (i~1)
    SminB(i) = 1;
  end
end
```

第二部分识别了非边界点，并确定 `U` 的哪些元素接收前向、后向或中心差分。

```matlab
NB = zeros(N,1);
for b=2:NV-1
  for k=b*NS-(NS-2):b*NS-2
    NB(k) = 1;
  end
end
% (剩余逻辑逻辑)
Cs = zeros(N,1); % 中心差分
Fs = zeros(N,1); % 前向差分
Bs = zeros(N,1); % 后向差分
for b=2:NV-1
  for k=b*NS-(NS-3):b*NS-2
    Cs(k) = 1;
  end
end
Fs((2:NV-1)*(NS-2):2*NS-1) = 1;
Bs((2:NV-1)*NS-1) = 1;
Cv = zeros(N,1); % 中心差分
Fv = zeros(N,1); % 前向差分
Bv = zeros(N,1); % 后向差分
for b=3:NV-2
  for k=b*NS-(NS-2):b*NS-1
    Cv(k) = 1;
  end
end
Fv(2*NS-(NS-2):2*NS-1) = 1;
Bv((N-1)*NS-(NS-2):(N-1)*NS) = 1;
Csv = zeros(N,1);
for b=2:NV-1
  for k=b*NS-(NS-2):b*NS-1
    Csv(k) = 1;
  end
end
```

## 312 MATLAB 和 C# 中的 HESTON 模型及其扩展

最后部分遍历识别出的点，并将中心差分、前向差分或后向差分的系数分配给每个一阶和二阶矩阵。为了节省空间，仅显示了内部的中心差分。

```matlab
I = find(Cs=1)
for k=1:length(I)
% 创建 S 导数矩阵
ders1(I(k),I(k)-1) = -1/2/ds * Si(I(k))
ders1(I(k),I(k)) = 0
ders1(I(k),I(k)+1) = 1/2/ds * Si(I(k))
ders2(I(k),I(k)-1) = -1/2/ds * Si(I(k))
ders2(I(k),I(k)) = -2/ds * Si(I(k))
ders2(I(k),I(k)+1) = 1/2/ds * Si(I(k))
end
I = find(Cv=1)
for k=1:length(I)
% 创建 V 导数矩阵
dver1(I(k),I(k)-NS) = -1/2/dv
dver1(I(k),I(k)) = 0
dver1(I(k),I(k)+NS) = 1/2/dv
dver2(I(k),I(k)-NS) = -1/2/dv * Vi(I(k))
dver2(I(k),I(k)) = 0
dver2(I(k),I(k)+NS) = 1/2/dv * Vi(I(k))
dver3(I(k),I(k)-NS) = -2/dv^2 * Vi(I(k))
dver3(I(k),I(k)+NS) = 1/dv^2 * Vi(I(k))
end
I = find(Sv=1)
for k=1:length(I)
% 创建 SV 导数矩阵
dsv1(I(k),I(k)+NS-1) = 1/(4*ds*dv) * Vi(I(k))
dsv1(I(k),I(k)-NS-1) = -1/(4*ds*dv) * Vi(I(k))
dsv2(I(k),I(k)+NS-1) = 1/(4*ds*dv) * Vi(I(k))
dsv2(I(k),I(k)-NS-1) = -1/(4*ds*dv) * Vi(I(k))
end
```

`BuildDerivatives` 函数用于 `WeightedMethod` 中，它应用方程 `(10.12)` 并每一步更新 `U`。通过在目标点 `(S_0, v_0)` 处对 `U` 进行插值返回导数值。

```matlab
function WPrice = WeightedMethod(...
nu = zeros(NS*NV,1);
Si = repmat(S',NV,1);
U = max(0, S - K);
for t=2:NT
nu = U;
```

![](img/bc3df6c26c22307f56b75ef87_319_0.png)

## 有限差分方法

```matlab
if the=0
    U = B*u; % 显式方法
elseif the=1
    U = invA*u; % 隐式方法
else
    U = A*B*u; % 加权方法
end
U = reshape(U,NS,NV); interp2(V,S,U,V0,S0);
```

为了说明加权方法，我们使用 `Foulon (2010)` Case 1 中定义的参数值：`kappa = 1.5, theta = 0.04, sigma = 0.3, rho = -0.9, r = 0.02, lambda = 0.05`，以及行权价 `K = 100`。此外，我们使用 `v_0 = 0.05`，到期时间 `tau = 0.15` 年。我们希望在波动率 `v = 0.05412` 时获得现价 `S = 101.52` 处的价格。以下 `Matlab` 代码构建了 `40 × 40` 的均匀网格并使用 20 个时间步。它从同一个 `WeightedMethod.m` 函数获取显式、隐式和 `Crank-Nicolson` 方案的价格，但参数 `theta` 的设置不同。

```matlab
nS = 39; % 股价
V = 39; % 波动率
nT = 19; % 到期日
[derS derV1 derV2 derVV derSV] = BuildDerivatives(S,V,T);
L = (r-q).*derS + kappa.*theta.derV1 - kappa.*derV2 + ...
I = q*(NS*NV);
S0 = 101.52;
V0 = 0.05412;
thet = 0;
A = (I - .thet.*dt.*L);
B = (I + (1-.thet).*dt.*L);
inA = inv(A);
Price = WeightedMethod(the,S0,V0,K,S,V,T,A,invA,B);
```

在这个示例中，使用 `Heston` 解析解得的精确价格为 4.1086。显式方案价格为 4.1679，正如预期，由于步数较少，近似效果较。隐式和 `Crank-Nicolson` 方案分别产生了 4.1023 和 4.1350，两者都更准确。

`Matlab` 函数 `BuildDerivativesNonUniform.m` 是 `BuildDerivatives.m` 函数的一个版本，它接受非均匀网格并返回 `L` 的子矩阵。

```matlab
function [derS derV1 derV2 derVV derSV] = BuildDerivativesNonUniform(S,V,T)
% (函数实现略)
```

# 316 MATLAB 和 C# 中的 HESTON 模型及其扩展

我们可以对 `partial U/partial S` 使用中心差分：

```
$\frac{\partial U}{\partial S}(S_i, 0, t_n) = \frac{U_{i+1,0}^n - U_{i-1,0}^n}{S_{i+1} - S_{i-1}}$
```

但对于 `partial U/partial v`，我们必须使用前向差分，例如简单形式：

```
$\frac{\partial U}{\partial v}(S_i, 0, t_n) = \frac{U_{i,1}^n - U_{i,0}^n}{v_1 - 0}$
```

因为 `v_0 = 0`。请记住，在此语境下，我们使用 `v_0` 表示方差网格上的第一个点，而不是现量波动的 `Heston` 参数。子矩阵 `L_{S,S}, L_{S,v}` 和 `L_{v,v}` 在边界点处值为零。

## 显式格式 (EXPLICIT SCHEME)

当网格均匀时，显式格式对产生产生一个非常简单的 PDE 表达式。它是加权平均法的一种特例，通过在方程 `(10.11)` 中设置 `theta=0` 得到：

```
$U^{n+1} = (I + dtL)U^n$.
```

给定矩阵 `L_i`，我们可以直接从 `U^n` 获得 `U^{n+1}`，而不需要矩阵逆。`U^{n+1}` 中对应于 `U_{i,j}^n` 的元素为：

```
$U_{i,j}^{n+1} = U_{i,j}^n + dt \left[ \frac{1}{2}S_i^2 \frac{\partial^2 U}{\partial S^2} + \frac{1}{2}\sigma_j^2 \frac{\partial^2 U}{\partial v^2} + \rho v_j S_i \frac{\partial^2 U}{\partial S \partial v} + (r-q)S_i \frac{\partial U}{\partial S} + \kappa(\theta - v_j) \frac{\partial U}{\partial v} \right] U_{i,j}^n$
```

这是使用显式格式为美式期权的示例。我们在第 8 章遇到过，当我们使用显式格式时，为了实现这一点，必须代入导数的有限差分近似。当对 `(S_j, v_j)` 使用均匀网格时，会出现最简单的实现方式。在这种情况下，`U_{i,j}^n` 的表达式可以简化为仅包含参数、索引值、与 `U_{i,j}^n` 相邻的点以及增量的简单表达式。我们将均匀网格下的导数近似值代入，得到：

```
$U_{i,j}^{n+1} = U_{i,j}^n + dt \left[ \frac{1}{2}S_i^2 \frac{U_{i+1,j}^n - 2U_{i,j}^n + U_{i-1,j}^n}{(dS)^2} + \frac{1}{2}\sigma_j^2 \frac{U_{i,j+1}^n - 2U_{i,j}^n + U_{i,j-1}^n}{(dv)^2} + \rho v_j S_i \frac{U_{i+1,j+1}^n - U_{i+1,j-1}^n - U_{i-1,j+1}^n + U_{i-1,j-1}^n}{4 ds dv} \right] + \rho v_j S_i \frac{U_{i,j+1}^n - U_{i,j-1}^n}{2 dv} + \frac{1}{2}\sigma^2 v_j \frac{U_{i+1,j}^n - U_{i-1,j}^n}{2 ds} + \kappa(\theta - v_j) \frac{U_{i,j+1}^n - U_{i,j-1}^n}{2 dv} ] U_{i,j}^n$
```

## 有限差分方法

合并同项并简化，注意 `S_i = i × ds` 且 `v_j = j × dv`，可以得到：

```
$U_{i,j}^{n+1} = \left[ 1 - dt (\rho jdv + \frac{\sigma_j^2}{dv} + r) \right] U_{i,j}^n + \left[ \frac{dt}{2} (ijdv - r + q) \right] U_{i-1,j}^n + \left[ \frac{dt}{2} (ijdv + r - q) \right] U_{i+1,j}^n + \left[ \frac{dt}{2dv} (\sigma_j^2 - \kappa(\theta - idv)) \right] U_{i,j-1}^n + \left[ \frac{dt}{2dv} (\sigma_j^2 + \kappa(\theta - idv)) \right] U_{i,j+1}^n + \frac{ijt\sigma}{4} (U_{i-1,j+1}^n + U_{i+1,j-1}^n - U_{i-1,j-1}^n - U_{i+1,j+1}^n). (10.20)$
```

`Matlab` 函数 `HestonExplicitPDE` 返回包含所有 `U_{i,j}` 的矩阵。所有 `t < N` 的中间值 `U_{i,j}` 都被丢弃。该函数需要 `S, v` 网格作为输入。为了节省某些步骤，函数已被移除：

```matlab
function U = HestonExplicitPDE(params,...)
for s=1:NS
  for v=1:NV
    U(s,v) = max(S - K, 0);
  end
for t=1:NT-1
  for v=1:NV
    U(s,v) = 0;
    U(NS,v) = max(0, Smax - K);
  end
  for s=1:NS
    U(s,v) = max(0, S(s) - K);
  end
  u = U % 更新临时网格 u(s,t)
  for s=2:NS
    DeV = (u(s,2) - u(s,1)) / dv;
    DeS = (u(s,1) - u(s-1)) / ds;
    U(s,1) = u(s,1)*(1 - r*dt - kappa*theta*dt/dv);
  end
  u = U;
  for v=2:NV-1
    A = (1/2*dt*(s-1)^2*(v-1)/dv - sigma^2*dv);
```
