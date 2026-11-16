# Example

Stock in company XYZ is currently trading at 50. Consider a call option on XYZ stock with an exercise price of K = 50 and time to maturity of 6 months. The volatility of XYZ stock has been estimated to be \(\sigma = 30\%\). The current risk free interest rate (with continuous compounding) for six month borrowing is 10%.

+   1. Determine the option price.

To calculate the price of this option we use the Black Scholes formula with inputs \(S = 50\) and \(K = 50\), \(r = 0.10\), \(\sigma = 0.3\) and \((T - t) = 0.5\).

Matlab program:

```
S = 100;
K = 100;
r = 0.1;
sigma = 0.1;
time = 1;
c = black.scholes.call(S,K,r,sigma,time)
```

Output from Matlab program:

c = 10.308

C++ program:

```
double S = 50; double K = 50; double r = 0.10;
double sigma = 0.30; double time=0.50;
cout << " Black Scholes call price = ";
cout << option_price_call_black_scholes( S, K , r, sigma, time) << endl;
```

Output from C++ program:

Black Scholes call price = 5.45325

# Exercise 9.1.

The Black Scholes price for a put option is:

\(p = Ke^{-r(T-t)} N(-d_2) - SN(-d_1)\)

where \(d_1\) and \(d_2\) are as for the call option:

\(\displaystyle d_1 = \frac{\ln \left(\frac{S}{K}\right) + (r + \frac{1}{2}\sigma^2)(T - t)}{\sigma \sqrt{T - t}}\)

\(d_2 = d_1 - \sigma \sqrt{T - t},\)

\(S\) is the price of the underlying security, \(K\) the exercise price, \(r\) the (continuously compounded) risk free interest rate, \(\sigma\) the standard deviation of the underlying asset, \(T - t\) the time to maturity for the option and \(N(\cdot)\) the cumulative normal distribution.

+   1. Implemet this formula.

# 9.2 Understanding the why's of the formula

To get some understanding of the Black Scholes formula and why it works will need to delve in some detail into the mathematics underlying its derivation. It does not help that there are a number of ways to prove the Black Scholes formula, depending on the setup. As it turns out, two of these ways are important to understand for computational purposes, the original Black Scholes continuous time way, and the "limit of a binomial process" way of Cox, Ross, and Rubinstein (1979).