
- max_element (C++ 函数)
- namespace (C++ 概念)
- return
- 标准命名空间 (C++ 概念)
- string (C++ 基本类型)
- using (C++ 概念)
- vector (C++ 容器类)。定义于 <vector>
- while

## 附录 C

### 与外部库的接口

### 目录

| 节 | 页 |
| :--- | :--- |
| C.1 Boost | 239 |
| C.2 Newmat | 239 |
| C.3 IT++ | 239 |
| C.4 GSL | 239 |
| C.4.1 \( N_3 \) 的求值 | 239 |
| C.5 互联网链接 | 240 |

在多个地方，我们使用了其他公共领域软件包中的例程。在本附录中，有一些关于所引用库的说明，以及关于链接到它们的一些评论。

### C.1 Boost

大量经过同行评审的代码。特别有用的是：date_time 库。

### C.2 Newmat

Newmat 是一个矩阵库，它试图在 C++ 中执行类似 MATLAB 的操作，即可以定义矩阵和向量，然后相乘等等，而无需显式调用子程序，而是以更面向数学的方式编写操作。

### C.3 IT++

IT++ 是一个庞大的库，包含各种不同的

### C.4 GSL

### C.4.1 \( N_3 \) 的求值

在 Geske 和 Johnson (1984) 的美式看跌期权近似计算中，需要求解三元正态分布。遵循论文中的讨论，其求值如下

```
N_3(h, k, j; \rho_{12}, \rho_{13}, \rho_{23}) = \int_{-\infty}^{j} n(z) N_2 \left( \frac{k - \rho_{23}z}{\sqrt{1 - \rho_{23}^2}}, \frac{h - \rho_{13}z}{\sqrt{1 - \rho_{13}^2}} \bigg| \frac{\rho_{12} - \rho_{13}\rho_{23}}{\sqrt{1 - \rho_{13}^2}\sqrt{1 - \rho_{23}^2}} \right)
```

这是一个一元积分，可以使用求积法进行求值。

```
#include <cmath>
#include <iostream>
using namespace std;

#include "gsl/gsl_integration.h"
#include "normdist.h"

struct n3_pars {double h; double k; double rho12; double rho13; double rho23; };

extern "C"{
double f3(double z, void *p){
  struct n3_pars* pars = (struct n3_pars*)p;
  double h = (pars->h);
  double k = (pars->k);
  double rho12 = (pars->rho12);
  double rho13 = (pars->rho13);
  double rho23 = (pars->rho23);
  double f = n(z);
  f*=N( (k-rho23*z)/sqrt(1.0-rho23*rho23),
        (h-rho13*z)/sqrt(1.0-rho13*rho13),
        (rho12-rho13*rho23)/(sqrt(1.0-rho13*rho13)*sqrt(1.0-rho23*rho23)));
  return f;
};

double N3(const double& h, const double& k, const double& j,
          const double& rho12, const double& rho13, const double& rho23){
  struct n3_pars pars = { h, k, rho12, rho13, rho23};
  size_t n = 1000;
  gsl_integration_workspace* w = gsl_integration_workspace_alloc(n);
  gsl_function F;
  F.function = &f3;
  F.params = &pars;
  double result, error;
  gsl_integration_qags(&F,-20.0,1e-7,1e-7,n,w,&result,&error);
  return result;
};
```

C++ 代码 C.1：使用 Geske 和 Johnson (1984) 的方法近似 $N_3()$

### C.5 互联网链接

一些有用的互联网链接

- http://www.robertnz.net：Newmat 的主页，Newmat 是示例中使用的矩阵类。

## 附录 D

### 例程名称汇总

在许多算法中都使用了其他例程。为简化问题，所有例程都汇总在一个头文件 fin_recipes.h 中。本附录展示了此文件。

