
```cpp
C++ program:
cout << "Testing general simulation of European options " << endl;
double S=100; double K=120; double r = 0.10;
time = 1.0; double sigma = 0.25; int no_sims = 10000; int no_steps = 250;
double q=0;
cout << "simulated arithmetic average " << endl;
<< " S= " << S << " r= " << r << " price="
<< derivative_price_simulate_european_option_generic(S,K,r,sigma,time,
payoff_arithmetic_average_call,
no_steps,no_sims)
<< endl;
cout << " simulated geometric average = " << endl;
<< derivative_price_simulate_european_option_generic(S,K,r,sigma,time,
payoff_geometric_average_call,
no_steps,no_sims)
<< endl;
cout << " analytical lookback put = " << endl;
<< option_price_european_lookback_put(S,S,r,q,sigma,time)
<< endl;
cout << " simulated lookback = " << endl;
<< derivative_price_simulate_european_option_generic(S,0,r,sigma,time,
payoff_lookback_put,
no_steps,no_sims)
<< endl;
cout << " analytical lookback call = " << endl;
<< option_price_european_lookback_call(S,S,r,q,sigma,time)
<< endl;
cout << " simulated lookback call = " << endl;
<< derivative_price_simulate_european_option_generic(S,0,r,sigma,time,
payoff_lookback_call,
no_steps,no_sims)
<< endl;
cout << " simulated lookback call using control variates = " << endl;
<< derivative_price_simulate_european_option_generic_with_control_variate(S,0,r,sigma,time,
payoff_lookback_call,
no_steps,no_sims)
<< endl;
```

```
Output from C++ program:
Testing general simulation of European options
simulated arithmetic average S= 100 r= 0.1 price=1.49696
simulated geometric average = 1.38017
analytical lookback put = 16.2665
simulated lookback put = 14.9846
analytical lookback call = 22.8089
simulated lookback call = 21.9336
simulated lookback call using control variates = 22.0685
```

## 16.6 References

Exotic options are covered in Hull (2011). Rubinstein (1993) has an extensive discussion of analytical solutions to various exotic options. Gray and Gray (2001) also looks at some analytical solutions.

# Chapter 17

## Generic binomial pricing

| Item | Page |
|---|---|
| 17.1 Introduction | 177 |
| 17.2 Delta calculation | 182 |

## 17.1 Introduction

In earlier chapters we have seen a large number of different versions of the binomial pricing formula. In this chapter we see how we can build a framework for binomial pricing that lets us write a single generic routine that can be used for a binomial approximation of all sorts of derivatives. The important feature that lets us write such a generic routine is that the only place the terms of the derivative appears in the calculation is the calculation of the value at each node. Consider the binomial approximation of an American call in Chapter 12's C++ Code 12.2, repeated below as C++ Code 17.1 for convenience.

The terms of the derivative only appears when calculating the value at the nodes, where the calculation max(prices[] -K,0) appears. The key to building a generic binomial routine lies in replacing this calculation with a generic routine. C++ Code 17.2 shows how the generic routine is implemented.

```cpp
#include <cmath>
// standard mathematical library
#include <algorithm>
// defines the max() operator
#include <vector>
// STL vector templates
using namespace std;

double option_price_call_american_binomial( const double& S, // spot price
const double& X, // exercise price
const double& r, // interest rate
const double& sigma, // volatility
const double& t, // time to maturity
const int& steps) { // no steps in binomial tree
double R = exp(r*(t/steps)); // interest rate for each step
double Rinv = 1.0/R; // inverse of interest rate
double u = exp(sigma*sqrt(t/steps)); // up movement
double d = 1.0/u;
double p_up = (R-d)/(u-d);
double p_down = 1.0-p_up;

vector<double> prices(steps+1); // price of underlying
prices[0] = S*pow(d,steps); // fill in the endnodes.
double uu = u*u;
for (int i=1; i<=steps; ++i) prices[i] = uu*prices[i-1];

vector<double> call_values(steps+1); // value of corresponding call
for (int i=0; i<=steps; ++i) call_values[i] = max(0.0, (prices[i]-X)); // call payoffs at maturity

for (int step=steps-1; step>=0; --step) {
for (int i=0; i<=step; ++i) {
call_values[i] = (p_up*call_values[i+1]+p_down*call_values[i])*Rinv;
call_values[i] = max(call_values[i],prices[i]-X); // check for exercise
}
}
return call_values[0];
}
```

