![](bbox=[0.28, 0.08, 0.76, 0.29])

Figure 6.10 A causal DAG representing a manipulation experiment.

other causal relationships. The causal DAG representing the manipulation just discussed appears in Figure 6.10.

# 6.3.2 Causality and the Markov Condition

First, we more rigorously define a causal DAG. After that, we state the causal Markov assumption and argue why it should be satisfied.

# 6.3.2.1 Causal DAGs

We say X is a cause of Y if a manipulation of X results in a change in the probability distribution of Y. A causal graph is a directed graph containing a set of causally related random variables V such that for every X, Y ∈ V there is an edge from X to Y if and only if X is a cause of Y, and there is no subset of variables W_XY of V such that if we knew the values of the variables in W_XY, a manipulation of X would no longer change the probability distribution of Y. If there is an edge from X to Y, we call X a direct cause of Y. Note that whether or not X is a direct cause of Y depends on the variables included in V. A causal graph is a causal DAG if the causal graph is acyclic (i.e., there are no causal feedback loops).

Example 6.4 Testosterone (T) is known to convert to dihydro-testosterone (D), and dihydro-testosterone is believed to be the hormone necessary for erectile function (E). A study in [Lugg et al., 1995] tested the causal relationship among these variables in rats. They manipulated testosterone to low levels and found that both dihydro-testosterone and erectile function declined. They then held dihydro-testosterone fixed at low levels and found that erectile function was low regardless of the manipulated value of testosterone. Finally, they held dihydro-testosterone fixed at high levels and found that erectile function was high regardless of the manipulated value of testosterone. So they learned that, in a causal graph containing only the variables T, D, and E, T is a direct cause