# 1.2 Modular arithmetic

gcd = 3 \cdot 23 = 69. However, we have no efficient algorithm for factoring. Is there some other way to compute greatest common divisors?

Euclid's algorithm uses the following simple formula.

![](bbox=[0.173, 0.166, 0.401, 0.403])

Euclid of Alexandria
BC 325–265

© Corbis

Euclid's rule If x and y are positive integers with x \geq y, then gcd(x, y) = gcd(x mod y).

Proof. It is enough to show the slightly simpler rule gcd(x, y) = gcd(x - y), from which the one stated can be derived by repeatedly subtracting y from x.

Here goes. Any integer that divides both x and y must also divide x - y, so gcd(x, y) \leq gcd(x - y). Likewise, any integer that divides both x - y and y must must divide both x and y, so gcd(x, y) \geq gcd(x - y, y).

Figure 1.5 Euclid's algorithm for finding the greatest common divisor of two numbers.

```
function Euclid(a,b)
Input: Two integers a and b with a \geq b \geq 0
Output: gcd(a,b)
```

```
if b = 0: return a
return Euclid(a, mod b)
```

Euclid's rule allows us to write down an elegant recursive algorithm (Figure 1.5), and its correctness follows immediately from the rule. In order to figure out its running time, we need to understand how quickly the arguments (a, b) decrease with each successive recursive call. In a single round, arguments (a, b) become (b, a mod b): their order is swapped, and the larger of them, a, gets reduced to a mod b. This substantial reduction.