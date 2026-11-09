must be made if the kth neighbor is not unique due to ties in proximity. This decision impacts the clustering step of the algorithm: if two compound NN lists have j neighbors in common, those compounds are in the same cluster. If only one of the tied kth neighbors remains in NN list, there is the possibility that some possible neighbors in common are ignored, impacting what data items get clustered. In the Pmin form of the algorithm, there are two parameters: k is the same as in Kmin; and p represents the percentage of neighbors, such if the percentage of neighbors in common is greater than or equal to p, then the neighbors are in the same cluster. The source of the ambiguity is the same for Pmin. residing in that the kth neighbor may not be unique. but the parameter p may change amount of ambiguity. Both forms of Jarvis-Patrick with the use of ties in the kNN can be transformed into algorithms that produce overlapping clusters.

# 9.6.3  *K-Means*

*K-means* clustering [43, 100] is a common clustering algorithm used in many fields to cluster relatively large data sets. It is more likely to be used with continuous data, but binary string data are sometimes employed. To use K-means with fingerprints, the 0, 1 bits are converted to continuous valued 0.0, and 1.0 respectively, and treated as separate variables. The algorithm steps are as follows:

+   - Choose k seed centroids from data set (e.g., quasi-randomly via van der Corput sequence)
+   - Find nearest neighbors to each of the centroids forming nearest neighbor group
+   - Recompute new centroids from nearest neighbor lists of old centroids.
+   - Repeat 2 until no neighbors change groups or some iterative threshold.

In step 2 centroids may compete for nearest neighbors in common due to ties in proximity. Given that the Euclidean distance is often used with this algorithm, the number of ties in proximity can be very high. In the K-Modal version of this algorithm, modal fingerprints are used to define centropytos rather than the metric space notion of centroids.

+   - Choose k seed modes from the data set
+   - Find nearest neighbors to the modes
+   - Re-compute new modes
+   - Same as step 4 in continuous *K-means*

Modes in step three can be determined via a simple matching coefficient [121]. The modes again may compete for nearest neighbors in common due to ties in proximity