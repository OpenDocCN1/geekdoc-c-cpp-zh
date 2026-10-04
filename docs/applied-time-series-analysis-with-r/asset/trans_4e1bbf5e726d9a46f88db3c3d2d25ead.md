

# 向量值（多变量）时间序列

## 431

![](img/41dcbfb9af56fa48895afde322197b0b_447_0.png)

**图 10.11**
示例 10.9 中 $X$ 的 AR(1) 模型长度为 $n=75$ 的实现（实线），以及对应的 AR(1)-加噪声模型 $Y_t$ 的实现（虚线）。

其中

```
$X_t = \begin{pmatrix} Y_{t-p+1} \\ Y_{t-p+2} \\ \vdots \\ Y_t \end{pmatrix}, \quad \Phi = \begin{pmatrix} 0 & 1 & 0 & \dots & 0 \\ 0 & 0 & 1 & \dots & 0 \\ \vdots & \vdots & \vdots & \vdots & \vdots \\ 0 & 0 & 0 & \dots & 1 \\ \Phi_p & \Phi_{p-1} & \Phi_{p-2} & \dots & \Phi_1 \end{pmatrix}, \quad V_t = \begin{pmatrix} a_1 \\ a_2 \\ \vdots \\ a_p \end{pmatrix}$
```

注意在此情况下，$v=p$，$w=1$ 且 $W_t=0$。该示例说明了 AR(1) 型状态方程并没有对预期的适用设置产生限制。
如果 $Y_t$ 满足零均值 VAR(p) 模型 $Y_t = \Phi_1 Y_{t-1} + \dots + \Phi_p Y_{t-p} + \mathbf{a}_t$，则通过以下方程得到状态空间表达式：

```
$X_t = \Phi X_{t-1} + V_t \quad \text{(状态方程)},$
$Y_t = (0 \ 0 \dots 1)X_t \quad \text{(观测方程)},$
```

其中 $X_t, \Phi$ 和 $V_t$ 分别是 $p \times 1$、$p \times p$ 和 $p \times m$ 矩阵，定义如下：

```
$X_t = \begin{pmatrix} Y_{t-p+1} \\ Y_{t-p+2} \\ \vdots \\ Y_t \end{pmatrix}, \quad \Phi = \begin{pmatrix} 0 & 0 & 0 & \dots & 0 \\ 0 & 0 & I & \dots & 0 \\ \vdots & \vdots & \vdots & \vdots & \vdots \\ 0 & 0 & 0 & \dots & I \\ \Phi_p & \Phi_{p-1} & \Phi_{p-2} & \dots & \Phi_1 \end{pmatrix}, \quad V_t = \begin{pmatrix} a_1 \\ a_2 \\ \vdots \\ a_p \end{pmatrix}$
```

## 示例 10.11：ARMA(p,q) 过程的状态空间形式

单变量零均值 ARMA(p,q) 过程的状态空间表达式为：

```
$Y_t - \phi_1 Y_{t-1} - \dots - \phi_p Y_{t-p} = a_t - \theta_1 a_{t-1} - \dots - \theta_q a_{t-q},$
```

由：

```
$X_t = \Phi X_{t-1} + V_t \quad \text{(状态方程),}$
$Y_t = (-\theta_1, -\theta_2, \dots, -\theta_q, 1)X_t \quad \text{(观测方程)},$
```

其中

$X_t = \begin{pmatrix} U_{t-r+1} \\ \vdots \\ U_{t+2} \end{pmatrix}, \Phi = \begin{pmatrix} 0 & 1 & 0 & \dots & 0 \\ 0 & 0 & 1 & \dots & 0 \\ \vdots & \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & 0 & \dots & 1 \\ \phi_r & \phi_{r-1} & & \dots & \phi_1 \end{pmatrix}, V_t = \begin{pmatrix} 0 \\ 0 \\ \vdots \\ a_t \end{pmatrix}$

其中 $U_t$ 是由 $\phi(B)U_t = a_t$ 给出的 AR(p) 过程，$r=\max(p,q+1)$，当 $j>p$ 时 $\phi_j=0$，当 $j>q$ 时 $\theta_j=0。（参见问题 10.9）

## 10.6.3 空间建模的目标

回顾在 ARMA 和 ARIMA 建模中，我们通常通过分析实现数据来估计模型参数，然后使用估计的模型用于预测未来值、谱估计等目的。给定一个状态空间模型：

```
$X_t = \Phi X_{t-1} + V_t$
$Y_t = GX_t + W_t$,
```

基本目标是在给定观测值 $Y_r, \dots, Y_t$（某些时间 $s$）的情况下估计未观测信号 $X_t$。实现这一目标的典型步骤是：

