# 12.7 Foreign Currency options

For American options, the usual method is approximation using binomial trees, checking for early exercise due to the interest rate differential.

```
#include <cmath>
#include <algorithm>
#include <vector>
using namespace std;
double currency_option_price_call_american_binomial(const double& S,
        const double& K,
        const double& r,
        const double& r_f,
        const double& sigma,
        const double& time,
        const int& no_steps) {
    vector<double> exchange_rates(no_steps+1);
    vector<double> call_values(no_steps+1);
    double t_delta = time/no_steps;
    double Rinv = exp(-r*t_delta);
    double u = exp(sigma*sqrt(t_delta));
    double d = 1.0/u;
    double pUp = (exp((r-r_f)*t_delta)-d)/(u-d); // adjust for foreign int.rate
    double pDown = 1.0 - pUp;
    exchange_rates[0] = S*pow(d, no_steps);
    for (i=1; i<=no_steps; ++i) {
        exchange_rates[i] = u*exchange_rates[i-1]; // terminal tree nodes
    }
    for (i=0; i<=no_steps; ++i) call_values[i] = max(0.0, (exchange_rates[i]-K));
    for (int step=no_steps-1; step>=0; --step) {
        for (i=0; i<=step; ++i) {
            exchange_rates[i] = d*exchange_rates[i+1];
            call_values[i] = (pDown*call_values[i]+pUp*call_values[i+1])*Rinv;
            call_values[i] = max(call_values[i], exchange_rates[i]-K); // check for exercise
        }
    }
    return call_values[0];
}
```

C++ Code 12.9: Pricing an american call on an option on currency using a binomial approximation

# Example

Price a futures currency option with the following information: S = 50, K = 52, r = 0.08, rf = 0.05, sigma = 0.2, time=0.5, number of steps = 100.

```
C++ program:
double S = 50.0; double K = 52.0;
double r = 0.08; double rf=0.05;
double sigma = 0.2; double time=0.5;
int no_steps = 100;
cout << " european currency option call = "
     << currency_option_price_call_american_binomial(S,K,r,rf,sigma,time,no_steps) << endl;
```

Output from C++ program:

european currency option call = 2.23129