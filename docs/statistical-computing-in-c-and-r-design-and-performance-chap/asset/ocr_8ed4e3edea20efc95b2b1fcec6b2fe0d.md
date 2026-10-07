# EXERCISES

147

probability mass function

```
$f(x) = \begin{cases} \binom{k}{x}p^x(1-p)^{k-x}, & x = 0, 1, \dots, k, \ 0 < p < 1, k \ge 1, \ 0, & \text{otherwise.} \end{cases}$
```

4.4. Rework the multiplicative congruential generator with $a=12, m=31$ and $x_0=9$. Does the resulting sequence numbers represent an improvement over the case of $a=3$? If so, is it better?

4.5. Rework the FM2 generator code from Section 4.3 so that it will adaptively produce output for any given value of n.

4.6. Discuss the behavior of mixed congruential generators that have $a=1, c=0$ and $a=m$.

4.7. Let $a, c$ and $m$ be parameters for a mixed congruential generator having $x_n = (ax_{n-1} + c) \pmod m$ and divide $d$ (without remainder).

+   a) If $y_{n-1} = x_{n-1} \pmod d$ show that $y_n = (ay_{n-1} + c) \pmod d$.

+   b) Use the previous method to show that when $m=2^p$ the first $r$ bits of $x_n$ form a congruential sequence that has period of at most $2^r$ for $r>1$ and this is either constant or strictly alternating.

+   c) Show that the bit pattern has for $m=2^p$ does not occur if $m=2^p \pm 1$.

+   d) Conclude from the two results (why?) that $m=2^p \pm 1$ may be preferable to using $m=2^p$.

(Knuth 1998a, Section 3.2.1.1)

4.8. Verify that the choices $m=2^p, c=3$ and $a=5$ satisfy the conditions of Theorem 4.2. Can you suggest a general result based on this example?

4.9. Let $a, c$ and $m$ be the parameters of a mixed congruential generator with $x_n = (ax_{n-1} + c) \pmod m$. Show that

```
$x_{n+k} = (ax_n + (a^k-1)c/(a-1)) \pmod m$.
```

Conclude this (why?) that the subsequence of every kth term from $\{x_n\}$ represents a linear congruential generator with multiplier $a^k \pmod m$ and increment $(a^k-1)c/(a-1) \pmod m$.

(Knuth 1998a, Section 3.2.1)

4.10. Create an alternative version of the FM2 class where the numbers are held in a pointer to double that is a private member of the class. Provide an overloaded [()] operator to access the random values.

4.11. Create an alternative version of class FM2 that allows for general specifications of $m$ and $a$ with (4.4) as the default. Other possible choices for $a$ that might be considered when $m=2^{31}-1$ is $a=729328550, 1228674159$ and (Fisman and Moore 1996). Generate some of these choices and assess the goodness-of-uniformity of the distribution using methods available in.

4.12. Develop C++ code that implements a feedback shift generator for specified values of $p, q$ and $r$. Do not store the sequence obtained from (4.5). Instead, use a p-bit pointer to retain the bits that are needed for the recursion and adaptively make contiguous, nonoverlapping blocks of $r$ bits from this working array. Make sure that your generator cycles the sequence produced from (4.5) in a way that will allow it to realize a full period.

4.13. Apply the feedback register code from Exercise 4.12 to the case where $p=9, q=4$ and $r=8$. The resulting generator has full period?