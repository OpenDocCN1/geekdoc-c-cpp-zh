
## 3. Model Selection

Cluster ensembles provide a novel approach to the model selection problem by matching the consensus across the base solutions to determine the final number of clusters to be obtained [25].

## 4. Knowledge Reuse

In certain applications, domain knowledge in the form of a variety of clustering under consideration may already exist due to past projects. A consensus solution can integrate such information to get a more consolidated clustering. Several examples are provided in [56], where such scenarios formed the main motivation for developing a consensus clustering methodology. As another example, a categorization of web pages on text analysis can be enhanced using the knowledge of topical document hierarchies available from Yahoo! or DMOZ.

## 5. Multivariate Clustering

Often the objects to be clustered have multiple aspects or “views,” and base clusters may be built on distinct views that involve nonsensical sets of subsets or data points. In marketing applications, examples may be segmented based on their needs, psychographic or demographic profiles, attitudes, etc. Different views can also be obtained by considering qualitatively different measures, an aspect that was exploited in clustering multifaceted proteins to functional groups in [5]. Consensus clustering can be effectively used to combine all clusterings into a single consolidated partition. Strehl and Ghosh [56] illustrate empirically the utility of cluster ensembles in two scenarios:

- Feature Distributed Clustering (FDC): base clusters are built by selecting different subsets of the features but utilizing all the data points. 
- Object Distributed Clustering (ODC): base clusters are constructed by selecting different subsets of the data points but utilizing all the features.

Fern and Brodley [177] also show that clustering in high dimensions is much more effective compared to clustering with PCA when the data points are randomly projected onto a subspace, in that subspace, and consensus is performed with this ensemble.

## 6. Distributed Clustering

In certain situations, data is inherently distributed and it is not possible to force the entire data at a certain site due to privacy/ownership issues or computational, bandwidth, and storage costs [46]. An ensemble can be used in situations where each clusterer has access to only a subset of the features of each object, as well as where each cluster has access to only a subset of the objects [25, 56].

The problem of combining multiple clusters can be viewed as a special case of the general problem of comparison and consensus of data “classifications,” studied in the pattern recognition and application communities in the 70s and 80s. In this literature, classification was used in a broad sense to include clustering, unrooted trees, graphs, etc., and problem-specific measures were made [47] for a broad, more conceptual coverage). For example, in the building of phylogenetic trees, it is important to get a strict consensus solution, wherein two objects in the same consensus partition or if they occur together in an individual cluster [13], typically resulting in a consensus solution with a much coarser resolution than the individual solutions.

A quick overview with pointers to such literature is given by Ayad and Kamel [6]. Moreover, based on the success of classifier and cluster ensembles, efforts have been made to combine both types of ensembles [1, 23]. Unsupervised models can provide a variety of supplementary constraints which be useful for improving the generalization capability of the resulting classifier, especially when labeled data is scarce. they might be useful for designing learning methods that are aware of the possible differences between training and target distributions, thus being interesting for applications in which concept drift might take place [2, 22]. A reasonable coverage of these problems is not feasible here, instead this article focuses on cluster ensembles and associated algorithms that have been proposed in the past decade.

This chapter is organized as follows. In Section 22.2, we formulate the cluster ensemble problem. In Section 22.3, different measures for comparing a pair of cluster solutions are introduced. Details of different cluster ensembles algorithms are presented in Section 22.4 followed by the applications of cluster ensembles in Section 22.5.

## 22.2 The Cluster Ensemble Problem

