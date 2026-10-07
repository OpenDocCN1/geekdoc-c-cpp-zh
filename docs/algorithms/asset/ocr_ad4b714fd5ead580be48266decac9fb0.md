# Figure 9.6 (a) Four centers chosen by farthest-first traversal. (b) The resulting clusters.

![](bbox=[0.298, 0.151, 0.936, 0.276])

Here’s the argument. Let $x \in X$ be the point farthest from $\mu_1, \dots, \mu_k$ (in other words the next center we would have chosen, if we wanted $k+1$ of them), and let $r$ be the distance to its closest center. Every point in $X$ must be within distance $r$ of its cluster center. By the triangle inequality, this means that every cluster has diameter at most $2r$.

But does $r$ relate to the diameter of the optimal clustering? Well, we have identified $k+1$ points $\{\mu_1, \mu_2, \dots, \mu_k, x\}$ that are all at a distance $r$ from each other (why?). Any partition into $k$ clusters must put two of these points in the same cluster and must therefore have diameter at least $r$.

This algorithm has a certain high-level similarity to our scheme for VERTEX COVER. Instead of a maximal matching, we use a easily computable scheme—a set of $k$ points that cover all of $X$ within some radius $r$, and at the same time being mutually separated by a distance of at least $r$. This structure is used to generate a clustering and to give a lower bound on the optimal clustering.

We know of no better approximation algorithm for this problem.

# 9.2.3 TSP

The triangle inequality played a crucial role in making the $k$-CLUSTER problem approximation. It also helps with the TRAVELING SALESMAN PROBLEM: if the distances between cities satisfy the metric properties, then there is an algorithm that outputs a tour of length at most 1.5 times optimal. We’ll now look at a slightly weaker result that achieves a factor of 2.

Continuing with the thoughts of our two approximation algorithms, we can ask whether there is some structure that is easy to compute and that is plausibly related to the best traveling salesman tour (as well as providing a good lower bound on OPT). A little thought and experimentation reveals the answer to be the minimum spanning tree.