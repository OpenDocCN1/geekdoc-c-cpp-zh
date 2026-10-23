

解析解可以通过分离变量法求得（Smith, 1978）：

$$u(x,t)=\frac{8}{\pi^2}\sum_{n=1}^{\infty}\frac{1}{n^2}\left(\sin\frac{1}{2}n\pi\right)(\sin\,n\pi x)e^{-n^2\pi^2 t}.$$

回答以下问题：

- a) 使用双精度和多精度数据类型实现上述解。特别地，确定在级数中需要取多少项才能达到给定的精度。
- b) 通过使用第 30 章中的并行归约和聚合代码，对 a) 部分的代码进行并行化。
- c) 使用从第 13 章开始的有限差分方法近似求解热方程。

## 5. （合流超几何函数）

该函数定义如下（Abramowitz and Stegun, 1965）：

$$M(\alpha,\gamma,z)=\sum_{n=0}^{\infty}\frac{\Gamma(\alpha)\Gamma(\alpha+n)}{\Gamma(\alpha)\Gamma(\gamma+n)}\frac{z^{n}}{n!}$$

其中 $\Gamma(z)$ 为伽马函数，即 $\Gamma(z)=\int_{0}^{\infty}t^{z-1}e^{-t}dt$。

回答以下问题：

- a) 将此公式实现为项的和，每一项都是以下 C++ 与 Boost 代码的混合：

```
template <typename T>
std::complex<T> CHFTerm(T alpha, T gamma, int n,
    const std::complex<T>& z)
{
    using boost::math::tgamma;
    using boost::math::factorial;

    T nt = static_cast<T>(n);
    T coeff = (tgamma(gamma) * tgamma(alpha + nt))
              / (tgamma(alpha) * tgamma(gamma + nt));

    // Write z^n in polar form
    T x = z.real(); T y = z.imag();
    T r = boost::multiprecision::sqrt(x*x + y*y);
    T rn  = boost::multiprecision::pow(static_cast<T>(r),
                static_cast<T>(n));
    std::complex<T> inTheta(static_cast<T>(0.0),
                static_cast<T>(n)*std::arg(z));
    std::complex<T> zn = rn*std::exp<T>(inTheta);
    T fac = 1.0 / factorial<T>(n);

    return coeff * zn * fac;
}
```

- b) 使用以下情况测试代码：
  
  \[
  \begin{aligned}
  M(0.3, 0.2, -0.1) &= 0.8578490\\
  M(-1.3, 1.2, .1) &= 0.8924108\\
  M(17, 16, 1) &= 2.8881744\\
  M'(-0.7, -0.6, 0.5) &= 1.724128 \text{ where } M'(a,b,z)=\frac{a}{b}M(a+1,b+1,z)\\
  M(a,b,z) &= e^z M(b-a,b,-z).
  \end{aligned}
  \]

- c) 现在使用多精度数据类型实现算法。你在 32 位和 64 位情况下得到的结果是否更好？

- d) 对代码进行并行化。

我们指出，合流超几何函数可用于计算描述某些类别期权的部分微分方程的解析近似。参见例如 Lewis (2016) 和 Linetsky (2004)，其中它被用于计算 CIR 扩散过程的击中时间。

## 6. （阶乘与伽马函数）

我们在第 11 章和第 12 章中已经看到如何计算阶乘：

\[
n! = n(n-1)\ldots 3.2.1.
\]  \hfill (A1.1)

对于整数自变量的较大值，我们采用伽马函数：

\[
\Gamma(z)=\int_0^\infty x^{z-1}e^{-x}\,dx,\quad z\in\mathbb{C}
\]  \hfill (A1.2)

$\Gamma(n)=(n-1)!$ 若 $n$ 为正整数。

本练习的目的是比较这两种算法计算阶乘的相对效率、鲁棒性和精度。

回答以下问题：

- a) 对一系列积分值实现算法，例如 $N=10^a$ 其中 $a$ 为整数。对于哪些 $a$ 值两种算法都会溢出？
- b) 添加类型特征库的代码以测试无限数、NaN 以及其他可能的溢出事件。
- c) 使用 Boost multiprecision 库创建部分 a) 和 b) 中算法的等价物，使用扩展数据类型，例如：

```
boost::multiprecision::cpp_dec_float_100 input(10'000'001);
std::cout << boost::math::tgamma(input) << '\n';
```

- d) 测试部分 a) 到 c) 中所有算法的相对运行时间性能。

## 附录 2

## 计算隐含波动率

