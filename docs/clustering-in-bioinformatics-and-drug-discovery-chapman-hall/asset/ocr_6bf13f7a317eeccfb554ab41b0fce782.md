asymmetric matrix. Here, the largest nearest neighbor table, whether in the row or column space, that is left in the matrix at each iteration is considered the next cluster. Setting up the asymmetric sparse matrix data structure is a bit more complex than the simple nearest neighbor table of the symmetric form of the algorithm, and the manipulation of that matrix to remove all of those members in the exclusion region also requires searching in both the row and column space of the matrix. The algorithm is therefore roughly twice as slow as the symmetric version, providing twice as much space is used to store both the row and column space. Smaller memory usage can be arranged, but only at the expense of the search time.

```
~~~
Algorithm 8.2 AsymmetricExclusionRegion(AsymSparseMatrix)
1: repeat
2:   C ← FindLargestSetNN(AsymSparseMatrix) //Assign largest row (or column) in matrix to cluster
3:   SparseMatrix ← SparseMatrix \ C //Remove row (or column) and its elements from the matrix
4:   Append(C,G) //Append cluster C to set of clusters G
5: until SparseMatrix == NULL
6: Output : G
~~~
```

In a bit of irony, the above asymmetric clustering algorithm with the use of SAM (sequence alignment and modeling system with the use of hidden Markov models), akin to edit distance in generation of asymmetric associations, was utilized for bank customer retention segmentation clustering [110]. Clearly, the asymmetry inherent in genetic sequence data relationships could utilize the same technique.

# 8.3 Glossary

+   - **asymmetric matrix:** a square matrix where the (i,j) element does not necessarily equal (j,i)
+   - **homology model:** a prediction of a 3D protein structure for a novel protein sequence that shares sequence homology with a known protein structure
+   - **similarity searching:** an m×n matrix of similarities where m ≪ n
+   - **skew symmetric:** the average difference between the (i,j)th element and the (j,i)th element in an asymmetric matrix