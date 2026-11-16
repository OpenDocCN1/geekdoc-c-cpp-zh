The general code in C++ for calculating the bond price with discrete annual compounding is shown in C++ Code 4.1.

```
#include <cmath>
#include <vector>
using namespace std;
double bonds_price_discrete(const vector<double>& times,
                             const vector<double>& cashflows,
                             const double& r) {
    double p=0;
    for (int i=0;i<times.size();++i) {
        p += cashflows[i]/(pow((1+r),times[i]));
    }
    return p;
}
```

C++ Code 4.1: Bond price calculation with discrete, annual compounding.

# 4.1.2 Yield to maturity

Since bonds are issued in terms of interest rate, it is also useful to find an interest rate number that summarizes the terms of the bond. The obvious way of doing that is asking the question: What is the internal rate of return on the investment of buying the bond now and keeping the bond to maturity? The answer to that question is the yield to maturity of a bond. The yield to maturity is the interest rate that makes the present value of the future coupon payments equal to the current bond price, that is, for a known price \( B_0 \), the yield is the solution \( y \) to the equation

\( B_0 = \sum_{t=1}^T \frac{C_t}{(1+y)^t} \) (4.2)

This calculation therefore has the same qualifications as discussed earlier calculating IRR, it supposes reinvestment of coupon at the bond yield (the IRR).

There is much less likelihood we'll have technical problems with multiple solutions when doing this yield estimation for bonds, since the structure of cash flows is such that there exist only one solution to the equation. The algorithm for finding a bonds yield to maturity shown in C++ Code 4.2 is thus simple bisection. We know that the bond yield is above zero and set zero as a lower bound on the bond yield. We then find an upper bound on the yield by increasing the interest rate until the bond price with this interest rate is negative. We then bisect the interval between the upper and lower untill we are “close enough.” C++ Code 4.2 implements this idea.