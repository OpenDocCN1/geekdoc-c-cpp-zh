
## Clustering Categorical Data

## 12.3.2 Probabilistic Measures

Probabilistic approaches take into account the probability of a match between attribute values taking place. The following measures are probabilistic:

Goodall: This measure assigns a higher similarity to a match if the value is infrequent than the value is frequent. This similarity measure essentially considers the probability that the similarity value would be observed in a random sample of two points from the dataset. The maximum similarity is attained when the matching value $X_k$ occurs twice and all other possible $A_k$ occur more than twice. The minimum similarity is attained when attribute $A_k$ has only one value. The Goodall's similarity formula is

```
$S_k(X_k, Y_k) = 1 - \sum_{q \in Q} p_k(q) \text{ if } X_k = Y_k, \text{ otherwise.}$
```

The original Goodall similarity combines similarities between attributes; in multivariate categorical data, by considering dependencies between attributes; however, this procedure is computationally expensive to compute and Boriah et al. have proposed 4 sampler variants [36, 22].

Smirnov: The Smirnov measure is a probabilistic measure that considers matches and mismatches. This measure considers both value's frequency as well as the distribution of the other values taken by the same attribute. The similarity is higher for a match, if the matching values are infrequent; but the other values are frequently occurring; the maximum similarity is attained if the matching value $X_k$ occurs twice and there is just one other value for $A_k$, occurring $N-2$ times. The minimum similarity for a matching value is attained if $X_k$ is the only value for $A_k$ occurring $N$ times. For a mismatch, the maximum similarity is attained if $X_k$ and $Y_k$ occur once and $A_k$ takes just one value occurring $N-2$ times. For a mismatch, the minimum similarity is attained when $X_k, Y_k$ are the only two values for $A_k$.

Aberg: This similarity measure also takes into account matches and mismatches. In this approach, matches on rare values indicate a strong similarity, while mismatches on rare values should be treated distinctly and indicate lower similarity. It assigns higher similarity for matches on rare values and lower similarity for matches on frequent values. As for mismatches, it decreases the similarity for mismatches on rare values (decreasing it for mismatches on frequent value) [6].

## 12.3.3 Information-Theoretic Measures

Information-theoretic approaches incorporate the information content of a particular attribute value with respect to the data set. These measures are informed by information theory, where attribute values that are rarely observed are more informative. The following measures are information-theoretic:

Burnaby: This measure assigns higher similarity to mismatches on frequent values and lower similarity to mismatches on rare values. For mismatches, the range of $S_k(X_k, Y_k)$ is $log(1-freq)/log(N-T)$ [1]. For matching values, this similarity returns $S_k(X_k, Y_k) = 1$. This formula returns the minimum similarity when all values for attribute $A_k$ are infrequent (occurring only once) and the maximum value when $X_k, Y_k$ are frequent (occurring $N/2$ times) [25].

Lin: This measure gives higher similarity to matches on frequent values and lower similarity to mismatches on infrequent values. The basic Lin similarity formula is [58]:

```
$S_k(X_k, Y_k) = 2 log(p_k(X_k)) \text{ if } X_k = Y_k, \ 2log(p_k(X_k) + p_k(Y_k))$ otherwise.
```

## 12.3.4 Context-Based Similarity Measures

Context-based measures evaluate similarity between two objects by examining the contexts in which they appear. For example, a context-based measure may evaluate the distance between two soft drink customers, considering one is a Coke customer and the other a Pepsi customer. So, the question becomes how to define the distance between two vectors of boolean or categorical attributes in m-space, which corresponds to Coke and Pepsi customers.

The context-based metric proposed by Das and Manila follows an iterative approach [26]. Given distances between all pairs of m attributes in the dataset, this approach iteratively computes distances between subrelations (e.g. Coke and Pepsi customers), and then computes distances between all attributes. After several iterations, a stable set of distances between all pairs of attributes is produced.

An overview of this similarity measure is given. We are given a set $R$ of $m$ attributes. Let $r$ be a boolean $0/1$ relation over $R$. Initially, distances between attributes $A, B \in R$ are attributed to random values. Then, subrelation centers are computed. For each $t \in R$, all attributes $A_1 \dots A_t$ to which $t$ is similar (according to a criterion) are used to compute a vector $f(t)$ consisting of all the pairwise distances between $t$ and $A_t$. Then, the subrelation for each attribute $A \in R$ is the vector $c_A$, defined by the average of all vectors $f(t)$ from the previous step where $t$ and $A$ are similar. Next, for each pair of attributes $A, B \in R$, the distance is defined by computing distance between subrelation centers $c_A$ and $c_B$. This iteration is repeated until the distance between $A, B \in R$ converges. Given attributes, it is easy to compute object distances and subrelation distances.

