c = Se^{-q(T-t)}N(d_1) - Ke^{-r(T-t)}N(d_2)

where

d_1 = \frac{\ln(\frac{S}{K}) + (r - q + \frac{1}{2}\sigma^2)(T - t)}{\sigma\sqrt{T - t}}

d_2 = d_1 - \sigma\sqrt{T - t}

S is the price of the underlying security, K the exercise price, r the risk free interest rate, q the (continuous) payout and \sigma the standard deviation of the underlying asset, t the current date, T the maturity date, T - t the time to maturity for the option and N() indicates normal distribution.

# Formula 11.1: Analytical prices for European call option on underlying security having a payout of q

```
#include <cmath> // mathematical library
#include "normdist.h" // this defines the normal distribution
using namespace std;

double option_price_european_call_payout( const double& S, // spot price
                                          const double& X, // Strike (exercise) price,
                                          const double& r, // interest rate
                                          const double& q, // yield on underlying
                                          const double& sigma, // volatility
                                          const double& time ) { // time to maturity
  double sigma_sqr = pow(sigma,2);
  double time_sqrt = sqrt(time);
  double d1 = (log(S/X) + (r - q + 0.5*sigma_sqr)*time)/(sigma*time_sqrt);
  double d2 = d1 - (sigma*time_sqrt);
  double call_price = S * exp(-q*time) * N(d1) - X * exp(-r*time) * N(d2);
  return call_price;
};
```

# C++ Code 11.1: Option price, continuous payout from underlying

# 11.1.2 Dividends.

A special case of payouts from the underlying security is stock options when the stock pays dividends. When the stock pays dividends, the pricing formula is adjusted, because the dividend changes the value of the underlying.

The case of continuous dividends is easiest to deal with. It corresponds to the continuous payouts we have looked at previously. The problem is the fact that most dividends are paid at discrete dates.

# European Options on dividend-paying stock.

To adjust the price of an European option for known dividends, we merely subtract the present value of the dividends from the current price of the underlying asset in calculating the Black Scholes value.

# Example

Consider a stock option with the following data given: S = 100, K = 100, r = 0.1, \sigma = 0.25, time to maturity is one year. dividend yield = 5%. Dividend payments at times 0.25 and 0.75.

+   Determine the option price