# 324 Data Clustering: Algorithms and Applications

and thus the document representation is simplified to be a vector of idf values. The RMcut value corresponding to a $K$-clustering $C$ of $\mathcal{D}$ is defined as

```
$RMcut(C) = \sum_{k=1}^{K} \frac{cut(C_k, C-C_k)}{\sum_{d_i,d_j \in C_k} sim(d_i,d_j)}$
```

The denominator of the above formula takes into account the intrimilarity of each cluster and size, the larger is used to avoid producing unbalanced clusters. The edge-cut function $cut(\cdot,\cdot)$ acts as an intercluster similarity criterion; it is defined as the summation over the weights of all connecting vertices (documents) within a specified cluster to the rest of the clusters.

Taking into account cluster frequencies for terms, we can observe that the sum of pair-wise document similarities within a cluster is equal to the product of the squared inverse document frequency and cluster frequency over all terms in the cluster. Thus, the RMcut criterion can be efficiently computed as

```
$RMcut(C) = \sum_{k=1}^{K} \frac{\sum_{M}(idf_f)^2 c_{f,k} c_{f,-k}}{\sum_{M}(idf_f) c_{f,k}^2}$
```

where $c_{f,k}$ and $c_{f,-k}$ denote the cluster frequency of the $f$-th term within the $k$-th cluster and the rest of the clusters. Note that the overall complexity of RMcut criterion is $O(N+M)$, which can be computed by a single scan of the documents in the collection, and by the computation of the numerator and the denominator in the above formula is $O(M)$.

Following the TermCut strategy, Ni et al. [78] propose two algorithms. The first tries to bisect clusters until the desired number of clusters is reached. The second takes a *minimal RMcut decrease threshold* as input, and as name suggests, continues the bisection process until the decrease in RMcut falls below the given threshold. While the idea behind the RMcut criterion is very similar to using the CLUTO cluster functions defined in Equations 13.5 and 13.6 of Table 13.2, Ni et al. show that their bisecting strategy outperforms CLUTO for a number of short text datasets.

# 13.5.2 Clustering with Knowledge Infusion

Motivated by the lack of common vocabulary in short documents, many document clustering algorithms first enrich or complement the statistical vector representation of terms with external knowledge, such as WordNet or Wikipedia. Banerjee et al. [8] propose to enrich the original term-feature space of search results with the titles of the Wikipedia articles are retrieved as two queries for each result. The first query is based on the result title, while the other is based on the result description, snippet. Scaiaella et al. [93] propose a "graph of topics" model to represent each snippet, in which vertices correspond to Wikipedia pages that are identified by topic annotators, and the edges are weighted to determine the semantic relationship between the linked topics. An online spectral clustering is used on an induced graph consisting of two types of vertices, topics and snippets, where the weighted edges express either similar topics or topic-snippet matches.

User actions have also been useful in identifying short document clusters. Wang and Zhai [109] exploit information in log data produced by a real search engine to cluster result snippets. Carpineto and Romano [17] introduce a meta-clustering strategy that clusters snippets by integrating partitions separately as a result of analyzing the *tf-document* term-matrix with SVD, NMF, and generalized trees. They also define an evaluation measure that takes into account the behavior of Web users in the time spent to satisfy their search needs.

© 2014 Taylor & Francis Group, LLC