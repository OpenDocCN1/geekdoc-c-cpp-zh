
```cpp
double payoff::binary::call(const double& S, const double& K){
    if (S>=K) return 1;
    return 0;
}

double payoff::binary::put(const double& S, const double& K){
    if (S<=K) return 1;
    return 0;
}
```

C++ Code 17.4: Payoff definitions for binomial options

```cpp
C++ program:

double S = 100.0;
double K = 120.0;
double r = 0.1;
double sigma = 0.25;
double time_to_maturity=1.0;
int steps = 100;
cout << " binary option price = "
     << option_price_generic::Binomial(S,K,payoff::binary::call, r, sigma, time_to_maturity, steps)
     << endl;
-------------------------------------------
Output from C++ program:

binary option price = 0.498858
```

## 17.2 Delta calculation

Deltas and other greeks are calculated using the same style of generic routine. C++ Code 17.5 shows how to calculate delta using the same generic approach.

```cpp
#include <cmath>
#include <algorithm>
#include <vector>
using namespace std;

double option_price_delta_generic_binomial(const double& S,
                                          const double& K,
                                          double generic_payoff(const double& S, const double& K),
                                          const double& r,
                                          const double& sigma,
                                         const double& t,
                                         const int& no_steps){
    double R = exp(r*(t/no_steps));
    double Rinv = 1.0/R;
    double u = exp(sigma*sqrt(t/no_steps));
    double d = 1.0/u;
    double uu = u*u;
    double pUp = (R-d)/(u-d);
    double pDown = 1.0 - pUp;

    vector<double> prices(no_steps+1);
    prices[0] = S*pow(d, no_steps);
    for (int i=1; i<=no_steps; ++i) prices[i] = uu*prices[i-1];

    vector<double> values(no_steps+1);
    for (int i=0; i<=no_steps; ++i) values[i] = generic_payoff(prices[i],K);

    for (int CurrStep=no_steps-1; CurrStep>=1; --CurrStep) {
        for (int i=0; i<=CurrStep; ++i) {
            prices[i] = d*prices[i+1];
            values[i] = (pDown*values[i]+pUp*values[i+1])*Rinv;
            values[i] = max(values[i], generic_payoff(prices[i],K));
        };
    };
    double delta = (values[1]-values[0])/(S*(u-u*d));
    return delta;
};
```

### C++ Code 17.5: Generic binomial calculation of delta

### Exercise 17.1.

The generic routines discussed in this chapter have been for American options. How would you modify them to account for European options?

## Chapter 18

## Trinomial trees

### Contents

- 18.1 Intro .................................................... 183
- 18.2 Implementation .................................... 183
- 18.3 Further reading .................................... 185

### 18.1 Intro

A trinomial tree is similar to a binomial tree, just with one more branch. At each point of time there are three possible future values of the underlying S.

![](img/f93b3f3a5d69957a07ff6e28c47bacdd_183_0.png)

### 18.2 Implementation

A trinomial tree can be implemented with various parameterizations. We will show the calculation using the following parameterization:

```
u = e^{\sigma \sqrt{\Delta t}}

e = \frac{1}{u}

p_u = -\sqrt{\frac{\Delta t}{12\sigma^2}} \left( r - q - \frac{\sigma^2}{2} \right) + \frac{1}{6}

p_m = \frac{2}{3}

p_d = \sqrt{\frac{\Delta t}{12\sigma^2}} \left( r - q - \frac{\sigma^2}{2} \right) + \frac{1}{6}
```

We calculate the option price using the usual roll back procedure with the continuation value

e^{-r \Delta t} (p_u f_u + p_m f_m + p_d f_d)

```cpp
#include <vector>
#include <cmath>
using namespace std;

double option_price_put_american_trinomial( const double& S,
        const double& K,
        const double& r,
        const double& q,
        const double& sigma,
        const double& t,
        const int& steps) {
    double delta_t = t / steps;
    double Rinv = exp(-r*(delta_t));
    double sigma_sqr = pow(sigma,2);
    double u = exp(sigma*sqrt(3.0*delta_t));
    double d = 1.0/u;
    double p_u = 1.0/6.0 + sqrt(delta_t/(12.0*sigma_sqr)) * (r-q-0.5*sigma_sqr);
    double p_m = 2.0/3.0;
    double p_d = 1.0/6.0 - sqrt(delta_t/(12.0*sigma_sqr)) * (r-q-0.5*sigma_sqr);

    vector<double> values; // price of underlying in a tree
    vector<double> Svec;
    Svec.push_back(S);
    for (int step=1; step<=steps; ++step){
        Svec.push_back(Svec[step-1]*u); // use the fact that only the extreme values change.
        Svec.push_back(Svec[step-1]*d);
    }

    vector<double> values_next;
    for (int i=0; i<m; ++i) values_next[i] = max(0.0, K-Svec[i]); // call payoffs at maturity
    vector<double> values; // value of option
    for (int step=steps-1; step>=0; --step) {
        int m = (int)(Svec[step].size());
        values = vector<double>(m); // value of option
        for (int i=0; i<m; ++i) {
            values[i] = (p_u*values_next[i+2]+p_m*values_next[i+1] + p_d*values_next[i])*Rinv;
            values[i] = max(values[i], K-Svec[step][i]); // check for exercise
        }
        values_next=values;
    }
    return values[0];
};
```

