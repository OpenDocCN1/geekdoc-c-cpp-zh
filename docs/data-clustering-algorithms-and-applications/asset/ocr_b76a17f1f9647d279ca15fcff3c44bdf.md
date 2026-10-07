# Spectral Clustering

# Normalized Spectral Clustering (random walk version)

+   1. Construct similarity by graph of one the methods described in Section 8.2. Let W be the adjacency matrix and D be the degree matrix.

+   2. Compute unnormalized graph Laplacian where L = D - W.

+   3. Find f1, f2, ..., fk, the top k eigenvectors of the generalized eigenproblem Lf = λDf.

+   4. Form the matrix F ∈ Rn×k from f1, f2, ..., fk.

+   5. Treat each row of F as a vertex in Rk, partition these vertices into k clusters using k-means algorithm.

# 8.5 Graph Cut View

In the last two, we introduced the definitions for different formulations of graph Laplacians and specific procedures for all kinds of spectral clustering algorithms. Although we have analyzed the spectrum of both normalized and normalized Laplacian matrices, the intuition behind the graph Laplacians is not clear. Therefore, in this section, the spectral clustering method will be presented from the perspective of graph cut.

Given a graph G = (V, E), suppose we have two subsets of vertices A1, A2, satisfying A1 ∩ A2 = 0 and A1 ∪ A2 ⊆ V. We then introduce the definition of the cut as the sum of weights of the edges across the two subsets:

> cut(A1, A2) = ∑_{v∈A1,u∈A2} Wij

Here, Wij is the weight of the edge between vertices i and j. It is evident that the cut describes the closeness between these two subsets in graph. In other words, a smaller value of the cut indicates greater separation of the two subsets.

In graph theory, a minimum Min cut (MinCut) of a graph is a cut with the condition A1 ∪ A2 = V. This is the most direct way to construct the partition. MinCut may be a classical problem in the literature and relatively easy to solve. More details of MinCut may be found in [49].

By extending the cut from two sets to the multi-set situation, we can reformulate the cut follows:

> cut(A1, A2, ..., Ak) = ∑_{i=1} cut(Ai, Ā)

where Ā stands for the set of vertices {v|v ∉ Ai}.

Although MinCut is an intuitive way to partition the graph, it suffers from a critical problem, in many cases, MinCut separates an individual vertex or a small set of vertices from the remaining graph, overlooking the balance between the sizes of different partitions. Some normalization strategies can be incorporated into the objective function of MinCut to circumvent this problem. Two examples of such normalized objective functions are the Ratio Cut (RatioCut) [19] and Normalized Cut (NC) [43].