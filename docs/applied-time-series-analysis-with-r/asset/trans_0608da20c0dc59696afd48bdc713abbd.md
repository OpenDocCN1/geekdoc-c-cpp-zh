

## 7.3 ARMA(p,q) 参数的 ML 估计

使用 ML 估计必然涉及分布假设。为了计算参数的 ML 估计，我们假设 $a_i$ 服从正态分布，因而 $X=(X_1, ..., X_n)'$ 具有均值为 $\mu$、协方差矩阵为 $\Sigma_n$ 的多元正态分布，其中

$$\mu = (\mu, \mu, \dots \mu)'$$

且

$$\Sigma_n = \begin{pmatrix} \gamma_0 & \gamma_1 & \dots & \gamma_{n-1} \\ \gamma_1 & \gamma_0 & \dots & \gamma_{n-2} \\ \vdots & \vdots & \dots & \vdots \\ \gamma_{n-1} & \gamma_{n-2} & \dots & \gamma_0 \end{pmatrix}$$

与之前的估计程序类似，我们分析 $X_t - X$ 并假设 $\mu = 0$。

### 7.3.1 条件和无条件 ML 估计

令 $\sigma_a^2 M_n^1 = \Sigma_n$，$X=(X_1, ..., X_n)'$ 的联合概率密度函数为

$$f(x_1, \dots, x_n) = \frac{1}{(2\pi\sigma_a^2)^{n/2}} |M_n|^{1/2} \exp\left\{-\frac{x^T M_n x}{2\sigma_a^2}\right\}$$

式 7.29 中的联合密度函数可写为

$$f(x_1, \dots, x_n) = f(x_{p+1}, \dots, x_n | x_1, \dots, x_p)f(x_1, \dots, x_p),$$

其中 $f(\cdot)$ 为条件概率密度函数。由于 $a_i$ 是不相关的 $N(0, \sigma_a^2)$ 随机变量，可得

$$f(a_{p+1}, \dots, a_n) = \frac{1}{(2\pi\sigma_a^2)^{(n-p)/2}} \exp\left\{-\frac{1}{2\sigma_a^2} \sum_{t=p+1}^n a_t^2}\right\}$$

## 参数估计

重新排列式 7.27 中的项，我们得到

$a_t = X_t - \phi_1 X_{t-1} - \dots - \phi_p X_{t-p} + \theta_1 a_{t-1} + \dots + \theta_q a_{t-q}. \quad (7.31)$

在 $X_1 = x_{t_1}, \dots, X_p = x_{t_p}$ 且初始值 $a_1 = a_1^*, \dots, a_p = a_p^*$ 的条件下，由式 7.31 可得（为方便记号假设 $q \leq p$），对 $\phi_s$ 和 $\theta_s$ 的一种选择，随机变量 $a_{p+1}, \dots, a_n$ 与 $X_{p+1}, \dots, X_n$ 由方程组关联

$a_{p+1} = X_{p+1} - \phi_1 X_p - \dots - \phi_p X_1 + \theta_1 a_p + \dots + \theta_q a_{p-1}$  
$a_{p+2} = X_{p+2} - \phi_1 X_{p+1} - \dots - \phi_p X_2 + \theta_1 a_{p+1} + \dots + \theta_q a_{p-2}$  
:  
:  
$a_n = X_n - \phi_1 X_{n-1} - \dots - \phi_p X_{n-p} + \theta_1 a_{n-1} + \dots + \theta_q a_{n-q}.$

$a_{t_1}, \dots, a_{t_p}$ 的值先前取为零，即其无条件均值。由于该变换雅可比行列式的绝对值为一，可得

$f(x_{p+1}, \dots, x_n | x_{t_1}, \dots, x_{t_p}) =$  
$= \frac{1}{(2\pi\sigma_a^2)^{(n-p)/2}} \exp \left\{ -\frac{1}{2\sigma_a^2} \sum_{t=p+1}^n (x_t - \phi_1 x_{t-1} - \dots - \phi_p x_{t-p} + \theta_1 a_{t-1} + \dots + \theta_q a_{t-q})^2 \right\} \quad (7.32)$

其中 $S_c$，由下式给出

