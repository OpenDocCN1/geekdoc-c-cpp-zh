

### 5.5.3 詹森 Alpha (Jensen's Alpha)

$\alpha_j = (R_P - R_F) - \beta_p(R_M - R_F)$

尽管这是一个基础指标，但在传统投资领域被广泛使用，尽管如此，它是解决 alpha 和 beta 分离问题的一个起点 (Jensen 1968)。分离过程有助于分解对冲基金中通常发现的收益三个组成部分：i. alpha（能力）、Anson (2008) 提到的 beta 连续体（从能力到无能力）以及无风险利率（无能力）。由于对冲基金经理通常对其服务收取高额费用（例如 2 和 20），对于投资者而言，清楚自己自己在为什么什么买单至关重要。来源 5.7 显示了 `JA()` 成员的声明和定义。

```cpp
SOURCE 5.7: JA() 成员的声明和定义
```cpp
// /
// PMetrics.h
// /

void JA(V2DD& v, const DBL& r); // JA()

// /
// PMetrics.cpp
// /

// JA())
void PMetrics::JA(V2DD& v, const DBL& r)
{
    UINT n = v.size();
    DBL tmp; // 一个临时持有变量
    V1DD ja; // 为詹森 alpha 定义一个 1D 向量

    V1DD mean = Mean(v, 12); // 从 Stats 类继承 Mean
}
```

```
V1DD slope = GetSlope(v); // 调用 GetSlope() 成员函数

// 使用等式 (5.9) 计算詹森 alpha
for (UINT j=1; j<v[0].size()-1; j++)
{
    tmp = 0.0;
    for (UINT i=0; i<n; i++)
    {
        tmp = mean[j - 1] - (r + slope[j - 1] * (mean[v[0]].size() - 2) - r));
    }
    ja.push_back(tmp);
}

return ja;

//...
// main.cpp
//...

// 声明并调用 JA() 成员函数
// 假设无风险利率 = 3.0%
V1DD ja = pmetrics.JA(data, 3.0);

// 输出结果
cout << "\nJensen's Alpha:\n"
pmetrics.SortPrint(ja, s);
//...
```

| | |
|---|---|
| CIT0 | 12.02 |
| CIT1 | 9.50 |
| GMZ | 0.65 |
| LS1 | 6.54 |
| LS2 | 6.27 |
| LS3 | 4.01 |
| CIT3 | 3.47 |
| GM2 | 2.60 |
| MNU | 1.72 |
| MNZ | 0.54 |

有趣的是，CTA1 已经被 CTA3 挤出了排名中的首位位置。换句话说，CTA1 被发现自己在很大程度上通过市场“搭便车”来产生其百分比的收益。这在行业内通常是不被认可的，因为经理不应为易于复制的资产类别获得风险报酬，因为通常可以使用廉价的 ETF 或通过做多并在必要时滚动期货来获得相同的风险敞口。根据 SR 排名的 CTA3 现在位居第一，其 JA 为 12.02%。虽然 CTA1 仍位第二，但 GM1 以与 TR 类似的排名保持其地位，LS1 在曾进入 SR 排名后被降至第四。MN52 仍然是更好的边界基金。

### 5.5.4 M 平方 (M-Squared)

M 平方 (MM) 指标由 Modigliani 和 Modigliani¹³ 开发，作为一种风险调整衡量，一旦对各种对冲基金的平均收益进行波动调整并进行排名，普通投资者可以更容易理解。其直觉是，通过使用一个与基金估计波动率匹配的基准进行杠杆或去杠杆处理，使其波动率与市场基准匹配。然后报告并对基金的杠杆或去杠杆收益进行排名。因此，基金的收益可以解释为当波动率等同于市场基准时所产生的收益。当各种基金以这种方式处理并排名时，不那么复杂的投资者更容易看到他们如何优于与其风险配置匹配的基准。在我们的情况下，市场基准 (SD) 的分析收益为 5.36%，匹配用途的波动率为 10.90%。MM 的公式为：

$MM = \frac{\sigma_M}{\sigma_P}(R_p - R_F) - R_F \quad (5.18)$

来源 5.8：MM() 成员的声明和定义。

| |
|---|---|
| SOURCE 5.8: MM() 成员的声明和定义 |
| // Metrics.h |
| // ... |
| void MM(V2DD& v, const DBL& r); // MM() |

```cpp
// ...

// ...
// PMetrics.cpp
// ...

// MM()
void PMetrics::MM(V2DD& v, const DBL& r)
{
    UINT n = v.size();
    DBL tmp; // 一个临时持有变量
    V1DD std = StDev(v, 12); // 为詹森 alpha 定义一个 1D 向量

    V1DD mean = Mean(v, 12); // 从 Stats 类继承 Mean
    V1DD std = // 从 Stats 类继承 StDev

    // 使用等式 (5.19) 计算 M 平方
    for (UINT j=1; j<v[0].size()-1; j++) {
        tmp = 0.0;
        for (UINT i=0; i<n; i++) {
            tmp = (std[v[0].size() - 2] / std[j - 1]) * (mean[j - 1] - r) - r;
        }
        mm.push_back(tmp);
    }
    return mm;
}
// ...
// main.cpp
// ...

// 声明并调用 MM() 成员函数
// 假设无风险利率 = 3.0%
V1DD mm = pmetrics.MM(data, 3.0);

// 输出结果
cout << "\nM-Squared (Rf = 3.0):\n"
pmetrics.SortPrint(mm, s);
// ...
```

```
File:/data/10_funds.dat
成功导入 792 个值！
M-Squared (Rf = 3.0):
CTA1    9.27
LS1    7.17
CTA3    6.43
CTA2    4.78
GMI    2.79
LS2    3.23
LS3    3.61
MN1    8.21
MN2   -1.10
MN2   -2.40
```

从结果可以看出，排名与夏普比率相同。然而，MM 指标的主要意义在于它代表了波动率与基准匹配时的收益。由于基准收益为 5.36%，这意味着收益高于 5.36% 的基金优于基准，例如 CTA1 和 CTA3（这在 SR 排名中是不言而易见的）。对于投资者来说，知道他们的收益比市场高出多少百分点是令人宽慰的。

## 5.6 最小接受收益 (Minimum' Return)

这两个指标基于区分“好波动”和“坏波动”的概念。方差和标准差是资产收益离程度的双侧衡量标准。然而，通常认为为特定统计量指定一个最小接受收益 (MAR) 阈值以定义亏损的限额。

### 5.6.1 索提诺系数 (Sortino Ratio)

索提诺¹⁴比率定义为：

$$R_p - MAR$$

$$Sortino = \frac{1}{T} \sum_{t=0, R_p<MAR}^T (R_{p,t} - MAR)^2 \quad (5.19)$$

STR 是 SR 的另一种增强变体。SR 的问题在于它将波动率作为整个收益序列的风险衡量标准。因此，价值的大幅上升和下降都会受到惩罚，因为它们会导致波动率增加并从而降低 SR。在许多方面，STR 是一个更好的选择，特别是在衡量和比较收益分布呈现偏态的经理表现时。STR 是 SR 的改进，但那些下撤低于用户指定目标（见图 5.7）或所需收益率的收益被认为是具有风险的。

