
# Data Clustering: Algorithms and Applications

where the first is the squared Euclidean distance measure on the numerical attributes and the second term is the matching dissimilarity measure on the categorical attributes. The weight γ is given to avoid favoring either type of attribute.

## 12.4.1.3 Fuzzy k-Modes

Fuzzy k-Modes extends fuzzy-Means to categorical data [48]. Fuzzy k-Modes is based on the same ideas as k-Modes, using iterative assignment of objects to the closest modes and evaluation of modes, until convergence. However, objects' assignments to clusters involve degree of membership between 0 and 1. The total membership of object $i$ across all clusters must equal 1, as $\sum_{j=1}^k w_{ij} = 1$, for any $i \le n$. The Fuzzy k-Modes algorithm evaluates the total cost against the whole dataset $X$, against a cost function $F(W, X, Z) = \sum_{i,j} w_{ij}^\alpha d(X_i, Z_j)$, where $\alpha \ge 1$ is a weighting factor and $Z_j = [z_{j1}, \dots, z_{jm}]$ is the mode of the $j$-th cluster. The weights $0 \le w_{ij} \le 1$ are set at each iteration, so that the $j$-th object will tend to join the $j$-th cluster with the least dissimilarity mode $Z_j$. In mode, $Z_j$ of cluster $l \le j \le k$, represented by $[z_{j1}, \dots, z_{jm}]$, has each position $z_{j j}$ for the attribute $A_j$ that will minimize the cost function. The cost function is the sum of the weighted distances of all objects against the cluster mode. It was proved that the k-Means algorithm will converge in a finite number of iterations. Its disadvantage is that it terminates at local optima.

## 12.4.1.4 Squeezer

Squeezer is a one-pass algorithm that is based on summarizing clusters like k-Modes. However, Squeezer improves the iteration-bound speed of k-Modes [43]. Squeezer reads objects one-by-one. The first tuple forms a cluster alone. Next objects are either put into an existing cluster or rejected to form a new cluster.
The Squeezer algorithm accepts as input the dataset of objects and a value $s$ for the similarity threshold. The algorithm then fetches cluster objects in an iterative fashion. Initially, the first object is read and a new Clustering Structure is established, which includes a summary and the cluster itself. For each subsequent object, the similarity between any existing cluster C and the object is computed. The maximal similarity value (denoted by sim-max) and the corresponding index of a cluster (denoted by index) are evaluated from the computing results. Then, if the similarity is larger than the input threshold $s$, the object is assigned to the selected cluster. Otherwise, a new Clustering Structure is constructed, consisting of the cluster and summary. Finally, outliers are handled and the clustering results are returned.

One of the disadvantages of Squeezer is that on some datasets, it may not produce accurate clusters. Squeezer is considered efficient with a complexity of $O(kN)$.

## 12.4.1.5 COOLAT

COOLAT is based on similar ideas as k-Modes, but uses objects as clusters. COOLAT adapts to k-Modes sensitivity to the cluster modes problems. Clusters are created by reducing their entropy [19]. COOLAT finds a set of maximally dissimilar objects to create initial clusters. All remaining objects are placed in one of the clusters, such that the increase in entropy is minimized. The name of COOLAT comes from the reducing of entropy of the clusters, "cooling". Entropy is the measure of information and uncertainty of a random variable. If $X$ is a random variable, $S(X)$ is the probability function of $X$, the entropy $E(X)$ is defined as $E(X) = \sum_{x \in S(X)} p(x)\log(p(x))$. Entropy is sometimes referred to as a measure of the amount of "disorder" in a system. The authors argue that a measure of the similarity between two vectors, the use of entropy is equivalent to that of other widely used similarity measures.

COOLAT starts with a sample of points. The initial step selects the k most dissimilar objects from the sample set, such that the pairwise entropy of the chosen objects is maximized. These serve as initial representatives of the k clusters. All objects of the dataset are placed in one of the clusters that, at each step, the increase in the entropy of the resulting clustering is minimized. After the initialization, COOLAT proceeds to process the objects of the dataset (not selected to select the clusters incrementally), finding a suitable cluster for each object. This is done by computing the expected entropy of results after placing the object in each of the clusters and selecting the cluster for each object. Table 12.2 compares three clusterings and the one that minimizes the expected entropy.

Disadvantages of COOLAT include its sensitivity to the order of object selection, as well as its quadratic complexity of O(n^2).

# Clustering Categorical Data

## TABLE 12.2: Three Different Clustering of a Zoo Dataset

