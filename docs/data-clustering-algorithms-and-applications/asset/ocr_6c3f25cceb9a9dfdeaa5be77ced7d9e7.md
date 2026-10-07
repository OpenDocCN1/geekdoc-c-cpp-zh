# Data Clustering: Algorithms and Applications

The RatioCut is defined as follows:

```
$RatioCut(A_1, \dots, A_k) = \sum_{i=1}^{k} \frac{cut(A_i, \bar{A}_i)}{|A_i|}$$
```

Here, $|A_i|$ denotes the number of vertices belonging to $A_i$. By minimizing this measure, the partitions with more balanced cluster sizes are preferred.

The objective function for NCut is defined as follows:

```
$NCut(A_1, \dots, A_k) = \sum_{i=1}^{k} \frac{cut(A_i, \bar{A}_i)}{assoc(A_i, V)}$
```

where $assoc(A_i, V) = \sum_{v_j \in A_i} d(v_j)$. Different from RatioCut which measures the balance by the cluster size, NCut focuses on the total degree within different clusters.

The incorporation of normalization into the objective function makes it NP-hard [53]. However, by relaxing some constraints, spectral clustering is a way to get the approximate solution. Specifically, unnormalized spectral clustering is a way to solve the relaxed RatioCut problem, and normalized spectral clustering are designed to solve the relaxed NCut problem.

# 8.5.1 RatioCut Relaxation

Suppose we already have $k$ vectors $\{f_i\}_{i=1}^k$ indicating the cluster labels for the vertices in the graph where $f_i = (f_{i1}, \dots, f_{in})$. Define that:

```
$f_{ij} = \begin{cases} \frac{1}{|A_i|} & \text{if } v_j \in A_i \ 0 & \text{otherwise.} \end{cases} \quad (8.6)$
```

Then, under this condition, for each cluster $i$ among $k$ clusters, we can write Equation 8.1 the unnormalized graph Laplacian as:

```
$f_i^T L f_i = \sum_{j=1}^{n} W_{ij}(f_{ij} - f_{it})^2 \n = \frac{1}{2} \sum_{v_j \in A_i, v_j \notin A_i} W_{ij}(\frac{1}{|A_i|})^2 + \sum_{v_j \in \bar{A}_i, v_j \in A_i} W_{ij}(0 - \frac{1}{|\bar{A}_i|})^2 \n = \frac{1}{2} \frac{cut(A_i, \bar{A}_i)}{|A_i|} + \frac{1}{2} \frac{cut(\bar{A}_i, A_i)}{|\bar{A}_i|}$
```

The RatioCut measure is linked to the unnormalized graph Laplacian because of the following calculation:

```
$$\sum_{i=1}^{k} f_i^T L f_i = Tr(F^T LF) \n = \sum_{i=1}^{k} \frac{cut(A_i, \bar{A}_i)}{|A_i|} \n = RatioCut(A_1, \dots, A_k)$
```

where $F \in \mathbb{R}^{n \times k}$ is formed from $f_1, f_2, \dots, f_k$.