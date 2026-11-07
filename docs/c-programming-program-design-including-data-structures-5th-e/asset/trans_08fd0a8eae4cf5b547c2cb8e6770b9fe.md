
如果树 *T* 是图 *G* 的子图，且满足 *V(T) = V(G)*，即 *G* 的所有顶点都在 *T* 中，则称树 *T* 为图 *G* 的**生成树**。

假设 *G* 表示图 21–14 中的图。那么，图 21–15 中的图展示了 *G* 的三棵生成树。让我们注意以下定理。

**定理：** 图 *G* 有生成树当且仅当 *G* 是连通的。

由该定理可知，为了确定一个图的生成树，该图必须是连通的。

设 *G* 是一个带权图。*G* 的**最小生成树**是权重最小的生成树。

Prim 算法和 Kruskal 算法是两种著名算法，可用于寻找图的最小生成树。本节讨论用于寻找最小生成树的 Prim 算法。感兴趣的读者可以在离散结构书或附录 H 中列出的数据结构书中找到 Kruskal 算法。

Prim 算法通过不断添加边来迭代构建树，直到获得最小生成树。我们从一个指定的顶点开始，称其为源顶点。在每次迭代中，向树中添加一条不会形成环的新边。

设 *G* 是一个带权图，指定 *V(G) = {v₀, v₁, …, vₙ₋₁}*，其中 *n* 是顶点数。设 *v₀* 为源顶点。设 *T* 为部分构建的树。初始时，*V(T)* 包含源顶点，*E(T)* 为空。在下一次迭代中，将一个不在 *V(T)* 中的新顶点加入 *V(T)*，使得从 *T* 中的一个顶点到该新顶点存在一条边，并且对应边的权重最小。将对应边加入 *E(T)*。

Prim 算法的一般形式如下。（设 *n* 为 *G* 中的顶点数。）

```
1.  Set V(T) = {source}
2.  Set E(T) = empty
3.  for i = 1 to n
    3.1.  minWeight = infinity;
    3.2.  for j = 1 to n
              if vⱼ is in V(T)
                  for k = 1 to n
                      if vₖ is not in T and weight[vⱼ, vₖ] < minWeight
                      {
                          endVertex = vₖ;
                          edge = (vⱼ, vₖ);
                          minWeight = weight[vⱼ, vₖ];
                      }
    3.3.  V(T) = V(T) ∪ {endVertex};
    3.4.  E(T) = E(T) ∪ {edge};
```

让我们使用图 21-16 中的图 G（它与图 21-14 中的图相同）来说明 Prim 算法。

![](img/f97f778697507bb6fdd80c5991210cba_1389_0.png)

**图 21-16** 带权图 G

设 N 表示 G 中不在 T 中的顶点集合。假设源顶点为 0。执行步骤 1 和 2 后，V(T)、E(T) 和 N 如图 21-17 所示。

![](img/f97f778697507bb6fdd80c5991210cba_1389_1.png)

**图 21-17** 执行步骤 1 和 2 后的图 G、V(T)、E(T) 和 N

步骤 3.2 检查以下边：

| 边 | 边的权重 |
| --- | --- |
| (0, 1) | 6 |
| (0, 2) | 5 |
| (0, 3) | 2 |

显然，边 (0, 3) 的权重最小。因此，将顶点 3 加入 $V(T)$，并将边 (0, 3) 加入 $E(T)$。图 21-18 展示了得到的图、$V(T)$、$E(T)$ 和 $N$。（虚线表示 $T$ 中的边。）

![](img/f97f778697507bb6fdd80c5991210cba_1390_0.png)

**图 21-18** 步骤 3 第一次迭代后的图 $G$、$V(T)$、$E(T)$ 和 $N$

接下来，步骤 3.2 检查以下边：

| 边 | 边的权重 |
|---|---:|
| (0,1) | 6 |
| (0,2) | 5 |
| (3,4) | 8 |

显然，边 (0, 2) 的权重最小。因此，将顶点 2 加入 $V(T)$，并将边 (0, 2) 加入 $E(T)$。图 21-19 展示了得到的图、$V(T)$、$E(T)$ 和 $N$。

![](img/f97f778697507bb6fdd80c5991210cba_1390_1.png)

**图 21-19** 步骤 3 第二次迭代后的图 $G$、$V(T)$、$E(T)$ 和 $N$

在下一次迭代中，步骤 3.2 检查以下边：

| 边 | 边的权重 |
| --- | --- |
| (0, 1) | 6 |
| (2, 5) | 7 |
| (2, 6) | 5 |
| (3, 4) | 8 |