$S_c = \sum_{t=p+1}^n (x_t - \phi_1 x_{t-1} - \dots - \phi_p x_{t-p} + \theta_1 a_{t-1} + \dots + \theta_q a_{t-q})^2.$

使用式 7.30 计算 $f(x_1, \dots, x_n)$ 涉及 $f(x_1, \dots, x_p)$，其由下式给出

$f(x_1, \dots, x_p) = \frac{1}{(2\pi\sigma_a^2)^{p/2}} |M_p|^{1/2} \exp \left\{ -\frac{x_p' M_p x_p}{2\sigma_a^2} \right\}. \quad (7.33)$

其中 $x_p = (x_1, \dots, x_p)'$。将式 7.32 中的 $f(x_{p+1}, \dots, x_n | x_{t_1}, \dots, x_{t_p})$ 乘以式 7.33 中的 $f(x_1, \dots, x_p)$ 得到

$f(x_1, \dots, x_n) = f(x_{p+1}, \dots, x_n | x_1, \dots, x_p)f(x_1, \dots, x_p)$

$= \frac{1}{(2\pi\sigma_a^2)^{(n-p)/2}} \exp\left\{-\frac{S_c}{2\sigma_a^2}\right\} \times \frac{1}{(2\pi\sigma_a^2)^{p/2}} |\mathbf{M}_p|^{1/2} \exp\left\{-\frac{\mathbf{x}_p^T\mathbf{M}_p\mathbf{x}_p}{2\sigma_a^2}\right\}$

$= \frac{1}{(2\pi\sigma_a^2)^{n/2}} |\mathbf{M}_p|^{1/2} \exp\left\{-\frac{S_u}{2\sigma_a^2}\right\}$

其中

$S_u = S_c + \mathbf{x}_p^T\mathbf{M}_p\mathbf{x}_p. \quad (7.34)$

通常将 $S_u$ 称为无条件平方和，将 $S_c$ 称为条件平方和。对数似然函数为

$l(\phi_1, \dots, \phi_p, \theta_1, \dots, \theta_q, \sigma_a^2) = -\frac{n}{2}\ln(2\pi\sigma_a^2) + \frac{1}{2}\ln|\mathbf{M}_p| - \frac{S_u}{2\sigma_a^2}. \quad (7.35)$

ML 估计量通过对参数 $\phi_1, \dots, \phi_p, \theta_1, \dots, \theta_q$ 和 $\sigma_a^2$ 最大化式 7.35 得到。得到的估计量为无条件或精确 ML 估计量。

## 288 应用时间序列分析与 R

### 示例 7.3：AR(1) 情形下的 ML 估计

考虑 AR(1) 模型，此时

$f(x_1, \dots, x_n) = f(x_2, \dots, x_n | x_1)f(x_1).$

此时，$f(x_1)$ 由下式给出

$f(x_1) = \frac{1}{(2\pi\sigma_a^2)^{1/2}} \exp\left\{-\frac{x_1^2}{2\sigma_a^2}\right\}$

$= \frac{1}{(2\pi\sigma_a^2)^{1/2}} (1-\phi_1^2)^{1/2} \exp\left\{-\frac{x_1^2(1-\phi_1^2)}{2\sigma_a^2}\right},$

由于 $\sigma_a^2 = \sigma_x^2/(1-\phi_1^2)$。因此，在式 7.33 的记号中，$|\mathbf{M}_p| = 1-\phi_1^2$ 且

$$f(x_1,\dots,x_n) = \left(\frac{1}{2\pi\sigma_0^2}\right)^{n/2}(1-\phi_1^2)^{1/2}$$
$\times\exp\left(-\frac{1}{2\sigma_0^2}\left((1-\phi_1^2)x_1^2+\sum_{t=2}^n(x_t-\phi_1 x_{t-1})^2\right)\right).$

对数似然函数为

$$l(\phi_1,\sigma_0^2)=-\frac{n}{2}\ln(2\pi\sigma_0^2)+\frac{1}{2}\ln(1-\phi_1^2)-\frac{S_u}{2\sigma_0^2}, \quad (7.36)$$

其中

$$S_u=(1-\phi_1^2)x_1^2+\sum_{t=2}^n(x_t-\phi_1 x_{t-1})^2.$$

示例 7.3 中 AR(1) 情形的精确 ML 估计不存在闭式解，且一般情况下 $\ln |\mathbf{M}_n|$ 的导数很复杂。Box 等人（2008）建议两种简化：

- 1. 对于大 $n$，他们声称 $\ln |\mathbf{M}_n|$ 与 $S_u$ 相比可忽略。这提示了简化的对数似然函数

$$l(\phi_1,\dots,\phi_n,\theta_1,\dots,\theta_n,\sigma_0^2)=-\frac{n}{2}\ln(2\pi\sigma_0^2)-\frac{S_u}{2\sigma_0^2}. \quad (7.37)$$

可以通过最大化式 7.37 中的 $l(\phi_1,\dots,\phi_n,\theta_1,\dots,\theta_n,\sigma_0^2)$ 得到对无条件 ML 估计的近似。该最大化可通过最小化有限非零 $\sigma_0^2$ 下的无条件平方和 $S_u$ 实现，因此这些估计有时被称为无条件最小二乘估计。

Box 等人（2008）建议了一种基于回溯预测（或回溯）技术的近似无条件平方和 $S_u$ 的实用方法。他们将无条件平方和表示为

$$S_u=\sum_{t=1}^nE[a_t|X]^2. \quad (7.38)$$

$E[a_t|X]$ 表示在给定 $X_1,\dots,X_n$ 的条件下 $a_t$ 的条件期望。式 7.38 中的无条件平方和可由和式近似

$$\hat{S}_u=\sum_{t=1}^n\hat{a}_t^2. \quad (7.39)$$

## 290 应用时间序列分析与 R

对于某个正整数 K。该方法本质上涉及“回溯”$X_t, X_{t-1}, ..., 并使用这些回溯值和式 7.31 来估计 $a_t, a_{t-1}, ..., a_{t-k}$。回溯将在第 7.4 节讨论。通过选择使式 7.39 最小的参数得到的估计有时称为无条件最小二乘估计，而无条件或精确 ML 估计是通过最小化式 7.35 中的对数似然得到的，其中 $S$ 使用式 7.39 计算。关于条件和无条件 ML 估计的进一步讨论，参见 Priestley（1981）。

另一种相似的方法是使用 $f(x_{t-p}, ..., x_{t-1}, ..., x_t)$ 作为似然函数并最大化

$l(\phi_1, ..., \phi_p, \theta_1, \sigma_a^2) = -\frac{n-p}{2} \ln(2\pi\sigma_a^2) - \frac{S}{2\sigma_a^2} \quad (7.40)$

通过最大化式 7.40 得到估计称为条件 ML 估计。

$\sigma_a^2$ 的估计：$\sigma_a^2$ 的 ML 估计（基于最大化式 7.35 或式 7.37）可通过对 $l(\phi, \theta, \sigma_a^2)$ 关于 $\sigma_a^2$ 求导得到，这给出（在情形下）

$\frac{\partial l}{\partial \sigma_a^2} = -\frac{n}{2\sigma_a^2} + \frac{S}{2\sigma_a^4} = 0$

其中 $S = S_u$ 或 $S_c$。令该偏导数为零并求解 $\sigma_a^2$ 得到

$$\hat{\sigma}_a^2 = \frac{1}{n} \sum_{t=1}^n \hat{a}_t^2 \quad (7.41)$$

式 7.41 中的 $\hat{a}_t$ 表示通过回溯得到的估计。如果不使用回溯且条件平方和 $\hat{S}_c = \sum_{t=p+1}^n \hat{a}_t^2$ 得到（基于 $\hat{a}_1 = \hat{a}_2 = ... = \hat{a}_p = 0$），则在这种情况下，$\sigma_a^2$ 的条件 ML 估计为

$$\hat{\sigma}_a^2 = \frac{\hat{S}_c}{(n-p)} \quad (7.42)$$

其中 $\hat{S}_c$，表示对 $\phi_1, ..., \phi_p, \theta_1, ..., \theta_q$ 插入条件 ML 估计后的平方和函数。

**使用 R：** 函数 est.arma.wge 基于基础 R 函数 arima 计算 ARMA(p,q) 参数的 ML 估计。默认

