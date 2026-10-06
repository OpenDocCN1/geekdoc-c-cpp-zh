

随机近似

将递归式 (8.67) 的两边乘以 $(n+1)^{\rho/2}$，得到关于 Z 的递归式：

```
$Z_{n+1} = (1+\varepsilon_n)Z_n + \frac{1}{(n+1)^{\rho}}\A(1+\varepsilon_n)Z_n+(n+1)^{\rho/2}\Delta_{n+1}\}; (8.71)
```

其中 $\varepsilon_n = O(n^{-1})$。结论 (ii) 得之得出。

## 8.7.3 Polyak–Ruppert 平均化

我们以使用 PJR 平均化得到的误差协方差近似结束，记为

```
$\bar{\Sigma}_{n_0}^{det} = E\{(\theta_n^0 - \theta^*)\{\theta_n^0 - \theta^*)^T\}$;
```

目标是证明近似 $n_0\bar{\Sigma}_{n_0}^{det} \approx \Sigma_{\Delta}^*$，其中 $\Sigma_{\Delta}^* \coltriangleq A^{-1}\Sigma_{\Delta}(A^{-1})^T$ 表示最优渐近协方差矩阵。

以下引理是我们的起点。

- **引理 8.11** Polyak–Ruppert 估计可以表示为：

```
$\theta_N^0 = \theta^* - \frac{1}{N-N_0}A^{-1}[M_N^0 - S_f^N + S_T^N + S_{\Delta}^N];$ (8.72)
```

其中 $A = A(\theta^*)$，

```
$M_N^0 = \sum_{n=N_0+1}^N f_{n+1}(\theta^0) = \sum_{n=N_0+1}^N \Delta_{n+1};$ (8.73a)
```

```
$S_f^N = \sum_{n=N_0+1}^N f_{n+1}(\theta_n^0);$ (8.73b)
```

```
$S_T^N = \sum_{n=N_0+1}^N E_f(\theta_n^0);$ (8.73c)
```

```
$S_{\Delta}^N = \sum_{n=N_0+1}^N {\Delta_{n+1} - \Delta_{n+1}^{\infty}\};$ (8.73d)
```

其中 $E_f(\theta)$ 的定义如 (8.65) 和 (8.3b) 所示。

```
$$\Delta_{n+1} = f_{n+1}(\theta_n^0) - \bar{f}(\theta_n^0);$ (8.74)
```

*证明* 根据定义。

```
$f_{n+1}(\theta_n^0) = \bar{f}(\theta_n^0) + \Delta_{n+1} = A[\theta_n^0 - \Delta_{n+1}^{\infty}] + E_f(\theta_n^0) + {\Delta_{n+1} - \Delta_{n+1}^{\infty}\};
```

通过等方程每边乘以 $A^{-1}$，对 $n$ 求和并重新排列项，即可得到该表示。

在一般条件下，第一项 (8.73a) 占据主导地位，由此我们得到

```
$$(N-N_0)\bar{\Sigma}_N^M = \frac{1}{N-N_0}ACov(M_N^0)A^T + o(1) = \Sigma_0^* + o(1);$ (8.75)
```

## 8.7 理论

证明另外两个项应该相对较小是困难的：

- (i) 当 $f$ 光滑时，$E_f(\theta_n^f) = O(\|\theta_n^f - \theta^*\|^2)$。
- (ii) 我们只能期望 $\Delta_{n+1} - \Delta_n^\infty = O(\|\theta_n^f - \theta^*\|)$（不带平方）。在 (SA2) 下，和 $S_N^f$ 才是较小的（相对于 $M_N$）。

考虑到它们的定义非常相似，$\{S_N^f\}$ 相对于 $\{M_N^\infty\}$ 是较小的这是一个简单的奇迹。通过阶表示，通过重新排列界限 (8.10a) 中的项，使得 $\{S_N^f\}$ 的界成为可能：

```
$f_{n+1}(\theta_n^f) = \frac{1}{\beta_{n+1}}[theta_{n+1}^f - \theta_n^f], \quad (8.76)$
```

其中 $\theta_n^f = \theta_n' - \theta^*$。使用这个简单的变换可以得到和的一个用表示：

**引理 8.2 (分部求法)** 对于任意两个实值序列 $\{x_n, y_n : n \geq 0\}$ 和整数 $0 \leq N_0 < N$，

```
$$\sum_{n=N_0+1}^N x_n(y_n - y_{n-1}) = x_N y_N - x_{N_0} y_{N_0} - \sum_{n=N_0+1}^N (x_{n+1} - x_n)y_n.
```

因此，

```
$S_N^f = \sum_{n=N_0+1}^N \frac{1}{\beta_n}[\theta_{n+1}^f - \theta_n^f] = \frac{1}{\beta_{N_0}}\theta_{N_0}^f - \frac{1}{\beta_N}\theta_N^f - \sum_{n=N_0+1}^N (\frac{1}{\beta_n} - \frac{1}{\beta_{n+1}})\theta_n^f; \quad (8.77)$
```

后续的假设意味着对每个项都有强界限。

## PJR 平均化的假设

对于固定的常数 $b_\delta, b_f, b_Z$，以及每个 $n \geq 1$，

