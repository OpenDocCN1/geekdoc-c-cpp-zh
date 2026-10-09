
变换 $\hat{w}(k)$ 定义在区域 $S_w$ 中，对于看涨期权，我们有 $S_w^{call}=\{k: k_i > 1\}$，对于看跌期权，我们有 $S_w^{put}=\{k: k_i < 0\}$，如下文所示

# 期权定价的基本变换

## 103

$k = \text{Im}[k]$

![](img/bc3df3b6c26c2272307f56b6cf75ef87_113_0.png)

图 4.2 看涨期权的积分带

在本章较早部分，特征函数 $\varphi(k)$ 在带 $S_X$ 内正则，该带 $S_X$ 跨越实轴反射并沿虚轴翻转。结论是方程 (4.28) 中的积分定义在这两个区域的交集上，即 $S_0 = S_X \cap S_{-X}$。对于看涨期权，我们有 $S_T^{call}=\{k: 1 < k_i < \beta\}$，如图 4.2 所示。

同理，对于看跌期权，我们有 $S_T^{put}=\{k: \alpha < k_i < 0\}$。Lewis (2001) 使用 (4.23) 中 Parseval 等式的复数形式提供了另一种推导方法。令 $s_T = \ln S_T$，$s_0 = \ln S_0$，累积分布函数 $Q(x|s_0) = \text{Pr}(s_T < x)$ 和 $P(x) = \text{Pr}(X_T < x)$。利用 $Y = s_0 + (r - q)T$，可以直接证明 $q(x|s_0) = p(x - Y)$，其中 $q$ 和 $p$ 分别对应于 $Q$ 和 $P$ 的密度。利用傅里叶变换的定义，通过变量换计算积分，并记得 $s_T = Y + X_T$，我们：

$\hat{q}(k|s_0) = \int_{ik_{-\infty}}^{ik_{\infty}} e^{iks_T} q(s_T|s_0) ds_T = \int_{ik_{-\infty}}^{ik_{\infty}} e^{ik(Y+X_T)} p(X_T|s_0) dX_T = e^{ikY}\hat{p}(k)$。

此外，我们可以写为 $\hat{q}(k|s_0) = e^{ikY}\varphi(k)$，因为 $\hat{p}(k)$ 是 $X_T$ 的特征函数，我们记为 $\varphi(k)$。注意 $\hat{q}(k|s_0)$ 是 $s_T = \ln S_T$ 的特征

## MATLAB 和 C 中的 Heston 模型及其扩展

### 104

通过应用方程 (4.22) 中的 Parseval 等式，我们有：

```
$U(S_0) = e^{-rT} E[w(x)] = e^{-rT} \int_{-\infty}^{\infty} q(s_0)w(x)dx\n= \frac{e^{-rT}}{2\pi} \int_{ik_0}^{ik_{\infty}} \hat{q}(-ks_0)\hat{w}(k) dk\n= \frac{e^{-rT}}{2\pi} \int_{ik_0}^{ik_{\infty}} e^{-ikY}\varphi(-k)\hat{w}(k) dk. \ (4.30)$
```

代入收益变换 $\hat{u}(x)$ 可产生对应于那些收益的定价公式。看涨期权的收益变换 $\hat{u}(x)$ 由方程 (4.2) 给出。这里，看涨价格 $C(S_0)$ 通过将 $\hat{u}(x)$ 代入 (4.30) 得到：

```
$C(S_0) = \frac{e^{-rT}}{2\pi} \int_{ik_0}^{ik_{\infty}} e^{-ikY}\varphi(-k)\hat{w}(k) dk$
```

（注：此处根据上下文逻辑补全了原文截断的公式含义，但严格遵循指令不翻译代码块，仅翻译描述部分。由于原文文本在输入处被截断，翻译也随在提供的文本处结束。）

## 106 HESTON 模型及其在 MATLAB 中的扩展

最后，Lewis (201) 显示，如果将积分路径移动到 $v_t \in (\alpha, 0)$，且 $\alpha < 0$，则两个极点都被包含在内，如图4 中的 $\mathcal{C}$ 所示。再次应用留数定理，$C(S_0)$ 等于沿新路径的积分减去 $2\pi$ 乘以留数之和。

