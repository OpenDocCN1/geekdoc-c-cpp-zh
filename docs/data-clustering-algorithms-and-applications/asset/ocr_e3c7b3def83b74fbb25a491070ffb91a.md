# A Survey of Stream Clustering Algorithms 249

the clustering process. Similarly, some of the clusters correspond to outliers and are partially populated. It is more important to ensure that assignments to "significant clusters" (for $f_n$ with a given threshold) are correct. Therefore, the work in [2] defines the concept of an $(f,b)$-significant assignment as follows:

Definition 10.6.1 An assignment error which results from the estimation of data products is $(f,b)$-significant, if a data point is incorrectly assigned to cluster index $p$ which contains at least a fraction $f$ of the points, and the correct cluster for assignment has index $q$ which satisfies the following relationship:

```
$D_{ip} \geq D_{q} + b$ (10.9)
```

It has been shown in [2] that it is possible to bound the probability of an $(f,b)$-significant error in a given assignment.

Lemma 10.6.1 The probability of an $(f,b)$-significant error in an assignment is at most equal to $k\cdot(d^2(b-f))^w$.

This can be further to bound the probability that there is no $(f,b)$-significant error over the entire course of the clustering of $N$ data points

Lemma 10.6.2 Let us assume that $N-k\cdot(d^2(b-f))^w<1$. The probability that there is at least one $(f,b)$-significant error in the clustering process of $N$ data points is by most $\frac{N\cdot k}{(b-f)d^2}^w$.

In addition, the experimental results in [2] show that the clustering process can be replaced exactly in practice with the use of this approximation process. Thus, the work in [2] proposes a fast and space-efficient method for clustering massive-dense data streams.

# 10.7 Text Stream Clustering

The problem of streaming text clustering is particularly challenging in the context of text data due to the clusters needing to be continuously maintained in real time. One of the earliest methods for streaming text clustering was proposed in [64]. This technique is referred to as the Online Spherical$k$-Means (OSKM) Algorithm, which reflects the broad approach used by the methodology. This technique divides the incoming stream into small segments, each of which can be processed effectively in memory.

Each of $k$-means iterations is applied to each such segment in order to cluster them. The advantage of using a segment-wise approach for clustering is that each segment can be held in memory multiple times as is held in memory. In addition, the centroids from the previous segment are used in the next iteration for clustering purposes. A decay factor is introduced to age out the old documents, so that the new documents are more important from a clustering perspective. This approach has been used in [64] to be extremely effective in clustering massive text streams.

A different method for clustering massive text and categorical data streams was used in [12]. This method uses an approach which examines the relationship between outliers, emerging trends, and clusters in the underlying data. Old clusters may become inactive and eventually get replaced by new clusters. Similarly, when newly arriving data points do not fit in any particular cluster, these need to be initially classified as outliers. However, as time progresses, these new points may create a distinctive pattern of activity which can be recognized as a new cluster. The temporal locality of the data stream is manifested by these new clusters. For example, the first web

© 2014 by Taylor & Francis Group, LLC