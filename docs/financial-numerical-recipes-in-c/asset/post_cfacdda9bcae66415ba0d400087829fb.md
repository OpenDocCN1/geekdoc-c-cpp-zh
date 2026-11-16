
## 5.4 Bond calculations with a general term structure and continuous compounding

Coupon bond paying coupons at times \(t_1, t_2, \dots\):
Bond Price \(B_0\):
\(B_0 = \sum_i d_i C_{t_i} = \sum_i e^{-r_{t_i} t_i} C_{t_i}\)
Duration \(D\):
\(D = \frac{1}{B_0} \sum_i t_i d_i C_{t_i}\)
\(D = \frac{1}{B_0} \sum_i t_i e^{-r_{t_i} t_i} C_{t_i}\)
\(D = \frac{1}{B_0} \sum_i t_i e^{-y t_i} C_{t_i}\)

Yield to maturity \(y\) solves:
\(B_0 = \sum_i C_{t_i} e^{-y t_i}\)
Convexity \(Cx\):
\(Cx = \frac{1}{B_0} \sum_i t_i^2 d_i C_{t_i}\)
\(Cx = \frac{1}{B_0} \sum_i t_i^2 e^{-r_{t_i} t_i} C_{t_i}\)
\(Cx = \frac{1}{B_0} \sum_i t_i^2 e^{-y t_i} C_{t_i}\)

### Formula 5.1: Bond pricing with a continuously compounded term structure

C++ Code 5.6 and C++ Code 5.7 illustrate how one would calculate bond prices and duration if one has a term structure class.

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

### C++ Code 5.6: Pricing a bond with a term structure class

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

### C++ Code 5.7: Calculating a bond's duration with a term structure class

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

### C++ Code 5.8: Calculating a bond's convexity with a term structure class

### Example

The term structure is flat with r = 10% continuously compounded interest. Calculate price, duration, and convexity of a 10%, 2 year bond.

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

References Shiller (1990) is a good reference on the use of the term structure.

## Chapter 6

## The Mean Variance Frontier

## Contents

- 6.1 Setup .................................................... 67
- 6.2 The minimum variance frontier ........................ 69
- 6.3 Calculation of frontier portfolios ................... 69
- 6.4 The global minimum variance portfolio ................ 72
- 6.5 Efficient portfolios ................................... 72
- 6.6 The zero beta portfolio ................................ 73
- 6.7 Allowing for a riskless asset .......................... 73
- 6.8 Efficient sets with risk free assets ................... 74
- 6.9 Short-sale constraints ................................. 75
- 6.10 The Sharpe Ratio ...................................... 75
- 6.11 Equilibrium: CAPM ..................................... 76
  - 6.11.1 Treynor ........................................... 76
  - 6.11.2 Jensen ............................................ 76
- 6.12 Working with Mean Variance and CAPM ................. 76
- 6.13 Mean variance analysis using matrix libraries ....... 77

We now discuss a classical topic in finance, mean variance analysis. This leads to ways of accounting for the riskiness of cashflows.

Mean variance analysis concerns investors choices between portfolios of risky assets, and how an investor chooses portfolio weights. Let r_p be a portfolio return. We assume that investors preferences over portfolios p satisfy a mean variance utility representation, u(p) = u(E[r_p], \sigma(r_p)), with utility increasing in expected return (\partial u / \partial E[r_p] > 0) and decreasing in variance (\partial u / \partial \text{var}(r_p) < 0). In this part we consider the representation of the portfolio opportunity set of such decision makers. There are a number of useful properties of this opportunity set which follows purely from the mathematical formulation of the optimization problem. It is these properties we focus on here.

## 6.1 Setup

We assume there exists n \ge 2 risky securities, with expected returns e

\[
e = \begin{bmatrix} E[r_1] \\ E[r_2] \\ \vdots \\ E[r_n] \end{bmatrix}
\]

and covariance matrix V:

\[
\mathbf{V} = \begin{bmatrix} \sigma(r_1, r_1) & \sigma(r_1, r_2) & \dots \\ \sigma(r_2, r_1) & \sigma(r_2, r_2) & \dots \\ \vdots & & \\ \sigma(r_n, r_1) & & \dots & \sigma(r_n, r_n) \end{bmatrix}
\]

The covariance matrix V is assumed to be invertible.

A portfolio \(\rho\) is defined by a set of weights w invested in the risky assets.

\[
\mathbf{w} = \begin{bmatrix} \omega_1 \\ \omega_2 \\ \vdots \\ \omega_n \end{bmatrix}
\]

where \(w_i\) is the fraction of the investors wealth invested in asset \(i\). Note that the weights sum to one.

The expected return on a portfolio is calculated as

\(E[r_p] = \mathbf{w}'\mathbf{e}\)

and the variance of the portfolio is

\(\sigma^2(r_p) = \mathbf{w}'\mathbf{Vw}\)

### Example

| t | Asset | E[r] | \(\sigma^2(r)\) |
|---|---|---|---|
| 1 | | 10% | 0.20 |
| 2 | | 11.5% | 0.10 |
| 3 | | 8% | 0.15 |

The three assets are independent (uncorrelated).

- 1. Determine the expected return and standard deviation of an equally weighted portfolio of the three assets

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

## 6.2 The minimum variance frontier

A portfolio is a *frontier* portfolio if it minimizes the variance for a given expected return, that is, a frontier portfolio $p$ solves

$$
\mathbf{w}_p = \arg \min_{\mathbf{w}} \frac{1}{2} \mathbf{w}' \mathbf{V} \mathbf{w}
$$

subject to:

$$
\mathbf{w}' \mathbf{e} = E[\bar{r}_p]
$$

$$
\mathbf{w}' \mathbf{1} = 1
$$

The set of all frontier portfolios is called the *minimum variance frontier*.

## 6.3 Calculation of frontier portfolios

**Proposition 1** If the matrix $\mathbf{V}$ is full rank, and there are no restrictions on short sales, the weights $\mathbf{w}_p$ for a frontier portfolio $p$ with mean $E[\bar{r}_p]$ can be found as

$$
\mathbf{w}_p = \mathbf{g} + \mathbf{h} E[\bar{r}_p]
$$

where

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

**Proof**

Any minimum variance portfolio solves the program

$$
\mathbf{w}_p = \arg \min_{\mathbf{w}} \frac{1}{2} \mathbf{w}' \mathbf{V} \mathbf{w}
$$

subject to

$$
\mathbf{w}' \mathbf{e} = E[\bar{r}_p]
$$

$$
\mathbf{w}' \mathbf{1} = 1
$$

Set up the Lagrangian corresponding to this problem

$$
L(\mathbf{w}, \lambda, \gamma | \mathbf{e}, \mathbf{V}) = \frac{1}{2} \mathbf{w}' \mathbf{V} \mathbf{w} - \lambda \left( E[\bar{r}_p] - \mathbf{w}' \mathbf{e} \right) - \gamma (1 - \mathbf{w}' \mathbf{1})
$$
