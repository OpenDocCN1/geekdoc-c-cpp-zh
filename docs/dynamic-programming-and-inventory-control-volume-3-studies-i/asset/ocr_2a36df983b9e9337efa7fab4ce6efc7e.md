We finally derive the equation to obtain the value of s

```
(14.8.5) \frac{(g(s) + \lambda c)(1 - \exp - \alpha L)}{\alpha} = K + c \lambda L \exp - \alpha L
+ \{ \inf_{n \ge s} c \lambda n (1 - \exp - \alpha L) + \exp - \alpha L E[H_s(\eta - D(L))]
+ \int_0^L f(y - D(t + L)) \exp - \alpha t dt \}
```

There is a useful transformation of the preceding relations, by making use of an important identity, namely

```
(14.8.6) \exp - \alpha L E f(x - D(L)) - f(x) + (\alpha + \lambda) \int_0^L f(x - D(t)) \exp - \alpha t dt
-\alpha t dt - \lambda \int_0^L f(x - 1 - D(t)) \exp - \alpha t dt = 0, \forall x
```

**Exercise 14.11.** Show identity (14.8.6). Check that it reduces to the identity
-x^+ + \exp - \alpha L E(x - D(L))^+ + (\alpha + \lambda) E \int_0^L (x - D(t))^+ \exp - \alpha t dt
-\lambda E \int_0^L (x - 1 - D(t))^+ \exp - \alpha t dt = 0.

The easiest way is to show that the derivative in x of this expression vanishes. Since it is 0 for x \le 0, it vanishes for all x.

With this expression we can assert that

```
(14.8.7) g(x) = \alpha c x + \exp - \alpha L E f(x - D(L)),
```

so we get the

# Lemma 14.2. The function g(x) is convex and continuous.

PROOF. It follows immediately from the convexity of f.

The function g is not continuously differentiable, and piece-wise linear.

# Lemma 14.3. Assume

```
\alpha c - p \exp - \alpha L < 0,
```

then the function g(x) satisfies

```
g(x) \to +\infty, as |x| \to +\infty.
```

It has a unique minimum denoted \hat{n} which is a positive integer.

# PROOF. Note that

```
g'(x) = \alpha c - p \exp - \alpha L, if x < 0,
```

and the assumption implies that g(x) decreases for x < 0. Moreover it guaranties that

```
g(x) \to +\infty, as x \to -\infty.
```

The same property holds trivially when x \to +\infty. Since the function is piece-wise linear with discontinuities at positive integers, the minimum is integer. It is a positive number, since the function decreases for x < 0.