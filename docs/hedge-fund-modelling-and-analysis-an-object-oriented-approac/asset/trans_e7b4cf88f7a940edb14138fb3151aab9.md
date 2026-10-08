

```cpp
VDD str; // 为 Sortino 比率声明 1D 向量
VDD avg; // 为平均值声明 1D 向量

// 从 Stats 类中继承 Mean
VDD mean = Mean(v, 12);
DBL m = mean.size();
DBL sum, pname;

// 计算投资组合（10只对冲基金）平均值
for(UINT i=0; i<m; i++)
{
    sum += mean[i];
}
pmean = sum/m;

// 计算平均值
for(UINT j=1; j<v[0].size(); j++)
{
    tmp = 0.0;
    for(UINT i=0; i<n; i++)
    {
        tmp += pow(min(0.0, v[i][j] - mar), 2);
    }
    tmp /= n;
    avg.push_back(tmp);
}

// 使用公式 (5.19) 计算 Sortino 比率
for(UINT j=1; j<v[0].size(); j++)
{
    tmp = 0.0;
    for(UINT i=0; i<n; i++)
    {
        tmp = (pmean - mar) / sqrt(avg[j - 1]);
    }
    str.push_back(tmp);
}

return str;

// ...
// main.cpp
// ...
```

```cpp
// 创建类实例
Import thfs;
Pmetrics pmetrics;

// 声明并调用 GetData()
V2D data = thfs.GetData(".data/10_hedge_funds.dat");

VIDs s; // 声明并初始化字符串 1D 向量
s.push_back("CTA1");
s.push_back("CTA2");
s.push_back("CTA3");
s.push_back("GM1");
s.push_back("GM2");
s.push_back("LS1");
s.push_back("LS2");
s.push_back("LS3");
s.push_back("MN1");
s.push_back("MN2");

// 声明并调用 TR() 成员函数
//  MAR = 3.0%
VIDD str = pmetrics.STR(data, 3.0);

// 输出结果
cout << "\nSortino ratio (MAR = 3.0%)";
pmetrics.SortPrint(str, s);
```

![](img/2d1ac831a270b8b08f8b8ec2205913dc_220_0.png)

# 性能衡量

注意，我们回到了原始的 10_hedge_funds.dat 文件，不再需要市场基准数据。结果显示，在风险调整后的排名中似乎出现了一个明显的领跑者，即 CTA1，也就是说它在多项性能指标中一直排名第一。MSR 结果显示 CTA3 优于 LS1，这意味着 CTA3 的高峰度必然与良好的峰度有关：即在正向偏差中具有高回报。虽然存在负偏偏，但其相对于 MAR 的下行偏差收益在风险调整的基础上，比与 LS1 的下行偏差相关的收益要温和。。随着 STR 排名的下降，我们还注意到 GM1 优于 CTA2。简而言之，这说明偏度和峰度的总体估计是误导性的，因为 CTA2 具有更高的偏度（CTA2: 0.351 对 GM1: –0.023）和较低的峰度（CTA2: –0.848 对 GM1: –0.114）；而 STR 将 GM1 的排名比 CTA2 高。

由 Keating 和 Shadwick (2002) 定义的 Omega 比率是一种非参数方法。它不依赖于计算收益分布的阶阶来确定每个对冲基金相对于阈值水平的排名。该方法开发于 20 世纪初，由于其通过包含收益分布的完整分布来描述基金的相对排名，在从业者中广受欢迎。因此，它整合了所有的矩（理论上如此）。正如前面提到的，投资者偏好高阶奇数矩和低阶偶数矩，且持有易受到四阶矩风险影响资产的风险是不容忽视的。它的流行也源于它本质上描述了收益分布的风险-收益特性，因此很容易解释。该比率考虑了特定阈值以下和以上的收益。在此过程中，它在收益分布上设置了一个阈值收益（面积为一的收益 PDF），该分布通过从左侧累加（即积分）形成累积分布函数 CDF，F(x)。我们使用 a 作为下限，使用 b 作为上界，而不是使用正负负号来表示积分两侧的限制。Omega 比率写为：

$$\Omega(L) = \frac{\int_{L}^{b}(1-F(x))dx}{\int_{a}^{L}F(x)dx} $$

低于某阈值的收益被视为损失，之上的收益被视为利润。根据 (5.20)，对于理性投资者来说，给定阈值的较高 Omega 值比较低值更优。因此，当 Omega 比率值为 1 时，它代表了投资组合的平均值，即矩方面的平衡点。因此，Omega 比率可以根据不同的收益阈值创建排名。排名可能会随着风险偏好的变化而变化，这里的偏好被解释为根据其偏好的收益阈值的大小。Omega 比率是非参数的，反映了分布的所有矩，因此在假设两个基金具有相同收益、波动性和偏度的前提下，具有超额峰度的基金排名将低于没有超额峰度的基金。

本章描述的风险调整收益指标是对冲基金行业中最常用的。最近还出现了其他指标，例如 Stutter 指数（Stutter 2000）、Sharpe-Omega 比率（Gupta, Kazemi and Schneeweiss 2003）、AIRAP (Sharma 2004) 以及 Kappa (Kaplan and Knowles 2004)。Lo (2002)。

# 第 6 章

# 均差优化

风险调整收益分析主要涉及确定对冲基金的统计特性以做出决策。我们已经详细查看了两个主要参数：平均值和标准差。1953 年，H. Markowitz 引入了现代投资组合理论，为可接受水平的优化提供了可能。本章介绍了均差优化的核心思想，并实现了拉格朗日乘子法以寻找最优权重。在后续章节中，我们将以相同的方式开发另一个 Optimise 类。源码6.1 显示了 Optimise 类的基础结构

源码6.1：Optimise 类的结构

// Optimise.h
#pragma once

#include "Stats.h"

class Optimise: public Stats
```

```cpp
{
  public:
    Optimise() {}
    virtual ~Optimise() {}

    // 成员函数声明
  private:
    // 成员变量声明
};
```

```cpp
// RMetrics.cpp
#include "Optimise.h"

在源码6.1 中，默认构造函数和析构函数再次在头文件中声明并定义，去掉了分号（）；并添加了大括号（{}）。此外，通过 PMetrics 类，我们让 Optimise 继承自 Stats 类，因为我们可以在 Stats 类中可以使用许多方法。

