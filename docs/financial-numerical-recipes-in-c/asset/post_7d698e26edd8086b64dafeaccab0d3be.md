
$d_t = e^{-r_t t}$

$r_t = \frac{-\ln(d_t)}{t}$

$f_{t_1, t_2} = \frac{\ln(\frac{d_{t_1}}{d_{t_2}})}{t_2 - t_1}$

$f_{t_1, t_2} = r_{t_2} \frac{t_2}{t_2 - t_1} - r_{t_1} \frac{t_1}{t_2 - t_1}$

Notation: $d_t$ discount factor for payment at time $t$, $r_t$: spot rate applying to cash flows at time $t$. $f_{t_1, t_2}$ forward rate between time $t_1$ and $t_2$, i.e. the interest rate you would agree on today on the future transactions.

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

C++ Code 5.1: Term structure transformations

C++ Code 5.1 shows the implementation of these transformations.

### Example

You are given the one period spot rate $r_1 = 5\%$ and the two period discount factor $d_2 = 0.9$. Calculate the two period spot rate and the forward rate from 1 to 2.

### C++ program:

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

### Output from C++ program:

```
a 1 period spot rate of 0.05 corresponds to a discount factor of 0.951229
a 2 period discount factor of 0.9 corresponds to a spot rate of 0.0526803
the forward rate between 1 and 2 is 0.0553605 using discount factors
and is 0.0553605 using yields
```

## 5.2 The term structure as an object

From the previous we see that the term structure can be described in terms of discount factors, spot rates or forward rates, but that does not help us in getting round the dimensionality problem. If we think in terms of discount factors, for a complete specification of the current term structure one needs an infinite number of discount factors $\{d_t\}_{t \in R+}$. It is perhaps easier to think about this set of discount factors as a function d(t), that, given a nonnegative time t, returns the discount factor. Since we have established that there are three equivalent ways of defining a term structure, discount factors, spot rates and forward rates, we can therefore describe a term structure as a collection of three different functions that offer different views of the same underlying object.

A term structure is an abstract object that to the user should provide

- discount factors d (prices of zero coupon bonds).
- spot rates r (yields of zero coupon bonds).
- forward rates f

for any future maturity t. The user of a term structure will not need to know how the term structure is implemented, all that is needed is an interface that specifies the above three functions.

This is tailor made for needing be implemented as a C++ class. A class in C++ terms is a collection of data structures and functions that operate on these data structures. In the present context it is a way of specifying the three functions.

```
r(t)
d(t)
f(t)
```

### 5.2.1 Base class

Header File 5.1 shows how we describe the generic term structure as a C++ class.

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

Header file 5.1: Header file describing the term_structure base class

The code for these functions uses algorithms that are described earlier in this chapter for transforming between various views of the term structure. The term structure class merely provide a convenient interface to these algorithms. The code is shown in C++ Code 5.2

Note that the definitions of calculations are circular. Any given specific type of term structure has to over-ride at least one of the functions r (yield), d (discount factor) or f (forward rate).

We next consider two examples of specific term structures.

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

C++ Code 5.2: Default code for transformations between discount factors, spot rates and forward rates in a term structure class

### 5.2.2 Flat term structure.

The flat term structure overrides the yield member function of the base class.
The only piece of data this type of term structure needs is an interest rate.

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

Header file 5.2: Header file for term structure class using a flat term structure

```
#include "fin_recipes.h"

term_structure_class_flat::term_structure_class_flat(const double& r) { R_ = r; };

term_structure_class_flat::~term_structure_class_flat(){};

double term_structure_class_flat::r(const double& T) const { if (T>=0) return R_; return 0; };

void term_structure_class_flat::set_int_rate(const double& r) { R_ = r; };
```

C++ Code 5.3: Implementing term structure class using a flat term structure

### Example

The term structure is flat with r = 5%. Determine the discount factors for years 1 and 2 and the forward rate between 1 and 2.

C++ program:

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

Output from C++ program:

```
discount factor t1 = 1:0.951229
discount factor t2 = 2:0.904837
spot rate t = 1:0.05
spot rate t = 2:0.05
forward rate from t1= 1 to t2= 2:0.05
```

## 5.3 Using the currently observed term structure.

A first step to a general term structure is to use market data on bond prices and interest rates to infer discount factors. The simplest way of presenting this problem is in terms of linear algebra. Suppose we have three bonds with cash flows at times 1, 2 and 3.

```
B_1 = d_1 C_{11} + d_2 C_{12} + d_3 C_{13}
B_2 = d_1 C_{21} + d_2 C_{22} + d_3 C_{23}
B_3 = d_1 C_{31} + d_2 C_{32} + d_3 C_{33}
```

Writing this in terms of matrices

```
\begin{bmatrix} B_1 \\ B_2 \\ B_3 \\ \end{bmatrix} = \begin{bmatrix} d_1 \\ d_2 \\ d_3 \\ \end{bmatrix} \begin{bmatrix} C_{11} & C_{12} & C_{13} \\ C_{21} & C_{22} & C_{23} \\ C_{31} & C_{32} & C_{33} \\ \end{bmatrix}
```

Solving for the discount factors

```
\begin{bmatrix} d_1 \\ d_2 \\ d_3 \\ \end{bmatrix} = \begin{bmatrix} C_{11} & C_{12} & C_{13} \\ C_{21} & C_{22} & C_{23} \\ C_{31} & C_{32} & C_{33} \\ \end{bmatrix}^{-1} \begin{bmatrix} B_1 \\ B_2 \\ B_3 \\ \end{bmatrix}
```

or

```
d = C^{-1}B
```

using the obvious matrix definitions

```
B = \begin{bmatrix} B_1 \\ B_2 \\ B_3 \\ \end{bmatrix} \quad d = \begin{bmatrix} d_1 \\ d_2 \\ d_3 \\ \end{bmatrix} \quad C = \begin{bmatrix} C_{11} & C_{12} & C_{13} \\ C_{21} & C_{22} & C_{23} \\ C_{31} & C_{32} & C_{33} \\ \end{bmatrix}
```

### Example

The following set of bond and bond prices is observed:

| Bond | Bond Price | 0 | 0.5 | 1 | 1.5 | 2 | 3 | 4 |
|---|---|---|---|---|---|---|---|---|
| 1 | 98 | | 100 | | | | | |
| 2 | 96 | | | 100 | | | | |
| 3 | 92 | | | | 100 | | | |
| 4 | 118 | | 10 | 10 | 10 | 110 | | | |
| 5 | 109 | | 8 | 8 | 8 | 8 | | 108 |
| 6 | 112 | | 9 | 9 | 9 | 9 | 9 | 109 |

The bonds are treasury securities, which can be viewed as nominally riskless.

- 1. For what maturities is it possible to infer discount factors?
- 2. Determine the implicit discount factors in the market.
- 3. What is the interest rates implied in this set of discount rates?

Here we can find the discount factors for maturities of 0.5,1,1.5,2,3 and 4.
