# Chapter 21

# Credit risk

# Contents

+   21.1 The Merton Model . . . . . . . . . . . . . . . . . . . . 195

+   21.2 Issues in implementation . . . . . . . . . . . . . . . . 196

Option pricing has obvious applications to the pricing of risky bonds.

# 21.1 The Merton Model

This builds on the Black and Scholes (1973) and Merton (1973) framework to find the value of the debt issued by the firm. The ideas were already in Black and Scholes, who discussed the view of the firm as a call option.

Assume debt structure: There is a single debt issue. Debt is issued as a zero coupon bond. The bond is due on a given date T.

Assuming the firm value V follows the usual Brownian motion proces, debt is found as a closed form solution, similar in structure to the Black Scholes equation for a call option.

Easiest seen from the interpretation of firm debt as the price of risk free debt, minus the value of a put option.

Price debt by the price B of risk free debt, and then subtract the price of the put, using the Black Scholes formula.

The Black Scholes formula for a call option is

```
c = S . N(d1) - K . e^{-r(T-t)} N(d2)
```

where

```
d1 = \frac{\ln(\frac{S}{K}) + (r + \frac{1}{2}\sigma^2)(T - t)}{\sigma\sqrt{T - t}}
```

```
d2 = d1 - \sigma\sqrt{T - t}
```

N(.) = The cumulative normal distribution

```
p = Ke^{-r(T-t)}N(-d2) - SN(-d1)
```

In the context here, reinterpret S as V, firm value. The put is priced as

```
p = Ke^{-r(T-t)}N(-d2) - V_t N(-d1)
```