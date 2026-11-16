![](bbox=[0.25, 0.08, 0.8, 0.35])

Figure 6.16 A Bayesian network. Each variable has only two possible values, so only the probability of one is shown.

After doing this computation, also computing \(P(w_1|y_2)\) (because X will need this value) and then determining \(P(y_1|w_1)\), we pass \(P(w_1|y_1)\) and \(P(w_1|y_2)\) to X. We then compute \(P(w_1|x_1)\) and \(P(x_1|w_1)\) in sequence:

```
P(w_1|x_1) = (P(w_1|y_1)P(y_1|x_1) + P(w_1|y_2)P(y_2|x_1)

P(x_1|w_1) = \frac{P(w_1|x_1)P(x_1)}{P(w_1)}.
```

It is left as an exercise to perform these computations. Clearly, this upward propagation scheme applies to an arbitrarily long linked list.

The next example shows how to turn corners in a tree.

**Example 6.12** Consider the Bayesian network in Figure 6.16. Suppose W is instantiated for \(w_1\). We compute \(P(y_1|w_1)\) followed by \(P(x_1|w_1)\) using the upward propagation algorithm just described. Then we proceed to compute \(P(z_1|w_1)\) followed by \(P(t_1|w_1)\) using the downward propagation algorithm. This is left as an exercise.

# 6.4.2 Inference Algorithms and Packages

By exploiting local independencies as we did in the previous subsection, Pearl [1986, 1988] developed a message-passing algorithm for inference in Bayesian networks. Based on a method originated in [Lauritzen and Spiegelhalter, 1988], Jensen et al. [1990] developed an inference algorithm that involves the extraction of an undirected triangulated graph from the DAG in a Bayesian network and the creation of a tree, whose vertices are the cliques of this triangulated