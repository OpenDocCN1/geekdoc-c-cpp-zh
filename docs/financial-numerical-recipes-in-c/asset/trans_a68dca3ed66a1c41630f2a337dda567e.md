

```cpp
double payoff::binary::call(const double& S, const double& K){
    if (S>=K) return 1;
    return 0;
}

double payoff::binary::put(const double& S, const double& K){
    if (S<=K) return 1;
    return 0;
}
```

C++ 代码 17.4：二叉树期权的收益函数定义

```cpp
C++ program:

double S = 100.0;
double K = 120.0;
double r = 0.1;
double sigma = 0.25;
double time_to_maturity=1.0;
int steps = 100;
cout << " binary option price = "
     << option_price_generic::Binomial(S,K,payoff::binary::call, r, sigma, time_to_maturity, steps)
     << endl;
-------------------------------------------
Output from C++ program:

binary option price = 0.498858
```

## 17.2 Delta 计算

Delta 和其他 Greeks 采用相同风格的通用例程进行计算。C++ 代码 17.5 展示了如何使用相同的通用方法计算 Delta。

```cpp
#include <cmath>
#include <algorithm>
#include <vector>
using namespace std;

double option_price_delta_generic_binomial(const double& S,
                                          const double& K,
                                          double generic_payoff(const double& S, const double& K),
                                          const double& r,
                                          const double& sigma,
                                         const double& t,
                                         const int& no_steps){
    double R = exp(r*(t/no_steps));
    double Rinv = 1.0/R;
    double u = exp(sigma*sqrt(t/no_steps));
    double d = 1.0/u;
    double uu = u*u;
    double pUp = (R-d)/(u-d);
    double pDown = 1.0 - pUp;

    vector<double> prices(no_steps+1);
    prices[0] = S*pow(d, no_steps);
    for (int i=1; i<=no_steps; ++i) prices[i] = uu*prices[i-1];

    vector<double> values(no_steps+1);
    for (int i=0; i<=no_steps; ++i) values[i] = generic_payoff(prices[i],K);

    for (int CurrStep=no_steps-1; CurrStep>=1; --CurrStep) {
        for (int i=0; i<=CurrStep; ++i) {
            prices[i] = d*prices[i+1];
            values[i] = (pDown*values[i]+pUp*values[i+1])*Rinv;
            values[i] = max(values[i], generic_payoff(prices[i],K));
        };
    };
    double delta = (values[1]-values[0])/(S*(u-u*d));
    return delta;
};
```

### C++ 代码 17.5：Delta 的通用二叉树计算

### 练习 17.1。

本章讨论的通用例程均针对美式期权。应如何修改它们以适用于欧式期权？

## 第 18 章

## 三叉树

### 目录

- 18.1 简介 .................................................... 183
- 18.2 实现 .................................... 183
- 18.3 进一步阅读 .................................... 185

### 18.1 简介

三叉树与二叉树类似，只是多了一个分支。在每个时间点，标的资产 S 都有三种可能的未来价值。

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_183_0.png)

### 18.2 实现

三叉树可以采用多种参数化方式实现。我们将使用以下参数化方式展示计算过程：

```
u = e^{\sigma \sqrt{\Delta t}}

e = \frac{1}{u}

p_u = -\sqrt{\frac{\Delta t}{12\sigma^2}} \left( r - q - \frac{\sigma^2}{2} \right) + \frac{1}{6}

p_m = \frac{2}{3}

p_d = \sqrt{\frac{\Delta t}{12\sigma^2}} \left( r - q - \frac{\sigma^2}{2} \right) + \frac{1}{6}
```

我们使用通常的回溯过程计算期权价格，持续价值为

e^{-r \Delta t} (p_u f_u + p_m f_m + p_d f_d)

```cpp
#include <vector>
#include <cmath>
using namespace std;

double option_price_put_american_trinomial( const double& S,
        const double& K,
        const double& r,
        const double& q,
        const double& sigma,
        const double& t,
        const int& steps) {
    double delta_t = t / steps;
    double Rinv = exp(-r*(delta_t));
    double sigma_sqr = pow(sigma,2);
    double u = exp(sigma*sqrt(3.0*delta_t));
    double d = 1.0/u;
    double p_u = 1.0/6.0 + sqrt(delta_t/(12.0*sigma_sqr)) * (r-q-0.5*sigma_sqr);
    double p_m = 2.0/3.0;
    double p_d = 1.0/6.0 - sqrt(delta_t/(12.0*sigma_sqr)) * (r-q-0.5*sigma_sqr);

    vector<double> values; // price of underlying in a tree
    vector<double> Svec;
    Svec.push_back(S);
    for (int step=1; step<=steps; ++step){
        Svec.push_back(Svec[step-1]*u); // use the fact that only the extreme values change.
        Svec.push_back(Svec[step-1]*d);
    }

    vector<double> values_next;
    for (int i=0; i<m; ++i) values_next[i] = max(0.0, K-Svec[i]); // call payoffs at maturity
    vector<double> values; // value of option
    for (int step=steps-1; step>=0; --step) {
        int m = (int)(Svec[step].size());
        values = vector<double>(m); // value of option
        for (int i=0; i<m; ++i) {
            values[i] = (p_u*values_next[i+2]+p_m*values_next[i+1] + p_d*values_next[i])*Rinv;
            values[i] = max(values[i], K-Svec[step][i]); // check for exercise
        }
        values_next=values;
    }
    return values[0];
};
```

