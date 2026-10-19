![](bbox=[0.05, 0.05, 0.95, 0.32])

# 5.2 Forward Difference (Algorithm)

The most direct method for numerical differentiation starts by expanding a function in a Taylor series to obtain its value at a small step h away:

```
y(t + h) = y(t) + h dy(t)/dt + (h²/2!) d²y(t)/dt² + (h³/3!) dy³(t)/dt³ + ⋯ ,
```

⇒ y(t + h) - y(t) / h = dy(t)/dt + (h/2!) d²y(t)/dt² + (h²/3!) dy³(t)/dt³ + ⋯ .

If we ignore the h² terms in (5.3), we obtain the forward-difference derivative algorithm for the derivative (5.2) for y(t):

```
dy(t)/dt |_{fd} = [y(t + h) - y(t)] / h .
```

An estimate of the error follows from substituting the Taylor series:

```
dy(t)/dt |_{fd} ≃ dy(t)/dt - (h/2) d²y(t)/dt² + ⋯ .
```

You can think of this approximation as using two points to represent the function by a straight line in the interval from x to x + h (Figure 5.1a). The approximation (5.4) has an error proportional to h (unless the heavens look down upon you kindly and make y'' vanish). We can make the approximation error smaller by making h smaller, yet precision will be lost through the subtractive cancelation on the left-hand side (LHS) of (5.4) for too small an h.

To see how the forward-difference algorithm works, let y(t) = a + bt². The exact derivative is y' = 2bt, while the computed derivative is

```
dy(t)/dt |_{fd} ≃ [y(t + h) - y(t)] / h = 2bt + bh .
```

This clearly becomes a good approximation only for small h (h << 1/b).