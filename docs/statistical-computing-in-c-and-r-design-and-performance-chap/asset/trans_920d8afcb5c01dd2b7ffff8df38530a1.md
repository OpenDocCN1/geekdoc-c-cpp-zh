

# 318

# 数值优化

为了说明 `mle` 的用法，考虑以下函数

```r
lfunc <- function(theta, xbar, n) -n*log(theta) + n*xbar*theta)
```

该函数计算了给定样本量 `n` 和样本平均值 `xbar` 时指数分布的负对数似然。为了优化，`n` 和 `xbar` 的值必须固固定，可以使用 `mle` 的固定参数来处理这一点。下面的列表使用了与我们之前的 `like` 类相同的数据来演示这一过程。

```r
> set.seed(123)
> x0 <- rep(100, 1)
> library("stats")
> mle(lfunc, start = list(theta = .5), fixed = list(xbar = mean(x0),
+ n = length(x0)))
```

```
Call:
mle(lfunc, start = list(theta = 0.6), fixed = list(xbar = mean(x0),
  n = length(x0))
```

Coefficients:

| theta | xbar |
|---|---|
| 0.95628036 | 1.0451781100000000 |

# 8.6 随机搜索

确定性优化方法（如黄金分割法和牛顿法）为寻找函数 $f$ 的全局极小值提供了替代全局搜索策略的实用方案。然而，它们受限于对良好初始搜索位置的要求。利用随机数生成器来寻找此类位置可能是非常有效的。这引发了一个问题：为什么要使用确定性方法呢？难道不直接用随机数序列搜索整个优化区域吗？有许多方法正是这样做的。Spall (2003) 提供了该领域的概述。

最简单的策略是盲目搜索法，在感兴趣的区域内进行模拟，直到找到（例如）极小值的合适近似。Spall (2003) 表，在对 $f$ 有弱限制的情况下，所得近似极小值序列以概率 1 收敛到全局极小值。该方法在算法 8.3 中进行了形式总结，该算法需要对迭代计数参数 `maxit` 进行选择。

# 算法 8.3 盲目随机搜索

```r
iter <- 0
在 [a, b] 上生成均匀分布的 minTemp
while iter < maxit do
  在 [a, b] 上生成均匀分布的 U
  if f(U) < f(minTemp) then
    minTemp = U
  end if
  iter <- iter + 1
end while
return minTemp
```

下面的 `ranSearch` 方法被添加到列表 8.8 中，它直接使用附录 E 中的 `ranGen` 对象实现了算法 8.3。

# 随机搜索

```cpp
double Optim::ranSearch(Functor& f, double a, double b,
  unsigned long seed) const {
  double minTemp, U;
  int niter = 0;
  ranGen RNG;
  RNG.setSeed(seed);
  double* pu = new double;
  RNG.ranUnif(1, pu);
  minTemp = a + (b - a)*(pu);
  while(niter < itMax) {
    RNG.ranUnif(1, pu);
    U = a + (b - a)*(pu);
    if (f(U) < f(minTemp))
      minTemp = U;
    niter++;
  }
  delete pu;
  return minTemp;
}
```

模拟退火是一种盲目搜索，它通过接受-拒绝策略尝试更快地向最小值移动。降低目标函数的值总是被接受的；增加目标函数的第 $k$ 步值 $\theta$ 被接受的概率为 $p = \exp\{(f(\theta^{(k-1)}) - f(\theta))/T_k\}$，其中 $\theta^{(k-1)}$ 是迭代迭代，$T_k$ 是一个递减序列。接受拒绝方案允许在搜索早期逃离局部极小值。模拟退火以概率 1 收敛到全局极小值，前提是目标函数的连续性（例如，Jenkins 1992 和 Spall 2003）。模拟退火依赖于冷却计划的选择、最大迭代次数 (`itMax`) 以及一个控制从当前近似值向极小值移动步长的参数 $d$。该方法的伪代码总结见算法 8.4。

# 算法 8.4 模拟退火

```r
niter = 0, 在 [a, b] 上均匀生成 minTemp
while niter < itMax do
  在 [max(minTemp - d), min(minTemp + d)] 上均匀生成 U
  if f(U) < f(minTemp)
    minTemp = U
  else
    p = exp((f(minTemp) - f(U))/temp)
    在 [0, 1] 上生成均匀分布的 V
    if V < p then
      minTemp = U
  end
  niter = niter + 1
end
return minTemp
```

