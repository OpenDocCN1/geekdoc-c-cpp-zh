

# 可靠性框图

现在，考虑每个组件的修复时间也呈指数分布。如果硬件的平均修复时间为 $24h$，操作系统的平均修复时间为 $8h$，相应程序的平均修复时间为 $4h$，则稳态可用性可以估计为：

```
$A = \prod_{i\in{hw, os, a_1, a_2}} A_i,$
```

其中 $A_i = \mu_i/(\lambda_i + \mu_i) = MTTF / (MTTF + MTTR_i)$。

稳态可用性为 $A=0.99122$。年度停机小时为 $DTyh = (1 - A) \times 8760/h = 76.928h$。系统的平均恢复时间可以从 $A = MTTF / (MTTF + MTTR)$ 估计，因为：

```
$A \times (MTTF + MTTR) = MTTF.$
```

```
$A \times MTTR = MTTF - A \times MTTF.$
```

```
$MTTR = \frac{MTTF \times (1 - A)}{A} TR = \frac{MTTF \times UA}{A}, \quad (18.5.10)
```

其中 $UA$ 是稳态不可用性。

取稳态可用性，我们 $UA = 1 - 0.99122 = 0.00878$。由于 $MTTF = 640h$，则 $MTTR = (640 \times 0.00878)/(0.99122) = 5.67h$。

假设程序 $A_2$ 的平均失效时间可能处于 $(1000h, 2000h)$ 区间。稳态可用性和年度停机小时如图 18.7 所示。

![](img/2d1450514bb14a0cdf0eb5048614afab_91_0.png)

**示例 18.5.2。** 设计了一个由 8 个串联功能组成的系统 $S$，其目标是任务时间 $t = 400h$ 内的可靠性不低于 $0.9 (R(t) \ge 0.9)$。如果功能的失效时间是根据指数分布独立同分布的 (i.i.d.) 的，那么每个功能允许的最大失效率是多少？

八组件组件独立同分布串联系统的系统可靠性为 $R(t) = e^{-8\lambda t}$。那么：

```
$$\lambda = \frac{-Ln(R(t))}{8 \times t}$$
```

# 计算系统的性能、可靠性与可用性评估

![](img/2d1450514bb14a0cdf0eb5048614afab_92_0.png)

**图 18.7** 稳态可用性 (a) 和停机时间 (b) 随 $MTTF_{a2}$ 的函数。

由于 $R(t) \geq 0.9$，则：

$\lambda < \frac{-LnR(t)}{8 \times t}$

因此

$\lambda < \frac{-Ln0.9}{8 \times 400} = 3.2925 \times 10^{-5} f/h$。

所需的系统平均失效时间为：

$MTTF = \frac{1}{8 \times \lambda} = \frac{1}{2.63401 \times 10^{-4}} = 3796.49h$。

# 并行组合

让我们考虑由 $n$ 个组件组成的系统 $S$（见图 18.8）。如果至少有一个组件 $b_i$ 工作系统即正常，则其结构函数为：

$\Phi(X) = 1 - \prod_{i=1}^{n} (1 - x_i)$。

由于 $\Phi(X)$ 是伯努利随机变量，我们有：

$E(\Phi(X)) = P(\Phi(X)) = 1$。

![](img/2d1450514bb14a0cdf0eb5048614afab_93_0.png)

**图 18.8** 并行组合。

因此，

$P(\Phi(\mathbf{X}) = 1) = E(1 - \prod_{i=1}^{n} (1 - x_i))$。

假设组件是独立的，我们有：

$P(\Phi(\mathbf{X}) = 1) = 1 - E(\prod_{i=1}^{n} (1 - x_i))$。

$P(\Phi(\mathbf{X}) = 1) = 1 - \prod_{i=1}^{n} E(1 - x_i)$。

$P(\Phi(\mathbf{X}) = 1) = 1 - \prod_{i=1}^{n} (1 - E(x_i))$。

由于 $E(x_i) = R_i(t)$（组件 $b_i$ 的可靠性），则：

$R_P(t) = P(\Phi(\mathbf{X}) = 1)$。

因此，系统可靠性为：

$R_P(t) = 1 - \prod_{i=1}^{n} (1 - R_i(t)), \quad (18.5.11)$

# 78 计算系统的性能、可靠性与可用性评估

以及系统的不可用性

```
$UR_p(t) = \prod_{i=1}^{n} UR_i(t) = \prod_{i=1}^{n} (1 - R_i(t)), \quad (18.5.12)$
```

其中 $UR_i(t)$ 是组件 $b_i$ 的不可用性。

另一种思考系统可靠性的方法是通过其不可用性。由 $n$ 个并行组件组成的系统在每个组件失效时失效。因此，系统的不可用性 $UR(t)$ 是组件不可用性的乘积 $\prod_{i=1}^{n} UR_i(t)$。因此，作为系统可靠性 $R(t) = 1 - UR(t)$，$R(t) = 1 - \prod_{i=1}^{n} UR_i(t)$。

如果 $E(x_i) = A_i(t)$（组件 $b_i$ 的瞬时可用性），则系统的瞬时可用性为：

