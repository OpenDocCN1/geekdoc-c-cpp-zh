

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_307_0.png)

图 9.7 线性回归示例，展示了基于 χ² 优值函数拟合质量相对于简单平方偏差和 S 的定性改善。

## 9.6 多线性回归模型

作为上一节介绍的线性回归的推广，下面我们考虑多线性回归，其重要特例是多项式回归。

多线性回归中的任务是拟合由 x 的任意函数的线性组合表示的模型，

$$F(x;\mathbf{a}) = \sum_{j=1}^{m} a_j F_j(x), \tag{9.49}$$

到一组 n 个观测数据点，$(x_i, y_i)$。该方法的线性性质仅指 $m$ 个参数 $a_j$ 进入模型的方式。至于基函数 $F_j(x)$，它们具有固定的形式，不依赖于模型参数，并且相对于 $x$ 可以是任意非线性的。

最常用的基集是整数幂族，$1, x, x^2, \dots, x^{m-1}$，多项式回归基于此，以及构成傅里叶级数的三角函数 $\sin kx$ 和 $\cos kx$。作为多项式回归的特例，线性回归仅涉及基函数 1 和 $x$。

多线性回归的 $\chi^2$ 优值函数形式为

$$\chi^2(\mathbf{a}) = \sum_{i=1}^{n} \frac{1}{\sigma_i^2} \left[ y_i - \sum_{j=1}^{m} a_j F_j(x_i) \right]^2, \tag{9.50}$$

其中 $\sigma_i$ 如前所述，表示与观测值 $y_i$ 相关的观测误差（标准差）。该形式主义在误差未知的情况下也适用，只需将所有 $\sigma_i$ 设为相等，例如 $\sigma_i = 1$。

最优模型参数使 $\chi^2$ 优值函数最小化，或等价地使其偏导数为零：

$$\frac{\partial \chi^2}{\partial a_k} \equiv -2 \sum_{i=1}^{n} \frac{1}{\sigma_i^2} \left[ y_i - \sum_{j=1}^{m} a_j F_j(x_i) \right] F_k(x_i) = 0, \quad k = 1,2,\dots,m. \tag{9.51}$$

改变求和顺序并重新排列项，可得到多线性拟合问题的所谓正规方程组，即

```
∑_{j=1}^{m} c_{kj} a_j = b_k,   k = 1,2,...,m,   (9.52)
```

其解即为所求的最优模型参数。系统矩阵 C = [c_{kj}]_{mm} 和常数项向量 b = [b_k]_m 定义为

```
c_{kj} = ∑_{i=1}^{n} 1/σ_i^2 F_k(x_i) F_j(x_i),   (9.53)
```

```
b_k = ∑_{i=1}^{n} y_i/σ_i^2 F_k(x_i).   (9.54)
```

与优化参数相关的平方不确定度（方差）的估计可通过应用一般公式得到

```
σ_{a_j}^2 = ∑_{i=1}^{n} σ_i^2 (∂a_j/∂y_i)^2 .   (9.55)
```

为计算所涉及的导数，我们形式上从正规方程组 (9.52) 中表达参数 a_j，

```
a_j = ∑_{k=1}^{m} c'_{jk} b_k = ∑_{k=1}^{m} c'_{jk} ∑_{i=1}^{n} y_i/σ_i^2 F_k(x_i),
```

其中 c'_{jk} 是逆系统矩阵的元，C^{-1} = [c'_{jk}]_{mm}。因此参数的导数为

```
∂a_j/∂y_i = ∑_{k=1}^{m} c'_{jk} 1/σ_i^2 F_k(x_i)
```

并将它们代入方差公式 9.55，改变求和顺序，并考虑矩阵元 c_{kj} 的定义 (9.53)，可依次得到

```
σ_{a_j}^2 = ∑_{k,l=1}^{m} c'_{jk} c'_{jl} ∑_{i=1}^{n} 1/σ_i^2 F_k(x_i) F_l(x_i) = ∑_{k,l=1}^{m} c'_{jk} c'_{jl} c_{kl} = ∑_{l=1}^{m} c'_{jl} δ_{jl}.
```

这里我们还使用了恒等式 ∑_{k=1}^{m} c'_{jk} c_{kl} = δ_{jl}，其中 δ_{jl} 是克罗内克 delta。因此，优化参数 a_j 的平方不确定度为

```
σ_{a_j}^2 = c'_{jj},   (9.56)
```

即为正规方程组系统矩阵逆 C^{-1} 的对应对角元 c'_{jj}。更广义地，c'_{jk} 表示参数对 (a_j, a_k) 相关的协方差 (Press et al. 2007)。