- (PR1) 步长 $\beta_n = n^{-\rho}$ 其中 $\frac{1}{2} < \rho < 1$。
- (PR2) $E[\Delta_n^\infty] = \Delta_n^\infty + O(n^{-\rho})$ 对于某些 $\rho \in (0,1)$。$E[\|\Delta_{n+1} - \Delta_n^\infty\|^2] \leq b_\delta|\theta_n^f|^2$。
- (PR3) $E[E_f(\theta_n^f)] \leq b_f|\theta_n^f|^2$。
- (PR4) $E[\|Z_n\|^4] \leq b_Z$，其中 $Z_n = n^{\rho/2}$。

再次，鞅差假设 (PR2) 比要求的更强，允许进行计算。$Z$ 的四阶矩在 (PR2) 的强化下足以建立：

```
$E[\|\Delta_{n+1} - \Delta_n^\infty\|^4] \leq b_\delta\|\theta_n^f\|^4.
```

对于常数 $b_\delta$，结合性质 (i)，PJR 的最优收敛性已经建立。为了简单，我们在定理 8.13 中取 $N_0 = 0$。

 随机近似

**定理 8.13** 在 (PR1)-(PR4)，考虑对于 $N \ge 1$ 和 $N_0 = 0$ 得到的 PJR 方案。那么 (8.75) 以如下形式成立：

```
$$\Sigma_0^N = \frac{1}{N}\Sigma_0^* + \Sigma_N^N
```

其中 $\tilde{\Sigma}_0 = A\Sigma_0 A^T$，$\|\Sigma_N^N\| \le O(N^{-\delta})$，且 $\delta = \min(\frac{1}{2}-\rho, \frac{\rho}{2}) > 0$。因此，$\Sigma$ 的渐近收敛是优的。我们需要简单的求和比较：

**引理 8.14** 在 (PR1) 下满足以下界限：

```
$$\sum_{n=1}^N [\frac{1}{\beta_{n+1}} - \frac{1}{\beta_n}] \sqrt{\beta_n} = 2N^{\rho/2} + O(1) \quad \sum_{n=1}^N \beta_n = \frac{1}{1-\rho}N^{1-\rho} + O(1).
```

**证明** 每个界限通过将和与积分比较得到。对于第一个界限：

```
\sum_{n=1}^N [\frac{1}{\beta_{n+1}} - \frac{1}{\beta_n}] \sqrt{\beta_n} = \sum_{n=1}^N [(n+1)^{\rho} - n^{\rho}]n^{-\rho/2}
= \rho \int_{1}^N x^{-1+\rho}x^{-\rho/2} dx + O(1)\\
= \rho [\frac{x^{\rho/2}}{\rho/2}]_1^N + O(1) = 2N^{\rho/2} + O(1).
```

第二个界限的证明类似的。对于证明的剩余部分，方便使用向量符号：

```
||Z||_2 = (E[|Z|^2])^{1/2}.
```

为了完善界限 (8.75) 当 $N_0 = 0$，我们从 (8.72) 开始，写为：

```
\bar{\mathcal{E}}_N = \mathcal{V}_N - \mathcal{E}_N, \quad \text{where} \mathcal{V}_N = \frac{1}{A^{-1}}M^N \quad \text{and} \mathcal{E}_N = \frac{1}{A^{-1}}[S_N^T].
```

**引理 8.15** 协方差允许近似：

```
\Sigma_N^{cov} = Cov(\mathcal{V}_N) + \Sigma_N^N
```

其中 $Cov(\mathcal{V}_N) = \frac{1}{N}\Sigma_0^* + O(N^{-2})$，$\|\Sigma_N^N\| \le \epsilon_N$，其中 $\epsilon_N = 2\|\mathcal{V}_N\|_2 + \|S_N^T\|_2$。

**证明** 首先注意协方差 $\mathcal{V}_N$ 的近似直接来自 (PR2)。接下来我们通过定义得到：

```
\Sigma_N^{cov} = E[(\mathcal{V}_N - \mathcal{E}_N)(\mathcal{V}_N - \mathcal{E}_N)^T] = Cov(\mathcal{V}_N) + \Sigma_N^N.
```

证明的剩余部分涉及误差项最大特征值的界限：

```
\max_{||v||=1} v^T \Sigma_N v
```

对于任意 $v \in \mathbb{R}^d$，我们得到：

```
v^T \Sigma_N v = E[2(\mathcal{V}_N v) + (\mathcal{E}_N v)^2].
```

根据向量 Cauchy-Schwarz 不式，当 $||v||=1$ 时有 $\|\mathcal{E}_N\| \le \|\mathcal{V}_N\|$ 和 $\|\mathcal{V}_N\| \le O(N^{-1})$，根据随机变量期望的 Cauchy-Schwarz 不式，我们得到：

```
v^T \Sigma_N v \le 2\|\mathcal{V}_N\|^2 \|\mathcal{E}_N\|_2 + \epsilon_N^2 = \epsilon_N.
```

定理 8.13 的证明我们根据定义和三角形不等式遵循：

```
\epsilon_N \le 2\|\mathcal{V}_N\| \frac{1}{2}(\|S_K^N\|^2 + \|S_L^N\|^2 + \|S_S^N\|^2) + N^{-2}(\|S_K^N\|^2 + \|S_L^N\|^2 + \|S_S^N\|^2)
```

并且 $\|\mathcal{V}_N\|^2 \le O(N^{-1/2})$，给出 $N^{-3/2}\|S_T^N\|_2 \le O(N^{-1-\rho})$。

应用 (8.77) 和引理 8.14：

```
\|S_T^N\|_2 \le \sum_{n=1}^{N} \|E_f(\theta_n)\|_2 \le bf\sqrt{b_z}\sum_{n=1}^{N} \beta_n \le O(N^{1-\rho}).$$
```

