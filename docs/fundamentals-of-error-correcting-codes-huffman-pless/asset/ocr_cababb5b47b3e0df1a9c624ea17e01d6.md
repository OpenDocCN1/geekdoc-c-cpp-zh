+   **Exercise 242** Continuing with Exercise 241, do the following:
+   (a) List the 2-cyclotomic cosets modulo 31.
+   (b) List the defining sets for all [31, 26] binary cyclic codes. Give a defining set for a representative of each equivalence class of the [31, 26] binary cyclic codes. Hint: Use Theorem 4.3.17 and Corollary 4.4.5.
+   (c) Repeat part (b) for [31, 5] binary cyclic codes. (Take advantage of your work in part (b).)
+   (d) List the 15 defining sets for all [31, 21] binary cyclic codes, and give a defining set for a representative of each equivalence class of these codes.
+   (e) List the 20 defining sets for all [31, 16] binary cyclic codes, and give a defining set for a representative of each equivalence class of these codes. ♦

If C is a code of length n over Fq, then a complement of C is a code C^c such that C + C^c = Fq^n and C ∩ C^c = {0}. In general, the complement is not unique. However, Exercise 243 shows that if C is a cyclic code, there is a unique complement of C that is also cyclic. We call this code the cyclic complement of C. In the following theorem we give the generator polynomial and generating idempotent of the cyclic complement.

**Exercise 243** Prove that a cyclic code has a unique complement that is also cyclic. ♦

**Theorem 4.4.6** Let C be a cyclic code of length n over Fq with generator polynomial g(x), generating idempotent e(x), and defining set T. Let C^c be the cyclic complement of C. The following hold.
(i) h(x) = (x^n - 1)/g(x) is the generator polynomial for C^c and 1 - e(x) is its generating idempotent.
(ii) C^c is the sum of the minimal ideals of R_n not contained in C.
(iii) If N = {0, 1, ..., n-1}, then N \ T is the defining set of C^c. ♦

**Exercise 244** Prove Theorem 4.4.6. ♦

The dual C^⊥ of a cyclic code C is also cyclic as Theorem 4.2.6 shows. The generator polynomial and generating idempotent for C^⊥ can be obtained from the generator polynomial and generating idempotent of C. To find these, we reintroduce the concept of the reciprocal polynomial encountered in Exercise 192. Let f(x) = f0 + f1 x + ... + fa x^a be a polynomial of degree a in Fq[x]. The reciprocal polynomial of f(x) is the polynomial f*(x) = x^a f(x^-1) = x^a (f(x))(x^-1) = fa + fa-1 x + ... + f0 x^a. So f*(x) has coefficients the reverse of those of f(x). Furthermore, f(x) is reversible provided f(x) = f*(x).

**Exercise 245** Show that a monic irreducible reversible polynomial 1 cannot be a primitive polynomial except for the polynomial 1 + x + x^2 over F2. ♦

We have the following basic properties of reciprocal polynomials. Their proofs are left as an exercise.