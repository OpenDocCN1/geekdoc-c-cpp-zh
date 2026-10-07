# Alternative Clustering Analysis: A Review

mining and digamos. In Section 21.3.1, we present a taxonomy of alternative clustering techniques and discuss different methods of evaluation. In Sections 21.3.2,21.3.3, 21.3.4 and 21.3.5, we review specific approaches for alternative clustering. In Section 21.4, we compare the areas of multiew clustering and subspace clustering to alternative clustering and identify similarities and dissimilarities. In Sections 21.5 and 21.6 we outline future directions and conclusion.

# 21.2 Technical Preliminaries

Let $D$ be a dataset containing $N$ objects $o_1,\dots,o_N$ and using $n$ features $F_1,\dots,F_n$. A (hard) clustering $C^$ is a partition of the objects in $D$ into $k$ clusters $\{c_1,\dots,c_k\}$, where each cluster is a set of objects and $c_i\cap c_j=0$. The universe of all clusterings of $D$ is denoted by $C_D$. We will also use the notation $C_c$ to refer to cluster $c$ of clustering $C$.

The quality of a clustering may be measured using a function Quality $Q: C_D \rightarrow [0,1]$ where higher values indicate higher quality. A large range of quality measures have been defined, with well-known examples like the Dunn Index [13], Davies-Bouldin Index [12], and the Silhouette Width [34].

Let $C_1=\{c_1,\dots,c_k\}$ and $C_2=\{c'_1,\dots,c'_l\}$ be two clusterings of $D$. The similarity between $C_1$ and $C_2$ may be measured using a function $Sim: C_D \times C_D \rightarrow [0,1]$ where higher values indicate higher similarity. For measuring similarity, there are a number of measures, including the Rand Index [33], Adjusted Rand Index [21], Jaccard Index [18], Normalized Mutual Information [24], and Adjusted Mutual Information [36]. Measuring similarity between clusterings is important, since it provides insight for the user in the relationship between them. When managing multiple clustering, assessment of similarity may allow removal of redundant clusters, selection of interesting clusters, or increased understanding about clustering evolution. It is a key step when exploring the convergence properties of a clustering algorithm or assessing its output compared to an expert generated clustering.

Given the large range of measures that can be "plugged in" for measuring quality and similarity, appropriate choices are made in an application dependent way. We will shortly describe the issues involved in generating alternative clusters and the different dimensions along which the existing algorithms may be. A general description of the tasks is follows

Definition 21.1 Generalized Alternative Clustering: Given a empty collection of clusters $K=\{C_1,\dots,C_m\}$ provided as background knowledge (either $K=0$, or $K\neq0$ and $m\geq 1$), generate alternative clustering(s) $O=\{C_{m+1},\dots,C_{m+j}\}$, such that $i$\sum_{i=m+1}^{m+j}Quality(C_i)$ is maximized and $\sum_{i=1}^mSim(C_i,C_j)$ is minimized.

The task here corresponds to generating a set of (alternative) clusters, where each individual is of high quality and also the pairwise similarity between the clusterings is low. Three common cases are

+   * $|K|=1$ and $|O|=1$: singular alternative clustering

+   * $|K=0$ and $|O|=2$: clusters are generated in parallel: simultaneous alternative clustering

+   * $|K|>1$ and $|O|=1$: sequential alternative clustering

> $1It is also possible to use fuzzy clustering as the basis for development, but the literature on alternative fuzzy clustering is less mature and we concentrate on the hard case.

© 2014 by Taylor & Francis Group, LLC