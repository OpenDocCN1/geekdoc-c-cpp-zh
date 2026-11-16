
算法的第一步是从接收向量中计算 $1 \le i \le 2t$ 的综合症 $S_i = y(\alpha^i)$。此过程由练习 296 中证明的以下定理辅助。在该定理中，即使 $i > 2t$，我们也允许将 $S_i$ 定义为 $y(\alpha^i)$；在这些情况下，这些可能不是合法的综合症，因为 $c(\alpha^i)$ 可能不为 0。

## 定理 5.4.1 对所有 $i \ge 1$，$S_i^q = S_{iq}$。

## 练习 295 设 $H$ 为 $t \times n$ 矩阵

$$ H = \begin{bmatrix} 1 & \alpha & \alpha^2 & \cdots & \alpha^{n-1} \\ 1 & \alpha^2 & \alpha^4 & \cdots & \alpha^{(n-1)2} \\ \vdots & & & & \vdots \\ 1 & \alpha^t & \alpha^{2t} & \cdots & \alpha^{(n-1)t} \end{bmatrix} $$

若 $y(x) = y_0 + y_1 x + \cdots + y_{n-1} x^{n-1}$，令 $\mathbf{y} = (y_0, y_1, \dots, y_{n-1})$。最后，令 $\mathbf{S} = (S_1, S_2, \dots, S_t)$，其中 $S_i = y(\alpha^i)$。

- (a) 证明 $H\mathbf{y}^T = \mathbf{S}^T$。
- (b) 利用练习 4.4.3 和部分 (a)，解释本节中给出的综合症概念与第 1.11 节中给出的综合症概念之间的联系。

## 练习 296 证明定理 5.4.1。

综合症导致一个涉及未知错误位置和未知错误幅值的方程组。注意，由 (5.5) 可知综合症满足

$$ S_i = y(\alpha^i) = \sum_{j=1}^v e_{k_j} (\alpha^{k_j})^i = \sum_{j=1}^v e_{k_j} (\alpha^i)^{k_j}. $$

对于 $1 \le i \le 2t$。为简化记号，对于 $1 \le j \le v$，令 $E_j = e_{k_j}$ 表示坐标 $k_j$ 处的错误幅值，并令 $X_j = \alpha^{k_j}$ 表示与错误位置 $k_j$ 对应的错误位置数。由定理 3.3.1，若 $0$ 到 $n-1$ 之间的 $i$ 和 $k$ 满足 $\alpha^i = \alpha^k$，则 $i = k$。因此，知道 $X_j$ 就唯一确定了错误位置 $k_j$。采用此记法，(5.6) 变为

$$ S_i = \sum_{j=1}^v E_j X_j^i, \quad \text{for } 1 \le i \le 2t, $$

这进而导致以下方程组：

$$ \begin{aligned} S_1 &= E_1 X_1 + E_2 X_2 + \cdots + E_v X_v, \\ S_2 &= E_1 X_1^2 + E_2 X_2^2 + \cdots + E_v X_v^2, \\ S_3 &= E_1 X_1^3 + E_2 X_2^3 + \cdots + E_v X_v^3, \\ &\vdots \\ S_{2t} &= E_1 X_1^{2t} + E_2 X_2^{2t} + \cdots + E_v X_v^{2t}. \end{aligned} $$

该方程组关于 $X_j$ 是非线性的，且系数 $E_j$ 未知。策略是利用 (5.7) 建立一个涉及新变量 $\sigma_1, \sigma_2, \dots, \sigma_v$ 的线性系统，该系统将直接导出错误位置数。一旦这些已知，我们就回到系统 (5.8)，此时它是关于 $E_j$ 的线性系统，从而求解错误幅值。

为此，定义*错误定位多项式*为

$$ \sigma(x) = (1 - x X_1)(1 - x X_2) \cdots (1 - x X_v) = 1 + \sum_{i=1}^v \sigma_i x^i. $$

