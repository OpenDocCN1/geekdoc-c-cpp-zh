

```cpp
#include "fin_recipes.h"
double bonds_duration_macaulay_discrete(const vector<double>& times,
                                       const vector<double>& cashflows,
                                       const double& bond_price){
    double y = bonds_yield_to_maturity_discrete(times, cashflows, bond_price);
    return bonds_duration_discrete(times, cashflows, y); // use YTM in duration calculation
};
```

### C++ Code 4.4: Calculating the Macaulay duration of a bond

- 1. Determine the current bond price.
- 2. Calculate the duration using the current interest rate.
- 3. Calculate the duration using the Macaulay definition.

Need to calculate the following:

The current bond price: \( B_0 = \frac{10}{(1+0.09)^1} + \frac{10}{(1+0.09)^2} + \frac{110}{(1+0.09)^3} = 102.531 \).

The bond's duration: \( D = \frac{102.531}{\frac{10}{1.09} + \frac{10}{1.09^2} + \frac{110}{1.09^3}} = 2.74 \).

```
Matlab program:
C = [10,10,110];
t = 1:3;
r = 0.09;
B = C' * (1./((1+r).^t));
D = (1/B)'*C .* (1./(1+r).^t)'
y = irr([-B C])
DM=(1/y)'.*C .* (1./(1+y).^t)'
```

```
Output from Matlab program:
B = 102.53
D = 2.7390
y = 0.090000
DM = 2.7390
```

```
C++ program:
vector<double> cflows; cflows.push_back(10); cflows.push_back(10); cflows.push_back(110);
vector<double> times; times.push_back(1); times.push_back(2); times.push_back(3);
double r=0.09;
double B = bonds_price_discrete(times, cflows, r);
cout << " bonds price = " << B << endl;
cout << " bond duration = " << bonds_duration_discrete(times, cflows, r) << endl;
cout << " bond macaulay = " << bonds_duration_macaulay_discrete(times, cflows, B) << endl;
```

```
Output from C++ program:
bonds price = 102.531
bond duration = 2.73895
bond macaulay = 2.73895
```

## 4.1.4 Measuring bond sensitivity to interest rate changes

Now, the reason for why we say that we can measure the sensitivity of a bond price using duration. To a first approximation, \(\Delta B_0\), the change in the bond price for a small change in the interest rate \(\Delta r\), can be calculated

\(\frac{\Delta B_0}{B_0} \approx -\frac{D}{1+r} \Delta r\)

where \(D\) is the bond's duration. For simplicity one often calculates the term in front of the \(\Delta y\) in the above, \(\frac{D}{1+y}\) directly and terms it the bond's *modified duration*.

\(\text{Modified Duration} = D^* = \frac{D}{1+r}\)

The sensitivity calculation is then

\(\frac{\Delta B_0}{B_0} \approx -D^* \Delta r\)

The modified duration is also written in terms of the bond's yield to maturity \(y\), and is then

\(D^* = \frac{D}{1+y}\)

C++ Code 4.5 shows this calculation.

```
#include <vector>
using namespace std;
#include "fin_recipes.h"

double bonds_duration_modified_discrete (const vector<double>& times,
                                         const vector<double>& cashflows,
                                         const double& bond_price){
    double y = bonds_yield_to_maturity_discrete(times, cashflows, bond_price);
    double D = bonds_duration_discrete(times, cashflows, y);
    return D/(1+y);
};
```

### C++ Code 4.5: Modified duration

Approximating bond price changes using duration is illustrated in the following figure.

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_43_0.png)

The modified duration measures the angle of the tangent at the current bond yield. Approximating the change in bond price with duration is thus only a first order approximation. To improve on this approximation we also need to account for the curvature in the relationship between bond price and interest rate. To quantify this curvature we calculate the *convexity* of a bond.

Convexity = \(Cx = \frac{1}{B_0} \frac{1}{(1+r)^2} \sum_{t=1}^T (t+t^2) \frac{C_t}{(1+r)^t}\) (4.6)

This calculation is implemented in C++ Code 4.6. To improve on the estimate of how the bond price

```
#include <cmath>
#include "fin_recipes.h"

double bonds_convexity_discrete(const vector<double>& times,
                                const vector<double>& cashflows,
                                const double& r ){
    double Cx=0;
    for (int i=0;i<times.size();i++){
        Cx+= cashflows[i]*times[i]*(times[i]+1)/(pow((1+r),times[i]));
    };
    double B=bonds_price_discrete(times, cashflows, r);
    return (Cx/(pow((1+r),2)))/B;
};
```

### C++ Code 4.6: Bond convexity with a flat term structure and annual compounding

change when the interest rate changes you will then calculate

\(\frac{\Delta B_0}{B_0} \approx -D^* \Delta y + \frac{1}{2} C_x (\Delta y)^2\)

Formula 4.1 summarizes the above calculations.

| Bond Price (\(B_0\)) | Modified duration |
|---|---|
| \(B_0 = \sum_{t=1}^T \frac{C_t}{(1+r)^t}\) | \(D^* = \frac{D}{1+y}\) |
| Yield to maturity \(y\) solves | Convexity (\(Cx\)) |
| \(B_0 = \sum_{t=1}^T \frac{C_t}{(1+y)^t}\) | \(Cx = \frac{1}{B_0} \frac{1}{(1+r)^2} \sum_{t=1}^T (t+t^2) \frac{C_t}{(1+r)^t}\) |
| Duration (\(D\)) | Approximating bond price changes |
| \(D = \frac{1}{B_0} \sum_{t=1}^T \frac{t C_t}{(1+r)^t}\) | \(\frac{\Delta B_0}{B_0} \approx -D^* \Delta y\) |
| Macaulay duration | \(\frac{\Delta B_0}{B_0} \approx -D^* \Delta y + \frac{1}{2} \times Cx \times (\Delta y)^2\) |
| \(D = \frac{1}{B_0} \sum_{t=1}^T \frac{t C_t}{(1+y)^t}\) | |

