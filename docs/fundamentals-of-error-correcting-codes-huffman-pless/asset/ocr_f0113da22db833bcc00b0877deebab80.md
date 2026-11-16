# Exercise 275 Verify the syndrome polynomials found in Example 4.6.3.

Step II: Suppose that y(x) is the received vector. Compute the syndrome polynomial S(y(x)) = R_g(x)(x^(n-k)y(x)). By Theorem 4.6.1(iv), S(y(x)) = S(e(x)), where y(x) = c(x) + e(x) with c(x) in C.

Example 4.6.4 Continuing with Example 4.6.3, suppose that y(x) = 1 + x^4 + x^7 + x^9 + x^10 + x^12 is received. Then S(y(x)) = x + x^2 + x^6 + x^7.

# Exercise 276 Verify that S(y(x)) = x + x^2 + x^6 + x^7 in Example 4.6.4.

Step III: If S(y(x)) is in the list computed in Step I, then you know the error polynomial e(x) and this can be subtracted from y(x) to obtain the codeword c(x). If S(y(x)) is not in the list, go on to Step IV.

Example 4.6.5 S(y(x)) from Example 4.6.4 is not in the list of syndrome polynomials given in Example 4.6.3.

Step IV: Compute the syndrome polynomial of xy(x), x^2y(x), ... in succession until the syndrome polynomial is in the list from Step I. If S(y^k(x)) is in this list and is associated with the error polynomial e'(x), then the received vector is decoded as y(x) - x^(k-1)e'(x).

The computation in Step IV is most easily carried out using Theorem 4.6.2. As R_g(x)(x^(n-k)y(x)) = S(y(x)) = sum_{i=0}^{n-k-1} s_i x^i.

```
S(y(xy(x)) = R_g(x)(x^(n-k)xy(x)) = R_g(x)(x(x^(n-k)y(x))) = R_g(x)(xS(y(x)))
= xS(y(x)) - s_(n-k-1)g(x). (4.8)
```

We proceed in the same fashion to get the syndrome of x^2y(x) from that of xy(x).

Example 4.6.6 Continuing with Example 4.6.4, we have, using (4.8) and S(y(x)) = x + x^2 + x^6 + x^7, that S(xy(x)) = (x + x^2 + x^6 + x^7) - 1 . g(x) = 1 + x^4 + x^7 + x^8 + x^9, which is not in the list in Example 4.6.3. Using (4.8), S(x^2y(x)) = x(1 + x^4 + x^7 + x^8 + x^9 + x^6) - g(x) = x + x^5 + x^8 + x^9 + x^10 + x^7, which corresponds to the error x^4 + x^14 implying that y(x) is decoded as y(x) - (x^2 + x^12) = 1 + x^2 + x^4 + x^7 + x^9 + x^10. Note that this is the codeword (1 + x^3)g(x).

The Meggitt decoder can be implemented with shift-register circuits, and a second version of the Meggitt Decoding Algorithm is often employed in order to simplify this circuit. In this second implementation, the circuitry only corrects coordinate n - 1 of the vector in the shift-register. The vector in the shift-register starts out as the received vector y(x); if there is an error in position n - 1, it is corrected. Then the shift xy(x) is moved into the shift-register. If there is an error in coordinate n - 1, it is corrected; this in effect corrects coordinate n - 2 of y(x). This continues until y(x) and its n - 1 shifts have been moved into the shift-register and have been examined. At each stage only the error at the end of the shift-register is corrected. This process corrects the original received vector y(x) since