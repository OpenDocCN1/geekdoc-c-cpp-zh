the difference equation is easier for this version; we only need to define one extra node, w(n) in Equation 11.17:

```
w(n) = x(n) + gw(n-D)
y(n) = -gw(n) + w(n-D)
   = -g[x(n) + gw(n-D)] + [(x(n-D) + gw(n-2D)]
   = -gx(n) - g^2w(n-D) + x(n-D) + gw(n-2D
   = -gx(n) + x(n-D) - g^2w(n-D) + gw(n-2D)

grouping:
```

In order to finish, find y(n - D) from the second line in Equation 11.18 and notice that this is the same as the last two terms in Equation 11.17.

```
y(n) = -gw(n) + w(n-D)

y(n-D) = -gw(n-D) + w(n-2D)

and

gy(n-D) = -g^2w(n-D) + gw(n-2D)
```

Thus, the last two terms in Equation 11.17 can be replaced by gy(n-D), and the final difference equation matches Schroeder's APF:

```
y(n) = -gx(n) + x(n-D) + gy(n-D)
```

Figure 11.13 shows another version of the same APF. The proof that it has the same difference equation is easy if you look at the node w(n) in Equation 11.20:

```
w(n) = x(n) + gw(n-D)
y(n) = -gw(n) + w(n-D)
```

![](bbox=[0.2, 0.55, 0.8, 0.7])

# Figure 11.12: Another version of the delaying all-pass reverberator.

These are the first two lines in the derivation for the delaying APF above. Figure 11.14 shows yet another structure. To figure this one out, once again find the internal node w(n) as it relates to the output in Equation 11.21:

```
w(n) = x(n) + gy(n)
y(n) = -gx(n) + w(n-D)

then

w(n-D) = x(n-D) + gy(n-D)

and

y(n) = -gx(n) + x(n-D) + gy(n-D)
```