**Exercise 617** Find the covering radius and the packing radius of the $[n, 1, n]$ repetition code over $\mathbb{F}_q$.

**Exercise 618** Prove that if $\mathcal{C}_1 \subseteq \mathcal{C}_2$, then $\rho(\mathcal{C}_2) \le \rho(\mathcal{C}_1)$.

The definitions of covering radius and packing radius lead directly to a relationship between the two as we noted in Section 1.12.

# **Theorem 11.1.1** Let $\mathcal{C}$ be a code of minimum distance $d$. Then

$$\rho(\mathcal{C}) \ge \left\lfloor \frac{d-1}{2} \right\rfloor.$$

Furthermore, we have equality if and only if $\mathcal{C}$ is perfect.

Another equivalent formulation of the covering radius is stated in Theorem 1.12.5; we restate this result but generalize slightly the first part to apply to nonlinear as well as linear codes. In order to simplify terminology, we will call the set $\mathbf{v} + \mathcal{C}$ a coset of $\mathcal{C}$ with coset representative $\mathbf{v}$ even if $\mathcal{C}$ is nonlinear. Care must be taken when using cosets with nonlinear codes; for example, distinct cosets need not be disjoint, as Exercise 619 shows.

# **Theorem 11.1.2** Let $\mathcal{C}$ be a code. The following hold:

+   (i) $\rho(\mathcal{C})$ is the largest value of the minimum weight of all cosets of $\mathcal{C}$.

+   (ii) If $\mathcal{C}$ is an $[n, k]$ linear code over $\mathbb{F}_q$ with parity check matrix $H$, then $\rho(\mathcal{C})$ is the smallest number $s$ such that every nonzero vector in $\mathbb{F}_q^{n-k}$ is a combination of $s$ or fewer columns of $H$.

**Exercise 619** Find a nonlinear code and a pair of cosets of that code that are neither equal nor disjoint.

**Exercise 620** Let $\mathcal{C}$ be an $[n, k, d]$ linear code over $\mathbb{F}_q$ with covering radius $\rho(\mathcal{C}) \ge d$. Explain why there is a linear code with more codewords than $\mathcal{C}$ but the same error-correcting capability.

An obvious corollary of part (ii) of Theorem 11.1.2 is the following upper bound on the covering radius of a linear code, called the Redundancy Bound.

# **Corollary 11.1.3 (Redundancy Bound)** Let $\mathcal{C}$ be an $[n, k]$ code. Then $\rho(\mathcal{C}) \le n - k$.

**Exercise 621** Prove Corollary 11.1.3.

Recall from (1.11) that a sphere of radius $r$ in $\mathbb{F}_q^n$ contains

$$\sum_{i=0}^r \binom{n}{i} (q-1)^i$$

vectors. The following is a lower bound on the covering radius, called the Sphere Covering Bound; its proof is left as an exercise.