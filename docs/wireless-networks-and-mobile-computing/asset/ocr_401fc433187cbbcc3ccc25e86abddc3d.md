# 3.4.1 Problem Formulation

Let us assume that the channel assignment problem is represented by a CAP graph and the frequency separation constraints are given by the matrix $C=(c_{ij})$ as described in Section 3.1.2. Suppose the CAP graph has $n$ nodes. A random order of these nodes is considered a string $S$ or chromosome. For example, $S=((20),(21),(10),(11),(00))$ is a string corresponding to the CAP graph of Figure 3.1(a). Let $M$ be the population size (we have taken $M$ as an even integer). Let $cp$ be the crossover probability. We set $cp$ to a high value, say 0.95, in the algorithm.

![](bbox=[0.25, 0.348, 0.747, 0.58])

**FIGURE 3.9:** Variation of mutation probability ($q$) with number of iterations ($t$)

Let $q$ be the mutation probability and $T$ be the total number of iterations. Usually, $T$ is a very large positive integer. We divide the total number of iterations into five equal intervals (assuming that $T$ is a multiple of 5) as $[0,T/5]$, $[T/5,2T/5]$, $[2T/5,3T/5]$, $[3T/5,4T/5]$ and $[4T/5,T]$. We start with a mutation probability of $q=0.5$ and then it is varied with the number of iterations as shown in Figure 3.9. The way in which the mutation probability is varied here is similar to that used in [48]. The reason for varying the mutation probability $q$ in this fashion is that we are to increase the value of $q$ to maintain the diversity of the