对多线性回归问题描述的正规方程方法的实现见列表 9.9。函数 MultiFit 接收观测数据点在数组 x 和 y 中的 n 个坐标，以及 y 坐标的标准差在数组 sigmy 中。模型参数的数量由参数 npar 指定。如果控制参数 iopt 设为 0，则数组 sigmy 的所有分量在内部初始化为 1，近似退化为基于优值函数

$$S = \sum_{i=1}^{n} \left[ y_i - \sum_{j=1}^{m} a_j F_j(x_i) \right]^2.$$

的最小二乘回归。

函数 MultiFit 在数组 a 和 sigma 中分别返回调整后的模型参数及其相关不确定度。作为拟合质量的综合指标，例程还通过 chi2 返回用最优参数计算的 χ² 优值函数值。

构成模型的基函数 F_j(x) 必须由单独的用户函数求值，该函数在 MultiFit 内部以通用名称 Func 识别，其实际名称通过参数列表传递。对于给定的自变量 x，用户函数在数组 func 的分量中返回 npar 个基函数的值。

原则上，正规方程组 (9.52) 可由任何通用方法求解。然而，由于评估参数不确定度时也需要系统矩阵的逆，最方便的方法是第 7 章讨论的 Gauss–Jordan 方法，它能够同时求解系统并就地求逆系统矩阵。开发的例程 GaussJordan 求解矩阵方程 A·X = B，其中 A 是方阵 (n × n)，而 B 和 X 是 (n × m) 矩阵，退出时用解 X 替换常数项 B，并用其逆 A⁻¹ 替换系统矩阵 A。通过从例程 MultiFit 对 GaussJordan 的特定调用，初始包含拟合矩阵的数组 c 返回其逆（协方差矩阵），而常数项数组 b 被系统解（模型参数）替换。作为技术细节，尽管在当前情况下矩阵方程简化为仅具有常数项向量的普通线性系统 (m = 1)，但出于与 GaussJordan 参数兼容的原因，b 必须声明为二维数组，具有 npar 行和单列。

图 9.8 通过一个简单示例说明了多线性回归方法，其中“观测”数据点（用圆圈表示）通过对函数 f(x) = sin x + cos x

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_310_0.png)

图 9.8 利用例程 MultiFit 执行的多线性回归。观测数据取自函数 f(x) = sin x + cos x。

### 列表 9.9  多线性回归 (Python 编码)

```
```python
#==============================================================================
def MultiFit(x, y, sigmy, n, iopt, a, sigma, npar, Func):
#------------------------------------------------------------------------------
# Determines the coefficients a[i], i=1,...,npar of a multilinear model
#     F(x;a) = a[1] * func[1](x) + ... + a[npar] * func[npar](x)
# and the associated uncertainties, sigma[i], for a set of observed data
# points by "Chi-square" regression
# x[]     - x-coordinates of observed data, i = 1,...,n
# y[]     - y-coordinates of observed data
# sigmy[]  - standard deviations of observed data
# n       - number of observed data points
# iopt    - iopt == 0 - initializes sigmy[i] = 1 (equal weights)
#           iopt != 0 - uses the received values of sigmy[i]
# a[]     - parameters of the multilinear model (output)
# sigma[] - uncertainties associated with the model parameters (output)
# npar    - number of model parameters
# chi2    - value of Chi-square merit function for the output parameters
# Func()  - user function returning for a given argument x the values of the
#           basis functions func[i](x):
#               Func(x, func, npar)
# Calls: GaussJordan (linsys.py)
#==============================================================================

    c = [[0]*(n+1) for i in range(n+1)]
    b = [0]*2 for i in range(n+1)]
    func = [0]*(npar+1)

    if (iopt == 0):
        for i in range(1,n+1): sigmy[i] = 1e0       # iopt = 0: equal weights

    for i in range(1,npar+1):                                      # initialization
        for j in range(1,npar+1): c[i][j] = 0e0
        b[i][1] = 0e0

    for i in range(1,n+1):                              # generate the system matrices
        yi = y[i]
        Func(x[i],func,npar)                            # evaluate the basis functions
        f = 1e0/(sigmy[i]*sigmy[i])
        for j in range(1,npar+1):
            fj = f * func[j]
            for k in range(1,npar+1): c[j][k] += fj * func[k]
            b[j][1] += fj * yi

    det = GaussJordan(c,b,npar,1)                                  # solve the system

    for i in range(1,npar+1):
        a[i] = b[i][1]                                             # model parameters
        sigma[i] = sqrt(c[i][i])                          # parameter uncertainties

    chi2 = 0e0                                           # value of Chi-square function
    for i in range(1,n+1):
        Func(x[i],func,npar)                              # evaluate the model function
        f = 0e0
        for j in range(1,npar+1): f += a[j]*func[j]
        f = (y[i] - f)/sigmy[i]
        chi2 += f*f
    return chi2
```
```

采样得到。