$\sigma(x)$ 的根是错误位置数的倒数，因此

$$ \sigma(X_j^{-1}) = 1 + \sigma_1 X_j^{-1} + \sigma_2 X_j^{-2} + \cdots + \sigma_v X_j^{-v} = 0 $$

对于 $1 \le j \le v$。两边乘以 $E_j X_j^{t+v}$ 得到

$$ E_j X_j^{t+v} + \sigma_1 E_j X_j^{t+v-1} + \cdots + \sigma_v E_j X_j^t = 0 $$

对于 $1 \le j \le v$。对 $j$ 从 $1$ 到 $v$ 求和得到

$$ \sum_{j=1}^v E_j X_j^{t+v} + \sigma_1 \sum_{j=1}^v E_j X_j^{t+v-1} + \cdots + \sigma_v \sum_{j=1}^v E_j X_j^t = 0. \quad (5.9) $$

只要 $1 \le i$ 且 $i + v \le 2t$，这些求和就是 (5.7) 中得到的综合症。因为 $v \le t$，(5.9) 变为

$$ S_{t+v} + \sigma_1 S_{t+v-1} + \sigma_2 S_{t+v-2} + \cdots + \sigma_v S_t = 0 $$

或

$$ \sigma_1 S_{t+v-1} + \sigma_2 S_{t+v-2} + \cdots + \sigma_v S_t = -S_{t+v} \quad (5.10) $$

对 $1 \le i \le v$ 有效。因此，若我们求解矩阵方程

$$ \begin{bmatrix} S_1 & S_2 & S_3 & \cdots & S_{v-1} & S_v \\ S_2 & S_3 & S_4 & \cdots & S_v & S_{v+1} \\ S_3 & S_4 & S_5 & \cdots & S_{v+1} & S_{v+2} \\ \vdots & & \vdots & & & \vdots \\ S_v & S_{v+1} & S_{v+2} & \cdots & S_{2v-2} & S_{2v-1} \end{bmatrix} \begin{bmatrix} \sigma_v \\ \sigma_{v-1} \\ \vdots \\ \vdots \\ \sigma_1 \end{bmatrix} = \begin{bmatrix} -S_{v+1} \\ -S_{v+2} \\ -S_{v+3} \\ \vdots \\ -S_{2v} \end{bmatrix} \quad (5.11) $$

该方程源自 (5.10)。我们算法的第二步是求解 (5.11) 以得到 $\sigma_1, \dots, \sigma_v$。

完成此第二步后，$\sigma(x)$ 已确定。然而，确定 $v(x)$ 受到我们不知道 $v$ 的事实所复杂化，因此我们不知道所涉系统的大小。我们正在寻找 $v$ 取最小值的解，这由以下辅助定理辅助。

## 辅助定理 5.4.2 设 $\mu \le t$ 且

$$ M_\mu = \begin{bmatrix} S_1 & S_2 & \cdots & S_\mu \\ S_2 & S_3 & \cdots & S_{\mu+1} \\ \vdots & & & \vdots \\ S_\mu & S_{\mu+1} & \cdots & S_{2\mu-1} \end{bmatrix}. $$

若 $\mu = v$，则 $M_\mu$ 非奇异；若 $\mu > v$，则 $M_\mu$ 奇异；其中 $v$ 为已发生错误的数量。

证明：若 $\mu > v$，令 $X_{v+1} = X_{v+2} = \cdots = X_\mu = 0$ 且 $E_{v+1} = E_{v+2} = \cdots = E_\mu = 0$。练习 297 表明，若 $A_\mu$ 和 $B_\mu$ 由以下给出

$$ A_\mu = \begin{bmatrix} 1 & 1 & \cdots & 1 \\ X_1 & X_2 & \cdots & X_\mu \\ \vdots & \vdots & & \vdots \\ X_1^{\mu-1} & X_2^{\mu-1} & \cdots & X_\mu^{\mu-1} \end{bmatrix} \text{ and } B_\mu = \begin{bmatrix} E_1 X_1 & 0 & \cdots & 0 \\ 0 & E_2 X_2 & \cdots & 0 \\ \vdots & \vdots & & \vdots \\ 0 & 0 & \cdots & E_\mu X_\mu \end{bmatrix}, $$

