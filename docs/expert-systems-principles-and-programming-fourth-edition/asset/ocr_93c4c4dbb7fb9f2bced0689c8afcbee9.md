(2) P(H | E ∩ e) = \frac{P(H | E ∩ e) P(E ∩ e)}{P(e)}

and since:

P(E | e) = \frac{P(E ∩ e)}{P(e)}

then (2) becomes:

P(H | E ∩ e) = P(H | E ∩ e) P(E | e)

Likewise:

P(H | E' | e) = P(H | E' ∩ e) P(E' | e)

and (1) becomes:

(3) P(H | e) = P(H | E ∩ e) P(E | e) + P(H | E' ∩ e) P(E' | e)

Normally, we do not know the probabilities P(H | E ∩ e) and P(H | E' ∩ e). However, if we assume these can be approximated by P(H | E) and P(H | E'), then (3) simplifies to:

(4) P(H | e) = P(H | E) P(E | e) + P(H | E') P(E' | e)

Equation (4) is essentially a linear interpolation of P(H | e) vs. P(E | e). The endpoints are:

+   (i) E is true and so P(H | e) = P(H | E).
+   (ii) E is false and so P(H | e) = P(H | E').

The problem with equation (4) shows up when P(E | e) equals the prior probability P(E). If the system obeys pure Bayesian probability, then:

(5) P(H | e) = P(H | E) P(E) + P(H | E') P(E')
(6) P(H | e) = P(H)

which is correct.

However, in the real world, experience has shown that human experts give subjective probabilities that are almost certain to be inconsistent. For example, if the expert uses the inconsistent case of LS > 1 and LN = 1, then:

O(H | E') = LN O(H) = O(H)