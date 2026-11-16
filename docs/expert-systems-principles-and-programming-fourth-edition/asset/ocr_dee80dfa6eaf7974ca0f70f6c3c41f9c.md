Probabilities are generally used with deductive problems in which a number of different events, E_n, may occur given the same hypothesis. For example, given that a die rolls an even number, there are three possible events:

```
P(2 | even)
P(4 | even)
P(6 | even)
```

In probability, we are generally interested in P(E | H) where E, are the possible events from a common hypothesis. In statistics and inductive reasoning, we know the event that has occurred and want to find the likelihood of the hypothesis that can cause E, which is P(E | H). Probability is naturally forward chaining or deductive while likelihood is backward chaining and inductive. Although we use the same symbolism, P(X | Y), for probability and likelihood, the applications are different. Normally we refer to the likelihood of a hypothesis or the probability of an event

One theory that has been developed using degrees of belief is personal probability. In personal probability, states are the possible hypotheses and the consequences are the results of actions based on the beliefs.

# 4.12 SUFFICIENCY AND NECESSITY

Bayes' Theorem is:

```
(1) P(H | E) = P(E | H)P(H) / P(E)
```

and for the negation of H becomes:

```
(2) P(H' | E) = P(E | H')P(H') / P(E)
```

Dividing (1) by (2) gives:

```
(3) P(H | E) / P(H' | E) = P(E | H)P(H) / P(E | H')P(H')
```

Defining the prior odds on H as:

```
O(H) = P(H) / P(H')
```