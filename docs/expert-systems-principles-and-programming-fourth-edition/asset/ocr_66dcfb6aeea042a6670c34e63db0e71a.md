# Difficulties with Certainty Factors

Although MYCIN was very successful in diagnosis, there were difficulties with the theoretical foundations of certainty factors. While certainty factors had some basis in both probability theory and confirmation theory, the CF were also partly ad hoc. The major advantage of CF was the simple computations by which certainty could be propagated in the system. The CF were also easy to understand and clearly separated belief from disbelief.

However, there were problems with CF. One problem was that the CF values could be the opposite of conditional probabilities. For example, if:

P (H1) = 0.8 P (H2) = 0.2
P (H1 | E) = 0.9 P (H2 | E) = 0.8

then:

CF (H1, E) = 0.5 and CF (H2, E) = 0.75

Since one purpose of CF is to rank hypotheses in terms of likely diagnosis, it is a contradiction for a disease to have a higher conditional probability P(H | E) and yet have a lower certainty factor, CF(H, E).

The second major problem with CF is that in general:

P (H | e) ≠ P (H | i) P (i | e)

where i is some intermediate hypothesis based on evidence e, and yet the certainty factor of two rules in an inference chain is calculated as independent probabilities by:

CF (H, e) = CF (H, i) : CF (i, e)

The above formula is only true in the special case that the statistical population with property H is contained in the population with property i, and that is contained in the population with property e. The success of MYCIN in spite of these problems is probably due to the short inference chains and simple hypotheses. There could be real problems in applying certainty factors to other domains that did not have short inference chains and simple hypotheses. In fact, Adams demonstrated that the theory of certainty factors is really an approximation to standard probability theory.

# 5.4 DEMPSTER-SHAFER THEORY

In this section, we will discuss a method of inexact reasoning called the Dempster-Shafer theory or Shafer-Dempster theory. It is based on work done originally by Dempster, who attempted to model uncertainty by a range of probabilities rather than as a single probabilistic number. Shafer later extended and refined Dempster's work in a book published in 1976 called A