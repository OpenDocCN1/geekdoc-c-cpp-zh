# Density-Based Clustering

+   * How is connectivity defined?
* Which data structures support the efficient implementation of the algorithm?

In the following, we will present the main density-based clustering algorithms and discuss the ways in which they answer these questions.

# 5.2 DBSCAN

DBSCAN [11] estimates the density by the chain of the number of points in a fixed-radius neighborhood and considers two points as connected if they lie within each other's neighborhood. A point is core point if the neighborhood of radius Eps contains at least MinPts points, i.e., the density in the neighborhood has exceeded some threshold. A point *q* is density-reachable from a core point *p* if *q* is in the Eps-neighborhood of *p*, and density-reachability is given by the transitive closure of density-reachability. Two points *p* and *q* are called density-connected if there is a third point *o* from which *p* and *q* are density-reachable. Noise is defined as the set of points in the database not belonging to any of its clusters. The task of density-based clustering is to find all clusters with respect to parameters *Eps* and *MinPts* in a given database.

In the following we provide more formal definitions. Let *D* be a (database) of data points. The definition of density-based clustering is based on a distance metric *dist(p,q)* for pairs of points. The *Eps*-neighborhood of a point *p*, is denoted by *NEps(p)*, is defined by *NEps(p) = {q \in D | dist(p,q) ≤ Eps}*. *p* is density-reachable from a point *q* with respect to *Eps*, *MinPts* if (1) *p \in NEps(q)* and (2) *|NEps(q)| ≥ MinPts*. A point *p* is density-reachable from a point *q* with respect to *Eps* and *MinPts* if there is a chain of points *p_1, ..., p_n=q, p_n=p* such that *p_{i+1}* is directly density-reachable from *p_i* with respect to *Eps* and *MinPts*. Density-reachability is a canonical extension of direct density-reachability. Since this relation is not symmetric, another relation is introduced. A point *p* is density-connected to a point *q* with respect to *Eps* and *MinPts* if both *p* and *q* are density-reachable from *o* with respect to *Eps* and *MinPts*. Figure 5.2 illustrates these concepts. While *p* is density-reachable from *q*, *q* is not density-reachable from *p*. *a* and *c* are density-connected via *b*.

Intuitively, a density-based cluster is a maximal set of density-connected points. A cluster *C* with respect to *Eps* and *MinPts* is a nonempty subset of *D* satisfying the two conditions:

+   1. *∀p,q if p \in C* and *q* is density-reachable from *p* with respect to to *Eps* and *MinPts*, then *q \in C*. (maximality)

![](bbox=[0.205, 0.745, 0.792, 0.883])

FIGURE 5.2: Density-reachability and connectivity.