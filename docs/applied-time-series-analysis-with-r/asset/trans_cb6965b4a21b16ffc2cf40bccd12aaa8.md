

## 预测

$E[(X_{t_0+\ell}-Z_{t_0}^*)X_j]=0, \quad j=1,2,\dots,t_0.$

$( )$ 设 $Z_{t_0}^*$ 满足 $E[(X_{t_0+\ell}-Z_{t_0}^*)X_j]=0, \ j=1,\dots,t_0,$ 且 $Z_t$ 为 $X_t, \ t=1,2,\dots,t_0$ 的任意线性组合。则有

$E[(X_{t_0+\ell}-Z_{t_0}^*)^2]=E[(X_{t_0+\ell}-Z_{t_0}^*+Z_{t_0}-Z_{t_0}^*)^2]$
$=E[(X_{t_0+\ell}-Z_{t_0}^*)^2]+E[(Z_{t_0}-Z_{t_0}^*)^2]$
$+2E[(X_{t_0+\ell}-Z_{t_0}^*)(Z_{t_0}-Z_{t_0}^*)]$
$\ge E[(X_{t_0+\ell}-Z_{t_0}^*)^2], \,{}$

因为交叉项 $E[(X_{t_0+\ell}-Z_{t_0}^*)(Z_{t_0}-Z_{t_0}^*)]\ge 0.$ 交叉项为零这一事实可利用条件期望的性质证明（参见 Billingsley 1995）。

$(\Rightarrow)$ 为证明 $A\Rightarrow B,$ 我们将使用逆否命题，即 $\sim B\Rightarrow\sim A.$ 我们假设 $E[(X_{t_0}-Z_t^*)X_j]=a\neq 0$ 对某个 $j$ 成立，并将证明 $Z_t^*$ 不具有最小 MSE，通过构造 $X_t, \ t=1,2,\dots,t_0$ 的线性组合 $Z_{it}$ 其 MSE 小于 $Z_t^*.$ 假设 $E[(X_{t_0+\ell}-Z_{t_0}^*)X_j]=a\neq 0$ 且令 $E[(X_{t_0+\ell}-Z_{t_0}^*)^2]\ge E\dots$

$Z_t=Z_{t_0}^*+\frac{aX_j}{E[X_j]^2},$

则

