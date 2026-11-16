
$d_t = e^{-r_t t}$

$r_t = \frac{-\ln(d_t)}{t}$

$f_{t_1, t_2} = \frac{\ln(\frac{d_{t_1}}{d_{t_2}})}{t_2 - t_1}$

$f_{t_1, t_2} = r_{t_2} \frac{t_2}{t_2 - t_1} - r_{t_1} \frac{t_1}{t_2 - t_1}$

符号：$d_t$ 时间 $t$ 付款的贴现因子，$r_t$：适用于时间 $t$ 现金流的即期利率。$f_{t_1, t_2}$ 时间 $t_1$ 和 $t_2$ 之间的远期利率，即你今天同意用于未来交易的利率。

```
#include <cmath>
using namespace std;
double term_structure_yield_from_discount_factor(const double& d, const double& t) {
return (-log(d)/t);
}
double term_structure_discount_factor_from_yield(const double& r, const double& t) {
return exp(-r*t);
};
double term_structure_forward_rate_from_discount_factors(const double& d1, const double& d2,
const double& time) {
return (log (d1/d2))/time;
};
double term_structure_forward_rate_from_yields(const double& r1, const double& r2,
const double& t1, const double& t2) {
return r2*t2/(t2-t1)-r1*t1/(t2-t1);
};
```

C++ 代码 5.1：期限结构转换

C++ 代码 5.1 展示了这些转换的实现。

### 示例

给定一期期限结构即期利率 $r_1 = 5\%$ 和两期贴现因子 $d_2 = 0.9$。计算两期即期利率以及从 1 到 2 的远期利率。

### C++ 程序：

```
double t1=1; double r1=0.05; double d1=term_structure_discount_factor_from_yield(r1,t1);
cout << " a " << " < t1 < " << " period spot rate of " << r1
<< " corresponds to a discount factor of " << d1 << endl;

double t2=2; double d2 = 0.9;
double r2 = term_structure_yield_from_discount_factor(d2,t2);
cout << " a " << " < t2 < " << " period discount factor of " << d2
<< " corresponds to a spot rate of " << r2 << endl;

cout << " the forward rate between " << t1 << " " << " and " << t2
<< " using " << " term_structure_forward_rate_from_discount_factors(d1,d2,t2-t1) is " << term_structure_forward_rate_from_discount_factors(d1,d2,t2-t1)
<< endl;
cout << " and is " << term_structure_forward_rate_from_yields(r1,r2,t1,t2)
<< " using yields" << endl;
```

### C++ 程序输出：

```
a 1 period spot rate of 0.05 corresponds to a discount factor of 0.951229
a 2 period discount factor of 0.9 corresponds to a spot rate of 0.0526803
the forward rate between 1 and 2 is 0.0553605 using discount factors
and is 0.0553605 using yields
```

## 5.2 将期限结构作为对象

从前面可以看出，期限结构可以用贴现因子、即期利率或远期利率来描述，但这并不能帮助我们解决维度问题。如果从贴现因子的角度思考，要对当前期限结构进行完全说明，需要无限多个贴现因子 $\{d_t\}_{t \in R+}$。也许将这组贴现因子视为一个函数 d(t) 更容易理解，该函数给定非负时间 t，返回贴现因子。既然我们已经确立了定义期限结构的三种等价方式——贴现因子、即期利率和远期利率，因此我们可以将期限结构描述为三个不同函数的集合，它们对同一底层对象提供不同的视图。

期限结构是一个抽象对象，对用户而言应提供

- 贴现因子 d（零息债券价格）。
- 即期利率 r（零息债券收益率）。
- 远期利率 f

针对任何未来到期期限 t。期限结构的用户不需要知道期限结构是如何实现的，只需要一个指定上述三个函数的接口。

这非常适合作为 C++ 类来实现。在 C++ 术语中，类是一组数据结构和操作这些数据结构的函数。在当前语境下，它是指定这三个函数的一种方式。

```
r(t)
d(t)
f(t)
```

### 5.2.1 基类

头文件 5.1 展示了如何将通用期限结构描述为 C++ 类。

```
#ifndef _TERM_STRUCTURE_CLASS.H_
#define _TERM_STRUCTURE_CLASS.H_
class term_structure_class {
public:
    virtual double r(const double& t) const; // yield on zero coupon bond
    virtual double d(const double& t) const; // discount factor/price of zero coupon bond
    virtual double f(const double& t1, const double& t2) const; // forward rate
};
// term_structure.class();
#endif
```

头文件 5.1：描述 term_structure 基类的头文件

这些函数的代码使用了本章前面描述的用于在期限结构各种视图之间转换的算法。期限结构类仅为这些算法提供一个方便的接口。代码如 C++ 代码 5.2 所示

请注意，计算定义是循环的。任何给定的特定类型期限结构都必须至少重写函数 r（收益率）、d（贴现因子）或 f（远期利率）中的一个。

接下来我们考虑两个特定期限结构的示例。

```
#include "fin_recipes.h"

term_structure_class::term_structure_class(){};

double term_structure_class::f(const double& t1, const double& t2) const{
  double d1 = d(t1);
  double d2 = d(t2);
  return term_structure_forward_rate_from_discount_factors(d1,d2,t2-t1);
};

double term_structure_class::r(const double& t) const{
  return term_structure_yield_from_discount_factor(d(t),t);
};

double term_structure_class::d(const double& t) const {
  return term_structure_discount_factor_from_yield(r(t),t);
};
```

