# 4.6 Meggitt decoding of cyclic codes

In this section we present a technique for decoding cyclic codes called Meggitt decoding [238, 239]. There are several variations of Meggitt decoding; we will present two of them. Meggitt decoding is a special case of permutation decoding, which will be explored further in Section 10.2. Permutation decoding itself is a special case of error trapping.

Let C be an [n, k, d] cyclic code over F_q with generator polynomial g(x) of degree n - k; C will correct t = [(d - 1)/2] errors. Suppose that c(x) in C is transmitted and y(x) = c(x) + e(x) is received, where e(x) = e_0 + e_1 x + ... + e_{n-1} x^{n-1} is the error vector with wt(e(x)) <= t. The Meggitt decoder stores syndromes of error patterns with coordinate n - 1 in error. The two versions of the Meggitt Decoding Algorithm that we present can be briefly described as follows. In the first version, by shifting y(x) at most n times, the decoder finds the error vector e(x) from the list and corrects the errors. In the second version, by shifting y(x) until an error appears in coordinate n - 1, the decoder finds the error in that coordinate, corrects only that error, and then corrects errors in coordinates n - 2, n - 3, ..., 1, 0 in that order by further shifting. As you can see, Meggitt decoding takes advantage of the cyclic nature of the code.

For any vector v(x) in F_q[x], let R_{g(x)}(v(x)) be the unique remainder when v(x) is divided by g(x) according to the Division Algorithm; that is, R_{g(x)}(v(x)) = r(x), where v(x) = g(x) f(x) + r(x) with r(x) = 0 or deg r(x) < n - k. The function R_{g(x)} satisfies the following properties; the proofs are left as an exercise.

+   **Theorem 4.6.1** With the preceding notation the following hold:
+   (i) R_{g(x)}(a v(x) + b v'(x)) = a R_{g(x)}(v(x)) + b R_{g(x)}(v'(x)) for all v(x), v'(x) in F_q[x] and all a, b in F_q.
+   (ii) R_{g(x)}(v(x) + a(x)(x^n - 1)) = R_{g(x)}(v(x)).
+   (iii) R_{g(x)}(v(x)) = 0 if and only if v(x) mod (x^n - 1) in C.
+   (iv) If c(x) in C, then R_{g(x)}(c(x) + e(x)) = R_{g(x)}(e(x)).
+   (v) If R_{g(x)}(e(x)) = R_{g(x)}(e'(x)), where e(x) and e'(x) each have weight at most t, then e(x) = e'(x).
+   (vi) R_{g(x)}(v(x)) = v(x) if deg v(x) < n - k.

+   **Exercise 274** Prove Theorem 4.6.1.

Part (ii) of this theorem shows that we can apply R_{g(x)} to either elements of R_n or elements of F_q[x] without ambiguity. We now need a theorem due to Meggitt that will simplify our computations with R_{g(x)}.

**Theorem 4.6.2** Let g(x) be a monic divisor of x^n - 1 of degree n - k. If R_{g(x)}(v(x)) = s(x), then
R_{g(x)}(x v(x) mod (x^n - 1)) = R_{g(x)}(x s(x)) = x s(x) - g(x) s_{n-k-1},
where s_{n-k-1} is the coefficient of x^{n-k-1} in s(x).