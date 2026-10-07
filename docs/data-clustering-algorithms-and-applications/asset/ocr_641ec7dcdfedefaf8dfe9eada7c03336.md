# 46 Data Clustering: Algorithms and Applications

[32], FTS adopted Landau–Vishkin (LV) to test three types of mismatches: insertion, deletion, substitution. Insertion means that all we need to insert $k$, or fewer, terms into the $FS_i$ in order to match $FS_j$. Deletion, in contrast, means we need to delete. While substitution we need to substitute terms from $FS_j$ with terms from $FS_i$.

These merged clusters are prone to overlap. Accordingly, merging will be performed when measuring the amount of overlap using the *Jaccard Index*:

```
$J(C_i, C_j) = \frac{|C_i \cup C_j|}{|C_i \cap C_j|}$
```

The larger $J(C_i, C_j)$ is, the more the overlap would be. The merge takes place here when the overlap exceeds a user defined threshold, $\delta$. However, the final number of clusters could be refined. In this case, this step would be repeated until the clusters meet the user’s demand.

# Algorithm 7 Frequent Term Sequence (FTS)

+   **Input:**
$D$: dataset
$min_{sup}$: minimum support
$\Psi(\cdot, \cdot)$: frequent item setter
$n$: number of documents
$K$: number of clusters
$\delta$: overlap threshold
**Output:**
Clusters
**Initialize:**
$Clusters = \{\}$
1: Frequent 2-Term Set $FS = \Psi(D, min_{sup})$
2: $D \leftarrow Reduce D$ by removing every term $f \notin FS$.
3: $G \leftarrow GST(D)$
4: **for** each node $j$ **in** $G$
5: **if** node $j$ has Frequent term $FS_j$ with documents id $ID_j$
6: $C_j \leftarrow \{FS_j, ID_j\}$
7: $Clusters \leftarrow Clusters \cup C_j$
8: **end if**
9: **end for**
10: Use Landau–Vishkin to find $k$--mismatch
11: $Clusters \leftarrow Merge$ clusters according to Landau–Vishkin results
12: **while** number of $Clusters > K$
13: $Clusters \leftarrow Combine$ Overl clusters based on Jaccard Index and $\delta$
14: **end while**

In Algorithm 7, the most time consuming element is constructing GST, it is still linear element with the number of terms. In [32], the terms reduction after refining the frequent terms is huge; it exceeds 90% in all cases.

Similar to FTS, [32] proposed another frequent term set algorithm (FTMS) that is based on the synonymous (synsets) of terms instead of the term itself. This is more adaptable with human language where we may use different terms to refer to the same meaning. This proposed algorithm used a WordNet dictionary to retrieve the synsets of word and replace each with the original term. each two synsets that intersect in at least one were merged into one synset. Thus, the

© 2014 by Taylor & Francis Group, LLC