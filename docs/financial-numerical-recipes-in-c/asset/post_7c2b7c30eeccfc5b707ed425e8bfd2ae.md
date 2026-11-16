
## Example

Price a perpetual call, given the following information \( S = 50.0, K = 40.0, r = 0.05, q = 0.02, \sigma = 0.05 \)

```
C++ program:

double S=50.0; double K=40.0;
double r=0.05; double q=0.02;
double sigma=0.05;
double price = option_price_american_perpetual_call(S,K,r,q,sigma);
cout << " perpetual call price = " << price << endl;

Output from C++ program:

perpetual call price = 19.4767
```

## Exercise 11.5.

The price for a perpetual american put is

\( P^p = \frac{K}{1-h_2} \left( \frac{h_2-1}{h_2} \frac{S}{K} \right)^{h_2} \)

where

\( h_2 = \frac{1}{2} - \frac{r-q}{\sigma^2} - \sqrt{ \left( \frac{r-q}{\sigma^2} - \frac{1}{2} \right)^2 + \frac{2r}{\sigma^2} } \)

- 1. Implement the calculation of this formula.

## 11.6 Readings

Hull (2011) and McDonald (2013) are general references. A first formulation of an analytical call price with dividends was in Roll (1977b). This had some errors, that were partially corrected in Geske (1979), before Whaley (1981) gave a final, correct formula. See Hull (2011) for a textbook summary. Black (1976) is the original development of the futures option. The original formulations of European foreign currency option prices are in Garman and Kohlhagen (1983) and Grabbe (1983). The price of a perpetual put was first shown in Merton (1973). For a perpetual call see McDonald and Siegel (1986). The notation for perpetual puts and calls follows the summary in (McDonald, 2013, pg. 393).

## Chapter 12

## Option pricing with binomial approximations

## Contents

- 12.1 Introduction ........................ 112
- 12.2 Pricing of options in the Black Scholes setting .................... 113
- 12.2.1 European Options .................... 114
- 12.2.2 American Options .................... 114
- 12.2.3 Matlab implementation ............... 116
- 12.3 How good is the binomial approximation? ............ 119
- 12.3.1 Estimating partials. ................ 120
- 12.4 Adjusting for payouts for the underlying ............ 123
- 12.5 Pricing options on stocks paying dividends using a binomial approximation ............ 124
- 12.5.1 Checking for early exercise in the binomial model. ............ 124
- 12.5.2 Proportional dividends. ............. 124
- 12.5.3 Discrete dividends .................. 126
- 12.6 Option on futures ..................... 128
- 12.7 Foreign Currency options .............. 130
- 12.8 References ............................ 131

## 12.1 Introduction

We have shown binomial calculations given an up and down movement in chapter 8. However, binomial option pricing can also be viewed as an *approximation* to a continuous time distribution by judicious choice of the constants u and d. To do so one has to ask: Is it possible to find a parametrization (choice of u and d) of a binomial process

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_113_0.png)

which has the same time series properties as a (continuous time) process with the same mean and volatility? There is actually any number of ways of constructing this, hence one uses one degree of freedom on imposing that the nodes *reconnect*, by imposing \(u = \frac{1}{d}\).

(To value an option using this approach, we specify the number \(n\) of periods to split the time to maturity \((T - t)\) into, and then calculate the option using a binomial tree with that number of steps.

Given \(S, X, r, \sigma, T\) and the number of periods \(n\), calculate

```
\(\Delta t = \frac{T - t}{n}\)
\(u = e^{\sigma \sqrt{\Delta t}}\)
\(d = e^{-\sigma \sqrt{\Delta t}}\)
```

We also redefine the “risk neutral probabilities”

```
\(R = e^{r \Delta t}\)
\(q = \frac{R - d}{u - d}\)
```

To find the option price, will “roll backwards.” At node \(t\), calculate the call price as a function of the two possible outcomes at time \(t + 1\). For example, if there is one step,

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_113_1.png)

find the call price at time 0 as

```
\(C_0 = e^{-r\tau}(qC_u + (1 - q)C_d)\)
```

With more periods one will “roll backwards” as discussed in chapter 8

## 12.2 Pricing of options in the Black Scholes setting

Consider options on underlying securities not paying dividend.

### 12.2.1 European Options

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
double R=exp(r/no_steps); // interest rate for each step
double Rinv = 1.0/R; // inverse of interest rate
double u = exp(sigma*sqrt(time/no_steps)); // up movement
double uu = u*u;
double d = 1.0/u;
double p_up = (R-d)/(u-d);
double p_down = 1.0-p_up;
vector<double> prices(no_steps+1); // price of underlying
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

### 12.2.2 American Options

An American option differs from an European option by the exercise possibility. An American option can be exercised at any time up to the maturity date, unlike the European option, which can only be exercised at maturity. In general, there is unfortunately no analytical solution to the American option problem, but in some cases it can be found. For example, for an American call option on non-dividend paying stock, the American price is the same as the European call.

It is in the case of American options, allowing for the possibility of early exercise, that binomial approximations are useful. At each node we calculate the value of the option as a function of the next periods prices, and then check for the value exercising of exercising the option now

C++ Code 12.2 illustrates the calculation of the price of an American call.

```
#include <cmath>
#include <vector>
using namespace std;

double option_price_call_american_binomial( const double& S,
    const double& K,
    const double& r,
    const double& sigma,
    const double& t,
    const int& steps) {
    double R = exp(r*(t/steps));
    double Rinv = 1.0/R;
    double u = exp(sigma*sqrt(t/steps));
    double d = 1.0/u;
    double p_up = (R-d)/(u-d);
    double p_down = 1.0-p_up;

    vector<double> prices(steps+1); // price of underlying
    prices[0] = S*pow(d, steps); // fill in the endnodes.
    double uu = u*u;
    for (int i=1; i<=steps; ++i) prices[i] = uu*prices[i-1];

    vector<double> call_values(steps+1); // value of corresponding call
    for (int i=0; i<=steps; ++i) call_values[i] = max(0.0, (prices[i]-K)); // call payoffs at maturity

    for (int step=steps-1; step>=0; --step) {
        for (int i=0; i<=step; ++i) {
            call_values[i] = (p_up*call_values[i+1]+p_down*call_values[i])*Rinv;
            prices[i] = d*prices[i+1];
            call_values[i] = max(call_values[i],prices[i]-K); // check for exercise
        }
    }
    return call_values[0];
};
```

C++ Code 12.2: Price of American call option using a binomial approximation

Actually, for this particular case, the american price will equal the european.
