

## 第 22 章 期限结构模型

### 目录

| 节 | 页码 |
|---|---|
| 22.1 Nelson Siegel 期限结构近似 | 198 |
| 22.2 扩展 Nelson Siegel 模型 | 200 |
| 22.3 三次样条 | 202 |
| 22.4 Cox Ingersoll Ross | 205 |
| 22.5 Vasicek | 208 |
| 22.6 推荐阅读 | 210 |

我们现在对第 5 章中的期限结构分析进行扩展。如所示，期限结构最好被视为一个抽象类，它作为到期期限的函数，提供零息债券价格（贴现因子）、零息债券收益率（即期利率）或远期利率。在之前的情况中，我们考虑了期限结构的两种特定实现。一种是平坦期限结构，另一种是通过对即期利率进行线性插值来估计的期限结构。我们现在考虑若干替代期限结构模型。本章的重点是实证性的。我们考虑以一种低维方式指定期限结构的方法。本质上，我们正在研究曲线拟合的方法，即估计时间与贴现因子之间，或时间与即期利率之间的非线性关系。由于关系是非线性的，这是一个非平凡问题。必须选择一个功能形式来估计，它允许足够的灵活性来“拟合”期限结构，但又不至于过于灵活以至于违反期限结构的经济限制。以下是一些考虑因素。

- 贴现因子必须为正。\( (d_t > 0) \)。这是因为它们是价格，负价格允许套利。
- 贴现因子必须是时间的非递增函数。\( (d_t \ge d_{t+k} \forall k > 0) \)。同样，这是为了避免套利。
- 名义利率不能为负。\( (r_t \ge 0 \forall t) \) 这是没有套利机会的另一个含义。
- 贴现因子和利率都必须是时间的平滑函数。
- 今天付款的价值就是今天的付款。\( d_0 = 1 \)。

已经考虑了若干替代的期限结构估计方法。有些纯粹用作插值函数，而另一些则是完全指定的动态期限结构模型。在接下来的模型中，Nelson 和 Siegel (1987) 提出的近似函数以及例如 McCulloch (1971) 使用的三次样条属于第一类，而 Cox、Ingersoll 和 Ross (1985) 以及 Vasicek (1977) 的期限结构模型属于第二类。

我们在这里考虑的函数的典型用途是什么？首先从一组固定收益证券开始，通常是一组国债券。观察这些债券的价格后，人们会问：哪一组贴现因子最有可能产生了观察到的价格。或者：哪种期限结构近似对这组观察到的债券价格提供了“最佳拟合”。

### 22.1 Nelson Siegel 期限结构近似

Nelson 和 Siegel (1987) 提出了公式 22.1 所示的参数化

```
r(t) = \beta_0 + (\beta_1 + \beta_2) \left[ \frac{1 - e^{-\frac{t}{\lambda}}}{\frac{t}{\lambda}} \right] + \beta_2 \left[ e^{-\frac{t}{\lambda}} \right]
```

符号说明：t：到期期限。r：即期利率，\beta_0、\beta_1、\beta_2 和 \lambda：常数。

公式 22.1：Nelson 和 Siegel (1987) 的期限结构参数化

此计算的实现如 C++ 代码 22.1 所示。

```
#include <cmath>
using namespace std;
double term_structure::yield_nelson_siegel(const double& t,
                                          const double& beta0,
                                          const double& beta1,
                                          const double& beta2,
                                          const double& lambda) {
  if (t==0.0) return beta0;
  double tl = t/lambda;
  double r = beta0 + (beta1+beta2) * ((1-exp(-tl))/tl) + beta2 * exp(-tl);
  return r;
};
```

C++ 代码 22.1：Nelson 和 Siegel (1987) 期限结构模型的计算

这被封装在期限结构类中，如头文件 22.1 和 C++ 代码 22.2 所示。

```
class term_structure_class_nelson_siegel : public term_structure_class {
private:
  double beta0_, beta1_, beta2_, lambda_;
public:
  term_structure_class_nelson_siegel(const double& beta0,
                                     const double& beta1,
                                     const double& beta2,
                                     const double& lambda);
  virtual double yield(const double& T) const;
};
```

头文件 22.1：定义 Nelson Siegel 近似期限结构类封装的头文件

```
#include "fin_recipes.h"

term_structure_class_nelson_siegel::term_structure_class_nelson_siegel(const double& b0,
                                                                       const double& b1,
                                                                       const double& b2,
                                                                       const double& lambda) {
    beta0_ = b0; beta1_ = b1; beta2_ = b2; lambda_ = lambda;
}

double term_structure_class_nelson_siegel::yield(const double& t) const {
    if (t <= 0.0) return beta0_;
    return term_structure::yield_nelson_siegel(t, beta0_, beta1_, beta2_, lambda_);
};
```