```math
$$\hat{u}(k) = \frac{K^{k+1}}{k^2-ik}$$
```

```text
这与看权公式相同，只是允许区域为 $k<0$。因此，当我们在方程 (31) 中取 $v_t$ 路径时，我们得到了期权的价值 $P(S_0)$。根据留数定理，看权是方程 (31) 中沿路径的积分加上 $2\pi$ 乘以留数之和
```

```math

$C(S_0) = P(S_0) + 2\pi \frac{S_0 e^{-rT}}{2\pi} - Ke^{-rT}$

```

```text

这正是看权与跌权期权的平价关系。
```

如果我们在方程 (32) 中选择 $v_t = \frac{i}{2}$，那么我们在图4 的两个极点之间进行积分。令 $k=u+\frac{i}{2}$ 使得 $k^2-ik=u^2+1/4$，我们可以将 (32) 表示为：

```math
$C(S_0) = S_0 e^{-rT} - \frac{Ke^{-rT}}{2\pi} \int_{1/2}^{\infty} e^{-(u+\frac{i}{2})\varphi W} \varphi(-u-\frac{i}{2}) \frac{du}{u^2+1/4}$
$$\= S_0 e^{-rT} - \frac{\sqrt{KS_0} e^{-(r-q)T/2}}{2\pi} \int_{1/2}^{\infty} e^{iu\varphi W} \varphi(-u+\frac{i}{2}) \frac{du}{u^2+1/4}$$
```

```text
第一行使用 $u$ 和 $W$ 替换 $k$，且 $W=\ln(S_0/K)+(r-q)T$，而最后一行使用了：
```

```math

$$\text{Re}[e^{-iu\varphi W} \varphi(-u-\frac{i}{2})] = \text{Re}[e^{iu\varphi W} \varphi(-u+\frac{i}{2})].$$

```

```text

从方程 (25) 可知 $\ln S_T=\ln S_0+(r-q)T+X_T=Y+X_T$。为了实现方程 (33) 中的看权价格，像我们在 (29) 中那样编写 $X_T$ 的函数是有用的，即：
```

```math
$$\varphi(u) = E[e^{iuX_T}] = f_2(u)e^{-iuY} (34)$$
```

```text
其中 $f_2(u)$ 是在 $u$ 处的 Heston 特征函数。
```

# 期权定价的基本变换

以下 Matlab 代码实现了方程 (33) 中的看权价格。Matlab 函数 `LewisIntegrand311.m` 根据 (34) 使用 $f_2(u)$ 计算 $\varphi(u)$。该函数的部分内容稍后给出。由于在该函数中使用 $i/2$，在最后部分，我们需要从 $u$ 中移除 $i/2$，以便在函数的最后行正确计算 $e^{iuW}$ 和 $u^2$。

```matlab

function y = LewisIntegrand311(u,...)

% ln S(T) 的 Heston 特征函数

ClnInst = exp(C + D*v + i*u*x);

% XT 的特征函数

Y = log(S) + (r-q)*tau;

CFXT = exp(i*u*Y)*ClnInst;

% 积分因子

u = u + i/2;

W = Y - log(K);

y = exp(i*u*W)*CFXT/(u^2 + 1/4);

```

