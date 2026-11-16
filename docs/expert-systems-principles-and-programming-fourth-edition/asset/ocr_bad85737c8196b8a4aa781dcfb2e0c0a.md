limited number of geologic hypotheses about minerals since there are only 92 natural elements. Possible disease hypotheses are much greater because there are many more pathogens.

While Bayes' Theorem is useful in medicine, its accurate use depends on knowing many probabilities. For example, Bayes' Theorem may be used to determine the probability of a specific disease, given certain symptoms as:

P ( D_i | E ) = \frac{P ( E | D_i ) P ( D_i )}{P ( E )} = \frac{P ( E | D_i ) P ( D_i )}{\sum_j P ( E | D_j ) P ( D_j )}

where the sum over j extends to all diseases, and:

+   - D_i is the i'th disease,
+   - E is the evidence,
+   - P(D_i) is the prior probability of the patient having the Disease; before any evidence is known,
+   - P(E | D_i) is the conditional probability that the patient will exhibit evidence E, given that disease D_i is present.

It is usually impossible to determine consistent and complete values for all these probabilities for the general population.

In practice, evidence tends to accumulate piece by piece. This accumulation costs considerable time and expense, especially when medical tests are involved. These factors of time, cost, and potential risk to the patient usually limit the number of tests performed to a minimum required for a good diagnosis (and malpractice protection.).

A convenient form of Bayes' Theorem that expresses the accumulation of incremental evidence like this is (see Problem 5.1):

P ( D_1 | E ) = \frac{\sum_j P ( E_2 | D_1 \cap E_1 ) P ( D_1 | E_1 )}{\sum_j P ( E_2 | D_j \cap E_1 ) P ( D_j | E_1 )}

where E_2 is the new evidence added to the existing body of evidence, E_1, to yield the new augmented evidence:
E = E_1 \cap E_2.

Although this formula is exact, all these probabilities are not generally known. Also, the situation grows much worse as more pieces of evidence accumulate and so more probabilities are required.

# Belief and Disbelief

Besides the problem of amassing all the conditional probabilities for the Bayesian method, another major problem that appeared with medical experts