> ... 所有伟大数学的源头都是特殊情形，具体例子。数学中经常出现，每个一般概念的实例本质上都与一个小而具体的特例相同。
> 
> —Paul Halmos

### A2.1 引言与目标

本附录有若干目的。首先，它通过关注一个具体问题（计算隐含波动率）并使用本章讨论的各种方法，对第 19 章中的主题进行了阐述。其次，它使用了我们在本书各章中讨论的一些概念、模型和方法，例如：

- 计算隐含波动率。
- 用于根查找和单变量优化的数值方法。
- 同伦方法和非线性方程的求解。
- 基于我们在第 9 章中介绍的设计原则创建函数优化的软件框架（另见图 19.1）。
- 在 C++ 中做数学；高阶函数。这是小研究课题。
- 无约束多变量优化。

最后，我们将在以后的工作中更详细地讨论一些新主题（例如高阶数学函数、差分进化以及多变量优化）。

### A2.2 通过最小二乘优化计算隐含波动率

在 Black–Scholes 模型中，普通期权的理论价值是标的资产波动率的单调递增函数。这意味着通常可以从期权给定的市场价格计算出唯一的隐含波动率。该隐含波动率

最好被视为期权价格的重标定，使得不同行权价、到期日和标的之间的比较更容易、更直观。基于这些观察，我们制定了以下 *非线性最小二乘问题*，我们将其写为：

```
f = market price − option price (σ)
optimise z = min_σ f²(σ).  (A2.1)
```

更一般地，在 n 维中，非线性方程组：

```
f(x) = 0, x ∈ ℝⁿ  (A2.2)
```

可以写成 *最小化问题*：

```
min_{x∈ℝⁿ} F(x)  (A2.3)
```

其中：

```
F(x) = Σ_{j=1}^n f_j²(x) = fᵀ(x)f(x).
```

另一种看待隐含波动率的方法是将其视为价格，而不是未来股价变动的衡量。我们简单地将其视为一种比货币更方便的方式来传达期权价格（Natenberg, 2007）。

我们现在讨论如何使用黄金搜索、三点区间搜索和 Brent 方法计算隐含波动率（我们使用 Boost 中的 Brent 方法）。我们的意图是在图 19.1 中的上下文图中描述每个参与类。每个组件的代码都放在自己的文件中以利于可维护性（我们在此版本中没有创建构建器）：

```
#include "Interfaces.hpp"
#include "Termination.hpp"
#include "Solvers.hpp"
#include "MIS.hpp"
#include "Reporting.hpp"
#include "Mediator.hpp"
#include "Pricers.hpp"
```

这些类中的一些代码已在第 19.7 节中给出，这里不再重复。当前的问题是从看涨期权（或看跌期权）价格计算隐含波动率。我们将这些需求封装在一个类中，该类实现了上述方程 (A2.1) 到 (A2.3)：

```
// Standardised interface
using IPricingFunction = std::function<double(double sig)>;

class ImpliedVolatilityEstimator
{ // Computes iv from call or put prices; we are using least squares
  // such Golden mean, Brent, 3-point interval, Differential Evolution
private:
    double mp;                  // Market price
    IPricingFunction pricer;    // Call or put price
public:
    ImpliedVolatilityEstimator
        (double marketPrice, const IPricingFunction& optionPricer)
        : mp(marketPrice), pricer(optionPricer) {}

    double operator () (double sig) const
    { // Compute current residual

        double calculatedValue = pricer(sig);
        double d = -mp + calculatedValue;

        // Least-squares form
        return d*d;
    }
};
```

通常，我们使用众所周知的定价器使用此类：

```
class Pricer
{ // Special adapter class to work with implied volatility
private:
    OptionData opt;
public:
    Pricer(const OptionData& optionData) : opt(optionData) {}

    double PutPrice(double sig) const
    {
        double tmp = sig * std::sqrt(opt.T);

        double d1 = (std::log(opt.S / opt.K)
                    + (opt.b + (sig*sig)*0.5) * opt.T) / tmp;
        double d2 = d1 - tmp;

        return opt.K * std::exp(-opt.r * opt.T)* N(-d2)
               - opt.S* std::exp((opt.b - opt.r)*opt.T) * N(-d1);
    }

    double CallPrice(double sig) const
    {
        double tmp = sig * std::sqrt(opt.T);

        double d1 = (std::log(opt.S / opt.K)
                    + (opt.b + (sig*sig)*0.5) * opt.T) / tmp;
        double d2 = d1 - tmp;
```

