We note that the above definition of edge coherence is focused on *relative presence* of subgraph patterns rather than the absolute presence. This ensures that only significant patterns are found. Therefore, large numbers of irrelevant patterns with high frequency but low significance are not considered. While the coherence definition is more effective, it is computationally quite challenging because of the size of the search space that may need to be explored. The randomized scheme discussed here is specifically designed in order to handle this challenge.

Next, the class discrimination power of the different subgraphs is defined. For this purpose, the *class confidence* of the edge set $P$ with respect to the class label $r \in \{1 \ldots m\}$ is defined as follows.

**Definition 9.5.2**  *Among all graphs containing subgraph $P$, let $s(P,r)$ be the fraction belonging to class label $r$. We denote this fraction as the confidence of the pattern $P$ with respect to the class $r$.*

Correspondingly, the concept of the dominant class confidence for a particular subgraph is defined.

**Definition 9.5.3**  *The dominant class confidence $DI(P)$ or subgraph $P$ is defined as the maximum class confidence across all the different classes $\{1 \ldots m\}$.*

A significantly large value of $DI(P)$ for a particular test instance indicates that the pattern $P$ is very relevant to classification, and the corresponding dominant class label may be an attractive candidate for the test instance label.

In general, one would like to determine patterns that are interesting in terms of absolute presence, and are also discriminative for a particular class. Therefore, the parameter-pair $(\alpha, \theta)$ is defined, which corresponds to threshold parameters on the edge coherence and class interest ratio.

**Definition 9.5.4**  *A subgraph $P$ is said to be $(\alpha,\theta)$-significant, if it satisfies the following two edge-coherence and class discrimination constraints:*

**(a) Edge Coherence Constraint:** *The edge-coherence $C(P)$ of subgraph $P$ is at least $\alpha$. In other words, it is the case that $C(P) \geq \alpha$.*

**(b) Class Discrimination Constraint:** *The dominant class confidence $DI(P)$ is at least $\theta$. In other words, it is the case that $DI(P) \geq \theta$.*

The above constraints are quite challenging because of the size of the search space that needs to be explored in order to determine relevant patterns. This approach is used, because it is well suited to massive graphs in which it is important to prune out as many irrelevant patterns as possible. The edge coherence constraint is designed to prune out many patterns that are abundantly present, but are not very significant from a relative perspective. This helps in more effective classification.

A probabilistic *min-hash approach* is used for determining discriminative subgraphs. The min-hash technique is an elegant probabilistic method, which has been used for the problem of finding interesting 2-itemsets [32]. This technique cannot be easily adapted to the graph classification problem, because of the large number of distinct edges in the graph. Therefore, a 2-dimensional compression technique was used, in which a min-hash function will be used in combination with a more straightforward randomized hashing technique. We will see that this combination approach is extremely effective for graph stream classification.

The aim of constructing this synopsis is to be able to design a continuously updatable data structure, which can determine the most relevant discriminative subgraphs for classification. Since the size of the synopsis is small, it can be maintained in main memory and be used at any point during the arrival of the data stream. The ability to continuously update an in-memory data structure is a natural and efficient design for the stream scenario. At the same time, this *structural synopsis* maintains sufficient information, which is necessary for classification purposes.

For ease in further discussion, a tabular binary representation of the graph data set with $N$ rows and $n$ columns will be utilized. This table is only *conceptually* used for description purposes, but it is *not explicitly maintained* in the algorithms or synopsis construction process. The $N$ rows correspond