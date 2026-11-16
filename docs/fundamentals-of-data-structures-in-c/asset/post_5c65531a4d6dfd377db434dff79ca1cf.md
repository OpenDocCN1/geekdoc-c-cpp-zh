
```
? 3
Delete the Node from the Tree
Enter the Element for Deleting the Node : 25
? 5
Binary search tree is ...
40
  15
? 3
Delete the Node from the Tree
Enter the Element for Deleting the Node : 40
? 5
Binary search tree is ...
15
? 3
Delete the Node from the Tree
Enter the Element for Deleting the Node : 15
? 5
Binary Tree is Empty ...
? 6
End of Run of your Program ...
```

## 4.6 Applications of Trees

- 1. Trees represent hierarchical relationships between individual data items. We can use trees to store information that naturally forms a hierarchy. For example, in Windows, go to command line and type tree. You can see the folder structure organized and stored as a tree structure.
- 2. Binary trees are used to represent arithmetic expressions. This feature is used in calculators and compilers for parsing the expressions and executing them.
- 3. Binary search tree arranges its node elements in a sorted manner, so the information can be easily inserted, deleted and searched.
- 4. Spell check and auto correct suggestions during typing are enabled using tree structure.
- 5. Used in router algorithms to identify where the next path/route of the packet to be sent.

## 4.7 The Set Representation, Union and Find Operation

The Set is a collection of data items that are accessed by operations such as Union, Intersection and Set Difference. A Set is an unbound collection of distinct elements. Consider the following collection of elements of set S shown in Fig. 4.21.

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_266_0.png)

Fig. 4.21 : An example of set.

The following are some of the different sets formed from the above collection of elements.

```
S = (95, 20, 17, 33, 4, 134)
S = (33, 95, 17, 4, 20, 134)
S = (134, 20, 95, 4, 17, 33)
S = (134, 17, 20, 4, 95, 33)
S = (4, 20, 134, 33, 17, 95)
S = (17, 134, 33, 95, 4, 20)
S = (20, 4, 95, 17, 134, 20)
```

Two sets are said to be disjoint set if they do not share any elements. Consider Fig. 4.21 which shows the two disjoint sets.

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_266_1.png)

Fig. 4.22 : An example of disjoint set.

The above two sets are disjoint, since they do not share any elements between each other.

The different operations that are carried in a set / disjoint set are as follows,

- find(x) - Find the unique representative of the set that contains "x".
- union(x, y) - Combine the sets containing "x" and "y" into a single set (note that before union operation "x" and "y" must be in different sets).
- make(x) - Create a single set, containing the element "x".

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_266_2.png)

Fig. 4.23 : Sets to explain find operation

Fig. 4.23 shows three sets A, B and C. The find operation of find (256) returns the Set C, which contains the element 256. find (256) = Set C.

The union operation is shown in Fig. 4.25 for the elements 95 and 134 for the three sets A, B and C is shown in Fig. 4.24.

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_267_0.png)

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_267_1.png)

### 4.7.1 Smart Union Algorithms

The two different smart union algorithms are as follows,

- Union-by-size.
- Union-by-height.

Consider the initial setup of a forest (collection of trees) in Fig. 4.26 below. The trees (not necessarily binary trees) are implemented using an array, using the parent of each node. The value of the array with -1 indicates the root node of the tree.

| INDEX | NODE | VALUE |
|---|---|---|
| 0 | A | -1 |
| 1 | B | -1 |
| 2 | C | -1 |
| 3 | D | -1 |
| 4 | E | -1 |
| 5 | F | -1 |
| 6 | G | -1 |

Fig. 4.26 : Initial setup of a forest.

To perform the operation of an union of two sets, merge the two trees by making the root of one tree, a child of the root of the other tree. Fig. 4.27 shows the forest after union of D and E. Fig. 4.28 shows the forest after union of F and G. Fig. 4.29 shows the forest after union of D and F.

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_268_0.png)