We denote a vector by bold letter and a scalar by var or in normal font. We start by considering $r$ base clusterings of a data set $X = \{x_i\}_{i=1}^n$ with the $q$th clustering content. The most straightforward representation of the $q$th clustering is $\lambda^{(q)} = \{C_l^{(q)}|l=1,...,k^{(q)}\}$ and $C_l^{(q)} \subseteq X$. Here, each clustering is denoted by a collection of subsets (not necessarily disjoint) of the original data. For hard clustering (where each object is assigned to a single cluster), the $q$th clustering can alternatively be represented by a label vector $\lambda^{(q)} \in L^n$. In this representation, each object is assigned some cluster label, and is 0 if the corresponding object is not aligned to cluster. The third way of representation of an individual clustering is by the binary membership matrix $H^q = \{h_{il}^{(q)} \in \{0,1\\}^{n \times k^{(q)}}$ which is defined as $h_{il}^{(q)} = 1$ if $x_i \in C_l^{(q)}$. For partial clustering, we additionally have

$h_{il}^{(q)} = 1 \quad \forall x_i \in X.$

A consensus $\Gamma$ is defined as a function $\mathbb{Z}_+^{n^r} \rightarrow \mathbb{Z}_+^n$ mapping a set of clusterings to an integrated clustering $\Gamma(\{\lambda^{(q)}|q \in [1,2,...,r]\}) \rightarrow \hat{\lambda}$. For conciseness, we shall denote the set of clusterings $\{\lambda^{(q)}\}_{q=1}^r$ available to the consensus by $\Lambda$. Moreover, the results of any hard clustering of $n$ objects can be represented as a binary, $n \times n$ co-association matrix, with an entry 1 if the corresponding objects are in the same cluster and 0 otherwise. For the $q$th base clustering, this matrix is given by

$S_{ij}^{(q)} = \begin{cases} 1 & (i, j) \in C_l^{(q)} \ 0 & \text{otherwise} \end{cases} \quad (22.1)$

Broadly speaking, there are two approaches to obtaining a consensus solution and determining its quality. One can postulate a probability model that determines the labeling of the individual solutions, using the true cluster labels, and then solve a maximum likelihood function to return the consensus. Alternatively, one directly see see consensus clustering that agrees with the most of the originalings. The second approach requires a way of measuring the similarity between two clusterings, for example, to evaluate how the consensus solution is to each base solution. These measuring indices will be discussed in more details in Section 22.3. For now, let $\lambda^{(a)}, \lambda^{(b)}$ represent a similarity index between two clustering. One can express the average similarity between a set of $r$ labelings, $\Phi(\Lambda, \tilde{\lambda}) = \frac{1}{r} \sum_{q=1}^r \ell^{(q)}, \tilde{\lambda}) \quad (22.2)$

This serves as the objective function in cluster ensemble formulations, where the goal is to find the combined clustering $\tilde{\lambda}$ with $k$ clusters such that $\Phi(\Lambda, \tilde{\lambda})$ is maximized. It turns out that this objective is intractable, so heuristic approaches have resorted to.

## 22.3 Measuring Similarity Between Clustering Solutions

Since no ground truth is available for clustering problems, cluster ensemble algorithms aim to maximize similarity between the consensus clustering and each of the base solutions. Two of the most desirable properties of such similarity measures are

- The index should be normalized for easy interpretation and comparison across solutions with varying numbers of clusters.
- The expected value of the index between independent clusterings should be constant (preferably zero). The utility of such a property will be clarified later.

Below, we present different indices and show how these are modified to achieve zero expected value of the same. The general rule for any "adjustment for chance" is as follows:

$adjusted\ index = \frac{index - Expected-index}{Max - Expected-index} \quad (22.3)$

where Expected-index is calculated using a permutation model. In such a model, cluster labels are assumed to be generated randomly to the constraints of a fixed number of clusters and a fixed number of points. Max-index is the maximum value the index can take.

Now us discuss two key approaches for measuring the similarity of two clustering solutions. The first is based on counting the number of pairs in agreement or disagreement. The second approach uses information from theory.

**1. Pair-Counting Base Measures:** These of type are based on counting the number of pairs on which two candidate solutions agree or disagree. More formally, suppose we $\lambda^{(a)} = \{C_h^{(a)}\}_{h=1,2,...,k^{(a)}}$ and $\lambda^{(b)} = \{C_l^{(b)}\}_{l=2,..,k^{(b)}}$. Let $n_h^{(a)}$ be the number of objects in cluster $C_h^{(a)}$ and $n_l^{(b)}$ be the number of objects in cluster $C_l^{(b)}$. Table 22.1 is a contingency table that shows the overlap between different clusters of these clusterings, $n_{hl} = |C_h^{(a)} \cap C_l^{(b)}|$. The most well-known index of this is the Rand Index (RI), which is a normalized measure of number of agreements between two candidate solutions and is

$$\phi^{(RI)}(\lambda^{(a)}, \lambda^{(b)}) = \sum_{hl} \left( \frac{n_{hl}}{2} \right) \frac{1}{2}(S_a + S_b) \quad (22.4)$$

Expected value of RI, however, is not constant. This led Hubert and Arabie [32] to propose
