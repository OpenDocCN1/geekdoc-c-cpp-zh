written f(1) + f(2) + ⋯ + f(n − 1) + f(n). Within a sentence, Sigma notation is typeset as ∑_{i=1}^{n} f(i).

Given a summation, you often wish to replace it with an algebraic equation with the same value as the summation. This is known as a closed-form solution, and the process of replacing the summation with its closed-form solution is known as solving the summation. For example, the summation ∑_{i=1}^{n} 1 is simply the expression “1” summed n times (remember that i ranges from 1 to n). Because the sum of n 1s is n, the closed-form solution is n. The following is a list of useful summations, along with their closed-form solutions.

∑_{i=1}^{n} i = n(n + 1)/2. (2.1)

∑_{i=1}^{n} i² = (2n³ + 3n² + n)/6 = n(2n + 1)(n + 1)/6. (2.2)

∑_{i=1}^{log n} n = n log n. (2.3)

∑_{i=0}^{∞} a^i = 1/(1 − a) for 0 < a < 1. (2.4)

∑_{i=0}^{n} a^i = (a^{n+1} − 1)/(a − 1) for a ≠ 1. (2.5)

As special cases to Equation 2.5,

∑_{i=1}^{n} 1/2^i = 1 − 1/2^n. (2.6)

and

∑_{i=0}^{n} 2^i = 2^{n+1} − 1. (2.7)

As a corollary to Equation 2.7,

∑_{i=0}^{log n} 2^i = 2^{log n +1} − 1 = 2n − 1. (2.8)

Finally,

∑_{i=1}^{n} i/2^i = 2 − (n + 2)/2^n. (2.9)

The sum of reciprocals from 1 to n, called the Harmonic Series and written ℋ_n, has a value between log_e n and log_e n + 1. To be more precise, as n grows, the