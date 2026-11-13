them by mapping each term with the index so that the \(i^{th}\) term is at the \((n-i)^{th}\) location of the array. We store polynomials in the decreasing order of their exponents. The degree of a polynomial is the highest exponent in the polynomial. For a polynomial of degree \(n\), we would need an array of size \(n+1\) and a store polynomial as follows:

For the term \(a_i x^i\), let us store its coefficient \(a_i\) at the \([n-i]^{th}\) index in an array, that is, store a coefficient of the term with exponent \(i\) at the \([n-i]^{th}\) index.

Poly[n-i] = \(a_i\) for \(i=0\) to \(n\)

This is represented in Fig. 2.20.

| Poly[0] | Poly[1] | Poly[2] | Poly[3] | ... | Poly[n-2] | Poly[n-1] |
|---|---|---|---|---|---|---|
| \(a_n\) | \(a_{n-1}\) | \(a_{n-2}\) | \(a_{n-3}\) | ... | \(a_1\) | \(a_0\) |

![](bbox=[0.386, 0.405, 0.726, 0.425])

```
int degree; float Poly[Max + 1];
```

Here, degree <= Max

This representation is very efficient with respect to operations such as store() and retrieve() as it requires constant time O(1). The conventional algorithms of addition, subtraction, multiplication, and so on can be used for this representation very efficiently.

Such representation is both time and space efficient when the polynomial is not a sparse one such as polynomial P(x) of degree 3 where P(x) = 3x^3 + x^2 - 2x + 5 (Fig. 2.21).

| Index i | 0 | 1 | 2 | 3 | ... | N-1 |
|---|---|---|---|---|---|---|
| Coefficient | 3 | 1 | -2 | 5 | ... | 0 |

![](bbox=[0.335, 0.722, 0.767, 0.742])

Figure 2.22 shows a polynomial of degree 8.

| Index i | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|---|---|---|
| Coefficient | 11 | 0 | 5 | 1 | 2 | 0 | -3 | 1 | 10 |

![](bbox=[0.273, 0.919, 0.835, 0.939])