suggesting that

$$a(n)=r^n\cdot a(0)\quad\text{for }n=0,1,2,\ldots$$

Let’s check with Maple.

```
```maple
rsolve({a(n+1) = 1.001 * a(n), a(0) = 1000}, a(n)):
Money := unapply(%, n);
Money -> 1000 (1001/1000)^n
```
```

Note that Maple converts to rational numbers when using `rsolve`. Recall that `unapply` turns an expression into a function.

What is the overall trend?

```
```maple
Limit(Money(n), n = infinity) = limit(Money(n), n = infinity);
lim[n→∞] 1000 (1001/1000)^n = ∞
```
```

```
```maple
with(plots):
```
```

```
```maple
pointplot([seq([i, Money(i)], i = 0..12·4)], title = "Money over Time");
```
```

![](bbox=[0.32, 0.428, 0.72, 0.731])

The graph looks like a line even though this function is obviously nonlinear.

How many years does it take for the plot to show some curvature?