
# Clustering Biological Data

The similarity between two sequences is measured using any metric that measures the similarity between two vectors, such as dot product, Euclidean distance, Jaccard coefficient, or even tf-idf [89]. This approach is also known as a keyword-based method, as one can consider each sequence as a document and each q-gram as a keyword in the document. The biggest advantage of similarity computation using a keyword-based method is that it is fast. Another advantage is that this method represents a sequence using an $\mathbb{R}^n$ vector, which can accommodate some of the clustering algorithms (such as, $k$-means) that work over vector-based data.

## 16.4.1.3 Kernel-Based Similarity

In recent years, kernel-based similarity metrics also got popular. In [67], the authors present several families of $k$-gram-based string kernels, such as restricted gamma kernels, substitution kernels, and wildcard kernels, all of which are based on feature spaces indexed by $k$-length subsequences ($k$-mers) from the string alphabet. Typically, kernels are used for supervised classification with support vector machines (SVM), however, they can also be used as a similarity metric for unsupervised clustering.

## 16.4.1.4 Model-Based Similarity

Probabilistic models, such as HMM, are here used for finding similarity metrics. For a given set of sequences to be clustered, such method trains an HMM for each of the sequences. Then, the similarity between two sequences can be obtained from the similarity (or distance) between the corresponding HMMs. In the past, few authors have proposed approaches for computing the distance between two HMMs [86]; early approaches were based on the Euclidean distance of the discrete observation probability, others on co-emission probability of two HMM models, or on Bayes probability of error [10].

## 16.4.2 Sequence Clustering Algorithms

In an earlier section, we discussed that given a similarity metric, we can use any clustering method for clustering biological sequences. Nevertheless, there have been many clustering methods that are explicitly proposed for clustering biological sequences. We discuss them under the following.

### 16.4.2.1 Subsequence-Based Clustering

A subsequence-based clustering method mines a set of frequent subsequences from each of the sequences and uses them as features for clustering the sequences. The idea of clustering is similar to the task of document clustering using the "bag-of-words" representation of a document. A traditional sequence mining method returns a large number of subsequences that are frequent, but all such subsequences are not good features for clustering. So, a good clustering method needs to choose a subset of these subsequences as features when projected on the feature-similarity between a pair of sequences is computed. Different algorithms of sequence clustering vary in way they choose the subsequence feature set. The advantages of subsequence-based clustering methods is that they are typically fast compared to other clustering methods. However, this approach ignores the relative position of various subsequences, so they cannot model some of the relations, such as ordering and sequential dependency.

One of the first subsequence-based sequence clustering methods was proposed by Gulnik and Karypis [45]. They used traditional frequent sequence mining methods [121] to mine subsequences, but to control the number of subsequences, they imposed minimum and maximum length constraint on the mined subsequences; then they used a subset of the mined subsequences as the feature set for clustering. To select the feature set, they followed two approaches: global and local. The global approach prunes the feature space by selecting a set of independent subsequences, where dependency is defined as the overlap between the sequences or as the overlap of their support locally from each of the sequences. On the other hand, the local approach finds independent features which are independent if they are supported by a non-overlapping segment of the corresponding sequences. Once the feature set is defined, they use a k-means algorithm to cluster the sequences.

A more sophisticated variant of the subsequence-based method was proposed in [111]. In this paper, the authors introduce the notion of frequent subsequence (FSS) and represent each sequence by a collection of those FSSs. Intuitively, an FSS is a keyword that can be viewed as a discriminating feature for clustering the input data sequences. However, in this, the authors use a tf-idf kind of weighting to assign to each of these FSSs. They also present an effective method that mines all the FSSs from the sequence data. The final clustering has two stages. The first stage generates microclusters by roughly grouping the sequences with a shared FSS. Typically, the number of microclusters is larger than the desired number of clusters, so a second stage is used to merge the microclusters using a hierarchical clustering method, until the desired number of clusters is obtained.

### 16.4.2.2 Graph-Based Clustering

A graph-based sequence clustering method represents the sequences in a similarity graph, where a vertex represents a sequence and an edge represents the similarity relation between the corresponding pair of sequences. In such representation, a partition of the similarity graph represents the clustering of the input sequences. The crucial requirement in a graph-based sequence clustering method is to obtain the similarity graph in an efficient manner. A brute-force approach to obtain a similarity graph computes the similarity values between all (n²) pairs of sequences, where n is the number of sequences and then uses a user-defined threshold to add edges between sequences in the similarity graph. Clearly, this is inefficient, as it requires to compute $O(n^2)$ scores, so many graph-based sequence clustering algorithms use an efficient method for similarity graph construction. If a similarity graph is obtained, one of the available graph-clustering methods [90] can be used to obtain the desired clustering. In Algorithm 35, we present the pseudocode for a graph-based clustering based on the specific method for the similarity routine (Line 4) and the graph clustering (Line 9), various graph-based sequence clustering methods can be obtained.

The graph-based sequence clustering method that shown in Algorithm 35 is sometimes not scalable as the computation grows quadratically with the number of sequences. Since the similarity computation of each pair of sequences is independent, a straightforward remedy to the lack of scalability is to distribute or parallel compute the tasks. Instead of finding the similarity between all the sequence-pairs explicitly, we use exploit methods that find similar segment-pairs across all the input sequences simultaneously. Then, they obtain the similarity by scanning the sequence of highly significant segment-pairs. For instance, if two sequences share a large number of segment-pairs, the pair obtains a high similarity score, and hence the method adds an edge to avoid the all-pair computation with quadratic complexity and replace it with a method that has linear or sublinear complexity.

Line 9 of Algorithm 35 calls a graph-clustering algorithm. Many of the graph-clustering methods, such as spectral clustering [97, 29] or Markov clustering [31], have quadratic ($O(|V|^²) complexity and, hence, are not efficient for this task. Unlike, the earlier task of similarity graph construction...

#### Algorithm 35 Generic Graph-Based Clustering

**Input:** Sequence database ($S$), Similarity threshold ($\sigma$), Cluster count ($k$)
**Output:** Clusters ($C$)

1. $V = S, E = \emptyset$
2. for each edge $s_1 \in S$
3.   for each edge $s_2 \in S$
4.     if $\text{sim}(s_1, s_2) \geq \sigma$ and $s_1 \neq s_2$ then
5.       $E = E \cup (s_1, s_2)$
6.     end
7.   end
8. end
9. $C = \text{graph-clustering}(G, k)$
10. return $C$

The graph-based sequence clustering method that shown in Algorithm 35 is sometimes not scalable as the computation grows quadratically with the number of sequences. Since the similarity computation of each pair of sequences is independent, a straightforward remedy to the lack of scalability is to distribute or parallel compute the tasks. Instead of finding the similarity between all the sequence-pairs explicitly, we use exploit methods that find similar segment-pairs across all the input sequences simultaneously. Then, they obtain the similarity by scanning the sequence of highly significant segment-pairs. For instance, if two sequences share a large number of segment-pairs, the pair obtains a high similarity score, and hence the method adds an edge to avoid the all-pair computation with quadratic complexity and replace it with a method that has linear or sublinear complexity.

Line 9 of Algorithm 35 calls a graph-clustering algorithm. Many of the graph-clustering methods, such as spectral clustering [97, 29] or Markov clustering [31], have quadratic ($O(|V|^²) complexity and, hence, are not efficient for this task. Unlike, the earlier task of similarity graph construction...