```
// file: fin_recipes.h
// author: Bernt Arne Oedegaard
// defines all routines in the financial numerical recipes "book"

#ifndef _FIN_RECIPES_H_
#define _FIN_RECIPES_H_

#include <vector>
#include <cmath>
using namespace std;

// ////////////////// present value ///////////////////////////////////
// discrete compounding
// discrete, annual compounding
double cash_flow_pv_discrete( const vector<double>& cflow_times, const vector<double>& cflow_amounts,
                              const double& r);
double cash_flow_irr_discrete(const vector<double>& cflow_times, const vector<double>& cflow_amounts);
bool cash_flow_unique_irr(const vector<double>& cflow_times, const vector<double>& cflow_amounts);
double bonds_price_discrete(const vector<double>& cashflow_times, const vector<double>& cashflows,
                            const double& r);
double bonds_yield_to_maturity_discrete(const vector<double>& cashflow_times, const vector<double>& cashflows,
                                        const double& bond_price);
double bonds_duration_discrete(const vector<double>& cashflow_times,
                               const vector<double>& cashflows,
                               const double& r);
double bonds_duration_macaulay_discrete(const vector<double>& cashflow_times,
                                        const vector<double>& cashflows,
                                        const double& bond_price);
double bonds_duration_modified_discrete(const vector<double>& cashflow_times,
                                        const vector<double>& cashflows,
                                        const double& bond_price);
double bonds_convexity_discrete(const vector<double>& cashflow_times,
                                const vector<double>& cashflows,
                                const double& r);
// ////////////////// continuous compounding ///////////////////////////////////
double cash_flow_pv(const vector<double>& cflow_times, const vector<double>& cflow_amounts,const double& r);
double cash_flow_irr(const vector<double>& cflow_times, const vector<double>& cflow_amounts);
double cash_flow_price(const vector<double>& cflow_times, const vector<double>& cflow_amounts, const vector<double>& cashflows, const double& r);
double bonds_price(const vector<double>& coupon_times, const vector<double>& coupon_amounts,
                   const vector<double>& principal_times, const vector<double>& principal_amounts,
                   const double& r);
double bonds::duration(const vector<double>& cashflow_times, const vector<double>& cashflows,
    const double& r);
double bonds::yield_to_maturity(const vector<double>& cashflow_times,const vector<double>& cashflow_amounts,
    const double& bond_price);
double bonds::duration_macaulay(const vector<double>& cashflow_times, const vector<double>& cashflows,
    const double& bond_price);
double bonds::convexity(const vector<double>& cashflow_times, const vector<double>& cashflow_amounts,
    const double& y );

# /// term structure basics

double term_structure::yield_from_discount_factor(const double& dfact, const double& t);
double term_structure::discount_factor_from_yield(const double& r, const double& t);
double term_structure::forward_rate_from_discount_factors(const double& d_t1, const double& d_t2,
    const double& t1, const double& t2);
double term_structure::forward_rate_from_yields(const double& t1, const double& r_t1, const double& r_t2,
    const double& t2);
double term_structure::yield_linearly_interpolated(const double& t,
    const vector<double>& obs_times,
    const vector<double>& obs_yields);

# /// a term structure class

class term_structure_class {
public:
    virtual ~term_structure_class();
    virtual double r(const double& t) const; // short rate, yield on zero coupon bond
    virtual double d(const double& t) const; // discount_factor
    virtual double f(const double& t1, const double& t2) const; // forward_rate
};

class term_structure_class_flat : public term_structure_class {
private:
    double R_; // interest rate
public:
    term_structure_class_flat(const double& r);
    virtual ~term_structure_class_flat();
    virtual double r(const double& t) const;
    void set_interest_rate(const double& r);
};

class term_structure_class_interpolated : public term_structure_class {
private:
    vector<double> times_; // use to keep a list of yields
    vector<double> yields_;
    void clear();
public:
    term_structure_class_interpolated();
    term_structure_class_interpolated(const vector<double>& times, const vector<double>& yields);
    virtual ~term_structure_class_interpolated();
    term_structure_class_interpolated(const term_structure_class_interpolated&);
    term_structure_class_interpolated operator=(const term_structure_class_interpolated&);
    int no_observations() const { return int(times_.size()); };
    virtual double r(const double& T) const;
    void set_interpolated_observations(vector<double>& times, vector<double>& yields);
};

# /// using the term structure classes

double bonds::price(const vector<double>& cashflow_times,
    const vector<double>& cashflow,
    const term_structure_class& d);
double bonds::duration(const vector<double>& cashflow_times,
    const vector<double>& cashflow_amounts,
    const term_structure_class& d);
```
