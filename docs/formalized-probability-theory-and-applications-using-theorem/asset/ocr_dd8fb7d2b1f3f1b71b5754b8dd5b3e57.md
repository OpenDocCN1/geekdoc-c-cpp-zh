For the special case when the sample space is finite, the definition of the expectation can be simplified to:

```
|- ∀ p X. FINITE (p_space p) ⇒
E [ X ] = SIGMA (λ x. r * distribution p X { r }) (IMAGE X
(p_space p))
```

We provide an alternative definition for the expectation of real-valued random variables. This formula is derived from Equation 4.5 and provides an easier way to compute the expectation of random variables without the need to work with integrals.

```
⊢ E[X] = sup_n Σ_{k=0}^{4^n-1} k/2^n × ( F_X((k+1)/2^n) - F_X(k/2^n) ) + 2^n × (1 - F_X(2^n)) (5.2)
```

# 5.2.2 Variance and Covariance

In the field of probabilistic analysis, it is often desirable to summarize the essential properties of distribution of a random variable by certain suitably defined measures. In the previous section, we formalized one such measure, i.e., the expectation, which yields the weighted average of the possible values of a random variable. Quite frequently, along with the average value, we are also interested in finding how typical is the average value or in other words the chances of observing an event far from the average. One possible way to measure the variation, or spread, of these values is to consider the quantity E|X - E[X]|, where |y| denote the abs value of y. However, it turns out to be mathematically inconvenient to deal with this quantity, so a more tractable quantity called variance is usually considered, which returns the expectation of the square of the difference between R and its expectation. Similarly, another closely related measure is the covariance, which is a measure of the correlation between two random variables. The covariance of two random variables X and Y is defined as Cov(X, Y) = E [ (X - E [ X ]) (Y - E [ Y ]) ]. Two random variables X and Y are uncorrelated iff Cov(X, Y) = 0.

Some of the formally verified properties for the variance and covariance include:

```
|- ∀ X. Var (X) = E [ X ^ 2 ] - E [ X ] ^ 2
|- ∀ X Y. Cov (X, Y) = E [ X Y ] - E [ X ] E [ Y ]
|- ∀ X. Var (X) ≥ 0
|- ∀ a ∈ R. Var (aX) = a^2 Var (X)
|- ∀ p X Y. Var (X+Y) = Var (X) + Var (Y) + 2 Cov(X,Y)
|- ∀ p XY. X and Y uncorrelated ⇒ Var (X + Y) = Var (X) + Var (Y)
```