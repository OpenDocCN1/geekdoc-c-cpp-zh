# Simple Additive Weighting

Criterion_j is k times as important as Criterion_i, then Criterion_j is 1/k, the reciprocal, times as important as Criterion_i.

Begin with comparing cost to the other criteria.

| to | Cost | City | Hwy | Perform. | Style | Safety | Reliable |
|---|---:|---:|---:|---:|---:|---:|---:|
| Cost | 1 | 4 | 5 | 3 | 7 | 2 | 3 |

Make all the pairwise assessments creating an upper triangular *comparison matrix*.

| to | Cost | City | Hwy | Perform. | Style | Safety | Reliable |
|---|---:|---:|---:|---:|---:|---:|---:|
| Cost | 1 | 4 | 5 | 3 | 7 | 2 | 3 |
| City |  | 1 | 3 | 1/2 | 6 | 1/3 | 1/3 |
| Hwy |  |  | 1 | 1/4 | 3 | 1/4 | 1/4 |
| Perform. |  |  |  | 1 | 6 | 1/2 | 1/2 |
| Style |  |  |  |  | 1 | 1/6 | 1/5 |
| Safety |  |  |  |  |  | 1 | 2 |
| Reliable |  |  |  |  |  |  | 1 |

Note that if cost is 3 (*weakly more important*) to performance, then performance is 1/3, the reciprocal value, to cost. Use reciprocals to fill in the lower triangle of the matrix, so that if m_ij = k, then m_ji = 1/k.

| to | Cost | City | Hwy | Perform. | Style | Safety | Reliable |
|---|---:|---:|---:|---:|---:|---:|---:|
| Cost | 1 | 4 | 5 | 3 | 7 | 2 | 3 |
| City | 1/4 | 1 | 3 | 1/2 | 6 | 1/3 | 1/3 |
| Hwy | 1/5 | 1/3 | 1 | 1/4 | 3 | 1/4 | 1/4 |
| Perform. | 1/3 | 2 | 4 | 1 | 6 | 1/2 | 1/2 |
| Style | 1/7 | 1/6 | 1/3 | 1/6 | 1 | 1/6 | 1/5 |
| Safety | 1/2 | 3 | 4 | 2 | 6 | 1 | 2 |
| Reliable | 1/3 | 3 | 4 | 2 | 5 | 1/2 | 1 |

A comparison matrix is a *positive reciprocal matrix*. This type of matrix has a dominant positive eigenvalue and eigenvector. That eigenvector will be our weighting vector. The *SAW* program will compute (approximate) the weighting vector from a comparison matrix using an abbreviated power method.

We must ensure that the comparison assessments are consistent; i.e., if a is preferred to b and b is preferred to c, then a is preferred to c; according to Saaty’s scheme, compute the consistency ratio CR as a test. The value of CR must be less than or equal to 0.1 to be considered consistent. If CR > 0.1, the preference choices must be revisited and adjusted. First compute the largest eigenvalue λ of the comparison matrix. Then calculate the consistency index CI

$$CI = \frac{\lambda - n}{n - 1}$$