1. 估计状态模型的参数 $(\mu, \Gamma_{\Phi}, \Gamma_G, \Gamma_W)$。
2. 在均方意义下估计 $X_t$ 的最佳线性估计器（对于时间 $t$）。具体来说，我们要找到 $E(X_t|Y_r, \dots, Y_t)$。为了简单起见，我们使用 $\hat{X}_t$ 表示 $E(X_t|Y_r, \dots, Y_t)$，用均方误差 $\Gamma_t^X = E[(X_t - \hat{X}_t)(X_t - \hat{X}_t)^T]$ 表示。根据时间 $t$ 与观测观测时间 $s$ 的关系分为三类：

   a. **预测 (Prediction)**：$s < t$ 的情况。例如一步步预测 $\hat{X}_t^1, \hat{X}_t^2, \dots$。
   b. **滤波 (Filtering)**：$s = t$ 的情况。
   c. **平滑 (Smoothing)**：$s > t$ 的情况。这种情况被称为平滑，因为 $\hat{X}_t^1, \hat{X}_t^2, \dots$ 的轨迹往往比一步步预测 $\hat{X}_t^0, \hat{X}_t^2, \dots$ 或“滤波” $\hat{X}_t^1, \hat{X}_t^2, \dots$ 更平滑。

## 10.6.4 卡尔曼滤波 (Kalman Filter)

卡尔曼滤波是一种非常有用的迭代程序，用于获取方程 10.48 和 10.49 中状态模型的估计值 $\hat{X}_t^i$，初始条件为 $\hat{X}_0=\mu$ 和 $\Gamma_0$。下给出了计算 $X_t$ 的预测、滤波和平滑处理的卡尔曼递归。附录 10A 给出了预测滤波递归的证明。

### 10.6.4.1 预测

以下方程提供了一步预测 $\hat{X}_t^1$（等效于 $\hat{X}_{t+1}$）；具体来说，我们观测了 $Y_0, \dots, Y_{t-1}$ 并希望利用这些信息预测 $X_t$。卡尔曼递归如下：

```
$\hat{X}_t^1 = \mathbf{F}\hat{X}_{t-1}^1$
```

```
$\Gamma_t^1 = \mathbf{F}\Gamma_{t-1}^1\mathbf{F}' + \Gamma_v$
```

### 10.6.4.2 滤波

滤波和预测递归同时运行。例如，方程 10.50 中的预测涉及滤波项 $\hat{X}_t^1$。基于 $Y_0, \dots, Y_t$ 估计 $X_t$ 的滤波递归方程为：

```
$\hat{X}_t = \hat{X}_t^1 + \mathbf{K}_t(Y_t - \mathbf{G}\hat{X}_t^1)$
```

```
$\Gamma_t = [\mathbf{I} - \mathbf{K}_t\mathbf{G}]\Gamma_{t-1}^1$
```

其中

```
$\mathbf{K}_t = \Gamma_t^{-1}\mathbf{G}'[\mathbf{G}\Gamma_{t-1}^1\mathbf{G}' + \Gamma_v]^{-1}$
```

$\mathbf{K}_t$ 被卡尔曼增益 (Kalman gain)。
证明：附录 10A 给出了预测滤波递归的有效性证明。

### 10.6.4.3 使用卡尔曼滤波进行平滑

在此设定下，观测了 $Y_1, \dots, Y_n$，目标是估计 $t < n$ 的 $X_t$，即我们计算 $X_t^f$。递归通过使用方程 10.50 到 10.54 计算 $\hat{X}_t^f, \hat{X}_{t-1}^f, \Gamma_t^f$（对于 $t=1, \dots, n$）。然后，对于 $t=n, n-1, \dots$，我们计算：

```
$\hat{X}_t^f = \hat{X}_{t-1}^f + \mathbf{J}_{t-1}(\hat{X}_t - \hat{X}_{t-1}^f)$
```

```
$\Gamma_{t-1}^f = \Gamma_t^f + \mathbf{J}_{t-1}(\Gamma_t^f - \Gamma_{t-1}^f)\mathbf{J}_{t-1}'
```

其中

```
$\mathbf{J}_{t-1} = \hat{X}_t - \mathbf{F}\hat{X}_{t-1}^f$
```

### 10.6.4.4 h 步预测

应该注意，方程 10.50 中的预测是一步预测（或预报），即在给定随机变量 $Y_1, \dots, Y_{t-1}$ 观测值的情况下 $X_t$ 的预测器。然而，第 6 章中基于 ARMA 的预测提供了前瞻预测，同时也提供了 $h$ 步预测。状态空间方法也可用于寻找 $h$ 步预测器，即在给定随机变量 $Y_1, \dots, Y_{t-1}$ 观测值的情况下 $X_{t+h-1}$ 的预测器。$h$ 步预测器 $\hat{X}_{t+h-1}^f$ 定义为：

```
$\hat{X}_{t+h-1}^f = E(X_{t+h-1} | Y_1, \dots, Y_{t-1})$
```

根据方程 10.48，得出 $\hat{X}_{t+h-1} = \mathbf{FX}_{t+h-2} + \mathbf{V}_{t+h-1}$，所以根据方程 10.58，我们有：

```
$\hat{X}_{t+h-1}^f = E(\mathbf{FX}_{t+h-2} + \mathbf{V}_{t+h-1} | Y_1, \dots, Y_{t-1})$
= \mathbf{F}(\hat{X}_{t+h-2} | Y_1, \dots, Y_{t-1})$
= \hat{X}_{t+h-2}^f$
```

递归推，得到：

```
$\hat{X}_{t+h-1}^f = \mathbf{F}^{h-1}\hat{X}_{t-1}^f$
```

