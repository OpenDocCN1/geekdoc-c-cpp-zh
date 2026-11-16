# 12.2.1 European Options

For European options, binomial trees are not that much used, since the Black Scholes model will give the correct answer, but it is useful to see the construction of the binomial tree without the checks for early exercise, which is the American case.

The computer algorithm for a binomial in the following merits some comments. There is only one vector of call prices, and one may think one needs two, one at time \( t \) and another at time \( t+1 \). (Try to write down the way you would solve it before looking at the algorithm below.) But by using the fact that the branches reconnect, it is possible to get away with the algorithm below, using one less array. You may want to check how this works. It is also a useful way to make sure one understands binomial option pricing.

```
#include <cmath> // standard mathematical library
#include <algorithm> // defining the max() operator
#include <vector> // STL vector templates
using namespace std;

double option_price_call_european_binomial(const double& S, // spot price
const double& K, // exercise price
const double& r, // interest rate
const double& sigma, // volatility
const double& time, // time to maturity
const int& no_steps) // no steps in binomial tree
{
double R=exp(*(r/no_steps)); // interest rate for each step
double Rinv = 1.0/R; // inverse of interest rate
double u = exp(sigma*sqrt(time/no_steps)); // up movement
double uu = u*u;
double d = 1.0/u;
double p_up = (R-d)/(u-d);
double p_down = 1.0-p_up;
vector<double> prices(no_steps+1); // price of underlying
vector<double> call_values(no_steps+1); // fill in the endnodes.
prices[0] = S*pow(u,double(no_steps)); // S*u^n
for (int i=1; i<=no_steps; ++i) prices[i] = uu*prices[i-1];
vector<double> call_values(no_steps+1); // value of corresponding call
for (int i=0; i<=no_steps; ++i) call_values[i] = max(0.0, (prices[i]-K)); // call payoffs at maturity
for (int step=no_steps-1; step>=0; --step) {
for (int i=0; i<=step; ++i) {
call_values[i] = (p_up*call_values[i+1]+p_down*call_values[i])*Rinv;
}
};
return call_values[0];
};
```

C++ Code 12.1: Option price for binomial european

# 12.2.2 American Options

An American option differs from an European option by the exercise possibility. An American option can be exercised at any time up to the maturity date, unlike the European option, which can only be exercised at maturity. In general, there is unfortunately no analytical solution to the American option problem, but in some cases it can be found. For example, for an American call option on non-dividend paying stock, the American price is the same as the European call.

It is in the case of American options, allowing for the possibility of early exercise, that binomial approximations are useful. At each node we calculate the value of the option as a function of the next periods prices, and then check for the value exercising of exercising the option now

C++ Code 12.2 illustrates the calculation of the price of an American call.