```
RUN2  Enter the no. of Vertices : 5
Enter the Weight of the Edge from V1 to V2 : 1
Enter the Weight of the Edge from V1 to V3 : 0
Enter the Weight of the Edge from V1 to V4 : 1
Enter the Weight of the Edge from V1 to V5 : 1
Enter the Weight of the Edge from V2 to V1 : 1
Enter the Weight of the Edge from V2 to V3 : 1
Enter the Weight of the Edge from V2 to V4 : 1
Enter the Weight of the Edge from V2 to V5 : 0
Enter the Weight of the Edge from V3 to V1 : 0
Enter the Weight of the Edge from V3 to V2 : 1
Enter the Weight of the Edge from V3 to V4 : 1
Enter the Weight of the Edge from V3 to V5 : 1
Enter the Weight of the Edge from V4 to V1 : 1
Enter the Weight of the Edge from V4 to V2 : 1
Enter the Weight of the Edge from V4 to V3 : 1
Enter the Weight of the Edge from V4 to V5 : 1
Enter the Weight of the Edge from V5 to V1 : 1
Enter the Weight of the Edge from V5 to V2 : 0
Enter the Weight of the Edge from V5 to V3 : 1
Enter the Weight of the Edge from V5 to V4 : 1
Incidence Matrix is . . .
    E1  E2  E3  E4  E5  E6  E7  E8
V1  1   1   1   0   0   0   0   0
V2  1   0   0   1   1   0   0   0
V3  0   0   0   1   1   0   1   0
V4  0   1   0   0   1   1   0   1
V5  0   0   1   0   0   0   1   1
Total No. of Vertices : 5
Total No. of Edges : 8
```

# 4.9.2 Adjacency Matrix

A graph containing n vertices can be represented by a matrix with n rows and n columns. The matrix is formed by storing the edge weight in its i^th row and j^th column of the matrix, if there exists an edge between i^th and j^th vertex of the graph, and a 0, if there is no edge between i^th and j^th vertex of the graph. Such matrix is referred as an adjacency matrix. Note that for an unweighted graph, the edge weight is 1.

```
AdjMat[i] [j] = Weight of the edge, if there is a path from vertex Vi to Vj.
= 0, Otherwise.
```