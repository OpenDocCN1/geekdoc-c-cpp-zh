# Theorem 11.1.4 (Sphere Covering Bound) If $C$ is a code of length $n$ over $\mathbb{F}_q$, then

\(\rho(C) \ge \min \left\{ r \mid \sum_{i=0}^{r} \binom{n}{i} (q-1)^i \ge q^{n-k} \right\}.\)

# Exercise 622 Prove Theorem 11.1.4.

# Exercise 623 Let $C$ be a [7, 3, 4] binary code. Give the upper and lower bounds for this code from the Redundancy Bound and the Sphere Covering Bound.

Another lower bound can be obtained from the following lemma, known as the Supercode Lemma.

# Lemma 11.1.5 (Supercode Lemma) If $C$ and $C'$ are linear codes with $C \subseteq C'$, then \(\rho(C) \ge \min\{wt(x) \mid x \in C' \setminus C\}\).

Proof: Let x be a vector in $C' \setminus C$ of minimum weight. Such a vector must be a coset leader of $C$ as $C \subseteq C'$; therefore \(\rho(C) \ge wt(x)\) and the result follows.

Theorem 11.12.6 will be used repeatedly, and we restate it here for convenience.

# Theorem 11.12.6 Let $C$ be an [n, k] code over $\mathbb{F}_q$. Let $\widehat{C}$ be the extension of $C$, and let $C^*$ be a code obtained from $C$ by puncturing on some coordinate. The following hold:

+   (i) If $C = C_1 \oplus C_2$, then \(\rho(C) = \rho(C_1) + \rho(C_2)\).
+   (ii) \(\rho(C^*) = \rho(C)\) or \(\rho(C^*) = \rho(C) + 1\).
+   (iii) \(\rho(\widehat{C}) = \rho(C)\) or \(\rho(\widehat{C}) = \rho(C) + 1\).
+   (iv) If $q = 2$, then \(\rho(\widehat{C}) = \rho(C) + 1\).
+   (v) Assume that x is a coset leader of C. If x' in $\mathbb{F}_q^n$ all of whose nonzero components agree with the same components of x, then x' is also a coset leader of C. In particular, if there is a coset of weight s, there is also a coset of any weight less than s.

# Exercise 624 This exercise is designed to find the covering radius of a [7, 3, 4] binary code C.

+   (a) Show that a [7, 3, 4] binary code is unique up to equivalence.
+   (b) Apply the Supercode Lemma to obtain a lower bound on \(\rho(C)\) using $C'$ equal to the [7, 4, 3] Hamming code; make sure you justify that C is indeed a subcode of $C'$.
+   (c) Show that there is no [7, 4, 4] binary code.
+   (d) Find \(\rho(C)\) and justify your answer.

# Exercise 625 Let C be an even binary code. Show that if C* is obtained from C by puncturing on one coordinate, then \(\rho(C^*) = \rho(C) - 1\).

Recall from Theorem 11.1.1 that the covering radius of a code equals the packing radius of the code if and only if the code is perfect. We have the following result dealing with extended perfect codes and codes whose covering radius is one larger than the packing radius.

# Theorem 11.1.7 If C is an [n, k, d] extended perfect code, then \(\rho(C) = d/2\). Furthermore, if C is an [n, k, d] binary code, then C is an extended perfect code if and only if \(\rho(C) = d/2\).