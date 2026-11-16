# 12.3.1 Estimating partials.

It is always necessary to calculate the partial derivatives as well as the option price. Let us start with Delta, the derivative of the option price with respect to the underlying. The binomial methods gives us ways to approximate these as well. How to find them in the binomial case are described in Hull (2011). The implementation in C++ Code 12.3 is for the non-dividend case.

```
#include <cmath>
#include <algorithm>
#include <vector>
using namespace std;
double option_price_delta_american_call_binomial(const double& S,
    const double& K,
    const double& r,
    const double& sigma,
    const double& t,
    const int& no_steps){ // steps in binomial
double R = exp(t/(*no_steps));
double Rinv = 1.0/R;
double u = exp(sigma*sqrt(t/no_steps));
double d = 1.0/u;
double uu = u*u;
double pUp = (R-d)/(u-d);
double pDown = 1.0 - pUp;
vector<double> prices (no_steps+1);
prices[0] = S*pow(d, no_steps);
for (int i=1; i<=no_steps; ++i) prices[i] = uu*prices[i-1];
vector<double> call_values (no_steps+1);
for (int i=0; i<=no_steps; ++i) call_values[i] = max(0.0, (prices[i]-K));
for (int curr_step=no_steps-1; curr_step>=0; --CurrStep) {
    for (int i=0; i<=CurrStep; ++i) {
        prices[i] = d*prices[i+1];
        call_values[i] = (pDown*call_values[i]+pUp*call_values[i+1])*Rinv;
        call_values[i] = max(call_values[i], prices[i]-K); // check for exercise
    };
};
double delta = (call_values[1]-call_values[0])/(S*u-S*d);
return delta;
};
```

# C++ Code 12.3: Delta

Calculation of all the derivatives are shown in C++ Code 12.4