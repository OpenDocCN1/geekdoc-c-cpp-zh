

对于精心选取的自变量 0、π/2、π、3π/2 和 π。在清单 9.10 的示例程序中，模型函数被选为具有两个可调参数：

F(x; a₁, a₂) = a₁ sin x + a₂ cos x，

基函数 F₁(x) = sin x 和 F₂(x) = cos x 的计算由用户函数 Func 执行。MultiFit 返回的调整后模型参数为 a₁ = 0.999929 和 a₂ = 1.000212，优值函数 χ² = 0.000000。值得注意的是，模型函数的拟合过程在舍入误差范围内恢复了提供“观测”数据的原始函数 f(x) 的系数。

将模型函数推广为包含更多基函数（1、sin x、cos x、sin 2x、cos 2x 等），原则上可以使用 MultiFit 例程从表格化的函数关系中提取傅里叶级数系数（见问题 9.9）。

在多项式回归的特殊情况下，具有 m 个可调参数的模型函数是 (m − 1) 次多项式：

F(x; a) = Σ_{j=1}^{m} a_j x^{j-1}. (9.57)

## 清单 9.10 多元线性回归的应用（Python 代码）

```
# Multilinear fit
from math import *
from modfunc import *

def Func(x, func, npar):
    func[1] = sin(x)      # returns the basis functions sin(x) and cos(x)
    func[2] = cos(x)

# main

n = 5                                   # number of observed data
npar = 2                                # number of model parameters

x     = [0]*(n+1)                      # x-coordinates of observed data
y     = [0]*(n+1)                      # y-coordinates of observed data
sigmy = [0]*(n+1)                      # standard deviations of observed data
func  = [0]*(npar+1)                   # values of basis functions
a     = [0]*(npar+1)                    # model parameters
sigma = [0]*(npar+1)                   # uncertainties of parameters

x[1] = 0e000; y[1] = 1e000              # observed data generated from:
x[2] = 0.785; y[2] = 1.414              # f(x) = sin(x) + cos(x)
x[3] = 1.571; y[3] = 1e000
x[4] = 2.356; y[4] = 0e000
x[5] = 3.141; y[5] = -1e000

iOpt = 0                               # least squares fit: equal errors sigmy
chi2 = MultiFit(x,y,sigmy,n,iOpt,a,sigma,npar,Func)

print("Multilinear fit:")
for i in range(1,npar+1):
    print("[a{0:d}] = {1:8.4f} +/- {2:8.4f}".format(i,a[i],sqrt(sigma[i])))
print("Chi^2 = {0:8.4f}".format(chi2))
```

## 清单 9.11 多项式回归（Python 代码）

```
#===============================================================================
def PolFit(x, y, sigmy, n, iopt, a, sigma, npar):
#-------------------------------------------------------------------------------
# Determines the coefficients a[i], i=1,...,npar of a polynomial model
#     F(x;a) = a[1] * x^(npar-1) + a[2] * x^(npar-2) + ... + a[npar]
# and the associated uncertainties, sigma[i], for a set of observed data
# points by "Chi-square" regression
# x[]      - x-coordinates of observed data, i = 1,..,n
# y[]      - y-coordinates of observed data
# sigmy[]  - standard deviations of observed data
# n        - number of observed data points
# iopt     - iopt == 0 - initializes sigmy[i] = 1 (equal weights)
#            - iopt != 0 - uses the received values of sigmy[i]
# a[]      - parameters of the polynomial model (output)
# sigma[]  - uncertainties associated with the model parameters (output)
# npar     - number of model parameters (polynomial order + 1)
# chi2     - value of Chi-square merit function for the output parameters
# Calls: GaussJordan (linsys.py)
#-------------------------------------------------------------------------------

c = [[0]*(n+1) for i in range(n+1)]
b = [[0]*2 for i in range(n+1)]
func = [0]*(npar+1)

if (iopt == 0):
    for i in range(1,n+1): sigmy[i] = 1e0        # iopt = 0: equal weights

for i in range(1,npar+1):                       # initialization
    for j in range(1,npar+1): c[i][j] = 0e0
    b[i][1] = 0e0

for i in range(1,n+1):                          # generate the system matrices
    xi = x[i]; yi = y[i]
    func[npar] = 1e0                            # basis functions 1, x, x^2,...
    for j in range(npar-1,0,-1): func[j] = xi * func[j+1]
    f = 1e0/(sigmy[i]*sigmy[i])
    for j in range(1,npar+1):
        fj = f * func[j]
        for k in range(1,npar+1): c[j][k] += fj * func[k]
        b[j][1] += fj * yi

det = GaussJordan(c,b,npar,1)                   # solution: corrections da

for i in range(1,npar+1):
    a[i] = b[i][1]                              # model parameters
    sigma[i] = sqrt(c[i][i])                    # parameter uncertainties

chi2 = 0e0                                      # value of Chi-square function
for i in range(1,n+1):
    xi = x[i]                                   # evaluate the model function
    f = a[1]
    for j in range(2,npar+1): f = f*xi + a[j]
    f = (y[i] - f)/sigmy[i]
    chi2 += f*f

return chi2
```

相应的用户函数可以利用连续基函数 1、x、x²、... 之间的简单递推关系，以最有效的方式进行编码：

```
def Func(x, func, npar):  # returns basis functions 1, x, x^2,...,x^(npar-1)
    func[npar] = 1e0                 # basis functions 1, x, x^2,...
    for i in range(npar-1,0,-1): func[i] = x * func[i+1]
```

实现多项式回归的另一种选择是像清单 9.11 那样重写 MultiFit 例程，以便就地计算基函数并且不调用任何用户函数。PolFit 例程对于从表格化的函数关系中提取幂级数系数等应用非常有用。

