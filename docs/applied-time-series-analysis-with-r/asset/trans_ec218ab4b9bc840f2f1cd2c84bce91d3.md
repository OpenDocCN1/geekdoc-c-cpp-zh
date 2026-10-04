

## 向量值（多元）时间序列

first method, 我们讨论基于方程 10.18 中给出的多元 Yule-Walker 方程的多元 Yule-Walker 估计。将 Yule-Walker 方程中的 $\Gamma(k)$ 替换为方程 10.11 中定义的 $\tilde{\Gamma}(k)$ 得到样本多元 Yule-Walker 方程

```
$\tilde{\Gamma}(k) = \hat{\Gamma}(k-1)\hat{\Phi}_1^* + \dots + \tilde{\Gamma}(k-p)\hat{\Phi}_p^*, k=1, 2, \dots, p.$
```

与单变量情形一样，多元 Yule-Walker 估计始终产生平稳过程。

## 10.3.3.2 最小二乘和条件 ML 估计

VAR($p$) 过程参数的最小二乘估计可以通过将 VAR($p$) 模型表示为

```
$X_t = \alpha + \sum_{i=1}^p \hat{\Phi}_i X_{t-i} + a_t$
= \alpha + \hat{\Phi}_p^* X_t(p), \ t=p+1, \dots, n,$
```

其中，$X_t(p)$ 是 $mp \times 1$ 矩阵

```
$X_t(p) = (X_{t-1}, \dots, X_{t-p})^*.$
```

方程 10.34 中的方程与单变量情形中方程 7.12 中的方程类似。我们用方程 10.10 中给出的 $X$ 估计 $\mu$ 并分析零均值过程 $X_t-X$。在本节中，为方便起见，我们称此均值调整过程为 $X_t^*$。因此，方程 10.35 中的模型没有常数项，即 $\alpha=0$，而 AR 参数的最小二乘估计在 $mp \times m$ 矩阵中

```
$\hat{\mathbf{\Phi}}_{p)} = [\hat{\Phi}_1, \dots, \hat{\Phi}_p]$
= (X')^{-1}X'X_t^*,$
```

其中 $X_{(ip)}$ 是 $(n-p) \times m$ 矩阵，其行 $(X_{t_1}, \dots, X_{t_m}), t=p+1, \dots, n,$ 且 $X$ 是 $(n-p) \times p$ 矩阵，其行

```
$(X_{t-1}, \dots, X_{t-p}), t=p+1, \dots, n,$
```

其中 $X_{t-j} = (X_{t-j,1}, \dots, X_{t-j,m})$。

## 10.3.3.3 Burg 型估计

Nuttall (1976a,b) 和 Strand (1977) 通过考虑与方程 7.16 类似的多元后向模型以及前向模型，获得了 AR 参数的 Burg 型估计。另见 Jones (1978)。与单变量 Burg 估计一样，Burg 型 AR 估计始终产生平稳解。Marple 和 Nuttall (1983) 通过仿真结果表明，Burg 型（Nuttall-Strand）估计器比 Yule-Walker 估计器具有更好的性质。

## 10.3.4 计算残差和估计 $\Gamma_a$

类似于方程 9.2，估计 VAR(p) 模型相关的残差由下式给出

```
$$\hat{\mathbf{a}}_t = \mathbf{X}_t - \sum_{j=1}^{p} \mathbf{\hat{\Phi}}_{t-j} - \hat{\mathbf{\alpha}}, \quad t=p+1,\dots,n.$$
```

$\hat{\Gamma}_a$ 的最小二乘估计量由下式给出

```
$$\hat{\Gamma}_a = \frac{1}{n-2p-1} \sum_{t=p+1}^{n} \hat{\mathbf{a}}_t \hat{\mathbf{a}}'_t.$$
```

而条件 ML 估计量为

```
$$\hat{\Gamma}_a = \frac{1}{n} \sum_{t=p+1}^{n} \hat{\mathbf{a}}_t \hat{\mathbf{a}}'_t.$$
```

