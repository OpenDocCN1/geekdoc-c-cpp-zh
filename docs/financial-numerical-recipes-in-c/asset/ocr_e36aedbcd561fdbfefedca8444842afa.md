The modified duration measures the angle of the tangent at the current bond yield. Approximating the change in bond price with duration is thus only a first order approximation. To improve on this approximation we also need to account for the curvature in the relationship between bond price and interest rate. To quantify this curvature we calculate the *convexity* of a bond.

Convexity = \(Cx = \frac{1}{B_0} \frac{1}{(1+r)^2} \sum_{t=1}^T (t+t^2) \frac{C_t}{(1+r)^t}\) (4.6)

This calculation is implemented in C++ Code 4.6. To improve on the estimate of how the bond price

```
#include <cmath>
#include "fin_recipes.h."

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

C++ Code 4.6: Bond convexity with a flat term structure and annual compounding

change when the interest rates changes you will then calculate

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

Formula 4.1: Bond pricing formulas with a flat term structure and discrete, annual compounding