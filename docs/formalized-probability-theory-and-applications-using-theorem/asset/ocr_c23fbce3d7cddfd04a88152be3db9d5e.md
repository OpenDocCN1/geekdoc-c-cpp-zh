```
D_{KL}(\mu || \nu) = \sum_{x \in s} \mu \{x\} \log \frac{\mu \{x\}}{\nu \{x\}} (9.8)
```

# Theorem 9.3

```
|- ∀ b u v. KL_divergence b u v =
SIGMA (λx. u { x } logr b (u { x } / v { x })) s
```

Some other formally verified properties of DKL in HOL4 are

```
|- ∀ b u. KL_divergence b u u = 0
```

```
|- ∀ b u v. 1 ≤ b ⇒ 0 ≤ KL_divergence b u v
```

The non-negativity of the KL divergence for absolutely continuous probability measures over finite spaces is extensively used to prove the properties of information theory measures like the mutual information and entropy. Next, we present the use of the KL divergence to formalize the mutual information, Shannon entropy, conditional entropy and the conditional mutual information, which are some of the most commonly used measures of information.

# 9.3 FORMALIZATION OF MUTUAL INFORMATION

The mutual information I (X; Y) of two random variables is a measure of the mutual dependence of the two random variables in the sense that it measures how much uncertainty about one of these variables is reduced when the other variable is known. The mutual information is usually used as a measure of information leakage from the secure inputs X of a program to its public outputs Y. It is defined as the KL divergence between the joint distribution and the product of marginal distributions. The following is a formalization of the mutual information in HOL.

# Definition 9.3

```
|- ∀ X Y. I (X ; Y) = KL_divergence b (joint_distribution p X Y)
prod_measure (distribution p X) (distribution p Y)
```

Various properties of the mutual information have been verified in HOL, such as the non-negativity, symmetry and reduced expression for finite spaces, using the result that the joint distribution is absolutely continuous w.r.t the product of marginal distributions.