显然，边 (2, 6) 的权重最小。因此，将顶点 6 加入 V(T)，并将边 (2, 6) 加入 E(T)。图 21-20 展示了得到的图、V(T)、E(T) 和 N。（虚线表示 T 中的边。）

![](img/f97f778697507bb6fdd80c5991210cba_1391_0.png)

**图 21-20** 步骤 3 第三次迭代后的图 G、V(T)、E(T) 和 N

在下一次迭代中，步骤 3.2 检查以下边：

| 边 | 边的权重 |
| --- | --- |
| (0, 1) | 6 |
| (2, 5) | 7 |
| (3, 4) | 8 |
| (6, 1) | 4 |

显然，边 (6, 1) 的权重最小。因此，将顶点 1 加入 V(T)，并将边 (6, 1) 加入 E(T)。图 21-21 展示了得到的图、V(T)、E(T) 和 N。（虚线表示 T 中的边。）

![](img/f97f778697507bb6fdd80c5991210cba_1392_0.png)

**图 21-21** 步骤 3 第四次迭代后的图 G、V(T)、E(T) 和 N

在下一次迭代中，步骤 3.2 检查以下边：

| 边 | 边的权重 |
|---|---:|
| (1, 4) | 2 |
| (2, 5) | 7 |
| (3, 4) | 8 |

显然，边 (1, 4) 的权重最小。因此，将顶点 4 加入 V(T)，并将边 (1, 4) 加入 E(T)。图 21-22 展示了得到的图、V(T)、E(T) 和 N。（虚线表示 T 中的边。）

![](img/f97f778697507bb6fdd80c5991210cba_1392_1.png)

**图 21-22** 步骤 3 第五次迭代后的图 G、V(T)、E(T) 和 N

在下一次迭代中，步骤 3.2 检查以下边：

| 边 | 边的权重 |
|---|---:|
| (2, 5) | 7 |
| (4, 5) | 10 |

显然，边 (2, 5) 的权重最小。因此，将顶点 5 加入 V(T)，并将边 (2, 5) 加入 E(T)。图 21-23 展示了得到的图、V(T)、E(T) 和 N。（虚线表示 T 中的边。）

![](img/f97f778697507bb6fdd80c5991210cba_1393_0.png)

**图 21-23** 步骤 3 第六次迭代后的图 G、V(T)、E(T) 和 N

虚线展示了 G 的一棵权重为 25 的最小生成树。

在给出实现 Prim 算法的函数定义之前，让我们首先将生成树定义为一种 ADT。

设 mstV 是一个 bool 数组，使得若顶点 v_j 在 T 中，则 mstV[j] 为 true，否则为 false。设 edges 是一个数组，使得若存在连接顶点 v_j 和 v_k 的边，则 edges[j] == k。假设边 (v_i, v_j) 在最小生成树中。设 edgeWeights 是一个数组，使得 edgeWeights[j] 是边 (v_i, v_j) 的权重。

使用这些约定，以下类将生成树定义为一种 ADT。

```cpp
class msTreeType: public graphType
{
public:
    void createSpanningGraph();
        //Function to create the graph and the weight matrix.
        //Postcondition: The graph using adjacency lists and
        //              its weight matrix is created.

    void minimalSpanning(int sVertex);
        //Function to create a minimal spanning tree with
        //root as sVertex.
        //Postcondition: A minimal spanning tree is created.
        //                The weight of the edges is also
        //                saved in the array edgeWeights.
        //
    void printTreeAndWeight();
        //Function to output the edges of the minimal
        //spanning tree and the weight of the minimal
        //spanning tree.
        //Postcondition: The edges of a minimal spanning tree
        //               and their weights are printed.

    msTreeType(int size = 0);
        //Constructor
        //Postcondition: gSize = 0; maxSize = size;
        //               graph is an array of pointers to linked
        //               lists.
        //               weights is a two-dimensional array to
        //               store the weights of the edges.
        //               edges is an array to store the edges
        //               of a minimal spanning tree.
        //               edgeWeights is an array to store the
        //               weights of the edges of a minimal
        //               spanning tree.

    ~msTreeType();
        //Destructor
        //The storage occupied by the vertices and the arrays
        //weights, edges, and edgeWeights is deallocated.

protected:
    int source;
    double **weights;
    int *edges;
    double *edgeWeights;
};
```

我们将类 `msTreeType` 的 UML 类图和继承层次结构留作练习。函数 `createSpanningGraph` 的定义也留作读者的练习。该函数创建图以及与图关联的权重矩阵。

以下 C++ 函数 `minimalSpanning` 实现了如前所述的 Prim 算法。

```cpp
void msTreeType::minimalSpanning(int sVertex)
{
    int startVertex, endVertex;
    double minWeight;

    source = sVertex;

    bool *mstV;
    mstV = new bool[gSize];
```