\(C_t\): Cash flow at time \(t\). \(r\): Interest rate, \(y\): bond yield to maturity, \(B_0\): current bond price. Bond pays coupon at evenly spaced dates \(t = 1, 2, 3, \dots, T\).

### Formula 4.1: Bond pricing formulas with a flat term structure and discrete, annual compounding

## Example

- 1. Determine the current bond price.
- 2. Suppose the interest rate changes to 10%, determine the new price of the bond by direct calculation.
- 3. Use duration to estimate the new price and compare it to the correct price.
- 4. Use convexity to improve on the estimate using duration only.

Need to calculate the following:

The current bond price: \( B_0 = \frac{10}{(1+0.09)^1} + \frac{10}{(1+0.09)^2} + \frac{110}{(1+0.09)^3} = 102.531 \).
The bond's duration: \( D = \frac{10 \times 1}{102.531} \frac{1}{(1.09)} + \frac{2 \times 10}{102.531} \frac{1}{(1.09)^2} + \frac{3 \times 110}{102.531} \frac{1}{(1.09)^3} = 2.74 \)
The modified duration: \( D^{mod} = \frac{D}{1+r} = \frac{2.74}{1.09} = 2.51 \).
The convexity: \( Cx = \frac{1}{(1+0.09)^2} \frac{10 \times 1 \times 2}{102.531} (\frac{1+1 \times 10}{1.09} + \frac{2^2+2 \times 10}{1.09^2} + \frac{(3+3)^2 \times 110}{1.09^3}) = 8.93 \).

Here are the calculations:

```
Matlab program:
C = [10,10,110];
t = 1:3;
r = 0.09;
B = C * (1./(1+r).^(-t));
De = (1/B)'* C .* (1./(1+t).^-2.*C .* (1./(1+r).^-t)');
Cx = (1/(1+t+2)) * (1/(B).^t).*2.*C .* (1./(1+r).^-t)';
newB=C* (1./(1+0.1).^-t);
```

Output from Matlab program:
B = 102.53
D = 2.7390
Cx = 6.6272
newB = 100.000

```
C++ program:
vector<double> cflows; cflows.push_back(10); cflows.push_back(10); cflows.push_back(110);
vector<double> times; times.push_back(1); times.push_back(2); times.push_back(3);
double r=0.09;
double B = bonds_price_discrete(times, cflows, r);
cout << " bond price = " << B << endl;
cout << " bond duration = " << bonds_duration_discrete(times, cflows, r) << endl;
cout << " bond duration modified = " << bonds_duration_modified_discrete(times, cflows, B) << endl;
cout << " bond convexity = " << bonds_convexity_discrete(times, cflows, r) << endl;
cout << " new bond price = " << bonds_price_discrete(times, cflows, 0.1);
```

Output from C++ program:
bonds price = 102.531
bond duration = 2.73895
bond duration modified = 2.5128
bond convexity = 8.93248
new bond price = 100

Using these numbers to answer the questions, let us see what happens when the interest rate increases to 10%. This means the bond will be selling at par, equal to 100, which can be confirmed with direct computation:

```
\( B_0 = \frac{10}{(1 + 0.1)^1} + \frac{10}{(1 + 0.1)^2} + \frac{110}{(1 + 0.1)^3} = 100 \)
```

Using duration to estimate the change in the bond price for a unit change in the interest rate:

```
\( \frac{\Delta B_0}{B_0} = -D^* \Delta y = -2.51 \cdot 0.01 = -0.0251 \)
```

Using this duration based number to estimate the new bond price.

```
\( \hat{B} = B_0 + \left( \frac{\Delta B_0}{B_0} \right) B_0 = 102.531 - 0.0251 \cdot 102.531 = 99.957 \)
```

Additionally using convexity in estimating the change in the bond price:

```
\( \frac{\Delta B_0}{B_0} = -D^* \Delta y + \frac{1}{2} C \Delta y^2 = -2.51 \cdot 0.01 + \frac{1}{2} 8.93(0.01)^2 = -0.0251 + 0.00044 = -0.02465 \)
```

```
\( \hat{B} = 102.531 \left( 1 + \left( \frac{\Delta B_0}{B_0} \right) \right) = 102.531(1 - 0.02465) = 100.0036 \)
```

## Exercise 4.1.

### Perpetual duration [4]

The term structure is flat with annual compounding. Consider the pricing of a perpetual bond. Let \( C \) be the per period cash flow

```
\( B_0 = \sum_{t=1}^{\infty} \frac{C}{(1 + r)^t} = \frac{C}{r} \)
```

- 1. Determine the first derivative of the price with respect to the interest rate.
- 2. Find the duration of the bond.

## Exercise 4.2.

### [5]

Consider an equally weighted portfolio of two bonds, A and B. Bond A is a zero coupon bond with 1 year to maturity. Bond B is a zero coupon bond with 3 years to maturity. Both bonds have face values of 100. The current interest rate is 5%.

- 1. Determine the bond prices.
- 2. Your portfolio is currently worth 2000. Find the number of each bond invested.
- 3. Determine the duration of the portfolio.
- 4. Determine the convexity of your position.

