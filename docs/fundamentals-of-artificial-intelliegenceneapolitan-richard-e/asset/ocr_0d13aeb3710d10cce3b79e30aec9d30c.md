Test to D, the value of Test will be known when the decision is made. So we need to determine the expected value of U given each value of Test. We have

EU(d1|r1, positive) = E(U|r1, d1, positive)
= P(good|positive)U(r1, d1, good) +
P(bad|positive)U(r1, d1, bad)
= (.571429)($11,000) + (.429571)($8000)
= $9522

EU(d2|r1, positive) = E(U|r1, d2, positive)
= P(good|positive)U(r1, d2, good) +
P(bad|positive)U(r1, d2, bad)
= (.571429)($9800) + (.429571)($9800)
= $9800

EU(D|r1, positive) = max(EU(d1|r1, positive), EU(d2|r1, positive))
= max($9522, $9800) = $9800

EU(d1|r1, negative) = E(U|r1, d1, negative)
= P(good|negative)U(r1, d1, good) +
P(bad|negative)U(r1, d1, bad)
= (.965517)($10,800) + (.034483)($7800)
= $10,697

EU(d2|r1, negative) = E(U|r1, d2, negative)
= P(good|negative)U(r1, d2, good) +
P(bad|negative)U(r1, d2, bad)
= (.965517)($9800) + (.034483)($9800)
= $9800

EU(D|r1, negative) = max(EU(d1|r1, negative), EU(d2|r1, negative))
= max($10,697, $9800) = $10,697.

As before, the conditional probabilities are obtained from a Bayesian network inference algorithm. Once we have the expected utilities of D, we can compute the expected utility of R as follows:

EU(r1) = EU(D|r1, positive)P(positive) + EU(D|r1, negative)P(negative)
= $9800(.42) + $10,697(.58)
= $10,320.