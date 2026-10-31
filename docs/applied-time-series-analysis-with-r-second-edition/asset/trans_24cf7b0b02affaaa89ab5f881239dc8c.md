
我们令 N_t ~ N(0, 1) 表示与 V_t 和 W_t 均不相关的噪声。因此，

σ²_W* = { 0.75, if t ≠ 2, 5
          1.75, if t = 2, 5. }

缺失值通过卡尔曼迭代估计，以计算 X̂_t^t、X̂_t^{t-1}、Γ_t^t 和 Γ_t^{t-1}，t = 1, ..., 75；然后对于 t = 75, 74, ..., 2,1，使用平滑迭代计算 X̂_2^{75} 和 X̂_5^{75} 的值，这些即为所求估计值。在表10.2中，我们展示了当 y_2 和 y_5 缺失时表10.1的修订版本。如预期的那样，可以看出，与 Y_t 数据可用的情况相比，X̂_2^2 和 X̂_2^{75} 具有更高的均方误差。

**使用R：** 表10.2中的结果是通过 tswge 中的 kalman.miss.wge 函数获得的。该函数基于对 CRAN 中 astsa 包中 ksmooth1 的调用。kalman.miss.wge 函数是一个单变量简化版本，旨在对缺失数据情形（如示例10.12中考虑的情形）执行预测、滤波和平滑等分析。关于用于生成表10.2中数据的语句的讨论，请参见附录10B。

## 10.6.6 参数估计

设 Θ 表示在方程10.48和10.49中指定的状态空间模型中待估计的参数向量。为了方便，我们将似然函数 L(Θ ; Y_1, ..., Y_n)（在 Y_0 条件下）写为 L(Θ ; Y_1, ..., Y_n) = Π_{t=1}^n f_t(Y_t | Y_{t-1}, ..., Y_1)，其中 f_t(Y_t | y_{t-1}, ..., y_1) 是 Y_t 在给定 Y_j = y_j, j = 1, ..., t-1（且条件 Y_0 = y_0）时的条件密度。似然函数的计算很复杂，但如果 V_t 和 W_t 联合正态分布且不相关，并且初始状态 X_0 ~ MVN(μ_0, Γ_0)，则计算可以变得更容易处理。计算新息 I_t，其中

I_t = Y_t - G_t X̂_t^{t-1},   (10.60)

且

$$\Gamma_{I_t} \equiv \operatorname{Var}[I_t] = \operatorname{Var}\left[\boldsymbol{G}_t\left(\boldsymbol{X}_t - \hat{\boldsymbol{X}}_t^{t-1}\right) + \boldsymbol{W}_t\right]$$ $$= \boldsymbol{G}_t \boldsymbol{\Gamma}_t^{t-1} \boldsymbol{G}_t' + \boldsymbol{\Gamma}_W.$$ \tag{10.61}

（另见附录10A中卡尔曼预测与滤波的证明）。基于上述正态性假设，似然函数可以写为