在第 74 节中讨论的回溯程序的扩展可用于获得 $t=1, \dots, n$ 的残差，并不可避免地提高估计 $\Gamma_a$ 的能力。

回想一下，在正态性下，$\Phi_1, \dots, \Phi_p$ 的最小二乘和条件 ML 估计是相同的。如果使用回溯来计算 $\hat{\mathbf{a}}_1, \dots, \hat{\mathbf{a}}_p$，则无条件 ML 估计量由下式给出

```
$$\hat{\Gamma}_a = \frac{1}{n} \sum_{t=1}^{n} \hat{\mathbf{a}}_t \hat{\mathbf{a}}'_t.$$
```

$\Gamma_a$ 的估计可以基于使用方程 10.39 从任何估计程序（例如 Burg 型估计器、Yule-Walker 等）获得的残差，只要使用回溯来计算 $\hat{\mathbf{a}}_1, \dots, \hat{\mathbf{a}}_p$。

## 向量值（多元）时间序列

## 10.3.5 VAR($p$) 谱密度估计

VAR($p$) 过程的多元谱（谱密度）在方程 10.32 中给出。VAR 谱估计只是拟合到多元时间序列数据集合的 VAR($p$) 模型相关的谱密度。那，VAR 谱估计由下式给出

```
$$\hat{\Phi}_X(f) = \hat{\Phi}^{-1}(e^{2\pi i f})\hat{\Gamma}_a\hat{\Phi}^{*-1}(e^{-2\pi i f})$$
```

当 $\hat{\Phi}$ 和 $\hat{\Gamma}_a$ 从数据中估计出来，如上所述。

## 10.3.6 将 VAR($p$) 模型拟合到数据

下面，我们简要总结将 VAR($p$) 模型拟合到向量时间序列实现所涉及的步骤。

### 10.3.6.1 模型选择

与单变量情形一样，拟合 VAR($p$) 模型到一组数据中的第一步是确定阶数 $p$。多元 AIC 的扩展（基于参数的 ML 估计）由下式给出

```
AIC = \ln|\hat{\Gamma}_a| + \frac{2m^2p}{n}$$
```

与单变量情形一样，基于其他估计程序（例如 Burg 型估计器）的 AIC 版本也可以使用方程 10.41 找到。模型阶数被选为在 $0 \le p \le P$ 的阶数范围内使用方程 10.41 计算的 AIC 值最小的那个，其中 $P$ 为某个整数。多元版本的 AIC 的替代方案，如 BIC 和 AICC 也是可用的（参见 Box of 2008）。

### 10.3.6.2 估计参数

一旦确定了阶数 $p$，则使用上述描述的方法获得与所选模型相关的参数 $\Phi_v, \dots, \Phi_w$ 和 $\mu$ 的估计。回想一下，通常使用 $\hat{\mathbf{X}}$ 估计，然后使用序列 $\mathbf{X}_t - \hat{\mathbf{X}}$ 估计剩余参数。我们将在下面使用此程序。

### 10.3.6.3 测试残差的白噪声

第 9.1 节中讨论的 Ljung-Box 检验已扩展到多元设定（参见 Hosking, 1981）。假设你想检验

## 420

## 应用时间序列分析与 R

多元时间序列 $Z$ 是否为多元白噪声。这里，$Z$ 可能只是观测到的时间序列，也可能是基于对一组数据拟合 VAR(p) 的残差序列。关于假设 $H_0$: $\rho(k) = 0, k=1, \dots,$ 对 $H_a$: $\rho(k) \neq 0$ 的 portanteau 检验，$k$ 在 1 到 $K$ 之间，基于检验统计量

```
$L = \sum_{k=1}^{K} \frac{k}{n-k} \text{tr}(\hat{\Gamma}(k)\hat{\Gamma}^{-1}(0)\hat{\Gamma}^{-1}(k)), \quad (10.42)$
```

