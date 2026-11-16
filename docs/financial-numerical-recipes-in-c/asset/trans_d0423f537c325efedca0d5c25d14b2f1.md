

## 5.4 采用一般期限结构和连续复利的债券计算

在时间 \(t_1, t_2, \dots\) 支付票息的附息债券：
债券价格 \(B_0\)：
\(B_0 = \sum_i d_i C_{t_i} = \sum_i e^{-r_{t_i} t_i} C_{t_i}\)
久期 \(D\)：
\(D = \frac{1}{B_0} \sum_i t_i d_i C_{t_i}\)
\(D = \frac{1}{B_0} \sum_i t_i e^{-r_{t_i} t_i} C_{t_i}\)
\(D = \frac{1}{B_0} \sum_i t_i e^{-y t_i} C_{t_i}\)

到期收益率 \(y\) 满足：
\(B_0 = \sum_i C_{t_i} e^{-y t_i}\)
凸性 \(Cx\)：
\(Cx = \frac{1}{B_0} \sum_i t_i^2 d_i C_{t_i}\)
\(Cx = \frac{1}{B_0} \sum_i t_i^2 e^{-r_{t_i} t_i} C_{t_i}\)
\(Cx = \frac{1}{B_0} \sum_i t_i^2 e^{-y t_i} C_{t_i}\)

### 公式 5.1：采用连续复利期限结构的债券定价

C++ 代码 5.6 和 C++ 代码 5.7 说明了如果拥有期限结构类，如何计算债券价格和久期。

```cpp
#include "fin_recipes.h"

double bonds_price(const vector<double>& times,
                   const vector<double>& cashflows,
                   const term_structure_class& d) {
    double p = 0;
    for (unsigned i=0; i<cashflow_times.size(); i++) {
        p += d.d(cashflow_times[i])*cashflows[i];
    }
    return p;
}
```

### C++ 代码 5.6：使用期限结构类对债券定价

```cpp
#include "fin_recipes.h"

double bonds_duration(const vector<double>& cashflow_times,
                      const vector<double>& cashflow_amounts,
                      const term_structure_class& d ) {
    double S=0;
    double D1=0;
    for (unsigned i=0;i<cashflow_times.size();i++){
        S += cashflow_amounts[i] * d.d(cashflow_times[i]);
        D1 += cashflow_times[i] * cashflow_amounts[i] * d.d(cashflow_times[i]);
    }
    return D1/S;
}
```

### C++ 代码 5.7：使用期限结构类计算债券久期

```cpp
#include "fin_recipes.h"
#include <cmath>

double bonds_convexity(const vector<double>& cashflow_times,
                       const vector<double>& cashflow_amounts,
                       const term_structure_class& d ) {
    double B=0;
    double Cx=0;
    for (unsigned i=0;i<cashflow_times.size();i++){
        B += cashflow_amounts[i] * d.d(cashflow_times[i]);
        Cx += pow(cashflow_times[i],2) * cashflow_amounts[i] * d.d(cashflow_times[i]);
    }
    return Cx/B;
}
```

### C++ 代码 5.8：使用期限结构类计算债券凸性

### 示例

期限结构为平坦，r = 10% 连续复利。计算一只 10%、2 年期债券的价格、久期和凸性。

```cpp
C++ program:
vector <double> times; times.push_back(1); times.push_back(2);
vector <double> cashflows; cashflows.push_back(10); cashflows.push_back(110);
term_structure_class tsfalt = flat_ts(0.1);
cout << " price = " << bonds_price(times, cashflows, tsfalt) << endl;
cout << " duration = " << bonds_duration(times, cashflows, tsfalt) << endl;
cout << " convexity = " << bonds_convexity(times, cashflows, tsfalt) << endl;
Output from C++ program:
price = 99.1088
duration = 1.9087
convexity = 3.72611
```

参考文献 Shiller (1990) 是关于期限结构应用的良好参考。

## 第 6 章

## 均值-方差边界

## 目录

- 6.1 设置 .................................................... 67
- 6.2 最小方差边界 ........................ 69
- 6.3 边界组合计算 ................... 69
- 6.4 全局最小方差组合 ................ 72
- 6.5 有效组合 ................................... 72
- 6.6 零贝塔组合 ................................ 73
- 6.7 考虑无风险资产 .......................... 73
- 6.8 含无风险资产的有效集 ................... 74
- 6.9 卖空约束 ................................. 75
- 6.10 夏普比率 ...................................... 75
- 6.11 均衡：CAPM ..................................... 76
  - 6.11.1 特雷诺 ........................................... 76
  - 6.11.2 詹森 ............................................ 76
- 6.12 使用均值-方差和 CAPM ................. 76
- 6.13 使用矩阵库进行均值-方差分析 ....... 77

我们现在讨论金融中的一个经典主题：均值-方差分析。这引出了考虑现金流风险性的方法。

