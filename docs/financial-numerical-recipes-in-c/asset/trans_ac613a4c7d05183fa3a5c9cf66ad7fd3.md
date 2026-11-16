
### 9.2.1 最初的 Black Scholes 分析

Black Scholes 分析的主要假设涉及管理底层资产价格的随机过程。底层资产的价格 S 被假设遵循几何 Brownian Motion 过程，可以方便地以以下任一简写形式表示

```
dS = μSdt + σSdZ
```

或

```
dS/S = μdt + σdZ
```

其中 μ 和 σ 是常数，Z 是 Brownian motion。

利用 Ito 引理、无套利假设以及连续交易的能力，Black 和 Scholes 表明，任何基于底层资产的或有索偿的价格必须求解 *偏微分方程* (9.1)。

```
∂f/∂S S + ∂f/∂t + 1/2 ∂²f/∂S² σ²S² = rf (9.1)
```

对于任何 *特定* 的或有索偿，索偿的条款将给出若干 *边界条件*，从而确定定价公式的形式。

Black 和 Scholes 表明，方程 (9.1) 给出的偏微分方程，结合边界条件 c_T = max(0, S_T - K)，具有解析解，其函数形式如 Black Scholes 公式 9.1 所示。

### 9.2.2 二项式情况的极限

另一种方法是使用二项式过程的极限（Cox et al., 1979）。后者尤其有趣，因为它使我们能够将 Black Scholes 公式与二项式联系起来，从而允许将二项式框架用作近似。

### 9.2.3 代表性代理人框架

展示 BS 公式的最后一种方法是假设存在代表性代理人和对数正态性，如 Rubinstein (1976) 所做。

## 9.3 偏导数。

在期权交易中，期权定价公式的若干偏导数非常重要。

### 9.3.1 Delta

期权价格相对于底层证券价格的第一个导数称为期权价格的 *delta*。这是大多数人会遇到的导数，因为它在期权对冲中很重要。

```
∂c/∂S = N(d₁)
```

C++ 代码 9.2 显示了看涨期权 delta 的计算。

```cpp
#include <cmath>
#include "normdist.h"

double option_price_delta_call_black_scholes(const double& S, // spot price
         const double& K, // Strike (exercise) price,
         const double& r, // interest rate
         const double& sigma, // volatility
         const double& time){ // time to maturity

        double time_sqrt = sqrt(time);
        double d1 = (log(S/K)+r*time)/(sigma*time_sqrt) + 0.5*sigma*time_sqrt;
        double delta = N(d1);
        return delta;
    };
```

C++ 代码 9.2：计算 Black Scholes 看涨期权价格的 delta

### 9.3.2 其他导数

其余的导数使用较少，但它们都很重要。所有这些都列在公式 9.3.2 中。

Delta ($\Delta$)

$\Delta = \frac{\partial c}{\partial S} = N(d_1)$

Gamma ($\Gamma$)

$\frac{\partial^2 c}{\partial S^2} = \frac{n(d_1)}{S\sigma\sqrt{T-t}}$

Theta ($\Theta$) (注意你想要的是哪一个)

$\frac{\partial c}{\partial(T-t)} = Sn(d_1)\frac{1}{2}\sigma\frac{1}{\sqrt{T-t}} + rKe^{-r(T-t)}N(d_2)$

$\frac{\partial c}{\partial t} = -Sn(d_1)\frac{1}{2}\sigma\frac{1}{\sqrt{T-t}} - rKe^{-r(T-t)}N(d_2)$

Vega

$\frac{\partial c}{\partial \sigma} = S\sqrt{T-t}n(d_1)$

Rho ($\rho$)

$\frac{\partial c}{\partial r} = K(T-t)e^{-r(T-t)}N(d_2)$

$S$ 是底层证券的价格，$K$ 是行权价，$r$ 是（连续复利）无风险利率，$\sigma$ 是底层资产的标准差，$t$ 是当前日期，$T$ 是到期日期，$T-t$ 是期权的到期时间。
$n(.)$ 是正态分布函数（$n(z) = \frac{1}{\sqrt{2\pi}}e^{-\frac{1}{2}z^2}$），$N(.)$ 是累积正态分布（$N(z) = \int_{-\infty}^z n(d)d$）。

公式 9.2：Black Scholes 看涨期权公式的偏导数

C++ 代码 9.3 显示了看涨期权所有这些偏导数的计算。

### 示例

再次考虑 XYZ 股票的六个月期看涨期权。期权将在 6 个月后到期，届时期权持有人可以通过支付行权价 K = 50 获得一单位底层证券。底层证券的当前价格为 S = 50。底层证券的波动率为 \(\sigma = 30\%\)。六个月期借款的当前无风险利率（连续复利）为 10%。

### C++ 程序：