$\hat{\Gamma}(k)$ 定义在方程 10.11 中，$\text{tr}[\mathbf{M}]$ 表示矩阵 $\mathbf{M}$ 的迹（即其对角元素之和）。方程 10.42 中的统计量 $L$ 在数据为多元白噪声时近似服从自由度为 $m'K$ 的 $\chi^2$ 分布，我们在计算的 $L$ 足够大时拒绝 $H_0$: $\rho(k)=0$。当数据为拟合 VAR($K-p$) 过程的残差时，在 $H_0$ 下检验统计量近似服从自由度为 $m^2(K-p)$ 的 $\chi^2$ 分布。

## 示例 10.4：示例 10.2 中数据的 AIC 和参数估计

在本例中，我们使用 R AIC 将 VAR(p) 模型拟合到双变量 VAR(1) 数据。让 AIC 选择模型阶数（允许 $1 \le p \le 8$），AIC 正确选择了 $p=1$。在本例中，我们将使用图 10.3 中绘制的双变量实现来估计示例 10.2 中的 VAR(1) 过程的参数。基础 R 函数 runif 计算 Yule-Walker 和最小二乘估计的 $\Phi_i$ 和 $\Gamma_a$。由此产生的 Yule-Walker 估计 $\Phi_1^{(YW)}$ 和 $\Gamma_a^{(YW)}$ 由下式给出

```
$$\Phi_1^{(YW)} = \begin{pmatrix} 0.89 & 0.58 \ -0.27 & 0.62 \end{pmatrix}$$
```

和

```
$$\Gamma_a^{(YW)} = \begin{pmatrix} 0.97 & 1.45 \ 1.45 & 3.83 \end{pmatrix}$$
```

相应的最小二乘估计为

```
$$\Phi_1^{(LS)} = \begin{pmatrix} 0.90 & 0.57 \ -0.27 & 0.63 \end{pmatrix}$$
```

和

```
$$\Gamma_a^{(LS)} = \begin{pmatrix} 0.78 & 1.47 \ 1.47 & 3.63 \end{pmatrix}$$
```

## 向量值（多元）时间序列 421

在两种情况下，估计值都可以看出与方程 10.21 和 10.22 中给出的真实模型参数非常接近。

**使用 R：** 如前所述，基础 R 函数计算 VAR 模型的 Yule-Walker 和最小二乘估计。mle 和 burg 方法仅适用于单变量情形。在下面的 R 代码中，我们使用 cbind 在 [图 10.3](#) 上创建双变量时间序列，使用 [图 10.3a](#) 和 [b](#) 中的单变量代码。

```
data(fig10.3.x1)
data(fig10.3.x2)
fig10.3 = cbind(fig10.3x1,fig10.3x2)
```

本例中用于使用 AIC 识别模型阶数并获得 Yule-Walker 和最小二乘估计的调用语句为

```
ar(fig10.3,order.max=8,aic=TRUE,method='wyw')
```

和

```
ar(fig10.3,order.max=8,aic=TRUE,method='ols')
```

分别。

一个有用的 CRAN 包用于 VAR 模型是 vars 包。以下 vars 命令应用于上面创建的双变量数据 [fig10.3](#)，将产生最小二乘估计（与上面匹配）以及 K= 24 的相应 Ljung-Box 检验：

```
lsfit=VAR(fig10.3,p=1,type=c("const"),ic=c("AIC")
serial.test(lsfit,ags.pt=24,type=c("PT.asymptotic"))
```

Ljung-Box 检验的 p 值大于 0.9，因此 $H_0:\rho(k)=0, k=1,..., 24$ 未被拒绝。对测试的其他 K 值也获得了类似的结果。
[图 10.6](#) 中显示的预测基于真实模型。预测可以使用 vars 包通过在两个命令行下方添加以下行获得：

```
predict(lsfit,n.ahead=25)
```

默认情况下你还将获得 95% 置信限。

## 10.4 非平稳 VARMA 过程

第 5.2 节中讨论的 ARUMA(p,d,q) 过程可以推广到多元情形。具体而言，我们考虑模型

> $$\Phi(B)\lambda(B)(X, \mu) = \Theta(B)a_1,$$

