![](bbox=[0.271, 0.103, 0.784, 0.401])

**FIGURE 9.16:** Example with Two Clusters. Cluster Centers are Marked with Solid Circles

the horizontal axis, then y is also “high”, defined as near the top end of the vertical axis. The relation can be described by the rule:

IF x is high THEN y is high (9.46)

It seems possible to make some intuitive definitions of the two instances of the word ‘high’ in the rule, based on the location of the cluster center. The cluster in the lower left part of the figure, could be described as

IF x is low THEN y is low (9.47)

# 9.6.3 Fuzzy C-Means (FCM) Clustering

Occasionally the points between cluster centers can be assumed to have a gradual membership of both clusters. Naturally this is accommodated by fuzzifying the definitions of “low” and “high” in (9.46) and (9.47). The fuzzified c-means algorithm allows each data point to belong to a cluster to a degree specified by a membership grade, and thus each point may belong to several clusters.

The fuzzy c-means algorithm partitions a collection of K data points specified by m-dimensional vectors u_k (k=1,2, ... K) into c fuzzy clusters, and finds a cluster center in each, minimizing an objective function. Fuzzy c-means is different from hard c-means, mainly because it