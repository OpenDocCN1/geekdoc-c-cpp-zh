# Clustering Biological Data

# Algorithm 35 Generic Graph-Based Sequence Clustering

**Require:** Sequence database ($S$)
Similarity threshold ($\sigma$)
Cluster count ($k$)

```
1: $G(V,E) = \text{build-graph}(V=S,E=\emptyset)$$
2: for each edge $s_1 \in S$
3:   for each edge $s_2 \in S$
4:     if $\text{sim}(s_1,s_2) \geq \sigma$ and $s_1 \neq s_2$ then
5:       $E = E \\cup (s_1,s_2)$$
6:     end
7:   end
8: end for
9: $C = \text{graph-clustering}(G,k)$$
10: return $C$
```

construction, obtaining a parallel or distributed method for clustering graph is nontrivial. So, the method of choices chooses single-link clustering (SLC), which is an agglomerative clustering method that merges two of the clusters based on the largest similarity between a pair of sequences that are taken from those clusters. The complexity of SLC is $O(|n|^2)$, which is much cheaper than $O(|V|^2)$ for sparse graphs. While similarity graphs are very sparse, sparse clustering on graph is highly efficient. However, the clustering of SLC can be poor; for instance, it can happen that the distance of an object from another belonging to a different cluster can be smaller than the distance of the first object to another belonging to the same cluster.

One of the earliest sequence clustering methods that uses a graph-based technique is GeneRAGE [34]. It performs an all-against-all sequence search using BLAST; if between proteins is higher than a given threshold, an edge is added between two proteins in the similarity graph. Along this process, GeneRAGE also performs some preprocessing on the similarity graphs. For example, it identifies whether a protein is multidomain by considering the transitivity of similarity among other proteins that are similar to the same protein; if multidomain are found, they are allowed to belong to multiple clusters. For the clustering task, GeneRAGE uses SLC. Another clustering method, d2_cluster [17] also uses SLC for clustering EST (expressed sequence tags) and full-length cDNA sequences. In a recent work [73], Miele et al. proposed a memory-efficient implementation of SLC by following the well-known Union-Rank data structure for disjoint sets.

Kawaji et al. [60] mention the limitations of single-link clustering and use recursive graph partitioning to find clusters from the similarity graph. However, the balanced bipartite technique that uses a one-change optimization scheme, which is very costly. In [81], the authors use spectral clustering with the multilayer normalized criterion for clustering the similarity graph; however, as we mentioned earlier, spectral-based methods are not scalable because they require finding eigenvectors and eigenvalues of similarity matrix—a computationally intensive task. Another clustering method BAG [62] also uses partitioning of the similarity graph, but its partitioning is targeted to find connected components of the similarity graph. For building the similarity graph, BAG uses the FASTA algorithm in an efficient manner; for every sequence $i$: $1 \leq i \leq n$, it calls FASTA($s_i, S$) and finds the pair of similar sequences with only $O(n)$ number of FASTA calls, instead of $O(n^2)$ for such cases. Very recently, Voevovski et al. [108] proposed a method that finds the similarity graph with $k(<n)$ number of BLAST calls, the value of k following an active learning paradigm.

© 2014 by Taylor & Francis Group, LLC