$$L(\boldsymbol{\Theta}; Y_1, \ldots, Y_n) = \frac{1}{(2\pi)^{n/2}}\left(\prod_{t=1}^{n} |\boldsymbol{\Gamma}_{I_t}|\right)^{-1/2} \exp\left[-\frac{1}{2}\sum_{t=1}^{n} I_t' \boldsymbol{\Gamma}_{I_t}^{-1} I_t\right].$$ \tag{10.62}

数值最大化过程用于从方程10.62中求出极大似然估计值。Shumway 和 Stoffer（1982, 2010）讨论了使用牛顿-拉弗森算法和期望最大化（EM）算法来执行这一最大化。

## 10.6.7 使用状态空间方法求单变量AR实现的加性分量

在第3.4节中，我们讨论了将AR实现分解为加性分量 $x_t = x_t^{(1)} + \cdots + x_t^{(m)}$，其中 $m$ 是因子表中的行数。也就是说，$m$ 等于特征方程的实根个数与复共轭根对个数之和。在该节中，我们给出了部分分式推导，以说明加性分量分别来自实根的AR(1)模型和复共轭根的ARMA(2,1)模型。我们证明了在每种情况下，与因子表第 $j$ 行相关的系统频率就是对应于第 $j$ 个分量的AR(1)或ARMA(2,1)模型所固有的系统频率。然而，第10.3.4节中的推导并未得出一种计算方法。在本例中，我们考虑该问题的状态空间形式，并且除了像之前一样说明分量是AR(1)和ARMA(2,1)之外，状态空间方法还提供了计算这些分量的一种简单方法。

在示例10.10中，我们给出了单变量零均值AR($p$)过程 $Y_t = \phi_1 Y_{t-1} + \cdots + \phi_p Y_{t-p} + a_t$ 的一组状态空间方程。状态方程和观测方程分别为

$\boldsymbol{X}_t = \boldsymbol{\Phi}\ \boldsymbol{X}_{t-1} + \boldsymbol{V}_t \quad\text{(状态方程)},$
$\boldsymbol{Y}_t = (0\ 0\ \dots\ 1)\boldsymbol{X}_t \quad\text{(观测方程)},$

其中
$\boldsymbol{X}_t = \begin{pmatrix} Y_{t-p+1}\\ Y_{t-p+2}\\ \vdots\\ Y_t \end{pmatrix},\quad \boldsymbol{\Phi}= \begin{pmatrix}0&1&0&\dots&0\\0&0&1&\dots&0\\\vdots&\vdots&\vdots&&\vdots\\0&0&0&\dots&1\\\phi_p&\phi_{p-1}&\phi_{p-2}&\dots&\phi_1\end{pmatrix},\quad \boldsymbol{V}_t = \begin{pmatrix}0\\0\\\vdots\\0\\a_t\end{pmatrix}$

在这种情况下，$v = p$，$w = 1$，且 $\mathbf{W}_t = \mathbf{0}$，我们假设 $a_t \sim N(0,\sigma_a^2)$。在下文中，我们将假设 $\boldsymbol{\Phi}$ 的特征值互不相同。这些特征值为 $1/r_1$, $1/r_2$, ..., $1/r_p$，其中 $r_1$, ..., $r_p$ 是特征方程 $\phi(z)=1-\phi_1 z-\phi_2 z^2-\dots-\phi_p z^p=0$ 的根。对应于 $1/r_j$ 的特征向量可以选为 $\boldsymbol{u}'_j = (r_j^{p-1}\ r_j^{p-2}\ \dots\ r_j\ 1)$，并且我们有 $\boldsymbol{\Phi}=U D U^{-1}$，其中 $\boldsymbol{U}=[\boldsymbol{u}_1\ \boldsymbol{u}_2\ \dots\ \boldsymbol{u}_p]$，且

$\boldsymbol{D}= \operatorname{diag}\left(\frac{1}{r_1}\ \frac{1}{r_2}\ \dots\ \frac{1}{r_p}\right)$

即，一个沿对角线具有所列元素的对角矩阵。注意，由于特征向量的选取，$\mathbf{U}$ 的最后一行是全1向量。出于我们的目的，我们排列 $\mathbf{D}$（以及 $\mathbf{U}$），使得 $|r_1| \ge |r_2| \ge \dots$

定义 $\boldsymbol{\Psi}_t = \boldsymbol{U}^{-1}\boldsymbol{X}_t$（即 $\boldsymbol{X}_t = \boldsymbol{U}\boldsymbol{\Psi}_t$），则状态空间模型可以重写，使得 $\mathbf{U}^{-1}$ 的行提供计算分量所需的滤波器系数。

### 10.6.7.1 修正后的状态空间模型

状态方程：$\boldsymbol{X}_t = \boldsymbol{\Phi}\ \boldsymbol{X}_{t-1} + \boldsymbol{V}_t$ 变为 $\boldsymbol{X}_t = (\boldsymbol{U}\boldsymbol{D}\boldsymbol{U}^{-1})(\boldsymbol{U}\boldsymbol{\Psi}_{t-1}) + \boldsymbol{V}_t$，即 $\boldsymbol{U}\boldsymbol{\Psi}_t = \boldsymbol{U}\boldsymbol{D}\boldsymbol{\Psi}_{t-1} + \boldsymbol{V}_t$，因此
$\boldsymbol{\Psi}_t = \boldsymbol{D}\boldsymbol{\Psi}_{t-1} + \boldsymbol{U}^{-1}\boldsymbol{V}_t$（新状态方程）。(10.63)

观测方程：在这种情况下，$\boldsymbol{Y}_t = (0\ 0\ \dots\ 0\ 1)\ \boldsymbol{X}_t$ 变为 $\boldsymbol{Y}_t = (0\ 0\ \dots\ 0\ 1)\ \boldsymbol{U}\boldsymbol{\Psi}_t$，即 (10.64)

$x_t^{(1)} = (-3.52\;\;5.26\;\;-2.16)\begin{pmatrix}x_{t-2}\\x_{t-1}\\x_t\end{pmatrix},$

其中 $t = 3, \dots, 200$。从 $\mathbf{U}^{-1}$ 的第三行，我们得到

$x_t^{(2)} = (3.52\;\;-5.61\;\;3.15)\begin{pmatrix}x_{t-2}\\x_{t-1}\\x_t\end{pmatrix},$

分量 $x_t^{(1)}$ 和 $x_t^{(2)}$ 已示于图3.24中，可以看出 $x_t^{(1)}$ 捕获了周期约为11（1/0.09）个单位的伪周期行为，而 $x_t^{(2)}$ 描绘了与正实根相关的游走行为。

**使用R：** AR实现的分解可以使用 tswge 包中的 `factor.comp.wge` 函数获得。示例10.14中显示的计算和图3.26中显示的分解基于与图3.16所示AR(3)实现相关的真实模型参数。`factor.comp.wge` 函数拟合指定阶数的AR(p)模型，并绘制原始序列和分解结果。以下命令将生成与图3.26所示图形相似的图（不同之处在于它们基于极大似然估计）：

```
data(fig3.16a)
factor.comp.wge(fig3.16a,p = 3,ncomp = 2)
```

## 附录10A：状态空间结果的推导

### 10A.1 卡尔曼预测与滤波递推的证明

由概率论可知，如果 $Y_1, \dots, Y_s,\ X_t$ 是联合正态的单变量随机变量，那么基于 $Y_1, Y_2, \dots, Y_s$ 在均方意义下对 $X_t$ 的最佳线性预测是条件期望 $E[X_t | Y_1, \dots, Y_s]$。也就是说，$E[X_t | Y_1, \dots, Y_s]$ 是 $Y'_j$ 的线性函数，记为 $E[X_t | Y'_1, \dots, Y'_s] = \sum_{j=1}^s a_j Y_j$，并且在所有线性
