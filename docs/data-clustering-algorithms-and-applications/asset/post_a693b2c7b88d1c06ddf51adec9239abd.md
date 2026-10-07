
## 422 Data Clustering: Algorithms and Applications

all unnumbered vertices of the current partition are added to the current partition until it is big enough and so on.

The graph-growing algorithms are very fast and able to divide the graph into the desired number of partitions directly, avoiding recursive bisection. As such, their running time is typically independent of the number of desired subpartitions. Although fast, the quality of the partitions is not always good and the last partitions are disconnected when partitioning into several subpartitions [51]. Given a predefined size of "big enough," clusters often tend to be of the same size which may not result in the best partitions of a graph from a qualitative point of view. They are also sensitive to the choice of the starting vertex. But one can run the process with different starting vertices and choose the best result since these algorithms are fast.

### 17.6.1 Kernigan-Lin Algorithm

One of the earliest graph-partitioning algorithms is the Kernigan-Lin algorithm [90], often abbreviated as K/L. It was originally developed to optimize the performance of electronic circuits onto printed cards to minimize the number of connections between cards. The K/L algorithm does not create partitions, rather improves them iteratively. The original idea was to take random partitions and apply K/L to.

Let us use some notations before explaining the algorithm. It is more convenient to describe the graph with weighted edges. $(\mathcal{V}, \mathcal{E}, \mathcal{W}_e)$ is a graph with partitions $A$ and $B$ such that $diff$-value of a vertex $v$ is defined to be the cut-size which will decrease when it is moved to the other partition. That, for $v \in \mathcal{V}_A:$

$$diff(v) = diff(v, \mathcal{V}_A, \mathcal{V}_B) := \sum_{b \in \mathcal{V}_B} w_e(e_{v,b}) - \sum_{a \in \mathcal{V}_A} w_e(e_{v,a})$$

It is obvious that moving a vertex from one partition to the other changes only the vertex's $diff$-value and the $diff$-values of its neighbors. The $gain$-value of a pair of vertices is the change in cut-size if the pair is paired.

**Lemma 17.6.1** For two partitions $A$ and $B$ and $a \in \mathcal{V}_A$ and $b \in \mathcal{V}_B$, if $a$ and $b$ are interchanged, the gain is

$$gain(a,b) = gain(a,b, \mathcal{V}_A, \mathcal{V}_B) := diff(a) + diff(b) - 2w_e(e_{a,b})$$

**Proof 3** Let $c$ be the cost due to all connections between $A$ and $B$ that do not overlap $a$ or $b$.

$$T = c + \sum_{y \in \mathcal{V}_A} w_e(e_{a,y}) + \sum_{x \in \mathcal{V}_B} w_e(e_{x,b}) - w_e(e_{a,b})$$

Let $T'$ be the new cost after swapping $a$ and $b$. Then, we have:

$$T' = c + \sum_{x \in \mathcal{V}_B} w_e(e_{a,x}) + \sum_{y \in \mathcal{V}_A} w_e(e_{y,b})$$

Now, gain is the change in cost:

$$T - T' = \sum_{y \in \mathcal{V}_A} w_e(e_{a,y}) - \sum_{x \in \mathcal{V}_B} w_e(e_{a,x}) + \sum_{x \in \mathcal{V}_A} w_e(e_{b,x}) - \sum_{y \in \mathcal{V}_B} w_e(e_{y,b}) - w_e(e_{a,b}) - w_e(e_{a,b}) = diff(a) + diff(b) - 2w_e(e_{a,b})$$

**Algorithm 37** Kernighan-Lin

Given two partitions $\mathcal{V}_A, \mathcal{V}_B$:

1. Compute diff-value for all vertices
2. Unmark all vertices
3. Let, $k_0 = cut-size
4. for $i = 1$ to $\min(|\mathcal{V}_A|, |\mathcal{V}_B|)$ do
   - Find the pair $((a_i, b_i)$ | $a_i \in \mathcal{V}_A, b_i \in \mathcal{V}_B$) with biggest gain among all unmarked vertices
   - Mark $a_i$ and $b_i$
   - for each neighbor $v$ of $a_i$ or $b_i$ do
     - Update $diff(v)$ assuming $a_i$ and $b_i$ have swapped,
     $$diff(v) := diff(v) + \begin{cases} 2w_e(e, a_i) - 2w_e(e, b_i) & \text{for } v \in \mathcal{V}_A \\ 2w_e(e, b_i) - 2w_e(e, a_i) & \text{for } v \in \mathcal{V}_B \end{cases}$$
   - $k_i = k_{i-1} - gain(a_i, b_i)$, that is, $k_i$ would be the cut-size if $a_1, a_2, \dots, a_i$ and $b_1, b_2, \dots, b_i$ have been swapped
5. end for
6. Select the smallest $j$ such that $k_j = \min(k_i)$
7. Swap the $j$ pairs. That is,
   $$\mathcal{V}_A = \mathcal{V}_A - \{a_1, a_2, \dots, a_j\} \cup \{b_1, b_2, \dots, b_j\}$$
   $$\mathcal{V}_B = \mathcal{V}_B - \{b_1, b_2, \dots, b_j\} \cup \{a_1, a_2, \dots, a_j\}$$
8. Repeat until no swap pairs is achieved

## Network Clustering

### 17.7 Agglomerative and Divisive Clustering

Agglomerative approaches start with each node as a community. Divisive approaches, on the other hand, work in the opposite direction. That is, they start with the whole graph as a single cluster and subsequently produce a binary tree, known as a dendrogram, where edges represent partitions.

The idea of betweenness was proposed to be used in the Girvan-Newman (GN) [68] algorithm. This has been proposed and used moves with betweenness scores to split the network. There are also variations such as random-walk betweenness and current-flow betweenness that assign the score.

**Algorithm 38** Divisive Clustering [105]
Input: Graph G, number k
repeat
  - Calculate betweenness score of each edge using suitable betweenness measure
  - Remove the edge with maximum betweenness score
  - Recalculate betweenness score of all edges
until Desired number of clusters are obtained

Experiments showed that the choice of betweenness measure is not very crucial as the recalculation step is executed [131]. The results for different betweenness differ only slightly. Although very intuitive, the algorithm is very costly in terms of computation. Computation of the betweenness score for all edges is $O(|V||E|)$ time. The whole algorithm takes $O(|V|^2)$ time.

### 17.8 Spectral Clustering

Spectral clustering has become one of the most popular clustering methods in recent years. It is simple to implement and can be efficiently solved with standard linear algebra software. Spectral
