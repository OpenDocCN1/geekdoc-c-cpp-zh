Exercise 397 Let C be a [16, 8, 4] self-dual doubly-even binary code. After having done Exercises 395 and 396, do the following: (a) Show that all odd weight vectors of F_2^16 are in a coset of C of either weight 1 or weight 3. (b) Show that there are exactly 16 cosets of C of weight 1 and exactly 112 cosets of C of weight 3.

Notice that this exercise shows that the cosets of weight 3 in fact exist.

Before proceeding with the computation of the weight distributions of the cosets of weight 2 in the [16, 8, 4] codes, we present the following useful result.

**Theorem 7.5.5** Let C be a code of length n over F_q, with A \in \Gamma Aut(C). Let v \in F_q^n. Then the weight distribution of the coset v + C is the same as the weight distribution of the coset vA + C.

**Proof:** If x \in F_q^n, then applying A to x rescales the components with nonzero scalars, permutes the components, and then maps them to other field elements under a field automorphism. Thus w(x) = w(xA). As A \in \Gamma Aut(C), vA + C = {vA + c | c \in C} = {(v + c)A | c \in C} implying that vA + C and v + C have the same weight distribution.

**Example 7.5.6** Let C be a [16, 8, 4] self-dual doubly-even binary code. By [262], up to equivalence there are two such codes. Each code has different weight distributions for its cosets of weight 2. These two codes, denoted C_1 and C_2, have generator matrices G_1 and G_2, respectively, where

![](bbox=[0.15, 0.51, 0.75, 0.68])

and

![](bbox=[0.15, 0.71, 0.75, 0.87])

In this example, we compute the weight distribution of the cosets of C_1 of weight 2. Notice that C_1 is the direct sum of an [8, 4, 4] code with itself, the only such code is \widehat{\mathcal{H}}_3 by Exercise 56. Let v be a weight 2 vector that is a coset leader of a coset of C_1. As we want to find the weight distribution of v + C_1, by Theorem 7.5.5, we may replace v by vA, where