## 9.7 非线性回归：莱文伯格–马夸特方法

最小二乘法原则上可以用于将任意模型函数拟合到观测数据点，但通常需要求解非线性方程组以确定最优模型参数。这种方法在这种情况下称为非线性回归，相应的算法通常具有相当高的复杂度。与多元线性回归（模型参数通过求解线性方程组一步确定）不同，非线性回归从初始猜测开始，通过迭代来改进模型参数。

优值函数被认为具有一般形式：

χ²(a) = Σ_{i=1}^n 1/σ_i² [y_i - F(x_i; a)]².  (9.58)

为了表征 χ² 的最小值，考虑其关于参数值的级数展开是有用的：

χ²(a + δa) = χ²(a) + Σ_{j=1}^m ∂χ²/∂a_j δa_j + 1/2 Σ_{j,l=1}^m ∂²χ²/∂a_j∂a_l δa_j δa_l + ⋯,  (9.59)

其中 δa 是参数修正向量。优值函数在使其梯度为零的修正集合 δa 处出现极值，或者等价地，使其关于所有参数的偏导数为零：

∂χ²/∂a_k |_{a+δa} = 0,  k = 1,2,...,m.  (9.60)

修正参数下的 χ² 导数由展开式 9.59 得出，

∂χ²/∂a_k |_{a+δa} = Σ_{j=1}^m ∂χ²/∂a_j δ_{jk} + 1/2 Σ_{j,l=1}^m ∂²χ²/∂a_j∂a_l (δ_{kj}δa_l + δa_jδ_{kl}) + ⋯
= ∂χ²/∂a_k + Σ_{j=1}^m ∂²χ²/∂a_k∂a_j δa_j + ⋯  (9.61)

上述表达式中参考参数的一阶导数可以从优值函数的定义 (9.58) 推导得出：

$$\frac{\partial \chi^2}{\partial a_k}=-2\sum_{i=1}^{n}\frac{1}{\sigma_i^2}\left[y_i-F(x_i;\mathbf{a})\right]\frac{\partial F(x_i;\mathbf{a})}{\partial a_k}. \tag{9.62}$$

类似地，对于构成优值函数所谓*海森矩阵*的混合二阶导数，可以得到：

$$\frac{\partial^2\chi^2}{\partial a_k\partial a_j}=2\sum_{i=1}^{n}\frac{1}{\sigma_i^2}\left\{\frac{\partial F(x_i;\mathbf{a})}{\partial a_k}\frac{\partial F(x_i;\mathbf{a})}{\partial a_j}-\left[y_i-F(x_i;\mathbf{a})\right]\frac{\partial^2F(x_i;\mathbf{a})}{\partial a_k\partial a_j}\right\}$$
$$\approx 2\sum_{i=1}^{n}\frac{1}{\sigma_i^2}\frac{\partial F(x_i;\mathbf{a})}{\partial a_k}\frac{\partial F(x_i;\mathbf{a})}{\partial a_j}. \tag{9.63}$$

在 χ² 最小值附近，混合二阶导数 ∂²F(x_i;𝐚)/∂a_k∂a_j 与一阶导数相比可以忽略不计；此外，由于它们还乘以随机取号且随机分布的 [y_i-F(x_i;𝐚)]，这些项在求和时往往在统计上相互抵消。进一步地，对 χ² 的导数施加消失条件 (9.60)，并将其展开式 9.61 限制在线性近似，可以得到关于参数修正的以下线性方程组（Press 等，2007）：

$$\sum_{j=1}^{m}c_{kj}\delta a_j=b_k,\qquad k=1,2,\ldots,m. \tag{9.64}$$

其中矩阵元素定义为

$$c_{kj}\equiv\frac{1}{2}\frac{\partial\chi^2}{\partial a_k\partial a_j}=\sum_{i=1}^{n}\frac{1}{\sigma_i^2}\frac{\partial F(x_i;\mathbf{a})}{\partial a_k}\frac{\partial F(x_i;\mathbf{a})}{\partial a_j}, \tag{9.65}$$

$$b_k=-\frac{1}{2}\frac{\partial\chi^2}{\partial a_k}=\sum_{i=1}^{n}\frac{1}{\sigma_i^2}\left[y_i-F(x_i;\mathbf{a})\right]\frac{\partial F(x_i;\mathbf{a})}{\partial a_k}. \tag{9.66}$$

c_{kj} 等于海森矩阵元素的一半，矩阵 C=[c_{kj}] 称为*曲率矩阵*。

*远离 χ² 的最小值时*，*展开式 9.59 可能无法很好地局部近似* χ²(𝐚+δ𝐚)。在这种情况下，为了加速向最小值收敛的过程，可以只保留海森矩阵的对角元素，因此优值函数的梯度分量 (9.61) 变为

$$\left.\frac{\partial\chi^2}{\partial a_k}\right|_{\mathbf{a}+\delta\mathbf{a}}\approx\frac{\partial\chi^2}{\partial a_k}+\frac{\partial^2\chi^2}{\partial a_k^2}\delta a_k. \tag{9.67}$$

利用记号 (9.65) 和 (9.66)，χ² 导数消失的条件 (9.60) 导出了以下关于参数修正的简化方程：

$$c_{kk}\delta a_k=b_k,\qquad k=1,2,\ldots,m. \tag{9.68}$$

莱文伯格–马夸特方法（Marquardt (1963)）在实践中已成为非线性回归的标准方法。它提供了一种有效的策略，通过在远离最小值时适用的方程 9.68 之间平滑切换来确定模型参数的最优修正。

