In tests and loops, the conditions built from the operators `or` and `and` are evaluated lazily from left to right. This means that the evaluation of a condition `or` ends as soon as the first `True` value is encountered, without evaluating the rightmost terms; similarly with `and` and `False`. Hence the following divisibility test of $b$ by $a$ does not produce any error even if $a = 0$:

```
```
sage: a = 0; b = 12; (a == 0 and b == 0) or (a != 0 and b % a == 0)
```
```

The operator `not` takes precedence over `and`, which in turn takes precedence over `or`, the equality and comparison tests having precedence over all boolean operators. The two following tests are thus equivalent to the above one:

```
```
sage: ((a == 0) and (b == 0)) or ((a != 0) and (b % a == 0))
sage: a == 0 and b == 0 or not a == 0 and b % a == 0
```
```

In addition, Sage allows multiple equality or inequality tests, exactly like in mathematics:

$x \le y < z \le t \quad \text{encoded by} \quad x \texttt{ <= } y \texttt{ < } z \texttt{ <= } t$
$x = y = z \ne t \quad \text{encoded by} \quad x \texttt{ == } y \texttt{ == } z \texttt{ != } t$

In the simple cases, these tests are automatically performed; otherwise we call the `bool` command to force the evaluation:

```
```
sage: x, y = var('x, y')
sage: bool( (x-y)*(x+y) == x^2-y^2 )
True
```
```

**Integers Modulo $n$.** To define an integer modulo $n$, we first build its parent, the ring $\mathbb{Z}/n\mathbb{Z}$:

```
```
sage: Z4 = IntegerModRing(4); Z4
Ring of integers modulo 4
sage: m = Z4(7); m
3
```
```

As in the case of floating-point numbers, the computations involving $m$ are done modulo 4 via automatic conversions. In the following example, 3 and 1 are automatically converted in elements of $\mathbb{Z}/4\mathbb{Z}$:

```
```
sage: 3 * m + 1
2
```
```

When $p$ is prime, we can also choose to build $\mathbb{Z}/p\mathbb{Z}$ as a field:

```
```
sage: Z3 = GF(3); Z3
Finite Field of size 3
```
```

Both `IntegerModRing(n)` and `GF(p)` are domains with a normal form: the reduction modulo $n$ or $p$ are done automatically. The computations in rings and finite fields are detailed in Chapter 6.