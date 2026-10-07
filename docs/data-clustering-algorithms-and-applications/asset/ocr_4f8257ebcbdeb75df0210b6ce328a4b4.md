# Clustering Categorical Data

4. Pass along the hierarchy: the COBWEB algorithm is called on the object and the subtree rooted in the node.

A benefit of COBWEB is that it can adjust the number of clusters in a partition, without the user specifying this input parameter. A disadvantage of COBWEB is that it assumes categorical attributes are independent and may assume correlated attributes are independent.

# 12.4.2.3 LIMBO

LIMBO handles the clustering problem by building a tree, where a node contains statistics about the objects that are members of the corresponding cluster. New objects are added to the tree in a top-down fashion by finding the best matching and breaking it into a new node, extending the tree. LIMBO employs Entropy and the Information Bottleneck (IB) framework for quantifying the relevant information preserved when clustering [16]. LIMBO scales to large datasets using a memory bound storage for the data, improving on the scalability of other hierarchical clustering algorithms. The most similar to LIMBO is the LOCOOL a nonhierarchical algorithm also based on minimization, which was presented previously.

LIMBO summarizes a cluster of objects using a Distribution Cluster Feature (DCF). For a cluster c, DCF(c) = (p(c), p(A(c))), where p(c) is the probability of cluster c, and p(A(c)) is the conditional probability distribution of the attributes within cluster c. The DCFs are used to calculate the distance between clusters or a cluster and an object. The LIMBO algorithm proceeds in three phases. In the first phase, the DCF tree is constructed to summarize the data. In the second phase, the DCFs of the tree leafs are merged to produce a number of clusters. In the third phase, each object is associated with the DCF to which the object is closest.

Phase 1 by starting and inserting objects into the DCF tree one or more DCFs. A tree is created, where a node contains each object. Object O is converted into DCF(o). Then, starting from the root, a path downward in the DCF tree is traced. When at nonleaf node, the DCF(o) and each DCF of the node is computed, finding the closest DCF to DCF(o). The child pointer of this entry to the next level of the tree. When at a leaf node, DCF(c) denotes the DCF in the leaf node that is closest to DCF(o). DCF(c) is the summary of some cluster c. At this point, the decision is made whether o belongs to the cluster or not. If there is an empty leaf in the leaf that contains DCF(c) (according to a space bound) DCF(o) is placed in that leaf. If there is no empty leaf and there sufficient free space, the leaf is split into two leaves. The two DCFs in the leaf node that are farthest apart are used as seeds for the new leaves. The remaining DCFs and DCF(o) are placed in the leaf that contains the closest DCF.

Phase 2 clusters the leafs of the DCF tree. After the construction of the DCF tree, the leaf nodes represents the DCFs of a cluster C objects. Each DCF corresponds to a cluster c ∈ C and contains statistics for clustering probability p(c). The Agglomerative Information Bottleneck (AIB) algorithm is used to cluster the DCFs in the leafs and produce clustering of the DCFs. Any clustering algorithm is applicable at this phase of the algorithm.

Phase 3 associates objects with clusters. For a chosen value of k, Phase 2 produced k DCFs In the final phase 3, a scan over the dataset assigns each object to the cluster whose representative DCF is closest to the object.

# 12.4.3 Density-Based Clustering

Density-based approaches use a local density criterion for clustering categorical data; clusters are subspaces in which the objects are dense and separated by subspaces of low density. Densitybased methods are used in bioinformatics for finding the subsets in networks, typical