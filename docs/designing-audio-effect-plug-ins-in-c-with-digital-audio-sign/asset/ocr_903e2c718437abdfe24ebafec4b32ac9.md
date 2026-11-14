![](bbox=[0.25, 0.0, 0.75, 0.22])

![](bbox=[0.25, 0.25, 0.75, 0.48])

Let's do one more example regarding the transformation of an input signal. This time, let's choose the DC signal—it goes on forever. Figure 5.21 shows the DC signal with the first sample at 1.0 and all preceding samples at 0.0 with a sequence of x(n) = {1, 1, 1, 1, 1...}.

Using Equation 5.26 you can directly write the z transform as (remember, 1z^0 = 1) in Equation 5.28:

```
X(z) = 1 + z^{-1} + z^{-2} + z^{-3} + ... + z^{-\infty} (5.28)
```

While that looks like an ugly, infinitely long equation, it can also be represented in a closed form. In fact, a closed form representation exists for this polynomial using a polynomial series expansion, as shown in Equation 5.29:

```
X(z) = 1 + z^{-1} + z^{-2} + z^{-3} + ... + z^{-\infty}
= \frac{1}{1 - z^{-1}}
= \frac{z}{z - 1} (5.29)
```

# 5.10 The z Transform of Difference Equations

The z transform of signals is interesting, but something fascinating happens when you take the z transform of a difference equation, converting it into a transfer function in z all at once. And, the same easy rules apply. Let's do that with the basic first-order feed-forward filter. The difference equation is