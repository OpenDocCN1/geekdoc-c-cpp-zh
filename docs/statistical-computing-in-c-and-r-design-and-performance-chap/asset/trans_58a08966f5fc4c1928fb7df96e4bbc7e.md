

# 132 伪随机数的生成

789\您的随机数是
1.22472 2.50259 0.159843 0.1064

与对 FM2 生成器的处理类似，使用了 `driverExp` 函数并结合种子 123, 456, 789 从均值为 1 的指数分布中生成了 500 个值的随机样本，并将其作为数值向量对象 `eDat` 导入到 R 中。关于这些数据获得了以下信息。

```
> summary(eDat)
Min. 1st Qu. Mean 3rd Qu. Max.
0.001526 0.258000 0.657300 0.980200 1.300000 8.784000
```

- sd(eDat)
[1] 1.06676
- [1] IQR(eDat)
[1] 1.042139
- [1] pnorm(length(eDat))*mean(eDat) - 1)
[1] 0.326831
- ks.test(eDat, pexp)

单样本 Kolmogorov-Smirnov 检验
data: eDat
D = 0.0402 p-value = 0.3954
alternative hypothesis: two-sided

在此会话中调用了 R 函数来计算导入数据的一些基本统计量。信息通过样本标准差（使用 `sd`）和样本四分位距（`IQR`）进行了补充。由于数据是使用输入值 $\lambda=1$ 生成的，因此总体的均值和方差分别等于均值和四分位距，即 6.93 和 1.1（练习 4.18）。结果，样本统计量与预期结果基本一致。尽管结果在范围之外，样本均值与我计算的归一化（乘以样本量的平方根）差异表明，如果值来自 $\lambda=1$ 的指数分布，其行为得像从标准正态分布中抽取的数字。使用正态分布累积分布函数 `pnorm` 获得的 p 值并不显著，Kolmogorov-Smirnov 拟合检验未检测出与指数模型的显著偏离。图 4.3 中的数据直方图显示了指数分布数据预期的 J 形。

如果 $F$ 有闭式解，但 $F^{-1}$ 没有闭式解，则仍可以使用算法 4.1，并通过数值方法评估分位数函数（`ec`，练习 8.26）。当 $F$ 没有闭式解时（如正态分布），可以使用数值方法（例如数值积分）对码 本身进行数值近似，并将相同的的基本方法应用于该近似。我们现在将描述另一种较不那么复杂的策略。

与之前一样，问题是从密度为 $f$ 的连续随机变量中进行模拟。但现在假设有另一个密度 $g$，其满足对于所有数字 $x$：

```
f(x) \le cg(x)
```

对于常数 $c \ge 1$，$g$ 密度有时被称为工具密度，而 $f$ 是目标密度。基础的接受-拒绝算法采用了



接受-拒绝法的合理性由定理 4.4 提供。

# 伪随机数的生成

**定理 4.4.** *设 $Y$ 具有密度 $g$ 满足 (4.13)，且 $U$ 在条件 $Y=y$ 下在 $[0, cg(y)]$ 上服从均匀分布。那么，$X=Y[U < f(Y)]$ 的密度为 $f$。*

*证明。* 定理4.4 可以在 Devoye (1986) 以及 Robert 和 Casella (2004) 中找到。其思想是如果 $A$ 是实线上的任何开区间：

```
$Prob(X \in A) = Prob(Y \in A[u \leq f(Y)])
= \int_A \int_0^{cg(y)} cg(y)du = \int_{-\infty}^{\infty} \int_0^{f(y)} f(y)dy = \int_A f(y)dy$
```

证明了定理。

注意定理 4.4 首先从密度 $g$ 生成一个值 $y$，然后在 $[0, cg(y)]$ 上生成一个均匀分布。但从区间 $[0, 1]$ 生成数字，然后乘以 $cg(y)$ 分位数函数 $Q(u)=bu$，对于 $u \in [0, 1]$ 且 $b>0$。因此，计划是 (i) 从密度 $g$ 生成 $y$，(ii) 从 $[0, 1]$ 上的均匀分布生成 $u$，如果 $cg(y)u \leq f(y)$ 则取 $y$ 为所需值，或者等价地，在我们的公式中 $ru \leq 1$。

拒绝算法的一个衡量标准是生成随机数所需的拒绝次数。$U$ 和 $Y$ 在定理 4.4 中。那么，任何给定的接受概率：

```
$Prob(U \leq f(Y)) = \int_{-\infty}^{\infty} \frac{f(y)}{cg(y)}dy = 1/c$
```