### C++ Code 18.1: Price of american put using a trinomial tree

### Example

You are given the following information about an option: S = 100, K = 100, r = 0.1, sigma = 0.25 and time to maturity is 1 year. Price an American put using a trinomial approximation with 100 steps.

```matlab
function P = opt_price_trinomial_am_put(S, K, r, q, sigma, t, steps)
delta_t = t/steps;
sigma_sqr=sigma^2;
R=exp(r*delta_t);
u = exp(sigma*sqrt(3.0*delta_t));
d = 1.0/u;
p.u = 1/6 + sqrt(delta_t/(12*sigma_sqr)) * (r-q-0.5*sigma_sqr);
p.m = 2/3;
p.d = 1/6 - sqrt(delta_t/(12*sigma_sqr)) * (r-q-0.5*sigma_sqr);
Svec = [ S ];
Stre = [ Svec ];
Sd = [ ];
for step=1:steps+1
    Su = Su*u;
    Sd = Sd*d;
    Svec = [ Sd; Svec; Su ];
    Stre= [ Stre, zeros(2,steps), Stre ];
end
values_next = max(K-Svec, 0);
for step = 2:steps+1
    m = 2*step-1;
    values = R*(p.u*values_next(1:3+m-2)+p.m*values_next(2:m+1)+p.d*values_next(1:m));
    values_next = max(values, K-Stre(1:m, step+1));
end
P = values;
end
```

### Matlab Code 18.1: Price of american put using a trinomial tree

```cpp
C++ program:
double S = 100.0; double K = 100.0;
double r = 0.1; double q = 0; double sigma = 0.25;
double time=1.0; int no_steps = 100;
cout << " american put = " << option_price_put_american_trinomial(S,K,r,q,sigma,time,no_steps) << endl;
Output of C++ program:
american put = 6.52719
```

### Exercise 18.1.

In the code for the trinomial tree the price of the underlying is put into a triangular data structure. This can be collapsed into a single array, since the only changes when you add one step is to add one price at the top and at the bottom. If you keep track of the top and bottom of the current array you can access the prices of the underlying through some clever indexing into the single vector of prices of the underlying.

### Exercise 18.2.

Similarly to the binomial case, one can build a generic trinomial tree where the payoff function is passed as a parameter to the routine. Implement such a generic trinomial tree.

### 18.3 Further reading

Hull (2011)

## Chapter 19

## Alternatives to the Black Scholes type option formula

### Contents

| Section | Page |
|---|---|
| 19.1 Merton's Jump diffusion model. | 186 |
| 19.2 Heston's pricing formula for a stochastic volatility model | 188 |

A large number of alternative formulations to the Black Scholes analysis has been proposed. Few of them have seen any widespread use, but we will look at some of these alternatives.

### 19.1 Merton's Jump diffusion model.

Merton (1976) has proposed a model where in addition to a Brownian Motion term, the price process of the underlying is allowed to have jumps. The risk of these jumps is assumed to not be priced.

In the following we look at an implementation of a special case of Merton's model, described in (Hull, 1993, pg 454), where the size of the jump has a normal distribution. \(\lambda\) and \(\kappa\) are parameters of the jump distribution. The price of an European call option is given in Formula 19.1 and implemented in C++ Code 19.1

```
c = \sum_{n=0}^{\infty} \frac{e^{\lambda \tau} (\lambda \tau)^n}{n!} C_{BS}(S, X, r_n, \sigma_n^2, T - t)

where

\tau = T - t

\lambda' = \lambda(1 + \kappa)

C_{BS}(\cdot) is the Black Scholes formula, and

\sigma_n^2 = \sigma^2 + \frac{n \delta^2}{\tau}

r_n = r - \lambda \kappa + \frac{n \ln(1 + \kappa)}{\tau}
```

Formula 19.1: The option pricing formula of the Merton (1976) model

In implementing this formula, we need to terminate the infinite sum at some point. But since the