| INDEX | NODE | VALUE |
|---|---|---|
| 0 | A | -1 |
| 1 | B | -1 |
| 2 | C | -1 |
| 3 | D | -1 |
| 4 | E | D |
| 5 | F | -1 |
| 6 | G | -1 |

**Fig. 4.27 : Setup of a forest after union(D, E)**

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_268_1.png)

| INDEX | NODE | VALUE |
|---|---|---|
| 0 | A | -1 |
| 1 | B | -1 |
| 2 | C | -1 |
| 3 | D | -1 |
| 4 | E | D |
| 5 | F | -1 |
| 6 | G | F |

**Fig. 4.28 : Setup of a forest after union(F, G)**

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_268_2.png)

| INDEX | NODE | VALUE |
|---|---|---|
| 0 | A | -1 |
| 1 | B | -1 |
| 2 | C | -1 |
| 3 | D | -1 |
| 4 | E | D |
| 5 | F | D |
| 6 | G | F |

**Fig. 4.29 : Setup of a forest after union(D, G)**

In case of union-by-size algorithm, we represent the root node of the tree with the size of the tree, hence for node D we represent the value as -4 since it contains 4 trees as shown in Fig. 4.30. In union-by-size algorithm, we always make the smaller tree a subtree of the larger tree. When depth increases, the tree is smaller than the other side. Thus, after union, it is at least twice as large as the earlier stage.

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_269_0.png)

| INDEX | NODE | VALUE |
|---|---|---|
| 0 | A | -1 |
| 1 | B | -1 |
| 2 | C | -1 |
| 3 | D | -4 |
| 4 | E | D |
| 5 | F | D |
| 6 | G | F |

Fig. 4.30 : Union-by-size

In case of union-by-height algorithm, we represent the root node of the tree with the height of the tree, hence for node D we represent the value as -3 since the height is 3 as shown in Fig. 4.31. In case of union-by-height algorithm, we always make the shorter tree a subtree of the higher tree.

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_269_1.png)

| INDEX | NODE | VALUE |
|---|---|---|
| 0 | A | -1 |
| 1 | B | -1 |
| 2 | C | -1 |
| 3 | D | -3 |
| 4 | E | D |
| 5 | F | D |
| 6 | G | F |

Fig. 4.31 : Union-by-height

### 4.7.2 Path Compression

Consider we have an algorithm, that does all the basic computations (i.e., insert, delete, modify, view and traversal) in a relatively faster time, but sometimes the search operation can take relatively more time because of the shape in a given tree. To decrease the time taken for the search operation, after we do a search on a node N, remember the path of the node N to the root. Then traverse the path a second time and make all the nodes in the path to point to the root of the tree. This shortens the length of the path from the node accessed to the root node and makes the tree shorter. This technique is referred to as path compression. Fig. 4.32 shows the tree before path compression in which node G is to be searched. Fig. 4.33 shows the tree after path compression, where all the nodes of the tree and connected to the root node of the tree “A”.

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_270_0.png)

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_270_1.png)

## 4.8 Graphs

A graph is a non-linear data structure that represents relationships between its adjacent elements. There is no hierarchical relationship between the adjacent elements in case of graphs. A graph consists of a set of non-empty vertices (referred as nodes in case of trees), together with a set of edges, and each edge joins two different vertices. A path is a sequence of distinct vertices each adjacent to the next, except possibly the first vertex and last vertex is different. In Fig. 4.34 1, 2, 3 is path and 3, 4, 1 is also a path. A cycle is path containing at least three vertices such that the starting and the ending vertices are the same. In Fig. 4.34, the path formed by vertices 1, 2, 3, 4 is a cycle.

### 4.8.1 Definitions in Graphs

Graphs are generally classified as,

- Undirected graph.
- Directed graph.

If an edge between any two nodes is not directionally oriented, a graph is referred as an undirected graph or unqualified graph. Fig. 4.34 shows an undirected graph in which 12 or 21, 23 or 32 or 34 or 43 and 14 or 41 are edges that are not oriented directionally. If an edge between any two nodes is directionally oriented, a graph is referred
