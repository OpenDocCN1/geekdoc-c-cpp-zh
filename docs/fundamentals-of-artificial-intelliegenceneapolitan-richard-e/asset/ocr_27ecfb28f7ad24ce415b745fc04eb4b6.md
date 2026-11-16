and therefore

BIC (G_2 : D) = ln (P(D|\hat{\Phi}, G_2)) - \frac{d}{2} ln m
= ln (2.5292 \times 10^{-5}) - \frac{2}{2} ln 8
= -12.644.

Note that although the data were more probable given G_1, G_2 won because it is less complex.

Looking at Examples 13.3 and 13.4, we see that the Bayesian score and the BIC can choose different DAG models. The reason is that the data set is small. In the limit they will both choose the same DAG model because the BIC is asymptotically correct. A scoring criterion for DAG models is called **asymptotically correct** if for a sufficiently large data set it chooses the DAG that maximizes P(D|G).

# 13.2.3 Consistent Scoring Criteria

We have presented two methods for scoring DAG models. There are others, several of which are discussed in [Neapolitan, 2004]. The question remains as to the quality of these scores. The probability distribution generating the data is called the **generative distribution**. Our goal with a Bayesian network is to represent the generative distribution succinctly. A consistent scoring criterion will almost certainly do this if the data set is large. Specifically, we say a DAG **includes** a probability distribution P if every conditional independence entailed by the DAG is in P. A **consistent scoring criterion** for DAG models has the following two properties:

+   1. As the size of the data set approaches infinity, the probability approaches one that a DAG that includes P will score higher than a DAG that does not include P.

+   2. As the size of the data set approaches infinity, the probability approaches one that a smaller DAG that includes P will score higher than a larger DAG that includes P.

Both the Bayesian score and the BIC are consistent scoring criteria.

# 13.2.4 How Many DAGs Must We Score?

When there are not many variables, we can exhaustively score all possible DAGs. We then select the DAG(s) with the highest score. However, when the number of variables is not small, it is computationally unfeasible to find the maximizing DAGs by exhaustively considering all DAG patterns. That is, Robinson [1977] showed that the number of DAGs containing n nodes is given