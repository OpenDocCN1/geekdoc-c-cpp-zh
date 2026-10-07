# 9.2 Approximation algorithms

Let's consider the O(nV) algorithm. In the bad case when V is large, what if we simply scale down all the values in some way? For instance, if

$v_1 = 117,586.003, v_2 = 738,493,291, v_3 = 238,827,453,$

we could simply knock off some precision and instead use 117, 738, and 238. This doesn't change the problem that all will and make the large algorithm, much faster!

Now for the details. Along with the input, user is asked to specify some approximation factor $\epsilon > 0$.

+   Discard any item weight > W
Let $V_{max} = \max v_i$
Rescale values $	ilde{V}_i = [v_i - \frac{n}{\epsilon_{max}}]$

Run the dynamic programming algorithm with values $(	ilde{V}_i)$
Output the resulting choice of items

Let's see why this. With the rescaled $	ilde{V}_i$ are all at most $n/\epsilon$, the dynamic programming is efficient, running in time $O(n^3/\epsilon)$

Now suppose the optimal solution to the original problem is to pick some subset of items, with total value $K^*$. The approximation value of this assignment is

$\sum_{i \in S} \tilde{V}_i = \sum_{i \in S} [v_i - \frac{n}{\epsilon_{max}}] \geq \sum_{i \in S} (v_i - \frac{n}{\epsilon_{max}}) \geq K^* - \frac{n^2}{\epsilon_{max}} = n.$

of at least this. In the original values, assignment S has a value of at least

$\sum_{i \in S} \tilde{V}_i \geq \sum_{i \in S} [v_i - \frac{n}{\epsilon_{max}}] \geq K^* - \frac{n^2}{\epsilon_{max}} = K^* - \epsilon_{max} \cdot n \geq K^*(1 - \epsilon).$

# 9.2.5 Approximation hierarchy

Given any NP-complete optimization problem, we seek the best approximation possible. Failing this, we try to prove lower bounds on the approximations that are achievable in polynomial time (we just carried out such a proof for the general TSP). All told, NP-complete optimization problems are classified as follows:

+   For those with a large ratio, no finite approximation is possible, but there are limits to how small this can be.

+   For those where an approximation is possible, e.g., VERTEX COVER, K-CLUSTER, and the TSP with triangle inequality below here. (For problems we have not established limits to their approximation, these limits do exist, and their proofs constitute some of the most sophisticated results in this field).

+   Down below we have a more fortunate case of NP-complete problems for which approximation has no limits, and polynomial approximation algorithms with error ratios arbitrarily close to zero exist. KNAPSACK resides here.

24