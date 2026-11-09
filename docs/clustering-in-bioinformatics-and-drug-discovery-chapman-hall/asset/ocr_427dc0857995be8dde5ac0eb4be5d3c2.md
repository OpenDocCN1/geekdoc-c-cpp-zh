The second common Jarvis-Patrick variant removes the length of the nearest neighbor list, K, and supplants the K_min constraint with a percentage, P_min, the minimum percentage of nearest neighbors that need to match between any two nearest neighbors to be considered within the same cluster.

# Algorithm 4.5 Jarvis–Patrick(Data, P_min, Threshold)

```
1: NNK ← FindNN(Data, Threshold) //Create nearest neighbor table at a (dis)similarity threshold
2: p ← 1
3: repeat
4: i ← 1
5: j ← i + 1
6: C_p ← i //Add i to cluster C_p
7: K_min ← min(length(NNK(i)), length(NNK(j))) //K_min constraint min of row lengths of i and j
8: repeat
9:   if K_min criterion is met between (i,j) rows for all j in NNK then
10:     C_p ← j //Add j to cluster C_p
11:     RemoveRow(NNK, j) //Remove the jth row from NNK
12:   else
13:     j ← j + 1
14:   end if
15: until j > RowLength(NNK)
16: RemoveRow(NNK, i) //Remove the ith (first) row from NNK
17: p ← p + 1
18: until NNK = NULL
19: Output: C //Return set of clusters C
```

# 4.3 Spectral Clustering

Spectral clustering was introduced in the late 1990s in conjunction with image processing. For example, clustering of pixels is an important part of image segmentation, where pixels may be vectors of RGB colors or the seven spectral bands common in satellite imagery. Such problems can be relatively large, though the dimension is typically small, in the hundreds of thousands or millions of pixels, so spectral clustering is typically done on small images or subsets of larger images. Luckily, computing eigenvalues and eigenvectors of fairly large matrices is possible, making spectral clustering of modestly large data sets in the thousands of data items in higher dimensions more reasonable. Therefore, spectral clustering has begun to be used in cheminformatics applications, with several groups now exploring its efficacy with respect to various data types within the early drug discovery process [18, 58].