## 12.4 Descriptions of Algorithms

In this section, a description of the key classes of categorical data clustering algorithms is provided.

## 12.4.1 Partition-Based Clustering

In the partitioning approach, objects are partitioned and may change clusters based on dis. Partitioning methods are useful for bioinformatics applications where a fixed number of clusters is desired, such as small gene expression datasets [24]. A drawback is that the user typically specifies the number of clusters as an input parameter.

### 12.4.1.1 k-Modes

The k-Modes algorithm represents a cluster by a summary of the attribute-value frequencies of objects classified under the node. Iteratively, objects are assigned to a cluster and the summaries are reevaluated. Usually, the algorithm converges after a finite (small) number of iterations. The number of clusters is user-specified.

The k-Modes algorithm is an adaptation of k-Means to categorical data. K-Modes removes the numerical-only limitation of the k-Means algorithm but maintains its efficiency in clustering large categorical datasets. K-Modes makes the following modifications: 1) it uses a dissimilarity measure for categorical objects; 2) it replaces the means of clusters with the modes; 3) it uses a frequency-based method for runtime, benefits, and drawbacks as k-Means [47]. The Hamming Distance can be used for finding an object's nearest cluster mode.

A cluster is used to assign an unassigned object to the closest cluster. Let $X = \{X_1, X_2, \dots, X_n\}$ be a set of $n$ categorical objects described by categorical attributes, $A_1, A_2, \dots, A_m$. A mode of $X$ is a vector $Q = [q_1, q_2, \dots, q_m]$ that minimizes

```
D(X,Q) = \sum_{i=1}^{n} d_i(X_i,Q)
```

where $d_i$ is a distance function, such as Hamming Distance. Then proven that the function $D(X,Q)$ is minimized if and only if every position $j$ of the mode $Q$ contains the most frequently occurring value in $A_j$, such that $fr(A_j = q_j) \geq fr(A_j = c_{i,j})$ for all $c_{i,j}$ for all $j=1, \dots, m$. Note that the mode $Q$ is not necessarily an element of $X$.

The mode of cluster $c$ is a vector $\mu_c = [\mu_{c,1}, \dots, \mu_{c,m}]$, where $\mu_{c,j}$ is the most frequent value in $c$ for the $j$-th attribute. The mode of $c$ is determined by setting $\mu_j$ to the most frequent value for the $j$-th category in $c$. To find a mode, let $n_{ij}$ be the number of objects having the $j$-th value $c_{i,j}$ in attribute $A_j$ and $fr(A_j = c_{i,j}) = n_{i,j}/n$ be the relative frequency of $c_{i,j}$ in $X$.

The basic algorithm evaluates the cost across the whole dataset, according to the cost function $P(X,Q) = \sum_{i=1}^{n} \sum_{j=1}^{m} \delta(X_{i,j}, q_j)$, each time a mode is obtained over the $k$ clusters, $n$ objects, and $m$ categorical attributes. To make the computation efficient, the efficient algorithm can be used in practice:

- 1. Select initial modes, one for each cluster.
- 2. Assign each object to the cluster with the nearest mode, according to a distance measure. Update the mode of the cluster after object allocation.
- 3. After all objects have been assigned to clusters, reset the dissimilarity of objects against the current modes. If an object is found that its nearest mode belongs to another cluster rather than its cluster, reassign it to that cluster and update the mode of both clusters.
- 4. Repeat until no object changes clusters.

In the original implementation of the k-Modes algorithm two methods were described. The first and simplest selects the $k$ distinct records from the dataset as The second method selects the frequencies of all values for all categorical attributes and stores them in an array descending order of frequency; then it assigns the most frequent values to the initial $k$ modes.

The main disadvantage of k-Modes is that (like the k-Means algorithm) it performs local solutions that are heavily dependent on the initial modes and the order of objects in the dataset.

### 12.4.1.2 k-Prototypes (Mixed Categorical and Numerical)

An extension of k-Modes k-Prototypes which handles mixed-type objects integrates the k-Means and k-Modes algorithms. The k-Prototypes algorithm is particularly useful because frequently encountered objects in real world databases are mixed-type; k-Prototypes uses a distance metric which weighs the contribution of numerical versus categorical attributes. Like the k-Means and k-Modes algorithms,

k-Prototypes iterates until few object changes.

The dissimilarity between two mixed-type objects X and Y, which are described by $p$ numerical and $m-p$ categorical attributes $A'_1, \dots, A'_p, A'_{p+1}, \dots, A'_m$, can be measured

```
d_2(X,Y) = \sum_{j=1}^{p} (x_j - y_j)^2 + \gamma \sum_{j=p+1}^{m} \delta(x_j, y_j)
```