$E[(X_{t_0+\ell}-Z_{t_0}^*)^2]=E[(X_{t_0}-Z_{t_0}^*+Z_{t_0}-Z_{t_0}^*)^2]$
$=E[(X_{t_0}-Z_{t_0}^*-(Z_{t_0}-Z_{t_0}^*)^2]$
$=E[(X_{t_0+\ell}-Z_{t_0}^*)^2]+E[(Z_{t_0}-Z_{t_0}^*)^2]-2E[(X_{t_0+\ell}-Z_{t_0}^*)(Z_{t_0}-Z_{t_0}^*)]$
$=E[(X_{t_0+\ell}-Z_{t_0}^*)^2]+E\left(\frac{aX_j}{E[X_j]^2}\right)^2-2E\left[(X_{t_0+\ell}-Z_{t_0}^*)\frac{aX_j}{E[X_j]^2}\right]$
$=E\left[(X_{t_0+\ell}-Z_{t_0}^*)^2\right]+\frac{a^2}{E[X_j]^2}-\frac{2a^2}{E[X_j]^2}$
$=E\left[(X_{t_0+\ell}-Z_{t_0}^*)^2\right]-\frac{a^2}{E[X_j]^2},$

由于 $a \neq 0$，可得

$E\left[(X_{t_0+\ell}-Z_{t})^2\right] < E\left[(X_{t_0+\ell}-Z_{t_0}^*)^2\right]$

结果得证。

## 附录 6B：基本预测程序

- a. fore.arma.wge(x,phi,theta,n.ahead,lastn,plot,limits)
该函数使用 Box-Jenkins 预测方法对平稳 ARMA 模型进行 n.ahead 步预测。预测值和限界可选择性地绘制。您可以选择计算并预测序列末端的 n.ahead 步，或预测最后 n.ahead 个数据值。注意：phi 和/或 theta 的分量如果模型以因子形式给出，可使用 mult.wge 获得
x = 实现
phi = AR 系数向量（默认值 = 0）
theta = MA 系数向量（默认值 = 0）
n.ahead = 您想要预测的步数（默认值 = 2）
lastn = 逻辑变量。若 lastn = FALSE 则预测值为 x(n+1), x(n+2), ..., x(n+n.ahead) 其中 n 为实现的长度。若 lastn = TRUE，则程序预测实现中最后 n.ahead 个值（默认值 = FALSE）
plot = 逻辑变量。若 plot = TRUE 则预测值将与实现一起绘制。若 plot = FALSE 则不输出绘图（默认值 = TRUE）
limits = 逻辑变量。若 limits = TRUE 则 95% 限界将与预测值一起绘制（默认值 = TRUE）
注意：ARMA 模型可以是本章中设定的已知/给定模型。更常见的是对数据拟合 ARMA(p,q) 模型并基于拟合模型进行预测。以下示例 (ii) 使用了第 7 章中描述的 tswge 函数 est.arma.wge。

## 预测

示例：

- 1. 使用已知模型
```
data(fig6.2nf)
example=fore.arma.wge(fig6.2nf,phi=c(1.2,-6),theta=.5,n.ahead=20)
```
该函数生成图 6.4 中的绘图以及以下输出：
example$f 是一个包含预测值的向量
example$ll 是一个包含下限的向量
example$ul 是一个包含上限的向量
example$resid 是一个包含残差的向量
example$wnv 是白噪声方差估计值
example$se 是一个包含每个预测值的标准误差（SE）的向量
example$psi 是一个包含 psi 权重的向量

- 2. 估计模型参数并将其用作预测的模型
```
data(fig6.2nf)
exii=est.arma.wge(fig6.2nf,p=2,q=1)
example=fore.arma.wge(fig6.2nf,phi=exii$phi,theta=exii$theta,n.ahead=20)
```

b. aruma.wge(x,phi,theta,d,lambda,n.ahead,lastn,plot,limits) 该函数使用 Box-Jenkins 预测方法对具有平稳 ARMA 分量的非平稳 ARIMA 模型进行 n.ahead 步预测，这些模型具有诸如 (I-B)^d、季节性和/或非平稳因子等因子。预测值和预测限界可以绘制。

x = 实现
phi 是 AR 系数向量（默认值 =0）
theta 是 MA 系数向量（默认值 =0）
d 是模型中差分算子 (1 −B)^d 的阶数（默认值 =0）
s 是季节阶数（默认值 =0）
lambda 是未包含在差分或季节算子中的非平稳系数的向量。（默认值 =0）
n.ahead = 您想要预测的步数（默认值 =2）

## 266 应用时间序列分析与 R

lastn = 逻辑变量。若 lastn = FALSE（默认值）则预测值为 x(H+1), x(H+2), ..., x(n.ahead) 其中 n 为实现的长度。若 lastn = TRUE，则程序预测实现中最后 n.ahead 个值。

plot = 逻辑变量。若 plot = TRUE（默认值）则预测值将沿实现绘制。若 plot = FALSE 则不输出绘图。（默认值 = TRUE）

limits = 逻辑变量。若 limits = TRUE 则 95% 预测限界将与预测值一起绘制。

注意：与 fore.arma.wge 函数一样，您可以使用“已知”或拟合模型。以下示例使用方程 6.42 中示例 6.4 的“真实” ARIMA(1,1,0) 模型。

示例：
data(fig6.6nf)
example = fore.arma.wge(fig6.6nf,phi=.8,d=1,n.ahead = 20)
此代码生成图 6.6 中的绘图以及以下输出：

- example$f 是一个包含预测值的向量
- example$l 是一个包含下限的向量
- example$ul 是一个包含上限的向量
- example$resid 是一个包含残差的向量
- example$wnv 是白噪声方差估计值
- example$se 是一个包含每个预测值的 SE 的向量
- example$psi 是一个包含 psi 权重的向量

c.sigplusnoise.wge(x, linear, freq, max, p, n.ahead, lastn, plot,limits)

该函数对形式为信号 + 噪声模型的 n.ahead 步进行预测

```
X_t = b_0 + b_1t + Z_t,
or
X_t = A_0 + A_1 cos(2πf_0t + A_2) + Z_t
```

注意信号限制为线性或（单一）正弦信号。与本章中的其他预测一样，我们假设在评估预测误差时信号和（自回归）噪声模型是已知的。预测值和预测限界可以有选择地绘制。您可以计算并绘制序列末端之后 n.ahead 步的预测值，或预测最后 n.ahead 个值。在上述线性模型中，所有参数均被估计，包括拟合到拟合直线残差的 AR(p) 模型的阶数（p）和相关参数。在余弦模型中，用户必须指定 x=f0。所有参数均被估计。

x = 实现

linear = 逻辑变量。若 linear = TRUE（默认值）则预测值基于上述线性加噪声模型。若 linear = FALSE 则对数据拟合余弦加噪声模型。

freq = 用户必须指定的 f0（默认值 freq=0）。

max.p 是要拟合的最大阶自回归模型（基于 AIC）到残差。

n.ahead = 您想要预测的步数（默认值 = 10）

last = 逻辑变量。若 last= FALSE 则预测值为 x(n+1), x(n+2), ...x+n.ahead 其中 n 为实现的长度。若 last= TRUE，则程序预测实现中最后 n.ahead 个值。（默认值 = FALSE）

plot = 逻辑变量。若 plot = TRUE 则预测值将与实现一起绘制。若 plot = FALSE 则不输出绘图。

（默认值 = TRUE）

limits = 逻辑变量。若 limits = TRUE 则 95% 预测限界将与预测值一起绘制。（默认值 = TRUE）

示例：假设长度为 n=50 的实现由 Xt=10+4cos(2t/12)+Z 生成，其中 (1−B)Zt=at，且 σ_t=1 使用附录 1.B 中描述的函数 gen.sigplusnoise.wge。以下代码将生成实现然后计算并绘制 51–70 时段的预测值。

```
x = gen.sigplusnoise.wge (n=50,b0=10,b1=0,coef=c(4,0),freq=c(0.0833),psi=c(2,0),phi=.8
```

```
xfore = for.sigplusnoise.wge (x,linear=FALSE,freq=0.0833,n.ahead=20,last=FALSE,FALSE)
```

注意均值 10 在调用函数 gen.sigplusnoise.wge 时使用 b0=10 输入。您也可以使用