```text

函数 `LewisPrice311.m` 使用传入的积分权重 $w$ 计算看权价格。它与本章之前介绍的 `HestonCallPrice.m` 类似，但向积分器传递了积分点 $u_i = x_i - i/2`。
```

```matlab
function y = LewisPrice311(...)
lambda = 0;
Y = log(S) + (r-q)*T;
W = Y - log(K);
% 计算积分
for j=1:length(x)
u = x(j) - (1/2)*i;
int(j) = w(j)*LewisIntegrand311(u);
end
Integral = sum(int);
% Lewis (2001) 中的方程 (3.11)
y = S*exp(-q*T) - (1/pi)*sqrt(K*S)*exp(-(r+q)*T/2);
```

```text
实现方程 (33) 看权的 C 代码在此未给出。为了说明，我们使用与表41相同的设置，通过 (33) 生成从 $K=95$ 到 $K=105$ 的看权价格。我们使用 32 点 Laguerre 积分通过原始 Heston (1993) 和 Lewis (2001) 的方程 (3.11) 获取看权价格。表4 中的结果显示两者之间高度一致。
```

# 表42 看权价格比较

| 权价 | 方程 (33) | 原始 Heston | 百分误差 |
| :--- | :--- | :--- | :--- |
| 95 | 7.9798 | 7.9835 | 0.047 |
| 96 | 7.3047 | 7.3085 | 0.052 |
| 97 | 6.6618 | 6.6665 | 0.057 |
| 98 | 6.0520 | 6.0559 | 0.064 |
| 99 | 5.4763 | 5.4802 | 0.072 |
| 100 | 4.9350 | 4.9391 | 0.081 |
| 101 | 4.4286 | 4.4327 | 0.092 |
| 102 | 3.9571 | 3.9613 | 0.105 |
| 103 | 3.5201 | 3.5244 | 0.120 |
| 104 | 3.1173 | 3.1216 | 0.138 |
| 105 | 2.7477 | 2.7521 | 0.158 |

# 波动率展开

Lewis (2000) 推导了适用于一般随机波动率模型的看权价格和隐含波动率的波动率序列。在本节中，我们仅介绍 Heston 模型的展开。使用这种方法获取 Heston 看权价格非常快，因为不需要数值积分。名称源于两个展开都是波动率参数 $\sigma$ 的幂次。第一个序列基于平均方差 $\bar{v}$ 处 Black-Scholes 价格的展开：

```math

$C_{BS}(S_0, \bar{v}, T) = S_0e^{-qT}\Phi(d_1) - Ke^{-rT}\Phi(d_2) \quad (35)$

```

```text

其中
```

```math
$d_1 = \frac{\log(S_0/K) + (r - q + \frac{\bar{v}}{2})T}{\sqrt{\bar{v}}}$
```

```text
且 $d_2 = d_1 - \sqrt{\bar{v}}$。量 $\bar{v}$ 表示第2章遇到的 CIR 过程在 $(0, T)$ 上的平均期望方差：
```

```math

$$\bar{v} = \frac{1}{T} \int_0^T v_t dt = \frac{1}{T} \int_0^T E[v_t|v_0] \quad (36)$$

$$\= \frac{1}{T} \int_0^T [\theta + (v_0 - \theta)e^{-\kappa t}]dt = (v_0 - \theta) \frac{1 - e^{-\kappa T}}{\kappa T} + \theta.$$

```

```text

期望方差 $\bar{v}$ 是 Heston 模型中方差交换的公平执行价，正如 Gatheral (2006) 所示，他在第2章中标记 $K_{var}^2 = \hat{w}/T$。第一个序列展开使用了 Black-Scholes 价格对于方差 $v$ 的导数，再次在 $\bar{v}$ 处求值：
```

```math
$C_v(S_0, \bar{v}, T) = \sqrt{\frac{T}{8\pi\bar{v}}} S_0e^{-qT} \exp\left(-\frac{1}{2}d_1^2\right) \quad (37)$
```

```text
两个展开都利用积分 $J_1, J_3$ 和 $J_4$，在 Heston 模型中，它们具有如下形式，使用了 Lewis (2000) 中的 (3.7)、(3.8) 和 (3.9) 位于第 86 页：
```

```math

$J_1(v, T) = \int_0^T (1 - e^{-\kappa(T-\tau)})(\theta + (v_0 - \theta)e^{-\kappa \tau})d\tau$

```

```math

$J_3(v, T) = \frac{\rho}{2K^2} \int_0^T (1 - e^{-\kappa(T-\tau)})^2(\theta + (v_0 - \theta)e^{-\kappa \tau})d\tau$

```

```math

$J_4(v, T) = \frac{\rho^2}{K^3} \int_0^T (1 - e^{-\kappa(T-\tau)})^3(\theta + (v_0 - \theta)e^{-\kappa \tau})d\tau$

