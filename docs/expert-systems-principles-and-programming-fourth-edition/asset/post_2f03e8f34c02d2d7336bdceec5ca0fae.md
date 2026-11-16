
choice should be made. However, unless the designers of the inference engine have been careful, the choice may be deterministic in a sense because it depends on the entry of the rule. This may come about because the designers of the inference engine used a stack or queue to store rules on the agenda. For an arbitrary choice of equally prioritized rules, there really should be a random choice from the stack or queue. Instead, the designers may simply take the easy way out and pop the stack or take the next rule from the queue. This selection method is easy but introduces a known artifact into the system because the choice of equally prioritized rules is not arbitrary.

## Subsumption and Uncertainty

The problem of subsumption becomes more uncertain if there are likelihoods associated with the rules, as in:

- (6) IF E1 THEN H with LS1
- (7) IF E1 AND E2 THEN H with LS2

For example, consider the following rules:

```
IF the starter motor doesn't work
THEN check the battery with LS1 = 5
IF the starter motor doesn't work AND
the lights don't work
THEN check the battery with LS2 = 10
```

where LS2 is greater than LS1, because of more evidence supporting the conclusion.

From Chapter 4, the posterior odds formula:

```
(8) O(H | E) = [\prod_{i=1}^N LS_i] O(H)
```

means that the product is 5 * 10 = 50, if both E1 and E2 are observed.

However, (8) was really meant to describe rules whose evidence combines independently. The antecedents of (6) and (7) are not really independent because they share evidence E1, in common. Thus, E1 AND E2, subsume E1, because E1 alone is a special case of E1, AND E2. The product of the likelihood ratios LS1 and LS2, is thus erroneously high because the antecedents are not independent. A solution is to replace LS1 by the ratio LS1 / LS, so that when both E1 and E2 exist, the correct product LS1 is computed. It may be hard to detect subsumption manually in a large knowledge base.

A third cause of uncertainty is redundant rules, which have the same consequent and evidence. Generally, these are accidentally entered by the knowledge engineer or accidentally occur when a rule is modified by pattern deletion. For example,

```
IF E1 AND E2 THEN H
```

```
IF E2 AND E1 AND E3 THEN H
```

are redundant rules if E3 is deleted since the antecedents are the same pattern. Deciding which redundant rule to delete is not necessarily simple. One redundant rule may lead to greater system efficiency if a rare pattern is listed first. The inference engine may not need to check the second pattern for a match if the first pattern fails to match. A further complication arises in expert system shells such as OPS5, in which the order of activation depends on the user-selected control strategy. Like the case of subsumption, redundant rules also give an erroneously high product of the likelihood ratio.

The fourth cause of uncertainty in rule consequents arises from missing rules, which occurs if the human expert forgets or is unaware of a rule such as:

```
IF E4 THEN H
```

If evidence E4 is ignored, then H is not concluded with the strength it deserves. One advantage of an inference network such as PROSPECTOR is the explicit nature of the network, which makes it easy to identify hypotheses that are impossible or difficult to achieve. If there are missing rules, the inference net may imply the need for these rules.

The fifth cause of uncertainty occurs because of problems with data fusion. This term refers to the uncertainty associated with fusing data from different types of information. For example, in making a diagnosis, a physician may consider evidence from widely different sources such as a physical exam, lab tests, patient history, socioeconomic environment, mental and emotional states, family and job problems, and so forth. These are all different types of evidence that must be fused to support a final hypothesis. The fusion of this evidence from so many different sources is much more difficult than evidence in one domain such as geology.

Likewise, a business decision may depend on the market for goods, economic conditions, foreign trade, takeover attempts, company politics, personal problems, unions, and many other factors. As with the medical problem, it is very difficult to assign likelihood ratios to all these factors and determine a reasonable combining function.

## 5.3 CERTAINTY FACTORS

Another method of dealing with uncertainty uses certainty factors, originally developed for the MYCIN expert system.

### Difficulties with the Bayesian Method

Like the geological problem addressed by PROSPECTOR, medical diagnosis is almost always subject to uncertainty. The major difference is that there are a limited number of geologic hypotheses about minerals since there are only 92 natural elements. Possible disease hypotheses are much greater because there are many more pathogens.

While Bayes' Theorem is useful in medicine, its accurate use depends on knowing many probabilities. For example, Bayes' Theorem may be used to determine the probability of a specific disease, given certain symptoms as:

P ( D_i | E ) = \frac{P ( E | D_i ) P ( D_i )}{P ( E )} = \frac{P ( E | D_i ) P ( D_i )}{\sum_j P ( E | D_j ) P ( D_j )}

- D_i is the i'th disease,
- E is the evidence,
- P(D_i) is the prior probability of the patient having the Disease; before any evidence is known,
- P(E | D_i) is the conditional probability that the patient will exhibit evidence E, given that disease D_i is present.

It is usually impossible to determine consistent and complete values for all these probabilities for the general population.

In practice, evidence tends to accumulate piece by piece. This accumulation costs considerable time and expense, especially when medical tests are involved. These factors of time, cost, and potential risk to the patient usually limit the number of tests performed to a minimum required for a good diagnosis (and malpractice protection).

A convenient form of Bayes' Theorem that expresses the accumulation of incremental evidence like this is (see Problem 5.1):

P ( D_1 | E ) = \frac{\sum_j P ( E_2 | D_1 \cap E_1 ) P ( D_1 | E_1 )}{\sum_j P ( E_2 | D_j \cap E_1 ) P ( D_j | E_1 )}

where E_2 is the new evidence added to the existing body of evidence, E_1, to yield the new augmented evidence:
E = E_1 \cap E_2.

Although this formula is exact, all these probabilities are not generally known. Also, the situation grows much worse as more pieces of evidence accumulate and so more probabilities are required.

Besides the problem of amassing all the conditional probabilities for the Bayesian method, another major problem that appeared with medical experts was the relationship of belief and disbelief. At first sight this may appear trivial, since obviously disbelief is simply the opposite of belief. In fact, the theory of probability states that:

```
P(H) + P(H') = 1
```

and so:

```
P(H) = 1 - P(H')
```

For the case of a posterior hypothesis that relies on evidence, E:

```
(1) P(H | E) = 1 - P(H' | E)
```

However, when the MYCIN knowledge engineers began interviewing medical experts, they found that physicians were extremely reluctant to state their knowledge in the form of equation (1).

For example, consider a MYCIN rule such as the following:

```
IF 1) The stain of the organism is gram positive,
and
2) The morphology of the organism is coccus,
and
3) The growth conformation of the organism is chains
THEN There is suggestive evidence (0.7) that the identity of the organism is streptococcus
```

In simple terms, this rule says that if a bacterial organism becomes colored when treated with Gram's stain and resembles chains of spheres, then there is a 70 percent likelihood that it is a type named streptococcus. This can be written in terms of posterior probability as:

```
(2) P(H | E1 ∩ E2 ∩ E3) = 0.7
```

where the Ei correspond to the three patterns of the antecedent.

The MYCIN knowledge engineers found that while an expert would agree to equation (2), they became uneasy and refused to agree with the probabilistic result:

```
(3) P(H' | E1 ∩ E2 ∩ E3) = 1 - 0.7 = 0.3
```

This reluctance by the experts to agree to equation (3) illustrates again that these numbers such as 0.7 and 0.3 are likelihoods of belief, not probabilities.

In order to fully appreciate this problem of inconsistent belief and disbelief, consider the following example. Suppose this is your last course required for a degree. Assume your grade point average (GPA) has not been too good and you
