**Example 7.10.13** By Theorem 2.7.5, the $[(q^k - 1)/(q - 1), k, q^{k-1}]$ simplex code $\mathcal{C}$ over $\mathbb{F}_q$ meets the Griesmer Bound. So by Theorem 7.10.12, the weight hierarchy of $\mathcal{C}$ is

$$d_r(C) = \sum_{i=0}^{r-1} \left\lceil \frac{q^k - 1}{q^i} \right\rceil = \sum_{i=0}^{r-1} q^{k-i-1} = q^{k-r} \frac{q^r - 1}{q - 1}.$$

**Exercise 432** From Example 7.10.13, what is the weight hierarchy of:
(a) the [15, 4, 8] binary simplex code (see also Example 7.10.2), and
(b) the [121, 5, 81] ternary simplex code?

**Exercise 433** Using the results of Exercise 432 and Theorem 7.10.4, find the weight hierarchy of:
(a) the [15, 11, 3] binary Hamming code, and
(b) the [121, 116, 3] ternary Hamming code.

**Exercise 434** Using the results of Example 7.10.13 and Theorem 7.10.4, find the weight hierarchy of the $[(q^k - 1)/(q - 1), (q^k - 1)/(q - 1) - k, 3]$ Hamming code $\mathcal{H}_{q,k}$ over $\mathbb{F}_q$.

As remarked earlier, generalized MacWilliams equations for generalized Hamming weights have been established by Barg [14], Kløve [175], and Simonis [310]. We refer the interested reader to those papers for details.

The generalized Hamming weights have been computed for other codes. Wei [348] computed the weight hierarchy of the binary Reed-Muller codes of all orders and the Hamming codes; see Exercise 434 and Section 5 of [329]. (Note that even though the weight hierarchies of the binary Reed-Muller codes are known, the weight distributions of these codes are unknown for orders larger than 2.) The weight hierarchies are known for codes that meet the Griesmer Bound by Theorem 7.10.12; for codes that have length one more than the Griesmer Bound, the weight hierarchies are also known [127].¹

**Research Problem 7.10.14** For families of codes such as $BCH$, quadratic residue, $duadic$, or lexicodes, find further information, either exact or asymptotic, about some or all of the generalized Hamming weights.