```

```text

使用了 $\rho = 1/2$。
```

# 110 MATLAB 和 C# 中的 Heston 模型及其扩展

第二次展开（级数 II）生成了隐含方差：

```

$v_{imp} \approx \sqrt{\bar{v} + \sigma_J \frac{R^{1,1}+}{T}}$

$$\sigma_J^2 \left[ \frac{J_2}{T} + \frac{J_{2,0}^2}{T^2} + \frac{J_4 R^{1,2}}{T} - \frac{(J_1)^2}{T^2} (R^{2,2} - (R^{1,1})^2 R^{2,0}) \right] (4.43)

```

随后将其代入 (4.35) 中的 Black-Scholes 公式，产生 $C_{II}(S_0, v_0, T)$，即级数 II 下的期权价格。换句话之，我们使用 (4.35) 来获取期权价格，但将 $\bar{v}$ 替换为来自 (4.43) 的 $v_{imp}$。

```

$C_{II}(S_0, v_0, T) = C_{BS}(S_0, v_{imp}, T).$ (4.44)

```

最后，在 (4.42) 和 (4.44) 的期权价格表达式中，积分 $J_1, J_3$ 和 $J_4$ 都在初始方差 $v_0$ 处评估，因此 $v$ 在 (4.38)、(4.39) 和 (4.40) 中全部替换为 Heston 参数 $v_0$。方程 (4.36) 中的确定性方差和 (4.35) 中的 Black-Scholes 价格很容易使用自定义函数在 Matlab 中实现。代码示例所示：

```

v = theta + (v0-theta)*(1-exp(-kappa*T))/(kappa*T);

BSC = @(S,K,rf,q,T) (S*exp(-q*T)*normcdf((log(S/K) + ...));

BSPrice = BSC(S,K,rf,q,T);

```

方程 (4.38) 至 (4.40) 中的函数 $J_1(v,T)$ 和 $J_4(v,T)$ 在单个 Matlab 函数 J.m 中实现。

```

function y = J(rho,theta,T,v0,Number)

if Number=-1

    y = (theta*T + (1-exp(-k*T))*(v0/k) - ...;

    y = y*rho/k;

elsif Number=3

    y = theta*T + theta/2/k*(1-exp(-2*k*T)) - ...;

    y = y/2/k;

elseif Number=4

    y = theta/k*(T*(1+exp(-k*T)) - 2/k*(1-exp(-k*T)) + ...;

    y = y*rho^2/k;

end

```

方程 (4.41) 中的函数 $R^{pd}$ 同样在单个函数 R.m 中实现。

# 用于期权定价的基本变换

```

function y = R(p,q,X,Z,T)

if p==2 & q==0

y = T*(0.5*(X/Z)^2 - 0.5/Z - 1/8)

elsif p==1 & q==1

y = X/Z + 0.5,

elif p==1 & q==2

y = (X/Z)^2 - X/Z - 0.25/Z*(4-X)

elif p==2 & q==2

y = T*(0.5*(X/Z)^4 - 0.5*(X/Z)^3 - 3*(X^2/Z) ...

```

函数 `SeriesCall.m` 返回 (4.42) 中的级数 I 期权。它使用了 (4.35) 中的 Black-Scholes 价格和 (37) 中的其方差导数。

```

function y = SeriesCall(...);

BSC = @S,K,rf,q,T) (S*exp(-q*T)*normcdf(...))

BSV = @S,K,rf,q,T) (S*exp(-q*T)/sqrt(pi))*S*exp(-q*T)*(-0.5...))

J1 = J(rho,theta,kappa,v0,1);

J2 = J(rho,theta,kappa,v0,2);

J3 = J(rho,theta,kappa,v0,3);

J4 = J(rho,theta,kappa,v0,4);

v = theta + (v0-theta)*(1-exp(-kappa*T))/(kappa*T);

X = log(S*exp((rf-q)*T)/K;

v = vT;

R20 = R(2,0,X,T);

R11 = R(1,1,X,T);

R12 = R(1,2,X,T);

R22 = R(2,2,X,T);
