The generic exclusion region Algorithm 3.5 can be modified to produce overlapping clusters given false singletons, under the assumption that it is possible for false singletons to have nearest neighbors in more than one exclusion region. One could argue that it would be better to distribute the false singletons to that exclusion region with its nearest neighbor. This would indeed produce disjoint regions. However, with discrete measures, there can be ties in nearest neighbor values. This ambiguity can be used to produce overlapping clusters. Figure 3.10 displays the fraction of a dataset involved in overlaps versus the Tanimoto threshold applied. A comparison of three different fingerprints is made with the shortest key based fingerprint revealing the largest portion of the data set participating in overlapping groups.

```
Algorithm 3.6 ExclusionRegionOverlapping(SparseMatrix)
1: repeat
2:     TiedRows ← FindLargestSetsNN(SparseMatrix) //Find largest row(s)
3:     i = 1
4:     repeat
5:         C ← AssignClusters(TiedRows[i]) //Assign rows to cluster non-disjoint clusters
6:         Append(C, G) //Append cluster C to set of clusters G
7:         i = i + 1
8:     until i == |TiedRows| //Repeat until largest tied rows processed
9:     SparseMatrix ← SparseMatrix \ TiedRows //Remove row and its elements from the matrix
10: until SparseMatrix == NULL
11: F ← FindFalseSingletons(SingletonClusters(G))
12: G' ← DistributeFalseSingletons(F, G) //Distribute false singletons to any cluster with a NN
13: Output : G'
```

Since overlapping clusters are a cover rather than a partition, any significant overlapping can be explosive combinatorially. If the groups are well-separated at the scale of the threshold, there will be very little ambiguity, and in practice in this instance most of the overlapping concerns a few false singletons, and perhaps a few overlapping groups of the same size.

# 3.6 Fuzzy

Fuzzy clustering is related to the principle of overlapping clusters, but unlike the simple overlapping clustering expressed in the last section, data elements have a degree of membership across those clusters that might contain them. It is sometimes useful to regard the degree of membership as a