第一次接受前的次数服从几何概率为 $c^{-1}$。$c$ 的值扩展了 $g$ 能够近似 $f$ 的程度。因此，接受-拒绝算法将受益于对 $g$ 的仔细选择，这允许我们取 $c$ 接近于一。

使用 Cauchy 密度生成标准正态变量的接受-拒绝法示例。Cauchy 密度尺度参数 $\sigma>0$ 具有

```
$g(x) = \frac{1}{\pi(1+x^2/\sigma^2)}, -\infty < x < \infty, \sigma>0$ (4.14)
```

分位数函数是

使用 $g$ 模拟标准正态分布需要找到一个 $c \geq 1$，使得 $f(y)/g(y) \leq c$：

```
$f(x) = \frac{1}{\sqrt{2\pi}}exp\{-x^2/2\}$.
```

按照 Devoye (1986) 第 3.2 节，我们将找到最小的 $f(x) \leq cg(x)$。这种选择平均而言会导致较少的拒绝，从而加快样本生成。

$f(x)/g(x)$ 在 $(1+x^2/\sigma^2)exp\{-x^2/2\}$ 时达到最大值。这等同于使该比例的对数最大化，这等同于求解 $2x=(\sigma^2+x^2)$，即 $x=0$ 和 $x=\pm\sqrt{2-\sigma^2}$。这两个根仅在 $\sigma\sqrt{2}$ 时适用，此时极大值位于 $\pm\sqrt{2-\sigma^2}$，对应于

# 非均匀

对于 $f/g$，一个最大值为 $c=\sqrt{2\pi}\exp\{\sigma^2/2 - 1\}/\sigma$。对于 $f/g$，$\sigma=\sqrt{2}$。

下面的代码是使用接受-拒绝法生成标准正数的 WHCauchy 头文件。

```
// WHCauchy.h
#ifndef WHCAUCHY_H
#define WHCAUCHY_H

class WHCauchy {
    double a1, a2, a3;
    unsigned long m1, m2, m3;
    double g(double x) const;
    double Ginv(double x) const;
    double f(double x) const;

public:
    WHCauchy();
    void range(unsigned long seed1, unsigned long seed2, int n, double* pNorm) const;
};
#endif
```

```
// WHCauchy.cpp
#include <cmath>
#include <iostream>
#include "WHCauchy.h"

using std::cout;
using std::endl;

double pi = acos(-1.0);
double sqrtpi = sqrt(2.*pi);
double c = sqrt(2pi);

WHCauchy::WHCauchy() {
    a1 = pi; a2 = sqrtpi; a3 = 1;
    m1 = 2; m2 = 0; m3 = 0;
}

void WHCauchy::range(unsigned long seed1, unsigned long seed2, int n, double* pNorm) {
    double temp, y;
    double u[2];
    int nFill = 0, iAccept, nReject = 0;

    while(nFill < n){
        iAccept = 0;
        while(iAccept == 0){
            for(int i = 0; i < 2; i++){
                seed1 = a1*seed1; seed2 = a2*seed2; seed3 = a3*seed3;
                temp = ((double)seed1)/((double)m1)
                        + (double)seed2)/((double)m2)
                        + (double)seed3)/((double)m3;
                if(temp > 2.) temp -= 2;
                if(temp > 1.) temp -= 1;
            }
            u[i] = temp;
            y = Ginv(u[i]);
            if(c*y < f(y])){
                pNorm[nFill] = y;
                nFill++;
                iAccept++;
            } else nReject += 1;
        }
    }
    cout << "The Number of rejections was " << nReject << endl;
}

double WHCauchy::g(double x) const {
    return 1/(1+x*x)*pi;
}

double WHCauchy::Ginv(double u) const {
    return tan(pi*(u));
}

double WHCauchy::f(double x) const {
    return exp(-5.*x*x);
}
```

![](img/b50973a0535e1d49ab735f151.png)

136 伪随机数的生成

```cpp
int nFill = 0, iAccept, nReject = 0;

while(nFill < n){
    iAccept = 0;
    while(iAccept == 0){
        for(int i = 0; i < 2; i++){
            seed1 = a1*seed1; seed2 = a2*seed2; seed3 = a3*seed3;
            temp = ((double)seed1)/((double)m1)
                    + (double)seed2)/((double)m2)
                    + (double)seed3)/((double)m3;
            if(temp > 2.) temp -= 2;
            if(temp > 1.) temp -= 1;
        }
        u[i] = temp;
        y = Ginv(u[i]);
        if(c*y < f(y])){
            pNorm[nFill] = y;
            nFill++;
            iAccept++;
        } else nReject += 1;
    }
}
cout << "The Number of rejections was " << nReject << endl;
```