```cpp
#include <cmath>
#include "normdist.h"
using namespace std;

void option_price_partials_call_black_scholes( const double& S, // spot price
const double& K, // Strike (exercise) price,
const double& r, // interest rate
const double& sigma, // volatility
const double& time, // time to maturity
double& Delta, // partial wrt S
double& Gamma, // second prt wrt S
double& Theta, // partial wrt time
double& Vega, // partial wrt sigma
double& Rho)// partial wrt r
{
double time_sqrt = sqrt(time);
double d1 = (log(S/K)+r*time)/(sigma*time_sqrt) + 0.5*sigma*time_sqrt;
double d2 = d1-sigma*time_sqrt;
Delta = N(d1);
Gamma = n(d1)/(S*sigma*time_sqrt);
Theta = -(S*sigma*n(d1))/(2*time_sqrt) - r*K*exp(-r*time)*N(d2);
Vega = S * time_sqrt*n(d1);
Rho = K*time*exp(-r*time)*N(d2);
}
```

C++ 代码 9.3：计算 Black Scholes 看涨期权的偏导数

- 1. 计算该期权的偏导数（Delta、Gamma、Theta、Vega 和 Rho）。

要计算偏导数，我们使用输入 S = 50、K = 50、r = 0.10、sigma = 0.3 和 (T - t) = 0.5。

### C++ 程序：

```cpp
cout << " Black Scholes call partial derivatives " << endl;
double S = 50; double K = 50; double r = 0.10;
double sigma = 0.30; double time=0.50;
double Delta, Gamma, Theta, Vega, Rho;
option_price_partials_call_black_scholes(S,K,r,sigma, time, Delta, Gamma, Theta, Vega, Rho);
cout << " Delta = " << Delta << endl;
cout << " Gamma = " << Gamma << endl;
cout << " Theta = " << Theta << endl;
cout << " Vega = " << Vega << endl;
cout << " Rho = " << Rho << endl;
```

### C++ 程序输出：

```
Black Scholes call partial derivatives
Delta = 0.633737
Gamma = 0.0354789
Theta = -6.61473
Vega = 13.3046
Rho = 13.1168
```

### 9.3.3 隐含波动率。

在期权定价公式的计算中，特别是 Black Scholes 公式中，唯一的未知数是底层股票的标准差。期权定价中一个常见的问题是，根据市场上观察到的报价找到隐含波动率。例如，给定看涨期权价格 \(c_0\)，应求解以下方程以得到 \(\sigma\) 的值：

\(c_0 = c(S, K, r, \sigma, T - t)\)

不幸的是，该方程没有解析解，这意味着必须通过数值方法求解 \(\sigma\)。可能是算法上最简单的求解方法是使用二分查找算法，该算法在 C++ 代码 9.4 中实现。我们首先通过找到使 BS 价格高于观察价格的高 sigma 来对 sigma 进行区间限定，然后，给定区间，我们以系统的方式搜索波动率。这显示了这样的计算。

```cpp
#include <cmath>
#include "fin_recipes.h"

double option_price_implied_volatility_call_black_scholes_bisections(const double& S,
        const double& K,
        const double& r,
        const double& time,
        const double& option_price){
    if (option_price<0.99*(S-K*exp(-time*r))) { // check for arbitrage violations
        return 0.0;
        // Option price is too low if this happens
    };
    // simple binomial search for the implied volatility.
    // relies on the value of the option increasing in volatility
    const double ACCURACY = 1.0e-5; // make this smaller for higher accuracy
    const int MAX_ITERATIONS = 100;
    const double HIGH_VALUE = 1e10;
    const double ERROR = -1e40;
    // want to bracket sigma, first find a maximum sigma by finding a sigma
    // with a estimated price higher than the actual price.
    double sigma_low=1e-5;
    double sigma_high=0.3;
    double sigma=option_price_call_black_scholes(S,K,r,sigma_high,time);
    while (price < option_price){
        sigma_high = 2.0 * sigma_high;
        sigma = option_price_call_black_scholes(S,K,r,sigma_high,time);
        if (sigma_high>HIGH_VALUE) return ERROR; // panic, something wrong.
    }
    for (int i=0;i<MAX_ITERATIONS;++i){
        double sigma = (sigma_low+sigma_high)*0.5;
        price = option_price_call_black_scholes(S,K,r,sigma,time);
        double test = (price-option_price);
        if (fabs(test)<ACCURACY) { return sigma; };
        if (test < 0.0) { sigma_low = sigma; }
        else { sigma_high = sigma; }
    };
    return ERROR;
}
```

C++ 代码 9.4：使用二分法计算 Black Scholes 的隐含波动率

与这种简单的区间限定不同，它实际上非常快，并且几乎总能找到解，我们可以使用 Newton–Raphson 公式来求解单变量方程的根。这种方法的一般描述是从一个我们想要找到其根的函数 \(f()\) 开始。

\(f(x) = 0.\)
