$\Theta$ does not assign *any* value to the subsets of $\Theta$, even though the subsets include the hostile subsets ({B,F}, {B}, and {F}).

Going back to the student example of the last section,

m(getting an 'A' and graduating) = 0.7

would not automatically mean:

m(getting an 'A' and not graduating) = 0.3

unless both of these were assigned values.

A mass has considerably more freedom than probabilities, as Table 5.3 shows.

| Dempster-Shafer Theory | Probability Theory |
|---|---|
| m($\Theta$) does not have to be 1 | $\sum P_i = 1$ |
| If $X \subseteq Y$, it is not necessary that m(X) $\le$ m(Y) | P(X) $\le$ P(Y) |
| No required relationship between m(X) and m(X') | P(X) + P(X') = 1 |

Every mass can formally be expressed as a function that maps each element of the power set into a real number in the interval 0 to 1. This simply means that the belief in a subset may take any values from 0 to 1. This mapping is formally stated:

$m: \wp(\Theta) \rightarrow [0, 1]$

By convention, the mass of the empty set is usually defined as zero:

$m(\emptyset) = 0$

and the sum of all the masses for every subset, X, of the power set is 1:

$\sum_{X \subseteq \Theta} m(X) = 1$

For example, in the aircraft environment:

$\sum_{X \subseteq \Theta} m(X) = m(\{B,F\}) + m(\emptyset) = 0.7 + 0.3 = 1$