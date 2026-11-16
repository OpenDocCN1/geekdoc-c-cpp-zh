
```cpp
#include "fin_recipes.h"

term_structure_class_vasicek::term_structure_class_vasicek(const double& r, const double& a,
const double& b, const double& sigma) {
 r = r; a = a; b = b; sigma = sigma;
};

double term_structure_class_vasicek::d(const double& T) const{
 return term_structure::discount_factor_vasicek(T,r,a,b,sigma);
};
```

### C++ Code 22.10: Class definition, Vasicek (1977) model

Example Parameters r = 0.05, a = -0.1, b = 0.1, \sigma = 0.1 Use the Vasicek term structure model. Find short rate and discount factor for t = 1, and forward rate between years 1 and 2.

C++ program:

```cpp
cout << "Example term structure calculation using the Vasicek term structure model"
<< endl;
double r=0.05; double a=-0.1; double b=0.1; double sigma=0.1;
cout << " direct calculation, discount factor (t=1): "
<< term_structure::discount_factor(1, r, a, b, sigma) << endl;
term_structure_class_vasicek vc(r,a,b,sigma);
cout << " using a term structure class " << endl;
cout << " yield (r) = " << vc.r(1) << endl;
cout << " discount factor (t=1) = " << vc.d(1) << endl;
cout << " forward rate (t1=1, t2=2 ) = " << vc.f(1,2) << endl;
```

Output from C++ program:

Example term structure calculation using the Vasicek term structure model
direct calculation, discount factor (t=1): 0.955408
using a term structure class
yield (t=1) = 0.0456168
discount factor (t=1) = 0.955408
forward rate (t1=1, t2=2) = 0.0281476

## 22.6 Readings

The methods in this chapter I first studied in my dissertation at Carnegie Mellon University in 1992, which lead to the paper published as Green and Ødegaard (1997). A textbook treatment of estimation and fitting of term structure models can be found in (Martinelli, Priaulet, and Priaulet, 2003, Ch 4)

## Chapter 23

### Binomial Term Structure models

### Contents

| Section | Page |
|---|---|
| 23.1 The Rendleman and Bartter model | 211 |
| 23.2 Readings | 213 |

Pricing bond options with the Black Scholes model, or its binomial approximation, as done in chapter 20, does not always get it right. For example, it ignores the fact that at the maturity of the bond, the bond volatility is zero. The bond volatility decreases as one gets closer to the bond maturity. This behaviour is not captured by the assumptions underlying the Black Scholes assumption. We therefore look at more complicated term structure models, the unifying theme of which is that they are built by building trees of the interest rate.

## 23.1 The Rendleman and Bartter model

The Rendleman and Bartter approach to valuation of interest rate contingent claims (see Rendleman and Bartter (1979) and Rendleman and Bartter (1980)) is a particular simple one. Essentially, it is to apply the same binomial approach that is used to approximate options in the Black Scholes world, but the random variable is now the interest rate. This has implications for multiperiod discounting: Taking the present value is now a matter of choosing the correct sequence of spot rates, and it may be necessary to keep track of the whole "tree" of interest rates. Such a tree can then be used to price various fixed income securities. In the next chapter we illustrate this more generally, here we show a direct implementation of the original model. C++ Code 23.1 implements the original algorithm for a call option on a (long maturity) zero coupon bond.

