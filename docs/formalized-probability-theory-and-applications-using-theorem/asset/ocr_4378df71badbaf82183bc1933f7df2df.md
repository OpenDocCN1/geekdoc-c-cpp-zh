The proof of the last subgoal is based on the property that if \(A1 \subseteq A2\) then \(Pr [ A1 ] \leq Pr [ A2 ]\) and real analysis. Now the main proof goal can be discharged based on the above subgoals and the formally verified Chebychev's inequality in addition to some real analysis.

The proof script of the formalization of the Heavy Hitter problem presented in this section consists of approximately 530 lines of HOL4 code. The higher-order-logic theorem proving based probabilistic analysis approach can be applied for the algorithm analysis of many other problems, such as the hat-check problem, the hiring problem, the balls and bins problem, the longest streak of heads problem, the on-line hiring problem, the Chinese appetizer problem and the Quicksort algorithm.

# ## 5.4 FORMALIZATION OF CONDITIONAL PROBABILITIES

The notion of conditional probability involves the probability of an event, say A, given the information that an event B has occurred. In order to understand usage of conditional probability, consider the example of an integrated circuit testing process where we test circuits in pairs. The concept of conditional probability allows us to compute the probability of correctness of two integrated circuits given that the first integrated circuit in the pair was found to be faultless. It is important to note that this probability would be different than the probability of both integrated circuits being accepted if no information about the first integrated circuit acceptance is given. This section provides a higher-order-logic formalization of the mathematical relationship for conditional probability and then utilizes this formal definition to verify some of its classical properties in the HOL4 theorem prover. The properties are explained in detail along with some hints on their verification to provide some insights about the formalization and verification process in HOL [Hasan, 2010b].

Conditional probability can be formally expressed in higher-order logic as follows:

# ### Definition 5.14

```
∀ ∀A B p. cond_prob p A B = prob p (A inter B) / prob p B
```

by inheriting the higher-order-logic formalization of the probability function described earlier. The function cond_prob accepts the probability space p and two sets A and B, corresponding to two events, and returns a real number that corresponds to the conditional probability of the first event A given the second event B. Using the above definition, we now verify most of the classical properties of conditional probabilities have been verified within the HOL4 theorem prover. The formal proofs for these properties not only ensure the correctness of the above mentioned condi-