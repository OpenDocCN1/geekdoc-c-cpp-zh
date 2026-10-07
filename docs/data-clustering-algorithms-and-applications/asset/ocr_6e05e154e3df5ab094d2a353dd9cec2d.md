# Clustering Categorical Data

Input: a set S of objects.
Parameters: (1) δϕ : the increment for ϕ.
(2) threshold for ϕ : the maximum number of values that can differ between an object and the mode of its cluster.
Default parameter values: (1) δϕ=1.
(2) threshold = the number of categorical attributes m.

Output: a set of clusters.
Method:
1. Order objects by decreasing frequency of their attributes.
2. Insert the first object into a new cluster, use the mode of the cluster, and remove the object from S.
3. Initialize ϕ to 1.
4. Loop through the objects until S is empty or ϕ > threshold
a. For each object o in S
i. Find o's nearest cluster c using the dissimilarity metric to compare o with the modes of all existing cluster(s).
ii. If the number of different values between o and c's mode is larger than ϕ, insert o into a new cluster
iii. Otherwise, insert o into c and update c's mode.
iv. Remove o from S.
b. For cluster c, if there is only one object in c, remove and put the object back in S.
c. If in this no objects were inserted in a cluster with size > 1, increment ϕ by δϕ.

FIGURE 12.7: The MULIC clustering algorithm.

12.7 shows the main part of the MULIC clustering algorithm. MULIC does not store the cube in makes simplifications to decrease the runtime. A MULIC starts from a dense area and expands outwards via radius represented by the ϕ variable. When MULIC expands a cluster it does not search all member objects as HIERDENC does. Instead, it uses a model that summarizes the content of the cluster. The mode is a vector μ = {μ₁, ..., μm} where μi is the most frequent value for the ith attribute in the given cluster c [47]. The MULIC algorithm ensures that whenever an object o is clustered, it is inserted into the cluster with the least dissimilar mode. The default dissimilarity metric between o and μ is the Hamming distance, although any metric could be used. A MULIC cluster consists of layers formed gradually, by relaxing the maximum dissimilarity criterion for inserting objects into clusters. MULIC does not require the user to specify the number of clusters and can identify outliers.

MULIC has several differences from traditional hierarchical clustering, which stores all distances in an upper square matrix and updates the distances after each merge [50, 61]. MULIC clusters have a clear separation. MULIC does not require a cut-off to identify the clusters, in hierarchical clustering; this of benefit for some MULIC applications, such as the one on protein interaction networks discovered in [7]. One of the drawbacks of hierarchical clustering is that the sequence of cluster mergers affect the result and “bad” mergers cannot be done later in the process. Moreover, if several large clusters are merged, interesting local cluster structure is likely to be lost. MULIC does not merge clusters during the clustering process.