
```cpp
double S = 100.0; double K = 100.0;
double r = 0.1; double sigma = 0.25;
double tau = 1.0; double tau1 = 0.5;
double D1 = 10.0;
cout << " american call price with one dividend = "
<< option_price_american_call_one_dividend(S,K,r,sigma,tau,D1, tau1)<< endl;
```
Output from C++ program:
american call price with one dividend = 10.0166

## Exercise 11.2.

The Black approximation to the price of a call option paying a fixed dividend is an approximation to the value of the call. Suppose the dividend is paid at some date t1 before the maturity date of the option T. Black's approximation calculates the value of two European options using the Black Scholes formula. One with expiry date equal the ex dividend date of the options. Another with expiry date equal to the option expiry, but the current price of the underlying security is adjusted down by the amount of the dividend.

- 1. Implement Black's approximation.

```cpp
#include <cmath>
#include "normdist.h" // define the normal distribution functions
#include "fin_recipes.h" // the regular black scholes formula
double option_price_american_call_one_dividend(const double& S,
                                               const double& K,
                                               const double& r,
                                               const double& sigma,
                                               const double& tau,
                                               const double& D1){
    if (D1 <= K* (1.0-exp(-(tau-tau1)))) // check for no exercise
        return option_price_call_black_scholes(S-exp(-r*tau)*D1,K,r,sigma,tau);
    const double ACCURACY = 1e-6; // decrease this for more accuracy
    double sigma_sqr = sigma*sigma;
    double tau_sqrt = sqrt(tau);
    double tau1_sqrt = sqrt(tau1);
    double rho = - sqrt(tau1/tau);
    double S_bar = 0; // first find the S.bar that solves c=S.bar+D1-K
    double S_low=0; // the simplest: binomial search
    double S_high=S; // start by finding a very high S above S.bar
    double c=option_price_call_black_scholes(S_high,K,r,sigma,tau-tau1);
    double c_low = S_high-D1+K;
    double test;
    while ((test>0.0) && (S_high-S_low>1e-10) ) {
    S_high *= 20;
    c = option_price_call_black_scholes(S_high,K,r,sigma,tau-tau1);
    test = c-S_high-D1+K;
    };
    if (S_high>1e10) { // early exercise never optimal, find BS value
    return option_price_call_black_scholes(S-D1*exp(-r*tau1),K,r,sigma,tau);
    }
    S_bar = 0.5 * S_high; // now find S.bar that solves c=S.bar+D1-K
    c = option_price_call_black_scholes(S_bar,K,r,sigma,tau-tau1);
    test = c-S_bar-D1-K;
    while ((fabs(test)>ACCURACY) && ((S_high-S_low)>ACCURACY) ) {
    if (test<0.0) { S_high = S_bar; }
    else { S_low = S_bar; };
    S_bar = 0.5 * (S_high + S_low);
    c = option_price_call_black_scholes(S_bar,K,r,sigma,tau-tau1);
    test = c-S_bar-D1-K;
    };
    double a1 = (log((S-D1*exp(-r*tau1))/K) + (r+0.5*sigma*sigma)*tau1)/ (sigma*tau1_sqrt);
    double a2 = a1 - sigma*tau1_sqrt;
    double b1 = (log((S-D1*exp(-r*tau1))/S_bar)+(r+0.5*sigma_sqr)*tau1)/(sigma*tau1_sqrt);
    double b2 = b1 - sigma * tau1_sqrt;
    double C = (S-D1*exp(-r*tau1)) * N(b1) + (S-D1*exp(-r*tau1)) * N(a1-b1*rho);
    return (K*exp(-r*tau))*N(a2-b2*rho) - (K-D1)*exp(-r*tau1)*N(b2);
};
```

### C++ Code 11.3: Option price, Roll-Geske-Whaley call formula for dividend paying stock

## 11.3 Options on futures

### 11.3.1 Black's model

For an European option written on a futures contract, we use an adjustment of the Black Scholes solution, which was developed in Black (1976). Essentially we replace \(S_0\) with \(e^{-r(T-t)}F\) in the Black Scholes formula, and get the formula shown in 11.3 and implemented in C++ Code 11.4.

\(c = e^{-r(T-t)} \left( FN(d_1) - KN(d_2) \right)\)

where

\(d_1 = \frac{\ln\left(\frac{F}{K}\right) + \frac{1}{2}\sigma^2(T-t)}{\sigma\sqrt{T-t}}\)

\(d_2 = d_1 - \sigma\sqrt{T-t}\)

\(F\) is the futures price, \(K\) is the exercise price, \(r\) the risk free interest rate, \(\sigma\) the volatility of the futures price, and \(T-t\) is the time to maturity of the option (in years).

### Formula 11.3: Black's formula for the price of an European Call option with a futures contract as the underlying security

```cpp
#include <cmath>
#include "normdist.h"
using namespace std;

double futures_option_price_call_european_black(const double& F, // futures price
        const double& K, // exercise price
        const double& r, // interest rate
        const double& sigma, // volatility
        const double& time){ // time to maturity
    double sigma_sqr = sigma*sigma;
    double time_sqrt = sqrt(time);
    double d1 = ( log(F/K) + 0.5 * sigma_sqr * time ) / (sigma * time_sqrt);
    double d2 = d1 - sigma * time_sqrt;
    return exp(-r*time) * (F * N(d1) - K * N(d2));
};
```