### C++ 代码 18.1：使用三叉树计算美式看跌期权价格

### 示例

给定某期权的以下信息：S = 100，K = 100，r = 0.1，sigma = 0.25，到期时间为 1 年。使用 100 步的三叉树近似计算美式看跌期权价格。

```matlab
function P = opt_price_trinomial_am_put(S, K, r, q, sigma, t, steps)
delta_t = t/steps;
sigma_sqr=sigma^2;
R=exp(r*delta_t);
u = exp(sigma*sqrt(3.0*delta_t));
d = 1.0/u;
p.u = 1/6 + sqrt(delta_t/(12*sigma_sqr)) * (r-q-0.5*sigma_sqr);
p.m = 2/3;
p.d = 1/6 - sqrt(delta_t/(12*sigma_sqr)) * (r-q-0.5*sigma_sqr);
Svec = [ S ];
Stre = [ Svec ];
Sd = [ ];
for step=1:steps+1
    Su = Su*u;
    Sd = Sd*d;
    Svec = [ Sd; Svec; Su ];
    Stre= [ Stre, zeros(2,steps), Stre ];
end
values_next = max(K-Svec, 0);
for step = 2:steps+1
    m = 2*step-1;
    values = R*(p.u*values_next(1:3+m-2)+p.m*values_next(2:m+1)+p.d*values_next(1:m));
    values_next = max(values, K-Stre(1:m, step+1));
end
P = values;
end
```

### Matlab 代码 18.1：使用三叉树计算美式看跌期权价格

```cpp
C++ program:
double S = 100.0; double K = 100.0;
double r = 0.1; double q = 0; double sigma = 0.25;
double time=1.0; int no_steps = 100;
cout << " american put = " << option_price_put_american_trinomial(S,K,r,q,sigma,time,no_steps) << endl;
Output of C++ program:
american put = 6.52719
```

### 练习 18.1。

在三叉树代码中，标的资产价格被存入三角形数据结构。由于每增加一步只需在顶部和底部各加一个价格，因此可以将其合并为一个数组。如果跟踪当前数组的顶部和底部，就可以通过对标的资产价格单一向量进行巧妙索引来访问价格。

### 练习 18.2。

类似于二叉树情况，可以构建一个通用三叉树，其中收益函数作为参数传递给例程。实现这样的通用三叉树。

### 18.3 进一步阅读

Hull (2011)

## 第 19 章

## 替代 Black-Scholes 类型期权公式的方法

### 目录

| 节 | 页码 |
|---|---|
| 19.1 Merton 的跳跃扩散模型。 | 186 |
| 19.2 随机波动性模型的 Heston 定价公式 | 188 |

已有大量替代 Black-Scholes 分析的公式被提出。其中少数获得了广泛应用，但我们将探讨其中一些替代方案。

### 19.1 Merton 的跳跃扩散模型。

Merton (1976) 提出了一种模型，除了布朗运动项外，标的资产的价格过程还允许出现跳跃。假设这些跳跃的风险不进行定价。

在以下内容中，我们将研究 Merton 模型的一个特例，该特例在 (Hull, 1993, pg 454) 中有描述，其中跳跃大小服从正态分布。\(\lambda\) 和 \(\kappa\) 是跳跃分布的参数。欧式看涨期权的价格在公式 19.1 中给出，并在 C++ 代码 19.1 中实现。

```
c = \sum_{n=0}^{\infty} \frac{e^{\lambda \tau} (\lambda \tau)^n}{n!} C_{BS}(S, X, r_n, \sigma_n^2, T - t)

where

\tau = T - t

\lambda' = \lambda(1 + \kappa)

C_{BS}(\cdot) is the Black Scholes formula, and

\sigma_n^2 = \sigma^2 + \frac{n \delta^2}{\tau}

r_n = r - \lambda \kappa + \frac{n \ln(1 + \kappa)}{\tau}
```

公式 19.1：Merton (1976) 模型的期权定价公式

在实现此公式时，我们需要在某个点终止无穷求和。但由于