C++ 代码 5.2：期限结构类中贴现因子、即期利率和远期利率之间转换的默认代码

### 5.2.2 平坦期限结构。

平坦期限结构重写了基类的收益率成员函数。这种类型的期限结构只需要一个利率这一数据。

```
#ifndef _TERM_STRUCTURE_CLASS_FLAT_
#define _TERM_STRUCTURE_CLASS_FLAT_

#include "term_structure_class.h"

class term_structure_class_flat : public term_structure_class {
private:
    double R_; // interest rate
public:
    term_structure_class_flat(const double& r);
    virtual double r(const double& t) const;
    void set_int_rate(const double& r);
};

#endif
```

头文件 5.2：使用平坦期限结构的期限结构类头文件

```
#include "fin_recipes.h"

term_structure_class_flat::term_structure_class_flat(const double& r) { R_ = r; };

term_structure_class_flat::~term_structure_class_flat(){};

double term_structure_class_flat::r(const double& T) const { if (T>=0) return R_; return 0; };

void term_structure_class_flat::set_int_rate(const double& r) { R_ = r; };
```

C++ 代码 5.3：使用平坦期限结构实现期限结构类

### 示例

期限结构为平坦，r = 5%。确定第 1 年和第 2 年的贴现因子以及 1 到 2 之间的远期利率。

C++ 程序：

```
term_structure_class_flat ts(0.05);
double t1=1;
cout << "discount factor t1 = " << t1 << "," << ts.d(t1) << endl;
double t2=2;
cout << "discount factor t2 = " << t2 << "," << ts.d(t2) << endl;
cout << "spot rate t = " << t1 << " = " << ts.r(t1) << endl;
cout << "spot rate t = " << t2 << " = " << ts.r(t2) << endl;
cout << "forward rate from t1= " << t1 << " to t2= " << t2 << "," << ts.f(t1,t2) << endl;
```

C++ 程序输出：

```
discount factor t1 = 1:0.951229
discount factor t2 = 2:0.904837
spot rate t = 1:0.05
spot rate t = 2:0.05
forward rate from t1= 1 to t2= 2:0.05
```

## 5.3 使用当前观察到的期限结构。

构建一般期限结构的第一步是使用债券价格和利率的市场数据来推断贴现因子。表达此问题的最简单方式是使用线性代数。假设我们有三种债券，现金流分别发生在时间 1、2 和 3。

```
B_1 = d_1 C_{11} + d_2 C_{12} + d_3 C_{13}
B_2 = d_1 C_{21} + d_2 C_{22} + d_3 C_{23}
B_3 = d_1 C_{31} + d_2 C_{32} + d_3 C_{33}
```

用矩阵表示

```
\begin{bmatrix} B_1 \\ B_2 \\ B_3 \\ \end{bmatrix} = \begin{bmatrix} d_1 \\ d_2 \\ d_3 \\ \end{bmatrix} \begin{bmatrix} C_{11} & C_{12} & C_{13} \\ C_{21} & C_{22} & C_{23} \\ C_{31} & C_{32} & C_{33} \\ \end{bmatrix}
```

求解贴现因子

```
\begin{bmatrix} d_1 \\ d_2 \\ d_3 \\ \end{bmatrix} = \begin{bmatrix} C_{11} & C_{12} & C_{13} \\ C_{21} & C_{22} & C_{23} \\ C_{31} & C_{32} & C_{33} \\ \end{bmatrix}^{-1} \begin{bmatrix} B_1 \\ B_2 \\ B_3 \\ \end{bmatrix}
```

或

```
d = C^{-1}B
```

使用明显的矩阵定义

```
B = \begin{bmatrix} B_1 \\ B_2 \\ B_3 \\ \end{bmatrix} \quad d = \begin{bmatrix} d_1 \\ d_2 \\ d_3 \\ \end{bmatrix} \quad C = \begin{bmatrix} C_{11} & C_{12} & C_{13} \\ C_{21} & C_{22} & C_{23} \\ C_{31} & C_{32} & C_{33} \\ \end{bmatrix}
```

### 示例

观察到以下债券和债券价格：

| 债券 | 债券价格 | 0 | 0.5 | 1 | 1.5 | 2 | 3 | 4 |
|---|---|---|---|---|---|---|---|---|
| 1 | 98 | | 100 | | | | | |
| 2 | 96 | | | 100 | | | | |
| 3 | 92 | | | | 100 | | | |
| 4 | 118 | | 10 | 10 | 10 | 110 | | | |
| 5 | 109 | | 8 | 8 | 8 | 8 | | 108 |
| 6 | 112 | | 9 | 9 | 9 | 9 | 9 | 109 |

这些债券是国债证券，可以被视为名义上无风险。

- 1. 对于哪些到期期限可以推断贴现因子？
- 2. 确定市场中的隐含贴现因子。
- 3. 这一组贴现率隐含的利率是多少？

在这里，我们可以找到到期期限为 0.5、1、1.5、2、3 和 4 的贴现因子。