C++ 代码 22.2：定义 Nelson Siegel 近似期限结构类封装

### 示例

使用 Nelson Siegel 近似中的参数 \(\beta_0 = 0.01, \beta_1 = 0.01, \beta_2 = 0.01, \lambda = 5.0\) 和 \(t = 1\)，求 1 年贴现因子和即期利率，以及第 1 年和第 2 年之间的远期利率。

```
C++ program:
double beta0=0.01; double beta1=0.01; double beta2=0.01; double lambda=5.0;
double t=1.0;
cout << "Example calculations using the Nelson Siegel term structure approximation"
<< endl;
cout << " direct calculation, yield = "
<< term_structure::yield_nelson_siegel(t,beta0,beta1,beta2,lambda) << endl;
term_structure.nelson_siegel_msr(beta0,beta1,beta2,lambda);
cout << " using a term structure class" << endl;
cout << " yield (t=1) = " << nsr(t) << endl;
cout << " discount factor (t=1) = " << ns_df(t) << endl;
cout << " forward rate (t1=1, t2=2) = " << nsf(1,2) << endl;
Output from C++ program:
Example calculations using the Nelson Siegel term structure approximation
using a term structure class
yield (t=1) = 0.0363142
discount factor (t=1) = 0.964337
forward rate (t1=1, t2=2) = 0.0300602
```

### 22.2 扩展 Nelson Siegel 模型

Nelson 和 Siegel (1987) 模型很简单，参数具有清晰明显的经济解释。它确实存在一个问题，即它允许的期限结构形状有限。为了允许更复杂的形状，例如驼峰形状，它已以各种方式进行了扩展。Lars Svensson 引入了一种流行的近似方法，参数化如公式 22.2 所示

```
\( r(t) = \beta_0 + \beta_1 \left( \frac{1 - e^{-\frac{t}{\tau_1}}}{\frac{t}{\tau_1}} \right) + \beta_2 \left( \frac{1 - e^{-\frac{t}{\tau_1}}}{\frac{t}{\tau_1}} - e^{-\frac{t}{\tau_1}} \right) + \beta_3 \left( \frac{1 - e^{-\frac{t}{\tau_2}}}{\frac{t}{\tau_2}} - e^{-\frac{t}{\tau_2}} \right) \)
```

符号说明：\(t\)：到期期限，\(r\)：即期利率，\(\beta_0, \beta_1, \beta_2\) 和 \(\tau_1, \tau_2\)：常数。

公式 22.2：Svensson 对 Nelson 和 Siegel (1987) 期限结构参数化的扩展

这被封装在期限结构类中，如头文件 22.2 和 C++ 代码 22.4 所示。

```
#include <cmath>
using namespace std;

double term_structure_yield_svensson(const double& t,
                                     const double& beta0,
                                     const double& beta1,
                                     const double& beta2,
                                     const double& beta3,
                                     const double& tau1,
                                     const double& tau2){
    if (t==0.0) return beta0;
    double r = beta0;
    r += beta1* ((1-exp(-t/tau1))/(t/tau1)) ;
    r += beta2 * ( ((1-exp(-t/tau1))/(t/tau1)) - exp(-t/tau1) ) ;
    r += beta3 * ( ((1-exp(-t/tau2))/(t/tau2)) - exp(-t/tau2) ) ;
    return r;
};
```

C++ 代码 22.3：Svensson 扩展 Nelson 和 Siegel (1987) 期限结构模型的计算

```
class term_structure_class_svensson : public term_structure_class {
private:
    double beta0_, beta1_, beta2_, beta3_, tau1_, tau2_;
public:
    term_structure_class_svensson(const double& beta0,
                                  const double& beta1,
                                  const double& beta2,
                                  const double& beta3,
                                  const double& tau1,
                                  const double& tau2);
    virtual double yield(const double& t) const;
};
```

头文件 22.2：定义 Svensson 模型期限结构类封装的头文件

```
#include "fin_recipes.h"

term_structure_class_svensson::term_structure_class_svensson(const double& b0, const double& b1, const double& b2, const double& b3,
                                                               const double& tau1, const double& tau2) {
    beta0_ = b0; beta1_ = b1; beta2_ = b2; beta3_ = b3; tau1_ = tau1; tau2_ = tau2;
};

double term_structure_class_svensson::yield(const double& t) const {
    if (t <= 0.0) return beta0_;
    return term_structure_yield_svensson(t, beta0_, beta1_, beta2_, beta3_, tau1_, tau2_);
};
```

C++ 代码 22.4：定义 Svensson 模型期限结构类封装

