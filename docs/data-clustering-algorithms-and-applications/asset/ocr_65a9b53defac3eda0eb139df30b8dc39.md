# Big Data Clustering

similar to each other the objects in the different clusters. Initially, $k$ objects are randomly selected as the center of clusters. The $k$-means algorithm performs the following two tasks iteratively:

+   * Step 1. Assign each object to the cluster whose center is the closest to the object.
* Step 2. For each cluster, update the center with the mean of the objects in the cluster.

PKMeans uses MapReduce to distribute the computation of k-means. PKMeans follows the general framework shown in Section 11.4.1. The partitioning is implicitly performed when the data is uploaded to the distributed file system (e.g., DFS or HDFS) of MapReduce. The local clustering, which corresponds to Step 1 above, is performed in the mapper. The global clustering, which corresponds to Step 2 above, is performed in the combiner and the reducer.
The specific data $x_1, \dots, x_n$, which are also $d$-dimensional points, of clusters are given to the mapper in the format of $\{i_j, y_j\}$ by the parameter passing mechanism of Hadoop. The mapper, the combiner, and the reducer are as:

+   * Mapper: Read the data $x_i$, and find the center $y_j$ which is closest to $x_i$. That is, $j = 	ext{argmin} ||x_i - y_j||$. Emit $i < j$.
* Combiner: Take $<j, \{y_j\}$ and emit $<j, \sum x_i, 	ext{num}$ where $	ext{num}$ is the number of objects that the combiner received with the key $j$.
* Reducer: Take $<j, \{\sum x_i, 	ext{num}\}$, and compute the new center. Emit the new center $<j, y_j>$ of the cluster.

The outputs of the reducer are centers of clusters which are fed into the mapper of the next iteration. The combiner greatly decreases the amount of intermediate data by emitting only the sum of the input.
Experimental results show that PKMeans provides good speed, scale up, and size up. The system is evaluated by the rating of running time while keeping the dataset constant and increasing the number of machines in the system. PKMeans shows near-linear speed up. The scale measures whether x-times larger system can perform x-times larger job in the same run-time as the original system. PKMeans provides a good scale up, better than 0.75 for 4 machines. PKMeans has a linear size up: given the number of machines, the running time grows linearly with the data size. Finally, PKMeans is an exact algorithm, and thus the quality of the clustering is the same as that of $k$-means.

# 11.4.5 Co-Clustering with MapReduce

DisCo $\{42\}$ is a co-clustering algorithm with MapReduce. Given a data matrix, co-clustering groups the rows and columns so that the resulting permuted matrix has concentrated nonzero elements. For example, co-clustering on documents-to-words matrix finds documents as well as groups. For an $n 	imes m$ matrix, co-clustering outputs the row and column vector $r \in \{1, \dots, k\}^n$ and $c \in \{1, \dots, l\}^m$, respectively, and $k 	imes l$ matrix $G$ where $k$ and $l$ are the number of desired row and column partitions, respectively. Searching for an optimal cluster is NP-hard [12], and thus co-clustering algorithms perform a local search. In the local search, each row is to be assigned to the best group that gives the minimum cost while the column assignments are fixed. Then in the fashion each column is iterated while the row group assignments are fixed. This process continues until the cost stops decreasing.
There are two important observations that affect the design of the distributed co-clustering algorithm on MapReduce: