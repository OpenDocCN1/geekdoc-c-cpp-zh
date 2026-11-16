We conclude this section with a theorem specifying exactly the condition on the length n which guarantees the existence of a self-dual code of that length; its proof is found in [260]. In Corollary 9.2.2, we give necessary and sufficient conditions on the length for the existence of self-dual codes over F2 and F3, which agree with the following theorem; the corollary will also give necessary and sufficient conditions on the length for existence of Type II codes that are not covered in this theorem.

**Theorem 9.1.3** There exists a self-dual code over Fq of even length n if and only if (-1)^(n/2) is a square in Fq. Furthermore, if n is even and (-1)^(n/2) is not a square in Fq, then the dimension of a maximal self-orthogonal code of length n is (n/2) - 1. If n is odd, then the dimension of a maximal self-orthogonal code of length n is (n - 1)/2.

**Example 9.1.4** Theorem 9.1.3 shows that a self-dual code of length n over F3 exists if and only if 4 | n. An example of such a code is the direct sum of m = n/4 copies of the {4, 2, 3} self-dual tetracode introduced in Example 1.3.3. If n = 2 (mod 4), then no self-dual code of length n over F3 exists; however, a maximal self-orthogonal code of dimension (n/2) - 1 does exist. An example is the direct sum of m = (n - 2)/4 copies of the tetracode and one copy of the zero code of length 2. The theorem also guarantees that a self-dual code of length n over F5 exists if and only if n is even. An example is the direct sum of m = n/2 copies of the {2, 1, 2} self-dual code with generator matrix [1 rho^2], where rho is the primitive element of F9 given in Table 6.4. Notice that the codes we have constructed show one direction of Theorem 9.1.3 when the fields are F3 and F9.

**Exercise 493** Use the codes constructed in Example 9.1.4 to show that if 4 | n, there exist self-dual codes of length n over F3, and if n is even, there exist self-dual codes of length n over F7 when n is even.

**Exercise 494** Prove Theorem 9.1.3 for q a power of 2.

# ## 9.2 Gleason polynomials

Self-dual codes over F2, F3, and F4, the last under the Hermitian inner product, all have weight enumerators that can be expressed as combinations of special polynomials that are the weight enumerators of specific codes of small length. These polynomials, known as Gleason polynomials, provide a powerful tool in the study of all self-dual codes over F2, F3, and F4.

Before stating Gleason's Theorem, we discuss the theorem in the case of formally self-dual binary codes. Let

```
g(x, y) = y^2 + x^2 and h(x, y) = y^8 + 14x^4y^4 + x^8.
```

Notice that g(x, y) is the weight enumerator of the binary repetition code of length 2, and h(x, y) is the weight enumerator of the [8, 4, 4] extended binary Hamming code H_8. Gleason's Theorem states that if C is any binary formally self-dual code that is divisible by Delta = 2, then W_C(x, y) = P(g, h), where P is a polynomial with rational coefficients in the