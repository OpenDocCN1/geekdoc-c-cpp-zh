# Chapter 11

# Big Data Clustering

Hanghang Tong
IBM T. J. Watson Research Center
Yorkown Heights, NY
htong@us.ibm.com

U Kang
KAIST
Seoul, Korea
uk@cs.cmu.edu

+   11.1 Introduction ... 259
11.2 One-Pass Clustering Algorithms ... 260
11.2.1 CLARANS: Fighting with Exponential Search Space 260
11.2.2 BIRCH: Fighting with Limited Memory 261
11.2.3 CURE: Fighting with the Irregular Clusters 263
11.3 Randomized Techniques for Clustering Algorithms 263
11.3.1 Locality-Preserving Projection 264
11.3.2 Global Projection ... 266
11.4 Parallel and Distributed Clustering Algorithms 268
11.4.1 General Framework 268
11.4.2 DBBC: Density-Based Clustering 269
11.4.3 ParMETIS: Graph Partitioning 269
11.4.4 PKMeans: K-Means with MapReduce 270
11.4.5 DisCo: Clustering with MapReduce 271
11.4.6 BoW: Subspace Clustering with MapReduce 272
11.5 Conclusion 274
Bibliography 274

# 11.1 Introduction

With the advance of Web2.0, the data size is increasing explosively. For example, Twitter data spans terabytes; Wikipedia data (e.g., articles and authors) is of similar size; web-click data is reported to reach petabyte scale [36]; Yahoo! web graph in 2002 has more than 1 billion nodes and almost 7 billion edges [27].

On the other hand, many data clustering algorithms have a high intrinsic complexity. For example, the classic k-means clustering is NP-hard when k=2. The normalized cut (NCut), a representative spectral clustering algorithm, is also NP-hard [43]. Therefore, a key challenge for data clustering lies in its scalability, that is, how we can speed up/scale the clustering algorithms with the minimum sacrifice to clustering quality.

At the high level, many data clustering algorithms have the following procedure: after some