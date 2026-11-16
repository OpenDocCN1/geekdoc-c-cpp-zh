![](bbox=[0.33, 0.07, 0.66, 0.34])

Figure 6.8 A Bayesian network representing the probability distribution P of the random variables L, S, and C defined on the set of objects in Figure 6.5.

There are a total of eight combinations. We show that the equality holds for one of them. It is left as an exercise to show that it holds for the others. To that end, we have directly from Figure 6.5 that

$P(s_1, l_1, c_1) = \frac{2}{13}$.

From Figure 6.8 we have

$P(s_1|c_1)P(l_1|c_1)P(c_1) = \frac{2}{3} \times \frac{1}{3} \times \frac{9}{13} = \frac{2}{13}$.

Owing to Theorem 6.1, we can represent a Bayesian network $(\mathbb{G}, P)$ using the DAG $\mathbb{G}$ and the conditional distributions. We do not need to show every value in the joint distributions. These values can all be computed from the conditional distributions. So we always show a Bayesian network as the DAG and the conditional distributions as we did in Figures 6.2, 6.3, and 6.8. Herein lies the representational power of Bayesian networks. If there are a large number of variables, there are many values in the joint distribution. However, if the DAG is sparse, there are relatively few values in the conditional distributions. For example, suppose all variables are binary, and a joint distribution satisfies the Markov condition with the DAG in Figure 6.9. Then there are $2^{10} = 1024$ values in the joint distribution, but only $2 + 2 + 8 \times 8 = 68$ values in the conditional distributions. Note that we are not even including redundant parameters in this count. For example, in the Bayesian network in Figure 6.8, it is not necessary to show $P(c_2) = 4/13$ because $P(c_2) = 1 - P(c_1)$. So we need only show $P(c_1) = 9/13$. If we eliminate redundant parameters, there are