则 $M_\mu = A_\mu B_\mu A_\mu^T$。因此 $\det M_\mu = \det A_\mu \det B_\mu \det A_\mu = 0$，因为 $B_\mu$ 是对角线上为 0 的对角矩阵。若 $\mu = v$，则 $\det B_\mu \neq 0$，因为 $B_\mu$ 是对角线上仅有非零项的对角矩阵。此外，由辅助定理 4.5.1，$\det A_\mu \neq 0$，因为 $A_\mu$ 是具有互异 $X_1, \dots, X_\mu$ 的范德蒙矩阵。因此，若 $\mu = v$，则 $M_\mu$ 非奇异。

## 练习 297

以下记号由辅助定理 5.4.2 给出：(a) 证明若 $\mu > v$，则对 $1 \le i \le 2t$ 有 $S_i = \sum_{j=1}^\mu E_j X_j^i$。 (b) 证明 $M_\mu = A_\mu B_\mu A_\mu^T$。$\blacklozenge$

为执行算法的第二步，我们尝试猜测错误数量 $v$。将我们的猜测记为 $\mu$，并从 $\mu = t$ 开始，这是 $v$ 可能取的最大值。我们试图求解的线性系统 (5.11) 的系数矩阵是辅助定理 5.4.2 中的 $M_\mu$。若 $M_\mu$ 奇异，我们将猜测 $\mu$ 减小到 $\mu = t - 1$，并判断 $M_\mu = M_{t-1}$ 是否奇异。只要得到奇异矩阵，我们就继续将错误数量的猜测 $\mu$ 减小 1，直到某个 $M_\mu$ 非奇异。令 $v = \mu$，求解 (5.11) 从而确定 $\sigma(x)$。

第三步是求 $\sigma(x)$ 的根并将其倒置以确定错误位置数。这通常通过穷举搜索完成，检查 $0 \le i < n$ 的 $\sigma(\alpha^i)$。第四步是将这些数字代入 (5.8) 并求解该线性系统以得到错误幅值 $E_j$。事实上，我们只需考虑 (5.8) 中的前 $v$ 个方程，理由如下。前 $v$ 个方程的系数矩阵的行列式为

$$ \det \begin{bmatrix} X_1 & X_2 & \cdots & X_v \\ X_1^2 & X_2^2 & \cdots & X_v^2 \\ \vdots & \vdots & & \vdots \\ X_1^v & X_2^v & \cdots & X_v^v \end{bmatrix} = X_1 X_2 \cdots X_v \det \begin{bmatrix} 1 & 1 & \cdots & 1 \\ X_1 & X_2 & \cdots & X_v \\ \vdots & \vdots & & \vdots \\ X_1^{v-1} & X_2^{v-1} & \cdots & X_v^{v-1} \end{bmatrix} . $$

右侧行列式是一个范德蒙矩阵的行列式；后者非零，因为 $X_j$ 互异。

因此，BCH 码的 Peterson-Gorenstein-Zierler 解码算法如下：

- I. 计算 $1 \le i \le 2t$ 的综合症 $S_i = y(\alpha^i)$。
- II. 按顺序 $\mu = t, \mu = t - 1, \dots$ 判断 $M_\mu$ 是否奇异，在 $M_\mu$ 首次非奇异的 $\mu$ 值处停止。设 $v = \mu$ 并求解 (5.11) 以确定 $\sigma(x)$。
- III. 通过计算 $0 \le i < n$ 的 $\sigma(\alpha^i)$ 求 $\sigma(x)$ 的根。将根倒置以得到错误位置数 $X_j$。
- IV. 求解 (5.8) 的前 $v$ 个方程以得到错误幅值 $E_j$。
