
## 9.2.2 Consequences

The third and fourth of these aspects of the curse of dimensionality have been actually the main motivation for developing specialized methods for clustering in subspaces of highly dimensional data even though this was not always recognized. The superficial reference to the second aspect that often be found in the literature misses the point. But even so the proposed approaches, perhaps partially unintentionally, actually tackled Aspect 3 and 4.

For decades, research was concerned with the effect of irrelevant (noise) attributes (sometimes called masking variables [53]) on the performance of clustering algorithms [100, 52, 59, 127]. They discuss how to identify which attributes that do not contribute to the cluster structure at all. The clustering task should then concentrate on the remaining attributes. In some cases, the contribution of attributes may be weighted instead of a discrete decision (contributing or masking). This view of the problem is obviously related to dimensionality reduction [66, 132].

The field of subspace clustering as we sketch it here a more complex view. The reason is that dimensionality reduction as a first step prior to clustering is not always resolving the issues since the choice of attributes or the relevance vs. attributes is usually characteristic for clusters but not for complete data. In other words, masking variables may be masking clusters but may help to discover others.

The phenomenon that different features or a different correlation of features may be relevant for different clusters within a single clustering solution has been called feature relevance or local feature correlation global in the following sense: they generate only one subspace of the original data in which the clustering can then be performed. The problem of local feature relevance or feature correlation describes the observation that multiple subspaces are needed because each cluster may exist in a different subspace. The critical requirement for the design of clustering algorithms is hence the interaction between deriving the characteristics for a certain subgroup of data and some heuristic for a data set that exhibits a significant level of similarity in that subspace of the space — obviously a circular dependency of two tasks (subspace determination vs cluster assignment) already in the most basic problem description.

Aspect 5 is a problem whenever ε-range queries of different dimensionality are compared, which is done in many of the available algorithms.

## 9.3 Clustering Tasks in Subspaces of High-Dimensional Data

For the design of specific clustering algorithms suitable for high-dimensional data all the aspects of the curse of dimensionality, as sketched above, are relevant. However motivating approaches to clustering in subspaces are mainly the phenomena of irrelevant attributes (Aspect 3) and correlated attributes (Aspect 4). These two phenomena result in different types of subspaces which pose different challenges to concrete algorithms.

### 9.3.1 Categories of Subspaces

#### 9.3.1.1 Axis-Parallel Subspaces

The distinction between relevant and irrelevant attributes generally assumes that the variance of the occurring values for a relevant attribute over the corresponding cluster is small compared to the overall range of attribute values whereas the variance for irrelevant attributes within

a given cluster is high (or indistinguishable from the values of the same attribute for other clusters or for background noise). For example, one could assume a relevant attribute for a given cluster being normally distributed with a small standard deviation whereas irrelevant attributes are uniformly distributed over the complete data. The geometrical intuition of these assumptions relates to the points of a cluster being widely scattered in the direction of irrelevant axes while densely clustered over relevant attributes. When selecting the relevant attributes only (by projection onto the subspace, i.e., the subspace spanned by these attributes), the cluster would appear as a full-dimensional cluster in the subspace. In the full-dimensional space (including the irrelevant attributes) the cluster points form a hyperplane parallel to the irrelevant axes. Due to this geometrical approach, this type of cluster is addressed as an axis-parallel subspace cluster.

### 9.3.2 Arbitrarily Oriented Subspaces

If two attributes $a_i$ and $a_j$ are linearly correlated for a set of points, the points will be scattered along a hyperplane defined by some linear dependency between both attributes that corresponds to the correlation. The subspace orthogonal to this hyperplane is a subspace where the points cluster densely of the variance of combined values of $a_i$ and $a_j$. This subspace is arbitrarily oriented and hence the more general case compared to axis-parallel subspaces.

### 9.3.3 Special Cases

The aforementioned types of subspaces have a direct relationship to the curse of dimensionality as discussed above, it should be noted that from the point of view of existing algorithms there are special types of subspaces. In fact, there is a large family of algorithms, addressed as “bi-clustering,” “co-clustering,” “two-mode clustering,” or “pattern-based clustering” [90, 99].