```cpp
#include <cmath>
#include <algorithm>
#include <vector>
using namespace std;

double bond_option_price_call_zero_american_rendleman_bartter(const double& X,
                                     const double& option_maturity,
                                     const double& S,
                                     const double& M, // term structure parameters
                                     const double& interest, // current short interest rate
                                     const double& sigma, // volatility
                                     const double& maturity_payment, // time to maturity for underlying
                                     const int& no_steps) {
    double delta_t = maturity_payment/no_steps;
    double u=exp(S*sqrt(delta_t));
    double d=1/u;
    double p_up = (exp(M*delta_t)-d)/(u-d);
    double p_down = 1.0-p_up;

    vector<double> r(no_steps+1);
    r[0]=interest*pow(d,no_steps);
    double uu=u*u;
    for (int i=1;i<=no_steps;++i) { r[i]=r[i-1]*uu; }
    vector<double> P(no_steps+1);
    for (int i=0;i<=no_steps;++i) { P[i] = maturity_payment; };
    for (int curr_step=no_steps-1;curr_step>=0;--curr_step) {
        for (int i=0;i<=curr_step;++i) {
            P[i] = exp(-r[i]*delta_t)*(p_down*P[i]+p_up*P[i+1]);
        }
    }
    vector<double> C(no_steps+1);
    for (int i=0;i<=no_steps;++i) { C[i]=max(0.0,P[i]-X); };
    for (int curr_step=no_steps-1;curr_step>=0;--curr_step) {
        for (int i=0;i<=curr_step;++i) {
            P[i] = exp(-r[i]*delta_t)*(p_down*P[i]+p_up*P[i+1]);
            C[i]=max(P[i]-X, exp(-r[i]*delta_t)*(p_up*C[i+1]+p_down*C[i]));
        }
    }
    return C[0];
}
```

### C++ Code 23.1: RB binomial model for European call on zero coupon bond

Example Parameters: K = 950, S = 0.15 and M = 0.05 The interest rate is 10%, The option matures in 4 years, the bond matures in year 5, with a bond maturity payment of 1000. Price the option on the zero coupon bond using a Rendleman-Bartter approximation with 100 steps.

C++ program:

```cpp
double K=950; double S=0.15; double M=0.05; double interest=0.10;
double option_maturity=4; double bond_maturity=5; double bond_maturity_payment=1000;
int no_steps=100;
cout << " Rendleman Bartter price of option on zero coupon bond : ";
cout << bond_option_price_call_zero_american_rendleman_bartter( K, option_maturity, S, M,
interest, bond_maturity,
bond_maturity_payment, no_steps);
```

Output from C++ program:

Rendleman Bartter price of option on zero coupon bond: 0.00713661

## 23.2 Readings

General references include Sundaresan (2001).

Rendleman and Bartter (1979) and Rendleman and Bartter (1980) are the original references for building standard binomial interest rate trees.

## Chapter 24

### Interest rate trees

### Contents

- 24.1 The movement of interest rates . . . . . . . . . . . . . . . . 214
- 24.2 Discount factors . . . . . . . . . . . . . . . . . . . . . . . . 216
- 24.3 Pricing bonds . . . . . . . . . . . . . . . . . . . . . . . . . 216
- 24.4 Callable bond . . . . . . . . . . . . . . . . . . . . . . . . . 218
- 24.5 Readings . . . . . . . . . . . . . . . . . . . . . . . . . . . 220

In this chapter we show a way of building interest rate trees and apply it to the pricing of various fixed income securities. The first need in such a procedure is to specify the future evolution of interest rates.

## 24.1 The movement of interest rates

We will assume that interest rates follow a Geometric Brownian Motion process

```
dr = μrdt + σrdZ
```

This is the same assumption which was used for stock prices in the Black Scholes case. This leads to the same binomial approximation, for one period:

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_214_0.png)

or several periods:

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_215_0.png)

When using this approach it turns out to be useful to keep the whole tree around, we therefore separate the building of the tree in one routine, as shown in C++ Code 24.1.

```cpp
#include <vector>
#include <cmath>
using namespace std;

vector< vector< double > > interest_rate_trees_gbm::build(const double& r0,
                                     const double& u,
                                     const double& d,
                                     const int& n){
vector< vector< double > > tree;
vector< double > r(1); r[0]=r0;
tree.push_back(r);
for (int i=1;i<n+1;++i) {
  vector< double > tmp(i*2+1);
  for (int j=0;j<i+1;++j){
    r[j] = d*r[j];
  }
  r.push_back(r.back());
  tree.push_back(r);
}
return tree;
};
```

### C++ Code 24.1: Building interest rate tree

```matlab
function tree = interest_rate_trees_gbm_build(r0,u,d,n)
r = r0;
tree = r;
rtop = r0;
for i = 1:n
  rtop = u * rtop;
  r = [rtop; r * rtop];
  tree = [zeros(i,1), tree, r];
endfor
endfunction
```

### Matlab Code 24.1: Building interest rate tree

### Example

Parameters: $r_0 = 10\%, u = 1.02, d = 0.99$. Build a 2 period interest rate tree.