| Cluster # | Clustering 1 | | Clustering 2 | | Clustering 3 |
| --- | --- | --- | --- | --- | --- |
| | members | E | members | E | members | E |
| Cluster 0 | { tail, 4-legs }, { tail, 2-legs } { no-tail, 0-legs } | 1.0 | { tail, 4-legs }, { no-tail, 0-legs } { tail, 2-legs } | 2.0 | 0 |
| Cluster 1 | | { tail, 2-legs }, { no-tail, 0-legs } | 0 | | 2.0 |
| Exp. E | | 0.66 | | 1.33 | | 1.33 |

**Note:** Table has three objects (in brackets) and two attributes: tail (yes/no) and length (two/four). As shown, clustering 1 minimizes the expected entropy of the two clusters.

## 12.4.2 Hierarchical Clustering

Hierarchical algorithms partition the objects into a tree of nodes, where each node represents a potential cluster [56, 61]. Hierarchical clustering methods applied to categorical data usually cluster the data in an aggregative (bottom-up) fashion, where the most similar objects are gradually clustered at different levels of the tree. For choosing a similarity metric, a divisive (top-down) fashion, where every node at a level consists of a statistical summary of the resulting cluster and a new object is placed in the most suitable cluster.

Disadvantages of hierarchical methods for categorical data include their quadratic runtime and often slower speed. Errors in merging clusters cannot be undone and will affect the result. If large clusters are merged too early, the local cluster structure may be lost. Next, we will discuss several hierarchical clustering algorithms for categorical data.

## 12.4.2.1 ROCK

ROCK is an agglomerative (bottom-up) hierarchical algorithm [39]. ROCK handles categorical data clustering by building a tree; at each tree level clusters are merged in a way that the resulting-cluster similarity is maximized, where similarity is evaluated by the number of similar object pairs within a resulting cluster. ROCK assumes a special similarity measure between objects and defines a "link" between two objects the similarity of which exceeds a threshold.

The motivation for ROCK was to develop a global clustering approach that considers the links between objects. For this purpose, ROCK uses common neighbors to define links. If a neighbor object C and object B are linked (even if they are not neighbors). Two objects belonging to the same cluster have many common neighbors, while objects belonging to different clusters have few common neighbors. Initially, each object is assigned to a separate cluster. Clusters are merged repeatedly according to their "closeness", defined by the sum of the number of links between all pairs of objects within clusters.

In order to decide which objects are "neighbors," ROCK defines a similarity function, sim(A,C), which encodes the level of similarity ("closeness") between two objects. The similarity is normalized, such that sim(A,C) is one when A and C are identical and zero when they are completely dissimilar. Objects A and C are considered to be "neighbors" if sim(A,C) > θ, where θ is a user-provided parameter. Link(A,B) is defined to be the number of common neighbors between A and B. The similarity can be any metric such as Euclidean distance or the Jaccard coefficient.

A hierarchical clustering algorithm uses links to the samples. It iteratively merges clusters Ci, Cj that maximize the goodness function

```
g(Ci,Cj) = \frac{total#crosslinks}{expected#crosslinks} = \frac{(ni+nj)*1+2(f(0))-ni}{nj-1+2(f(0))-nj}
```

It stops once there are no more links between clusters or the required number of clusters has been reached.

The best set of clusters is characterized through the use of a criterion function, Er, that the best set of clusters is the one maximizing Er. The number of links between pairs in each cluster: Er = \sum \sum link(pq,pr). This criterion keeps points that share many links in the same cluster, but it does not force links to split into different clusters. This criterion approach may end up with a large cluster, or it may result in relatively weak clusters.

Disadvantages of ROCK include its cubic complexity in N, which makes it generally unsuitable for large datasets [38, 76].

## 12.4.2.2 COBEW

COBEW represents a hierarchical clustering in the form of a classification tree. COBEW organizes objects into a classification tree. A classification tree differs from decision trees, which labels branches rather than nodes and uses logical rather than probabilistic descriptions. Sibling nodes in a classification tree form a leaf partition [31].

Each node in a classification tree represents a class (concept) and is labeled by a probabilistic attribute-value distributions of objects under the node. This classification tree can be used to predict the class of a new object or missing attributes. COBEW integrates objects incrementally into an existing classification tree by classifying the object along a path of best matching nodes.

There are four operations COBEW employs in building the classification tree. What operation is selected for a step depends on the category utility of the classification tree achieved by it:

- 1. Insert a node: a node is created corresponding to the object being inserted into the tree.
- 2. Merge two nodes: replace two nodes by a node whose child is the union of the original nodes. The new node summarizes the attribute-value distributions of all objects classified under.
- 3. Split a node: a node is split by replacing it with its children.