$A_p(t) = 1 - \prod_{i=1}^{n} (1 - A_i(t)), \quad (18.5.13)$

以及瞬时不可用性为：

$UA_p(t) = \prod_{i=1}^{n} UA_i(t) = \prod_{i=1}^{n} (1 - A_i(t)), \quad (18.5.14)$

同样，如果 $E(x_i) = A_i$（组件 $b_i$ 的稳态可用性），则系统的稳态可用性为：

$A_p = 1 - \prod_{i=1}^{n} (1 - A_i), \quad (18.5.15)$

以及稳态不可用性为：

$UA_p = \prod_{i=1}^{n} UA_i, \quad (18.5.16)$

如果 $n$ 个组件同分布，则对于每个组件 $b_i$，$A_i = MTTF/(MTTF + MTTR)$，系统的稳态可用性为：

$A_p = 1 - \prod_{i=1}^{n} \left( 1 - \frac{MTTF}{MTTF + MTTR} \right) \quad (18.5.17)$

# 可靠性框图

因此，

$A_p = 1 - \left(\frac{MTTF}{MTTF + MTTR}\right)^n \quad (18.5.18)$

如果每个组件的失效时间服从速率为 $\lambda$ 的指数分布，且每个组件的修复时间也是同分布并服从速率为 $\mu$ 的指数分布，则组件的稳态可用性为：

$A_i = \frac{\mu}{\lambda + \mu}$

因此，系统的稳态可用性为：

$A = 1 - \left(1 - \frac{\mu}{\lambda + \mu}\right)^n \quad (18.5.19)$

因此，

$A = 1 - \left(\frac{\lambda}{\lambda + \mu}\right)^n \quad (18.5.20)$

以及系统的不可用性为：

$UA = \left(\frac{\lambda}{\lambda + \mu}\right)^n \quad (18.5.21)$

考虑一个由失效时间速率为 $\lambda_1$ 和 $\lambda_2$ 的两个并行组件组成的系统。系统的可靠性为：

$R(t) = 1 - (1 - e^{-\lambda_1 t})(1 - e^{-\lambda_2 t})$

该系统的 MTTF 由：

$MTTF = \int_0^{\infty}R(t)dt = \int_0^{\infty}(1 - e^{-\lambda_1 t})(1 - e^{-\lambda_2 t})dt$

$MTTF = \int_0^{\infty}(e^{-\lambda_1 t} + e^{-\lambda_2 t} - e^{-(\lambda_1 + \lambda_2)t})dt$

$MTTF = \frac{1}{\lambda_1} + \frac{1}{\lambda_2} - \frac{1}{\lambda_1 + \lambda_2} \quad (18.5.22)$

# 80 计算系统的性能、可靠性与可用性评估

假设一个由失效时间为 $\lambda1, \lambda_2, \lambda_3$ 的三个组件组成的系统。系统的可靠性为：

$R(t) = 1 - (1 - e^{-\lambda_1 t})(1 - e^{-\lambda_2 t})(1 - e^{-\lambda_3 t})$

因此，系统的平均失效时间为：

$MTFF = \int_0^{\infty}R(t)dt = \int_0^{\infty}(1 - (1 - e^{-\lambda_1 t})(1 - e^{-\lambda_2 t})(1 - e^{-\lambda_3 t}))dt$

$MTFF = \int_0^{\infty}(e^{-\lambda_1 t} + e^{-\lambda_2 t} + e^{-\lambda_3 t} - e^{-(\lambda_1+\lambda_2)t} - e^{-(\lambda_1+\lambda_3)t} - e^{-(\lambda_2+\lambda_3)t} + e^{-(\lambda_1+\lambda_2+\lambda_3)t})dt$

$MTFF = \frac{1}{\lambda_1} + \frac{1}{\lambda_2} + \frac{1}{\lambda_3} - \frac{1}{\lambda_1+\lambda_2} - \frac{1}{\lambda_1+\lambda_3} - \frac{1}{\lambda_2+\lambda_3} + \frac{1}{\lambda_1+\lambda_2+\lambda_3} \quad (18.5.23)$

同样，具有大量组件的系统的 MTFF 应该获得。但如果组件是同分布的，则有一个闭式表达式。考虑由 $n$ 个块组成的系统 $S$，其 $TTF_i$ 同分布于速率为 $\lambda$ 的指数分布。系统的可靠性为：

$R(t) = 1 - \prod_{i=1}^{n} (1 - e^{-\lambda t}).$

$R(t) = 1 - (1 - e^{-\lambda t})^n. \quad (18.5.24)$

因此平均失效时间为：

$MTFF = \int_{0}^{\infty} R(t) dt = \int_{0}^{\infty} (1 - (1 - e^{-\lambda t})^n) dt.$

令 $x = 1 - e^{-\lambda t}$。因此，当 $t=0, x=0$，当 $t \to \infty, x=1$。对 $x$ 求导，得 $dx = \lambda e^{-\lambda t} dt$。因此：

```
$\int_{0}^{\infty} R(t) dt = \int_{0}^{\infty} (1 - (1 - e^{-\lambda t})^n) dt = \int_{0}^{1} \frac{1 - x^n}{1-x} \times \frac{1}{\lambda} dx,$
```