```
$ ./opt 100 10 123 .000001 .25 .99
牛顿法得到的近似极小值是 0.937336
失败次数为 3
黄金分割法得到的近似极小值是 0.937335
盲目搜索得到的近似极小值是 0.9280009
模拟退火得到的近似极小值是 0.59431477
```

# 随机搜索

```
$ ./opt 500 123 .0000001 .25 .99
牛顿法得到的近似极小值是 0.9373336
失败次数为 3
黄金分割法得到的近似极小值是 0.9368375
盲目搜索得到的近似极小值是 0.93680426
模拟退火得到的近似极小值是 0.93380905
$ ./opt 1000 123 .0000001 .25 .99
牛顿法得到的近似极小值是 0.9373336
失败次数为 3
黄金分割法得到的近似极小值是 0.9373335
盲目搜索得到的近似极小值是 0.93786242
模拟退火得到的近似极小值是 0.93175934
```

对结果类型的“分类观点”将是：所有方法都能产生全局优化器附近的解。对这个特定示例的进一步经验表明，模拟退火对其调优参数最为敏感，相比之下，其他方法更可靠。部分内容由于我们的实现细节未被检测到。然而，应该指出模拟退火对于可能非光滑目标函数的高维解更具意义。相比之下，盲目搜索不可行，黄金分割法变得难以处理。在第8.4节中，R函数通过 "SANN" 方法提供了模拟退火。`optim` 使用的冷却计划是 $T_k = inf/(k)$，其中 `temp` 是冷却计划的起始温度（默认为10），而 `max` 是每个温度下允许的函数评估次数（同样默认为10）。`temp` 和 `max` 的值通过 `optim` 的 `control` 参数设置，该参数必须以列出参数值的列表给出。`optim` 的另一个参数是 `maxit`，用于设置最大迭代次数。它也使用 `control` 参数设置，基于派的方法默认为100，对于SANN则默认为10000。

为了与C++ 代码进行比较，我们应对图8.1函数应用 `optim`。这样做存在一点小问题，因为SANN方法不允许指定搜索区边界。如果没有这样的结果，将会产生：

```
> set.seed(123)
> optim(par = .5, fn = func, method = "SANN") [1:2]
$par
[1] 11.52728

$value
[1] -11.51742
```

在这里，使用 `optim` 应用了模拟退火方法，初始值为 `par = .5`，`func = function(theta){theta*sin(4*pi*theta^2)}，且其他参数均取默认值。结果是，`optim`尝试搜索整个实线并定位到不在目标优化区域的点。对于类似退火不依赖连续性的情况，随机范围很容易找到：只需重新定义函数

```r
func function(theta)
if(theta < 1 && theta > 0) f = theta*sin(4*pi*theta^2)
else f = Inf
f }
```

# 数值优化

此版本的 `func` 在 [0, 1] 上与原始版本一致，在其他地方在R的正无穷表示处计算。因此，[0, 1] 之外的值被有效地排除在考虑。有了这个新版本的 `func`，`optim` 的运行要顺畅得多，返回：

```r
set.seed(123)
optim(par) = .5, fn = func, method = "SANN")[1:2]
$par
[1] 0.9373296
```

```
$value
[1] -0.936377
```

此处使用了默认选择，在该实例中效果良好。为了查看对 `temp`、`tmax` 和 `maxit` 选择的敏感性，考虑了几种情况，结果如下：

```r
set.seed(123)
optim(par) = .2, fn = func, method = "SANN"
+ control = list(maxit = 5, temp = 2, tmax = 1))[1]
$par
[1] 0.1829546
```

```r
set.seed(123)
optim(par) = .2, fn = func, method = "SANN"
+ control = list(maxit = 10, temp = 2, tmax = 1))[1]
$par
[1] 0.9542554
```

```r
set.seed(123)
optim(par) = .2, fn = func, method = "SANN"
+ control = list(maxit = 100, temp = 2,0 = 250))[1]
$par
[1] 0.9651814
```

至少在这个示例语境下，该算法在调优参数的选择上表现得稳健。当迭代次数（例如）设置得较小时，它将我们置于寻找全局极小值的正确区域。

# 练习

8.1. 可以有多个模板参数。（例如，参见第9.5.2节。）特别是，如下语法：

```cpp
template class<T1, T2, T3> class myClass
```

将产生具有三个模板参数的类。利用这一事实，创建一个具有以下属性的函数模板：

- a) 该类封装了一个指向任意类的成员函数的指针，该函数具有单个任意参数和返回类型并且

