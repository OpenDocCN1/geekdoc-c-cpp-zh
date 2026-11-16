![](bbox=[0.156, 0.085, 0.715, 0.135])

| P(F = yes) = .6 | P(D = low | F = yes) = .2 | P(E = yes | D = low) = .7 |
| P(F = no) = .4 | P(D = medium | F = yes) = .4 | P(E = no | D = low) = .3 |
| | P(D = high | F = yes) = .4 | P(E = yes | D = medium) = .2 |
| | P(D = low | F = no) = .3 | P(E = no | D = medium) = .8 |
| | P(D = medium | F = no) = .2 | P(E = yes | D = high) = .1 |
| | P(D = high | F = no) = .5 | P(E = no | D = high) = .9 |

**Figure 7.7** The probability distribution in this Bayesian network is faithful to the DAG in the network.

X has a causal influence on Z through Y. However, in a manipulation study, Merck found that F does not appear to have a causal influence on E. That is, they learned $I_P(E, F)$. The explanation for this is that finasteride does not lower dihydro-testosterone levels beneath some threshold level, and that threshold level is all that is necessary for erectile function. The numbers we assigned in the Bayesian network in Figure 7.6 reflect these causal relationships. The value of F has no effect on whether D is low, and D must be low to make the probability that E is yes high.

# ## 7.2.2 Faithfulness Condition

The probability distribution in the Bayesian network in Figure 7.6 is said to be unfaithful to the DAG in that figure because it contains a conditional independency that is not entailed by the Markov condition. We have the following definition:

**Definition 7.4** Suppose we have a joint probability distribution P of the random variables in some set V and a DAG G = (V, E). We say that (G, P) satisfies the **faithfulness condition** if all and only the conditional independencies in P are entailed by G. Furthermore, we say that P and G are faithful to each other.$\blacklozenge$

Notice that the faithfulness condition includes the Markov condition because *only* conditional independencies in P can be entailed by G. However, it requires more; that is, it requires that *all* conditional independencies in P must be entailed by G. As noted previously, almost all assignments of values to the conditional distributions will result in a faithful distribution. For example, it is left as an exercise to show that the probability distribution P in the Bayesian network in Figure 7.7 is faithful to the DAG in that figure. We arbitrarily assigned values to the conditional distributions in the figure. However, owing to the result in [Meek, 1995] that almost all assignments of values to the con-