### C++ Code 11.4: Price of European Call option on Futures contract

## Example

Price a futures option in the Black setting. Information: \(F = 50, K = 45, r = 8\%, \sigma = 0.2\), and time to maturity is a half year.

```cpp
C++ program:

double F = 50.0; double K = 45.0;
double r = 0.08; double sigma = 0.2;
double time=0.5;

cout << " european futures call option = "
<< futures_option_price_call_european_black(F,K,r,sigma,time) << endl;
```

Output from C++ program:

european futures call option = 0.851476

## Exercise 11.3.

The Black formula for a put option on a futures contract is

$$p = e^{-r(T-t)} (KN(-d_2) - FN(-d_1))$$

where the variables are as defined for the call option.

- 1. Implement the put option price.

## 11.4 Foreign Currency Options

Another relatively simple adjustment of the Black Scholes formula occurs when the underlying security is a currency exchange rate (spot rate). In this case one adjusts the Black-Scholes equation for the interest-rate differential.

Let $S$ be the spot exchange rate, and now let $r$ be the domestic interest rate and $r_f$ the foreign interest rate. $\sigma$ is then the volatility of changes in the exchange rate. The calculation of the price of an European call option is then shown in formula 11.4 and implemented in C++ Code 11.5.

$$c = Se^{-r_f(T-t)}N(d_1) - Ke^{-r(T-t)}N(d_2)$$

where

$$d_1 = \frac{\ln(\frac{S}{K}) + (r - r_f + \frac{1}{2}\sigma^2)(T-t)}{\sigma\sqrt{T-t}}$$

$$d_2 = d_1 - \sigma\sqrt{T-t}$$

$S$ is the spot exchange rate and $K$ the exercise price. $r$ is the domestic interest rate and $r_f$ the foreign interest rate. $\sigma$ is the volatility of changes in the exchange rate. $T - t$ is the time to maturity for the option.

### Formula 11.4: European currency call

```cpp
#include <cmath>
#include "normdist.h" // define the normal distribution function

double currency_option_price_call_european( const double& S, // exchange rate
        const double& X, // exercise
        const double& r, // r_domestic,
        const double& r_f, // r_foreign,
        const double& sigma, // volatility,
        const double& time) // time to maturity
{
    double sigma_sqr = sigma*sigma;
    double time_sqrt = sqrt(time);
    double d1 = (log(S/X) + (r-r_f + 0.5*sigma_sqr)* time)/(sigma*time_sqrt);
    double d2 = d1 - sigma*time_sqrt;
    return S * exp(-r_f*time) * N(d1) - X * exp(-r*time) * N(d2);
};
```

### C++ Code 11.5: European Futures Call option on currency

## Example

Price a European currency call given the following information $S = 50, K = 52, r = 8\%, r_f = 5\%, \sigma = 20\%$ and time to maturity = 0.5 years.

```cpp
C++ program:
double S = 50.0;     double K = 52.0;
double r = 0.08;     double r_f=0.05;
double sigma = 0.2;  double time=0.5;
cout << " european currency call option = "
     << currency_option_price_call_european(S,K,r,r_f,sigma,time) << endl;
```

Output from C++ program:

european currency call option = 2.22556

## Exercise 11.4.

The price for an european put for a currency option is

$$p = Ke^{-r(T-t)}N(-d_2) - Se^{-q(T-t)}N(-d_1)$$

- 1. Implement this formula.

## 11.5 Perpetual puts and calls

A perpetual option is one with no maturity date, it is infinitely lived. Of course, only American perpetual options make any sense, European perpetual options would probably be hard to sell¹. For both puts and calls analytical formulas has been developed. We consider the price of an American call, and discuss the put in an exercise. Formula 11.5 gives the analytical solution.

$$C^P = \frac{K}{h_1 - 1} \left( \frac{h_1 - 1}{h_1} \frac{S}{K} \right)^{h_1}$$

where

$$h_1 = \frac{1}{2} - \frac{r-q}{\sigma^2} + \sqrt{\left( \frac{r-q}{\sigma^2} - \frac{1}{2} \right)^2 + \frac{2r}{\sigma^2}}$$

$S$ is the current price of the underlying security, $K$ is the exercise price, $r$ is the risk free interest rate, $q$ is the dividend yield and $\sigma$ is the volatility of the underlying asset.

### Formula 11.5: Price for a perpetual call option

```cpp
#include <cmath>
using namespace std;
double option_price_american_perpetual_call(const double& S,
                                               const double& K,
                                               const double& r,
                                               const double& q,
                                               const double& sigma){
  double sigma_sqr=pow(sigma,2);
  double h1 = 0.5 - ((r-q)/sigma_sqr);
  h1 += sqrt(pow(((r-q)/sigma_sqr-0.5),2)+2.0*r/sigma_sqr);
  double price=(K/(h1-1.0))*pow(((h1-1.0)/h1)*(S/K),h1);
  return price;
};
```

### C++ Code 11.6: Price for an american perpetual call option
