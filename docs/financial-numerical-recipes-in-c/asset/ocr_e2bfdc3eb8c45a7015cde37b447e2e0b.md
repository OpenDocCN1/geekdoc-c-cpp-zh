# Chapter 9

# Basic Option Pricing, the Black Scholes formula

# Contents

| 9.1 | The formula | 90 |
| --- | --- | --- |
| 9.2 | Understanding the why's of the formula | 92 |
| 9.2.1 | The original Black Scholes analysis | 93 |
| 9.2.2 | The limit of a binomial case | 93 |
| 9.2.3 | The representative agent framework | 93 |
| 9.3 | Partial derivatives | 93 |
| 9.3.1 | Delta | 93 |
| 9.3.2 | Other Derivatives | 94 |
| 9.3.3 | Implied Volatility | 96 |
| 9.4 | References | 98 |

The pricing of options and related instruments has been a major breakthrough for the use of financial theory in practical application. Since the original papers of Black and Scholes (1973) and Merton (1973), there has been a wealth of practical and theoretical applications. We will now consider the original Black Scholes formula for pricing options, how it is calculated and used. For the basic intuition about option pricing the reader should first read the discussion of the binomial model in the previous chapter, as that is a much better environment for understanding what is actually calculated.

An option is a derivative security, its value depends on the value, or price, of some other underlying security, called the underlying security. Let \( S \) denote the value, or price, of this underlying security. We need to keep track of what time this price is observed at, so let \( S_t \) denote that the price is observed at time \( t \). A call (put) option gives the holder the right, but not the obligation, to buy (sell) some underlying asset at a given price \( K \), called the exercise price, on or before some given date \( T \). If the option is a so called European option, it can only be used (exercised) at the maturity date. If the option is of the so called American type, it can be used (exercised) at any date up to and including the maturity date \( T \). If exercised at time \( T \), a call option provides payoff

```
C_T = \max(0, S_T - K)
```

and a put option provides payoff

```
P_T = \max(0, K - S_T)
```

The Black Scholes formulas provides analytical solutions for European put and call options, options which can only be exercised at the options maturity date. Black and Scholes showed that the additional