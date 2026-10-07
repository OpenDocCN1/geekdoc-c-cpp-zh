
# 310 Clustering: Algorithms and Applications

documents in $c$ and $Y$ is the label assigned to document $j$. The most destructive projections are the eigenvectors associated with the largest eigenvalues of $S_c^{-1}S_h$.

A number of non-linear [9, 41, 101] and approximate [92, 68] extensions address the problems of non-separable data and high computational complexity in the previous algorithms. While shown initially to be less effective than other methods [33], algorithms based on random projections are actively being investigated due to their lower computational complexity [3].

Feature transformation techniques have also been used for feature selection. Let Yan et al. choose a subset of features by principal components [71]. Hardin at al. compare SVM and Markov Blanket based feature selection [43]. In the supervised domain, Yan at al. use the Orthogonal CO subspace learning algorithm to achieve optimal feature selection. As a way to bridge the gap between the two dimensionality reduction techniques, Yan at al. proposed TOFA [115], an optimization framework for both feature selection and feature transformation algorithms. Dy and Brodley [31], Vinay at al [107], Aldo and Verelsen [66], and Cunningham [23] survey different aspects of dimensionality reduction. Chapter 2 of this book includes a deeper discussion on feature selection.

## 13.2.5 Characterizing Extremes

As the two extremes of text representations, long and short documents have additional characteristics that can impact how they are processed in information retrieval and data management tasks. For example, short texts often lack context, can have multiple interpretations, and use imprecise or incorrect language. Long documents are often specific and address multiple subjects. Linguistic characteristics include the size of the text and the type of language used to express ideas. Topical characteristics focus on the communicative function and targets of the documents. Specifically, we identify the following characterizing attributes:

- *Noise*, which is related to the use of informal language. Noisy texts are usually rich in contracted forms of words, colloquialisms, emotional punctuation and graphs, and frequently occurring types.
- *Amount of context-shared information*, which is related to the sparseness of the text representation.
- *Community-focus*, which is regarded as the extent to which the contents of a document are of interest to a specific group of users (e.g., neighbors in a social network or a research community).
- *Domain-specificity*, which expresses the degree of alignment of the document vocabulary to a lexicon that is specific to a certain subject domain.

Note that the amount of noise and context-shared information are regarded as linguistic characteristics, whereas the remaining fall into the topical category.

Figures 13.2 (a) and (b) generally compare short and long documents under the listed attributes. We have taken two of the most representative examples for each type of document: Web pages and scientific articles as long documents, and microblogs, such as tweets and result snippets, as short documents. Increasing positions along each of the axes correspond to an increasing impact of a certain characteristic. As represented in the graphs, tweets generally feature high noise, low amount of context-shared information, high degree of community focus, low/mid domain-specificity; by contrast, specific documents are usually less noisy and sparse, but more domain-specific.

© 2014 by Taylor & Francis Group, LLC

# Document Clustering: The Next Frontier

![](img/b94d85a2e934001944bcc21abd9a9943_337_0.png)

**FIGURE 13.2: Comparison of example short and long documents: (a) linguistic and (b) topical characteristics. Thicker (as opposed to thinner) ovals correspond to examples of long (as opposed to short documents).**

## 13.3 General Purpose Clustering

Most documents have moderate length, often address a single topic, and useunderset language. Examples include Web pages, emails, encyclopedic articles, and newspaper articles. These documents have been the focus of the data mining community for many years. As a result, most document clustering algorithms pertain to clustering these standard document collections. In the following, we provide an overview of the most prominent of algorithms.

## 13.3.1 Similarity/Dissimilarity-Based Algorithms