## C++ Code 17.1: Binomial price of American Call

```cpp
#include <cmath>        // standard mathematical library
#include <algorithm>    // defines the max() operator
#include <vector>       // STL vector templates
using namespace std;

double option_price_generic_binomial( const double& S,
                                      const double& K,
                                      const double& r,
                                      const double& sigma,
                                      const double& t,
                                      const int& steps) {
    // interest rate for each step
    double R = exp(r*(t/steps));
    // inverse of interest rate
    double Rinv = 1.0/R;
    // up movement
    double u = exp(sigma*sqrt(t/steps));
    double d = 1.0/u;
    double p_up = (R-d)/(u-d);
    double p_down = 1.0-p_up;

    vector<double> prices(steps+1); // price of underlying
    prices[0] = S*pow(d, steps); // fill in the endnodes.
    double uu = u*u;
    for (int i=1; i<=steps; ++i) prices[i] = uu*prices[i-1];

    vector<double> values(steps+1); // value of corresponding call
    for (int i=0; i<=steps; ++i) values[i] = generic_payoff(prices[i],K); // payoffs at maturity

    for (int step=steps-1; step>=0; --step) {
        for (int i=0; i<=step; ++i) {
            values[i] = (p_up*values[i+1]+p_down*values[i])*Rinv; // value by not exercising
            prices[i] = d*prices[i+1];
            values[i] = max(values[i],generic_payoff(prices[i],K)); // check for exercise
        }
    }
    return values[0];
};
```

## C++ Code 17.2: Generic binomial calculation

Using this routine is then merely a matter of providing a definition of the derivative payoff. C++ Code 17.3 shows how the payoffs are defined for standard put and call options. Pricing American put and call options is then merely a matter of supplying these payoff definitions to the generic binomial routine.

```cpp
#include <algorithm>
using namespace std;

double payoff_call(const double& S, const double& K){
    return max(0.0,S-K);
};

double payoff_put (const double& S, const double& K) {
    return max(0.0,K-S);
};
```

## C++ Code 17.3: Payoff definitions for put and call options

## Example

Consider American call and put option on non-dividend paying stock, where S = 100, K = 100, sigma = 0.2, (T - t) = 1 and r = 0.1.

- 1. Price the options using binomial approximations with 100 steps.

C++ program:

```cpp
double S = 100.0;
double K = 100.0;
double r = 0.1;
double sigma = 0.25;
double time_to_maturity=1.0;
int steps = 100;

cout << " american call price = "
     << option_price_generic_binomial(S,K,payoff_call, r, sigma, time_to_maturity, steps)
     << endl;
cout << " american put price = "
     << option_price_generic_binomial(S,K,payoff_put, r, sigma, time_to_maturity, steps)
     << endl;
```

----------------------------------------
Output from C++ program:
american call price = 14.9505
american put price = 6.54691

More exotic options can also be calculated using the same approach. For example, C++ Code 17.4 shows payoff definitions for two binary options, options that pay off one dollar if the price of the underlying is above K (call) or below K (put). The typical such option is European, the check for whether the option is in the money happens at maturity, but one can also think of cases where the binary option pays off one dollar as soon as S, the price of the underlying, hits the "barrier" K.

## Example

Consider binary options that pays one dollar if the price S of the underlying increases to K or above during some time period. Suppose the current price of the underlying is S = 100. Using sigma = 0.2, (T - t) = 1 and r = 0.1, price such a binary option when K = 120.
