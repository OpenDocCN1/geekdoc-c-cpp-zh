![](bbox=[0.13, 0.01, 0.86, 0.29])

Figure 11.5: An EDR for a theater.

![](bbox=[0.15, 0.36, 0.85, 0.65])

Figure 11.6: An EDR for a cathedral.

# 11.3 The Comb Filter Reverberator

One of the reverberator modules that Schroeder proposed is a comb filter. Remember that we are looking for modules that produce echoes and the comb filter with feedback will do just that. The comb filter reverberator is familiar looking because it's also the delay with feedback algorithm you studied in Chapter 7. We derived the difference equation and transfer function for the comb filter in Figure 11.7 in Chapter 7:

```
y(n) = x(n-D) + gy(n-D)
```

and

```
H(z) = \frac{z^{-D}}{1 - gz^{-D}}
```