Traditionally, clusters are grouped by how similar they are to other documents. Similarity-based algorithms define a function for computing document similarity and use it as the basis for assigning documents to clusters. Each group (cluster) should have documents that are similar to each other and dissimilar to others in clusters. Clustering falls into different categories based on the underlying methodology of the algorithm (aggregative or partitioning), the structure of the final solution (flat or hierarchical), or the multiplicity of cluster membership (hard or soft, overlapping, fuzzy). Agglomerative algorithms find the clusters by initially assigning each object to its cluster and repeatedly merging pairs of clusters until a certain criterion is met. Many different methods have been proposed for determining the next pair of clusters to be merged, such as group average (UPGMA) [53], single-link [97], complete-link [62], CURE [39], ROCK [40], and Chameleon [59]. Hierarchical algorithms produce a clustering that produces a dendrogram, with a single-inclusive cluster at the top and single-point clusters at the leaves. On the other hand, partitioning algorithms such as k-Means [72], k-Medoids [53], graph partitioning [117, 53, 100], and spectral partitioning [14, 21], find the clusters by partitioning the entire dataset into either a predefined or automatically determined number of clusters. Depending on the algorithm, a k-clustering solution can be obtained directly or via a sequence of repeated restarts. The Spherical k-Means algorithm (Sk-Means) [51] is used extensively for clustering due to its low computational requirements and its ability to find high-quality solutions. A variant of the “fuzzy” version of k-Means, called Fuzzy Spatial k-Means (FSk-Means) [123], provides an overlapping clustering by using a matrix of degrees of membership of objects with respect to clusters and a real value f > 1. The latter is called the “fuzzier”, or fuzziness control, and controls the “softness” of clustering. Higher f values lead to harder clustering solutions.

In recent years, researchers have recognized that particular clustering algorithms are well suited for clustering large datasets due to their relatively low computational requirements [1, 99]. A key characteristic of many particular clustering algorithms is that they use a global

©2014 Taylor & Francis Group, LLC

# TABLE 13.2: The Mathematical Definition of Various Clustering Criterion Functions

| Criterion Function | Optimization Function | | |
| --- | --- | --- |
| $L_\infty$ | maximize $\sum_{i=1}^K \frac{1}{n_i} \sum_{v,u \in S_i} \text{sim}(v,u)$ | (13.1) |
| $L_\Sigma$ | maximize $\sum_{i=1}^K \frac{1}{n_i} \sum_{v,u \in S_i} \text{sim}(v,u)$ | (13.2) |
| $\mathcal{E}_\infty$ | minimize $\sum_{i=1}^K \frac{1}{n_i} \sum_{v,u \in S_i} \text{sim}(v,u)$ | (13.3) |
| $\mathcal{G}_\infty$ | minimize $\sum_{i=1}^K \frac{1}{n_i} \sum_{v,u \in S_i} \text{sim}(v,u)$ | (13.4) |
| $\mathcal{G}_\Sigma$ | minimize $\sum_{r=1}^K \frac{\text{cut}(V_r, V-r)}{W(V_r)}$ | (13.5) |
| $\mathcal{H}_\infty$ | maximize $\frac{\mathcal{L}_\infty}{\mathcal{E}_\infty}$ | (13.6) |
| $\mathcal{H}_\Sigma$ | maximize $\frac{\mathcal{L}_\Sigma}{\mathcal{E}_\Sigma}$ | (13.7) |

Note: The notations in these equations are as follows: $K$ is the total number of clusters, $S$ is the total set of objects to be clustered, $S_i$ is the set of objects assigned to $i$th cluster, $n_i$ is the number of objects in the $i$th cluster, $v$ and $u$ represent two objects, and $\text{sim}(v,u)$ is the similarity between two objects.

criterion function whose optimization drives the entire clustering process.$1$ is implicit for some of the algorithms (e.g., PDDP [141]), whereas for others (e.g., $k$-Means) the criterion is explicit and can be easily stated. This later class of algorithms can be thought as consisting of two components. The first is the criterion function that needs to be optimized by the clustering solution, and the second is the actual algorithm that achieves this. These components are largely independent of each other.

Table 13.2 lists some of the most widely used criterion functions for document clustering. Zhao and Karyapis analyze these criterion functions in both hard and soft clustering and provide insights into their relative performance [121, 122, 123]. Various clustering algorithms and criterion functions described in this section are part of the CLUTO [58] clustering toolkit, which is available online at http://www.cs.umn.edu/~cluto.

## 13.3 Density-Based Algorithms

In contrast to similarity-based algorithms that often optimize a global clustering function, density-based clustering algorithms focus on the local picture. DBSCAN [32] and OPTICS [7], typical density-based clustering, are designed to discover clusters of arbitrary shape in the presence of noise and have been shown effective for some datasets. Users do not need to know the number of clusters in advance, but have to provide other parameters that are sometimes hard to identify, e.g., a density threshold and the radius of a neighborhood in the case of DBSCAN. Additionally, the indexing techniques the algorithms use for efficient neighborhood do not scale to high-dimensional feature spaces.

> $1$Global criterion functions are an inherent feature of partitioning algorithms, but they can also be used in the context of agglomerative algorithms.
