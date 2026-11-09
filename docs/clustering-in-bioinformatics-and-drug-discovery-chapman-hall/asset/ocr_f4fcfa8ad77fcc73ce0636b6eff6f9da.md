for positive integers, p, q, and n. This is a sequence of rational numbers called the Farey sequence of order n. For large n, the expected value of Fₙ is

$\frac{3n^2}{\pi^2}+O(n\log n)$.  (12.20)

This remarkable result relates π to reduced proper fractions. In fact, it can be easily shown from this result that the probability of any two integers being coprime is

$\frac{6}{\pi^2}\approx 0.608\approx\frac{3}{5}$.  (12.21)

Thus, roughly three fifths of the set of proper fractions $p/q$, where $p<q$, $q\le n$, for large n are fully reduced fractions and the remainder reduce to one of these fully reduced fractions. (the probability that any three integers are relatively prime is given by Apéry’s constant ~ (approximately 0.832)). Given rational similarity measures, it is important to keep this fact in mind, as it may have a bearing on the form of the distribution of the similarity values, where low order fractions (e.g. 1/9, 1/2, 1/3, 1/4, etc.) are more prominent in the distribution than would be our natural expectation.

These distributions have fractal properties (ruler pattern plot) as do other prime number distributions (Ulam’s square). Other curious relationships to $\frac{6}{\pi^2}$ are:

$\frac{6}{\pi^2}=\sum_{n=1}^{\infty}\mu(n)n^{-2}$  (12.22)

$=P((m,n)\text{ are coprime}\mid m,n\in\mathbb{N})$  (12.23)

$=P(n\text{ is square free}\mid n\in\mathbb{N})$  (12.24)

$=\left(\prod_{p=2}^{\infty}(1-p^{-2})\right)^{-1}$  (12.25)

$=\sum_{n=1}^{\infty}\mu(n)n^{-2}$  (12.26)

Equation 12.22 is Riemann’s zeta function, ζ(2). A square free number has no power greater than 1 in its prime factorization (e.g. 2 × 3 × 5 = 30 is square free; 2 × 3² = 18 is not). The expression in 12.25, the ∏ refers to prime numbers. In Equation 12.26, μ(n) is the mobius function: μ(n) = 0, if n has a square factor, else 1 if n has an even number of prime factors, and −1 otherwise.

As simple to state as the Farey sequence is, it can be used to state the Riemann hypothesis. Let the total number of fractions in the Farey sequence of order n equal K (namely, it can be determined exactly, but it is approximately on average related to the expression 12.23). For each Farey number in sequence they are ranked ordered), fit the Farey number, take the absolute difference