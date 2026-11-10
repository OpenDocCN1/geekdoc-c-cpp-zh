```
sage: p_cheb.substitute_function(T, chebyshev_T).expand()
4*x^6 + 4*x^5 + 1/9*x^4 - 2*x^3 + 2/19*x^2 + 1
```

**Exercise 26 page 135.** A direct translation of the algorithm in Sage gives something like:

```
sage: def mydiv(u, v, n):
....:     v0 = v.constant_coefficient()
....:     quo = 0; rem = u
....:     for k in xrange(n+1):
....:         c = rem[0] / v0
....:         rem = (rem - c*v) >> 1  # shifting the coefficients
....:         quo += c*x^k
....:     return quo, rem
```

(One can apply this function to larger examples and measure the execution time and try to make the code more efficient, keeping the same algorithm.)

But the division by increasing powers up to order \(n\) is the series expansion of the rational function \(u/v\) truncated at order \(n+1\). Using the division of formal power series (see §7.5), we can compute the division by increasing powers like in the following function.

```
sage: def mydiv2(u, v, n):
....:     x = u.parent().gen()
....:     quo = (u / (v + O(x^(n+1)))).polynomial()
....:     rem = (u - quo*v) >> (n+1)
....:     return quo, rem
```

The line `quo = ...` uses the fact that, if we add \(O(\) to a polynomial, it is converted into a truncated series and that the default precision used when dividing a polynomial by a series is that of the divisor.

**Exercise 27 page 136.** First of all, \(u_{10^{10000}}\) has about \(10^{10000}\) expected digits. Computing it entirely is absolutely out of reach. But as we are only interested by the last five digits, it is not a real problem: we will compute everything modulo \(10^5\). The fast exponentiation method as presented in §3.2.4 needs tens of thousands of matrix multiplications, the matrix size being 1000 × 1000, with coefficients in \(\mathbb{Z}/10^5\mathbb{Z}\). Each of these matrix products costs about one billion multiplications, or less with a fast algorithm. It is not impossible, but a test with only one multiplication suggests that the full computation with Sage would take at least one hour:

```
sage: Mat = MatrixSpace (IntegerModRing(10^5), 1000)
sage: m1, m2 = (Mat.random_element() for i in (1,2))
sage: %time p = m1*m2
CPU times: user 48 ms, sys: 4 ms, total: 52 ms
Wall time: 54.3 ms
```

It is possible to do much better from the algorithmic point of view. Let us denote \(S\) the shift operator \((a_n)_{n\in\mathbb{N}} \mapsto (a_{n+1})_{n\in\mathbb{N}}\). The equation satisfied by \(u =