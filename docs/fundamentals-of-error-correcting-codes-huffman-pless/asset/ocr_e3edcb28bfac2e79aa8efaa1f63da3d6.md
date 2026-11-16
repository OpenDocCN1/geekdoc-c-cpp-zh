# 1.7 More general equivalence of codes

**Exercise 45** Let $\mathcal{S}$ be the set of all codes over $\mathbb{F}_q$ of length $n$. Let $C_1, C_2 \in \mathcal{S}$. Define $C_1 \sim C_2$ to mean that there exists an $n \times n$ monomial matrix $M$ such that $C_1 M = C_2$. Prove that $\sim$ is an equivalence relation on $\mathcal{S}$. (The definition of "equivalence relation" is given in Exercise 37.)

There is one more type of map that we need to consider: that arising from automorphisms of the field $\mathbb{F}_q$, called Galois automorphisms. We will apply this in conjunction with monomial maps. (We will apply field automorphisms on the right of field elements since we are applying matrices on the right of vectors.) If $\gamma$ is a field automorphism of $\mathbb{F}_q$ and $M = DP$ is a monomial map with entries in $\mathbb{F}_q$, then applying the map $M\gamma$ to a vector $\mathbf{x}$ is described by the following process, where again $\sigma$ is the permutation associated to the matrix $P$. For all $i$:

+   - first, multiply the $i$th component of $\mathbf{x}$ by the $i$th diagonal entry of $D$,
+   - second, move this product to coordinate position $i\sigma$, and
+   - third, apply $\gamma$ to this component.

**Example 1.7.4** The field $\mathbb{F}_4$ has automorphism $\gamma$ given by $xy = x^2$. If $M = DP = \text{diag}(a, b, c)(1, 2, 3)$ is the monomial map of Example 1.7.2 and $\mathbf{x} = x_1 x_2 x_3 = (x_1, x_2, x_3) \in \mathbb{F}_4^3$, then

$xM\gamma = (ax_1, bx_2, cx_3)P\gamma = (cx_3, ax_1, bx_2)\gamma = ((cx_3)^2, (ax_1)^2, (bx_2)^2).$

For instance, $(1, \omega, 0)\text{diag}(\omega, \overline{\omega}, 1)(1, 2, 3)\gamma = (0, \overline{\omega}, 1).$

We say that two codes $C_1$ and $C_2$ of the same length over $\mathbb{F}_q$ are _equivalent_ provided there is a monomial matrix $M$ and an automorphism $\gamma$ of the field such that $C_2 = C_1 M\gamma$. This is the most general notion of equivalence that we will consider. Thus we have three notions of when codes are the "same": permutation equivalence, monomial equivalence, and equivalence. All three are the same if the codes are binary; monomial equivalence and equivalence are the same if the field considered has a prime number of elements. The fact that these are the appropriate maps to consider for equivalence is a consequence of a theorem by MacWilliams [212] regarding weight preserving maps discussed in Section 7.9.

Two equivalent codes have the same weight distribution. However, two codes with the same weight distribution need not be equivalent as Example 1.6.1 shows. Exercise 35 shows that if $C_1$ and $C_2$ are permutation equivalent codes, then so are their duals under the same map. However, if $C_1 M = C_2$, it is not necessarily the case that $C_1^\perp M = C_2^\perp$.

**Example 1.7.5** Let $C_1$ and $C_2$ be $[2, 1, 2]$ codes over $\mathbb{F}_4$ with generator matrices $[1 \quad 1]$ and $[1 \quad \omega]$, respectively. Then the duals $C_1^\perp$ and $C_2^\perp$ under the ordinary inner product have generator matrices $[1 \quad 1]$ and $[1 \quad \overline{\omega}]$, respectively. Notice that $C_1 \text{diag}(1, \omega) \neq C_2$, but $C_1^\perp \text{diag}(1, \omega) \neq C_2^\perp$.

In the above example, $C_1$ is self-dual but $C_2$ is not. Thus equivalence may not preserve self-duality. However, the following theorem is valid, and its proof is left as an exercise.