have merging criterion such that they can only be used with metric measures. Other forms utilizing either weighted merging criteria or centroid merging criteria can fail to be monotonic. Monotonicity is a property of the hierarchy consistent with ultrametricity.

$$d[(u, v)] \leq d[w, (u, v)]$$  (6.4)

u and v are either groups or members. d is the merging criteria and w is another group or member. If Equation 6.4 does not hold, the clustering is not monotonic and crossovers can occur in the hierarchy.

# 6.2  Divisive

This chapter so far has only considered agglomerative algorithms, but there are methods which are hierarchical and divisive. Divisive algorithms begin with all data set members in one cluster and then divide the data from the top-down, recursively into smaller groups. These algorithms have the advantage a more global consideration of the data than agglomerative methods. The disadvantage of divisive algorithms are that they can be computationally more expensive if the entire hierarchy has to be created. Divisive algorithms can be used in drug discovery or bioinformatics applications if the entire hierarchy is not built. The requirement for level selection occur at a high level in the dendrogram. increases the efficiency of these algorithms to be linear to data set size, but the challenge is devising meaningful stopping criteria akin to level selection, such that the resulting groups have validity [5].

# 6.3  Glossary

+   - **chaining:** where an individual cluster is spread out in feature space versus spherical or near-spherical-like clusters
+   - **crossover:** condition where the merging criterion value of a child group is greater than its parent group within the hierarchy
+   - **merging criterion:** a quantitative expression used in an algorithm to join or merge groups or clusters
+   - **monotonicity:** the property of the entire hierarchy such that there are no crossovers, conforming with Equation 6.4