均值-方差分析关注投资者在风险资产组合之间的选择，以及投资者如何选择组合权重。设 r_p 为组合收益率。我们假设投资者对组合 p 的偏好满足均值-方差效用表示，u(p) = u(E[r_p], \sigma(r_p))，效用随预期收益增加而增加（\partial u / \partial E[r_p] > 0），随方差增加而减少（\partial u / \partial \text{var}(r_p) < 0）。在此部分，我们考虑此类决策者的组合机会集的表示。该机会集具有若干有用特性，这些特性纯粹源于优化问题的数学表述。我们在此关注这些特性。

## 6.1 设置

我们假设存在 n \ge 2 种风险证券，其预期收益为 e

\[
e = \begin{bmatrix} E[r_1] \\ E[r_2] \\ \vdots \\ E[r_n] \end{bmatrix}
\]

和协方差矩阵 V：

\[
\mathbf{V} = \begin{bmatrix} \sigma(r_1, r_1) & \sigma(r_1, r_2) & \dots \\ \sigma(r_2, r_1) & \sigma(r_2, r_2) & \dots \\ \vdots & & \\ \sigma(r_n, r_1) & & \dots & \sigma(r_n, r_n) \end{bmatrix}
\]

假设协方差矩阵 V 可逆。

组合 \(\rho\) 由投资于风险资产的一组权重 w 定义。

\[
\mathbf{w} = \begin{bmatrix} \omega_1 \\ \omega_2 \\ \vdots \\ \omega_n \end{bmatrix}
\]

其中 \(w_i\) 是投资于资产 \(i\) 的投资者财富比例。注意权重之和为一。

组合的预期收益计算如下

\(E[r_p] = \mathbf{w}'\mathbf{e}\)

组合的方差为

\(\sigma^2(r_p) = \mathbf{w}'\mathbf{Vw}\)

### 示例

| t | 资产 | E[r] | \(\sigma^2(r)\) |
|---|---|---|---|
| 1 | | 10% | 0.20 |
| 2 | | 11.5% | 0.10 |
| 3 | | 8% | 0.15 |

这三种资产相互独立（不相关）。

- 1. 确定三种资产等权重组合的预期收益和标准差

```
Matlab program:
e=[0.1 0.11 0.08]
V=[0.2 0.0 0.0; 0.0 0.1 0 ; 0 0 0.15]
w=1/3*[1 1 1]
er = w*e'
sigma=sqrt(w*V*w*')
Output from Matlab program:
e =
 0.10000 0.11000 0.08000
V =
 0.20000 0.00000 0.00000
 0.00000 0.10000 0.00000
 0.00000 0.00000 0.15000
w =
 0.33333 0.33333 0.33333
er = 0.096667
sigma = 0.22361
```

## 6.2 最小方差边界

如果一个组合在给定预期收益下使方差最小化，则称其为*边界*组合，即边界组合 $p$ 求解

$$
\mathbf{w}_p = \arg \min_{\mathbf{w}} \frac{1}{2} \mathbf{w}' \mathbf{V} \mathbf{w}
$$

约束条件为：

$$
\mathbf{w}' \mathbf{e} = E[\bar{r}_p]
$$

$$
\mathbf{w}' \mathbf{1} = 1
$$

所有边界组合的集合称为*最小方差边界*。

## 6.3 边界组合计算

**提议 1** 如果矩阵 $\mathbf{V}$ 满秩，且没有卖空限制，则均值为 $E[\bar{r}_p]$ 的边界组合 $p$ 的权重 $\mathbf{w}_p$ 可表示为

$$
\mathbf{w}_p = \mathbf{g} + \mathbf{h} E[\bar{r}_p]
$$

其中

$$
\mathbf{g} = \frac{1}{D} (B\mathbf{1} - A\mathbf{e}') \mathbf{V}^{-1}
$$

$$
\mathbf{h} = \frac{1}{D} (C\mathbf{e} - A\mathbf{1}') \mathbf{V}^{-1}
$$

$$
A = \mathbf{1}' \mathbf{V}^{-1} \mathbf{e}
$$

$$
B = \mathbf{e}' \mathbf{V}^{-1} \mathbf{e}
$$

$$
C = \mathbf{1}' \mathbf{V}^{-1} \mathbf{1}
$$

$$
\mathbf{\Lambda} = \begin{bmatrix} B & A \\ A & C \end{bmatrix}
$$

$$
D = BC - A^2 = |\mathbf{\Lambda}|
$$

**证明**

任何最小方差组合都求解以下规划问题

$$
\mathbf{w}_p = \arg \min_{\mathbf{w}} \frac{1}{2} \mathbf{w}' \mathbf{V} \mathbf{w}
$$

约束条件为

$$
\mathbf{w}' \mathbf{e} = E[\bar{r}_p]
$$

$$
\mathbf{w}' \mathbf{1} = 1
$$

为此问题构建拉格朗日函数

$$
L(\mathbf{w}, \lambda, \gamma | \mathbf{e}, \mathbf{V}) = \frac{1}{2} \mathbf{w}' \mathbf{V} \mathbf{w} - \lambda \left( E[\bar{r}_p] - \mathbf{w}' \mathbf{e} \right) - \gamma (1 - \mathbf{w}' \mathbf{1})
$$