Considering the intuition of subspaces for subspace clustering, these algorithms address different kinds of subspaces such as very specific ones (e.g., points that form a cluster along the bisecting line) or specific half-spaces (e.g., in some subspace, only points located on one side of the bisecting line can form a cluster). Thus, the types of subspaces considered by these methods do not directly relate to the phenomena of the curse of dimensionality discussed here but rather the products of subspace cluster models.

As these methods are predominantly used in biological data analysis, refer to Chapter 16 for an overview on this methods that come with the cluster models has been elaborated in detail by Kriegel et al. [90].

### 9.3.2 Search Spaces for the Clustering Problem

Recognizing the different categories of subspaces can guide us to recognize different categories of subspace clustering. If we describe the problem in general as clusters, where each cluster can reside in a different subspace, it is obvious that the problem of finding the subspaces containing clusters is intractable. The number of axis-parallel subspaces is exponential in the number of dimensions (we can see this as a result of the first aspect of the curse of dimensionality). Also, since different subspaces can be relevant for different clusters, feature reduction is not a solution. Aside from the search for intersecting subspaces, the search for clustering solutions is also challenging, as clustering in general is an NP-complete problem [125]. Even worse here: the search for clusters and the search for subspaces are depending on each other. Neither is a good solution to, first, find the subspaces and then the clusters in the subspaces, as this results in a redundant set of clusters (we will see this problem of redundancy in more detail). Now is it a viable approach to, first, find the clusters and then define the subspace for each cluster. Hence the definition of a cluster, with an algorithmic heuristic for clustering, and the heuristic to derive

a subspace for each cluster are closely related for each approach. Yet how this relationship is defined in particular will be differing in the different approaches.

Many heuristics and for efficiently solving the clustering problem have been discussed in the past decades. We will focus on the subspace search problem in this chapter. However, for the sake of completeness, we should keep in mind the fact that the solutions discussed here rely on assumptions and heuristics that consider the clustering problem (i.e., whether, for example, a partitioning or a density-based clustering paradigm is used or adopted). These assumptions and heuristics are reflected by the underlying clustering model that specifies the meaning of clusters and the algorithms to compute clusters. One important aspect to describe the meaning of clusters that has an impact on the subspace search problem is the choice of a certain distance or similarity measure. Data points are considered more similar than others, and thus, cluster depends crucially on such choice. Some approaches are based on Euclidean space, particularly using an $L_p$-norm as distance measure. Others take into account a similar "behavior" of attribute values over a range of attributes (often called "patterns”). But different approaches also make use of the definition of similarity in different ways, based on different intuitions of the meaning of a cluster and resulting in different cluster models. If we stay with the name of Euclidean distance subspace of a cluster will mean similarity defined in different ways for different clusters. In the case of axis-parallel subspace, only a subset of the attributes is considered to compute the $L_p$-distance. For arbitrarily oriented subspaces, correlations of attributes are considered and combinations are computed to define a rotated subspace (such as one variant of a Mahalanobis distance).

## 9.4 Fundamental Algorithmic Ideas

Different paradigms of clustering heuristics are discussed in other chapters. Here, we survey some fundamental algorithmic ideas and example approaches considering the different heuristic restrictions of the space for subspaces.

### 9.4.1 Clustering in Axis-Parallel Subspaces

#### 9.4.1.1 Cluster Model

So far, most research in this field mainly transferred the full-dimensional cluster models of differing clustering techniques into some (or many)—more or less—interesting subspaces (i.e., subsets of attributes) of a data space. Hence, there is no "subspace cluster model" describing axis-parallel subspace clusters concisely. Instead, there are only cluster models describing clustering in a subspace as if... The first statistically sound model for axis-parallel subspace clusters was proposed by Moise and Sander [101]. It is based on assumption (statistically speaking: hypothesis) that values of a relevant attribute for a subspace cluster are not uniformly distributed over the complete attribute domain (i.e., the null hypothesis is a uniform distribution of irrelevant attributes over the complete domain) and that this satisfies a statistical test.

#### 9.4.1.2 Basic Techniques

The number of possible axis-parallel subspaces where clusters could reside is exponential in the dimensionality of the data space. Here, the main task of research in the field was the development
